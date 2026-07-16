# Function Calling 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Function Callingは、VTaBridge OSのAIが外部システム・業務API・データベース・Workflow・MCPツールなどを安全かつ正確に呼び出すための設計を定義する。

Azure OpenAI Function Calling・Structured Outputs・Model Context Protocol（MCP）を活用し、AIが業務機能を安全に実行できるアーキテクチャを実現する。

---

# 2. 目的

Function Calling導入目的

- AIと業務システムの連携
- AIによる業務自動化
- Function利用の標準化
- 安全なツール実行
- AI品質向上
- 監査性向上

---

# 3. 基本方針

採用方針

- Tool First
- Structured Output
- Least Privilege
- Zero Trust
- Human Approval（必要時）
- Audit First

AIは許可されたFunctionのみ実行可能とする。

---

# 4. 対象Function

対象

- 顧客検索
- 案件検索
- エンジニア検索
- Workflow起動
- Outlookメール送信
- Teams通知
- OCR実行
- AI Search
- PostgreSQL検索
- GitHub操作

---

# 5. アーキテクチャ

```
User

↓

AI Model

↓

Function Calling

↓

MCP Server

↓

Business API

↓

Database / External Service
```

FunctionはMCP ServerまたはBusiness API経由で実行する。

---

# 6. Function定義

管理項目

- Function ID
- Name
- Description
- Input Schema
- Output Schema
- Permission
- Timeout
- Version

JSON Schemaで標準化する。

---

# 7. Input Validation

確認項目

- 型チェック
- 必須項目
- 最大文字数
- Enum
- Pattern
- Range

入力値を実行前に検証する。

---

# 8. Output Validation

確認項目

- JSON Schema
- 必須項目
- 型
- Nullチェック
- データ整合性

不正なレスポンスを防止する。

---

# 9. 権限制御

実施

- RBAC
- Scope Validation
- Tool Permission
- User Permission
- Resource Ownership

利用者ごとに実行可能なFunctionを制御する。

---

# 10. Human Approval

承認対象

- 契約更新
- メール送信
- データ削除
- 支払処理
- ワークフロー承認

高リスク操作は人による承認を必須とする。

---

# 11. エラーハンドリング

対応

- Retry
- Timeout
- Fallback
- Validation Error
- Permission Error

エラー内容を標準化して返却する。

---

# 12. Retry Policy

設定例

- 最大3回
- Exponential Backoff
- Timeout：30秒

一時的な障害時のみ再試行する。

---

# 13. タイムアウト

標準値

| Function | Timeout |
|----------|---------|
| Database | 10秒 |
| AI Search | 15秒 |
| Workflow | 30秒 |
| Outlook | 20秒 |
| GitHub | 30秒 |

用途に応じて設定する。

---

# 14. 監査ログ

取得項目

- User ID
- Function Name
- Parameter
- Result
- Execution Time
- Status
- Correlation ID

すべてのFunction実行を記録する。

---

# 15. セキュリティ

実施

- Managed Identity
- OAuth2
- RBAC
- Input Validation
- Output Validation
- Secretless Architecture

認証・認可されたFunctionのみ実行する。

---

# 16. KPI

管理項目

- Function成功率
- Retry率
- Error率
- Timeout率
- 平均実行時間
- Human Approval件数

継続的に評価する。

---

# 17. ベストプラクティス

- Functionは単一責務とする
- JSON Schemaを必須とする
- 実行前に入力値を検証する
- 監査ログを取得する
- 高リスクFunctionは承認制とする

---

# 18. 運用

実施内容

- Functionレビュー
- 権限棚卸し
- スキーマ更新
- KPI分析
- ログ監査

継続的にFunction品質を改善する。

---

# 19. 関連ドキュメント

関連

- Agent Architecture
- MCP
- Prompt Engineering
- Security Architecture
- API Protection

Function基盤全体で整合性を維持する。

---

# 20. 将来拡張

- Dynamic Tool Discovery
- Tool Registry
- Tool Marketplace
- Parallel Function Calling
- AI Tool Selection
- Function Analytics Dashboard
- Tool Health Monitoring
- Continuous Function Validation
- Autonomous Tool Orchestration
- Self-Healing Function Execution
