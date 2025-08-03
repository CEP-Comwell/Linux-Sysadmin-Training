# Module 13: OpenSSH Best Practices

## Overview
Securing and scaling SSH access through robust configuration, key management, and auditing strategies. This module focuses on enterprise-grade SSH security implementation including modern cryptographic algorithms, fine-grained access controls, and comprehensive session auditing.

**Key Points:**
- Key management: ED25519 vs. RSA, secure key storage, and agent forwarding
- Hardened sshd_config: Protocol 2 only, disable root login, rate limiting, MaxAuthTries
- Authorized_keys options: from=, command=, environment=, no-pty, no-X11-forwarding
- Bastion hosts and proxying: ProxyJump, ProxyCommand, bastion server architecture
- Multi-factor authentication: OTP (Google Authenticator), hardware tokens (YubiKey)
- Session logging and auditing: custom log formats, auditd integration, SSH jump logging

## Learning Objectives
By the end of this module, you will be able to:
1. Generate strong SSH key pairs (ED25519) and configure SSH agent forwarding
2. Harden the SSH server by tuning sshd_config parameters and enforcing Protocol 2
3. Implement fine-grained access controls using authorized_keys options
4. Design and deploy a bastion host using ProxyJump for secure access
5. Integrate multi-factor authentication for SSH logins with OTP or hardware tokens
6. Audit SSH sessions through enhanced logging and detect anomalous behavior
7. Rotate, revoke, and manage SSH host and user keys in a scalable manner

## Topics

### 13.1 Modern SSH Key Management and Agent Forwarding
- ED25519 vs. RSA key comparison and selection criteria
- Strong SSH key pair generation and storage practices
- SSH agent configuration and secure agent forwarding
- Key lifecycle management and rotation strategies
- Secure key distribution and centralized management

### 13.2 Hardened SSH Server Configuration
- Protocol 2 enforcement and legacy protocol removal
- Root login restrictions and privilege escalation prevention
- Rate limiting, MaxAuthTries, and brute force protection
- Connection limits and resource management
- Security-focused sshd_config parameter tuning

### 13.3 Fine-grained Access Control with Authorized Keys
- Advanced authorized_keys options and restrictions
- Source IP filtering with from= directive
- Command forcing and environment variable injection
- PTY and X11 forwarding restrictions
- Time-based and conditional access controls

### 13.4 Bastion Host Architecture and SSH Proxying
- ProxyJump configuration and chained connections
- ProxyCommand customization and advanced routing
- Bastion server design and security considerations
- SSH gateway patterns and network segmentation
- Jump host logging and audit trail maintenance

### 13.5 Multi-Factor Authentication Integration
- OTP implementation with Google Authenticator
- Hardware token integration (YubiKey, FIDO2)
- PAM module configuration for MFA
- Certificate-based authentication workflows
- Backup authentication methods and recovery procedures

### 13.6 Comprehensive SSH Session Auditing
- Enhanced logging configuration and custom formats
- Auditd integration for system-level tracking
- SSH jump host logging and connection chains
- Session recording and playback capabilities
- Anomaly detection and behavioral analysis

### 13.7 Scalable SSH Key and Host Management
- Automated key rotation and lifecycle management
- Host key verification and trust management
- Certificate authority implementation for SSH
- Key revocation and emergency procedures
- Enterprise-scale key distribution systems

### 13.6 Monitoring and Auditing
- SSH logging and log analysis
- Connection monitoring and alerting
- Session recording and playback
- Compliance reporting and auditing
- Intrusion detection for SSH

## Practical Examples

### Modern SSH Key Management and Agent Forwarding

#### ED25519 vs. RSA Key Comparison and Generation
```bash
# ED25519 Key Generation (Recommended - Modern, Fast, Secure)
# Advantages: Small key size, fast generation, quantum-resistant design
ssh-keygen -t ed25519 -C "user@$(hostname)-$(date +%Y%m%d)" -f ~/.ssh/id_ed25519

# RSA Key Generation (Legacy Support)
# Use 4096-bit minimum for security (3072-bit acceptable, 2048-bit deprecated)
ssh-keygen -t rsa -b 4096 -C "user@$(hostname)-$(date +%Y%m%d)" -f ~/.ssh/id_rsa

# ECDSA Key Generation (Alternative)
ssh-keygen -t ecdsa -b 521 -C "user@$(hostname)-$(date +%Y%m%d)" -f ~/.ssh/id_ecdsa

# Key Comparison Script
#!/bin/bash
# compare-ssh-keys.sh - Analyze SSH key characteristics

compare_key_types() {
    echo "SSH Key Type Comparison"
    echo "======================="
    
    for key_type in ed25519 rsa ecdsa; do
        case $key_type in
            ed25519)
                echo "ED25519:"
                echo "  - Key Size: 32 bytes (256-bit)"
                echo "  - Public Key Size: ~68 characters"
                echo "  - Security: Excellent (modern, quantum-resistant design)"
                echo "  - Performance: Very fast"
                echo "  - Compatibility: OpenSSH 6.5+ (2014)"
                ;;
            rsa)
                echo "RSA 4096:"
                echo "  - Key Size: 4096 bits"
                echo "  - Public Key Size: ~724 characters"
                echo "  - Security: Good (with 4096-bit minimum)"
                echo "  - Performance: Slower than ED25519"
                echo "  - Compatibility: Universal"
                ;;
            ecdsa)
                echo "ECDSA P-521:"
                echo "  - Key Size: 521 bits"
                echo "  - Public Key Size: ~178 characters"
                echo "  - Security: Good"
                echo "  - Performance: Fast"
                echo "  - Compatibility: OpenSSH 5.7+ (2011)"
                ;;
        esac
        echo
    done
}

compare_key_types
```

#### Secure SSH Agent Configuration and Forwarding
```bash
# SSH Agent Security Configuration
# ~/.ssh/config
Host *
    # Enable agent forwarding selectively
    ForwardAgent no
    
# Enable agent forwarding only for trusted hosts
Host bastion.example.com
    ForwardAgent yes
    # Limit agent forwarding duration
    AddKeysToAgent confirm
    IdentitiesOnly yes

Host internal-*.example.com
    ProxyJump bastion.example.com
    ForwardAgent no  # Disable on internal hosts for security

# Advanced SSH Agent Management Script
#!/bin/bash
# ssh-agent-manager.sh - Secure SSH agent management

AGENT_TIMEOUT=3600  # 1 hour timeout
KEY_DIR="$HOME/.ssh"
AGENT_ENV="$HOME/.ssh/agent-env"

start_ssh_agent() {
    echo "Starting SSH agent with timeout: $AGENT_TIMEOUT seconds"
    
    # Start agent with timeout
    ssh-agent -t "$AGENT_TIMEOUT" > "$AGENT_ENV"
    source "$AGENT_ENV"
    
    # Set restrictive permissions
    chmod 600 "$AGENT_ENV"
    
    echo "SSH Agent started (PID: $SSH_AGENT_PID)"
}

load_ssh_keys() {
    echo "Loading SSH keys with confirmation requirement..."
    
    # Load keys with confirmation (prevents silent key usage)
    ssh-add -c "$KEY_DIR/id_ed25519" 2>/dev/null && echo "Loaded: ED25519 key"
    ssh-add -c "$KEY_DIR/id_rsa" 2>/dev/null && echo "Loaded: RSA key"
    ssh-add -c "$KEY_DIR/id_ecdsa" 2>/dev/null && echo "Loaded: ECDSA key"
    
    # Display loaded keys
    echo "Currently loaded keys:"
    ssh-add -l
}

secure_agent_forwarding() {
    # Create a restricted agent for forwarding
    echo "Setting up secure agent forwarding..."
    
    # Use ssh-add with time limits for forwarded connections
    ssh-add -t 1800 "$KEY_DIR/id_ed25519"  # 30-minute timeout for forwarded key
    
    echo "Agent configured for secure forwarding (30-minute timeout)"
}

cleanup_agent() {
    echo "Cleaning up SSH agent..."
    ssh-add -D  # Remove all keys
    kill "$SSH_AGENT_PID" 2>/dev/null
    rm -f "$AGENT_ENV"
    echo "SSH agent cleaned up"
}

# Trap to cleanup on script exit
trap cleanup_agent EXIT

# Main execution
case "${1:-start}" in
    start)
        start_ssh_agent
        load_ssh_keys
        ;;
    forward)
        secure_agent_forwarding
        ;;
    cleanup)
        cleanup_agent
        ;;
    *)
        echo "Usage: $0 {start|forward|cleanup}"
        exit 1
        ;;
esac
```

