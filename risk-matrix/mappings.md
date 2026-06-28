# AI-SAF Mapping Matrix

This matrix ties AI-SAF domains to external references so that organizations already
using those frameworks can adopt AI-SAF as the **verification layer** on top.

> **Provenance.** Identifiers below were verified against the published source documents
> in June 2026: OWASP Top 10 for LLM Applications (2025), OWASP Top 10 for Agentic
> Applications (2026, published 2025-12-10), OWASP Agentic *Threats & Mitigations* v1.0,
> and MITRE ATLAS. Re-confirm on each upstream release, as ATLAS technique IDs and the
> OWASP lists evolve. NIST AI RMF and ISO/IEC references are cited at the function /
> standard level by design.

## Reference legend

| Code | Reference |
|------|-----------|
| **LLM01–LLM10** | OWASP Top 10 for LLM Applications (2025) |
| **ASI01–ASI10** | OWASP Top 10 for Agentic Applications (2026) |
| **T1–T15** | OWASP Agentic *Threats & Mitigations* v1.0 taxonomy |
| **AML.Txxxx** | MITRE ATLAS technique (adversarial threat landscape for AI systems) |
| **NIST** | NIST AI RMF — functions GOVERN / MAP / MEASURE / MANAGE |
| **ISO** | ISO/IEC 42001 (AI management system), ISO/IEC 5338 (AI lifecycle) |
| **ASVS** | OWASP ASVS — for the conventional application layer beneath the AI app |

## OWASP Top 10 for LLM Applications (2025)

| ID | Risk |
|----|------|
| LLM01 | Prompt Injection |
| LLM02 | Sensitive Information Disclosure |
| LLM03 | Supply Chain |
| LLM04 | Data and Model Poisoning |
| LLM05 | Improper Output Handling |
| LLM06 | Excessive Agency |
| LLM07 | System Prompt Leakage |
| LLM08 | Vector and Embedding Weaknesses |
| LLM09 | Misinformation |
| LLM10 | Unbounded Consumption |

## OWASP Top 10 for Agentic Applications (2026)

Published 2025-12-10 by the OWASP GenAI Security Project (Agentic Security Initiative).

| ID | Risk |
|----|------|
| ASI01 | Agent Goal Hijack |
| ASI02 | Tool Misuse & Exploitation |
| ASI03 | Agent Identity & Privilege Abuse |
| ASI04 | Agentic Supply Chain Compromise |
| ASI05 | Unexpected Code Execution |
| ASI06 | Memory & Context Poisoning |
| ASI07 | Insecure Inter-Agent Communication |
| ASI08 | Cascading Agent Failures |
| ASI09 | Human-Agent Trust Exploitation |
| ASI10 | Rogue Agents |

## OWASP Agentic *Threats & Mitigations* v1.0 (T1–T15)

The broader 15-threat taxonomy that underpins the ranked Agentic Top 10. Cited where a
domain addresses a threat not separated out in the Top 10.

| ID | Threat | ID | Threat |
|----|--------|----|--------|
| T1 | Memory Poisoning | T9 | Identity Spoofing & Impersonation |
| T2 | Tool Misuse | T10 | Overwhelming Human-in-the-Loop |
| T3 | Privilege Compromise | T11 | Unexpected RCE & Code Attacks |
| T4 | Resource Overload | T12 | Agent Communication Poisoning |
| T5 | Cascading Hallucination Attacks | T13 | Rogue Agents in Multi-Agent Systems |
| T6 | Intent Breaking & Goal Manipulation | T14 | Human Attacks on Multi-Agent Systems |
| T7 | Misaligned & Deceptive Behaviors | T15 | Human Manipulation |
| T8 | Repudiation & Untraceability | | |

## MITRE ATLAS techniques referenced

