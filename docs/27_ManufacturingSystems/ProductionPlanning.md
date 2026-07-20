# Production Planning 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Production Planningは、需要・受注・在庫・能力・資材情報を基に最適な生産計画を策定する仕組みを定義する。

# 2. 管理対象

- 需要計画
- 基準生産計画
- 資材所要量計画
- 能力所要量計画
- 在庫計画
- 外注計画

# 3. 業務フロー

```text
Demand → Capacity Check → Material Check → Production Plan → Approval → MES Release
```

# 4. 主な機能

- 需要連携
- MPS/MRP
- 能力負荷確認
- シナリオ比較
- 計画承認
- 実績差異分析

# 5. AI活用

- 需要予測
- 欠品予測
- 能力制約検知
- 計画案自動生成
- リスクシミュレーション

# 6. KPI

- 計画達成率
- 納期遵守率
- 欠品率
- 在庫日数
- 計画変更頻度
