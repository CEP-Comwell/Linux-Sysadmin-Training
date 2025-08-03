# Module 6: Users, Groups & Authentication

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [6.1 User Account Fundamentals](#61-user-account-fundamentals)
  - [6.2 Advanced User Management](#62-advanced-user-management)
  - [6.3 Group Management and Access Control](#63-group-management-and-access-control)
  - [6.4 Sudo and Privilege Escalation](#64-sudo-and-privilege-escalation)
  - [6.5 Authentication Systems](#65-authentication-systems)
  - [6.6 SSH and Key Management](#66-ssh-and-key-management)
  - [6.7 PAM and Security Policies](#67-pam-and-security-policies)
  - [6.8 Enterprise Authentication Integration](#68-enterprise-authentication-integration)
  - [6.9 Security Auditing and Compliance](#69-security-auditing-and-compliance)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [User and Group Management](#user-and-group-management)
  - [Advanced Authentication Configuration](#advanced-authentication-configuration)
  - [SSH Security and Key Management](#ssh-security-and-key-management)
  - [Security Auditing Scripts](#security-auditing-scripts)
  - [Enterprise Integration Examples](#enterprise-integration-examples)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Comprehensive User Management System](#lab-1-comprehensive-user-management-system)
  - [Lab 2: Authentication Security Implementation](#lab-2-authentication-security-implementation)
  - [Lab 3: Enterprise Directory Integration](#lab-3-enterprise-directory-integration)
  - [Lab 4: Security Compliance and Auditing](#lab-4-security-compliance-and-auditing)
- [Best Practices Summary](#best-practices-summary)
- [Troubleshooting Guide](#troubleshooting-guide)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
Master comprehensive user and group management, authentication systems, and access control mechanisms essential for enterprise Linux environments. This module covers everything from basic user administration to advanced authentication integration, security policies, and compliance frameworks.

**Key Learning Outcomes:**
- Implement enterprise-grade user and group management with automated provisioning
- Configure advanced authentication systems including LDAP, Kerberos, and multi-factor authentication
- Design and deploy comprehensive access control policies with role-based permissions
- Integrate Linux systems with enterprise directory services and identity management platforms
- Implement security auditing, compliance monitoring, and automated threat detection
- Deploy and manage SSH infrastructure with advanced security configurations

## Learning Objectives
By the end of this module, you will be able to:

1. **Master User Administration**: Implement comprehensive user lifecycle management with automated provisioning and deprovisioning
2. **Configure Authentication Systems**: Deploy and integrate multiple authentication methods including PAM, LDAP, and Kerberos
3. **Implement Access Control**: Design role-based access control systems with fine-grained permissions and privilege escalation
4. **Manage SSH Infrastructure**: Configure secure SSH environments with advanced key management and access controls
5. **Integrate Enterprise Systems**: Connect Linux systems with Active Directory, LDAP, and other enterprise identity providers
6. **Ensure Security Compliance**: Implement security auditing, monitoring, and compliance frameworks for enterprise environments
7. **Automate Identity Management**: Create automated systems for user provisioning, access reviews, and security monitoring
8. **Troubleshoot Authentication Issues**: Diagnose and resolve complex authentication and authorization problems

## Topics

### 6.1 User Account Fundamentals
- User account types: system users, service accounts, regular users, and administrative accounts
- User identification systems: UID/GID management, namespace considerations, and enterprise scaling
- Core account files: `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow` deep dive
- Home directory management: templates, quotas, and automated provisioning
- User environment configuration: shells, profiles, and environment variables
- Account lifecycle management: creation, modification, suspension, and deletion procedures

### 6.2 Advanced User Management
- Automated user provisioning and deprovisioning workflows
- Bulk user operations and template-based account creation
- User account security hardening and compliance requirements
- Home directory encryption and data protection policies
- User resource quotas and limits enforcement
- Account delegation and administrative role separation

### 6.3 Group Management and Access Control
- Group hierarchy design and nested group management
- Role-based access control (RBAC) implementation strategies
- Dynamic group membership and automated group assignment
- Group-based file permissions and access control lists (ACLs)
- Service account management and application-specific groups
- Cross-system group synchronization and consistency

### 6.4 Sudo and Privilege Escalation
- Advanced sudoers configuration with complex rule sets
- Least privilege principle implementation and enforcement
- Sudo logging, auditing, and security monitoring
- Alternative privilege escalation methods and tools
- Session recording and command auditing for compliance
- Automated sudo rule management and deployment

### 6.5 Authentication Systems
- PAM (Pluggable Authentication Modules) architecture and advanced configuration
- Multi-factor authentication implementation and integration
- Single sign-on (SSO) solutions and federation protocols
- Password policies, complexity requirements, and rotation strategies
- Account lockout mechanisms and intrusion detection
- Authentication logging and security event correlation

### 6.6 SSH and Key Management
- SSH server hardening and advanced security configurations
- Public key infrastructure (PKI) for SSH key management
- Certificate-based SSH authentication and certificate authorities
- SSH key rotation, lifecycle management, and compliance
- Jump hosts, bastion servers, and secure access patterns
- SSH tunneling, port forwarding, and secure remote access

### 6.7 PAM and Security Policies
- Custom PAM module development and integration
- Advanced password quality enforcement and policy management
- Session security controls and resource limitations
- Integration with external authentication providers and APIs
- Security policy automation and enforcement mechanisms
- Compliance framework integration and reporting

### 6.8 Enterprise Authentication Integration
- Active Directory integration with Samba and SSSD
- LDAP directory services configuration and management
- Kerberos authentication and single sign-on implementation
- RADIUS authentication for network access control
- SAML and OAuth integration for web-based authentication
- Identity provider federation and trust relationships

### 6.9 Security Auditing and Compliance
- User activity monitoring and behavioral analysis
- Access review automation and compliance reporting
- Security event correlation and threat detection
- Privileged access monitoring and session recording
- Compliance framework implementation (SOX, HIPAA, PCI-DSS)
- Automated security assessments and vulnerability management

## Essential Command Reference

### User Management Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `useradd` | Create user account | `-m`, `-s`, `-u`, `-g`, `-G` | `useradd -m -s /bin/bash -G sudo john` |
| `usermod` | Modify user account | `-aG`, `-L`, `-U`, `-e`, `-f` | `usermod -aG developers john` |
| `userdel` | Delete user account | `-r`, `-f` | `userdel -r john` |
| `passwd` | Change password | `-S`, `-l`, `-u`, `-e` | `passwd -S john` |
| `chage` | Change password aging | `-l`, `-E`, `-M`, `-m`, `-W` | `chage -E 2025-12-31 john` |
| `id` | Display user/group IDs | `-u`, `-g`, `-G`, `-n` | `id -G john` |

### Group Management Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `groupadd` | Create group | `-g`, `-r` | `groupadd -g 1500 developers` |
| `groupmod` | Modify group | `-n`, `-g` | `groupmod -n devs developers` |
| `groupdel` | Delete group | None | `groupdel developers` |
| `gpasswd` | Manage group membership | `-a`, `-d`, `-A`, `-M` | `gpasswd -a john developers` |
| `groups` | Show user's groups | None | `groups john` |
| `getent` | Query system databases | `passwd`, `group`, `shadow` | `getent group developers` |

### Authentication and Access Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `sudo` | Execute as another user | `-u`, `-i`, `-l`, `-k` | `sudo -u www-data command` |
| `su` | Switch user | `-`, `-l`, `-c` | `su - john` |
| `visudo` | Edit sudoers file safely | None | `visudo` |
| `ssh-keygen` | Generate SSH keys | `-t`, `-b`, `-C`, `-f` | `ssh-keygen -t ed25519 -C "user@host"` |
| `ssh-copy-id` | Copy SSH public key | `-i` | `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host` |
| `lastlog` | Show last login times | `-u`, `-t` | `lastlog -u john` |

### Monitoring and Auditing Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `who` | Show logged in users | `-a`, `-b`, `-H` | `who -a` |
| `w` | Show user activity | `-h`, `-s` | `w john` |
| `last` | Show login history | `-n`, `-F`, `-i` | `last -n 10 john` |
| `lastb` | Show failed logins | `-n`, `-F` | `lastb -n 20` |
| `aureport` | Generate audit reports | `-au`, `-m`, `-x` | `aureport -au --summary` |
| `ausearch` | Search audit logs | `-m`, `-ts`, `-te`, `-u` | `ausearch -m USER_LOGIN -ts today` |

## Practical Examples

### User and Group Management

#### Comprehensive User Management Script
```bash
#!/bin/bash
# user-manager.sh - Enterprise user management automation

# Configuration
USER_HOME_BASE="/home"
USER_SHELL_DEFAULT="/bin/bash"
USER_GROUPS_DEFAULT="users"
USER_SKEL_DIR="/etc/skel"
AUDIT_LOG="/var/log/user-management.log"

# Logging function
log_action() {
    local action="$1"
    local user="$2"
    local details="$3"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    echo "$timestamp - $action - User: $user - Details: $details" >> "$AUDIT_LOG"
    echo "$timestamp - $action - User: $user - Details: $details"
}

# Create user with comprehensive options
create_user() {
    local username="$1"
    local full_name="$2"
    local department="$3"
    local expiry_date="$4"
    local additional_groups="$5"
    
    if [[ -z "$username" ]]; then
        echo "Usage: create_user <username> [full_name] [department] [expiry_date] [additional_groups]"
        return 1
    fi
    
    # Check if user already exists
    if id "$username" &>/dev/null; then
        log_action "CREATE_FAILED" "$username" "User already exists"
        return 1
    fi
    
    echo "Creating user: $username"
    
    # Determine next available UID
    local next_uid=$(awk -F: '$3 >= 1000 && $3 < 65534 {uid[$3]=1} END {for(i=1000;i<65534;i++) if(!uid[i]) {print i; exit}}' /etc/passwd)
    
    # Create user account
    local useradd_cmd="useradd"
    useradd_cmd+=" -m"                                    # Create home directory
    useradd_cmd+=" -s $USER_SHELL_DEFAULT"               # Set shell
    useradd_cmd+=" -d $USER_HOME_BASE/$username"         # Set home directory
    useradd_cmd+=" -k $USER_SKEL_DIR"                    # Copy skeleton files
    useradd_cmd+=" -u $next_uid"                         # Set UID
    
    # Add GECOS information
    if [[ -n "$full_name" ]]; then
        local gecos="$full_name"
        [[ -n "$department" ]] && gecos+=",,$department"
        useradd_cmd+=" -c \"$gecos\""
    fi
    
    # Set expiry date
    if [[ -n "$expiry_date" ]]; then
        useradd_cmd+=" -e $expiry_date"
    fi
    
    # Execute user creation
    if eval "sudo $useradd_cmd $username"; then
        log_action "CREATE_SUCCESS" "$username" "UID: $next_uid, Home: $USER_HOME_BASE/$username"
        
        # Add to additional groups
        if [[ -n "$additional_groups" ]]; then
            if sudo usermod -aG "$additional_groups" "$username"; then
                log_action "GROUP_ADD" "$username" "Added to groups: $additional_groups"
            else
                log_action "GROUP_ADD_FAILED" "$username" "Failed to add to groups: $additional_groups"
            fi
        fi
        
        # Set initial password (force change on first login)
        local temp_password=$(openssl rand -base64 12)
        echo "$username:$temp_password" | sudo chpasswd
        sudo chage -d 0 "$username"  # Force password change on first login
        
        # Set home directory permissions
        sudo chmod 750 "$USER_HOME_BASE/$username"
        sudo chown "$username:$username" "$USER_HOME_BASE/$username"
        
        log_action "SETUP_COMPLETE" "$username" "Initial password set, home directory configured"
        echo "User $username created successfully"
        echo "Temporary password: $temp_password (must be changed on first login)"
        
    else
        log_action "CREATE_FAILED" "$username" "useradd command failed"
        return 1
    fi
}

# Modify user account
modify_user() {
    local username="$1"
    local action="$2"
    local value="$3"
    
    if [[ -z "$username" || -z "$action" ]]; then
        echo "Usage: modify_user <username> <action> [value]"
        echo "Actions: lock, unlock, expire, extend, add_group, remove_group, change_shell"
        return 1
    fi
    
    # Check if user exists
    if ! id "$username" &>/dev/null; then
        log_action "MODIFY_FAILED" "$username" "User does not exist"
        return 1
    fi
    
    case "$action" in
        "lock")
            if sudo usermod -L "$username"; then
                log_action "ACCOUNT_LOCKED" "$username" "Account locked"
            else
                log_action "LOCK_FAILED" "$username" "Failed to lock account"
            fi
            ;;
        "unlock")
            if sudo usermod -U "$username"; then
                log_action "ACCOUNT_UNLOCKED" "$username" "Account unlocked"
            else
                log_action "UNLOCK_FAILED" "$username" "Failed to unlock account"
            fi
            ;;
        "expire")
            if [[ -n "$value" ]]; then
                if sudo usermod -e "$value" "$username"; then
                    log_action "EXPIRY_SET" "$username" "Account expires: $value"
                else
                    log_action "EXPIRY_FAILED" "$username" "Failed to set expiry: $value"
                fi
            else
                echo "Expiry date required for expire action"
                return 1
            fi
            ;;
        "extend")
            if sudo usermod -e "" "$username"; then
                log_action "EXPIRY_REMOVED" "$username" "Account expiry removed"
            else
                log_action "EXTEND_FAILED" "$username" "Failed to remove expiry"
            fi
            ;;
        "add_group")
            if [[ -n "$value" ]]; then
                if sudo usermod -aG "$value" "$username"; then
                    log_action "GROUP_ADDED" "$username" "Added to group: $value"
                else
                    log_action "GROUP_ADD_FAILED" "$username" "Failed to add to group: $value"
                fi
            else
                echo "Group name required for add_group action"
                return 1
            fi
            ;;
        "remove_group")
            if [[ -n "$value" ]]; then
                if sudo gpasswd -d "$username" "$value"; then
                    log_action "GROUP_REMOVED" "$username" "Removed from group: $value"
                else
                    log_action "GROUP_REMOVE_FAILED" "$username" "Failed to remove from group: $value"
                fi
            else
                echo "Group name required for remove_group action"
                return 1
            fi
            ;;
        "change_shell")
            if [[ -n "$value" ]]; then
                if sudo usermod -s "$value" "$username"; then
                    log_action "SHELL_CHANGED" "$username" "Shell changed to: $value"
                else
                    log_action "SHELL_CHANGE_FAILED" "$username" "Failed to change shell to: $value"
                fi
            else
                echo "Shell path required for change_shell action"
                return 1
            fi
            ;;
        *)
            echo "Unknown action: $action"
            return 1
            ;;
    esac
}

# Delete user account
delete_user() {
    local username="$1"
    local remove_home="${2:-yes}"
    local archive_home="${3:-no}"
    
    if [[ -z "$username" ]]; then
        echo "Usage: delete_user <username> [remove_home:yes/no] [archive_home:yes/no]"
        return 1
    fi
    
    # Check if user exists
    if ! id "$username" &>/dev/null; then
        log_action "DELETE_FAILED" "$username" "User does not exist"
        return 1
    fi
    
    # Check if user is currently logged in
    if who | grep -q "^$username "; then
        echo "Warning: User $username is currently logged in"
        read -p "Do you want to continue? (y/N): " confirm
        if [[ "$confirm" != "y" && "$confirm" != "Y" ]]; then
            log_action "DELETE_CANCELLED" "$username" "User deletion cancelled - user logged in"
            return 1
        fi
        
        # Kill user processes
        sudo pkill -u "$username"
        log_action "PROCESSES_KILLED" "$username" "User processes terminated"
    fi
    
    # Archive home directory if requested
    if [[ "$archive_home" == "yes" && -d "$USER_HOME_BASE/$username" ]]; then
        local archive_dir="/var/backups/user-archives"
        sudo mkdir -p "$archive_dir"
        local archive_file="$archive_dir/${username}_$(date +%Y%m%d_%H%M%S).tar.gz"
        
        if sudo tar -czf "$archive_file" -C "$USER_HOME_BASE" "$username"; then
            log_action "HOME_ARCHIVED" "$username" "Home directory archived to: $archive_file"
        else
            log_action "ARCHIVE_FAILED" "$username" "Failed to archive home directory"
        fi
    fi
    
    # Delete user account
    local userdel_options=""
    if [[ "$remove_home" == "yes" ]]; then
        userdel_options="-r"
    fi
    
    if sudo userdel $userdel_options "$username"; then
        log_action "DELETE_SUCCESS" "$username" "User account deleted (remove_home: $remove_home)"
        echo "User $username deleted successfully"
    else
        log_action "DELETE_FAILED" "$username" "userdel command failed"
        return 1
    fi
}

# Bulk user operations from CSV
bulk_user_operations() {
    local csv_file="$1"
    local operation="$2"
    
    if [[ -z "$csv_file" || ! -f "$csv_file" ]]; then
        echo "Usage: bulk_user_operations <csv_file> <operation>"
        echo "Operations: create, delete, modify"
        echo "CSV format for create: username,full_name,department,expiry_date,additional_groups"
        return 1
    fi
    
    echo "Processing bulk $operation operations from: $csv_file"
    
    local line_num=0
    while IFS=',' read -r username full_name department expiry_date additional_groups; do
        ((line_num++))
        
        # Skip header line
        if [[ $line_num -eq 1 ]]; then
            continue
        fi
        
        # Skip empty lines
        if [[ -z "$username" ]]; then
            continue
        fi
        
        echo "Processing line $line_num: $username"
        
        case "$operation" in
            "create")
                create_user "$username" "$full_name" "$department" "$expiry_date" "$additional_groups"
                ;;
            "delete")
                delete_user "$username"
                ;;
            *)
                echo "Unsupported bulk operation: $operation"
                return 1
                ;;
        esac
        
        sleep 1  # Brief pause between operations
    done < "$csv_file"
    
    log_action "BULK_OPERATION" "MULTIPLE" "$operation completed for $csv_file"
    echo "Bulk $operation operation completed"
}

# Generate user report
generate_user_report() {
    local output_file="${1:-/tmp/user_report_$(date +%Y%m%d_%H%M%S).html}"
    
    echo "Generating user report: $output_file"
    
    cat > "$output_file" << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>Linux User Management Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        table { border-collapse: collapse; width: 100%; margin: 20px 0; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
        .header { background-color: #f0f0f0; padding: 10px; border-radius: 5px; }
        .warning { background-color: #fff3cd; padding: 10px; border-left: 5px solid #ffc107; }
        .critical { background-color: #f8d7da; padding: 10px; border-left: 5px solid #dc3545; }
    </style>
</head>
<body>
    <div class="header">
        <h1>Linux User Management Report</h1>
        <p>Generated: REPORT_TIMESTAMP</p>
        <p>Hostname: HOSTNAME</p>
    </div>
EOF

    # Replace placeholders
    sed -i "s/REPORT_TIMESTAMP/$(date)/" "$output_file"
    sed -i "s/HOSTNAME/$(hostname)/" "$output_file"
    
    # Add user statistics
    cat >> "$output_file" << EOF
    <h2>User Statistics</h2>
    <table>
        <tr><th>Metric</th><th>Count</th></tr>
        <tr><td>Total Users</td><td>$(getent passwd | wc -l)</td></tr>
        <tr><td>Regular Users (UID >= 1000)</td><td>$(getent passwd | awk -F: '$3 >= 1000 && $3 < 65534' | wc -l)</td></tr>
        <tr><td>System Users (UID < 1000)</td><td>$(getent passwd | awk -F: '$3 < 1000' | wc -l)</td></tr>
        <tr><td>Users with Shell Access</td><td>$(getent passwd | grep -E '(bash|zsh|fish|ksh)$' | wc -l)</td></tr>
        <tr><td>Total Groups</td><td>$(getent group | wc -l)</td></tr>
    </table>
EOF

    # Add user list
    echo "    <h2>Regular Users (UID >= 1000)</h2>" >> "$output_file"
    echo "    <table>" >> "$output_file"
    echo "        <tr><th>Username</th><th>UID</th><th>GID</th><th>Full Name</th><th>Home Directory</th><th>Shell</th><th>Last Login</th></tr>" >> "$output_file"
    
    getent passwd | awk -F: '$3 >= 1000 && $3 < 65534' | while IFS=: read username x uid gid gecos home shell; do
        local last_login=$(lastlog -u "$username" 2>/dev/null | tail -1 | awk '{for(i=4;i<=NF;i++) printf "%s ", $i; print ""}' | sed 's/Never logged in/Never/')
        echo "        <tr><td>$username</td><td>$uid</td><td>$gid</td><td>$gecos</td><td>$home</td><td>$shell</td><td>$last_login</td></tr>" >> "$output_file"
    done
    
    echo "    </table>" >> "$output_file"
    
    # Add security warnings
    echo "    <h2>Security Warnings</h2>" >> "$output_file"
    
    # Check for accounts without passwords
    local no_password_accounts=$(sudo awk -F: '($2 == "" || $2 == "!") && $3 >= 1000 {print $1}' /etc/shadow)
    if [[ -n "$no_password_accounts" ]]; then
        echo "    <div class=\"critical\">" >> "$output_file"
        echo "        <strong>Critical:</strong> Accounts without passwords found:" >> "$output_file"
        echo "        <ul>" >> "$output_file"
        for account in $no_password_accounts; do
            echo "            <li>$account</li>" >> "$output_file"
        done
        echo "        </ul>" >> "$output_file"
        echo "    </div>" >> "$output_file"
    fi
    
    # Check for duplicate UIDs
    local duplicate_uids=$(awk -F: '{print $3}' /etc/passwd | sort -n | uniq -d)
    if [[ -n "$duplicate_uids" ]]; then
        echo "    <div class=\"warning\">" >> "$output_file"
        echo "        <strong>Warning:</strong> Duplicate UIDs found: $duplicate_uids" >> "$output_file"
        echo "    </div>" >> "$output_file"
    fi
    
    # Close HTML
    echo "</body></html>" >> "$output_file"
    
    echo "Report generated: $output_file"
}

# Usage
case "${1:-help}" in
    "create")
        create_user "$2" "$3" "$4" "$5" "$6"
        ;;
    "modify")
        modify_user "$2" "$3" "$4"
        ;;
    "delete")
        delete_user "$2" "$3" "$4"
        ;;
    "bulk")
        bulk_user_operations "$2" "$3"
        ;;
    "report")
        generate_user_report "$2"
        ;;
    "help")
        echo "Usage: $0 {create|modify|delete|bulk|report} [arguments]"
        echo ""
        echo "Commands:"
        echo "  create <username> [full_name] [dept] [expiry] [groups] - Create user"
        echo "  modify <username> <action> [value]                    - Modify user"
        echo "  delete <username> [remove_home] [archive_home]        - Delete user"
        echo "  bulk <csv_file> <operation>                           - Bulk operations"
        echo "  report [output_file]                                  - Generate report"
        ;;
esac
```

#### Advanced Group Management
```bash
#!/bin/bash
# group-manager.sh - Advanced group management and access control

# Create role-based groups
create_role_groups() {
    echo "Creating role-based groups for enterprise environment..."
    
    # Administrative groups
    local admin_groups=(
        "system-admins:System Administrators:10000"
        "security-admins:Security Administrators:10001"
        "network-admins:Network Administrators:10002"
        "database-admins:Database Administrators:10003"
    )
    
    # Department groups
    local dept_groups=(
        "engineering:Engineering Department:11000"
        "operations:Operations Department:11001"
        "marketing:Marketing Department:11002"
        "sales:Sales Department:11003"
        "hr:Human Resources:11004"
        "finance:Finance Department:11005"
    )
    
    # Project groups
    local project_groups=(
        "project-alpha:Project Alpha Team:12000"
        "project-beta:Project Beta Team:12001"
        "project-gamma:Project Gamma Team:12002"
    )
    
    # Service groups
    local service_groups=(
        "web-servers:Web Server Administrators:13000"
        "app-servers:Application Server Administrators:13001"
        "db-servers:Database Server Administrators:13002"
        "monitoring:Monitoring System Access:13003"
    )
    
    # Create groups
    for groups_array in admin_groups[@] dept_groups[@] project_groups[@] service_groups[@]; do
        for group_info in "${!groups_array}"; do
            IFS=':' read -r group_name description gid <<< "$group_info"
            
            if ! getent group "$group_name" &>/dev/null; then
                if sudo groupadd -g "$gid" "$group_name"; then
                    echo "Created group: $group_name (GID: $gid)"
                    
                    # Add description to group file (if supported)
                    if [[ -f /etc/group.desc ]]; then
                        echo "$group_name:$description" | sudo tee -a /etc/group.desc >/dev/null
                    fi
                else
                    echo "Failed to create group: $group_name"
                fi
            else
                echo "Group already exists: $group_name"
            fi
        done
    done
}

# Implement group hierarchy
setup_group_hierarchy() {
    echo "Setting up group hierarchy and nested permissions..."
    
    # Create hierarchy mapping
    declare -A group_hierarchy=(
        ["system-admins"]="security-admins network-admins database-admins"
        ["engineering"]="web-servers app-servers"
        ["operations"]="monitoring db-servers"
    )
    
    # Note: Linux doesn't support nested groups natively
    # This creates sudo rules for group-based access
    cat > /tmp/group-hierarchy-sudo << 'EOF'
# Group hierarchy sudo rules
# System admins can act as other admin groups
%system-admins ALL=(ALL) ALL
%system-admins ALL=(%security-admins,%network-admins,%database-admins) ALL

# Department-specific access
%engineering ALL=(%web-servers,%app-servers) NOPASSWD: /usr/bin/systemctl restart nginx, /usr/bin/systemctl restart apache2
%operations ALL=(%monitoring,%db-servers) NOPASSWD: /usr/bin/systemctl status *, /usr/bin/journalctl -u *

# Project-based access
%project-alpha ALL=(project-alpha) ALL
%project-beta ALL=(project-beta) ALL
%project-gamma ALL=(project-gamma) ALL
EOF

    echo "Group hierarchy sudo rules created in /tmp/group-hierarchy-sudo"
    echo "Review and append to /etc/sudoers.d/group-hierarchy if appropriate"
}

# Group membership audit
audit_group_membership() {
    local output_file="${1:-/tmp/group_audit_$(date +%Y%m%d_%H%M%S).txt}"
    
    echo "Performing group membership audit..."
    echo "Group Membership Audit - $(date)" > "$output_file"
    echo "======================================" >> "$output_file"
    echo "" >> "$output_file"
    
    # List all groups with members
    echo "Groups with Members:" >> "$output_file"
    echo "-------------------" >> "$output_file"
    
    getent group | while IFS=: read group_name x gid members; do
        if [[ -n "$members" ]]; then
            echo "Group: $group_name (GID: $gid)" >> "$output_file"
            echo "Members: $members" >> "$output_file"
            echo "" >> "$output_file"
        fi
    done
    
    # List users and their group memberships
    echo "" >> "$output_file"
    echo "User Group Memberships:" >> "$output_file"
    echo "----------------------" >> "$output_file"
    
    getent passwd | awk -F: '$3 >= 1000 && $3 < 65534 {print $1}' | while read username; do
        local user_groups=$(groups "$username" 2>/dev/null | cut -d: -f2)
        echo "User: $username" >> "$output_file"
        echo "Groups: $user_groups" >> "$output_file"
        echo "" >> "$output_file"
    done
    
    # Security analysis
    echo "" >> "$output_file"
    echo "Security Analysis:" >> "$output_file"
    echo "-----------------" >> "$output_file"
    
    # Find users in admin groups
    echo "Users in administrative groups:" >> "$output_file"
    for admin_group in "sudo" "wheel" "admin" "root" "system-admins"; do
        if getent group "$admin_group" &>/dev/null; then
            local admin_users=$(getent group "$admin_group" | cut -d: -f4)
            if [[ -n "$admin_users" ]]; then
                echo "  $admin_group: $admin_users" >> "$output_file"
            fi
        fi
    done
    
    # Find empty groups
    echo "" >> "$output_file"
    echo "Empty groups:" >> "$output_file"
    getent group | awk -F: '$4 == "" {print "  " $1 " (GID: " $3 ")"}' >> "$output_file"
    
    # Find groups with single members
    echo "" >> "$output_file"
    echo "Groups with single members:" >> "$output_file"
    getent group | awk -F: '$4 != "" && gsub(/,/, "", $4) == 0 {print "  " $1 ": " $4}' >> "$output_file"
    
    echo "Group audit completed: $output_file"
}

# Clean up unused groups
cleanup_unused_groups() {
    local dry_run="${1:-yes}"
    
    echo "Cleaning up unused groups (dry_run: $dry_run)"
    
    # Find groups with no members and no files owned by them
    local unused_groups=()
    
    getent group | while IFS=: read group_name x gid members; do
        # Skip system groups (GID < 1000)
        if [[ $gid -lt 1000 ]]; then
            continue
        fi
        
        # Skip if group has members
        if [[ -n "$members" ]]; then
            continue
        fi
        
        # Check if any files are owned by this group
        local files_owned=$(find / -group "$group_name" -type f 2>/dev/null | head -1)
        if [[ -n "$files_owned" ]]; then
            continue
        fi
        
        # Check if any processes are running with this group
        local processes=$(ps -eo gid,comm | awk -v gid="$gid" '$1 == gid {print $2}' | head -1)
        if [[ -n "$processes" ]]; then
            continue
        fi
        
        unused_groups+=("$group_name")
    done
    
    if [[ ${#unused_groups[@]} -eq 0 ]]; then
        echo "No unused groups found"
        return 0
    fi
    
    echo "Found ${#unused_groups[@]} unused groups:"
    for group in "${unused_groups[@]}"; do
        echo "  - $group"
    done
    
    if [[ "$dry_run" == "no" ]]; then
        echo ""
        read -p "Do you want to delete these groups? (y/N): " confirm
        if [[ "$confirm" == "y" || "$confirm" == "Y" ]]; then
            for group in "${unused_groups[@]}"; do
                if sudo groupdel "$group"; then
                    echo "Deleted group: $group"
                else
                    echo "Failed to delete group: $group"
                fi
            done
        fi
    else
        echo ""
        echo "Run with 'no' as first argument to actually delete groups"
    fi
}

# Usage
case "${1:-help}" in
    "create-roles")
        create_role_groups
        ;;
    "setup-hierarchy")
        setup_group_hierarchy
        ;;
    "audit")
        audit_group_membership "$2"
        ;;
    "cleanup")
        cleanup_unused_groups "$2"
        ;;
    "help")
        echo "Usage: $0 {create-roles|setup-hierarchy|audit|cleanup} [arguments]"
        echo ""
        echo "Commands:"
        echo "  create-roles              - Create role-based groups"
        echo "  setup-hierarchy           - Setup group hierarchy"
        echo "  audit [output_file]       - Audit group membership"
        echo "  cleanup [dry_run:yes/no]  - Cleanup unused groups"
        ;;
esac
```

### Advanced Authentication Configuration

#### PAM Configuration Management
```bash
#!/bin/bash
# pam-config.sh - Advanced PAM configuration management

# Backup PAM configuration
backup_pam_config() {
    local backup_dir="/var/backups/pam-config-$(date +%Y%m%d_%H%M%S)"
    
    echo "Backing up PAM configuration to: $backup_dir"
    sudo mkdir -p "$backup_dir"
    
    # Backup PAM files
    sudo cp -r /etc/pam.d "$backup_dir/"
    sudo cp -r /etc/security "$backup_dir/"
    
    # Backup related files
    if [[ -f /etc/login.defs ]]; then
        sudo cp /etc/login.defs "$backup_dir/"
    fi
    
    if [[ -f /etc/default/useradd ]]; then
        sudo cp /etc/default/useradd "$backup_dir/"
    fi
    
    echo "PAM configuration backed up successfully"
    echo "Restore with: sudo cp -r $backup_dir/* /etc/"
}

# Configure password quality
configure_password_quality() {
    echo "Configuring password quality requirements..."
    
    # Create comprehensive password quality configuration
    cat > /tmp/pwquality.conf << 'EOF'
# Password quality requirements
# Minimum password length
minlen = 12

# Minimum number of character classes
minclass = 3

# Maximum number of consecutive same characters
maxrepeat = 2

# Maximum number of consecutive characters from same class
maxclasschars = 3

# Minimum number of digits
dcredit = -1

# Minimum number of uppercase characters
ucredit = -1

# Minimum number of lowercase characters
lcredit = -1

# Minimum number of other characters
ocredit = -1

# Check against dictionary words
dictcheck = 1

# Check against username
usercheck = 1

# Check against previous passwords
difok = 3

# Reject palindromes
palindrome = reject

# Check character sequences
sequence = reject

# Word-based checks
wordlist = /usr/share/dict/words
EOF

    if sudo cp /tmp/pwquality.conf /etc/security/pwquality.conf; then
        echo "Password quality configuration updated"
    else
        echo "Failed to update password quality configuration"
        return 1
    fi
    
    # Update PAM configuration for password quality
    cat > /tmp/pam-password << 'EOF'
# PAM configuration for password quality
password    requisite     pam_pwquality.so retry=3
password    [success=1 default=ignore]      pam_unix.so obscure use_authtok try_first_pass sha512
password    sufficient    pam_unix.so
password    required      pam_deny.so
EOF

    echo "PAM password configuration created in /tmp/pam-password"
    echo "Review and integrate with /etc/pam.d/common-password"
}

# Configure account lockout
configure_account_lockout() {
    local max_attempts="${1:-5}"
    local lockout_time="${2:-600}"  # 10 minutes
    
    echo "Configuring account lockout: $max_attempts attempts, ${lockout_time}s lockout"
    
    # Create account lockout configuration
    cat > /tmp/pam-auth-lockout << EOF
# Account lockout configuration
auth        required      pam_tally2.so file=/var/log/tallylog deny=$max_attempts unlock_time=$lockout_time
auth        sufficient    pam_unix.so
auth        required      pam_deny.so

# Account status check
account     required      pam_tally2.so
account     required      pam_unix.so
account     required      pam_permit.so
EOF

    echo "Account lockout PAM configuration created in /tmp/pam-auth-lockout"
    echo "Review and integrate with /etc/pam.d/common-auth and /etc/pam.d/common-account"
    
    # Create unlock script
    cat > /tmp/unlock-user.sh << 'EOF'
#!/bin/bash
# unlock-user.sh - Unlock user account after lockout

username="$1"
if [[ -z "$username" ]]; then
    echo "Usage: $0 <username>"
    exit 1
fi

echo "Unlocking user: $username"

# Reset tally counter
sudo pam_tally2 --user="$username" --reset

# Check current status
sudo pam_tally2 --user="$username"

echo "User $username unlocked"
EOF

    chmod +x /tmp/unlock-user.sh
    echo "User unlock script created: /tmp/unlock-user.sh"
}

# Configure session security
configure_session_security() {
    echo "Configuring session security controls..."
    
    # Create session limits configuration
    cat > /tmp/limits.conf << 'EOF'
# Session limits configuration
# Format: <domain> <type> <item> <value>

# Process limits
*               soft    nproc           1024
*               hard    nproc           2048

# Memory limits (MB)
*               soft    as              unlimited
*               hard    as              unlimited

# File limits
*               soft    nofile          1024
*               hard    nofile          65536

# Core dump limits
*               soft    core            0
*               hard    core            0

# Login time limits (minutes)
*               hard    maxlogins       3

# CPU time limits (minutes)
*               soft    cpu             unlimited
*               hard    cpu             unlimited

# Login session timeout (seconds)
*               soft    maxsyslogins    10

# Group-specific limits
@admin          soft    nproc           4096
@admin          hard    nproc           8192
@admin          soft    nofile          8192
@admin          hard    nofile          65536

# Developer limits
@developers     soft    nproc           2048
@developers     hard    nproc           4096
@developers     soft    nofile          4096
@developers     hard    nofile          32768
EOF

    echo "Session limits configuration created in /tmp/limits.conf"
    echo "Review and copy to /etc/security/limits.conf"
    
    # Create session timeout configuration
    cat > /tmp/profile-timeout << 'EOF'
# Automatic logout after inactivity
# Add to /etc/profile or /etc/bash.bashrc

# Set timeout for interactive shells (in seconds)
TMOUT=1800  # 30 minutes

# Export for subshells
export TMOUT

# Make readonly to prevent users from changing
readonly TMOUT
EOF

    echo "Session timeout configuration created in /tmp/profile-timeout"
}

# Test PAM configuration
test_pam_config() {
    local test_user="${1:-pamtest}"
    
    echo "Testing PAM configuration with user: $test_user"
    
    # Create test user if it doesn't exist
    if ! id "$test_user" &>/dev/null; then
        echo "Creating test user: $test_user"
        sudo useradd -m -s /bin/bash "$test_user"
        echo "$test_user:TestPassword123!" | sudo chpasswd
    fi
    
    # Test password quality
    echo "Testing password quality..."
    echo "Attempting to set weak password:"
    echo "$test_user:weak" | sudo chpasswd 2>&1 | grep -i "error\|bad\|weak" || echo "Weak password was accepted (check configuration)"
    
    # Test account lockout (if configured)
    echo ""
    echo "Testing account lockout..."
    if command -v pam_tally2 &>/dev/null; then
        # Show current tally
        sudo pam_tally2 --user="$test_user"
        
        # Simulate failed logins (don't actually lock the account)
        echo "Current lockout status shown above"
    else
        echo "pam_tally2 not available for testing"
    fi
    
    # Test session limits
    echo ""
    echo "Testing session limits..."
    sudo -u "$test_user" bash -c 'ulimit -a' | head -10
    
    # Cleanup
    echo ""
    read -p "Delete test user $test_user? (y/N): " cleanup
    if [[ "$cleanup" == "y" || "$cleanup" == "Y" ]]; then
        sudo userdel -r "$test_user"
        echo "Test user deleted"
    fi
}

# Usage
case "${1:-help}" in
    "backup")
        backup_pam_config
        ;;
    "password-quality")
        configure_password_quality
        ;;
    "account-lockout")
        configure_account_lockout "$2" "$3"
        ;;
    "session-security")
        configure_session_security
        ;;
    "test")
        test_pam_config "$2"
        ;;
    "help")
        echo "Usage: $0 {backup|password-quality|account-lockout|session-security|test} [arguments]"
        echo ""
        echo "Commands:"
        echo "  backup                              - Backup PAM configuration"
        echo "  password-quality                    - Configure password quality"
        echo "  account-lockout [attempts] [time]   - Configure account lockout"
        echo "  session-security                    - Configure session limits"
        echo "  test [username]                     - Test PAM configuration"
        ;;
esac
```
### SSH Security and Key Management

#### Advanced SSH Configuration
```bash
#!/bin/bash
# ssh-security.sh - Comprehensive SSH security configuration

# Backup SSH configuration
backup_ssh_config() {
    local backup_dir="/var/backups/ssh-config-$(date +%Y%m%d_%H%M%S)"
    
    echo "Backing up SSH configuration to: $backup_dir"
    sudo mkdir -p "$backup_dir"
    
    # Backup SSH daemon configuration
    sudo cp /etc/ssh/sshd_config "$backup_dir/"
    
    # Backup SSH client configuration
    if [[ -f /etc/ssh/ssh_config ]]; then
        sudo cp /etc/ssh/ssh_config "$backup_dir/"
    fi
    
    # Backup host keys
    sudo cp /etc/ssh/ssh_host_* "$backup_dir/" 2>/dev/null || true
    
    echo "SSH configuration backed up successfully"
}

# Harden SSH configuration
harden_ssh_config() {
    echo "Implementing SSH security hardening..."
    
    # Create hardened SSH configuration
    cat > /tmp/sshd_config_hardened << 'EOF'
# Hardened SSH Configuration
# Network settings
Port 2222
AddressFamily inet
ListenAddress 0.0.0.0

# Protocol settings
Protocol 2
Compression delayed

# Authentication settings
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

# Kerberos and GSSAPI
KerberosAuthentication no
GSSAPIAuthentication no

# Connection settings
MaxAuthTries 3
MaxSessions 10
MaxStartups 10:30:60
LoginGraceTime 60
ClientAliveInterval 300
ClientAliveCountMax 2
TCPKeepAlive no

# User restrictions
AllowUsers admin-user operator-user
DenyUsers guest test
AllowGroups ssh-users admin
DenyGroups noremote

# Logging
LogLevel VERBOSE
SyslogFacility AUTH

# Security features
StrictModes yes
IgnoreRhosts yes
HostbasedAuthentication no
PermitUserEnvironment no
AcceptEnv LANG LC_*
PrintMotd no
PrintLastLog yes
ShowPatchLevel no
DebianBanner no

# Subsystems
Subsystem sftp internal-sftp

# X11 and forwarding
X11Forwarding no
X11DisplayOffset 10
X11UseLocalhost yes
PermitTunnel no
AllowAgentForwarding yes
AllowTcpForwarding yes
GatewayPorts no

# Host key algorithms (strongest first)
HostKeyAlgorithms ssh-ed25519,rsa-sha2-512,rsa-sha2-256

# Key exchange algorithms
KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512

# Ciphers (strongest first)
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

# MAC algorithms
MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha2-512

# Banner
Banner /etc/ssh/banner
EOF

    echo "Hardened SSH configuration created in /tmp/sshd_config_hardened"
    echo "Review and copy to /etc/ssh/sshd_config (after backing up original)"
    
    # Create SSH banner
    cat > /tmp/ssh_banner << 'EOF'
********************************************************************************
*                                                                              *
*  AUTHORIZED ACCESS ONLY                                                      *
*                                                                              *
*  This system is for authorized users only. All activities are monitored     *
*  and recorded. Unauthorized access is prohibited and will be prosecuted     *
*  to the full extent of the law.                                             *
*                                                                              *
*  By accessing this system, you consent to monitoring and recording.         *
*                                                                              *
********************************************************************************
EOF

    echo "SSH banner created in /tmp/ssh_banner"
    echo "Copy to /etc/ssh/banner"
}

# Manage SSH keys
manage_ssh_keys() {
    local action="$1"
    local username="$2"
    local key_file="$3"
    
    if [[ -z "$action" || -z "$username" ]]; then
        echo "Usage: manage_ssh_keys <action> <username> [key_file]"
        echo "Actions: generate, install, remove, list, rotate"
        return 1
    fi
    
    case "$action" in
        "generate")
            echo "Generating SSH key for user: $username"
            local key_type="${key_file:-ed25519}"
            local key_path="/tmp/${username}_ssh_key"
            
            # Generate key pair
            ssh-keygen -t "$key_type" -C "${username}@$(hostname)" -f "$key_path" -N ""
            
            if [[ $? -eq 0 ]]; then
                echo "SSH key generated successfully:"
                echo "Private key: ${key_path}"
                echo "Public key: ${key_path}.pub"
                echo ""
                echo "Public key content:"
                cat "${key_path}.pub"
                echo ""
                echo "Install with: $0 install $username ${key_path}.pub"
            else
                echo "Failed to generate SSH key"
                return 1
            fi
            ;;
            
        "install")
            echo "Installing SSH key for user: $username"
            
            if [[ -z "$key_file" || ! -f "$key_file" ]]; then
                echo "Key file required and must exist"
                return 1
            fi
            
            # Get user home directory
            local user_home=$(getent passwd "$username" | cut -d: -f6)
            if [[ -z "$user_home" ]]; then
                echo "User $username not found"
                return 1
            fi
            
            # Create .ssh directory
            sudo -u "$username" mkdir -p "$user_home/.ssh"
            sudo -u "$username" chmod 700 "$user_home/.ssh"
            
            # Install public key
            if sudo -u "$username" cat "$key_file" >> "$user_home/.ssh/authorized_keys"; then
                sudo -u "$username" chmod 600 "$user_home/.ssh/authorized_keys"
                echo "SSH key installed successfully for $username"
                
                # Log the installation
                echo "$(date): SSH key installed for $username from $key_file" | sudo tee -a /var/log/ssh-key-management.log
            else
                echo "Failed to install SSH key"
                return 1
            fi
            ;;
            
        "remove")
            echo "Removing SSH key for user: $username"
            
            if [[ -z "$key_file" ]]; then
                echo "Key content or identifier required"
                return 1
            fi
            
            local user_home=$(getent passwd "$username" | cut -d: -f6)
            local auth_keys="$user_home/.ssh/authorized_keys"
            
            if [[ ! -f "$auth_keys" ]]; then
                echo "No authorized_keys file found for $username"
                return 1
            fi
            
            # Remove key (assuming key_file contains the key comment or full key)
            if sudo grep -v "$key_file" "$auth_keys" | sudo tee "${auth_keys}.tmp" >/dev/null; then
                sudo mv "${auth_keys}.tmp" "$auth_keys"
                sudo chown "$username:$username" "$auth_keys"
                sudo chmod 600 "$auth_keys"
                echo "SSH key removed for $username"
                
                # Log the removal
                echo "$(date): SSH key removed for $username (pattern: $key_file)" | sudo tee -a /var/log/ssh-key-management.log
            else
                echo "Failed to remove SSH key"
                return 1
            fi
            ;;
            
        "list")
            echo "Listing SSH keys for user: $username"
            
            local user_home=$(getent passwd "$username" | cut -d: -f6)
            local auth_keys="$user_home/.ssh/authorized_keys"
            
            if [[ ! -f "$auth_keys" ]]; then
                echo "No authorized_keys file found for $username"
                return 1
            fi
            
            echo "SSH keys for $username:"
            echo "======================"
            local key_num=1
            while read -r key; do
                if [[ -n "$key" && ! "$key" =~ ^# ]]; then
                    local key_type=$(echo "$key" | awk '{print $1}')
                    local key_comment=$(echo "$key" | awk '{print $NF}')
                    local key_fingerprint=$(echo "$key" | ssh-keygen -lf - 2>/dev/null | awk '{print $2}')
                    
                    echo "Key $key_num:"
                    echo "  Type: $key_type"
                    echo "  Comment: $key_comment"
                    echo "  Fingerprint: $key_fingerprint"
                    echo ""
                    ((key_num++))
                fi
            done < "$auth_keys"
            ;;
            
        "rotate")
            echo "Rotating SSH keys for user: $username"
            
            # Backup current keys
            local user_home=$(getent passwd "$username" | cut -d: -f6)
            local backup_file="$user_home/.ssh/authorized_keys.backup.$(date +%Y%m%d_%H%M%S)"
            
            if [[ -f "$user_home/.ssh/authorized_keys" ]]; then
                sudo cp "$user_home/.ssh/authorized_keys" "$backup_file"
                echo "Current keys backed up to: $backup_file"
            fi
            
            # Generate new key
            manage_ssh_keys generate "$username" "ed25519"
            
            echo "Key rotation initiated. Install new key and remove old ones manually."
            ;;
            
        *)
            echo "Unknown action: $action"
            return 1
            ;;
    esac
}

# SSH key audit
audit_ssh_keys() {
    local output_file="${1:-/tmp/ssh_key_audit_$(date +%Y%m%d_%H%M%S).txt}"
    
    echo "Performing SSH key audit..."
    echo "SSH Key Audit - $(date)" > "$output_file"
    echo "=========================" >> "$output_file"
    echo "" >> "$output_file"
    
    # Audit user SSH keys
    echo "User SSH Keys:" >> "$output_file"
    echo "-------------" >> "$output_file"
    
    getent passwd | awk -F: '$3 >= 1000 && $3 < 65534 {print $1":"$6}' | while IFS=: read username home_dir; do
        local auth_keys="$home_dir/.ssh/authorized_keys"
        
        if [[ -f "$auth_keys" ]]; then
            echo "User: $username" >> "$output_file"
            
            local key_count=$(grep -c "^ssh-\|^ecdsa-\|^ed25519" "$auth_keys" 2>/dev/null || echo "0")
            echo "  Key count: $key_count" >> "$output_file"
            
            if [[ $key_count -gt 0 ]]; then
                echo "  Keys:" >> "$output_file"
                grep "^ssh-\|^ecdsa-\|^ed25519" "$auth_keys" 2>/dev/null | while read -r key; do
                    local key_type=$(echo "$key" | awk '{print $1}')
                    local key_comment=$(echo "$key" | awk '{print $NF}')
                    local key_fingerprint=$(echo "$key" | ssh-keygen -lf - 2>/dev/null | awk '{print $2}')
                    echo "    - Type: $key_type, Comment: $key_comment, Fingerprint: $key_fingerprint" >> "$output_file"
                done
            fi
            echo "" >> "$output_file"
        fi
    done
    
    # Audit system SSH host keys
    echo "" >> "$output_file"
    echo "System SSH Host Keys:" >> "$output_file"
    echo "--------------------" >> "$output_file"
    
    for key_file in /etc/ssh/ssh_host_*_key.pub; do
        if [[ -f "$key_file" ]]; then
            local key_info=$(ssh-keygen -lf "$key_file" 2>/dev/null)
            echo "  $(basename "$key_file"): $key_info" >> "$output_file"
        fi
    done
    
    # Security analysis
    echo "" >> "$output_file"
    echo "Security Analysis:" >> "$output_file"
    echo "-----------------" >> "$output_file"
    
    # Find weak or old key types
    echo "Weak key types found:" >> "$output_file"
    find /home -name "authorized_keys" -exec grep -l "ssh-dss\|ssh-rsa.*== " {} \; 2>/dev/null | while read file; do
        local username=$(echo "$file" | cut -d'/' -f3)
        echo "  $username: Contains weak keys (DSS or short RSA)" >> "$output_file"
    done
    
    # Find duplicate keys
    echo "" >> "$output_file"
    echo "Potential duplicate keys:" >> "$output_file"
    find /home -name "authorized_keys" -exec cat {} \; 2>/dev/null | \
        grep "^ssh-\|^ecdsa-\|^ed25519" | sort | uniq -d | while read -r dup_key; do
            echo "  Duplicate key found: $(echo "$dup_key" | awk '{print $1, $NF}')" >> "$output_file"
        done
    
    echo "SSH key audit completed: $output_file"
}

# Configure SSH client
configure_ssh_client() {
    local username="$1"
    local config_type="${2:-secure}"
    
    if [[ -z "$username" ]]; then
        echo "Usage: configure_ssh_client <username> [config_type]"
        echo "Config types: secure, convenience, enterprise"
        return 1
    fi
    
    local user_home=$(getent passwd "$username" | cut -d: -f6)
    local ssh_config="$user_home/.ssh/config"
    
    echo "Configuring SSH client for user: $username"
    
    # Create SSH directory
    sudo -u "$username" mkdir -p "$user_home/.ssh"
    sudo -u "$username" chmod 700 "$user_home/.ssh"
    
    case "$config_type" in
        "secure")
            cat > /tmp/ssh_config_secure << 'EOF'
# Secure SSH client configuration
Host *
    # Security settings
    Protocol 2
    HashKnownHosts yes
    HostKeyAlgorithms ssh-ed25519,rsa-sha2-512,rsa-sha2-256
    KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,diffie-hellman-group16-sha512
    Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr
    MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com
    
    # Connection settings
    ConnectTimeout 30
    ServerAliveInterval 60
    ServerAliveCountMax 3
    
    # Authentication
    PubkeyAuthentication yes
    PasswordAuthentication no
    ChallengeResponseAuthentication no
    GSSAPIAuthentication no
    
    # Disable potentially dangerous features
    ForwardAgent no
    ForwardX11 no
    PermitLocalCommand no
    
    # Identity files
    IdentitiesOnly yes
    IdentityFile ~/.ssh/id_ed25519
    IdentityFile ~/.ssh/id_rsa
EOF
            ;;
            
        "convenience")
            cat > /tmp/ssh_config_convenience << 'EOF'
# Convenient SSH client configuration
Host *
    # Security settings (balanced)
    Protocol 2
    HashKnownHosts yes
    
    # Connection settings
    ConnectTimeout 30
    ServerAliveInterval 60
    ServerAliveCountMax 3
    ControlMaster auto
    ControlPath ~/.ssh/control-%r@%h:%p
    ControlPersist 300
    
    # Authentication
    PubkeyAuthentication yes
    PasswordAuthentication yes
    
    # Convenience features
    ForwardAgent yes
    Compression yes
    
# Example host configurations
Host production-server
    HostName prod.example.com
    User deploy
    Port 2222
    IdentityFile ~/.ssh/production_key
    
Host staging-server
    HostName staging.example.com
    User deploy
    Port 2222
    IdentityFile ~/.ssh/staging_key
    
Host jump-host
    HostName jump.example.com
    User admin
    Port 22
    ProxyCommand none
    
Host internal-*
    ProxyCommand ssh -W %h:%p jump-host
    User admin
EOF
            ;;
            
        "enterprise")
            cat > /tmp/ssh_config_enterprise << 'EOF'
# Enterprise SSH client configuration
Host *
    # Security settings
    Protocol 2
    HashKnownHosts yes
    StrictHostKeyChecking ask
    
    # Logging
    LogLevel INFO
    
    # Connection settings
    ConnectTimeout 30
    ServerAliveInterval 120
    ServerAliveCountMax 2
    ControlMaster auto
    ControlPath ~/.ssh/control-%r@%h:%p
    ControlPersist 600
    
    # Authentication
    PubkeyAuthentication yes
    PasswordAuthentication no
    GSSAPIAuthentication yes
    GSSAPIDelegateCredentials yes
    
    # Certificate authentication
    CertificateFile ~/.ssh/id_rsa-cert.pub
    CertificateFile ~/.ssh/id_ed25519-cert.pub
    
# Corporate environments
Host *.corp.example.com
    User %r
    GSSAPIAuthentication yes
    GSSAPIDelegateCredentials yes
    
Host bastion-*.corp.example.com
    User admin
    Port 2222
    
Host prod-*.corp.example.com
    ProxyCommand ssh -W %h:%p bastion-prod.corp.example.com
    User operator
    
Host dev-*.corp.example.com
    ProxyCommand ssh -W %h:%p bastion-dev.corp.example.com
    User developer
EOF
            ;;
    esac
    
    # Install configuration
    if sudo -u "$username" cp "/tmp/ssh_config_$config_type" "$ssh_config"; then
        sudo -u "$username" chmod 600 "$ssh_config"
        echo "SSH client configuration installed: $ssh_config"
    else
        echo "Failed to install SSH client configuration"
        return 1
    fi
}

# Usage
case "${1:-help}" in
    "backup")
        backup_ssh_config
        ;;
    "harden")
        harden_ssh_config
        ;;
    "keys")
        manage_ssh_keys "$2" "$3" "$4"
        ;;
    "audit")
        audit_ssh_keys "$2"
        ;;
    "client")
        configure_ssh_client "$2" "$3"
        ;;
    "help")
        echo "Usage: $0 {backup|harden|keys|audit|client} [arguments]"
        echo ""
        echo "Commands:"
        echo "  backup                                    - Backup SSH configuration"
        echo "  harden                                    - Create hardened SSH config"
        echo "  keys <action> <user> [key_file]           - Manage SSH keys"
        echo "  audit [output_file]                       - Audit SSH keys"
        echo "  client <username> [type]                  - Configure SSH client"
        echo ""
        echo "Key actions: generate, install, remove, list, rotate"
        echo "Client types: secure, convenience, enterprise"
        ;;
esac
```

### Security Auditing Scripts

#### Comprehensive Security Audit
```bash
#!/bin/bash
# security-audit.sh - Comprehensive user and authentication security audit

# Configuration
AUDIT_DIR="/var/log/security-audits"
AUDIT_DATE=$(date +%Y%m%d_%H%M%S)
AUDIT_LOG="$AUDIT_DIR/security_audit_$AUDIT_DATE.log"
HTML_REPORT="$AUDIT_DIR/security_audit_$AUDIT_DATE.html"

# Severity levels
CRITICAL_ISSUES=()
HIGH_ISSUES=()
MEDIUM_ISSUES=()
LOW_ISSUES=()

# Initialize audit
init_audit() {
    echo "Initializing security audit..."
    sudo mkdir -p "$AUDIT_DIR"
    
    # Start log file
    cat > "$AUDIT_LOG" << EOF
Security Audit Log
Generated: $(date)
Hostname: $(hostname)
Kernel: $(uname -r)
Distribution: $(cat /etc/os-release | grep PRETTY_NAME | cut -d'"' -f2)

===============================================================================
EOF

    echo "Security audit initialized"
}

# Log finding
log_finding() {
    local severity="$1"
    local category="$2"
    local description="$3"
    local details="$4"
    
    local finding="[$severity] $category: $description"
    if [[ -n "$details" ]]; then
        finding+="\n    Details: $details"
    fi
    
    echo -e "$finding" >> "$AUDIT_LOG"
    
    # Add to appropriate severity array
    case "$severity" in
        "CRITICAL") CRITICAL_ISSUES+=("$category: $description") ;;
        "HIGH") HIGH_ISSUES+=("$category: $description") ;;
        "MEDIUM") MEDIUM_ISSUES+=("$category: $description") ;;
        "LOW") LOW_ISSUES+=("$category: $description") ;;
    esac
}

# Audit user accounts
audit_user_accounts() {
    echo "Auditing user accounts..." | tee -a "$AUDIT_LOG"
    
    # Check for accounts without passwords
    local no_password_accounts=$(sudo awk -F: '($2 == "" || $2 == "!") && $3 >= 1000 && $3 < 65534 {print $1}' /etc/shadow)
    if [[ -n "$no_password_accounts" ]]; then
        log_finding "CRITICAL" "User Accounts" "Accounts without passwords found" "$no_password_accounts"
    fi
    
    # Check for accounts with UID 0 (root equivalent)
    local root_accounts=$(awk -F: '$3 == 0 && $1 != "root" {print $1}' /etc/passwd)
    if [[ -n "$root_accounts" ]]; then
        log_finding "CRITICAL" "User Accounts" "Non-root accounts with UID 0 found" "$root_accounts"
    fi
    
    # Check for duplicate UIDs
    local duplicate_uids=$(awk -F: '{print $3}' /etc/passwd | sort -n | uniq -d)
    if [[ -n "$duplicate_uids" ]]; then
        log_finding "HIGH" "User Accounts" "Duplicate UIDs found" "$duplicate_uids"
    fi
    
    # Check for users with non-standard shells
    local suspicious_shells=$(getent passwd | awk -F: '$3 >= 1000 && $7 !~ /(bash|sh|zsh|fish|ksh|csh|tcsh|nologin|false)$/ {print $1":"$7}')
    if [[ -n "$suspicious_shells" ]]; then
        log_finding "MEDIUM" "User Accounts" "Users with non-standard shells" "$suspicious_shells"
    fi
    
    # Check for inactive users (no login in 90 days)
    local inactive_threshold=90
    local current_time=$(date +%s)
    local inactive_users=""
    
    getent passwd | awk -F: '$3 >= 1000 && $3 < 65534 {print $1}' | while read username; do
        local last_login=$(lastlog -u "$username" 2>/dev/null | tail -1)
        if echo "$last_login" | grep -q "Never logged in"; then
            inactive_users+="$username (never logged in), "
        else
            local login_date=$(echo "$last_login" | awk '{print $4, $5, $6, $7}')
            if [[ -n "$login_date" && "$login_date" != "**Never" ]]; then
                local login_timestamp=$(date -d "$login_date" +%s 2>/dev/null)
                if [[ -n "$login_timestamp" ]]; then
                    local days_since=$(( (current_time - login_timestamp) / 86400 ))
                    if [[ $days_since -gt $inactive_threshold ]]; then
                        inactive_users+="$username ($days_since days), "
                    fi
                fi
            fi
        fi
    done
    
    if [[ -n "$inactive_users" ]]; then
        log_finding "MEDIUM" "User Accounts" "Inactive users (>$inactive_threshold days)" "${inactive_users%, }"
    fi
    
    # Check for accounts with expired passwords
    local expired_passwords=$(sudo chage -l $(getent passwd | awk -F: '$3 >= 1000 && $3 < 65534 {print $1}') 2>/dev/null | \
        grep -B1 "Password expires" | grep -B1 "never\|$(date +%Y)" | grep "Account expires" | cut -d: -f1)
    if [[ -n "$expired_passwords" ]]; then
        log_finding "HIGH" "User Accounts" "Accounts with expired passwords" "$expired_passwords"
    fi
}

# Audit password policies
audit_password_policies() {
    echo "Auditing password policies..." | tee -a "$AUDIT_LOG"
    
    # Check login.defs settings
    if [[ -f /etc/login.defs ]]; then
        local pass_max_days=$(grep "^PASS_MAX_DAYS" /etc/login.defs | awk '{print $2}')
        local pass_min_days=$(grep "^PASS_MIN_DAYS" /etc/login.defs | awk '{print $2}')
        local pass_warn_age=$(grep "^PASS_WARN_AGE" /etc/login.defs | awk '{print $2}')
        
        if [[ -z "$pass_max_days" || $pass_max_days -gt 365 ]]; then
            log_finding "MEDIUM" "Password Policy" "Password maximum age not set or too high" "Current: $pass_max_days"
        fi
        
        if [[ -z "$pass_min_days" || $pass_min_days -lt 1 ]]; then
            log_finding "LOW" "Password Policy" "Password minimum age not set or too low" "Current: $pass_min_days"
        fi
        
        if [[ -z "$pass_warn_age" || $pass_warn_age -lt 7 ]]; then
            log_finding "LOW" "Password Policy" "Password warning age not set or too low" "Current: $pass_warn_age"
        fi
    else
        log_finding "MEDIUM" "Password Policy" "login.defs file not found" ""
    fi
    
    # Check PAM password quality
    if [[ -f /etc/security/pwquality.conf ]]; then
        local minlen=$(grep "^minlen" /etc/security/pwquality.conf | awk '{print $3}')
        if [[ -z "$minlen" || $minlen -lt 8 ]]; then
            log_finding "MEDIUM" "Password Policy" "Minimum password length too low" "Current: $minlen"
        fi
    else
        log_finding "MEDIUM" "Password Policy" "pwquality.conf not found - password complexity not enforced" ""
    fi
    
    # Check for weak passwords (if john is available)
    if command -v john &>/dev/null; then
        echo "Running password strength check with John the Ripper..."
        local weak_passwords=$(sudo john --show /etc/shadow 2>/dev/null | wc -l)
        if [[ $weak_passwords -gt 0 ]]; then
            log_finding "HIGH" "Password Policy" "Weak passwords detected" "$weak_passwords accounts with weak passwords"
        fi
    fi
}

# Audit authentication mechanisms
audit_authentication() {
    echo "Auditing authentication mechanisms..." | tee -a "$AUDIT_LOG"
    
    # Check SSH configuration
    if [[ -f /etc/ssh/sshd_config ]]; then
        local permit_root=$(grep "^PermitRootLogin" /etc/ssh/sshd_config | awk '{print $2}')
        if [[ "$permit_root" == "yes" ]]; then
            log_finding "HIGH" "SSH Configuration" "Root login via SSH is enabled" ""
        fi
        
        local password_auth=$(grep "^PasswordAuthentication" /etc/ssh/sshd_config | awk '{print $2}')
        if [[ "$password_auth" == "yes" ]]; then
            log_finding "MEDIUM" "SSH Configuration" "Password authentication enabled" ""
        fi
        
        local max_auth_tries=$(grep "^MaxAuthTries" /etc/ssh/sshd_config | awk '{print $2}')
        if [[ -z "$max_auth_tries" || $max_auth_tries -gt 6 ]]; then
            log_finding "MEDIUM" "SSH Configuration" "MaxAuthTries not set or too high" "Current: $max_auth_tries"
        fi
    fi
    
    # Check for failed login attempts
    local failed_logins=$(sudo lastb -n 100 2>/dev/null | wc -l)
    if [[ $failed_logins -gt 50 ]]; then
        log_finding "MEDIUM" "Authentication" "High number of failed login attempts" "$failed_logins recent failures"
    fi
    
    # Check sudo configuration
    if [[ -f /etc/sudoers ]]; then
        local nopasswd_entries=$(sudo grep "NOPASSWD" /etc/sudoers /etc/sudoers.d/* 2>/dev/null | grep -v "^#")
        if [[ -n "$nopasswd_entries" ]]; then
            log_finding "HIGH" "Sudo Configuration" "NOPASSWD entries found in sudoers" "$nopasswd_entries"
        fi
    fi
    
    # Check for users in admin groups
    local admin_users=""
    for group in "sudo" "wheel" "admin" "root"; do
        if getent group "$group" &>/dev/null; then
            local group_members=$(getent group "$group" | cut -d: -f4)
            if [[ -n "$group_members" ]]; then
                admin_users+="$group: $group_members; "
            fi
        fi
    done
    
    if [[ -n "$admin_users" ]]; then
        echo "Admin group memberships: $admin_users" >> "$AUDIT_LOG"
    fi
}

# Audit file permissions
audit_file_permissions() {
    echo "Auditing file permissions..." | tee -a "$AUDIT_LOG"
    
    # Check world-writable files in system directories
    local world_writable=$(find /bin /sbin /usr/bin /usr/sbin /lib /lib64 /usr/lib -type f -perm -002 2>/dev/null | head -20)
    if [[ -n "$world_writable" ]]; then
        log_finding "HIGH" "File Permissions" "World-writable system files found" "$world_writable"
    fi
    
    # Check SUID/SGID files
    local suid_files=$(find /usr /bin /sbin -type f \( -perm -4000 -o -perm -2000 \) 2>/dev/null | head -20)
    if [[ -n "$suid_files" ]]; then
        echo "SUID/SGID files found (review required): $suid_files" >> "$AUDIT_LOG"
    fi
    
    # Check home directory permissions
    local insecure_homes=$(find /home -maxdepth 1 -type d -perm -002 2>/dev/null)
    if [[ -n "$insecure_homes" ]]; then
        log_finding "MEDIUM" "File Permissions" "World-writable home directories found" "$insecure_homes"
    fi
    
    # Check SSH key permissions
    local insecure_ssh_keys=$(find /home -name "authorized_keys" -not -perm 600 2>/dev/null)
    if [[ -n "$insecure_ssh_keys" ]]; then
        log_finding "HIGH" "File Permissions" "SSH authorized_keys with insecure permissions" "$insecure_ssh_keys"
    fi
}

# Audit system configuration
audit_system_config() {
    echo "Auditing system configuration..." | tee -a "$AUDIT_LOG"
    
    # Check if firewall is enabled
    if command -v ufw &>/dev/null; then
        local ufw_status=$(sudo ufw status | grep "Status:" | awk '{print $2}')
        if [[ "$ufw_status" != "active" ]]; then
            log_finding "HIGH" "System Configuration" "UFW firewall is not active" ""
        fi
    elif command -v firewall-cmd &>/dev/null; then
        local firewalld_status=$(sudo firewall-cmd --state 2>/dev/null)
        if [[ "$firewalld_status" != "running" ]]; then
            log_finding "HIGH" "System Configuration" "firewalld is not running" ""
        fi
    else
        log_finding "MEDIUM" "System Configuration" "No firewall management tool found" ""
    fi
    
    # Check for unnecessary services
    local unnecessary_services=("telnet" "rsh" "rlogin" "ftp" "tftp")
    for service in "${unnecessary_services[@]}"; do
        if systemctl is-enabled "$service" &>/dev/null; then
            log_finding "HIGH" "System Configuration" "Unnecessary service enabled" "$service"
        fi
    done
    
    # Check system updates
    if command -v apt &>/dev/null; then
        local updates_available=$(apt list --upgradable 2>/dev/null | wc -l)
        if [[ $updates_available -gt 10 ]]; then
            log_finding "MEDIUM" "System Configuration" "Many system updates available" "$updates_available updates pending"
        fi
    elif command -v dnf &>/dev/null; then
        local updates_available=$(dnf check-update 2>/dev/null | wc -l)
        if [[ $updates_available -gt 10 ]]; then
            log_finding "MEDIUM" "System Configuration" "Many system updates available" "$updates_available updates pending"
        fi
    fi
}

# Generate HTML report
generate_html_report() {
    echo "Generating HTML report..." | tee -a "$AUDIT_LOG"
    
    cat > "$HTML_REPORT" << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>Security Audit Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; background-color: #f5f5f5; }
        .header { background-color: #2c3e50; color: white; padding: 20px; border-radius: 5px; }
        .summary { background-color: white; padding: 20px; margin: 20px 0; border-radius: 5px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
        .critical { background-color: #e74c3c; color: white; padding: 15px; margin: 10px 0; border-radius: 5px; }
        .high { background-color: #e67e22; color: white; padding: 15px; margin: 10px 0; border-radius: 5px; }
        .medium { background-color: #f39c12; color: white; padding: 15px; margin: 10px 0; border-radius: 5px; }
        .low { background-color: #95a5a6; color: white; padding: 15px; margin: 10px 0; border-radius: 5px; }
        .good { background-color: #27ae60; color: white; padding: 15px; margin: 10px 0; border-radius: 5px; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; }
        th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
        th { background-color: #34495e; color: white; }
    </style>
</head>
<body>
    <div class="header">
        <h1>Security Audit Report</h1>
        <p>Generated: TIMESTAMP</p>
        <p>Hostname: HOSTNAME</p>
    </div>
EOF

    # Replace placeholders
    sed -i "s/TIMESTAMP/$(date)/" "$HTML_REPORT"
    sed -i "s/HOSTNAME/$(hostname)/" "$HTML_REPORT"
    
    # Add summary
    cat >> "$HTML_REPORT" << EOF
    <div class="summary">
        <h2>Executive Summary</h2>
        <table>
            <tr><th>Severity</th><th>Count</th><th>Issues</th></tr>
            <tr><td style="background-color: #e74c3c; color: white;">Critical</td><td>${#CRITICAL_ISSUES[@]}</td><td>Immediate attention required</td></tr>
            <tr><td style="background-color: #e67e22; color: white;">High</td><td>${#HIGH_ISSUES[@]}</td><td>Should be addressed soon</td></tr>
            <tr><td style="background-color: #f39c12; color: white;">Medium</td><td>${#MEDIUM_ISSUES[@]}</td><td>Should be reviewed</td></tr>
            <tr><td style="background-color: #95a5a6; color: white;">Low</td><td>${#LOW_ISSUES[@]}</td><td>Minor improvements</td></tr>
        </table>
    </div>

    <h2>Findings</h2>
EOF

    # Add findings by severity
    if [[ ${#CRITICAL_ISSUES[@]} -gt 0 ]]; then
        echo "    <h3>Critical Issues</h3>" >> "$HTML_REPORT"
        for issue in "${CRITICAL_ISSUES[@]}"; do
            echo "    <div class=\"critical\">$issue</div>" >> "$HTML_REPORT"
        done
    fi
    
    if [[ ${#HIGH_ISSUES[@]} -gt 0 ]]; then
        echo "    <h3>High Priority Issues</h3>" >> "$HTML_REPORT"
        for issue in "${HIGH_ISSUES[@]}"; do
            echo "    <div class=\"high\">$issue</div>" >> "$HTML_REPORT"
        done
    fi
    
    if [[ ${#MEDIUM_ISSUES[@]} -gt 0 ]]; then
        echo "    <h3>Medium Priority Issues</h3>" >> "$HTML_REPORT"
        for issue in "${MEDIUM_ISSUES[@]}"; do
            echo "    <div class=\"medium\">$issue</div>" >> "$HTML_REPORT"
        done
    fi
    
    if [[ ${#LOW_ISSUES[@]} -gt 0 ]]; then
        echo "    <h3>Low Priority Issues</h3>" >> "$HTML_REPORT"
        for issue in "${LOW_ISSUES[@]}"; do
            echo "    <div class=\"low\">$issue</div>" >> "$HTML_REPORT"
        done
    fi
    
    # Close HTML
    echo "</body></html>" >> "$HTML_REPORT"
    
    echo "HTML report generated: $HTML_REPORT"
}

# Main audit execution
run_full_audit() {
    echo "Starting comprehensive security audit..."
    
    init_audit
    audit_user_accounts
    audit_password_policies
    audit_authentication
    audit_file_permissions
    audit_system_config
    generate_html_report
    
    # Summary
    echo ""
    echo "Security Audit Complete"
    echo "======================"
    echo "Critical issues: ${#CRITICAL_ISSUES[@]}"
    echo "High priority issues: ${#HIGH_ISSUES[@]}"
    echo "Medium priority issues: ${#MEDIUM_ISSUES[@]}"
    echo "Low priority issues: ${#LOW_ISSUES[@]}"
    echo ""
    echo "Reports generated:"
    echo "  Text log: $AUDIT_LOG"
    echo "  HTML report: $HTML_REPORT"
}

# Usage
case "${1:-help}" in
    "full")
        run_full_audit
        ;;
    "users")
        init_audit
        audit_user_accounts
        echo "User account audit completed: $AUDIT_LOG"
        ;;
    "passwords")
        init_audit
        audit_password_policies
        echo "Password policy audit completed: $AUDIT_LOG"
        ;;
    "auth")
        init_audit
        audit_authentication
        echo "Authentication audit completed: $AUDIT_LOG"
        ;;
    "permissions")
        init_audit
        audit_file_permissions
        echo "File permissions audit completed: $AUDIT_LOG"
        ;;
    "system")
        init_audit
        audit_system_config
        echo "System configuration audit completed: $AUDIT_LOG"
        ;;
    "help")
        echo "Usage: $0 {full|users|passwords|auth|permissions|system}"
        echo ""
        echo "Commands:"
        echo "  full        - Run complete security audit"
        echo "  users       - Audit user accounts only"
        echo "  passwords   - Audit password policies only"
        echo "  auth        - Audit authentication mechanisms only"
        echo "  permissions - Audit file permissions only"
        echo "  system      - Audit system configuration only"
        ;;
esac
```

## Lab Exercises

### Lab 1: User Management Automation
**Objective**: Create a comprehensive user management system with automation and audit trails.

**Tasks**:
1. Develop a user provisioning script that:
   - Creates users from CSV input
   - Sets up appropriate groups and permissions
   - Configures SSH keys
   - Implements password policies
   - Logs all activities

2. Create user lifecycle management:
   - User onboarding workflow
   - Permission modification procedures
   - Account deactivation process
   - Data retention policies

**Deliverables**:
- User management script with error handling
- CSV template for bulk user creation
- Audit log analysis report
- Documentation of procedures

**Success Criteria**:
- Script successfully creates 10+ users from CSV
- All security policies are enforced
- Complete audit trail is maintained
- Zero permission escalation vulnerabilities

### Lab 2: Authentication Security Implementation
**Objective**: Implement enterprise-grade authentication security measures.

**Tasks**:
1. Configure multi-factor authentication:
   - Install and configure TOTP
   - Set up SSH key + password requirements
   - Implement session management

2. Harden authentication systems:
   - Configure PAM security modules
   - Implement account lockout policies
   - Set up failed login monitoring

**Deliverables**:
- PAM configuration files
- MFA setup documentation
- Security monitoring scripts
- Incident response procedures

**Success Criteria**:
- MFA working for all admin accounts
- Account lockouts function correctly
- Failed login attempts are logged and monitored
- Authentication bypass attempts are detected

### Lab 3: SSH Security Hardening
**Objective**: Implement comprehensive SSH security measures across infrastructure.

**Tasks**:
1. SSH server hardening:
   - Disable password authentication
   - Configure key-based authentication only
   - Implement host-based restrictions
   - Set up SSH certificates

2. SSH client security:
   - Create secure client configurations
   - Implement SSH agent forwarding controls
   - Set up SSH connection multiplexing

**Deliverables**:
- Hardened SSH configurations
- SSH key management procedures
- Client configuration templates
- SSH security audit script

**Success Criteria**:
- SSH passes security scan with no critical findings
- Key-based authentication works reliably
- Connection restrictions are properly enforced
- SSH tunneling is controlled appropriately

### Lab 4: Group-Based Access Control
**Objective**: Design and implement role-based access control using groups.

**Tasks**:
1. Design role hierarchy:
   - Define organizational roles
   - Map roles to system permissions
   - Create group structure
   - Document access matrix

2. Implement RBAC system:
   - Create automated group management
   - Set up permission inheritance
   - Implement access reviews
   - Create compliance reporting

**Deliverables**:
- Role definition documentation
- Group management automation
- Access control matrix
- Compliance audit reports

**Success Criteria**:
- All users assigned appropriate roles
- Permissions follow principle of least privilege
- Group membership is properly managed
- Regular access reviews are documented

### Lab 5: Security Audit and Compliance
**Objective**: Develop comprehensive security auditing capabilities.

**Tasks**:
1. Create security audit framework:
   - User account security checks
   - Permission analysis tools
   - Compliance verification scripts
   - Automated reporting system

2. Implement continuous monitoring:
   - Real-time account monitoring
   - Permission change detection
   - Failed login analysis
   - Security event correlation

**Deliverables**:
- Comprehensive audit script suite
- Automated monitoring system
- Security dashboard
- Incident response playbooks

**Success Criteria**:
- Security audit runs without errors
- All compliance requirements are met
- Monitoring detects security events
- Reports are generated automatically

## Best Practices

### Security Best Practices

#### Account Management
- **Regular Account Reviews**: Conduct quarterly reviews of all user accounts
- **Automated Provisioning**: Use automated tools for consistent user creation
- **Principle of Least Privilege**: Grant minimum necessary permissions
- **Account Lifecycle Management**: Implement proper onboarding/offboarding processes
- **Shared Account Prohibition**: Avoid shared accounts except for specific system accounts

#### Password Security
- **Strong Password Policies**: Enforce complexity, length, and rotation requirements
- **Multi-Factor Authentication**: Implement MFA for all privileged accounts
- **Password Managers**: Encourage use of enterprise password management tools
- **Secure Storage**: Never store passwords in plain text
- **Regular Audits**: Periodically check for weak or compromised passwords

#### SSH Security
- **Key-Based Authentication**: Disable password authentication for SSH
- **Key Rotation**: Regularly rotate SSH keys
- **Host Key Verification**: Always verify host keys
- **Session Management**: Implement proper session timeouts
- **Connection Monitoring**: Log and monitor all SSH connections

#### Group Management
- **Role-Based Groups**: Create groups based on job functions
- **Nested Groups**: Use group hierarchies for complex organizations
- **Regular Cleanup**: Remove unused groups periodically
- **Documentation**: Maintain clear group purpose documentation
- **Access Reviews**: Regularly review group memberships

### Operational Best Practices

#### Documentation
- **User Procedures**: Document all user management procedures
- **Security Policies**: Maintain up-to-date security policy documentation
- **Incident Response**: Create clear incident response procedures
- **Change Management**: Document all account and permission changes
- **Compliance Records**: Maintain audit trails for compliance requirements

#### Automation
- **Scripted Operations**: Automate repetitive user management tasks
- **Configuration Management**: Use tools like Ansible for consistent configuration
- **Monitoring Integration**: Integrate with monitoring and alerting systems
- **Backup Procedures**: Automate backup of authentication configurations
- **Testing Automation**: Implement automated security testing

#### Monitoring and Alerting
- **Real-Time Monitoring**: Monitor authentication events in real-time
- **Anomaly Detection**: Implement systems to detect unusual access patterns
- **Failed Login Tracking**: Monitor and alert on failed login attempts
- **Privilege Escalation Detection**: Monitor for unauthorized privilege changes
- **Compliance Monitoring**: Continuously monitor compliance with security policies

## Troubleshooting

### Common Authentication Issues

#### User Cannot Login
**Symptoms**: User reports inability to log in via SSH or console

**Diagnostic Steps**:
1. Check account status:
   ```bash
   sudo passwd -S username
   sudo chage -l username
   ```

2. Verify account isn't locked:
   ```bash
   sudo pam_tally2 --user=username
   sudo faillock --user=username
   ```

3. Check SSH configuration:
   ```bash
   sudo sshd -T | grep -i allowusers
   sudo sshd -T | grep -i denyusers
   ```

4. Verify file permissions:
   ```bash
   ls -la /home/username/.ssh/
   ls -la /home/username/.ssh/authorized_keys
   ```

**Solutions**:
- Unlock account: `sudo passwd -u username`
- Reset failed attempts: `sudo pam_tally2 --user=username --reset`
- Fix permissions: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys`
- Check SSH server configuration for user restrictions

#### SSH Key Authentication Fails
**Symptoms**: SSH key authentication not working, falls back to password

**Diagnostic Steps**:
1. Check SSH client debug output:
   ```bash
   ssh -vvv user@hostname
   ```

2. Check SSH server logs:
   ```bash
   sudo tail -f /var/log/auth.log
   ```

3. Verify key permissions:
   ```bash
   ls -la ~/.ssh/
   ```

4. Test key format:
   ```bash
   ssh-keygen -l -f ~/.ssh/id_rsa.pub
   ```

**Solutions**:
- Fix key permissions: `chmod 600 ~/.ssh/id_rsa`
- Regenerate corrupted keys
- Verify public key is in authorized_keys
- Check SSH server configuration allows key authentication

#### Permission Denied Errors
**Symptoms**: Users cannot access files or directories they should have access to

**Diagnostic Steps**:
1. Check file permissions:
   ```bash
   ls -la problematic_file
   ```

2. Check user group membership:
   ```bash
   groups username
   id username
   ```

3. Check ACLs if enabled:
   ```bash
   getfacl problematic_file
   ```

4. Verify sudo configuration:
   ```bash
   sudo -l -U username
   ```

**Solutions**:
- Fix file ownership: `chown user:group file`
- Add user to appropriate group: `usermod -aG group username`
- Set correct permissions: `chmod appropriate_permissions file`
- Update sudo configuration if needed

#### Account Lockouts
**Symptoms**: Accounts getting locked due to failed login attempts

**Diagnostic Steps**:
1. Check PAM configuration:
   ```bash
   cat /etc/pam.d/common-auth | grep tally
   ```

2. Check failed attempts:
   ```bash
   sudo pam_tally2 --user=username
   ```

3. Review authentication logs:
   ```bash
   sudo grep "authentication failure" /var/log/auth.log
   ```

**Solutions**:
- Unlock account: `sudo pam_tally2 --user=username --reset`
- Adjust PAM lockout thresholds if too aggressive
- Investigate source of failed attempts
- Implement IP-based restrictions if needed

### Performance Issues

#### Slow Authentication
**Symptoms**: Login process takes unusually long time

**Diagnostic Steps**:
1. Check DNS resolution:
   ```bash
   time nslookup client_ip
   ```

2. Monitor authentication process:
   ```bash
   sudo strace -p $(pgrep sshd)
   ```

3. Check LDAP/AD connectivity:
   ```bash
   ldapsearch -x -H ldap://server
   ```

**Solutions**:
- Disable reverse DNS lookups in SSH: `UseDNS no`
- Optimize LDAP queries
- Check network connectivity to authentication servers
- Implement local caching for remote authentication

#### High CPU Usage from Authentication
**Symptoms**: High CPU usage from authentication processes

**Diagnostic Steps**:
1. Monitor process usage:
   ```bash
   top -p $(pgrep -d, "sshd|login|auth")
   ```

2. Check authentication frequency:
   ```bash
   sudo grep "authentication" /var/log/auth.log | wc -l
   ```

**Solutions**:
- Implement connection multiplexing
- Reduce authentication frequency where possible
- Optimize authentication mechanisms
- Consider hardware-based authentication acceleration

### Network and Connectivity Issues

#### SSH Connection Timeouts
**Symptoms**: SSH connections timing out or dropping

**Diagnostic Steps**:
1. Test network connectivity:
   ```bash
   ping -c 4 ssh_server
   telnet ssh_server 22
   ```

2. Check SSH keep-alive settings:
   ```bash
   grep -i "keepalive\|timeout" /etc/ssh/sshd_config
   ```

**Solutions**:
- Configure SSH keep-alive: `ClientAliveInterval 60`
- Adjust firewall timeout settings
- Use SSH connection multiplexing
- Check for network equipment with aggressive timeouts

## Assessment Criteria

### Knowledge Assessment

#### Theoretical Understanding (25 points)
- **User Management Concepts** (5 points): Understanding of user lifecycle, permissions, and security principles
- **Authentication Mechanisms** (5 points): Knowledge of various authentication methods and their security implications
- **Group Management** (5 points): Understanding of role-based access control and group hierarchies
- **SSH Security** (5 points): Knowledge of SSH configuration, key management, and security best practices
- **PAM Configuration** (5 points): Understanding of PAM modules and authentication policies

#### Practical Implementation (50 points)
- **User Creation and Management** (15 points):
  - Create users with appropriate settings
  - Implement password policies
  - Configure account expiration and aging
  - Demonstrate bulk user operations

- **Group and Permission Management** (10 points):
  - Create and manage groups
  - Configure role-based access
  - Implement file permissions correctly
  - Use ACLs where appropriate

- **SSH Configuration** (15 points):
  - Configure SSH server securely
  - Set up key-based authentication
  - Implement SSH client configurations
  - Demonstrate key management

- **Security Implementation** (10 points):
  - Configure PAM modules
  - Implement account lockout policies
  - Set up audit logging
  - Demonstrate security monitoring

#### Problem-Solving and Troubleshooting (15 points)
- **Diagnostic Skills** (5 points): Ability to identify and diagnose authentication issues
- **Resolution Techniques** (5 points): Effective troubleshooting and problem resolution
- **Security Analysis** (5 points): Ability to identify and address security vulnerabilities

#### Documentation and Best Practices (10 points)
- **Technical Documentation** (5 points): Clear and comprehensive documentation of procedures
- **Security Best Practices** (5 points): Implementation of industry-standard security practices

### Practical Evaluation Rubric

#### Excellent (90-100%)
- Demonstrates mastery of all user and authentication management concepts
- Implements comprehensive security measures with automation
- Creates robust, scalable solutions with proper error handling
- Provides detailed documentation and follows all best practices
- Troubleshoots complex issues efficiently

#### Proficient (80-89%)
- Shows solid understanding of user and authentication management
- Implements most security measures correctly
- Creates functional solutions with basic automation
- Provides adequate documentation
- Handles most troubleshooting scenarios

#### Developing (70-79%)
- Understands basic user and authentication concepts
- Implements fundamental security measures
- Creates basic functional solutions
- Documentation covers essential elements
- Requires guidance for complex troubleshooting

#### Needs Improvement (Below 70%)
- Limited understanding of user management concepts
- Inconsistent implementation of security measures
- Solutions lack robustness or have significant issues
- Minimal or incomplete documentation
- Cannot troubleshoot effectively without assistance

### Certification Requirements

To receive certification for Module 6, candidates must:

1. **Score 80% or higher** on the practical assessment
2. **Complete all lab exercises** with satisfactory results
3. **Demonstrate proficiency** in troubleshooting common issues
4. **Submit comprehensive documentation** of implemented solutions
5. **Pass a practical evaluation** demonstrating real-world application of skills

### Continuing Education

#### Advanced Topics for Further Study
- LDAP/Active Directory integration
- Certificate-based authentication
- Hardware security modules (HSMs)
- Identity federation and SSO
- Advanced auditing and compliance frameworks

#### Recommended Certifications
- CompTIA Security+
- Linux Professional Institute Certification (LPIC)
- Red Hat Certified System Administrator (RHCSA)
- Certified Information Systems Security Professional (CISSP)

#### Industry Resources
- NIST Cybersecurity Framework
- CIS Critical Security Controls
- SANS Institute training materials
- Linux documentation project
- Distribution-specific security guides

## Next Steps

With comprehensive user, group, and authentication management mastered, you're ready to advance to **Module 7: Networking Fundamentals**. This next module will build upon your security foundation by covering:

- Network configuration and management
- Firewall configuration and security
- Network troubleshooting and monitoring
- VPN and secure remote access
- Network security best practices

The authentication and user management skills learned in this module are essential for implementing secure network access controls and managing network-based services in the enterprise environment.
