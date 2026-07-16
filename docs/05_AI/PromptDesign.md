# Prompt Design

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Prompt Designでは、VTaBridge OSで利用するすべてのAIプロンプトの設計・管理方法を定義する。

プロンプトはシステムに直接記述せず、テンプレートとして一元管理する。

Azure OpenAI・RAG・AI Agent・Function Callingはすべて本設計に従う。

---

# 2. 目的

本設計の目的

- AI品質の標準化
- 回答精度向上
- プロンプト管理
- バージョン管理
- A/Bテスト
- メンテナンス性向上
- ハルシネーション抑制

---

# 3. プロンプト構成

すべてのプロンプトは以下の構成とする。

```
System Prompt

↓

Developer Prompt

↓

Retrieved Context（RAG）

↓

User Prompt

↓

Function Result

↓

LLM
```

---

# 4. System Prompt

役割

AIの基本ルールを定義する。

例

```
あなたはVTaBridge OSのAIアシスタントです。

回答は必ず業務データを優先してください。

不明な情報は推測せず、

「情報が見つかりません」

と回答してください。
```

---

# 5. Developer Prompt

役割

業務ごとのルールを定義する。

例

営業支援

```
営業担当者向けに提案してください。
```

契約レビュー

```
法律上のリスクを列挙してください。
```

AIマッチング

```
スキル一致率を優先してください。
```

---

# 6. User Prompt

ユーザー入力

例

```
React案件に最適なエンジニアを探してください。
```

---

# 7. RAG Context

検索結果を自動追加する。

例

```
Engineer A

React 6年

Node.js 5年

AWS

日本語N1
```

ContextはSystem Promptより後に追加する。

---

# 8. Function Calling

AIが必要に応じてAPIを呼び出す。

例

```
Engineer Search

Project Search

Contract Search

Meeting Create

Mail Send
```

---

# 9. Prompt Template

Promptはテンプレートとして管理する。

項目

- TemplateID
- Name
- Category
- Version
- Prompt
- Variables
- Status

---

# 10. Prompt Variables

変数例

```
{{EngineerName}}

{{CompanyName}}

{{ProjectName}}

{{Skill}}

{{Language}}
```

実行時に値を展開する。

---

# 11. Version管理

管理項目

- Version
- Author
- CreatedAt
- UpdatedAt
- Description

旧バージョンは削除しない。

---

# 12. Promptカテゴリ

| Category | 用途 |
|----------|------|
| Chat | AIチャット |
| Proposal | 提案書生成 |
| Resume | 履歴書分析 |
| Matching | マッチング |
| Meeting | 議事録 |
| Mail | メール作成 |
| Contract | 契約レビュー |
| Translation | 翻訳 |
| OCR | OCR補正 |
| Dashboard | 分析 |

---

# 13. Guardrails

禁止事項

- ハルシネーション
- 個人情報漏洩
- 権限外データ参照
- 差別的表現
- 不適切な出力
- 根拠のない推測

---

# 14. Few-shot Learning

必要に応じてExampleを追加する。

```
Input

↓

Expected Output

↓

Input

↓

Expected Output

↓

User Prompt
```

---

# 15. Token最適化

実施内容

- 不要なContext除外
- Chunk最適化
- Prompt圧縮
- Few-shot数制限

Token数を最適化する。

---

# 16. 評価

評価項目

- 正確性
- 一貫性
- 回答速度
- Token数
- ユーザー評価
- ハルシネーション率

---

# 17. Prisma実装方針

Model

```
PromptTemplate

PromptVersion

PromptExecutionLog
```

Relation

```
User

AIConversation
```

PromptTemplateをマスターとして管理する。

---

# 18. AI利用ログ

保存項目

- PromptID
- PromptVersion
- UserID
- Model
- InputTokens
- OutputTokens
- TotalTokens
- ResponseTime
- Cost

---

# 19. セキュリティ

実装内容

- Prompt編集権限管理
- RBAC
- Prompt監査ログ
- Prompt暗号化
- Key Vault連携
- PIIマスキング

---

# 20. 将来拡張

- Prompt Workflow
- Dynamic Prompt
- Self-Reflection Prompt
- Automatic Prompt Optimization
- Prompt A/B Testing
- Prompt Marketplace
- Multi Agent Prompt
- Prompt評価AI
- Promptテンプレート共有
- Prompt自動改善
