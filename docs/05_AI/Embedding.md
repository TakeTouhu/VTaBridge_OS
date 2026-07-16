# Embedding 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Embeddingは、テキスト・ドキュメント・メール・議事録・契約書などのデータをベクトル化し、AIが意味検索（Semantic Search）を実行するための基盤である。

VTaBridge OSではAzure OpenAIのEmbeddingモデルとPostgreSQL(pgvector)、Azure AI Searchを組み合わせて利用する。

---

# 2. 目的

Embeddingを利用する目的

- RAG検索
- 類似案件検索
- 類似エンジニア検索
- FAQ検索
- 社内ナレッジ検索
- 契約書検索
- 提案書検索
- AIマッチング精度向上

---

# 3. アーキテクチャ

```
Document

↓

Chunk

↓

Embedding生成

↓

Vector

↓

pgvector

↓

Azure AI Search

↓

Similarity Search
```

---

# 4. Embedding対象

対象データ

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
- Resume
- Skill

---

# 5. Embeddingモデル

利用モデル

```
text-embedding-3-large
```

用途

- Semantic Search
- Vector Search
- RAG
- Similarity Search

---

# 6. Chunk設計

Chunk Size

```
800 Tokens
```

Overlap

```
150 Tokens
```

Chunk Metadata

- DocumentID
- ChunkID
- Type
- Page
- Source
- Language
- UpdatedAt

---

# 7. ベクトル保存

保存先

```
PostgreSQL

(pgvector)
```

バックアップ

```
Azure AI Search
```

---

# 8. 類似検索

検索方式

- Cosine Similarity
- Hybrid Search
- Semantic Ranking

Top K

```
5
```

Score Threshold

```
0.75
```

---

# 9. Embedding更新

更新タイミング

- 新規登録
- 更新
- 削除
- バッチ更新
- 手動更新

Embeddingは差分更新を基本とする。

---

# 10. バッチ処理

夜間バッチ

実施内容

- 再Embedding
- Index最適化
- 削除データ同期
- 品質チェック

---

# 11. Index設計

Index

```
knowledge_vector

engineer_vector

project_vector

contract_vector

proposal_vector
```

全文検索Indexも併用する。

---

# 12. キャッシュ

Redis

キャッシュ対象

- Query
- Search Result
- Embedding

TTL

```
300秒
```

---

# 13. 性能目標

Embedding生成

```
2秒以内
```

検索時間

```
500ms以内
```

RAG検索

```
3秒以内
```

---

# 14. ログ

保存項目

- UserID
- Query
- VectorID
- SimilarityScore
- ResponseTime
- Token数

---

# 15. セキュリティ

実装

- Entra ID
- RBAC
- ACL
- Document Permission
- Row Level Security

権限外データは検索対象外とする。

---

# 16. Prisma実装方針

Model

```
EmbeddingDocument

EmbeddingChunk

EmbeddingVector
```

Relation

```
Knowledge

Engineer

Project

Company

Contract
```

pgvectorを利用する。

---

# 17. 運用

定期実施

- Index再構築
- Vector再生成
- Embedding品質確認
- Token使用量確認
- Storage監視

---

# 18. 将来拡張

- Multilingual Embedding
- Image Embedding
- Audio Embedding
- Video Embedding
- Graph Embedding
- Cross-Modal Search
- Hybrid Ranking
- AI Re-ranking
- Incremental Embedding
- Vector Compression
