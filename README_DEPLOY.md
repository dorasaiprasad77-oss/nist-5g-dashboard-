# Azure Deployment Guide: UCC Dashboard

This project is containerized and ready for deployment to **Azure App Service for Containers**.

> [!IMPORTANT]
> To automate this deployment using GitHub Actions, please follow the [DEPLOYMENT_SECRETS_GUIDE.md](file:///c:/Users/doras/OneDrive/Desktop/nist%205g_private%20network%20dashbord/DEPLOYMENT_SECRETS_GUIDE.md).

## Prerequisites
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) installed.
- [Docker](https://www.docker.com/products/docker-desktop/) installed locally.

## Step 1: Login to Azure
```bash
az login
```

## Step 2: Create a Resource Group
```bash
az group create --name nist-5g-ucc-rg --location eastus
```

## Step 3: Create an Azure Container Registry (ACR)
```bash
az acr create --resource-group nist-5g-ucc-rg --name uccregistry --sku Basic
az acr login --name uccregistry
```

## Step 4: Build and Push Docker Images
```bash
# Backend
docker build -t uccregistry.azurecr.io/ucc-backend:v1 ./backend
docker push uccregistry.azurecr.io/ucc-backend:v1

# Frontend
docker build -t uccregistry.azurecr.io/ucc-frontend:v1 ./nist-5g-dashboard
docker push uccregistry.azurecr.io/ucc-frontend:v1
```

## Step 5: Deploy to Azure App Service
1. In the Azure Portal, create a **Web App for Containers**.
2. Select the images pushed to ACR.
3. Configure Environment Variables:
   - `DATABASE_URL`: Your Azure PostgreSQL connection string.
   - `JWT_SECRET`: A strong secret key.
   - `NEXT_PUBLIC_API_URL`: The URL of your deployed backend.

## Step 6: Verify
Navigate to your App Service URL to access the live UCC Dashboard.
