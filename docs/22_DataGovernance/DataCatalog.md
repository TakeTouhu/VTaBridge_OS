# Data Catalog 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Data Catalogは、VTaBridge OSにおけるデータ資産を検索・理解・評価・利用するための統合カタログ設計である。

Microsoft Purviewを中核とし、Microsoft Fabric、Azure Data Lake、Dataverse、Power BI、SQL、SaaSデータを横断的に可視化する。

---

# 2. 目的

- データ資産の可視化
- 検索性向上
- 再利用促進
- データ理解の迅速化
- ガバナンス強化
- AI活用支援

---

# 3. 基本方針

- Metadata First
- Search First
- Automated Scanning
- Business Context
- Security Trimming
- Continuous Curation

---

# 4. 管理対象

- Dataset
- Table
- Column
- File
- Data Product
- Report
- Semantic Model
- Pipeline
- API
- AI Dataset

---

# 5. カタログ情報

- Asset Name
- Description
- Owner
- Steward
- Domain
- Classification
- Quality Score
- Lineage
- Sensitivity
- Usage Status

---

# 6. 登録フロー

```text
Source Registration
↓
Automated Scan
↓
Metadata Extraction
↓
Classification
↓
Owner Assignment
↓
Business Enrichment
↓
Publication
↓
Periodic Review
```

---

# 7. 検索機能

- Keyword Search
- Semantic Search
- Faceted Search
- Domain Search
- Owner Search
- Classification Search
- Lineage Search
- Natural Language Search

---

# 8. KPI

- Catalog Coverage
- Metadata Completeness
- Search Success Rate
- Certified Asset Rate
- Owner Assignment Rate
- Monthly Active Users

---

# 9. セキュリティ

- Microsoft Entra ID
- RBAC
- ACL連携
- Sensitive Data Masking
- Audit Log
- Access Review

---

# 10. 運用

- データソース登録
- スキャン監視
- メタデータ補完
- 認定データ管理
- 利用状況分析
- 定期棚卸し

---

# 11. 将来構想

AIが利用目的に適したデータ資産を推薦し、品質・機密性・鮮度・利用条件を考慮したData Discoveryを実現する。
