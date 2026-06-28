# AI.V2 — User & Agent Identity / Authentication

**Objective:** ensure that users, services, and agents are authenticated with distinct, attributable identities.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V2.1 | Verify that every AI-exposing endpoint requires authentication and that anonymous or unauthenticated access to model, agent, or tool functionality is not possible. | ✓ | | | ASI, NIST |
| AI.V2.2 | Verify that human users, agents, and services each authenticate with distinct identities and that no shared, ambient, or hard-coded credential is reused across multiple agents or services. | ✓ | | | LLM06, ASI |
| AI.V2.3 | Verify that every action taken by an agent is attributable to a single agent identity, recorded at the time of the action so the responsible principal can be determined after the fact. | | ✓ | | ASI, ATLAS |
| AI.V2.4 | Verify that strong authentication is enforced on AI-exposing endpoints — MFA for human users and mutual authentication (e.g., mTLS) for service and agent callers — at the API/gateway layer. | | ✓ | | NIST, ISO |
| AI.V2.5 | Verify that agent and service credentials are short-lived and revocable, and that revocation takes effect for in-flight and subsequent requests without requiring a redeploy. | | ✓ | | ASI, NIST |
| AI.V2.6 | Verify that delegation or impersonation (an agent acting on behalf of a user) is explicit, carries bounded and auditable authority, and cannot exceed the delegating principal's permissions. | | | ✓ | LLM06, ASI |
| AI.V2.7 | Verify that each session is cryptographically bound to its authenticated principal and tenant so a session token cannot be replayed or reused across users, agents, or tenants. | | | ✓ | ASI, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains required at all higher levels.

## Verification guidance

**AI.V2.1** — Inventory every endpoint that reaches model, agent, or tool functionality (including internal and management interfaces). Send requests with no credentials and with malformed/expired credentials; expect consistent denial. Confirm no debug, health, or fallback path bypasses authentication.

**AI.V2.2** — Enumerate the identities used by humans, agents, and services. Inspect credential stores and configuration for shared secrets, hard-coded API keys, or a single service account fronting multiple agents. Each agent and service must present its own credential; cross-reference issued identities against the running principals.

**AI.V2.3** — Trigger an agent action and inspect the resulting audit record. Confirm it names the specific agent identity (not a generic gateway or service account) and is written atomically with the action. Run two agents concurrently and verify their actions remain individually attributable. Links to AI.V8.8.

**AI.V2.4** — For human flows, attempt authentication with a valid password but no second factor (expect denial). For service/agent flows, attempt connection without a client certificate or with an untrusted one (expect denial). Confirm enforcement happens at the API/gateway layer rather than relying on the application or model behavior.

**AI.V2.5** — Read an issued agent/service credential and record its lifetime; confirm it is bounded and renewed via short-lived issuance rather than a long-lived static secret. Revoke a credential, then replay it on an in-flight and a new request; both must be rejected without redeploying the service.

**AI.V2.6** — Identify a delegation/impersonation path. Confirm the on-behalf-of relationship is explicit in the token/request, that the effective authority is the intersection of agent and user permissions (never broader than the user), and that the delegation is logged. Attempt to escalate beyond the delegating user's scope (expect denial).

**AI.V2.7** — Capture a valid session token and replay it from a different user, agent, or tenant context; expect rejection. Verify the token is bound to principal and tenant (e.g., via cryptographic binding to identity/tenant claims) so a leaked or copied session cannot be reused outside its original context.

## Related domains

- **AI.V8 MCP & Tool Security** — tool invocation depends on the caller already holding a distinct, authenticated identity; per-agent attribution here (AI.V2.3) feeds the tool-level logging in AI.V8.8.
- **AI.V9 Agent Security** — agents are the principals authenticated and attributed by this domain; bounded delegation (AI.V2.6) constrains the authority an agent may exercise.
- **AI.V3 Authorization & Access Control** — authentication establishes *who* a principal is; authorization decides *what* that identity may do, consuming the distinct identities and session bindings defined here.