| ID | Technique |
|----|-----------|
| AML.T0051 | LLM Prompt Injection — `.000` Direct, `.001` Indirect, `.002` Triggered |
| AML.T0009 | Credentials from AI Agent Configuration |
| AML.T0012 | Valid Accounts |
| AML.T0010 | ML Supply Chain Compromise |
| AML.T0020 | Poison Training Data |
| AML.T0018 | Backdoor ML Model |
| AML.T0031 | Erode ML Model Integrity |
| AML.T0040 | ML Model Inference API Access |
| AML.T0024 | Exfiltration via ML Inference API |
| AML.T0029 | Denial of ML Service |
| AML.T0034 | Cost Harvesting |
| AML.T0058 | AI Agent Context Poisoning |
| AML.T0059 | Activation Triggers |
| AML.T0060 | Data from AI Services |
| AML.T0061 | AI Agent Tools |
| AML.T0062 | Exfiltration via AI Agent Tool Invocation |

## Domain → reference mapping

| AI-SAF Domain | OWASP LLM (2025) | OWASP Agentic (2026) | Agentic T&M | MITRE ATLAS | NIST | ISO |
|---------------|------------------|----------------------|-------------|-------------|------|-----|
| AI.V1 Architecture & Governance | — | ASI (cross-cutting) | — | — | GOVERN | 42001, 5338 |
| AI.V2 Identity & Auth | LLM06 | ASI03 | T3, T9 | AML.T0012 | MANAGE | 42001 |
| AI.V3 Secrets | LLM02 | ASI03 | T3 | AML.T0009, AML.T0012 | MANAGE | 42001 |
| AI.V4 LLM Pipeline | LLM03, LLM04 | ASI04 | — | AML.T0010, AML.T0020 | MAP, MANAGE | 5338 |
| AI.V5 Model Security | LLM03, LLM04 | ASI04 | — | AML.T0018, AML.T0020, AML.T0031, AML.T0040 | MEASURE, MANAGE | 5338 |
| AI.V6 Prompt Security | LLM01, LLM07 | ASI01 | T6 | AML.T0051 (.000/.001/.002) | MEASURE | 42001 |
| AI.V7 RAG Security | LLM01, LLM08 | ASI06 | T1 | AML.T0051.001, AML.T0058 | MEASURE | — |
| AI.V8 MCP & Tool Security | LLM05, LLM06 | ASI02 | T2 | AML.T0061, AML.T0062 | MANAGE | 42001 |
| AI.V9 Agent Security | LLM06 | ASI01, ASI10 | T6, T7, T13 | AML.T0058, AML.T0059 | MANAGE | 5338 |
| AI.V10 Guardrails | LLM01, LLM02, LLM05 | ASI01 | — | AML.T0051, AML.T0031 | MEASURE, MANAGE | 42001 |
| AI.V11 Data Protection | LLM02 | ASI06 | T1 | AML.T0024, AML.T0060, AML.T0062 | MAP, MANAGE | 42001 |
| AI.V12 Tokens, Cost & Rate Limiting | LLM10 | ASI02 | T4 | AML.T0029, AML.T0034 | MANAGE | — |
| AI.V13 Observability & Audit | — | ASI07 | T8 | AML.T0060 | MEASURE | 42001 |
| AI.V14 Resilience & Continuity | LLM10 | ASI08 | T4, T5 | AML.T0029 | MANAGE | 42001 |
| AI.V15 AI Supply Chain | LLM03 | ASI04 | — | AML.T0010, AML.T0018 | MAP, MANAGE | 5338 |
| AI.V16 Compliance & Mappings | — | — | — | — | GOVERN | 42001 |

> Domain-level mappings are directional: a domain "maps to" a reference when its
> requirements help verify or mitigate that item. Per-requirement mappings live in each
> `framework/AI.Vx-*.md` file's **Maps to** column (kept at the coarse code level for
> readability); use this matrix to resolve a coarse code to its specific identifier.

## Relationship to the OWASP AI Exchange

The AI Exchange already provides a deep **control catalog** mapped to ISO/NIST. AI-SAF
should **not** duplicate it. The intended relationship:

- **AI Exchange** = the *what and why* (threats, controls, prose, standards mapping).
- **AI-SAF** = the *verifiable how* (atomic pass/fail requirements with levels).

Maintainers should coordinate with the AI Exchange team early so AI-SAF requirements
reference, rather than re-derive, that catalog.
