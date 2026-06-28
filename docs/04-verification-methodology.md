# Verification Methodology

AI-SAF verification combines conventional AppSec testing with AI-specific,
non-deterministic testing. Because model behavior is probabilistic, a single passing
run is **not** sufficient evidence.

## Evidence types

1. **Design evidence** — architecture diagrams, data-flow, trust boundaries showing
   where a control is enforced (not just that it exists).
2. **Configuration evidence** — settings, policies, IaC for gateways, guardrails,
   quotas, IAM scopes.
3. **Test evidence** — results of executing a documented test suite, including
   adversarial / red-team batteries.
4. **Operational evidence** — logs, metrics, and alerts demonstrating the control
   works in production.

## AI-specific testing requirements

- **Adversarial, not anecdotal.** Where a requirement says "blocked", verification
  needs a *maintained corpus* of payloads (e.g., jailbreaks, indirect-injection docs),
  with a stated pass threshold and tracked false-negative rate.
- **Repeatable under non-determinism.** Run each adversarial case N times; report the
  bypass rate, not a single result.
- **Enforcement-layer check.** For any control that *could* be implemented in the
  prompt, verify it is actually enforced outside the model (gateway/app/service).
  Prompt-only controls fail verification.
- **Fail-closed check.** Confirm that when a guardrail or quota errors, the system
  denies rather than allows.

## Suggested tooling (non-normative)

Automated red-team / probing frameworks, output DLP scanners, AI gateways/firewalls,
and observability platforms. AI-SAF is tool-agnostic; the standard specifies the
*property to verify*, never the product.
