# MES Integration

Version: 1.0

Status: Draft

---

# 1. 概要

Digital TwinとMES間で生産指示、工程実績、品質、設備状態、ロット情報を連携する方式を定義する。

# 2. 連携データ

- Work Order
- Routing
- Operation Result
- Lot and Serial
- Quality Result
- Equipment Status

# 3. 連携方式

API、イベント、メッセージ、バッチを用途別に使い分ける。

# 4. 統制

一意識別、順序保証、重複排除、再送、監査ログを実装する。

# 5. 完成像

生産現場の実績をTwinへ反映し、計画差異と設備影響をリアルタイムに分析する。
