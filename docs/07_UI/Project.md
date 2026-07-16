# Project UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Project画面は、VTaBridge OSにおける案件情報を管理する中核画面である。

案件の募集要件・契約情報・参画エンジニア・顧客情報・進捗・売上・AIマッチング結果を一元管理する。

営業・採用・PMが共通利用する重要な画面とする。

---

# 2. 目的

Project画面の目的

- 案件管理
- 募集管理
- 契約管理
- 要員管理
- AIマッチング
- 売上管理
- 契約更新
- 進捗管理

---

# 3. 画面構成

```
Header

↓

Search

↓

Filter

↓

Project Table

↓

Pagination

↓

Project Detail Drawer
```

---

# 4. 一覧表示

表示項目

- 案件名
- 顧客名
- 募集人数
- 参画人数
- 契約期間
- 単価
- ステータス
- 担当営業
- 最終更新日

TanStack Tableを利用する。

---

# 5. 検索

検索対象

- 案件名
- 顧客名
- 募集スキル
- 担当営業
- 契約番号
- 勤務地

全文検索に対応する。

---

# 6. フィルター

対応

- ステータス
- 顧客
- 単価
- 契約期間
- リモート可否
- 募集人数
- 担当営業
- 業種

複数条件検索に対応する。

---

# 7. 詳細画面

Drawer表示を標準とする。

表示タブ

- 基本情報
- 募集要件
- 参画エンジニア
- 契約
- 売上
- タスク
- 会議
- 添付ファイル
- AI分析

---

# 8. 募集要件

表示項目

- 必須スキル
- 尚可スキル
- 開始日
- 終了予定
- 勤務地
- 勤務形態
- 面談回数
- 外国籍可否

スキルはBadge表示する。

---

# 9. 参画エンジニア

表示項目

- 氏名
- 役割
- 契約開始日
- 契約終了日
- 稼働率
- 単価
- ステータス

Engineer APIと連携する。

---

# 10. AIマッチング

AI Agentが表示

- おすすめエンジニア
- マッチングスコア
- 推薦理由
- 不足スキル
- 採用優先順位
- 市場分析

Recruit Agentと連携する。

---

# 11. 売上情報

表示項目

- 売上
- 粗利
- 原価
- 利益率
- 請求状況
- 入金状況

Dashboard APIと連携する。

---

# 12. クイックアクション

表示

- 新規案件
- 編集
- 削除
- エンジニア提案
- 契約作成
- AI分析
- Meeting作成
- メール送信

---

# 13. API

```
GET

/api/v1/projects
```

```
GET

/api/v1/projects/{id}
```

```
POST

/api/v1/projects
```

```
PUT

/api/v1/projects/{id}
```

```
DELETE

/api/v1/projects/{id}
```

Project APIを利用する。

---

# 14. UIコンポーネント

利用

- Table
- Drawer
- Tabs
- Card
- Badge
- Timeline
- Tooltip
- Accordion
- Chart

shadcn/uiを利用する。

---

# 15. 状態表示

対応

- Loading
- Empty
- Error
- Success

一覧・詳細ともSkeletonを利用する。

---

# 16. レスポンシブ

Desktop

```
Table + Drawer
```

Tablet

```
簡易Table
```

Mobile

```
Card一覧
```

---

# 17. アクセシビリティ

対応

- キーボード操作
- Focus表示
- Screen Reader
- ARIA属性
- WCAG 2.2 AA

---

# 18. セキュリティ

実装

- RBAC
- API認可
- HTTPS
- 部署別アクセス制御

契約金額・利益率は権限に応じて表示制御する。

---

# 19. パフォーマンス

実施

- Server Components
- Streaming
- Pagination
- Lazy Loading
- TanStack Query Cache

---

# 20. 関連画面

遷移先

- Customer
- Company
- Engineer
- Contract
- Meeting
- Task
- Invoice
- Payment
- AI Chat

相互リンクを提供する。

---

# 21. デザインルール

- 一覧画面を優先
- 詳細はDrawer表示
- AI分析は右サイドパネル
- ステータスはBadge表示
- 売上はChart表示
- 契約期間はTimeline表示

---

# 22. 将来拡張

- AI案件生成
- AI単価予測
- AI売上予測
- AIリスク分析
- AI人員計画
- ガントチャート表示
- カレンダー表示
- Power BI連携
- Process Mining連携
- Project 360ビュー
