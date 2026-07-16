# Network Security 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Network Securityは、VTaBridge OSにおけるネットワーク境界・通信経路・アクセス制御・ネットワーク分離・外部公開・内部通信を保護するための設計を定義する。

Microsoft Azureのネットワークセキュリティサービスを活用し、Zero Trust NetworkおよびDefense in Depthに基づく多層防御を実現する。

---

# 2. 目的

Network Security導入目的

- 不正アクセス防止
- 通信保護
- ネットワーク分離
- 外部攻撃対策
- 可用性向上
- Zero Trust Network実現

---

# 3. 基本方針

採用方針

- Zero Trust Network
- Defense in Depth
- Private First
- Least Exposure
- Secure by Default
- Network Segmentation

公開範囲を最小限に抑える。

---

# 4. ネットワーク構成

```
Internet

↓

Azure Front Door (WAF)

↓

Azure Container Apps

↓

Backend API

↓

Private Endpoint

↓

PostgreSQL

↓

Azure Storage

↓

Azure OpenAI

↓

Azure AI Search
```

内部通信は可能な限りプライベートネットワークを利用する。

---

# 5. Azure Front Door

役割

- HTTPS終端
- WAF
- CDN
- 負荷分散
- グローバルルーティング

インターネット公開入口として利用する。

---

# 6. Web Application Firewall

実装

- OWASP Managed Rule
- Custom Rule
- IP Filter
- Geo Filter
- Bot Protection

Web攻撃を検知・遮断する。

---

# 7. Azure Firewall

対象

- Outbound通信
- Inbound通信
- FQDN制御
- Application Rule
- Network Rule

ネットワーク通信を集中管理する。

---

# 8. Network Security Group

対象

- Subnet
- Private Endpoint
- 管理ネットワーク

不要なポート・プロトコルを遮断する。

---

# 9. Private Endpoint

対象

- PostgreSQL
- Azure Storage
- Key Vault
- Azure OpenAI
- Azure AI Search

PaaSサービスへのアクセスをプライベートネットワークへ限定する。

---

# 10. 通信暗号化

対象

- HTTPS
- REST API
- Database接続
- Azure Service通信

TLS 1.2以上を必須とする。

---

# 11. DDoS Protection

利用

- Azure DDoS Protection Standard（必要時）
- Azure Front Door

大規模攻撃への耐性を確保する。

---

# 12. 通信制御

許可対象

- HTTPS（443）
- SSH（運用時のみ）
- Azure内部通信

不要なポートは開放しない。

---

# 13. ネットワーク分離

分離対象

- Production
- Staging
- Development
- Test

環境間の通信を制限する。

---

# 14. AI通信

対象

- Azure OpenAI
- Azure AI Search
- AI Agent

Managed IdentityおよびPrivate Endpointを利用する。

---

# 15. 監視

監視対象

- Firewall Log
- NSG Flow Log
- WAF Log
- DDoS Log
- Traffic Analytics

Azure Monitorへ集約する。

---

# 16. インシデント対応

対象

- 不正アクセス
- DDoS攻撃
- ポートスキャン
- 通信異常
- Firewall検知

Runbookに従って対応する。

---

# 17. KPI

管理項目

- WAF検知件数
- Firewall拒否件数
- DDoS検知件数
- Private Endpoint利用率
- TLS適用率

定期的に分析する。

---

# 18. ベストプラクティス

- Private Endpointを優先する
- インターネット公開を最小限にする
- WAFを必須とする
- NSGで不要通信を遮断する
- 通信ログを監査対象とする

---

# 19. 運用

実施内容

- Firewallルールレビュー
- NSGレビュー
- WAFルール更新
- 通信分析
- セキュリティ監査

継続的にネットワーク防御を改善する。

---

# 20. 将来拡張

- Azure Virtual WAN
- Azure Bastion
- Network Virtual Appliance（NVA）
- Service Mesh（Istio等）
- eBPFベース監視
- AI通信異常検知
- Zero Trust Network Analytics
- Network Security Dashboard
- Micro Segmentation
- Autonomous Network Security
