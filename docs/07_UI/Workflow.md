# Workflow UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Workflow画面は、VTaBridge OSにおける業務ワークフローを設計・実行・監視するためのノーコード／ローコード画面である。

Power Automate・Azure Logic Apps・AI Agent・Python・Playwrightなどの自動化コンポーネントをドラッグ＆ドロップで接続し、業務フローを構築できる。

---

# 2. 目的

Workflow画面の目的

- ワークフロー作成
- ワークフロー編集
- ノーコード開発
- AIによるフロー生成
- 実行監視
- エラー分析
- 業務可視化
- 再利用性向上

---

# 3. 画面構成

```
Header

↓

Toolbar

↓

Workflow Designer

↓

Property Panel

↓

Execution Log

↓

History
```

---

# 4. Workflow Designer

中央エリア

表示内容

- ノード
- 接続線
- 開始ノード
- 終了ノード
- グループ
- コメント

ドラッグ＆ドロップに対応する。

---

# 5. ノード一覧

利用可能ノード

- Start
- End
- API
- Python
- Playwright
- Power Automate
- AI Agent
- Condition
- Loop
- Delay
- Approval
- Notification
- File
- OCR
- Speech
- Translation

---

# 6. プロパティパネル

設定項目

- ノード名
- 説明
- 入力パラメータ
- 出力パラメータ
- タイムアウト
- リトライ回数
- 実行条件

右サイドパネルへ表示する。

---

# 7. 条件分岐

対応

- IF
- ELSE
- SWITCH

条件はGUIで設定する。

---

# 8. 並列処理

Parallel Nodeを利用する。

対応

- 並列API
- 並列通知
- 並列AI
- 並列RPA

終了後にMerge Nodeへ接続する。

---

# 9. AI Workflow

AI Agentが実施

- Workflow生成
- ノード提案
- 条件提案
- 最適化
- エラー分析

自然言語からWorkflowを生成できる。

---

# 10. 実行

実施内容

- 手動実行
- テスト実行
- 定期実行
- イベント実行

実行状況をリアルタイム表示する。

---

# 11. 実行履歴

表示項目

- Workflow名
- 実行日時
- 実行時間
- Status
- 実行者
- Error

履歴から再実行できる。

---

# 12. API

```
GET

/api/v1/workflows
```

```
POST

/api/v1/workflows
```

```
PUT

/api/v1/workflows/{id}
```

```
POST

/api/v1/workflows/{id}/execute
```

```
GET

/api/v1/workflows/history
```

Workflow APIを利用する。

---

# 13. UIコンポーネント

利用

- React Flow
- Drawer
- Dialog
- Tabs
- Card
- Badge
- Tooltip
- Context Menu
- Scroll Area

Workflow DesignerにはReact Flowを採用する。

---

# 14. 状態表示

対応

- Loading
- Executing
- Success
- Error
- Warning

ノードごとに状態を色分け表示する。

---

# 15. レスポンシブ

Desktop

```
Designer表示
```

Tablet

```
閲覧中心
```

Mobile

```
実行履歴のみ
```

Workflow編集はDesktopを推奨する。

---

# 16. アクセシビリティ

対応

- キーボード操作
- Focus表示
- ARIA属性
- WCAG 2.2 AA

主要操作はショートカットキーに対応する。

---

# 17. セキュリティ

実装

- RBAC
- API認可
- Workflow権限
- HTTPS

Workflowごとに閲覧・編集・実行権限を管理する。

---

# 18. パフォーマンス

実施

- Lazy Loading
- Virtual Rendering
- Server Components
- TanStack Query

大規模Workflowでも快適に操作できることを目標とする。

---

# 19. デザインルール

- ノードは色数を抑える
- 接続線は直感的に表示
- ノードサイズを統一
- ズーム対応
- ミニマップ表示
- 自動レイアウト機能を提供する

---

# 20. 将来拡張

- BPMN 2.0対応
- AI Workflow Designer
- Workflow Marketplace
- Git連携
- バージョン比較
- Process Mining
- Human in the Loop強化
- リアルタイム共同編集
- Workflowテンプレート共有
- AIによる自動リファクタリング
