# Manufacturing Security 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Manufacturing Securityは、製造システム・OTネットワーク・設備・データ・ユーザーを保護するセキュリティ設計を定義する。

# 2. 保護対象

- ERP/MES/SCADA
- PLC/HMI
- Edge Device
- 製造ネットワーク
- 製造データ
- 保守端末

# 3. 基本方針

- Zero Trust for OT
- Defense in Depth
- Least Privilege
- Network Segmentation
- Secure Remote Access
- Continuous Monitoring

# 4. 主な対策

- ID・権限管理
- OTネットワーク分離
- 脆弱性管理
- アプリケーション制御
- ログ監視
- バックアップ・復旧

# 5. インシデント対応

```text
Detect → Isolate → Assess → Recover → Investigate → Improve
```

# 6. KPI

- 未修正脆弱性数
- 不正アクセス件数
- 検知時間
- 復旧時間
- バックアップ成功率
- 教育受講率
