# Azure OpenAI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Azure OpenAI Serviceは、VTaBridge OSのAI基盤となるサービスである。

チャット、RAG、要約、翻訳、議事録生成、AIマッチングなど、すべてのAI機能はAzure OpenAI Serviceを経由して実行する。

Azure環境内で完結する構成とし、セキュリティ・可用性・監査性を重視する。

---

# 2. システム構成

```
User

↓

Next.js

↓

API Gateway

↓

AI API

↓

Azure OpenAI

↓

GPT-5.5
GPT-5.5 mini

↓

Response
```

---

# 3. デプロイ構成

Azure OpenAI Resource

```
Production

Staging

Development
```

各環境ごとにResourceを分離する。

---

# 4. モデル構成

| 用途 | モデル |
|------|---------|
| AIチャット | GPT-5.5 |
| 高速応答 | GPT-5.5 mini |
| Embedding | text-embedding-3-large |

---

# 5. AI利用機能

Azure OpenAIを利用する機能

- AIチャット
- AI営業支援
- AIマッチング
- AIメール生成
- AI議事録生成
- AI翻訳
- AI要約
- AI契約レビュー
- AI提案書生成
- AI検索（RAG）

---

# 6. API構成

```
POST

/api/v1/ai/chat

POST

/api/v1/ai/summary

POST

/api/v1/ai/matching

POST

/api/v1/ai/search

POST

/api/v1/ai/translate
```

---

# 7. Token管理

保存項目

- Prompt Tokens
- Completion Tokens
- Total Tokens
- UserID
- Model
- Endpoint
- Cost
- Response Time

---

# 8. モデル選択

AI APIが自動選択する。

GPT-5.5

用途

- 高品質回答
- 契約レビュー
- 提案書
- RAG

GPT-5.5 mini

用途

- チャット
- 要約
- 翻訳
- メール
- OCR後処理

---

# 9. Rate Limit

制御対象

- User
- Organization
- API Key

制限

- Request / Minute
- Token / Minute
- Concurrent Request

---

# 10. Retry

失敗時

最大

```
3回
```

Retry

```
Exponential Backoff
```

---

# 11. Timeout

標準

```
60秒
```

Streaming時

```
180秒
```

---

# 12. Streaming

対応

- Chat
- Summary
- Translation
- Proposal

SSEを利用する。

---

# 13. Security

実装

- Azure Entra ID
- Managed Identity
- Key Vault
- HTTPS Only
- Private Endpoint
- RBAC

API Keyをアプリへ保存しない。

---

# 14. Prompt管理

保存

```
PromptMaster
```

Version管理

変更履歴

利用履歴

A/Bテスト

---

# 15. ログ

保存項目

- Prompt
- Response
- Model
- Token数
- Cost
- User
- Latency
- Error

---

# 16. 監視

Azure Monitor

Application Insights

Log Analytics

監視項目

- エラー率
- Token利用量
- レスポンス時間
- Cost
- API回数

---

# 17. コスト管理

管理項目

- User別
- 部署別
- 月別
- モデル別
- API別

AI利用料金をダッシュボードへ表示する。

---

# 18. フェイルオーバー

Primary Region

↓

Secondary Region

自動切替を行う。

---

# 19. Prisma実装方針

Model

```
AIUsageLog

AIPrompt

AIConversation

AIModel

AITokenUsage
```

---

# 20. 将来拡張

- GPT-6対応
- Claude連携
- Gemini連携
- Grok連携
- DeepSeek連携
- Azure AI Foundry対応
- Fine-tuning対応
- Prompt Flow対応
- AI Workflow対応
- Multi LLM Routing
