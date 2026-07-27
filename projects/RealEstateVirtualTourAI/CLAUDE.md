# CLAUDE.md

# Real Estate Virtual Tour AI - Claude Code Guide

Version: 1.0

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
4. `DataModel.md`
5. `API.md`
6. `UXFlow.md`
7. `SecurityCompliance.md`
8. `SaaSOperations.md`
9. `Roadmap.md`

Priority order:

1. Explicit user instruction
2. Security and compliance requirements
3. Product requirements
4. Architecture and API documents
5. Existing implementation

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

## 5. Initial Repository Structure

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

## 6. Domain Boundaries

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

## 7. Generation Workflow

The generation request must follow this order:

```text
Authenticate
→ Authorize
→ Validate project and assets
→ Moderate prompt and images
→ Estimate cost
→ Reserve credits
→ Create idempotent job
→ Enqueue
→ Process scenes
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
- allow a controlled manual retry.

---

## 8. Security Rules

- No `any` in TypeScript.
- Validate all API input with schemas.
- Use signed upload and download URLs.
- Verify MIME type using file content.
- Apply rate limits to upload, generation, login, and billing endpoints.
- Remove sensitive EXIF metadata.
- Record audit logs for uploads, generation, approvals, downloads, billing, and admin actions.
- Secrets must come from environment variables or a secret manager.
- Never log raw access tokens, API keys, full prompts containing personal data, or signed URLs.
- Add automated tenant-isolation tests.

---

## 9. Data and Billing Rules

- Every tenant-owned record requires `organization_id`.
- Resolve the organization from the authenticated session, never from trusted client input alone.
- Use database transactions for credit reservation and settlement.
- Generation APIs require an idempotency key.
- Store estimated cost and actual cost separately.
- Store provider job IDs without exposing them as public resource identifiers.
- Use soft deletion only where recovery is required; implement scheduled physical deletion.

---

## 10. UI Rules

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
- quality or privacy warnings,
- AI-generated disclosure,
- clear failure recovery actions.

AI decisions such as room classification and image order must be editable.

---

## 11. Testing

Minimum test layers:

- Unit tests for domain and pricing logic
- Integration tests for database, storage, queue, and billing webhooks
- API authorization and tenant-isolation tests
- Worker idempotency and retry tests
- E2E tests for the core generation flow
- Security tests for file upload and signed URLs

Critical paths must not rely only on mocked unit tests.

---

## 12. Definition of Done

A feature is complete only when:

- behavior matches the design documents,
- authorization is implemented,
- input validation is implemented,
- audit logging is implemented where required,
- error states are visible to users,
- tests pass,
- documentation is updated,
- no secrets or generated customer assets are committed,
- production build succeeds.

---

## 13. Implementation Sequence

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

## 14. First Assignment

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

Run all available checks and report exact results.
