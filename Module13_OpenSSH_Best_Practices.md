# Module 13: OpenSSH Best Practices

## Overview
This module covers advanced OpenSSH configuration, security hardening, and best practices for secure remote access. You'll learn to implement robust SSH security, manage keys at scale, and configure advanced features for enterprise environments.

## Learning Objectives
By the end of this module, you will be able to:
- Configure and harden OpenSSH for enterprise security
- Implement advanced SSH authentication methods
- Manage SSH keys at scale across infrastructure
- Configure SSH tunneling and port forwarding
- Set up SSH Certificate Authorities (CA)
- Monitor and audit SSH access

## Topics

### 13.1 SSH Security Fundamentals
- SSH protocol versions and security implications
- Authentication methods and their security levels
- Common SSH attack vectors and mitigation
- Security hardening principles
- Compliance and regulatory considerations

### 13.2 Advanced SSH Server Configuration
- SSH daemon configuration options
- Security-focused sshd_config settings
- Multi-factor authentication integration
- Host-based authentication
- Custom banner and legal notices

### 13.3 SSH Key Management
- Key generation best practices
- Key rotation and lifecycle management
- Centralized key management
- SSH agent and agent forwarding
- Key-based restrictions and forced commands

### 13.4 SSH Certificate Authorities
- Understanding SSH CA architecture
- Setting up SSH Certificate Authority
- User and host certificate management
- Certificate-based authentication workflow
- Revocation and certificate lifecycle

### 13.5 SSH Tunneling and Port Forwarding
- Local, remote, and dynamic port forwarding
- VPN-like functionality with SSH
- Reverse tunnels and NAT traversal
- ProxyCommand and jump hosts
- SSH bastion host configuration

### 13.6 Monitoring and Auditing
- SSH logging and log analysis
- Connection monitoring and alerting
- Session recording and playback
- Compliance reporting and auditing
- Intrusion detection for SSH

## Practical Examples

### SSH Server Hardening

#### Secure sshd_config Configuration
```bash
# /etc/ssh/sshd_config - Hardened configuration

# Protocol and Encryption
Protocol 2
Port 2222  # Change default port
AddressFamily inet  # IPv4 only (or inet6 for IPv6)

# Host Keys - Use only strong algorithms
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key

# Ciphers and algorithms
Ciphers aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr
MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp521,ecdh-sha2-nistp384,ecdh-sha2-nistp256

# Authentication
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM yes

# Login restrictions
LoginGraceTime 30
MaxAuthTries 3
MaxSessions 2
MaxStartups 3:30:10

# User and group restrictions
AllowUsers admin deploy
AllowGroups ssh-users
DenyUsers root
DenyGroups wheel

# Network and connection settings
ClientAliveInterval 300
ClientAliveCountMax 2
TCPKeepAlive no
Compression no
X11Forwarding no
AllowTcpForwarding no
AllowStreamLocalForwarding no
GatewayPorts no

# Logging
SyslogFacility AUTH
LogLevel VERBOSE

# Banner and messages
Banner /etc/ssh/banner
PrintMotd no
PrintLastLog yes

# Chroot and restrictions
Match User deploy
    ChrootDirectory /srv/deployment
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
```

#### SSH Security Banner
```bash
# /etc/ssh/banner
***************************************************************************
                            AUTHORIZED ACCESS ONLY
                           
This system is for authorized users only. All activities are monitored
and logged. Unauthorized access is prohibited and may result in criminal
prosecution.

By continuing, you acknowledge that you have read and agree to comply
with the organization's security policies.
***************************************************************************
```

#### Fail2ban Configuration for SSH
```bash
# /etc/fail2ban/jail.d/sshd.conf
[sshd]
enabled = true
port = 2222
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
findtime = 600
action = iptables[name=SSH, port=2222, protocol=tcp]
         sendmail-whois[name=SSH, dest=admin@example.com]
```

### Advanced SSH Authentication

#### Multi-Factor Authentication with Google Authenticator
```bash
# Install Google Authenticator PAM module
sudo apt install libpam-google-authenticator

# Configure PAM for SSH
# /etc/pam.d/sshd
auth required pam_google_authenticator.so nullok
auth required pam_permit.so

# Update sshd_config
AuthenticationMethods publickey,keyboard-interactive
ChallengeResponseAuthentication yes

# User setup
google-authenticator
# Follow prompts to set up TOTP
```

