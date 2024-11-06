
## Overview

This Ansible repository contains a playbook designed to execute the `ping` module across Linux, Windows, and Mac hosts, ensuring connectivity.

## Prerequisites

- Ansible installed on the control node
- SSH access for Linux and Mac hosts (configure as needed in `inventories/hosts.ini`)
- WinRM access for Windows hosts (configure as needed in `inventories/hosts.ini`)

## Usage

1. Clone this repository.
2. Update `inventories/hosts.ini` with your hosts' details.
3. Run the playbook:
   ```bash
   ansible-playbook -i inventories/hosts.ini playbooks/ping_pong.yml