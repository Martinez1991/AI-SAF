# AI.V13 — Observability, Logging & Audit

**Objective:** ensure AI-specific events are logged, correlated, retained, and
auditable without leaking sensitive data — so that any AI action can be attributed,
reconstructed, and investigated, and so that logs feed detection and alerting rather
than becoming a new exfiltration surface.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V13.1 | Verify that security-relevant AI events — prompt-injection detections, guardrail decisions, tool/MCP invocations, authentication and authorization decisions, and agent steps — are recorded to a durable log. | ✓ | | | ASI, NIST |
| AI.V13.2 | Verify that a single correlation identifier links every related event (prompt, guardrail, retrieval, tool, and agent steps) across one request or session. | ✓ | | | ASI, ATLAS |
| AI.V13.3 | Verify that sensitive data, secrets, and PII-bearing prompt content are masked or redacted before log records are written, so they never appear in logs in the clear. | ✓ | | | LLM02, ISO |
| AI.V13.4 | Verify that logs are emitted in a structured, queryable format. | | ✓ | | NIST, ISO |
| AI.V13.5 | Verify that the audit trail is sufficient to reconstruct who or what caused a given AI action, including the initiating identity, the model and prompt version, and the resulting decision or output. | | ✓ | | ASI, NIST, ISO |
| AI.V13.6 | Verify that AI logs and metrics are exported to detection and alerting pipelines, enabling anomaly and rogue-agent alerts to fire on defined conditions. | | ✓ | | ATLAS, NIST |
| AI.V13.7 | Verify that audit logs are tamper-evident and retained for a defined retention period in accordance with a documented retention and disposal policy. | | | ✓ | ISO, NIST |
| AI.V13.8 | Verify that event timestamps derive from a synchronized, trusted time source, within a defined acceptable clock skew. | | ✓ | | NIST, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V13.1** — Enumerate the security-relevant AI event types and trigger one of each
(e.g., force a guardrail block per AI.V10.5, invoke a tool per AI.V8.3, attempt an
unauthorized action). Confirm each produces a corresponding durable log record.

**AI.V13.2** — Issue a request that traverses prompt, retrieval, guardrail, tool, and
agent steps. Query the logs by the correlation identifier and confirm every step of the
chain is returned under that single identifier.

**AI.V13.3** — Submit a prompt containing known secrets and synthetic PII. Inspect the
resulting log records and confirm the sensitive values are masked/redacted before write
(links to AI.V11 data protection and AI.V3 secrets).

**AI.V13.4** — Parse sampled log records programmatically to confirm a consistent
structured schema.

**AI.V13.8** — Compare event timestamps across components against the reference time
source and confirm clock synchronization within the defined acceptable skew.

**AI.V13.5** — Pick a completed AI action and, using only the audit trail, reconstruct
the initiating identity, model/prompt version, inputs, and resulting decision. Confirm
the trail is complete enough to support attribution (traceability for AI.V16).

**AI.V13.6** — Inject a condition that should raise an alert (e.g., an anomalous
consumption spike per AI.V12.6 or rogue-agent behavior per AI.V9) and confirm the log/
metric pipeline detects it and fires the alert.

**AI.V13.7** — Attempt to modify or delete an existing audit record and confirm the
tamper-evidence mechanism detects or prevents it. Review the retention policy and
confirm records are kept — and disposed of — per the documented period.

## Related domains

- **AI.V8 MCP & Tool Security** — tool/MCP invocation logging (AI.V8.3) writes into
  this observability substrate.
- **AI.V10 Guardrails** — guardrail decisions (AI.V10.5) are a primary logged event.
- **AI.V11 Data Protection & Privacy** — defines the sensitive-data and PII classes that
  AI.V13.3 redaction must cover before write.
- **AI.V16 Compliance & Mappings** — relies on this audit trail for traceability and
  evidence of control operation.
