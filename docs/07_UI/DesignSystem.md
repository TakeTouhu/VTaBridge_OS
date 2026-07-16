# Design System

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Design Systemは、VTaBridge OS全体で利用するUIコンポーネント・デザインルール・アクセシビリティ基準を定義する。

すべての画面は本Design Systemに従って実装する。

---

# 2. 目的

Design System導入目的

- UI品質統一
- コンポーネント再利用
- 保守性向上
- 開発効率向上
- アクセシビリティ向上
- デザイン一貫性

---

# 3. デザインコンセプト

基本方針

- Microsoft 365ライク
- Enterprise SaaS
- シンプル
- 視認性重視
- 高速操作
- AIファースト

---

# 4. カラーパレット

Primary

```
Blue-600
```

Secondary

```
Slate-700
```

Success

```
Green-600
```

Warning

```
Amber-500
```

Danger

```
Red-600
```

Info

```
Sky-500
```

Background

```
Slate-50
```

Dark Mode

```
Slate-950
```

---

# 5. タイポグラフィ

Font

```
Inter
```

Fallback

```
Noto Sans JP
```

サイズ

| 用途 | Size |
|------|------|
| H1 | 32px |
| H2 | 28px |
| H3 | 24px |
| H4 | 20px |
| H5 | 18px |
| Body | 16px |
| Small | 14px |
| Caption | 12px |

---

# 6. スペーシング

基本単位

```
4px
```

利用例

```
4

8

12

16

20

24

32

48

64
```

Tailwind Spacing Scaleに準拠する。

---

# 7. アイコン

採用

```
Lucide React
```

用途

- メニュー
- CRUD
- AI
- 通知
- ダッシュボード
- ファイル
- 設定

Material Iconsは使用しない。

---

# 8. ボタン

種類

- Primary
- Secondary
- Outline
- Ghost
- Destructive
- Link

サイズ

- Small
- Medium
- Large

shadcn/ui Buttonを利用する。

---

# 9. 入力フォーム

利用Component

- Input
- Textarea
- Select
- Checkbox
- Radio
- Switch
- Combobox
- Date Picker

React Hook Formで統一する。

---

# 10. テーブル

利用

```
TanStack Table
```

対応

- Sort
- Filter
- Pagination
- Column Resize
- Export
- Selection

---

# 11. カード

用途

- KPI
- AI
- Dashboard
- Customer
- Engineer
- Project

Card Componentを利用する。

---

# 12. ダイアログ

利用

```
shadcn/ui Dialog
```

対象

- 登録
- 編集
- 削除
- 詳細
- 承認

---

# 13. 通知

利用

```
Sonner
```

種類

- Success
- Error
- Warning
- Info

画面右上へ表示する。

---

# 14. ローディング

利用

- Skeleton
- Spinner
- Progress

画面全体をブロックしない。

---

# 15. チャート

利用

```
Recharts
```

対応

- Line
- Bar
- Pie
- Area
- Radar
- KPI Card

---

# 16. テーマ

対応

- Light
- Dark
- System

next-themesを利用する。

---

# 17. アニメーション

利用

- Fade
- Slide
- Scale

Tailwind CSS Animationを利用する。

派手な演出は避ける。

---

# 18. アクセシビリティ

対応

- WCAG 2.2 AA
- キーボード操作
- Screen Reader
- Focus表示
- ARIA属性

---

# 19. コンポーネント命名規則

例

```
CustomerCard

EngineerTable

ProjectDialog

AIChatPanel

DashboardChart
```

PascalCaseを採用する。

---

# 20. 将来拡張

- Design Token管理
- Figma Token同期
- Storybook連携
- Component Catalog
- Motion Design
- Brand Theme
- White Label対応
- Dynamic Theme
- Design Analytics
- AI UI Generator
