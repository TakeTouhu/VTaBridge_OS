# RPA Architecture

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

RPA Architectureでは、VTaBridge OS全体の業務自動化基盤を定義する。

Power Automate、Python、Playwright、Azure Functions、Azure Logic Apps、AI Agentを組み合わせ、営業・採用・契約・請求・通知・レポート作成などの業務を自動化する。

GUI操作だけに依存せず、APIファーストの設計を採用する。

---

# 2. 目的

RPA導入目的

- 定型業務の自動化
- 入力ミス削減
- 作業時間短縮
- 業務品質向上
- AIとの連携
- 人手不足対策
- 24時間自動処理
- 業務標準化

---

# 3. 全体アーキテクチャ

```
                User

                  │

             Next.js UI

                  │

            Business API

                  │

         Automation Orchestrator

                  │

 ┌────────────────────────────────┐

 Power Automate

 Python Worker

 Playwright

 Azure Functions

 Azure Logic Apps

 AI Agent

 └────────────────────────────────┘

                  │

          Queue / Scheduler

                  │

            Business API

                  │

            PostgreSQL

                  │

         Teams / Outlook

         SharePoint

         External API
```

---

# 4. コンポーネント

| Component | 役割 |
|-----------|------|
| Power Automate | Microsoftサービス連携 |
| Python | 業務処理・帳票生成 |
| Playwright | Web自動操作 |
| Azure Functions | サーバーレス処理 |
| Logic Apps | ワークフロー |
| AI Agent | AIによる業務判断 |

---

# 5. 自動化対象

対象業務

- メール送信
- Outlook同期
- Teams通知
- 契約期限通知
- 請求書生成
- PDF生成
- OCR処理
- 定期レポート
- データ同期
- AI実行

---

# 6. 処理フロー

```
イベント発生

↓

Queue登録

↓

Scheduler

↓

Automation実行

↓

Business API

↓

DB更新

↓

通知

↓

ログ保存
```

---

# 7. イベント

トリガー

- API
- Timer
- Webhook
- Queue
- File Upload
- Manual
- AI Agent

---

# 8. Queue

利用サービス

- Azure Storage Queue
- Azure Service Bus

用途

- 非同期処理
- リトライ
- 負荷分散

---

# 9. Scheduler

実行方式

- Cron
- Timer Trigger
- Event Trigger
- Queue Trigger

定期ジョブはSchedulerで管理する。

---

# 10. AI連携

AI Agentが以下を実施する。

- Workflow選択
- RPA起動
- エラー分析
- 自動リトライ
- 通知生成

---

# 11. ログ

保存項目

- JobID
- Workflow
- Status
- StartTime
- EndTime
- User
- Error
- RetryCount

---

# 12. エラー処理

異常時

- Retry
- Queueへ戻す
- 管理者通知
- ログ保存
- AI分析

---

# 13. セキュリティ

実装

- Azure Entra ID
- RBAC
- Managed Identity
- Key Vault
- TLS通信
- Audit Log

---

# 14. Prisma実装方針

Model

```
AutomationJob

AutomationHistory

AutomationQueue

AutomationWorkflow

AutomationLog
```

Relation

```
User

Project

Company

Task
```

---

# 15. 性能目標

Job開始

```
1秒以内
```

Queue処理

```
500ms以内
```

通知

```
3秒以内
```

---

# 16. 可用性

目標

```
99.9%
```

冗長化

- Azure Functions
- Queue
- PostgreSQL
- Redis

---

# 17. 監視

Azure Monitor

Application Insights

Log Analytics

監視項目

- Job数
- Error率
- Retry数
- Queue数
- 実行時間

---

# 18. 将来拡張

- AI Workflow Engine
- Human Approval Workflow
- BPMN対応
- Power Platform連携強化
- SAP連携
- Salesforce連携
- ServiceNow連携
- GitHub Actions連携
- Kubernetes Job対応
- Event Grid連携
