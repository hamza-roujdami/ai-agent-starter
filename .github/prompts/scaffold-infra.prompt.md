---
description: 'Scaffold infra/ (Bicep AVM) and deploy to Azure Container Apps using the Azure Skills.'
agent: implementer
---

Prepare and deploy this app to Azure, constrained to the engagement stack.

Follow `.github/instructions/azure-prepare.instructions.md` strictly:

1. Use the **azure-prepare** skill to generate `infra/` (Bicep with Azure Verified Modules via the
   Bicep MCP), a `Dockerfile` for the self-hosted MAF container, and `.azure/plan.md`.
   Target **Azure Container Apps** with managed identity. Provision/connect Foundry (account/project/
   model), Container Registry, Storage, Key Vault, and Application Insights + Log Analytics.
   Add Azure AI Search only if the use case needs RAG. No Cosmos/VNet in the prototype.
2. Pause and show me the plan for approval.
3. Use the **azure-validate** skill (config, RBAC, managed-identity permissions, what-if).
4. Use the **azure-deploy** skill (`azd up`) once validation passes.

Never use App Service, Functions, or Foundry-hosted agents. No secrets in IaC.
