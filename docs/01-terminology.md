# Terminology

Working definitions for AI-SAF. These will be reconciled with the OWASP AI Exchange
glossary before v0.5.

- **AI application** — a software system that uses one or more AI models to deliver
  functionality to users or other systems. The unit of assessment.
- **Model** — the trained artifact performing inference (LLM, multimodal, classifier).
- **Prompt** — input assembled and sent to a model, including system, developer, user,
  and retrieved/tool content.
- **System prompt** — privileged instructions set by the application operator.
- **Prompt injection** — adversarial input that subverts intended instructions.
  *Direct*: from the user. *Indirect*: from content the model ingests (web, RAG, tools).
- **Guardrail** — a control, independent of the model, that inspects inputs and/or
  outputs and enforces policy.
- **LLM firewall / AI gateway** — a network-positioned guardrail between clients and
  the model.
- **RAG** — Retrieval-Augmented Generation; injecting retrieved documents into context.
- **Tool** — an external capability the model can invoke (function, API, MCP server).
- **MCP** — Model Context Protocol; a standard interface for exposing tools/data to AI.
- **Agent** — an LLM combined with planning logic, memory, and tool access that can
  take multi-step actions.
- **Context / memory** — state carried across turns or sessions.
- **Assurance level (L1/L2/L3)** — the depth of verification a requirement demands.
- **Verification** — producing pass/fail evidence that a requirement is met.
