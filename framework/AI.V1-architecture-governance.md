# AI.V1 — Architecture & Governance

**Objective:** establish ownership, threat modeling, trust boundaries, and an AI-specific security program across the whole AI lifecycle.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V1.1 | Verify that a documented architecture exists for the AI system, identifying every component (models, data stores, prompts, tools, memory, external services) and the trust boundaries and data flows between them. | ✓ | | | ASI, ISO |
| AI.V1.2 | Verify that an inventory of AI assets — models, datasets, prompts/templates, tools/plugins, and memory/vector stores — is maintained, with a named owner accountable for the security of each asset. | ✓ | | | ASI, ISO |
| AI.V1.3 | Verify that accountability for AI risk is formally assigned, with a defined owner empowered to accept, reject, or require remediation of identified risks before a system is deployed. | ✓ | | | NIST, ISO |
| AI.V1.4 | Verify that the AI system is included in the organization's secure development lifecycle (SDLC) and security program, with AI-specific security activities defined at each lifecycle stage. | | ✓ | | ISO, NIST |
| AI.V1.5 | Verify that a threat model covering AI-specific threats (prompt injection, data poisoning, model extraction, excessive agency) is produced and reviewed before model selection and again on material architecture change. | | ✓ | | ASI, NIST |
| AI.V1.6 | Verify that a policy governs which models, providers, and data-handling practices are approved for use, and that deployed systems are verified to conform to it. | | ✓ | | ISO, NIST |
| AI.V1.7 | Verify that an AI-specific risk assessment is performed, documented, and formally accepted, and that it is re-evaluated on a defined cadence and after significant changes to the system or its threat environment. | | | ✓ | NIST, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains required at all higher levels.

## Verification guidance

**AI.V1.1** — Request the architecture document and data-flow diagram. Confirm it names each model, data store, prompt source, tool/MCP server, and memory/vector store, and that trust boundaries are drawn where untrusted input crosses into the model context. Reject diagrams that omit external services or that show no boundary between user-supplied content and privileged operations.

**AI.V1.2** — Inspect the asset inventory. Sample entries and confirm each lists a named, current owner. Cross-check the inventory against the running system (deployed models, configured tools, connected data stores) to detect undocumented "shadow" assets.

**AI.V1.5** — Obtain the threat model and its revision history. Confirm it predates the model-selection decision and that it enumerates AI-specific threats rather than only generic application threats. Verify a review was triggered by the most recent material architecture change.

**AI.V1.6** — Review the approved-model/provider policy and the data-handling rules it sets. Select a deployed component and trace it back to an approved entry; flag any model, provider, or data flow in production that is absent from the policy.

**AI.V1.7** — Examine the risk assessment for explicit risk-acceptance sign-off by the accountable owner from AI.V1.3. Confirm a defined re-evaluation cadence exists and that the last review occurred within it, or was triggered by a significant change.

## Related domains

- **AI.V8 MCP & Tool Security** — the trust boundaries and asset inventory defined here scope the tools and MCP servers whose authentication and least-privilege controls AI.V8 enforces.
- **AI.V9 Agent Security** — governance ownership and threat modeling established here set the authority limits that agent-level controls operationalize at runtime.
- **AI.V15 AI Supply Chain** — the dataset and model inventory and the approved-provider policy feed directly into supply-chain provenance and integrity verification.
