# Layout 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Layoutは、VTaBridge OS全画面で共通利用するレイアウトを定義する。

一貫した操作性・視認性・レスポンシブ対応を実現し、業務効率を向上させる。

---

# 2. 設計方針

基本方針

- Microsoft 365ライク
- シンプル
- AIファースト
- 情報量重視
- マウス・キーボード双方に最適化
- レスポンシブ対応

---

# 3. 全体レイアウト

```
┌──────────────────────────────────────────────┐
│ Header                                       │
├──────────────┬───────────────────────────────┤
│              │                               │
│ Sidebar      │ Main Content                  │
│              │                               │
│              │                               │
│              │                               │
├──────────────┴───────────────────────────────┤
│ Footer                                       │
└──────────────────────────────────────────────┘
```

---

# 4. Header

表示項目

- ロゴ
- パンくずリスト
- 全体検索
- AIチャット
- 通知
- ユーザー
- 設定

Header高さ

```
64px
```

固定表示とする。

---

# 5. Sidebar

表示項目

- Dashboard
- Customer
- Company
- Contact
- Engineer
- Project
- Contract
- Invoice
- Payment
- Meeting
- Task
- AI
- Workflow
- Reports
- Settings

幅

```
280px
```

折りたたみに対応する。

---

# 6. Main Content

構成

```
Page Header

↓

Toolbar

↓

Content

↓

Pagination
```

スクロールはMain Contentのみ行う。

---

# 7. Footer

表示内容

- Version
- Copyright
- Build番号
- Environment

高さ

```
32px
```

---

# 8. AI Chat

配置

```
右サイドパネル
```

幅

```
420px
```

対応

- 開閉
- 履歴
- Agent切替
- RAG検索
- Function実行

全画面共通で利用可能とする。

---

# 9. Notification Panel

配置

```
右サイド
```

表示

- 未読通知
- AI通知
- Workflow通知
- 契約通知
- エラー通知

---

# 10. Breadcrumb

例

```
Dashboard

＞

Engineer

＞

Detail
```

App Routerと同期する。

---

# 11. Toolbar

表示内容

- 新規登録
- 編集
- 削除
- CSV
- Excel
- PDF
- AI
- Filter

画面ごとに変更可能とする。

---

# 12. Search

Header検索

対象

- Customer
- Company
- Engineer
- Project
- Contract
- Meeting
- Knowledge

AI検索にも対応する。

---

# 13. モーダル

利用

```
Dialog

Sheet

Drawer
```

編集画面はDrawerを優先する。

---

# 14. レスポンシブ

Desktop

```
≥1280px
```

Tablet

```
768〜1279px
```

Mobile

```
≤767px
```

Sidebarは自動折りたたみする。

---

# 15. 状態表示

表示

- Loading
- Empty
- Error
- Success
- Permission Denied
- Maintenance

Skeletonを標準とする。

---

# 16. アクセシビリティ

対応

- Tab移動
- Focus表示
- Screen Reader
- ARIA
- Skip Navigation

---

# 17. パフォーマンス

実施

- Lazy Loading
- Dynamic Import
- Route Cache
- Streaming
- Image Optimization

Server Componentsを優先利用する。

---

# 18. Prisma実装方針

UIレイヤーではPrismaを利用しない。

Business API経由でデータを取得する。

---

# 19. デザインルール

- 余白は16pxを基本とする
- 一覧画面を優先する
- モーダルの多重表示は禁止
- 操作ボタンは右上へ配置
- KPIはカード表示を標準とする
- アイコンのみのボタンにはTooltipを表示する

---

# 20. 将来拡張

- マルチレイアウト対応
- ドラッグ＆ドロップレイアウト
- ウィジェット配置変更
- AIレイアウト最適化
- White Label対応
- PWA専用レイアウト
- Electron専用レイアウト
- マルチモニター対応
- コンパクトモード
- カスタムダッシュボード
