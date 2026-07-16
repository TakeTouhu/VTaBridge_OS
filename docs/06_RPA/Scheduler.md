# Scheduler 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Schedulerは、VTaBridge OSにおけるすべての定期ジョブ・イベントジョブ・非同期ジョブを管理する実行基盤である。

Power Automate、Python、Playwright、AI Agent、Azure Functionsなどの自動処理はSchedulerを経由して実行する。

ジョブの依存関係・優先順位・リトライ・監視・履歴管理を統一的に提供する。

---

# 2. 目的

Scheduler導入目的

- 定期実行
- 非同期処理
- ジョブ管理
- リトライ
- 実行履歴管理
- 負荷分散
- ワークフロー管理
- AI Agent起動

---

# 3. アーキテクチャ

```
Trigger

↓

Scheduler

↓

Queue

↓

Worker

────────────────────────

Python

Playwright

Power Automate

Azure Functions

AI Agent

────────────────────────

↓

Business API

↓

PostgreSQL
```

---

# 4. Trigger

対応トリガー

- Cron
- Timer
- Queue
- API
- Webhook
- File Upload
- Manual
- AI Agent

---

# 5. ジョブ種別

| 種別 | 説明 |
|------|------|
| Scheduled Job | 定期実行 |
| Event Job | イベント実行 |
| Queue Job | 非同期実行 |
| Manual Job | 手動実行 |
| AI Job | AI Agent実行 |

---

# 6. スケジュール

対応形式

- Cron Expression
- ISO8601
- UTC
- JST

例

```
0 9 * * *
```

毎日9:00実行

---

# 7. ジョブ状態

| Status | 説明 |
|---------|------|
| Waiting | 待機 |
| Running | 実行中 |
| Success | 成功 |
| Failed | 失敗 |
| Retry | リトライ |
| Cancelled | キャンセル |

---

# 8. 優先順位

Priority

- Critical
- High
- Normal
- Low

Criticalを優先実行する。

---

# 9. Queue

利用サービス

- Azure Storage Queue
- Azure Service Bus

用途

- 非同期処理
- 負荷分散
- リトライ

---

# 10. リトライ

最大

```
3回
```

方式

- Exponential Backoff

失敗時はQueueへ戻す。

---

# 11. ジョブ依存関係

例

```
CSV取込

↓

OCR

↓

AI解析

↓

DB登録

↓

Teams通知
```

前ジョブ成功時のみ次ジョブを実行する。

---

# 12. API

```
GET

/api/v1/scheduler/jobs
```

```
POST

/api/v1/scheduler/jobs
```

```
PUT

/api/v1/scheduler/jobs/{id}
```

```
DELETE

/api/v1/scheduler/jobs/{id}
```

```
POST

/api/v1/scheduler/jobs/{id}/run
```

---

# 13. Prisma実装方針

Model

```
SchedulerJob

SchedulerHistory

SchedulerQueue

SchedulerTrigger
```

Relation

```
AutomationJob

User

Organization
```

---

# 14. ログ

保存項目

- JobID
- Trigger
- Worker
- Queue
- StartTime
- EndTime
- Duration
- RetryCount
- Status
- Error

---

# 15. 通知

ジョブ失敗時

通知先

- Teams
- メール
- Slack

Notification APIを利用する。

---

# 16. セキュリティ

実装

- Azure Entra ID
- RBAC
- JWT
- Audit Log
- Key Vault

ジョブの実行権限を管理する。

---

# 17. 監視

Azure Monitor

Application Insights

Log Analytics

監視項目

- 実行数
- エラー率
- Queue数
- 平均実行時間
- Retry率

---

# 18. 性能目標

ジョブ起動

```
500ms以内
```

Queue登録

```
300ms以内
```

Worker起動

```
1秒以内
```

---

# 19. 運用

実施内容

- 古いジョブ削除
- 履歴アーカイブ
- Queue監視
- スケジュール変更
- ジョブ再実行

---

# 20. 将来拡張

- DAG Workflow
- Event Grid連携
- Kubernetes CronJob対応
- Airflow連携
- AIスケジューリング
- 優先度自動最適化
- 自動負荷分散
- ジョブ予測実行
- マルチリージョン対応
- Workflow可視化
