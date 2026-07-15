# VTaBridge OS

> AI Native Business Operating System

![Version](https://img.shields.io/badge/version-v0.1-blue)
![Status](https://img.shields.io/badge/status-Design-yellow)
![License](https://img.shields.io/badge/license-Private-red)

---

# 概要

VTaBridge OS は、VTaBridge株式会社専用に設計された AI ネイティブ経営OSです。

営業活動から案件管理、見積作成、契約、請求、入金確認、経営分析までを一元管理し、
AI・API・RPA を組み合わせることで、社長が「判断」に集中できる環境を構築することを目的としています。

本プロジェクトは Claude Code を利用した AI 駆動開発を前提としています。

---

# プロジェクト目的

VTaBridge OS の目的は以下です。

- 営業業務の自動化
- AIによる業務支援
- 経営状況のリアルタイム可視化
- 属人化の排除
- AIを活用した意思決定支援
- 将来的なSaaS化

---

# 開発方針

本プロジェクトは以下の設計思想に基づいて開発します。

- AI First
- API First
- Event Driven Architecture
- Clean Architecture
- Domain Driven Design (DDD)
- Human in the Loop

---

# システム構成

VTaBridge OS は以下のモジュールで構成されます。

| Module | Description |
|---------|-------------|
| CEO Dashboard | 経営ダッシュボード |
| Sales OS | 営業管理 |
| Communication OS | メール・チャット管理 |
| Project OS | 案件管理 |
| Proposal OS | 見積・契約・請求 |
| Finance OS | 売上・利益管理 |
| Knowledge OS | ナレッジ管理 |
| AI Manager | AI統括システム |
| RPA Manager | RPA統括システム |

---

# ディレクトリ構成

```text
VTaBridge-OS

├── README.md
├── CLAUDE.md
├── docs
├── diagrams
├── schemas
├── prompts
├── examples
├── assets
└── word
```

---

# ドキュメント一覧

| No | Document | Status |
|----|----------|--------|
| 00 | Architecture | 🚧 |
| 01 | System Architecture | ⏳ |
| 02 | Database Design | ⏳ |
| 03 | API Design | ⏳ |
| 04 | UI / UX Design | ⏳ |
| 05 | Workflow Design | ⏳ |
| 06 | AI Manager | ⏳ |
| 07 | AI Agents | ⏳ |
| 08 | RPA Design | ⏳ |
| 09 | Security | ⏳ |
| 10 | Deployment | ⏳ |

---

# 開発ルール

本プロジェクトでは以下を必須とします。

- Markdownを設計書の正本とする
- Wordはレビュー用成果物とする
- Mermaidで図を管理する
- API仕様は OpenAPI を採用
- DB設計は Prisma Schema を採用
- AI設計は JSON Schema を採用
- ADR (Architecture Decision Record) を記録する

---

# 使用予定技術

## Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui

## Backend

- Next.js API
- PostgreSQL
- Prisma ORM

## AI

- OpenAI GPT
- Claude
- Gemini

## Automation

- Power Automate
- PowerShell
- RPA

## Authentication

- Microsoft Entra ID
- Google OAuth

---

# 開発フェーズ

## Phase 0

Project Setup

## Phase 1

Architecture

## Phase 2

Database

## Phase 3

Workflow

## Phase 4

API

## Phase 5

UI

## Phase 6

AI

## Phase 7

RPA

## Phase 8

Testing

## Phase 9

Deployment

---

# 最終目標

VTaBridge OS を、

「社長が判断だけに集中できるAIネイティブ経営OS」

として完成させる。

また、将来的には VTaBridge株式会社のサービスとしてSaaS化することを目指す。
