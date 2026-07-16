# Engineer UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Engineer画面は、VTaBridge OSにおけるエンジニア情報を管理する中核画面である。

プロフィール・スキル・資格・語学・案件参画履歴・稼働状況・履歴書・職務経歴書・AIマッチング結果を一元管理し、営業・採用・案件管理の中心となる。

---

# 2. 目的

Engineer画面の目的

- エンジニア管理
- スキル管理
- 資格管理
- 稼働管理
- 案件履歴管理
- AIマッチング
- 履歴書管理
- 採用支援

---

# 3. 画面構成

```
Header

↓

Search

↓

Filter

↓

Engineer Table

↓

Pagination

↓

Engineer Detail Drawer
```

---

# 4. 一覧表示

表示項目

- 氏名
- 所属会社
- 雇用形態
- 稼働状況
- 保有スキル
- 経験年数
- 希望単価
- 最寄駅
- 最終更新日

TanStack Tableを利用する。

---

# 5. 検索

検索対象

- 氏名
- スキル
- 資格
- 語学
- 所属会社
- 最寄駅
- メールアドレス
- 電話番号

全文検索に対応する。

---

# 6. フィルター

対応

- 稼働状況
- 雇用形態
- スキル
- 資格
- 語学
- 経験年数
- 希望単価
- 所属会社

複数条件検索に対応する。

---

# 7. 詳細画面

Drawer表示を標準とする。

表示タブ

- 基本情報
- スキル
- 資格
- 語学
- 案件履歴
- 稼働履歴
- 履歴書
- 職務経歴書
- 添付ファイル
- AI分析

---

# 8. スキル表示

表示内容

- スキル名
- 経験年数
- レベル
- 最終利用日
- 自己評価
- AI評価

スキルレベルを視覚的に表示する。

---

# 9. 資格表示

表示項目

- 資格名
- 発行団体
- 取得日
- 有効期限
- 資格番号

期限切れ資格は警告表示する。

---

# 10. 語学表示

表示項目

- 言語
- 会話レベル
- 読み書きレベル
- 資格
- ビジネス対応可否

多言語対応状況を表示する。

---

# 11. 稼働状況

表示項目

- 稼働中
- 待機中
- 参画予定
- 提案中
- 退職予定

色分けして表示する。

---

# 12. 案件履歴

表示内容

- 案件名
- 顧客
- 期間
- 担当工程
- 使用技術
- 評価

Project APIと連携する。

---

# 13. AIマッチング

AI Agentが表示

- おすすめ案件
- マッチングスコア
- 推薦理由
- 不足スキル
- 推定参画率
- 市場価値分析

Recruit Agentと連携する。

---

# 14. 履歴書・職務経歴書

表示内容

- PDFプレビュー
- OCR結果
- AI要約
- ダウンロード
- 更新履歴

OCR APIと連携する。

---

# 15. クイックアクション

表示

- 新規登録
- 編集
- 削除
- 案件提案
- AI分析
- メール送信
- 面談登録
- PDF出力

---

# 16. API

```
GET

/api/v1/engineers
```

```
GET

/api/v1/engineers/{id}
```

```
POST

/api/v1/engineers
```

```
PUT

/api/v1/engineers/{id}
```

```
DELETE

/api/v1/engineers/{id}
```

Engineer APIを利用する。

---

# 17. UIコンポーネント

利用

- Table
- Drawer
- Tabs
- Card
- Badge
- Avatar
- Timeline
- Tooltip
- Accordion

shadcn/uiを利用する。

---

# 18. 状態表示

対応

- Loading
- Empty
- Error
- Success

一覧・詳細ともSkeletonを利用する。

---

# 19. レスポンシブ

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

# 20. アクセシビリティ

対応

- キーボード操作
- Focus表示
- Screen Reader
- ARIA属性
- WCAG 2.2 AA

---

# 21. セキュリティ

実装

- RBAC
- API認可
- HTTPS
- PIIマスキング

個人情報は権限に応じて表示・非表示を切り替える。

---

# 22. パフォーマンス

実施

- Server Components
- Streaming
- Pagination
- Lazy Loading
- TanStack Query Cache

---

# 23. 関連画面

遷移先

- Company
- Skill
- Qualification
- Language
- Project
- Meeting
- Contract
- AI Chat

相互リンクを提供する。

---

# 24. デザインルール

- 一覧画面を優先
- 詳細はDrawer表示
- AI分析は右サイドパネル
- スキルはBadge表示
- 稼働状況は色分け表示
- 案件履歴はTimeline表示

---

# 25. 将来拡張

- AIキャリア提案
- AIスキル分析
- スキルレーダーチャート
- GitHub連携
- Qiita連携
- Zenn連携
- 技術ブログ分析
- AI市場価値分析
- キャリアロードマップ
- エンジニア360ビュー
