# Ansible Documentation

Ansible is an open-source automation platform for configuration management, application deployment, and infrastructure automation. It is agentless and communicates with managed nodes using SSH on Linux or WinRM on Windows.

> In simple terms, Ansible lets you control and configure many computers from one place.

## Contents

- [Key Features](#key-features)
- [Why Use Ansible?](#why-use-ansible)
- [How Ansible Connects to Servers](#how-ansible-connects-to-servers)
- [Remote Python Requirement](#remote-python-requirement)
- [Ansible Architecture](#ansible-architecture)
- [Installation](#installation)
- [Configuration File](#configuration-file)
- [Inventory](#inventory)
- [Playbooks](#playbooks)
- [Modules and Tasks](#modules-and-tasks)
- [Variables and Facts](#variables-and-facts)
- [Roles](#roles)
- [Ansible Vault](#ansible-vault)

## Key Features

- **Agentless:** No Ansible software is required on managed nodes.
- **Secure communication:** Uses SSH for Linux and WinRM for Windows by default.
- **YAML-based:** Playbooks use YAML, which is readable and easy to maintain.
- **Declarative:** You describe the desired state instead of every implementation step.
- **Idempotent:** Repeating a playbook should produce the same intended result without unnecessary changes.

## Why Use Ansible?

Before automation, infrastructure tasks were often performed manually or with ad hoc scripts. This can lead to:

- Logging into servers one by one
- Human errors
- Inconsistent configurations
- Time-consuming deployments
- Difficult scaling
- Poor repeatability and rollback

Ansible addresses these problems with:

- **Automation:** Reduces manual work.
- **Consistency:** Applies the same configuration everywhere.
- **Scalability:** Manages anything from a few servers to thousands of hosts.
- **Fast deployments:** Runs repeatable changes across many systems.
- **Repeatability:** Reuses the same automation for development, testing, and production.

For example, instead of installing Nginx manually on 50 servers, you can use one playbook to install and configure it consistently across all of them.

## How Ansible Connects to Servers

Ansible uses the following connection methods by default:

| Managed node | Connection method |
| --- | --- |
| Linux and other Unix-like systems | SSH |
| Windows systems | WinRM |

For Linux hosts, the control node generally requires:

- Network access to the managed host
- SSH access and valid credentials
- Python installed on the managed host

## Remote Python Requirement

Many Ansible modules are implemented in Python. Ansible transfers and executes these modules on the managed host, so Python must be installed on remote systems when the selected modules require it.

## Ansible Architecture

Ansible uses a control node to automate managed nodes.

| Component | Purpose |
| --- | --- |
| **Control node** | The machine where Ansible is installed and automation is executed. |
| **Managed nodes** | The servers and devices Ansible configures. |
| **Inventory** | A file or source that defines managed hosts and groups. |
| **Playbooks** | YAML files that describe the desired state and automation workflow. |
| **Modules** | Reusable units of code that perform individual operations. |
| **Roles** | Reusable project structures that organize playbooks, tasks, variables, and handlers. |

The control node reads the inventory, connects to managed nodes, and runs the tasks defined in playbooks.

## Installation

On Ubuntu or another Debian-based Linux distribution:

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

Verify the installation:

```bash
ansible --version
```

## Configuration File

Ansible uses `ansible.cfg` for configuration. It searches for the configuration file in the following order:

1. The path specified by the `ANSIBLE_CONFIG` environment variable
2. `ansible.cfg` in the current project directory
3. `~/.ansible.cfg` in the user's home directory
4. `/etc/ansible/ansible.cfg` as the system-wide default

Keeping `ansible.cfg` in the project directory makes project-specific settings explicit and easier to share.

## Inventory

An inventory defines the hosts managed by Ansible. Hosts can be grouped so the same automation can target a specific environment or role.

The default inventory file is:

```text
/etc/ansible/hosts
```

Example inventory:

```ini
[webservers]
web-01 ansible_host=192.0.2.10
web-02 ansible_host=192.0.2.11

[dbservers]
db-01 ansible_host=192.0.2.20
```

Test connectivity to all hosts in an inventory:

```bash
ansible all -i hosts -m ping
```

## Playbooks

Playbooks are YAML files that define automation steps and the desired state of systems.

Example playbook:

```yaml
---
- name: Configure web servers
  hosts: webservers
  become: true
  tasks:
    - name: Install Nginx
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: true
```

Run a playbook with a custom inventory:

```bash
ansible-playbook -i hosts site.yml
```

## Modules and Tasks

Modules perform actions such as installing packages, managing services, creating users, and copying files. Tasks call modules within a playbook.

Example task:

```yaml
- name: Ensure Nginx is running
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: true
```

Using fully qualified collection names, such as `ansible.builtin.apt`, makes the module source explicit and improves readability.

## Variables and Facts

Variables make playbooks reusable and dynamic. Facts are system information that Ansible gathers automatically from managed hosts, such as operating system, network, and hardware details.

Example variable usage:

```yaml
vars:
  web_package: nginx

tasks:
  - name: Install the web package
    ansible.builtin.apt:
      name: "{{ web_package }}"
      state: present
```

## Roles

Roles organize automation into reusable components. A typical role can contain:

```text
roles/
└── webserver/
    ├── defaults/
    ├── handlers/
    ├── tasks/
    ├── templates/
    ├── vars/
    └── README.md
```

Roles are recommended for larger or production environments because they make automation easier to reuse, test, and maintain.

## Ansible Vault

Ansible Vault encrypts sensitive data such as passwords, API keys, and private configuration values.

Create an encrypted variables file:

```bash
ansible-vault create secrets.yml
```

Run a playbook that uses vaulted data:

```bash
ansible-playbook -i hosts site.yml --ask-vault-pass
```

Avoid committing plaintext secrets to source control. Keep encryption keys and vault passwords outside the repository.