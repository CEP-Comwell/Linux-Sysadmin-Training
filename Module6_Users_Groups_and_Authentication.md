# Module 6: Users, Groups & Authentication

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [6.1 User Account Fundamentals](#61-user-account-fundamentals)
  - [6.2 Basic User Management](#62-basic-user-management)
  - [6.3 Group Management Basics](#63-group-management-basics)
  - [6.4 Sudo Configuration](#64-sudo-configuration)
  - [6.5 Password Policies and Security](#65-password-policies-and-security)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
- [Lab Exercises](#lab-exercises)
- [Best Practices Summary](#best-practices-summary)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
Master essential user and group management, and sudo configuration for Linux systems. This module focuses on fundamental user administration tasks that every Linux administrator needs to know, providing practical hands-on experience with user accounts, groups, and privilege escalation.

**Key Learning Outcomes:**
- Create, modify, and delete user accounts with proper configuration
- Manage groups and group memberships effectively
- Configure sudo access for administrative users
- Implement basic password policies and account security
- Perform routine user administration tasks safely and efficiently

## Learning Objectives
By the end of this module, you will be able to:

1. **Master Basic User Administration**: Create, modify, and manage user accounts with appropriate settings
2. **Manage Groups Effectively**: Create groups, assign users, and understand group-based permissions
3. **Configure Sudo Access**: Set up sudoers file for safe administrative access
4. **Implement Password Policies**: Configure basic password requirements and account security
5. **Perform Daily Tasks**: Handle routine user administration tasks confidently and safely
6. **Troubleshoot Common Issues**: Identify and resolve typical user and authentication problems

## Topics

### 6.1 User Account Fundamentals
- User account types: regular users, system users, and service accounts
- User identification: UID/GID basics and numbering conventions
- Key account files: `/etc/passwd`, `/etc/shadow`, `/etc/group` overview
- Home directory management and user environment setup
- Default shell configuration and user profiles
- Account creation, modification, and deletion procedures

### 6.2 Basic User Management
- Creating user accounts with `useradd` command and options
- Modifying existing users with `usermod`
- Setting and changing passwords with `passwd`
- Managing account expiration and password aging with `chage`
- Deleting user accounts safely with `userdel`
- Understanding user account status and information commands

### 6.3 Group Management Basics
- Creating and deleting groups with `groupadd` and `groupdel`
- Adding and removing users from groups with `gpasswd` and `usermod`
- Understanding primary vs supplementary groups
- Using groups for file permissions and access control
- Managing group passwords and group administrators
- Common system groups and their purposes

### 6.4 Sudo Configuration
- Understanding sudo vs su for privilege escalation
- Basic sudoers file configuration and syntax
- Using `visudo` to safely edit the sudoers file
- Granting administrative access to users and groups
- Common sudo rules and best practices
- Sudo logging and security considerations

### 6.5 Password Policies and Security
- Configuring password complexity requirements
- Setting password aging policies with `/etc/login.defs`
- Account lockout mechanisms for security
- Understanding authentication logs and basic monitoring
- User session monitoring and login tracking
- Basic security best practices for user management

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
| `lastlog` | Show last login times | `-u`, `-t` | `lastlog -u john` |

### Monitoring and Auditing Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `who` | Show logged in users | `-a`, `-b`, `-H` | `who -a` |
| `w` | Show user activity | `-h`, `-s` | `w john` |
| `last` | Show login history | `-n`, `-F`, `-i` | `last -n 10 john` |
| `lastb` | Show failed logins | `-n`, `-F` | `lastb -n 20` |

## Practical Examples

### Basic User and Group Management

#### Creating and Managing Users
```bash
# Create a new user with home directory
sudo useradd -m -s /bin/bash john
sudo passwd john

# Create user with specific UID and groups
sudo useradd -m -u 1500 -G sudo,developers -c "John Doe" john

# Modify existing user - add to group
sudo usermod -aG sudo john

# Lock and unlock user accounts
sudo usermod -L john    # Lock account
sudo usermod -U john    # Unlock account

# Set account expiration
sudo chage -E 2025-12-31 john

# View user information
id john
getent passwd john
groups john
finger john    # If finger package is installed

# Delete user (with or without home directory)
sudo userdel john           # Keep home directory
sudo userdel -r john        # Remove home directory
```

#### Basic Group Management
```bash
# Create new groups
sudo groupadd developers
sudo groupadd -g 2000 webadmins    # With specific GID

# Add users to groups
sudo gpasswd -a john developers
sudo usermod -aG webadmins john

# Remove user from group
sudo gpasswd -d john developers

# List group members
getent group developers
grep developers /etc/group

# Delete group
sudo groupdel developers
```

### Basic Sudo Configuration

#### Understanding Sudoers File
```bash
# Edit sudoers file safely
sudo visudo

# Basic sudoers syntax examples:
# user    host=(runasuser) commands
# %group  host=(runasuser) commands

# Grant full sudo access to user
john    ALL=(ALL:ALL) ALL

# Grant sudo access to group
%sudo   ALL=(ALL:ALL) ALL

# Allow specific commands without password
john    ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx

# Allow user to run commands as specific user
john    ALL=(www-data) /usr/bin/php

# Allow group to manage services
%webadmins ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart apache2, /usr/bin/systemctl reload nginx
```

## Lab Exercises

### Lab 1: Basic User Management
**Objective:** Practice fundamental user account operations and group management.

**Tasks:**
1. Create three user accounts: alice, bob, and charlie
2. Set up a `developers` group and add alice and bob to it
3. Create a `managers` group and add charlie to it
4. Configure password aging for all users (90-day maximum age)
5. Practice modifying user accounts (changing shells, adding groups)
6. Safely delete a test user account

**Commands to Practice:**
```bash
# User creation and management
sudo useradd -m -s /bin/bash alice
sudo passwd alice
sudo usermod -aG developers alice
sudo chage -M 90 alice

# Group management
sudo groupadd developers
sudo gpasswd -a alice developers

# User information
id alice
groups alice
getent passwd alice
```

**Deliverables:**
- Documentation of all commands used
- Screenshot showing user and group information
- Notes on any issues encountered and how they were resolved

## Lab Exercises

### Lab 1: Basic User Management
**Objective:** Practice fundamental user account operations and group management.

**Tasks:**
1. Create three user accounts: alice, bob, and charlie
2. Set up a `developers` group and add alice and bob to it
3. Create a `managers` group and add charlie to it
4. Configure password aging for all users (90-day maximum age)
5. Practice modifying user accounts (changing shells, adding groups)
6. Safely delete a test user account

**Commands to Practice:**
```bash
# User creation and management
sudo useradd -m -s /bin/bash alice
sudo passwd alice
sudo usermod -aG developers alice
sudo chage -M 90 alice

# Group management
sudo groupadd developers
sudo gpasswd -a alice developers

# User information
id alice
groups alice
getent passwd alice
```

**Deliverables:**
- Documentation of all commands used
- Screenshot showing user and group information
- Notes on any issues encountered and how they were resolved

### Lab 2: Sudo Configuration and Access Control
**Objective:** Configure sudo access for administrative tasks.

**Tasks:**
1. Grant alice full sudo access
2. Allow bob to restart web services without a password
3. Create a custom sudo rule for charlie to manage user accounts
4. Test all sudo configurations
5. Monitor sudo usage in logs

**Example Configurations:**
```bash
# Add alice to sudo group
sudo usermod -aG sudo alice

# Create custom rule for bob (in /etc/sudoers.d/bob)
bob ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart apache2, /usr/bin/systemctl restart nginx

# Create custom rule for charlie (in /etc/sudoers.d/charlie)
charlie ALL=(ALL) /usr/sbin/useradd, /usr/sbin/usermod, /usr/sbin/userdel
```

**Deliverables:**
- Working sudo configurations
- Test results showing proper access control
- Log entries showing sudo usage

### Lab 3: Password Policies and Security
**Objective:** Implement basic password policies and monitor user activity.

**Tasks:**
1. Configure system-wide password aging policies
2. Set up password complexity requirements
3. Monitor user login activity
4. Practice account lockout and recovery procedures
5. Generate basic user activity reports

**Security Commands:**
```bash
# Monitor user activity
who
w
last -n 20
lastb -n 10

# Check password aging
chage -l username

# View authentication logs
sudo grep "authentication" /var/log/auth.log
```

**Deliverables:**
- Configured password policies
- User activity monitoring reports
- Documentation of security measures implemented



## Best Practices Summary

### User Management Best Practices

1. **Naming Conventions**
   - Use lowercase usernames
   - Keep usernames simple and descriptive
   - Avoid special characters and spaces
   - Keep usernames under 32 characters

2. **Account Creation**
   - Always create home directories with `-m` flag
   - Set appropriate default shell with `-s` option
   - Use meaningful account descriptions
   - Set initial passwords securely

3. **Password Management**
   - Enforce reasonable password requirements
   - Set appropriate password aging (e.g., 90 days)
   - Require users to change default passwords
   - Monitor password strength

4. **Group Management**
   - Use groups to organize users by function
   - Follow principle of least privilege
   - Keep group membership up to date
   - Use descriptive group names

### Sudo Configuration Best Practices

1. **Configuration Management**
   - Use `/etc/sudoers.d/` for individual user rules
   - Always use `visudo` for editing sudo files
   - Start with minimal privileges and expand as needed
   - Document why specific sudo access is granted

2. **Security Guidelines**
   - Use groups rather than individual users when possible
   - Specify exact commands instead of ALL when possible
   - Test all sudo configurations before deploying
   - Monitor sudo usage in logs regularly

### Security and Maintenance

1. **Account Hygiene**
   - Remove accounts for departing users promptly
   - Disable rather than delete accounts when unsure
   - Monitor for unused accounts
   - Keep user information current

2. **Monitoring**
   - Check authentication logs for failed attempts
   - Monitor sudo usage and privilege escalation
   - Be aware of users with multiple group memberships
   - Review user account activity regularly

3. **Documentation**
   - Keep documentation of user management procedures
   - Back up important configuration files
   - Test user account functionality regularly
   - Know how to recover from common issues
- **Backup Procedures**: Automate backup of authentication configurations
- **Testing Automation**: Implement automated security testing

#### Monitoring and Alerting
- **Real-Time Monitoring**: Monitor authentication events in real-time
- **Anomaly Detection**: Implement systems to detect unusual access patterns
- **Failed Login Tracking**: Monitor and alert on failed login attempts
- **Privilege Escalation Detection**: Monitor for unauthorized privilege changes
- **Compliance Monitoring**: Continuously monitor compliance with security policies

## Troubleshooting Common Issues

### User Account Problems

#### User Cannot Login
**Common Causes:**
- Account is locked or disabled
- Password has expired
- Account has expired

**Quick Checks:**
```bash
# Check account status
sudo passwd -S username
sudo chage -l username

# Check recent login attempts
last username
lastb username
```

**Solutions:**
- Unlock account: `sudo passwd -u username`
- Reset password: `sudo passwd username`
- Remove account expiration: `sudo chage -E -1 username`

#### Password Issues
**Common Problems:**
- User forgot password
- Password complexity requirements not met
- Password has expired

**Solutions:**
```bash
# Reset password as administrator
sudo passwd username

# Force password change on next login
sudo chage -d 0 username

# Check password aging settings
sudo chage -l username
```

### Sudo Problems

#### "User not in sudoers file" Error
**Cause:** User doesn't have sudo privileges

**Solution:**
```bash
# Add user to sudo group
sudo usermod -aG sudo username

# Or create custom sudo rule
sudo visudo
# Add line: username ALL=(ALL:ALL) ALL
```

#### Sudo Configuration Errors
**Symptoms:** Syntax errors in sudoers file

**Solution:**
```bash
# Always use visudo to edit safely
sudo visudo

# Check syntax without saving
sudo visudo -c
```

### Group Management Issues

#### User Not Getting Group Permissions
**Cause:** User needs to log out and back in for group changes

**Solutions:**
- Have user log out and log back in
- Use `newgrp groupname` for temporary group change
- Verify group membership with `groups username`

#### Cannot Delete Group
**Cause:** Group is still assigned to files or users

**Solutions:**
```bash
# Check if group has members
getent group groupname

# Find files owned by group
find /home -group groupname 2>/dev/null

# Remove group after fixing ownership
sudo groupdel groupname
```

### General Troubleshooting Tips

1. **Check logs first:** `/var/log/auth.log` for authentication issues
2. **Verify file permissions:** Use `ls -l` to check ownership and permissions
3. **Test one change at a time:** Don't make multiple changes simultaneously
4. **Use diagnostic commands:** `id`, `groups`, `getent` for information gathering
5. **Have a rollback plan:** Know how to undo changes if something breaks
- **Remove users from group first:** `sudo gpasswd -d username groupname`
- **Change file ownership:** `sudo chgrp newgroup /path/to/files`
- **Use correct syntax:** `sudo groupdel groupname`

### Password and Authentication Issues

#### Password Policy Not Enforced
**Symptoms:** Users can set weak passwords

**Diagnostic Steps:**
```bash
# Check password policy settings
sudo cat /etc/login.defs | grep PASS_
sudo cat /etc/security/pwquality.conf

# Test password setting
echo "username:weakpass" | sudo chpasswd
```

**Common Solutions:**
- **Configure pwquality:** Edit `/etc/security/pwquality.conf`
- **Update login.defs:** Set proper values in `/etc/login.defs`
- **Install required packages:** `sudo apt install libpam-pwquality`

### File Permission Issues

#### Home Directory Problems
**Symptoms:** User cannot access their own home directory

**Diagnostic Steps:**
```bash
# Check home directory ownership and permissions
ls -ld /home/username
ls -la /home/username

# Check if home directory exists
getent passwd username | cut -d: -f6
```

**Common Solutions:**
```bash
# Fix ownership
sudo chown username:username /home/username

# Fix permissions
sudo chmod 755 /home/username

# Create missing home directory
sudo mkdir /home/username
sudo cp -r /etc/skel/. /home/username/
sudo chown -R username:username /home/username
```

### Quick Reference Commands

#### Essential Troubleshooting Commands
```bash
# User information
id username
getent passwd username
groups username

# Account status
sudo passwd -S username
sudo chage -l username

# Login history
last username
lastb username

# File permissions
ls -la /home/username
ls -la /home/username/.ssh

# System logs
sudo tail -f /var/log/auth.log
sudo grep username /var/log/auth.log


## Summary

This module covered the essential skills for managing users, groups, and basic authentication in Linux systems. You learned:

### Key Concepts
- Creating and managing user accounts
- Working with groups and permissions
- Configuring sudo access
- Basic password management and security
- Troubleshooting common authentication issues

### Essential Commands Mastered
- User management: `useradd`, `usermod`, `userdel`
- Group management: `groupadd`, `groupmod`, `groupdel`
- Password management: `passwd`, `chage`
- Information commands: `id`, `groups`, `getent`
- Sudo configuration: `visudo`, `usermod -aG sudo`

### Best Practices Applied
- Following principle of least privilege
- Using proper naming conventions
- Maintaining good documentation
- Regular monitoring and maintenance
- Safe configuration file editing

## Next Steps

Continue your Linux administration journey with:

- **Module 7: Networking Fundamentals** - Learn network configuration and security
- **Module 8: Logging and Monitoring** - Monitor user activity and system health
- **Module 13: OpenSSH Best Practices** - Advanced SSH security (referenced in this module)

The user management skills from this module provide the foundation for all subsequent Linux system administration tasks.
