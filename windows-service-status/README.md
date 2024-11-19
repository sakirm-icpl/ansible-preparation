# Ansible Playbook for Windows Service Status Check
==============================================


## Overview
------------

This Ansible playbook project is designed to check the status of specific Windows services, including:

* Wazuh
* Osquery
* Sysmon
* Defender
* Invinsense Agent

## Directory Layout
-------------------

Our project follows the alternative directory layout suggested by Ansible Best Practices  <sup><a href="https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html" target="_blank" rel="noreferrer" style="color: rgb(59, 130, 246); text-decoration: none; hover:text-decoration: underline;">2</a></sup>:

```plain
windows-service-status/
├── roles/
│   └── windows_services/
│       ├── tasks/
│       │   └── main.yml
│       ├── defaults/
│       │   └── main.yml
│       └── meta/
├── hosts
├── windows-service-status.yml
└── README.md