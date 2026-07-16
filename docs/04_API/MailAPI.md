# Mail API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Mail APIは、VTaBridge OSのメール機能を提供する中核APIである。

Microsoft Outlook、Microsoft Graph API、Gmailと連携し、送受信メール・AI返信・AI要約・案件との紐付け・営業活動の自動記録を実現する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/mails | メール一覧取得 |
| GET | /api/v1/mails/{id} | メール詳細取得 |
| POST | /api/v1/mails/send | メール送信 |
| POST | /api/v1/mails/reply | メール返信 |
| POST | /api/v1/mails/draft | 下書き保存 |
| DELETE | /api/v1/mails/{id} | メール削除 |
| POST | /api/v1/mails/{id}/summary | AI要約 |
| POST | /api/v1/mails/{id}/reply | AI返信作成 |
| POST | /api/v1/mails/{id}/translate | AI翻訳 |
| POST | /api/v1/mails/{id}/classify | AI分類 |

---

# 3. メール一覧取得

GET

```
/api/v1/mails
```

Query Parameter

| Name | Type |
|------|------|
| keyword | string |
| companyId | UUID |
| contactId | UUID |
| projectId | UUID |
| unread | boolean |
| from | Date |
| to | Date |
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
      "subject":"React案件のご提案",
      "from":"customer@example.com",
      "receivedAt":"2026-08-01T10:00:00Z",
      "unread":true
    }
  ]
}
```

---

# 4. メール詳細取得

GET

```
/api/v1/mails/{id}
```

Response

```json
{
  "id":"UUID",
  "subject":"React案件のご提案",
  "from":"customer@example.com",
  "to":[
    "sales@vtabridge.jp"
  ],
  "cc":[
    "manager@vtabridge.jp"
  ],
  "body":"本文",
  "attachments":[],
  "summary":"",
  "projectId":"UUID"
}
```

---

# 5. メール送信

POST

```json
{
  "to":[
    "customer@example.com"
  ],
  "cc":[
    "manager@example.com"
  ],
  "subject":"ご提案ありがとうございます",
  "body":"本文",
  "attachments":[]
}
```

Response

```json
{
  "success": true,
  "message":"Mail sent."
}
```

---

# 6. メール返信

POST

```
/api/v1/mails/reply
```

返信メールを送信する。

---

# 7. メール削除

DELETE

```
/api/v1/mails/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- メール要約
- メール返信生成
- 英訳・和訳
- 添削
- トーン変更
- 件名生成
- 重要度判定
- 自動分類
- 案件自動紐付け
- タスク抽出
- フォロー漏れ検知
- スパム判定

---

# 9. Validation

subject

- 必須
- 最大255文字

to

- 1件以上必須

body

- 必須

---

# 10. Permission

| Permission |
|------------|
| mail.read |
| mail.write |
| ai.use |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| MAIL001 | Mail Not Found |
| MAIL002 | Send Failed |
| MAIL003 | Attachment Error |
| MAIL004 | Invalid Recipient |
| MAIL005 | AI Processing Failed |

---

# 12. OpenAPI

```yaml
paths:

  /mails:

    get:
      summary: Get Mail List

  /mails/send:

    post:
      summary: Send Mail

  /mails/reply:

    post:
      summary: Reply Mail

  /mails/{id}/summary:

    post:
      summary: AI Summary

  /mails/{id}/reply:

    post:
      summary: AI Reply
```

---

# 13. Prisma実装方針

Model

```
Mail

MailThread

MailAttachment
```

Relation

```
Company

Contact

Project

Task

User
```

メールスレッド単位で管理する。

添付ファイルは別テーブルで管理する。

Microsoft Graph APIのMessage IDを保持する。

---

# 14. AI返信

Request

```json
{
  "tone":"Business",
  "language":"Japanese"
}
```

Response

```json
{
  "subject":"Re: React案件について",
  "body":"お世話になっております。..."
}
```

---

# 15. 外部サービス連携

対応サービス

- Microsoft Graph API
- Outlook
- Exchange Online
- Gmail API
- SMTP
- IMAP

---

# 16. 将来拡張

- AIメール自動送信
- AIフォローアップ自動生成
- AI営業メール作成
- AIメール分析
- AI感情分析
- AIスパム判定
- Outlookアドイン
- Gmailアドイン
- Teams通知
- Slack通知
