# Linux Sysadmin & DevOps Training Program
 
This comprehensive repository guides experienced Windows sysadmins through a structured journey from fundamental Linux administration to advanced DevOps infrastructure automation using enterprise-grade tools including ZFS, Proxmox VE, OpenSSH, Cloud-Init, Terraform, and Ansible.

---
 
## Table of Contents

### 📚 Basic Linux & SysAdmin Foundations
 
1. **[Module 1: Linux Distributions & Philosophy](Module1_Linux_Distributions_and_Philosophy.md)**
   - [1.1 Linux History and Philosophy](Module1_Linux_Distributions_and_Philosophy.md#11-linux-history-and-philosophy)
   - [1.2 Distribution Families and Package Management](Module1_Linux_Distributions_and_Philosophy.md#12-distribution-families-and-package-management)
   - [1.3 Release Models and Support Cycles](Module1_Linux_Distributions_and_Philosophy.md#13-release-models-and-support-cycles)
   - [1.4 Open Source Licensing and Governance](Module1_Linux_Distributions_and_Philosophy.md#14-open-source-licensing-and-governance)
   - [1.5 Distribution Selection Criteria](Module1_Linux_Distributions_and_Philosophy.md#15-distribution-selection-criteria)

2. **[Module 2: Filesystem Hierarchy & Permissions](Module2_Filesystem_Hierarchy_and_Permissions.md)**
   - [2.1 Filesystem Hierarchy Standard (FHS)](Module2_Filesystem_Hierarchy_and_Permissions.md#21-filesystem-hierarchy-standard-fhs)
   - [2.2 Basic File and Directory Permissions](Module2_Filesystem_Hierarchy_and_Permissions.md#22-basic-file-and-directory-permissions)
   - [2.3 Special Permission Modes](Module2_Filesystem_Hierarchy_and_Permissions.md#23-special-permission-modes)
   - [2.4 Access Control Lists (ACLs)](Module2_Filesystem_Hierarchy_and_Permissions.md#24-access-control-lists-acls)
   - [2.5 File Attributes and Extended Attributes](Module2_Filesystem_Hierarchy_and_Permissions.md#25-file-attributes-and-extended-attributes)

3. **[Module 3: Command-Line Essentials](Module3_Command-Line_Essentials.md)**
   - [3.1 Shell Basics and Environment](Module3_Command-Line_Essentials.md#31-shell-basics-and-environment)
   - [3.2 Navigation and File Operations](Module3_Command-Line_Essentials.md#32-navigation-and-file-operations)
   - [3.3 File Content Management](Module3_Command-Line_Essentials.md#33-file-content-management)
   - [3.4 Text Processing and Data Manipulation](Module3_Command-Line_Essentials.md#34-text-processing-and-data-manipulation)
   - [3.5 Pipes, Redirection, and Command Chaining](Module3_Command-Line_Essentials.md#35-pipes-redirection-and-command-chaining)
   - [3.6 File Searching and Pattern Matching](Module3_Command-Line_Essentials.md#36-file-searching-and-pattern-matching)
   - [3.7 Shell Customization and Productivity](Module3_Command-Line_Essentials.md#37-shell-customization-and-productivity)
   - [3.8 Debugging and Error Handling](Module3_Command-Line_Essentials.md#38-debugging-and-error-handling)
   - [3.9 Archives and Compression](Module3_Command-Line_Essentials.md#39-archives-and-compression)

4. **[Module 4: Package Management](Module4_Package_Management.md)**
   - [4.1 Package Management Fundamentals](Module4_Package_Management.md#41-package-management-fundamentals)
   - [4.2 Debian/Ubuntu Package Management (APT)](Module4_Package_Management.md#42-debianubuntu-package-management-apt)
   - [4.3 Red Hat/CentOS Package Management (YUMDNF)](Module4_Package_Management.md#43-red-hatcentos-package-management-yumdnf)
   - [4.4 SUSE Package Management (Zypper)](Module4_Package_Management.md#44-suse-package-management-zypper)
   - [4.5 Arch Linux Package Management (Pacman)](Module4_Package_Management.md#45-arch-linux-package-management-pacman)
   - [4.6 Universal Package Managers](Module4_Package_Management.md#46-universal-package-managers)
   - [4.7 Repository Management and Security](Module4_Package_Management.md#47-repository-management-and-security)
   - [4.8 Source Compilation and Custom Packages](Module4_Package_Management.md#48-source-compilation-and-custom-packages)
   - [4.9 Package Automation and Scripting](Module4_Package_Management.md#49-package-automation-and-scripting)

5. **[Module 5: Processes & Services](Module5_Processes_and_Services.md)**
   - [5.1 Process Basics (Beginner)](Module5_Processes_and_Services.md#51-process-basics-beginner)
   - [5.2 Process Monitoring (Intermediate)](Module5_Processes_and_Services.md#52-process-monitoring-intermediate)
   - [5.3 Process Control (Intermediate)](Module5_Processes_and_Services.md#53-process-control-intermediate)
   - [5.4 Basic Service Management (Intermediate)](Module5_Processes_and_Services.md#54-basic-service-management-intermediate)
   - [5.5 Essential Systemd Operations (Advanced)](Module5_Processes_and_Services.md#55-essential-systemd-operations-advanced)

6. **[Module 6: Users, Groups & Authentication](Module6_Users_Groups_and_Authentication.md)**
   - [6.1 User Account Fundamentals](Module6_Users_Groups_and_Authentication.md#61-user-account-fundamentals)
   - [6.2 Basic User Management](Module6_Users_Groups_and_Authentication.md#62-basic-user-management)
   - [6.3 Group Management Basics](Module6_Users_Groups_and_Authentication.md#63-group-management-basics)
   - [6.4 Sudo Configuration](Module6_Users_Groups_and_Authentication.md#64-sudo-configuration)
   - [6.5 Password Policies and Security](Module6_Users_Groups_and_Authentication.md#65-password-policies-and-security)

7. **[Module 7: Networking Fundamentals](Module7_Networking_Fundamentals.md)**
   - [7.1 Network Interface Management](Module7_Networking_Fundamentals.md#71-network-interface-management)
   - [7.2 IP Configuration with Netplan](Module7_Networking_Fundamentals.md#72-ip-configuration-with-netplan)
   - [7.3 Legacy Network Configuration](Module7_Networking_Fundamentals.md#73-legacy-network-configuration)
   - [7.4 DNS and Name Resolution](Module7_Networking_Fundamentals.md#74-dns-and-name-resolution)
   - [7.5 Basic Network Troubleshooting](Module7_Networking_Fundamentals.md#75-basic-network-troubleshooting)
   - [7.6 Firewall Basics](Module7_Networking_Fundamentals.md#76-firewall-basics)
   - [7.7 SSH Configuration](Module7_Networking_Fundamentals.md#77-ssh-configuration)
   - [7.8 VPN Setup (WireGuard)](Module7_Networking_Fundamentals.md#78-vpn-setup-wireguard)

8. **[Module 8: Logging & Monitoring](Module8_Logging_and_Monitoring.md)**
   - [8.1 System Logging Fundamentals](Module8_Logging_and_Monitoring.md#81-system-logging-fundamentals)
   - [8.2 rsyslog Configuration](Module8_Logging_and_Monitoring.md#82-rsyslog-configuration)
   - [8.3 systemd Journal (journald)](Module8_Logging_and_Monitoring.md#83-systemd-journal-journald)
   - [8.4 Log Rotation and Management](Module8_Logging_and_Monitoring.md#84-log-rotation-and-management)
   - [8.5 Resource Monitoring Fundamentals](Module8_Logging_and_Monitoring.md#85-resource-monitoring-fundamentals)
   - [8.6 Prometheus and Node Exporter](Module8_Logging_and_Monitoring.md#86-prometheus-and-node-exporter)
   - [8.7 Grafana Visualization](Module8_Logging_and_Monitoring.md#87-grafana-visualization)
   - [8.8 Centralized Logging Solutions](Module8_Logging_and_Monitoring.md#88-centralized-logging-solutions)

9. **[Module 9: Shell Scripting Fundamentals](Module9_Shell_Scripting_Fundamentals.md)**
   - [9.1 Shell Scripting Foundations](Module9_Shell_Scripting_Fundamentals.md#91-shell-scripting-foundations)
   - [9.2 Variables and Parameter Management](Module9_Shell_Scripting_Fundamentals.md#92-variables-and-parameter-management)
   - [9.3 Control Structures and Flow Control](Module9_Shell_Scripting_Fundamentals.md#93-control-structures-and-flow-control)
   - [9.4 Functions and Modular Programming](Module9_Shell_Scripting_Fundamentals.md#94-functions-and-modular-programming)
   - [9.5 Advanced InputOutput Operations](Module9_Shell_Scripting_Fundamentals.md#95-advanced-inputoutput-operations)
   - [9.6 Error Handling and Debugging](Module9_Shell_Scripting_Fundamentals.md#96-error-handling-and-debugging)
   - [9.7 System Integration and Automation](Module9_Shell_Scripting_Fundamentals.md#97-system-integration-and-automation)
   - [9.8 Enterprise Script Development](Module9_Shell_Scripting_Fundamentals.md#98-enterprise-script-development)

10. **[Module 10: Storage & Filesystem Management](Module10_Storage_and_Filesystem_Management.md)**
    - [10.1 Storage Fundamentals and Basic Partitioning](Module10_Storage_and_Filesystem_Management.md#101-storage-fundamentals-and-basic-partitioning)
    - [10.2 Ext4 and Xfs Filesystem Management](Module10_Storage_and_Filesystem_Management.md#102-ext4-and-xfs-filesystem-management)
    - [10.3 Lvm Fundamentals and Benefits](Module10_Storage_and_Filesystem_Management.md#103-lvm-fundamentals-and-benefits)
    - [10.4 Storage Security and Backup Basics](Module10_Storage_and_Filesystem_Management.md#104-storage-security-and-backup-basics)
    - [10.5 Looking Ahead Zfs Overview](Module10_Storage_and_Filesystem_Management.md#105-looking-ahead-zfs-overview)
    - [10.7 Network Storage and Clustering](Module10_Storage_and_Filesystem_Management.md#107-network-storage-and-clustering)
    - [10.8 Storage Security and Encryption](Module10_Storage_and_Filesystem_Management.md#108-storage-security-and-encryption)
 
### 🚀 Advanced DevOps & Infrastructure Automation
 
11. **[Module 11: ZFS Fundamentals](Module11_ZFS_Fundamentals.md)**
    - [11.1 ZFS Architecture and Copy-on-Write Fundamentals](Module11_ZFS_Fundamentals.md#111-zfs-architecture-and-copy-on-write-fundamentals)
    - [11.2 Pool Management and Storage Hierarchies](Module11_ZFS_Fundamentals.md#112-pool-management-and-storage-hierarchies)
    - [11.3 Datasets, Zvols, and Hierarchical Management](Module11_ZFS_Fundamentals.md#113-datasets-zvols-and-hierarchical-management)
    - [11.4 Advanced Features: Compression, Deduplication, and Optimization](Module11_ZFS_Fundamentals.md#114-advanced-features-compression-deduplication-and-optimization)
    - [11.5 Snapshot and Clone Management](Module11_ZFS_Fundamentals.md#115-snapshot-and-clone-management)
    - [11.6 Replication and Backup Strategies](Module11_ZFS_Fundamentals.md#116-replication-and-backup-strategies)
    - [11.7 Performance Tuning and Caching](Module11_ZFS_Fundamentals.md#117-performance-tuning-and-caching)
    - [11.8 Monitoring and Troubleshooting](Module11_ZFS_Fundamentals.md#118-monitoring-and-troubleshooting)

12. **[Module 12: Proxmox Virtual Environment](Module12_Proxmox_Virtual_Environment.md)**
    - [12.1 Installation and Initial Setup](Module12_Proxmox_Virtual_Environment.md#121-installation-and-initial-setup)
    - [12.2 Storage Configuration](Module12_Proxmox_Virtual_Environment.md#122-storage-configuration)
    - [12.3 Virtual Machine Management](Module12_Proxmox_Virtual_Environment.md#123-virtual-machine-management)
    - [12.4 Container Management](Module12_Proxmox_Virtual_Environment.md#124-container-management)
    - [12.5 Basic Networking](Module12_Proxmox_Virtual_Environment.md#125-basic-networking)
    - [12.6 Backup and Maintenance](Module12_Proxmox_Virtual_Environment.md#126-backup-and-maintenance)
    - [12.7 Clustering Basics](Module12_Proxmox_Virtual_Environment.md#127-clustering-basics)
    - [12.8 Future Technologies in Proxmox VE 9](Module12_Proxmox_Virtual_Environment.md#128-future-technologies-in-proxmox-ve-9)

13. **[Module 13: OpenSSH Best Practices](Module13_OpenSSH_Best_Practices.md)**
    - [13.1 SSH Key Generation and Management](Module13_OpenSSH_Best_Practices.md#131-ssh-key-generation-and-management)
    - [13.2 Secure Key Distribution](Module13_OpenSSH_Best_Practices.md#132-secure-key-distribution)
    - [13.3 SSH Server Security Configuration](Module13_OpenSSH_Best_Practices.md#133-ssh-server-security-configuration)
    - [13.5 SSH Security Best Practices](Module13_OpenSSH_Best_Practices.md#135-ssh-security-best-practices)
    - [13.6 Practical Labs and Troubleshooting](Module13_OpenSSH_Best_Practices.md#136-practical-labs-and-troubleshooting)

14. **[Module 14: Proxmox Infrastructure Automation](Module14_Proxmox_Infrastructure_Automation.md)**
    - [14.1 Infrastructure as Code Fundamentals](Module14_Proxmox_Infrastructure_Automation.md#141-infrastructure-as-code-fundamentals)
    - [14.2 Terraform with Proxmox](Module14_Proxmox_Infrastructure_Automation.md#142-terraform-with-proxmox)
    - [14.3 Advanced Terraform Practices](Module14_Proxmox_Infrastructure_Automation.md#143-advanced-terraform-practices)
    - [14.4 Ansible Configuration Management](Module14_Proxmox_Infrastructure_Automation.md#144-ansible-configuration-management)
    - [14.5 Advanced Ansible Techniques](Module14_Proxmox_Infrastructure_Automation.md#145-advanced-ansible-techniques)
    - [14.6 Cloud-Init Integration](Module14_Proxmox_Infrastructure_Automation.md#146-cloud-init-integration)
    - [14.7 Secrets Management](Module14_Proxmox_Infrastructure_Automation.md#147-secrets-management)
    - [14.8 Testing and Validation](Module14_Proxmox_Infrastructure_Automation.md#148-testing-and-validation)
    - [14.9 CI/CD Pipeline Integration](Module14_Proxmox_Infrastructure_Automation.md#149-cicd-pipeline-integration)
    - [14.10 Monitoring and Observability](Module14_Proxmox_Infrastructure_Automation.md#1410-monitoring-and-observability)

15. **[Module 15: Git & GitHub Setup with SSH Access](Module15_Git_GitHub_SSH_Setup.md)**
    - [15.1 SSH Key Setup for GitHub](Module15_Git_GitHub_SSH_Setup.md#151-ssh-key-setup-for-github)
    - [15.2 Git Installation and Basic Configuration](Module15_Git_GitHub_SSH_Setup.md#152-git-installation-and-basic-configuration)
    - [15.3 Basic Git Operations and Workflow](Module15_Git_GitHub_SSH_Setup.md#153-basic-git-operations-and-workflow)
    - [15.4 GitHub Integration and Collaboration](Module15_Git_GitHub_SSH_Setup.md#154-github-integration-and-collaboration)
    - [15.5 File Management with .gitignore](Module15_Git_GitHub_SSH_Setup.md#155-file-management-with-gitignore)
    - [15.6 Practical Git Workflows](Module15_Git_GitHub_SSH_Setup.md#156-practical-git-workflows)
    - [15.7 Troubleshooting Common Issues](Module15_Git_GitHub_SSH_Setup.md#157-troubleshooting-common-issues)
    - [15.8 Lab Exercises](Module15_Git_GitHub_SSH_Setup.md#158-lab-exercises)

---

## 📋 Training Program Structure

Each comprehensive module contains:

### 🎯 **Core Components**
- **Overview & Learning Objectives** - Clear goals and expected outcomes
- **Detailed Topic Coverage** - 6-8 comprehensive sections per module
- **Essential Command Reference** - Comprehensive command tables with examples
- **Practical Examples** - Real-world scenarios and implementation guides
- **Hands-on Lab Exercises** - 5-7 progressive labs per module
- **Assessment Criteria** - Professional evaluation frameworks
- **Integration Guidance** - Connections to other modules and next steps

### 📊 **Learning Progression**
- **Foundation Modules (1-6)** - Core Linux administration skills
- **System Management (7-10)** - Advanced system configuration and automation
- **Infrastructure Modules (11-12)** - Enterprise storage and virtualization
- **DevOps Integration (13-15)** - Security, automation, and version control

### 🔧 **Practical Focus**
- Enterprise-grade configurations and best practices
- Real-world automation scenarios and use cases
- Comprehensive security implementations
- Professional development workflows and tools
- Industry-standard compliance and governance

---

## 🚀 **Getting Started**

### Prerequisites
- Experience with Windows system administration
- Basic understanding of networking concepts
- Familiarity with virtualization technologies
- Access to lab environment (physical or virtual machines)

### Recommended Learning Path
1. **Start with Module 1** for Linux fundamentals and philosophy
2. **Progress sequentially** through Modules 2-10 for core skills
3. **Advance to Modules 11-12** for enterprise infrastructure
4. **Complete with Modules 13-15** for DevOps automation mastery

### Lab Environment Setup
- **Virtual Machines**: 2-4 VMs with different Linux distributions
- **Storage**: Sufficient disk space for ZFS and storage labs
- **Network**: Isolated lab network for security testing
- **Tools**: Access to Proxmox VE, Git, and automation tools

---

**🎓 Ready to transform your infrastructure skills?** Start with [Module 1: Linux Distributions & Philosophy](Module1_Linux_Distributions_and_Philosophy.md) and begin your journey from Windows sysadmin to DevOps automation expert!

Feel free to fork, contribute, or raise issues. Let's build your team's next-generation infrastructure together! 🚀