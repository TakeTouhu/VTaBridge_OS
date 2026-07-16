# RPA Security 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

RPA Securityは、VTaBridge OSのRPA基盤全体におけるセキュリティ設計を定義する。

Power Automate、Python、Playwright、Azure Functions、Scheduler、Workflowなど、すべての自動化コンポーネントを対象とし、認証・認可・シークレット管理・監査・ゼロトラストを実現する。

---

# 2. 目的

RPA Security導入目的

- 不正アクセス防止
- Bot権限管理
- シークレット保護
- 監査ログ保存
- API保護
- 外部連携保護
- コンプライアンス対応
- ゼロトラスト実現

---

# 3. アーキテクチャ

```
User

↓

Azure Entra ID

↓

RBAC

↓

Automation API

↓

────────────────────

Power Automate

Python

Playwright

Azure Functions

────────────────────

↓

Key Vault

↓

Business API

↓

Database

↓

Audit Log
```

---

# 4. 認証

認証方式

- Azure Entra ID
- OAuth2
- JWT
- Managed Identity
- Multi-Factor Authentication（MFA）

Bot専用アカウントを利用する。

---

# 5. 認可

RBACを採用する。

ロール例

- SuperAdmin
- Admin
- Operator
- Developer
- Viewer
- Bot

最小権限の原則（Principle of Least Privilege）を適用する。

---

# 6. Botアカウント

Botごとに専用アカウントを作成する。

管理項目

- BotID
- BotName
- Permission
- Expiration
- Status

Bot間でアカウントを共有しない。

---

# 7. シークレット管理

保存対象

- API Key
- OAuth Token
- Client Secret
- Connection String
- Database Password

Azure Key Vaultで一元管理する。

---

# 8. Power Automateセキュリティ

実装

- Managed Identity
- Connection Reference
- Environment分離
- DLPポリシー
- RBAC

接続情報をFlowへ直接保存しない。

---

# 9. Pythonセキュリティ

実装

- 環境変数管理
- Key Vault利用
- 型チェック
- Dependency Scan
- Secret Masking

ログへシークレットを出力しない。

---

# 10. Playwrightセキュリティ

実装

- Cookie暗号化
- Session管理
- Key Vault
- TLS通信
- Browser Sandbox

ログイン情報をコードへ記述しない。

---

# 11. APIセキュリティ

実装

- HTTPS Only
- JWT認証
- RBAC
- Rate Limit
- Input Validation
- API監査ログ

Business API経由のみアクセスを許可する。

---

# 12. データ保護

保存時

- AES-256

通信時

- TLS 1.3

ファイル

- Azure Blob Storage暗号化

個人情報はマスキングして保存する。

---

# 13. 監査ログ

保存項目

- UserID
- BotID
- Automation名
- 実行結果
- 実行時間
- IP Address
- Device
- Timestamp

監査ログは改ざん防止を考慮して保存する。

---

# 14. ネットワーク

実装

- Private Endpoint
- Azure Firewall
- Network Security Group
- IP制限
- VNet Integration

外部アクセスを最小限に制限する。

---

# 15. Prisma実装方針

Model

```
BotAccount

BotPermission

AutomationAuditLog

SecretReference

SecurityPolicy
```

Relation

```
User

AutomationJob

Organization
```

---

# 16. コンプライアンス

対応予定

- ISO 27001
- SOC 2
- GDPR
- 日本個人情報保護法
- Microsoft Security Baseline

---

# 17. インシデント対応

異常検知時

- Bot停止
- Token失効
- セッション無効化
- 管理者通知
- 監査ログ保存

重大インシデントはSOCへ通知する。

---

# 18. セキュリティ監視

Azure Monitor

Microsoft Defender for Cloud

Log Analytics

監視項目

- 不正アクセス
- Bot異常実行
- API異常
- シークレット利用状況
- 権限変更

---

# 19. 性能目標

認証

```
500ms以内
```

認可

```
300ms以内
```

Key Vault取得

```
1秒以内
```

監査ログ保存

```
500ms以内
```

---

# 20. 将来拡張

- Zero Trust Architecture
- Just-In-Time Access
- Privileged Identity Management（PIM）
- Confidential Computing
- Hardware Security Module（HSM）
- AI異常検知
- シークレット自動ローテーション
- Botリスク分析
- 自動コンプライアンスチェック
- セキュリティダッシュボード
