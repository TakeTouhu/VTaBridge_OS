# Data Protection 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Data Protectionは、VTaBridge OSで取り扱う業務データ・個人情報・AIデータ・ログ・バックアップのライフサイクル全体を保護するための設計を定義する。

データの分類・保存・利用・共有・バックアップ・アーカイブ・削除までを管理し、情報漏えい防止と法令遵守を実現する。

---

# 2. 目的

Data Protection導入目的

- 情報資産保護
- 個人情報保護
- データ漏えい防止
- コンプライアンス遵守
- AI利用時の安全性向上
- データライフサイクル管理

---

# 3. 保護対象

対象

- 顧客情報
- エンジニア情報
- 案件情報
- 契約情報
- 請求情報
- AI Prompt
- AI Response
- OCRデータ
- Embedding
- Audit Log

---

# 4. データ分類

| 分類 | 内容 |
|------|------|
| Public | 公開可能情報 |
| Internal | 社内利用情報 |
| Confidential | 機密情報 |
| Restricted | 極秘情報・個人情報 |

データ分類に応じて保護レベルを適用する。

---

# 5. 個人情報

対象

- 氏名
- メールアドレス
- 電話番号
- 住所
- 生年月日
- マイナンバー（保存しない）
- 履歴書情報

個人情報保護法およびGDPRを考慮する。

---

# 6. データ保存

保存先

- PostgreSQL
- Azure Storage
- Azure AI Search
- Backup Storage

保存データは暗号化する。

---

# 7. データアクセス制御

実装

- RBAC
- Resource Ownership
- Row Level Security（必要時）
- Azure RBAC

必要最小限のアクセス権を付与する。

---

# 8. データマスキング

対象

- 電話番号
- メールアドレス
- 住所
- 契約金額
- 個人識別情報

画面表示やログ出力時にマスキングを適用する。

---

# 9. 匿名化・仮名化

対象

- AI学習用データ
- 分析データ
- 統計データ
- テストデータ

個人を識別できない形式へ変換する。

---

# 10. AIデータ保護

対象

- Prompt
- AI Response
- OCR
- Embedding
- Vector Data

AIモデルへの不要な個人情報送信を防止する。

---

# 11. バックアップ

対象

- Database
- Blob Storage
- Audit Log
- AIデータ

バックアップデータも暗号化し、安全に保管する。

---

# 12. データ保持期間

| データ | 保持期間 |
|---------|---------|
| Audit Log | 7年 |
| Application Log | 90日 |
| AI利用ログ | 1年 |
| 業務データ | 契約・法令に準拠 |
| Backup | 90日（標準） |

法令・契約要件に応じて保持期間を変更する。

---

# 13. データ削除

対象

- 個人情報
- 契約終了データ
- 一時ファイル
- AIキャッシュ

削除時は復元不能な方法を採用する。

---

# 14. Data Loss Prevention（DLP）

実装

- Microsoft Purview（導入時）
- DLPポリシー
- メール制御
- ファイル共有制御
- AIデータ送信制御

機密情報の外部流出を防止する。

---

# 15. データ共有

共有対象

- 社内利用者
- AIサービス
- 外部システム

共有時は認証・認可・暗号化を必須とする。

---

# 16. 監査

取得項目

- データ参照
- データ更新
- データ削除
- エクスポート
- AI利用

すべて監査ログへ記録する。

---

# 17. KPI

管理項目

- データ暗号化率
- DLP検知件数
- 個人情報漏えい件数
- データ削除完了率
- 保持期間遵守率

継続的に評価する。

---

# 18. ベストプラクティス

- データ分類を徹底する
- 最小限のデータのみ収集する
- AIへ不要な個人情報を送信しない
- 定期的に不要データを削除する
- DLPを活用する

---

# 19. 運用

実施内容

- データ分類レビュー
- 保持期間確認
- DLP監査
- データ棚卸し
- 削除証跡管理

継続的にデータ保護を改善する。

---

# 20. 将来拡張

- Microsoft Purview統合
- Data Catalog
- AIデータ分類
- AI個人情報検知
- Data Protection Dashboard
- Confidential Computing
- Data Lineage管理
- AIデータリスク分析
- Continuous Data Protection
- Autonomous Data Governance
