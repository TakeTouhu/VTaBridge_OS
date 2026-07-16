# RAG 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

RAG（Retrieval-Augmented Generation）は、大規模言語モデル（LLM）に対して社内データや業務データを検索・参照させ、より正確で根拠のある回答を生成する仕組みである。

VTaBridge OSでは、Azure AI SearchとPostgreSQL（pgvector）を利用したHybrid Searchを採用する。

---

# 2. 目的

RAGを導入する目的

- ハルシネーションの抑制
- 最新情報の参照
- 社内ナレッジの活用
- 提案品質の向上
- AIマッチング精度向上
- 契約レビュー支援
- FAQ自動回答
- 社内マニュアル検索

---

# 3. アーキテクチャ

```
User

↓

Next.js

↓

AI API

↓

Query Rewrite

↓

Embedding生成

↓

Azure AI Search

↓

Vector Search

↓

Hybrid Search

↓

Top K取得

↓

GPT-5.5

↓

回答生成
```

---

# 4. データソース

RAGで検索対象とするデータ

- エンジニア情報
- スキル情報
- 案件情報
- 顧客情報
- 契約書
- 提案書
- 議事録
- メール
- FAQ
- マニュアル
- ナレッジ記事
- 社内ルール

---

# 5. インデックス構成

Index例

```
engineer-index

project-index

company-index

contract-index

proposal-index

knowledge-index

manual-index
```

---

# 6. 検索方式

採用する検索方式

- Vector Search
- Semantic Search
- Keyword Search
- Hybrid Search

Hybrid Searchを標準とする。

---

# 7. Embedding

Embeddingモデル

```
text-embedding-3-large
```

保存先

```
PostgreSQL (pgvector)

Azure AI Search
```

---

# 8. Chunk設計

チャンクサイズ

```
800 Tokens
```

オーバーラップ

```
150 Tokens
```

Chunk Metadata

- Document ID
- Document Type
- Title
- Page
- Source
- UpdatedAt

---

# 9. Retrieval

Top K

```
5
```

Score Threshold

```
0.75
```

検索結果が閾値未満の場合は「該当情報なし」と判定する。

---

# 10. Query Rewrite

AIが以下を実施する。

- クエリ補完
- 類義語展開
- 表記ゆれ補正
- 英語⇔日本語変換
- 略語展開

---

# 11. Prompt構成

```
System Prompt

↓

Retrieved Context

↓

User Prompt

↓

GPT
```

取得したContextのみを根拠として回答を生成する。

---

# 12. セキュリティ

アクセス制御

- Entra ID
- RBAC
- Document ACL

ユーザー権限に応じて検索対象を制限する。

---

# 13. キャッシュ

Redisを利用する。

キャッシュ対象

- Embedding
- Search Result
- Prompt
- AI Response

TTL

```
300秒
```

---

# 14. ログ

保存項目

- UserID
- Query
- Retrieved Documents
- Score
- Response Time
- Model
- Token数

---

# 15. 性能目標

検索時間

```
500ms以内
```

AI応答時間

```
5秒以内
```

RAG全体

```
8秒以内
```

---

# 16. エラー処理

RAG失敗時

- リトライ
- キャッシュ利用
- キーワード検索へフォールバック
- AIへ検索失敗を通知

---

# 17. Prisma実装方針

Model

```
KnowledgeDocument

KnowledgeChunk

EmbeddingDocument

EmbeddingVector

SearchHistory
```

Relation

```
User

Engineer

Project

Company

Contract
```

全文検索インデックスを設定する。

---

# 18. 将来拡張

- Graph RAG
- Multi Vector Search
- Image RAG
- Video RAG
- Audio RAG
- SQL RAG
- Web RAG
- Agentic RAG
- Knowledge Graph
- Cross Document Reasoning
