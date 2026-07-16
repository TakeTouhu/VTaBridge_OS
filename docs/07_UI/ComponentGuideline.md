# Component Guideline

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Component Guidelineは、VTaBridge OSにおけるフロントエンドコンポーネントの設計・実装・保守ルールを定義する。

UI品質・保守性・再利用性・一貫性を維持するため、すべてのReactコンポーネントは本ガイドラインに従って開発する。

---

# 2. 目的

Component Guideline導入目的

- UI品質向上
- 再利用性向上
- 保守性向上
- 開発効率向上
- 一貫した命名
- 責務分離

---

# 3. 基本方針

実装方針

- Server Componentsを優先
- Client Componentsは必要最小限
- 単一責任原則（SRP）
- 再利用可能な設計
- ビジネスロジックとUIを分離
- Propsを最小限に保つ

---

# 4. ディレクトリ構成

```
components/

├── ui/
├── common/
├── layout/
├── dashboard/
├── customer/
├── engineer/
├── project/
├── ai/
└── workflow/
```

---

# 5. 命名規則

Component

```
CustomerCard
```

Hook

```
useCustomer
```

Store

```
useCustomerStore
```

Type

```
Customer
```

Props

```
CustomerCardProps
```

PascalCaseを採用する。

---

# 6. Component分類

| 種類 | 用途 |
|------|------|
| ui | shadcn/uiラッパー |
| common | 共通部品 |
| layout | レイアウト |
| feature | 業務画面 |
| chart | グラフ |
| ai | AI関連 |

---

# 7. Server Components

利用対象

- 一覧画面
- 詳細画面
- Dashboard
- Report
- KPI

データ取得を担当する。

---

# 8. Client Components

利用対象

- Form
- Dialog
- Drawer
- Chart
- AI Chat
- Drag & Drop

状態管理が必要な画面のみ利用する。

---

# 9. Props設計

原則

- 必要最小限
- Optionalを減らす
- 型を明確化
- Callbackを整理

Props Drillingを避ける。

---

# 10. 状態管理

利用

- Zustand
- TanStack Query

ローカルStateはuseStateを利用する。

---

# 11. API

API呼び出しはComponent内で直接行わない。

利用

```
services/

↓

TanStack Query

↓

Business API
```

---

# 12. カスタムHook

例

```
useCustomer()

useEngineer()

useDashboard()

useAIChat()
```

ロジックをComponentから分離する。

---

# 13. UI Component

利用

- Button
- Card
- Table
- Dialog
- Drawer
- Input
- Badge
- Tabs

shadcn/uiを優先利用する。

---

# 14. スタイリング

利用

- Tailwind CSS
- clsx
- tailwind-merge

CSS Moduleは原則利用しない。

---

# 15. バリデーション

利用

- React Hook Form
- Zod

ValidationはSchemaで管理する。

---

# 16. エラーハンドリング

実装

- Error Boundary
- Loading
- Retry
- Empty State
- Toast

画面ごとに統一したUIを提供する。

---

# 17. テスト

実施

- Unit Test
- Component Test
- E2E Test

利用

- Vitest
- React Testing Library
- Playwright

---

# 18. パフォーマンス

実施

- React.memo
- Dynamic Import
- Lazy Loading
- Suspense
- Streaming

不要な再レンダリングを防止する。

---

# 19. アクセシビリティ

対応

- Semantic HTML
- ARIA
- Focus
- WCAG 2.2 AA

アクセシビリティを標準実装とする。

---

# 20. セキュリティ

実装

- Input Validation
- CSP
- XSS対策
- HTTPS
- Secure Cookie

機密情報はComponentへ保持しない。

---

# 21. コードレビュー

確認項目

- 命名規則
- 型定義
- 責務分離
- 再利用性
- パフォーマンス
- アクセシビリティ
- テスト

Pull Requestでレビューを実施する。

---

# 22. 将来拡張

- Storybook
- Design Token自動同期
- Component Catalog
- Visual Regression Test
- AIコードレビュー
- AIコンポーネント生成
- マイクロフロントエンド対応
- Web Components対応
- React Compiler対応
- デザイン品質メトリクス
