# AI-SAF — AI Security Assurance Framework

**A community draft of a verifiable security standard for AI applications.**
**Status:** `v0.2 — Full Draft` · **Proposed for submission to the OWASP Foundation.**

> ⚠️ **Affiliation notice.** AI-SAF is **not yet an OWASP project**. "OWASP" is a
> registered trademark of the OWASP Foundation, and the name/logo may only be used
> after a project is formally accepted. Until then this work is an independent
> community draft. The OWASP branding in this repository is intentionally withheld
> and will be enabled only upon acceptance into the OWASP Incubator. See
> [`docs/00-introduction.md`](docs/00-introduction.md#affiliation--naming).

---

## What this is

AI-SAF is a list of **numbered, testable security requirements** for designing,
building, deploying, and operating applications based on generative AI — LLMs, RAG,
MCP/tools, and autonomous agents. It is technology- and vendor-neutral.

It answers, with evidence:

- Is my AI application secure?
- Which controls must I implement, at what assurance level?
- How do I *verify* each control (not just assert it)?
- How do I audit an AI application against a repeatable baseline?

## Why it exists (the gap)

The OWASP GenAI ecosystem is already strong, but it is mostly **risk catalogs**
(Top 10 for LLM Applications, Top 10 for Agentic Applications) and **prose guidance**
(AI Exchange). What is missing is an **ASVS-style verification standard**: each
requirement is atomic, objectively testable, and tagged to an assurance level.

AI-SAF is positioned as the **verification layer on top of** those catalogs, not as a
competing catalog. Every requirement maps back to existing references
(see [`risk-matrix/mappings.md`](risk-matrix/mappings.md)).

## Assurance levels

Requirements are cumulative — L2 includes all of L1; L3 includes all of L2.

| Level | Name | Target |
|-------|------|--------|
| **L1** | Baseline / Essential | Minimum for any AI application; mostly black-box verifiable. |
| **L2** | Standard / Recommended | Apps handling sensitive data or exposing tools/agents. Most production targets. |
| **L3** | Advanced / High-Assurance | High-risk, autonomous, or regulated deployments; defense-in-depth + formal verification. |

Full definitions: [`docs/03-levels.md`](docs/03-levels.md).

## Requirement identifier

```
AI.V<domain>.<number>
        │        └── sequential within the domain
        └── domain number (V1–V16)
```

Example: `AI.V6.2` = second requirement of the Prompt Security domain.

## Domains

| ID | Domain | Status |
|----|--------|--------|
| AI.V1 | Architecture & Governance | drafted |
| AI.V2 | User & Agent Identity / Authentication | drafted |
| AI.V3 | Secrets & Credential Management | drafted |
| AI.V4 | LLM Pipeline Security | drafted |
| AI.V5 | Model Security | drafted |
| AI.V6 | Prompt Security | drafted |
| AI.V7 | RAG Security | drafted |
| AI.V8 | MCP & Tool Security | drafted |
| AI.V9 | Autonomous Agent Security | drafted |
| AI.V10 | Guardrails & LLM Firewalls | drafted |
| AI.V11 | Data Protection & Privacy | drafted |
| AI.V12 | Tokens, Cost & Rate Limiting | drafted |
| AI.V13 | Observability, Logging & Audit | drafted |
| AI.V14 | Resilience & Continuity | drafted |
| AI.V15 | AI Supply Chain | drafted |
| AI.V16 | Compliance & Mappings | drafted |

Domain index and conventions: [`framework/README.md`](framework/README.md).

## Repository layout

```
/docs                    Introduction, terminology, levels, methodology
/framework               The standard itself — one file per domain (V1–V16)
/examples                Worked assessments applying AI-SAF to real architectures
/reference-architecture  Secure reference design for AI applications
/threat-models           Threat models the requirements defend against
/risk-matrix             Cross-standard mappings + maturity matrix
/checklists              Role-derived views (architect, developer, pentester, auditor)
```

## Roadmap

- **v0.1 Foundation** — manifesto, terminology, levels, domain structure, mapping
  skeleton.
- **v0.2 Full Draft** *(this release)* — all 16 domains drafted with ~115 verifiable,
  level-tagged requirements; cross-domain references; mapping matrix.
- **v0.5 Core Standard** — requirement review and refinement; confirmed external-standard
  sub-IDs; full mappings; first worked examples.
- **v0.9 Community Preview** — public consultation, expert review.
- **OWASP Incubator** — formal submission; maintainer committee.
- **Production** — tooling (self-assessment, CLI, CI/CD API, dashboard), adoption.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). Requirements must be atomic, testable, and
mapped before merge.

## License

Documentation is intended to be released under **CC BY-SA 4.0**; any tooling under a
permissive license (Apache-2.0 / MIT). Final terms to be confirmed by project leads.
See [`LICENSE`](LICENSE).
