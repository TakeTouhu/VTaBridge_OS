# UI設計

Version: 1.0

Status: Draft

---

# 概要

本ディレクトリでは、VTaBridge OSのフロントエンド設計を管理する。

Next.js 15・React 19・TypeScript・Tailwind CSS・shadcn/uiを採用し、企業向けSaaSとして保守性・拡張性・操作性を重視したUI/UXを設計する。

---

# 設計一覧

| No | ファイル | 内容 |
|----|---------|------|
| 01 | UIArchitecture.md | UI全体アーキテクチャ |
| 02 | DesignSystem.md | デザインシステム |
| 03 | Layout.md | レイアウト設計 |
| 04 | Authentication.md | ログイン・認証UI |
| 05 | Dashboard.md | ダッシュボード |
| 06 | Customer.md | 顧客管理画面 |
| 07 | Engineer.md | エンジニア管理画面 |
| 08 | Project.md | 案件管理画面 |
| 09 | AIChat.md | AIチャット画面 |
| 10 | Workflow.md | ワークフロー画面 |
| 11 | Responsive.md | レスポンシブ設計 |
| 12 | Accessibility.md | アクセシビリティ |
| 13 | Theme.md | テーマ設計 |
| 14 | ComponentGuideline.md | コンポーネント設計ガイドライン |

---

# 採用技術

- Next.js 15
- React 19
- TypeScript
- Tailwind CSS v4
- shadcn/ui
- React Hook Form
- Zod
- TanStack Query
- Zustand
- Recharts

---

# UI設計方針

- シンプルで高速
- レスポンシブ対応
- ダークモード対応
- アクセシビリティ準拠
- コンポーネント指向設計
- Atomic Designを参考に設計
- Server Componentsを基本とする

---

# デザインコンセプト

- Microsoft 365ライクなUI
- シンプル
- 視認性重視
- 操作回数を最小化
- AIを中心としたUX
- エンタープライズ向けデザイン

---

# ディレクトリ構成

```
07_UI/

├── README.md
├── UIArchitecture.md
├── DesignSystem.md
├── Layout.md
├── Authentication.md
├── Dashboard.md
├── Customer.md
├── Engineer.md
├── Project.md
├── AIChat.md
├── Workflow.md
├── Responsive.md
├── Accessibility.md
├── Theme.md
└── ComponentGuideline.md
```

---

# 対応ブラウザ

- Microsoft Edge
- Google Chrome
- Firefox
- Safari

最新版をサポート対象とする。

---

# 更新履歴

| Version | Date | 内容 |
|----------|------|------|
| 1.0 | 2026-07 | 初版 |
