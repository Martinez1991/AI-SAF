# Changelog

All notable changes to AI-SAF are documented here. Versions follow the roadmap in the
[README](README.md). This is a community draft proposed for submission to the OWASP
Foundation; it is not yet an OWASP project.

## [v0.2] — 2026-06-27 — Full Draft

### Added
- **All 16 domains drafted.** AI.V1–AI.V16 now contain atomic, testable,
  level-tagged (L1/L2/L3) requirements in the "Verify that …" house style
  (~115 requirements total), each with verification guidance and cross-domain
  references. Previously only AI.V6, AI.V8, AI.V10, AI.V12 were drafted.
- **Verified external mappings.** `risk-matrix/mappings.md` now cites real
  identifiers, verified against the published sources (June 2026):
  - OWASP Top 10 for LLM Applications (2025) — LLM01–LLM10.
  - OWASP Top 10 for Agentic Applications (2026) — ASI01–ASI10.
  - OWASP Agentic *Threats & Mitigations* v1.0 — T1–T15.
  - MITRE ATLAS technique IDs (AML.Txxxx), including the AML.T0051 prompt-injection
    sub-techniques.
- **Worked examples** for the L1, L2, and L3 archetypes:
  internal doc-Q&A prototype (L1), internal tool-using assistant (L2),
  multi-agent financial-operations workflow (L3) — alongside the existing RAG chatbot (L2).
- **Per-archetype threat models** (RAG chatbot, tool-using assistant, multi-agent
  system, fine-tuning pipeline) plus ATLAS/ASI identifiers added to the generic
  threat catalog.

### Changed
- Roadmap, status tables, and version banner updated to v0.2.
- Applied an adversarial review pass across all domains: fixed broken cross-references
  (AI.V2→AI.V3, AI.V7→AI.V2/AI.V15), corrected an AI.V6.7 mislabel in AI.V9, resolved a
  level/duplication conflict between AI.V9.2 and AI.V12.5, and re-leveled AI.V5.7
  (model-extraction defenses) from L3 to L2.

### Known follow-ups (targeting v0.5)
- Split a few remaining non-atomic requirements (e.g. AI.V8.4, AI.V10.6, AI.V11.5)
  into single-property requirements; this will renumber within those domains.
- Confirm per-requirement (not just per-domain) external mappings.
- Coordinate with the OWASP AI Exchange to reference rather than re-derive its catalog.

## [v0.1] — Foundation

- Initial manifesto, terminology, assurance levels, domain structure, mapping skeleton,
  and four fully drafted domains (AI.V6, AI.V8, AI.V10, AI.V12).
