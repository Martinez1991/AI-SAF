# AI-SAF Mapping Matrix

This matrix ties AI-SAF domains to external references so that organizations already
using those frameworks can adopt AI-SAF as the **verification layer** on top.

> ⚠️ **Draft — verify before publishing.** Domain-level mappings below are directional.
> **Exact item identifiers** (e.g., specific MITRE ATLAS technique IDs and the precise
> 2026 OWASP Agentic item numbers) **must be confirmed against the published source
> documents** before v0.5. Do not cite specific sub-IDs as authoritative until checked.

## Reference legend

| Code | Reference |
|------|-----------|
| **LLM01–LLM10** | OWASP Top 10 for LLM Applications (2025) |
| **ASI** | OWASP Top 10 for Agentic Applications (2026) |
| **ATLAS** | MITRE ATLAS (adversarial threat landscape for AI systems) |
| **NIST** | NIST AI RMF — functions GOVERN / MAP / MEASURE / MANAGE |
| **ISO** | ISO/IEC 42001 (AI management system), ISO/IEC 5338 (AI lifecycle) |
| **ASVS** | OWASP ASVS — for the conventional application layer beneath the AI app |

## OWASP Top 10 for LLM Applications (2025) — reference list

| ID | Risk |
|----|------|
| LLM01 | Prompt Injection |
| LLM02 | Sensitive Information Disclosure |
| LLM03 | Supply Chain |
| LLM04 | Data & Model Poisoning |
| LLM05 | Improper Output Handling |
| LLM06 | Excessive Agency |
| LLM07 | System Prompt Leakage |
| LLM08 | Vector & Embedding Weaknesses |
| LLM09 | Misinformation |
| LLM10 | Unbounded Consumption |

## Domain → reference mapping

| AI-SAF Domain | OWASP LLM Top 10 | OWASP Agentic (ASI) | MITRE ATLAS | NIST AI RMF | ISO |
|---------------|------------------|---------------------|-------------|-------------|-----|
| AI.V1 Architecture & Governance | — | ASI (governance) | — | GOVERN | 42001, 5338 |
| AI.V2 Identity & Auth | LLM06 | ASI (identity/spoofing) | Initial Access | MANAGE | 42001 |
| AI.V3 Secrets | LLM02 | — | Credential Access | MANAGE | 42001 |
| AI.V4 LLM Pipeline | LLM03, LLM04 | — | ML Attack Staging | MAP, MANAGE | 5338 |
| AI.V5 Model Security | LLM03, LLM04 | — | ML Model Access, Poisoning | MEASURE, MANAGE | 5338 |
| AI.V6 Prompt Security | LLM01, LLM02, LLM07 | ASI (goal hijacking) | LLM Prompt Injection | MEASURE | 42001 |
| AI.V7 RAG Security | LLM01, LLM08 | ASI (memory poisoning) | — | MEASURE | — |
| AI.V8 MCP & Tool Security | LLM05, LLM06, LLM03 | ASI (tool misuse) | Execution | MANAGE | 42001 |
| AI.V9 Agent Security | LLM06 | ASI (loss of control, rogue agents) | — | MANAGE | 5338 |
| AI.V10 Guardrails | LLM01, LLM02, LLM05 | ASI | Defense Evasion | MEASURE, MANAGE | 42001 |
| AI.V11 Data Protection | LLM02 | ASI (context leakage) | Exfiltration | MAP, MANAGE | 42001 |
| AI.V12 Tokens, Cost & Rate Limiting | LLM10 | ASI (resource abuse) | Impact | MANAGE | — |
| AI.V13 Observability & Audit | — | ASI | Discovery (detection) | MEASURE | 42001 |
| AI.V14 Resilience & Continuity | LLM10 | ASI | Impact | MANAGE | 42001 |
| AI.V15 AI Supply Chain | LLM03 | — | Supply Chain | MAP, MANAGE | 5338 |
| AI.V16 Compliance & Mappings | — | — | — | GOVERN | 42001 |

## Relationship to the OWASP AI Exchange

The AI Exchange already provides a deep **control catalog** mapped to ISO/NIST. AI-SAF
should **not** duplicate it. The intended relationship:

- **AI Exchange** = the *what and why* (threats, controls, prose, standards mapping).
- **AI-SAF** = the *verifiable how* (atomic pass/fail requirements with levels).

Maintainers should coordinate with the AI Exchange team early so AI-SAF requirements
reference, rather than re-derive, that catalog.
