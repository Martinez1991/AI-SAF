# AI.V5 — Model Security

**Objective:** protect model artifacts and behavior against poisoning, tampering, theft,
and unsafe alignment drift — so that every model placed into service is of verified
provenance, loaded safely, stored with integrity, and continuously observed for
deviation from its approved behavior.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V5.1 | Verify that every model artifact's provenance, version, and license are recorded and confirmed against the supplier's published source before the artifact is used. | ✓ | | | LLM03, ISO |
| AI.V5.2 | Verify that each model artifact is loaded only after its cryptographic checksum (or signature) is validated against a trusted reference, and that mismatches block loading. | ✓ | | | LLM03, NIST |
| AI.V5.3 | Verify that model files are deserialized using a safe-by-design format (e.g., safetensors) and that unsafe-by-default formats permitting arbitrary code execution (e.g., pickle) are rejected at load time. | ✓ | | | LLM03, ATLAS |
| AI.V5.4 | Verify that stored model weights are integrity-protected and access-controlled, with read/write restricted to authorized identities and all modifications logged. | | ✓ | | LLM04, NIST |
| AI.V5.5 | Verify that every fine-tuned or otherwise customized model is tested for backdoors, triggers, and poisoning artifacts, and that promotion to production is blocked until results are reviewed. | | ✓ | | LLM04, ATLAS |
| AI.V5.6 | Verify that production model behavior is monitored for alignment and behavioral drift against an approved baseline, with alerting on deviation. | | ✓ | | LLM04, NIST |
| AI.V5.7 | Verify that controls against model extraction are enforced (query-rate and abuse limits, response shaping, and anomaly detection on high-volume or systematic querying patterns). | | | ✓ | ATLAS, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V5.1 / AI.V5.2** — Inspect the model inventory and confirm each entry records
source, version, and license. For a sample, recompute the artifact checksum and compare
to the trusted reference; tamper with one byte of a staged artifact and confirm loading
is refused (links to AI.V15 supply-chain provenance).

**AI.V5.3** — Attempt to load a model serialized in an unsafe format (e.g., pickle) and
confirm it is rejected. Confirm the loader does not silently fall back to code-executing
deserialization for unrecognized or legacy files.

**AI.V5.4** — Review storage ACLs and integrity controls on the weight store. Attempt
read and write as an unauthorized identity (expect denial). Modify a stored artifact and
confirm the change is detected and logged.

**AI.V5.5** — Identify the pre-promotion test suite for customized models. Confirm it
includes trigger/backdoor probing and poisoning checks, that results are recorded, and
that a human review gate blocks promotion on unresolved findings.

**AI.V5.6** — Confirm a behavioral baseline exists and that production outputs are
sampled and compared against it. Induce a known deviation and verify the alert fires and
is routed to an owner.

**AI.V5.7** — Exercise the inference endpoint with high-volume and systematic query
patterns and confirm rate/abuse limits and anomaly detection engage before enough
input/output pairs are exposed to reconstruct the model (links to AI.V12 rate limiting).

## Related domains

- **AI.V15 AI Supply Chain** — provenance, checksum, and license verification of model
  artifacts originates with supply-chain controls (AI.V5.1/AI.V5.2).
- **AI.V12 Tokens, Cost & Rate Limiting** — the query-rate and abuse controls that blunt
  model-extraction attacks (AI.V5.7).
- **AI.V13 Observability & Audit** — the monitoring and logging substrate for drift
  detection and weight-modification audit (AI.V5.4/AI.V5.6).
- **AI.V4 LLM Pipeline** — training and fine-tuning data integrity that upstream of
  backdoor/poisoning testing (AI.V5.5).
