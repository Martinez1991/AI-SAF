# Reference Architecture

A vendor-neutral secure reference design for AI applications. Each numbered control
point ties back to the AI-SAF domain(s) it satisfies. This is a **target architecture**
to reason about where requirements are enforced — not a mandated product list.

## Data flow (high level)

```
                        ┌─────────────────────────────────────────────┐
  User / Client ──▶ (1) │ AI Gateway / LLM Firewall (input guardrails) │
                        └───────────────┬─────────────────────────────┘
                                        │  (2) AuthN/AuthZ (user & agent identity)
                                        ▼
                        ┌─────────────────────────────────────────────┐
                        │ Orchestration / Agent layer                 │
                        │  • context construction & trust hierarchy   │  (3)
                        │  • iteration/recursion & token budgets       │
                        └───────┬───────────────────────┬─────────────┘
                                │                       │
                  (4) RAG retrieval            (5) Tools / MCP servers
                  • source allow-list          • per-tool auth & scope
                  • doc sanitization           • schema validation
                  • vector store isolation     • sandboxed execution
                                │                       │
                                ▼                       ▼
                        ┌─────────────────────────────────────────────┐
                        │ Model(s) — hosted or local                  │  (6)
                        └───────────────┬─────────────────────────────┘
                                        ▼
                        ┌─────────────────────────────────────────────┐
  User / downstream ◀── │ Output guardrails: validation + DLP masking │  (7)
                        └─────────────────────────────────────────────┘

        (8) Cross-cutting: Observability/Audit · Secrets · Rate limiting/Cost ·
            Supply-chain integrity · Resilience/fail-closed
```

## Control points → AI-SAF domains

| # | Control point | Domains |
|---|---------------|---------|
| 1 | Input guardrail / firewall | AI.V10 |
| 2 | User & agent authentication/authorization | AI.V2, AI.V6.5 |
| 3 | Orchestration: context, trust hierarchy, budgets | AI.V6, AI.V9, AI.V12 |
| 4 | RAG retrieval | AI.V7 |
| 5 | Tools / MCP | AI.V8 |
| 6 | Model serving | AI.V5 |
| 7 | Output guardrail + DLP | AI.V10, AI.V11 |
| 8 | Cross-cutting | AI.V3, AI.V12, AI.V13, AI.V14, AI.V15 |

**Key principle:** every security decision is enforced at a layer **independent of the
model**. The model is treated as untrusted (zero-trust model handling).
