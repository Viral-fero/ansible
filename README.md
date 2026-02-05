## Ansible Localhost Development Setup (Ubuntu 24.04)

This repository contains Ansible playbooks to configure a local Ubuntu 24.04 virtual machine. All playbooks are intended to run on **localhost** (local VM), not on remote servers.

---

### Repository Structure

- `inventory.ini`
- `user-create.yaml`
- `setup.yaml`
- `postgres.yaml`
- `README.md`

---

### Playbooks Overview

### `user-create.yaml`
- Creates a new local user
- Sets the hostname based on user input
- Adds the user to the `sudo` group
- **No automatic reboot is performed** after hostname change

### `setup.yaml`
Installs a full local development environment:
- Base system packages
- NVM + Node.js (LTS) for all detected users
- Redis
- Visual Studio Code
- Google Chrome
- PyCharm Community Edition

### `postgres.yaml`
- Installs PostgreSQL 16
- Installs PostGIS
- Creates a PostgreSQL user and database
- PostgreSQL user is created with **SUPERUSER** privileges
- Enables PostGIS extension
  
---

### Prerequisites

- Ubuntu 24.04
- Local VM or local machine
- Sudo privileges

**Install Ansible:**
```
sudo apt update
sudo apt install -y ansible
```
### Verify installation
```
ansible --version
```

### Inventory Configuration (Localhost)

- This project is configured to run on localhost.

  Example inventory.ini:
```
[dev]
localhost ansible_connection=local
```
### How to Run Playbooks

Run all commands from the project root directory.

1. Create User and Set Hostname
```
 ansible-playbook -i inventory.ini user-create.yaml
```

 You will be prompted for:

  - Location
  -  First name
  -  Last name
  -  Employee ID   

2. Setup Development Environment
```
ansible-playbook -i inventory.ini setup.yaml
```
This installs:
  - Node.js
  - Redis
  - VS Code
  - Google Chrome
  - PyCharm Community Edition

3. Install PostgreSQL and PostGIS
```
ansible-playbook -i inventory.ini postgres.yaml
```

Default PostgreSQL configuration:
  - Version: 16
  - Database: ferodb
  - User: fero (SUPERUSER)

You can change these values inside postgres.yaml.

### Recommended Execution Order
  -  user-create.yaml
  -  setup.yaml
  -  postgres.yaml

