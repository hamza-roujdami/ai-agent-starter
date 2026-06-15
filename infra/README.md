# Infrastructure

Bicep (Azure Verified Modules) for the self-hosted MAF agent on Azure Container Apps.

```
infra/
  main.bicep
  main.bicepparam
  modules/
    ai-foundry.bicep        # Foundry account + project + model deployment
    container-apps.bicep     # ACA environment + agent container app (managed identity)
    container-registry.bicep # Azure Container Registry (image source)
    storage.bicep            # Storage account (Foundry dependency + kb/ staging)
    key-vault.bicep          # Key Vault
    monitoring.bicep         # Log Analytics + Application Insights
    rbac.bicep               # least-privilege role assignments
    search.bicep             # Azure AI Search (only when the use case needs RAG)
```

Prototype is **public + simple** (no VNet, RBAC + managed identity). Cosmos DB, APIM, WAF, and
private networking are productionization steps — not in the prototype. See [AGENTS.md](../AGENTS.md) Part 2.

Generated/maintained via the `azure-prepare` skill (see `.github/instructions/azure-prepare.instructions.md`).
