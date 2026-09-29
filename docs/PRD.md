# Product requirements: Event Reliability & Reconciliation Platform

**Status:** Initial product definition; repository audit only.  
**Last updated:** 2026-09-29

## Product vision

Make distributed external events reliable, idempotent, observable, replayable, and reconcilable. The deterministic processing system is authoritative; AI helps people investigate evidence and never independently changes financial state.

## Problem

External providers retry, duplicate, delay, and reorder webhook deliveries. Consumers can fail while applying an event, leaving provider state and internal state inconsistent. Teams need durable event history, safe processing and replay, and evidence-backed reconciliation instead of ad hoc logs and manual repair.

## Target users and assumed personas

These personas are working assumptions, not validated research:

- **Platform/backend engineer:** integrates providers and needs durable ingestion, idempotency, ordering, retries, and replay.
- **Operations/on-call engineer:** needs to find affected aggregates, understand incident timelines, and take auditable corrective action.
- **Finance/reconciliation operator:** compares provider, application, and settlement state and resolves discrepancies.
- **Security/organization administrator:** manages members, roles, provider credentials, and tenant access.

## Use cases and core workflows

1. Configure an organization and an authenticated provider endpoint.
2. Verify a provider signature before accepting an event; persist a normalized, immutable event and its payload hash.
3. Deduplicate durably, validate ordering and state transitions, then process deterministically.
4. Retry transient failures with bounded backoff; retain terminal failures in a dead-letter state.
5. Inspect an event or incident timeline and request an authorized, audited replay.
6. Compare external and internal state; record discrepancies with evidence.
7. Use AI, when introduced, to assemble evidence and propose a hypothesis and action for human review.

## MVP scope

The roadmap prioritizes authentication, organizations, database design, secure webhook ingestion, signature verification, durable idempotency, persistence, deterministic event processing, a basic state machine, retry/DLQ/replay, audit history, and an operational dashboard. Implement only after repository/product setup decisions are approved in a follow-up task. Initial provider support must be an adapter boundary, not a provider-specific product model.

## Out of scope for the initial milestone

- Autonomous financial remediation or money movement.
- Broad provider catalog, settlement-file ingestion, or production-scale claims.
- LangGraph/RAG investigation before deterministic evidence and authorization exist.
- C++ processing service absent a measured performance need.
- Redis as a correctness boundary or microservices without a demonstrated need.
- Compliance or legal-compliance claims.

## Functional requirements

- Tenant-aware signup/login/session and organization membership with server-side authorization.
- Provider signature verification, bounded payload validation, and safe webhook response semantics.
- Canonical event storage with provider identity, aggregate/correlation/causation metadata, timestamps, payload hash, schema version, status, attempts, and errors.
- Database-enforced uniqueness and transactional handling of concurrent duplicate delivery.
- Explicit pending-order state when causal predecessors are unknown; timestamps alone never establish causality.
- Server-side deterministic state-transition validation.
- Bounded retries, dead-letter visibility, authorized replay, and auditable actions.
- Search, event/incident views, empty/loading/error states, and responsive operational dashboard as stages are implemented.
- Reconciliation records compare provider state with internal state and preserve discrepancy evidence.

## Non-functional and security requirements

- PostgreSQL is the durable source of truth for events and idempotency.
- Enforce organization isolation in server authorization and database policy (RLS where supported); never trust tenant, user, role, or permission claims supplied by the browser.
- Keep provider secrets and service-role credentials server-side; validate all inputs; rate-limit appropriately; use restrictive CORS and secure headers/cookies in production.
- Preserve auditability and avoid logging sensitive payloads or secrets.
- Support keyboard access, semantic markup, visible focus, reduced motion, readable contrast, and intentional mobile layouts.
- Do not report simulated metrics as production measurements.

## Privacy and legal

Minimize collected data, keep sensitive event contents out of analytics, and define retention/access controls before production. If legal pages are added, label them as templates for counsel review; do not invent company details or compliance status. Cookie/analytics behavior must be reviewed for the launch jurisdictions.

## Success measures

Define baselines before setting targets. Candidate measures: accepted webhook rate, duplicate suppression correctness, processing/retry outcomes, age and count of pending-order/DLQ events, reconciliation match/discrepancy counts, time to investigate, and replay outcomes. Any demo data must be labeled simulated. No numeric targets or market statistics are asserted here.

## Acceptance criteria

- Duplicate concurrent deliveries produce at most one durable state transition.
- Invalid signatures are rejected before event processing.
- Invalid transitions and causally blocked events are explicit and inspectable.
- Retry exhaustion is visible in a durable dead-letter state; authorized replay is auditable.
- Tenant authorization is enforced server-side and verified for cross-organization access.
- No secret is present in browser bundles, committed config, or example environment values.
- Errors are actionable without exposing stack traces; operational UI supports mobile and keyboard use.
- Documentation, migrations, and tests accompany implemented features.

## Future roadmap

1. Ordering, provider adapters, reconciliation, incident management, timeline, search, and observability.
2. Evidence retrieval and human-approved AI investigation (LangGraph/RAG only where justified).
3. Production hardening, load/security/accessibility/performance review.
4. Consider a C++ component only after a benchmark establishes a meaningful advantage.
