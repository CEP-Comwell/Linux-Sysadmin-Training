# Module 13: OpenSSH Best Practices

## Overview

Learn secure SSH key management and server configuration best practices for system administrators. This module covers essential SSH security concepts, from generating secure keys to configuring hardened SSH servers. You'll learn to implement modern cryptographic algorithms and understand the differences between key types to make informed security decisions.

This module provides practical guidance for securing SSH access in small to medium environments, with focus on hands-on implementation of secure key generation, distribution, and server hardening techniques that system administrators use daily.

**Core Security Skills:**
- Generate and manage secure SSH keys using modern algorithms
- Understand encryption levels and choose appropriate key types
- Configure hardened SSH server settings (sshd_config)
- Implement secure key distribution with ssh-copy-id
- Apply SSH security best practices for daily administration
- Troubleshoot common SSH configuration issues

## Learning Objectives

By completing this module, you will be able to:

1. **Generate and Manage Secure SSH Keys**
   - Create SSH keys using ED25519, RSA, and ECDSA algorithms
   - Understand the differences between encryption levels and key types
   - Choose appropriate key types for different scenarios
   - Manage key passphrases and file permissions securely

2. **Distribute SSH Keys Securely**
   - Use ssh-copy-id to deploy public keys safely
   - Configure authorized_keys files with proper permissions
   - Understand key-based authentication benefits over passwords
   - Implement basic key rotation practices

3. **Configure Secure SSH Servers**
   - Harden sshd_config with recommended security settings
   - Disable weak algorithms and enable strong cryptography
   - Configure access controls and authentication methods
   - Implement basic logging and monitoring

4. **Apply SSH Security Best Practices**
   - Choose secure default settings for SSH clients and servers
   - Understand common SSH security vulnerabilities and mitigations
   - Implement defense-in-depth strategies for SSH access
   - Troubleshoot SSH connectivity and security issues

## Table of Contents

