# Analytics Security 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Analytics Securityは、分析データ・モデル・レポート・ワークスペースを保護し、適切な利用者だけが必要な情報へアクセスできるようにする基盤である。

Microsoft Entra ID、Microsoft Purview、Microsoft Fabric、Power BIのセキュリティ機能を統合して実装する。

---

# 2. 目的

- 機密データ保護
- 不正アクセス防止
- 権限最小化
- 外部共有統制
- 監査対応
- コンプライアンス遵守

---

# 3. 基本方針

- Zero Trust
- Least Privilege
- Defense in Depth
- Data Centric Security
- Segregation of Duties
- Continuous Monitoring

---

# 4. 管理対象

- User
- Group
- Workspace
- Dataset
- Semantic Model
- Report
- Data Source
- Sharing Link

---

# 5. セキュリティフロー

```text
User Authentication
↓
Conditional Access
↓
Workspace Authorization
↓
Data-Level Security
↓
Usage Monitoring
↓
Audit / Review
```

---

# 6. 主な機能

- RBAC
- Row-Level Security
- Object-Level Security
- Sensitivity Label
- DLP
- Private Endpoint
- External Sharing Control
- Audit Log

---

# 7. AI活用

- Risk Detection
- Abnormal Access Detection
- Permission Recommendation
- Sensitive Data Detection
- Sharing Risk Analysis
- Security Summary

---

# 8. KPI

- Unauthorized Access Count
- Excess Permission Rate
- Access Review Completion
- Sensitive Data Coverage
- Security Incident Count
- Remediation Lead Time

---

# 9. Integration

- Microsoft Entra ID
- Microsoft Purview
- Microsoft Fabric
- Power BI
- Microsoft Defender
- Microsoft Sentinel

---

# 10. ガバナンス

- Access Control Policy
- Sharing Policy
- Classification Standard
- Quarterly Access Review
- Incident Response
- Continuous Improvement

---

# 11. 将来構想

AIがデータ機密度・利用状況・役割を分析し、最適なアクセス権と保護設定を継続的に適用するAdaptive Analytics Securityを実現する。
