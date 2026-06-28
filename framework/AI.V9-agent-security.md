# AI.V9 — Autonomous Agent Security

**Objective:** constrain autonomous, multi-step, and multi-agent behavior so agents act
within bounded, attributable, recoverable authority.

## Requirements

| # | Requirement | L1 | L2 | L3 | Maps to |
|---|-------------|:--:|:--:|:--:|---------|
| AI.V9.1 | Verify that each agent has an explicitly defined goal and authority scope, enforced by the orchestrator, so the agent cannot pursue objectives or invoke capabilities outside that bounded scope. | ✓ | | | LLM06, ASI |
| AI.V9.2 | Verify that the orchestrator enforces hard limits on agent loops, recursion depth, iteration count, and total steps per task, independent of the model's own reasoning. | ✓ | | | LLM06, LLM10, ASI |
| AI.V9.3 | Verify that high-impact or irreversible agent actions require human-in-the-loop approval enforced outside the model, and that the agent cannot self-authorize or bypass the approval gate. | | ✓ | | LLM06, ASI, NIST |
| AI.V9.4 | Verify that agent memory and working state are isolated per session, user, and agent, with no cross-context leakage, demonstrated by test. | | ✓ | | LLM06, ASI, ISO |
| AI.V9.5 | Verify that agent planning is constrained and validated so that injected or retrieved content cannot redirect the agent's goal, scope, or authorized action set (links to AI.V6.7). | | ✓ | | LLM06, ATLAS |
| AI.V9.6 | Verify that inter-agent communication uses authenticated, attributable agent identities, so messages cannot be spoofed and every delegated action is traceable to its originating agent (links to AI.V2). | | ✓ | | ASI, ATLAS, NIST |
| AI.V9.7 | Verify that anomalous or rogue agent behavior is detected and that an emergency stop / kill-switch can immediately halt an agent or fleet, enforced outside the model. | | | ✓ | LLM06, ASI, NIST |
| AI.V9.8 | Verify that agent actions are reversible or compensatable, or that the orchestrator requires explicit confirmation and records a recovery path when they are not. | | | ✓ | LLM06, ASI, ISO |

> A ✓ marks the lowest level at which the requirement first applies; it remains
> required at all higher levels.

## Verification guidance

**AI.V9.1** — Locate where each agent's goal and authority scope are declared and
enforced. Confirm the binding is held by the orchestrator, not the prompt: attempt to
make an agent invoke a capability or pursue an objective outside its scope (expect
orchestrator-level denial, not merely model refusal). High-impact actions inside scope
remain gated per AI.V8.5.

**AI.V9.2** — Drive an agent into a non-terminating or self-referential task and confirm
the orchestrator terminates it at the configured loop/recursion/step ceiling. Verify the
limits are configured outside the model and cannot be raised by model output (links to
AI.V12.5 for budget enforcement).

**AI.V9.3** — Enumerate the irreversible / high-impact action inventory. For each,
confirm a human approval gate exists outside the model and that the agent cannot
fabricate, replay, or skip the approval (e.g., by emitting a fake "approved" token).

**AI.V9.4** — Run two concurrent sessions/users and probe whether one agent can read
another's memory, scratchpad, or retrieved context. Confirm isolation boundaries hold
under multi-agent delegation and that shared memory stores are partitioned by
session/user/agent.

**AI.V9.5** — Inject adversarial instructions via tool output, retrieved documents, or a
peer agent's message and confirm the agent's plan, goal, and authorized action set are
unchanged. Verify plans are validated against the declared scope before execution (links
to AI.V6.7 instruction hierarchy).

**AI.V9.6** — Inspect the inter-agent transport: each agent presents a non-shared,
verifiable identity, messages are authenticated, and a spoofed sender is rejected.
Confirm delegated actions are attributable end-to-end to the originating agent
(links to AI.V2 identity).

**AI.V9.7** — Confirm behavioral monitoring exists for anomalous agent activity (action
spikes, scope drift, repeated denied attempts). Exercise the kill-switch and verify a
running agent or fleet halts promptly and that the stop cannot be overridden by model
output.

**AI.V9.8** — For each agent action class, confirm a reversal or compensating action
exists, or that the orchestrator forces confirmation and persists a recovery path
(undo, saga/compensation, or rollback record) before committing.

## Related domains

- **AI.V8 MCP & Tool Security** — agents are the primary tool callers; per-action tool
  authority and high-impact gating (AI.V8.5) are enforced there.
- **AI.V12 Tokens, Cost & Rate Limiting** — the budget/step-limit substrate behind
  AI.V9.2 loop and iteration ceilings.
- **AI.V2 Identity & Authentication** — issues the attributable agent identities required
  for AI.V9.6 inter-agent communication.
- **AI.V6 Prompt Security** — the instruction-hierarchy and indirect-injection defenses
  (AI.V6.6/AI.V6.7) that AI.V9.5 relies on to keep agent goals stable.
