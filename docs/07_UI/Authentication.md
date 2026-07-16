# Authentication UI 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Authentication UIは、VTaBridge OSにおける認証・認可・セッション管理・SSOのユーザーインターフェースを定義する。

Azure Entra IDを認証基盤とし、安全かつシンプルなログイン体験を提供する。

---

# 2. 目的

Authentication導入目的

- SSO対応
- MFA対応
- Azure Entra ID連携
- セッション管理
- 権限制御
- セキュリティ向上
- ユーザー管理
- 監査対応

---

# 3. 認証フロー

```
User

↓

Login

↓

Azure Entra ID

↓

MFA

↓

JWT

↓

Business API

↓

Dashboard
```

---

# 4. ログイン画面

表示項目

- ロゴ
- システム名
- Microsoftでサインイン
- 利用規約
- プライバシーポリシー
- バージョン

パスワード入力画面は表示しない。

---

# 5. Azure Entra ID

利用機能

- Single Sign-On
- Multi-Factor Authentication
- Conditional Access
- Identity Protection

Microsoftアカウントで認証する。

---

# 6. セッション管理

保存情報

- Access Token
- Refresh Token
- User Profile
- Role
- Organization

セッション期限は自動更新する。

---

# 7. Role

ロール

- SuperAdmin
- Admin
- Sales
- Recruiter
- Engineer
- Viewer

画面表示はRoleに応じて切り替える。

---

# 8. 権限制御

対象

- Menu
- Button
- API
- AI
- Workflow

権限のない画面は表示しない。

---

# 9. MFA

対応

- Microsoft Authenticator
- SMS
- Email
- FIDO2

MFAはAzure Entra IDで管理する。

---

# 10. ログアウト

処理

```
Logout

↓

Token削除

↓

Azure Logout

↓

Login画面
```

すべてのセッションを終了する。

---

# 11. パスワード管理

Azure Entra IDで管理する。

VTaBridge OSでは

- パスワード変更
- パスワードリセット

は提供しない。

---

# 12. エラー画面

表示

- 認証失敗
- MFA失敗
- セッション切れ
- 権限不足
- システムエラー

ユーザーが次に取るべき操作を表示する。

---

# 13. UIコンポーネント

利用

- Card
- Button
- Alert
- Dialog
- Avatar
- Dropdown Menu

shadcn/uiを利用する。

---

# 14. セッションタイムアウト

標準

```
30分
```

期限切れ前

```
5分前
```

更新ダイアログを表示する。

---

# 15. ローディング

表示

- 認証中
- リダイレクト中
- MFA確認中

Skeletonは利用しない。

---

# 16. セキュリティ

実装

- HTTPS
- Secure Cookie
- CSP
- XSS対策
- CSRF対策
- SameSite Cookie

トークンはLocal Storageへ保存しない。

---

# 17. Prisma実装方針

認証情報はPrismaで管理しない。

Azure Entra IDを利用する。

Business API経由でユーザー情報を取得する。

---

# 18. アクセシビリティ

対応

- キーボード操作
- Focus表示
- ARIA
- WCAG 2.2 AA

---

# 19. パフォーマンス

目標

認証

```
3秒以内
```

画面遷移

```
1秒以内
```

Dashboard表示

```
2秒以内
```

---

# 20. 将来拡張

- パスキー（Passkey）対応
- 生体認証対応
- QRコードログイン
- 多要素認証ポリシー
- テナント切替
- ソーシャルログイン
- デバイス管理
- セッション一覧
- リスクベース認証
- Zero Trust Authentication
