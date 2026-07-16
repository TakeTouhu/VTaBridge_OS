# Function Calling 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Function Callingは、AIがVTaBridge OSの業務APIを安全に呼び出すための仕組みである。

LLMは自然言語を理解し、必要に応じてFunctionを選択し、業務APIを実行する。

AIが直接データベースへアクセスすることは禁止し、必ずAPIを経由する。

---

# 2. 目的

Function Callingを利用する目的

- AIによる業務自動化
- ハルシネーション防止
- 最新データ取得
- システム操作
- AI Agent実装
- MCP連携

---

# 3. アーキテクチャ

```
User

↓

AI Chat

↓

GPT-5.5

↓

Function Calling

↓

AI API

↓

Business API

↓

PostgreSQL

↓

Response

↓

GPT

↓

User
```

---

# 4. 呼び出しフロー

```
User

↓

AI

↓

Function判定

↓

API実行

↓

JSON取得

↓

AI回答生成
```

---

# 5. Function一覧

標準Function

- SearchEngineer
- SearchProject
- SearchCompany
- SearchCustomer
- SearchContract
- SearchInvoice
- SearchMeeting
- SearchMail
- SearchTask
- GetDashboard

---

# 6. 更新系Function

更新可能Function

- CreateMeeting
- CreateTask
- SendMail
- CreateProposal
- CreateContract
- CreateInvoice
- UpdateEngineer
- UpdateProject

更新系Functionは権限チェックを必須とする。

---

# 7. Function定義

例

```json
{
  "name":"SearchEngineer",
  "description":"Search engineer",
  "parameters":{
      "skill":"string",
      "country":"string",
      "available":"boolean"
  }
}
```

---

# 8. 実行結果

FunctionはJSONのみ返却する。

例

```json
{
  "engineers":[
    {
      "name":"John Smith",
      "score":98
    }
  ]
}
```

AIはJSONを利用して自然文を生成する。

---

# 9. 認証

認証方式

- JWT
- Entra ID
- RBAC

ユーザー権限をAIへ渡す。

権限外Functionは禁止する。

---

# 10. 権限制御

Role例

- SuperAdmin
- Admin
- Sales
- Recruiter
- Engineer

Functionごとに実行権限を定義する。

---

# 11. Validation

Function実行前

実施内容

- Parameter Validation
- Permission Check
- Input Validation
- Prompt Injection Check

---

# 12. エラー処理

例

```json
{
    "code":"FUNC001",
    "message":"Permission Denied"
}
```

エラー時はAIへエラー内容のみ返却する。

---

# 13. ログ

保存項目

- UserID
- Function名
- Parameter
- Response
- ResponseTime
- Success
- Timestamp

---

# 14. Prisma実装方針

Model

```
FunctionExecutionLog

FunctionDefinition

FunctionPermission
```

---

# 15. セキュリティ

実装

- RBAC
- Parameter Validation
- Prompt Injection対策
- SQL Injection対策
- Rate Limit
- API監査ログ

---

# 16. 対応API

Function対象

- Engineer API
- Company API
- Customer API
- Contact API
- Project API
- Meeting API
- Proposal API
- Contract API
- Invoice API
- Payment API
- Task API
- Dashboard API

---

# 17. AI Agent連携

AI AgentはFunction Callingのみ利用する。

直接DBアクセスは禁止。

外部APIもFunction経由で呼び出す。

---

# 18. MCP連携

MCP Server経由で利用可能なFunction

- GitHub
- Microsoft 365
- Teams
- Outlook
- SharePoint
- Slack
- Notion

---

# 19. 性能目標

Function判定

```
300ms以内
```

API実行

```
1秒以内
```

AI回答

```
5秒以内
```

---

# 20. 将来拡張

- Parallel Function Calling
- Multi Function Calling
- Dynamic Function Discovery
- Workflow Function
- Event Driven Function
- Tool Chaining
- External MCP Function
- AI Self Planning
- Human Approval Workflow
- Function Marketplace
