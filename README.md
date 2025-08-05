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
   - [2.1 Linux Filesystem Hierarchy Standard (FHS)](Module2_Filesystem_Hierarchy_and_Permissions.md#21-linux-filesystem-hierarchy-standard-fhs)
   - [2.2 File and Directory Permissions](Module2_Filesystem_Hierarchy_and_Permissions.md#22-file-and-directory-permissions)
   - [2.3 Advanced Permission Systems](Module2_Filesystem_Hierarchy_and_Permissions.md#23-advanced-permission-systems)
   - [2.4 File Attributes and Extended Attributes](Module2_Filesystem_Hierarchy_and_Permissions.md#24-file-attributes-and-extended-attributes)
   - [2.5 Security Contexts and MAC Systems](Module2_Filesystem_Hierarchy_and_Permissions.md#25-security-contexts-and-mac-systems)

3. **[Module 3: Command-Line Essentials](Module3_Command-Line_Essentials.md)**
   - [3.1 Shell Fundamentals and Environment](Module3_Command-Line_Essentials.md#31-shell-fundamentals-and-environment)
   - [3.2 File and Directory Operations](Module3_Command-Line_Essentials.md#32-file-and-directory-operations)
   - [3.3 Text Processing and Data Manipulation](Module3_Command-Line_Essentials.md#33-text-processing-and-data-manipulation)
   - [3.4 Process and System Management](Module3_Command-Line_Essentials.md#34-process-and-system-management)
   - [3.5 Search and Information Gathering](Module3_Command-Line_Essentials.md#35-search-and-information-gathering)
   - [3.6 Advanced Command Line Techniques](Module3_Command-Line_Essentials.md#36-advanced-command-line-techniques)

4. **[Module 4: Package Management](Module4_Package_Management.md)**
   - [4.1 Package Management Fundamentals](Module4_Package_Management.md#41-package-management-fundamentals)
   - [4.2 APT Package Management (Debian/Ubuntu)](Module4_Package_Management.md#42-apt-package-management-debianubuntu)
   - [4.3 YUM/DNF Package Management (RHEL/CentOS/Fedora)](Module4_Package_Management.md#43-yumdnf-package-management-rhelcentosfedora)
   - [4.4 Advanced Package Operations](Module4_Package_Management.md#44-advanced-package-operations)
   - [4.5 Repository Management and Third-Party Sources](Module4_Package_Management.md#45-repository-management-and-third-party-sources)
   - [4.6 Package Building and Custom Repositories](Module4_Package_Management.md#46-package-building-and-custom-repositories)

5. **[Module 5: Processes & Services](Module5_Processes_and_Services.md)**
   - [5.1 Process Basics (Beginner)](Module5_Processes_and_Services.md#51-process-basics-beginner)
   - [5.2 Process Monitoring (Intermediate)](Module5_Processes_and_Services.md#52-process-monitoring-intermediate)
   - [5.3 Process Control (Intermediate)](Module5_Processes_and_Services.md#53-process-control-intermediate)
   - [5.4 Basic Service Management (Intermediate)](Module5_Processes_and_Services.md#54-basic-service-management-intermediate)
   - [5.5 Essential Systemd Operations (Advanced)](Module5_Processes_and_Services.md#55-essential-systemd-operations-advanced)
   - [Essential Command Reference](Module5_Processes_and_Services.md#essential-command-reference)
   - [Quick Start Commands](Module5_Processes_and_Services.md#quick-start-commands)
   - [Understanding Linux Service Management Evolution](Module5_Processes_and_Services.md#understanding-linux-service-management-evolution)
   - [Practical Examples](Module5_Processes_and_Services.md#practical-examples)
   - [Lab Exercises](Module5_Processes_and_Services.md#lab-exercises-45-minutes-total)
   - [Best Practices](Module5_Processes_and_Services.md#best-practices)
   - [Troubleshooting](Module5_Processes_and_Services.md#troubleshooting)
   - [Summary](Module5_Processes_and_Services.md#summary)
   - [Next Steps](Module5_Processes_and_Services.md#next-steps)

6. **[Module 6: Users, Groups & Authentication](Module6_Users_Groups_and_Authentication.md)**
   - [6.1 User and Group Management](Module6_Users_Groups_and_Authentication.md#61-user-and-group-management)
   - [6.2 Authentication Systems and PAM](Module6_Users_Groups_and_Authentication.md#62-authentication-systems-and-pam)
   - [6.3 Access Control and Security](Module6_Users_Groups_and_Authentication.md#63-access-control-and-security)
   - [6.4 Directory Services Integration](Module6_Users_Groups_and_Authentication.md#64-directory-services-integration)
   - [6.5 Multi-Factor Authentication](Module6_Users_Groups_and_Authentication.md#65-multi-factor-authentication)
   - [6.6 Enterprise Identity Management](Module6_Users_Groups_and_Authentication.md#66-enterprise-identity-management)

7. **[Module 7: Networking Fundamentals](Module7_Networking_Fundamentals.md)**
   - [7.1 Modern Network Interface Management](Module7_Networking_Fundamentals.md#71-modern-network-interface-management)
   - [7.2 IP Address Configuration and Management](Module7_Networking_Fundamentals.md#72-ip-address-configuration-and-management)
   - [7.3 DNS Resolution and Host Management](Module7_Networking_Fundamentals.md#73-dns-resolution-and-host-management)
   - [7.4 Network Connectivity Diagnostics](Module7_Networking_Fundamentals.md#74-network-connectivity-diagnostics)
   - [7.5 SSH Security and Hardening](Module7_Networking_Fundamentals.md#75-ssh-security-and-hardening)
   - [7.6 Comprehensive Firewall Management](Module7_Networking_Fundamentals.md#76-comprehensive-firewall-management)
   - [7.7 Network Security Best Practices](Module7_Networking_Fundamentals.md#77-network-security-best-practices)

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
   - [9.5 Advanced Input/Output Operations](Module9_Shell_Scripting_Fundamentals.md#95-advanced-inputoutput-operations)
   - [9.6 Error Handling and Debugging](Module9_Shell_Scripting_Fundamentals.md#96-error-handling-and-debugging)
   - [9.7 System Integration and Automation](Module9_Shell_Scripting_Fundamentals.md#97-system-integration-and-automation)
   - [9.8 Enterprise Script Development](Module9_Shell_Scripting_Fundamentals.md#98-enterprise-script-development)

10. **[Module 10: Storage & Filesystem Management](Module10_Storage_and_Filesystem_Management.md)**
    - [10.1 Storage Fundamentals and Partition Management](Module10_Storage_and_Filesystem_Management.md#101-storage-fundamentals-and-partition-management)
    - [10.2 Filesystem Creation and Advanced Tuning](Module10_Storage_and_Filesystem_Management.md#102-filesystem-creation-and-advanced-tuning)
    - [10.3 Logical Volume Manager (LVM) Deep Dive](Module10_Storage_and_Filesystem_Management.md#103-logical-volume-manager-lvm-deep-dive)
    - [10.4 Software and Hardware RAID Implementation](Module10_Storage_and_Filesystem_Management.md#104-software-and-hardware-raid-implementation)
    - [10.5 Storage Performance Optimization](Module10_Storage_and_Filesystem_Management.md#105-storage-performance-optimization)
    - [10.6 Backup and Recovery Strategies](Module10_Storage_and_Filesystem_Management.md#106-backup-and-recovery-strategies)
    - [10.7 Network Storage and Clustering](Module10_Storage_and_Filesystem_Management.md#107-network-storage-and-clustering)
    - [10.8 Storage Security and Encryption](Module10_Storage_and_Filesystem_Management.md#108-storage-security-and-encryption)
 
### 🚀 Advanced DevOps & Infrastructure Automation
 
11. **[Module 11: ZFS Fundamentals](Module11_ZFS_Fundamentals.md)**
    - [11.1 ZFS Architecture and Core Concepts](Module11_ZFS_Fundamentals.md#111-zfs-architecture-and-core-concepts)
    - [11.2 Storage Pool (zpool) Management](Module11_ZFS_Fundamentals.md#112-storage-pool-zpool-management)
    - [11.3 Dataset and Volume Administration](Module11_ZFS_Fundamentals.md#113-dataset-and-volume-administration)
    - [11.4 Advanced ZFS Features](Module11_ZFS_Fundamentals.md#114-advanced-zfs-features)
    - [11.5 Performance Tuning and Optimization](Module11_ZFS_Fundamentals.md#115-performance-tuning-and-optimization)
    - [11.6 Backup and Replication Strategies](Module11_ZFS_Fundamentals.md#116-backup-and-replication-strategies)
    - [11.7 Disaster Recovery and High Availability](Module11_ZFS_Fundamentals.md#117-disaster-recovery-and-high-availability)
    - [11.8 Enterprise Integration and Monitoring](Module11_ZFS_Fundamentals.md#118-enterprise-integration-and-monitoring)

12. **[Module 12: Proxmox Virtual Environment](Module12_Proxmox_Virtual_Environment.md)**
    - [12.1 Proxmox VE Installation and Initial Configuration](Module12_Proxmox_Virtual_Environment.md#121-proxmox-ve-installation-and-initial-configuration)
    - [12.2 Virtual Machine Management and Configuration](Module12_Proxmox_Virtual_Environment.md#122-virtual-machine-management-and-configuration)
    - [12.3 Container Technology with LXC](Module12_Proxmox_Virtual_Environment.md#123-container-technology-with-lxc)
    - [12.4 Storage Configuration and Management](Module12_Proxmox_Virtual_Environment.md#124-storage-configuration-and-management)
    - [12.5 Networking and Security](Module12_Proxmox_Virtual_Environment.md#125-networking-and-security)
    - [12.6 Cluster Configuration and High Availability](Module12_Proxmox_Virtual_Environment.md#126-cluster-configuration-and-high-availability)
    - [12.7 Backup, Disaster Recovery, and Migration](Module12_Proxmox_Virtual_Environment.md#127-backup-disaster-recovery-and-migration)
    - [12.8 Performance Monitoring and Optimization](Module12_Proxmox_Virtual_Environment.md#128-performance-monitoring-and-optimization)

13. **[Module 13: OpenSSH Best Practices](Module13_OpenSSH_Best_Practices.md)**
    - [13.1 SSH Architecture and Security Fundamentals](Module13_OpenSSH_Best_Practices.md#131-ssh-architecture-and-security-fundamentals)
    - [13.2 Key-Based Authentication and Management](Module13_OpenSSH_Best_Practices.md#132-key-based-authentication-and-management)
    - [13.3 Server Hardening and Configuration](Module13_OpenSSH_Best_Practices.md#133-server-hardening-and-configuration)
    - [13.4 Advanced SSH Features and Tunneling](Module13_OpenSSH_Best_Practices.md#134-advanced-ssh-features-and-tunneling)
    - [13.5 Enterprise Access Control and Monitoring](Module13_OpenSSH_Best_Practices.md#135-enterprise-access-control-and-monitoring)
    - [13.6 SSH Automation and Integration](Module13_OpenSSH_Best_Practices.md#136-ssh-automation-and-integration)
    - [13.7 Certificate Authority and Enterprise PKI](Module13_OpenSSH_Best_Practices.md#137-certificate-authority-and-enterprise-pki)
    - [13.8 Incident Response and Forensics](Module13_OpenSSH_Best_Practices.md#138-incident-response-and-forensics)

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
    - [15.1 Enterprise SSH Key Management and Authentication](Module15_Git_GitHub_SSH_Setup.md#151-enterprise-ssh-key-management-and-authentication)
    - [15.2 Advanced Git Configuration and Workflow Architecture](Module15_Git_GitHub_SSH_Setup.md#152-advanced-git-configuration-and-workflow-architecture)
    - [15.3 GitHub Enterprise Integration and Administration](Module15_Git_GitHub_SSH_Setup.md#153-github-enterprise-integration-and-administration)
    - [15.4 Infrastructure as Code Version Control Integration](Module15_Git_GitHub_SSH_Setup.md#154-infrastructure-as-code-version-control-integration)
    - [15.5 Automated Quality Assurance and Security Validation](Module15_Git_GitHub_SSH_Setup.md#155-automated-quality-assurance-and-security-validation)
    - [15.6 Professional Collaboration and Code Review Workflows](Module15_Git_GitHub_SSH_Setup.md#156-professional-collaboration-and-code-review-workflows)
    - [15.7 Enterprise Governance and Compliance Management](Module15_Git_GitHub_SSH_Setup.md#157-enterprise-governance-and-compliance-management)
    - [15.8 Advanced Integration and Automation Patterns](Module15_Git_GitHub_SSH_Setup.md#158-advanced-integration-and-automation-patterns)

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