# AI Chat UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

AI Chatは、VTaBridge OS全体で利用できるAIアシスタント画面である。

Azure OpenAI Service、RAG、AI Agent、Function Calling、MCPを統合し、業務支援・情報検索・データ分析・システム操作を自然言語で実行する。

すべての画面から利用可能なCopilotライクなUIを提供する。

---

# 2. 目的

AI Chat導入目的

- 業務支援
- AI検索
- RAG検索
- AI Agent実行
- Function Calling
- MCP連携
- OCR解析
- 音声対話

---

# 3. 画面構成

```
Header

↓

Conversation

↓

Suggestion

↓

Message Input

↓

Attachment

↓

AI Status
```

右サイドDrawerとして全画面から利用可能とする。

---

# 4. チャット画面

表示項目

- 会話履歴
- AI回答
- Function実行履歴
- RAG引用情報
- Agent名
- Token使用量

Markdown表示に対応する。

---

# 5. 入力エリア

対応

- テキスト入力
- 音声入力
- ファイル添付
- 画像添付
- OCR実行
- Enter送信
- Shift+Enter改行

---

# 6. AI Agent切替

選択可能

- General Agent
- Sales Agent
- Recruit Agent
- Matching Agent
- Legal Agent
- Finance Agent
- Project Agent
- Support Agent

AIが自動選択するモードも提供する。

---

# 7. Suggestion

初期表示

- エンジニアを検索
- 案件を検索
- 契約を確認
- 売上を分析
- メールを作成
- 会議を要約

クリックするとプロンプトへ入力する。

---

# 8. Function Calling

表示

- 実行Function
- 実行状況
- 実行時間
- 成功
- 失敗

Function実行内容をユーザーへ表示する。

---

# 9. RAG表示

回答時に表示

- 参照ドキュメント
- 関連度
- 更新日時
- Knowledge分類

引用元を確認できるようにする。

---

# 10. MCP表示

利用Tool

- GitHub
- Teams
- Outlook
- SharePoint
- Notion
- Jira

利用したToolを履歴へ表示する。

---

# 11. 添付ファイル

対応

- PDF
- Word
- Excel
- CSV
- PNG
- JPG

アップロード後にOCR解析を実行できる。

---

# 12. 音声入力

利用

Azure AI Speech

対応

- Speech To Text
- リアルタイム入力
- 多言語認識

マイクボタンから開始する。

---

# 13. AI回答

対応

- Markdown
- Table
- Code
- Chart
- Link
- File

コードブロックのコピー機能を提供する。

---

# 14. Conversation History

保存項目

- タイトル
- Agent
- 日時
- Token数
- Cost

過去履歴を検索可能とする。

---

# 15. Quick Action

表示

- 新しいチャット
- 履歴
- Agent切替
- Clear
- Export
- Feedback

---

# 16. API

```
POST

/api/v1/ai/chat
```

```
GET

/api/v1/ai/history
```

```
POST

/api/v1/ai/upload
```

```
POST

/api/v1/ai/speech
```

AI APIを利用する。

---

# 17. UIコンポーネント

利用

- Drawer
- Scroll Area
- Textarea
- Button
- Card
- Badge
- Avatar
- Tabs
- Tooltip
- Markdown Viewer

shadcn/uiを利用する。

---

# 18. 状態表示

対応

- Thinking
- Streaming
- Loading
- Error
- Success

ストリーミング表示を標準とする。

---

# 19. セキュリティ

実装

- RBAC
- Prompt Guard
- PIIマスキング
- Content Safety
- HTTPS

アップロードファイルはウイルススキャン後に解析する。

---

# 20. パフォーマンス

目標

初回応答

```
2秒以内
```

ストリーミング開始

```
1秒以内
```

Function Calling

```
1秒以内
```

RAG検索

```
3秒以内
```

---

# 21. アクセシビリティ

対応

- キーボード操作
- Focus表示
- Screen Reader
- ARIA属性
- WCAG 2.2 AA

---

# 22. デザインルール

- CopilotライクなUI
- AI回答は吹き出し表示
- Function実行は折りたたみ表示
- RAG引用は回答下部へ表示
- AI Agentは色分けしない
- 右サイドパネルで全画面共通利用

---

# 23. 将来拡張

- マルチAI会話
- AI画面操作
- AI Workflow生成
- AIコード生成
- AIプレゼン作成
- AI議事録共同編集
- AI動画解析
- AI画像生成
- AI自動タスク作成
- AIパーソナルアシスタント
