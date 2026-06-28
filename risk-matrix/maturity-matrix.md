# AI-SAF Maturity Matrix

Assurance **levels** (L1/L2/L3) describe *which requirements apply*. The **maturity
matrix** describes *how well* an organization implements and operates them — useful for
program planning and roadmaps. The two are orthogonal: you can be mature (M3) at L1, or
immature (M1) while attempting L3.

| Maturity | Name | Characteristics |
|----------|------|-----------------|
| **M0** | Absent | No AI-specific controls; ad hoc usage. |
| **M1** | Initial | Some controls exist but are inconsistent, undocumented, untested. |
| **M2** | Defined | Controls documented and applied consistently; verified at release. |
| **M3** | Managed | Controls measured (FP/FN rates, bypass rates); metrics tracked over time. |
| **M4** | Optimizing | Continuous adversarial testing in CI/CD; automated response; feedback loop. |

## Suggested use

1. Pick a **target assurance level** per application (see `docs/03-levels.md`).
2. Assess current **maturity** per domain (M0–M4).
3. Prioritize gaps where a high-impact domain sits at low maturity.

| Domain | Target level | Current maturity | Gap |
|--------|:-----------:|:----------------:|-----|
| AI.V6 Prompt Security | L2 | _e.g. M1_ | _…_ |
| AI.V8 MCP & Tool Security | L2 | | |
| AI.V10 Guardrails | L2 | | |
| AI.V12 Tokens/Cost | L1 | | |

(Reproduce the row set for all 16 domains during a real assessment.)
