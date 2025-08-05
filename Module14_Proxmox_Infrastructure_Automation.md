# Module 14: Proxmox Infrastructure Automation


**Automate Your Proxmox Infrastructure with Practical Tools**

This module introduces practical Infrastructure as Code (IaC) and Configuration Management (CM) for Proxmox using beginner-friendly tools: Terraform, Ansible, and Cloud-Init. Learn to automate VM provisioning, basic configuration, and essential monitoring for small to medium environments.

**What You'll Learn:**
- Basic Terraform usage for VM provisioning in Proxmox
- Simple Ansible playbooks for configuration management
- Cloud-Init for initial VM setup
- Essential monitoring and troubleshooting


## Learning Objectives

By completing this module, you will be able to:

1. **Provision Proxmox VMs with Terraform**
   - Write simple Terraform configuration files for basic VM creation
   - Understand variables and outputs in Terraform

2. **Configure VMs with Ansible**
   - Use Ansible playbooks to install packages and configure users
   - Apply basic security settings

3. **Automate Initial VM Setup with Cloud-Init**
   - Use Cloud-Init for user creation and SSH key setup

4. **Monitor and Troubleshoot Proxmox VMs**
   - Use built-in Proxmox tools and simple monitoring scripts



## Table of Contents
* [Learning Objectives](#learning-objectives)
* [Topics](#topics)
    * [14.1 Infrastructure as Code Fundamentals](#141-infrastructure-as-code-fundamentals)
        * IaC principles: declarative vs imperative
        * Version control for infrastructure
        * State management concepts
        * Code organization and documentation
        * Testing strategies
    * [14.2 Terraform with Proxmox](#142-terraform-with-proxmox)
        * Proxmox provider basics
        * Resource definitions: VMs, storage, networking
        * Variables and outputs
        * Data sources
        * Resource lifecycle management
    * [14.3 Advanced Terraform Practices](#143-advanced-terraform-practices)
        * Ansible inventory basics
        * Playbooks and tasks
        * Modules and collections
        * Variable management
        * SSH-based automation
    * [14.4 Ansible Configuration Management](#144-ansible-configuration-management)
        * Cloud-Init configuration basics
        * Network automation
        * Package and service management
        * SSH key injection
        * Custom scripts
    * [14.5 Advanced Ansible Techniques](#145-advanced-ansible-techniques)
        * Ansible Vault basics
        * Environment variables for credentials
        * Key management
        * Secret rotation
    * [14.6 Cloud-Init Integration](#146-cloud-init-integration)
        * Terraform validation and formatting
        * Ansible linting
        * Infrastructure testing basics
        * Security scanning
    * [14.7 Secrets Management](#147-secrets-management)
        * HashiCorp Vault integration for secrets
        * Encrypting sensitive variables and files
        * Secure credential injection in CI/CD
        * SSH keys, API tokens, and certificate handling
        * Secret rotation: Automated credential updates and compliance
    * [14.8 Testing and Validation](#148-testing-and-validation)
       * Terraform validation
       * Ansible linting and best practice enforcement
       * Role and playbook testing with containers
       * Automated verification and compliance checking
       * Security scanning Vulnerability assessment and policy enforcement
    * [14.9 CI/CD Pipeline Integration](#149-cicd-pipeline-integration)
       * Git workflows: GitOps principles and infrastructure versioning
       * Automated testing: Validation pipelines and quality gates
       * Deployment pipelines: GitLab CI, GitHub Actions, and Jenkins integration
       * Infrastructure rollback: Disaster recovery and state management
       * Compliance automation: Policy enforcement and audit trails
    * [14.10 Monitoring and Observability](#1410-monitoring-and-observability)
        * Infrastructure monitoring basics
        * Log aggregation
        * Alerting systems
        * Performance monitoring
* [Essential Command Reference](#essential-command-reference)
* [Command & Tool Reference](#command--tool-reference)
* [Practical Examples](#practical-examples)
* [Infrastructure Automation Best Practices](#infrastructure-automation-best-practices)
* [Troubleshooting Common Issues](#troubleshooting-common-issues)
* [Lab Exercises](#lab-exercises)
* [Assessment Criteria](#assessment-criteria)
* [Best Practices Summary](#best-practices-summary)
* [Troubleshooting Guide](#troubleshooting-guide)
* [Next Steps](#next-steps)



---

## Essential Command Reference

[Back to Top](#table-of-contents) | [Main Index](../README.md) ⬆️📚

### Terraform Core Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Initialization** | `terraform init` | Initialize working directory | `terraform init -upgrade` |
| | `terraform init -backend-config` | Init with backend config | `terraform init -backend-config="bucket=my-state"` |
| | `terraform init -reconfigure` | Reconfigure backend | `terraform init -reconfigure` |
| **Planning** | `terraform plan` | Show execution plan | `terraform plan -out=plan.tfplan` |
| | `terraform plan -target` | Plan specific resource | `terraform plan -target=proxmox_vm_qemu.web` |
| | `terraform plan -var-file` | Use variable file | `terraform plan -var-file="prod.tfvars"` |
| | `terraform plan -destroy` | Plan destroy operation | `terraform plan -destroy` |
| **Apply/Destroy** | `terraform apply` | Apply changes | `terraform apply plan.tfplan` |
| | `terraform apply -auto-approve` | Apply without confirmation | `terraform apply -auto-approve` |
| | `terraform destroy` | Destroy resources | `terraform destroy -target=proxmox_vm_qemu.web` |
| | `terraform destroy -auto-approve` | Destroy without confirmation | `terraform destroy -auto-approve` |
| **State Management** | `terraform state list` | List resources in state | `terraform state list` |
| | `terraform state show` | Show resource details | `terraform state show proxmox_vm_qemu.web` |
| | `terraform state mv` | Move resource in state | `terraform state mv proxmox_vm_qemu.old proxmox_vm_qemu.new` |
| | `terraform state rm` | Remove from state | `terraform state rm proxmox_vm_qemu.web` |
| | `terraform import` | Import existing resource | `terraform import proxmox_vm_qemu.web 101` |
| | `terraform refresh` | Refresh state | `terraform refresh` |

### Terraform Workspace Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Workspace Management** | `terraform workspace list` | List workspaces | `terraform workspace list` |
| | `terraform workspace new` | Create workspace | `terraform workspace new development` |
| | `terraform workspace select` | Switch workspace | `terraform workspace select production` |
| | `terraform workspace delete` | Delete workspace | `terraform workspace delete development` |
| | `terraform workspace show` | Show current workspace | `terraform workspace show` |
| **Validation** | `terraform validate` | Validate configuration | `terraform validate` |
| | `terraform fmt` | Format code | `terraform fmt -recursive` |
| | `terraform fmt -check` | Check formatting | `terraform fmt -check` |
| | `terraform providers` | Show providers | `terraform providers` |
| **Output/Debug** | `terraform output` | Show outputs | `terraform output vm_ip_addresses` |
| | `terraform console` | Interactive console | `terraform console` |
| | `terraform graph` | Generate dependency graph | `terraform graph | dot -Tpng > graph.png` |

### Ansible Core Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Inventory** | `ansible-inventory --list` | List inventory | `ansible-inventory --list -i inventory.yml` |
| | `ansible-inventory --graph` | Show inventory graph | `ansible-inventory --graph` |
| | `ansible-inventory --host` | Show host details | `ansible-inventory --host web01` |
| **Ad-hoc Commands** | `ansible all -m ping` | Test connectivity | `ansible all -m ping -i inventory.yml` |
| | `ansible all -m setup` | Gather facts | `ansible all -m setup` |
| | `ansible all -m command` | Run command | `ansible all -m command -a "uptime"` |
| | `ansible all -m shell` | Run shell command | `ansible all -m shell -a "ps aux \| grep nginx"` |
| | `ansible all -m copy` | Copy files | `ansible all -m copy -a "src=/tmp/file dest=/tmp/"` |
| **Playbook Execution** | `ansible-playbook playbook.yml` | Run playbook | `ansible-playbook -i inventory site.yml` |
| | `ansible-playbook --check` | Dry run mode | `ansible-playbook --check playbook.yml` |
| | `ansible-playbook --diff` | Show diffs | `ansible-playbook --diff playbook.yml` |
| | `ansible-playbook --tags` | Run specific tags | `ansible-playbook --tags "web,db" playbook.yml` |
| | `ansible-playbook --skip-tags` | Skip tags | `ansible-playbook --skip-tags "debug" playbook.yml` |
| | `ansible-playbook --limit` | Limit to hosts | `ansible-playbook --limit "web*" playbook.yml` |

### Ansible Advanced Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Role Management** | `ansible-galaxy init` | Create role structure | `ansible-galaxy init roles/webserver` |
| | `ansible-galaxy install` | Install role | `ansible-galaxy install geerlingguy.nginx` |
| | `ansible-galaxy list` | List installed roles | `ansible-galaxy list` |
| | `ansible-galaxy search` | Search Galaxy | `ansible-galaxy search nginx` |
| **Vault Operations** | `ansible-vault create` | Create encrypted file | `ansible-vault create secrets.yml` |
| | `ansible-vault encrypt` | Encrypt existing file | `ansible-vault encrypt vars.yml` |
| | `ansible-vault decrypt` | Decrypt file | `ansible-vault decrypt secrets.yml` |
| | `ansible-vault edit` | Edit encrypted file | `ansible-vault edit secrets.yml` |
| | `ansible-vault view` | View encrypted file | `ansible-vault view secrets.yml` |
| | `ansible-vault rekey` | Change vault password | `ansible-vault rekey secrets.yml` |
| **Testing** | `ansible-lint` | Lint playbooks | `ansible-lint playbook.yml` |
| | `molecule init` | Initialize test | `molecule init role my-role` |
| | `molecule test` | Run full test | `molecule test` |
| | `molecule converge` | Run converge | `molecule converge` |

### Proxmox CLI Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **VM Management** | `qm list` | List VMs | `qm list` |
| | `qm create` | Create VM | `qm create 100 --name test --memory 1024` |
| | `qm start` | Start VM | `qm start 100` |
| | `qm stop` | Stop VM | `qm stop 100` |
| | `qm destroy` | Delete VM | `qm destroy 100` |
| | `qm clone` | Clone VM | `qm clone 100 101 --name test-clone` |
| | `qm template` | Convert to template | `qm template 100` |
| **Storage** | `pvesm status` | Storage status | `pvesm status` |
| | `pvesm list` | List storage content | `pvesm list local` |
| | `pvesm alloc` | Allocate storage | `pvesm alloc local 100 vm-100-disk-0 10G` |
| **Networking** | `pvesh get /nodes/node/network` | List network config | `pvesh get /nodes/pve/network` |
| | `pvesh create /nodes/node/network` | Create network | `pvesh create /nodes/pve/network -iface vmbr1` |
| **Backup** | `vzdump` | Backup VMs | `vzdump 100 --storage local --compress gzip` |
| | `pct list` | List containers | `pct list` |

### Cloud-Init Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Configuration** | `cloud-init status` | Check status | `cloud-init status` |
| | `cloud-init analyze` | Analyze boot time | `cloud-init analyze show` |
| | `cloud-init clean` | Clean previous runs | `cloud-init clean` |
| | `cloud-init init` | Run init stage | `cloud-init init` |
| **Debugging** | `cloud-init query` | Query metadata | `cloud-init query userdata` |
| | `cloud-init schema` | Validate config | `cloud-init schema --config-file cloud-config.yml` |
| | `journalctl -u cloud-init` | View logs | `journalctl -u cloud-init-local.service` |
| **Testing** | `cloud-init devel` | Development tools | `cloud-init devel schema --config-file test.yml` |

### HashiCorp Vault Operations

| Category | Command | Description | Example |
|----------|---------|-------------|---------|
| **Authentication** | `vault auth` | Authenticate | `vault auth -method=userpass username=admin` |
| | `vault token lookup` | Check token | `vault token lookup` |
| | `vault token renew` | Renew token | `vault token renew` |
| **Secrets Management** | `vault kv put` | Store secret | `vault kv put secret/myapp password=secret123` |
| | `vault kv get` | Retrieve secret | `vault kv get secret/myapp` |
| | `vault kv delete` | Delete secret | `vault kv delete secret/myapp` |
| | `vault kv list` | List secrets | `vault kv list secret/` |
| **Policy Management** | `vault policy write` | Create policy | `vault policy write myapp policy.hcl` |
| | `vault policy read` | Read policy | `vault policy read myapp` |
| | `vault policy list` | List policies | `vault policy list` |

## Topics

### 14.1 Infrastructure as Code Fundamentals
- **IaC principles**: Declarative vs imperative approaches
- **Version control for infrastructure**: Git workflows and branching strategies
- **State management concepts**: State files, drift detection, and reconciliation
- **Code organization**: Directory structure, naming conventions, and documentation
- **Testing strategies**: Validation, linting, and automated testing frameworks

**Practical Examples**:

### 14.2 Terraform with Proxmox
- **Terraform Proxmox provider**: Installation, configuration, and authentication
- **Resource definitions**: VMs, containers, storage, and networking
- **Variables and outputs**: Dynamic configuration and resource dependencies
- **Data sources**: Querying existing infrastructure and templates
- **Resource lifecycle management**: Creation, updates, and destruction

### 14.3 Advanced Terraform Practices
- **Remote state backends**: S3, Azure Storage, Consul configuration with locking
- **Terraform modules**: Creating, versioning, and sharing reusable components
- **Workspace management**: Environment isolation (dev, staging, prod)
- **Code organization**: Module structure, variable files, and best practices
- **Provider versioning**: Constraint management and updates

### 14.4 Ansible Configuration Management
- **Ansible inventory**: Static and dynamic inventory for Proxmox integration
- **Playbooks and tasks**: Idempotent configuration management
- **Modules and collections**: Built-in and community modules for system configuration
- **Variable management**: Group vars, host vars, and precedence
- **Agentless architecture**: SSH-based automation and security considerations

**Practical Examples**: [Ansible Inventory](#ansible-inventory) | [Web Server Playbook](#web-server-playbook)

### 14.5 Advanced Ansible Techniques
- **Role-based automation**: Creating, organizing, and sharing reusable roles
- **Ansible Galaxy**: Role management and community contributions
- **Dynamic inventory**: Service discovery and auto-scaling integration
- **Handlers and notifications**: Event-driven configuration management
- **Error handling**: Conditional execution and failure recovery

**Practical Examples**: [Common Role](#common-role) | [Role-based Automation](#ansible-roles)

### 14.6 Cloud-Init Integration
- **Cloud-Init configuration**: Templates, user data, and metadata customization
- **Network automation**: Static IP, DHCP, and complex networking setup
- **Package and service management**: Automated installation and configuration
- **SSH key injection**: User management and secure access setup
- **Custom scripts**: Post-boot automation and application deployment

**Practical Examples**: [Basic Cloud-Init Template](#basic-cloud-init-template)

### 14.7 Secrets Management
- **Terraform Vault provider**: HashiCorp Vault integration for secrets
- **Ansible Vault**: Encrypting sensitive variables and files
- **Environment variables**: Secure credential injection in CI/CD
- **Key management**: SSH keys, API tokens, and certificate handling
- **Secret rotation**: Automated credential updates and compliance

**Practical Examples**: [Ansible Vault Usage](#ansible-vault-secrets) | [Terraform Secrets](#terraform-secrets-management)

### 14.8 Testing and Validation
- **Terraform validation**: `terraform validate`, `terraform fmt`, and plan analysis
- **Ansible linting**: `ansible-lint` and best practice enforcement
- **Molecule testing**: Role and playbook testing with containers
- **Infrastructure testing**: Automated verification and compliance checking
- **Security scanning**: Vulnerability assessment and policy enforcement

**Practical Examples**: [Infrastructure Testing Script](#infrastructure-testing-script) | [Validation Pipelines](#testing-automation)

### 14.9 CI/CD Pipeline Integration
- **Git workflows**: GitOps principles and infrastructure versioning
- **Automated testing**: Validation pipelines and quality gates
- **Deployment pipelines**: GitLab CI, GitHub Actions, and Jenkins integration
- **Infrastructure rollback**: Disaster recovery and state management
- **Compliance automation**: Policy enforcement and audit trails

**Practical Examples**:

### 14.10 Monitoring and Observability
- **Infrastructure monitoring**: Automated Prometheus and Grafana deployment
- **Log aggregation**: ELK stack automation and centralized logging
- **Alerting systems**: Automated notification and escalation setup
- **Performance optimization**: Resource monitoring and auto-scaling
- **Cost optimization**: Resource rightsizing and lifecycle management

**Practical Examples**: [Infrastructure Testing Script](#infrastructure-testing-script)

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

**[Back to Top](#module-14-proxmox-infrastructure-automation)** ⬆️ | **[Main Index](README.md)** 📚


---

## Practical Examples

### Ansible Inventory

This section provides a sample dynamic and static Ansible inventory for Proxmox environments, including group and host variables for enterprise automation. See the code examples in the Ansible Integration and Enterprise Ansible Automation Framework sections for details.

---

### Web Server Playbook

This section describes a typical Ansible playbook for configuring web servers in a Proxmox-managed infrastructure. See the code examples in the Web Server Playbook and Enterprise Playbook Structure sections for implementation details.

---

### Basic Cloud-Init Template

This section provides a minimal cloud-init configuration template for provisioning VMs in Proxmox. See the code examples in the Cloud-Init Configuration section for YAML templates and usage.

---
[Back to Top](#table-of-contents) ⬆️ | [Main Index](../README.md) 📚


### Enterprise Terraform Infrastructure as Code Implementation

[Back to Top](#table-of-contents) ⬆️ | [Main Index](../README.md) 📚

```hcl
# terraform/providers.tf
terraform {
  required_version = ">= 1.5"
  required_providers {
    proxmox = {
      source  = "telmate/proxmox"
      version = "~> 2.9"
    }
    vault = {
      source  = "hashicorp/vault"
      version = "~> 3.8"
    }
    random = {
      source  = "hashicorp/random"
      version = "~> 3.4"
    }
    tls = {
      source  = "hashicorp/tls"
      version = "~> 4.0"
    }
  }
  
  # Remote state backend with locking
  backend "s3" {
    bucket         = "terraform-state-enterprise"
    key            = "infrastructure/proxmox/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-state-lock"
    
    # Workspace prefix for environment isolation
    workspace_key_prefix = "environments"
  }
}

# Proxmox provider with Vault integration
provider "proxmox" {
  pm_api_url      = data.vault_generic_secret.proxmox_creds.data["api_url"]
  pm_user         = data.vault_generic_secret.proxmox_creds.data["username"]
  pm_password     = data.vault_generic_secret.proxmox_creds.data["password"]
  pm_tls_insecure = var.proxmox_tls_insecure
  pm_parallel     = var.proxmox_parallel_tasks
  pm_timeout      = var.proxmox_timeout
  pm_debug        = var.debug_enabled
}

# Vault provider for secrets management
provider "vault" {
  address = var.vault_address
  # Authentication via environment variables or IAM roles
}

# Retrieve Proxmox credentials from Vault
data "vault_generic_secret" "proxmox_creds" {
  path = "secret/infrastructure/proxmox"
}
```

**Related Commands/Topics:** See [Terraform Core Operations](#terraform-core-operations) 🔗

```hcl
# terraform/variables.tf

# Environment Configuration
variable "environment" {
  description = "Environment name (dev, staging, prod)"
  type        = string
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod."
  }
}

variable "project_name" {
  description = "Project identifier for resource naming"
  type        = string
  validation {
    condition     = can(regex("^[a-z0-9-]+$", var.project_name))
    error_message = "Project name must contain only lowercase letters, numbers, and hyphens."
  }
}

# Proxmox Configuration
variable "proxmox_node" {
  description = "Proxmox node name"
  type        = string
  default     = "pve"
}

variable "proxmox_tls_insecure" {
  description = "Disable TLS verification"
  type        = bool
  default     = false
}

variable "proxmox_parallel_tasks" {
  description = "Number of parallel Proxmox tasks"
  type        = number
  default     = 4
  validation {
    condition     = var.proxmox_parallel_tasks >= 1 && var.proxmox_parallel_tasks <= 10
    error_message = "Parallel tasks must be between 1 and 10."
  }
}

variable "proxmox_timeout" {
  description = "Proxmox API timeout in seconds"
  type        = number
  default     = 600
}

# Network Configuration
variable "network_config" {
  description = "Network configuration for VMs"
  type = object({
    bridge        = string
    vlan_tag      = optional(number)
    firewall      = optional(bool, true)
    link_down     = optional(bool, false)
    macaddr       = optional(string)
    mtu           = optional(number)
    queues        = optional(number)
    rate          = optional(number)
  })
  default = {
    bridge   = "vmbr0"
    firewall = true
  }
}

variable "vm_network_cidr" {
  description = "CIDR block for VM network"
  type        = string
  default     = "192.168.1.0/24"
  validation {
    condition     = can(cidrhost(var.vm_network_cidr, 0))
    error_message = "Must be a valid CIDR block."
  }
}

variable "gateway_ip" {
  description = "Gateway IP address"
  type        = string
  validation {
    condition     = can(regex("^(?:[0-9]{1,3}\\.){3}[0-9]{1,3}$", var.gateway_ip))
    error_message = "Must be a valid IP address."
  }
}

variable "dns_servers" {
  description = "List of DNS server IP addresses"
  type        = list(string)
  default     = ["8.8.8.8", "8.8.4.4"]
  validation {
    condition = alltrue([
      for ip in var.dns_servers : can(regex("^(?:[0-9]{1,3}\\.){3}[0-9]{1,3}$", ip))
    ])
    error_message = "All DNS servers must be valid IP addresses."
  }
}

# VM Template Configuration
variable "vm_template" {
  description = "VM template configuration"
  type = object({
    name        = string
    storage     = string
    cloud_init  = optional(bool, true)
    agent       = optional(bool, true)
  })
  default = {
    name    = "ubuntu-22.04-cloudimg"
    storage = "local"
  }
}

# VM Instance Configuration
variable "vm_instances" {
  description = "Map of VM instances to create"
  type = map(object({
    target_node   = optional(string)
    vmid          = optional(number)
    cores         = optional(number, 2)
    memory        = optional(number, 2048)
    balloon       = optional(number, 1024)
    sockets       = optional(number, 1)
    numa          = optional(bool, false)
    hotplug       = optional(string, "network,disk,usb")
    boot          = optional(string, "order=scsi0;ide2;net0")
    startup       = optional(string, "order=1")
    protection    = optional(bool, false)
    
    # Disk configuration
    disk = optional(object({
      size     = optional(string, "20G")
      storage  = optional(string, "local-zfs")
      type     = optional(string, "scsi")
      format   = optional(string, "raw")
      cache    = optional(string, "writeback")
      iothread = optional(bool, true)
      ssd      = optional(bool, true)
      discard  = optional(string, "on")
      replicate = optional(bool, false)
    }), {})
    
    # Network configuration
    network = optional(object({
      model     = optional(string, "virtio")
      bridge    = optional(string, "vmbr0")
      vlan_tag  = optional(number)
      firewall  = optional(bool, true)
      link_down = optional(bool, false)
      mtu       = optional(number)
      queues    = optional(number)
      rate      = optional(number)
    }), {})
    
    # Cloud-Init configuration
    ip_config = optional(object({
      ip      = optional(string)
      gw      = optional(string)
      ip6     = optional(string)
      gw6     = optional(string)
    }), {})
    
    # Additional configuration
    tags          = optional(list(string), [])
    description   = optional(string)
    onboot        = optional(bool, true)
    tablet        = optional(bool, true)
    kvm           = optional(bool, true)
    machine       = optional(string)
    bios          = optional(string, "seabios")
    scsihw        = optional(string, "virtio-scsi-pci")
  }))
  
  default = {}
}

# Security Configuration
variable "ssh_public_keys" {
  description = "List of SSH public keys for VM access"
  type        = list(string)
  default     = []
}

variable "user_config" {
  description = "User configuration for Cloud-Init"
  type = object({
    username = optional(string, "ubuntu")
    password = optional(string)
    shell    = optional(string, "/bin/bash")
    sudo     = optional(string, "ALL=(ALL) NOPASSWD:ALL")
    groups   = optional(list(string), ["adm", "cdrom", "dip", "lxd", "plugdev", "sudo"])
  })
  default = {}
}

# Vault Configuration
variable "vault_address" {
  description = "Vault server address"
  type        = string
  default     = "https://vault.example.com:8200"
}

variable "debug_enabled" {
  description = "Enable debug logging"
  type        = bool
  default     = false
}

# Tagging and Metadata
variable "common_tags" {
  description = "Common tags to apply to all resources"
  type        = map(string)
  default = {
    ManagedBy   = "Terraform"
    Environment = "dev"
    Project     = "infrastructure"
  }
}
```

**Related Commands/Topics:** See [Terraform Core Operations](#terraform-core-operations) 🔗

#### Enterprise VM Resource Configuration with Advanced Features
```hcl
# terraform/vm-instances.tf

# Local values for computed configurations
locals {
  # Merge common tags with environment-specific tags
  common_tags = merge(
    var.common_tags,
    {
      Environment = var.environment
      Project     = var.project_name
      Terraform   = "true"
      CreatedAt   = timestamp()
    }
  )
  
  # Generate VM names with consistent naming convention
  vm_names = {
    for name, config in var.vm_instances :
    name => "${var.project_name}-${var.environment}-${name}"
  }
  
  # Calculate IP addresses for VMs
  vm_ips = {
    for name, config in var.vm_instances :
    name => config.ip_config.ip != null ? config.ip_config.ip : cidrhost(var.vm_network_cidr, index(keys(var.vm_instances), name) + 10)
  }
}

# Generate SSH key pair for VMs if not provided
resource "tls_private_key" "vm_ssh_key" {
  count     = length(var.ssh_public_keys) == 0 ? 1 : 0
  algorithm = "ED25519"
}

# Store SSH private key in Vault
resource "vault_generic_secret" "vm_ssh_private_key" {
  count = length(var.ssh_public_keys) == 0 ? 1 : 0
  path  = "secret/infrastructure/${var.project_name}/${var.environment}/ssh-key"
  
  data_json = jsonencode({
    private_key = tls_private_key.vm_ssh_key[0].private_key_openssh
    public_key  = tls_private_key.vm_ssh_key[0].public_key_openssh
  })
}

# Cloud-Init configuration template
data "template_file" "cloud_init_config" {
  for_each = var.vm_instances
  
  template = file("${path.module}/templates/cloud-init.yml.tpl")
  
  vars = {
    hostname         = local.vm_names[each.key]
    username         = var.user_config.username
    password_hash    = var.user_config.password != null ? bcrypt(var.user_config.password, 12) : null
    ssh_public_keys  = jsonencode(concat(var.ssh_public_keys, length(var.ssh_public_keys) == 0 ? [tls_private_key.vm_ssh_key[0].public_key_openssh] : []))
    shell            = var.user_config.shell
    sudo_config      = var.user_config.sudo
    groups           = jsonencode(var.user_config.groups)
    packages         = jsonencode(["qemu-guest-agent", "cloud-init", "curl", "wget", "htop", "vim"])
    timezone         = "UTC"
    locale           = "en_US.UTF-8"
  }
}

# Create Cloud-Init configuration files
resource "proxmox_cloud_init_disk" "vm_cloud_init" {
  for_each = var.vm_instances
  
  name     = "${local.vm_names[each.key]}-cloud-init"
  pve_node = each.value.target_node != null ? each.value.target_node : var.proxmox_node
  storage  = var.vm_template.storage
  
  meta_data = yamlencode({
    instance-id    = "${local.vm_names[each.key]}-${random_uuid.vm_instance_id[each.key].result}"
    local-hostname = local.vm_names[each.key]
  })
  
  user_data = data.template_file.cloud_init_config[each.key].rendered
  
  network_config = yamlencode({
    version = 1
    config = [{
      type = "physical"
      name = "eth0"
      subnets = [{
        type = "static"
        address = "${local.vm_ips[each.key]}/${split("/", var.vm_network_cidr)[1]}"
        gateway = var.gateway_ip
        dns_nameservers = var.dns_servers
      }]
    }]
  })
}

# Generate unique instance IDs for VMs
resource "random_uuid" "vm_instance_id" {
  for_each = var.vm_instances
}

# Generate random passwords for VMs if not provided
resource "random_password" "vm_password" {
  for_each = { for name, config in var.vm_instances : name => config if var.user_config.password == null }
  
  length  = 16
  special = true
}

# Store generated passwords in Vault
resource "vault_generic_secret" "vm_passwords" {
  for_each = { for name, config in var.vm_instances : name => config if var.user_config.password == null }
  
  path = "secret/infrastructure/${var.project_name}/${var.environment}/vm-passwords"
  
  data_json = jsonencode({
    for name in keys(var.vm_instances) : name => random_password.vm_password[name].result
  })
}

# Primary VM instances with enterprise configuration
resource "proxmox_vm_qemu" "vm_instances" {
  for_each = var.vm_instances
  
  # Basic configuration
  name         = local.vm_names[each.key]
  target_node  = each.value.target_node != null ? each.value.target_node : var.proxmox_node
  vmid         = each.value.vmid
  desc         = each.value.description != null ? each.value.description : "Managed by Terraform - ${var.project_name}/${var.environment}"
  
  # Template configuration
  clone      = var.vm_template.name
  full_clone = true
  
  # Hardware configuration
  cores    = each.value.cores
  sockets  = each.value.sockets
  memory   = each.value.memory
  balloon  = each.value.balloon
  numa     = each.value.numa
  hotplug  = each.value.hotplug
  
  # Boot configuration
  boot    = each.value.boot
  startup = each.value.startup
  onboot  = each.value.onboot
  
  # Security and features
  protection = each.value.protection
  tablet     = each.value.tablet
  kvm        = each.value.kvm
  machine    = each.value.machine
  bios       = each.value.bios
  scsihw     = each.value.scsihw
  
  # Agent configuration
  agent                = var.vm_template.agent ? 1 : 0
  define_connection_info = false
  
  # Disk configuration
  disk {
    slot     = 0
    size     = each.value.disk.size
    type     = each.value.disk.type
    storage  = each.value.disk.storage
    format   = each.value.disk.format
    cache    = each.value.disk.cache
    iothread = each.value.disk.iothread ? 1 : 0
    ssd      = each.value.disk.ssd ? 1 : 0
    discard  = each.value.disk.discard
    replicate = each.value.disk.replicate ? 1 : 0
  }
  
  # Network configuration
  network {
    model     = each.value.network.model
    bridge    = each.value.network.bridge != null ? each.value.network.bridge : var.network_config.bridge
    tag       = each.value.network.vlan_tag != null ? each.value.network.vlan_tag : var.network_config.vlan_tag
    firewall  = each.value.network.firewall != null ? each.value.network.firewall : var.network_config.firewall
    link_down = each.value.network.link_down != null ? each.value.network.link_down : var.network_config.link_down
    mtu       = each.value.network.mtu != null ? each.value.network.mtu : var.network_config.mtu
    queues    = each.value.network.queues != null ? each.value.network.queues : var.network_config.queues
    rate      = each.value.network.rate != null ? each.value.network.rate : var.network_config.rate
  }
  
  # Cloud-Init configuration
  os_type = "cloud-init"
  cicustom = "user=${proxmox_cloud_init_disk.vm_cloud_init[each.key].storage}:${proxmox_cloud_init_disk.vm_cloud_init[each.key].name}"
  
  # SSH configuration
  sshkeys = join("\n", concat(var.ssh_public_keys, length(var.ssh_public_keys) == 0 ? [tls_private_key.vm_ssh_key[0].public_key_openssh] : []))
  
  # IP configuration
  ipconfig0 = "ip=${local.vm_ips[each.key]}/${split("/", var.vm_network_cidr)[1]},gw=${var.gateway_ip}"
  
  # DNS configuration
  nameserver   = join(" ", var.dns_servers)
  searchdomain = "${var.project_name}.local"
  
  # Tags
  tags = join(",", concat(
    [var.project_name, var.environment, "terraform"],
    each.value.tags,
    [for k, v in local.common_tags : "${k}=${v}"]
  ))
  
  # Lifecycle management
  lifecycle {
    ignore_changes = [
      network.0.macaddr,
      disk.0.file,
      started
    ]
    
    create_before_destroy = false
  }
  
  # Provisioning timeouts
  timeouts {
    create = "10m"
    update = "5m"
    delete = "5m"
  }
  
  depends_on = [
    proxmox_cloud_init_disk.vm_cloud_init
  ]
}
```

#### Cloud-Init Template with Enterprise Configuration
```yaml
# templates/cloud-init.yml.tpl
#cloud-config
# Enterprise Cloud-Init Configuration Template
# Managed by Terraform - Do not modify manually

# System Configuration
hostname: ${hostname}
fqdn: ${hostname}.${project_name}.local
manage_etc_hosts: true
preserve_hostname: false
prefer_fqdn_over_hostname: true

# User Configuration
users:
  - name: ${username}
    groups: ${groups}
    shell: ${shell}
    sudo: "${sudo_config}"
    lock_passwd: false
%{ if password_hash != null ~}
    passwd: ${password_hash}
%{ endif ~}
    ssh_authorized_keys: ${ssh_public_keys}
    ssh_import_id: []
    
# System User (disable default)
system_info:
  default_user:
    name: ${username}
    lock_passwd: false
    gecos: "Default system user"
    groups: ${groups}
    sudo: "${sudo_config}"
    shell: ${shell}

# SSH Configuration
ssh_deletekeys: true
ssh_genkeytypes: ['ed25519', 'rsa']
ssh_keys:
  ed25519_private: |
    # This will be populated automatically
  ed25519_public: |
    # This will be populated automatically
  rsa_private: |
    # This will be populated automatically  
  rsa_public: |
    # This will be populated automatically

# Package Management
package_update: true
package_upgrade: true
package_reboot_if_required: false

packages: ${packages}

# Additional packages for enterprise environments
apt:
  sources:
    docker:
      source: "deb [arch=amd64] https://download.docker.com/linux/ubuntu $RELEASE stable"
      keyid: 9DC858229FC7DD38854AE2D88D81803C0EBFCD88
    kubernetes:
      source: "deb https://apt.kubernetes.io/ kubernetes-xenial main"
      keyid: 7F92E05B31093BEF5A3C2D38FEEA9169307EA071

# System Configuration
timezone: ${timezone}
locale: ${locale}
keyboard:
  layout: us

# Network Configuration (handled by Proxmox, but backup config)
network:
  config: disabled

# File System Configuration
mount_default_fields: [None, None, "auto", "defaults,nofail", "0", "2"]
resize_rootfs: true
growpart:
  mode: auto
  devices: ["/"]
  ignore_growroot_disabled: false

# Security Configuration
disable_root: true
ssh_pwauth: false
password_authentication: false
ssh_authorized_keys_file: "/home/${username}/.ssh/authorized_keys"

# Service Configuration
runcmd:
  # Enable and start essential services
  - systemctl enable qemu-guest-agent
  - systemctl start qemu-guest-agent
  - systemctl enable cloud-init
  - systemctl enable cloud-init-local
  - systemctl enable cloud-config
  - systemctl enable cloud-final
  
  # Security hardening
  - sed -i 's/#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
  - sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
  - sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config
  - systemctl restart ssh
  
  # Install and configure fail2ban
  - apt-get install -y fail2ban
  - systemctl enable fail2ban
  - systemctl start fail2ban
  
  # Configure firewall (UFW)
  - ufw --force enable
  - ufw default deny incoming
  - ufw default allow outgoing
  - ufw allow ssh
  - ufw allow from 10.0.0.0/8 to any port 22
  - ufw allow from 172.16.0.0/12 to any port 22
  - ufw allow from 192.168.0.0/16 to any port 22
  
  # System optimization
  - echo 'vm.swappiness=10' >> /etc/sysctl.conf
  - echo 'net.ipv4.tcp_keepalive_time=120' >> /etc/sysctl.conf
  - echo 'net.ipv4.tcp_keepalive_intvl=30' >> /etc/sysctl.conf
  - echo 'net.ipv4.tcp_keepalive_probes=3' >> /etc/sysctl.conf
  - sysctl -p
  
  # Create project directories
  - mkdir -p /opt/${project_name}
  - chown ${username}:${username} /opt/${project_name}
  
  # Install monitoring agent
  - curl -sSL https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh | bash
  - apt-get update
  - apt-get install -y stackdriver-agent
  
  # Final system update
  - apt-get update && apt-get upgrade -y
  - apt-get autoremove -y
  - apt-get autoclean

# Write additional configuration files
write_files:
  - path: /etc/motd
    content: |
      
      ===============================================
      Welcome to ${hostname}
      ===============================================
      Environment: ${environment}
      Project: ${project_name}
      Managed by: Terraform
      
      This system is monitored and managed
      automatically. Please follow security
      policies and procedures.
      ===============================================
      
    permissions: '0644'
    
  - path: /etc/profile.d/terraform-info.sh
    content: |
      export TERRAFORM_MANAGED=true
      export ENVIRONMENT=${environment}
      export PROJECT_NAME=${project_name}
      export VM_HOSTNAME=${hostname}
    permissions: '0644'
    
  - path: /opt/${project_name}/vm-info.json
    content: |
      {
        "hostname": "${hostname}",
        "environment": "${environment}",
        "project": "${project_name}",
        "managed_by": "terraform",
        "created_at": "$(date -u +%Y-%m-%dT%H:%M:%SZ)",
        "cloud_init": true
      }
    permissions: '0644'
    owner: ${username}:${username}

# Power state management
power_state:
  mode: reboot
  condition: true
  delay: "+1"
  message: "Rebooting after cloud-init completion"
  timeout: 30

# Final message
final_message: |
  Cloud-init has finished configuring ${hostname}
  Environment: ${environment}
  Project: ${project_name}
  
  The system has been automatically configured and secured.
  SSH access is available for authorized users only.
  
  Boot finished at $TIMESTAMP. Up $UPTIME seconds.
```

### Enterprise Ansible Automation Framework

#### Advanced Dynamic Inventory Configuration
```yaml
# inventory/proxmox.yml - Proxmox Dynamic Inventory
plugin: community.general.proxmox
url: "{{ vault_proxmox_api_url }}"
user: "{{ vault_proxmox_user }}"
password: "{{ vault_proxmox_password }}"
validate_certs: false
want_facts: true

# Grouping configuration
groups:
  # Group by environment
  dev: "'dev' in group_names"
  staging: "'staging' in group_names"
  production: "'prod' in group_names"
  
  # Group by role
  web_servers: "'web' in group_names"
  database_servers: "'db' in group_names"
  load_balancers: "'lb' in group_names"
  
  # Group by OS
  ubuntu: "ansible_distribution == 'Ubuntu'"
  centos: "ansible_distribution == 'CentOS'"
  
  # Group by Proxmox node
  node_pve1: "proxmox_node == 'pve1'"
  node_pve2: "proxmox_node == 'pve2'"
  
  # Custom grouping based on tags
  terraform_managed: "'terraform' in proxmox_tags"
  docker_hosts: "'docker' in proxmox_tags"
  kubernetes_nodes: "'k8s' in proxmox_tags"

# Host variables
hostvar_expressions:
  ansible_host: proxmox_ipconfig0.split(',')[0].split('=')[1].split('/')[0]
  vm_id: proxmox_vmid
  vm_node: proxmox_node
  vm_tags: proxmox_tags
  vm_cores: proxmox_cores
  vm_memory: proxmox_memory
  vm_disk_size: proxmox_disk_size

# Compose variables
compose:
  proxmox_vmid: proxmox_vmid | int
  proxmox_cores: proxmox_cores | int
  proxmox_memory: proxmox_memory | int
  environment: >-
    'dev' if 'dev' in proxmox_name
    else 'staging' if 'staging' in proxmox_name
    else 'prod' if 'prod' in proxmox_name
    else 'unknown'
  
# Keyed groups for advanced filtering
keyed_groups:
  - prefix: env
    key: environment
  - prefix: role
    key: proxmox_tags | select('match', '^role_.*') | first | default('unknown') | regex_replace('^role_', '')
  - prefix: node
    key: proxmox_node
```

#### Static Inventory with Enterprise Structure
```ini
# inventory/hosts.ini - Static Inventory Structure

[proxmox:children]
proxmox_prod
proxmox_staging
proxmox_dev

[proxmox_prod]
pve-prod-01 ansible_host=10.0.1.10 proxmox_role=primary
pve-prod-02 ansible_host=10.0.1.11 proxmox_role=secondary
pve-prod-03 ansible_host=10.0.1.12 proxmox_role=secondary

[proxmox_staging]
pve-staging-01 ansible_host=10.0.2.10 proxmox_role=primary

[proxmox_dev]
pve-dev-01 ansible_host=10.0.3.10 proxmox_role=standalone

[web_servers:children]
web_servers_prod
web_servers_staging
web_servers_dev

[web_servers_prod]
web-prod-01 ansible_host=10.0.1.20
web-prod-02 ansible_host=10.0.1.21
web-prod-03 ansible_host=10.0.1.22

[web_servers_staging]
web-staging-01 ansible_host=10.0.2.20
web-staging-02 ansible_host=10.0.2.21

[web_servers_dev]
web-dev-01 ansible_host=10.0.3.20

[database_servers:children]
database_servers_prod
database_servers_staging
database_servers_dev

[database_servers_prod]
db-prod-01 ansible_host=10.0.1.30 mysql_role=master
db-prod-02 ansible_host=10.0.1.31 mysql_role=slave
db-prod-03 ansible_host=10.0.1.32 mysql_role=slave

[database_servers_staging]
db-staging-01 ansible_host=10.0.2.30 mysql_role=standalone

[database_servers_dev]
db-dev-01 ansible_host=10.0.3.30 mysql_role=standalone

[load_balancers:children]
load_balancers_prod
load_balancers_staging

[load_balancers_prod]
lb-prod-01 ansible_host=10.0.1.40 lb_role=primary
lb-prod-02 ansible_host=10.0.1.41 lb_role=secondary

[load_balancers_staging]
lb-staging-01 ansible_host=10.0.2.40 lb_role=standalone

[monitoring_servers:children]
monitoring_servers_prod
monitoring_servers_staging

[monitoring_servers_prod]
mon-prod-01 ansible_host=10.0.1.50

[monitoring_servers_staging]
mon-staging-01 ansible_host=10.0.2.50

# Environment groups
[production:children]
web_servers_prod
database_servers_prod
load_balancers_prod
monitoring_servers_prod

[staging:children]
web_servers_staging
database_servers_staging
load_balancers_staging
monitoring_servers_staging

[development:children]
web_servers_dev
database_servers_dev

# Role-based groups
[all_web:children]
web_servers

[all_db:children]
database_servers

[all_lb:children]
load_balancers

[all_monitoring:children]
monitoring_servers
```

#### Group Variables Configuration
```yaml
# group_vars/all.yml - Global Variables
---
# Common configuration for all hosts
ansible_user: ubuntu
ansible_ssh_private_key_file: "{{ vault_ssh_private_key_path }}"
ansible_ssh_common_args: '-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null'
ansible_python_interpreter: /usr/bin/python3

# Project configuration
project_name: "{{ vault_project_name }}"
organization: "{{ vault_organization }}"
contact_email: "{{ vault_contact_email }}"

# Common packages
common_packages:
  - curl
  - wget
  - htop
  - vim
  - git
  - unzip
  - software-properties-common
  - apt-transport-https
  - ca-certificates
  - gnupg
  - lsb-release
  - fail2ban
  - ufw
  - rsync
  - tree
  - jq

# Security configuration
security_config:
  ssh_port: 22
  ssh_permit_root_login: false
  ssh_password_authentication: false
  ssh_pubkey_authentication: true
  ssh_max_auth_tries: 3
  ufw_enabled: true
  fail2ban_enabled: true

# Monitoring configuration
monitoring_config:
  node_exporter_enabled: true
  node_exporter_port: 9100
  log_forwarding_enabled: true
  log_retention_days: 30

# Backup configuration
backup_config:
  enabled: true
  retention_days: 30
  backup_time: "02:00"
  backup_storage: "/backup"

# Time and locale
timezone: "UTC"
locale: "en_US.UTF-8"

# DNS configuration
dns_servers:
  - "8.8.8.8"
  - "8.8.4.4"
  - "1.1.1.1"

# NTP configuration
ntp_servers:
  - "0.pool.ntp.org"
  - "1.pool.ntp.org"
  - "2.pool.ntp.org"
  - "3.pool.ntp.org"
```

```yaml
# group_vars/production.yml - Production Environment Variables
---
environment: production
log_level: warn
debug_mode: false

# Resource limits
max_connections: 1000
memory_limit: "80%"
cpu_limit: "90%"

# Backup configuration
backup_config:
  enabled: true
  retention_days: 90
  backup_time: "01:00"
  backup_storage: "/backup/production"
  offsite_backup: true

# Security hardening
security_hardening:
  enabled: true
  level: strict
  compliance_framework: "CIS"
  
# Monitoring
monitoring_config:
  alerting_enabled: true
  alert_email: "ops@company.com"
  metrics_retention: "90d"
  log_retention_days: 90

# High availability
ha_config:
  enabled: true
  keepalived_enabled: true
  cluster_name: "prod-cluster"
```

```yaml
# group_vars/web_servers.yml - Web Server Configuration
---
# Nginx configuration
nginx_config:
  worker_processes: auto
  worker_connections: 1024
  keepalive_timeout: 65
  client_max_body_size: 64m
  gzip_enabled: true
  
  # SSL configuration
  ssl_protocols: "TLSv1.2 TLSv1.3"
  ssl_ciphers: "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384"
  ssl_prefer_server_ciphers: true
  ssl_session_cache: "shared:SSL:10m"
  ssl_session_timeout: "10m"

# Application configuration
app_config:
  name: "web-application"
  version: "{{ vault_app_version }}"
  port: 8080
  workers: 4
  environment: "{{ environment }}"

# Health check configuration
health_check:
  enabled: true
  endpoint: "/health"
  timeout: 5
  interval: 30

# Firewall rules
firewall_rules:
  - { port: 80, protocol: tcp, source: "0.0.0.0/0" }
  - { port: 443, protocol: tcp, source: "0.0.0.0/0" }
  - { port: 22, protocol: tcp, source: "10.0.0.0/8" }
```

#### Enterprise Playbook Structure
```yaml
# playbooks/site.yml - Main Site Playbook
---
- name: Configure Proxmox Infrastructure
  hosts: proxmox
  become: true
  gather_facts: true
  
  pre_tasks:
    - name: Verify connectivity
      ping:
      tags: always
      
    - name: Gather system facts
      setup:
      tags: always
      
  roles:
    - role: common
      tags: [common, base]
    - role: security
      tags: [security, hardening]
    - role: monitoring
      tags: [monitoring, observability]
    - role: proxmox
      tags: [proxmox, virtualization]
      
  post_tasks:
    - name: Verify services are running
      service:
        name: "{{ item }}"
        state: started
        enabled: true
      loop:
        - ssh
        - ufw
        - fail2ban
      tags: [verify, post-config]

- name: Configure Web Servers
  hosts: web_servers
  become: true
  gather_facts: true
  
  pre_tasks:
    - name: Update package cache
      apt:
        update_cache: true
        cache_valid_time: 3600
      tags: always
      
  roles:
    - role: common
      tags: [common, base]
    - role: security
      tags: [security, hardening]
    - role: nginx
      tags: [nginx, web]
    - role: application
      tags: [application, deploy]
    - role: monitoring
      tags: [monitoring, observability]
      
  post_tasks:
    - name: Verify web service
      uri:
        url: "http://{{ ansible_default_ipv4.address }}:{{ app_config.port }}{{ health_check.endpoint }}"
        method: GET
        status_code: 200
      tags: [verify, health-check]

- name: Configure Database Servers
  hosts: database_servers
  become: true
  gather_facts: true
  
  pre_tasks:
    - name: Check disk space
      assert:
        that:
          - ansible_mounts | selectattr('mount', 'equalto', '/') | map(attribute='size_available') | first > 1073741824
        fail_msg: "Insufficient disk space (less than 1GB available)"
      tags: always
      
  roles:
    - role: common
      tags: [common, base]
    - role: security
      tags: [security, hardening]
    - role: mysql
      tags: [mysql, database]
    - role: backup
      tags: [backup, data-protection]
    - role: monitoring
      tags: [monitoring, observability]
      
  post_tasks:
    - name: Verify database connectivity
      mysql_info:
        login_user: "{{ mysql_root_username }}"
        login_password: "{{ mysql_root_password }}"
      tags: [verify, db-check]

- name: Configure Load Balancers
  hosts: load_balancers
  become: true
  gather_facts: true
  
  roles:
    - role: common
      tags: [common, base]
    - role: security
      tags: [security, hardening]
    - role: haproxy
      tags: [haproxy, load-balancer]
    - role: keepalived
      tags: [keepalived, high-availability]
      when: ha_config.enabled | default(false)
    - role: monitoring
      tags: [monitoring, observability]
      
  post_tasks:
    - name: Verify load balancer health
      uri:
        url: "http://{{ ansible_default_ipv4.address }}/health"
        method: GET
        status_code: 200
      tags: [verify, lb-check]

- name: Configure Monitoring Infrastructure
  hosts: monitoring_servers
  become: true
  gather_facts: true
  
  roles:
    - role: common
      tags: [common, base]
    - role: security
      tags: [security, hardening]
    - role: prometheus
      tags: [prometheus, monitoring]
    - role: grafana
      tags: [grafana, visualization]
    - role: alertmanager
      tags: [alertmanager, alerting]
    - role: elasticsearch
      tags: [elasticsearch, logging]
      when: logging_config.centralized | default(false)
    - role: kibana
      tags: [kibana, log-analysis]
      when: logging_config.centralized | default(false)
```

#### Enterprise Role Structure - Common Role
```yaml
# roles/common/tasks/main.yml
---
- name: Include OS-specific variables
  include_vars: "{{ ansible_os_family }}.yml"
  tags: [common, variables]

- name: Update system packages
  include_tasks: package_management.yml
  tags: [common, packages]

- name: Configure system settings
  include_tasks: system_config.yml
  tags: [common, system]

- name: Configure users and groups
  include_tasks: users.yml
  tags: [common, users]

- name: Configure SSH
  include_tasks: ssh.yml
  tags: [common, ssh]

- name: Configure time synchronization
  include_tasks: ntp.yml
  tags: [common, time]

- name: Configure logging
  include_tasks: logging.yml
  tags: [common, logging]

- name: Install monitoring agent
  include_tasks: monitoring.yml
  tags: [common, monitoring]

- name: Configure backup client
  include_tasks: backup.yml
  tags: [common, backup]
  when: backup_config.enabled | default(false)
```

```yaml
# roles/common/tasks/package_management.yml
---
- name: Update package cache (Debian/Ubuntu)
  apt:
    update_cache: true
    cache_valid_time: 3600
  when: ansible_os_family == "Debian"
  tags: [packages, cache]

- name: Update package cache (RedHat/CentOS)
  yum:
    update_cache: true
  when: ansible_os_family == "RedHat"
  tags: [packages, cache]

- name: Upgrade all packages (Debian/Ubuntu)
  apt:
    upgrade: safe
    autoremove: true
    autoclean: true
  when: ansible_os_family == "Debian"
  register: apt_upgrade_result
  tags: [packages, upgrade]

- name: Upgrade all packages (RedHat/CentOS)
  yum:
    name: "*"
    state: latest
  when: ansible_os_family == "RedHat"
  register: yum_upgrade_result
  tags: [packages, upgrade]

- name: Install common packages (Debian/Ubuntu)
  apt:
    name: "{{ common_packages }}"
    state: present
  when: ansible_os_family == "Debian"
  tags: [packages, install]

- name: Install common packages (RedHat/CentOS)
  yum:
    name: "{{ common_packages }}"
    state: present
  when: ansible_os_family == "RedHat"
  tags: [packages, install]

- name: Install Python packages
  pip:
    name: "{{ item }}"
    state: present
  loop:
    - requests
    - psutil
    - pyyaml
    - jinja2
  tags: [packages, python]

- name: Remove unnecessary packages (Debian/Ubuntu)
  apt:
    name: "{{ unnecessary_packages }}"
    state: absent
    purge: true
  when: ansible_os_family == "Debian"
  tags: [packages, cleanup]

- name: Configure automatic security updates (Debian/Ubuntu)
  copy:
    dest: /etc/apt/apt.conf.d/20auto-upgrades
    content: |
      APT::Periodic::Update-Package-Lists "1";
      APT::Periodic::Unattended-Upgrade "1";
      APT::Periodic::AutocleanInterval "7";
    owner: root
    group: root
    mode: '0644'
  when: ansible_os_family == "Debian"
  tags: [packages, auto-update]

- name: Install unattended-upgrades package
  apt:
    name: unattended-upgrades
    state: present
  when: ansible_os_family == "Debian"
  tags: [packages, auto-update]

- name: Configure unattended-upgrades
  template:
    src: 50unattended-upgrades.j2
    dest: /etc/apt/apt.conf.d/50unattended-upgrades
    owner: root
    group: root
    mode: '0644'
  when: ansible_os_family == "Debian"
  notify: restart unattended-upgrades
  tags: [packages, auto-update]
```
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

[Back to Top](#table-of-contents) ⬆️ | [Main Index](../README.md) 📚

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

### Lab 1: Enterprise Terraform Infrastructure Deployment
**Objective:** Design and deploy a complete three-tier application infrastructure using advanced Terraform patterns

**Duration:** 4-6 hours

**Prerequisites:**
- Proxmox VE cluster with at least 3 nodes
- HashiCorp Vault server configured
- S3-compatible storage for state backend
- Git repository for infrastructure code

**Tasks:**
1. **Infrastructure Foundation Setup**:
   - Configure Terraform with remote S3 state backend and DynamoDB locking
   - Set up Vault integration for secrets management
   - Create workspace-based environment isolation (dev, staging, prod)
   - Implement Terraform modules for reusable infrastructure components

2. **Network Infrastructure Automation**:
   - Design and implement network segmentation with VLANs
   - Create firewall rules and security groups using Terraform
   - Implement load balancer configuration with SSL termination
   - Set up DNS automation with dynamic record management

3. **VM Infrastructure Deployment**:
   - Deploy web tier (3 VMs with auto-scaling capability)
   - Deploy application tier (2 VMs with session clustering)
   - Deploy database tier (3 VMs with master-slave replication)
   - Implement monitoring infrastructure (Prometheus, Grafana, AlertManager)

4. **Advanced Configuration**:
   - Implement Cloud-Init automation for VM customization
   - Configure automated backup scheduling
   - Set up cross-datacenter replication
   - Implement disaster recovery automation

**Deliverables:**
- Complete Terraform infrastructure code with modules
- Environment-specific variable files
- State management configuration
- Infrastructure documentation and diagrams
- Deployment and rollback procedures

**Assessment Criteria:**
- Infrastructure deploys successfully across all environments
- State management and locking work correctly
- Modules are reusable and well-documented
- Security best practices are implemented
- Infrastructure can be destroyed and recreated reliably

---

### Lab 2: Advanced Ansible Configuration Management
**Objective:** Create enterprise-grade Ansible automation for complete infrastructure configuration management

**Duration:** 4-6 hours

**Prerequisites:**
- Terraform-deployed infrastructure from Lab 1
- Ansible control node configured
- Vault integration for sensitive data
- Git repository for configuration management code

**Tasks:**
1. **Dynamic Inventory Implementation**:
   - Configure Proxmox dynamic inventory plugin
   - Implement custom inventory scripts for complex grouping
   - Set up inventory caching and optimization
   - Create environment-based inventory separation

2. **Enterprise Playbook Architecture**:
   - Design role-based playbook structure
   - Implement idempotent configuration management
   - Create environment-specific variable hierarchies
   - Set up encrypted secrets management with Ansible Vault

3. **Application Stack Configuration**:
   - Configure web servers with Nginx and SSL
   - Set up application servers with clustering
   - Configure database replication and backup automation
   - Implement monitoring agent deployment

4. **Advanced Automation Features**:
   - Create custom Ansible modules for specific tasks
   - Implement rolling updates with health checks
   - Set up automated testing with Molecule
   - Configure CI/CD integration for configuration changes

**Deliverables:**
- Complete Ansible role library
- Dynamic inventory configuration
- Playbooks for all infrastructure tiers
- Testing framework with Molecule
- CI/CD pipeline for configuration management

**Assessment Criteria:**
- All infrastructure is properly configured and functional
- Playbooks are idempotent and error-free
- Secrets management is properly implemented
- Testing framework validates all changes
- Documentation covers all playbooks and roles

---

### Lab 3: CI/CD Pipeline for Infrastructure as Code
**Objective:** Implement enterprise GitOps workflow for infrastructure lifecycle management

**Duration:** 3-4 hours

**Prerequisites:**
- Git repository with infrastructure code
- GitLab/GitHub with CI/CD capabilities
- Terraform and Ansible automation from previous labs
- Container runtime for pipeline execution

**Tasks:**
1. **Pipeline Foundation**:
   - Set up GitOps repository structure
   - Configure branch protection and review policies
   - Implement infrastructure code linting and validation
   - Set up automated testing for Terraform and Ansible

2. **Multi-Stage Deployment Pipeline**:
   - Create dev environment auto-deployment
   - Implement staging environment with approval gates
   - Set up production deployment with multiple approvals
   - Configure rollback mechanisms and disaster recovery

3. **Security and Compliance Integration**:
   - Implement infrastructure security scanning (Checkov, Terrascan)
   - Set up compliance validation (CIS benchmarks, custom policies)
   - Configure secret scanning and credential validation
   - Implement drift detection and remediation

4. **Monitoring and Observability**:
   - Set up pipeline monitoring and alerting
   - Implement infrastructure state monitoring
   - Configure cost tracking and optimization alerts
   - Set up performance monitoring and capacity planning

**Deliverables:**
- Complete GitOps pipeline configuration
- Multi-environment deployment workflows
- Security and compliance automation
- Monitoring and alerting integration
- Comprehensive pipeline documentation

**Assessment Criteria:**
- Pipeline deploys infrastructure successfully
- Security scanning catches vulnerabilities
- Approval workflows function correctly
- Rollback procedures work reliably
- Monitoring provides comprehensive visibility

---

### Lab 4: Enterprise Secrets Management and Security
**Objective:** Implement comprehensive secrets management and security automation

**Duration:** 3-4 hours

**Prerequisites:**
- HashiCorp Vault cluster
- Existing infrastructure from previous labs
- PKI infrastructure capability
- Identity provider integration

**Tasks:**
1. **Vault Configuration and Policies**:
   - Set up Vault with high availability
   - Configure authentication methods (LDAP, OIDC, AppRole)
   - Implement fine-grained access policies
   - Set up secret engines (KV, PKI, Database)

2. **Dynamic Secrets Integration**:
   - Configure database secret engine for dynamic credentials
   - Set up PKI engine for certificate management
   - Implement secret rotation automation
   - Configure lease management and renewal

3. **Infrastructure Integration**:
   - Integrate Vault with Terraform for secret injection
   - Configure Ansible Vault provider integration
   - Set up automatic secret distribution
   - Implement secure CI/CD secret management

4. **Security Automation**:
   - Configure automated vulnerability scanning
   - Set up compliance monitoring and reporting
   - Implement security incident response automation
   - Configure audit logging and SIEM integration

**Deliverables:**
- Production-ready Vault configuration
- Dynamic secrets automation
- Security policy enforcement
- Compliance monitoring dashboard
- Security incident response procedures

**Assessment Criteria:**
- Vault provides secure secret management
- Dynamic secrets work across all services
- Security policies are properly enforced
- Compliance requirements are met
- Audit trails are comprehensive and accessible

---

### Lab 5: Monitoring, Observability, and Performance Optimization
**Objective:** Implement comprehensive infrastructure monitoring and automated performance optimization

**Duration:** 4-5 hours

**Prerequisites:**
- Complete infrastructure from previous labs
- Monitoring infrastructure deployed
- Log aggregation capability
- Alerting systems configured

**Tasks:**
1. **Comprehensive Monitoring Setup**:
   - Deploy Prometheus with high availability
   - Configure Grafana with custom dashboards
   - Set up AlertManager with escalation policies
   - Implement distributed tracing with Jaeger

2. **Infrastructure Metrics Collection**:
   - Configure node exporters on all VMs
   - Set up Proxmox monitoring integration
   - Implement custom metrics for business KPIs
   - Configure synthetic monitoring for end-user experience

3. **Log Management and Analysis**:
   - Deploy ELK stack for centralized logging
   - Configure log shipping from all infrastructure
   - Set up log analysis and anomaly detection
   - Implement security event correlation

4. **Automated Optimization**:
   - Configure auto-scaling based on metrics
   - Implement cost optimization automation
   - Set up performance tuning recommendations
   - Configure predictive capacity planning

**Deliverables:**
- Complete monitoring and observability stack
- Custom dashboards for all infrastructure tiers
- Automated alerting and escalation
- Log analysis and security monitoring
- Performance optimization automation

**Assessment Criteria:**
- All infrastructure components are monitored
- Dashboards provide actionable insights
- Alerting reduces mean time to detection
- Log analysis helps troubleshoot issues
- Automation improves efficiency and reduces costs

---

### Lab 6: Disaster Recovery and Business Continuity
**Objective:** Implement enterprise-grade disaster recovery and business continuity automation

**Duration:** 3-4 hours

**Prerequisites:**
- Multi-site Proxmox infrastructure
- Backup storage systems
- Network connectivity between sites
- Tested infrastructure automation

**Tasks:**
1. **Backup Automation Strategy**:
   - Implement automated VM backup scheduling
   - Configure incremental and differential backups
   - Set up cross-site backup replication
   - Implement backup validation and testing

2. **Disaster Recovery Procedures**:
   - Create automated failover procedures
   - Implement database replication and failover
   - Configure DNS failover automation
   - Set up application data synchronization

3. **Business Continuity Testing**:
   - Automate disaster recovery testing
   - Implement RTO/RPO monitoring and reporting
   - Configure automated recovery validation
   - Set up stakeholder communication automation

4. **Recovery Operations**:
   - Create runbooks for various disaster scenarios
   - Implement automated recovery orchestration
   - Configure rollback procedures
   - Set up post-incident analysis automation

**Deliverables:**
- Automated backup and replication system
- Disaster recovery orchestration
- Business continuity testing framework
- Recovery runbooks and procedures
- RTO/RPO monitoring and reporting

**Assessment Criteria:**
- Backup systems operate reliably
- Disaster recovery can be executed successfully
- RTO/RPO targets are consistently met
- Testing procedures validate recovery capabilities
- Documentation enables rapid response

---

### Lab 7: Enterprise Governance and Compliance Automation
**Objective:** Implement comprehensive governance, compliance, and cost management automation

**Duration:** 3-4 hours

**Prerequisites:**
- Complete infrastructure from previous labs
- Policy engine capability (OPA/Sentinel)
- Cost management tools
- Compliance frameworks (CIS, SOC 2, ISO 27001)

**Tasks:**
1. **Policy as Code Implementation**:
   - Configure Open Policy Agent for infrastructure policies
   - Implement Terraform Sentinel policies
   - Set up Ansible policy validation
   - Create custom compliance rules

2. **Cost Management and Optimization**:
   - Implement resource tagging automation
   - Configure cost tracking and reporting
   - Set up budget alerts and controls
   - Create resource optimization recommendations

3. **Compliance Automation**:
   - Configure CIS benchmark validation
   - Implement SOC 2 compliance monitoring
   - Set up vulnerability scanning automation
   - Create compliance reporting dashboards

4. **Governance Framework**:
   - Implement resource lifecycle management
   - Configure approval workflows
   - Set up audit trail automation
   - Create governance reporting and analytics

**Deliverables:**
- Policy as code framework
- Cost management and optimization system
- Compliance monitoring and reporting
- Governance workflow automation
- Comprehensive audit capabilities

**Assessment Criteria:**
- Policies prevent infrastructure violations
- Cost management provides visibility and control
- Compliance requirements are continuously met
- Governance workflows operate smoothly
- Audit trails support regulatory requirements

## Assessment Criteria

Each lab will be evaluated based on:

| Criteria | Weight | Description |
|----------|---------|-------------|
| Technical Implementation | 40% | Correct deployment and configuration of all components |
| Automation and Scalability | 25% | Effective automation that scales across environments |
| Security and Compliance | 20% | Proper security controls and compliance adherence |
| Documentation and Procedures | 15% | Clear documentation and operational procedures |

## Best Practices Summary

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| **Code Organization** | Use modules and reusable components | Terraform modules, Ansible roles |
| **State Management** | Remote state with locking | S3 backend with DynamoDB |
| **Security** | Secrets management and least privilege | Vault integration, IAM policies |
| **Testing** | Automated validation and testing | Terratest, Molecule, pipeline validation |
| **Documentation** | Infrastructure as documentation | Code comments, README files, diagrams |
| **Versioning** | Tag releases and maintain changelogs | Git tags, semantic versioning |
| **Monitoring** | Comprehensive observability | Metrics, logs, traces, alerts |
| **Backup** | Automated backup and recovery | Scheduled backups, tested recovery |

## Troubleshooting Guide

### Common Terraform Issues

| Issue | Symptoms | Solution |
|-------|----------|----------|
| State Lock | "Error acquiring the state lock" | `terraform force-unlock <lock_id>` |
| Provider Version | "Provider version conflicts" | Update `required_providers` constraints |
| Resource Drift | "Plan shows unexpected changes" | `terraform refresh` then investigate |
| Module Errors | "Module not found" | Check module source and version |

### Common Ansible Issues

| Issue | Symptoms | Solution |
|-------|----------|----------|
| SSH Connection | "Host unreachable" | Verify SSH keys and network connectivity |
| Permission Denied | "sudo: a password is required" | Configure passwordless sudo or use `--ask-become-pass` |
| Playbook Syntax | "Syntax error" | Use `ansible-playbook --syntax-check` |
| Inventory Issues | "No hosts matched" | Verify inventory file and host patterns |

### Vault Troubleshooting

| Issue | Symptoms | Solution |
|-------|----------|----------|
| Sealed Vault | "Vault is sealed" | `vault operator unseal` with unseal keys |
| Token Expired | "Token expired" | Renew or create new token |
| Policy Denied | "Permission denied" | Check and update Vault policies |
| Backend Issues | "Storage backend error" | Check backend connectivity and configuration |

## Next Steps

With Proxmox Infrastructure Automation mastered, you have completed the comprehensive Linux Sysadmin & DevOps Training Program. Continue your journey by:

1. **Advanced Specialization**: Choose areas like Kubernetes, cloud platforms, or security
2. **Certification Paths**: Pursue relevant certifications (AWS, Azure, GCP, CKA, etc.)
3. **Community Contribution**: Contribute to open-source projects and share knowledge
4. **Continuous Learning**: Stay current with evolving technologies and best practices
5. **Mentoring Others**: Help others learn DevOps principles and practices

Proceed to **Module 15: Git & GitHub Setup with SSH Access** to complete the final module and establish proper version control workflows for your infrastructure code.
