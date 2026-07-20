# CLAUDE.md

# VTaBridge OS — Claude Code Operating Instructions

Version: 2.0
Status: Active

This file is the primary execution guide for Claude Code in this repository.
Read it completely before changing code.

---

## 1. Mission

Build VTaBridge OS as a secure, maintainable, AI-native enterprise business platform.

The repository currently contains the product vision, architecture, governance, platform, business, data, IoT, manufacturing, robotics, and smart-factory design documents under `docs/01_*` through `docs/30_*`.

These documents describe the target enterprise architecture. They are not an instruction to implement every documented capability at once.

The implementation must proceed incrementally through small, testable vertical slices.

---

## 2. Source of Truth

Use the following precedence when requirements conflict:

1. The current user request
2. This `CLAUDE.md`
3. Approved ADRs in `docs/adr/`
4. Relevant files under `docs/`
5. Existing tests and public interfaces
6. Existing implementation

Do not silently invent business requirements.

When a required decision is not defined:

- choose the smallest reversible option;
- record the assumption in the implementation summary;
- create an ADR when the decision affects architecture, security, data, APIs, or operations;
- leave a clear TODO only when implementation cannot safely continue.

---

## 3. Working Method

Before editing:

1. Inspect the repository structure.
2. Read the relevant design documents.
3. Identify existing conventions and dependencies.
4. State the intended change as a short implementation plan.
5. Implement only the requested scope.

After editing:

1. Run formatting.
2. Run static analysis and type checking.
3. Run relevant unit and integration tests.
4. Run the build when practical.
5. Review the diff for accidental or unrelated changes.
6. Summarize changed files, decisions, tests, and remaining risks.

Never claim a command passed unless it was actually executed successfully.

---

## 4. Delivery Strategy

Do not attempt to implement all 30 chapters as one program increment.

Use this order:

### Phase 0 — Repository Foundation

- workspace and package structure;
- local development environment;
- configuration validation;
- logging and error handling;
- linting, formatting, type checking, tests, and CI;
- architecture decision records;
- secure secret handling.

### Phase 1 — First Vertical Slice

Implement one complete business flow from UI to persistence:

`Customer -> Opportunity -> Estimate -> Approval -> Audit Log`

The slice must include:

- domain model;
- application use cases;
- persistence adapter;
- API contract;
- authorization checks;
- user interface;
- validation and error handling;
- audit trail;
- automated tests;
- minimal operational documentation.

### Phase 2 — Core Business Platform

Expand one bounded context at a time:

- Sales and CRM;
- estimates and contracts;
- delivery and project tracking;
- invoicing and payments;
- document and workflow management.

### Phase 3 — AI Assistance

Add AI only after the underlying deterministic workflow is reliable.

AI may propose, summarize, classify, search, or recommend. High-impact actions require explicit human approval.

### Phase 4 — Enterprise Integrations

Add Microsoft 365, Azure, Fabric, Power Platform, Dynamics 365, IoT, manufacturing, robotics, and smart-factory integrations only through explicit milestones.

---

## 5. Architecture Rules

Use a modular monolith first. Do not introduce microservices unless measured scaling, isolation, deployment, security, or ownership requirements justify them.

Organize the system by bounded context and keep dependencies directed inward:

```text
interface / delivery
        ↓
application
        ↓
domain
        ↑
infrastructure adapters
```

Rules:

- Domain code must not depend on frameworks, databases, HTTP, UI, or external SDKs.
- Application services orchestrate use cases and transactions.
- Infrastructure implements ports defined by inner layers.
- UI and API layers must not contain business rules.
- Cross-context access must use explicit contracts.
- Prefer synchronous calls initially; add messaging only for genuine asynchronous behavior.
- Do not introduce CQRS or event sourcing by default.
- Use domain events only when another part of the system has a real reaction to a completed domain action.

---

## 6. Baseline Technology

Use the existing repository configuration when present. For new foundation work, use this baseline unless an ADR approves a change:

