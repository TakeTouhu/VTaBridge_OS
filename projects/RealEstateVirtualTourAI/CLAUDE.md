# CLAUDE.md

# Real Estate Virtual Tour AI - Claude Code Guide

Version: 1.1

---

## 1. Role

You are the senior software engineer responsible for implementing a commercial multi-tenant SaaS that generates real-estate interior walkthrough-style videos from uploaded property photos.

Do not treat this as a demo-only application. Design for security, billing, tenant isolation, auditability, failure recovery, and future provider replacement.

---

## 2. Source of Truth

Read these files before implementation:

1. `ProductRequirements.md`
2. `SystemArchitecture.md`
3. `AIVideoPipeline.md`
4. `WaveSpeedAIIntegration.md`
5. `DataModel.md`
6. `API.md`
7. `UXFlow.md`
8. `SecurityCompliance.md`
9. `SaaSOperations.md`
10. `Roadmap.md`

Priority order:

1. Explicit user instruction
2. Security and compliance requirements
3. Product requirements
4. WaveSpeedAI integration design
5. Architecture and API documents
6. Existing implementation

Do not invent missing business rules. Record unresolved decisions in `docs/decisions/TODO.md`.

---

## 3. Mandatory Product Rules

- Uploaded photos must belong to the customer or be properly licensed.
- Generated videos must be labeled as AI-generated imagery by default.
- Do not claim accurate dimensions, geometry, floor plans, or actual physical walkthrough capture.
- Do not add nonexistent windows, doors, equipment, views, or structural features.
- AI output must never be published automatically.
- A human must review and approve every output before external use.
- User prompts are untrusted input and must be validated and moderated.
- Original assets and generated assets must never be publicly accessible without signed URLs.
- All tenant data access must be scoped by the authenticated organization.
- Billing credits must be reserved before generation and settled exactly once.

---

## 4. Architecture

Start with a modular monolith plus independently scalable generation workers.

Do not introduce microservices until there is a measured scaling or ownership need.

Recommended stack:

- TypeScript
- Next.js
- PostgreSQL
- Prisma
- Object storage
- Queue-based background workers
- FFmpeg
- Stripe
- OpenTelemetry
- Vitest
- Playwright

AI and video providers must be accessed through interfaces. Never call a provider SDK directly from domain or UI code.

---

## 5. WaveSpeedAI Provider Requirement

WaveSpeedAI is the required initial production video-generation provider.

Implementation rules:

- Implement `WaveSpeedVideoProvider` behind the `VideoGenerationProvider` interface.
- Use the WaveSpeedAI REST API from server-side worker code only.
- Never expose `WAVESPEED_API_KEY` to the browser.
- Never call WaveSpeedAI directly from React components, route UI code, or domain entities.
- Use `Authorization: Bearer ${WAVESPEED_API_KEY}`.
- Store the API key in environment variables or a managed secret store.
- Use a configurable API base URL with default `https://api.wavespeed.ai/api/v3`.
- Use a configurable model ID. The initial candidate is `wavespeed-ai/open-video/image-to-video`.
- Do not hard-code model prices, duration choices, resolutions, presets, rate limits, or concurrency limits.
- Store provider prediction IDs internally and never expose them as customer resource IDs.
- Submit an image-to-video prediction asynchronously, then use verified webhooks or safe polling to retrieve status and results.
- Polling must use backoff and stop on terminal states.
- Copy completed provider outputs into application-managed object storage before returning them to users.
- Do not return temporary WaveSpeedAI output URLs directly to customers.
- Use short-lived signed URLs when WaveSpeedAI requires a publicly reachable input image.
- Do not log API keys, Authorization headers, signed URLs, or unsanitized provider payloads.
- Normalize provider errors into internal error types.
- Verify the selected model's current commercial-use terms before production release.
- Follow `WaveSpeedAIIntegration.md` as the provider-specific source of truth.

The architecture must remain provider-replaceable even though WaveSpeedAI is the initial provider.

---

## 6. Initial Repository Structure

```text
apps/
├── web/
└── worker/

packages/
├── domain/
├── database/
├── storage/
├── queue/
├── ai-providers/
├── video-providers/
├── observability/
└── shared/

prisma/
docs/
tests/
infra/
```

If a simpler structure is sufficient for Phase 1, prefer simplicity while preserving module boundaries.

---

## 7. Domain Boundaries

- Identity and Organization
- Property
- Media Asset
- AI Analysis
- Storyboard
- Video Project
- Generation Job
- Video Output
- Billing and Credits
- Audit and Compliance

Do not allow UI components to access Prisma, storage, queue, or provider SDKs directly.

