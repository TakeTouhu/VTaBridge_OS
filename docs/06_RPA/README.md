# RPA設計

Version: 1.0

Status: Draft

---

# 概要

本ディレクトリでは、VTaBridge OSのRPA（Robotic Process Automation）基盤を設計する。

Power Automate、Python、Playwright、定期ジョブ、AI Agentと連携し、営業・採用・契約・請求・通知などの業務を自動化する。

---

# 設計一覧

| No | ファイル | 内容 |
|----|---------|------|
| 01 | RPAArchitecture.md | RPA全体アーキテクチャ |
| 02 | PowerAutomate.md | Power Automate設計 |
| 03 | Playwright.md | Playwright設計 |
| 04 | PythonAutomation.md | Python自動化設計 |
| 05 | Scheduler.md | スケジューラー設計 |
| 06 | Workflow.md | ワークフロー設計 |
| 07 | Notification.md | 通知自動化 |
| 08 | Monitoring.md | RPA監視設計 |
| 09 | Security.md | RPAセキュリティ |
| 10 | ErrorHandling.md | エラー処理設計 |

---

# 利用技術

- Microsoft Power Automate
- Python
- Playwright
- Azure Functions
- Azure Logic Apps
- Azure Storage Queue
- Azure Service Bus
- Azure Monitor

---

# 自動化対象

- メール送信
- Outlook連携
- Teams通知
- 請求書生成
- PDF生成
- OCR実行
- データ同期
- 定期レポート
- 契約期限通知
- AI Agent実行

---

# RPA基本方針

- API連携を最優先とする
- GUI操作は最終手段とする
- AI Agentと連携可能とする
- ログを必ず保存する
- エラー時は自動復旧を試行する

---

# ディレクトリ構成

```
06_RPA/

├── README.md
├── RPAArchitecture.md
├── PowerAutomate.md
├── Playwright.md
├── PythonAutomation.md
├── Scheduler.md
├── Workflow.md
├── Notification.md
├── Monitoring.md
├── Security.md
└── ErrorHandling.md
```

---

# 更新履歴

| Version | Date | 内容 |
|----------|------|------|
| 1.0 | 2026-07 | 初版 |
