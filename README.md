# Module 6 Assignment — Premium 3-Tier Infrastructure (IaC, CI/CD, Monitoring)

This repository contains the complete implementation for the **DevOps Module 6 Assignment**. The project recreates a manually-deployed 3-tier application architecture using **Terraform (Infrastructure as Code)**, automates deployments using **GitHub Actions (CI/CD)**, and integrates full telemetry visualization using **Prometheus & Grafana**.

---

## ✨ Features

- 🏗️ **Modular Terraform IaC**: Secure custom VPC with 6 subnets across multiple Availability Zones, Bastion SSH Gateway, public Application Load Balancer (ALB), and a private RDS PostgreSQL Database.
- 🔄 **Training IAM Compatibility**: Designed specifically for restricted training credentials, avoiding Secrets Manager and custom IAM policy creations in favor of direct variable injections.
- 🚀 **GitHub-Hosted CI/CD**: Fully automated delivery pipeline (`runs-on: ubuntu-latest`) deploying frontend React apps to Nginx and backend Node.js APIs to PM2, running SQL schema migrations and automated health checks on every push.
- 📊 **Dynamic Monitoring Stack**: Preloaded configurations for Prometheus and Grafana, collecting exporter details (Node, PostgreSQL, Nginx, API Business metrics) and mapping them onto interactive Grafana charts.
- 🖥️ **Premium Direct Access**: Routing is managed through direct HTTP Load Balancer DNS or public IPs without the need for Route53 domain locks or SSL configurations.

---

## 📂 Repository Structure

```
mahmud_assignment_6/
├── .github/
│   └── workflows/
│       └── deploy.yml              # CI/CD pipeline using ubuntu-latest and SSH ProxyJump
├── src/
│   ├── frontend/                   # React Vite application
│   ├── backend/                    # Express Node.js application
│   └── database/                   # PostgreSQL schema and migrations
├── terraform/
│   ├── modules/
│   │   ├── vpc/                    # Subnets, route tables, IGW, NAT GW
│   │   ├── security-groups/        # Security groups for Bastion, ALB, Frontend, Backend, RDS
│   │   ├── rds/                    # RDS PostgreSQL engine configuration
│   │   ├── alb/                    # Public ALB (HTTP port 80, path-based routing)
│   │   └── ec2/                    # EC2 module referencing existing SSH key pairs
│   └── environments/
│       └── prod/
│           ├── main.tf             # Composition orchestrator
│           ├── variables.tf        # Input variable definitions
│           ├── outputs.tf          # Output IP/DNS addresses
│           └── terraform.tfvars    # Environment configurations (Default ap-south-1)
├── monitoring/
│   ├── prometheus/                 # Prometheus scrape configs
│   ├── grafana/                    # Grafana dashboards and telemetry
│   └── scripts/
│       ├── setup-monitoring.sh     # Setup script for telemetry stack server
│       └── setup-exporters.sh      # Setup script for application exporters
├── DEPLOYMENT_GUIDE.md             # Complete step-by-step master setup manual
└── README.md                       # High-level architecture overview
```

---

## ⚡ Quick Start

1. **Configure AWS Credentials**: Make sure your local terminal has access to your training account (`aws configure`).
2. **Deploy the Infrastructure**:
   ```bash
   cd terraform/environments/prod
   terraform init
   terraform apply -auto-approve
   ```
3. **Configure GitHub Secrets**: Add the required secrets (`EC2_SSH_KEY`, `EC2_BASTION_HOST`, `EC2_FRONTEND_HOST`, `EC2_BACKEND_HOST`, `RDS_HOST`, `DB_PASSWORD`, `ALB_DNS_NAME`) to your GitHub repository secrets.
4. **Deploy Application**: Push this repository to your GitHub account to trigger the automated Actions runner.
5. **Set up Monitoring**: Run the telemetry exporter and dashboard scripts to visualize infrastructure and database health.

For full, step-by-step guidance on setting up, deploying, and verifying each tier, please see the [**Master Deployment Guide** (DEPLOYMENT_GUIDE.md)](file:///d:/1_Office_Document/4.%20Training/DevOps/Ostad/Assignment6/CombineProject/mahmud_assignment_6/DEPLOYMENT_GUIDE.md) included in this repository.

---

## 🧑‍💻 Author
**Mahmudur Rahman**  
*DevOps Engineer Trainee*  
Ostad Batch 11  
Key Pair Reference: `ostad_batch_11_mahmud`
