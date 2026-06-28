# AI.V11 — Data Protection & Privacy

**Objective:** protect personal and sensitive data across prompts, outputs, memory,
embeddings, logs, and backups.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V11.1 | Verify that a data classification scheme defines what is "personal", "sensitive", and "regulated" for the AI system, and that this scheme is the authoritative source driving masking and minimization controls. | ✓ | | | LLM02, ISO |
| AI.V11.2 | Verify that sensitive data at rest and in transit across the AI data flow (prompts, context, embeddings, memory, caches, logs, backups) is encrypted using approved algorithms and managed keys. | ✓ | | | LLM02, NIST, ISO |
| AI.V11.3 | Verify that only the minimum sensitive data necessary enters prompts and model context, and that it is masked, tokenized, or omitted where the task does not require it in cleartext. | | ✓ | | LLM02, ASI |
| AI.V11.4 | Verify that retention limits are defined and enforced for conversation, memory, and derived data, so that records are automatically purged once the retention period expires. | | ✓ | | LLM02, ISO |
| AI.V11.5 | Verify that sensitive or regulated data is not sent to third-party model providers without a lawful basis and a contractual data-handling agreement, and that training/retention opt-out is enabled where the provider offers it. | | ✓ | | LLM02, ATLAS, ISO |
| AI.V11.6 | Verify that a right-to-erasure (deletion) request can be fully executed across all stores — primary database, vector embeddings, caches, logs, backups, and agent memory — with evidence that no recoverable copy of the subject's data remains. | | | ✓ | LLM02, ISO |
| AI.V11.7 | Verify that privacy-enhancing techniques (e.g., differential privacy, anonymization, or pseudonymization) are applied when training or fine-tuning models on personal data, with a documented and measurable privacy parameter. | | | ✓ | LLM02, ATLAS, NIST |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V11.1** — Obtain the data classification scheme and confirm it enumerates concrete
categories (PII, secrets, regulated/special-category data). Trace at least one category
to the control that consumes it — masking (AI.V10.4) and minimization (AI.V11.3) must
reference this scheme rather than ad-hoc, per-component definitions.

**AI.V11.2** — Inspect each store in the AI data flow (prompt/context store, vector
database, memory store, cache, log pipeline, backups) and confirm encryption at rest with
managed keys, plus TLS in transit between components. Confirm embeddings and backups are
not an unencrypted exception.

**AI.V11.3** — Capture the actual prompt/context sent to the model for a representative
task and confirm sensitive fields not required for the task are masked, tokenized, or
absent. A field present in cleartext must be justified by the task.

**AI.V11.5** — Review the contract/DPA with each external provider and the provider
configuration. Confirm a lawful basis is recorded and that training/retention opt-out is
set where available. Attempt to identify any sensitive payload leaving the boundary
without coverage.

**AI.V11.6** — Issue a test erasure request for a seeded data subject. After completion,
query each store independently — primary DB, embeddings, caches, logs, backups, and agent
memory — and confirm no recoverable copy remains (including derived embeddings).

**AI.V11.7** — Where models are trained/fine-tuned on personal data, review the pipeline
for the privacy technique applied and confirm a measurable parameter (e.g., the ε budget
for differential privacy) is documented rather than asserted qualitatively.

## Related domains

- **AI.V10 Guardrails** — AI.V10.4 performs the runtime masking/redaction; AI.V11.1
  defines *what* must be masked.
- **AI.V3 Secrets** — manages the keys underpinning the encryption required by AI.V11.2.
- **AI.V7 RAG Security** — embeddings are an in-scope store for encryption (AI.V11.2)
  and erasure (AI.V11.6).
- **AI.V13 Observability** — logs are a sensitive-data store subject to classification,
  retention, and deletion controls.
