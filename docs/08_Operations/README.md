# DevOps設計

Version: 1.0

Status: Draft

---

# 概要

本ディレクトリでは、VTaBridge OSのDevOps・CI/CD・インフラ運用・監視・セキュリティ・リリース戦略を管理する。

Infrastructure as Code（IaC）とGitOpsを基本方針とし、Azureを中心としたクラウドネイティブな運用基盤を構築する。

---

# 設計一覧

| No | ファイル | 内容 |
|----|---------|------|
| 01 | Architecture.md | DevOpsアーキテクチャ |
| 02 | GitStrategy.md | Git運用戦略 |
| 03 | GitHubActions.md | GitHub Actions |
| 04 | Docker.md | Docker設計 |
| 05 | AzureContainerApps.md | Azure Container Apps |
| 06 | Terraform.md | Terraform設計 |
| 07 | CICD.md | CI/CD設計 |
| 08 | Monitoring.md | 運用監視 |
| 09 | Security.md | DevSecOps |
| 10 | ReleaseStrategy.md | リリース戦略 |

---

# 採用技術

- GitHub
- GitHub Actions
- Docker
- Azure Container Apps
- Azure Container Registry
- Terraform
- Azure Monitor
- Application Insights
- Azure Key Vault
- Microsoft Defender for Cloud

---

# DevOps設計方針

- GitOps
- Infrastructure as Code
- Immutable Infrastructure
- DevSecOps
- Zero Downtime Deployment
- 自動テスト
- 自動デプロイ
- 自動監視

---

# CI/CD対象

対象

- Frontend
- Backend
- AI Services
- API
- Database Migration
- Terraform
- Docker Image

---

# インフラ構成

```
GitHub

↓

GitHub Actions

↓

Azure Container Registry

↓

Azure Container Apps

↓

Azure Database for PostgreSQL

↓

Azure Monitor

↓

Application Insights
```

---

# セキュリティ

対応

- Azure Entra ID
- Azure Key Vault
- RBAC
- Secret Scan
- Dependency Scan
- CodeQL

---

# ディレクトリ構成

```
08_DevOps/

├── README.md
├── Architecture.md
├── GitStrategy.md
├── GitHubActions.md
├── Docker.md
├── AzureContainerApps.md
├── Terraform.md
├── CICD.md
├── Monitoring.md
├── Security.md
└── ReleaseStrategy.md
```

---

# 更新履歴

| Version | Date | 内容 |
|----------|------|------|
| 1.0 | 2026-07 | 初版 |
