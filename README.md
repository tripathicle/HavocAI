# HavocAI CI/CD Pipeline

A highly modular, secure, and production-grade **Continuous Integration / Continuous Deployment (CI/CD)** system for the **HavocAI** platform, designed with best practices in DevOps, infrastructure as code, and automation. This repository enables consistent, reliable, and scalable deployment workflows across **Azure**, **AWS**, or **GCP**.

---

## 📌 Overview

The goal of this repository is to automate:
- Infrastructure provisioning
- Application deployment
- Environment management (Dev → Stage → Prod)
  
Built using:
- **Terraform** for IaC
- **GitHub Actions** / **Azure DevOps Pipelines**
- **Docker & Kubernetes** (optional)
- **Secrets Management** (Azure Key Vault / AWS Secrets Manager)

---

## ⚙️ Features

 Modular pipeline structure (YAML-based)  
 Multi-environment IaC setup (dev, staging, production)  
 Secure secrets handling  
 Linting, testing, and code quality gates  
 GitHub flow with PR-based deployment triggers  
 Rollbacks and release tracking  
 Multicloud support (Azure / AWS / GCP)

---
## 📁 Folder Structure

The repository is organized into different directories based on their functions:

```
HavocAI-CI-CD/
├── InfraPipeline/
│ ├── environments/
│ │ ├── dev/
│ │ ├── staging/
│ │ └── prod/
│ ├── modules/
│ └── .pipeline/
├── .github/workflows/
├── src/
├── manifests/
└── README.md
```
---

### 🔧 InfraPipeline/

Contains all files related to infrastructure provisioning, including Terraform configurations for creating and managing cloud resources, and pipeline YAML files for continuous integration and deployment.

---

## ⚙️ Setting Up CI/CD Pipeline

This repository provides a set of pipelines for different CI/CD tasks. These can be integrated with **Azure DevOps**, **GitHub Actions**, or other CI/CD platforms depending on your needs. Below is an example of setting up a pipeline using Azure DevOps:

### 1. Clone the Repository

```bash
git clone https://github.com/tripathicle/HavocAI-CI-CD.git
cd HavocAI-CI-CD
```
### 2. Configure Cloud Provider (Azure)
Ensure that you have set up a Service Principal for Azure DevOps to authenticate with your Azure subscription:

Azure: Ensure that you have set up a Service Principal for Azure DevOps to authenticate with your Azure subscription. You can create a service principal using the following Azure CLI command:
```
az ad sp create-for-rbac --name "devops-sp" --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group}
```
Save the client ID, tenant ID, and client secret for later use in your pipeline configuration.

#### 3. Set Up Azure DevOps Pipeline
```
3.1 Create a New Pipeline

1. Navigate to Azure DevOps → Pipelines.
2. Click Create Pipeline.
3. Select Azure Repos Git as the source.
4. Choose the repository containing this code.
5. Select YAML as the pipeline configuration format.
6. Choose the appropriate YAML file from the .pipeline/ directory.
```
➡️ This is a step-by-step setup guide for manually creating an Azure DevOps pipeline from the Azure DevOps UI. It's useful for someone who is new to Azure Pipelines and needs a walk-through on how to link the repo and select the pipeline file.


#### 3.2 Set Up GitHub Actions Pipeline
```
.github/workflows/deploy.yml: Executes on PR merge to main

Runs lint, tests, Terraform validation & deployment

Notifies via Slack / Teams on status

```

#### 3.3 Set Up Azure DevOps Pipeline (Alternative)
```
.pipeline/infra-pipeline.yml: Infra provisioning via Terraform

.pipeline/app-pipeline.yml: App deployment pipeline

```
---
### 4.Testing Strategy
```
| Type              | Tooling            | Stage     |
| ----------------- | ------------------ | --------- |
| Linting           | ESLint, tflint     | Pre-build |
| Unit Tests        | pytest / Jest      | Build     |
| Integration Tests | Postman / REST     | Deploy    |
| IaC Validation    | terraform validate | Build     |
```
---
### 5.Secrets Management
Use Azure Key Vault or AWS Secrets Manager and inject values via pipeline integrations.
Example (GitHub Secrets):
```
AZURE_CLIENT_ID
AZURE_TENANT_ID
AZURE_CLIENT_SECRET
```
---
### 6.Deployment Environments
Dev: Auto-deploy on feature branch merge
Staging: Manual or auto-deploy from release/* branches
Production: Protected branch deployment via PR + approvals

---
### 7.Toolchain
```
| Category              | Tools                                     |
| --------------------- | ----------------------------------------- |
| IaC                   | Terraform                                 |
| CI/CD                 | GitHub Actions / Azure Pipelines          |
| Cloud Providers       | Azure, AWS, GCP                           |
| Containers (optional) | Docker, Kubernetes, Helm                  |
| Monitoring (optional) | Prometheus, Grafana, Application Insights |
| Secrets Management    | Azure Key Vault, AWS Secrets Manager      |

```
---
### 8.Future Enhancements
Add Helm-based Kubernetes deployment support
Canary / blue-green deployments
Dynamic secrets rotation
Terraform remote backend with state locking

---
 ### Contributing
 We welcome contributions! If you have suggestions, bug fixes, or improvements for the pipeline, feel free to create an issue or submit a pull request.
How to Contribute

1.Fork the repository.

2.Create a new branch (```git checkout -b feature-branch```).

3.Make your changes.

4.Commit your changes (```git commit -am 'Add new feature'```).

5.Push to the branch (```git push origin feature-branch```).

6.Open a pull request.



