# Knowledge Base 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Knowledge Base（ナレッジベース）は、VTaBridge OSにおけるAIの知識基盤である。

社内文書・契約書・提案書・FAQ・マニュアル・議事録などを一元管理し、RAGの検索対象として利用する。

Azure AI SearchとEmbeddingを組み合わせ、高精度な検索を実現する。

---

# 2. 目的

Knowledge Baseを利用する目的

- AI回答精度向上
- ナレッジ共有
- 属人化防止
- FAQ自動回答
- 社内検索
- AI営業支援
- AI契約レビュー
- AIマッチング支援

---

# 3. アーキテクチャ

```
Document

↓

Document Parser

↓

Chunk

↓

Embedding

↓

Knowledge DB

↓

Azure AI Search

↓

RAG

↓

GPT-5.5
```

---

# 4. 管理対象

対象ドキュメント

- FAQ
- 社内マニュアル
- 提案書
- 契約書
- 見積書
- 仕様書
- 議事録
- メール
- プロジェクト資料
- 人事資料
- 技術記事
- 社内ルール

---

# 5. ドキュメント形式

対応形式

- PDF
- Word
- Excel
- PowerPoint
- TXT
- Markdown
- HTML
- CSV
- JSON

---

# 6. ドキュメント情報

管理項目

- DocumentID
- Title
- Category
- Owner
- Department
- Tags
- Language
- Status
- CreatedAt
- UpdatedAt

---

# 7. カテゴリ

| Category | 内容 |
|-----------|------|
| Manual | マニュアル |
| FAQ | FAQ |
| Contract | 契約書 |
| Proposal | 提案書 |
| Meeting | 議事録 |
| Technical | 技術資料 |
| HR | 人事 |
| Sales | 営業 |
| Project | プロジェクト |
| Company | 社内情報 |

---

# 8. タグ

例

```
React

Java

AWS

SES

営業

契約

請求

AI

Azure

Microsoft
```

複数タグを設定可能とする。

---

# 9. 検索

対応

- Keyword Search
- Semantic Search
- Vector Search
- Hybrid Search

検索条件

- Category
- Tag
- Department
- Language
- UpdatedDate

---

# 10. 更新

更新方法

- 手動登録
- API登録
- RPA登録
- SharePoint同期
- OneDrive同期
- GitHub同期

---

# 11. AI利用

AIが利用する用途

- RAG検索
- FAQ回答
- 契約レビュー
- 提案書生成
- 社内検索
- マッチング支援
- 要約
- 翻訳

---

# 12. 権限管理

アクセス制御

- Entra ID
- RBAC
- Department
- Project
- Document ACL

権限のない文書は検索対象外とする。

---

# 13. バージョン管理

保存内容

- Version
- Editor
- UpdatedAt
- ChangeLog

過去バージョンを保持する。

---

# 14. インデックス

Azure AI Search

Index例

```
knowledge-index

faq-index

manual-index

proposal-index

contract-index
```

---

# 15. Prisma実装方針

Model

```
KnowledgeDocument

KnowledgeCategory

KnowledgeTag

KnowledgeVersion

KnowledgeAttachment
```

Relation

```
User

Department

Project
```

---

# 16. ログ

保存項目

- UserID
- Search Query
- Open Document
- Download
- AI利用有無
- Timestamp

---

# 17. 性能目標

検索時間

```
500ms以内
```

ドキュメント登録

```
10秒以内
```

RAG応答

```
5秒以内
```

---

# 18. セキュリティ

実装

- Entra ID認証
- RBAC
- Row Level Security
- Document ACL
- PIIマスキング
- 監査ログ

---

# 19. バックアップ

保存先

- Azure Blob Storage
- Azure Backup

バックアップ

- 毎日
- 世代管理
- リストア対応

---

# 20. 将来拡張

- AI自動タグ付け
- AIカテゴリ分類
- AI要約生成
- AI重複文書検出
- AIナレッジ推薦
- SharePoint双方向同期
- Confluence連携
- Notion連携
- GitHub Wiki連携
- Graph RAG対応
