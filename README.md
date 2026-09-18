# Ansible WordPress Deployment CI/CD Pipeline

## Overview

This project implements an automated **CI/CD deployment pipeline for WordPress** using **Ansible, Docker, Docker Compose, and GitHub Actions**.

The solution automates the provisioning, configuration, and deployment of a containerized WordPress application on a remote Linux server. GitHub Actions provides the CI/CD orchestration layer, while a **self-hosted GitHub Actions runner** executes the deployment workflow and Ansible manages the target server configuration.

The project demonstrates how configuration management, containerization, and CI/CD automation can be integrated into a repeatable and maintainable deployment workflow.

---

## Architecture

```text
                    Developer
                        │
                        │ Git Push
                        ▼
              ┌─────────────────────┐
              │  GitHub Repository  │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   GitHub Actions    │
              │    CI/CD Pipeline   │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │  Self-Hosted Runner │
              └──────────┬──────────┘
                         │
                         │ SSH / Ansible
                         ▼
              ┌─────────────────────┐
              │   WordPress Server  │
              │     Linux Host      │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │        Docker       │
              │    Docker Compose   │
              └──────────┬──────────┘
                         │
                 ┌───────┴────────┐
                 ▼                ▼
        ┌───────────────┐  ┌───────────────┐
        │   WordPress   │  │     MySQL     │
        │   Container   │  │   Container   │
        └───────────────┘  └───────────────┘
```

---

## Technology Stack

| Technology | Purpose |
|---|---|
| **GitHub** | Source code management |
| **GitHub Actions** | CI/CD workflow automation |
| **Self-Hosted Runner** | Executes deployment jobs |
| **Ansible** | Configuration management and deployment automation |
| **Docker** | Application containerization |
| **Docker Compose** | Multi-container orchestration |
| **WordPress** | Web application |
| **MySQL** | Database service |
| **Linux** | Server environment |
| **SSH** | Secure remote communication |

---

## Deployment Workflow

The pipeline automates the deployment lifecycle from source-code changes to a running WordPress application.

### 1. Source Code Management

A developer pushes changes to the GitHub repository.

```text
Git Push
   │
   ▼
GitHub Repository
```

The configured GitHub Actions workflow is triggered according to the workflow configuration.

### 2. CI/CD Execution

GitHub Actions starts the deployment job on the configured **self-hosted runner**.

The runner provides the execution environment for the Ansible-based deployment process.

### 3. Environment Validation

Before deployment, the workflow validates the environment by performing tasks such as:

- Checking out the repository
- Verifying the Ansible installation
- Testing connectivity to the WordPress server
- Validating the Ansible inventory
- Validating the Ansible playbook

### 4. Infrastructure Configuration

Ansible connects to the target WordPress server over SSH and performs the required configuration tasks.

These tasks include:

- Installing required packages
- Installing Docker
- Starting Docker
- Creating the application directory
- Deploying the Docker Compose configuration

### 5. Application Deployment

Docker Compose starts the WordPress application stack.

```text
Docker Compose
      │
      ├── WordPress
      │
      └── MySQL
```

The services communicate through the Docker Compose network, while persistent volumes provide storage for application and database data.

### 6. Deployment Completion

After the Ansible playbook completes successfully, the WordPress and MySQL containers are running on the target server.

---

## CI/CD Pipeline Stages

The GitHub Actions workflow follows a structured deployment sequence:

```text
Checkout Repository
        │
        ▼
Check Ansible Version
        │
        ▼
Test WordPress Server Connectivity
        │
        ▼
Validate Ansible Playbook
        │
        ▼
Execute Ansible Deployment
        │
        ▼
Configure Docker
        │
        ▼
Deploy Docker Compose Stack
        │
        ▼
WordPress Application Running
```

This validation-first approach helps identify configuration or connectivity problems before the deployment is applied.

---

## Ansible Automation

Ansible provides the configuration-management and deployment layer of the project.

Instead of manually configuring the WordPress server, the required configuration is defined as code in Ansible playbooks.

The playbook automates:

- Remote server configuration
- Package installation
- Docker installation
- Docker service management
- Application directory creation
- Docker Compose configuration
- WordPress stack deployment

