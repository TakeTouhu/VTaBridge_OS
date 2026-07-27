# WaveSpeedAI Integration Design

Version: 1.0

Status: Approved Provider Design

---

## 1. 目的

Real Estate Virtual Tour AIの動画生成プロバイダーとして、WaveSpeedAIのREST APIを利用する。

WaveSpeedAIは画像から動画を生成する複数モデルを統一APIで提供する。サービス本体はWaveSpeedAI固有仕様をドメイン層へ漏らさず、Provider Adapter経由で利用する。

---

## 2. 採用方針

- 初期動画生成プロバイダーはWaveSpeedAIとする
- APIキーはサーバー側のみで保持する
- ブラウザからWaveSpeedAI APIを直接呼び出さない
- モデルID・料金・入力制約は設定テーブルで管理する
- WaveSpeedAIのPrediction IDは内部情報として保存し、顧客向けIDとして公開しない
- モデルの商用利用条件を導入前およびモデル変更時に確認する
- モデル障害に備え、Provider Interfaceは維持する

---

## 3. 認証

環境変数またはSecret Managerで以下を管理する。

```text
WAVESPEED_API_KEY
WAVESPEED_API_BASE_URL=https://api.wavespeed.ai/api/v3
WAVESPEED_DEFAULT_MODEL=wavespeed-ai/open-video/image-to-video
WAVESPEED_WEBHOOK_SECRET
```

APIリクエストでは以下を付与する。

```http
Authorization: Bearer ${WAVESPEED_API_KEY}
Content-Type: application/json
```

APIキー、Authorizationヘッダー、署名付き画像URLをログへ記録しない。

---

## 4. 基本APIフロー

```text
Normalized room image
↓
Create short-lived signed image URL
↓
POST WaveSpeedAI model endpoint
↓
Receive prediction ID
↓
Persist provider job record
↓
Webhook reception or status polling
↓
GET /predictions/{predictionId}/result
↓
Download provider output to managed object storage
↓
Validate video
↓
Delete or expire temporary provider-facing URLs
↓
Compose final walkthrough video with FFmpeg
```

代表的な送信先:

```text
POST /api/v3/{model-id}
GET  /api/v3/predictions/{predictionId}/result
```

モデルIDはコードへ固定せず、管理設定から取得する。

---

## 5. Image-to-Video入力

内部の標準入力モデル:

```ts
export type ImageToVideoRequest = {
  sourceImageUrl: string;
  prompt: string;
  negativePrompt?: string;
  durationSeconds: number;
  resolution: "480p" | "720p" | "1080p";
  aspectRatio: "16:9" | "9:16" | "1:1";
  seed?: number;
  cameraMotion:
    | "slow-forward"
    | "slow-pan-left"
    | "slow-pan-right"
    | "gentle-orbit"
    | "static-depth";
};
```

WaveSpeedAI Adapterが、選択モデル固有のパラメータへ変換する。

モデルにより利用可能な`duration`、`resolution`、`preset`、`movement_amplitude`などが異なるため、UIへ表示する選択肢は選択モデルのCapabilityから動的に生成する。

---

## 6. 不動産動画用プロンプト

各シーンのプロンプトは以下を結合して生成する。

```text
Room classification
+ property facts
+ camera instruction
+ user customization
+ preservation constraints
+ negative constraints
```

標準制約:

```text
Create a realistic, slow real-estate walkthrough-style camera movement based strictly on the supplied room photograph. Preserve the existing architecture, room dimensions as perceived in the source image, doors, windows, fixtures, materials, furniture, lighting direction, and exterior view. Do not add, remove, enlarge, replace, redesign, or relocate any structural element or furnishing. Do not introduce people, animals, text, logos, or imaginary spaces. Avoid fisheye distortion and exaggerated wide-angle effects. Use stable cinematic motion suitable for a property listing.
```

日本語のユーザープロンプトは、意味を維持したままモデル向けプロンプトへ正規化する。ユーザー入力で標準制約を解除できないようにする。

---

## 7. シーン生成

1枚の写真から1つの短いクリップを生成する。

```text
Photo A → 3〜10秒 clip
Photo B → 3〜10秒 clip
Photo C → 3〜10秒 clip
          ↓
     FFmpeg composition
          ↓
15〜90秒 final video
```

WaveSpeedAIモデルが対応する最大尺を超える長尺動画は、複数クリップ生成と後処理で構成する。

同じ写真を再利用する場合は、構造を創作する移動ではなく、パン、軽い前進、静的な奥行き表現など安全なカメラ動作だけを使用する。

---

## 8. 非同期状態管理

内部状態:

```text
QUEUED
SUBMITTED
PROCESSING
DOWNLOADING
VALIDATING
COMPOSING
REVIEW_REQUIRED
COMPLETED
FAILED_RETRYABLE
FAILED_FINAL
CANCELLED
```

保存項目:

- provider
- provider_model_id
- provider_prediction_id
- submitted_at
- completed_at
- request_payload_hash
- provider_status
- provider_error_code
- provider_error_message_sanitized
- estimated_cost
- actual_cost
- retry_count
- output_source_expiry

