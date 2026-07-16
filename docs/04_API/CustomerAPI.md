# Customer API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Customer APIは、顧客企業を管理するためのAPIである。

営業活動、案件管理、契約管理、請求管理、AI分析の基盤となる中核APIとして位置付ける。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/customers | 顧客一覧取得 |
| GET | /api/v1/customers/{id} | 顧客詳細取得 |
| POST | /api/v1/customers | 顧客登録 |
| PUT | /api/v1/customers/{id} | 顧客更新 |
| DELETE | /api/v1/customers/{id} | 顧客削除 |
| GET | /api/v1/customers/search | 顧客検索 |
| GET | /api/v1/customers/{id}/projects | 案件一覧取得 |
| GET | /api/v1/customers/{id}/contacts | 担当者一覧取得 |
| GET | /api/v1/customers/{id}/contracts | 契約一覧取得 |
| GET | /api/v1/customers/{id}/invoices | 請求一覧取得 |

---

# 3. 顧客一覧取得

GET

```
/api/v1/customers?page=1&pageSize=20
```

Query Parameter

| Name | Type |
|------|------|
| keyword | string |
| industry | string |
| country | string |
| status | string |
| page | number |
| pageSize | number |
| sort | string |
| order | asc / desc |

---

Response

```json
{
  "success": true,
  "data": [
    {
      "id": "UUID",
      "companyName": "株式会社〇〇",
      "industry": "IT",
      "country": "Japan",
      "status": "Active"
    }
  ]
}
```

---

# 4. 顧客詳細取得

GET

```
/api/v1/customers/{id}
```

Response

```json
{
  "id":"UUID",
  "companyName":"株式会社〇〇",
  "companyKana":"カブシキガイシャ〇〇",
  "industry":"IT",
  "country":"Japan",
  "website":"https://example.com",
  "employeeCount":300,
  "annualRevenue":100000000,
  "status":"Active",
  "contacts":[],
  "projects":[],
  "contracts":[]
}
```

---

# 5. 顧客登録

POST

```json
{
  "companyName":"株式会社VTaBridge",
  "industryId":"UUID",
  "countryId":"UUID",
  "website":"https://vtabridge.jp",
  "employeeCount":50,
  "annualRevenue":500000000,
  "memo":"重要顧客"
}
```

Response

```json
{
  "success": true,
  "message": "Customer created."
}
```

---

# 6. 顧客更新

PUT

```
/api/v1/customers/{id}
```

更新対象

- 基本情報
- 業界
- 国
- メモ
- ステータス

---

# 7. 顧客削除

DELETE

```
/api/v1/customers/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 顧客分析
- 商談確率予測
- 解約リスク分析
- 売上予測
- 顧客ランク判定
- 次回営業提案
- フォロー漏れ検知

---

# 9. バリデーション

companyName

- 必須
- 最大255文字

website

- URL形式

employeeCount

- 0以上

annualRevenue

- 0以上

---

# 10. Permission

| Permission |
|------------|
| customer.read |
| customer.write |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| CUS001 | Customer Not Found |
| CUS002 | Duplicate Company |
| CUS003 | Invalid Industry |
| CUS004 | Invalid Country |
| CUS005 | Validation Error |

---

# 12. OpenAPI

```yaml
paths:

  /customers:

    get:
      summary: Get Customer List

    post:
      summary: Create Customer

  /customers/{id}:

    get:
      summary: Get Customer

    put:
      summary: Update Customer

    delete:
      summary: Delete Customer
```

---

# 13. Prisma実装方針

Model

```
Customer
```

Relation

```
IndustryMaster

CountryMaster

Contact

Project

Contract

Invoice
```

Soft Deleteを採用する。

---

# 14. 将来拡張

- Salesforce同期
- HubSpot同期
- Microsoft Dynamics連携
- 名刺OCR連携
- AI顧客スコアリング
- AI営業戦略提案
- AI失注分析
- 顧客360ビュー
