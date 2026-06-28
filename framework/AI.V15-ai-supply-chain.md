# AI.V15 — AI Supply Chain

**Objective:** establish provenance, integrity, and assessment for models, datasets,
libraries, plugins, and MCP servers — so that every component entering the AI stack is
inventoried, sourced from a trusted origin, verified before use, version-pinned, and
kept current under a controlled update process.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V15.1 | Verify that an AI Bill of Materials (AIBOM) inventories every model, dataset, library, plugin, and MCP server in the stack, including version and source, and that it is updated whenever a component is added, removed, or upgraded. | ✓ | | | LLM03, ISO |
| AI.V15.2 | Verify that every model, dataset, and dependency is acquired only from an approved, trusted source, and that artifacts from unverifiable or untrusted origins are rejected before adoption. | ✓ | | | LLM03, NIST |
| AI.V15.3 | Verify that each model and dataset has its provenance and integrity confirmed (cryptographic signature or checksum validated against a trusted reference) before it is used, and that mismatches block use. | ✓ | | | LLM03, ATLAS |
| AI.V15.4 | Verify that the licensing and usage terms of every third-party model, dataset, and library are recorded and confirmed as compatible with the intended use before adoption. | ✓ | | | LLM03, ISO |
| AI.V15.5 | Verify that third-party models, datasets, and MCP servers are security-assessed against a defined acceptance standard before adoption, with results recorded and a gate blocking adoption on unresolved findings. | | ✓ | | LLM03, LLM04 |
| AI.V15.6 | Verify that the AI stack (frameworks, runtimes, libraries, and plugins) is continuously scanned for known vulnerabilities and that remediation occurs within a defined, severity-based patch SLA. | | ✓ | | LLM03, NIST |
| AI.V15.7 | Verify that all model, dataset, and dependency versions are pinned, and that updates are applied only through a reviewed, controlled process with no silent automatic pulling of latest versions. | | | ✓ | LLM03, ATLAS |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V15.1** — Inspect the AIBOM and confirm it enumerates every model, dataset,
library, plugin, and MCP server with version and source. Add or upgrade a component and
confirm the inventory is updated as part of that change (links to AI.V8.6 third-party
tool inventory).

**AI.V15.2** — Review the list of approved sources and the acquisition process. Attempt
to introduce an artifact from an unapproved or unverifiable origin and confirm it is
rejected before it can be adopted.

**AI.V15.3** — For a sample of models and datasets, recompute the checksum or validate
the signature against the trusted reference. Tamper with one byte of a staged artifact
and confirm its use is refused (links to AI.V5.1/AI.V5.2 model provenance and integrity).

**AI.V15.4** — Confirm that license and usage terms are recorded for each third-party
component and that an adoption gate verifies compatibility with the intended use before
the component enters the stack.

**AI.V15.5** — Identify the pre-adoption assessment standard for third-party models,
datasets, and MCP servers. Confirm assessments are performed and recorded, and that an
adoption gate blocks components with unresolved findings (links to AI.V8.6).

**AI.V15.6** — Review the vulnerability-scanning coverage across frameworks, runtimes,
libraries, and plugins. Introduce a component with a known vulnerability and confirm it
is detected; confirm a severity-based patch SLA is defined and tracked to remediation.

**AI.V15.7** — Inspect manifests/lockfiles and confirm models, datasets, and
dependencies are version-pinned. Confirm updates flow through a reviewed change process
and that no component auto-pulls the latest version without that review.

## Related domains

- **AI.V5 Model Security** — provenance, checksum/signature, and license verification of
  model artifacts (AI.V15.3/AI.V15.4) are the supply-chain origin of AI.V5.1/AI.V5.2.
- **AI.V8 MCP & Tool Security** — inventory, version-pinning, and security assessment of
  third-party MCP servers (AI.V15.1/AI.V15.5) underpin AI.V8.6.
- **AI.V4 LLM Pipeline** — dataset provenance and integrity controls protect training
  and fine-tuning data against poisoning upstream of the pipeline.
- **AI.V13 Observability & Audit** — the inventory and scanning records that evidence
  AIBOM currency and patch-SLA compliance.
