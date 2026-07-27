# Data Model

Version: 1.0

Status: Draft

---

## 1. 主要エンティティ

### Organization

- id
- name
- slug
- plan_id
- billing_customer_id
- brand_settings
- retention_days
- created_at

### User

- id
- organization_id
- email
- display_name
- role
- status
- last_login_at

### Property

- id
- organization_id
- name
- property_type
- address_text
- listing_reference
- description
- status
- created_by

### MediaAsset

- id
- organization_id
- property_id
- storage_key
- original_filename
- mime_type
- size_bytes
- width
- height
- checksum
- perceptual_hash
- room_type
- room_confidence
- quality_score
- safety_status
- processing_status
- sort_order

### VideoProject

- id
- organization_id
- property_id
- title
- status
- aspect_ratio
- duration_seconds
- resolution
- style_preset
- user_prompt
- negative_prompt
- camera_motion
- music_setting
- caption_setting
- watermark_setting
- created_by

### StoryboardScene

- id
- video_project_id
- media_asset_id
- scene_order
- room_type
- duration_seconds
- prompt_override
- transition_type
- status

### GenerationJob

- id
- organization_id
- video_project_id
- provider
- provider_job_id
- idempotency_key
- status
- progress
- attempt_count
- estimated_cost
- actual_cost
- reserved_credits
- error_code
- error_message
- started_at
- completed_at

### VideoOutput

- id
- video_project_id
- generation_job_id
- version_number
- storage_key
- thumbnail_key
- duration_seconds
- resolution
- file_size_bytes
- quality_status
- moderation_status
- approved_by
- approved_at

### Subscription

- id
- organization_id
- plan_id
- provider_subscription_id
- status
- current_period_start
- current_period_end

### CreditLedger

- id
- organization_id
- transaction_type
- amount
- balance_after
- generation_job_id
- description
- created_at

### AuditLog

- id
- organization_id
- actor_user_id
- action
- resource_type
- resource_id
- metadata
- ip_address
- user_agent
- created_at

---

## 2. 状態管理

### VideoProjectStatus

- DRAFT
- ANALYZING
- READY
- GENERATING
- REVIEW
- APPROVED
- REJECTED
- ARCHIVED

### GenerationJobStatus

- QUEUED
- VALIDATING
- ANALYZING
- GENERATING_SCENES
- COMPOSING
- VALIDATING_OUTPUT
- COMPLETED
- FAILED
- CANCELLED

---

## 3. データ保持

- 原本画像: 契約プランまたは組織設定に従う
- 処理用中間ファイル: 原則7日以内に削除
- 生成動画: 契約期間中保持、削除設定可能
- 監査ログ: 商用版では最低1年を推奨
- 決済記録: 法令・会計要件に従う

論理削除と物理削除を分離し、削除ジョブの完了を記録する。

---

## 4. インデックス

- organization_id + created_at
- property_id + status
- video_project_id + scene_order
- generation_job status + created_at
- idempotency_key unique
- checksum / perceptual_hash
- billing_customer_id unique

---

## 5. データ分離

すべてのテナントデータ取得でorganization_idを必須条件とする。URLやクライアント入力だけでorganization_idを決定せず、認証済みセッションから解決する。
