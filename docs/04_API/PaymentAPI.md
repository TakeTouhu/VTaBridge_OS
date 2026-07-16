# Payment API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Payment APIは、VTaBridge OSにおける入金管理を行う中核APIである。

請求書に対する入金情報を管理し、売掛金管理、未収金管理、会計システム連携、AIによる資金予測の基盤となる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/payments | 入金一覧取得 |
| GET | /api/v1/payments/{id} | 入金詳細取得 |
| POST | /api/v1/payments | 入金登録 |
| PUT | /api/v1/payments/{id} | 入金更新 |
| DELETE | /api/v1/payments/{id} | 入金削除 |
| POST | /api/v1/payments/{id}/confirm | 入金確認 |
| GET | /api/v1/payments/unpaid | 未入金一覧取得 |
| GET | /api/v1/payments/overdue | 入金遅延一覧取得 |

---

# 3. 入金一覧取得

GET

```
/api/v1/payments
```

Query Parameter

| Name | Type |
|------|------|
| companyId | UUID |
| invoiceId | UUID |
| status | string |
| paymentMethod | string |
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
      "paymentNo":"PAY-202600001",
      "invoiceNo":"INV-202600001",
      "company":"株式会社〇〇",
      "amount":935000,
      "paymentDate":"2026-08-31",
      "status":"Completed"
    }
  ]
}
```

---

# 4. 入金詳細取得

GET

```
/api/v1/payments/{id}
```

Response

```json
{
  "id":"UUID",
  "paymentNo":"PAY-202600001",
  "invoiceId":"UUID",
  "invoiceNo":"INV-202600001",
  "company":"株式会社〇〇",
  "paymentMethod":"Bank Transfer",
  "paymentDate":"2026-08-31",
  "amount":935000,
  "status":"Completed",
  "memo":"予定通り入金"
}
```

---

# 5. 入金登録

POST

```json
{
  "invoiceId":"UUID",
  "paymentDate":"2026-08-31",
  "paymentMethod":"Bank Transfer",
  "amount":935000,
  "memo":"8月分入金"
}
```

Response

```json
{
  "success": true,
  "message":"Payment registered."
}
```

---

# 6. 入金更新

PUT

```
/api/v1/payments/{id}
```

更新対象

- 入金日
- 入金金額
- 入金方法
- メモ
- ステータス

---

# 7. 入金削除

DELETE

```
/api/v1/payments/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 入金遅延予測
- 未収金分析
- キャッシュフロー予測
- 督促タイミング提案
- 売掛金分析
- 異常入金検知
- 資金繰り予測
- 回収率分析

---

# 9. Validation

invoiceId

- 必須

paymentDate

- 必須

amount

- 0以上

paymentMethod

- 必須

---

# 10. Permission

| Permission |
|------------|
| payment.read |
| payment.write |
| payment.confirm |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| PAY001 | Payment Not Found |
| PAY002 | Invoice Not Found |
| PAY003 | Invalid Amount |
| PAY004 | Validation Error |
| PAY005 | Payment Already Confirmed |

---

# 12. OpenAPI

```yaml
paths:

  /payments:

    get:
      summary: Get Payment List

    post:
      summary: Create Payment

  /payments/{id}:

    get:
      summary: Get Payment

    put:
      summary: Update Payment

    delete:
      summary: Delete Payment

  /payments/{id}/confirm:

    post:
      summary: Confirm Payment
```

---

# 13. Prisma実装方針

Model

```
Payment
```

Relation

```
Invoice

Company

User
```

Soft Deleteを採用する。

payment_noにはUnique制約を設定する。

invoice_idとの外部キー制約を設定する。

---

# 14. 入金確認

Request

```json
{
  "confirmedBy":"UUID"
}
```

Response

```json
{
  "status":"Completed",
  "confirmedAt":"2026-08-31T09:15:00Z"
}
```

---

# 15. 将来拡張

- 銀行API連携
- Stripe Webhook連携
- PayPal連携
- freee会計連携
- マネーフォワード会計連携
- AI入金予測
- AI未収金分析
- AI督促自動化
- 自動消込
- 多通貨対応
