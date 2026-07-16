# AI Agent 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

AI Agentは、VTaBridge OSにおいて業務を自律的に支援・実行するAIエージェント群である。

各Agentは専門分野ごとの知識・権限・Function Callingを持ち、必要に応じて複数Agentが連携しながら業務を遂行する。

AI AgentはLLM単体ではなく、RAG・Function Calling・MCP・Workflowを組み合わせた構成とする。

---

# 2. 目的

AI Agentを導入する目的

- 営業支援
- 採用支援
- SESマッチング
- 契約レビュー
- メール自動化
- タスク自動化
- AIによる業務効率化
- 人的作業削減

---

# 3. アーキテクチャ

```
User

↓

AI Chat

↓

AI Orchestrator

↓

────────────────────────

Sales Agent

Recruit Agent

Legal Agent

Finance Agent

Project Agent

Support Agent

Dashboard Agent

RPA Agent

────────────────────────

↓

Function Calling

↓

Business API

↓

Database

↓

Response
```

---

# 4. AI Orchestrator

AI Orchestratorは各Agentを統括する。

役割

- Agent選択
- Task分割
- Prompt生成
- Function実行
- 結果統合
- ログ保存

---

# 5. Agent一覧

| Agent | 役割 |
|---------|------|
| Sales Agent | 営業支援 |
| Recruit Agent | 採用支援 |
| Matching Agent | AIマッチング |
| Legal Agent | 契約レビュー |
| Finance Agent | 請求・入金分析 |
| Project Agent | 案件管理 |
| Meeting Agent | 議事録作成 |
| Mail Agent | メール生成 |
| Dashboard Agent | KPI分析 |
| Support Agent | 社内QA |
| RPA Agent | 業務自動化 |

---

# 6. Sales Agent

機能

- 営業メール作成
- 提案書生成
- 顧客分析
- 商談要約
- 次回アクション提案
- 営業レポート生成

利用API

- Customer API
- Company API
- Proposal API
- Mail API
- Dashboard API

---

# 7. Recruit Agent

機能

- エンジニア検索
- スキル分析
- AIマッチング
- 履歴書分析
- 面接質問生成
- 人材推薦

利用API

- Engineer API
- Project API
- Matching API

---

# 8. Legal Agent

機能

- 契約レビュー
- 契約比較
- リスク分析
- 条項要約
- 更新期限通知

利用API

- Contract API

---

# 9. Finance Agent

機能

- 売上分析
- 請求分析
- 入金分析
- 未収金分析
- キャッシュフロー分析

利用API

- Invoice API
- Payment API
- Dashboard API

---

# 10. Project Agent

機能

- 案件分析
- 要員提案
- タスク生成
- リスク分析
- 進捗分析

利用API

- Project API
- Task API
- Engineer API

---

# 11. Agent連携

複数Agentが協調動作する。

例

```
Sales Agent

↓

Recruit Agent

↓

Matching Agent

↓

Proposal Agent

↓

Mail Agent
```

---

# 12. Function Calling

各Agentは以下のみ利用可能。

- Business API
- RAG
- MCP
- Internal Function

DBへ直接アクセスしない。

---

# 13. RAG利用

検索対象

- Knowledge Base
- FAQ
- Manual
- Proposal
- Contract
- Meeting
- Mail

検索後にLLMへ渡す。

---

# 14. MCP利用

接続先

- GitHub
- Microsoft 365
- Teams
- Outlook
- SharePoint
- Slack
- Notion

---

# 15. Agent Memory

保存項目

- Conversation
- User Preference
- Task History
- Agent State
- Workflow

長期記憶はKnowledge Baseへ保存する。

---

# 16. セキュリティ

実装

- RBAC
- Agent Permission
- Function Permission
- Prompt Guard
- PII Masking
- Audit Log

---

# 17. ログ

保存項目

- UserID
- Agent
- Prompt
- Function
- Response
- Tokens
- Cost
- ResponseTime

---

# 18. Prisma実装方針

Model

```
AIAgent

AIAgentExecution

AIAgentMemory

AIAgentWorkflow
```

Relation

```
User

Project

Meeting

AIConversation
```

---

# 19. 性能目標

Agent選択

```
300ms以内
```

Function実行

```
1秒以内
```

AI回答

```
5秒以内
```

---

# 20. 将来拡張

- Multi Agent Collaboration
- Supervisor Agent
- Planner Agent
- Code Agent
- Data Analyst Agent
- Voice Agent
- Video Agent
- Human Approval Agent
- Autonomous Workflow
- Self Learning Agent
