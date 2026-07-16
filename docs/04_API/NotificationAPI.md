# Notification API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Notification APIは、VTaBridge OS全体の通知機能を提供する中核APIである。

営業、案件、契約、請求、AI処理、RPA、システムイベントなどの通知を一元管理し、ユーザーへリアルタイム通知を配信する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/notifications | 通知一覧取得 |
| GET | /api/v1/notifications/{id} | 通知詳細取得 |
| POST | /api/v1/notifications | 通知作成 |
| PUT | /api/v1/notifications/{id}/read | 既読 |
| PUT | /api/v1/notifications/read-all | 全件既読 |
| DELETE | /api/v1/notifications/{id} | 通知削除 |
| POST | /api/v1/notifications/send | 通知送信 |
| GET | /api/v1/notifications/unread-count | 未読件数取得 |

---

# 3. 通知一覧取得

GET

```
/api/v1/notifications
```

Query Parameter

| Name | Type |
|------|------|
| unread | boolean |
| type | string |
| priority | string |
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
      "title":"契約更新のお知らせ",
      "type":"Contract",
      "priority":"High",
      "isRead":false,
      "createdAt":"2026-08-01T09:00:00Z"
    }
  ]
}
```

---

# 4. 通知詳細取得

GET

```
/api/v1/notifications/{id}
```

Response

```json
{
  "id":"UUID",
  "title":"契約更新のお知らせ",
  "message":"契約更新期限が近づいています。",
  "type":"Contract",
  "priority":"High",
  "link":"/contracts/UUID",
  "isRead":false,
  "createdAt":"2026-08-01T09:00:00Z"
}
```

---

# 5. 通知作成

POST

```json
{
  "userId":"UUID",
  "title":"新規案件",
  "message":"React案件が登録されました。",
  "type":"Project",
  "priority":"Normal"
}
```

Response

```json
{
  "success":true,
  "message":"Notification created."
}
```

---

# 6. 通知送信

POST

```
/api/v1/notifications/send
```

通知チャネル

- システム通知
- メール
- Teams
- Slack
- Push通知

---

# 7. 通知削除

DELETE

```
/api/v1/notifications/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 通知重要度判定
- 通知要約
- 通知グループ化
- 通知最適化
- 通知タイミング最適化
- 異常通知検知
- AIリマインダー
- 優先順位付け

---

# 9. Validation

title

- 必須
- 最大255文字

message

- 必須

userId

- 必須

---

# 10. Permission

| Permission |
|------------|
| notification.read |
| notification.write |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| NOTI001 | Notification Not Found |
| NOTI002 | User Not Found |
| NOTI003 | Validation Error |
| NOTI004 | Send Failed |

---

# 12. OpenAPI

```yaml
paths:

  /notifications:

    get:
      summary: Get Notifications

    post:
      summary: Create Notification

  /notifications/{id}/read:

    put:
      summary: Read Notification

  /notifications/send:

    post:
      summary: Send Notification
```

---

# 13. Prisma実装方針

Model

```
Notification
```

Relation

```
User
```

Soft Deleteを採用する。

以下のIndexを設定する。

- user_id
- is_read
- created_at
- priority

---

# 14. 配信チャネル

対応チャネル

- In App
- Email
- Microsoft Teams
- Slack
- Web Push
- Mobile Push

通知設定に応じて配信先を切り替える。

---

# 15. リアルタイム通知

リアルタイム配信方式

- WebSocket
- SignalR
- Server-Sent Events（SSE）

通知受信時は画面更新を行わず、リアルタイムで通知バッジを更新する。

---

# 16. 通知種別

| Type | 説明 |
|------|------|
| Project | 案件 |
| Engineer | エンジニア |
| Contract | 契約 |
| Invoice | 請求 |
| Payment | 入金 |
| Meeting | 会議 |
| Task | タスク |
| Mail | メール |
| AI | AI処理 |
| System | システム |

---

# 17. 将来拡張

- LINE WORKS連携
- Discord連携
- Microsoft Outlook通知
- Google Chat連携
- AI通知最適化
- AI異常検知通知
- AIダイジェスト通知
- 通知テンプレート
- 多言語通知
- 通知配信履歴分析
