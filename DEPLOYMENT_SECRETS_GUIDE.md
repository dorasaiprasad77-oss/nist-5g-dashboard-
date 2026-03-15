# GitHub Secrets Configuration for Azure Deployment

To enable the automated deployment workflow, you must add the following secrets to your GitHub repository:

1. Go to your repository on GitHub.
2. Navigate to **Settings** > **Secrets and variables** > **Actions**.
3. Add the following **New repository secrets**:

| Secret Name | Description | Example / Link |
|-------------|-------------|----------------|
| `AZURE_CREDENTIALS` | JSON output from Azure SP creation | [Create Service Principal](https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-portal%2Clinux) |
| `REGISTRY_LOGIN_SERVER` | Your Azure Container Registry login server | `uccregistry.azurecr.io` |
| `REGISTRY_USERNAME` | ACR Admin username | `uccregistry` |
| `REGISTRY_PASSWORD` | ACR Admin password | `••••••••` |
| `DATABASE_URL` | Production PostgreSQL connection string | `postgresql://admin:password@host:5432/db` |
| `JWT_SECRET` | A long, secure random string | `your-super-long-random-string` |

## How to get `AZURE_CREDENTIALS`
Run this in your terminal (with Azure CLI):
```bash
az ad sp create-for-rbac --name "nist-5g-ucc-sp" --role contributor --scopes /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP> --json-auth
```
Copy the entire JSON output and paste it into the `AZURE_CREDENTIALS` secret.

## How to enable ACR Admin User
1. Go to your ACR in Azure Portal.
2. Go to **Access keys**.
3. Enable the **Admin user** toggle.
4. Use the username and password provided there for the GitHub secrets.
