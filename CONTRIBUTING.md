# Contributing to AI-SAF

AI-SAF is a community draft. Contributions are welcome from anyone.

## Principles for every requirement

A requirement is only mergeable if it is:

1. **Atomic** — one verifiable property per requirement.
2. **Testable** — a competent assessor can produce a pass/fail result with evidence.
   Avoid unfalsifiable verbs ("should consider", "be aware of").
3. **Level-tagged** — assigned to L1, L2, and/or L3 (cumulative).
4. **Mapped** — references at least one external standard (OWASP LLM Top 10 2025,
   OWASP Top 10 for Agentic Applications 2026, MITRE ATLAS, NIST AI RMF, ISO/IEC 42001).
5. **Vendor-neutral** — no requirement may assume a specific model, provider, or SDK.

## Writing style

- Phrase every requirement as: **"Verify that …"** (matches ASVS convention).
- Prefer enforceable, layer-specific language ("enforced at the API/gateway layer")
  over model-dependent language ("the model should refuse").
- If a control can be bypassed by prompt content, it is not a control — say where it
  is actually enforced.

## Requirement format

Each domain file uses one table:

| # | Requirement | L1 | L2 | L3 | Maps to |

…followed by a **Verification guidance** subsection for non-obvious requirements,
keyed by requirement ID.

## Workflow

1. Open an issue describing the gap or proposed requirement.
2. Submit a PR editing the relevant `framework/AI.Vx-*.md` file.
3. Update `risk-matrix/mappings.md` if you add/alter a mapping.
4. At least one maintainer review is required to merge.
