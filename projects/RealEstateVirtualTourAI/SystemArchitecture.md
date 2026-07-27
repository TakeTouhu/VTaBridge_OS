# System Architecture

Version: 1.0

Status: Draft

---

## 1. アーキテクチャ方針

MVPはモジュラーモノリスで開始し、動画生成ワーカーのみ独立スケール可能な非同期サービスとする。

- Web/API: TypeScript
- Frontend: Next.js
- Database: PostgreSQL
- ORM: Prisma
- Object Storage: S3互換ストレージまたはAzure Blob Storage
- Queue: Redis Queue / Azure Service Bus / SQSのいずれか
- Worker: コンテナ実行
- Video Processing: FFmpeg
- Authentication: Entra ID / Google / Email認証
- Billing: Stripeを第一候補
- Observability: OpenTelemetry

---

## 2. 論理構成

```text
Browser
  |
  v
Web Application
  |
  v
API / BFF
  |--------------------|
  v                    v
PostgreSQL        Object Storage
  |
  v
Job Queue
  |
  v
Generation Orchestrator
  |-----------------------------|
  v              v              v
Vision Model   Video Model    FFmpeg Composer
  |              |              |
  +--------------+--------------+
                 |
                 v
          Generated Video
                 |
                 v
        Review / Download / Share
```

---

## 3. 主要モジュール

### Identity

- 組織
- ユーザー
- ロール
- 招待
- セッション

### Property

- 物件
- 住所
- 物件種別
- 掲載情報
- ブランド

### Asset

- 原本画像
- サムネイル
- メタデータ
- 品質判定
- 保存・削除

### AI Analysis

- 部屋分類
- 画像品質評価
- 重複検知
- 写真順序提案
- プロンプト補強

### Video Project

- 生成設定
- ストーリーボード
- シーン
- バージョン
- 承認状態

### Generation

- ジョブ
- プロバイダー
- 再試行
- コスト
- 進捗
- 失敗理由

### Billing

- プラン
- サブスクリプション
- クレジット
- 利用量
- 請求

### Governance

- 監査ログ
- 同意
- モデレーション
- 保持期間
- 削除要求

---

## 4. マルチテナント設計

全業務テーブルに`organization_id`を持たせる。

- APIで必ずテナントスコープを適用
- DBアクセス層でテナント条件を強制
- オブジェクトストレージを組織単位のプレフィックスで分離
- 署名付きURLは短時間のみ有効
- 管理者の横断アクセスは監査対象

将来的には大口顧客向けに専用DB・専用ストレージを選択可能にする。

---

## 5. 非同期生成

動画生成は同期APIで待たない。

```text
POST generation request
↓
Validation
↓
Credit reservation
↓
Job enqueue
↓
Worker processing
↓
Progress event
↓
Output validation
↓
Credit settlement
↓
Notification
```

各ジョブにidempotency keyを持たせ、重複課金と重複生成を防止する。

---

## 6. プロバイダー抽象化

特定の動画生成AIに依存しない。

```text
VideoProvider
├── createGeneration()
├── getStatus()
├── cancelGeneration()
├── estimateCost()
└── normalizeError()
```

画像解析、動画生成、音声、BGMも同様にアダプター化する。

---

## 7. 環境

- local
- development
- staging
- production

本番データを開発環境へコピーしない。各環境で認証情報、ストレージ、DB、AI APIキーを分離する。
