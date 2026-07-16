# Theme 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Themeは、VTaBridge OS全体で利用するテーマ・カラー・デザイントークンを定義する。

Light・Dark・Systemテーマを標準提供し、企業ブランドやユーザー設定に応じたテーマ切り替えを可能とする。

---

# 2. 目的

Theme導入目的

- UIの一貫性
- ダークモード対応
- ブランド対応
- アクセシビリティ向上
- カスタマイズ性向上
- デザイン保守性向上

---

# 3. 対応テーマ

標準テーマ

- Light
- Dark
- System

SystemはOS設定に追従する。

---

# 4. テーマ構成

```
Theme

↓

Design Token

↓

Tailwind CSS

↓

shadcn/ui

↓

Component

↓

Page
```

---

# 5. カラーパレット

Primary

```
Blue
```

Secondary

```
Slate
```

Success

```
Green
```

Warning

```
Amber
```

Danger

```
Red
```

Info

```
Sky
```

Neutral

```
Gray
```

---

# 6. Light Theme

背景

```
#FFFFFF
```

カード

```
#F8FAFC
```

文字

```
#0F172A
```

境界線

```
#E2E8F0
```

---

# 7. Dark Theme

背景

```
#020617
```

カード

```
#0F172A
```

文字

```
#F8FAFC
```

境界線

```
#334155
```

---

# 8. Design Token

対象

- Color
- Font
- Radius
- Shadow
- Border
- Space
- Animation

CSS Variablesで管理する。

---

# 9. タイポグラフィ

Font

```
Inter
```

日本語

```
Noto Sans JP
```

Monospace

```
JetBrains Mono
```

---

# 10. Radius

利用値

```
0

4

8

12

16

24
```

Cardは12pxを標準とする。

---

# 11. Shadow

種類

- Small
- Medium
- Large
- Extra Large

ダークモードではShadowを弱める。

---

# 12. アイコン

利用

```
Lucide React
```

テーマ切替時も形状は変更しない。

---

# 13. テーマ切替

方法

- Header
- User Menu
- Settings

切替後は即時反映する。

---

# 14. 保存

保存先

- User Settings
- Local Storage

ログイン時はユーザー設定を優先する。

---

# 15. コンポーネント

対応

- Button
- Card
- Dialog
- Table
- Input
- Badge
- Tabs
- Chart

全コンポーネントがテーマ対応する。

---

# 16. チャート

Light

- 明るい背景

Dark

- 高コントラスト

Recharts Themeを利用する。

---

# 17. AI Chat

対応

- Light Theme
- Dark Theme

コードブロックもテーマに追従する。

---

# 18. アクセシビリティ

対応

- WCAG 2.2 AA
- Color Contrast
- Focus表示
- Color Blind対応

テーマ変更後もアクセシビリティを維持する。

---

# 19. パフォーマンス

実施

- CSS Variables
- Tailwind CSS
- next-themes
- Server Components

テーマ切替時に画面リロードを行わない。

---

# 20. Prisma実装方針

テーマ設定はUser Settingsへ保存する。

Business API経由で取得・更新する。

---

# 21. デザインルール

- ブランドカラーを統一
- 色数を増やしすぎない
- ダークモードを標準サポート
- アイコン色のみで意味を伝えない
- コントラスト比を維持する

---

# 22. 将来拡張

- White Label対応
- ブランドテーマ
- 顧客別テーマ
- Dynamic Theme
- Figma Token同期
- Design Token API
- AIテーマ生成
- 高コントラストテーマ
- 色覚補正テーマ
- 季節テーマ
