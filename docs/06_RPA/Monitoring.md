# RPA Monitoring 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

RPA Monitoringは、VTaBridge OSにおけるRPA基盤全体の監視・可観測性・運用管理を定義する。

Power Automate、Python、Playwright、Scheduler、Workflow、Azure Functions、AI Agentなどの自動化コンポーネントを対象とし、障害の早期検知・性能分析・運用品質向上を実現する。

---

# 2. 目的

Monitoring導入目的

- ジョブ監視
- Queue監視
- エラー検知
- SLA監視
- パフォーマンス分析
- 可用性向上
- 障害通知
- 運用効率化

---

# 3. アーキテクチャ

```
Automation Jobs

↓

OpenTelemetry

↓

Application Insights

↓

Azure Monitor

↓

Log Analytics

↓

Dashboard

↓

Alert

↓

Teams / Outlook / Slack
```

---

# 4. 監視対象

対象

- Scheduler
- Workflow
- Python Worker
- Playwright
- Power Automate
- Azure Functions
- Queue
- AI Agent
- Notification

---

# 5. ジョブ監視

監視項目

- 実行数
- 成功率
- 失敗率
- 平均実行時間
- 同時実行数
- キャンセル数

---

# 6. Queue監視

監視項目

- Queue件数
- 待機時間
- Retry件数
- Dead Letter Queue件数

閾値超過時はアラートを送信する。

---

# 7. Worker監視

監視対象

- Python Worker
- Playwright Worker
- Azure Functions

取得項目

- CPU
- Memory
- 実行時間
- エラー数
- スレッド数

---

# 8. Power Automate監視

取得項目

- Flow実行数
- 成功率
- 失敗率
- 実行時間
- Connectorエラー

---

# 9. Playwright監視

取得項目

- Browser起動時間
- ログイン成功率
- UIエラー数
- スクリーンショット件数

---

# 10. Python監視

取得項目

- Script実行時間
- API呼び出し数
- PDF生成時間
- Excel生成時間
- エラー率

---

# 11. SLA監視

監視項目

- Job Success Rate
- Availability
- Response Time
- Queue Delay
- Retry Rate

SLAを超えた場合は即時通知する。

---

# 12. アラート

通知条件

- Error Rate > 5%
- Queue > 1,000件
- Retry > 3回
- Worker停止
- Job Timeout

通知先

- Teams
- Outlook
- Slack

---

# 13. ダッシュボード

表示項目

- ジョブ数
- 成功率
- エラー率
- Queue件数
- Worker稼働状況
- SLA
- 通知数
- AI実行数

Dashboard APIと連携する。

---

# 14. ログ

保存項目

- JobID
- Worker
- Queue
- Trigger
- Duration
- Status
- Error
- Retry
- Timestamp

AutomationLogへ保存する。

---

# 15. Prisma実装方針

Model

```
AutomationLog

AutomationMetric

AutomationAlert

AutomationPerformance

AutomationHealth
```

Relation

```
AutomationJob

SchedulerJob

Workflow

User
```

---

# 16. セキュリティ

実装

- Azure Entra ID
- RBAC
- TLS通信
- Azure Key Vault
- Audit Log

監視データへのアクセス権限を制御する。

---

# 17. 保持期間

ログ

```
90日
```

メトリクス

```
1年
```

監査ログ

```
7年
```

Azure Monitorの保持ポリシーに従う。

---

# 18. 障害対応

異常検知時

- 自動アラート
- 自動リトライ
- Queue退避
- 管理者通知
- インシデント登録

重大障害時はRPAを一時停止する。

---

# 19. 性能目標

ジョブ開始

```
1秒以内
```

Queue取得

```
300ms以内
```

アラート送信

```
3秒以内
```

ダッシュボード更新

```
5秒以内
```

---

# 20. 将来拡張

- Grafana連携
- Prometheus Exporter
- Azure Fabric連携
- AI異常検知
- AI障害予測
- 自動スケール
- リアルタイム監視画面
- AI運用レポート
- AIキャパシティ予測
- Process Mining連携
