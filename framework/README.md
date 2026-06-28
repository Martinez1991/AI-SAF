# AI-SAF — The Framework

This directory contains the standard itself: one file per domain.

## Conventions

- **Identifier:** `AI.V<domain>.<number>` — stable, never reused.
- **Levels:** `L1` ⊂ `L2` ⊂ `L3` (cumulative). A ✓ marks the **lowest** level at which
  the requirement first applies; it remains required at higher levels.
- **Maps to:** external references — `LLM01–LLM10` (OWASP Top 10 for LLM Apps 2025),
  `ASI` (OWASP Top 10 for Agentic Applications 2026), `ATLAS` (MITRE ATLAS),
  `NIST` (AI RMF function), `ISO` (ISO/IEC 42001/5338). See
  [`../risk-matrix/mappings.md`](../risk-matrix/mappings.md).
- **Phrasing:** every requirement begins "Verify that …" and describes a single
  testable property. See [`_TEMPLATE.md`](_TEMPLATE.md).

## Domains

| ID | File | Status |
|----|------|--------|
| AI.V1 | [AI.V1-architecture-governance.md](AI.V1-architecture-governance.md) | **drafted** |
| AI.V2 | [AI.V2-identity-authentication.md](AI.V2-identity-authentication.md) | **drafted** |
| AI.V3 | [AI.V3-secrets-credentials.md](AI.V3-secrets-credentials.md) | **drafted** |
| AI.V4 | [AI.V4-llm-pipeline.md](AI.V4-llm-pipeline.md) | **drafted** |
| AI.V5 | [AI.V5-model-security.md](AI.V5-model-security.md) | **drafted** |
| AI.V6 | [AI.V6-prompt-security.md](AI.V6-prompt-security.md) | **drafted** |
| AI.V7 | [AI.V7-rag-security.md](AI.V7-rag-security.md) | **drafted** |
| AI.V8 | [AI.V8-mcp-tool-security.md](AI.V8-mcp-tool-security.md) | **drafted** |
| AI.V9 | [AI.V9-agent-security.md](AI.V9-agent-security.md) | **drafted** |
| AI.V10 | [AI.V10-guardrails.md](AI.V10-guardrails.md) | **drafted** |
| AI.V11 | [AI.V11-data-protection-privacy.md](AI.V11-data-protection-privacy.md) | **drafted** |
| AI.V12 | [AI.V12-tokens-cost-rate-limiting.md](AI.V12-tokens-cost-rate-limiting.md) | **drafted** |
| AI.V13 | [AI.V13-observability-audit.md](AI.V13-observability-audit.md) | **drafted** |
| AI.V14 | [AI.V14-resilience-continuity.md](AI.V14-resilience-continuity.md) | **drafted** |
| AI.V15 | [AI.V15-ai-supply-chain.md](AI.V15-ai-supply-chain.md) | **drafted** |
| AI.V16 | [AI.V16-compliance-mappings.md](AI.V16-compliance-mappings.md) | **drafted** |
