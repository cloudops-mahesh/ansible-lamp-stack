# Ansible LAMP Stack Deployment

Automated deployment of a production-grade LAMP (Linux, Apache, MySQL, PHP) stack across multiple servers using Ansible.

## Project Structure

## Features
- Multi-tier architecture (web server + database server)
- Ansible Roles for modular, reusable configuration
- Jinja2 templates for dynamic config files
- Idempotent playbooks (safe to run multiple times)
- Automated MySQL database and user creation
- PHP application deployment

## Prerequisites
- Ansible 2.16+
- Docker
- sshpass

## Usage

### 1. Clone the repository
```bash
git clone https://github.com/cloudops-mahesh/ansible-lamp-stack.git
cd ansible-lamp-stack
```

### 2. Start target servers
```bash
docker network create ansible-net

docker run -d --name web-server --network ansible-net \
  -p 8080:80 -p 2222:22 ubuntu-ssh

docker run -d --name db-server --network ansible-net \
  -p 2223:22 ubuntu-ssh
```

### 3. Run the playbook
```bash
ansible-playbook -i inventory/hosts.ini site.yml
```

### 4. Verify deployment
```bash
# Test web server
curl http://localhost:8080

# Test PHP
curl http://localhost:8080/info.php
```

## Results
- Apache serving app on port 8080
- PHP 7.4 running on Apache
- MySQL database created with dedicated app user
- App deployed across 2 containers automatically

## Tech Stack
- Ansible 2.16
- Apache 2
- MySQL 8
- PHP 7.4
- Docker
- Ubuntu 20.04
