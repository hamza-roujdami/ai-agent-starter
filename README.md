# ai-agent-starter

Reusable **Layer A** starter for AI agent engagements. Clone it per customer use case and open it in
VS Code — GitHub Copilot is instantly configured with your stack, rules, agents, and slash commands.

> This is the **build-assistant configuration + project skeleton**. The actual customer agent
> (the deliverable) gets built into `src/`, `skills/`, etc. per engagement.

## Stage 1 — Assess & Design (your "plan mode")

For discovery and architecture, use the **`architect` agent** (via `/init-engagement` or the agent
dropdown) — it's your plan mode, specialized for these engagements: **read-only** (no code edits),
it interviews you, debates the agent topology (single vs multi-agent vs workflow), and produces
`docs/context.md`, `docs/SPEC.md`, and `README.md` with two diagrams (agent internals + solution
architecture). It follows **Anthropic's _Building Effective Agents_** design principles and the
topology decision in [AGENTS.md](AGENTS.md) Part 1 — start simplest, add complexity only when it pays.

## Prerequisites (set up once on your machine)

- **VS Code** + **GitHub Copilot** (agent mode). Models: any Copilot model (Claude recommended).
- **Azure Skills** installed (the `azure-prepare` → `azure-validate` → `azure-deploy` family, plus
  `microsoft-foundry`, `azure-rbac`, `azure-ai`, `appinsights-instrumentation`). See
  [Azure Skills](https://learn.microsoft.com/azure/developer/azure-skills/overview).
- **One global MCP setup** in your VS Code user `mcp.json` (`MCP: Open User Configuration`):
  **Azure MCP** + **Microsoft Foundry MCP** + **Bicep MCP** (Foundry/Bicep come from the AI Toolkit
  & Bicep extensions). Optional: **Work IQ MCP** (M365 meeting/email context for discovery).
- **Azure**: a subscription + `az login`; Foundry access for model deployments.
- *(Optional, recommended)* local clones the agents can consult for patterns — see *References* below.

## Use it

Use this repo as a **GitHub template** (or `git clone`) into a new folder per use case, then open it:

```bash
git clone <this-repo-url> my-usecase && cd my-usecase && code .
```

Then in Copilot chat:

1. `/init-engagement` — the **architect** agent interviews you and writes `docs/context.md`,
   `docs/SPEC.md`, and `README.md` (with Mermaid diagrams).
2. Switch to the **implementer** agent (or use the handoff) — builds the MAF agent, skills, FastAPI,
   mock backend, and tests in `src/`, `skills/`, `mock/`, `tests/`.
3. `/eval` — run tests + Foundry evaluation (pass/fail with evidence).
4. `/scaffold-infra` — `azure-prepare` → `azure-validate` → `azure-deploy` to Azure Container Apps.
5. Switch to the **reviewer** agent — OWASP + `DefaultAzureCredential` + least-privilege RBAC pass.

## What's in here (Layer A)

| Path | Purpose |
|---|---|
| `AGENTS.md` | Stack lock — read by Copilot every chat (portable, also read by Claude tools) |
| `.github/copilot-instructions.md` | Imports `AGENTS.md` + VS Code specifics |
| `.github/instructions/*.instructions.md` | Auto-applied rules: Python/MAF, Bicep/AVM, FastAPI, azure-prepare constraint |
| `.github/agents/*.agent.md` | `architect` → `implementer` → `reviewer` (with handoffs) |
| `.github/prompts/*.prompt.md` | `/init-engagement`, `/scaffold-infra`, `/eval` |
| `infra/ src/ skills/ mock/ kb/ tests/ docs/` | Project skeleton |

> MCP is **not** configured per repo. All MCP servers live in your single global
> user-level `mcp.json` (+ extension-contributed Foundry/Bicep). See *Prerequisites* above.

## What's committed vs generated

| Committed (the baseline you clone) | Generated per engagement (by the agents) |
|---|---|
| `AGENTS.md`, `README.md`, `.gitignore`, `.env.example` | `docs/context.md`, `docs/SPEC.md` (architect) |
| `.github/` instructions, agents, prompts | `src/*.py`, `pyproject.toml` (implementer) |
| Empty `src/ infra/ skills/ mock/ kb/ tests/ docs/` + READMEs | `infra/*.bicep` (azure-prepare) |
| | `skills/*/SKILL.md`, `mock/*`, `kb/*`, `tests/*` |
| | Local only (gitignored): `.venv/`, `.env`, `.azure/`, `references/` |

The baseline carries **config + empty skeleton**. Everything in `src/`, `infra/`, `skills/`, etc. is
written per use case — the folders ship with a README placeholder so the agents know what goes where.

## The fixed stack (the deliverable)

Self-hosted **MAF** (Python) → **FastAPI** + AG-UI/DevUI → **Azure Container Apps**, using
**Foundry** (models), **Storage**, **Key Vault**, **App Insights/Log Analytics**, **Container
Registry**, **Bicep (AVM)**, `DefaultAzureCredential` everywhere. **AI Search** only for RAG;
history is **FileHistoryProvider** (Cosmos is a productionization step). Public + simple, no VNet.
See [AGENTS.md](AGENTS.md).

## Relies on (global, set once on your machine)

- **One global MCP setup** — the VS Code user-level `mcp.json` (Azure MCP, Foundry MCP, Bicep MCP;
  optional Work IQ). No per-repo MCP files.
- **Azure Skills** (`azure-prepare`, `azure-validate`, `azure-deploy`, `microsoft-foundry`,
  `azure-rbac`, `azure-ai`, `appinsights-instrumentation`). The agents reference these by name.

## References (optional, recommended)

The agents consult these for real MAF patterns and the landing-zone reference. Clone them anywhere
and link into `references/` (gitignored), e.g.:

```bash
mkdir -p references
git clone https://github.com/microsoft/agent-framework references/agent-framework
# (optional) the GenAI app landing-zone bicep pattern, if you use it:
# git clone <ai-landing-zone-repo> references/bicep-ptn-aiml-landing-zone
cp .env.example .env   # then fill in, and run: az login
python3.13 -m venv .venv && source .venv/bin/activate
```

If `references/agent-framework` is absent, the agents still work — they just can't cite local samples.
