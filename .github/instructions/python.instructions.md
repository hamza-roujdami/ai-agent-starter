---
name: 'Python / MAF standards'
description: 'Python and Microsoft Agent Framework conventions'
applyTo: '**/*.py'
---

# Python & MAF conventions

- Python 3.13, dependencies in `pyproject.toml` (no `setup.py`). Lint/format with **Ruff**.
- **Always use a virtual environment.** Create/activate `.venv` at the repo root before installing
  or running anything (`python3.13 -m venv .venv && source .venv/bin/activate`). Never install into
  the system Python. `.venv/` is gitignored.
- **Async by default** for I/O. Type hints on all function signatures.
- Config via **`pydantic-settings`** in `config.py` reading `.env`. Never read env vars ad hoc.
- Auth: **`DefaultAzureCredential`** everywhere. Never hardcode keys/endpoints/connection strings.

## Microsoft Agent Framework

- Build the agent in `app/src/agent.py`; system prompts as module-level constants.
- **Skills-based**: one folder per skill under `app/skills/<name>/SKILL.md`, loaded via `SkillsProvider`.
- **KB-first**: search the knowledge base (`app/kb/`) before escalating or taking an action.
- Use `HistoryProvider` for memory (FileHistoryProvider in the prototype).
- Use `MCPStreamableHTTPTool` for external systems via MCP.
- Models via **Foundry** model deployments (`FoundryChatClient`), not direct OpenAI endpoints.
- **Observability**: wire **OpenTelemetry** tracing (App Insights) — trace agent runs, tool calls, model calls.
- Reference patterns from `references/agent-framework/python/samples/`.

## Supporting Azure services

- Telemetry: follow the `appinsights-instrumentation` skill — instrument the FastAPI app and agent.
- AI Search: follow the `azure-ai` skill for vector/hybrid index setup (only when the use case needs RAG).
- History is **FileHistoryProvider** in the prototype. The `cosmosdb-best-practices` skill applies only
  at productionization (CosmosHistoryProvider) — do not provision Cosmos for the prototype.

## Tests

- Every feature ships with tests in `app/tests/`. Provide an eval entry point (`app/tests/test_eval.py`).
- Do not mark work done until tests pass — show the output as evidence.
