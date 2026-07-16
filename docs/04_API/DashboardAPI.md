# Dashboard API

Version: 1.0

Status: Draft

Priority: ★★★★★ (Core API)

---

# 1. 概要

Dashboard APIは、VTaBridge OS全体のKPI・統計情報・分析データを提供するAPIである。

営業活動、案件、エンジニア、契約、売上、AI利用状況をリアルタイムで可視化し、経営判断・営業戦略・人材管理を支援する。

---

# 2. API一覧

| Method | Endpoint | 説明 |
|---------|----------|------|
| GET | /api/v1/dashboard | ダッシュボード取得 |
| GET | /api/v1/dashboard/sales | 売上分析 |
| GET | /api/v1/dashboard/projects | 案件分析 |
| GET | /api/v1/dashboard/engineers | エンジニア分析 |
| GET | /api/v1/dashboard/contracts | 契約分析 |
| GET | /api/v1/dashboard/invoices | 請求分析 |
| GET | /api/v1/dashboard/payments | 入金分析 |
| GET | /api/v1/dashboard/ai | AI利用分析 |
| GET | /api/v1/dashboard/kpi | KPI取得 |

---

# 3. ダッシュボード取得

GET

```
/api/v1/dashboard
```

Response

```json
{
  "sales": {},
  "projects": {},
  "engineers": {},
  "contracts": {},
  "payments": {},
  "ai": {}
}
```

---

# 4. 売上分析

GET

```
/api/v1/dashboard/sales
```

Response

```json
{
  "monthlySales": 125000000,
  "monthlyProfit": 42000000,
  "salesGrowth": 18.2,
  "targetAchievement": 92.5
}
```

---

# 5. 案件分析

取得項目

- 募集中案件数
- 成約案件数
- 失注案件数
- 平均成約率
- 業界別案件数
- 営業担当別案件数

---

# 6. エンジニア分析

取得項目

- 登録人数
- 稼働人数
- 待機人数
- 国別人数
- スキルランキング
- 平均単価
- AIマッチ率

---

# 7. 契約分析

取得項目

- 契約件数
- 更新率
- 解約率
- 契約金額
- 契約期間

---

# 8. AI分析

取得項目

- AI利用回数
- Token使用量
- 利用ユーザー数
- AI利用ランキング
- モデル利用率
- AI処理時間

---

# 9. KPI

主要KPI

- 売上
- 粗利
- 成約率
- 稼働率
- 平均単価
- 平均契約期間
- AI利用率
- 顧客満足度

---

# 10. グラフ

対応

- Line Chart
- Bar Chart
- Pie Chart
- Doughnut Chart
- Heatmap
- KPI Card

---

# 11. Permission

| Permission |
|------------|
| dashboard.read |
| dashboard.admin |
| admin.all |

---

# 12. Error Code

| Code | 内容 |
|------|------|
| DASH001 | Dashboard Not Available |
| DASH002 | KPI Error |
| DASH003 | Analytics Error |
| DASH004 | Permission Denied |

---

# 13. OpenAPI

```yaml
paths:

  /dashboard:

    get:
      summary: Dashboard

  /dashboard/sales:

    get:
      summary: Sales Dashboard

  /dashboard/projects:

    get:
      summary: Project Dashboard

  /dashboard/engineers:

    get:
      summary: Engineer Dashboard

  /dashboard/ai:

    get:
      summary: AI Dashboard
```

---

# 14. Prisma実装方針

Dashboard専用テーブルは作成しない。

以下のModelから集計する。

```
Company

Project

Engineer

Contract

Invoice

Payment

AIUsageLog

Meeting

Task
```

Redisを利用してキャッシュする。

---

# 15. キャッシュ

Redis

TTL

```
300秒
```

リアルタイム更新が必要な項目

- AI利用数
- 売上
- 稼働率
- タスク数

---

# 16. AIダッシュボード

AIが自動分析する。

分析内容

- 売上予測
- 案件不足予測
- 人材不足予測
- 解約リスク
- 顧客分析
- 営業改善提案
- 採用予測

---

# 17. 将来拡張

- Power BI連携
- Microsoft Fabric連携
- Grafana連携
- Kibana連携
- Tableau連携
- AI経営レポート
- AI異常検知
- AI KPI予測
- リアルタイムダッシュボード
- モバイルダッシュボード
