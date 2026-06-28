# AI.V14 — Resilience & Continuity

**Objective:** ensure the AI application degrades gracefully, recovers cleanly, and
withstands abuse and provider failure — failing closed on security-relevant paths,
surviving the loss of any single model or dependency, and restoring critical AI state
to a known-clean baseline after compromise.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V14.1 | Verify that when the model, guardrail, or a security-relevant dependency is unavailable, the application fails closed for that path — denying or safely degrading the action rather than bypassing the control. | ✓ | | | LLM10, ASI |
| AI.V14.2 | Verify that model and tool calls enforce bounded timeouts and that a failed or slow dependency returns a defined error or fallback instead of hanging indefinitely. | ✓ | | | LLM10 |
| AI.V14.3 | Verify that critical AI state (configurations, system prompts, guardrail policies, vector indexes, agent memory) is backed up and integrity-protected. | | ✓ | | LLM10, ISO |
| AI.V14.4 | Verify that critical AI functions do not depend on a single model provider or endpoint, providing documented failover or redundancy so the loss of one provider does not cause total outage. | | ✓ | | LLM10, NIST |
| AI.V14.5 | Verify that AI-specific incident scenarios (prompt injection, data leakage, rogue agent, denial-of-wallet) are documented in the incident-response plan and exercised through tabletop or simulation. | | ✓ | | ATLAS, NIST, ISO |
| AI.V14.6 | Verify that circuit breakers and back-pressure constrain model and tool call volume under failure or abuse, preventing a single failing dependency from cascading into broader outage. | | | ✓ | LLM10, ASI |
| AI.V14.7 | Verify that, following a detected compromise (e.g. poisoned memory, tampered index, leaked credentials), the application can be recovered to a defined known-clean state with the affected AI state rolled back and reissued. | | | ✓ | ATLAS, NIST, ISO |
| AI.V14.8 | Verify that critical AI state is demonstrably recoverable through a periodic, tested restore drill. | | ✓ | | LLM10, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V14.1** — Disable or fault-inject the model and each guardrail in turn. Confirm
that security-relevant paths deny or safely degrade rather than fail open (links to
AI.V10.5). A guardrail outage must never silently allow unmoderated model output.

**AI.V14.2** — Inject latency and forced errors into model/tool dependencies. Confirm
each call enforces a finite timeout and returns a defined error or fallback. Verify no
unbounded retry loop amplifies load on the failing dependency (links to AI.V12).

**AI.V14.3** — Inspect backup coverage for configs, prompts, guardrail policies, indexes,
and agent memory. Verify backups are integrity-protected (signed or checksummed).

**AI.V14.8** — Perform a restore drill from backup and confirm the critical AI state is
recovered intact (links to AI.V7, AI.V9).

**AI.V14.4** — Review the dependency map for critical functions. For each, identify the
failover or redundancy mechanism and exercise provider failover, confirming no single
hard dependency causes total loss of a critical function.

**AI.V14.5** — Review the incident-response plan for the named AI-specific scenarios.
Confirm each has owners, detection sources, and containment steps, and that a tabletop
or simulation has been conducted and its findings tracked.

**AI.V14.6** — Drive the system past tool/model failure or abuse thresholds. Confirm
circuit breakers open, back-pressure is applied, and the failure is contained rather
than cascading across components (links to AI.V12).

**AI.V14.7** — Define the known-clean baseline. Simulate poisoning of memory or an index
and execute the recovery runbook, confirming the tainted state is rolled back, affected
credentials reissued, and the system returns to a verified-clean condition.

## Related domains

- **AI.V10 Guardrails** — fail-closed behaviour when a guardrail is unavailable
  (AI.V14.1 links to AI.V10.5).
- **AI.V12 Tokens, Cost & Rate Limiting** — timeouts, circuit breakers, and back-pressure
  that contain cascading failure and denial-of-wallet abuse.
- **AI.V7 RAG Security** — clean-state recovery and rollback of poisoned indexes.
- **AI.V9 Agent Security** — recovery of compromised agent memory and rogue-agent
  incident handling.