- [13.1 SSH Key Generation and Management](#131-ssh-key-generation-and-management)
  - Understanding SSH key types: ED25519, RSA, and ECDSA
  - Practical key generation examples with ssh-keygen
  - Key security levels and algorithm comparison
  - Managing key passphrases and file permissions

- [13.2 Secure Key Distribution](#132-secure-key-distribution)
  - Using ssh-copy-id for safe key deployment
  - Manual key installation and authorized_keys configuration
  - Key-based authentication setup and testing
  - Basic key rotation and management practices

- [13.3 SSH Server Security Configuration](#133-ssh-server-security-configuration)
  - Essential sshd_config hardening settings
  - Disabling weak algorithms and enabling strong cryptography
  - Access control and authentication configuration
  - Common security misconfigurations to avoid

- [13.4 SSH Client Configuration](#134-ssh-client-configuration)
  - Secure SSH client defaults and configuration
  - Host-specific settings and connection management
  - SSH agent usage and security considerations
  - Connection troubleshooting and debugging

- [13.5 SSH Security Best Practices](#135-ssh-security-best-practices)
  - Defense-in-depth strategies for SSH access
  - Common vulnerabilities and mitigation techniques
  - Monitoring and logging SSH activities
  - Incident response for SSH security issues

- [13.6 Practical Labs and Troubleshooting](#136-practical-labs-and-troubleshooting)
  - Hands-on key generation and distribution exercises
  - SSH server hardening configuration lab
  - Common SSH problems and solutions
  - Security validation and testing procedures
  - Advanced persistent threat (APT) detection and response
  - Insider threat monitoring and prevention
  - Supply chain security and trusted computing base
  - International security standards and regulatory compliance
  - Security architecture documentation and threat modeling


---

## Essential SSH Commands Reference

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### SSH Key Generation and Management

| Command | Description | Example |
|---------|-------------|---------|
| `ssh-keygen -t ed25519` | Generate ED25519 key (recommended) | `ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -C "user@domain.com"` |
| `ssh-keygen -t rsa -b 4096` | Generate 4096-bit RSA key | `ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -C "user@domain.com"` |
| `ssh-keygen -l -f <keyfile>` | Display key fingerprint | `ssh-keygen -l -f ~/.ssh/id_ed25519.pub` |
| `ssh-keygen -p -f <keyfile>` | Change key passphrase | `ssh-keygen -p -f ~/.ssh/id_ed25519` |
| `ssh-copy-id user@host` | Copy public key to remote host | `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server` |

### SSH Connection and Client Commands

| Command | Description | Example |
|---------|-------------|---------|
| `ssh user@host` | Basic SSH connection | `ssh admin@192.168.1.100` |
| `ssh -i <keyfile> user@host` | Connect with specific key | `ssh -i ~/.ssh/id_ed25519 user@server` |
| `ssh -p <port> user@host` | Connect to non-default port | `ssh -p 2022 user@server` |
| `scp file user@host:/path/` | Secure copy file | `scp document.txt user@server:/home/user/` |
| `ssh user@host 'command'` | Execute remote command | `ssh user@server 'sudo systemctl status nginx'` |

### SSH Server Management

| Command | Description | Example |
|---------|-------------|---------|
| `sudo systemctl status sshd` | Check SSH service status | `sudo systemctl status sshd` |
| `sudo systemctl reload sshd` | Reload SSH configuration | `sudo systemctl reload sshd` |
| `sudo sshd -t` | Test SSH configuration | `sudo sshd -t` |
| `sudo sshd -T` | Show effective configuration | `sudo sshd -T` |

### SSH Security and Troubleshooting

| Command | Description | Example |
|---------|-------------|---------|
| `ssh -v user@host` | Verbose connection (debug) | `ssh -v user@server` |
| `ssh-keygen -R hostname` | Remove host from known_hosts | `ssh-keygen -R server.domain.com` |
| `chmod 600 ~/.ssh/id_*` | Fix private key permissions | `chmod 600 ~/.ssh/id_ed25519` |
| `chmod 644 ~/.ssh/*.pub` | Fix public key permissions | `chmod 644 ~/.ssh/id_ed25519.pub` |

---


---

## 13.1 SSH Key Generation and Management

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### Understanding SSH Key Types: Choosing the Right Algorithm

#### **ED25519 (The Modern Recommended Choice)**
- **What it is**: A modern elliptic curve signature algorithm
- **Key size**: Always 256 bits (fixed, no options needed)
- **Performance**: Very fast key generation and operations
- **Security**: Excellent security with smaller key sizes
- **Compatibility**: Supported by OpenSSH 6.5+ (2014+)
- **Best for**: New systems, high-security environments, frequent use

#### **RSA (The Traditional Compatible Choice)**  
- **What it is**: Classic public-key algorithm based on factoring large numbers
- **Key size**: 2048, 3072, or 4096 bits (4096 recommended for new keys)
- **Performance**: Slower, especially for key generation
- **Security**: Good security with sufficient key size (≥4096 bits)
- **Compatibility**: Universal support across all SSH implementations
- **Best for**: Legacy systems, maximum compatibility requirements

#### **ECDSA (The Middle Ground)**
- **What it is**: Elliptic curve variant of the DSA algorithm
- **Key size**: 256, 384, or 521 bits
- **Performance**: Good performance, better than RSA
- **Security**: Good security when properly implemented
- **Compatibility**: Widely supported in modern systems
- **Best for**: When ED25519 isn't available but you want better performance than RSA

### Encryption Level Comparison

| Algorithm | Key Size | Security Level | Performance | Quantum Resistance | Recommendation |
|-----------|----------|----------------|-------------|-------------------|----------------|
| **ED25519** | 256-bit | Excellent | Very Fast | Better | ✅ **Recommended** |
| **RSA-4096** | 4096-bit | Very Good | Slow | Moderate | ✅ Legacy Support |
| **RSA-2048** | 2048-bit | Adequate | Moderate | Poor | ⚠️ Minimum Acceptable |
| **ECDSA-521** | 521-bit | Very Good | Fast | Moderate | ✅ Alternative |
| **RSA-1024** | 1024-bit | **BROKEN** | Fast | **NONE** | ❌ **Never Use** |

### Practical Key Generation Examples

```bash
# Generate ED25519 key with descriptive comment
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -C "$(whoami)@$(hostname)-$(date +'%Y%m%d')"

# Example with specific comment
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -C "admin@webserver-20250803"

# Generate with custom filename for specific purpose
ssh-keygen -t ed25519 -f ~/.ssh/backup_server_key -C "backup-server-access"
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

```bash
# Generate 4096-bit RSA key (minimum recommended size)
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -C "$(whoami)@$(hostname)-rsa4096"

# For maximum security (slower but stronger)
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_secure -C "admin@server-rsa4096"
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

```bash
# Generate ECDSA key with 521-bit curve (highest security)
ssh-keygen -t ecdsa -b 521 -f ~/.ssh/id_ecdsa -C "$(whoami)@$(hostname)-ecdsa521"
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

### Key Security Best Practices

```bash
# Generate key with interactive passphrase prompt
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_secure

# Tips for strong passphrases:
# - Use 4+ random words: "correct horse battery staple"
# - Include numbers and symbols: "correct-horse-battery-staple-42!"
# - Make it memorable but unpredictable
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

```bash
# Fix permissions for SSH directory and keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_*
chmod 644 ~/.ssh/*.pub
chmod 644 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/known_hosts

# Check permissions
ls -la ~/.ssh/
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

```bash
# Display key fingerprint and details
ssh-keygen -l -f ~/.ssh/id_ed25519.pub

# Show verbose key information
ssh-keygen -l -v -f ~/.ssh/id_ed25519.pub

# Display public key content
cat ~/.ssh/id_ed25519.pub

# Extract public key from private key (if needed)
ssh-keygen -y -f ~/.ssh/id_ed25519 > ~/.ssh/id_ed25519.pub
```

**Related Commands/Topics:** See [SSH Key Generation and Management](#ssh-key-generation-and-management) 🔗

### When to Use Each Key Type

#### **Use ED25519 When:**
- Setting up new systems (recommended default)
- High-security environments
- Performance is important
- Planning for future quantum threats
- OpenSSH 6.5+ available

#### **Use RSA-4096 When:**
- Supporting very old systems
- Corporate policy requires RSA
- Maximum compatibility needed
- Hardware tokens only support RSA

#### **Avoid These Scenarios:**
- ❌ RSA keys smaller than 4096 bits for new deployments
- ❌ DSA keys (deprecated and weak)
- ❌ RSA-1024 (completely broken)
- ❌ Unprotected private keys (no passphrase)

---


---

## 13.2 Secure Key Distribution

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### Using ssh-copy-id (Recommended Method)

The `ssh-copy-id` command is the safest and easiest way to install your public key on remote servers.

```bash
# Copy your default public key to remote server
ssh-copy-id user@server.domain.com

# Copy specific key to remote server
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server.domain.com

# Copy key to specific port
ssh-copy-id -p 2022 user@server.domain.com

# Copy key and test connection
ssh-copy-id user@server.domain.com && ssh user@server.domain.com
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

```bash
# Force key installation (overwrite existing)
ssh-copy-id -f -i ~/.ssh/id_ed25519.pub user@server

# Specify SSH options during copy
ssh-copy-id -o "StrictHostKeyChecking=no" user@server

# Copy multiple keys
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

### Manual Key Installation

Sometimes you need to manually install keys, especially in environments where ssh-copy-id isn't available or when you need more control.

```bash
# On the remote server, create SSH directory
mkdir -p ~/.ssh
chmod 700 ~/.ssh

# Add your public key to authorized_keys
echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJcZQ... user@hostname" >> ~/.ssh/authorized_keys

# Set correct permissions
chmod 600 ~/.ssh/authorized_keys

# Alternative: Copy key content from local machine
# Local: cat ~/.ssh/id_ed25519.pub
# Remote: echo "copied_key_content" >> ~/.ssh/authorized_keys
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

```bash
# Copy public key to remote server (password authentication required)
scp ~/.ssh/id_ed25519.pub user@server:~/

# On remote server, install the key
ssh user@server
cat ~/id_ed25519.pub >> ~/.ssh/authorized_keys
rm ~/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

### Testing Key-Based Authentication

```bash
# Test connection with specific key
ssh -i ~/.ssh/id_ed25519 user@server

# Test with verbose output to debug issues
ssh -v -i ~/.ssh/id_ed25519 user@server

# Test without using SSH agent
ssh -o IdentitiesOnly=yes -i ~/.ssh/id_ed25519 user@server
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

```bash
# Problem: Permission denied (publickey)
# Solutions:
# 1. Check file permissions
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys

# 2. Verify key is in authorized_keys
grep "$(cat ~/.ssh/id_ed25519.pub)" user@server:~/.ssh/authorized_keys

# 3. Check SSH server configuration allows key auth
sudo grep "PubkeyAuthentication yes" /etc/ssh/sshd_config
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

### Key Management Best Practices

```bash
# Use descriptive key names
~/.ssh/id_ed25519_webserver
~/.ssh/id_ed25519_database
~/.ssh/id_rsa_legacy_system

# Create SSH config for easy management
cat >> ~/.ssh/config << EOF
Host webserver
    HostName web.domain.com
    User admin
    IdentityFile ~/.ssh/id_ed25519_webserver

Host database
    HostName db.domain.com
    User dbadmin
    IdentityFile ~/.ssh/id_ed25519_database
EOF
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

```bash
# 1. Generate new key
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_new -C "user@host-$(date +%Y%m%d)"

# 2. Install new key alongside old one
ssh-copy-id -i ~/.ssh/id_ed25519_new.pub user@server

# 3. Test new key works
ssh -i ~/.ssh/id_ed25519_new user@server

# 4. Remove old key from authorized_keys (on remote server)
# Edit ~/.ssh/authorized_keys and remove the old key line

# 5. Replace old key locally
mv ~/.ssh/id_ed25519 ~/.ssh/id_ed25519_old
mv ~/.ssh/id_ed25519_new ~/.ssh/id_ed25519
mv ~/.ssh/id_ed25519_new.pub ~/.ssh/id_ed25519.pub
```

**Related Commands/Topics:** See [Secure Key Distribution](#secure-key-distribution) 🔗

---


---

## 13.3 SSH Server Security Configuration

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### Essential sshd_config Security Settings

The SSH server configuration file (`/etc/ssh/sshd_config`) controls how your SSH server behaves. Here are the most important security settings every system administrator should understand and implement.

#### Basic Hardened sshd_config
```bash
# /etc/ssh/sshd_config - Basic hardened configuration

# ============================================================================
# PROTOCOL AND BASIC SETTINGS
# ============================================================================

# Always use SSH Protocol 2 (SSH-1 is insecure and deprecated)
Protocol 2

# Consider changing the default port to reduce automated attacks
# Port 2022

# ============================================================================
# AUTHENTICATION SETTINGS
# ============================================================================

# Disable root login - use sudo instead
PermitRootLogin no

# Prefer key-based authentication over passwords
PubkeyAuthentication yes
PasswordAuthentication no
PermitEmptyPasswords no

# Allow up to 3 authentication attempts
MaxAuthTries 3

# ============================================================================
# CRYPTOGRAPHIC ALGORITHMS (MODERN SECURE DEFAULTS)
# ============================================================================

# Strong ciphers only
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

# Secure Message Authentication Codes
MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha2-512

# Modern key exchange algorithms
KexAlgorithms curve25519-sha256@libssh.org,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512

# ============================================================================
# ACCESS CONTROL
# ============================================================================

# Limit which users can connect (choose one approach)
# Option 1: Allow specific users
AllowUsers sysadmin deployer

# Option 2: Allow specific groups
# AllowGroups ssh-users admin

# Option 3: Deny specific users/groups
# DenyUsers guest nobody root

# ============================================================================
# CONNECTION LIMITS AND TIMEOUTS
# ============================================================================

# Maximum concurrent connections
MaxStartups 3:30:10

# Disconnect idle connections
ClientAliveInterval 300
ClientAliveCountMax 2

# Time limit for authentication
LoginGraceTime 30

# ============================================================================
# DISABLE UNNECESSARY FEATURES
# ============================================================================

# Disable X11 forwarding (security risk)
X11Forwarding no

# Disable TCP forwarding by default (enable per-user if needed)
AllowTcpForwarding no

# Disable agent forwarding by default
AllowAgentForwarding no

# ============================================================================
# LOGGING
# ============================================================================

# Enhanced logging for security monitoring
LogLevel VERBOSE
SyslogFacility AUTH

# ============================================================================
# OPTIONAL: USER-SPECIFIC SETTINGS
# ============================================================================

# Example: Allow specific features for certain users
# Match User deployer
#     AllowTcpForwarding yes
#     X11Forwarding no
```

#### Step-by-Step Configuration Process

```bash
# 1. Backup the original configuration
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup

# 2. Edit the configuration file
sudo nano /etc/ssh/sshd_config

# 3. Test the configuration before applying
sudo sshd -t

# 4. If test passes, reload SSH service
sudo systemctl reload sshd

# 5. Test your connection from another terminal
ssh user@localhost
```

### Understanding Key sshd_config Options

#### Authentication Settings
```bash
# PermitRootLogin no
# Prevents direct root SSH access. Use sudo instead.
# Alternative: "prohibit-password" allows key-based root login

# PasswordAuthentication no
# Disables password login, forcing key-based authentication
# Keep "yes" initially, change to "no" after keys are deployed

# MaxAuthTries 3
# Limits failed authentication attempts per connection
# Prevents brute force attacks
```

#### Cryptographic Algorithm Choices
```bash
# These algorithms are recommended for 2025:

# Ciphers (Encryption):
# - chacha20-poly1305@openssh.com: Modern, fast, secure
# - aes256-gcm@openssh.com: Standard AES with authentication
# - aes256-ctr: Strong AES cipher

# MACs (Message Authentication):
# - hmac-sha2-256-etm@openssh.com: Encrypt-then-MAC (preferred)
# - hmac-sha2-512-etm@openssh.com: Stronger variant

# Key Exchange:
# - curve25519-sha256@libssh.org: Modern elliptic curve
# - diffie-hellman-group16-sha512: Strong traditional method
```

#### Access Control Options
```bash
# Choose ONE approach for user access control:

# Method 1: Allow specific users (most common)
AllowUsers admin deployer john

# Method 2: Allow specific groups
AllowGroups ssh-users administrators

# Method 3: Deny specific users (use with caution)
DenyUsers root guest nobody

# Method 4: Combination (more complex)
AllowGroups ssh-users
DenyUsers root
```

### Common Configuration Mistakes to Avoid

#### Security Anti-Patterns
```bash
# ❌ DON'T DO THESE:

# Never disable all authentication methods
# PasswordAuthentication no
# PubkeyAuthentication no

# Don't use weak algorithms
# Ciphers 3des-cbc,blowfish-cbc
# MACs hmac-md5,hmac-sha1

# Don't allow unrestricted root access
# PermitRootLogin yes

# Don't allow empty passwords
# PermitEmptyPasswords yes

# Don't disable host key checking
# StrictHostKeyChecking no
```

#### Safe Configuration Changes
```bash
# ✅ DO THIS INSTEAD:

# Keep password auth enabled until keys are deployed
PasswordAuthentication yes  # Initially
# Then change to:
# PasswordAuthentication no  # After key deployment

# Always test configuration before applying
sudo sshd -t

# Keep a backup SSH session open when making changes
ssh user@server  # Keep this session open while testing

# Use Match blocks for user-specific settings
Match User deployer
    AllowTcpForwarding yes
    X11Forwarding no
```

### Configuration Validation and Testing

#### Test Configuration Changes
```bash
# 1. Test configuration syntax
sudo sshd -t

# 2. Show effective configuration
sudo sshd -T

# 3. Test specific user settings
sudo sshd -T -C user=admin,host=server,addr=192.168.1.100

# 4. Check what algorithms are actually available
ssh -Q kex    # Key exchange algorithms
ssh -Q cipher # Cipher algorithms
ssh -Q mac    # MAC algorithms
```

#### Monitor SSH Service
```bash
# Check SSH service status
sudo systemctl status sshd

# View recent SSH logs
sudo journalctl -u sshd --since "1 hour ago"

# Monitor failed login attempts
sudo grep "Failed password" /var/log/auth.log

# View successful logins
sudo grep "Accepted" /var/log/auth.log
```

---


---

### SSH Client Configuration and Best Practices

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

The SSH client configuration file (`~/.ssh/config`) allows you to set defaults and host-specific settings for easier and more secure connections.

#### Basic SSH Client Configuration
```bash
# ~/.ssh/config - User SSH client configuration

# Global defaults for all connections
Host *
    # Use only secure algorithms
    KexAlgorithms curve25519-sha256@libssh.org,diffie-hellman-group16-sha512
    Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com
    MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com
    
    # Security settings
    StrictHostKeyChecking ask
    VerifyHostKeyDNS yes
    
    # Prefer newer SSH protocol features
    Protocol 2
    
    # Connection settings
    ServerAliveInterval 60
    ServerAliveCountMax 3
    
    # Disable weak features
    ForwardAgent no
    ForwardX11 no

# Example: Web server connection
Host webserver
    HostName web.example.com
    User admin
    Port 2022
    IdentityFile ~/.ssh/id_ed25519_webserver
    
# Example: Database server with jump host
Host database
    HostName db.internal.example.com
    User dbadmin
    ProxyJump bastion.example.com
    IdentityFile ~/.ssh/id_ed25519_database

# Example: Bastion host configuration
Host bastion
    HostName bastion.example.com
    User sysadmin
    Port 22
    IdentityFile ~/.ssh/id_ed25519
    ForwardAgent no
```

#### Advanced Client Configuration Examples
```bash
# Multiple environments with different keys
Host prod-*
    User admin
    IdentityFile ~/.ssh/id_ed25519_production
    StrictHostKeyChecking yes

Host dev-*
    User developer
    IdentityFile ~/.ssh/id_ed25519_development
    StrictHostKeyChecking ask

Host test-*
    User testuser
    IdentityFile ~/.ssh/id_rsa_testing
    
# SFTP-only host
Host fileserver
    HostName files.example.com
    User backup
    IdentityFile ~/.ssh/id_ed25519_backup
    RequestTTY no
    RemoteCommand /usr/lib/openssh/sftp-server
```

#### SSH Agent Usage and Security

SSH Agent stores decrypted private keys in memory, allowing you to use them without entering passphrases repeatedly.

```bash
# Start SSH agent (usually automatic in modern systems)
eval $(ssh-agent)

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Add key with timeout (removes after 1 hour)
ssh-add -t 3600 ~/.ssh/id_ed25519

# List loaded keys
ssh-add -l

# Remove specific key from agent
ssh-add -d ~/.ssh/id_ed25519

# Remove all keys from agent
ssh-add -D

# Stop SSH agent
ssh-agent -k
```

#### SSH Agent Security Considerations
```bash
# ✅ Good practices:
# - Use timeouts for keys in production
ssh-add -t 7200 ~/.ssh/id_ed25519  # 2 hours

# - Don't forward agent to untrusted hosts
Host untrusted-server
    ForwardAgent no

# - Use confirmation for sensitive keys
ssh-add -c ~/.ssh/id_ed25519_critical

# ❌ Avoid these:
# - Don't forward agent by default
# ForwardAgent yes  # Dangerous

# - Don't leave agent running indefinitely on servers
```

---


---

## 13.5 SSH Security Best Practices

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### Defense-in-Depth Strategies

#### Network Level Security
```bash
# 1. Use non-standard SSH ports
Port 2022

# 2. Implement firewall rules
sudo ufw allow 2022/tcp
sudo ufw deny 22/tcp

# 3. Use fail2ban for brute force protection
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

#### Host Level Security
```bash
# 1. Keep SSH updated
sudo apt update && sudo apt upgrade openssh-server

# 2. Use host-based keys
sudo ssh-keygen -A  # Generate new host keys

# 3. Implement proper logging
sudo journalctl -u sshd -f  # Monitor SSH logs in real-time
```

#### User Level Security
```bash
# 1. Use strong key passphrases
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_strong

# 2. Rotate keys regularly
# Generate new key, deploy, remove old key

# 3. Use principle of least privilege
# Grant minimum necessary access per user
```

### Common SSH Vulnerabilities and Mitigations

#### Weak Authentication
```bash
# Problem: Password-based authentication
# Solution: Enforce key-based authentication
PasswordAuthentication no
PubkeyAuthentication yes

# Problem: Weak passwords
# Solution: Disable password auth, use strong key passphrases
```

#### Poor Key Management
```bash
# Problem: Shared or unprotected keys
# Solution: Individual keys per user, proper permissions
chmod 600 ~/.ssh/id_*
chmod 700 ~/.ssh/

# Problem: Old or weak keys
# Solution: Regular key rotation, use ED25519
```

#### Configuration Errors
```bash
# Problem: Default settings
# Solution: Explicit secure configuration
Protocol 2
PermitRootLogin no
MaxAuthTries 3

# Problem: Unnecessary features enabled
# Solution: Disable unused features
X11Forwarding no
AllowTcpForwarding no
```

### Monitoring and Logging SSH Activities

#### Essential Log Monitoring
```bash
# Monitor failed authentication attempts
sudo grep "Failed password" /var/log/auth.log

# Monitor successful logins
sudo grep "Accepted" /var/log/auth.log

# Monitor root login attempts
sudo grep "root" /var/log/auth.log

# Monitor unusual activity
sudo grep "Invalid user" /var/log/auth.log
```

#### Real-time Monitoring
```bash
# Watch SSH logs in real-time
sudo tail -f /var/log/auth.log | grep ssh

# Monitor with journalctl
sudo journalctl -u sshd -f

# Monitor failed attempts specifically
sudo journalctl -u sshd --since "1 hour ago" | grep -i failed
```

#### Setting Up Alerts
```bash

> **Note:** Automated alert scripts and cron-based email notifications are considered advanced/enterprise topics. For beginner and intermediate training, focus on learning basic SSH log monitoring and manual review. Once you are comfortable with shell scripting and cron jobs, you can explore automation as a next step.

---


---

## 13.6 Practical Labs and Troubleshooting

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

### Lab 1: SSH Key Generation and Distribution

**Objective:** Generate secure keys and distribute them to remote servers

**Tasks:**
1. Generate ED25519 and RSA keys with proper security
2. Use ssh-copy-id to distribute keys to test servers
3. Test key-based authentication and disable password auth
4. Verify security with key fingerprints

**Step-by-Step Lab:**
```bash
# 1. Generate keys
ssh-keygen -t ed25519 -f ~/.ssh/lab_ed25519 -C "lab-exercise-$(date +%Y%m%d)"
ssh-keygen -t rsa -b 4096 -f ~/.ssh/lab_rsa -C "lab-exercise-rsa-$(date +%Y%m%d)"

# 2. Set proper permissions
chmod 600 ~/.ssh/lab_*
chmod 644 ~/.ssh/lab_*.pub

# 3. Copy keys to test server
ssh-copy-id -i ~/.ssh/lab_ed25519.pub user@testserver
ssh-copy-id -i ~/.ssh/lab_rsa.pub user@testserver

# 4. Test connections
ssh -i ~/.ssh/lab_ed25519 user@testserver
ssh -i ~/.ssh/lab_rsa user@testserver

# 5. Verify key fingerprints match
ssh-keygen -l -f ~/.ssh/lab_ed25519.pub
ssh user@testserver "ssh-keygen -l -f ~/.ssh/authorized_keys"
```

### Lab 2: SSH Server Hardening

**Objective:** Configure a secure SSH server with hardened settings

**Tasks:**
1. Backup original sshd_config
2. Implement recommended security settings
3. Test configuration and reload service
4. Validate security improvements

**Step-by-Step Lab:**
```bash
# 1. Backup configuration
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup

# 2. Apply hardened configuration (use previous example)
sudo nano /etc/ssh/sshd_config

# 3. Test configuration
sudo sshd -t

# 4. Reload SSH service
sudo systemctl reload sshd

# 5. Test connection
ssh user@localhost

# 6. Verify security settings
sudo sshd -T | grep -E "(Protocol|PasswordAuth|PermitRoot|MaxAuth)"
```

### Common SSH Problems and Solutions

#### Problem: "Permission denied (publickey)"
```bash
# Diagnosis:
ssh -v user@server  # Verbose output shows what's failing

# Common causes and solutions:
# 1. Wrong key permissions
chmod 600 ~/.ssh/id_*

# 2. Wrong authorized_keys permissions on server
chmod 600 ~/.ssh/authorized_keys

# 3. Key not in authorized_keys
ssh-copy-id user@server

# 4. Server doesn't allow key auth
# Check: PubkeyAuthentication yes
```

#### Problem: "Host key verification failed"
```bash
# Diagnosis:
ssh -v user@server

# Solutions:
# 1. Remove old host key
ssh-keygen -R server.domain.com

# 2. Accept new host key
ssh -o StrictHostKeyChecking=ask user@server

# 3. Verify host key fingerprint
ssh-keygen -l -f /etc/ssh/ssh_host_ed25519_key.pub  # On server
```

#### Problem: Connection timeouts or hangs
```bash
# Diagnosis:
ssh -v user@server  # Shows where connection stops

# Common solutions:
# 1. Check network connectivity
ping server.domain.com

# 2. Check firewall rules
sudo ufw status

# 3. Check SSH service status
sudo systemctl status sshd

# 4. Try different port
ssh -p 2022 user@server
```

#### Problem: Slow SSH connections
```bash
# Common causes and solutions:

# 1. DNS resolution issues
# Add to sshd_config: UseDNS no

# 2. GSSAPI authentication delay
# Add to ssh_config: GSSAPIAuthentication no

# 3. Large known_hosts file
ssh-keygen -H -f ~/.ssh/known_hosts  # Hash hostnames
```

### Security Validation and Testing

#### SSH Security Audit Checklist
```bash
# 1. Check SSH version
ssh -V

# 2. Verify secure algorithms
sudo sshd -T | grep -E "(Ciphers|MACs|KexAlgorithms)"

# 3. Check authentication settings
sudo sshd -T | grep -E "(PasswordAuth|PubkeyAuth|PermitRoot)"

# 4. Verify access controls
sudo sshd -T | grep -E "(AllowUsers|AllowGroups|DenyUsers)"

# 5. Check logging configuration
sudo sshd -T | grep -E "(LogLevel|SyslogFacility)"

# 6. Review active connections
who
w
last
```

#### Automated Security Testing
```bash
# Using ssh-audit (install with: pip install ssh-audit)
ssh-audit server.domain.com

# Manual algorithm testing
ssh -Q kex    # List supported key exchange algorithms
ssh -Q cipher # List supported ciphers
ssh -Q mac    # List supported MAC algorithms

# Test specific algorithm support
ssh -o KexAlgorithms=curve25519-sha256@libssh.org user@server
ssh -o Ciphers=chacha20-poly1305@openssh.com user@server
```

---


---

## Summary

[1a Back to Top](#table-of-contents) | [139 Main Index](../README.md) 1a

This streamlined Module 13 provides essential SSH best practices for beginner to intermediate system administrators. The module emphasizes:

- **Practical Key Generation**: Understanding ED25519 vs RSA encryption levels and choosing appropriate algorithms
- **Secure Key Distribution**: Using ssh-copy-id for safe public key deployment
- **SSH Server Hardening**: Essential sshd_config settings for secure server configuration
- **Hands-on Troubleshooting**: Common SSH problems and practical solutions
- **Security Best Practices**: Defense-in-depth strategies suitable for small to medium environments

Key takeaways include using ED25519 keys for new systems, implementing key-based authentication, hardening SSH server configuration with modern algorithms, and maintaining proper security monitoring. These fundamentals provide a solid foundation for secure SSH administration without overwhelming complexity.
