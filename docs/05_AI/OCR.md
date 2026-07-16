# OCR 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

OCR（Optical Character Recognition）は、紙媒体やPDF、画像ファイルから文字情報を抽出し、VTaBridge OSへ構造化データとして登録する機能である。

Azure AI Document Intelligenceを利用し、高精度なOCRとAIによる文書解析を実現する。

---

# 2. 目的

OCR導入目的

- 履歴書取込
- 職務経歴書解析
- 契約書登録
- 請求書登録
- 名刺OCR
- 提案書解析
- 手書き文書解析
- PDF検索対応

---

# 3. アーキテクチャ

```
PDF

Image

Scan

↓

Upload

↓

Azure Blob Storage

↓

Azure AI Document Intelligence

↓

OCR Parser

↓

Structured Data

↓

Validation

↓

Business API

↓

PostgreSQL

↓

Embedding生成

↓

Knowledge Base
```

---

# 4. 対応ファイル

対応形式

- PDF
- JPG
- JPEG
- PNG
- TIFF
- BMP
- DOCX
- XLSX

---

# 5. OCR対象

対象文書

- 履歴書
- 職務経歴書
- 契約書
- 見積書
- 請求書
- 発注書
- 名刺
- 会議資料
- 提案書
- マニュアル

---

# 6. Azure Document Intelligence

利用機能

- Read OCR
- Layout
- Key Value Pair
- Table Extraction
- Selection Mark
- Handwriting
- Custom Model

---

# 7. 文書解析

抽出項目

- タイトル
- 氏名
- 日付
- 金額
- 契約番号
- メールアドレス
- 電話番号
- スキル
- 資格
- テーブル

---

# 8. 名刺OCR

取得項目

- 氏名
- 会社名
- 部署
- 役職
- メール
- 電話番号
- 住所
- Webサイト

取得後はContactへ登録する。

---

# 9. 履歴書OCR

取得項目

- 氏名
- 生年月日
- 学歴
- 職歴
- スキル
- 資格
- 語学
- 自己PR

Engineerへ登録する。

---

# 10. 契約書OCR

取得項目

- 契約番号
- 契約日
- 開始日
- 終了日
- 契約金額
- 契約種別
- 当事者

Contractへ登録する。

---

# 11. AI補正

OCR後にAIが実施

- 誤認識補正
- 表記ゆれ補正
- 項目補完
- 住所正規化
- 氏名正規化
- 日付正規化

---

# 12. Validation

チェック内容

- 必須項目
- データ型
- 日付形式
- メール形式
- 電話番号形式
- 金額形式

エラー時はユーザー確認を要求する。

---

# 13. RAG連携

OCR完了後

```
Document

↓

Chunk

↓

Embedding

↓

Knowledge Base

↓

Azure AI Search
```

自動登録する。

---

# 14. Prisma実装方針

Model

```
OCRDocument

OCRResult

OCRField

OCRTable

OCRJob
```

Relation

```
Engineer

Contract

Invoice

Company

Contact
```

---

# 15. API

```
POST

/api/v1/ai/ocr
```

```
GET

/api/v1/ai/ocr/{id}
```

```
POST

/api/v1/ai/ocr/{id}/retry
```

---

# 16. ログ

保存項目

- UserID
- FileName
- FileSize
- OCRModel
- ResponseTime
- Accuracy
- Timestamp

---

# 17. セキュリティ

実装

- Entra ID
- RBAC
- Blob SAS Token
- PII Masking
- Audit Log
- Encryption at Rest
- TLS通信

---

# 18. 性能目標

OCR解析

```
10秒以内
```

履歴書解析

```
15秒以内
```

契約書解析

```
20秒以内
```

---

# 19. エラー処理

OCR失敗時

- リトライ
- AI補正
- ユーザー確認
- 手動入力へ切替

---

# 20. 将来拡張

- AIフォーム自動生成
- レイアウト学習
- AI帳票解析
- QRコード解析
- バーコード解析
- パスポートOCR
- 運転免許証OCR
- マイナンバーカードOCR
- 多言語OCR
- リアルタイムOCR
