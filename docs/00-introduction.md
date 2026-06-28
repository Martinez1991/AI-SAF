# Introduction

## Mission

Define an open standard of **verifiable** requirements to design, develop, deploy, and
operate applications based on generative AI — LLMs, RAG, MCP, and autonomous agents —
securely, independent of vendor or technology.

## Scope

AI-SAF covers any AI application, regardless of provider or stack:

- Commercial and open-source LLMs
- Autonomous agents and multi-agent systems
- Retrieval-Augmented Generation (RAG)
- Model Context Protocol (MCP) and tools
- Memory / context stores
- Multimodal models
- AI pipelines, fine-tuning, and inference
- Hosted or locally-run models

It deliberately avoids being "about OpenAI" or "about LLMs" specifically. The unit of
assessment is the **application**, not the model.

## What AI-SAF is and is not

| AI-SAF **is** | AI-SAF **is not** |
|---------------|-------------------|
| A list of testable requirements with assurance levels | A risk catalog / "Top 10" |
| A verification layer that maps to existing catalogs | A replacement for the OWASP AI Exchange |
| Vendor- and model-neutral | A product, tool, or benchmark of a model |
| A basis for audit and CI/CD gating | A compliance certification (on its own) |

## Affiliation & naming

AI-SAF is an **independent community draft** that is *proposed for submission* to the
OWASP Foundation. It is **not** an OWASP project at this time.

- "OWASP" is a registered trademark; its name and logo may not be used until a project
  is formally accepted by the Foundation.
- Until acceptance, the canonical name is **AI-SAF / AI Security Assurance Framework**
  with no OWASP prefix or logo.
- On acceptance into the OWASP Incubator, branding can be enabled per the OWASP
  Branding Guidelines, and the project must then identify itself as an OWASP project.

> **Naming note for maintainers:** the core artifact is a set of *verifiable,
> leveled requirements*. The label "Verification Standard" describes this more
> precisely than "Assurance Framework" and positions the project as the
> AI counterpart to OWASP ASVS, while "Assurance" overlaps semantically with
> OWASP SAMM. This is flagged for a deliberate naming decision before submission.

## How to read a requirement

```
AI.V6.2  | Verify that inbound prompts pass through a prompt-injection            | L1
         | detection/mitigation mechanism positioned before the model.            |
         |                                                    Maps to: LLM01, ATLAS
```

- **ID** — stable identifier, never reused.
- **Requirement** — a single property an assessor can test.
- **Level** — lowest assurance level at which it applies (cumulative upward).
- **Maps to** — external references this requirement satisfies/supports.