This makes the deployment process **repeatable, consistent, and maintainable**.

---

## Containerized Application

The WordPress environment is deployed using Docker Compose.

The application consists of two primary services.

### WordPress

Provides the web application and runtime required to run WordPress.

### MySQL

Provides the relational database used by WordPress to store application data.

Docker Compose manages:

- Service definitions
- Container networking
- Persistent volumes
- Service startup
- Container lifecycle

---

## Self-Hosted GitHub Actions Runner

A self-hosted GitHub Actions runner is used as the execution environment for the deployment pipeline.

The runner executes the GitHub Actions workflow and provides the environment from which Ansible communicates with the target WordPress server.

The deployment flow is:

```text
GitHub Actions
      │
      ▼
Self-Hosted Runner
      │
      │ Ansible + SSH
      ▼
Remote WordPress Server
```

This architecture provides control over the CI/CD execution environment and enables the runner to communicate with the configured deployment infrastructure.

---

## Project Structure

A typical project structure is:

```text
docker-wordpress-ansible-automation/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── ansible/
│   ├── inventory
│   └── wordpress.yml
│
├── docker-compose.yml
│
└── README.md
```

> The exact structure may vary depending on the current implementation of the repository.

---

## Key DevOps Practices Demonstrated

This project demonstrates practical implementation of:

- **Infrastructure as Code**
- **Configuration Management**
- **Continuous Integration**
- **Continuous Deployment**
- **Containerization**
- **Container Orchestration**
- **Deployment Automation**
- **SSH-Based Remote Automation**
- **Self-Hosted CI/CD Infrastructure**
- **Repeatable Deployments**
- **Source-Controlled Infrastructure Configuration**

---

## Project Objectives

The primary objectives of this project are to:

1. Automate WordPress server configuration using Ansible.
2. Containerize WordPress and MySQL using Docker.
3. Orchestrate the application stack using Docker Compose.
4. Implement an automated GitHub Actions CI/CD pipeline.
5. Execute deployments through a self-hosted GitHub Actions runner.
6. Reduce manual configuration and deployment steps.
7. Establish a repeatable deployment process using Infrastructure as Code principles.

---

## Deployment Flow

The complete DevOps workflow can be summarized as:

```text
Developer
    │
    │ Git Push
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ▼
Self-Hosted Runner
    │
    ▼
Ansible
    │
    ▼
Remote Linux Server
    │
    ▼
Docker
    │
    ▼
Docker Compose
    │
    ├───────────────┐
    ▼               ▼
WordPress          MySQL
Container          Container
```

---

## Validation and Deployment

The CI/CD workflow includes validation steps before deployment, including:

- Ansible version verification
- Remote server connectivity testing
- Ansible playbook validation
- Automated deployment execution

A successful pipeline results in the WordPress application stack being deployed through Ansible and Docker Compose.

---

## Skills Demonstrated

### DevOps
- CI/CD
- Infrastructure as Code
- Configuration Management
- Deployment Automation

### Automation
- Ansible
- GitHub Actions
- Self-Hosted GitHub Actions Runner

### Containerization
- Docker
- Docker Compose
- Multi-Container Applications

### Linux & Infrastructure
- Linux server administration
- SSH
- Remote server configuration
- Service management

### Application Deployment
- WordPress
- MySQL
- Containerized web application deployment

---

## Future Improvements

Potential enhancements for a production-oriented implementation include:

- Add automated application health checks
- Add deployment rollback mechanisms
- Introduce environment-specific configurations
- Store sensitive values using GitHub Actions Secrets
- Add Docker image versioning
- Add automated backup and restore procedures
- Add monitoring and logging
- Introduce staging and production environments
- Add security scanning to the CI/CD pipeline

---

## Conclusion

This project demonstrates an end-to-end DevOps deployment workflow for a containerized WordPress application.

By combining **GitHub Actions, a self-hosted runner, Ansible, Docker, and Docker Compose**, the project replaces repetitive manual deployment activities with an automated and repeatable process.

The resulting workflow provides a practical foundation for understanding modern **CI/CD, configuration management, containerization, and infrastructure automation**.

👨‍💻 Author Shyam Raut

GitHub: techconet57

This project is created for learning, practice, and DevOps portfolio purposes.