#### Enterprise Key Distribution and Management
```bash
#!/bin/bash
# enterprise-key-manager.sh - Scalable SSH key management

KEY_SERVER="keys.internal.example.com"
KEY_SYNC_USER="keysync"
MASTER_KEY_DIR="/srv/ssh-keys"
CLIENT_KEY_DIR="$HOME/.ssh"
LOG_FILE="/var/log/ssh-key-mgmt.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

generate_user_keys() {
    local username="$1"
    local key_type="${2:-ed25519}"
    local user_key_dir="$MASTER_KEY_DIR/users/$username"
    
    log "Generating $key_type key for user: $username"
    
    mkdir -p "$user_key_dir"
    
    # Generate key with enterprise naming convention
    local key_file="$user_key_dir/id_${key_type}_$(date +%Y%m%d)"
    ssh-keygen -t "$key_type" -f "$key_file" \
        -C "$username@enterprise-$(date +%Y%m%d)" -N ""
    
    # Set proper permissions
    chmod 600 "$key_file"
    chmod 644 "$key_file.pub"
    
    # Create authorized_keys entry with restrictions
    cat > "$user_key_dir/authorized_keys" << EOF
# Generated: $(date)
# User: $username
# Key Type: $key_type
# Restrictions: Source IP, command forcing disabled by default
$(cat "$key_file.pub")
EOF
    
    log "Key generated: $key_file"
    return 0
}

distribute_user_keys() {
    local username="$1"
    local target_hosts="${2:-all}"
    local user_key_dir="$MASTER_KEY_DIR/users/$username"
    
    if [[ ! -d "$user_key_dir" ]]; then
        log "ERROR: No keys found for user $username"
        return 1
    fi
    
    log "Distributing keys for user: $username"
    
    # Get list of target hosts
    local hosts
    if [[ "$target_hosts" == "all" ]]; then
        hosts=$(cat "$MASTER_KEY_DIR/host-list.txt")
    else
        hosts="$target_hosts"
    fi
    
    for host in $hosts; do
        log "Deploying keys to host: $host"
        
        # Deploy authorized_keys
        if scp "$user_key_dir/authorized_keys" \
           "$KEY_SYNC_USER@$host:/tmp/authorized_keys_$username"; then
            
            # Install keys remotely
            ssh "$KEY_SYNC_USER@$host" "
                sudo mkdir -p /home/$username/.ssh
                sudo cp /tmp/authorized_keys_$username /home/$username/.ssh/authorized_keys
                sudo chown -R $username:$username /home/$username/.ssh
                sudo chmod 700 /home/$username/.ssh
                sudo chmod 600 /home/$username/.ssh/authorized_keys
                rm /tmp/authorized_keys_$username
            "
            
            log "Successfully deployed keys for $username to $host"
        else
            log "ERROR: Failed to deploy keys for $username to $host"
        fi
    done
}

rotate_user_keys() {
    local username="$1"
    local key_type="${2:-ed25519}"
    
    log "Rotating keys for user: $username"
    
    # Backup old keys
    local backup_dir="$MASTER_KEY_DIR/users/$username/backup-$(date +%Y%m%d-%H%M%S)"
    mkdir -p "$backup_dir"
    
    find "$MASTER_KEY_DIR/users/$username" -name "id_*" -not -path "*/backup-*" \
        -exec mv {} "$backup_dir/" \;
    
    # Generate new keys
    generate_user_keys "$username" "$key_type"
    
    # Distribute new keys
    distribute_user_keys "$username"
    
    log "Key rotation completed for user: $username"
}

# Usage examples:
# generate_user_keys "alice" "ed25519"
# distribute_user_keys "alice" "server1.example.com server2.example.com"
# rotate_user_keys "alice" "ed25519"
```

### Hardened SSH Server Configuration with Protocol 2 Enforcement

#### Enterprise-Grade sshd_config Configuration
```bash
# /etc/ssh/sshd_config - Production hardened configuration

# ============================================================================
# PROTOCOL AND ENCRYPTION SETTINGS
# ============================================================================

# Enforce SSH Protocol 2 only (SSH-1 is deprecated and insecure)
Protocol 2

# Change default port to reduce automated attacks
Port 2022

# Address family (inet = IPv4, inet6 = IPv6, any = both)
AddressFamily inet

# ============================================================================
# HOST KEY CONFIGURATION
# ============================================================================

# Use only modern, secure host key algorithms
HostKey /etc/ssh/ssh_host_ed25519_key
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key

# Remove weak host keys if they exist
# rm /etc/ssh/ssh_host_dsa_key*

# ============================================================================
# CRYPTOGRAPHIC ALGORITHMS
# ============================================================================

# Strong ciphers only (AES-GCM preferred for performance and security)
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

# Secure MACs with Encrypt-then-MAC (ETM) variants
MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha2-512

# Modern key exchange algorithms
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp521,ecdh-sha2-nistp384,ecdh-sha2-nistp256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512

# ============================================================================
# AUTHENTICATION CONFIGURATION
# ============================================================================

# Disable root login completely
PermitRootLogin no

# Disable password authentication (key-based only)
PasswordAuthentication no
PermitEmptyPasswords no

# Enable public key authentication
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys .ssh/authorized_keys2

# PAM configuration
UsePAM yes
ChallengeResponseAuthentication no

# Disable legacy authentication methods
RhostsRSAAuthentication no
HostbasedAuthentication no
IgnoreUserKnownHosts yes
IgnoreRhosts yes

# ============================================================================
# RATE LIMITING AND BRUTE FORCE PROTECTION
# ============================================================================

# Maximum authentication attempts per connection
MaxAuthTries 3

# Maximum concurrent sessions per connection
MaxSessions 2

# Connection rate limiting (start:rate:full)
MaxStartups 3:30:10

# Login grace time (time to authenticate after connection)
LoginGraceTime 30

# ============================================================================
# ACCESS CONTROL
# ============================================================================

# Restrict access to specific users and groups
AllowUsers sysadmin deployuser
AllowGroups ssh-users administrators

# Explicitly deny dangerous users/groups
DenyUsers root guest nobody
DenyGroups wheel root

# ============================================================================
# NETWORK AND CONNECTION SETTINGS
# ============================================================================

# Client alive settings (detect dead connections)
ClientAliveInterval 300
ClientAliveCountMax 2

# Disable TCP keep alive (use SSH keep alive instead)
TCPKeepAlive no

# Disable compression (can be exploited)
Compression no

# ============================================================================
# FORWARDING AND TUNNELING RESTRICTIONS
# ============================================================================

# Disable X11 forwarding (security risk)
X11Forwarding no
X11DisplayOffset 10
X11UseLocalhost yes

# Disable TCP forwarding by default
AllowTcpForwarding no

# Disable stream local forwarding
AllowStreamLocalForwarding no

# Disable gateway ports
GatewayPorts no

# Disable agent forwarding by default
AllowAgentForwarding no

# ============================================================================
# LOGGING AND AUDITING
# ============================================================================

# Enhanced logging
SyslogFacility AUTH
LogLevel VERBOSE

# Print login information
PrintMotd yes
PrintLastLog yes

# ============================================================================
# LEGAL AND COMPLIANCE
# ============================================================================

# Display legal banner
Banner /etc/ssh/legal-banner

# ============================================================================
# USER-SPECIFIC OVERRIDES
# ============================================================================

# Bastion host users (allow forwarding)
Match Group bastion-users
    AllowTcpForwarding yes
    AllowAgentForwarding yes
    X11Forwarding no
    Banner /etc/ssh/bastion-banner
    MaxSessions 5

# Service accounts (restricted)
Match User deployuser
    AllowTcpForwarding no
    AllowAgentForwarding no
    X11Forwarding no
    ForceCommand /usr/local/bin/deployment-shell
    MaxSessions 1

# SFTP-only users
Match Group sftp-only
    ChrootDirectory /srv/sftp/%u
    ForceCommand internal-sftp
    AllowTcpForwarding no
    AllowAgentForwarding no
    X11Forwarding no
```

#### SSH Hardening Validation Script
```bash
#!/bin/bash
# ssh-hardening-validator.sh - Validate SSH security configuration

CONFIG_FILE="/etc/ssh/sshd_config"
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

check_setting() {
    local setting="$1"
    local expected="$2"
    local current
    
    # Extract current value from config
    current=$(grep -E "^${setting}\s+" "$CONFIG_FILE" | awk '{print $2}' | tail -1)
    
    if [[ "$current" == "$expected" ]]; then
        echo -e "${GREEN}✓${NC} $setting: $current"
        return 0
    else
        echo -e "${RED}✗${NC} $setting: $current (expected: $expected)"
        return 1
    fi
}

check_protocol_2() {
    echo "Checking SSH Protocol version..."
    if grep -q "^Protocol 2" "$CONFIG_FILE"; then
        echo -e "${GREEN}✓${NC} SSH Protocol 2 enforced"
    else
        echo -e "${RED}✗${NC} SSH Protocol not set to 2 only"
    fi
}

check_weak_algorithms() {
    echo "Checking for weak cryptographic algorithms..."
    
    # Check for weak ciphers
    if grep -E "^Ciphers.*3des|arcfour|blowfish" "$CONFIG_FILE"; then
        echo -e "${RED}✗${NC} Weak ciphers detected"
    else
        echo -e "${GREEN}✓${NC} No weak ciphers found"
    fi
    
    # Check for weak MACs
    if grep -E "^MACs.*md5|sha1[^-]" "$CONFIG_FILE"; then
        echo -e "${RED}✗${NC} Weak MACs detected"
    else
        echo -e "${GREEN}✓${NC} No weak MACs found"
    fi
}

main() {
    echo "SSH Security Configuration Validator"
    echo "====================================="
    echo
    
    # Check critical security settings
    check_protocol_2
    check_setting "PermitRootLogin" "no"
    check_setting "PasswordAuthentication" "no"
    check_setting "PermitEmptyPasswords" "no"
    check_setting "MaxAuthTries" "3"
    check_setting "X11Forwarding" "no"
    check_setting "AllowTcpForwarding" "no"
    
    echo
    check_weak_algorithms
    
    echo
    echo "Testing SSH configuration syntax..."
    if sshd -t 2>/dev/null; then
        echo -e "${GREEN}✓${NC} SSH configuration syntax is valid"
    else
        echo -e "${RED}✗${NC} SSH configuration has syntax errors"
        sshd -t
    fi
}

main
```

