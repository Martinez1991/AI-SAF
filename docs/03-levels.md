# Assurance Levels

Levels are **cumulative**: an application targeting L2 must satisfy all L1 and L2
requirements; L3 adds the L3 set on top.

## L1 — Baseline / Essential

- **Who:** every AI application, including internal tools and prototypes that touch
  real users or data.
- **Verification style:** largely black-box; achievable without source access.
- **Intent:** prevent the most common, high-likelihood failures (e.g., unfiltered
  input/output, no rate limiting, system-prompt leakage, cross-session leakage).

## L2 — Standard / Recommended

- **Who:** applications handling sensitive/regulated data, or exposing tools, RAG,
  or agentic behavior. **Default target for production.**
- **Verification style:** grey-box; assessor has architecture docs and config access.
- **Intent:** defense against realistic adversaries — indirect injection, tool misuse,
  data exfiltration, cost/abuse attacks.

## L3 — Advanced / High-Assurance

- **Who:** high-risk, highly autonomous, or regulated deployments (finance, health,
  critical infrastructure, large-blast-radius agents).
- **Verification style:** white-box; design review, adversarial testing, and evidence
  of defense-in-depth.
- **Intent:** assume controls will be probed; require independent, layered enforcement
  that fails closed.

## Choosing a target level

| If the application… | Minimum level |
|---------------------|---------------|
| Is read-only, no sensitive data, no tools | L1 |
| Handles PII/regulated data, or uses RAG | L2 |
| Can invoke tools / take actions | L2 |
| Acts autonomously with high-impact actions | L3 |
| Is in a regulated or safety-critical domain | L3 |
