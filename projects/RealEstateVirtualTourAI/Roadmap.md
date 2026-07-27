# Roadmap

Version: 1.0

Status: Draft

---

## Phase 0: Validation

- 顧客インタビュー
- 写真品質と動画品質のPoC
- AIプロバイダー比較
- 1動画当たり原価測定
- 不動産広告上の表示方針確認
- MVP対象媒体の決定

Completion Gate:

- 10件以上の物件で試作
- 生成品質と許容原価を確認
- β顧客候補を確保

---

## Phase 1: Foundation

- リポジトリ・CI
- Next.js基盤
- PostgreSQL / Prisma
- 認証
- Organization / User / Role
- オブジェクトストレージ
- 監査ログ基盤

---

## Phase 2: Property and Upload

- 物件CRUD
- 画像アップロード
- 画像検証
- サムネイル
- EXIF除去
- 品質チェック
- 写真並べ替え

---

## Phase 3: AI Analysis

- 部屋種別分類
- 信頼度表示
- 重複検知
- 写真品質評価
- ストーリーボード提案
- 利用者による修正

---

## Phase 4: Video Generation MVP

- プロンプト編集
- 15 / 30 / 60秒
- 16:9 / 9:16 / 1:1
- 非同期ジョブ
- シーン動画生成
- FFmpeg結合
- 進捗・失敗表示
- MP4出力

---

## Phase 5: Review and Commercialization

- プレビュー
- シーン再生成
- 承認・差し戻し
- AI生成表示
- ロゴ・字幕・BGM
- ダウンロード
- Stripe課金
- クレジット台帳
- プラン制御

---

## Phase 6: SaaS Hardening

- RBAC強化
- MFA / SSO
- テナント分離テスト
- 監査ログ出力
- バックアップ・復旧
- Observability
- レート制限
- セキュリティ診断
- 利用規約・削除フロー

---

## Phase 7: Beta

- 限定顧客提供
- 品質評価
- 操作ログ分析
- 原価・粗利検証
- サポート運用
- 不具合修正

---

## Phase 8: General Availability

- 正式料金
- SLA
- ステータスページ
- サポート窓口
- 法務文書
- 本番運用Runbook
- 営業資料・デモ

---

## Future

- 間取り図との連携
- 360度写真
- 物件ポータルAPI連携
- 多言語字幕・ナレーション
- ブランド別テンプレート
- 自動ハイライト動画
- バーチャルステージング
- 空室家具配置

バーチャルステージングは実物と生成内容を明確に区別し、誤認防止表示を必須とする。
