# Authorization 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Authorizationは、認証済みユーザー・システム・AI Agentに対し、どのリソースへ、どの操作を許可するかを制御するための設計を定義する。

Microsoft Entra ID・Azure RBAC・アプリケーションRBACを組み合わせ、最小権限（Least Privilege）の原則に基づいた認可を実現する。

---

# 2. 目的

Authorization導入目的

- 最小権限の実現
- 不正アクセス防止
- 権限昇格防止
- 業務ロール管理
- Zero Trust実現
- 監査性向上

---

# 3. 基本方針

採用方針

- Least Privilege
- Role Based Access Control（RBAC）
- Deny by Default
- Just Enough Access
- Just In Time Access（将来対応）

許可された操作のみ実行可能とする。

---

# 4. 認可対象

対象

- Web UI
- REST API
- AI Agent
- Workflow
- Database
- Azure Resource
- Storage
- 管理機能

---

# 5. ロール

標準ロール

- Super Administrator
- Administrator
- Sales
- Recruiter
- Engineer
- Finance
- Viewer

業務ロールごとに権限を管理する。

---

# 6. 権限モデル

```
User

↓

Role

↓

Permission

↓

Resource

↓

Action
```

ロールを介して権限を付与する。

---

# 7. 権限一覧

基本権限

- Create
- Read
- Update
- Delete
- Execute
- Approve
- Export
- Import

CRUD以外の業務権限も定義する。

---

# 8. リソース

対象

- Customer
- Engineer
- Project
- Contract
- Invoice
- AI Chat
- Workflow
- Report
- User
- Setting

リソース単位でアクセス制御を行う。

---

# 9. API認可

実装

- JWT Scope
- Role Validation
- Permission Check
- Resource Ownership

APIごとに認可を実施する。

---

# 10. Workflow認可

対象

- 作成
- 編集
- 実行
- 削除
- 公開

Workflow単位で権限を制御する。

---

# 11. AI認可

対象

- AI Chat
- AI Agent
- OCR
- RAG
- Function Calling
- Prompt管理

AI機能ごとに利用権限を設定する。

---

# 12. データアクセス制御

実装

- Row Level Security（必要時）
- Organization単位制御
- 所有者制御
- 部門単位制御

必要最小限のデータのみ参照可能とする。

---

# 13. Azure RBAC

対象

- Storage
- Key Vault
- PostgreSQL
- Azure OpenAI
- AI Search

Azure標準RBACを利用する。

---

# 14. 管理者権限

対象

- ユーザー管理
- ロール管理
- システム設定
- AI設定
- 監査ログ

管理者権限を最小限に限定する。

---

# 15. 権限棚卸し

実施

- 月次レビュー
- 不要権限削除
- 管理者確認
- 監査実施

定期的に権限を見直す。

---

# 16. 認可失敗

対応

- HTTP 403
- Audit Log
- Alert通知
- Security Review

不正アクセス試行を監査対象とする。

---

# 17. ログ

取得項目

- User
- Role
- Resource
- Action
- Result
- Timestamp

監査ログとして保存する。

---

# 18. KPI

管理項目

- RBAC適用率
- 権限変更件数
- 不正アクセス件数
- 権限棚卸し実施率
- 管理者数

継続的に評価する。

---

# 19. ベストプラクティス

- Deny by Defaultを採用する
- ロールを細分化しすぎない
- 一時的な権限は期限付きとする
- 権限変更は監査対象とする
- 定期的な棚卸しを実施する

---

# 20. 将来拡張

- Attribute Based Access Control（ABAC）
- Policy Based Access Control
- Microsoft Entra PIM
- Dynamic Authorization
- AI権限分析
- リスクベース認可
- AIアクセス異常検知
- Just In Time Access
- Continuous Authorization
- Autonomous Authorization Management
