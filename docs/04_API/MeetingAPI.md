# Meeting API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Meeting APIは、商談・面談・打ち合わせ・オンライン会議を管理するAPIである。

営業活動の記録だけではなく、AIによる議事録作成、ToDo抽出、次回アクション提案までを一元管理する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/meetings | 会議一覧取得 |
| GET | /api/v1/meetings/{id} | 会議詳細取得 |
| POST | /api/v1/meetings | 会議登録 |
| PUT | /api/v1/meetings/{id} | 会議更新 |
| DELETE | /api/v1/meetings/{id} | 会議削除 |
| POST | /api/v1/meetings/{id}/minutes | AI議事録生成 |
| POST | /api/v1/meetings/{id}/summary | AI要約生成 |
| POST | /api/v1/meetings/{id}/tasks | AIタスク抽出 |

---

# 3. 会議一覧取得

GET

```
/api/v1/meetings
```

Query Parameter

| Name | Type |
|------|------|
| companyId | UUID |
| contactId | UUID |
| engineerId | UUID |
| projectId | UUID |
| from | Date |
| to | Date |
| keyword | string |
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
      "title":"React開発案件打合せ",
      "meetingDate":"2026-08-01T10:00:00Z",
      "company":"株式会社〇〇",
      "meetingType":"Online",
      "status":"Completed"
    }
  ]
}
```

---

# 4. 会議詳細取得

GET

```
/api/v1/meetings/{id}
```

Response

```json
{
  "id":"UUID",
  "title":"React開発案件打合せ",
  "meetingDate":"2026-08-01T10:00:00Z",
  "duration":60,
  "location":"Microsoft Teams",
  "participants":[],
  "minutes":"",
  "summary":"",
  "tasks":[]
}
```

---

# 5. 会議登録

POST

```json
{
  "title":"React開発案件打合せ",
  "companyId":"UUID",
  "contactIds":[
    "UUID"
  ],
  "projectId":"UUID",
  "meetingDate":"2026-08-01T10:00:00Z",
  "duration":60,
  "meetingType":"Online"
}
```

---

# 6. 会議更新

PUT

```
/api/v1/meetings/{id}
```

更新対象

- 会議タイトル
- 日時
- 参加者
- 議事録
- 会議種別
- ステータス

---

# 7. 会議削除

DELETE

```
/api/v1/meetings/{id}
```

論理削除する。

---

# 8. AI機能

AIは以下を支援する。

- 音声文字起こし
- AI議事録作成
- 会議要約
- タスク抽出
- 決定事項抽出
- リスク抽出
- フォローアップメール作成
- 次回アジェンダ提案
- 感情分析
- 商談成功率分析

---

# 9. Validation

title

- 必須
- 最大255文字

meetingDate

- 必須

duration

- 1〜1440分

meetingType

- 必須

---

# 10. Permission

| Permission |
|------------|
| meeting.read |
| meeting.write |
| ai.use |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| MET001 | Meeting Not Found |
| MET002 | Invalid Company |
| MET003 | Invalid Participant |
| MET004 | Validation Error |
| MET005 | AI Processing Failed |

---

# 12. OpenAPI

```yaml
paths:

  /meetings:

    get:
      summary: Get Meeting List

    post:
      summary: Create Meeting

  /meetings/{id}:

    get:
      summary: Get Meeting

    put:
      summary: Update Meeting

    delete:
      summary: Delete Meeting

  /meetings/{id}/minutes:

    post:
      summary: Generate AI Minutes
```

---

# 13. Prisma実装方針

Model

```
Meeting
```

Relation

```
Company

Contact

Engineer

Project

MeetingParticipant

Task

MailThread
```

Soft Deleteを採用する。

MeetingParticipantで多対多を管理する。

---

# 14. AI議事録生成

Request

```json
{
  "audioFileId":"UUID"
}
```

Response

```json
{
  "summary":"React開発案件について打ち合わせを実施...",
  "minutes":"...",
  "tasks":[
    {
      "title":"提案書を送付",
      "dueDate":"2026-08-03"
    }
  ]
}
```

---

# 15. 将来拡張

- Microsoft Teams連携
- Zoom連携
- Google Meet連携
- Google Calendar連携
- Outlook Calendar連携
- AI会話分析
- AI営業コーチング
- AI次回商談予測
- リアルタイム文字起こし
- リアルタイム翻訳
