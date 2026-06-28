# AI.V4 — LLM Pipeline Security

**Objective:** secure the build-and-serve pipeline: data ingestion, fine-tuning,
evaluation, and deployment, so that every model artifact reaching production has a
verifiable lineage, was built and promoted through controlled stages, and cannot be
tampered with, poisoned, or promoted without passing its safety gates.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V4.1 | Verify that each model version has a recorded, auditable manifest binding it to the exact training/fine-tuning datasets, configuration, and base model used to produce it. | ✓ | | | ISO, NIST |
| AI.V4.2 | Verify that training and fine-tuning data has documented provenance and is integrity-checked (checksums or signatures) before ingestion, and that ingestion rejects sources that fail verification. | ✓ | | | LLM04, LLM03 |
| AI.V4.3 | Verify that pipeline stages (ingestion, training, evaluation, deployment) enforce access control, so only authorized identities can trigger or modify each stage. | ✓ | | | ISO, NIST |
| AI.V4.4 | Verify that model artifacts are produced by a protected CI/CD pipeline and are cryptographically signed, with signatures verified before promotion or serving. | | ✓ | | LLM03 |
| AI.V4.5 | Verify that promotion to production is blocked by an automated pre-deployment evaluation gate covering adversarial robustness and safety, with a recorded pass/fail result per model version. | | ✓ | | LLM04, NIST |
| AI.V4.6 | Verify that training and evaluation environments are isolated from production data, secrets, and serving infrastructure. | | ✓ | | LLM04, ISO |
| AI.V4.7 | Verify that separation of duties is enforced across the pipeline, so that no single identity can ingest data, train, approve, and deploy a model version. | | | ✓ | NIST, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V4.1** — Pick a deployed model version and retrieve its manifest. Confirm it
records the dataset identifiers/versions, training configuration, and base model, and
that the record is immutable and timestamped. A model in production with no
reconstructable build record fails.

**AI.V4.2** — Inspect the ingestion process for a training dataset. Confirm each source
carries documented provenance and a checksum/signature, and that ingestion fails closed
when verification does not match. Attempt to ingest a source with a tampered or missing
checksum (expect rejection).

**AI.V4.4** — Review the build pipeline configuration: protected branches/runners,
restricted credentials, and signing of output artifacts. Attempt to load an unsigned or
re-signed artifact into the serving path (expect rejection). Confirm signature
verification occurs at promotion and at load, not only at build.

**AI.V4.5** — Identify the evaluation gate and its thresholds. Confirm a failing
adversarial/safety result blocks promotion automatically (not by manual discretion) and
that the result is recorded against the model version. Submit a model that fails a
known-bad test and confirm it cannot be promoted.

**AI.V4.6** — Map the training/eval environments' network and credential access. Confirm
they cannot reach production secrets or live serving systems. Attempt to read a
production secret from within a training job (expect denial).

**AI.V4.7** — Trace the identities authorized at each stage. Confirm that the union of
permissions held by any single identity cannot complete ingest → train → approve →
deploy without a second party. Attempt the full chain as one identity (expect a blocked
step).

## Related domains

- **AI.V5 Model Security** — protects the model artifact itself (weights, integrity,
  extraction); AI.V4 protects the process that builds and ships it.
- **AI.V15 AI Supply Chain** — provenance and assessment of base models, datasets, and
  third-party build dependencies consumed by the pipeline.
- **AI.V3 Secrets & Credentials** — issuance and isolation of the pipeline and signing
  credentials relied on by AI.V4.4 and AI.V4.6.
- **AI.V13 Observability & Audit** — the audit substrate for the build manifests and
  gate results recorded in AI.V4.1 and AI.V4.5.
