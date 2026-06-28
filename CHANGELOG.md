# Changelog

All notable changes to AI-SAF are documented here. Versions follow the roadmap in the
[README](README.md). This is a community draft proposed for submission to the OWASP
Foundation; it is not yet an OWASP project.

## [v0.2.1] — 2026-06-27 — Atomicity splits

### Changed
- Split nine bundled requirements into single-property requirements so each is
  independently testable, **without reusing or renumbering existing IDs** (per the
  stable-identifier rule in [CONTRIBUTING.md](CONTRIBUTING.md)). The original ID was
  narrowed to one property and the second property added as a new trailing ID:
  - AI.V2.4 (MFA) → new **AI.V2.8** (service/agent mutual auth).
  - AI.V6.2 (injection detection) → new **AI.V6.9** (detection logging).
  - AI.V8.4 (input schema validation) → new **AI.V8.9** (tool output treated as untrusted).
  - AI.V8.5 (policy decision) → new **AI.V8.10** (human-in-the-loop confirmation).
  - AI.V10.4 (sensitive-data detection, now layer-independent) → new **AI.V10.8** (masking/redaction).
  - AI.V10.6 (guardrail versioning) → new **AI.V10.9** (FP/FN efficacy metrics).
  - AI.V11.5 (lawful basis + DPA) → new **AI.V11.8** (provider training/retention opt-out).
  - AI.V13.4 (structured log format) → new **AI.V13.8** (synchronized time source).
  - AI.V14.3 (backup + integrity) → new **AI.V14.8** (tested restore drill).
- Requirement count rises from 113 to 122. Cross-references in examples, threat models,
  and checklists updated to the split IDs.

## [v0.2] — 2026-06-27 — Full Draft

### Added
- **All 16 domains drafted.** AI.V1–AI.V16 now contain atomic, testable,
  level-tagged (L1/L2/L3) requirements in the "Verify that …" house style
  (113 requirements total), each with verification guidance and cross-domain
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
- Confirm per-requirement (not just per-domain) external mappings.
- Coordinate with the OWASP AI Exchange to reference rather than re-derive its catalog.

## [v0.1] — Foundation

- Initial manifesto, terminology, assurance levels, domain structure, mapping skeleton,
  and four fully drafted domains (AI.V6, AI.V8, AI.V10, AI.V12).