---

## 9. PollingとWebhook

Webhookを優先し、Webhook未着または検証失敗時の補完としてPollingを行う。

Polling方針:

- 初回は約2秒後
- 以降は指数バックオフ
- GETのみ安全に再試行
- 最大待機時間を設定
- Terminal Status到達後は停止
- 同じPredictionを複数Workerが処理しないようロックする

Webhook:

- 署名検証
- タイムスタンプ検証
- イベント重複排除
- Raw body hash保存
- 再処理可能なInbox Pattern

WaveSpeedAIの実際のWebhook仕様は、実装時点の公式ドキュメントを確認してAdapter内に閉じ込める。

---

## 10. ファイル受け渡し

モデルが公開アクセス可能な画像URLを要求する場合、Object Storageから短時間の署名付きURLを発行する。

- 有効期限は必要最小限
- 推測困難なオブジェクトキー
- 原本ではなく処理用コピー
- URLをログへ出さない
- Providerの取得完了後に早期失効できる設計
- 出力URLは一時URLとして扱い、完了後すぐ自社ストレージへコピーする

WaveSpeedAIの一時出力URLを顧客へ直接返さない。

---

## 11. モデル選択

初期候補:

```text
wavespeed-ai/open-video/image-to-video
```

ただし本番採用モデルは以下の検証を通過したものに限定する。

- 商用利用条件
- 室内構造保持率
- 家具・設備の増殖率
- ちらつき
- カメラ移動の自然さ
- 生成時間
- 失敗率
- 解像度
- 対応尺
- 1シーンあたり原価
- 同時実行制限

モデル名・価格・能力は変化し得るため、DBまたはRemote Configで管理する。

---

## 12. コスト管理

生成開始前にWaveSpeedAIのモデル・解像度・尺に基づく推定原価を算出する。

```text
estimated provider cost
+ storage cost
+ FFmpeg processing cost
+ retry reserve
+ platform margin
= customer credit price
```

- Creditはジョブ開始前に予約
- 実課金は一度だけ確定
- Provider側成功後に内部処理が失敗した場合の再処理は、同じProvider出力を再利用する
- 同一入力と設定の重複生成をRequest Hashで防止
- Provider課金記録と顧客課金記録を分離する

---

## 13. エラー処理

分類:

- Authentication Error: 再試行しない、運用通知
- Validation Error: 再試行しない、ユーザーへ修正案
- Rate Limit: Retry-AfterまたはBackoff
- Provider Capacity: Backoff後に再試行
- Timeout: Prediction状態を再照会
- Content Rejection: 理由を安全に表示、入力変更を案内
- Output Download Failure: 出力URL有効期間内に再試行
- Corrupt Output: シーン単位で再生成
- Unknown Error: 回数制限付き再試行後にDead Letter

Providerの生レスポンスをそのまま顧客へ表示しない。

---

## 14. 品質ゲート

WaveSpeedAI出力後に以下を検証する。

- 動画ファイルのデコード可否
- 尺・解像度・コーデック
- 黒フレーム
- 強いちらつき
- 画像との類似性
- 窓、扉、設備、家具の重大な変形
- 不自然な人物・文字・ロゴの生成
- カメラ速度
- 安全ポリシー

品質基準未達の場合は自動公開せず、シーン再生成または人間確認へ送る。

---

## 15. Provider Interface

```ts
export interface VideoGenerationProvider {
  getCapabilities(modelId: string): Promise<VideoModelCapabilities>;
  estimateCost(input: ImageToVideoRequest): Promise<Money>;
  submit(input: ImageToVideoRequest): Promise<ProviderSubmission>;
  getStatus(providerJobId: string): Promise<ProviderJobStatus>;
  getResult(providerJobId: string): Promise<ProviderResult>;
  cancel(providerJobId: string): Promise<void>;
  normalizeError(error: unknown): ProviderError;
}
```

実装クラス:

```text
WaveSpeedVideoProvider
```

Domain、API Route、UIからWaveSpeedAI SDKまたはHTTP APIを直接呼び出してはならない。

---

## 16. テスト

- Adapter request mapping unit test
- Authorization header omission test
- API key redaction test
- Prediction state mapping test
- Retry and backoff test
- Duplicate webhook test
- Timeout recovery test
- Signed URL expiry test
- Output download and storage test
- Cost settlement idempotency test
- Provider sandboxまたは最小額の実API contract test

実API contract testは通常CIから分離し、明示的な環境でのみ実行する。

---

## 17. 運用メトリクス

- submission success rate
- completion success rate
- provider latency p50 / p95 / p99
- queue wait time
- generation time per model
- failure rate by model and error type
- retry rate
- cost per generated second
- cost per accepted output
- quality rejection rate
- provider balance / quota alerts

---

## 18. 変更管理

WaveSpeedAIのモデル、パラメータ、価格、同時実行制限、利用規約は変更される可能性がある。

本番変更前に以下を行う。

1. 公式ドキュメント確認
2. 商用利用条件確認
3. StagingでGolden Dataset評価
4. 原価試算
5. Feature Flagによる段階導入
6. Rollback設定
7. ADR更新
