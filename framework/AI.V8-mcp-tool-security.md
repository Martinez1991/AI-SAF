# AI.V8 — MCP & Tool Security

**Objective:** ensure that every capability a model can invoke — functions, APIs, and
MCP servers — is authenticated, least-privileged, independently scoped, validated, and
fully logged, so a model (or a compromised tool) cannot exceed its intended authority.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V8.1 | Verify that every tool / MCP server requires authentication and that anonymous tool invocation is not possible. | ✓ | | | ASI |
| AI.V8.2 | Verify that each tool operates under least privilege, with an explicitly defined and independently scoped authorization boundary. | ✓ | | | LLM06, ASI |
| AI.V8.3 | Verify that all tool / MCP invocations are logged with caller identity, inputs, outputs, and a correlation identifier. | ✓ | | | LLM06 |
| AI.V8.4 | Verify that tool inputs are validated against a schema and that non-conforming inputs are rejected. | | ✓ | | LLM05 |
| AI.V8.5 | Verify that high-impact tool actions (state-changing, financial, destructive, or irreversible) require an explicit policy decision enforced outside the model. | | ✓ | | LLM06, ASI |
| AI.V8.6 | Verify that third-party MCP servers and tools are inventoried, version-pinned, and security-assessed before being connected. | | ✓ | | LLM03 |
| AI.V8.7 | Verify that tool execution is sandboxed/isolated (constrained network egress, ephemeral credentials, resource limits) so a compromised tool cannot pivot to other systems. | | | ✓ | LLM03, ASI |
| AI.V8.8 | Verify that agent-to-tool identities are non-shared and revocable, enabling per-action attribution and immediate de-authorization. | | | ✓ | ASI |
| AI.V8.9 | Verify that tool / MCP outputs are treated as untrusted data and cannot drive privileged action when they contain instruction-like content. | | ✓ | | LLM01 |
| AI.V8.10 | Verify that the high-impact action inventory defines which actions require human-in-the-loop confirmation, and that such confirmation is enforced outside the model. | | | ✓ | LLM06, ASI |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V8.1 / AI.V8.2** — Enumerate every registered tool/MCP server. Attempt invocation
without credentials (expect denial). For each tool, inspect its granted scope and
confirm it is independent — compromising one tool's credentials must not grant another
tool's authority.

**AI.V8.4** — Send malicious/oversized/wrong-type payloads to a tool and confirm schema
validation rejects them.

**AI.V8.9** — Confirm tool output is not implicitly trusted: inject instruction-like
text in a tool result and verify it does not drive privileged action (links to
AI.V6.6/AI.V6.7 indirect injection).

**AI.V8.5** — Identify the high-impact action inventory. For each, verify a policy
decision point exists outside the model.

**AI.V8.10** — For actions flagged as requiring human-in-the-loop confirmation, verify
the confirmation is enforced outside the model (not merely prompted for by the model).

**AI.V8.7** — Review the execution environment: network egress allow-list, credential
TTLs, CPU/memory/time limits, filesystem isolation. Attempt egress to a disallowed
host from within a tool sandbox (expect block).

## Related domains

- **AI.V9 Agent Security** — agents are the primary tool *callers*; multi-step
  orchestration risks (loops, delegation) live there.
- **AI.V3 Secrets** — ephemeral credential issuance for tools.
- **AI.V15 Supply Chain** — provenance/assessment of third-party MCP servers.
- **AI.V13 Observability** — the logging substrate for AI.V8.3.
