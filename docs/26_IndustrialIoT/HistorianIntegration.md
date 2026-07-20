# Historian Integration

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Historian Integrationは、時系列設備データをIndustrial IoT基盤および分析基盤へ連携する設計を定義する。

# 2. 対象データ

- Process Value
- Equipment State
- Alarm
- Event
- Batch Context
- Quality Context

# 3. 連携方式

- Historian Connector
- OPC HDA / OPC UA
- API
- Bulk Export
- Streaming

# 4. 管理方針

- タグ辞書標準化
- 資産IDマッピング
- 時刻補正
- 圧縮ルール管理
- 保持期間管理
- 再取得手順整備

# 5. セキュリティ

- 読み取り専用接続
- 接続アカウント分離
- 暗号化
- アクセス監査

# 6. KPI

- データ取得成功率
- 欠損率
- 時刻ずれ
- 連携遅延
- タグ対応率
