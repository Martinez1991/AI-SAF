# Worked Example — Internal Doc-Q&A Prototype (target L1)

**System:** an internal proof-of-concept "doc Q&A" assistant built by a single developer over a few days. It lets staff ask natural-language questions over an indexed set of internal documents by calling a hosted LLM API directly. There is no guardrail layer, no gateway, and no dedicated ops. It is exposed to a small internal pilot group on the corporate network.

**Target level:** L1 (minimum baseline).

This is an illustrative **partial** assessment — a real one covers all applicable requirements across all 16 domains. Only L1 requirements are assessed here, since L1 is the target.

| Requirement | Verification performed | Result | Evidence |
|-------------|------------------------|:------:|----------|
| AI.V6.1 Untrusted input separated from instructions | Reviewed prompt-assembly code; user question is passed as a distinct `user` role message, not concatenated into the system string | **PASS** | `chat.py` uses structured messages; system prompt is a separate constant |
| AI.V6.2 Injection detection on input | Sent 50 direct-injection payloads ("ignore previous instructions…") through the live path | **FAIL** | No detection control exists before the model; 50/50 reached the LLM unfiltered |
| AI.V6.3 Per-session/user context isolation | Opened two concurrent sessions and probed for cross-session bleed | **PASS** | History is keyed per session id; no leakage observed across 20 trials |
| AI.V6.8 No secrets in system prompt | Inspected the rendered system prompt for embedded credentials or endpoints | **PASS** | System prompt contains role/format guidance only; no secrets present |
| AI.V3.1 No secrets in model context | Inspected prompt-construction path for credentials injected into context | **PASS** | API key is read from an env var and used only on the HTTP client, never placed in context |
| AI.V3.2 No secrets in source control | Grepped the working tree and config for plaintext secrets | **FAIL** | Hardcoded provider API key found in `config.py` (`API_KEY = "sk-..."`), committed to the local repo |
| AI.V10.1 Independent input guardrail | Architecture review for an input policy layer ahead of the model | **FAIL** | No guardrail layer exists; the app calls the hosted LLM directly |
| AI.V12.2 Rate limiting on model endpoints | Drove 500 rapid requests at the `/ask` endpoint from one user | **FAIL** | No rate limiting; all 500 requests reached the provider (denial-of-wallet exposure) |
| AI.V13.1 Security-relevant events logged | Triggered an injection attempt and an error path, then inspected logs | **FAIL** | Only stdout `print()` debug lines exist; no durable security event log |

## Outcome

**Not yet conformant (L1).** The prototype meets several baseline essentials — input is structurally separated from instructions (AI.V6.1), sessions are isolated (AI.V6.3), and no secrets reach the model context or system prompt (AI.V3.1, AI.V6.8) — but it fails five L1 requirements, any one of which is disqualifying at the minimum baseline.

Must-fix gaps before this prototype is even L1-safe to expose to real users or data:

1. **Remove the hardcoded API key (AI.V3.2).** Pull the key out of `config.py`, rotate it (assume it is burned), and load it from an environment variable or secret store. This is the single most urgent item — a leaked provider key is direct denial-of-wallet and data-access risk.
2. **Add an independent input guardrail and injection detection (AI.V10.1, AI.V6.2).** Even a lightweight policy layer in front of the model that screens and logs injection payloads is required; today nothing sits between user input and the LLM.
3. **Enforce rate limiting on model-invoking endpoints (AI.V12.2).** Server-side per-user limits returning HTTP 429 to cap runaway cost and abuse.
4. **Record security-relevant events to a durable log (AI.V13.1).** Replace ad-hoc `print()` calls with structured logging of injection detections, errors, and request metadata so incidents can be reconstructed.

Until at least items 1–4 are closed, this prototype should remain off real user traffic and real document data, even for an internal pilot.
