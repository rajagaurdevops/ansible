# 📘 Ansible Documentation

---

## 1. Introduction

**Ansible** is an open-source automation tool used for:
- Configuration management  
- Application deployment  
- Infrastructure automation  

Ansible is **agentless** and communicates with managed nodes using:
- **SSH** (Linux)
- **WinRM** (Windows)

👉 **In simple words:**  
Ansible lets you control many computers from one place automatically.

---

## 2. Key Features of Ansible

- Agentless (no software needed on target machines)
- Uses SSH (Linux) or WinRM (Windows)
- Written in YAML (easy to read)
- Declarative (you say *what* you want, not *how*)
- Idempotent (runs safely multiple times)

---

## 3. Why Do We Need Ansible?

Before Ansible, tasks were done manually or with scripts.

### Problems Without Ansible ❌
- Logging into servers one by one
- Human errors
- Different configurations on different servers
- Time-consuming and hard to scale
- Difficult to reproduce the same setup again

### What Ansible Solves ✅
- Automation (no manual work)
- Consistency (same configuration everywhere)
- Scalability (manage 10 or 10,000 servers)
- Faster deployments
- Easy rollback and repeatability

**Example:**  
Instead of installing **Nginx** manually on 50 servers, Ansible does it in **one command**.

---

## 4. How Ansible Connects to Servers

- Uses **SSH** by default
- Requires:
  - SSH access
  - Python installed on the remote machine

---

## 5. Why Do We Need Python Installed on Remote Servers?

### Short Answer (Interview-Ready ✅)
Ansible modules are written in **Python**, so the remote server needs Python to execute those modules.

---

## 6. Ansible Architecture

Ansible consists of:
- Control Node
- Managed Nodes
- Inventory
- Playbooks
- Modules
- Roles  

The **control node** pushes tasks to managed nodes.

---

## 7. Installation

### Install Ansible on Linux (Ubuntu)

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
ansible --version
```
### 8. Configuration File
The Ansible configuration file is:
```
/etc/ansible/ansible.cfg
```
### 9. Inventory
Inventory defines the hosts managed by Ansible<br>
Default inventory file:
```
/etc/ansible/hosts
```
### 10. Playbooks
Playbooks are YAML files that define automation steps<br>
They describe the desired state of systems<br>
Run a playbook:
```
ansible-playbook -i hosts file.yml
```

### 11. Modules and Tasks
Modules perform actual tasks such as:<br>
Installing packages<br>
Managing services<br>
Copying files<br>
Tasks call modules within playbooks 

### 12. Variables and Facts
Variables make playbooks dynamic<br>
Facts are system information collected automatically from hosts (OS, IP, memory, etc.)

### 13. Roles
Roles organize playbooks into reusable components and are recommended for production environments.
