---
name: 'Azure prepare/deploy constraints'
description: 'Constrains the Azure Skills to this engagement stack'
applyTo: '{infra/**,azure.yaml,Dockerfile,.azure/**}'
---

# Constraints for azure-prepare / azure-validate / azure-deploy

When using the Azure Skills to prepare or deploy this app, enforce the engagement stack —
do not accept the skill's generic defaults.

- **Hosting: Azure Container Apps only.** Never App Service, never Functions, never Foundry-hosted agents.
- The app is a **self-hosted MAF container** (FastAPI). Generate a `Dockerfile` for it.
- **Prototype is public + simple: no VNet, no private endpoints** — RBAC + managed identity only.
- Standard resources: **Foundry** (account/project/model), **Container Registry**, **Storage**,
  **Key Vault**, **Application Insights + Log Analytics**.
- Conditional: **Azure AI Search** — only when the use case needs RAG.
- **Not in the prototype:** Cosmos DB (history is FileHistoryProvider), APIM, App Gateway/WAF, Purview.
- **Managed identity** on the container app; **`DefaultAzureCredential`** in code.
- RBAC via Bicep, least privilege (`azure-rbac` skill).
- IaC = **Bicep with Azure Verified Modules**. `infra/` lives at repo root.
- Run order: `azure-prepare` (writes `.azure/plan.md`, infra, Dockerfile) →
  `azure-validate` (RBAC + what-if) → `azure-deploy` (`azd up`).
- Always pause for plan approval before provisioning.
