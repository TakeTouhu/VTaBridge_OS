# Telemetry Ingestion 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Telemetry Ingestionは、センサー・設備・製品から送信される時系列データを安全かつ高可用に収集する基盤を定義する。

# 2. 対象データ

- Sensor Data
- Equipment Status
- Event
- Alarm
- Log
- Location

# 3. フロー

```text
Device → Gateway → Message Broker → Stream Processing → OneLake → Analytics
```

# 4. 主な機能

- ストリーム受信
- スキーマ検証
- 重複排除
- 時刻補正
- バッファリング
- ルーティング
- 永続化

# 5. 非機能要件

- スループット
- 低遅延
- 順序保証
- 再送
- バックプレッシャー
- 障害復旧

# 6. KPI

- 受信件数
- 取り込み遅延
- 欠損率
- エラー率
- 再処理件数
