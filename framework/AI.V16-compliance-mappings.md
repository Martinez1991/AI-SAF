# AI.V16 — Compliance & Mappings

**Objective:** tie AI-SAF requirements to external standards and regulatory
obligations for audit and adoption, so that every assessment result is traceable to
evidence and to the frameworks an organization is accountable to.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V16.1 | Verify that a target assurance level (L1/L2/L3) is documented and approved for the application, with a recorded justification for the selection. | ✓ | | | NIST, ISO |
| AI.V16.2 | Verify that each implemented requirement has traceable evidence (an assessment artifact) supporting its pass/fail claim, suitable for independent audit. | ✓ | | | NIST, ISO |
| AI.V16.3 | Verify that a maintained mapping exists linking each applicable AI-SAF requirement to the external frameworks it satisfies (OWASP LLM Top 10, OWASP Agentic Security Initiative, MITRE ATLAS, NIST AI RMF, ISO/IEC 42001) per ../risk-matrix/mappings.md. | | ✓ | | NIST, ISO |
| AI.V16.4 | Verify that gaps — requirements not met at the approved target level — are documented with a risk-acceptance decision or a remediation plan with an owner and target date. | | ✓ | | NIST, ISO |
| AI.V16.5 | Verify that applicable AI regulation (e.g., EU AI Act) is identified and mapped to the relevant AI-SAF requirements where in scope, with the basis for applicability recorded. | | | ✓ | NIST, ISO |
| AI.V16.6 | Verify that the mapping and evidence set is reviewed and updated when referenced standards or the application materially change, so that no stale mappings remain. | | | ✓ | NIST, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V16.1** — Locate the approval record for the target assurance level. Confirm it
names the approver, the level, and a justification tied to the application's risk
profile (data sensitivity, exposure, regulatory scope). A level chosen without recorded
rationale fails.

**AI.V16.2** — Sample implemented requirements across domains and trace each pass/fail
claim to its artifact (test output, configuration snapshot, design record, scan result).
A claim with no retrievable evidence is not auditable and fails.

**AI.V16.3** — Open the mapping in ../risk-matrix/mappings.md. For a sample of
applicable requirements, confirm a current entry exists for each referenced framework
and that the cited control identifiers resolve in the source standard.

**AI.V16.4** — Cross-check the requirement set against the gap register. Every unmet
requirement at the target level must appear with either a signed risk acceptance or a
remediation plan carrying an owner and a date. Silent gaps fail.

**AI.V16.5** — Review the regulatory-applicability determination. Where a regulation is
in scope, confirm its obligations are mapped to specific AI-SAF requirements and that
the scoping basis (jurisdiction, system role, risk tier) is documented.

**AI.V16.6** — Inspect review metadata (dates, change triggers) on the mapping and
evidence set. Confirm a review followed the most recent standard revision or material
application change; mappings referencing superseded versions are stale and fail.

## Related domains

- **AI.V1 Architecture & Governance** — defines the governance and risk-ownership
  structures that approve target levels and accept residual risk (AI.V16.1, AI.V16.4).
- **AI.V13 Observability & Audit** — produces much of the evidence traced in AI.V16.2.
- **AI.V11 Data Protection & Privacy** — primary source of regulatory obligations
  mapped under AI.V16.5.
- **../risk-matrix/mappings.md** — the canonical cross-framework mapping maintained and
  verified by this domain.
