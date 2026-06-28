# Developer Checklist

Build-time controls.

- [ ] User input treated as untrusted; not concatenated into privileged context (AI.V6.1)
- [ ] Injection detection wired before the model; detections logged (AI.V6.2/.9)
- [ ] No secrets/credentials/rules in system prompts (AI.V6.8, AI.V3)
- [ ] Session/tenant context isolation implemented and tested (AI.V6.3)
- [ ] Retrieved/tool content sanitized and delimited (AI.V6.6)
- [ ] Tool inputs schema-validated; tool outputs treated as untrusted (AI.V8.4/.9)
- [ ] High-impact actions gated by policy / human confirmation (AI.V8.5/.10)
- [ ] Output validation + PII/secret masking before delivery (AI.V10.2/.4/.8)
- [ ] Per-user/per-agent quotas + rate limits enforced server-side (AI.V12.1/.2/.3)
- [ ] Iteration/recursion/token budget caps for agents (AI.V12.5)
- [ ] Ephemeral, scoped credentials for tools (AI.V3, AI.V8.8)
