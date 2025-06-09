# 🚀 GitOps with ArgoCD on Kubernetes (AWS EC2)

A complete implementation of a GitOps workflow using **ArgoCD** on **Kubernetes (k3s)** running on an **AWS EC2 Ubuntu instance**.

---

## 📌 Table of Contents

- [✨ Features](#-features)
- [🏗 Architecture](#-architecture)
- [🛠 Prerequisites](#-prerequisites)
- [🚀 Setup Guide](#-setup-guide)
- [🖥 Usage](#-usage)
- [🔄 Testing GitOps](#-testing-gitops)
- [🐛 Troubleshooting](#-troubleshooting)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## ✨ Features

- **Git as Single Source of Truth** – All Kubernetes manifests stored in Git
- **Automated Synchronization** – ArgoCD auto-syncs changes from Git to cluster
- **Self-Healing** – Automatic drift correction
- **Declarative Infrastructure** – Everything defined as code
- **Easy Rollbacks** – Git history enables version control

---

## 🏗 Architecture

This setup leverages:

- Lightweight Kubernetes using **k3s**
- GitHub for version-controlled manifests
- **ArgoCD** for syncing Git changes to the cluster

---

## 🛠 Prerequisites

- AWS account with EC2 access
- Ubuntu 22.04 EC2 instance (recommended: t2.medium)
- GitHub account
- Basic knowledge of Kubernetes & Git

---

## 🚀 Setup Guide

### 1. Launch EC2 Instance

- Ubuntu 22.04 LTS, instance type: `t2.medium`
- Security groups must allow:
  - Port 22 (SSH)
  - Port 80 (HTTP)
  - Port 443 (HTTPS)
  - NodePort range: 30000–32767

### 2. Install Dependencies


ssh -i "your-key.pem" ubuntu@<EC2_PUBLIC_IP>

sudo apt update && sudo apt upgrade -y

sudo apt install -y docker.io git curl

### 3. Install k3s (Lightweight Kubernetes)

curl -sfL https://get.k3s.io | sh -

sudo kubectl get nodes 

### 4. Deploy ArgoCD

sudo kubectl create namespace argocd

sudo kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

### 5. Access ArgoCD UI

# Expose ArgoCD

sudo kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

# Get credentials

echo "Username: admin"

sudo kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

Access dashboard at: http://<EC2_PUBLIC_IP>

🖥 Usage

## Clone the Repository

git clone https://github.com/your-username/gitops-apps.git

cd gitops-apps

## Configure Application in ArgoCD UI

Application Name: nginx-app

Project: default

Repository URL: Your GitHub repo

Path: nginx-deployment/

Cluster: https://kubernetes.default.svc

Namespace: default

Sync Policy: Automatic

## Verify Deployment

sudo kubectl get pods

sudo kubectl get svc nginx-service

Access Nginx at: http://<NGINX_SERVICE_IP>

🔄 Testing GitOps

Make a change to the deployment (e.g., update Nginx version):

vim nginx-deployment/deployment.yaml

Commit and push the change:

git add .

git commit -m "Update nginx version"

git push origin main

ArgoCD will automatically sync the update to your cluster!

🐛 Troubleshooting

❌ ArgoCD Pods Not Starting

sudo kubectl get pods -n argocd

sudo kubectl describe pod <pod-name> -n argocd

sudo kubectl logs <pod-name> -n argocd

❌ Cannot Access ArgoCD UI

sudo kubectl get svc -n argocd

## Check if EXTERNAL-IP is assigned.

Contributions are welcome! Please follow these steps:

Fork the repository

Create your feature branch (git checkout -b feature/fooBar)

Commit your changes (git commit -am 'Add some fooBar')

Push to the branch (git push origin feature/fooBar)

Create a new Pull Request