#### Rate Limiting and Brute Force Protection
```bash
# Advanced Fail2ban configuration for SSH
# /etc/fail2ban/jail.d/ssh-hardened.conf

[ssh-iptables]
enabled = true
port = 2022
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
findtime = 600
bantime = 7200
action = iptables-multiport[name=SSH, port="2022", protocol=tcp]
         sendmail-buffered[name=SSH, dest=security@example.com]

# Aggressive protection against SSH scanning
[ssh-aggressive]
enabled = true
port = 2022
filter = sshd-aggressive
logpath = /var/log/auth.log
maxretry = 1
findtime = 86400  # 24 hours
bantime = 604800   # 1 week
action = iptables-multiport[name=SSH-AGG, port="2022", protocol=tcp]

# Custom filter for aggressive SSH protection
# /etc/fail2ban/filter.d/sshd-aggressive.conf
[Definition]
failregex = ^%(__prefix_line)s(?:error: PAM: )?[aA]uthentication (?:failure|error|failed) for .* from <HOST>( via \S+)?\s*$
            ^%(__prefix_line)s(?:error: )?Received disconnect from <HOST>: 11: .+$
            ^%(__prefix_line)sReceived disconnect from <HOST>: 3: .+: Auth fail$
            ^%(__prefix_line)sFailed (?:password|publickey) for .* from <HOST>(?: port \d*)?(?: ssh\d*)?$
            ^%(__prefix_line)sROOT LOGIN REFUSED.* FROM <HOST>$
            ^%(__prefix_line)s[iI](?:llegal|nvalid) user .* from <HOST>$
            ^%(__prefix_line)sUser .+ from <HOST> not allowed because not listed in AllowUsers$

ignoreregex =

# IPTables rate limiting script
#!/bin/bash
# ssh-rate-limit.sh - Implement connection rate limiting

setup_rate_limiting() {
    echo "Setting up SSH rate limiting..."
    
    # Allow established connections
    iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    
    # Rate limit new SSH connections
    iptables -A INPUT -p tcp --dport 2022 -m state --state NEW -m recent --set --name SSH
    iptables -A INPUT -p tcp --dport 2022 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j DROP
    
    # Log dropped connections
    iptables -A INPUT -p tcp --dport 2022 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j LOG --log-prefix "SSH Rate Limit: "
    
    # Allow remaining SSH connections
    iptables -A INPUT -p tcp --dport 2022 -j ACCEPT
    
    echo "SSH rate limiting configured"
}

setup_rate_limiting
```

### Fine-grained Access Control with Authorized Keys Options

#### Advanced authorized_keys Restrictions and Options
```bash
# ~/.ssh/authorized_keys - Enterprise access control examples

# Basic unrestricted key (NOT recommended for production)
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... user@workstation

# SOURCE IP RESTRICTION - Limit access from specific networks
from="192.168.1.0/24,10.0.0.0/8" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... admin@internal

# COMMAND FORCING - Force execution of specific command only
command="/usr/local/bin/backup-script.sh" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... backup@server

# ENVIRONMENT VARIABLES - Set custom environment for this key
environment="PATH=/usr/local/bin:/usr/bin:/bin",environment="BACKUP_DIR=/srv/backups" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... backup@server

# DISABLE PTY ALLOCATION - Prevent interactive shell (for service accounts)
no-pty ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... service@automation

# DISABLE X11 FORWARDING - Block GUI application forwarding
no-X11-forwarding ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... user@headless-server

# DISABLE PORT FORWARDING - Block all tunneling capabilities
no-port-forwarding ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... restricted@server

# DISABLE AGENT FORWARDING - Prevent SSH agent forwarding
no-agent-forwarding ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... user@untrusted

# COMBINE MULTIPLE RESTRICTIONS - Production service account example
command="/opt/deploy/deploy.sh",no-pty,no-X11-forwarding,no-port-forwarding,from="10.0.0.0/8" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... deploy@ci-server

# TIME-BASED ACCESS - Using expiry dates (requires OpenSSH 8.2+)
expiry-time="20241231235959" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... contractor@project

# AUDIT LOGGING - Custom principals for certificate-based auth
cert-authority,principals="admin,emergency" ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAB... ca@organization
```

#### Authorized Keys Management Script
```bash
#!/bin/bash
# authorized-keys-manager.sh - Enterprise authorized_keys management

USERS_DIR="/home"
TEMPLATE_DIR="/etc/ssh/key-templates"
LOG_FILE="/var/log/ssh-key-management.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

create_restricted_key_entry() {
    local username="$1"
    local public_key="$2"
    local restrictions="$3"
    local comment="$4"
    
    local user_home="$USERS_DIR/$username"
    local auth_keys="$user_home/.ssh/authorized_keys"
    
    log "Creating restricted key entry for user: $username"
    
    # Ensure .ssh directory exists
    if [[ ! -d "$user_home/.ssh" ]]; then
        mkdir -p "$user_home/.ssh"
        chown "$username:$username" "$user_home/.ssh"
        chmod 700 "$user_home/.ssh"
    fi
    
    # Create authorized_keys entry with restrictions
    cat >> "$auth_keys" << EOF

# Added: $(date)
# User: $username
# Comment: $comment
# Restrictions: $restrictions
$restrictions $public_key $comment
EOF
    
    # Set proper permissions
    chown "$username:$username" "$auth_keys"
    chmod 600 "$auth_keys"
    
    log "Restricted key entry created for $username with restrictions: $restrictions"
}

create_service_account_key() {
    local service_name="$1"
    local allowed_command="$2"
    local source_networks="$3"
    local public_key="$4"
    
    local restrictions="command=\"$allowed_command\",no-pty,no-X11-forwarding,no-port-forwarding,no-agent-forwarding"
    
    if [[ -n "$source_networks" ]]; then
        restrictions="from=\"$source_networks\",$restrictions"
    fi
    
    create_restricted_key_entry "$service_name" "$public_key" "$restrictions" "Service account for $service_name"
}

create_admin_key() {
    local username="$1"
    local source_networks="$2"
    local public_key="$3"
    
    local restrictions="from=\"$source_networks\""
    
    create_restricted_key_entry "$username" "$public_key" "$restrictions" "Administrative access from trusted networks"
}

create_backup_key() {
    local username="$1"
    local backup_script="$2"
    local public_key="$3"
    
    local restrictions="command=\"$backup_script\",no-pty,no-X11-forwarding,no-port-forwarding,no-agent-forwarding,environment=\"BACKUP_USER=$username\""
    
    create_restricted_key_entry "$username" "$public_key" "$restrictions" "Backup service account"
}

validate_authorized_keys() {
    local username="$1"
    local auth_keys="$USERS_DIR/$username/.ssh/authorized_keys"
    
    if [[ ! -f "$auth_keys" ]]; then
        log "No authorized_keys file found for user: $username"
        return 1
    fi
    
    log "Validating authorized_keys for user: $username"
    
    # Check file permissions
    local perms=$(stat -c %a "$auth_keys")
    if [[ "$perms" != "600" ]]; then
        log "WARNING: Incorrect permissions on $auth_keys: $perms (should be 600)"
        chmod 600 "$auth_keys"
    fi
    
    # Validate key format
    local line_num=1
    while IFS= read -r line; do
        if [[ -n "$line" && ! "$line" =~ ^[[:space:]]*# ]]; then
            if ! ssh-keygen -l -f /dev/stdin <<< "$line" >/dev/null 2>&1; then
                log "ERROR: Invalid key format at line $line_num in $auth_keys"
            fi
        fi
        ((line_num++))
    done < "$auth_keys"
    
    log "Validation completed for user: $username"
}

audit_key_usage() {
    local username="$1"
    local days="${2:-7}"
    
    log "Auditing SSH key usage for user: $username (last $days days)"
    
    # Search auth logs for this user
    grep -E "Accepted.*for $username" /var/log/auth.log* | \
        grep -E "$(date -d "$days days ago" '+%b %d')" | \
        while read -r logline; do
            echo "$logline" | awk '{
                print "Date: " $1 " " $2 " " $3
                print "User: " $9
                print "Source: " $11
                print "Method: " $6
                print "---"
            }'
        done
    
    log "Key usage audit completed for user: $username"
}

# Usage examples:
# create_service_account_key "backupuser" "/usr/local/bin/backup.sh" "10.0.0.0/8,192.168.1.0/24" "ssh-ed25519 AAAAC3..."
# create_admin_key "alice" "192.168.1.0/24" "ssh-ed25519 AAAAC3..."
# validate_authorized_keys "alice"
# audit_key_usage "alice" 30
```

