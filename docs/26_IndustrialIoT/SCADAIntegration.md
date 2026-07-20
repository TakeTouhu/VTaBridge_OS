# SCADA Integration

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

SCADA Integrationは、監視制御システムとIndustrial IoT基盤を安全に連携する設計を定義する。

# 2. 連携対象

- Tag Data
- Alarm
- Event
- Equipment Status
- Operator Action
- Production Context

# 3. 連携方式

- OPC UA
- Historian連携
- Message Broker
- API
- ファイル連携

# 4. 方針

- 読み取り連携を標準とする
- 制御命令は個別承認する
- SCADA負荷を最小化する
- タグ命名と資産IDを統一する
- 時刻同期を保証する

# 5. セキュリティ

- DMZ経由
- 接続元制限
- 証明書認証
- 操作監査
- 異常通信検知

# 6. KPI

- データ取得成功率
- タグ欠損率
- アラーム連携遅延
- SCADA影響件数
