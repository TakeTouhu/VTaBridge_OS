# Secrets Management 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Secrets Managementは、VTaBridge OSで利用するパスワード・APIキー・接続文字列・証明書・暗号鍵などの機密情報（シークレット）を安全に管理するための設計を定義する。

Azure Key Vault・Managed Identity・GitHub OIDCを中心としたシークレットレスアーキテクチャを採用し、シークレット漏えいリスクを最小限に抑える。

---

# 2. 目的

Secrets Management導入目的

- シークレット漏えい防止
- シークレットレス運用
- 最小権限の実現
- 自動ローテーション
- 監査性向上
- DevSecOps推進

---

# 3. 基本方針

採用方針

- Secretless First
- Azure Key Vault利用
- Managed Identity優先
- GitHub OIDC利用
- Least Privilege
- Zero Trust

コード・設定ファイルへシークレットを保存しない。

---

# 4. 管理対象

対象

- API Key
- Database Password
- Storage Key
- OAuth Secret
- JWT Secret
- TLS Certificate
- Encryption Key
- Connection String

---

# 5. Azure Key Vault

管理対象

- Secret
- Certificate
- Key

Azure Key Vaultを唯一のシークレット保管場所とする。

---

# 6. Managed Identity

対象

- Backend API
- Azure Container Apps
- AI API
- Workflow
- Azure Functions（将来対応）

Azureリソース間通信ではManaged Identityを優先する。

---

# 7. GitHub OIDC

対象

- GitHub Actions
- Azure Login
- Terraform
- Container Registry

長期アクセストークンを使用せず、OIDCフェデレーション認証を利用する。

---

# 8. シークレット取得

フロー

```
Application

↓

Managed Identity

↓

Azure Key Vault

↓

Secret取得

↓

Application利用
```

実行時にのみシークレットを取得する。

---

# 9. シークレットローテーション

対象

- API Key
- Database Password
- Certificate
- Storage Key
- Encryption Key

定期的に自動ローテーションを実施する。

---

# 10. 証明書管理

対象

- HTTPS
- API
- Internal Service

Azure Key Vault Certificateで一元管理する。

---

# 11. アクセス制御

実装

- Azure RBAC
- Managed Identity
- Least Privilege
- Key Vault Access Policy（必要時）

必要最小限のアクセス権のみ付与する。

---

# 12. 開発環境

利用

- Azure Developer CLI
- Azure CLI
- .env（ローカル開発のみ）
- User Secrets（必要時）

本番シークレットをローカルへ保存しない。

---

# 13. 禁止事項

禁止

- Gitへコミット
- ソースコードへ埋め込み
- ハードコード
- Teams・メールで共有
- Wikiへ平文保存

シークレットの取り扱いルールを徹底する。

---

# 14. 監査

取得項目

- Secret取得
- Secret更新
- Secret削除
- Certificate更新
- Key利用

監査ログをAzure Monitorへ送信する。

---

# 15. 障害対応

対応

- Secret失効
- Rotation失敗
- Key Vault障害
- アクセス拒否

Runbookに従って復旧する。

---

# 16. DevSecOps

CI/CD

- GitHub Secret Scan
- GitHub Push Protection
- CodeQL
- Trivy
- IaC Scan

シークレット漏えいをPipelineで検知する。

---

# 17. KPI

管理項目

- ハードコード件数
- Secret Rotation成功率
- Key Vault利用率
- Managed Identity利用率
- Secret漏えい件数

継続的に評価する。

---

# 18. ベストプラクティス

- Key Vaultを唯一の保管場所とする
- Managed Identityを優先する
- GitHub OIDCを利用する
- Secretは短寿命とする
- 定期的にローテーションを実施する

---

# 19. 運用

実施内容

- Secret棚卸し
- Rotation確認
- Key Vault監査
- 権限見直し
- シークレット利用状況分析

継続的に改善を実施する。

---

# 20. 将来拡張

- Azure Managed HSM
- Dynamic Secret
- HashiCorp Vault連携
- External Secret Operator
- Secret自動分類
- AI漏えい検知
- AI Rotation最適化
- Secret Dashboard
- Continuous Secret Validation
- Autonomous Secrets Management
