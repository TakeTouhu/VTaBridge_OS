# Company API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Company APIは、VTaBridge OSで管理する企業情報を管理するAPIである。

Companyはシステム全体の基盤エンティティであり、Customer、Partner、Vendor、Supplierなど複数の役割を持つことができる。

営業・契約・請求・AI分析・RPAの基礎データとなる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/companies | 一覧取得 |
| GET | /api/v1/companies/{id} | 詳細取得 |
| POST | /api/v1/companies | 登録 |
| PUT | /api/v1/companies/{id} | 更新 |
| DELETE | /api/v1/companies/{id} | 削除 |
| GET | /api/v1/companies/search | 検索 |
| GET | /api/v1/companies/{id}/contacts | 担当者取得 |
| GET | /api/v1/companies/{id}/projects | 案件取得 |
| GET | /api/v1/companies/{id}/contracts | 契約取得 |

---

# 3. 一覧取得

GET

```
/api/v1/companies
```

Query

| Name | Type |
|------|------|
| keyword | string |
| role | string |
| industry | string |
| country | string |
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
      "id":"UUID",
      "companyName":"VTaBridge株式会社",
      "role":"Customer",
      "industry":"IT",
      "country":"Japan",
      "status":"Active"
    }
  ]
}
```

---

# 4. 詳細取得

GET

```
/api/v1/companies/{id}
```

Response

```json
{
  "id":"UUID",
  "companyName":"VTaBridge株式会社",
  "companyKana":"ブイティーエーブリッジ",
  "industry":"IT",
  "country":"Japan",
  "website":"https://vtabridge.jp",
  "employeeCount":20,
  "annualRevenue":100000000,
  "roles":[
      "Customer",
      "Partner"
  ],
  "contacts":[],
  "projects":[],
  "contracts":[]
}
```

---

# 5. 登録

POST

```json
{
  "companyName":"VTaBridge株式会社",
  "industryId":"UUID",
  "countryId":"UUID",
  "website":"https://vtabridge.jp",
  "roles":[
      "Customer"
  ]
}
```

---

# 6. 更新

PUT

```
/api/v1/companies/{id}
```

更新対象

- 基本情報
- Role
- Website
- Industry
- Country
- Memo

---

# 7. 削除

DELETE

```
/api/v1/companies/{id}
```

論理削除する。

---

# 8. AI機能

AIは以下を支援する。

- 企業分析
- 与信分析
- 商談成功率分析
- AI営業戦略
- 顧客ランク判定
- AIリスク分析
- 類似企業推薦

---

# 9. Validation

companyName

- 必須
- 最大255文字

roles

- 1件以上必須

website

- URL形式

---

# 10. Permission

| Permission |
|------------|
| company.read |
| company.write |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| COM001 | Company Not Found |
| COM002 | Duplicate Company |
| COM003 | Invalid Industry |
| COM004 | Invalid Country |
| COM005 | Validation Error |

---

# 12. OpenAPI

```yaml
paths:

  /companies:

    get:
      summary: Company List

    post:
      summary: Create Company

  /companies/{id}:

    get:
      summary: Get Company

    put:
      summary: Update Company

    delete:
      summary: Delete Company
```

---

# 13. Prisma実装方針

Model

```
Company
```

関連

```
CountryMaster

IndustryMaster

Contact

Project

Contract

Invoice

Payment
```

Soft Deleteを採用する。

Roleは中間テーブルで管理する。

---

# 14. 将来拡張

- 法人番号API連携
- Google Maps API連携
- OpenCorporates連携
- Salesforce同期
- HubSpot同期
- AI企業分析
- AI与信分析
- AI営業先推薦