#### Host-Based Authentication
```bash
# Enable host-based authentication in sshd_config
HostbasedAuthentication yes
IgnoreUserKnownHosts no
IgnoreRhosts yes

# Configure known hosts
# /etc/ssh/ssh_known_hosts
server1.example.com ssh-rsa AAAAB3NzaC1yc2EAAAA...
server2.example.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA...

# Configure equivalent hosts
# /etc/ssh/shosts.equiv
server1.example.com
server2.example.com admin
```

### SSH Key Management at Scale

#### SSH Key Generation Script
```bash
#!/bin/bash
# generate-ssh-keys.sh - Enterprise SSH key generation

KEY_TYPE="ed25519"
KEY_SIZE="4096"  # For RSA keys
KEY_DIR="/etc/ssh/keys"
USERS_FILE="/etc/ssh/authorized_users"

generate_user_key() {
    local username="$1"
    local key_file="$KEY_DIR/$username"
    
    echo "Generating SSH key for user: $username"
    
    # Create key directory
    mkdir -p "$KEY_DIR"
    
    # Generate key based on type
    case "$KEY_TYPE" in
        "ed25519")
            ssh-keygen -t ed25519 -f "$key_file" -C "$username@$(hostname)" -N ""
            ;;
        "rsa")
            ssh-keygen -t rsa -b "$KEY_SIZE" -f "$key_file" -C "$username@$(hostname)" -N ""
            ;;
        "ecdsa")
            ssh-keygen -t ecdsa -b 521 -f "$key_file" -C "$username@$(hostname)" -N ""
            ;;
    esac
    
    # Set proper permissions
    chmod 600 "$key_file"
    chmod 644 "$key_file.pub"
    chown "$username:$username" "$key_file"*
    
    echo "Key generated: $key_file"
    echo "Public key: $(cat $key_file.pub)"
}

# Batch key generation
while IFS= read -r username; do
    [[ -n "$username" && ! "$username" =~ ^# ]] && generate_user_key "$username"
done < "$USERS_FILE"
```

#### Centralized Key Management Script
```bash
#!/bin/bash
# sync-ssh-keys.sh - Centralized SSH key deployment

CENTRAL_KEY_SERVER="keys.example.com"
KEY_SYNC_USER="keysync"
LOCAL_KEY_DIR="/home"
LOG_FILE="/var/log/ssh-key-sync.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

sync_user_keys() {
    local username="$1"
    local user_home="/home/$username"
    local ssh_dir="$user_home/.ssh"
    
    if [[ ! -d "$user_home" ]]; then
        log "User home directory not found: $user_home"
        return 1
    fi
    
    # Create .ssh directory if it doesn't exist
    if [[ ! -d "$ssh_dir" ]]; then
        mkdir -p "$ssh_dir"
        chown "$username:$username" "$ssh_dir"
        chmod 700 "$ssh_dir"
    fi
    
    # Download authorized_keys from central server
    log "Syncing keys for user: $username"
    if scp "$KEY_SYNC_USER@$CENTRAL_KEY_SERVER:/keys/$username/authorized_keys" \
           "$ssh_dir/authorized_keys" 2>/dev/null; then
        chown "$username:$username" "$ssh_dir/authorized_keys"
        chmod 600 "$ssh_dir/authorized_keys"
        log "Successfully synced keys for $username"
    else
        log "Failed to sync keys for $username"
    fi
}

# Sync keys for all users
for user_dir in /home/*; do
    username=$(basename "$user_dir")
    if [[ -d "$user_dir" && "$username" != "lost+found" ]]; then
        sync_user_keys "$username"
    fi
done
```

### SSH Certificate Authority

#### Setting up SSH CA
```bash
# Generate CA key pair
ssh-keygen -t ed25519 -f /etc/ssh/ca/ssh_ca -C "SSH-CA-$(hostname)"

# Create user certificate
ssh-keygen -s /etc/ssh/ca/ssh_ca -I "user-john" -n john -V +52w ~/.ssh/id_ed25519.pub

# Create host certificate
ssh-keygen -s /etc/ssh/ca/ssh_ca -I "host-server1" -h -n server1.example.com,server1,192.168.1.100 -V +52w /etc/ssh/ssh_host_ed25519_key.pub

# Configure sshd to trust CA
# /etc/ssh/sshd_config
TrustedUserCAKeys /etc/ssh/ca/ssh_ca.pub
HostCertificate /etc/ssh/ssh_host_ed25519_key-cert.pub

# Configure client to trust CA
# ~/.ssh/known_hosts or /etc/ssh/ssh_known_hosts
@cert-authority *.example.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA...
```

