# API設計書

Version: 1.0

Status: Draft

---

# 1. 目的

本章では、VTaBridge OSで利用するREST APIを定義する。

Claude Codeが本設計書のみで以下を実装できることを目的とする。

- REST API
- Controller
- Service
- Repository
- Prisma
- DTO
- Validation
- 認証
- 権限制御
- OpenAPI(Swagger)

---

# 2. API設計方針

RESTful APIを採用する。

URLは複数形で統一する。

例

GET /customers

GET /projects

GET /engineers

---

# 3. HTTP Method

| Method | 用途 |
|---------|------|
| GET | 取得 |
| POST | 登録 |
| PUT | 更新 |
| PATCH | 一部更新 |
| DELETE | 削除 |

---

# 4. HTTP Status

| Code | 内容 |
|------|------|
|200|成功|
|201|作成成功|
|204|削除成功|
|400|入力エラー|
|401|認証エラー|
|403|権限エラー|
|404|存在しない|
|409|重複|
|422|バリデーションエラー|
|500|サーバーエラー|

---

# 5. 共通レスポンス

成功

```json
{
  "success": true,
  "data": {},
  "message": ""
}
```

失敗

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation Error"
  }
}
```

---

# 6. Pagination

Request

```
?page=1
&pageSize=20
```

Response

```json
{
  "page":1,
  "pageSize":20,
  "total":100,
  "totalPages":5,
  "data":[]
}
```

---

# 7. Sort

```
?sort=name

?order=asc
```

---

# 8. Filter

```
?status=Active

?country=JP

?keyword=React
```

---

# 9. Authentication

JWT Authentication

Bearer Token

```
Authorization: Bearer xxxxxxxxxxx
```

---

# 10. Authorization

RBACを採用する。

Role

- SuperAdmin
- Admin
- SalesManager
- Sales
- Recruiter
- Engineer
- Customer
- Guest

---

# 11. Audit Log

以下を全APIで保存する。

- User
- IP
- Browser
- API
- Method
- Request
- Response
- DateTime

---

# 12. OpenAPI

OpenAPI 3.1

Swagger UI

Redoc

---

# 13. Rate Limit

標準

100 req/min

AI API

20 req/min

Login

5 req/min

---

# 14. Version

URL Versioning

```
/api/v1/
```

---

# 15. Error Code

```
AUTH001

AUTH002

CUS001

ENG001

PRJ001

MAIL001

AI001

SYS001
```

---

# 16. AI API

AI専用APIを提供する。

- AI Chat

- AI Summary

- AI Mail Reply

- AI Matching

- AI Translation

- AI OCR

- AI Meeting Minutes

---

# 17. Webhook

対応予定

- Stripe

- GitHub

- Microsoft Graph

- Google

- Slack

- Teams

---

# 18. 非同期処理

Queueを採用する。

Redis

BullMQ

Job Worker

---

# 19. API一覧

実装予定

- Auth

- User

- Customer

- Contact

- Company

- Engineer

- Skill

- Project

- Meeting

- Mail

- Proposal

- Contract

- Invoice

- Payment

- Task

- AI

- Dashboard

- Notification

---

# 20. 今後作成するAPI

以下を個別設計する。

- Auth API
- Customer API
- Company API
- Contact API
- Engineer API
- Project API
- Meeting API
- Mail API
- Proposal API
- Contract API
- Invoice API
- Payment API
- Task API
- AI API
- Dashboard API
- Notification API

これらはOpenAPI形式(yaml)でも提供する。
