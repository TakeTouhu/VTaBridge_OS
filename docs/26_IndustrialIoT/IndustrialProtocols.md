# Industrial Protocols

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Industrial Protocolsは、産業設備との相互運用性を確保するための通信プロトコル標準を定義する。

# 2. 対象プロトコル

- OPC UA
- MQTT
- Modbus TCP
- PROFINET
- EtherNet/IP
- BACnet
- REST API

# 3. 適用方針

- OPC UAを設備情報モデルの標準とする
- MQTTをイベント・テレメトリ連携に利用する
- レガシープロトコルはGatewayで変換する
- 新規連携は暗号化と認証を必須とする

# 4. 管理項目

- Endpoint
- Namespace
- Topic
- Tag
- Certificate
- Version
- Owner

# 5. セキュリティ

- TLS
- 証明書認証
- Topic ACL
- 接続元制限
- プロトコル監視

# 6. KPI

- 標準プロトコル採用率
- 接続成功率
- 変換エラー率
- 証明書更新率
