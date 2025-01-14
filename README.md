# Infrastructure

# Infrastructure Project

## Project Overview

The objective of this project is to provide a reusable infrastructure setup for managing and deploying resources
efficiently. Using [Ansible](https://www.ansible.com/) as the core configuration and provisioning tool, this project
ensures consistent and reliable automation for infrastructure management. Additionally, the project supports a
Continuous Integration (CI) pipeline created using [GitLab CI/CD](https://docs.gitlab.com/ee/ci/).

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
    - [Installing Ansible](#installing-ansible)
3. [Configuration](#configuration)
4. [Running the Project](#running-the-project)
5. [CI/CD Pipeline Overview](#cicd-pipeline-overview)
6. [Purpose of the Project](#purpose-of-the-project)
7. [License](#license)

---

## Prerequisites

Before you begin, ensure you have the following:

- A machine running Linux/MacOS (or Windows with WSL), properly configured for Python.
- Python 3.9 or later installed. You can install it through your OS package manager or from the official Python website.
- Git installed to clone this repository.
- Access to a GitLab project to execute the CI pipeline, with proper permissions to trigger jobs.

---

## Installation

### Step 1: Clone the Repository

Clone this repository to your local machine using the command:

```bash
git clone <repository-url>
cd <repository-name>
```

### Step 2: Installing Ansible

Ansible is the foundation of this project. Follow these steps to install it:

#### For Ubuntu/Debian:

```bash
sudo apt update
sudo apt install -y ansible
```

#### For MacOS:

```bash
brew install ansible
```

#### For other systems:

Refer to
the [official Ansible installation guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

To verify the installation, check the Ansible version:

```bash
ansible --version
```

---

## Configuration

Before running the project or pipeline, you may need to configure the following:

1. **Inventory Files**: Ensure the `inventory` file contains your target server details.
   Example format:
   ```ini
   [webservers]
   192.168.1.1 ansible_user=ubuntu ansible_port=22 ansible_private_key_file=~/.ssh/id_rsa
   ```

2. **Variables**: Customize the variables in the `group_vars` or `host_vars` directories as needed for your
   infrastructure's requirements.

---

## Running the Project

Once Ansible is installed and the configuration is complete, use the following command to execute a playbook:

```bash
ansible-playbook -i inventory site.yml
```

### Key Notes:

- Replace `inventory` with the path to your hosts inventory file.
- Replace `site.yml` with the desired playbook (e.g., `deploy.yml` for deployments).

---

## CI/CD Pipeline Overview

This project includes a highly structured GitLab CI pipeline defined in the `.gitlab-ci.yml` file. Here's how it works:

### Pipeline Stages:

1. **Linting**: Ensures syntax validation of playbooks and scripts.
    - Command: `ansible-playbook --syntax-check`
2. **Testing**: Executes Ansible in "check mode" to perform a dry run of the playbooks.
    - Command: `ansible-playbook --check -i inventory site.yml`
3. **Deployment**: Runs the playbooks for actual provisioning and configuration of resources.

### Key Features:

- **Cache Management**: Optimizes repeated tasks by caching files/directories between stages.
- **Artifact Storage**: Ensures logs and target configuration files are saved as artifacts for auditing or review.
- **Fail-Safe Execution**: Any error in a stage halts the pipeline, ensuring no faulty deployments.

### Triggering the Pipeline:

The pipeline is triggered on:

- Any push to the `main` branch or a merge request.
- Optional manual execution through GitLab's CI/CD interface.

---

## Purpose of the Project

The primary objective of this project is to standardize and streamline infrastructure deployments. It adheres to *
*Infrastructure as Code (IaC)** principles, enabling:

1. **Automation**:
    - Simplifies the deployment of applications and infrastructure.
    - Eliminates manual errors by automating repetitive tasks.

2. **Consistency**:
    - Ensures uniform configurations across multiple environments (e.g., staging, production).

3. **Integration**:
    - Provides effective CI/CD pipelines for rapid deployment cycles.

4. **Scalability**:
    - Enables quick scaling of resources as per organizational needs.

By combining Ansible's simplicity with GitLab CI/CD's powerful automation, this project reduces overhead and provides a
comprehensive way to manage infrastructure.

---

## License

This project is open-source and licensed under an MIT license. See the [LICENSE](LICENSE) file for more details.