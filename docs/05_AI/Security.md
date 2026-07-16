# AI Security 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

AI Securityは、VTaBridge OSにおけるAI利用時のセキュリティ設計を定義する。

AIチャット、RAG、AI Agent、Function Calling、MCPなど、すべてのAI機能は本設計に従う。

企業向けSaaSとして、情報漏えい防止・権限制御・監査性を重視した構成とする。

---

# 2. 目的

AI Security導入目的

- 情報漏えい防止
- Prompt Injection対策
- AI誤利用防止
- 権限制御
- 個人情報保護
- 監査ログ保存
- AIガバナンス
- コンプライアンス対応

---

# 3. アーキテクチャ

```
User

↓

Authentication

↓

Authorization

↓

Input Validation

↓

Content Safety

↓

Prompt Guard

↓

Azure OpenAI

↓

Output Validation

↓

Audit Log

↓

Response
```

---

# 4. 認証

認証方式

- Azure Entra ID
- OAuth2
- JWT
- Multi-Factor Authentication（MFA）

シングルサインオン（SSO）を標準とする。

---

# 5. 認可

RBACを採用する。

ロール例

- SuperAdmin
- Admin
- Sales
- Recruiter
- Engineer
- Viewer

ロールごとにAI機能の利用範囲を制御する。

---

# 6. Prompt Injection対策

実施内容

- 入力内容の検査
- システムプロンプト保護
- Function実行制限
- 不正命令の除外
- URL・コード解析
- 危険キーワード検出

異常検知時はAI処理を中止する。

---

# 7. PII（個人情報）保護

対象

- 氏名
- メールアドレス
- 電話番号
- 住所
- 契約番号
- 銀行口座
- マイナンバー

AI送信前にマスキングを実施する。

---

# 8. Content Safety

Azure AI Content Safetyを利用する。

検査対象

- 暴力
- ヘイト
- 自傷
- 性的表現
- 個人情報
- 不適切な入力

危険度に応じてブロックまたは警告を行う。

---

# 9. Function Calling保護

実施内容

- Function実行権限確認
- 入力パラメータ検証
- 実行回数制限
- API監査
- SQL Injection対策

直接DBアクセスは禁止する。

---

# 10. RAG保護

アクセス制御

- Document ACL
- Department ACL
- Project ACL
- Organization ACL

権限のない文書は検索対象外とする。

---

# 11. MCP保護

実施内容

- Tool権限確認
- OAuth2認証
- Secret管理
- Tool監査ログ
- Tool利用制限

外部サービスへのアクセスはMCP経由のみ許可する。

---

# 12. 出力検証

AI回答に対して以下を実施する。

- 個人情報漏えい確認
- 禁止語句チェック
- ハルシネーション検知
- 不適切表現検出
- URL検査

異常時は回答を破棄する。

---

# 13. Rate Limit

制限対象

- User
- Organization
- API Key
- IP Address

制御項目

- Request/Minute
- Token/Minute
- Concurrent Request

---

# 14. 監査ログ

保存項目

- UserID
- Prompt
- Response
- Model
- Function
- MCP Tool
- Token数
- Cost
- Timestamp
- IP Address

---

# 15. 暗号化

保存時

- AES-256

通信時

- TLS 1.3

Secret

- Azure Key Vault

---

# 16. Prisma実装方針

Model

```
AISecurityLog

PromptAudit

SecurityPolicy

RateLimitLog

PIIMaskingLog
```

Relation

```
User

Organization

AIConversation
```

---

# 17. コンプライアンス

対応予定

- ISO 27001
- SOC 2
- GDPR
- 日本個人情報保護法
- Microsoft Responsible AI Standard

---

# 18. 監視

Azure Monitor

Application Insights

Microsoft Defender for Cloud

監視項目

- 不正アクセス
- 異常トークン使用
- Prompt Injection
- APIエラー
- AI利用状況

---

# 19. インシデント対応

検知時

- AI利用停止
- 管理者通知
- ログ保存
- セッション無効化
- アラート送信

重大インシデントはSOCへ通知する。

---

# 20. 将来拡張

- AI異常検知
- Zero Trust AI
- AI Risk Score
- AI Policy Engine
- Dynamic Guardrails
- AI Explainability
- Confidential Computing
- Data Loss Prevention（DLP）
- AI Governance Dashboard
- 自動コンプライアンス監査
