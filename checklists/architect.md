# Architect Checklist

Design-time. Goal: enforce every security decision at a layer **independent of the model**.

- [ ] Trust boundaries and data-flow documented (AI.V1)
- [ ] Distinct identities for users, agents, services (AI.V2)
- [ ] Input + output guardrail layers placed on the request path (AI.V10.1/.2)
- [ ] Instruction trust hierarchy defined: system > developer > user > tool/retrieved (AI.V6.7)
- [ ] Authorization enforced outside the prompt, at API/service layer (AI.V6.5)
- [ ] Per-tool auth, least privilege, independent scopes (AI.V8.1/.2)
- [ ] Tool execution sandbox with egress controls (AI.V8.7)
- [ ] RAG source allow-list and vector-store isolation (AI.V7)
- [ ] Quotas, budgets, rate limits, loop/recursion caps designed in (AI.V12)
- [ ] Fail-closed behavior for guardrails and quotas (AI.V10.5)
- [ ] Observability with correlation IDs across components (AI.V13)