#### Conditional Access Control Script
```bash
#!/bin/bash
# conditional-access.sh - Time and condition-based SSH access

ACCESS_RULES="/etc/ssh/access-rules.conf"
LOG_FILE="/var/log/ssh-conditional-access.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

check_time_based_access() {
    local username="$1"
    local current_hour=$(date +%H)
    local current_day=$(date +%u)  # 1=Monday, 7=Sunday
    
    log "Checking time-based access for user: $username"
    
    # Business hours: Monday-Friday, 8 AM to 6 PM
    if [[ "$current_day" -ge 1 && "$current_day" -le 5 ]] && \
       [[ "$current_hour" -ge 8 && "$current_hour" -le 18 ]]; then
        log "Access granted: Business hours"
        return 0
    fi
    
    # Check for emergency access override
    if [[ -f "/etc/ssh/emergency-access" ]]; then
        if grep -q "^$username$" "/etc/ssh/emergency-access"; then
            log "Access granted: Emergency override for $username"
            return 0
        fi
    fi
    
    log "Access denied: Outside business hours and no emergency override"
    return 1
}

check_network_based_access() {
    local username="$1"
    local source_ip="$2"
    
    log "Checking network-based access for user: $username from IP: $source_ip"
    
    # Define trusted networks
    local trusted_networks=(
        "192.168.1.0/24"    # Office network
        "10.0.0.0/8"        # VPN network
        "172.16.0.0/12"     # Management network
    )
    
    for network in "${trusted_networks[@]}"; do
        if check_ip_in_network "$source_ip" "$network"; then
            log "Access granted: IP $source_ip is in trusted network $network"
            return 0
        fi
    done
    
    log "Access denied: IP $source_ip is not in any trusted network"
    return 1
}

check_ip_in_network() {
    local ip="$1"
    local network="$2"
    
    # Simple network check using ipcalc
    if command -v ipcalc >/dev/null 2>&1; then
        ipcalc -c "$network" 2>/dev/null && \
        ipcalc -c "$ip" 2>/dev/null && \
        [[ $(ipcalc -n "$network" | grep -o '[0-9.]*') == $(ipcalc -n "$ip/$network" | grep -o '[0-9.]*') ]]
    else
        # Fallback to python if ipcalc not available
        python3 -c "
import ipaddress
import sys
try:
    net = ipaddress.IPv4Network('$network', strict=False)
    ip = ipaddress.IPv4Address('$ip')
    sys.exit(0 if ip in net else 1)
except:
    sys.exit(1)
" 2>/dev/null
    fi
}

generate_dynamic_authorized_keys() {
    local username="$1"
    local source_ip="${SSH_CLIENT%% *}"  # Extract IP from SSH_CLIENT
    local user_home="/home/$username"
    local static_keys="$user_home/.ssh/authorized_keys.static"
    local dynamic_keys="$user_home/.ssh/authorized_keys"
    
    log "Generating dynamic authorized_keys for $username from $source_ip"
    
    # Check access conditions
    if ! check_time_based_access "$username" || ! check_network_based_access "$username" "$source_ip"; then
        # Create empty authorized_keys (deny access)
        echo "# Access denied due to conditional access policy" > "$dynamic_keys"
        chmod 600 "$dynamic_keys"
        chown "$username:$username" "$dynamic_keys"
        log "Access denied: Dynamic key generation blocked"
        return 1
    fi
    
    # Copy static keys to dynamic keys with additional restrictions
    if [[ -f "$static_keys" ]]; then
        cp "$static_keys" "$dynamic_keys"
        
        # Add source IP restriction to all keys
        sed -i "s/^ssh-/from=\"$source_ip\" ssh-/" "$dynamic_keys"
        sed -i "s/^from=\"[^\"]*\"/from=\"$source_ip\"/" "$dynamic_keys"
        
        chmod 600 "$dynamic_keys"
        chown "$username:$username" "$dynamic_keys"
        
        log "Dynamic authorized_keys generated with IP restriction: $source_ip"
    else
        log "No static keys found for user: $username"
        return 1
    fi
}

# This script can be called from SSH forced commands or via cron
# Example usage in authorized_keys:
# command="/usr/local/bin/conditional-access.sh $USER && /bin/bash" ssh-ed25519 AAAAC3...
```

### Bastion Host Architecture and SSH Proxying

#### ProxyJump Configuration and Advanced Routing
```bash
# ~/.ssh/config - Client-side ProxyJump configuration

# Simple jump host configuration
Host internal-server
    HostName 10.0.1.100
    User admin
    ProxyJump bastion.example.com
    IdentityFile ~/.ssh/internal_key

# Multi-hop jump configuration
Host internal-db
    HostName 10.0.2.50
    User dbadmin
    ProxyJump bastion.example.com,gateway.internal.com
    IdentityFile ~/.ssh/db_key

# Conditional ProxyJump based on network
Host production-*
    ProxyJump bastion-prod.example.com
    User sysadmin
    IdentityFile ~/.ssh/prod_key
    ServerAliveInterval 60
    ServerAliveCountMax 3

Host staging-*
    ProxyJump bastion-staging.example.com
    User developer
    IdentityFile ~/.ssh/staging_key

# ProxyJump with custom port and options
Host secure-internal
    HostName 192.168.100.10
    User security
    Port 2022
    ProxyJump bastion.example.com:2222
    IdentityFile ~/.ssh/security_key
    UserKnownHostsFile ~/.ssh/known_hosts_internal
```

#### Advanced ProxyCommand Configuration
```bash
# ~/.ssh/config - Advanced ProxyCommand examples

# ProxyCommand with SSH
Host legacy-server
    HostName 172.16.1.100
    User oldadmin
    ProxyCommand ssh -W %h:%p bastion.example.com

# ProxyCommand with netcat through bastion
Host internal-service
    HostName 10.0.3.200
    Port 22
    ProxyCommand ssh bastion.example.com nc %h %p

# ProxyCommand with custom script for complex routing
Host complex-internal
    HostName 192.168.200.50
    ProxyCommand /usr/local/bin/ssh-proxy-router.sh %h %p

# Conditional ProxyCommand based on source network
Match host internal-* !exec "ip route get 8.8.8.8 | grep -q 'src 10\.'"
    ProxyCommand ssh -W %h:%p bastion.example.com

# SSH over HTTP proxy (corporate environments)
Host corporate-server
    HostName server.corp.example.com
    ProxyCommand corkscrew proxy.corp.com 8080 %h %p
```

#### Enterprise Bastion Host Configuration
```bash
# /etc/ssh/sshd_config - Bastion host specific configuration

# Bastion host identification
Banner /etc/ssh/bastion-banner

# Enhanced logging for bastion hosts
LogLevel VERBOSE
SyslogFacility LOCAL0

# Restricted capabilities for bastion users
Match Group bastion-users
    # Allow forwarding for jump functionality
    AllowTcpForwarding yes
    AllowStreamLocalForwarding no
    
    # Disable interactive features
    X11Forwarding no
    PermitTunnel no
    
    # Limit sessions
    MaxSessions 10
    
    # Force command to log connections
    ForceCommand /usr/local/bin/bastion-logger.sh

# Service account restrictions on bastion
Match User service-*
    AllowTcpForwarding local
    AllowStreamLocalForwarding no
    X11Forwarding no
    MaxSessions 3
    ClientAliveInterval 120
    ClientAliveCountMax 1

# Administrative access with full privileges
Match Group bastion-admins
    AllowTcpForwarding yes
    AllowStreamLocalForwarding yes
    X11Forwarding yes
    MaxSessions 5
```

#### Bastion Host Connection Logger
```bash
#!/bin/bash
# bastion-logger.sh - Log all bastion host connections

LOG_FILE="/var/log/bastion-connections.log"
ALERT_THRESHOLD=10  # Alert if more than 10 connections per minute

log_connection() {
    local user="$USER"
    local source_ip="${SSH_CLIENT%% *}"
    local ssh_command="$SSH_ORIGINAL_COMMAND"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    local session_id="$$"
    
    # Log connection details
    echo "[$timestamp] SESSION_START: User=$user Source=$source_ip SessionID=$session_id Command='$ssh_command'" >> "$LOG_FILE"
    
    # Check for connection flooding
    recent_connections=$(grep "$source_ip" "$LOG_FILE" | grep "$(date '+%Y-%m-%d %H:%M')" | wc -l)
    if [[ $recent_connections -gt $ALERT_THRESHOLD ]]; then
        echo "[$timestamp] ALERT: High connection rate from $source_ip ($recent_connections connections)" >> "$LOG_FILE"
        # Send alert to security team
        echo "High SSH connection rate detected from $source_ip" | \
            mail -s "Bastion Security Alert" security@example.com
    fi
    
    # Execute original command or provide shell
    if [[ -n "$ssh_command" ]]; then
        echo "[$timestamp] COMMAND_EXEC: User=$user Command='$ssh_command'" >> "$LOG_FILE"
        exec $ssh_command
    else
        echo "[$timestamp] SHELL_START: User=$user Interactive shell started" >> "$LOG_FILE"
        exec /bin/bash
    fi
}

# Trap to log session end
trap 'echo "[$(date "+%Y-%m-%d %H:%M:%S")] SESSION_END: User=$USER SessionID=$$" >> "$LOG_FILE"' EXIT

log_connection
```