- Language: TypeScript with strict mode
- Runtime: current active Node.js LTS
- Package manager: pnpm
- Workspace: pnpm workspaces
- Web: Next.js with React Server Components where appropriate
- UI: Tailwind CSS and accessible reusable components
- API: REST with OpenAPI
- Database: PostgreSQL
- ORM: Prisma
- Validation: schema-based runtime validation
- Unit and integration tests: Vitest
- End-to-end tests: Playwright
- Containers: Docker for reproducible local dependencies
- CI: GitHub Actions

Do not add a dependency when the platform or an existing dependency already solves the problem adequately.

Do not ban raw SQL categorically. Use it only when Prisma cannot express a correct or performant query, isolate it in infrastructure, parameterize it, test it, and document the reason.

---

## 7. Repository Target Structure

Prefer the following structure for implementation:

```text
apps/
  web/
  api/

packages/
  domain/
  application/
  database/
  contracts/
  ui/
  config/
  observability/
  testing/

infra/
  docker/
  terraform/

scripts/

tests/
  integration/
  e2e/

docs/
  adr/
```

Do not create empty placeholder packages. Add a package only when the current milestone uses it.

---

## 8. Coding Standards

- Enable strict TypeScript settings.
- Do not use `any`; use `unknown` with narrowing when the input is untrusted.
- Prefer explicit domain types over primitive strings and numbers for important concepts.
- Keep functions focused and readable.
- Prefer composition over inheritance.
- Avoid premature abstraction.
- Avoid duplicated business rules.
- Use dependency injection at architectural boundaries, not throughout every object.
- Comments should explain decisions and constraints, not restate code.
- Public APIs, exported types, and non-obvious domain rules require documentation.

Naming:

- variables and functions: `camelCase`
- types, classes, React components: `PascalCase`
- constants: `UPPER_SNAKE_CASE` only for true constants
- files: follow the framework convention consistently
- database tables and columns: `snake_case`
- REST paths: plural nouns in `kebab-case`

---

## 9. API Rules

- Define contracts before implementation.
- Use resource-oriented REST endpoints.
- Use correct HTTP methods and status codes.
- Validate all external input at the boundary.
- Return a consistent error envelope.
- Use idempotency keys for retryable state-changing operations where duplication is harmful.
- Paginate collection endpoints.
- Do not expose database entities directly.
- Generate and maintain OpenAPI documentation.
- Version public APIs only when a breaking change is necessary.

Example error shape:

```json
{
  "error": {
    "code": "ESTIMATE_NOT_FOUND",
    "message": "The estimate was not found.",
    "requestId": "...",
    "details": []
  }
}
```

---

## 10. Data and Transaction Rules

- Migrations are mandatory for schema changes.
- Never edit an applied migration.
- Use database constraints for invariants that must always hold.
- Define transaction boundaries in the application layer.
- Store timestamps in UTC.
- Use stable generated identifiers.
- Add optimistic concurrency control where concurrent edits can cause data loss.
- Do not perform destructive schema or data changes without an explicit migration and rollback plan.
- Seed data must be deterministic and safe for non-production use.

---

## 11. Security Rules

Security is part of the feature definition, not a later task.

Every implementation must consider:

- authentication;
- authorization and least privilege;
- tenant or organizational data isolation when applicable;
- input validation;
- output encoding;
- CSRF protection where relevant;
- XSS prevention;
- SQL injection prevention;
- rate limiting and abuse protection;
- secret management;
- secure headers and cookies;
- audit logging;
- dependency and supply-chain risk;
- personal and confidential data handling.

Never commit secrets, tokens, credentials, private keys, production data, or sensitive logs.

High-impact operations must require explicit authorization and produce an immutable audit record.

---

## 12. AI Rules

AI capabilities must be implemented as replaceable adapters behind stable application interfaces.

Required pattern:

```text
User or System Request
        ↓
Deterministic validation and authorization
        ↓
AI orchestration
        ↓
Structured result with evidence and confidence
        ↓
Human approval when the action is high impact
        ↓
Deterministic execution
        ↓
Audit log
```

Rules:

- Never allow model output to bypass authorization or validation.
- Treat model output as untrusted input.
- Require structured outputs for machine-consumed responses.
- Record model, prompt version, tool calls, latency, and outcome without logging sensitive content unnecessarily.
- Ground business answers in authorized enterprise data.
- Enforce permission trimming before retrieval and before presenting results.
- Provide citations or source references for RAG responses.
- Add evaluation datasets and regression tests before promoting AI behavior.
- Do not automatically send email, approve estimates, sign contracts, issue invoices, make payments, or control industrial equipment without an explicitly approved policy.
- Make providers replaceable; do not spread vendor-specific SDK calls through domain or application code.