#### Certificate Management Script
```bash
#!/bin/bash
# ssh-cert-manager.sh - SSH Certificate management

CA_KEY="/etc/ssh/ca/ssh_ca"
CA_PUB="/etc/ssh/ca/ssh_ca.pub"
CERT_DIR="/etc/ssh/certificates"
VALIDITY_PERIOD="+52w"

create_user_cert() {
    local username="$1"
    local public_key="$2"
    local principals="$3"
    local cert_id="user-$username-$(date +%Y%m%d)"
    
    echo "Creating user certificate for: $username"
    
    # Create certificate
    ssh-keygen -s "$CA_KEY" \
        -I "$cert_id" \
        -n "$principals" \
        -V "$VALIDITY_PERIOD" \
        "$public_key"
    
    echo "Certificate created: ${public_key}-cert.pub"
    
    # Log certificate creation
    echo "$(date): Created user certificate for $username (ID: $cert_id)" >> /var/log/ssh-certs.log
}

create_host_cert() {
    local hostname="$1"
    local host_key="$2"
    local principals="$3"
    local cert_id="host-$hostname-$(date +%Y%m%d)"
    
    echo "Creating host certificate for: $hostname"
    
    # Create certificate
    ssh-keygen -s "$CA_KEY" \
        -I "$cert_id" \
        -h \
        -n "$principals" \
        -V "$VALIDITY_PERIOD" \
        "$host_key"
    
    echo "Certificate created: ${host_key}-cert.pub"
    
    # Log certificate creation
    echo "$(date): Created host certificate for $hostname (ID: $cert_id)" >> /var/log/ssh-certs.log
}

revoke_certificate() {
    local cert_serial="$1"
    local revocation_list="/etc/ssh/ca/revoked_keys"
    
    echo "Revoking certificate with serial: $cert_serial"
    
    # Add to revocation list
    ssh-keygen -k -f "$revocation_list" -s "$CA_KEY" "$cert_serial"
    
    # Update sshd_config to use revocation list
    # RevokedKeys /etc/ssh/ca/revoked_keys
    
    systemctl reload sshd
}

# Example usage
# create_user_cert "john" "/tmp/john_id_ed25519.pub" "john,admin"
# create_host_cert "server1" "/etc/ssh/ssh_host_ed25519_key.pub" "server1.example.com,server1,192.168.1.100"
```

### SSH Tunneling and Port Forwarding

#### SSH Tunnel Examples
```bash
# Local port forwarding (access remote service locally)
ssh -L 8080:localhost:80 user@remote-server

# Remote port forwarding (expose local service remotely)
ssh -R 9090:localhost:3000 user@remote-server

# Dynamic port forwarding (SOCKS proxy)
ssh -D 1080 user@remote-server

# X11 forwarding
ssh -X user@remote-server

# SSH jump host / ProxyCommand
ssh -J jump-host.example.com user@internal-server

# Persistent tunnel with autossh
autossh -M 20000 -L 8080:localhost:80 user@remote-server
```

#### SSH Bastion Host Configuration
```bash
# /etc/ssh/sshd_config - Bastion host settings
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowTcpForwarding yes
GatewayPorts no
X11Forwarding no
Banner /etc/ssh/bastion-banner

# Restrict users to specific actions
Match Group bastion-users
    AllowTcpForwarding yes
    AllowStreamLocalForwarding no
    PermitTunnel no
    X11Forwarding no
    ForceCommand echo 'This is a bastion host. Use it to connect to internal servers only.'

# Client configuration for bastion usage
# ~/.ssh/config
Host internal-*
    ProxyJump bastion.example.com
    User admin

Host bastion.example.com
    User bastion-user
    IdentityFile ~/.ssh/bastion_key
```

### SSH Monitoring and Auditing

