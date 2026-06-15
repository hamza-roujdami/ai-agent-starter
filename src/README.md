# Source

The MAF agent runtime (the deliverable) lives here:

- `agent.py` — agent definition: system prompt, tools, SkillsProvider, HistoryProvider, Foundry model
- `config.py` — pydantic-settings config (reads `.env`)
- `server.py` — FastAPI app + AG-UI/DevUI

Run locally: `uvicorn src.server:app --reload`
