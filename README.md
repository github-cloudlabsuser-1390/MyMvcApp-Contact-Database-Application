# MyMvcApp - Contact Database Application

MyMvcApp is a simple CRUD application built with ASP.NET Core MVC that allows users to manage contact information. This guide provides instructions for deploying the application to Azure using an ARM template and setting up a GitHub Actions pipeline for CI/CD.

---

## Table of Contents
1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Deploying to Azure with ARM Template](#deploying-to-azure-with-arm-template)
4. [Setting Up GitHub Actions for CI/CD](#setting-up-github-actions-for-cicd)
5. [Folder Structure](#folder-structure)
6. [License](#license)

---

## Features
- Create, Read, Update, and Delete (CRUD) operations for managing user contacts.
- Search functionality to filter users by name.
- Built-in validation for user input.

---

## Prerequisites
Before deploying or setting up CI/CD, ensure you have the following:
1. **Azure Account**: Create an account at [Azure Portal](https://portal.azure.com/).
2. **Azure CLI**: Install the Azure CLI from [here](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
3. **GitHub Repository**: Push your project to a GitHub repository.
4. **Dotnet SDK**: Install the .NET SDK from [here](https://dotnet.microsoft.com/download).

---

## Deploying to Azure with ARM Template

### Step 1: Create a Resource Group
Run the following command to create a resource group:
```bash
az group create --name MyMvcAppResourceGroup --location eastus