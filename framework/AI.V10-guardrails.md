# AI.V10 — Guardrails & LLM Firewalls

**Objective:** ensure that an enforcement layer **independent of the model** inspects
inputs and outputs, applies policy, masks sensitive data, and fails closed — so that
security does not depend on the model behaving correctly.

> **Boundary with AI.V6 (Prompt Security).** AI.V6 governs how context is *constructed*
> and the trust hierarchy among message sources. AI.V10 governs the *independent policy
> engine* (gateway / firewall / guardrail service) that evaluates traffic regardless of
> what the prompt says. Input validation appears in both only at their interface:
> V6.1 = "don't trust user input when composing context"; V10.1 = "an independent
> layer evaluates that input against policy."

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V10.1 | Verify that all inputs are evaluated by an input policy/guardrail layer, independent of the model, before reaching the model. | ✓ | | | LLM01 |
| AI.V10.2 | Verify that all model outputs are evaluated by an output policy/guardrail layer before delivery to the user or any downstream system. | ✓ | | | LLM05 |
| AI.V10.3 | Verify that known malicious and jailbreak patterns are blocked, demonstrated against a maintained adversarial test suite with a stated pass threshold. | ✓ | | | LLM01 |
| AI.V10.4 | Verify that sensitive data (PII, secrets, regulated data) in outputs is automatically detected and masked or redacted. | | ✓ | | LLM02 |
| AI.V10.5 | Verify that guardrail decisions are logged and that guardrail errors or unavailability fail closed (deny) rather than open. | | ✓ | | LLM05 |
| AI.V10.6 | Verify that guardrails are versioned and that their efficacy is measured with tracked metrics (false-positive and false-negative rates). | | ✓ | | NIST |
| AI.V10.7 | Verify that guardrails operate in defense-in-depth (multiple independent layers) and cannot be disabled or bypassed by model output or user input. | | | ✓ | LLM01 |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V10.1 / AI.V10.2** — Confirm via architecture review that the guardrail sits on
the request/response path and runs irrespective of model cooperation. Bypassing the
application entry point must not bypass the guardrail.

**AI.V10.3** — Execute the jailbreak/abuse corpus through the live path; run each case
N times; report bypass rate. The corpus must be maintained and dated.

**AI.V10.5 (fail-closed)** — Disable or fault-inject the guardrail service and confirm
the system denies requests rather than passing them straight to the model. Inspect
logs for the denial event.

**AI.V10.7** — Verify at least two independent enforcement layers (e.g., gateway WAF +
output DLP) and confirm neither can be turned off by crafted input/output.

## Related domains

- **AI.V6 Prompt Security** — context construction & trust hierarchy (see boundary
  note above).
- **AI.V11 Data Protection** — defines *what* counts as sensitive for AI.V10.4.
- **AI.V13 Observability** — logging/metrics substrate for AI.V10.5/AI.V10.6.