#### SSH Log Analysis Script
```bash
#!/bin/bash
# ssh-log-analyzer.sh - SSH connection analysis

LOG_FILE="/var/log/auth.log"
REPORT_FILE="/var/log/ssh-report-$(date +%Y%m%d).txt"

generate_ssh_report() {
    echo "SSH Activity Report - $(date)" > "$REPORT_FILE"
    echo "=========================================" >> "$REPORT_FILE"
    echo >> "$REPORT_FILE"
    
    # Successful logins
    echo "Successful SSH Logins:" >> "$REPORT_FILE"
    grep "Accepted" "$LOG_FILE" | \
        awk '{print $1, $2, $3, $9, $11}' | \
        sort | uniq -c | sort -nr >> "$REPORT_FILE"
    echo >> "$REPORT_FILE"
    
    # Failed login attempts
    echo "Failed SSH Login Attempts:" >> "$REPORT_FILE"
    grep "Failed password" "$LOG_FILE" | \
        awk '{print $1, $2, $3, $9, $11}' | \
        sort | uniq -c | sort -nr >> "$REPORT_FILE"
    echo >> "$REPORT_FILE"
    
    # Top source IPs
    echo "Top Source IP Addresses:" >> "$REPORT_FILE"
    grep -E "(Accepted|Failed)" "$LOG_FILE" | \
        awk '{print $NF}' | \
        sort | uniq -c | sort -nr | head -20 >> "$REPORT_FILE"
    echo >> "$REPORT_FILE"
    
    # Connection duration analysis
    echo "SSH Session Analysis:" >> "$REPORT_FILE"
    grep "session opened\|session closed" "$LOG_FILE" | \
        awk '/opened/ {start[$7] = $1 " " $2 " " $3} 
             /closed/ {if (start[$7]) print "User:", $7, "Duration:", $1 " " $2 " " $3 " - " start[$7]; delete start[$7]}' >> "$REPORT_FILE"
    
    echo "Report generated: $REPORT_FILE"
}

# Real-time SSH monitoring
monitor_ssh_realtime() {
    echo "Monitoring SSH connections in real-time..."
    tail -f "$LOG_FILE" | while read line; do
        if echo "$line" | grep -q "Accepted\|Failed"; then
            timestamp=$(echo "$line" | awk '{print $1, $2, $3}')
            action=$(echo "$line" | grep -o "Accepted\|Failed")
            user=$(echo "$line" | awk '{print $9}')
            ip=$(echo "$line" | awk '{print $NF}')
            
            echo "[$timestamp] $action login for user '$user' from $ip"
            
            # Alert on suspicious activity
            if [[ "$action" == "Failed" ]]; then
                failed_count=$(grep "Failed password.*$ip" "$LOG_FILE" | wc -l)
                if [[ $failed_count -gt 5 ]]; then
                    echo "ALERT: Multiple failed attempts from $ip"
                    # Send notification
                    echo "Multiple SSH failed attempts from $ip" | \
                        mail -s "SSH Security Alert" admin@example.com
                fi
            fi
        fi
    done
}

generate_ssh_report
```

#### SSH Session Recording with asciinema
```bash
# Install asciinema
sudo apt install asciinema

# Force session recording for specific users
# /etc/ssh/sshd_config
Match User audit-user
    ForceCommand /usr/bin/asciinema rec --title "SSH Session $(date)" /var/log/ssh-sessions/session-$(date +%Y%m%d-%H%M%S)-$USER.cast

# Create recording directory
sudo mkdir -p /var/log/ssh-sessions
sudo chmod 755 /var/log/ssh-sessions
```

## SSH Security Best Practices

| Category | Best Practice |
|----------|---------------|
| Authentication | Use key-based auth, disable passwords |
| Protocol | Use SSH v2 only, strong ciphers |
| Access Control | Restrict users/groups, change default port |
| Monitoring | Log all connections, monitor for anomalies |
| Key Management | Regular key rotation, centralized management |
| Network | Use VPN, bastion hosts for sensitive access |
| Compliance | Document configurations, regular audits |

## SSH Troubleshooting

### Common SSH Issues
```bash
# Debug SSH connection
ssh -vv user@server

# Test SSH configuration
sudo sshd -t

# Check SSH service status
systemctl status sshd

# View SSH logs
journalctl -u sshd -f

# Test key authentication
ssh-add -l
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server

# Check file permissions
ls -la ~/.ssh/
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_*
chmod 644 ~/.ssh/*.pub
```

### SSH Performance Optimization
```bash
# Client-side optimizations
# ~/.ssh/config
Host *
    Compression yes
    ServerAliveInterval 60
    ServerAliveCountMax 3
    ControlMaster auto
    ControlPath ~/.ssh/master-%r@%h:%p
    ControlPersist 600

# Server-side optimizations
# /etc/ssh/sshd_config
Compression delayed
UseDNS no
GSSAPIAuthentication no
```

## Lab Exercises
1. Implement comprehensive SSH hardening
2. Set up SSH Certificate Authority
3. Configure SSH bastion host infrastructure
4. Implement SSH monitoring and alerting
5. Create automated SSH key management system

## Next Steps
With OpenSSH best practices mastered, you're ready to explore Proxmox Infrastructure Automation in Module 14, where you'll learn to automate infrastructure deployment and management using modern DevOps tools and practices.
