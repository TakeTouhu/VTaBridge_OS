# Contact API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Contact APIは、企業担当者（Contact）の管理を行うAPIである。

担当者情報、所属企業、役職、連絡先、営業履歴を管理し、営業活動・案件・契約・AI営業支援の基盤となる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/contacts | 担当者一覧取得 |
| GET | /api/v1/contacts/{id} | 担当者詳細取得 |
| POST | /api/v1/contacts | 担当者登録 |
| PUT | /api/v1/contacts/{id} | 担当者更新 |
| DELETE | /api/v1/contacts/{id} | 担当者削除 |
| GET | /api/v1/contacts/search | 担当者検索 |
| GET | /api/v1/contacts/{id}/meetings | 面談履歴取得 |
| GET | /api/v1/contacts/{id}/mails | メール履歴取得 |
| GET | /api/v1/contacts/{id}/tasks | タスク一覧取得 |

---

# 3. 担当者一覧取得

GET

```
/api/v1/contacts
```

Query

| Name | Type |
|------|------|
| keyword | string |
| companyId | UUID |
| department | string |
| position | string |
| status | string |
| page | integer |
| pageSize | integer |

---

Response

```json
{
  "success": true,
  "data": [
    {
      "id": "UUID",
      "name": "山田 太郎",
      "company": "株式会社〇〇",
      "department": "情報システム部",
      "position": "部長",
      "email": "taro@example.com",
      "status": "Active"
    }
  ]
}
```

---

# 4. 担当者詳細取得

GET

```
/api/v1/contacts/{id}
```

Response

```json
{
  "id": "UUID",
  "companyId": "UUID",
  "companyName": "株式会社〇〇",
  "name": "山田 太郎",
  "department": "情報システム部",
  "position": "部長",
  "email": "taro@example.com",
  "phone": "03-1234-5678",
  "mobile": "090-1234-5678",
  "preferredContact": "Email",
  "status": "Active",
  "meetings": [],
  "tasks": [],
  "mails": []
}
```

---

# 5. 担当者登録

POST

```json
{
  "companyId": "UUID",
  "name": "山田 太郎",
  "department": "情報システム部",
  "position": "部長",
  "email": "taro@example.com",
  "phone": "03-1234-5678",
  "mobile": "090-1234-5678"
}
```

Response

```json
{
  "success": true,
  "message": "Contact created."
}
```

---

# 6. 担当者更新

PUT

```
/api/v1/contacts/{id}
```

更新対象

- 氏名
- 部署
- 役職
- メール
- 電話番号
- 携帯番号
- メモ
- ステータス

---

# 7. 担当者削除

DELETE

```
/api/v1/contacts/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 担当者分析
- 次回アプローチ提案
- 面談内容要約
- メール返信提案
- フォロー漏れ検知
- 商談成功率分析
- キーパーソン判定
- 関係性スコア分析

---

# 9. Validation

name

- 必須
- 最大100文字

email

- メール形式
- 重複不可（企業内）

phone

- 電話番号形式

mobile

- 電話番号形式

---

# 10. Permission

| Permission |
|------------|
| contact.read |
| contact.write |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| CON001 | Contact Not Found |
| CON002 | Duplicate Email |
| CON003 | Invalid Company |
| CON004 | Validation Error |

---

# 12. OpenAPI

```yaml
paths:

  /contacts:

    get:
      summary: Get Contact List

    post:
      summary: Create Contact

  /contacts/{id}:

    get:
      summary: Get Contact

    put:
      summary: Update Contact

    delete:
      summary: Delete Contact
```

---

# 13. Prisma実装方針

Model

```
Contact
```

Relation

```
Company

Meeting

MailThread

Task
```

Soft Deleteを採用する。

company_idとの外部キー制約を設定する。

(company_id, email)には複合Unique制約を設定する。

---

# 14. 将来拡張

- 名刺OCR
- Outlook連携
- Microsoft Graph連携
- Google Contacts同期
- LinkedIn連携
- AI人物分析
- AI担当者異動検知
- AI営業アシスタント
