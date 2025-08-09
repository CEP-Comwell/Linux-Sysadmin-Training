
# Module 2: Filesystem Hierarchy & Permissions

**📍 Module Progress: 2/15 Complete**  
**⏱️ Estimated Time: 2-3 hours**  
**📋 Prerequisites: Module 1 (Distributions & Philosophy)**  
**🎯 Difficulty Level: ⭐⭐ (Beginner to Intermediate)**

## Table of Contents
- [Module 2: Filesystem Hierarchy \& Permissions](#module-2-filesystem-hierarchy--permissions)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Learning Objectives](#learning-objectives)
  - [Topics](#topics)
    - [2.1 Filesystem Hierarchy Standard (FHS)](#21-filesystem-hierarchy-standard-fhs)
    - [2.2 Basic File and Directory Permissions](#22-basic-file-and-directory-permissions)
    - [2.3 Special Permission Modes](#23-special-permission-modes)
    - [2.4 Access Control Lists (ACLs)](#24-access-control-lists-acls)
    - [2.5 File Attributes and Extended Attributes](#25-file-attributes-and-extended-attributes)
  - [Essential Command Reference](#essential-command-reference)
  - [Practical Examples](#practical-examples)
    - [Filesystem Navigation and Understanding 🟢](#filesystem-navigation-and-understanding-)
      - [Exploring the Filesystem Hierarchy](#exploring-the-filesystem-hierarchy)
    - [Permission Management 🟢](#permission-management-)
      - [Basic Permission Operations](#basic-permission-operations)
      - [Ownership Management](#ownership-management)
      - [Advanced Permission Scenarios](#advanced-permission-scenarios)
    - [Advanced Access Control 🟡](#advanced-access-control-)
      - [SUID, SGID, and Sticky Bit Implementation](#suid-sgid-and-sticky-bit-implementation)
      - [Access Control Lists (ACLs)](#access-control-lists-acls)
      - [Comprehensive ACL Management Script](#comprehensive-acl-management-script)
    - [Security Auditing and Troubleshooting 🟡](#security-auditing-and-troubleshooting-)
      - [Permission Audit Script](#permission-audit-script)
  - [Lab Exercises](#lab-exercises)
    - [Lab 1: Filesystem Hierarchy Exploration 🟢](#lab-1-filesystem-hierarchy-exploration-)
    - [Lab 2: Permission Management Mastery 🟢](#lab-2-permission-management-mastery-)
    - [Lab 3: Advanced Access Control Implementation 🟡](#lab-3-advanced-access-control-implementation-)
    - [Lab 4: Security Auditing and Remediation 🟡](#lab-4-security-auditing-and-remediation-)
  - [Best Practices Summary](#best-practices-summary)
    - [Filesystem Security Guidelines](#filesystem-security-guidelines)
    - [Permission Management Workflow](#permission-management-workflow)
    - [Common Permission Patterns](#common-permission-patterns)
  - [Troubleshooting Common Issues](#troubleshooting-common-issues)
    - [Permission Denied Errors](#permission-denied-errors)
    - [ACL Issues](#acl-issues)
    - [Ownership Issues](#ownership-issues)
  - [Assessment Criteria](#assessment-criteria)
  - [Next Steps](#next-steps)


## Overview
This module breaks down the Filesystem Hierarchy Standard (FHS) and Linux permission systems to help you secure and organize your server infrastructure. Students will master the traditional Unix permission model, special permission modes, and modern access control mechanisms to implement robust security policies.

**Key Learning Outcomes:**
- Navigate and understand the purpose of key directories (`/etc`, `/var`, `/usr`, `/home`, `/opt`, etc.)
- Master the 9-bit permission model for owner, group, and others
- Implement special modes: SUID, SGID, and sticky bit for advanced access control
- Configure Access Control Lists (ACLs) for granular permission management
- Audit and troubleshoot permission issues using modern tools

[⬆️ Back to Top](#table-of-contents)


## Learning Objectives
By the end of this module, you will be able to:

1. **Navigate FHS Structure**: Map files and directories to their functional roles in the Linux filesystem hierarchy
2. **Manage Basic Permissions**: Configure file and directory access using `chmod`, `chown`, and `chgrp` commands
3. **Implement Special Permissions**: Apply SUID, SGID, and sticky bit modes for advanced security scenarios
4. **Configure ACLs**: Set up granular access control using POSIX Access Control Lists
5. **Audit Security**: Identify and remediate permission issues using `find`, `stat`, `getfacl`, and security scanning tools
6. **Apply Security Principles**: Implement least privilege and defense-in-depth strategies for filesystem security

## Topics
[⬆️ Back to Top](#table-of-contents)

### 2.1 Filesystem Hierarchy Standard (FHS)
[Related Commands/Topics: ls, cd, pwd, du, df, tree] 🟢
- **Root Directory Structure**: Understanding `/`, `/bin`, `/sbin`, `/lib`, `/lib64`
- **Configuration and Data**: `/etc` for system configuration, `/var` for variable data
- **User and Application Areas**: `/home`, `/usr`, `/opt`, `/srv` organization
- **Temporary and Runtime**: `/tmp`, `/var/tmp`, `/run`, `/proc`, `/sys` purposes
- **Mount Points and Storage**: `/mnt`, `/media`, `/dev` device management
- **Distribution-Specific Variations**: How different distributions modify FHS

### 2.2 Basic File and Directory Permissions
[Related Commands/Topics: chmod, chown, chgrp, umask, stat, find] 🟢
- **Permission Bits**: Read (r), Write (w), Execute (x) for files and directories
- **Ownership Model**: User (owner), Group, Others permission structure
- **Numeric and Symbolic Notation**: Octal values and symbolic representation
- **Default Permissions**: Understanding umask and permission inheritance
- **Directory vs File Permissions**: Different behaviors for directories and files

### 2.3 Special Permission Modes
[Related Commands/Topics: chmod, find, stat] 🟡
- **Set User ID (SUID)**: Execution with owner privileges
- **Set Group ID (SGID)**: File inheritance and directory group ownership
- **Sticky Bit**: Directory protection and shared workspace security
- **Security Implications**: Understanding attack vectors and proper usage
- **Common SUID/SGID Programs**: System utilities and security considerations

### 2.4 Access Control Lists (ACLs)
[Related Commands/Topics: setfacl, getfacl, lsattr, chattr] 🟡
- **POSIX ACL Implementation**: Extended permissions beyond basic owner/group/other
- **ACL Types**: Access ACLs vs Default ACLs for directories
- **Granular Control**: User-specific and group-specific permissions
- **ACL Inheritance**: How directory ACLs affect new files and subdirectories
- **Backup and Migration**: Preserving ACLs during system operations

### 2.5 File Attributes and Extended Attributes
[Related Commands/Topics: lsattr, chattr, getfattr, setfattr] 🟡
- **File Attributes**: Immutable, append-only, and other protective attributes
- **Extended Attributes**: User-defined metadata and system attributes
- **SELinux/AppArmor Context**: Security context as extended attributes
- **Filesystem Support**: ext4, XFS, Btrfs attribute capabilities
- **Security Applications**: Using attributes for system hardening

## Essential Command Reference

[⬆️ Back to Top](#table-of-contents)

| Command | Description | Example |
|---------|-------------|---------|
| `ls -la` | List files with detailed permissions | `ls -la /etc/` |
| `chmod` | Change file permissions | `chmod 755 file.sh` |
| `chown` | Change file ownership | `chown user:group file.txt` |
| `chgrp` | Change group ownership | `chgrp developers project/` |
| `umask` | Set default permission mask | `umask 022` |
| `stat` | Display detailed file information | `stat /etc/passwd` |
| `find` | Search files by permissions | `find /usr -perm 4755` |
| `getfacl` | Display ACL information | `getfacl /shared/data` |
| `setfacl` | Set ACL permissions | `setfacl -m u:user:rwx file` |
| `lsattr` | List file attributes | `lsattr file.txt` |
| `chattr` | Change file attributes | `chattr +i important.conf` |
| `getfattr` | Get extended attributes | `getfattr -d file` |
| `setfattr` | Set extended attributes | `setfattr -n user.comment -v "text" file` |

## Practical Examples
[⬆️ Back to Top](#table-of-contents)

[⬆️ Back to Top](#table-of-contents)

### Filesystem Navigation and Understanding 🟢

#### Exploring the Filesystem Hierarchy
```bash
# Navigate and understand key directories
echo "=== Root Directory Structure ==="
ls -la /
echo ""

echo "=== Essential System Directories ==="
echo "/bin - Essential user binaries:"
ls /bin | head -10

echo "/sbin - System binaries (admin tools):"
ls /sbin | head -10

echo "/etc - System configuration:"
ls /etc | head -10

echo "/var - Variable data:"
ls /var

echo "/usr - User programs and data:"
ls /usr

echo "/home - User home directories:"
ls /home
```


### Permission Management 🟢

#### Basic Permission Operations
```bash
# Understanding permission representation
ls -la /etc/passwd
# Output: -rw-r--r-- 1 root root 1234 date /etc/passwd
# Format: [type][owner perms][group perms][other perms] links owner group size date name

# Permission breakdown:
# - = regular file (d for directory, l for symlink, etc.)
# rw- = owner: read, write, no execute
# r-- = group: read only
# r-- = others: read only

# Numeric permission calculation
# r = 4, w = 2, x = 1
# 644 = 4+2+0, 4+0+0, 4+0+0 = rw-r--r--
# 755 = 4+2+1, 4+0+1, 4+0+1 = rwxr-xr-x

# Common permission settings
chmod 644 file.txt        # rw-r--r-- (readable by all, writable by owner)
chmod 755 script.sh       # rwxr-xr-x (executable by all, writable by owner)
chmod 600 private.key     # rw------- (readable/writable by owner only)
chmod 700 private_dir/    # rwx------ (full access by owner only)

# Symbolic permission changes
chmod u+x script.sh       # Add execute for user (owner)
chmod g-w file.txt        # Remove write for group
chmod o+r public.txt      # Add read for others
chmod a+r everyone.txt    # Add read for all (user, group, others)

# Recursive permission changes
chmod -R 755 /var/www/html/    # Set permissions recursively
find /var/www -type d -exec chmod 755 {} \;  # Directories only
find /var/www -type f -exec chmod 644 {} \;  # Files only
```

#### Ownership Management
```bash
# Change ownership
chown username file.txt           # Change owner only
chown username:groupname file.txt # Change owner and group
chown :groupname file.txt         # Change group only (same as chgrp)
chgrp groupname file.txt          # Change group only

# Recursive ownership changes
chown -R webuser:webgroup /var/www/html/

# Copy ownership from another file
chown --reference=/etc/passwd newfile.txt

# Display current ownership
stat -c "%U %G" file.txt    # Show owner and group names
stat -c "%u %g" file.txt    # Show owner and group IDs
id username                 # Show user's UID, GID, and groups
```

#### Advanced Permission Scenarios
```bash
#!/bin/bash
# permission-scenarios.sh - Common permission management scenarios

# Scenario 1: Web server directory structure
setup_webserver_permissions() {
    local webroot="/var/www/html"
    
    echo "Setting up web server permissions for $webroot"
    
    # Create directory structure
    mkdir -p "$webroot"/{public,private,uploads,logs}
    
    # Set ownership to web server user
    chown -R www-data:www-data "$webroot"
    
    # Set directory permissions (755 = rwxr-xr-x)
    find "$webroot" -type d -exec chmod 755 {} \;
    
    # Set file permissions (644 = rw-r--r--)
    find "$webroot" -type f -exec chmod 644 {} \;
    
    # Special permissions for uploads (web server needs write access)
    chmod 775 "$webroot/uploads"
    
    # Logs directory (web server needs write, others no access)
    chmod 750 "$webroot/logs"
    
    echo "Web server permissions configured"
}

# Scenario 2: Shared development directory
setup_development_permissions() {
    local devdir="/opt/development"
    local devgroup="developers"
    
    echo "Setting up development directory permissions for $devdir"
    
    # Create directory
    mkdir -p "$devdir"
    
    # Set group ownership
    chgrp "$devgroup" "$devdir"
    
    # Set group sticky bit (new files inherit group)
    chmod g+s "$devdir"
    
    # Set permissions: owner and group full access, others read-only
    chmod 775 "$devdir"
    
    echo "Development directory permissions configured"
    echo "New files will inherit group: $devgroup"
}

# Scenario 3: Secure backup directory
setup_backup_permissions() {
    local backupdir="/backup"
    local backupuser="backup"
    
    echo "Setting up secure backup directory permissions for $backupdir"
    
    # Create directory
    mkdir -p "$backupdir"
    
    # Set ownership to backup user
    chown "$backupuser:$backupuser" "$backupdir"
    
    # Set restrictive permissions (only backup user can access)
    chmod 700 "$backupdir"
    
    # Make backup files read-only after creation
    find "$backupdir" -type f -exec chmod 400 {} \; 2>/dev/null
    
    echo "Secure backup permissions configured"
}

# Run scenarios based on argument
case "${1:-help}" in
    "webserver")
        setup_webserver_permissions
        ;;
    "development")
        setup_development_permissions
        ;;
    "backup")
        setup_backup_permissions
        ;;
    "help")
        echo "Usage: $0 {webserver|development|backup}"
        echo ""
        echo "Scenarios:"
        echo "  webserver    - Set up web server directory permissions"
        echo "  development  - Set up shared development directory"
        echo "  backup       - Set up secure backup directory"
        ;;
esac
```

### Advanced Access Control 🟡

#### SUID, SGID, and Sticky Bit Implementation
```bash
# Understanding special permissions
# SUID (Set User ID) - 4000 in octal, s in user execute position
# SGID (Set Group ID) - 2000 in octal, s in group execute position  
# Sticky Bit - 1000 in octal, t in other execute position

# Examples of special permissions in the system
echo "=== System SUID Programs ==="
find /usr -perm -4000 -type f 2>/dev/null | head -10
# Common SUID programs: passwd, su, sudo, ping

echo "=== System SGID Programs ==="
find /usr -perm -2000 -type f 2>/dev/null | head -10

echo "=== Directories with Sticky Bit ==="
find / -perm -1000 -type d 2>/dev/null | head -10
# /tmp typically has sticky bit set

# Setting special permissions
chmod 4755 /usr/local/bin/special-program  # Add SUID
chmod 2755 /shared/group-directory         # Add SGID to directory
chmod 1777 /tmp/shared-temp                # Add sticky bit

# Symbolic notation for special permissions
chmod u+s program      # Add SUID
chmod g+s directory    # Add SGID
chmod +t directory     # Add sticky bit

# Remove special permissions
chmod u-s program      # Remove SUID
chmod g-s directory    # Remove SGID
chmod -t directory     # Remove sticky bit
```

#### Access Control Lists (ACLs)
```bash
# Check if filesystem supports ACLs
mount | grep acl
# or
tune2fs -l /dev/sda1 | grep acl

# Enable ACLs on filesystem (if not enabled)
mount -o remount,acl /
# or add to /etc/fstab: defaults,acl

# Basic ACL operations
echo "=== ACL Examples ==="

# Grant specific user read/write access
setfacl -m u:alice:rw file.txt

# Grant specific group execute access  
setfacl -m g:developers:rx /opt/project

# Set default ACL for directory (inherited by new files)
setfacl -m d:u:alice:rw /shared/documents
setfacl -m d:g:team:rwx /shared/workspace

# View ACL information
getfacl file.txt
getfacl /shared/documents

# Remove specific ACL entry
setfacl -x u:alice file.txt

# Remove all ACL entries (revert to standard permissions)
setfacl -b file.txt

# Copy ACLs from one file to another
getfacl source.txt | setfacl --set-file=- target.txt
```

#### Comprehensive ACL Management Script
```bash
#!/bin/bash
# acl-manager.sh - Comprehensive ACL management

show_acl_info() {
    local path="$1"
    
    if [[ ! -e "$path" ]]; then
        echo "Path does not exist: $path"
        return 1
    fi
    
    echo "=== ACL Information for: $path ==="
    echo "Basic permissions:"
    ls -la "$path"
    echo ""
    
    echo "Detailed ACL:"
    getfacl "$path"
    echo ""
    
    if [[ -d "$path" ]]; then
        echo "Default ACL (for directories):"
        getfacl -d "$path" 2>/dev/null || echo "No default ACL set"
    fi
    echo ""
}

set_project_acls() {
    local project_dir="$1"
    local team_group="$2"
    local manager_user="$3"
    
    if [[ -z "$project_dir" || -z "$team_group" || -z "$manager_user" ]]; then
        echo "Usage: set_project_acls <project_dir> <team_group> <manager_user>"
        return 1
    fi
    
    echo "Setting up project ACLs for: $project_dir"
    
    # Create directory if it doesn't exist
    mkdir -p "$project_dir"
    
    # Set base permissions
    chmod 750 "$project_dir"
    
    # Set ACLs for team collaboration
    setfacl -m g:"$team_group":rwx "$project_dir"
    setfacl -m u:"$manager_user":rwx "$project_dir"
    
    # Set default ACLs for new files/directories
    setfacl -m d:g:"$team_group":rwx "$project_dir"
    setfacl -m d:u:"$manager_user":rwx "$project_dir"
    setfacl -m d:o::--- "$project_dir"  # No access for others
    
    echo "Project ACLs configured successfully"
    show_acl_info "$project_dir"
}

backup_acls() {
    local path="$1"
    local backup_file="$2"
    
    if [[ -z "$path" || -z "$backup_file" ]]; then
        echo "Usage: backup_acls <path> <backup_file>"
        return 1
    fi
    
    echo "Backing up ACLs from $path to $backup_file"
    
    if [[ -d "$path" ]]; then
        # Backup ACLs recursively for directory
        getfacl -R "$path" > "$backup_file"
    else
        # Backup ACLs for single file
        getfacl "$path" > "$backup_file"
    fi
    
    echo "ACL backup completed: $backup_file"
}

restore_acls() {
    local backup_file="$1"
    
    if [[ ! -f "$backup_file" ]]; then
        echo "Backup file not found: $backup_file"
        return 1
    fi
    
    echo "Restoring ACLs from $backup_file"
    setfacl --restore="$backup_file"
    echo "ACL restoration completed"
}

# Main function
case "${1:-help}" in
    "show")
        show_acl_info "$2"
        ;;
    "project")
        set_project_acls "$2" "$3" "$4"
        ;;
    "backup")
        backup_acls "$2" "$3"
        ;;
    "restore")
        restore_acls "$2"
        ;;
    "help")
        echo "ACL Management Tool"
        echo "==================="
        echo ""
        echo "Usage: $0 <command> [arguments]"
        echo ""
        echo "Commands:"
        echo "  show <path>                           - Show ACL information"
        echo "  project <dir> <group> <manager>      - Set up project ACLs"
        echo "  backup <path> <backup_file>          - Backup ACLs"
        echo "  restore <backup_file>                - Restore ACLs"
        echo ""
        echo "Examples:"
        echo "  $0 show /shared/project"
        echo "  $0 project /opt/dev developers alice"
        echo "  $0 backup /shared/project acls.backup"
        echo "  $0 restore acls.backup"
        ;;
esac
```

### Security Auditing and Troubleshooting 🟡

#### Permission Audit Script
```bash
#!/bin/bash
# permission-audit.sh - Comprehensive permission security audit

# Configuration
REPORT_FILE="/tmp/permission_audit_$(date +%Y%m%d_%H%M%S).txt"
CRITICAL_DIRS=("/etc" "/usr/bin" "/usr/sbin" "/bin" "/sbin")
SENSITIVE_FILES=("/etc/passwd" "/etc/shadow" "/etc/sudoers" "/etc/ssh/sshd_config")

exec > >(tee "$REPORT_FILE")

echo "=== FILESYSTEM PERMISSION SECURITY AUDIT ==="
echo "Generated on: $(date)"
echo "Report file: $REPORT_FILE"
echo ""

# Check for files with dangerous permissions
echo "=== DANGEROUS PERMISSIONS AUDIT ==="

echo "World-writable files (excluding /tmp, /var/tmp, /dev):"
find / -type f -perm -0002 ! -path "/tmp/*" ! -path "/var/tmp/*" ! -path "/dev/*" ! -path "/proc/*" ! -path "/sys/*" 2>/dev/null | head -20

echo ""
echo "World-writable directories without sticky bit:"
find / -type d -perm -0002 ! -perm -1000 ! -path "/tmp/*" ! -path "/var/tmp/*" ! -path "/dev/*" ! -path "/proc/*" ! -path "/sys/*" 2>/dev/null | head -20

echo ""
echo "SUID files:"
find / -type f -perm -4000 2>/dev/null | while read file; do
    echo "$file ($(stat -c "%U:%G %a" "$file"))"
done

echo ""
echo "SGID files:"
find / -type f -perm -2000 2>/dev/null | while read file; do
    echo "$file ($(stat -c "%U:%G %a" "$file"))"
done

echo ""
echo "=== SENSITIVE FILE PERMISSIONS ==="
for file in "${SENSITIVE_FILES[@]}"; do
    if [[ -f "$file" ]]; then
        echo "$file: $(stat -c "%A %U:%G" "$file")"
    else
        echo "$file: FILE NOT FOUND"
    fi
done

echo ""
echo "=== CRITICAL DIRECTORY PERMISSIONS ==="
for dir in "${CRITICAL_DIRS[@]}"; do
    if [[ -d "$dir" ]]; then
        echo "$dir: $(stat -c "%A %U:%G" "$dir")"
        # Check for world-writable files in critical directories
        world_writable=$(find "$dir" -type f -perm -0002 2>/dev/null | wc -l)
        if [[ $world_writable -gt 0 ]]; then
            echo "  WARNING: $world_writable world-writable files found"
        fi
    fi
done

echo ""
echo "=== HOME DIRECTORY PERMISSIONS ==="
if [[ -d "/home" ]]; then
    for home in /home/*; do
        if [[ -d "$home" ]]; then
            user=$(basename "$home")
            perms=$(stat -c "%A" "$home")
            echo "$home: $perms"
            
            # Check for overly permissive home directories
            if [[ "$perms" =~ ....w.w.. ]] || [[ "$perms" =~ .......w. ]]; then
                echo "  WARNING: Home directory is group or world writable"
            fi
            
            # Check SSH directory permissions
            ssh_dir="$home/.ssh"
            if [[ -d "$ssh_dir" ]]; then
                ssh_perms=$(stat -c "%A" "$ssh_dir")
                echo "  $ssh_dir: $ssh_perms"
                if [[ ! "$ssh_perms" =~ ^drwx------ ]]; then
                    echo "    WARNING: .ssh directory permissions should be 700"
                fi
            fi
        fi
    done
fi

echo ""
echo "=== UNUSUAL OWNERSHIP PATTERNS ==="
echo "Files owned by UID 0 (root) in user directories:"
find /home -uid 0 2>/dev/null | head -10

echo ""
echo "Files with no owner (orphaned files):"
find / -nouser 2>/dev/null | head -10

echo ""
echo "Files with no group (orphaned files):"
find / -nogroup 2>/dev/null | head -10

echo ""
echo "=== ACL AUDIT ==="
echo "Files/directories with ACLs:"
find / -type f -exec getfacl {} \; 2>/dev/null | grep -l "user:" | head -10
find / -type d -exec getfacl {} \; 2>/dev/null | grep -l "user:" | head -10

echo ""
echo "=== IMMUTABLE FILES ==="
echo "Files with immutable attribute:"
find / -type f -exec lsattr {} \; 2>/dev/null | grep "i" | head -10

echo ""
echo "=== SECURITY RECOMMENDATIONS ==="
echo "1. Review all SUID/SGID files for necessity"
echo "2. Fix world-writable files and directories"
echo "3. Ensure sensitive files have appropriate permissions"
echo "4. Check home directory permissions (should be 755 or 750)"
echo "5. Verify .ssh directories are mode 700"
echo "6. Investigate orphaned files"
echo "7. Review ACL configurations for complexity"
echo ""
echo "=== AUDIT COMPLETE ==="
echo "Full report saved to: $REPORT_FILE"
```

## Lab Exercises
[⬆️ Back to Top](#table-of-contents)

### Lab 1: Filesystem Hierarchy Exploration 🟢
**Objective:** Navigate and understand the Linux filesystem hierarchy and directory purposes.

**Tasks:**
1. Create a comprehensive map of your system's filesystem hierarchy
2. Identify the purpose and contents of major directories
3. Analyze disk usage patterns across different filesystem areas
4. Document distribution-specific variations from standard FHS
5. Create navigation shortcuts and aliases for common locations

**Deliverables:**
- Detailed filesystem hierarchy documentation
- Disk usage analysis report
- Custom navigation script or alias collection

### Lab 2: Permission Management Mastery 🟢
**Objective:** Master basic and advanced permission management techniques.

**Tasks:**
1. Set up realistic permission scenarios (web server, shared development, backup)
2. Practice numeric and symbolic permission notation
3. Implement SUID, SGID, and sticky bit scenarios
4. Create permission inheritance patterns for directory structures
5. Troubleshoot common permission-related issues

**Deliverables:**
- Permission scenario implementations
- Troubleshooting documentation
- Permission management scripts

### Lab 3: Advanced Access Control Implementation 🟡
**Objective:** Implement granular access control using ACLs and special attributes.

**Tasks:**
1. Set up complex ACL scenarios with multiple users and groups
2. Implement default ACLs for directory inheritance
3. Create ACL backup and restore procedures
4. Use file attributes for enhanced security
5. Test ACL behavior with different applications

**Deliverables:**
- ACL implementation documentation
- Backup/restore procedures
- Security testing results

### Lab 4: Security Auditing and Remediation 🟡
**Objective:** Audit filesystem security and remediate identified issues.

**Tasks:**
1. Run comprehensive permission audits
2. Identify and fix security vulnerabilities
3. Implement monitoring for permission changes
4. Create security baseline documentation
5. Develop incident response procedures for permission issues

**Deliverables:**
- Security audit reports
- Remediation procedures
- Monitoring implementation
- Security baseline documentation

## Best Practices Summary

[⬆️ Back to Top](#table-of-contents)

### Filesystem Security Guidelines

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| **File Permissions** | Use least privilege principle | `chmod 644` for files, `chmod 755` for directories |
| **Directory Permissions** | Restrict access appropriately | `chmod 750` for shared dirs, `chmod 700` for private |
| **SUID/SGID** | Minimize usage | Regular audits, remove unnecessary permissions |
| **Sticky Bit** | Use on shared directories | `chmod +t /shared/temp` |
| **ACLs** | Document complex permissions | Backup ACLs, use sparingly |
| **Home Directories** | Secure user spaces | `chmod 755` or `chmod 750` for home dirs |
| **System Files** | Protect critical configurations | `chmod 644` for configs, `chmod 600` for secrets |

### Permission Management Workflow

1. **Assessment Phase**
   - Identify security requirements
   - Map user and group access needs
   - Document compliance requirements

2. **Implementation Phase**
   - Apply least privilege principle
   - Use groups for shared access
   - Implement ACLs for complex scenarios
   - Set appropriate umask values

3. **Monitoring Phase**
   - Regular permission audits
   - Monitor for unauthorized changes
   - Review access logs
   - Update permissions as needed

### Common Permission Patterns

```bash
# Web server files
find /var/www -type d -exec chmod 755 {} \;  # Directories
find /var/www -type f -exec chmod 644 {} \;  # Files
chown -R www-data:www-data /var/www

# Log files (readable by admin group)
chmod 640 /var/log/application.log
chown root:adm /var/log/application.log

# Configuration files (readable by service user)
chmod 640 /etc/app/config.conf
chown root:appuser /etc/app/config.conf

# Temporary shared directory
chmod 1777 /tmp/shared
# or with ACLs for specific groups:
setfacl -m d:g:team:rwx /shared/temp
```

## Troubleshooting Common Issues

[⬆️ Back to Top](#table-of-contents)

### Permission Denied Errors
```bash
# Diagnose permission issues
ls -la file_or_directory        # Check current permissions
stat file_or_directory          # Detailed file information
namei -mo /path/to/file         # Check all path components

# Check if user is in required groups
groups username
id username

# Test file access
sudo -u username test -r file   # Test read access
sudo -u username test -w file   # Test write access
sudo -u username test -x file   # Test execute access
```

### ACL Issues
```bash
# Common ACL problems and solutions
# Problem: ACL not working
mount | grep acl                # Check if ACL is enabled
getfacl file                   # Check current ACLs

# Problem: Default ACL not inherited
setfacl -k directory           # Remove default ACL
setfacl -m d:u:user:rwx dir    # Set new default ACL

# Problem: ACL conflicts with standard permissions
setfacl -b file                # Remove all ACLs
chmod standard_perms file      # Set standard permissions
```

### Ownership Issues
```bash
# Fix common ownership problems
# Problem: Files owned by wrong user after copy
chown --reference=original_file copied_file

# Problem: Recursive ownership change needed
chown -R user:group directory/

# Problem: Preserve ownership during operations
cp -p source destination       # Preserve attributes
rsync -a source/ destination/  # Archive mode preserves ownership
```

## Assessment Criteria

[⬆️ Back to Top](#table-of-contents) | **[Main Index](README.md)** 📚

Students will be evaluated based on:

| Criteria | Proficient (4) | Developing (3) | Beginning (2) | Inadequate (1) |
|----------|----------------|----------------|---------------|----------------|
| **FHS Knowledge** | Demonstrates comprehensive understanding of filesystem hierarchy and directory purposes | Good understanding with minor gaps | Basic understanding with some confusion | Limited knowledge of filesystem structure |
| **Permission Management** | Expertly manages basic and special permissions using appropriate tools | Good permission management with minor issues | Basic permission operations with guidance | Struggles with permission concepts |
| **Security Implementation** | Implements comprehensive security policies using ACLs and advanced features | Good security practices with adequate implementation | Basic security awareness with simple implementations | Poor security practices or understanding |
| **Troubleshooting Skills** | Quickly diagnoses and resolves complex permission issues | Good troubleshooting with systematic approach | Basic problem-solving with assistance | Difficulty identifying or resolving issues |

## Next Steps

[⬆️ Back to Top](#table-of-contents)

After mastering filesystem hierarchy and permissions, proceed to:

- **Module 3: Command-Line Essentials** - Apply permission knowledge while mastering essential command-line tools
- **Module 6: Users, Groups & Authentication** - Build on permission concepts to implement comprehensive user management
- **Module 8: Logging & Monitoring** - Use filesystem knowledge to understand log file organization and security monitoring

The security principles and permission management skills learned here form the foundation for all subsequent system administration tasks, from user management to service configuration and security hardening.
