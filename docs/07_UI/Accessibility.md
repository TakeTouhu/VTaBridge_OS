# Accessibility 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Accessibilityは、VTaBridge OS全体に適用するアクセシビリティ設計を定義する。

すべての利用者がデバイスや身体的特性に関わらず快適に操作できるUIを提供することを目的とし、WCAG 2.2 AA準拠を目標とする。

---

# 2. 目的

Accessibility導入目的

- 誰でも利用できるUI
- 操作性向上
- キーボード操作対応
- スクリーンリーダー対応
- 色覚バリアフリー
- 法令・ガイドライン対応

---

# 3. 対応基準

準拠

- WCAG 2.2 AA
- WAI-ARIA 1.2
- HTML Living Standard
- Microsoft Accessibility Guidelines

---

# 4. キーボード操作

対応

- Tab移動
- Shift + Tab
- Enter
- Space
- Escape
- Arrow Key
- Home
- End

すべての主要操作をキーボードのみで実行可能とする。

---

# 5. Focus管理

実装

- Focus Ring表示
- Focus Trap
- Dialog Focus
- Drawer Focus
- Skip Navigation

現在のフォーカス位置を明確に表示する。

---

# 6. スクリーンリーダー

対応

- NVDA
- JAWS
- VoiceOver
- Narrator

適切な読み上げ順序を維持する。

---

# 7. ARIA

利用例

- aria-label
- aria-labelledby
- aria-describedby
- aria-expanded
- aria-hidden
- aria-live
- role

不要なARIA属性は付与しない。

---

# 8. 色覚対応

対応

- 色だけで状態を表現しない
- アイコン併用
- テキスト併用
- コントラスト確保

状態は色＋ラベルで表現する。

---

# 9. コントラスト

基準

通常文字

```
4.5:1以上
```

大きな文字

```
3:1以上
```

WCAG 2.2 AAを満たすこと。

---

# 10. フォーム

実装

- Label必須
- Error Message
- Required表示
- Placeholder依存禁止

入力エラーは視覚・音声の両方で伝える。

---

# 11. ボタン

実装

- Icon Only禁止
- Tooltip表示
- aria-label設定

クリック領域は44px以上とする。

---

# 12. テーブル

対応

- Header設定
- Caption
- Sort状態通知
- 行選択通知

スクリーンリーダー対応を行う。

---

# 13. Dialog

対応

- Focus Trap
- Escape閉じる
- 背景操作禁止
- aria-modal

閉じたら元のFocusへ戻す。

---

# 14. 通知

対応

- aria-live
- Toast読み上げ
- Error通知
- Success通知

重要通知は自動読み上げ対象とする。

---

# 15. AI Chat

対応

- メッセージ読み上げ
- 入力補助
- 音声入力
- キーボード操作
- AI回答通知

Streaming中も読み上げに対応する。

---

# 16. 動画・音声

対応

- 字幕
- Transcript
- 音量調整
- 再生速度変更

Speech APIと連携する。

---

# 17. モーション

実装

- prefers-reduced-motion対応
- アニメーション停止
- 点滅禁止

ユーザー設定を優先する。

---

# 18. テスト

実施

- Lighthouse
- axe DevTools
- Accessibility Insights
- Playwright

CI/CDで自動チェックする。

---

# 19. UIコンポーネント

利用

- shadcn/ui
- Radix UI

アクセシブルなコンポーネントを利用する。

---

# 20. パフォーマンス

実施

- Semantic HTML
- 適切なDOM構造
- Lazy Loading
- ARIA最適化

アクセシビリティと性能を両立する。

---

# 21. デザインルール

- Semantic HTMLを優先する
- divよりbutton・nav・main等を利用する
- 見出し階層を守る
- 色だけで情報を伝えない
- アイコンのみで意味を伝えない

---

# 22. セキュリティ

実装

- HTTPS
- CSP
- XSS対策
- CSRF対策

アクセシビリティとセキュリティを両立する。

---

# 23. 将来拡張

- AIアクセシビリティ評価
- 音声UI
- ジェスチャー操作
- 視線入力対応
- 多言語読み上げ
- AI入力支援
- AI要約読み上げ
- リアルタイム字幕
- 認知支援モード
- パーソナライズドUI
