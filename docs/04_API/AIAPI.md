# AI API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

AI APIは、VTaBridge OS全体のAI機能を提供する中核APIである。

Azure OpenAI Serviceを中心とし、RAG（Retrieval-Augmented Generation）、Embedding、Function Calling、AIエージェントを統合管理する。

営業支援、エンジニアマッチング、メール作成、契約書レビュー、議事録生成など、システム全体のAI機能は本APIを経由して利用する。

---

# 2. AIサービス一覧

| Service | 説明 |
|---------|------|
| AI Chat | AIチャット |
| AI Summary | 要約 |
| AI Translation | 翻訳 |
| AI Matching | エンジニアマッチング |
| AI Proposal | 提案書生成 |
| AI Mail | メール作成 |
| AI Meeting | 議事録生成 |
| AI OCR | OCR解析 |
| AI Search | RAG検索 |
| AI Agent | AIエージェント |

---

# 3. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| POST | /api/v1/ai/chat | AIチャット |
| POST | /api/v1/ai/summary | AI要約 |
| POST | /api/v1/ai/translate | AI翻訳 |
| POST | /api/v1/ai/matching | AIマッチング |
| POST | /api/v1/ai/proposal | AI提案書生成 |
| POST | /api/v1/ai/mail | AIメール生成 |
| POST | /api/v1/ai/meeting | AI議事録生成 |
| POST | /api/v1/ai/ocr | OCR解析 |
| POST | /api/v1/ai/search | RAG検索 |
| POST | /api/v1/ai/agent | AIエージェント実行 |

---

# 4. AI Chat

POST

```
/api/v1/ai/chat
```

Request

```json
{
  "message":"Reactエンジニアを紹介してください"
}
```

Response

```json
{
  "answer":"おすすめのエンジニアは..."
}
```

---

# 5. AI Summary

POST

```
/api/v1/ai/summary
```

Request

```json
{
  "text":"長文..."
}
```

Response

```json
{
  "summary":"要約結果..."
}
```

---

# 6. AI Translation

対応言語

- 日本語
- 英語
- ベトナム語
- 中国語
- 韓国語
- タイ語
- インドネシア語

---

# 7. AI Matching

入力

```json
{
  "projectId":"UUID"
}
```

出力

```json
{
  "engineers":[
    {
      "engineerId":"UUID",
      "score":98
    }
  ]
}
```

---

# 8. RAG

検索対象

- Engineer
- Project
- Contract
- Proposal
- Meeting
- Mail
- FAQ
- Knowledge

Embeddingを利用する。

---

# 9. AI Agent

Agent一覧

- Sales Agent
- Recruiter Agent
- HR Agent
- Legal Agent
- Finance Agent
- Customer Support Agent
- Project Manager Agent

---

# 10. Prompt管理

PromptはTemplateMasterで管理する。

Version管理を行う。

利用履歴を保存する。

---

# 11. Token管理

保存項目

- Prompt Tokens
- Completion Tokens
- Total Tokens
- Model
- Response Time

---

# 12. AIモデル

標準

- GPT-5.5
- GPT-5.5 mini

Embedding

- text-embedding-3-large

OCR

- Azure AI Document Intelligence

Speech

- Azure AI Speech

---

# 13. Validation

message

- 必須

最大

- 20000文字

---

# 14. Permission

| Permission |
|------------|
| ai.use |
| ai.admin |
| admin.all |

---

# 15. Error Code

| Code | 内容 |
|------|------|
| AI001 | Invalid Prompt |
| AI002 | Token Limit |
| AI003 | Model Error |
| AI004 | Timeout |
| AI005 | RAG Error |
| AI006 | OCR Error |

---

# 16. OpenAPI

```yaml
paths:

  /ai/chat:

    post:
      summary: AI Chat

  /ai/summary:

    post:
      summary: AI Summary

  /ai/matching:

    post:
      summary: AI Matching

  /ai/search:

    post:
      summary: RAG Search
```

---

# 17. Prisma実装方針

Model

```
AIConversation

AIPrompt

AIUsageLog

EmbeddingDocument

EmbeddingChunk

KnowledgeBase
```

Relation

```
User

Project

Engineer

Meeting

Mail
```

AI利用履歴を保存する。

Embeddingは別テーブルで管理する。

全文検索インデックスを設定する。

---

# 18. AI利用ログ

保存項目

- UserID
- Prompt
- Response
- Model
- Token数
- 処理時間
- 利用日時

---

# 19. 将来拡張

- Claude API
- Gemini API
- Grok API
- DeepSeek API
- MCP対応
- AI Workflow
- Multi Agent
- Voice Agent
- Video Agent
- AI Code Review
- AI BI分析
- AIダッシュボード生成