---

## 13. Observability and Audit

Use structured logs with a request or correlation ID.

Capture:

- errors and warnings;
- security-relevant events;
- business events;
- external dependency failures;
- latency and throughput;
- AI invocation metadata;
- audit events for sensitive changes.

Do not log secrets, access tokens, full prompts containing confidential data, or unnecessary personal data.

Audit records must state who performed the action, what changed, when it occurred, and the originating request.

---

## 14. Testing Requirements

Use the test pyramid:

- unit tests for domain rules and pure logic;
- integration tests for database, repositories, APIs, and external adapters;
- end-to-end tests for critical user journeys;
- contract tests for external integrations;
- security tests for authorization boundaries;
- AI evaluation tests for prompt and retrieval behavior.

Every bug fix must include a regression test when practical.

Tests must be deterministic. Do not depend on real production services in normal CI.

A feature is not complete when tests, migrations, API documentation, security checks, or operational behavior are missing.

---

## 15. Definition of Done

A change is complete only when:

- the requested behavior works;
- acceptance criteria are satisfied;
- relevant design documents were followed;
- types and validation are complete;
- authorization is enforced;
- errors are handled consistently;
- audit and observability requirements are addressed;
- migrations are included when required;
- tests pass;
- formatting, linting, type checking, and build pass;
- documentation and OpenAPI are updated;
- no unrelated changes are included;
- remaining risks and assumptions are reported.

---

## 16. Git and Change Discipline

- Keep changes small and reviewable.
- One commit should represent one coherent change.
- Use clear imperative commit messages.
- Do not rewrite unrelated files.
- Do not reformat the entire repository during a feature change.
- Never force-push or delete branches without explicit instruction.
- Never disable tests, lint rules, type checks, security checks, or CI merely to make a build pass.

For substantial work, use a feature branch and pull request.

---

## 17. Architecture Decision Records

Create an ADR under `docs/adr/` for decisions involving:

- framework or language changes;
- service boundaries;
- data ownership;
- authentication or authorization architecture;
- messaging and event design;
- public API compatibility;
- AI provider or orchestration architecture;
- infrastructure topology;
- major security or compliance trade-offs.

Use the format:

```text
Title
Status
Context
Decision
Consequences
Alternatives considered
```

---

## 18. Prohibited Behavior

Do not:

- implement all design documents at once;
- create speculative microservices;
- create empty scaffolding for future chapters;
- duplicate business logic across UI, API, and database layers;
- hide failures with broad exception handling;
- use `any` to silence type errors;
- weaken validation or authorization for convenience;
- expose secrets or confidential data;
- silently change documented behavior;
- claim tests passed without running them;
- replace working code without a clear benefit;
- make irreversible production changes without explicit approval.

---

## 19. First Implementation Assignment

When asked to begin implementation and no narrower task is provided:

1. Inspect the complete repository.
2. Identify existing executable code and configuration.
3. Create a short gap analysis between the current repository and Phase 0.
4. Propose the smallest foundation milestone.
5. Implement that milestone only after the scope is clear.
6. Do not begin with all business modules.

The preferred first milestone is:

- pnpm workspace;
- `apps/web` and `apps/api` only when they are immediately used;
- shared TypeScript configuration;
- environment validation;
- PostgreSQL local development setup;
- Prisma initialization;
- health endpoint;
- structured logging;
- Vitest setup;
- lint, format, type-check, test, and build scripts;
- GitHub Actions CI;
- one ADR describing the modular-monolith baseline.

The preferred first product slice after the foundation is:

`Customer -> Opportunity -> Estimate -> Approval -> Audit Log`

---

## 20. Final Response Format

At the end of each Claude Code task, report:

1. What changed
2. Files changed
3. Commands and tests executed
4. Architectural or security decisions
5. Assumptions
6. Remaining risks or follow-up work

Be concise, factual, and explicit about anything not completed.
