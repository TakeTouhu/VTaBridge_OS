# DevSecOps 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

DevSecOpsは、VTaBridge OSの開発・ビルド・テスト・デプロイ・運用までのライフサイクル全体にセキュリティを組み込むための設計を定義する。

ソースコード・依存ライブラリ・コンテナ・Infrastructure as Code・クラウド環境を継続的に監査し、安全なソフトウェア供給（Secure Software Supply Chain）を実現する。

---

# 2. 目的

DevSecOps導入目的

- Secure SDLC
- Supply Chain Security
- 脆弱性管理
- コンプライアンス対応
- セキュアデプロイ
- 継続的セキュリティ監査
- ゼロトラスト運用

---

# 3. 全体アーキテクチャ

```
Developer

↓

GitHub

↓

GitHub Actions

↓

────────────────────────

SAST

Dependency Scan

Secret Scan

IaC Scan

Container Scan

License Check

────────────────────────

↓

Deploy

↓

Azure

↓

Defender for Cloud

↓

Security Dashboard
```

---

# 4. Secure SDLC

開発工程

- 要件定義
- 設計レビュー
- セキュアコーディング
- コードレビュー
- セキュリティテスト
- デプロイ
- 運用監視

全工程でセキュリティを考慮する。

---

# 5. SAST

Static Application Security Testing

対象

- TypeScript
- Python
- Terraform

利用ツール

- CodeQL
- Semgrep（将来対応）

Pull Request時に自動実行する。

---

# 6. DAST

Dynamic Application Security Testing

対象

- Frontend
- Backend API

利用ツール

- OWASP ZAP

Staging環境で定期実行する。

---

# 7. Dependency Scan

対象

- npm
- pnpm
- pip

利用

- Dependabot
- npm audit
- pip-audit

重大な脆弱性がある場合はビルドを停止する。

---

# 8. Secret Scan

検査対象

- API Key
- Token
- Password
- Connection String
- Private Key

GitHub Secret Scanningを利用する。

---

# 9. Container Security

対象

- Docker Image

利用

- Trivy
- Microsoft Defender for Cloud

Critical脆弱性があるイメージはデプロイしない。

---

# 10. IaC Security

対象

- Terraform

利用

- Checkov
- tfsec

Infrastructureの設定ミスを検出する。

---

# 11. SBOM

Software Bill of Materials

生成対象

- Frontend
- Backend
- Worker

CycloneDX形式を採用する。

---

# 12. Supply Chain Security

実装

- 署名付きイメージ（将来対応）
- 信頼済みレジストリ利用
- パッケージ検証
- 依存関係固定

信頼できる成果物のみ利用する。

---

# 13. Azure Security

利用

- Microsoft Defender for Cloud
- Microsoft Sentinel（将来対応）
- Azure Key Vault
- Azure Policy

Azure環境を継続監視する。

---

# 14. GitHub Security

利用

- CodeQL
- Dependabot
- Secret Scanning
- Branch Protection
- Required Reviews

mainブランチを保護する。

---

# 15. シークレット管理

保存先

- Azure Key Vault
- GitHub Secrets

ソースコード・Terraform Stateへシークレットを保存しない。

---

# 16. 認証・認可

実装

- Azure Entra ID
- RBAC
- Managed Identity
- MFA

最小権限の原則を適用する。

---

# 17. 監査

保存項目

- Login
- Deploy
- Secret Access
- Permission Change
- API Access

監査ログは改ざん防止を考慮して保存する。

---

# 18. コンプライアンス

対応予定

- ISO/IEC 27001
- SOC 2
- GDPR
- 日本個人情報保護法
- Microsoft Security Benchmark

---

# 19. 運用

実施内容

- 脆弱性レビュー
- パッチ適用
- ライブラリ更新
- イメージ更新
- 権限棚卸し

定期的なセキュリティレビューを実施する。

---

# 20. 将来拡張

- SLSA Level対応
- Cosign署名
- Sigstore連携
- AI脆弱性分析
- AIコードセキュリティレビュー
- AIポリシーチェック
- Runtime Protection
- CSPM強化
- CNAPP対応
- Security Score Dashboard
