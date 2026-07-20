# Data Access Governance 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Data Access Governanceは、データへのアクセス申請、承認、付与、利用、定期レビュー、剥奪を統制するための設計である。

---

# 2. 目的

- 最小権限の徹底
- 不正アクセス防止
- 職務分離
- アクセス透明性向上
- 監査対応
- 自動化促進

---

# 3. 管理対象

- User
- Role
- Group
- Dataset
- Access Policy
- Approval
- Entitlement
- Exception

---

# 4. 基本方針

- Least Privilege
- Need to Know
- Zero Trust
- Segregation of Duties
- Time-Bound Access
- Continuous Review

---

# 5. 業務フロー

```text
Access Request
↓
Policy Evaluation
↓
Owner Approval
↓
Access Provisioning
↓
Usage Monitoring
↓
Periodic Review
↓
Revocation
```

---

# 6. 主な機能

- アクセス申請
- 承認ワークフロー
- ロール管理
- 期限付きアクセス
- 定期棚卸し
- 利用監視
- 例外管理
- 自動剥奪

---

# 7. AI活用

- 権限推薦
- 過剰権限検知
- 異常アクセス検知
- 承認リスク評価
- 利用状況分析
- 剥奪候補抽出

---

# 8. KPI

- Access Review Completion Rate
- Excess Privilege Count
- Orphan Account Count
- Approval Lead Time
- Revocation Lead Time
- Policy Violation Count
- Temporary Access Ratio

---

# 9. Integration

- Microsoft Entra ID
- Microsoft Purview
- Microsoft Fabric
- Azure
- Microsoft 365
- Dataverse
- PAM
- SIEM

---

# 10. セキュリティ

- MFA
- Conditional Access
- RBAC
- ABAC
- Privileged Identity Management
- Audit Log

---

# 11. 将来構想

AIが業務役割・利用目的・データ機密度・行動リスクを評価し、アクセス権を動的に付与・制限するAdaptive Data Access Governanceを実現する。
