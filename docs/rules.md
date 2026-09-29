# Engineering and security rules

These rules govern implementation and supersede convenience-driven shortcuts.

1. Correctness comes before cleverness; deterministic processing is the source of truth.
2. Security comes before convenience. Never trust the frontend for identity, tenant, role, permission, or transition validity.
3. Derive authorization from a verified server-side session and enforce it on every tenant-owned read and mutation; use database isolation policies as defense in depth.
4. Never hardcode, commit, log, or expose secrets. Keep service-role, provider-signing, database, JWT, and AI credentials server-side. `.env.example` contains names only.
5. Persist idempotency in PostgreSQL with unique constraints and transactions. Redis is never the sole correctness boundary.
6. Authenticate webhooks before processing; validate size, schema, timestamp/replay constraints, and provider-specific signatures.
7. Never silently discard an event or silently reorder a causally ambiguous sequence. Use explicit states such as `PENDING_ORDER` and DLQ.
8. Never use timestamps as the sole causal ordering mechanism. Validate aggregate transitions on the server.
9. Bound retries and make retry, replay, reconciliation, and administrative actions auditable.
10. AI is investigative decision support, never authority over financial state. Require human approval for high-risk actions.
11. Validate inputs server-side, use parameterized database access, safely render untrusted text, and return errors without stack traces or secrets.
12. Minimize sensitive data in logs, analytics, and evidence; define retention and access controls.
13. Use restrictive CORS, secure production cookies/HTTPS, and deliberate security headers.
14. Label demo/simulated data. Do not invent scale, customers, certifications, legal entities, or performance results.
15. Prefer a simple application architecture. Do not add services, dependencies, AI, or C++ without a justified need and measurement.
16. Preserve existing good work; inspect before changing. Update architecture, tasks, and memory when decisions or implementation change.
17. Every completed feature needs error handling, authorization, tenant isolation, constraints, auditability, documentation, tests, accessibility, and responsive behavior appropriate to its risk.
