# Playwright 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Playwrightは、VTaBridge OSにおけるWebブラウザ自動化基盤である。

APIを提供していない外部サービスに対して、ブラウザ操作を自動化する。

データ取得、帳票ダウンロード、ログイン、画面入力、テスト自動化などを担当する。

GUI操作は最終手段とし、APIが利用可能な場合はAPI連携を優先する。

---

# 2. 目的

Playwright導入目的

- Web操作自動化
- データ収集
- 帳票ダウンロード
- フォーム入力
- UIテスト
- 回帰テスト
- 定期スクレイピング
- RPA補完

---

# 3. アーキテクチャ

```
Scheduler

↓

Automation API

↓

Playwright Worker

↓

Browser

↓

External Website

↓

Data Parser

↓

Business API

↓

PostgreSQL
```

---

# 4. 対象ブラウザ

対応ブラウザ

- Chromium
- Microsoft Edge
- Google Chrome
- Firefox
- WebKit

標準はChromiumを採用する。

---

# 5. 自動化対象

対象

- ログイン
- フォーム入力
- 一覧取得
- PDF取得
- CSV取得
- スクリーンショット
- ファイルアップロード
- ボタンクリック

---

# 6. 実行フロー

```
Job開始

↓

Playwright起動

↓

ログイン

↓

画面遷移

↓

操作実行

↓

データ取得

↓

Business API

↓

ログ保存

↓

終了
```

---

# 7. 認証

対応方式

- ID / Password
- OAuth2
- SAML
- Azure Entra ID
- Cookie
- Session

認証情報はAzure Key Vaultで管理する。

---

# 8. ファイル操作

対応

- PDFダウンロード
- CSVダウンロード
- Excelダウンロード
- ZIP取得
- ファイルアップロード

取得したファイルはAzure Blob Storageへ保存する。

---

# 9. スクリーンショット

取得タイミング

- エラー時
- テスト終了時
- 手動実行時

PNG形式で保存する。

---

# 10. UIテスト

対象

- ログイン
- CRUD
- 検索
- ページ遷移
- API連携
- レスポンシブ表示

CI/CDで自動実行する。

---

# 11. Retry

失敗時

- 最大3回リトライ
- Exponential Backoff
- スクリーンショット保存
- エラーログ保存

---

# 12. API

```
POST

/api/v1/rpa/playwright/run
```

```
GET

/api/v1/rpa/playwright/{id}
```

```
POST

/api/v1/rpa/playwright/{id}/retry
```

---

# 13. Prisma実装方針

Model

```
PlaywrightJob

PlaywrightExecution

PlaywrightLog

PlaywrightScreenshot
```

Relation

```
AutomationJob

User

Project
```

---

# 14. ログ

保存項目

- JobID
- Browser
- URL
- StartTime
- EndTime
- Status
- Error
- Screenshot

---

# 15. セキュリティ

実装

- Azure Entra ID
- Azure Key Vault
- TLS通信
- RBAC
- Secret Masking
- Audit Log

認証情報はログへ出力しない。

---

# 16. 性能目標

ブラウザ起動

```
2秒以内
```

ログイン

```
5秒以内
```

ジョブ全体

```
30秒以内
```

---

# 17. 運用

実施内容

- ブラウザバージョン管理
- Playwright更新
- 定期テスト
- スクリーンショット管理
- ログ監視

---

# 18. CI/CD

GitHub Actionsで実施

対象

- UIテスト
- 回帰テスト
- スモークテスト
- E2Eテスト

失敗時はTeamsへ通知する。

---

# 19. エラー処理

異常時

- 自動リトライ
- スクリーンショット取得
- エラーログ保存
- 管理者通知
- Queueへ戻す

---

# 20. 将来拡張

- Headless Browser Cluster
- Browser Pool
- CAPTCHA対応
- AI UI認識
- Visual Regression Test
- Mobile Browser対応
- Remote Browser実行
- Selenium連携
- Puppeteer互換
- Browser Automation Dashboard
