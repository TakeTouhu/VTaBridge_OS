# GitHub Actions 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

GitHub Actionsは、VTaBridge OSのCI/CDパイプラインを構築するための自動化基盤である。

コードの品質チェック、ビルド、テスト、Dockerイメージ作成、Terraform検証、Azureへのデプロイまでを自動化する。

---

# 2. 目的

GitHub Actions導入目的

- CI自動化
- CD自動化
- 品質向上
- デプロイ自動化
- セキュリティ強化
- リリース効率化
- 運用負荷軽減

---

# 3. ワークフロー構成

```
Push / Pull Request

↓

Checkout

↓

Install

↓

Lint

↓

Test

↓

Build

↓

Security Scan

↓

Docker Build

↓

Terraform Validate

↓

Deploy

↓

Smoke Test

↓

Notification
```

---

# 4. 実行タイミング

実行条件

- Push
- Pull Request
- Release
- Tag作成
- 手動実行（workflow_dispatch）
- Schedule

---

# 5. CIパイプライン

実施内容

- Checkout
- Node.jsセットアップ
- Pythonセットアップ
- 依存関係インストール
- キャッシュ復元
- Lint
- Unit Test
- Build

---

# 6. Lint

対象

- TypeScript
- Python
- Markdown
- YAML

利用ツール

- ESLint
- Ruff
- markdownlint
- yamllint

---

# 7. テスト

実施

- Unit Test
- Integration Test
- API Test
- UI Test
- E2E Test

利用

- Vitest
- Pytest
- Playwright

---

# 8. Build

対象

- Next.js
- FastAPI
- Python Worker

成果物を生成し、ビルドエラーがないことを確認する。

---

# 9. Docker

実施

- Docker Build
- Image Scan
- Tag付与
- Azure Container RegistryへPush

イメージタグはGit SHAを利用する。

---

# 10. Terraform

実施

- fmt
- validate
- plan

mainブランチではapplyを実行する。

---

# 11. セキュリティ

実施

- CodeQL
- Dependabot
- Secret Scan
- Trivy
- npm audit
- pip-audit

脆弱性が検出された場合はパイプラインを停止する。

---

# 12. デプロイ

対象

- Frontend
- Backend API
- AI API
- Python Worker
- Playwright Worker

Azure Container Appsへデプロイする。

---

# 13. Smoke Test

確認項目

- API疎通
- Health Check
- ログイン確認
- Dashboard表示
- AI API疎通

異常時はロールバックする。

---

# 14. 通知

通知先

- Microsoft Teams
- Outlook
- Slack

通知内容

- 成功
- 失敗
- デプロイ開始
- デプロイ完了

---

# 15. Secrets

利用

- GitHub Secrets
- Azure Key Vault

対象

- Azure認証情報
- API Key
- JWT Secret
- Container Registry情報

---

# 16. キャッシュ

利用対象

- npm
- pnpm
- pip
- Docker Layer

ビルド時間短縮を目的とする。

---

# 17. ログ

保存項目

- Workflow名
- 実行者
- Commit SHA
- 実行時間
- Status
- Job結果

GitHub Actionsの実行履歴として保存する。

---

# 18. ブランチ別動作

| Branch | 実行内容 |
|---------|----------|
| feature/* | Build・Test |
| develop | Build・Test・Docker |
| release/* | Build・Deploy(Staging) |
| main | Full Pipeline・Production Deploy |

---

# 19. 性能目標

CI

```
10分以内
```

Docker Build

```
5分以内
```

Deploy

```
5分以内
```

Smoke Test

```
2分以内
```

---

# 20. 将来拡張

- GitHub Merge Queue
- Self-hosted Runner
- AIテスト生成
- AIコードレビュー
- AI障害分析
- Preview Environment
- 並列ジョブ最適化
- キャッシュ最適化
- GitHub Copilot Autofix
- Policy as Code
