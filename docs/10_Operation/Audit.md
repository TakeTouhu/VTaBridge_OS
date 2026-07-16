# Audit 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Auditは、VTaBridge OSにおける監査・証跡管理・コンプライアンス対応を実現するための設計を定義する。

利用者操作・システム変更・認証・AI利用・管理操作などの監査ログを適切に取得・保管し、内部統制・セキュリティ・法令対応を支援する。

---

# 2. 目的

Audit導入目的

- 内部統制強化
- 証跡管理
- コンプライアンス対応
- セキュリティ向上
- 不正検知
- インシデント調査

---

# 3. 監査対象

対象

- ログイン
- ログアウト
- ユーザー管理
- 権限変更
- データ更新
- Workflow変更
- AI利用
- システム設定変更
- API利用
- デプロイ

---

# 4. 監査ログ

取得項目

- 実行日時
- ユーザーID
- ロール
- 操作内容
- 対象リソース
- IPアドレス
- User Agent
- 実行結果

改ざん防止を考慮した形式で保存する。

---

# 5. ログ保存先

保存先

- Azure Monitor
- Log Analytics
- Azure Storage（長期保管）

ログは一元管理する。

---

# 6. アクセス監査

対象

- ログイン
- MFA
- ログアウト
- 認証失敗
- 権限エラー

認証イベントをすべて記録する。

---

# 7. 権限監査

対象

- RBAC変更
- ロール変更
- 管理者追加
- 権限付与
- 権限削除

権限変更履歴を保持する。

---

# 8. データ監査

対象

- 顧客
- エンジニア
- 案件
- 契約
- 請求
- Workflow

CRUD操作を監査対象とする。

---

# 9. AI監査

対象

- Prompt実行
- AI Agent利用
- Function Calling
- RAG検索
- OCR実行

AI利用履歴を監査対象とする。

---

# 10. システム監査

対象

- デプロイ
- Infrastructure変更
- Terraform Apply
- GitHub Actions
- Container更新

運用変更を記録する。

---

# 11. API監査

取得項目

- API名
- Method
- URL
- Status Code
- Response Time
- 呼び出し元

異常なAPI利用を検知する。

---

# 12. 保持期間

Audit Log

```
7年間
```

Application Log

```
90日
```

Security Log

```
1年間
```

法令・契約要件に応じて見直す。

---

# 13. 改ざん防止

実装

- RBAC
- Immutable Storage（必要に応じて）
- Azure Storage Versioning
- Log Export

監査ログの完全性を確保する。

---

# 14. 検索・分析

利用

- KQL
- Azure Monitor
- Log Analytics

監査ログを迅速に検索できるようにする。

---

# 15. レポート

出力内容

- ログイン履歴
- 権限変更履歴
- AI利用履歴
- 管理操作
- API利用状況

月次・四半期ごとに作成する。

---

# 16. コンプライアンス

対応

- ISO/IEC 27001
- SOC 2
- GDPR
- 日本個人情報保護法
- Microsoft Security Benchmark

監査証跡として利用可能な形式を維持する。

---

# 17. セキュリティ

実施

- Defender for Cloud連携
- Sentinel連携（将来対応）
- 異常検知
- アクセス監査
- 権限棚卸し

セキュリティ監査を定期的に実施する。

---

# 18. KPI

管理項目

- 監査ログ取得率
- 異常検知件数
- 権限変更件数
- AI利用件数
- API監査件数

監査品質を定量的に評価する。

---

# 19. 運用

実施内容

- ログレビュー
- 権限棚卸し
- コンプライアンス監査
- レポート作成
- Runbook更新

監査結果を継続的な改善へ反映する。

---

# 20. 将来拡張

- Microsoft Sentinel統合
- AI異常検知
- AI監査レポート生成
- UEBA（User and Entity Behavior Analytics）
- SIEM高度化
- 監査ダッシュボード
- リアルタイム監査
- AIコンプライアンス分析
- 自動証跡生成
- Continuous Compliance
