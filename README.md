# Ansible Ping Pong Repository
==========================

## Overview

This Ansible repository provides a comprehensive setup for demonstrating Ansible's connectivity and ping functionality across multiple operating systems, including:

* **Linux**
* **Mac** (macOS)
* **Windows**

## Repository Structure

* **`inventories/`**: Hosts and inventory files for Ansible
    + `hosts.ini`: Example inventory file with Linux, Mac, and Windows hosts
* **`playbooks/`**: Ansible playbooks for ping and connectivity testing
    + `ping_pong.yml`: Playbook for pinging all hosts in the inventory
* **`establishing-ssh-connectivity/`**: Guides for setting up SSH connectivity
    + **`mac-setup/`**: Setup SSH on Mac
    + **`linux-setup/`**: Setup SSH on Linux
    + `README.md`: Overview of SSH connectivity setup
* **`establishing-winrm-connectivity/`**: Guides for setting up WinRM connectivity on Windows
    + **`windows-setup/`**: Setup WinRM on Windows
    + **`windows-setup/script`**: Ansible winrm powershell script for setup winrm
    + `README.md`: Overview of WinRM connectivity setup

## Getting Started

1. **Clone this repository**: `git clone https://github.com/sakirm-icpl/ansible-preparation.git`
2. **Update `inventories/hosts.ini`**: Replace placeholders with your actual host IPs, usernames, and passwords
3. **Setup SSH connectivity** (if needed):
    * Follow guides in `establishing-ssh-connectivity/` for Mac and Linux hosts
4. **Setup WinRM connectivity** (if needed):
    * Follow guide in `establishing-winrm-connectivity/` for Windows hosts
5. **Run the Ansible playbook**:
    * `ansible-playbook -i inventories/hosts.ini playbooks/ping_pong.yml`

