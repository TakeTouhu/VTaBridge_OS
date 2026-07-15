# 00 Architecture

Version: 1.0

Status: Draft

---

# 1. 目的

VTaBridge OS は、VTaBridge株式会社の業務を AI・API・RPA を活用して自動化し、
営業・案件管理・契約・請求・経営判断までを一元管理する AI Native Business Operating System である。

本設計書では VTaBridge OS 全体の設計思想とアーキテクチャを定義する。

---

# 2. システムコンセプト

VTaBridge OS は、

「社長が入力するシステム」

ではない。

「社長が判断するためのシステム」

である。

すべてのデータは AI により収集・整理され、
必要な情報のみを人へ提示する。

---

# 3. システムの目的

VTaBridge OS の目的は以下である。

- 営業活動の自動化
- 案件情報の一元管理
- AIによるメール支援
- AIによる議事録作成
- 見積・契約・請求の効率化
- 経営状況のリアルタイム可視化
- 属人化の排除
- 将来的なSaaS化

---

# 4. 設計思想

## AI First

AIを前提として設計する。

人が入力することを前提にしない。

---

## API First

APIで実現できる機能はAPIを優先する。

RPAは最後の手段とする。

---

## Event Driven

システム内のすべての処理はイベントを起点とする。

例

Meeting Completed

↓

Generate Minutes

↓

Create Tasks

↓

Update CRM

↓

Notify CEO

---

## Human in the Loop

AIは提案する。

最終判断は人間が行う。

---

# 5. Project中心設計

VTaBridge OS は Project（案件）を中心に管理する。

Projectには以下が紐付く。

- Customer
- Meeting
- Mail
- Task
- Proposal
- Contract
- Invoice
- Payment
- Engineer
- Source Code

---

# 6. コアシステム

VTaBridge OS は以下のモジュールで構成される。

- CEO Dashboard
- AI Manager
- Sales OS
- Communication OS
- Proposal OS
- Project OS
- Finance OS
- Knowledge OS
- RPA Manager

---

# 7. AIの役割

AIの役割は以下とする。

- メール解析
- メール返信案作成
- 議事録作成
- TODO抽出
- リスク検知
- 顧客分析
- 売上予測
- 見積作成補助

AIは契約締結や送金などの重要な処理を自動実行しない。

---

# 8. RPAの役割

RPAは以下に限定する。

- GUI操作
- Legacyシステム入力
- ブラウザ操作
- ファイル操作

業務判断をRPAに持たせない。

---

# 9. アーキテクチャ概要

VTaBridge OS は以下のレイヤーで構成する。

- Presentation
- Application
- Domain
- Infrastructure

各レイヤーの責務は今後の設計書で定義する。

---

# 10. この章で定義する範囲

本章では以下のみを定義する。

- システム思想
- 基本方針
- アーキテクチャ方針

詳細な実装仕様は以降の章で定義する。
