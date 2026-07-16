# MCP（Model Context Protocol）設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Model Context Protocol（MCP）は、LLMが外部システム・社内システム・クラウドサービスへ安全かつ標準化された方法でアクセスするためのプロトコルである。

VTaBridge OSでは、AI Agentが各種サービスと連携する際の標準インターフェースとしてMCPを採用する。

---

# 2. 目的

MCP導入目的

- AIと外部サービスの統一接続
- AI Agentの拡張性向上
- Tool管理の標準化
- Function Callingの簡素化
- セキュリティ向上
- ベンダーロックイン回避

---

# 3. アーキテクチャ

```
User

↓

AI Chat

↓

GPT-5.5

↓

AI Orchestrator

↓

MCP Client

↓

──────────────────────────────

MCP Server

GitHub

Microsoft 365

Teams

Outlook

SharePoint

Notion

Jira

Backlog

Slack

Google Workspace

──────────────────────────────

↓

Business API

↓

Database
```

---

# 4. MCP Client

役割

- Tool Discovery
- Tool選択
- Tool実行
- 認証
- エラー処理
- レスポンス統合

---

# 5. MCP Server

管理対象

- GitHub
- Microsoft 365
- Teams
- Outlook
- SharePoint
- Azure DevOps
- Slack
- Notion
- Jira
- Backlog
- Google Workspace

---

# 6. Tool一覧

代表Tool

- Search Repository
- Create Issue
- Read Calendar
- Send Mail
- Search Files
- Create Meeting
- Read Document
- Search Wiki
- Create Task
- Send Teams Message

---

# 7. GitHub連携

利用機能

- Repository検索
- Issue取得
- Pull Request取得
- Release取得
- Wiki検索

---

# 8. Microsoft 365連携

利用機能

- Outlook
- Teams
- SharePoint
- OneDrive
- Excel
- Word
- PowerPoint
- Calendar

---

# 9. Google Workspace連携

利用機能

- Gmail
- Calendar
- Drive
- Docs
- Sheets
- Meet

---

# 10. Notion連携

利用機能

- Database検索
- ページ取得
- ドキュメント検索
- 更新履歴取得

---

# 11. Jira・Backlog連携

利用機能

- Issue検索
- Sprint取得
- チケット更新
- コメント追加

---

# 12. Tool Discovery

AIは利用可能なToolを取得する。

取得項目

- Name
- Description
- Input Schema
- Output Schema
- Permission

---

# 13. Tool実行

処理

```
Prompt

↓

Tool選択

↓

Permission確認

↓

Tool実行

↓

JSON取得

↓

LLM回答
```

---

# 14. 認証

認証方式

- OAuth2
- Azure Entra ID
- API Key
- JWT
- Managed Identity

接続先ごとに認証方式を管理する。

---

# 15. 権限制御

実装

- RBAC
- Tool Permission
- User Permission
- Organization Permission

権限外Toolは実行不可とする。

---

# 16. ログ

保存項目

- UserID
- Agent
- MCP Server
- Tool
- Request
- Response
- ResponseTime
- Timestamp

---

# 17. エラー処理

エラー例

```
MCP001

Tool Not Found
```

```
MCP002

Permission Denied
```

```
MCP003

Authentication Failed
```

```
MCP004

Server Timeout
```

リトライはExponential Backoffで最大3回実施する。

---

# 18. Prisma実装方針

Model

```
MCPServer

MCPTool

MCPExecutionLog

MCPPermission
```

Relation

```
User

AIAgent

Organization
```

---

# 19. セキュリティ

実装

- RBAC
- OAuth2
- Prompt Injection対策
- Tool Validation
- Audit Log
- Rate Limit
- TLS通信
- Secret管理(Key Vault)

---

# 20. 性能目標

Tool Discovery

```
500ms以内
```

Tool実行

```
2秒以内
```

AI応答

```
5秒以内
```

---

# 21. 将来拡張

- MCP Registry対応
- Dynamic Tool Discovery
- Remote MCP Server
- Local MCP Server
- Multi MCP Routing
- AI Tool Marketplace
- MCP Workflow
- AI Self Tool Selection
- Enterprise MCP Hub
- Custom MCP Plugin
