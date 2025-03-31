# Ansible

## What is Ansible?
Ansible is an open-source automation and configuration management tool used to automate tasks. It provides simple yet powerful automation that reduces complexity and runs on multiple platforms. With Ansible, you can automate virtually any task efficiently.

## Steps to Install Ansible
```sh
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

## Ansible Commands
### Ping Hosts
```sh
ansible -i hosts all -m ping
ansible all -m ping -i inventory.ini --private-key ~/.ssh/my-key.pem
```

### Run Playbook
```sh
ansible-playbook -i hosts playbook.yml
ansible-playbook -i inventory.ini playbook.yml --private-key ~/.ssh/my-key.pem
```

## Ansible Galaxy
Ansible Galaxy is a repository for Ansible roles that allows you to share, download, and manage roles easily.

### Create a New Role
```sh
ansible-galaxy init my_role_name
```

### Directory Structure of a Role
```
my_role_name/
├── defaults/
│   └── main.yml    # Default variables for the role
├── files/          # Static files that can be copied to remote hosts
├── handlers/       # Handlers to be notified on changes (e.g., restart a service)
├── meta/           # Metadata, including dependencies, author info
│   └── main.yml
├── tasks/          # Main tasks that the role will perform
│   └── main.yml
├── templates/      # Jinja2 templates to be rendered
├── tests/          # Test playbooks for role verification
├── vars/           # Variables specific to the role
│   └── main.yml
└── README.md       # Documentation for the role
```

## Additional Resources
- [Official Ansible Documentation](https://docs.ansible.com/)
- [Ansible Galaxy](https://galaxy.ansible.com/)
- [Ansible GitHub Repository](https://github.com/ansible/ansible)

