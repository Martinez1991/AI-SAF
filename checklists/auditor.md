# Auditor Checklist

Evidence-based conformance. For each requirement, require **design + config + test +
operational** evidence (see `docs/04-verification-methodology.md`). A single passing run
is insufficient.

- [ ] Target assurance level declared and justified per application (AI.V1, docs/03)
- [ ] Each in-scope requirement has traceable evidence (AI.V16)
- [ ] Adversarial test corpora are maintained and dated (AI.V6.2, AI.V10.3)
- [ ] Bypass-rate metrics tracked over time, not point-in-time (AI.V10.9)
- [ ] Logs are tamper-evident, retained, and correlation-linked (AI.V13)
- [ ] Guardrail/quota failures demonstrably fail closed (AI.V10.5, AI.V12)
- [ ] Tool/MCP inventory with version pinning and assessments (AI.V8.6, AI.V15)
- [ ] Mappings to external standards current and verified (AI.V16, risk-matrix/)
- [ ] Deletion/erasure verifiable across stores, embeddings, logs, backups (AI.V11)
