# Module 6: Users, Groups & Authentication

## Overview
This module covers user and group management, authentication mechanisms, and access control in Linux systems. You'll learn to create and manage user accounts, configure authentication methods, and implement security policies.

## Learning Objectives
By the end of this module, you will be able to:
- Create and manage user accounts and groups
- Configure password policies and account security
- Implement sudo access and privilege escalation
- Understand and configure authentication methods
- Manage SSH keys and secure remote access
- Implement access control and security policies

## Topics

### 6.1 User Account Fundamentals
- User types: system vs regular users
- User identification: UID, GID
- User account files: `/etc/passwd`, `/etc/shadow`, `/etc/group`
- Home directories and user environments
- Default user creation settings

### 6.2 User Management Commands
- Creating users: `useradd`, `adduser`
- Modifying users: `usermod`
- Deleting users: `userdel`
- Password management: `passwd`, `chage`
- User information: `id`, `whoami`, `who`, `w`

### 6.3 Group Management
- Understanding groups and group membership
- Creating groups: `groupadd`
- Modifying groups: `groupmod`
- Deleting groups: `groupdel`
- Managing group membership: `usermod`, `gpasswd`

### 6.4 Sudo and Privilege Escalation
- Understanding sudo vs su
- Configuring sudoers file
- Sudo policies and restrictions
- Logging and auditing sudo usage
- Best practices for privilege escalation

### 6.5 Authentication Methods
- PAM (Pluggable Authentication Modules)
- LDAP integration
- Kerberos authentication
- Multi-factor authentication
- SSH key-based authentication

### 6.6 Access Control and Security
- Account lockout policies
- Password complexity requirements
- Session management
- User activity monitoring
- Security hardening practices

## Practical Examples

### User Management
```bash
# Create new user
sudo useradd -m -s /bin/bash john

# Create user with specific UID and GID
sudo useradd -u 1500 -g 1500 -m -s /bin/bash jane

# Set user password
sudo passwd john

# Modify user account
sudo usermod -aG sudo john

# Change user shell
sudo usermod -s /bin/zsh john

# Lock user account
sudo usermod -L john

# Unlock user account
sudo usermod -U john

# Delete user and home directory
sudo userdel -r john

# Show user information
id john
getent passwd john
```

### Group Management
```bash
# Create new group
sudo groupadd developers

# Add user to group
sudo usermod -aG developers john

# Remove user from group
sudo gpasswd -d john developers

# Change user's primary group
sudo usermod -g developers john

# List user's groups
groups john

# Show group information
getent group developers

# Delete group
sudo groupdel developers
```

### Password and Account Policies
```bash
# Set password expiration
sudo chage -E 2024-12-31 john

# Set password change requirements
sudo chage -m 7 -M 90 -W 7 john

# Show password aging information
chage -l john

# Force password change on next login
sudo chage -d 0 john

# Show account status
sudo passwd -S john
```

### Sudo Configuration
```bash
# Edit sudoers file safely
sudo visudo

# Add user to sudo group (Debian/Ubuntu)
sudo usermod -aG sudo john

# Add user to wheel group (Red Hat/CentOS)
sudo usermod -aG wheel john

# Check sudo privileges
sudo -l

# Run command as another user
sudo -u www-data command

# Switch to another user
sudo -i -u john
```

## Configuration Files

### /etc/passwd Format
```
username:x:UID:GID:GECOS:home_directory:shell
john:x:1001:1001:John Doe,,,:/home/john:/bin/bash
```

### /etc/shadow Format
```
username:encrypted_password:last_change:min_age:max_age:warn:inactive:expire:reserved
john:$6$salt$hash:18000:0:99999:7:::
```

### /etc/group Format
```
group_name:x:GID:user_list
developers:x:1001:john,jane
```

