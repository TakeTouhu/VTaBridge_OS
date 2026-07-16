# Proposal API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Proposal APIは、VTaBridge OSにおける提案書の作成・管理・承認・送付を行うAPIである。

営業案件、エンジニア紹介、見積書と連携し、AIによる提案書生成・要約・改善提案を提供する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/proposals | 提案書一覧取得 |
| GET | /api/v1/proposals/{id} | 提案書詳細取得 |
| POST | /api/v1/proposals | 提案書作成 |
| PUT | /api/v1/proposals/{id} | 提案書更新 |
| DELETE | /api/v1/proposals/{id} | 提案書削除 |
| POST | /api/v1/proposals/{id}/approve | 承認 |
| POST | /api/v1/proposals/{id}/send | メール送付 |
| POST | /api/v1/proposals/{id}/generate | AI生成 |
| POST | /api/v1/proposals/{id}/improve | AI改善提案 |

---

# 3. 提案書一覧取得

GET

```
/api/v1/proposals
```

Query Parameter

| Name | Type |
|------|------|
| companyId | UUID |
| projectId | UUID |
| status | string |
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
      "proposalNo":"PROP-202600001",
      "title":"React開発案件提案書",
      "company":"株式会社〇〇",
      "status":"Draft",
      "createdAt":"2026-08-01"
    }
  ]
}
```

---

# 4. 提案書詳細取得

GET

```
/api/v1/proposals/{id}
```

Response

```json
{
  "id":"UUID",
  "proposalNo":"PROP-202600001",
  "title":"React開発案件提案書",
  "company":"株式会社〇〇",
  "project":"React開発案件",
  "engineers":[],
  "summary":"...",
  "status":"Approved",
  "attachments":[]
}
```

---

# 5. 提案書作成

POST

```json
{
  "companyId":"UUID",
  "projectId":"UUID",
  "title":"React開発案件提案書",
  "templateId":"UUID"
}
```

Response

```json
{
  "success":true,
  "message":"Proposal created."
}
```

---

# 6. 提案書更新

PUT

```
/api/v1/proposals/{id}
```

更新対象

- タイトル
- 内容
- 添付資料
- エンジニア
- ステータス

---

# 7. 提案書削除

DELETE

```
/api/v1/proposals/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- 提案書自動生成
- 提案内容改善
- 誤字脱字チェック
- 技術説明生成
- エンジニア推薦
- 提案成功率予測
- 差別化ポイント抽出
- 提案内容要約

---

# 9. Validation

title

- 必須
- 最大255文字

companyId

- 必須

projectId

- 必須

---

# 10. Permission

| Permission |
|------------|
| proposal.read |
| proposal.write |
| proposal.approve |
| ai.use |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| PROPOSAL001 | Proposal Not Found |
| PROPOSAL002 | Invalid Company |
| PROPOSAL003 | Invalid Project |
| PROPOSAL004 | Approval Failed |
| PROPOSAL005 | Validation Error |

---

# 12. OpenAPI

```yaml
paths:

  /proposals:

    get:
      summary: Get Proposal List

    post:
      summary: Create Proposal

  /proposals/{id}:

    get:
      summary: Get Proposal

    put:
      summary: Update Proposal

    delete:
      summary: Delete Proposal

  /proposals/{id}/generate:

    post:
      summary: AI Generate Proposal
```

---

# 13. Prisma実装方針

Model

```
Proposal

ProposalItem

ProposalAttachment
```

Relation

```
Company

Project

Engineer

TemplateMaster

User
```

Soft Deleteを採用する。

proposal_noにはUnique制約を設定する。

---

# 14. AI提案書生成

Request

```json
{
  "projectId":"UUID",
  "engineerIds":[
    "UUID"
  ],
  "templateId":"UUID"
}
```

Response

```json
{
  "title":"React開発案件提案書",
  "summary":"...",
  "content":"..."
}
```

---

# 15. 将来拡張

- Word自動生成
- PDF自動生成
- PowerPoint自動生成
- 電子署名連携
- AI提案成功率予測
- AI競合分析
- AI価格提案
- AI営業支援
- Microsoft Word連携
- Google Docs連携
