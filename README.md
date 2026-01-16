# Kubernetes DevSecOps Pipeline on Azure AKS

End-to-end DevSecOps pipeline that deploys a hardened Kubernetes workload to Azure AKS with automated security scanning and enforcement using GitHub Actions and Trivy.

---

## 🚀 Project Overview

This project demonstrates how to securely deploy an application to **Azure Kubernetes Service (AKS)** using **DevSecOps best practices**.

The pipeline scans Kubernetes manifests for security misconfigurations, enforces security gates, and deploys only hardened workloads to AKS.

The focus is on **real-world security**, not toy examples.

---

## 🏗 Architecture Overview

Pipeline flow:

1. Code is pushed to GitHub  
2. GitHub Actions pipeline is triggered  
3. Trivy scans Kubernetes manifests for security issues  
4. Pipeline fails if security policies are violated  
5. Secure manifests are deployed to Azure AKS  

---

## 🧰 Tech Stack

- Azure Kubernetes Service (AKS)
- GitHub Actions (CI/CD)
- Kubernetes (RBAC, NetworkPolicies, SecurityContexts)
- Trivy (IaC & Kubernetes security scanning)
- Azure AD Service Principal authentication
- Linux containers (non-root, hardened runtime)

---

## 🔐 Security Controls Implemented

- Non-root containers (`runAsNonRoot`)
- Read-only root filesystem
- Dropped all Linux capabilities
- Seccomp profile (`RuntimeDefault`)
- Dedicated ServiceAccount per workload
- Least-privilege RBAC roles
- Namespace isolation
- Default-deny NetworkPolicy
- Explicit allow-only HTTP traffic
- No privileged containers

---

## 🔄 CI/CD Pipeline Details

The GitHub Actions pipeline performs:

- Trivy configuration scanning on Kubernetes manifests
- Security gate enforcement (fails on HIGH/CRITICAL issues)
- Secure authentication to Azure
- Namespace creation if missing
- Ordered deployment of hardened Kubernetes resources
- Deployment to Azure AKS


---

## ▶️ How to Run Locally

```bash
kubectl create namespace secure-app
kubectl apply -f secure/
kubectl get pods -n secure-app
