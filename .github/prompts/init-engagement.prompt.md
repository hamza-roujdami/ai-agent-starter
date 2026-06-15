---
description: 'Start a new engagement: interview, then write context.md, SPEC.md, and README.'
agent: architect
argument-hint: short description of the AI use case (optional)
---

Start discovery for this AI agent engagement.

If the user provided a use case, use it as the starting point: ${input:useCase:describe the AI use case}.

1. **Discover** — interview me with the askQuestion tool (use case & goal, users & channels, the
   end-to-end agentic workflow, data & knowledge sources, APIs, auth, access rules, success criteria,
   constraints). If Work IQ or the `agent-project-intake` skill is available, pull my customer
   meeting/email context first; otherwise ask me to paste notes.
2. **Design the agent** — debate the topology (single vs multi-agent vs workflow) against AGENTS.md
   Part 1 and apply the Anthropic _Building Effective Agents_ principles. Default single-agent; justify
   any escalation. Specify per-agent: role, system-prompt intent, model, tools, skills, KB, memory.
3. **Derive the Azure services from the design** — baseline (Foundry, ACA, ACR, Storage, Key Vault,
   App Insights/LAW) plus only the conditional services this design needs (e.g. AI Search ← RAG,
   Speech ← voice), each with a one-line justification. Produce a "Required Azure services + why" table.
4. **Diagram** — agent-internals + solution-architecture (showing exactly the derived services).
5. **Write** `docs/context.md`, `docs/SPEC.md` (topology decision, per-agent design, services table,
   interfaces, mock contract, out-of-scope, end-to-end verification step), and `README.md`
   (title, capabilities, both Mermaid diagrams, data flow, structure, quick start, curl, tech stack, evals).

Keep it public + simple (no VNet/Cosmos/APIM in the prototype). When the spec is approved, offer the
handoff to the implementer.
