# Customer UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Customer画面は、顧客企業の情報を管理するための画面である。

顧客情報だけでなく、担当者・案件・契約・請求・商談・AI分析まで一元管理する。

営業担当者が最も利用する画面の一つである。

---

# 2. 目的

Customer画面の目的

- 顧客管理
- 顧客検索
- 顧客分析
- 契約確認
- 案件確認
- 商談管理
- AI分析
- KPI表示

---

# 3. 画面構成

```
Header

↓

Search

↓

Filter

↓

Customer Table

↓

Pagination

↓

Customer Detail Drawer
```

---

# 4. 一覧表示

表示項目

- 顧客名
- 業種
- 担当営業
- 所在地
- 契約数
- 案件数
- 売上
- 最終更新日

一覧はTanStack Tableを利用する。

---

# 5. 検索

検索対象

- 顧客名
- 法人番号
- 業種
- 担当営業
- 所在地

全文検索に対応する。

---

# 6. フィルター

対応

- 業種
- 地域
- 担当営業
- 契約有無
- 案件有無
- 売上規模

複数条件検索に対応する。

---

# 7. 詳細画面

表示項目

- 基本情報
- 担当者一覧
- 案件一覧
- 契約一覧
- 請求一覧
- 商談履歴
- 添付ファイル
- AI分析

Drawer表示を標準とする。

---

# 8. AI分析

AI Agentが表示する内容

- 売上推移分析
- 契約更新予測
- 商談成功率
- 類似顧客
- 提案候補
- リスク分析

AI Chatから詳細分析を実行できる。

---

# 9. クイックアクション

表示

- 顧客登録
- 編集
- 削除
- 新規案件
- 新規契約
- 新規商談
- メール送信
- AI分析

---

# 10. API

```
GET

/api/v1/customers
```

```
GET

/api/v1/customers/{id}
```

```
POST

/api/v1/customers
```

```
PUT

/api/v1/customers/{id}
```

```
DELETE

/api/v1/customers/{id}
```

Customer APIを利用する。

---

# 11. UIコンポーネント

利用

- Table
- Card
- Drawer
- Tabs
- Badge
- Avatar
- Tooltip
- Dropdown Menu

shadcn/uiを利用する。

---

# 12. 状態表示

対応

- Loading
- Empty
- Error
- Success

一覧表示はSkeletonを利用する。

---

# 13. レスポンシブ

Desktop

```
Table表示
```

Tablet

```
簡易Table
```

Mobile

```
Card表示
```

---

# 14. アクセシビリティ

対応

- キーボード操作
- Focus表示
- ARIA属性
- WCAG 2.2 AA

---

# 15. セキュリティ

実装

- RBAC
- API認可
- HTTPS
- 部署別アクセス制御

閲覧権限に応じて表示内容を変更する。

---

# 16. パフォーマンス

実施

- Server Components
- Streaming
- Pagination
- Lazy Loading
- TanStack Query Cache

---

# 17. 操作履歴

表示

- 登録
- 更新
- 削除
- 契約追加
- 案件追加

Customer History APIと連携する。

---

# 18. 関連画面

遷移先

- Company
- Contact
- Project
- Contract
- Invoice
- Meeting
- AI Chat

相互リンクを提供する。

---

# 19. デザインルール

- 一覧画面を優先
- 詳細はDrawer表示
- 編集はDialogではなくDrawer
- AI分析は右サイドパネル
- KPIはCard表示

---

# 20. 将来拡張

- 顧客タイムライン
- 地図表示
- Power BI分析
- AI営業アシスタント
- AI売上予測
- AI契約更新提案
- CRM連携
- Salesforce同期
- Dynamics 365同期
- 顧客360ビュー
