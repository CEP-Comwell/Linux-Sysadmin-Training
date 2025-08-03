# Module 14: Proxmox Infrastructure Automation

## Overview
This module covers infrastructure automation using Proxmox VE with modern DevOps tools including Terraform, Ansible, Cloud-Init, and CI/CD pipelines. You'll learn to build scalable, automated infrastructure deployment and management systems.

## Learning Objectives
By the end of this module, you will be able to:
- Automate Proxmox infrastructure with Terraform
- Configure VMs and containers using Ansible
- Implement Cloud-Init for automated provisioning
- Build CI/CD pipelines for infrastructure deployment
- Monitor and manage infrastructure as code
- Implement GitOps workflows for infrastructure

## Topics

### 14.1 Infrastructure as Code Concepts
- Infrastructure as Code (IaC) principles
- Declarative vs imperative approaches
- Version control for infrastructure
- State management and drift detection
- Testing and validation strategies

### 14.2 Terraform with Proxmox
- Terraform Proxmox provider setup
- Resource definitions and modules
- State management and remote backends
- Terraform workflows and best practices
- Multi-environment deployments

### 14.3 Ansible for Configuration Management
- Ansible inventory and Proxmox integration
- Playbooks for VM and container configuration
- Role-based automation
- Ansible Vault for secrets management
- Dynamic inventory and service discovery

### 14.4 Cloud-Init Integration
- Cloud-Init configuration and templates
- User data and metadata customization
- Network configuration automation
- Package installation and service setup
- SSH key injection and user management

### 14.5 CI/CD Pipeline Integration
- Git workflows for infrastructure
- Automated testing and validation
- Deployment pipelines with GitLab/GitHub
- Infrastructure rollback strategies
- Compliance and governance automation

### 14.6 Monitoring and Observability
- Infrastructure monitoring automation
- Prometheus and Grafana deployment
- Log aggregation and analysis
- Alerting and notification systems
- Performance optimization automation

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
    state: present

- name: Configure SSH hardening
  template:
    src: sshd_config.j2
    dest: /etc/ssh/sshd_config
    backup: yes
  notify: restart ssh

- name: Configure firewall
  ufw:
    state: enabled
    policy: deny
    direction: incoming

- name: Allow SSH
  ufw:
    rule: allow
    port: "{{ ssh_port | default('22') }}"
    proto: tcp

- name: Configure automatic updates
  apt:
    name: unattended-upgrades
    state: present

- name: Configure unattended upgrades
  template:
    src: 50unattended-upgrades.j2
    dest: /etc/apt/apt.conf.d/50unattended-upgrades
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
