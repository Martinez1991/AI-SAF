# AI.V3 — Secrets & Credential Management

**Objective:** ensure secrets used by AI components and tools are stored, injected,
scoped, and rotated securely — so that credentials never enter the model context, never
persist in plaintext, and a leaked secret has the smallest possible blast radius and the
shortest possible lifetime.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V3.1 | Verify that no secret (API key, token, password, private key, connection string) is present in prompts, system prompts, code, or any content placed into the model context. | ✓ | | | LLM02 |
| AI.V3.2 | Verify that secrets are never committed to source control or stored in plaintext in configuration or environment files distributed with the application. | ✓ | | | ISO |
| AI.V3.3 | Verify that secrets are never written to logs, traces, telemetry, or error messages in cleartext, and that redaction is applied before persistence. | ✓ | | | LLM02, ISO |
| AI.V3.4 | Verify that all secrets used by AI components and tools are retrieved at runtime from a centralized secret manager / vault rather than from static files or hardcoded values. | | ✓ | | NIST, ISO |
| AI.V3.5 | Verify that each tool and agent receives a distinct, least-privilege credential scoped to only the resources it requires, so a leaked credential cannot access other systems. | | ✓ | | NIST, ATLAS |
| AI.V3.6 | Verify that the CI/CD pipeline runs automated secrets scanning that blocks build artifacts, images, and commits containing detectable credentials. | | ✓ | | LLM02, ISO |
| AI.V3.7 | Verify that credentials are ephemeral / just-in-time and automatically rotated and revocable, with no long-lived static keys issued to AI components or tools. | | | ✓ | NIST, ATLAS |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V3.1** — Inspect rendered prompts, system prompts, retrieved context, and tool
definitions for embedded credentials. Search prompt-construction code for secret
references injected into model input. Any secret reaching the context window is a fail
(links to AI.V6.8 system-prompt hygiene).

**AI.V3.2 / AI.V3.3** — Scan the repository history, build artifacts, container images,
and deployed config for plaintext secrets. Exercise error and verbose-logging paths,
then inspect logs, traces, and telemetry sinks to confirm secrets are redacted before
persistence (links to AI.V13 observability).

**AI.V3.4** — Trace how each component obtains its secrets at runtime. Confirm retrieval
is from a vault / secret manager with access control and audit, not from static files,
baked-in values, or unmanaged environment variables.

**AI.V3.5** — Enumerate the credentials issued to each tool/agent and inspect their
granted scope. Confirm credentials are non-shared and minimally scoped: compromising one
tool's credential must not grant access to another tool's resources (links to AI.V8.7).

**AI.V3.6** — Submit a known test credential through a commit and a build and confirm the
scanning gate detects and blocks it. Review pipeline configuration to confirm the scan is
enforced (fails the build) rather than advisory.

**AI.V3.7** — Inspect credential issuance for time-to-live and rotation policy. Confirm
no long-lived static keys exist for AI components; revoke an active credential and verify
in-flight access is denied within the documented window.

## Related domains

- **AI.V8 MCP & Tool Security** — consumes the ephemeral, per-tool credentials defined
  here for sandboxed tool execution (AI.V8.7).
- **AI.V13 Observability & Audit** — the logging/telemetry substrate that must enforce
  the secret redaction required by AI.V3.3.
- **AI.V6 Prompt Security** — system-prompt and context hygiene that keeps secrets out of
  the model context (AI.V6.8).
- **AI.V2 Identity & Authentication** — the identity model under which scoped, revocable
  tool/agent credentials are issued.
