# Speech 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Speechは、Azure AI Speechを利用して音声認識・音声合成・リアルタイム文字起こし・話者分離・翻訳を提供するAI基盤である。

営業商談・オンライン会議・面接・社内会議の音声を解析し、議事録作成やAI分析へ活用する。

---

# 2. 目的

Speech導入目的

- 会議文字起こし
- AI議事録生成
- 音声翻訳
- AI音声対話
- 話者分析
- 面接分析
- 営業分析
- 音声検索

---

# 3. アーキテクチャ

```
Microphone

↓

Audio Upload

↓

Azure AI Speech

↓

Speech To Text

↓

Speaker Diarization

↓

Language Detection

↓

GPT-5.5

↓

Meeting API

↓

Knowledge Base

↓

RAG
```

---

# 4. 利用サービス

Azure AI Speech

利用機能

- Speech to Text
- Text to Speech
- Speaker Diarization
- Language Detection
- Translation
- Pronunciation Assessment

---

# 5. Speech To Text

入力

- MP3
- WAV
- M4A
- FLAC

出力

- テキスト
- タイムスタンプ
- 話者情報
- 信頼度

---

# 6. Text To Speech

利用用途

- AI Agent
- AIチャット
- 音声ガイド
- 音声通知
- 音声回答

対応言語

- 日本語
- 英語
- ベトナム語
- 中国語
- 韓国語

---

# 7. 話者分離

Speaker Diarization

取得項目

- Speaker ID
- 開始時間
- 終了時間
- 発話内容

---

# 8. リアルタイム字幕

リアルタイム処理

```
音声

↓

Speech

↓

字幕

↓

AI要約

↓

議事録
```

---

# 9. 翻訳

対応

- 日本語⇔英語
- 日本語⇔ベトナム語
- 英語⇔中国語
- 多言語翻訳

リアルタイム翻訳に対応する。

---

# 10. AI議事録

Speech結果をGPTへ渡す。

生成内容

- 要約
- 決定事項
- ToDo
- 課題
- 次回アクション

Meeting APIへ保存する。

---

# 11. 音声検索

検索対象

- 会議
- 商談
- 面接
- 社内会議

全文検索とEmbedding検索に対応する。

---

# 12. API

```
POST

/api/v1/ai/speech
```

```
POST

/api/v1/ai/transcribe
```

```
POST

/api/v1/ai/translate
```

```
POST

/api/v1/ai/text-to-speech
```

---

# 13. Prisma実装方針

Model

```
SpeechJob

SpeechTranscript

SpeechSpeaker

SpeechTranslation
```

Relation

```
Meeting

User

Project

AIConversation
```

---

# 14. ログ

保存項目

- UserID
- AudioFile
- Duration
- Language
- Model
- ResponseTime
- Accuracy
- Timestamp

---

# 15. セキュリティ

実装

- Azure Entra ID
- RBAC
- Blob Storage
- TLS通信
- PIIマスキング
- Audit Log

音声ファイルは暗号化して保存する。

---

# 16. 性能目標

リアルタイム文字起こし

```
1秒以内
```

音声認識完了

```
5秒以内
```

AI議事録生成

```
10秒以内
```

---

# 17. エラー処理

エラー時

- 自動リトライ
- 音声品質チェック
- ノイズ除去
- ユーザー通知

---

# 18. AI分析

AIが分析する内容

- 会話要約
- 感情分析
- 発話比率
- 話題分類
- キーワード抽出
- 商談成功率予測

---

# 19. 外部連携

対応サービス

- Microsoft Teams
- Zoom
- Google Meet
- Webex

録画・録音データを直接解析できる。

---

# 20. 将来拡張

- Voice Agent
- 音声コマンド操作
- リアルタイム同時通訳
- AIプレゼンテーション支援
- 音声感情分析
- AI営業コーチング
- 音声認証
- 多話者会議分析
- AI音声要約
- 音声BI分析
