# Invoice API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Invoice APIは、VTaBridge OSにおける請求書の作成・送付・管理を行う中核APIである。

契約情報・稼働実績・支払条件と連携し、請求書の自動作成、送付、入金状況の管理を実現する。

営業・経理・AI分析の基盤となる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/invoices | 請求書一覧取得 |
| GET | /api/v1/invoices/{id} | 請求書詳細取得 |
| POST | /api/v1/invoices | 請求書作成 |
| PUT | /api/v1/invoices/{id} | 請求書更新 |
| DELETE | /api/v1/invoices/{id} | 請求書削除 |
| POST | /api/v1/invoices/{id}/issue | 請求書発行 |
| POST | /api/v1/invoices/{id}/send | メール送付 |
| POST | /api/v1/invoices/{id}/pdf | PDF生成 |
| GET | /api/v1/invoices/{id}/payments | 入金履歴取得 |

---

# 3. 請求書一覧取得

GET

```
/api/v1/invoices
```

Query Parameter

| Name | Type |
|------|------|
| companyId | UUID |
| projectId | UUID |
| contractId | UUID |
| status | string |
| dueDateFrom | Date |
| dueDateTo | Date |
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
      "invoiceNo":"INV-202600001",
      "company":"株式会社〇〇",
      "amount":850000,
      "status":"Issued",
      "dueDate":"2026-08-31"
    }
  ]
}
```

---

# 4. 請求書詳細取得

GET

```
/api/v1/invoices/{id}
```

Response

```json
{
  "id":"UUID",
  "invoiceNo":"INV-202600001",
  "company":"株式会社〇〇",
  "contract":"SES契約",
  "project":"React開発案件",
  "issueDate":"2026-08-01",
  "dueDate":"2026-08-31",
  "amount":850000,
  "tax":85000,
  "totalAmount":935000,
  "status":"Issued",
  "payments":[]
}
```

---

# 5. 請求書作成

POST

```json
{
  "contractId":"UUID",
  "projectId":"UUID",
  "companyId":"UUID",
  "issueDate":"2026-08-01",
  "dueDate":"2026-08-31"
}
```

Response

```json
{
  "success":true,
  "message":"Invoice created."
}
```

---

# 6. 請求書更新

PUT

```
/api/v1/invoices/{id}
```

更新対象

- 請求日
- 支払期限
- 金額
- 備考
- ステータス

---

# 7. 請求書削除

DELETE

```
/api/v1/invoices/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 請求書自動作成
- 請求漏れ検知
- 入金遅延予測
- 売上予測
- キャッシュフロー分析
- 督促メール作成
- 異常請求検知
- 月次分析

---

# 9. Validation

contractId

- 必須

issueDate

- 必須

dueDate

- 必須

amount

- 0以上

---

# 10. Permission

| Permission |
|------------|
| invoice.read |
| invoice.write |
| invoice.issue |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| INV001 | Invoice Not Found |
| INV002 | Invalid Contract |
| INV003 | Invalid Company |
| INV004 | Validation Error |
| INV005 | Invoice Already Issued |

---

# 12. OpenAPI

```yaml
paths:

  /invoices:

    get:
      summary: Get Invoice List

    post:
      summary: Create Invoice

  /invoices/{id}:

    get:
      summary: Get Invoice

    put:
      summary: Update Invoice

    delete:
      summary: Delete Invoice

  /invoices/{id}/issue:

    post:
      summary: Issue Invoice

  /invoices/{id}/pdf:

    post:
      summary: Generate Invoice PDF
```

---

# 13. Prisma実装方針

Model

```
Invoice

InvoiceItem

InvoiceAttachment
```

Relation

```
Company

Project

Contract

Payment

User
```

Soft Deleteを採用する。

invoice_noにはUnique制約を設定する。

InvoiceItemで請求明細を管理する。

---

# 14. PDF生成

Request

```json
{
  "templateId":"UUID"
}
```

Response

```json
{
  "pdfUrl":"https://storage.vtabridge.jp/invoices/INV-202600001.pdf"
}
```

---

# 15. 将来拡張

- インボイス制度対応
- Stripe連携
- freee連携
- マネーフォワード連携
- PCA会計連携
- AI売上分析
- AI督促メール作成
- AIキャッシュフロー予測
- 電子請求書(Peppol)対応
- 定期請求自動生成
