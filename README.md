# Production-Ready Amazon EKS Platform

This repository provides a **production-ready Amazon EKS platform** built with **Terraform, Kubernetes best practices, and GitHub Actions**. It is designed for real-world workloads with strong defaults for **security, scalability, observability, and multi-environment operations**.

---

## 🚀 What This Repository Is

* A **platform foundation**, not an app
* Designed for **dev / staging / prod** environments
* Secure-by-default Kubernetes on AWS
* CI/CD-driven infrastructure lifecycle
* Ready for GitOps adoption

This repo is suitable for:

* Platform engineering teams
* SaaS backends
* Internal developer platforms
* Regulated and enterprise workloads

---

## 🧱 Architecture Overview

**High-level components:**

* Amazon VPC (multi-AZ, private subnets)
* Amazon EKS (managed Kubernetes)
* Managed node groups (no public nodes)
* IAM Roles for Service Accounts (IRSA)
* Kubernetes platform add-ons
* GitHub Actions CI/CD

**Design principles:**

* Private by default
* Least privilege everywhere
* Everything defined as code
* Immutable infrastructure

---

## 📁 Repository Structure

```text
eks-platform/
├── .github/
│   └── workflows/
│       ├── terraform-plan.yml
│       ├── terraform-apply.yml
│       └── kubernetes-deploy.yml
├── terraform/
│   ├── modules/
│   │   ├── vpc/
│   │   ├── eks/
│   │   ├── iam/
│   │   └── addons/
│   ├── envs/
│   │   ├── dev/
│   │   ├── staging/
│   │   └── prod/
│   └── backend.tf
├── kubernetes/
│   ├── base/
│   │   ├── namespaces/
│   │   ├── rbac/
│   │   └── network-policies/
│   ├── addons/
│   │   ├── aws-load-balancer-controller/
│   │   ├── external-dns/
│   │   ├── cert-manager/
│   │   └── prometheus/
│   └── apps/
│       └── sample-app/
├── scripts/
│   ├── bootstrap.sh
│   └── destroy.sh
└── README.md
```

---

## 🛠️ Tooling & Versions

| Tool           | Purpose                |
| -------------- | ---------------------- |
| Terraform      | Infrastructure as Code |
| AWS EKS        | Managed Kubernetes     |
| GitHub Actions | CI/CD                  |
| Helm           | Kubernetes packaging   |
| kubectl        | Cluster management     |

**Recommended:**

* Terraform >= 1.6
* Kubernetes >= 1.28
* AWS CLI v2

---

## 🔐 Security Features

* Private EKS cluster endpoint
* Worker nodes in private subnets only
* IAM Roles for Service Accounts (IRSA)
* Encrypted Terraform remote state
* NetworkPolicies for pod isolation
* Pod Security Standards (baseline/restricted)
* Secrets stored outside Git (AWS Secrets Manager)

---

## 🌍 Environments

Each environment is isolated via:

* Separate Terraform state
* Independent node groups
* Configurable scaling

```text
terraform/envs/
├── dev/
├── staging/
└── prod/
```

Promotion happens through **Git pull requests**, not manual changes.

---

## 🔄 CI/CD Workflow

### Terraform Plan

* Runs on every pull request
* Shows infrastructure diff
* No changes applied

### Terraform Apply

* Runs on merge to `main`
* Protected by GitHub Environments
* Full audit trail

### Kubernetes Deploy

* Applies manifests / Helm charts
* Designed for GitOps or push-based models

---

## 📦 Platform Add-ons

Installed as part of the platform:

* AWS Load Balancer Controller
* External DNS
* Cert-Manager
* Cluster Autoscaler
* Prometheus & Grafana

Add-ons are **version-pinned and reproducible**.

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/eks-platform.git
cd eks-platform
```

### 2. Configure AWS Credentials

```bash
aws configure
```

Ensure the IAM user/role has permissions for:

* EKS
* EC2
* IAM
* S3
* DynamoDB

---

### 3. Boo
