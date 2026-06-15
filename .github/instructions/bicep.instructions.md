---
name: 'Bicep / AVM standards'
description: 'Infrastructure-as-code conventions for the infra/ folder'
applyTo: 'infra/**'
---

# Bicep & infrastructure conventions

- **Azure Verified Modules (AVM)** first. Resolve modules via the Bicep MCP `get_azure_verified_module`.
- `targetScope = 'resourceGroup'`. Deterministic naming:
  `resourceToken = toLower(uniqueString(subscription().id, environmentName, location))`.
- Parameters in `main.bicepparam`. Modules under `infra/modules/`.
- **No secrets in Bicep or params.** Use Key Vault references and managed identity.
- RBAC role assignments in Bicep with **least privilege** (use the `azure-rbac` skill to pick roles).

## Standard modules for this stack (self-hosted MAF on ACA, public + simple)

- `ai-foundry.bicep` — Foundry account + project + model deployment
- `container-apps.bicep` — ACA environment + the agent container app (managed identity enabled)
- `container-registry.bicep` — Azure Container Registry (image source for ACA)
- `storage.bicep` — Storage account (Foundry dependency + `app/kb/` staging)
- `key-vault.bicep` — Key Vault
- `monitoring.bicep` — Log Analytics + Application Insights
- `rbac.bicep` — role assignments for the container app's managed identity
- `search.bicep` — Azure AI Search **(only when the use case needs RAG)**

**Prototype is public + simple:** no VNet, no private endpoints, RBAC + managed identity.
**Not in the prototype:** Cosmos DB (history is FileHistoryProvider; Cosmos is a productionization
step), APIM, App Gateway/WAF, Purview. See [AGENTS.md](../../AGENTS.md) Part 2.

## Reference

- AI Landing Zone pattern: `references/bicep-ptn-aiml-landing-zone/`.
- Prefer the `azure-prepare` skill to scaffold infra, constrained to this topology
  (see `azure-prepare.instructions.md`).
