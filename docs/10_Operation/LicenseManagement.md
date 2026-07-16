# License Management 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

License Managementは、VTaBridge OSで利用するクラウドサービス・ソフトウェア・OSS・AIサービス・商用ライブラリのライセンスを適切に管理するための設計を定義する。

ライセンスコンプライアンスを維持し、契約違反・コスト増加・セキュリティリスクを防止する。

---

# 2. 目的

License Management導入目的

- ライセンス遵守
- ソフトウェア資産管理（SAM）
- コスト最適化
- OSS管理
- 契約更新管理
- セキュリティ向上

---

# 3. 管理対象

対象

- Microsoft Azure
- Microsoft 365
- Azure OpenAI
- Azure AI Search
- GitHub Enterprise
- Docker
- Terraform
- OSSライブラリ
- 商用ライブラリ

---

# 4. ライセンス分類

分類

| 種類 | 例 |
|------|----|
| SaaS | Microsoft 365 |
| PaaS | Azure |
| AI Service | Azure OpenAI |
| OSS | React・FastAPI・Prisma |
| Commercial | Playwright Enterprise（利用時） |

ライセンス種別ごとに管理する。

---

# 5. OSS管理

対象

- npm
- pnpm
- Python Package
- Terraform Module

OSSライセンスを継続的に確認する。

---

# 6. OSSライセンス

対象

- MIT
- Apache License 2.0
- BSD
- MPL
- GPL（利用可否を評価）

ライセンス条件を確認したうえで採用する。

---

# 7. SBOM

Software Bill of Materials

対象

- Frontend
- Backend
- AI API
- Worker

CycloneDX形式を標準とする。

---

# 8. ライセンス監査

確認項目

- OSSライセンス
- 商用契約
- サブスクリプション
- 利用数
- 更新期限

定期監査を実施する。

---

# 9. Azure契約

対象

- Azure Subscription
- Resource利用量
- Azure OpenAI
- AI Search
- Storage
- PostgreSQL

Azure Cost Managementと連携する。

---

# 10. Microsoft契約

対象

- Microsoft 365
- Entra ID
- Defender
- Power Platform（利用時）

契約更新日を管理する。

---

# 11. GitHub

対象

- Enterprise
- Copilot
- Actions Minutes
- Packages

利用状況を定期的に確認する。

---

# 12. AIライセンス

対象

- Azure OpenAI
- GPTモデル
- Embedding Model
- AI Search

利用量・コスト・契約条件を管理する。

---

# 13. 更新管理

管理項目

- 契約開始日
- 契約終了日
- 更新期限
- 自動更新有無

期限前に更新計画を立てる。

---

# 14. ライブラリ管理

利用

- Dependabot
- GitHub Advisory
- npm audit
- pip-audit

脆弱性とライセンスを同時に確認する。

---

# 15. コンプライアンス

対応

- OSSライセンス遵守
- Microsoft利用規約
- Azure利用規約
- AI利用規約

利用条件を継続的に確認する。

---

# 16. レポート

出力内容

- ライセンス一覧
- 契約状況
- 更新期限
- OSS利用状況
- SBOM

月次レポートを作成する。

---

# 17. KPI

管理項目

- ライセンス遵守率
- 更新漏れ件数
- OSS利用数
- SBOM生成率
- 契約更新率

定期的にレビューする。

---

# 18. セキュリティ

実施

- SBOM管理
- Supply Chain Security
- OSS脆弱性確認
- ライセンス監査

安全なソフトウェア供給を維持する。

---

# 19. 運用

実施内容

- 契約更新
- OSS棚卸し
- SBOM更新
- コスト確認
- ライセンス監査

継続的にソフトウェア資産を管理する。

---

# 20. 将来拡張

- SPDX対応
- OSS Review Toolkit（ORT）
- AIライセンス分析
- FinOps統合
- ライセンスダッシュボード
- 自動契約更新通知
- AIコスト分析
- Continuous Compliance
- AI契約リスク分析
- Software Asset Management高度化
