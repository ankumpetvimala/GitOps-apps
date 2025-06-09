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

```bash
ssh -i "your-key.pem" ubuntu@<EC2_PUBLIC_IP>
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io git curl

