# Azure Container Apps 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Azure Container Apps（ACA）は、VTaBridge OSのアプリケーション実行基盤として採用する。

Kubernetesを意識することなくコンテナアプリケーションを実行できるサーバーレスコンテナサービスとして、Frontend・Backend API・AI API・Worker群をホストする。

---

# 2. 目的

Azure Container Apps導入目的

- コンテナ実行
- オートスケール
- サーバーレス運用
- コスト最適化
- 高可用性
- マネージド運用
- DevOps効率化

---

# 3. 全体構成

```
Internet

↓

Azure Front Door

↓

Azure Container Apps Environment

├── Frontend
├── Backend API
├── AI API
├── Python Worker
├── Playwright Worker
└── Scheduler

↓

Azure Database for PostgreSQL

↓

Azure Storage

↓

Azure Monitor
```

---

# 4. Container Apps Environment

Environmentは環境ごとに分離する。

対象

- Development
- Test
- Staging
- Production

各環境でネットワーク・ログ・スケール設定を独立して管理する。

---

# 5. Container Apps

対象サービス

| サービス | Ingress |
|-----------|---------|
| Frontend | External |
| Backend API | External |
| AI API | Internal |
| Python Worker | Internal |
| Playwright Worker | Internal |
| Scheduler | Internal |

公開範囲を最小限にする。

---

# 6. Revision

運用

- Single Revision
- Multiple Revision（リリース時）

Canary ReleaseやBlue/Green Deploymentに利用する。

---

# 7. Auto Scaling

スケール条件

- HTTPリクエスト数
- CPU使用率
- Memory使用率
- Queue件数

KEDAによるイベントドリブンスケーリングを利用する。

---

# 8. Managed Identity

利用対象

- Azure Key Vault
- Azure Storage
- Azure OpenAI
- Azure AI Search
- Azure Monitor

シークレットレス認証を基本とする。

---

# 9. Ingress

External

- Frontend
- Backend API

Internal

- AI API
- Worker
- Scheduler

HTTPSのみ許可する。

---

# 10. ネットワーク

実装

- Virtual Network Integration
- Private Endpoint
- Network Security Group
- Azure Firewall

内部通信はプライベートネットワークを利用する。

---

# 11. Dapr

利用機能

- Service Invocation
- Pub/Sub
- Secret Management
- State Store（将来対応）

マイクロサービス間通信を簡素化する。

---

# 12. ジョブ

Container Apps Jobsを利用

対象

- OCR
- PDF生成
- CSV取込
- AIバッチ
- 定期処理

長時間処理を分離して実行する。

---

# 13. 環境変数

設定対象

- Database URL
- API Endpoint
- Storage Account
- OpenAI Endpoint
- AI Search Endpoint

機密情報はManaged Identity経由で取得する。

---

# 14. ログ

出力先

- Azure Monitor
- Log Analytics
- Application Insights

構造化ログ（JSON）を標準とする。

---

# 15. 監視

監視項目

- CPU
- Memory
- Replica数
- Response Time
- HTTP Error
- Restart Count

Azure Monitorと統合する。

---

# 16. セキュリティ

実装

- Azure Entra ID
- Managed Identity
- TLS 1.3
- Azure Key Vault
- Defender for Cloud

コンテナイメージはACRからのみ取得する。

---

# 17. デプロイ

GitHub Actionsから実施

フロー

```
Build

↓

ACR Push

↓

Container Apps Update

↓

Health Check

↓

Traffic切替
```

Revisionを利用して無停止デプロイを行う。

---

# 18. パフォーマンス

目標

起動

```
30秒以内
```

Auto Scale

```
60秒以内
```

API応答

```
500ms以内
```

---

# 19. 運用

実施内容

- Revision管理
- イメージ更新
- ログ分析
- コスト監視
- スケール調整

Azure Advisorの推奨事項を定期的に確認する。

---

# 20. 将来拡張

- GPU Container Apps対応
- Dapr State Store活用
- Event Grid連携
- Azure Service Busスケーリング
- マルチリージョン構成
- 災害対策（DR）
- AIによるオートスケール最適化
- Azure Arc対応
- Workload Identity対応
- FinOps連携
