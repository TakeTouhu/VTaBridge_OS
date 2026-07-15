# Database Rules

Version: 1.0

Status: Approved

---

# 1. 目的

本書は VTaBridge OS におけるデータベース設計ルールを定義する。

すべてのテーブル設計は本ルールに従うこと。

本ルールは

- Prisma Schema
- PostgreSQL
- API設計
- Claude Code

すべての基準となる。

---

# 2. 基本方針

VTaBridge OS は

Project（案件）

を中心にデータを管理する。

Customer を中心にしない。

User を中心にしない。

Project が唯一の業務の中心となる。

---

# 3. データベース

採用

- PostgreSQL

ORM

- Prisma ORM

文字コード

- UTF-8

タイムゾーン

- UTC保存
- 表示はAsia/Tokyo

---

# 4. 命名規則

## テーブル

複数形

例

customers

projects

meetings

tasks

mail_threads

mail_messages

---

## カラム

snake_case

例

project_id

customer_id

created_at

updated_at

---

## Enum

PascalCase

例

ProjectStatus

TaskPriority

InvoiceStatus

---

# 5. 主キー

全テーブル

UUID

```
id UUID
```

AUTO_INCREMENTは禁止

---

# 6. 外部キー

必ず外部キーを設定する。

例

```
project_id

customer_id

user_id
```

NULLを許可する場合は理由を記載すること。

---

# 7. 日時

すべてのテーブルに以下を持つ。

```
created_at

updated_at

deleted_at
```

deleted_at は論理削除用とする。

---

# 8. 論理削除

物理削除は禁止。

削除時は

deleted_at

を更新する。

---

# 9. ステータス管理

Booleanは禁止。

状態を持つものは Enum を利用する。

例

×

is_complete

〇

status

- Draft
- Pending
- Approved
- Completed
- Cancelled

---

# 10. 金額

金額は Decimal を利用する。

Floatは禁止。

例

```
amount Decimal
```

---

# 11. メールアドレス

VARCHAR(255)

インデックス付与

---

# 12. 電話番号

文字列

数値型は禁止

---

# 13. URL

VARCHAR(2048)

---

# 14. UUID生成

Prismaで生成する。

DB側では生成しない。

---

# 15. Index

必須

- created_at
- updated_at

必要に応じて追加

- status
- customer_id
- project_id
- engineer_id

---

# 16. AI関連

AIが生成したデータは

以下を保持する。

- ai_model
- ai_version
- ai_prompt
- ai_generated_at

必要に応じて

AI Log

へ保存する。

---

# 17. 監査

更新対象

- Before
- After
- User
- Timestamp

すべて Audit Log に保存する。

---

# 18. 添付ファイル

DBへ保存しない。

ファイルストレージへ保存する。

DBには

- URL
- サイズ
- MIME Type

のみ保持する。

---

# 19. JSON

自由入力は禁止。

JSONを利用する場合は

JSON Schema

を必ず定義する。

---

# 20. Null

Nullを許可する場合は

理由を設計書へ記載する。

---

# 21. 命名禁止

略称禁止

×

cust

proj

usr

〇

customer

project

user

---

# 22. AI実装ルール

Claude Code は

本ルールを最優先する。

独自判断で

型

カラム

テーブル

を追加してはならない。

---

# 23. 将来拡張

新しいテーブル追加時は

本書を更新する。

例外ルールは禁止する。

---

# 24. 設計レビュー

テーブル追加前に

以下を確認する。

- Projectに紐付くか
- Customerに紐付くか
- Userに紐付くか
- AI Log対象か
- Audit対象か

---

# 25. この章の責務

本章では

DB設計ルールのみ

を定義する。

テーブル設計は

個別設計書で定義する。
