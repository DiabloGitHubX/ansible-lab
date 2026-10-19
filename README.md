# Ansible Docker Lab

A lightweight Ansible lab that simulates a configuration-management
environment using Docker Compose.

## Architecture

- **Control node:** Ubuntu 22.04 with Ansible, SSH client, and Python.
- **Managed nodes:** Two Ubuntu 22.04 containers with OpenSSH server and Python.
- **Networking:** A private Docker bridge network.
- **Authentication:** SSH public-key authentication.
- **Inventory:** An INI inventory defining both managed nodes.

## Project Structure

```text
ansible-lab/
├── ansible/
│   └── .gitkeep
├── inventory/
│   └── hosts.ini
├── keys/                  # Generated locally; excluded from Git
├── .gitignore
├── compose.yaml
├── Dockerfile.control
├── Dockerfile.node
└── README.md
Prerequisites
- Docker Desktop
- Docker Compose
- Git
- An SSH key-generation utility (ssh-keygen)
Setup
Clone the repository and enter its directory:
git clone <your-repository-url>
cd ansible-lab


Generate a dedicated lab SSH key before building the images:
mkdir -p keys
ssh-keygen -t ed25519 -f keys/id_ed25519 -N ""


This creates a private key and a matching public key. Keep both local.
The keys/ directory is excluded from version control.
Start the Lab
Build the images:
docker compose build


Start the containers:
docker compose up -d


Open a shell in the control node:
docker compose exec control bash


Test connectivity to both managed nodes:
ansible managed_nodes -i /lab/inventory/hosts.ini -m ping


A successful test returns SUCCESS and pong for both nodes.
Stop and Clean Up
Stop and remove the containers and Compose network:
docker compose down


To also remove the images built for this lab:
docker image rm ansible-lab-control ansible-lab-node1 ansible-lab-node2


Security Notes
- SSH keys are excluded from version control.
- Use a dedicated key for this disposable lab.
- Host-key checking is disabled in the inventory for lab convenience.
  Do not use that setting in production environments.
- Never commit private keys, credentials, or other secrets.
Scope
This project demonstrates Ansible control-node setup, Docker networking,
SSH authentication, inventory configuration, and connectivity testing.
It does not currently include a configuration-management playbook.
EOF