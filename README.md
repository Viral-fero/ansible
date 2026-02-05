# Ansible Localhost Development Setup (Ubuntu 24.04)

This repository contains Ansible playbooks to configure a local Ubuntu 24.04 virtual machine. All playbooks are intended to run on **localhost** (local VM), not on remote servers.

---

## Repository Structure

- `inventory.ini`
- `user-create.yaml`
- `setup.yaml`
- `postgres.yaml`
- `README.md`

---

## Playbooks Overview

### `user-create.yaml`
- Creates a new local user
- Sets the hostname based on user input
- Adds the user to the `sudo` group
- Reboots the system if the hostname changes

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
- Enables PostGIS extension

---

## Prerequisites

- Ubuntu 24.04
- Local VM or local machine
- Sudo privileges

**Install Ansible:**
```bash
sudo apt update
sudo apt install -y ansible
```
## Verify installation
```
ansible --version
```


#=========
Ansible Localhost Development Setup (Ubuntu 24.04)

This repository contains Ansible playbooks to configure a local Ubuntu 24.04 virtual machine.
All playbooks are intended to run on localhost (local VM), not on remote servers.

Repository Structure
.
├── inventory.ini
├── user-create.yaml
├── setup.yaml
├── postgres.yaml
└── README.md

Playbooks Overview
1. user-create.yaml

Creates a new local user

Sets hostname based on user input

Adds the user to the sudo group

Reboots the system if the hostname changes

2. setup.yaml

Installs a full local development environment:

Base system packages

NVM + Node.js (LTS) for all detected users

Redis

Visual Studio Code

Google Chrome

PyCharm Community Edition

3. postgres.yaml

Installs PostgreSQL 16

Installs PostGIS

Creates PostgreSQL user and database

Enables PostGIS extension

Prerequisites

Ubuntu 24.04

Local VM or local machine

Sudo privileges

Install Ansible
sudo apt update
sudo apt install -y ansible


Verify installation:

ansible --version

Inventory Configuration (Localhost)

This project is configured to run on localhost.

Example inventory.ini:

[dev]
localhost ansible_connection=local

How to Run Playbooks

Run all commands from the project root directory.

1. Create User and Set Hostname
ansible-playbook -i inventory.ini user-create.yaml --ask-become-pass


You will be prompted for:

Location

First name

Last name

Employee ID

The system will reboot automatically if the hostname changes.

2. Setup Development Environment
ansible-playbook -i inventory.ini setup.yaml --ask-become-pass


This installs Node.js, Redis, VS Code, Chrome, PyCharm, and other tools.

3. Install PostgreSQL and PostGIS
ansible-playbook -i inventory.ini postgres.yaml --ask-become-pass


Default PostgreSQL configuration:

Version: 16

Database: ferodb

User: fero

You can change these values inside postgres.yaml.

Recommended Execution Order

user-create.yaml

setup.yaml

postgres.yaml

Notes

Designed for local development only

Safe to re-run (idempotent)

Uses sudo (become: true)

Not intended for production servers