### Sudoers File Examples
```bash
# User privileges
john ALL=(ALL:ALL) ALL

# Group privileges
%sudo ALL=(ALL:ALL) ALL

# Command-specific privileges
john ALL=(root) NOPASSWD: /usr/bin/systemctl restart nginx

# Restricted command access
jane ALL=(ALL) /usr/bin/apt update, /usr/bin/apt upgrade

# Host-specific privileges
john web-servers=(ALL) ALL
```

## SSH Key Management

### Generating SSH Keys
```bash
# Generate SSH key pair
ssh-keygen -t ed25519 -C "john@example.com"

# Generate RSA key (if ed25519 not supported)
ssh-keygen -t rsa -b 4096 -C "john@example.com"

# Copy public key to remote server
ssh-copy-id user@remote-server

# Manually add public key
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
```

### SSH Configuration
```bash
# Client SSH config (~/.ssh/config)
Host myserver
    HostName server.example.com
    User john
    IdentityFile ~/.ssh/id_ed25519
    Port 2222

# Server SSH config (/etc/ssh/sshd_config)
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

## PAM Configuration

### Common PAM Modules
```bash
# /etc/pam.d/common-password
password requisite pam_pwquality.so retry=3 minlen=8 difok=3

# /etc/pam.d/common-auth
auth required pam_tally2.so deny=5 unlock_time=600

# /etc/pam.d/common-account
account required pam_access.so
```

### Password Quality Settings
```bash
# /etc/security/pwquality.conf
minlen = 8
minclass = 3
maxrepeat = 2
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
```

## User Environment Management

### Default User Settings
```bash
# /etc/default/useradd
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes

# /etc/login.defs
PASS_MAX_DAYS 90
PASS_MIN_DAYS 7
PASS_WARN_AGE 7
UID_MIN 1000
UID_MAX 60000
```

### User Profile Templates
```bash
# /etc/skel/.bashrc
# Default bashrc for new users

# /etc/skel/.profile
# Default profile for new users

# Copy skeleton files to existing user
sudo cp -r /etc/skel/. /home/john/
sudo chown -R john:john /home/john/
```

## Monitoring and Auditing

### User Activity Monitoring
```bash
# Show logged in users
who
w

# Show last logins
last
lastlog

# Show failed login attempts
sudo lastb

# Monitor user sessions
sudo aureport -au

# Check sudo usage
sudo grep sudo /var/log/auth.log
```

### Account Security Auditing
```bash
# Find accounts without passwords
sudo awk -F: '($2 == "") {print $1}' /etc/shadow

# Find accounts with UID 0
awk -F: '($3 == 0) {print $1}' /etc/passwd

# Check for duplicate UIDs
awk -F: '{print $3}' /etc/passwd | sort -n | uniq -d

# Find world-writable files in home directories
find /home -type f -perm -002 -ls
```

## Security Best Practices

| Practice | Description |
|----------|-------------|
| Strong Passwords | Enforce complex password policies |
| Regular Audits | Monitor user accounts and permissions |
| Principle of Least Privilege | Grant minimum necessary permissions |
| Disable Unused Accounts | Remove or lock inactive accounts |
| Use SSH Keys | Prefer key-based authentication |
| Monitor Login Attempts | Track failed authentication attempts |
| Regular Password Changes | Implement password rotation policies |

## Troubleshooting Common Issues

### Account Lockouts
```bash
# Check account status
sudo passwd -S username

# Unlock account
sudo passwd -u username

# Reset failed login attempts
sudo pam_tally2 --user=username --reset
```

### Permission Issues
```bash
# Fix home directory permissions
sudo chown -R username:username /home/username
sudo chmod 755 /home/username

# Reset SSH permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_*
chmod 644 ~/.ssh/*.pub
```

## Lab Exercises
1. Create a comprehensive user management script
2. Implement password policies and test enforcement
3. Configure sudo access for different user roles
4. Set up SSH key-based authentication
5. Audit user accounts and permissions

## Next Steps
With user and authentication management mastered, you're ready to explore Networking Fundamentals in Module 7, where you'll learn about network configuration and troubleshooting.
