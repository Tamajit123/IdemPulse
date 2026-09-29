# Implementation roadmap

Status reflects the repository audit on 2026-09-29. This workspace was empty; no implementation tasks have started.

## Phase 0 — Repository and product setup

- [x] Audit current workspace contents and identify absent app, Git, database, auth, test, and deployment configuration.
- [x] Create initial PRD, architecture, engineering rules, design direction, roadmap, and memory.
- [ ] Confirm intended repository/branch and whether this empty workspace is the correct project root.
- [ ] Confirm deployment/database/auth environment and initial provider(s); document assumptions.
- [ ] Initialize project/framework and secret-safe environment examples; establish Git and deployment baseline.

## Phase 1 — Secure deterministic MVP (P0)

- [ ] Authentication, sessions, organization/member/role model, and server-side authorization.
- [ ] PostgreSQL schema, migrations, tenant isolation/RLS, indexes, unique/check constraints, audit records.
- [ ] Canonical event model and provider adapter boundary.
- [ ] Webhook ingress: size/schema validation, provider signature verification, safe HTTP semantics.
- [ ] Transactional durable idempotency and immutable event persistence.
- [ ] Deterministic processing and basic server-side state machine.
- [ ] Bounded retry/backoff, durable DLQ, authorized audited replay.
- [ ] Operational dashboard with event explorer, loading/error/empty states, and responsive/accessibility baseline.
- [ ] Tests for signature validation, concurrent duplicates, transitions, retry/DLQ/replay, and cross-tenant denial.

## Phase 2 — Operations and reconciliation (P1)

- [ ] Ordering/dependency validation and explicit pending-order handling.
- [ ] Provider adapters and provider-specific retry/signature semantics.
- [ ] Reconciliation runs and discrepancy categories with evidence.
- [ ] Incident lifecycle, timeline, search, and observability.

## Phase 3 — Evidence-led investigation (P2)

- [ ] Authorized evidence retrieval and provider documentation ingestion.
- [ ] AI investigation workflow (LangGraph only if the multi-step workflow warrants it).
- [ ] Cited evidence, confidence/risk, policy review, and human approval UI.
- [ ] Verify AI cannot mutate financial state autonomously.

## Phase 4 — Production hardening (P3)

- [ ] Threat model, security review, rate limiting, headers/CORS, retention/privacy decisions.
- [ ] Load/reliability testing and measured performance improvements.
- [ ] Accessibility and responsive verification; Lighthouse where available.
- [ ] Decide on queues/cache/deployment scaling from measured requirements.
- [ ] Benchmark before considering a C++ engine; defer if no material benefit.
