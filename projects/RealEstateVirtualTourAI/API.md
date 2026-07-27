# API Design

Version: 1.0

Status: Draft

---

## 1. 方針

- REST API
- JSON
- `/api/v1`
- OpenAPIを正本とする
- 認証必須
- 組織スコープ必須
- 書き込みAPIは監査ログ対象
- 生成開始APIはIdempotency-Key必須

---

## 2. 主要エンドポイント

### Authentication

- `POST /auth/login`
- `POST /auth/logout`
- `POST /auth/invitations`
- `POST /auth/invitations/{token}/accept`

### Properties

- `GET /properties`
- `POST /properties`
- `GET /properties/{propertyId}`
- `PATCH /properties/{propertyId}`
- `DELETE /properties/{propertyId}`

### Assets

- `POST /properties/{propertyId}/assets/upload-url`
- `POST /properties/{propertyId}/assets/complete`
- `GET /properties/{propertyId}/assets`
- `PATCH /assets/{assetId}`
- `DELETE /assets/{assetId}`
- `POST /assets/{assetId}/reanalyze`

### Video Projects

- `POST /video-projects`
- `GET /video-projects`
- `GET /video-projects/{projectId}`
- `PATCH /video-projects/{projectId}`
- `POST /video-projects/{projectId}/storyboard/generate`
- `PATCH /video-projects/{projectId}/storyboard`

### Generation

- `POST /video-projects/{projectId}/estimate`
- `POST /video-projects/{projectId}/generations`
- `GET /generations/{jobId}`
- `POST /generations/{jobId}/cancel`
- `POST /generations/{jobId}/retry`

### Outputs

- `GET /video-projects/{projectId}/outputs`
- `GET /outputs/{outputId}/download-url`
- `POST /outputs/{outputId}/approve`
- `POST /outputs/{outputId}/reject`
- `DELETE /outputs/{outputId}`

### Billing

- `GET /billing/plan`
- `GET /billing/usage`
- `GET /billing/credits`
- `POST /billing/checkout-session`
- `POST /billing/webhooks/stripe`

---

## 3. 生成開始例

```json
{
  "durationSeconds": 30,
  "aspectRatio": "16:9",
  "resolution": "1080p",
  "stylePreset": "natural",
  "cameraMotion": "slow-walkthrough",
  "prompt": "明るく清潔感のある自然な内覧動画",
  "negativePrompt": "新しい家具や設備を追加しない",
  "includeMusic": true,
  "includeCaptions": true
}
```

レスポンス:

```json
{
  "jobId": "job_123",
  "status": "QUEUED",
  "reservedCredits": 12,
  "estimatedCompletionSeconds": 420
}
```

---

## 4. エラー形式

```json
{
  "error": {
    "code": "INSUFFICIENT_CREDITS",
    "message": "動画生成に必要なクレジットが不足しています",
    "requestId": "req_123",
    "details": {}
  }
}
```

---

## 5. Webhook / Event

- generation.started
- generation.progressed
- generation.completed
- generation.failed
- output.approved
- credit.consumed
- subscription.updated

Webhookには署名検証と再送制御を実装する。
