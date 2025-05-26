# vprofile-action

## 📎 Related Repositories

➡️ [iac-vprofile](https://github.com/shreyas4114/iac-vprofile): Terraform code for setting up the EKS infrastructure.

CI/CD pipeline for building, testing, analyzing, and deploying the `vProfile` microservices application to an AWS EKS cluster.

## 🚀 Overview

This repository automates the lifecycle of a multi-component microservices application (Java Maven app, MySQL, RabbitMQ, Memcache) using GitHub Actions. It covers:

- Code checkout and testing
- Static analysis with SonarQube
- Docker image build and push to Amazon ECR
- Kubernetes deployment via Helm on EKS

---

## ⚙️ Tech Stack

- **Java**, **Maven**
- **Docker**, **Amazon ECR**
- **AWS EKS**, **kubectl**, **Helm**
- **SonarQube** for code quality
- **GitHub Actions** for CI/CD

---

## 📁 Structure

<pre>
📁 <b>vprofile-action/</b>
├── src/
├── helm/
│   └── vprofilecharts/
│       └── (Helm chart files)
├── k8s/
│   └── (Kubernetes manifest files e.g., vproappdeploy.yml)
├── .github/
│   └── workflows/
│       └── main.yaml
├── Dockerfile
├── pom.xml
└── README.md
</pre>

---

## 🔄 GitHub Actions Workflow

The main workflow (`.github/workflows/main.yaml`) is triggered via **manual dispatch** and consists of three sequential jobs:

1. **Testing**
   - Runs unit tests with Maven
   - Performs static analysis via Checkstyle
   - Runs a SonarQube scan and checks the Quality Gate

2. **Build & Publish**
   - Builds a Docker image
   - Pushes it to Amazon ECR with `latest` and run-specific tags

3. **Deploy to EKS**
   - Configures AWS credentials and kubeconfig
   - Deploys the application using Helm with updated image tags

---

## 🔐 Required Secrets

To run this workflow, the following GitHub secrets must be configured:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `REGISTRY` (ECR registry URI)
- `SONAR_TOKEN`
- `SONAR_URL`
- `SONAR_ORGANIZATION`
- `SONAR_PROJECT_KEY`

---

## 🛠️ Helm Deployment

The Helm chart (`helm/vprofilecharts/`) is configured to pull the latest Docker image from ECR and deploy all services into the `default` namespace of your EKS cluster.

You can customize values using the `values:` input inside the workflow or by editing chart defaults.
