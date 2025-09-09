# Homelab Ansible

Ansible automation for my homelab infrastructure. This repository contains playbooks and roles to set up and manage various types of servers in my home environment.

![GitHub](https://img.shields.io/github/license/diedomin/homelab-ansible?style=flat-square)
![GitHub Repo stars](https://img.shields.io/github/stars/diedomin/homelab-ansible?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/diedomin/homelab-ansible?style=flat-square)

## Structure

```
├── playbooks/
│   └── basic-server/          # Basic server setup playbook
├── inventory                  # Inventory file defining hosts
└── vault-password.txt         # Ansible vault password file
```

## What it does

- **Basic Server Setup**: Updates packages, configures passwordless sudo, and performs initial server hardening
- **Node Exporter**: Installs Prometheus node-exporter on standalone instances for monitoring
- **Kubernetes Prep**: Disables swap on designated k8s instances

## Usage

### Prerequisites

- Ansible installed on your control machine
- SSH access to target hosts
- Inventory file configured with your hosts

### Running the playbook

```bash
# Install required roles
ansible-galaxy install -r playbooks/basic-server/requirements.yml

# Run the basic server setup
ansible-playbook -i inventory playbooks/basic-server/basic-server.yml
```

### Host Groups

The playbook uses different host groups:
- `all`: Basic server setup applied to all hosts
- `standalone`: Standalone servers that get node-exporter
- `k8s_instances`: Kubernetes nodes that need swap disabled

## External Roles

This project uses custom roles hosted on GitHub:
- [disable_swap](https://github.com/diedomin/ansible.disable_swap) - Disables swap for Kubernetes nodes
- [node_exporter](https://github.com/diedomin/ansible.node-exporter) - Installs Prometheus node-exporter
- [grafana_alloy](https://github.com/diedomin/ansible.grafana_alloy) - Install and configure Grafana Alloy as a systemd service

## Configuration

Update the `inventory` file with your server details and group them according to their purpose (standalone, k8s_instances, etc.).
