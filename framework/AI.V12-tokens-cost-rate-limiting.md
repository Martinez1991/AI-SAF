# AI.V12 — Tokens, Cost & Rate Limiting

**Objective:** protect the application against resource-exhaustion, denial-of-wallet,
and runaway-agent failures by enforcing quotas, budgets, and limits, and by detecting
abnormal consumption.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V12.1 | Verify that per-user token/request quotas are enforced. | ✓ | | | LLM10 |
| AI.V12.2 | Verify that rate limiting is applied at the API/gateway layer for all model-invoking endpoints. | ✓ | | | LLM10 |
| AI.V12.3 | Verify that per-agent / per-session token budgets are enforced for multi-step or autonomous workflows. | | ✓ | | LLM10, ASI |
| AI.V12.4 | Verify that per-application cost budgets are configured with billing alerts and hard spending caps. | | ✓ | | LLM10 |
| AI.V12.5 | Verify that protections exist against context-window exhaustion and recursive/looping agent calls (maximum iterations and recursion-depth limits). | | ✓ | | LLM10, ASI |
| AI.V12.6 | Verify that anomaly detection on consumption (token spikes, abnormal call patterns) triggers automated throttling and alerting. | | | ✓ | LLM10 |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V12.1 / AI.V12.2** — Drive traffic past the configured per-user quota and rate
limit; confirm enforcement (HTTP 429 / rejection) and that limits are server-side, not
client-side.

**AI.V12.3 / AI.V12.5** — For agentic workflows, construct an input that would induce
many tool calls or deep recursion; confirm the run halts at the configured iteration /
depth / token budget rather than running unbounded.

**AI.V12.4** — Inspect provider/billing configuration for hard caps and alert
thresholds; confirm an alert fires on a simulated threshold breach.

**AI.V12.6** — Replay an abnormal consumption pattern; confirm automated throttling and
an alert (ties to AI.V13 observability).

## Related domains

- **AI.V9 Agent Security** — loop/recursion limits for autonomous orchestration.
- **AI.V13 Observability** — metrics and alerting substrate.
- **AI.V14 Resilience** — graceful degradation under load/abuse.
