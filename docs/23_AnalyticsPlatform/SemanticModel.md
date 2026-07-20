# Semantic Model 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Semantic Modelは、業務データを共通指標・用語・関係性として整理し、組織全体で一貫した分析を実現する基盤である。

Power BI Semantic ModelとMicrosoft Fabricを中核に、再利用可能なメジャー、ディメンション、アクセス制御を提供する。

---

# 2. 目的

- KPI定義統一
- 分析品質向上
- 再利用促進
- セルフサービスBI支援
- レポート開発効率化
- ガバナンス強化

---

# 3. 基本方針

- Semantic Model First
- Reuse First
- Certified Dataset
- Business Glossary Alignment
- Security by Design
- Performance by Design

---

# 4. 管理対象

- Table
- Relationship
- Measure
- Hierarchy
- Calculation Group
- Business Term
- Dataset
- Refresh Policy

---

# 5. モデル構成

```text
Data Source
↓
Curated Data
↓
Semantic Model
↓
Business Measures
↓
Power BI Report
↓
Decision Making
```

---

# 6. 主な機能

- スタースキーマ
- DAXメジャー
- 階層管理
- 計算グループ
- 用語定義
- モデル認証
- 増分更新
- 利用状況分析

---

# 7. AI活用

- Measure Generation
- Model Recommendation
- Natural Language Query
- Relationship Detection
- Performance Optimization
- Metadata Enrichment

---

# 8. KPI

- Certified Model Usage
- Measure Reuse Rate
- Refresh Success Rate
- Query Response Time
- Duplicate KPI Reduction
- User Satisfaction

---

# 9. Integration

- Microsoft Fabric
- Power BI
- OneLake
- Microsoft Purview
- Excel
- AI Platform

---

# 10. セキュリティ

- Row-Level Security
- Object-Level Security
- RBAC
- Sensitivity Label
- Encryption
- Audit Log

---

# 11. ガバナンス

- KPI Definition Standard
- Naming Convention
- Certification Process
- Change Management
- Ownership
- Continuous Improvement

---

# 12. 将来構想

AIが業務用語とデータ構造を理解し、最適なモデル・指標・関係性を自動提案するEnterprise Semantic Layerを実現する。
