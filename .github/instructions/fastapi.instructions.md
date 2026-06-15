---
name: 'FastAPI standards'
description: 'API layer conventions'
applyTo: '**/server.py'
---

# FastAPI conventions

- App in `src/server.py`; expose the agent over FastAPI + Uvicorn (`uvicorn src.server:app --reload`).
- Mount **AG-UI / DevUI** for the interactive UI.
- Health endpoint at `/health`. Stream agent responses where the UX benefits.
- Instrument with Application Insights (OpenTelemetry) — follow the `appinsights-instrumentation` skill.
- Validate request bodies with Pydantic models. Validate/authorize at the API boundary only.
- No secrets in code; read config from `config.py` (`pydantic-settings`).
