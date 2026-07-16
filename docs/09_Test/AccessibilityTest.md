# Accessibility Test 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Accessibility Testは、VTaBridge OSがすべての利用者にとって利用しやすいシステムであることを保証するためのテスト設計を定義する。

WCAG 2.2 AAへの準拠を目標とし、自動テストと手動テストを組み合わせてアクセシビリティ品質を継続的に維持する。

---

# 2. 目的

Accessibility Test導入目的

- WCAG準拠確認
- 操作性向上
- 多様な利用者への対応
- 法令・ガイドライン対応
- 継続的品質改善
- アクセシビリティの標準化

---

# 3. 対象

対象

- Frontend
- Dashboard
- Customer
- Engineer
- Project
- AI Chat
- Workflow
- Authentication
- Settings

すべての画面を対象とする。

---

# 4. 利用ツール

利用

- axe DevTools
- Lighthouse
- Accessibility Insights
- Playwright
- NVDA
- VoiceOver
- Narrator

自動テストと手動確認を組み合わせる。

---

# 5. WCAG 2.2 AA

確認項目

- Perceivable（知覚可能）
- Operable（操作可能）
- Understandable（理解可能）
- Robust（堅牢）

WCAG 2.2 AAを品質基準とする。

---

# 6. キーボード操作

確認項目

- Tab移動
- Shift + Tab
- Enter
- Escape
- Arrow Key
- Space

すべての主要機能をキーボードのみで操作可能とする。

---

# 7. Focus

確認項目

- Focus表示
- Focus順序
- Focus Trap
- Dialog Focus
- Drawer Focus

フォーカスの見失いを防止する。

---

# 8. スクリーンリーダー

対象

- NVDA
- VoiceOver
- Narrator
- JAWS（必要時）

読み上げ順序・内容を確認する。

---

# 9. ARIA

確認項目

- aria-label
- aria-labelledby
- aria-describedby
- aria-live
- role
- aria-expanded

不要なARIA属性が付与されていないことも確認する。

---

# 10. コントラスト

確認項目

通常文字

```
4.5:1以上
```

大文字

```
3:1以上
```

Light・Dark両テーマで確認する。

---

# 11. 色覚対応

確認項目

- 色のみで情報を表現していない
- アイコン併用
- テキスト併用
- エラー表示

色覚多様性に配慮する。

---

# 12. フォーム

確認項目

- Label表示
- 必須項目
- Error Message
- Validation
- Placeholder依存禁止

入力支援を確認する。

---

# 13. テーブル

確認項目

- Header
- Caption
- Sort状態
- 行選択
- ページング

スクリーンリーダーで正しく認識されることを確認する。

---

# 14. Dialog

確認項目

- Focus Trap
- Escape閉じる
- aria-modal
- 背景操作禁止

モーダル操作の一貫性を確認する。

---

# 15. AI Chat

確認項目

- チャット履歴読み上げ
- Streaming通知
- 音声入力
- AI回答通知
- キーボード操作

AI機能もアクセシビリティ要件を満たすことを確認する。

---

# 16. レスポンシブ

対象

- Desktop
- Tablet
- Mobile

画面サイズ変更時も操作性を維持する。

---

# 17. 自動テスト

GitHub Actionsで実施

- axe
- Lighthouse
- Playwright Accessibility

品質ゲートとして利用する。

---

# 18. 手動テスト

実施内容

- キーボード操作
- スクリーンリーダー確認
- 色覚確認
- ズーム表示（200%）
- 高コントラストモード

自動検出できない項目を確認する。

---

# 19. レポート

出力内容

- WCAG適合率
- 違反一覧
- Lighthouse Score
- axe Report
- 改善提案

HTML形式で保存する。

---

# 20. 品質基準

目標

Lighthouse Accessibility

```
95点以上
```

WCAG AA

```
100%適合
```

重大なアクセシビリティ違反はリリースを停止する。

---

# 21. ベストプラクティス

- Semantic HTMLを利用
- ARIAは必要最小限
- キーボード操作を標準対応
- 色だけで意味を伝えない
- アクセシビリティを設計段階から考慮する

---

# 22. 将来拡張

- AIアクセシビリティ診断
- 自動改善提案
- 音声UIテスト
- ジェスチャー操作テスト
- 視線入力テスト
- 認知負荷評価
- 多言語読み上げ評価
- Visual Regression連携
- AI品質スコア
- Continuous Accessibility Testing
