# Dashboard 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Dashboardは、VTaBridge OSへログイン後に最初に表示されるホーム画面である。

営業活動・案件・エンジニア・売上・AI・通知・タスクなど、業務に必要な情報をリアルタイムで可視化し、ユーザーが迅速に意思決定できる環境を提供する。

ロールに応じて表示内容を切り替える。

---

# 2. 目的

Dashboard導入目的

- KPI可視化
- 業務状況把握
- AIインサイト表示
- タスク確認
- 通知確認
- 売上分析
- 案件分析
- 業務効率向上

---

# 3. 画面構成

```
Header

↓

KPI Cards

↓

Charts

↓

AI Insight

↓

Task

↓

Notification

↓

Recent Activity
```

---

# 4. KPIカード

表示項目

- 売上
- 粗利
- 稼働中エンジニア数
- 案件数
- 契約数
- 未請求件数
- 未入金件数
- タスク件数

カードクリックで詳細画面へ遷移する。

---

# 5. チャート

表示

- 月別売上推移
- 案件推移
- エンジニア稼働率
- 契約推移
- AI利用状況
- 売上ランキング

Rechartsを利用する。

---

# 6. AI Insight

AI Agentが分析結果を表示する。

例

- 売上予測
- 契約更新提案
- 人材不足予測
- 営業改善提案
- リスク案件
- KPI異常検知

詳細画面へ遷移可能とする。

---

# 7. タスク

表示

- 今日のタスク
- 今週期限
- 承認待ち
- 自分の担当
- AI提案タスク

Task APIと連携する。

---

# 8. 通知

表示

- Workflow通知
- 契約期限
- 請求期限
- AI通知
- システム通知

未読件数を表示する。

---

# 9. 最近の活動

表示

- 商談
- 契約
- 案件更新
- AI利用履歴
- Workflow実行履歴

時系列で表示する。

---

# 10. クイックアクション

表示

- 新規案件
- 新規エンジニア
- 新規顧客
- AIチャット
- 契約作成
- 請求書作成

ワンクリックで実行可能とする。

---

# 11. フィルター

対応

- 日付
- 部署
- 担当者
- 顧客
- プロジェクト

フィルター結果をチャート・KPIへ反映する。

---

# 12. API

```
GET

/api/v1/dashboard
```

```
GET

/api/v1/dashboard/kpi
```

```
GET

/api/v1/dashboard/chart
```

```
GET

/api/v1/dashboard/activity
```

Dashboard APIを利用する。

---

# 13. UIコンポーネント

利用

- Card
- Table
- Tabs
- Chart
- Badge
- Avatar
- Scroll Area
- Tooltip

shadcn/uiを利用する。

---

# 14. 状態表示

対応

- Loading
- Empty
- Error
- Success

KPIはSkeleton表示を採用する。

---

# 15. パフォーマンス

実施

- Server Components
- Streaming
- Lazy Loading
- Cache
- TanStack Query

KPIを優先表示する。

---

# 16. レスポンシブ

Desktop

```
4列表示
```

Tablet

```
2列表示
```

Mobile

```
1列表示
```

チャートは画面幅に応じて自動調整する。

---

# 17. アクセシビリティ

対応

- キーボード操作
- Focus表示
- ARIA属性
- WCAG 2.2 AA

---

# 18. セキュリティ

実装

- RBAC
- 部署別表示制御
- API認可
- HTTPS

ロールごとに表示するKPIを変更する。

---

# 19. 将来拡張

- カスタムダッシュボード
- ドラッグ＆ドロップ配置
- AIダッシュボード生成
- ウィジェット追加
- Power BI埋め込み
- リアルタイム更新
- 個人設定保存
- KPIアラート
- AIレポート自動生成
- マルチテナント対応
