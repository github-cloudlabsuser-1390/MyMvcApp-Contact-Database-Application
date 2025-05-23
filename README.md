# MyMvcApp-Contact-Database-Application

## Overview
This is an ASP.NET Core MVC CRUD application for managing user contacts. It demonstrates basic CRUD operations (Create, Read, Update, Delete) and search functionality, all managed in-memory for demonstration purposes.

## Features
- List all users
- View user details
- Create new users
- Edit existing users
- Delete users
- Search users by name or email

## Project Structure
- `Controllers/` — Contains MVC controllers (e.g., `UserController.cs`)
- `Models/` — Contains data models (e.g., `User.cs`)
- `Views/` — Contains Razor views for each controller action
- `wwwroot/` — Static files (CSS, JS, etc.)
- `deploy.json` — ARM template for Azure deployment
- `deploy.parameters.json` — Parameters for ARM template
- `.github/workflows/azure-webapps.yml` — GitHub Actions workflow for CI/CD

## Deploying to Azure with ARM Template

1. **Edit Parameters (Optional):**
   - Update `deploy.parameters.json` to set your desired web app name, location, and SKU.

2. **Deploy via Azure CLI:**
   - Log in to Azure:
     ```powershell
     az login
     ```
   - Deploy the ARM template:
     ```powershell
     az deployment group create --resource-group <YourResourceGroup> --template-file deploy.json --parameters @deploy.parameters.json
     ```
   - Example resource group: `GitHub-Copilot-Challenges`

3. **Result:**
   - An Azure App Service plan and Web App will be created. The web app URL will be output after deployment.

## Setting Up GitHub Actions for CI/CD

1. **Create Azure Service Principal:**
   - Get your subscription ID:
     ```powershell
     az account show --query id --output tsv
     ```
   - Create the service principal (replace `<SUBSCRIPTION_ID>`):
     ```powershell
     az ad sp create-for-rbac --name "github-actions-deploy" --role contributor --scopes /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/GitHub-Copilot-Challenges --sdk-auth
     ```
   - Copy the JSON output.

2. **Add GitHub Secret:**
   - Go to your GitHub repository > Settings > Secrets and variables > Actions > New repository secret.
   - Name: `AZURE_CREDENTIALS`
   - Value: Paste the JSON output from the previous step.

3. **Workflow File:**
   - The workflow is defined in `.github/workflows/azure-webapps.yml`.
   - It builds the app, publishes to the correct output path, uploads the artifact, logs in to Azure, and deploys to your Azure Web App.

4. **Triggering the Workflow:**
   - Push to the `master` branch or use the Actions tab to manually trigger the workflow.

## Notes
- The build and publish output path is set to:
  ```
  D:\a\MyMvcApp-Contact-Database-Application\MyMvcApp-Contact-Databse-Application\bin\Release\net8.0\MyMvcApp
  ```
- Ensure your Azure Web App name in `deploy.parameters.json` matches the one in your workflow file.
- The app uses in-memory storage for demonstration. For production, integrate with a database.

## Useful Links
- [Azure ARM Templates Documentation](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview)
- [GitHub Actions for Azure](https://github.com/Azure/actions)
- [ASP.NET Core MVC Documentation](https://docs.microsoft.com/aspnet/core/mvc/overview)

---

**This guide was generated with GitHub Copilot.**
