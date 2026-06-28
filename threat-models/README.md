# Threat Models

Threat models that motivate the AI-SAF requirements. Each entry names the threat, the
asset, the relevant AI-SAF domain(s), and the requirement(s) that defend against it.
Threats are aligned to OWASP LLM Top 10 (2025), the OWASP Agentic threat taxonomy, and
MITRE ATLAS. (See `risk-matrix/mappings.md` for the cross-standard table.)

## Generic LLM application — threat catalog

| Threat | Asset at risk | Domain | Defended by | ATLAS / ASI |
|--------|---------------|--------|-------------|-------------|
| Direct prompt injection | Model behavior | AI.V6, AI.V10 | AI.V6.1/.2, AI.V10.1/.3 | AML.T0051.000, ASI01 |
| Indirect prompt injection (RAG/tool content) | Model behavior | AI.V6, AI.V7, AI.V8 | AI.V6.6/.7, AI.V8.4 | AML.T0051.001, ASI01 |
| System-prompt leakage | Confidentiality of instructions | AI.V6 | AI.V6.4/.8 | AML.T0051, ASI01 |
| Cross-session / cross-tenant context leakage | User data | AI.V6, AI.V11 | AI.V6.3 | ASI06, T1 |
| Sensitive data disclosure in output | PII / secrets | AI.V10, AI.V11 | AI.V10.4/.8 | AML.T0024, AML.T0060 |
| Excessive agency / unauthorized tool action | Downstream systems | AI.V8, AI.V9 | AI.V8.2/.5 | ASI02, AML.T0061 |
| Tool compromise → lateral movement | Infrastructure | AI.V8 | AI.V8.7/.8 | AML.T0062, ASI02 |
| Denial-of-wallet / resource exhaustion | Availability & budget | AI.V12 | AI.V12.1–.6 | AML.T0034, ASI02, T4 |
| Runaway / looping agent | Availability & budget | AI.V9, AI.V12 | AI.V12.5 | ASI08, T4 |
| Supply-chain compromise (model/MCP/dep) | Integrity | AI.V5, AI.V15 | AI.V8.6, AI.V15 | AML.T0010, ASI04 |
| Guardrail bypass / fail-open | All of the above | AI.V10 | AI.V10.5/.7 | AML.T0031, ASI01 |
| Rogue agent | Other agents / systems | AI.V9 | AI.V9 | ASI10, T13 |

## Per-archetype threat models

Starter models for the four common deployment shapes. Each refines the generic catalog
for the assets and trust boundaries specific to that archetype.

### Archetype A — RAG chatbot

| Threat | Asset at risk | Domain | Defended by | ATLAS / ASI |
|--------|---------------|--------|-------------|-------------|
| Indirect injection via retrieved documents | Model behavior | AI.V7, AI.V6 | AI.V7, AI.V6.6/.7 | AML.T0051.001, ASI06 |
| Embedding / vector-store leakage | User data | AI.V7, AI.V11 | AI.V7, AI.V11 | LLM08, AML.T0060 |
| Cross-tenant retrieval (filter bypass) | Other tenants' data | AI.V7, AI.V11 | AI.V7, AI.V11 | ASI06, T1 |
| PII / secret disclosure in answer | PII / secrets | AI.V10, AI.V11 | AI.V10.4/.8, AI.V11 | AML.T0024, AML.T0060 |
| Retrieval-context poisoning (persisted) | Knowledge base integrity | AI.V7 | AI.V7 | AML.T0058, ASI06 |

### Archetype B — Tool-using assistant

| Threat | Asset at risk | Domain | Defended by | ATLAS / ASI |
|--------|---------------|--------|-------------|-------------|
| Excessive agency (scope creep) | Downstream systems | AI.V8, AI.V9 | AI.V8.2/.5 | ASI02, AML.T0061 |
| Unauthorized / unintended tool invocation | Downstream systems | AI.V8 | AI.V8.2/.5 | AML.T0062, ASI02 |
| Tool-output injection | Model behavior | AI.V8, AI.V6 | AI.V8.9, AI.V6.6 | AML.T0051.001, ASI01 |
| Sandbox / execution escape | Infrastructure | AI.V8 | AI.V8.7/.8 | ASI05, T11 |
| High-impact action without approval | Downstream systems | AI.V8, AI.V9 | AI.V8.5 | ASI02, AML.T0062 |

### Archetype C — Multi-agent system

| Threat | Asset at risk | Domain | Defended by | ATLAS / ASI |
|--------|---------------|--------|-------------|-------------|
| Agent goal hijack | Mission integrity | AI.V9, AI.V6 | AI.V9, AI.V6.1/.2 | ASI01, AML.T0051.000 |
| Inter-agent message spoofing / poisoning | Agent trust | AI.V9, AI.V13 | AI.V9, AI.V13 | ASI07, T12 |
| Rogue agent | Other agents / systems | AI.V9 | AI.V9 | ASI10, T13 |
| Cascading failure | Availability | AI.V9, AI.V14 | AI.V14, AI.V12.5 | ASI08, T5 |
| Memory poisoning | Shared state integrity | AI.V9, AI.V11 | AI.V9, AI.V11 | AML.T0058, ASI06, T1 |
| Loss of attribution / repudiation | Auditability | AI.V13 | AI.V13 | ASI07, T8 |

### Archetype D — Fine-tuning / training pipeline

| Threat | Asset at risk | Domain | Defended by | ATLAS / ASI |
|--------|---------------|--------|-------------|-------------|
| Training-data poisoning | Model integrity | AI.V4, AI.V5 | AI.V4, AI.V5 | AML.T0020, ASI04 |
| Model backdoor / trigger implant | Model integrity | AI.V5 | AI.V5 | AML.T0018, AML.T0059 |
| Supply-chain compromise (base model / datasets) | Integrity | AI.V4, AI.V15 | AI.V4, AI.V15 | AML.T0010, ASI04 |
| Pipeline privilege / separation-of-duties failure | Pipeline integrity | AI.V4, AI.V2 | AI.V4, AI.V2 | AML.T0012, T3 |
| Model theft / extraction | Model IP | AI.V5 | AI.V5 | AML.T0040, AML.T0031 |

## Notes

- These are **starter** models, to be deepened per requirement and per deployment in
  later revisions. Each row maps the threat to the assets and trust boundaries of its
  archetype; sub-requirement IDs are cited where stable and otherwise rolled up to the
  domain level.
- Every ATLAS technique ID and OWASP ASI / T identifier above was verified against the
  cross-standard matrix in `risk-matrix/mappings.md` (June 2026). Re-confirm on each
  upstream release, as ATLAS techniques and the OWASP lists evolve.
