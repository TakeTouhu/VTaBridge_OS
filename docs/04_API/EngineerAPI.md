# Engineer API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Engineer APIは、VTaBridge OSに登録されるエンジニア情報を管理する中核APIである。

プロフィール、スキル、資格、語学、職歴、希望条件、稼働状況を管理し、AIマッチング・案件推薦・営業活動・契約・請求・分析機能の基盤として利用する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/engineers | エンジニア一覧取得 |
| GET | /api/v1/engineers/{id} | 詳細取得 |
| POST | /api/v1/engineers | 登録 |
| PUT | /api/v1/engineers/{id} | 更新 |
| DELETE | /api/v1/engineers/{id} | 削除 |
| GET | /api/v1/engineers/search | 高度検索 |
| GET | /api/v1/engineers/{id}/skills | スキル一覧 |
| GET | /api/v1/engineers/{id}/career | 職歴 |
| GET | /api/v1/engineers/{id}/certifications | 資格一覧 |
| GET | /api/v1/engineers/{id}/languages | 語学一覧 |
| GET | /api/v1/engineers/{id}/projects | 案件履歴 |
| GET | /api/v1/engineers/{id}/resume | 履歴書 |
| GET | /api/v1/engineers/{id}/cv | 職務経歴書 |
| POST | /api/v1/engineers/{id}/matching | AIマッチング |

---

# 3. 一覧取得

GET

```
/api/v1/engineers
```

Query Parameter

| Name | Type |
|------|------|
| keyword | string |
| skill | string |
| certification | string |
| language | string |
| country | string |
| status | string |
| available | boolean |
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
      "name":"John Smith",
      "country":"Philippines",
      "experienceYears":6,
      "available":true,
      "skills":[
        "React",
        "Node.js",
        "AWS"
      ]
    }
  ]
}
```

---

# 4. 詳細取得

GET

```
/api/v1/engineers/{id}
```

Response

```json
{
  "id":"UUID",
  "firstName":"John",
  "lastName":"Smith",
  "email":"john@example.com",
  "country":"Philippines",
  "experienceYears":6,
  "hourlyRate":40,
  "available":true,
  "summary":"Senior Full Stack Engineer",
  "skills":[],
  "certifications":[],
  "languages":[],
  "career":[]
}
```

---

# 5. 登録

POST

```json
{
  "firstName":"John",
  "lastName":"Smith",
  "email":"john@example.com",
  "countryId":"UUID",
  "experienceYears":6,
  "hourlyRate":40
}
```

---

# 6. 更新

PUT

```
/api/v1/engineers/{id}
```

更新対象

- 基本情報
- スキル
- 資格
- 語学
- 希望単価
- 稼働状況
- 履歴書
- 職務経歴書

---

# 7. 削除

DELETE

```
/api/v1/engineers/{id}
```

論理削除する。

---

# 8. AI機能

AIは以下を支援する。

- 案件マッチング
- スキル分析
- スキル不足分析
- キャリア分析
- 履歴書生成
- 職務経歴書生成
- 英訳・和訳
- 単価予測
- 案件推薦
- 面接質問生成
- 市場価値分析
- スキルレベル推定

---

# 9. Validation

firstName

- 必須
- 最大100文字

lastName

- 必須
- 最大100文字

email

- メール形式
- 一意

experienceYears

- 0以上50以下

hourlyRate

- 0以上

---

# 10. Permission

| Permission |
|------------|
| engineer.read |
| engineer.write |
| engineer.delete |
| ai.use |
| admin.all |

---

# 11. Error Code

| Code | 内容 |
|------|------|
| ENG001 | Engineer Not Found |
| ENG002 | Duplicate Email |
| ENG003 | Invalid Skill |
| ENG004 | Invalid Country |
| ENG005 | Validation Error |
| ENG006 | Resume Not Found |

---

# 12. OpenAPI

```yaml
paths:

  /engineers:

    get:
      summary: Get Engineers

    post:
      summary: Create Engineer

  /engineers/{id}:

    get:
      summary: Get Engineer

    put:
      summary: Update Engineer

    delete:
      summary: Delete Engineer

  /engineers/{id}/matching:

    post:
      summary: AI Matching
```

---

# 13. Prisma実装方針

Model

```
Engineer
```

Relation

```
EngineerSkill

EngineerCertification

EngineerLanguage

EngineerCareer

CountryMaster

ProjectAssignment

Resume

CurriculumVitae
```

Soft Deleteを採用する。

emailにはUnique制約を設定する。

全文検索インデックスを設定する。

---

# 14. AIマッチング

入力

```json
{
  "projectId":"UUID"
}
```

出力

```json
{
  "score":95,
  "reason":[
    "React経験6年",
    "AWS Professional保有",
    "英語ビジネスレベル"
  ]
}
```

---

# 15. 将来拡張

- GitHub連携
- GitLab連携
- Stack Overflow連携
- LinkedIn連携
- AIスキル自動抽出
- AI職務経歴書生成
- AI面接評価
- AI単価予測
- AI離職リスク分析
- AIキャリアプランニング