#### Automated Bastion Host Deployment
```bash
#!/bin/bash
# deploy-bastion.sh - Automated bastion host setup

BASTION_USERS="alice bob charlie"
ADMIN_USERS="admin security"
INTERNAL_NETWORKS="10.0.0.0/8 172.16.0.0/12 192.168.0.0/16"

setup_bastion_host() {
    echo "Setting up bastion host..."
    
    # Create bastion user groups
    groupadd bastion-users
    groupadd bastion-admins
    
    # Create bastion users
    for user in $BASTION_USERS; do
        useradd -m -g bastion-users -s /bin/bash "$user"
        mkdir -p "/home/$user/.ssh"
        chmod 700 "/home/$user/.ssh"
        chown "$user:bastion-users" "/home/$user/.ssh"
    done
    
    # Create admin users
    for admin in $ADMIN_USERS; do
        useradd -m -g bastion-admins -s /bin/bash "$admin"
        usermod -aG sudo "$admin"
    done
    
    # Configure SSH for bastion functionality
    configure_bastion_ssh
    
    # Set up logging and monitoring
    setup_bastion_monitoring
    
    # Configure firewall rules
    configure_bastion_firewall
    
    echo "Bastion host setup completed"
}

configure_bastion_ssh() {
    echo "Configuring SSH for bastion functionality..."
    
    # Copy bastion-specific sshd_config
    cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
    
    # Update sshd_config with bastion settings
    cat >> /etc/ssh/sshd_config << EOF

# Bastion Host Configuration
Port 22
Port 2222  # Alternative port for admin access

# Enhanced logging for bastion
LogLevel VERBOSE
SyslogFacility LOCAL0

# Bastion user restrictions
Match Group bastion-users
    AllowTcpForwarding yes
    AllowStreamLocalForwarding no
    X11Forwarding no
    PermitTunnel no
    MaxSessions 10
    ForceCommand /usr/local/bin/bastion-logger.sh

# Admin access
Match Group bastion-admins
    AllowTcpForwarding yes
    X11Forwarding yes
    MaxSessions 5
EOF
    
    # Install bastion logger script
    cp bastion-logger.sh /usr/local/bin/
    chmod +x /usr/local/bin/bastion-logger.sh
    
    # Restart SSH service
    systemctl restart sshd
}

setup_bastion_monitoring() {
    echo "Setting up bastion monitoring..."
    
    # Configure rsyslog for bastion logs
    cat > /etc/rsyslog.d/30-bastion.conf << EOF
# Bastion host logging
local0.*    /var/log/bastion-connections.log
& stop
EOF
    
    # Restart rsyslog
    systemctl restart rsyslog
    
    # Set up log rotation
    cat > /etc/logrotate.d/bastion << EOF
/var/log/bastion-connections.log {
    daily
    missingok
    rotate 365
    compress
    delaycompress
    notifempty
    copytruncate
    postrotate
        /bin/kill -HUP \$(cat /var/run/rsyslogd.pid 2> /dev/null) 2> /dev/null || true
    endscript
}
EOF
}

configure_bastion_firewall() {
    echo "Configuring bastion firewall rules..."
    
    # Allow SSH from anywhere
    iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    iptables -A INPUT -p tcp --dport 2222 -j ACCEPT
    
    # Allow outbound connections to internal networks only
    for network in $INTERNAL_NETWORKS; do
        iptables -A OUTPUT -d "$network" -j ACCEPT
    done
    
    # Block outbound internet access (except DNS)
    iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
    iptables -A OUTPUT -p tcp --dport 53 -j ACCEPT
    iptables -A OUTPUT -o lo -j ACCEPT
    iptables -A OUTPUT -j DROP
    
    # Save firewall rules
    iptables-save > /etc/iptables/rules.v4
}

setup_bastion_host
```

### Multi-Factor Authentication Integration

#### OTP Implementation with Google Authenticator
```bash
# Install Google Authenticator PAM module
sudo apt update
sudo apt install libpam-google-authenticator qrencode

# Configure PAM for MFA
# /etc/pam.d/sshd
# Comment out or remove: @include common-auth
auth required pam_google_authenticator.so nullok
auth required pam_permit.so

# Update SSH configuration for MFA
# /etc/ssh/sshd_config
AuthenticationMethods publickey,keyboard-interactive
ChallengeResponseAuthentication yes
PasswordAuthentication no
PubkeyAuthentication yes
UsePAM yes

# User setup script for TOTP
#!/bin/bash
# setup-totp.sh - Set up TOTP for users

setup_user_totp() {
    local username="$1"
    local user_home="/home/$username"
    
    echo "Setting up TOTP for user: $username"
    
    # Switch to user context
    sudo -u "$username" bash << 'EOF'
cd ~
google-authenticator \
    --time-based \
    --disallow-reuse \
    --force \
    --rate-limit=3 \
    --rate-time=30 \
    --window-size=3 \
    --qr-mode=UTF8

echo "TOTP setup completed. Please scan the QR code with your authenticator app."
EOF

    # Set proper permissions
    chmod 600 "$user_home/.google_authenticator"
    chown "$username:$username" "$user_home/.google_authenticator"
    
    echo "TOTP configuration file secured for user: $username"
}

# Batch setup for multiple users
for user in alice bob charlie; do
    setup_user_totp "$user"
done
```

#### Hardware Token Integration (YubiKey)
```bash
# Install YubiKey PAM module
sudo apt install libpam-yubico yubikey-personalization

# Configure PAM for YubiKey
# /etc/pam.d/sshd
auth required pam_yubico.so id=12345 key=base64key authfile=/etc/yubikey_mappings

# Create YubiKey user mappings
# /etc/yubikey_mappings
alice:ccccccfhcgcc:ccccccfhcddi
bob:ccccccfhcgcd:ccccccfhcddk
charlie:ccccccfhcgce:ccccccfhcddl

# Set permissions
chmod 600 /etc/yubikey_mappings

# YubiKey management script
#!/bin/bash
# yubikey-manager.sh - Manage YubiKey authentication

MAPPING_FILE="/etc/yubikey_mappings"
LOG_FILE="/var/log/yubikey-auth.log"

add_yubikey_user() {
    local username="$1"
    local yubikey_id="$2"
    
    echo "Adding YubiKey for user: $username"
    
    # Validate YubiKey ID format (12 characters)
    if [[ ! "$yubikey_id" =~ ^[cbdefghijklnrtuv]{12}$ ]]; then
        echo "Error: Invalid YubiKey ID format"
        return 1
    fi
    
    # Add to mapping file
    echo "$username:$yubikey_id" >> "$MAPPING_FILE"
    
    # Log the addition
    echo "$(date): Added YubiKey $yubikey_id for user $username" >> "$LOG_FILE"
    
    echo "YubiKey added successfully"
}

remove_yubikey_user() {
    local username="$1"
    
    echo "Removing YubiKey for user: $username"
    
    # Remove from mapping file
    sed -i "/^$username:/d" "$MAPPING_FILE"
    
    # Log the removal
    echo "$(date): Removed YubiKey for user $username" >> "$LOG_FILE"
    
    echo "YubiKey removed successfully"
}

list_yubikey_users() {
    echo "YubiKey user mappings:"
    cat "$MAPPING_FILE"
}

# Usage: yubikey-manager.sh {add|remove|list} [username] [yubikey_id]
case "$1" in
    add)
        add_yubikey_user "$2" "$3"
        ;;
    remove)
        remove_yubikey_user "$2"
        ;;
    list)
        list_yubikey_users
        ;;
    *)
        echo "Usage: $0 {add|remove|list} [username] [yubikey_id]"
        exit 1
        ;;
esac
```

#### Combined MFA with Backup Methods
```bash
# /etc/pam.d/sshd - Advanced MFA configuration with fallback

# Primary MFA: YubiKey + TOTP
auth [success=2 default=ignore] pam_yubico.so id=12345 key=base64key authfile=/etc/yubikey_mappings
auth [success=1 default=ignore] pam_google_authenticator.so nullok
auth requisite pam_deny.so

# Backup authentication for emergency access
auth sufficient pam_exec.so expose_authtok /usr/local/bin/emergency-auth.sh

# Standard authentication
auth required pam_permit.so

# Emergency authentication script
#!/bin/bash
# emergency-auth.sh - Emergency MFA bypass with strict controls

EMERGENCY_FILE="/etc/ssh/emergency-access"
LOG_FILE="/var/log/emergency-auth.log"
SECURITY_EMAIL="security@example.com"

log_emergency_access() {
    local user="$1"
    local source_ip="${SSH_CLIENT%% *}"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    echo "[$timestamp] EMERGENCY_ACCESS: User=$user Source=$source_ip" >> "$LOG_FILE"
    
    # Send immediate alert
    echo "Emergency SSH access used by $user from $source_ip at $timestamp" | \
        mail -s "CRITICAL: Emergency SSH Access Used" "$SECURITY_EMAIL"
    
    # Log to syslog
    logger -p auth.crit "Emergency SSH access used by $user from $source_ip"
}

# Check if emergency access is enabled and valid
if [[ -f "$EMERGENCY_FILE" ]]; then
    # Check if user is authorized for emergency access
    if grep -q "^$PAM_USER$" "$EMERGENCY_FILE"; then
        # Check if emergency access window is valid (e.g., 24 hours)
        emergency_timestamp=$(stat -c %Y "$EMERGENCY_FILE")
        current_timestamp=$(date +%s)
        time_diff=$((current_timestamp - emergency_timestamp))
        
        if [[ $time_diff -lt 86400 ]]; then  # 24 hours
            log_emergency_access "$PAM_USER"
            exit 0  # Allow access
        fi
    fi
fi

exit 1  # Deny access
```

### Comprehensive SSH Session Auditing and Logging

#### Enhanced Logging Configuration and Custom Formats
```bash
# /etc/ssh/sshd_config - Enhanced audit logging configuration

# Maximum verbosity for security auditing
LogLevel VERBOSE

# Use dedicated syslog facility for SSH
SyslogFacility LOCAL0

# Force logging of all key fingerprints
LogLevel INFO
# In OpenSSH 8.0+, add:
FingerprintHash sha256

# Custom rsyslog configuration for SSH audit logging
# /etc/rsyslog.d/20-ssh-audit.conf
# SSH authentication events
local0.info     /var/log/ssh/ssh-auth.log
local0.debug    /var/log/ssh/ssh-debug.log

# SSH connection events to separate file
if $programname == 'sshd' and $msg contains 'Accepted' then /var/log/ssh/ssh-successful.log
if $programname == 'sshd' and $msg contains 'Failed' then /var/log/ssh/ssh-failed.log
if $programname == 'sshd' and $msg contains 'Invalid user' then /var/log/ssh/ssh-invalid.log

# Stop processing after SSH logs
& stop
```

