# Project API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Project APIは、VTaBridge OSにおける案件管理を行う中核APIである。

営業案件、募集案件、契約案件、参画案件までを一元管理し、AIマッチング・営業支援・契約・請求・分析機能の中心となる。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/projects | 案件一覧取得 |
| GET | /api/v1/projects/{id} | 案件詳細取得 |
| POST | /api/v1/projects | 案件登録 |
| PUT | /api/v1/projects/{id} | 案件更新 |
| DELETE | /api/v1/projects/{id} | 案件削除 |
| GET | /api/v1/projects/search | 高度検索 |
| GET | /api/v1/projects/{id}/engineers | 候補者一覧 |
| POST | /api/v1/projects/{id}/matching | AIマッチング |
| POST | /api/v1/projects/{id}/assign | エンジニア参画 |
| GET | /api/v1/projects/{id}/contracts | 契約一覧 |
| GET | /api/v1/projects/{id}/invoices | 請求一覧 |

---

# 3. 案件一覧取得

GET

```
/api/v1/projects
```

Query Parameter

| Name | Type |
|------|------|
| keyword | string |
| companyId | UUID |
| industryId | UUID |
| status | string |
| contractType | string |
| requiredSkill | string |
| country | string |
| page | integer |
| pageSize | integer |
| sort | string |
| order | asc / desc |

---

Response

```json
{
  "success": true,
  "data": [
    {
      "id":"UUID",
      "projectName":"React開発案件",
      "company":"株式会社〇〇",
      "status":"Recruiting",
      "startDate":"2026-08-01",
      "endDate":"2027-01-31",
      "requiredEngineers":3
    }
  ]
}
```

---

# 4. 案件詳細取得

GET

```
/api/v1/projects/{id}
```

Response

```json
{
  "id":"UUID",
  "projectName":"React開発案件",
  "company":"株式会社〇〇",
  "industry":"IT",
  "contractType":"SES",
  "location":"東京都",
  "remoteType":"Hybrid",
  "requiredSkills":[
    "React",
    "TypeScript",
    "AWS"
  ],
  "preferredSkills":[
    "Next.js",
    "Docker"
  ],
  "headCount":3,
  "startDate":"2026-08-01",
  "endDate":"2027-01-31",
  "status":"Recruiting",
  "engineers":[]
}
```

---

# 5. 案件登録

POST

```json
{
  "companyId":"UUID",
  "projectName":"React開発案件",
  "contractTypeId":"UUID",
  "requiredSkills":[
    "UUID",
    "UUID"
  ],
  "headCount":3,
  "startDate":"2026-08-01"
}
```

---

# 6. 案件更新

PUT

```
/api/v1/projects/{id}
```

更新対象

- 案件名
- 必須スキル
- 募集人数
- 契約形態
- 単価
- 稼働条件
- ステータス

---

# 7. 案件削除

DELETE

```
/api/v1/projects/{id}
```

論理削除を行う。

---

# 8. AI機能

AIは以下を支援する。

- エンジニアマッチング
- スキル不足分析
- 適正単価予測
- 採用難易度分析
- 案件要約
- 募集文自動生成
- 類似案件検索
- 成約率予測
- 人員不足予測
- 案件リスク分析

---

# 9. Validation

projectName

- 必須
- 最大255文字

headCount

- 1以上

startDate

- 必須

requiredSkills

- 1件以上必須

---

# 10. Permission

| Permission |
|------------|
| project.read |
| project.write |
| project.delete |
| ai.use |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| PRO001 | Project Not Found |
| PRO002 | Invalid Company |
| PRO003 | Invalid Skill |
| PRO004 | Invalid Contract Type |
| PRO005 | Validation Error |
| PRO006 | Engineer Already Assigned |

---

# 12. OpenAPI

```yaml
paths:

  /projects:

    get:
      summary: Get Project List

    post:
      summary: Create Project

  /projects/{id}:

    get:
      summary: Get Project

    put:
      summary: Update Project

    delete:
      summary: Delete Project

  /projects/{id}/matching:

    post:
      summary: AI Matching
```

---

# 13. Prisma実装方針

Model

```
Project
```

Relation

```
Company

ContractTypeMaster

ProjectSkill

ProjectAssignment

Contract

Invoice

Meeting

Task
```

Soft Deleteを採用する。

全文検索インデックスを設定する。

---

# 14. AIマッチング

Request

```json
{
  "top":10
}
```

Response

```json
{
  "projectId":"UUID",
  "engineers":[
    {
      "engineerId":"UUID",
      "score":98,
      "reason":[
        "React経験7年",
        "AWS認定資格保有",
        "稼働可能"
      ]
    }
  ]
}
```

---

# 15. 将来拡張

- AI案件自動作成
- AI単価予測
- AI成約率予測
- AI募集文生成
- GitHub Issue連携
- Jira連携
- Backlog連携
- Azure DevOps連携
- AIプロジェクト分析
- AIリスク予測
