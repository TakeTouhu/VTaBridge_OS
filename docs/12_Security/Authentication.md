# Authentication 設計

Version: 1.0

Status: Draft

Priority: ★★★★★

---

# 1. 概要

Authenticationは、VTaBridge OSにアクセスする利用者・システム・サービスの本人確認を行うための認証基盤を定義する。

Microsoft Entra IDを認証基盤として採用し、OAuth 2.0・OpenID Connect・MFA・Passkey・FIDO2を組み合わせ、安全かつ利便性の高い認証を実現する。

---

# 2. 目的

Authentication導入目的

- 不正アクセス防止
- シングルサインオン実現
- MFAによる認証強化
- パスワードレス認証
- Zero Trust実現
- 利便性向上

---

# 3. 認証対象

対象

- 管理者
- 営業担当
- 採用担当
- エンジニア
- AI Agent
- Backend API
- Workflow
- GitHub Actions

---

# 4. 認証アーキテクチャ

```
User

↓

Microsoft Entra ID

↓

OAuth2 / OIDC

↓

JWT Access Token

↓

Backend API

↓

Database
```

認証はMicrosoft Entra IDへ集約する。

---

# 5. 認証方式

採用

- OAuth 2.0
- OpenID Connect
- JWT
- MFA
- Passkey
- FIDO2
- Passwordless Authentication

用途に応じて適切な認証方式を利用する。

---

# 6. Single Sign-On

対象

- Web Application
- AI Chat
- Workflow
- Admin Portal

Microsoft Entra IDによるSSOを提供する。

---

# 7. Multi-Factor Authentication

適用対象

- 全管理者
- 一般利用者
- 外部アクセス
- 管理API

MFAを必須とする。

---

# 8. Passwordless

採用方式

- Passkey
- Microsoft Authenticator
- Windows Hello
- FIDO2 Security Key

パスワードレス認証を推奨する。

---

# 9. JWT

利用

- Access Token
- ID Token
- Refresh Token

署名付きJWTを利用する。

---

# 10. Token Lifetime

Access Token

```
60分
```

Refresh Token

```
90日
```

Azure Entra IDのポリシーに従って管理する。

---

# 11. Session Management

管理内容

- Session Timeout
- Logout
- Token Revocation
- Concurrent Session

セッションを安全に管理する。

---

# 12. Conditional Access

条件

- MFA必須
- 管理者強制
- リスクベース認証
- デバイス準拠
- 地域制限

Microsoft Entra IDでポリシーを適用する。

---

# 13. Service Authentication

対象

- Managed Identity
- Service Principal
- GitHub OIDC

シークレットレス認証を優先する。

---

# 14. API Authentication

実装

- OAuth2
- Bearer Token
- JWT Validation
- Scope Validation

APIごとに認証・認可を実施する。

---

# 15. AI Authentication

対象

- Azure OpenAI
- Azure AI Search
- AI Agent

Managed IdentityまたはMicrosoft Entra IDで認証する。

---

# 16. ログ

記録項目

- Login
- Logout
- MFA
- Token Refresh
- Authentication Failure
- Conditional Access

監査ログとして保存する。

---

# 17. セキュリティ

実装

- HTTPS必須
- Secure Cookie
- HttpOnly
- SameSite
- Token Validation
- Replay Attack対策

認証情報を安全に保護する。

---

# 18. KPI

管理項目

- MFA利用率
- 認証成功率
- 認証失敗率
- Passwordless利用率
- Token失効件数

継続的に監視する。

---

# 19. ベストプラクティス

- パスワードレス認証を推奨する
- MFAを必須とする
- シークレットを保持しない
- Managed Identityを優先する
- トークンは短寿命とする

---

# 20. 将来拡張

- Continuous Access Evaluation
- Risk-Based Authentication
- Face Authentication
- AI異常ログイン検知
- Adaptive MFA
- Decentralized Identity
- Verifiable Credentials
- Microsoft Entra Verified ID
- AI認証分析
- Autonomous Identity Protection
