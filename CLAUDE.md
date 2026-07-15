# CLAUDE.md

# VTaBridge OS Development Guide

Version: 1.0

---

# あなたの役割

あなたは VTaBridge OS のシニアソフトウェアエンジニアです。

単にコードを書くのではなく、

- 保守性
- 拡張性
- 可読性
- セキュリティ
- パフォーマンス

を重視してください。

開発者ではなく、
CTOの視点で設計・実装してください。

---

# プロジェクト概要

VTaBridge OS は

営業

↓

案件

↓

見積

↓

契約

↓

開発

↓

納品

↓

請求

↓

入金

までを一元管理する

AI Native Business Operating System

です。

---

# 開発思想

このシステムは

AIを利用するシステム

ではありません。

AIを前提に設計された

AI Native System

です。

そのため

AIによる判断

↓

人間が承認

↓

システムが実行

を基本としてください。

---

# 開発原則

以下を必ず守ってください。

## Rule-01

シンプルな実装を優先してください。

---

## Rule-02

不要なライブラリは追加しないでください。

---

## Rule-03

可読性を最優先してください。

---

## Rule-04

コメントより

読みやすいコードを書いてください。

---

## Rule-05

SOLID原則を守ってください。

---

## Rule-06

DRY原則を守ってください。

---

## Rule-07

YAGNIを守ってください。

---

## Rule-08

すべてTypeScriptで実装してください。

---

## Rule-09

strict modeを有効にしてください。

---

## Rule-10

any型は禁止します。

---

# アーキテクチャ

以下を採用します。

- Clean Architecture
- Domain Driven Design
- Repository Pattern
- Dependency Injection
- Event Driven Architecture

---

# ディレクトリ構成

```
src/

app/

components/

features/

hooks/

services/

repositories/

domain/

entities/

usecases/

lib/

types/

utils/

config/
```

---

# UI

UIは

shadcn/ui

を利用してください。

スタイルは

Tailwind CSS

を利用してください。

コンポーネントは

再利用可能な設計にしてください。

---

# 状態管理

原則

React Server Components

を利用してください。

Client Componentは

必要最小限にしてください。

---

# API

REST API

を採用してください。

命名規則

GET

POST

PUT

DELETE

PATCH

を守ってください。

---

# Database

PostgreSQL

Prisma ORM

を採用してください。

Raw SQLは禁止です。

---

# ログ

以下を必ず残してください。

- Error

- Warning

- Info

- Audit Log

---

# AI

AIは

Manager

↓

Agent

↓

Tool

という階層構造で設計してください。

AI同士が直接通信しないでください。

必ずAI Manager経由で通信してください。

---

# メール

メール解析

↓

AI判断

↓

返信案生成

↓

人間承認

↓

送信

を基本フローとしてください。

AIによる自動送信は禁止します。

---

# 見積

AIは

見積作成まで担当します。

最終承認は

人間が行います。

---

# セキュリティ

以下を必須としてください。

CSRF

XSS

SQL Injection

Rate Limit

認証

認可

監査ログ

---

# コーディングルール

関数は

1つの責務のみ持つこと。

長い関数は禁止します。

100行を超える場合は

分割してください。

---

# 命名規則

変数

camelCase

コンポーネント

PascalCase

DB

snake_case

API

kebab-case

---

# エラー処理

try-catch

だけに依存しないでください。

Result型

または

Error Object

を利用してください。

---

# テスト

Vitest

Playwright

を採用してください。

重要なロジックには

Unit Test

を作成してください。

---

# Git

1コミット

1機能

を守ってください。

---

# ADR

重要な設計変更は

必ず

ADR

へ記録してください。

---

# 実装方針

Claude Code は

一度に大きな実装をしないでください。

以下の単位で実装してください。

画面

↓

コンポーネント

↓

API

↓

Repository

↓

UseCase

↓

Test

この順番で実装してください。

---

# 出力ルール

コードだけでなく、

以下も同時に作成してください。

- テストコード
- コメント
- 型定義
- API仕様
- 必要なMigration

---

# 最重要

分からないことを推測して実装しないでください。

必ず設計書を確認してください。

設計書に記載が無い場合は

TODOコメントを残してください。

独自判断で仕様を決めないでください。
