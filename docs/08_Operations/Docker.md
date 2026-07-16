# Docker 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Dockerは、VTaBridge OSの各サービスをコンテナ化し、開発・テスト・本番環境で一貫した実行環境を提供する。

Azure Container Appsを実行基盤とし、軽量・高速・セキュアなコンテナイメージを構築する。

---

# 2. 目的

Docker導入目的

- 実行環境統一
- デプロイ容易化
- スケーラビリティ向上
- 開発効率向上
- セキュリティ強化
- Infrastructure as Code対応

---

# 3. コンテナ構成

対象コンテナ

- Frontend（Next.js）
- Backend API（FastAPI）
- AI API
- Python Worker
- Playwright Worker

各サービスを独立したコンテナとして管理する。

---

# 4. 全体構成

```
Azure Container Apps

├── Frontend
├── Backend API
├── AI API
├── Python Worker
└── Playwright Worker

↓

Azure Database for PostgreSQL

↓

Azure Blob Storage
```

---

# 5. Dockerfile設計

採用方針

- マルチステージビルド
- 最小イメージ
- 非rootユーザー
- Build Cache活用

本番イメージには不要な開発ツールを含めない。

---

# 6. ベースイメージ

| サービス | ベースイメージ |
|-----------|----------------|
| Frontend | node:22-alpine |
| Backend API | python:3.13-slim |
| AI API | python:3.13-slim |
| Python Worker | python:3.13-slim |
| Playwright Worker | mcr.microsoft.com/playwright/python |

公式イメージを利用する。

---

# 7. マルチステージビルド

構成

```
Builder

↓

Install

↓

Build

↓

Production Image
```

最終イメージには実行に必要なファイルのみ含める。

---

# 8. ネットワーク

通信

- Frontend → Backend API
- Backend API → AI API
- Backend API → PostgreSQL
- Backend API → Azure Blob Storage
- Worker → Queue

外部公開はFrontend・Backend APIのみとする。

---

# 9. ボリューム

利用対象

- 一時ファイル
- Playwrightダウンロード
- OCR処理
- ログ

永続データはAzure Blob Storageへ保存する。

---

# 10. 環境変数

管理対象

- Database URL
- Azure OpenAI Endpoint
- Azure Storage
- JWT Secret
- API Key

機密情報はAzure Key Vaultから取得する。

---

# 11. コンテナセキュリティ

実装

- 非rootユーザー
- Read Only Root Filesystem（可能な範囲）
- 最小権限
- 不要パッケージ削除
- イメージ署名（将来対応）

---

# 12. ヘルスチェック

確認項目

- HTTP Health Check
- AI API疎通
- Database接続
- Queue接続

正常時のみトラフィックを受け付ける。

---

# 13. ログ

出力先

- 標準出力（stdout）
- 標準エラー（stderr）

Azure Monitorで収集する。

---

# 14. イメージ管理

保存先

Azure Container Registry

タグ

- latest
- develop
- staging
- production
- Git SHA

Semantic Versioningと組み合わせて管理する。

---

# 15. Docker Compose

利用環境

- Local Development
- Integration Test

起動対象

- Frontend
- Backend API
- PostgreSQL
- Redis（必要時）
- Azurite（ローカルストレージエミュレーター）

開発環境でのみ利用する。

---

# 16. パフォーマンス

実施

- Build Cache
- Layer最適化
- Alpine利用
- 不要ファイル除外（.dockerignore）

ビルド時間とイメージサイズを最適化する。

---

# 17. CI/CD連携

GitHub Actionsで実施

- Docker Build
- Image Scan
- ACR Push
- Azure Container Apps Deploy

パイプラインへ統合する。

---

# 18. 監視

監視項目

- CPU
- Memory
- Restart Count
- Health Check
- Response Time

Azure Monitorで監視する。

---

# 19. 運用

実施内容

- ベースイメージ更新
- セキュリティパッチ適用
- イメージクリーンアップ
- イメージ脆弱性スキャン
- バージョン管理

定期的に更新を実施する。

---

# 20. 将来拡張

- Distroless Image採用
- Docker Buildx
- Multi-Architecture Build
- SBOM生成
- Cosign署名
- OCI Artifact管理
- Rootless Container
- Kubernetes対応
- AIによるイメージ最適化
- コンテナライフサイクル自動管理
