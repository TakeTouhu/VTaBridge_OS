# Power Automate 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Power Automateは、Microsoft 365を中心とした業務自動化を実現するためのRPA基盤である。

VTaBridge OSとMicrosoftサービスを連携し、メール送信・承認フロー・Teams通知・SharePoint同期・Excel処理などを自動化する。

API連携を優先し、Power AutomateはMicrosoftサービスとのオーケストレーションを担当する。

---

# 2. 目的

Power Automate導入目的

- Outlook自動化
- Teams通知
- 承認フロー
- SharePoint同期
- OneDrive同期
- Excel更新
- PDF保存
- 定期レポート配信

---

# 3. アーキテクチャ

```
Business API

↓

Power Automate Flow

↓

Microsoft Graph

↓

────────────────────

Outlook

Teams

SharePoint

OneDrive

Excel

Planner

Approvals

────────────────────

↓

Notification API

↓

Audit Log
```

---

# 4. 利用サービス

対象サービス

- Outlook
- Microsoft Teams
- SharePoint
- OneDrive
- Excel Online
- Planner
- Approvals
- Forms
- Power BI

---

# 5. フロー一覧

| Flow | 内容 |
|------|------|
| Mail Send | メール送信 |
| Teams Notify | Teams通知 |
| Contract Approval | 契約承認 |
| Invoice Notify | 請求通知 |
| OCR Upload | OCR実行 |
| Daily Report | 日次レポート |
| Weekly Report | 週次レポート |
| Monthly Report | 月次レポート |

---

# 6. Outlook連携

実施内容

- メール送信
- 添付ファイル取得
- 添付ファイル保存
- メール分類
- フォルダー振分け
- AI要約実行
- Meeting作成

Mail APIと連携する。

---

# 7. Teams連携

実施内容

- 通知送信
- Adaptive Card送信
- 承認通知
- AI通知
- エラー通知
- レポート通知

Notification APIと連携する。

---

# 8. SharePoint連携

対象

- 契約書
- 提案書
- 履歴書
- 請求書
- マニュアル

登録後はKnowledge Baseへ同期する。

---

# 9. Excel連携

対象

- 売上管理
- 請求一覧
- KPI一覧
- エンジニア一覧

Business API経由でデータ更新を行う。

---

# 10. Approvals

対象

- 契約承認
- 提案承認
- 請求承認
- ユーザー承認

承認結果はBusiness APIへ通知する。

---

# 11. Trigger

対応トリガー

- HTTP Request
- Outlook受信
- SharePoint更新
- Timer
- Teams
- Manual
- Webhook

---

# 12. API連携

呼び出し対象

- Mail API
- Contract API
- Invoice API
- Proposal API
- Notification API
- Dashboard API

認証はJWTを利用する。

---

# 13. ログ

保存項目

- FlowID
- FlowName
- Trigger
- Status
- StartTime
- EndTime
- UserID
- Error

AutomationHistoryへ保存する。

---

# 14. セキュリティ

実装

- Azure Entra ID
- Managed Identity
- Key Vault
- RBAC
- TLS通信

接続情報はPower Automateへ保存しない。

---

# 15. エラー処理

実施内容

- Retry
- Queue登録
- Teams通知
- Mail通知
- Error Log保存

最大3回リトライする。

---

# 16. 性能目標

Flow開始

```
1秒以内
```

メール送信

```
5秒以内
```

通知

```
3秒以内
```

承認開始

```
5秒以内
```

---

# 17. Prisma実装方針

Model

```
AutomationFlow

AutomationExecution

AutomationApproval

AutomationLog
```

Relation

```
User

Contract

Proposal

Invoice

Task
```

Power Automateの実行履歴をAutomationExecutionで管理する。

---

# 18. 将来拡張

- Power Apps連携
- Microsoft Fabric連携
- Copilot Studio連携
- Dynamics 365連携
- Planner双方向同期
- Loop連携
- Viva連携
- AI Agent連携強化
- Power Platform Center of Excellence対応
- カスタムコネクタ対応
