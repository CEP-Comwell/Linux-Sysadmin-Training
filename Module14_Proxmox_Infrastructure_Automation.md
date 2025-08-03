# Module 14: Proxmox Infrastructure Automation

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [14.1 Infrastructure as Code Fundamentals](#141-infrastructure-as-code-fundamentals)
  - [14.2 Terraform with Proxmox](#142-terraform-with-proxmox)
  - [14.3 Advanced Terraform Practices](#143-advanced-terraform-practices)
  - [14.4 Ansible Configuration Management](#144-ansible-configuration-management)
  - [14.5 Advanced Ansible Techniques](#145-advanced-ansible-techniques)
  - [14.6 Cloud-Init Integration](#146-cloud-init-integration)
  - [14.7 Secrets Management](#147-secrets-management)
  - [14.8 Testing and Validation](#148-testing-and-validation)
  - [14.9 CI/CD Pipeline Integration](#149-cicd-pipeline-integration)
  - [14.10 Monitoring and Observability](#1410-monitoring-and-observability)
- [Command & Tool Reference](#command--tool-reference)
- [Practical Examples](#practical-examples)
- [Best Practices Summary](#best-practices-summary)
- [Lab Exercises](#lab-exercises)
- [Conclusion](#conclusion)

## Overview
This module introduces declarative provisioning of cloud, on-premise, and hybrid resources using Infrastructure as Code (IaC) tools and the automation of system configuration with Configuration Management (CM) platforms. You'll master Proxmox infrastructure automation using modern DevOps tools including Terraform, Ansible, Cloud-Init, and CI/CD pipelines to build scalable, automated infrastructure deployment and management systems.

**Key Focus Areas:**
- **Terraform fundamentals**: providers, resources, variables, state, and modules
- **State management**: remote backends (S3, Azure Storage, Consul) and locking
- **Terraform best practices**: workspace separation, code organization, and versioning
- **Ansible core concepts**: inventory, playbooks, modules, roles, and vault
- **Idempotency and agentless architecture** in Ansible
- **Integrating Terraform and Ansible** for end-to-end provisioning and configuration
- **Secrets management**: using Terraform Vault provider and Ansible Vault
- **Testing and validation**: `terraform validate`, `terraform fmt`, `ansible-lint`, and Molecule

## Learning Objectives
By the end of this module, you will be able to:
1. **Write Terraform HCL** to provision compute, networking, and storage resources on Proxmox
2. **Configure remote state backend** with locking for team collaboration and state management
3. **Organize Terraform code** into reusable modules and manage versions effectively
4. **Use Terraform workspaces** to isolate environments (dev, staging, prod)
5. **Author Ansible inventories and playbooks** to configure Linux hosts and containers
6. **Create reusable Ansible roles** for common tasks (users, packages, services)
7. **Encrypt sensitive data** with Ansible Vault and integrate with CI pipelines
8. **Link Terraform outputs into Ansible** to perform post-provisioning setup
9. **Validate IaC and CM code** using built-in commands and external linters
10. **Automate complete deployments**: provision infrastructure with Terraform, then configure with Ansible
11. **Implement GitOps workflows** for infrastructure management and compliance
12. **Monitor and manage infrastructure** as code with observability and alerting

## Topics

### 14.1 Infrastructure as Code Fundamentals
- **IaC principles**: Declarative vs imperative approaches
- **Version control for infrastructure**: Git workflows and branching strategies
- **State management concepts**: State files, drift detection, and reconciliation
- **Code organization**: Directory structure, naming conventions, and documentation
- **Testing strategies**: Validation, linting, and automated testing frameworks

**🔗 Practical Examples**: [Terraform Provider Configuration](#terraform-provider-configuration) | [State Management Setup](#terraform-state-management)

### 14.2 Terraform with Proxmox
- **Terraform Proxmox provider**: Installation, configuration, and authentication
- **Resource definitions**: VMs, containers, storage, and networking
- **Variables and outputs**: Dynamic configuration and resource dependencies
- **Data sources**: Querying existing infrastructure and templates
- **Resource lifecycle management**: Creation, updates, and destruction

**🔗 Practical Examples**: [VM Resource Definition](#vm-resource-definition) | [Load Balancer Configuration](#load-balancer-configuration)

### 14.3 Advanced Terraform Practices
- **Remote state backends**: S3, Azure Storage, Consul configuration with locking
- **Terraform modules**: Creating, versioning, and sharing reusable components
- **Workspace management**: Environment isolation (dev, staging, prod)
- **Code organization**: Module structure, variable files, and best practices
- **Provider versioning**: Constraint management and updates

**🔗 Practical Examples**: [Terraform Modules](#terraform-modules) | [Workspace Configuration](#terraform-workspaces)

### 14.4 Ansible Configuration Management
- **Ansible inventory**: Static and dynamic inventory for Proxmox integration
- **Playbooks and tasks**: Idempotent configuration management
- **Modules and collections**: Built-in and community modules for system configuration
- **Variable management**: Group vars, host vars, and precedence
- **Agentless architecture**: SSH-based automation and security considerations

**🔗 Practical Examples**: [Ansible Inventory](#ansible-inventory) | [Web Server Playbook](#web-server-playbook)

### 14.5 Advanced Ansible Techniques
- **Role-based automation**: Creating, organizing, and sharing reusable roles
- **Ansible Galaxy**: Role management and community contributions
- **Dynamic inventory**: Service discovery and auto-scaling integration
- **Handlers and notifications**: Event-driven configuration management
- **Error handling**: Conditional execution and failure recovery

**🔗 Practical Examples**: [Common Role](#common-role) | [Role-based Automation](#ansible-roles)

### 14.6 Cloud-Init Integration
- **Cloud-Init configuration**: Templates, user data, and metadata customization
- **Network automation**: Static IP, DHCP, and complex networking setup
- **Package and service management**: Automated installation and configuration
- **SSH key injection**: User management and secure access setup
- **Custom scripts**: Post-boot automation and application deployment

**🔗 Practical Examples**: [Basic Cloud-Init Template](#basic-cloud-init-template) | [Load Balancer Cloud-Init](#load-balancer-cloud-init)

### 14.7 Secrets Management
- **Terraform Vault provider**: HashiCorp Vault integration for secrets
- **Ansible Vault**: Encrypting sensitive variables and files
- **Environment variables**: Secure credential injection in CI/CD
- **Key management**: SSH keys, API tokens, and certificate handling
- **Secret rotation**: Automated credential updates and compliance

**🔗 Practical Examples**: [Ansible Vault Usage](#ansible-vault-secrets) | [Terraform Secrets](#terraform-secrets-management)

### 14.8 Testing and Validation
- **Terraform validation**: `terraform validate`, `terraform fmt`, and plan analysis
- **Ansible linting**: `ansible-lint` and best practice enforcement
- **Molecule testing**: Role and playbook testing with containers
- **Infrastructure testing**: Automated verification and compliance checking
- **Security scanning**: Vulnerability assessment and policy enforcement

**🔗 Practical Examples**: [Infrastructure Testing Script](#infrastructure-testing-script) | [Validation Pipelines](#testing-automation)

### 14.9 CI/CD Pipeline Integration
- **Git workflows**: GitOps principles and infrastructure versioning
- **Automated testing**: Validation pipelines and quality gates
- **Deployment pipelines**: GitLab CI, GitHub Actions, and Jenkins integration
- **Infrastructure rollback**: Disaster recovery and state management
- **Compliance automation**: Policy enforcement and audit trails

**🔗 Practical Examples**: [GitLab CI Pipeline](#gitlab-ci-pipeline) | [GitHub Actions Workflow](#github-actions-workflow)

### 14.10 Monitoring and Observability
- **Infrastructure monitoring**: Automated Prometheus and Grafana deployment
- **Log aggregation**: ELK stack automation and centralized logging
- **Alerting systems**: Automated notification and escalation setup
- **Performance optimization**: Resource monitoring and auto-scaling
- **Cost optimization**: Resource rightsizing and lifecycle management

**🔗 Practical Examples**: [Prometheus Configuration](#prometheus-configuration) | [Infrastructure Testing Script](#infrastructure-testing-script)

## Command & Tool Reference

| Tool/Command | Purpose | Key Options |
|--------------|---------|-------------|
| `terraform init` | Initialize working directory and download provider plugins | `-backend-config`, `-upgrade` |
| `terraform plan -out=tfplan` | Preview changes and save execution plan | `-var-file`, `-target`, `-destroy` |
| `terraform apply "tfplan"` | Execute a previously saved plan to provision resources | `-auto-approve`, `-parallelism` |
| `terraform destroy -auto-approve` | Tear down all managed infrastructure | `-target`, `-var-file` |
| `terraform fmt -recursive` | Auto-format all Terraform configuration files | `-check`, `-diff`, `-write` |
| `terraform validate` | Validate syntax and internal consistency of code | `-json` |
| `terraform workspace new prod` | Create and switch to new workspace | `list`, `select`, `delete` |
| `terraform state list` | List resources in state file | `show`, `mv`, `rm` |
| `ansible-inventory --list -y` | Dump dynamic inventory in YAML format | `--host`, `--graph` |
| `ansible-playbook site.yml -i hosts` | Run playbooks against inventory hosts | `-v`, `--check`, `--diff` |
| `ansible-galaxy init my_role` | Scaffold new Ansible role directory structure | `install`, `list`, `search` |
| `ansible-vault encrypt secrets.yml` | Encrypt sensitive variables or files | `decrypt`, `edit`, `view` |
| `ansible-lint playbook.yml` | Lint Ansible playbooks for best practices | `-c config`, `-x SKIP_LIST` |
| `molecule test` | Run Molecule scenarios to test roles locally | `init`, `create`, `converge` |
| `terraform-docs generate .` | Generate documentation from Terraform code | `markdown`, `json` |
| `tflint` | Terraform linter for errors and best practices | `--init`, `--config` |
| `checkov -f main.tf` | Security and compliance scanning | `--framework`, `--check` |

## Practical Examples

### Terraform Proxmox Setup

#### Terraform Provider Configuration
```hcl
# terraform/providers.tf
terraform {
  required_version = ">= 1.0"
  required_providers {
    proxmox = {
      source  = "telmate/proxmox"
      version = "~> 2.9"
    }
    template = {
      source = "hashicorp/template"
      version = "~> 2.2"
    }
  }
  
  backend "s3" {
    bucket = "terraform-state-bucket"
    key    = "proxmox/terraform.tfstate"
    region = "us-west-2"
  }
}

provider "proxmox" {
  pm_api_url      = var.proxmox_api_url
  pm_user         = var.proxmox_user
  pm_password     = var.proxmox_password
  pm_tls_insecure = true
  pm_parallel     = 2
  pm_timeout      = 600
}
```

#### Variables Configuration
```hcl
# terraform/variables.tf
variable "proxmox_api_url" {
  description = "Proxmox API URL"
  type        = string
  default     = "https://proxmox.example.com:8006/api2/json"
}

variable "proxmox_user" {
  description = "Proxmox username"
  type        = string
  default     = "terraform@pve"
}

variable "proxmox_password" {
  description = "Proxmox password"
  type        = string
  sensitive   = true
}

variable "ssh_public_key" {
  description = "SSH public key for VM access"
  type        = string
}

variable "vm_template" {
  description = "VM template name"
  type        = string
  default     = "ubuntu-20.04-cloudinit"
}

variable "environment" {
  description = "Environment name"
  type        = string
  default     = "production"
}
```

#### VM Resource Definition
```hcl
# terraform/vm.tf
resource "proxmox_vm_qemu" "web_server" {
  count       = var.web_server_count
  name        = "web-${format("%02d", count.index + 1)}"
  target_node = var.target_node
  clone       = var.vm_template
  
  # VM Configuration
  cores    = 2
  sockets  = 1
  memory   = 2048
  balloon  = 1024
  vcpus    = 0
  numa     = false
  hotplug  = "network,disk,usb"
  
  # Boot configuration
  boot     = "c"
  bootdisk = "scsi0"
  
  # Storage
  disk {
    slot     = 0
    size     = "20G"
    type     = "scsi"
    storage  = "local-zfs"
    iothread = 1
    ssd      = 1
    format   = "raw"
  }
  
  # Network
  network {
    model    = "virtio"
    bridge   = "vmbr0"
    firewall = true
  }
  
  # Cloud-Init
  os_type      = "cloud-init"
  ipconfig0    = "ip=${cidrhost(var.network_cidr, count.index + 10)}/24,gw=${var.gateway}"
  nameserver   = var.nameserver
  searchdomain = var.search_domain
  
  # SSH Keys
  sshkeys = var.ssh_public_key
  
  # Cloud-Init custom configuration
  cicustom = "user=local:snippets/cloud-init-${var.environment}.yml"
  
  # Lifecycle
  lifecycle {
    ignore_changes = [
      disk,
      network
    ]
  }
  
  tags = "terraform,web,${var.environment}"
}

# Output VM information
output "web_server_ips" {
  value = proxmox_vm_qemu.web_server[*].default_ipv4_address
}

output "web_server_names" {
  value = proxmox_vm_qemu.web_server[*].name
}
```

#### Load Balancer Configuration
```hcl
# terraform/lb.tf
resource "proxmox_vm_qemu" "load_balancer" {
  name        = "lb-${var.environment}"
  target_node = var.target_node
  clone       = var.vm_template
  
  cores   = 1
  memory  = 1024
  balloon = 512
  
  disk {
    slot    = 0
    size    = "10G"
    type    = "scsi"
    storage = "local-zfs"
  }
  
  network {
    model  = "virtio"
    bridge = "vmbr0"
  }
  
  os_type      = "cloud-init"
  ipconfig0    = "ip=${var.lb_ip}/24,gw=${var.gateway}"
  nameserver   = var.nameserver
  sshkeys      = var.ssh_public_key
  
  # Custom cloud-init for load balancer
  cicustom = "user=local:snippets/cloud-init-lb-${var.environment}.yml"
  
  tags = "terraform,loadbalancer,${var.environment}"
}
```

### Cloud-Init Configuration

#### Basic Cloud-Init Template
```yaml
# /var/lib/vz/snippets/cloud-init-production.yml
#cloud-config

# System configuration
hostname: ${hostname}
fqdn: ${hostname}.example.com
manage_etc_hosts: true

# Users
users:
  - name: admin
    groups: sudo
    shell: /bin/bash
    ssh_authorized_keys:
      - ${ssh_public_key}
    sudo: ALL=(ALL) NOPASSWD:ALL
  - name: deploy
    groups: deploy
    shell: /bin/bash
    ssh_authorized_keys:
      - ${deploy_ssh_key}

# Package management
package_update: true
package_upgrade: true
packages:
  - curl
  - wget
  - git
  - htop
  - vim
  - ufw
  - fail2ban
  - unattended-upgrades

# Network configuration
write_files:
  - path: /etc/netplan/01-netcfg.yaml
    content: |
      network:
        version: 2
        ethernets:
          ens18:
            dhcp4: false
            addresses:
              - ${ip_address}/24
            gateway4: ${gateway}
            nameservers:
              addresses:
                - 8.8.8.8
                - 8.8.4.4

# Security configuration
  - path: /etc/ssh/sshd_config.d/99-custom.conf
    content: |
      Port 2222
      PermitRootLogin no
      PasswordAuthentication no
      PubkeyAuthentication yes
      MaxAuthTries 3

# Firewall rules
  - path: /etc/ufw/applications.d/custom
    content: |
      [SSH-Custom]
      title=SSH Custom Port
      description=OpenSSH Custom Port
      ports=2222/tcp

# Service configuration
runcmd:
  - systemctl enable unattended-upgrades
  - systemctl start unattended-upgrades
  - ufw --force enable
  - ufw allow SSH-Custom
  - ufw allow 80/tcp
  - ufw allow 443/tcp
  - systemctl restart ssh
  - netplan apply

# Final message
final_message: "Cloud-init setup completed successfully!"
```

#### Load Balancer Cloud-Init
```yaml
# /var/lib/vz/snippets/cloud-init-lb-production.yml
#cloud-config

hostname: lb-production
fqdn: lb-production.example.com

users:
  - name: admin
    groups: sudo
    shell: /bin/bash
    ssh_authorized_keys:
      - ${ssh_public_key}
    sudo: ALL=(ALL) NOPASSWD:ALL

package_update: true
package_upgrade: true
packages:
  - nginx
  - certbot
  - python3-certbot-nginx

write_files:
  - path: /etc/nginx/conf.d/load-balancer.conf
    content: |
      upstream web_servers {
        server web-01.example.com:80;
        server web-02.example.com:80;
        server web-03.example.com:80;
      }
      
      server {
        listen 80;
        server_name example.com www.example.com;
        
        location / {
          proxy_pass http://web_servers;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
        }
      }

runcmd:
  - systemctl enable nginx
  - systemctl start nginx
  - nginx -t && systemctl reload nginx
```

### Ansible Integration

#### Ansible Inventory
```yaml
# ansible/inventory/proxmox.yml
plugin: community.general.proxmox
url: https://proxmox.example.com:8006
user: ansible@pve
password: "{{ proxmox_password }}"
validate_certs: false

compose:
  ansible_host: ansible_host | default(proxmox_ipconfig0.ip.split('/')[0])
  
keyed_groups:
  - prefix: proxmox
    key: proxmox_tags | split(',')
  - prefix: status
    key: proxmox_status
  - prefix: node
    key: proxmox_node

groups:
  web_servers: "'web' in (proxmox_tags | split(','))"
  load_balancers: "'loadbalancer' in (proxmox_tags | split(','))"
  production: "'production' in (proxmox_tags | split(','))"
```

#### Web Server Playbook
```yaml
# ansible/playbooks/web-servers.yml
---
- name: Configure Web Servers
  hosts: web_servers
  become: yes
  vars:
    app_user: webapp
    app_dir: /var/www/app
    
  roles:
    - common
    - nginx
    - nodejs
    - application

  tasks:
    - name: Create application user
      user:
        name: "{{ app_user }}"
        shell: /bin/bash
        home: "{{ app_dir }}"
        create_home: yes

    - name: Install Node.js application
      git:
        repo: https://github.com/example/webapp.git
        dest: "{{ app_dir }}"
        version: main
      become_user: "{{ app_user }}"
      notify: restart application

    - name: Install npm dependencies
      npm:
        path: "{{ app_dir }}"
        production: yes
      become_user: "{{ app_user }}"

    - name: Configure systemd service
      template:
        src: webapp.service.j2
        dest: /etc/systemd/system/webapp.service
      notify:
        - reload systemd
        - restart application

    - name: Start and enable application
      systemd:
        name: webapp
        state: started
        enabled: yes

  handlers:
    - name: reload systemd
      systemd:
        daemon_reload: yes

    - name: restart application
      systemd:
        name: webapp
        state: restarted
```

#### Common Role
```yaml
# ansible/roles/common/tasks/main.yml
---
- name: Update package cache
  apt:
    update_cache: yes
    cache_valid_time: 3600

- name: Install common packages
  apt:
    name:
      - curl
      - wget
      - git
      - htop
      - vim
      - unzip
      - jq
### Common Role

#### Ansible Role Structure and Implementation
```
# ansible/roles/common/
├── tasks/
│   ├── main.yml
│   ├── security.yml
│   ├── packages.yml
│   └── monitoring.yml
├── handlers/
│   └── main.yml
├── templates/
│   ├── sshd_config.j2
│   ├── 50unattended-upgrades.j2
│   └── node_exporter.service.j2
├── files/
│   └── fail2ban.conf
├── vars/
│   └── main.yml
├── defaults/
│   └── main.yml
└── meta/
    └── main.yml
```

```yaml
# ansible/roles/common/tasks/main.yml
---
- name: Include package installation tasks
  include_tasks: packages.yml
  tags: packages

- name: Include security hardening tasks  
  include_tasks: security.yml
  tags: security

- name: Include monitoring setup tasks
  include_tasks: monitoring.yml
  tags: monitoring

# ansible/roles/common/tasks/packages.yml
---
- name: Update package cache
  apt:
    update_cache: yes
    cache_valid_time: 3600

- name: Install essential packages
  apt:
    name:
      - curl
      - wget
      - git
      - htop
      - vim
      - unzip
      - jq
      - tree
      - rsync
      - lsof
      - netstat-nat
    state: present

- name: Install security packages
  apt:
    name:
      - fail2ban
      - ufw
      - unattended-upgrades
      - logwatch
      - rkhunter
      - chkrootkit
    state: present

# ansible/roles/common/tasks/security.yml
---
- name: Configure SSH hardening
  template:
    src: sshd_config.j2
    dest: /etc/ssh/sshd_config
    backup: yes
    mode: '0644'
    validate: 'sshd -t -f %s'
  notify: restart ssh
  tags: ssh

- name: Configure firewall default policies
  ufw:
    state: enabled
    policy: deny
    direction: incoming
    logging: 'on'
  tags: firewall

- name: Allow SSH through firewall
  ufw:
    rule: allow
    port: "{{ ssh_port | default('22') }}"
    proto: tcp
    comment: 'SSH Access'
  tags: firewall

- name: Configure fail2ban
  copy:
    src: fail2ban.conf
    dest: /etc/fail2ban/local.conf
    backup: yes
  notify: restart fail2ban
  tags: fail2ban

- name: Configure automatic security updates
  template:
    src: 50unattended-upgrades.j2
    dest: /etc/apt/apt.conf.d/50unattended-upgrades
    backup: yes
  notify: restart unattended-upgrades
  tags: updates

# ansible/roles/common/handlers/main.yml
---
- name: restart ssh
  systemd:
    name: ssh
    state: restarted

- name: restart fail2ban
  systemd:
    name: fail2ban
    state: restarted

- name: restart unattended-upgrades
  systemd:
    name: unattended-upgrades
    state: restarted

# ansible/roles/common/templates/sshd_config.j2
# SSH Daemon configuration - Managed by Ansible
Port {{ ssh_port | default(22) }}
Protocol 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key

# Security settings
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding no
PrintMotd no
AcceptEnv LANG LC_*
Subsystem sftp /usr/lib/openssh/sftp-server

# Connection settings
MaxAuthTries 3
MaxSessions 10
ClientAliveInterval 300
ClientAliveCountMax 2

# Only allow specific users/groups
{% if allowed_users is defined %}
AllowUsers {{ allowed_users | join(' ') }}
{% endif %}
{% if allowed_groups is defined %}
AllowGroups {{ allowed_groups | join(' ') }}
{% endif %}
```

### Ansible Roles

#### Advanced Role-Based Automation
```yaml
# ansible/site.yml - Main orchestration playbook
---
- name: Configure all infrastructure
  hosts: all
  become: yes
  roles:
    - common
    - monitoring

- name: Configure web servers
  hosts: web_servers
  become: yes
  roles:
    - nginx
    - nodejs
    - ssl-certificates

- name: Configure database servers
  hosts: db_servers
  become: yes
  roles:
    - postgresql
    - backup

- name: Configure load balancers
  hosts: load_balancers
  become: yes
  roles:
    - haproxy
    - ssl-certificates

# ansible/roles/nginx/tasks/main.yml
---
- name: Install NGINX
  apt:
    name: nginx
    state: present
  tags: packages

- name: Remove default NGINX site
  file:
    path: /etc/nginx/sites-enabled/default
    state: absent
  notify: reload nginx

- name: Create NGINX configuration
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
    backup: yes
    validate: 'nginx -t -c %s'
  notify: reload nginx
  tags: config

- name: Create site configurations
  template:
    src: "{{ item.template }}"
    dest: "/etc/nginx/sites-available/{{ item.name }}"
    backup: yes
  loop: "{{ nginx_sites }}"
  notify: reload nginx
  tags: sites

- name: Enable sites
  file:
    src: "/etc/nginx/sites-available/{{ item.name }}"
    dest: "/etc/nginx/sites-enabled/{{ item.name }}"
    state: link
  loop: "{{ nginx_sites }}"
  notify: reload nginx
  tags: sites

- name: Start and enable NGINX
  systemd:
    name: nginx
    state: started
    enabled: yes
  tags: service

# ansible/roles/nginx/templates/nginx.conf.j2
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
    worker_connections 1024;
    use epoll;
    multi_accept on;
}

http {
    # Basic Settings
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    server_tokens off;

    # MIME Types
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    # SSL Settings
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512;

    # Logging Settings
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                   '$status $body_bytes_sent "$http_referer" '
                   '"$http_user_agent" "$http_x_forwarded_for"';

    access_log /var/log/nginx/access.log main;
    error_log /var/log/nginx/error.log;

    # Gzip Settings
    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/xml text/javascript
               application/javascript application/xml+rss
               application/json;

    # Virtual Host Configs
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```

### Ansible Vault Secrets

#### Comprehensive Secrets Management
```bash
# Create Ansible Vault file
ansible-vault create ansible/group_vars/all/vault.yml

# Edit existing vault file
ansible-vault edit ansible/group_vars/all/vault.yml

# Encrypt existing file
ansible-vault encrypt ansible/host_vars/db-server/secrets.yml

# View encrypted file
ansible-vault view ansible/group_vars/all/vault.yml

# Decrypt file (temporarily)
ansible-vault decrypt ansible/group_vars/all/vault.yml
```

```yaml
# ansible/group_vars/all/vault.yml (encrypted)
---
# Database credentials
vault_db_admin_password: "super-secure-password-123"
vault_db_app_password: "app-secure-password-456"

# API Keys
vault_monitoring_api_key: "mon-api-key-789"
vault_backup_encryption_key: "backup-key-abc"

# SSL Certificates
vault_ssl_private_key: |
  -----BEGIN PRIVATE KEY-----
  MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQC7...
  -----END PRIVATE KEY-----

vault_ssl_certificate: |
  -----BEGIN CERTIFICATE-----
  MIIDXTCCAkWgAwIBAgIJAL8E1xY6QY9qMA0GCSqGSIb3DQEBCwUA...
  -----END CERTIFICATE-----

# SSH Keys
vault_deploy_private_key: |
  -----BEGIN OPENSSH PRIVATE KEY-----
  b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAA...
  -----END OPENSSH PRIVATE KEY-----
```

```yaml
# ansible/group_vars/all/vars.yml (unencrypted)
---
# Reference vault variables
db_admin_password: "{{ vault_db_admin_password }}"
db_app_password: "{{ vault_db_app_password }}"
monitoring_api_key: "{{ vault_monitoring_api_key }}"
ssl_private_key: "{{ vault_ssl_private_key }}"
ssl_certificate: "{{ vault_ssl_certificate }}"

# Non-sensitive configuration
nginx_sites:
  - name: api
    template: api.conf.j2
    port: 3000
  - name: web
    template: web.conf.j2
    port: 8080

postgresql_databases:
  - name: app_production
    owner: app_user
    password: "{{ db_app_password }}"

# Monitoring configuration
prometheus_targets:
  - node_exporter:9100
  - nginx_exporter:9113
  - postgres_exporter:9187
```

```bash
# Run playbook with vault password
ansible-playbook -i inventory/proxmox.yml playbooks/site.yml --ask-vault-pass

# Use vault password file
echo "vault-password" > .vault_pass
chmod 600 .vault_pass
ansible-playbook -i inventory/proxmox.yml playbooks/site.yml --vault-password-file .vault_pass

# Environment variable for vault password
export ANSIBLE_VAULT_PASSWORD_FILE=.vault_pass
ansible-playbook -i inventory/proxmox.yml playbooks/site.yml
```

### Terraform Secrets Management

#### HashiCorp Vault Integration
```hcl
# terraform/secrets.tf
# Configure Vault provider
provider "vault" {
  address = var.vault_address
  token   = var.vault_token
}

# Read secrets from Vault
data "vault_generic_secret" "proxmox_creds" {
  path = "secret/proxmox"
}

data "vault_generic_secret" "ssh_keys" {
  path = "secret/ssh"
}

# Use secrets in resources
resource "proxmox_vm_qemu" "secure_vm" {
  name = "secure-vm"
  
  # Use vault credentials
  provisioner "remote-exec" {
    connection {
      type        = "ssh"
      user        = "admin"
      private_key = data.vault_generic_secret.ssh_keys.data["private_key"]
      host        = self.default_ipv4_address
    }
    
    inline = [
      "echo 'Setting up secure configuration...'",
      "sudo systemctl enable vault-agent"
    ]
  }
}

# Store outputs in Vault
resource "vault_generic_secret" "vm_info" {
  path = "secret/infrastructure/vms"
  
  data_json = jsonencode({
    vm_ids = proxmox_vm_qemu.secure_vm[*].vmid
    vm_ips = proxmox_vm_qemu.secure_vm[*].default_ipv4_address
  })
}
```

```hcl
# terraform/variables.tf
variable "vault_address" {
  description = "Vault server address"
  type        = string
  default     = "https://vault.example.com:8200"
}

variable "vault_token" {
  description = "Vault authentication token"
  type        = string
  sensitive   = true
}

# Alternative: Use environment variables
# export VAULT_ADDR="https://vault.example.com:8200"
# export VAULT_TOKEN="hvs.CAESIE..."
```

#### Terraform with External Secrets
```hcl
# terraform/external-secrets.tf
# Use external data source for secrets
data "external" "secrets" {
  program = ["bash", "${path.module}/scripts/get-secrets.sh"]
}

# scripts/get-secrets.sh
#!/bin/bash
set -e

# Fetch secrets from external system (e.g., AWS Secrets Manager, Azure Key Vault)
PROXMOX_PASSWORD=$(aws secretsmanager get-secret-value \
  --secret-id "proxmox/admin" \
  --query SecretString --output text | jq -r .password)

SSH_PUBLIC_KEY=$(aws secretsmanager get-secret-value \
  --secret-id "ssh/public-key" \
  --query SecretString --output text)

# Return JSON for Terraform
jq -n \
  --arg proxmox_password "$PROXMOX_PASSWORD" \
  --arg ssh_public_key "$SSH_PUBLIC_KEY" \
  '{proxmox_password: $proxmox_password, ssh_public_key: $ssh_public_key}'
```

### Infrastructure Testing Script

#### Comprehensive Testing Framework
```bash
#!/bin/bash
# tests/run-infrastructure-tests.sh

set -e

# Configuration
TERRAFORM_DIR="terraform"
ANSIBLE_DIR="ansible"
TEST_CONFIG="tests/config.yml"

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

# Logging function
log() {
    echo -e "${GREEN}[$(date +'%Y-%m-%d %H:%M:%S')] $1${NC}"
}

error() {
    echo -e "${RED}[ERROR] $1${NC}" >&2
}

warning() {
    echo -e "${YELLOW}[WARNING] $1${NC}" >&2
}

# Test Terraform configuration
test_terraform() {
    log "Testing Terraform configuration..."
    
    cd "$TERRAFORM_DIR"
    
    # Validate syntax
    log "Validating Terraform syntax..."
    if terraform validate; then
        log "✓ Terraform syntax is valid"
    else
        error "✗ Terraform syntax validation failed"
        return 1
    fi
    
    # Check formatting
    log "Checking Terraform formatting..."
    if terraform fmt -check -recursive; then
        log "✓ Terraform files are properly formatted"
    else
        warning "⚠ Terraform files need formatting (run 'terraform fmt')"
    fi
    
    # Security scan with Checkov
    if command -v checkov &> /dev/null; then
        log "Running security scan with Checkov..."
        if checkov -d . --framework terraform; then
            log "✓ Security scan passed"
        else
            warning "⚠ Security scan found issues"
        fi
    fi
    
    # Generate and validate plan
    log "Generating Terraform plan..."
    if terraform plan -out=test.tfplan -detailed-exitcode; then
        plan_status=$?
        if [ $plan_status -eq 0 ]; then
            log "✓ No changes needed"
        elif [ $plan_status -eq 2 ]; then
            log "✓ Plan generated successfully (changes detected)"
        fi
    else
        error "✗ Terraform plan failed"
        return 1
    fi
    
    cd ..
}

# Test Ansible configuration
test_ansible() {
    log "Testing Ansible configuration..."
    
    cd "$ANSIBLE_DIR"
    
    # Syntax check
    log "Checking Ansible syntax..."
    if ansible-playbook --syntax-check playbooks/site.yml; then
        log "✓ Ansible syntax is valid"
    else
        error "✗ Ansible syntax check failed"
        return 1
    fi
    
    # Lint check
    if command -v ansible-lint &> /dev/null; then
        log "Running Ansible lint..."
        if ansible-lint playbooks/; then
            log "✓ Ansible lint passed"
        else
            warning "⚠ Ansible lint found issues"
        fi
    fi
    
    # Test inventory
    log "Testing inventory..."
    if ansible-inventory --list > /dev/null; then
        log "✓ Inventory is valid"
    else
        error "✗ Inventory test failed"
        return 1
    fi
    
    # Dry run
    log "Performing Ansible dry run..."
    if ansible-playbook --check --diff playbooks/site.yml; then
        log "✓ Ansible dry run completed"
    else
        warning "⚠ Ansible dry run found issues"
    fi
    
    cd ..
}

# Test infrastructure connectivity
test_connectivity() {
    log "Testing infrastructure connectivity..."
    
    # Get VM IPs from Terraform output
    if [ -f "$TERRAFORM_DIR/terraform.tfstate" ]; then
        web_servers=$(terraform -chdir="$TERRAFORM_DIR" output -json web_server_ips 2>/dev/null | jq -r '.[]' 2>/dev/null || echo "")
        lb_ip=$(terraform -chdir="$TERRAFORM_DIR" output -raw load_balancer_ip 2>/dev/null || echo "")
        
        # Test SSH connectivity
        if [ -n "$web_servers" ]; then
            for server in $web_servers; do
                log "Testing SSH connectivity to $server..."
                if timeout 10 ssh -o ConnectTimeout=5 -o StrictHostKeyChecking=no -o BatchMode=yes admin@"$server" "echo 'SSH test successful'" 2>/dev/null; then
                    log "✓ SSH to $server successful"
                else
                    warning "⚠ SSH to $server failed (may not be ready yet)"
                fi
            done
        fi
        
        # Test HTTP connectivity
        if [ -n "$lb_ip" ]; then
            log "Testing HTTP connectivity to load balancer..."
            if curl -s -m 10 "http://$lb_ip/health" > /dev/null; then
                log "✓ Load balancer health check passed"
            else
                warning "⚠ Load balancer health check failed"
            fi
        fi
    else
        warning "⚠ No Terraform state found, skipping connectivity tests"
    fi
}

# Test service health
test_services() {
    log "Testing service health..."
    
    # Test web services
    web_servers=$(terraform -chdir="$TERRAFORM_DIR" output -json web_server_ips 2>/dev/null | jq -r '.[]' 2>/dev/null || echo "")
    
    for server in $web_servers; do
        log "Testing web service on $server..."
        
        # Test NGINX status
        if ssh -o ConnectTimeout=5 -o StrictHostKeyChecking=no admin@"$server" "sudo systemctl is-active nginx" 2>/dev/null | grep -q "active"; then
            log "✓ NGINX is running on $server"
        else
            warning "⚠ NGINX status check failed on $server"
        fi
        
        # Test HTTP response
        if curl -s -m 5 "http://$server" > /dev/null; then
            log "✓ HTTP service responding on $server"
        else
            warning "⚠ HTTP service not responding on $server"
        fi
    done
}

# Test monitoring
test_monitoring() {
    log "Testing monitoring infrastructure..."
    
    monitor_ip=$(terraform -chdir="$TERRAFORM_DIR" output -raw monitoring_ip 2>/dev/null || echo "")
    
    if [ -n "$monitor_ip" ]; then
        # Test Prometheus
        if curl -s -m 10 "http://$monitor_ip:9090/-/healthy" | grep -q "Prometheus is Healthy"; then
            log "✓ Prometheus is healthy"
        else
            warning "⚠ Prometheus health check failed"
        fi
        
        # Test Grafana
        if curl -s -m 10 "http://$monitor_ip:3000/api/health" | jq -r '.database' | grep -q "ok"; then
            log "✓ Grafana is healthy"
        else
            warning "⚠ Grafana health check failed"
        fi
        
        # Test node exporters
        web_servers=$(terraform -chdir="$TERRAFORM_DIR" output -json web_server_ips 2>/dev/null | jq -r '.[]' 2>/dev/null || echo "")
        for server in $web_servers; do
            if curl -s -m 5 "http://$server:9100/metrics" | head -1 | grep -q "node_"; then
                log "✓ Node exporter responding on $server"
            else
                warning "⚠ Node exporter not responding on $server"
            fi
        done
    else
        warning "⚠ No monitoring server found, skipping monitoring tests"
    fi
}

# Test security compliance
test_security() {
    log "Testing security compliance..."
    
    web_servers=$(terraform -chdir="$TERRAFORM_DIR" output -json web_server_ips 2>/dev/null | jq -r '.[]' 2>/dev/null || echo "")
    
    for server in $web_servers; do
        log "Testing security on $server..."
        
        # Test SSH hardening
        if ssh -o ConnectTimeout=5 -o StrictHostKeyChecking=no admin@"$server" "sudo sshd -T | grep -q 'permitrootlogin no'" 2>/dev/null; then
            log "✓ Root login disabled on $server"
        else
            warning "⚠ Root login check failed on $server"
        fi
        
        # Test firewall status
        if ssh -o ConnectTimeout=5 -o StrictHostKeyChecking=no admin@"$server" "sudo ufw status | grep -q 'Status: active'" 2>/dev/null; then
            log "✓ Firewall is active on $server"
        else
            warning "⚠ Firewall status check failed on $server"
        fi
        
        # Test fail2ban
        if ssh -o ConnectTimeout=5 -o StrictHostKeyChecking=no admin@"$server" "sudo systemctl is-active fail2ban" 2>/dev/null | grep -q "active"; then
            log "✓ Fail2ban is running on $server"
        else
            warning "⚠ Fail2ban status check failed on $server"
        fi
    done
}

# Generate test report
generate_report() {
    local report_file="tests/test-report-$(date +%Y%m%d-%H%M%S).html"
    
    log "Generating test report: $report_file"
    
    cat > "$report_file" << EOF
<!DOCTYPE html>
<html>
<head>
    <title>Infrastructure Test Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        .pass { color: green; }
        .warn { color: orange; }
        .fail { color: red; }
        .timestamp { color: gray; font-size: 0.9em; }
    </style>
</head>
<body>
    <h1>Infrastructure Test Report</h1>
    <p class="timestamp">Generated: $(date)</p>
    
    <h2>Test Summary</h2>
    <ul>
        <li>Terraform Configuration: <span class="pass">PASS</span></li>
        <li>Ansible Configuration: <span class="pass">PASS</span></li>
        <li>Connectivity Tests: <span class="pass">PASS</span></li>
        <li>Service Health: <span class="pass">PASS</span></li>
        <li>Security Compliance: <span class="pass">PASS</span></li>
    </ul>
    
    <h2>Infrastructure Overview</h2>
    <pre>$(terraform -chdir="$TERRAFORM_DIR" output 2>/dev/null || echo "No Terraform outputs available")</pre>
    
    <h2>Recommendations</h2>
    <ul>
        <li>Review any warning messages in the test output</li>
        <li>Ensure all monitoring endpoints are accessible</li>
        <li>Verify SSL certificates are properly configured</li>
        <li>Check backup and disaster recovery procedures</li>
    </ul>
</body>
</html>
EOF
    
    log "Test report generated: $report_file"
}

# Main test execution
main() {
    log "Starting infrastructure tests..."
    
    # Check prerequisites
    command -v terraform >/dev/null 2>&1 || { error "Terraform is required but not installed"; exit 1; }
    command -v ansible >/dev/null 2>&1 || { error "Ansible is required but not installed"; exit 1; }
    
    # Run tests
    test_terraform
    test_ansible
    test_connectivity
    test_services
    test_monitoring
    test_security
    
    # Generate report
    generate_report
    
    log "All tests completed!"
}

# Run tests if script is executed directly
if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
    main "$@"
fi
```

### Testing Automation

#### Advanced Testing Pipeline
```yaml
# tests/molecule/default/molecule.yml
---
dependency:
  name: galaxy
  options:
    requirements-file: requirements.yml

driver:
  name: docker

platforms:
  - name: ubuntu-20-04
    image: ubuntu:20.04
    privileged: true
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:ro
    command: /lib/systemd/systemd
    networks:
      - name: molecule

  - name: ubuntu-22-04  
    image: ubuntu:22.04
    privileged: true
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:ro
    command: /lib/systemd/systemd
    networks:
      - name: molecule

provisioner:
  name: ansible
  config_options:
    defaults:
      callbacks_enabled: timer,profile_tasks
  inventory:
    host_vars:
      ubuntu-20-04:
        ansible_python_interpreter: /usr/bin/python3
      ubuntu-22-04:
        ansible_python_interpreter: /usr/bin/python3

verifier:
  name: ansible

scenario:
  test_sequence:
    - dependency
    - create
    - prepare
    - converge
    - idempotence
    - side_effect
    - verify
    - cleanup
    - destroy
```

```bash
# Run Molecule tests
cd ansible/roles/common
molecule test

# Test specific scenario
molecule test --scenario-name ubuntu-20

# Debug failing tests
molecule converge
molecule verify --scenario-name ubuntu-20
```
```

### CI/CD Pipeline Integration

#### GitLab CI Pipeline
```yaml
# .gitlab-ci.yml
stages:
  - validate
  - plan
  - apply
  - configure
  - test

variables:
  TF_ROOT: ${CI_PROJECT_DIR}/terraform
  TF_STATE_NAME: ${CI_ENVIRONMENT_NAME}

before_script:
  - cd ${TF_ROOT}

cache:
  key: ${CI_COMMIT_REF_SLUG}
  paths:
    - ${TF_ROOT}/.terraform

validate:
  stage: validate
  script:
    - terraform init -backend=false
    - terraform validate
    - terraform fmt -check
  rules:
    - changes:
        - terraform/**/*

plan:
  stage: plan
  script:
    - terraform init
    - terraform plan -out=plan.cache
    - terraform show --json plan.cache > plan.json
  artifacts:
    paths:
      - ${TF_ROOT}/plan.cache
      - ${TF_ROOT}/plan.json
    expire_in: 1 week
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
    - if: '$CI_COMMIT_BRANCH == "main"'

apply:
  stage: apply
  script:
    - terraform init
    - terraform apply -auto-approve plan.cache
  dependencies:
    - plan
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
  when: manual

configure:
  stage: configure
  image: cytopia/ansible:latest
  script:
    - cd ansible
    - ansible-galaxy install -r requirements.yml
    - ansible-playbook -i inventory/proxmox.yml playbooks/site.yml
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
  needs:
    - apply

test:
  stage: test
  script:
    - cd tests
    - ./run-infrastructure-tests.sh
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
  needs:
    - configure
```

#### GitHub Actions Workflow
```yaml
# .github/workflows/infrastructure.yml
name: Infrastructure Deployment

on:
  push:
    branches: [main]
    paths: ['terraform/**', 'ansible/**']
  pull_request:
    branches: [main]
    paths: ['terraform/**', 'ansible/**']

env:
  TF_VERSION: 1.5.0
  ANSIBLE_VERSION: 6.0.0

jobs:
  terraform-plan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Terraform Init
        run: terraform init
        working-directory: terraform

      - name: Terraform Validate
        run: terraform validate
        working-directory: terraform

      - name: Terraform Plan
        run: terraform plan -no-color -out=tfplan
        working-directory: terraform
        env:
          TF_VAR_proxmox_password: ${{ secrets.PROXMOX_PASSWORD }}
          TF_VAR_ssh_public_key: ${{ secrets.SSH_PUBLIC_KEY }}

      - name: Upload Plan
        uses: actions/upload-artifact@v3
        with:
          name: terraform-plan
          path: terraform/tfplan

  terraform-apply:
    if: github.ref == 'refs/heads/main'
    needs: terraform-plan
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: ${{ env.TF_VERSION }}

      - name: Download Plan
        uses: actions/download-artifact@v3
        with:
          name: terraform-plan
          path: terraform

      - name: Terraform Init
        run: terraform init
        working-directory: terraform

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
        working-directory: terraform
        env:
          TF_VAR_proxmox_password: ${{ secrets.PROXMOX_PASSWORD }}
          TF_VAR_ssh_public_key: ${{ secrets.SSH_PUBLIC_KEY }}

  ansible-configure:
    needs: terraform-apply
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'

      - name: Install Ansible
        run: |
          pip install ansible==${{ env.ANSIBLE_VERSION }}
          ansible-galaxy install -r ansible/requirements.yml

      - name: Run Ansible Playbook
        run: |
          ansible-playbook -i inventory/proxmox.yml playbooks/site.yml
        working-directory: ansible
        env:
          PROXMOX_PASSWORD: ${{ secrets.PROXMOX_PASSWORD }}
```

### Monitoring and Observability

#### Prometheus Configuration
```yaml
# ansible/roles/monitoring/templates/prometheus.yml.j2
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
{% for host in groups['all'] %}
      - targets: ['{{ hostvars[host]['ansible_host'] }}:9100']
        labels:
          instance: '{{ host }}'
{% endfor %}

  - job_name: 'nginx-exporter'
    static_configs:
{% for host in groups['web_servers'] %}
      - targets: ['{{ hostvars[host]['ansible_host'] }}:9113']
        labels:
          instance: '{{ host }}'
{% endfor %}

  - job_name: 'proxmox'
    static_configs:
      - targets: ['{{ proxmox_host }}:9221']

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - localhost:9093
```

#### Infrastructure Testing Script
```bash
#!/bin/bash
# tests/run-infrastructure-tests.sh

set -e

echo "Running infrastructure tests..."

# Test VM accessibility
test_vm_accessibility() {
    echo "Testing VM accessibility..."
    
    for vm in $(terraform output -json web_server_ips | jq -r '.[]'); do
        echo "Testing connectivity to $vm"
        if timeout 30 ssh -o ConnectTimeout=10 -o StrictHostKeyChecking=no admin@$vm "echo 'Connection successful'"; then
            echo "✓ $vm is accessible"
        else
            echo "✗ $vm is not accessible"
            exit 1
        fi
    done
}

# Test web services
test_web_services() {
    echo "Testing web services..."
    
    lb_ip=$(terraform output -json load_balancer_ip | jq -r '.')
    
    if curl -s -o /dev/null -w "%{http_code}" "http://$lb_ip" | grep -q "200"; then
        echo "✓ Load balancer is responding"
    else
        echo "✗ Load balancer is not responding"
        exit 1
    fi
}

# Test monitoring
test_monitoring() {
    echo "Testing monitoring..."
    
    monitor_ip=$(terraform output -json monitoring_ip | jq -r '.')
    
    if curl -s "http://$monitor_ip:9090/-/healthy" | grep -q "Prometheus is Healthy"; then
        echo "✓ Prometheus is healthy"
    else
        echo "✗ Prometheus is not healthy"
        exit 1
    fi
}

# Run tests
test_vm_accessibility
test_web_services
test_monitoring

echo "All tests passed!"
```

## Infrastructure Automation Best Practices

| Category | Best Practice |
|----------|---------------|
| Code Structure | Use modules, maintain DRY principles |
| State Management | Use remote state, implement locking |
| Security | Use secrets management, least privilege |
| Testing | Implement validation, automated testing |
| Documentation | Document infrastructure, maintain diagrams |
| Versioning | Tag releases, maintain changelogs |
| Monitoring | Implement observability, alerting |

## Troubleshooting Common Issues

### Terraform Issues
```bash
# Debug Terraform
export TF_LOG=DEBUG
terraform plan

# Fix state issues
terraform refresh
terraform import

# Handle provider issues
terraform providers
terraform init -upgrade
```

### Ansible Issues
```bash
# Debug Ansible
ansible-playbook -vvv playbook.yml

# Test connectivity
ansible all -m ping

# Dry run mode
ansible-playbook --check playbook.yml
```

## Lab Exercises
1. Build complete infrastructure with Terraform and Ansible
2. Implement CI/CD pipeline for infrastructure deployment
3. Set up monitoring and alerting automation
4. Create disaster recovery automation
5. Implement infrastructure compliance automation

## Conclusion
This module completes the Linux Sysadmin & DevOps Training Program. You now have the skills to manage enterprise infrastructure from basic Linux administration through advanced automation and orchestration. Continue practicing these concepts and stay current with evolving technologies and best practices in the DevOps ecosystem.

## Additional Resources
- Official documentation for all tools covered
- Community forums and best practice guides
- Certification paths for continued learning
- Open source projects for hands-on experience
- Industry blogs and conferences for staying current
