# Ansible AWX Training Module

A comprehensive, hands-on, 5-day training program for deploying, configuring, and operating a **production-ready Ansible AWX** platform. This Training takes participants from AWX fundamentals through advanced enterprise integration, high availability, security hardening, and day-2 operations.

![Duration](https://img.shields.io/badge/Duration-5%20Days-blue)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-orange)
![Format](https://img.shields.io/badge/Format-Hands--on%20Labs-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Learning Objectives](#-learning-objectives)
- [Audience](#-audience)
- [Prerequisites](#-prerequisites)
- [Lab Environment](#-lab-environment)
- [Training Schedule](#-training-schedule)
  - [Day 1: AWX Fundamentals & Architecture](#day-1-awx-fundamentals--architecture)
  - [Day 2: Production Deployment](#day-2-production-deployment)
  - [Day 3: Automation Content & Job Execution](#day-3-automation-content--job-execution)
  - [Day 4: RBAC, Security & Enterprise Integration](#day-4-rbac-security--enterprise-integration)
  - [Day 5: High Availability, Scaling & Operations](#day-5-high-availability-scaling--operations)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Lab Exercises](#-lab-exercises)
- [Assessment & Certification](#-assessment--certification)
- [Reference Architecture](#-reference-architecture)
- [Troubleshooting Guide](#-troubleshooting-guide)
- [Additional Resources](#-additional-resources)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

This training module is designed to give infrastructure, DevOps, and platform engineering teams the practical skills required to design, deploy, and operate **Ansible AWX** — the open-source upstream project for Red Hat Ansible Automation Platform's controller component — in a real-world, production-grade environment.

The course blends conceptual instruction with extensive hands-on labs, culminating in participants deploying a fully functional, highly available AWX cluster integrated with enterprise authentication, secrets management, and monitoring.

## 🎓 Learning Objectives

By the end of this training, participants will be able to:

- Explain AWX architecture, components, and how it relates to Ansible Core and Automation Platform
- Deploy AWX using the AWX Operator on Kubernetes/OpenShift, as well as via Docker Compose for lightweight environments
- Design and implement Organizations, Teams, Users, and Role-Based Access Control (RBAC)
- Build and manage Projects, Inventories, Credentials, and Job Templates
- Integrate AWX with source control (Git), external credential stores (HashiCorp Vault), and CI/CD pipelines
- Configure Workflow Templates for complex, multi-step automation
- Implement Single Sign-On (SSO/SAML) and LDAP/Active Directory authentication
- Harden AWX for production: TLS, secrets encryption, network policies, and backup/restore
- Configure high availability, horizontal scaling, and capacity planning for execution nodes
- Monitor AWX using Prometheus/Grafana and troubleshoot common operational issues
- Automate AWX configuration itself using the `awx.awx` Ansible Collection (Configuration as Code)

## 👥 Audience

- Systems Administrators and DevOps Engineers
- Platform/SRE teams responsible for automation infrastructure
- Ansible practitioners moving from ad-hoc/CLI usage to centralized automation
- IT teams evaluating or migrating to Red Hat Ansible Automation Platform

## ✅ Prerequisites

**Required:**
- Working knowledge of Linux system administration
- Basic familiarity with Ansible (playbooks, inventories, modules)
- Comfort with the command line and text editors (vim/nano)
- Basic understanding of networking (DNS, TLS/SSL, firewalls)

**Recommended:**
- Prior exposure to containers (Docker) and Kubernetes concepts
- Basic Git version control experience
- Familiarity with YAML syntax

**Not required but helpful:** Python scripting basics, cloud provider experience (AWS/Azure/GCP)

## 🖥️ Lab Environment

Each participant is provisioned with an isolated lab environment consisting of:

| Component | Specification |
|---|---|
| Control Node | 4 vCPU / 8 GB RAM / 40 GB disk (Ubuntu 22.04 or RHEL 9) |
| Kubernetes Cluster | 3-node K3s/kubeadm cluster (or OpenShift sandbox) |
| Target Managed Nodes | 4× Linux VMs (mixed RHEL/Ubuntu) |
| Supporting Services | Git server (Gitea), HashiCorp Vault, LDAP server, Prometheus/Grafana stack |
| Access | SSH keys + browser-based VS Code / terminal access |

> 💡 A cloud-based lab (AWS/Azure) or fully local (Vagrant + VirtualBox/libvirt) option is provided — see [`/labs/environment-setup`](./labs/environment-setup).

---

## 🗓️ Training Schedule

### Day 1: AWX Fundamentals & Architecture

**Morning — Concepts**
- What is AWX? History, relationship to Ansible Core and AAP
- AWX architecture deep dive: Web/API, Task dispatcher, PostgreSQL, Redis/RabbitMQ, execution/hop nodes, Receptor mesh
- The AWX Operator and Kubernetes-native deployment model
- Deployment options compared: AWX Operator vs. Docker Compose vs. source install

**Afternoon — Hands-on Labs**
- **Lab 1.1:** Provision the lab Kubernetes cluster
- **Lab 1.2:** Install the AWX Operator and deploy a baseline AWX instance
- **Lab 1.3:** Explore the AWX UI, API browser (`/api/v2/`), and `awx` CLI
- **Lab 1.4:** Create your first Organization, Project, Inventory, and Job Template

**Deliverable:** A running single-node AWX instance with a working "Hello World" job template.

---

### Day 2: Production Deployment

**Morning — Concepts**
- Sizing and capacity planning (control vs. execution nodes, database sizing)
- External PostgreSQL vs. managed-in-cluster database
- TLS/ingress configuration and custom domain setup
- Execution Environments (EE): the shift from virtualenvs to container-based automation
- Building custom Execution Environments with `ansible-builder`

**Afternoon — Hands-on Labs**
- **Lab 2.1:** Deploy AWX with an external PostgreSQL database and persistent storage
- **Lab 2.2:** Configure Ingress with TLS certificates (cert-manager)
- **Lab 2.3:** Build a custom Execution Environment image with `ansible-builder` and push it to a registry
- **Lab 2.4:** Configure AWX to use the custom EE for job execution

**Deliverable:** A production-configured AWX deployment with external database, TLS, and a custom EE.

---

### Day 3: Automation Content & Job Execution

**Morning — Concepts**
- Projects and SCM integration (Git branches, webhooks, signed commits)
- Dynamic inventories and inventory plugins (AWS, Azure, VMware, custom scripts)
- Credential types and the credential plugin system (Vault lookups)
- Job Templates vs. Workflow Job Templates vs. Workflow Approval nodes
- Surveys, extra variables, and prompt-on-launch fields

**Afternoon — Hands-on Labs**
- **Lab 3.1:** Connect AWX to a Git-backed Project with webhook-triggered updates
- **Lab 3.2:** Configure a dynamic cloud inventory with host filtering and smart inventories
- **Lab 3.3:** Integrate HashiCorp Vault as an external credential source
- **Lab 3.4:** Build a multi-step Workflow Template with conditional branching and an approval node
- **Lab 3.5:** Create a Survey-driven, self-service Job Template

**Deliverable:** An end-to-end automated workflow: code commit → webhook → multi-stage deployment workflow with approval gate.

---

### Day 4: RBAC, Security & Enterprise Integration

**Morning — Concepts**
- Organizations, Teams, and the AWX RBAC model (roles, permissions inheritance)
- Authentication backends: LDAP/Active Directory, SAML, OIDC/OAuth2
- Secrets management best practices; encrypted fields and `SECRET_KEY` rotation
- Network security: isolated/hop nodes, Receptor mesh security, NetworkPolicies
- Auditing: activity streams, external logging (Splunk/ELK/Loki)

**Afternoon — Hands-on Labs**
- **Lab 4.1:** Design and implement a multi-tenant RBAC model (Orgs/Teams/Roles) for a sample organization
- **Lab 4.2:** Integrate AWX with LDAP for authentication and team mapping
- **Lab 4.3:** Configure SAML SSO against a mock Identity Provider
- **Lab 4.4:** Ship AWX activity stream and job logs to an external logging stack
- **Lab 4.5:** Harden the deployment — Kubernetes NetworkPolicies, secret rotation, least-privilege service accounts

**Deliverable:** A secured, multi-tenant AWX instance with SSO and centralized logging.

---

### Day 5: High Availability, Scaling & Operations

**Morning — Concepts**
- AWX clustering model: control plane replicas, execution/hop node topology
- Horizontal scaling of execution capacity; instance groups and container groups (Kubernetes-native job execution)
- Backup and restore strategy (AWX Operator backup/restore CRs, database backups, disaster recovery)
- Upgrade strategy and change management
- Monitoring and alerting with Prometheus/Grafana; key AWX metrics
- Configuration as Code: managing AWX itself with the `awx.awx` Ansible Collection / Terraform AWX provider

**Afternoon — Hands-on Labs**
- **Lab 5.1:** Scale AWX control plane replicas and configure Instance Groups / Container Groups
- **Lab 5.2:** Perform a full backup and disaster-recovery restore exercise
- **Lab 5.3:** Deploy Prometheus/Grafana dashboards for AWX metrics and configure alert rules
- **Lab 5.4:** Codify the entire AWX configuration (Orgs, Projects, Credentials, Templates) using the `awx.awx` collection in a Git repository
- **Lab 5.5 (Capstone):** From a clean cluster, deploy production AWX end-to-end using only your Day 5 Configuration-as-Code repo

**Deliverable (Capstone Project):** A fully automated, reproducible, production-ready AWX deployment — infrastructure, security, and automation content all defined as code.

---

## 📁 Repository Structure

```
ansible-awx-training/
├── README.md
├── slides/                    # Day-by-day presentation decks
│   ├── day1-fundamentals.pdf
│   ├── day2-production-deployment.pdf
│   ├── day3-automation-content.pdf
│   ├── day4-security-rbac.pdf
│   └── day5-ha-operations.pdf
├── labs/
│   ├── environment-setup/     # Vagrant/Terraform/cloud lab bootstrap
│   ├── day1/
│   ├── day2/
│   ├── day3/
│   ├── day4/
│   └── day5/
├── manifests/
│   ├── awx-operator/          # AWX Operator install manifests
│   ├── awx-instance/          # AWX CR examples (baseline → production)
│   └── ingress-tls/
├── execution-environments/
│   ├── ee-base/               # ansible-builder definitions
│   └── ee-cloud/
├── playbooks/
│   └── sample-content/        # Example playbooks used across labs
├── config-as-code/
│   └── awx-config/            # awx.awx collection variable structure
├── solutions/                 # Reference solutions for each lab
└── docs/
    ├── troubleshooting.md
    ├── architecture-diagrams/
    └── glossary.md
```
## 🧪 Lab Exercises

Each day's lab folder (`labs/dayN/`) contains:
- `README.md` — step-by-step instructions and success criteria
- `starter/` — starting-point files/configs
- `hints.md` — progressive hints for anyone who gets stuck
- Corresponding reference solution in `solutions/dayN/`

Labs are designed to be completed sequentially, with each day building on the environment created the day before.

## 📜 Assessment & Certification

- **Daily checkpoints:** short knowledge checks at the end of each day
- **Capstone project (Day 5):** graded on functionality, security posture, and use of Configuration-as-Code
- **Certificate of completion** issued to participants who complete all daily labs and the capstone project

## 🏗️ Reference Architecture

The course builds toward the following production reference architecture:

```
                         ┌─────────────────────┐
                         │   Load Balancer /    │
                         │   Ingress (TLS)       │
                         └──────────┬───────────┘
                                    │
                 ┌──────────────────┴──────────────────┐
                 │         AWX Control Plane            │
                 │   (2+ Web/Task replicas, HA)         │
                 └───────┬───────────────────┬─────────┘
                         │                   │
              ┌──────────▼───────┐  ┌────────▼─────────┐
              │  PostgreSQL (HA) │  │  Redis            │
              └───────────────────┘  └────────────────────┘
                         │
                 ┌───────▼────────────────────┐
                 │   Receptor Mesh             │
                 │  (Hop Nodes / Execution      │
                 │   Nodes / Container Groups)  │
                 └───────┬────────────────────┘
                         │
             ┌───────────┴────────────┐
             │   Managed Node Fleet     │
             └─────────────────────────┘

     Sidecars: Prometheus/Grafana, external logging, Vault
```

See [`docs/architecture-diagrams/`](./docs/architecture-diagrams) for detailed diagrams per day.

## 🛠️ Troubleshooting Guide

Common issues and resolutions are documented in [`docs/troubleshooting.md`](./docs/troubleshooting.md), covering:
- AWX Operator reconciliation failures
- Job execution stuck in "pending"
- Receptor mesh connectivity issues
- Database migration failures during upgrades
- Certificate/TLS handshake errors

## 📚 Additional Resources

- [AWX GitHub Repository](https://github.com/ansible/awx)
- [AWX Operator GitHub Repository](https://github.com/ansible/awx-operator)
- [Ansible AWX Documentation](https://ansible.readthedocs.io/projects/awx/en/latest/)
- [`awx.awx` Ansible Collection Docs](https://github.com/ansible/awx/tree/devel/awx_collection)
- [Ansible Builder Documentation](https://ansible-builder.readthedocs.io/)

## 🤝 Contributing

Contributions to improve labs, fix errata, or add advanced modules are welcome. Please open an issue or submit a pull request following the guidelines in `CONTRIBUTING.md`.

## 📄 License

This training material is released under the [MIT License](./LICENSE).

---

*Questions or feedback? Open an issue in this repository or contact the training team.*
