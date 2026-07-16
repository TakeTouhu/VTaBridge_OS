# UI Architecture

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

UI Architectureでは、VTaBridge OSのフロントエンド全体構成を定義する。

Next.js 15 App Routerを採用し、Server Componentsを基本としながら、必要に応じてClient Componentsを利用する。

企業向けSaaSとして、高速表示・保守性・拡張性・AIとの親和性を重視したアーキテクチャを採用する。

---

# 2. 目的

UI設計の目的

- 高速表示
- 保守性向上
- 再利用性向上
- AIとの統合
- SEO対応
- レスポンシブ対応
- ダークモード対応
- アクセシビリティ対応

---

# 3. 全体アーキテクチャ

```
Browser

↓

Next.js 15

(App Router)

↓

Server Components

↓

Client Components

↓

TanStack Query

↓

Business API

↓

PostgreSQL
```

---

# 4. 技術スタック

| 技術 | 用途 |
|------|------|
| Next.js 15 | フレームワーク |
| React 19 | UI |
| TypeScript | 型管理 |
| Tailwind CSS | CSS |
| shadcn/ui | UI Component |
| TanStack Query | API通信 |
| Zustand | 状態管理 |
| React Hook Form | フォーム |
| Zod | バリデーション |
| Recharts | グラフ |

---

# 5. ディレクトリ構成

```
app/

components/

features/

hooks/

lib/

providers/

services/

store/

types/

utils/
```

---

# 6. App Router

ページ例

```
/

dashboard

customers

companies

contacts

engineers

projects

contracts

invoices

payments

meetings

tasks

ai

settings

login
```

---

# 7. コンポーネント構成

```
Page

↓

Feature

↓

UI Component

↓

shadcn/ui

↓

HTML
```

共通部品を優先して利用する。

---

# 8. 状態管理

Zustand

管理対象

- User
- Theme
- Sidebar
- Notification
- AI Chat
- Filter

サーバーデータはTanStack Queryで管理する。

---

# 9. API通信

利用

TanStack Query

実施内容

- Cache
- Retry
- Loading
- Error
- Mutation

Business APIのみ通信対象とする。

---

# 10. フォーム

React Hook Form

Validation

Zod

対応

- CRUD
- 検索
- 編集
- AI入力補助

---

# 11. AIチャット

AI Chatは全画面から利用可能とする。

配置

```
右サイドパネル
```

AI Agentと連携する。

---

# 12. レイアウト

共通レイアウト

```
Header

↓

Sidebar

↓

Main

↓

Footer
```

App Router Layoutを利用する。

---

# 13. 認証

Azure Entra ID

JWT

RBAC

認証後のみ画面を表示する。

---

# 14. エラー処理

実装

- Error Boundary
- Loading UI
- Retry
- Toast
- 404
- 500

---

# 15. セキュリティ

実装

- CSP
- XSS対策
- CSRF対策
- Input Validation
- HTTPS
- Secure Cookie

---

# 16. パフォーマンス

実施内容

- Server Components
- Lazy Loading
- Image Optimization
- Dynamic Import
- Route Cache
- Streaming

---

# 17. Prisma実装方針

UIではPrismaを直接利用しない。

Business API経由でデータ取得を行う。

---

# 18. 可観測性

利用

- Azure Application Insights
- OpenTelemetry

取得項目

- Page View
- API Response
- Error
- Performance

---

# 19. デザイン方針

- Microsoft 365ライク
- 余白を広く取る
- アイコンを多用しすぎない
- 一貫したUI
- 学習コストを下げる

---

# 20. 将来拡張

- PWA対応
- Electron対応
- モバイルアプリ対応
- オフライン対応
- マルチテナントUI
- AI Copilot UI
- ドラッグ＆ドロップレイアウト
- ノーコード画面生成
- AIレイアウト最適化
- マイクロフロントエンド対応