#### Auditd Integration for System-Level Tracking
```bash
# /etc/audit/rules.d/30-ssh.rules - Comprehensive SSH auditing

# Monitor SSH daemon configuration changes
-w /etc/ssh/sshd_config -p wa -k ssh_config
-w /etc/ssh/ -p wa -k ssh_config

# Monitor SSH key files
-w /etc/ssh/ssh_host_rsa_key -p wa -k ssh_host_keys
-w /etc/ssh/ssh_host_ecdsa_key -p wa -k ssh_host_keys
-w /etc/ssh/ssh_host_ed25519_key -p wa -k ssh_host_keys

# Monitor user SSH directories
-a always,exit -F dir=/home -F perm=wa -F auid>=1000 -F auid!=4294967295 -k ssh_user_keys

# Monitor SSH agent usage
-a always,exit -F arch=b64 -S connect -F a2=16 -k ssh_agent
-a always,exit -F arch=b32 -S connect -F a2=16 -k ssh_agent

# Monitor SSH binary execution
-w /usr/sbin/sshd -p x -k ssh_execution
-w /usr/bin/ssh -p x -k ssh_execution
-w /usr/bin/scp -p x -k ssh_execution
-w /usr/bin/sftp -p x -k ssh_execution

# Monitor privilege escalation after SSH
-a always,exit -F arch=b64 -S execve -F euid=0 -F auid>=1000 -F auid!=4294967295 -k ssh_privilege_escalation
-a always,exit -F arch=b32 -S execve -F euid=0 -F auid>=1000 -F auid!=4294967295 -k ssh_privilege_escalation

# Restart auditd after adding rules
# systemctl restart auditd
```

#### SSH Jump Host Logging and Connection Chains
```bash
#!/bin/bash
# ssh-chain-logger.sh - Track SSH connection chains through jump hosts

CHAIN_LOG="/var/log/ssh-connection-chains.log"
SESSION_DIR="/var/run/ssh-sessions"

log_connection_chain() {
    local session_id="$$"
    local user="$USER"
    local source_ip="${SSH_CLIENT%% *}"
    local source_port="${SSH_CLIENT#* }"
    source_port="${source_port% *}"
    local target_command="$SSH_ORIGINAL_COMMAND"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Create session directory
    mkdir -p "$SESSION_DIR"
    
    # Determine if this is a jump connection
    local connection_type="direct"
    local parent_session=""
    
    if [[ -n "$SSH_TTY" ]]; then
        connection_type="interactive"
    elif [[ -n "$target_command" ]]; then
        connection_type="command"
        if echo "$target_command" | grep -q "ssh\|nc\|netcat"; then
            connection_type="jump"
            # Extract target from command
            local jump_target=$(echo "$target_command" | grep -oE '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}|[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}')
        fi
    fi
    
    # Check for parent SSH session
    local parent_pid=$(ps -o ppid= -p $PPID | tr -d ' ')
    if [[ -f "$SESSION_DIR/$parent_pid" ]]; then
        parent_session=$(cat "$SESSION_DIR/$parent_pid")
        connection_type="chained"
    fi
    
    # Create session record
    local session_record="$timestamp|$user|$source_ip:$source_port|$connection_type|$target_command|$parent_session"
    echo "$session_record" > "$SESSION_DIR/$session_id"
    
    # Log to chain log
    cat >> "$CHAIN_LOG" << EOF
[$timestamp] SESSION_START
  Session ID: $session_id
  User: $user
  Source: $source_ip:$source_port
  Type: $connection_type
  Command: $target_command
  Parent Session: $parent_session
  Chain: $(build_connection_chain "$session_id")
EOF
    
    # Set up session cleanup
    trap "cleanup_session $session_id" EXIT
    
    # Execute original command or shell
    if [[ -n "$target_command" ]]; then
        exec $target_command
    else
        exec /bin/bash
    fi
}

build_connection_chain() {
    local session_id="$1"
    local chain=""
    local current_session="$session_id"
    
    while [[ -f "$SESSION_DIR/$current_session" ]]; do
        local session_data=$(cat "$SESSION_DIR/$current_session")
        local session_user=$(echo "$session_data" | cut -d'|' -f2)
        local session_source=$(echo "$session_data" | cut -d'|' -f3)
        local parent_session=$(echo "$session_data" | cut -d'|' -f6)
        
        if [[ -n "$chain" ]]; then
            chain="$session_user@$session_source -> $chain"
        else
            chain="$session_user@$session_source"
        fi
        
        current_session="$parent_session"
        [[ -z "$current_session" ]] && break
    done
    
    echo "$chain"
}

cleanup_session() {
    local session_id="$1"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    echo "[$timestamp] SESSION_END: Session ID $session_id" >> "$CHAIN_LOG"
    rm -f "$SESSION_DIR/$session_id"
}

log_connection_chain
```

#### Session Recording and Playback with Script/asciinema
```bash
# Install session recording tools
sudo apt install asciinema script

# /usr/local/bin/ssh-session-recorder.sh - Automated session recording
#!/bin/bash
# ssh-session-recorder.sh - Record SSH sessions for audit

RECORDING_DIR="/var/log/ssh-sessions"
USER_RECORDING_DIR="$RECORDING_DIR/$USER"
SESSION_ID="ssh-$(date +%Y%m%d-%H%M%S)-$$"
RECORDING_FILE="$USER_RECORDING_DIR/$SESSION_ID.cast"

# Create recording directory
mkdir -p "$USER_RECORDING_DIR"
chmod 750 "$USER_RECORDING_DIR"

# Start session recording
start_recording() {
    local user="$USER"
    local source_ip="${SSH_CLIENT%% *}"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Log session start
    echo "[$timestamp] Recording started: User=$user Source=$source_ip File=$RECORDING_FILE" >> "/var/log/ssh-session-recordings.log"
    
    # Start asciinema recording
    exec asciinema rec \
        --title "SSH Session: $user@$(hostname) from $source_ip" \
        --command "/bin/bash" \
        "$RECORDING_FILE"
}

# Alternative using script command for TTY sessions
start_script_recording() {
    local user="$USER"
    local source_ip="${SSH_CLIENT%% *}"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    local script_file="$USER_RECORDING_DIR/$SESSION_ID.log"
    
    # Log session start
    echo "[$timestamp] Script recording started: User=$user Source=$source_ip File=$script_file" >> "/var/log/ssh-session-recordings.log"
    
    # Start script recording
    exec script -a -f -q "$script_file"
}

# Force session recording for specific users via sshd_config Match block
# Match User audit-user
#     ForceCommand /usr/local/bin/ssh-session-recorder.sh

# Check if TTY is available
if [[ -t 0 ]]; then
    start_recording
else
    # For non-TTY sessions, use command logging
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] Non-TTY session: User=$USER Command='$SSH_ORIGINAL_COMMAND'" >> "/var/log/ssh-command-log.log"
    exec $SSH_ORIGINAL_COMMAND
fi
```

#### Anomaly Detection and Behavioral Analysis
```bash
#!/bin/bash
# ssh-anomaly-detector.sh - Detect unusual SSH patterns

LOG_FILES=("/var/log/ssh/ssh-successful.log" "/var/log/auth.log")
ALERT_EMAIL="security@example.com"
BASELINE_FILE="/etc/ssh/behavioral-baseline.conf"
ANOMALY_LOG="/var/log/ssh-anomalies.log"

# Behavioral analysis functions
analyze_login_patterns() {
    local user="$1"
    local hours="${2:-24}"
    
    echo "Analyzing login patterns for $user over last $hours hours..."
    
    # Extract login times for user
    local login_times=$(grep "Accepted.*for $user" "${LOG_FILES[@]}" 2>/dev/null | \
        grep "$(date -d "$hours hours ago" '+%b %d')" | \
        awk '{print $3}' | cut -d: -f1 | sort | uniq -c)
    
    # Check for unusual login times
    echo "$login_times" | while read count hour; do
        if [[ $count -gt 10 ]] && [[ $hour -lt 6 || $hour -gt 22 ]]; then
            alert_anomaly "Unusual login time" "$user logged in $count times at hour $hour"
        fi
    done
}

analyze_source_ips() {
    local user="$1"
    local hours="${2:-24}"
    
    echo "Analyzing source IPs for $user over last $hours hours..."
    
    # Get unique source IPs for user
    local source_ips=$(grep "Accepted.*for $user" "${LOG_FILES[@]}" 2>/dev/null | \
        grep "$(date -d "$hours hours ago" '+%b %d')" | \
        awk '{print $NF}' | sort | uniq)
    
    local ip_count=$(echo "$source_ips" | wc -l)
    
    # Alert if user connects from many different IPs
    if [[ $ip_count -gt 5 ]]; then
        alert_anomaly "Multiple source IPs" "$user connected from $ip_count different IPs: $source_ips"
    fi
    
    # Check for connections from new countries/regions
    echo "$source_ips" | while read ip; do
        check_geo_anomaly "$user" "$ip"
    done
}

analyze_command_patterns() {
    local user="$1"
    local hours="${2:-24}"
    
    echo "Analyzing command patterns for $user..."
    
    # Extract commands from session logs
    local commands=$(grep "COMMAND_EXEC.*User=$user" /var/log/bastion-connections.log 2>/dev/null | \
        grep "$(date -d "$hours hours ago" '+%Y-%m-%d')" | \
        sed "s/.*Command='//; s/'.*//" | sort | uniq -c | sort -nr)
    
    # Check for unusual commands
    echo "$commands" | while read count command; do
        if [[ "$command" =~ (wget|curl|nc|netcat|python|perl|ruby|base64|xxd) ]]; then
            alert_anomaly "Suspicious command usage" "$user executed '$command' $count times"
        fi
    done
}

check_geo_anomaly() {
    local user="$1"
    local ip="$2"
    
    # Simple GeoIP check (requires geoip-bin package)
    if command -v geoiplookup >/dev/null 2>&1; then
        local country=$(geoiplookup "$ip" 2>/dev/null | grep "Country" | cut -d: -f2 | tr -d ' ')
        local baseline_countries=$(grep "^$user:" "$BASELINE_FILE" 2>/dev/null | cut -d: -f2)
        
        if [[ -n "$baseline_countries" ]] && ! echo "$baseline_countries" | grep -q "$country"; then
            alert_anomaly "New country login" "$user connected from new country: $country (IP: $ip)"
        fi
    fi
}

analyze_connection_frequency() {
    local user="$1"
    local hours="${2:-1}"
    
    # Count connections in the last hour
    local connection_count=$(grep "Accepted.*for $user" "${LOG_FILES[@]}" 2>/dev/null | \
        grep "$(date -d "$hours hours ago" '+%b %d %H')" | wc -l)
    
    # Get baseline for this user and hour
    local baseline=$(grep "^$user:.*:$(date +%H):" "$BASELINE_FILE" 2>/dev/null | cut -d: -f3)
    baseline=${baseline:-5}  # Default baseline
    
    # Alert if significantly above baseline
    if [[ $connection_count -gt $((baseline * 3)) ]]; then
        alert_anomaly "High connection frequency" "$user made $connection_count connections (baseline: $baseline)"
    fi
}

alert_anomaly() {
    local alert_type="$1"
    local message="$2"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Log anomaly
    echo "[$timestamp] ANOMALY: $alert_type - $message" >> "$ANOMALY_LOG"
    
    # Send email alert
    echo "SSH Anomaly Detected: $alert_type

Time: $timestamp
Details: $message

Please investigate this activity immediately.

Automated SSH Security Monitor" | \
    mail -s "SSH Security Alert: $alert_type" "$ALERT_EMAIL"
    
    # Log to syslog
    logger -p auth.warning "SSH Anomaly: $alert_type - $message"
}

generate_baseline() {
    local days="${1:-30}"
    
    echo "Generating behavioral baseline from last $days days..."
    
    # Analyze typical login patterns for each user
    grep "Accepted" "${LOG_FILES[@]}" 2>/dev/null | \
        grep "$(date -d "$days days ago" '+%b')" | \
        awk '{print $9, $3}' | \
        cut -d: -f1 | \
        sort | uniq -c | \
        awk '{
            user_hour = $2 " " $3
            count[user_hour] += $1
            users[user_hour] = $2
            hours[user_hour] = $3
        } END {
            for (uh in count) {
                avg = count[uh] / '$days'
                if (avg > 0) print users[uh] ":" hours[uh] ":" int(avg + 0.5)
            }
        }' > "$BASELINE_FILE"
    
    echo "Baseline generated: $BASELINE_FILE"
}

# Main analysis function
main() {
    local action="${1:-analyze}"
    local user="${2:-all}"
    local hours="${3:-24}"
    
    case "$action" in
        analyze)
            if [[ "$user" == "all" ]]; then
                # Analyze all active users
                grep "Accepted" "${LOG_FILES[@]}" 2>/dev/null | \
                    awk '{print $9}' | sort | uniq | \
                    while read active_user; do
                        echo "Analyzing user: $active_user"
                        analyze_login_patterns "$active_user" "$hours"
                        analyze_source_ips "$active_user" "$hours"
                        analyze_command_patterns "$active_user" "$hours"
                        analyze_connection_frequency "$active_user" 1
                    done
            else
                analyze_login_patterns "$user" "$hours"
                analyze_source_ips "$user" "$hours"
                analyze_command_patterns "$user" "$hours"
                analyze_connection_frequency "$user" 1
            fi
            ;;
        baseline)
            generate_baseline "$hours"
            ;;
        *)
            echo "Usage: $0 {analyze|baseline} [user|all] [hours]"
            exit 1
            ;;
    esac
}

main "$@"
```

