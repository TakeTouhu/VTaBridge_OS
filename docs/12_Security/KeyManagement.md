# Key Management 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Key Managementは、VTaBridge OSで利用する暗号鍵・署名鍵・証明書・シークレットのライフサイクル全体を管理するための設計を定義する。

Azure Key Vaultを標準の鍵管理基盤とし、高いセキュリティ要件が求められる場合はAzure Managed HSMを利用する。

---

# 2. 目的

Key Management導入目的

- 暗号鍵保護
- 鍵ライフサイクル管理
- 不正利用防止
- コンプライアンス対応
- 監査性向上
- 暗号化基盤の標準化

---

# 3. 基本方針

採用方針

- Azure Key Vault First
- Least Privilege
- Key Rotation
- Key Separation
- Zero Trust
- Security by Design

鍵はアプリケーションから分離して管理する。

---

# 4. 管理対象

対象

- AES Encryption Key
- RSA Key
- ECDSA Key
- JWT Signing Key
- TLS Certificate
- Customer Managed Key（CMK）
- BYOK（必要時）

---

# 5. Azure Key Vault

管理内容

- Key
- Secret
- Certificate

すべての暗号鍵をAzure Key Vaultで管理する。

---

# 6. Azure Managed HSM

利用対象

- 高機密データ
- 電子署名
- コード署名
- 規制対応システム

必要に応じてManaged HSMを利用する。

---

# 7. 鍵ライフサイクル

```
生成

↓

登録

↓

利用

↓

更新

↓

失効

↓

削除
```

各ライフサイクルを監査対象とする。

---

# 8. 鍵生成

要件

- Azure Key Vault Generate
- HSM利用（必要時）
- 強力なアルゴリズム
- ランダム生成

鍵をアプリケーションで生成しない。

---

# 9. 鍵利用

利用対象

- Database
- Storage
- JWT
- API
- AI Data
- Backup

Managed Identity経由で利用する。

---

# 10. 鍵ローテーション

対象

- Encryption Key
- Signing Key
- Certificate
- API Key

定期的なローテーションを自動化する。

---

# 11. Customer Managed Key

対象

- Azure Storage
- PostgreSQL
- Azure AI Search
- Backup

高いセキュリティ要件がある場合に利用する。

---

# 12. Bring Your Own Key

利用条件

- 顧客要求
- 法令対応
- 契約条件

BYOK利用時は管理責任を明確化する。

---

# 13. アクセス制御

実装

- Azure RBAC
- Managed Identity
- PIM（導入時）
- Least Privilege

鍵へのアクセス権を最小限に制限する。

---

# 14. バックアップ

対象

- Key Vault
- Certificate
- Metadata

復旧手順をRunbookへ定義する。

---

# 15. 監査

取得項目

- Key Access
- Key Create
- Key Update
- Key Delete
- Certificate Access
- Rotation

Azure Monitorへ送信する。

---

# 16. 障害対応

対象

- 鍵失効
- Rotation失敗
- Key Vault障害
- 証明書期限切れ

Runbookに従って迅速に復旧する。

---

# 17. KPI

管理項目

- Rotation実施率
- Key Vault利用率
- 証明書期限切れ件数
- 鍵アクセス件数
- 鍵失効件数

継続的に分析する。

---

# 18. ベストプラクティス

- 鍵をソースコードへ保存しない
- Managed Identityを優先する
- 定期的にローテーションする
- HSM利用を検討する
- 鍵利用を監査する

---

# 19. 運用

実施内容

- 鍵棚卸し
- Rotation確認
- アクセス権レビュー
- 証明書更新
- 監査ログ分析

継続的に改善する。

---

# 20. 将来拡張

- Azure Managed HSM全面移行
- BYOK高度化
- External Key Management
- Double Key Encryption
- AI鍵利用分析
- Quantum Safe Cryptography
- Key Management Dashboard
- Continuous Key Validation
- AI鍵異常検知
- Autonomous Key Management
