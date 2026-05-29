# Azure DevOps federated credential runbook

Configure workload identity federation so Azure Pipelines can mint a token the `deslicer` CLI accepts as `DESLICER_OIDC_TOKEN`.

## Steps

1. Create or select an Azure DevOps **service connection** with workload identity federation enabled.
2. In Azure Portal → App registrations → Federated credentials, add:
   - **Issuer:** `https://vstoken.dev.azure.com/<org-id>`
   - **Subject:** `sc://<org>/<project>/<service-connection-name>`
   - **Audience:** `https://api.deslicer.ai`
3. Register the issuer/subject pair in Observer (Plan 1b multi-issuer registry) if not already present.
4. Reference `azure/deslicer.yml` from your pipeline with `serviceConnection` and `environments` parameters.

## Verification

Run the install template alone, then `deslicer auth status` on an agent with OIDC configured.
