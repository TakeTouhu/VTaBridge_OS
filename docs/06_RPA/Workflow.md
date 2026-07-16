# Workflow 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Workflowは、VTaBridge OSにおける業務プロセスを自動化・標準化するための実行基盤である。

Power Automate、Python、Playwright、AI Agentを組み合わせ、複数の業務をワークフローとして管理・実行する。

Human in the Loop（人による承認）を考慮した設計とし、自動化と人の判断を両立する。

---

# 2. 目的

Workflow導入目的

- 業務標準化
- 承認フロー
- AI自動化
- タスク連携
- 通知自動化
- 非同期処理
- 再利用性向上
- Human in the Loop対応

---

# 3. アーキテクチャ

```
Trigger

↓

Workflow Engine

↓

Decision

↓

────────────────────────────

Power Automate

Python

Playwright

AI Agent

Business API

────────────────────────────

↓

Approval

↓

Notification

↓

Complete
```

---

# 4. Workflow構成

Workflowは以下で構成する。

- Trigger
- Step
- Condition
- Action
- Approval
- Notification
- Error Handling
- Audit Log

---

# 5. Trigger

対応トリガー

- API
- Scheduler
- Webhook
- File Upload
- Manual
- AI Agent
- Event

---

# 6. Step

Step種別

- API実行
- Python実行
- Playwright実行
- Power Automate実行
- AI実行
- メール送信
- Teams通知
- 承認依頼

---

# 7. 条件分岐

対応

- IF
- ELSE
- SWITCH

例

```
契約金額

↓

100万円以上

↓

部長承認

↓

100万円未満

↓

担当者承認
```

---

# 8. 並列処理

Parallel Workflow対応

例

```
契約作成

↓

──────────────

PDF生成

Teams通知

メール送信

AI要約

──────────────

↓

終了
```

---

# 9. Human in the Loop

AIだけでは判断できない処理は人が承認する。

対象

- 契約
- 提案書
- 請求
- 削除
- 顧客登録

Approvalsと連携する。

---

# 10. AI Agent連携

AI Agentが実施

- Workflow選択
- Step生成
- 条件判断
- エラー分析
- 再実行
- 通知生成

---

# 11. Notification

通知先

- Teams
- Outlook
- Slack
- In App

Notification APIを利用する。

---

# 12. API

```
GET

/api/v1/workflows
```

```
POST

/api/v1/workflows
```

```
PUT

/api/v1/workflows/{id}
```

```
DELETE

/api/v1/workflows/{id}
```

```
POST

/api/v1/workflows/{id}/execute
```

---

# 13. Prisma実装方針

Model

```
Workflow

WorkflowStep

WorkflowExecution

WorkflowApproval

WorkflowHistory
```

Relation

```
AutomationJob

User

Task

Contract

Proposal
```

---

# 14. ログ

保存項目

- WorkflowID
- Step
- UserID
- Status
- StartTime
- EndTime
- Duration
- Error

---

# 15. エラー処理

実施内容

- Retry
- Rollback
- Queue登録
- 管理者通知
- AI分析

---

# 16. セキュリティ

実装

- Azure Entra ID
- RBAC
- Workflow Permission
- Audit Log
- Key Vault

Workflowごとに実行権限を管理する。

---

# 17. 性能目標

Workflow開始

```
1秒以内
```

Step実行

```
500ms以内
```

全Workflow

```
30秒以内
```

---

# 18. 可視化

Workflow Designerを提供する。

表示内容

- フロー図
- 実行履歴
- 実行状況
- エラー箇所
- 実行時間

BPMNライクな表示に対応する。

---

# 19. 運用

実施内容

- Workflowバージョン管理
- Workflowエクスポート
- Workflowインポート
- テンプレート管理
- 利用統計

---

# 20. 将来拡張

- BPMN 2.0対応
- Dynamic Workflow
- AI Workflow Designer
- Workflow Marketplace
- Process Mining
- Event Sourcing
- Saga Pattern対応
- Workflow Simulation
- ノーコードWorkflow作成
- AIによるWorkflow最適化
