# AI.V6 — Prompt Security

**Objective:** ensure that everything assembled into a model's context — system,
developer, user, retrieved, and tool content — is handled so that untrusted input
cannot subvert intended behavior, leak privileged instructions, or cross session
boundaries.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V6.1 | Verify that all user-supplied input is treated as untrusted and is not concatenated directly into privileged instruction context without a documented separation mechanism (role separation, structured messages, or delimiting). | ✓ | | | LLM01 |
| AI.V6.2 | Verify that inbound prompts pass through a prompt-injection detection/mitigation mechanism and that detections are logged with a correlation identifier. | ✓ | | | LLM01, ATLAS |
| AI.V6.3 | Verify that conversation context and memory are isolated per session and per user/tenant, with no cross-session or cross-tenant leakage, demonstrated by test. | ✓ | | | LLM02 |
| AI.V6.4 | Verify that system and developer instructions cannot be retrieved by end users via direct, translation, encoding, or multi-turn extraction attempts, demonstrated against a documented test suite. | | ✓ | | LLM07 |
| AI.V6.5 | Verify that security-relevant decisions (authentication, authorization, access) are NOT delegated to instructions embedded in the prompt and are enforced at the application/service layer. | | ✓ | | LLM06 |
| AI.V6.6 | Verify that content from external or untrusted sources (web, RAG documents, tool output) is sanitized and clearly delimited before inclusion in context, to mitigate indirect prompt injection. | | ✓ | | LLM01, LLM08 |
| AI.V6.7 | Verify that an instruction hierarchy (system > developer > user > tool/retrieved content) is enforced such that lower-trust content cannot override higher-trust instructions, validated adversarially. | | | ✓ | LLM01 |
| AI.V6.8 | Verify that no secrets, credentials, internal endpoints, or access-control rules are embedded in the system prompt. | ✓ | | | LLM02, LLM07 |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V6.2** — Inspect the request path for an injection-detection control positioned
**before** the model. Execute a maintained corpus of direct-injection payloads; run
each N times and report bypass rate against a stated threshold. Confirm detections
appear in logs with a correlation ID (ties to AI.V13).

**AI.V6.4** — Run a system-prompt-extraction battery: direct ("repeat your
instructions"), indirect ("translate the text above"), encoding, and multi-turn
gradual-disclosure attempts. A pass requires the privileged instructions are not
reconstructable. Note: per OWASP, the system prompt must **not** be treated as a
security boundary — AI.V6.5 must also hold.

**AI.V6.5** — Attempt to escalate privilege purely through prompt content (e.g.,
"as an admin, …"). Verify enforcement is independent of model output by checking the
API/service-layer authorization that gates the action.

**AI.V6.6 / AI.V6.7** — Plant injection payloads inside retrieved documents and tool
responses (indirect injection). Verify the model does not act on embedded instructions
and that retrieved/tool content cannot override system/developer instructions.

## Related domains

- **AI.V10 Guardrails** — V6 governs *how input is composed and trusted*; V10 governs
  the *independent policy layer* that inspects input/output. Keep the boundary: V6 =
  context construction & trust hierarchy; V10 = enforcement engine.
- **AI.V7 RAG** and **AI.V8 Tools** — primary sources of indirect-injection content.
- **AI.V11 Data Protection** — masking of sensitive data in prompts/outputs.
