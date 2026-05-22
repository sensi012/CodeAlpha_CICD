# ☁️ CodeAlpha DevOps Internship — Task 1: CI/CD Pipeline using Azure

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Azure Pipelines](https://img.shields.io/badge/Azure_Pipelines-2560E0?style=for-the-badge&logo=azure-pipelines&logoColor=white)
![CodeAlpha](https://img.shields.io/badge/Internship-CodeAlpha-blue?style=for-the-badge)

---

## 📌 Project Overview

This project demonstrates a fully automated **CI/CD (Continuous Integration / Continuous Deployment) pipeline** built on **Microsoft Azure**. Every time code is pushed to GitHub, the pipeline automatically builds a Docker image, stores it in Azure Container Registry, and deploys it to Azure App Service — with zero manual steps.

> **Internship:** CodeAlpha DevOps Internship  
> **Task:** Task 1 — CI/CD Pipeline using Azure  
> **Intern:** [Your Name]  
> **Duration:** [Start Date] – [End Date]

---

## 🧠 What I Learned

- What CI/CD is and why it matters in modern software development
- Building automated pipelines with **Azure Pipelines**
- Storing Docker images in **Azure Container Registry (ACR)**
- Deploying web applications to **Azure App Service**
- Writing YAML pipeline configuration files
- Monitoring pipeline runs and troubleshooting failures
- Connecting GitHub to Azure DevOps for automated triggers

---

## 🏗️ Architecture Overview

```
Developer pushes code
        │
        ▼
  GitHub Repository
        │
        ▼ (triggers automatically)
  Azure Pipelines
        │
        ├── Step 1: Build Docker Image
        │
        ├── Step 2: Push to Azure Container Registry
        │
        └── Step 3: Deploy to Azure App Service
                        │
                        ▼
              Live Web Application 🌐
```

---

## 🛠️ Technologies Used

| Tool | Purpose |
|------|---------|
| Azure Pipelines | CI/CD automation |
| Azure Container Registry | Docker image storage |
| Azure App Service | Web app hosting (deployment target) |
| Docker | Application containerization |
| Python + Flask | Sample web application |
| GitHub | Source code repository |

---

## 📁 Project Structure

```
CodeAlpha_CICD/
├── app.py                        # Flask web application
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Container build instructions
├── azure-pipelines.yml           # Azure CI/CD pipeline definition
└── README.md                     # Project documentation
```

---

## ⚙️ Prerequisites

- [Microsoft Azure Account](https://azure.microsoft.com/free) (free tier works)
- [Azure DevOps Account](https://dev.azure.com) (free)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [GitHub Account](https://github.com)
- Python 3.9+

---

## 🚀 How to Set This Up

### Step 1 — Clone the Repository
```bash
git clone https://github.com/YOURUSERNAME/CodeAlpha_CICD.git
cd CodeAlpha_CICD
```

### Step 2 — Run Locally (Optional Test)
```bash
pip install -r requirements.txt
python app.py
```
Visit `http://localhost:5000` to confirm the app works.

### Step 3 — Build & Run with Docker Locally
```bash
docker build -t codealpha-cicd-app .
docker run -p 5000:5000 codealpha-cicd-app
```

### Step 4 — Set Up Azure Resources

**Create Azure Container Registry:**
```bash
az group create --name codealpha-rg --location eastus
az acr create --resource-group codealpha-rg --name codealphaACR --sku Basic
```

**Create Azure App Service:**
```bash
az appservice plan create --name codealpha-plan --resource-group codealpha-rg --sku B1 --is-linux
az webapp create --resource-group codealpha-rg --plan codealpha-plan --name codealpha-webapp-[yourname] --deployment-container-image-name nginx
```

### Step 5 — Connect Azure DevOps to GitHub
1. Go to [https://dev.azure.com](https://dev.azure.com)
2. Create a new project
3. Go to **Pipelines** → **New Pipeline**
4. Select **GitHub** → choose this repository
5. Select **Existing Azure Pipelines YAML file**
6. Choose `azure-pipelines.yml`
7. Click **Run**

---

## 📄 Pipeline Configuration (azure-pipelines.yml)

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  acrName: 'YOUR_ACR_NAME.azurecr.io'
  imageName: 'codealpha-app'

steps:
  - task: Docker@2
    displayName: 'Build Docker Image'
    inputs:
      command: build
      dockerfile: '**/Dockerfile'
      tags: '$(Build.BuildId)'

  - task: Docker@2
    displayName: 'Push to Azure Container Registry'
    inputs:
      command: push
      containerRegistry: 'your-acr-service-connection'
      repository: '$(imageName)'
      tags: '$(Build.BuildId)'

  - task: AzureWebAppContainer@1
    displayName: 'Deploy to Azure App Service'
    inputs:
      azureSubscription: 'your-subscription'
      appName: 'codealpha-webapp-[yourname]'
      containers: '$(acrName)/$(imageName):$(Build.BuildId)'
```

---

## 🔍 Pipeline Stages Explained

| Stage | What Happens |
|-------|-------------|
| **Trigger** | Pipeline starts automatically when code is pushed to `main` branch |
| **Build** | Docker image is built from the `Dockerfile` |
| **Push** | Image is pushed to Azure Container Registry for storage |
| **Deploy** | App Service pulls the new image and goes live automatically |

---

## 📸 Project Screenshots

> *(Add screenshots of your Azure Pipeline, successful build, and live app URL here)*

---

## 🌐 Live App

> App URL: `https://codealpha-webapp-[AdepegbaIsaiah].azurewebsites.net`

---

## 💡 Key Concepts Demonstrated

- **Continuous Integration:** Every code push triggers an automated build and test cycle
- **Continuous Deployment:** Successful builds are automatically deployed — no manual steps
- **Infrastructure as Code:** The entire pipeline is defined in a YAML file stored in Git
- **Container Registry:** A private, secure storage for Docker images in the cloud
- **Zero-Downtime Deployment:** Azure App Service swaps to the new container without interruption

---

## 🔗 Resources

- [Azure Pipelines Documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/)
- [Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/)
- [Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/)
- [CodeAlpha Website](https://www.codealpha.tech)

---

## 👤 Author

**[Adepegba Isaiah Ayooluwa]**  
DevOps Intern @ CodeAlpha  
🔗 [LinkedIn Profile](https://www.linkedin.com/in/isaiah-adepegba)  
🐙 [GitHub Profile](https://github.com/sens012)

---

*This project was completed as part of the CodeAlpha DevOps Internship Program.*
