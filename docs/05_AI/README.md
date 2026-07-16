# AI設計

Version: 1.0

Status: Draft

---

# 概要

本ディレクトリでは、VTaBridge OSのAI機能全体の設計を管理する。

Azure OpenAI Serviceを中核とし、RAG・Embedding・AI Agent・OCR・音声認識・プロンプト管理・Function Calling・MCPなど、AI基盤に関する設計を定義する。

---

# 設計一覧

| No | ファイル | 内容 |
|----|---------|------|
| 01 | AIArchitecture.md | AI全体アーキテクチャ |
| 02 | AzureOpenAI.md | Azure OpenAI設計 |
| 03 | PromptDesign.md | プロンプト設計 |
| 04 | RAG.md | RAG設計 |
| 05 | Embedding.md | Embedding設計 |
| 06 | KnowledgeBase.md | ナレッジベース設計 |
| 07 | FunctionCalling.md | Function Calling設計 |
| 08 | AIAgent.md | AI Agent設計 |
| 09 | MCP.md | MCP対応設計 |
| 10 | OCR.md | OCR設計 |
| 11 | Speech.md | 音声認識設計 |
| 12 | Translation.md | 翻訳設計 |
| 13 | Security.md | AIセキュリティ設計 |
| 14 | Monitoring.md | AI監視設計 |

---

# 利用サービス

- Azure OpenAI
- Azure AI Search
- Azure AI Document Intelligence
- Azure AI Speech
- Azure Blob Storage
- Azure Key Vault
- Azure Monitor

---

# AI機能

- AIチャット
- AI営業支援
- AIマッチング
- AI議事録
- AIメール作成
- AI提案書作成
- AI契約レビュー
- AI翻訳
- AI OCR
- AI Agent
- RAG検索

---

# 採用技術

- GPT-5.5
- GPT-5.5 mini
- text-embedding-3-large
- Azure AI Search
- LangChain
- Semantic Kernel
- MCP
- OpenTelemetry

---

# ディレクトリ構成

```
05_AI/

├── README.md
├── AIArchitecture.md
├── AzureOpenAI.md
├── PromptDesign.md
├── RAG.md
├── Embedding.md
├── KnowledgeBase.md
├── FunctionCalling.md
├── AIAgent.md
├── MCP.md
├── OCR.md
├── Speech.md
├── Translation.md
├── Security.md
└── Monitoring.md
```

---

# 開発方針

- Azure OpenAI Serviceを標準採用
- RAGを前提とする
- AI Agent化を前提とする
- MCP対応を前提とする
- マルチモデル対応
- AI利用ログを保存する
- セキュリティを最優先とする

---

# 更新履歴

| Version | Date | 内容 |
|----------|------|------|
| 1.0 | 2026-07 | 初版 |
