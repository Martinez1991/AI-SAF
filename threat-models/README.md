# Threat Models

Threat models that motivate the AI-SAF requirements. Each entry names the threat, the
asset, the relevant AI-SAF domain(s), and the requirement(s) that defend against it.
Threats are aligned to OWASP LLM Top 10 (2025), the OWASP Agentic threat taxonomy, and
MITRE ATLAS. (See `risk-matrix/mappings.md` for the cross-standard table.)

## Generic LLM application — threat catalog

| Threat | Asset at risk | Domain | Defended by |
|--------|---------------|--------|-------------|
| Direct prompt injection | Model behavior | AI.V6, AI.V10 | AI.V6.1/.2, AI.V10.1/.3 |
| Indirect prompt injection (RAG/tool content) | Model behavior | AI.V6, AI.V7, AI.V8 | AI.V6.6/.7, AI.V8.4 |
| System-prompt leakage | Confidentiality of instructions | AI.V6 | AI.V6.4/.8 |
| Cross-session / cross-tenant context leakage | User data | AI.V6, AI.V11 | AI.V6.3 |
| Sensitive data disclosure in output | PII / secrets | AI.V10, AI.V11 | AI.V10.4 |
| Excessive agency / unauthorized tool action | Downstream systems | AI.V8, AI.V9 | AI.V8.2/.5 |
| Tool compromise → lateral movement | Infrastructure | AI.V8 | AI.V8.7/.8 |
| Denial-of-wallet / resource exhaustion | Availability & budget | AI.V12 | AI.V12.1–.6 |
| Runaway / looping agent | Availability & budget | AI.V9, AI.V12 | AI.V12.5 |
| Supply-chain compromise (model/MCP/dep) | Integrity | AI.V5, AI.V15 | AI.V8.6, AI.V15 |
| Guardrail bypass / fail-open | All of the above | AI.V10 | AI.V10.5/.7 |

## Notes

- This is a **starter** model for the generic case. v0.5 should add per-archetype
  models: RAG chatbot, tool-using assistant, multi-agent system, and a fine-tuning
  pipeline.
- Each threat row should eventually carry an ATLAS technique ID once verified.