### Scalable SSH Key and Host Management

#### Automated Key Rotation and Lifecycle Management
```bash
#!/bin/bash
# ssh-key-lifecycle-manager.sh - Enterprise SSH key lifecycle management

KEY_STORE="/srv/ssh-keys"
ROTATION_LOG="/var/log/ssh-key-rotation.log"
NOTIFICATION_EMAIL="security@example.com"
KEY_EXPIRY_DAYS=90
WARNING_DAYS=7

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$ROTATION_LOG"
}

rotate_user_key() {
    local username="$1"
    local key_type="${2:-ed25519}"
    local user_key_dir="$KEY_STORE/users/$username"
    local backup_dir="$user_key_dir/rotated-$(date +%Y%m%d-%H%M%S)"
    
    log "Starting key rotation for user: $username"
    
    # Create backup of current keys
    if [[ -d "$user_key_dir" ]]; then
        mkdir -p "$backup_dir"
        cp -a "$user_key_dir"/* "$backup_dir/" 2>/dev/null || true
        log "Backed up existing keys to: $backup_dir"
    fi
    
    # Generate new key pair
    mkdir -p "$user_key_dir"
    local new_key_file="$user_key_dir/id_${key_type}_$(date +%Y%m%d)"
    
    ssh-keygen -t "$key_type" -f "$new_key_file" \
        -C "$username@enterprise-rotated-$(date +%Y%m%d)" -N ""
    
    # Set metadata
    echo "$(date +%s)" > "$user_key_dir/.created"
    echo "$KEY_EXPIRY_DAYS" > "$user_key_dir/.expiry_days"
    
    # Create new authorized_keys with transition period
    create_transition_authorized_keys "$username" "$user_key_dir" "$backup_dir"
    
    # Deploy new keys
    deploy_rotated_keys "$username"
    
    log "Key rotation completed for user: $username"
    
    # Schedule old key cleanup
    echo "#!/bin/bash
# Auto-generated cleanup script
rm -rf '$backup_dir'
log 'Cleaned up old keys for $username: $backup_dir'
" > "/tmp/cleanup-$username-$(date +%s).sh"
    
    # Schedule cleanup in 30 days
    at now + 30 days < "/tmp/cleanup-$username-$(date +%s).sh" 2>/dev/null || \
        log "Warning: Could not schedule automatic cleanup"
}

create_transition_authorized_keys() {
    local username="$1"
    local user_key_dir="$2"
    local backup_dir="$3"
    
    local auth_keys="$user_key_dir/authorized_keys"
    
    cat > "$auth_keys" << EOF
# SSH Key Rotation Transition Period
# Generated: $(date)
# User: $username
# Transition expires: $(date -d "+7 days")

# NEW KEY (Primary)
$(cat "$user_key_dir"/id_*.pub 2>/dev/null | head -1)

# OLD KEY (Grace period - expires in 7 days)
EOF
    
    # Add old key with expiry comment
    if [[ -d "$backup_dir" ]]; then
        cat "$backup_dir"/id_*.pub 2>/dev/null | head -1 | \
            sed 's/$/ # OLD-KEY-EXPIRES-'"$(date -d '+7 days' +%Y%m%d)"'/' >> "$auth_keys"
    fi
    
    chmod 600 "$auth_keys"
}

deploy_rotated_keys() {
    local username="$1"
    local user_key_dir="$KEY_STORE/users/$username"
    local target_hosts=$(cat "$KEY_STORE/deployment-targets.txt" 2>/dev/null || echo "localhost")
    
    log "Deploying rotated keys for $username to target hosts"
    
    for host in $target_hosts; do
        log "Deploying to host: $host"
        
        if scp "$user_key_dir/authorized_keys" "keysync@$host:/tmp/authorized_keys_$username"; then
            ssh "keysync@$host" "
                sudo mkdir -p /home/$username/.ssh
                sudo cp /tmp/authorized_keys_$username /home/$username/.ssh/authorized_keys
                sudo chown -R $username:$username /home/$username/.ssh
                sudo chmod 700 /home/$username/.ssh
                sudo chmod 600 /home/$username/.ssh/authorized_keys
                rm /tmp/authorized_keys_$username
            " && log "Successfully deployed to $host" || log "Failed to deploy to $host"
        else
            log "Failed to copy keys to $host"
        fi
    done
}

check_key_expiry() {
    local username="$1"
    local user_key_dir="$KEY_STORE/users/$username"
    
    if [[ ! -f "$user_key_dir/.created" ]]; then
        log "No creation timestamp found for $username keys"
        return 1
    fi
    
    local created_timestamp=$(cat "$user_key_dir/.created")
    local expiry_days=$(cat "$user_key_dir/.expiry_days" 2>/dev/null || echo "$KEY_EXPIRY_DAYS")
    local current_timestamp=$(date +%s)
    local key_age_days=$(( (current_timestamp - created_timestamp) / 86400 ))
    local days_until_expiry=$((expiry_days - key_age_days))
    
    if [[ $days_until_expiry -le 0 ]]; then
        log "EXPIRED: Keys for $username expired $((0 - days_until_expiry)) days ago"
        return 2
    elif [[ $days_until_expiry -le $WARNING_DAYS ]]; then
        log "WARNING: Keys for $username expire in $days_until_expiry days"
        return 1
    else
        log "OK: Keys for $username expire in $days_until_expiry days"
        return 0
    fi
}

bulk_key_rotation() {
    local users_file="${1:-$KEY_STORE/managed-users.txt}"
    
    if [[ ! -f "$users_file" ]]; then
        log "Users file not found: $users_file"
        return 1
    fi
    
    log "Starting bulk key rotation for users in: $users_file"
    
    while IFS= read -r username; do
        [[ -z "$username" || "$username" =~ ^# ]] && continue
        
        check_key_expiry "$username"
        local expiry_status=$?
        
        case $expiry_status in
            2)
                log "Rotating expired keys for: $username"
                rotate_user_key "$username"
                ;;
            1)
                log "Scheduling rotation for: $username (expires soon)"
                # Add to priority rotation queue
                echo "$username" >> "$KEY_STORE/priority-rotation.queue"
                ;;
            0)
                log "Keys OK for: $username"
                ;;
        esac
    done < "$users_file"
}

generate_key_inventory() {
    local output_file="${1:-/tmp/ssh-key-inventory-$(date +%Y%m%d).csv}"
    
    log "Generating SSH key inventory: $output_file"
    
    echo "Username,KeyType,Created,Age(days),ExpiryDays,Status,Fingerprint" > "$output_file"
    
    for user_dir in "$KEY_STORE/users"/*; do
        [[ ! -d "$user_dir" ]] && continue
        
        local username=$(basename "$user_dir")
        local key_file=$(find "$user_dir" -name "id_*" -not -name "*.pub" | head -1)
        
        if [[ -f "$key_file" ]]; then
            local key_type=$(ssh-keygen -l -f "$key_file" | awk '{print $NF}' | tr -d '()')
            local fingerprint=$(ssh-keygen -l -f "$key_file" | awk '{print $2}')
            local created_timestamp=$(cat "$user_dir/.created" 2>/dev/null || echo "0")
            local expiry_days=$(cat "$user_dir/.expiry_days" 2>/dev/null || echo "$KEY_EXPIRY_DAYS")
            
            if [[ "$created_timestamp" != "0" ]]; then
                local created_date=$(date -d "@$created_timestamp" '+%Y-%m-%d')
                local key_age_days=$(( ($(date +%s) - created_timestamp) / 86400 ))
                local status="OK"
                
                if [[ $key_age_days -gt $expiry_days ]]; then
                    status="EXPIRED"
                elif [[ $key_age_days -gt $((expiry_days - WARNING_DAYS)) ]]; then
                    status="EXPIRES_SOON"
                fi
            else
                local created_date="UNKNOWN"
                local key_age_days="UNKNOWN"
                local status="NO_METADATA"
            fi
            
            echo "$username,$key_type,$created_date,$key_age_days,$expiry_days,$status,$fingerprint" >> "$output_file"
        fi
    done
    
    log "Key inventory generated: $output_file"
}

# Automated rotation scheduler
schedule_automated_rotation() {
    # Create cron job for daily key expiry checks
    cat > /etc/cron.d/ssh-key-rotation << EOF
# SSH Key Rotation Schedule
# Check for expiring keys daily at 2 AM
0 2 * * * root /usr/local/bin/ssh-key-lifecycle-manager.sh bulk_rotation
# Generate weekly inventory report
0 8 * * 1 root /usr/local/bin/ssh-key-lifecycle-manager.sh inventory
EOF
    
    log "Automated rotation scheduled via cron"
}

# Main function
main() {
    local action="${1:-check}"
    local target="${2:-all}"
    
    case "$action" in
        rotate)
            rotate_user_key "$target"
            ;;
        check)
            if [[ "$target" == "all" ]]; then
                bulk_key_rotation
            else
                check_key_expiry "$target"
            fi
            ;;
        bulk_rotation)
            bulk_key_rotation
            ;;
        inventory)
            generate_key_inventory
            ;;
        schedule)
            schedule_automated_rotation
            ;;
        *)
            echo "Usage: $0 {rotate|check|bulk_rotation|inventory|schedule} [user|all]"
            exit 1
            ;;
    esac
}

main "$@"
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

### Lab 1: Strong SSH Key Generation and Agent Forwarding
**Objective:** Generate strong SSH key pairs (ED25519) and configure SSH agent forwarding

**Tasks:**
1. Generate and compare different SSH key types:
   - Create ED25519, RSA 4096-bit, and ECDSA P-521 keys
   - Analyze security characteristics and performance
   - Document key selection rationale for different use cases
2. Configure secure SSH agent:
   - Set up SSH agent with timeout restrictions
   - Implement agent forwarding with confirmation requirements
   - Create agent management scripts for automated workflows
3. Deploy keys with proper permissions and metadata

**Deliverables:**
- Key generation and comparison documentation
- Secure SSH agent configuration
- Automated key deployment scripts

### Lab 2: SSH Server Hardening and Protocol 2 Enforcement
**Objective:** Harden the SSH server by tuning sshd_config parameters and enforcing Protocol 2

**Tasks:**
1. Implement comprehensive sshd_config hardening:
   - Enforce SSH Protocol 2 only
   - Configure strong cryptographic algorithms
   - Disable dangerous features (root login, password auth)
   - Implement rate limiting and brute force protection
2. Set up advanced logging and monitoring:
   - Configure enhanced SSH logging
   - Implement Fail2ban with custom rules
   - Create SSH connection monitoring scripts
3. Validate configuration security and performance

**Deliverables:**
- Hardened sshd_config with documentation
- Automated security validation scripts
- Monitoring and alerting system

### Lab 3: Fine-grained Access Control with Authorized Keys
**Objective:** Implement fine-grained access controls using authorized_keys options

**Tasks:**
1. Create authorized_keys entries with advanced restrictions:
   - Source IP filtering (from= directive)
   - Command forcing for service accounts
   - Environment variable injection
   - PTY and forwarding restrictions
2. Implement conditional access controls:
   - Time-based access restrictions
   - Network-based access policies
   - Dynamic key generation based on conditions
3. Create management tools for authorized_keys at scale

**Deliverables:**
- Comprehensive authorized_keys templates
- Conditional access control system
- Automated key management tools

### Lab 4: Bastion Host Design and ProxyJump Implementation
**Objective:** Design and deploy a bastion host using ProxyJump for secure access

**Tasks:**
1. Deploy enterprise bastion host:
   - Configure bastion-specific SSH settings
   - Implement user access controls and logging
   - Set up network isolation and firewall rules
2. Configure ProxyJump and ProxyCommand:
   - Set up multi-hop SSH connections
   - Implement conditional routing based on target
   - Create complex proxy command configurations
3. Implement bastion monitoring and audit logging:
   - Connection chain tracking
   - Session recording and playback
   - Alert system for suspicious activity

**Deliverables:**
- Fully configured bastion host infrastructure
- Client-side proxy configuration
- Comprehensive audit and monitoring system

### Lab 5: Multi-Factor Authentication Integration
**Objective:** Integrate multi-factor authentication for SSH logins with OTP or hardware tokens

**Tasks:**
1. Implement OTP authentication:
   - Deploy Google Authenticator PAM module
   - Configure TOTP for multiple users
   - Set up backup authentication methods
2. Integrate hardware token authentication:
   - Configure YubiKey PAM module
   - Manage hardware token mappings
   - Implement emergency access procedures
3. Test and validate MFA workflows:
   - Authentication method combinations
   - Emergency access scenarios
   - User enrollment and recovery procedures

**Deliverables:**
- Multi-factor authentication system
- User enrollment and management tools
- Emergency access procedures and documentation

### Lab 6: Comprehensive SSH Session Auditing
**Objective:** Audit SSH sessions through enhanced logging and detect anomalous behavior

**Tasks:**
1. Implement enhanced SSH logging:
   - Configure custom log formats and facilities
   - Integrate with auditd for system-level tracking
   - Set up connection chain logging for jump hosts
2. Deploy session recording and analysis:
   - Implement automated session recording
   - Create session playback and analysis tools
   - Set up command logging and filtering
3. Develop anomaly detection system:
   - Behavioral baseline establishment
   - Real-time anomaly detection algorithms
   - Automated alerting and response procedures

**Deliverables:**
- Comprehensive SSH audit logging system
- Session recording and analysis tools
- Automated anomaly detection and alerting

### Lab 7: Scalable SSH Key and Host Management
**Objective:** Rotate, revoke, and manage SSH host and user keys in a scalable manner

**Tasks:**
1. Implement automated key lifecycle management:
   - Create key rotation scheduling system
   - Develop key expiry monitoring and alerts
   - Set up automated key distribution
2. Deploy SSH Certificate Authority:
   - Configure SSH CA for user and host certificates
   - Implement certificate-based authentication
   - Create certificate revocation procedures
3. Build enterprise key management system:
   - Centralized key storage and distribution
   - Key inventory and compliance reporting
   - Automated provisioning and deprovisioning

**Deliverables:**
- Automated key lifecycle management system
- SSH Certificate Authority implementation
- Enterprise key management infrastructure

## Assessment Criteria

Each lab will be evaluated based on:

| Criteria | Weight | Description |
|----------|---------|-------------|
| Security Implementation | 35% | Proper security controls and hardening |
| Automation and Scalability | 25% | Effective automation and enterprise scalability |
| Documentation and Procedures | 20% | Clear documentation and operational procedures |
| Monitoring and Auditing | 20% | Comprehensive logging and anomaly detection |

## SSH Security Best Practices Summary

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| Key Management | Use ED25519 keys with proper lifecycle | Automated rotation every 90 days |
| Authentication | Multi-factor authentication required | OTP + Hardware tokens |
| Server Hardening | Protocol 2 only, strong algorithms | Comprehensive sshd_config |
| Access Control | Fine-grained authorized_keys restrictions | Source IP, command, time limits |
| Network Security | Bastion hosts with ProxyJump | Isolated network segments |
| Auditing | Enhanced logging and session recording | Real-time anomaly detection |
| Scalability | Centralized key and certificate management | Automated provisioning systems |

## Advanced Challenge Scenarios

For additional learning, consider these advanced scenarios:

1. **Zero-Trust SSH Architecture:** Implement certificate-based authentication with short-lived certificates
2. **SSH in Container Environments:** Secure SSH access to containerized workloads
3. **Compliance Integration:** Implement SOC 2, PCI DSS, or FedRAMP compliance controls
4. **Cross-Platform Management:** Manage SSH across Linux, Windows (OpenSSH), and network devices
5. **High-Availability SSH:** Implement redundant bastion hosts with load balancing

## Next Steps
With OpenSSH best practices mastered, you're ready to explore Proxmox Infrastructure Automation in Module 14, where you'll learn to automate infrastructure deployment and management using modern DevOps tools and practices.
