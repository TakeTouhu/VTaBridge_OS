# AI Architecture

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

AI Architectureでは、VTaBridge OS全体のAI基盤アーキテクチャを定義する。

システム内のすべてのAI機能は、本アーキテクチャを経由して利用する。

Azure OpenAI Serviceを中心に、RAG・Embedding・AI Agent・OCR・Speech・Function Calling・MCPを統合する。

---

# 2. アーキテクチャ全体

```
                        User
                         │
                 Next.js Frontend
                         │
                  API Gateway(BFF)
                         │
                AI Orchestrator API
                         │
 ┌──────────────────────────────────────────────┐
 │                                              │
 │ Azure OpenAI                                │
 │ GPT-5.5                                     │
 │ GPT-5.5 mini                                │
 │                                              │
 └──────────────────────────────────────────────┘
                         │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼

   Azure AI Search   Function Calling   AI Agent

        │               │               │

        ▼               ▼               ▼

  Knowledge Base     Internal APIs     MCP Server

        │

        ▼

 PostgreSQL + pgvector

        │

        ▼

 Azure Blob Storage
```

---

# 3. AI構成要素

| Component | 説明 |
|------------|------|
| Azure OpenAI | LLM |
| Azure AI Search | RAG検索 |
| PostgreSQL | 業務データ |
| pgvector | ベクトル検索 |
| Blob Storage | ファイル保存 |
| AI Agent | 自律実行 |
| Function Calling | API呼び出し |
| MCP | 外部AI連携 |

---

# 4. AI利用フロー

```
ユーザー

↓

Next.js

↓

AI API

↓

Prompt生成

↓

RAG検索

↓

Embedding検索

↓

Azure OpenAI

↓

Function Calling

↓

DB検索

↓

AI回答生成

↓

ユーザーへ返却
```

---

# 5. AIサービス

提供するAIサービス

- AI Chat
- AI Search
- AI Summary
- AI Translation
- AI Proposal
- AI Resume
- AI Matching
- AI Meeting
- AI Mail
- AI OCR
- AI Speech
- AI Dashboard

---

# 6. AIモデル

| 用途 | モデル |
|------|---------|
| 高品質チャット | GPT-5.5 |
| 高速応答 | GPT-5.5 mini |
| Embedding | text-embedding-3-large |
| OCR | Azure AI Document Intelligence |
| 音声 | Azure AI Speech |

---

# 7. RAG構成

検索対象

- Engineer
- Project
- Company
- Contract
- Proposal
- Meeting
- Mail
- FAQ
- Knowledge
- Manual

検索方法

- Hybrid Search
- Semantic Search
- Vector Search

---

# 8. AI Agent

Agent一覧

- Sales Agent
- Recruit Agent
- HR Agent
- Finance Agent
- Legal Agent
- Support Agent
- Dashboard Agent
- RPA Agent

---

# 9. Function Calling

AIから呼び出すAPI

- Engineer Search
- Project Search
- Customer Search
- Company Search
- Contract Search
- Mail Send
- Meeting Create
- Proposal Generate
- Dashboard Get

---

# 10. MCP

対応予定

- Microsoft 365
- GitHub
- Slack
- Teams
- Notion
- Jira
- Backlog
- Google Workspace

---

# 11. セキュリティ

実装内容

- Azure Entra ID認証
- RBAC
- Prompt Injection対策
- PIIマスキング
- Token制限
- Rate Limit
- Content Filter
- Input Validation

---

# 12. AIログ

保存する情報

- UserID
- Prompt
- Response
- Model
- Tokens
- Latency
- Cost
- Timestamp

---

# 13. キャッシュ

Redisを利用する。

対象

- Prompt Cache
- Embedding Cache
- AI Response Cache

TTL

```
300秒
```

---

# 14. 可観測性

Azure Monitor

Application Insights

OpenTelemetry

Grafana

監視項目

- Token数
- レスポンス時間
- エラー率
- API呼び出し数
- AI利用率

---

# 15. 可用性

目標

- SLA 99.9%

冗長化

- Multi AZ
- Azure OpenAI Failover
- Redis Replica
- PostgreSQL HA

---

# 16. 将来拡張

- Multi LLM
- Claude
- Gemini
- Grok
- DeepSeek
- ローカルLLM対応
- AI Workflow
- Multi Agent
- Voice Agent
- Video Agent
- AI自律実行
- AIコード生成
- AIデータ分析
- AI BI
