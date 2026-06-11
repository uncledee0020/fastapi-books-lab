## Cleanup & Cost Optimization

### Infrastructure Teardown
To permanently delete all provisioned resources for this lab and stop ongoing charges, run the following Azure CLI command in your terminal:

```bash
az group delete --name AzureDevelopers-MoringaSchool --yes --no-wait
```

### Cost Estimation Table
Below is the estimated monthly cost profile for this API architecture under active development vs. optimization:

| Resource Component | Azure Tier / SKU | Est. Monthly Cost (Active) | Cost Optimization Action | Optimized Est. Cost |
| :--- | :--- | :--- | :--- | :--- |
| **API Management (APIM)** | Developer Tier | ~$48.00 / month | Scale to Consumption Tier for production | Pay-per-use ($0.00 base) |
| **Azure App Service** | Premium V3 (P1v3) | ~$120.00 / month | Downgrade to B1 (Basic) or F1 (Free) for labs | $0.00 - $13.00 / month |
| **Azure Container Registry** | Standard | ~$20.00 / month | Clear old untagged images via retention policies | ~$5.00 / month |
| **Application Insights** | Pay-as-you-go | Data volume dependent | Restrict ingestion sampling rate to 10% in prod | Minimal / Free tier limits |

### Cost-Saving Tips for Lab Environments
1. **Apply Auto-Shutdown Rules:** Configure your App Service or environment VMs to automatically stop outside of core lab hours (e.g., 6:00 PM).
2. **Aggressive Sampling:** Lower your APIM Application Insights diagnostics sampling parameter from 100% down to 10% or 20% once testing concludes to lower data ingestion volume bills.
3. **Purge Container Layers:** Periodically run `az acr repository untagged-list` and purge orphaned Docker build tags to save on underlying block storage space.
