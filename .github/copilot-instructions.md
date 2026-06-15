# Copilot instructions

Read and follow [AGENTS.md](../AGENTS.md) — it locks the tech stack and workflow for this engagement.

## VS Code specifics

- Prefer the **Azure Skills** for infra and deployment: `azure-prepare` → `azure-validate` → `azure-deploy`.
- Use the **Azure MCP** and **Microsoft Foundry MCP** for live Azure/Foundry operations.
- Use the **Bicep MCP** (`get_azure_verified_module`) so `infra/` uses Azure Verified Modules.
- Custom agents for this repo: `architect`, `implementer`, `reviewer` (see `.github/agents/`).
- Slash commands: `/init-engagement`, `/scaffold-infra`, `/eval` (see `.github/prompts/`).

## Hard rules

- Self-hosted MAF on Azure Container Apps. Do **not** scaffold Foundry-hosted agents or App Service.
- `DefaultAzureCredential` only — never hardcode keys or connection strings.
- Secrets come from Key Vault / `.env` (never committed). Validate input at system boundaries.
- Keep `AGENTS.md` and instruction files short; put multi-step workflows in skills, not here.
