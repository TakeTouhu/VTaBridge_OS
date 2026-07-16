# Task API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Task APIは、VTaBridge OS全体のタスクを管理するAPIである。

営業、採用、案件、契約、請求、AI、RPAなど、システム内のあらゆる業務タスクを一元管理する。

AIによるタスク生成・優先順位付け・期限管理・リマインダーにも対応する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/tasks | タスク一覧取得 |
| GET | /api/v1/tasks/{id} | タスク詳細取得 |
| POST | /api/v1/tasks | タスク作成 |
| PUT | /api/v1/tasks/{id} | タスク更新 |
| DELETE | /api/v1/tasks/{id} | タスク削除 |
| POST | /api/v1/tasks/{id}/complete | タスク完了 |
| POST | /api/v1/tasks/ai-generate | AIタスク生成 |
| POST | /api/v1/tasks/priority | AI優先順位付け |

---

# 3. タスク一覧取得

GET

```
/api/v1/tasks
```

Query Parameter

| Name | Type |
|------|------|
| assigneeId | UUID |
| projectId | UUID |
| companyId | UUID |
| priority | string |
| status | string |
| dueDate | Date |
| page | integer |
| pageSize | integer |

---

Response

```json
{
  "success": true,
  "data": [
    {
      "id":"UUID",
      "title":"提案書送付",
      "priority":"High",
      "status":"InProgress",
      "dueDate":"2026-08-03"
    }
  ]
}
```

---

# 4. タスク詳細取得

GET

```
/api/v1/tasks/{id}
```

Response

```json
{
  "id":"UUID",
  "title":"提案書送付",
  "description":"React案件提案書を送付する",
  "projectId":"UUID",
  "companyId":"UUID",
  "assigneeId":"UUID",
  "priority":"High",
  "status":"InProgress",
  "dueDate":"2026-08-03",
  "completedAt":null
}
```

---

# 5. タスク作成

POST

```json
{
  "title":"提案書送付",
  "description":"React案件提案書を送付",
  "assigneeId":"UUID",
  "projectId":"UUID",
  "dueDate":"2026-08-03",
  "priority":"High"
}
```

Response

```json
{
  "success":true,
  "message":"Task created."
}
```

---

# 6. タスク更新

PUT

```
/api/v1/tasks/{id}
```

更新対象

- タイトル
- 内容
- 担当者
- 優先度
- ステータス
- 期限

---

# 7. タスク削除

DELETE

```
/api/v1/tasks/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- タスク自動生成
- 優先順位判定
- 期限予測
- 作業時間予測
- リマインダー生成
- 会議からタスク抽出
- メールからタスク抽出
- タスク要約
- 遅延予測
- 生産性分析

---

# 9. Validation

title

- 必須
- 最大255文字

priority

- Low
- Medium
- High
- Critical

dueDate

- 必須

---

# 10. Permission

| Permission |
|------------|
| task.read |
| task.write |
| task.complete |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| TASK001 | Task Not Found |
| TASK002 | Invalid Assignee |
| TASK003 | Validation Error |
| TASK004 | Already Completed |
| TASK005 | Due Date Invalid |

---

# 12. OpenAPI

```yaml
paths:

  /tasks:

    get:
      summary: Get Task List

    post:
      summary: Create Task

  /tasks/{id}:

    get:
      summary: Get Task

    put:
      summary: Update Task

    delete:
      summary: Delete Task

  /tasks/{id}/complete:

    post:
      summary: Complete Task
```

---

# 13. Prisma実装方針

Model

```
Task
```

Relation

```
User

Company

Project

Meeting

Mail

Contract
```

Soft Deleteを採用する。

priority・status・due_dateにはIndexを設定する。

---

# 14. AIタスク生成

Request

```json
{
  "meetingId":"UUID"
}
```

Response

```json
{
  "tasks":[
    {
      "title":"提案書を送付",
      "priority":"High",
      "dueDate":"2026-08-03"
    }
  ]
}
```

---

# 15. 将来拡張

- Microsoft To Do連携
- Planner連携
- Trello連携
- Asana連携
- Jira連携
- Backlog連携
- Notion連携
- Slack通知
- Teams通知
- AIスケジュール最適化
