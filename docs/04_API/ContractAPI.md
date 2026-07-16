# Contract API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Contract APIは、VTaBridge OSにおける契約管理を行う中核APIである。

案件成立後の契約書作成、契約締結、更新、終了までを管理し、電子契約サービスとも連携する。

営業・法務・請求・AI分析の基盤となる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/contracts | 契約一覧取得 |
| GET | /api/v1/contracts/{id} | 契約詳細取得 |
| POST | /api/v1/contracts | 契約作成 |
| PUT | /api/v1/contracts/{id} | 契約更新 |
| DELETE | /api/v1/contracts/{id} | 契約削除 |
| POST | /api/v1/contracts/{id}/approve | 契約承認 |
| POST | /api/v1/contracts/{id}/sign | 電子署名 |
| POST | /api/v1/contracts/{id}/renew | 契約更新 |
| POST | /api/v1/contracts/{id}/terminate | 契約終了 |

---

# 3. 契約一覧取得

GET

```
/api/v1/contracts
```

Query Parameter

| Name | Type |
|------|------|
| companyId | UUID |
| projectId | UUID |
| engineerId | UUID |
| contractType | string |
| status | string |
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
      "contractNo":"CON-202600001",
      "company":"株式会社〇〇",
      "project":"React開発案件",
      "status":"Active",
      "startDate":"2026-08-01",
      "endDate":"2027-01-31"
    }
  ]
}
```

---

# 4. 契約詳細取得

GET

```
/api/v1/contracts/{id}
```

Response

```json
{
  "id":"UUID",
  "contractNo":"CON-202600001",
  "company":"株式会社〇〇",
  "project":"React開発案件",
  "engineer":"John Smith",
  "contractType":"SES",
  "amount":850000,
  "startDate":"2026-08-01",
  "endDate":"2027-01-31",
  "status":"Active",
  "attachments":[]
}
```

---

# 5. 契約作成

POST

```json
{
  "companyId":"UUID",
  "projectId":"UUID",
  "engineerId":"UUID",
  "contractTypeId":"UUID",
  "templateId":"UUID",
  "startDate":"2026-08-01",
  "endDate":"2027-01-31",
  "amount":850000
}
```

Response

```json
{
  "success":true,
  "message":"Contract created."
}
```

---

# 6. 契約更新

PUT

```
/api/v1/contracts/{id}
```

更新対象

- 契約期間
- 契約金額
- 契約内容
- 添付資料
- ステータス

---

# 7. 契約削除

DELETE

```
/api/v1/contracts/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 契約書生成
- 契約内容要約
- 契約リスク分析
- 契約更新通知
- 契約終了予測
- 契約比較
- 条項チェック
- 法務レビュー支援

---

# 9. Validation

contractTypeId

- 必須

companyId

- 必須

projectId

- 必須

amount

- 0以上

startDate

- endDate以前

---

# 10. Permission

| Permission |
|------------|
| contract.read |
| contract.write |
| contract.approve |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| CONTRACT001 | Contract Not Found |
| CONTRACT002 | Invalid Company |
| CONTRACT003 | Invalid Project |
| CONTRACT004 | Invalid Contract Type |
| CONTRACT005 | Validation Error |
| CONTRACT006 | Contract Already Signed |

---

# 12. OpenAPI

```yaml
paths:

  /contracts:

    get:
      summary: Get Contract List

    post:
      summary: Create Contract

  /contracts/{id}:

    get:
      summary: Get Contract

    put:
      summary: Update Contract

    delete:
      summary: Delete Contract

  /contracts/{id}/sign:

    post:
      summary: Electronic Signature
```

---

# 13. Prisma実装方針

Model

```
Contract

ContractAttachment

ContractHistory
```

Relation

```
Company

Project

Engineer

ContractTypeMaster

TemplateMaster

Invoice

User
```

Soft Deleteを採用する。

contract_noにはUnique制約を設定する。

契約履歴はContractHistoryで管理する。

---

# 14. 電子署名

Request

```json
{
  "provider":"DocuSign"
}
```

Response

```json
{
  "status":"Signed",
  "signedAt":"2026-08-01T10:00:00Z"
}
```

---

# 15. 将来拡張

- DocuSign連携
- Adobe Sign連携
- クラウドサイン連携
- GMOサイン連携
- AI契約書レビュー
- AI契約更新予測
- AI法務チェック
- AIリスク分析
- 電子印鑑対応
- 契約ワークフロー