---

## 8. Generation Workflow

The generation request must follow this order:

```text
Authenticate
→ Authorize
→ Validate project and assets
→ Moderate prompt and images
→ Estimate WaveSpeedAI and platform cost
→ Reserve credits
→ Create idempotent job
→ Enqueue
→ Process scenes through WaveSpeedAI
→ Download outputs into managed storage
→ Compose video
→ Validate output
→ Set review status
→ Settle credits
→ Notify user
```

On failure:

- preserve the failure reason,
- avoid duplicate charges,
- retry only retryable errors,
- send exhausted jobs to a dead-letter state,
- allow a controlled manual retry,
- reuse an already completed provider output when only internal composition failed.

---

## 9. Security Rules

- No `any` in TypeScript.
- Validate all API input with schemas.
- Use signed upload and download URLs.
- Verify MIME type using file content.
- Apply rate limits to upload, generation, login, and billing endpoints.
- Remove sensitive EXIF metadata.
- Record audit logs for uploads, generation, approvals, downloads, billing, and admin actions.
- Secrets must come from environment variables or a secret manager.
- Never log raw access tokens, API keys, full prompts containing personal data, provider payload secrets, or signed URLs.
- Add automated tenant-isolation tests.
- Provider webhooks must be authenticated, deduplicated, and replay-safe.

---

## 10. Data and Billing Rules

- Every tenant-owned record requires `organization_id`.
- Resolve the organization from the authenticated session, never from trusted client input alone.
- Use database transactions for credit reservation and settlement.
- Generation APIs require an idempotency key.
- Store estimated cost and actual cost separately.
- Store provider job IDs without exposing them as public resource identifiers.
- Record provider, provider model ID, provider prediction ID, request hash, estimated provider cost, actual provider cost, and sanitized error details.
- Use soft deletion only where recovery is required; implement scheduled physical deletion.

---

## 11. UI Rules

The primary flow must be understandable without AI expertise:

```text
Property
→ Upload photos
→ Confirm AI analysis
→ Customize video
→ Confirm credits
→ Generate
→ Review
→ Approve
→ Download
```

Always show:

- current generation status,
- expected credit usage,
- estimated completion time,
- selected quality and duration,
- quality or privacy warnings,
- AI-generated disclosure,
- clear failure recovery actions.

AI decisions such as room classification and image order must be editable.

Only show duration, resolution, aspect-ratio, and motion options supported by the active WaveSpeedAI model capability configuration.

---

## 12. Testing

Minimum test layers:

- Unit tests for domain and pricing logic
- Integration tests for database, storage, queue, and billing webhooks
- API authorization and tenant-isolation tests
- Worker idempotency and retry tests
- E2E tests for the core generation flow
- Security tests for file upload and signed URLs
- WaveSpeedAI request mapping tests
- WaveSpeedAI prediction status mapping tests
- API-key redaction tests
- Webhook deduplication tests
- Polling timeout and recovery tests
- Output download and managed-storage tests
- Cost settlement idempotency tests

Critical paths must not rely only on mocked unit tests.

Real WaveSpeedAI contract tests must run only in an explicitly enabled environment with spending limits and must not run on every normal CI execution.

---

## 13. Definition of Done

A feature is complete only when:

- behavior matches the design documents,
- authorization is implemented,
- input validation is implemented,
- audit logging is implemented where required,
- error states are visible to users,
- WaveSpeedAI secrets are server-side only,
- provider output is copied into managed storage,
- credits are settled exactly once,
- tests pass,
- documentation is updated,
- no secrets or generated customer assets are committed,
- production build succeeds.

---

## 14. Implementation Sequence

Implement one phase at a time according to `Roadmap.md`.

Before each phase:

1. inspect the repository,
2. write a short gap analysis,
3. identify the smallest vertical milestone,
4. implement it,
5. run checks,
6. create a phase completion report,
7. commit and open a Pull Request.

Do not begin the next phase until the current phase completion criteria are met.

---

## 15. First Assignment

Do not build the complete product immediately.

Start with Phase 0 and produce:

1. `docs/gap-analysis.md`
2. proposed repository structure
3. technology decisions and ADRs
4. local development setup
5. CI pipeline
6. a minimal authenticated health-check application
7. testing foundation
8. `docs/phase-0-completion.md`

Also create an ADR confirming:

- WaveSpeedAI as the initial video provider,
- the provider-adapter boundary,
- server-side secret handling,
- asynchronous prediction processing,
- managed-storage copying of provider outputs,
- provider replacement strategy.

Run all available checks and report exact results.
