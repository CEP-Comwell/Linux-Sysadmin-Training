# Module 13: OpenSSH Best Practices

## Overview

Master enterprise-grade SSH security and management through comprehensive implementation of modern cryptographic protocols, advanced access controls, and scalable key management infrastructure. OpenSSH serves as the foundation for secure remote administration in enterprise environments, requiring sophisticated configuration to meet security, compliance, and operational requirements.

This module provides in-depth coverage of SSH security hardening, from basic server configuration to advanced enterprise architectures including certificate authorities, multi-factor authentication, and zero-trust access models. Learn to design and implement SSH infrastructure that scales from small environments to large enterprise deployments while maintaining the highest security standards.

**Enterprise Security Capabilities:**
- Modern cryptographic algorithm implementation and quantum-resistant preparations
- Advanced access control mechanisms with fine-grained authorization policies
- Enterprise key management with automated lifecycle and certificate authorities
- Multi-factor authentication integration with hardware tokens and biometric systems
- Comprehensive session auditing and real-time security monitoring
- Zero-trust network architecture with bastion hosts and micro-segmentation

## Learning Objectives

By completing this module, you will be able to:

1. **Implement Advanced Cryptographic Security**
   - Deploy modern SSH algorithms and prepare for post-quantum cryptography
   - Configure secure key exchange, encryption, and authentication methods
   - Implement cryptographic best practices for enterprise environments

2. **Design Scalable Key Management Infrastructure**
   - Build enterprise SSH Certificate Authority (CA) systems
   - Implement automated key lifecycle management and rotation
   - Deploy centralized key distribution and revocation mechanisms

3. **Configure Enterprise Access Controls**
   - Implement fine-grained authorization with advanced authorized_keys options
   - Design role-based access control (RBAC) for SSH infrastructure
   - Configure conditional access based on time, location, and risk factors

4. **Build Secure Remote Access Architecture**
   - Design and implement bastion host architectures with multiple security layers
   - Configure zero-trust network access with micro-segmentation
   - Implement secure SSH tunneling and port forwarding controls

5. **Integrate Multi-Factor Authentication**
   - Deploy hardware token-based authentication (YubiKey, FIDO2)
   - Implement time-based one-time passwords (TOTP) and mobile push notifications
   - Configure adaptive authentication based on risk assessment

6. **Establish Comprehensive Security Monitoring**
   - Implement real-time SSH session monitoring and anomaly detection
   - Configure automated threat response and incident management
   - Deploy compliance reporting and audit trail management

## Table of Contents

### [13.1 Advanced Cryptographic Implementation](#131-advanced-cryptographic-implementation)
- Modern SSH algorithm selection and quantum-resistance preparation
- Secure key exchange protocols and perfect forward secrecy
- Cryptographic policy implementation and compliance requirements
- Performance optimization for cryptographic operations
- Future-proofing strategies for post-quantum cryptography

### [13.2 Enterprise Key Management Infrastructure](#132-enterprise-key-management-infrastructure)
- SSH Certificate Authority design and implementation
- Automated key lifecycle management and rotation policies
- Centralized key distribution and secure storage systems
- Hardware Security Module (HSM) integration
- Key escrow and recovery procedures for enterprise environments

### [13.3 Advanced Access Control and Authorization](#133-advanced-access-control-and-authorization)
- Fine-grained authorized_keys configuration and restrictions
- Role-based access control (RBAC) implementation
- Conditional access policies based on context and risk
- Integration with enterprise identity management systems
- Privilege escalation controls and session recording

### [13.4 Secure Network Architecture and Bastion Hosts](#134-secure-network-architecture-and-bastion-hosts)
- Zero-trust network architecture with SSH micro-segmentation
- Multi-tier bastion host design and implementation
- Secure tunneling and port forwarding policies
- Network segmentation and traffic flow analysis
- High-availability bastion infrastructure with load balancing

### [13.5 Multi-Factor Authentication and Adaptive Security](#135-multi-factor-authentication-and-adaptive-security)
- Hardware token integration (YubiKey, FIDO2, smart cards)
- Biometric authentication and behavioral analysis
- Risk-based adaptive authentication systems
- Mobile device integration and push notification services
- Compliance requirements and audit trail management

### [13.6 Comprehensive Security Monitoring and Auditing](#136-comprehensive-security-monitoring-and-auditing)
- Real-time session monitoring and anomaly detection
- Security Information and Event Management (SIEM) integration
- Automated threat response and incident management
- Compliance reporting and regulatory audit support
- Forensic analysis and incident reconstruction capabilities

### [13.7 Enterprise Operations and Automation](#137-enterprise-operations-and-automation)
- Infrastructure as Code (IaC) for SSH configuration management
- Automated provisioning and deprovisioning workflows
- Configuration compliance monitoring and drift detection
- Performance monitoring and capacity planning
- Disaster recovery and business continuity planning

### [13.8 Advanced Security Scenarios and Threat Response](#138-advanced-security-scenarios-and-threat-response)
- Advanced Persistent Threat (APT) detection and response
- Insider threat monitoring and prevention
- Supply chain security and trusted computing base
- International security standards and regulatory compliance
- Security architecture documentation and threat modeling

## Essential Command Reference

### SSH Key Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Key Generation** | `ssh-keygen -t ed25519` | Generate ED25519 key pair | `ssh-keygen -t ed25519 -f ~/.ssh/enterprise_key -C "admin@company.com"` |
| | `ssh-keygen -t rsa -b 4096` | Generate 4096-bit RSA key | `ssh-keygen -t rsa -b 4096 -f ~/.ssh/legacy_rsa_key` |
| | `ssh-keygen -t ecdsa -b 521` | Generate ECDSA key | `ssh-keygen -t ecdsa -b 521 -f ~/.ssh/ecdsa_key` |
| **Key Operations** | `ssh-keygen -l -f <keyfile>` | Display key fingerprint | `ssh-keygen -l -f ~/.ssh/id_ed25519.pub` |
| | `ssh-keygen -y -f <private_key>` | Extract public key | `ssh-keygen -y -f ~/.ssh/id_ed25519 > ~/.ssh/id_ed25519.pub` |
| | `ssh-keygen -p -f <keyfile>` | Change key passphrase | `ssh-keygen -p -f ~/.ssh/id_ed25519` |
| | `ssh-keygen -R <hostname>` | Remove host from known_hosts | `ssh-keygen -R server.company.com` |
| **Key Validation** | `ssh-keygen -t rsa -b 4096 -f /dev/stdout` | Test key generation | `ssh-keygen -t ed25519 -N "" -f /dev/stdout` |
| | `ssh-keygen -l -v -f <keyfile>` | Verbose key information | `ssh-keygen -l -v -f ~/.ssh/id_ed25519.pub` |

### SSH Certificate Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **CA Operations** | `ssh-keygen -t ed25519 -f ssh_ca` | Create CA key pair | `ssh-keygen -t ed25519 -f /etc/ssh/ssh_ca -C "SSH-CA"` |
| | `ssh-keygen -s <ca_key> -I <identity>` | Sign user certificate | `ssh-keygen -s ssh_ca -I "john.doe" -n john ~/.ssh/id_ed25519.pub` |
| | `ssh-keygen -s <ca_key> -h -I <identity>` | Sign host certificate | `ssh-keygen -s ssh_ca -h -I server.company.com /etc/ssh/ssh_host_ed25519_key.pub` |
| **Certificate Validation** | `ssh-keygen -L -f <cert_file>` | Display certificate details | `ssh-keygen -L -f ~/.ssh/id_ed25519-cert.pub` |
| | `ssh-keygen -T <cert_file>` | Test certificate validity | `ssh-keygen -T ~/.ssh/id_ed25519-cert.pub` |
| **Certificate Options** | `-V <validity_interval>` | Set certificate validity | `ssh-keygen -s ca_key -I user -V +1d ~/.ssh/key.pub` |
| | `-O <option>` | Add certificate options | `ssh-keygen -s ca_key -I user -O force-command="/bin/bash" key.pub` |

### SSH Server Configuration

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Service Management** | `systemctl status sshd` | Check SSH service status | `systemctl status sshd` |
| | `systemctl reload sshd` | Reload SSH configuration | `systemctl reload sshd` |
| | `systemctl restart sshd` | Restart SSH service | `systemctl restart sshd` |
| **Configuration Testing** | `sshd -t` | Test SSH configuration | `sshd -T` |
| | `sshd -T` | Display effective configuration | `sshd -T -f /etc/ssh/sshd_config` |
| | `sshd -d` | Debug mode (foreground) | `sshd -d -p 2222` |
| **Host Key Management** | `ssh-keygen -A` | Generate all host keys | `ssh-keygen -A` |
| | `ssh-keygen -H` | Hash known_hosts file | `ssh-keygen -H -f ~/.ssh/known_hosts` |

### SSH Client Configuration

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Connection Options** | `ssh -o <option>` | Specify connection option | `ssh -o StrictHostKeyChecking=yes user@server` |
| | `ssh -F <config_file>` | Use alternate config file | `ssh -F ~/.ssh/config_prod user@server` |
| | `ssh -i <identity_file>` | Use specific private key | `ssh -i ~/.ssh/enterprise_key user@server` |
| **Tunneling** | `ssh -L <local_port>:<remote_host>:<remote_port>` | Local port forwarding | `ssh -L 8080:localhost:80 user@server` |
| | `ssh -R <remote_port>:<local_host>:<local_port>` | Remote port forwarding | `ssh -R 9090:localhost:3000 user@server` |
| | `ssh -D <port>` | Dynamic SOCKS proxy | `ssh -D 1080 user@server` |
| **ProxyJump** | `ssh -J <jump_host>` | Connect via jump host | `ssh -J bastion.company.com user@internal-server` |
| | `ssh -o ProxyJump=<host1,host2>` | Multi-hop connection | `ssh -o ProxyJump=bastion1,bastion2 user@target` |

### SSH Agent Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Agent Operations** | `ssh-agent bash` | Start SSH agent | `eval $(ssh-agent)` |
| | `ssh-add <keyfile>` | Add key to agent | `ssh-add ~/.ssh/id_ed25519` |
| | `ssh-add -l` | List loaded keys | `ssh-add -l` |
| | `ssh-add -d <keyfile>` | Remove key from agent | `ssh-add -d ~/.ssh/id_ed25519` |
| | `ssh-add -D` | Remove all keys | `ssh-add -D` |
| **Agent Forwarding** | `ssh -A` | Enable agent forwarding | `ssh -A user@server` |
| | `ssh -o ForwardAgent=yes` | Enable agent forwarding | `ssh -o ForwardAgent=yes user@server` |
| **Agent Security** | `ssh-add -c` | Require confirmation | `ssh-add -c ~/.ssh/id_ed25519` |
| | `ssh-add -t <timeout>` | Set key timeout | `ssh-add -t 3600 ~/.ssh/id_ed25519` |

### Security Monitoring and Auditing

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Log Analysis** | `journalctl -u sshd` | View SSH service logs | `journalctl -u sshd --since today` |
| | `grep "Failed password"` | Find failed login attempts | `grep "Failed password" /var/log/auth.log` |
| | `lastlog` | Show last login information | `lastlog -u username` |
| | `last` | Show login history | `last -n 20` |
| **Security Scanning** | `nmap -sV -p 22` | SSH service detection | `nmap -sV -p 22 target-server` |
| | `ssh-audit` | SSH security audit | `ssh-audit server.company.com` |
| **Session Recording** | `script -T timing.log session.log` | Record SSH session | `script -T timing.log -a session.log` |
| | `scriptreplay timing.log session.log` | Replay recorded session | `scriptreplay timing.log session.log` |

### Advanced SSH Operations

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **File Operations** | `scp -r <source> <destination>` | Secure copy with recursion | `scp -r ./files/ user@server:/path/` |
| | `rsync -avz -e ssh` | Rsync over SSH | `rsync -avz -e ssh ./data/ user@server:/backup/` |
| | `sftp` | Secure FTP session | `sftp user@server` |
| **Remote Execution** | `ssh user@server 'command'` | Execute remote command | `ssh user@server 'systemctl status nginx'` |
| | `ssh -t user@server command` | Force pseudo-terminal | `ssh -t user@server sudo systemctl restart nginx` |
| **Escape Sequences** | `~.` | Terminate connection | Press `~.` to disconnect |
| | `~^Z` | Suspend connection | Press `~Ctrl+Z` to suspend |
| | `~#` | List forwarded connections | Press `~#` to list connections |
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

#### ED25519 vs. RSA: Cryptographic Analysis and Practical Implications

##### **Understanding the Basics: Why Different SSH Key Types Matter**

**ED25519 (The Modern Choice)**
- **What it is**: A newer encryption method based on mathematical curves
- **Think of it like**: A high-tech security system designed from the ground up for modern threats
- **Key benefits**: Fast, secure, and built to resist future attacks
- **Best for**: All new systems and security-conscious environments

**RSA (The Traditional Choice)**  
- **What it is**: An older encryption method based on large number factorization
- **Think of it like**: A reliable, well-tested security system that's been around since the 1970s
- **Key benefits**: Works everywhere, extensively tested, widely understood
- **Best for**: Legacy systems and environments requiring maximum compatibility

##### **Why We Care About "Quantum Resistance"**

**The Quantum Computer Threat (Simplified):**
Imagine if someone invented a tool that could crack any traditional lock in seconds. Quantum computers might be that tool for current encryption.

**Current Status:**
- **Today**: No quantum computer exists that can break SSH encryption
- **Timeline**: Experts estimate 10-20 years before this becomes a real threat
- **Preparation**: Using quantum-resistant encryption now prepares us for the future

**Real-World Impact:**
```
If a powerful quantum computer existed today:
- Your RSA-2048 SSH key: Could be broken in hours/days
- Your RSA-4096 SSH key: Could be broken in weeks/months  
- Your ED25519 SSH key: Would take much longer to break
- Post-quantum algorithms: Would remain secure (still being developed)
```

##### **Cryptographic Security Advantages**

**Why ED25519 is Better for Modern Security:**

**🔐 Stronger Security Foundation**
```
Think of encryption like a lock on your house:
- ED25519 is like a modern smart lock with multiple security layers
- RSA is like a traditional lock that's been around for decades

Key Advantages:
✓ Built-in protection against timing attacks (hackers can't measure how long operations take)
✓ No "weak" keys possible - every key generated is strong
✓ Smaller keys = faster operations = better performance
✓ Future-ready design that's harder for quantum computers to break
```

**🛡️ Attack Resistance Comparison**

**ED25519 Protection:**
- **Timing Attacks**: Immune by design - operations always take the same time
- **Weak Random Numbers**: Can't generate weak keys even with poor randomness
- **Side-Channel Attacks**: Protected against hackers analyzing power usage or electromagnetic emissions
- **Implementation Bugs**: Simpler code = fewer places for security vulnerabilities

**RSA Vulnerabilities:**
- **Timing Attacks**: Vulnerable unless carefully implemented
- **Weak Key Generation**: Historical problems with poor random number generators
- **Complex Implementation**: More code = more potential security bugs
- **Performance**: Slower operations, especially for key generation

**🚀 Quantum Computer Resistance**

**Why This Matters:**
Large quantum computers (which don't exist yet but are being developed) could potentially break current encryption. Think of it like having a master key that could open any traditional lock.

**ED25519 vs RSA Against Quantum Computers:**
- **ED25519**: Would take a quantum computer ~2⁶⁴ operations to break (very difficult)
- **RSA**: Would take a quantum computer ~2⁵¹² operations to break (easier target)
- **Timeline**: Experts estimate 10-20 years before quantum computers become a real threat
- **Recommendation**: Start using ED25519 now to be prepared for the future

**📊 Real-World Performance Impact**

**Speed Comparison (simpler terms):**
```
Key Generation Time:
- ED25519: Nearly instant
- RSA-4096: Noticeable delay (500x slower)

Connection Setup:
- ED25519: Faster SSH connections
- RSA: Slower, especially on older hardware

Network Usage:
- ED25519: 16x smaller keys = less bandwidth
- RSA: Larger keys = more network traffic
```

**🎯 Practical Recommendations for System Administrators**

**What to Use When:**
1. **New Systems (2025+)**: Always use ED25519
2. **Legacy Support**: Keep RSA-4096 as backup for old systems
3. **Hardware Tokens**: Use ED25519 if supported, RSA-4096 otherwise
4. **Compliance**: Check if your security frameworks accept ED25519 (most do now)

**Migration Strategy:**
```bash
# Generate both key types during transition
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_modern
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_legacy

# Use ED25519 for new systems
Host modern-servers
    IdentityFile ~/.ssh/id_ed25519_modern

# Keep RSA for older systems that don't support ED25519
Host legacy-systems  
    IdentityFile ~/.ssh/id_rsa_legacy
```

**⚠️ Security Warnings:**
- **Never use RSA-2048 or smaller** - too weak for modern threats
- **RSA-1024 is completely broken** - if you see this, replace immediately
- **ED25519 is not supported** on very old SSH versions (pre-2014)
- **Always use strong passphrases** regardless of key type

**🔮 Future-Proofing Your Infrastructure**

**Quantum-Resistant Planning:**
- **Short-term**: ED25519 provides better quantum resistance than RSA
- **Medium-term**: Monitor post-quantum cryptography standards (NIST is working on this)
- **Long-term**: Plan for algorithm updates when quantum computers become practical
- **Best Practice**: Design systems that can easily switch encryption methods

##### **Performance and Efficiency Analysis**

**Computational Complexity:**
```bash
# ED25519 Operations (theoretical cycles on modern CPU)
Key Generation:    ~100,000 cycles
Signature:         ~150,000 cycles  
Verification:      ~400,000 cycles
Key Size:          32 bytes private, 32 bytes public

# RSA-4096 Operations
Key Generation:    ~50,000,000 cycles (500x slower)
Signature:         ~8,000,000 cycles (53x slower)
Verification:      ~200,000 cycles (similar to ED25519)
Key Size:          512 bytes private, 512 bytes public
```

**Memory and Bandwidth Efficiency:**
- **ED25519**: 64-byte signatures, 32-byte public keys (16x smaller than RSA-4096)
- **RSA-4096**: 512-byte signatures, 512-byte public keys
- **Network Impact**: ED25519 reduces SSH handshake by ~1KB per connection
- **Storage Impact**: Certificate chains significantly smaller with ECC

##### **Practical Security Implications**

**Key Generation Security:**
```bash
# ED25519: Inherently secure key generation
# - Private key is 32 random bytes
# - Public key derived through well-defined curve operations
# - No "weak" keys possible due to curve properties

openssl genpkey -algorithm Ed25519 -out ed25519.pem

# RSA: Vulnerable to implementation flaws
# - Requires strong prime generation
# - Susceptible to weak random number generators
# - Historical vulnerabilities (Debian OpenSSL bug, etc.)

openssl genpkey -algorithm RSA -pkcs8 -pkeyopt rsa_keygen_bits:4096 -out rsa4096.pem
```

**Implementation Security:**
```
ED25519 Advantages:
✓ Constant-time operations by design
✓ Complete addition formulas prevent exceptional cases
✓ Single coordinate system eliminates conversion vulnerabilities
✓ Smaller attack surface due to algorithmic simplicity

RSA Vulnerabilities:
✗ Timing attacks on modular exponentiation
✗ Blinding required for side-channel resistance
✗ Padding oracle attacks (if improperly implemented)
✗ Larger codebase increases vulnerability surface
```

##### **Enterprise Deployment Considerations**

**Compatibility Matrix:**
```
ED25519 Support:
- OpenSSH: 6.5+ (January 2014)
- OpenSSL: 1.1.1+ (September 2018)
- GnuPG: 2.1+ (November 2014)
- Hardware tokens: Limited (YubiKey 5 series+)

RSA Support:
- Universal compatibility across all SSH implementations
- Hardware security modules: Extensive support
- Legacy systems: Full backward compatibility
- Compliance frameworks: Widely accepted
```

**Migration Strategy:**
```bash
# Hybrid approach for enterprise environments
# Primary: ED25519 for modern systems
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_primary

# Fallback: RSA-4096 for legacy compatibility
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_legacy

# SSH config for automatic fallback
Host modern-systems
    IdentityFile ~/.ssh/id_ed25519_primary
    IdentitiesOnly yes

Host legacy-systems
    IdentityFile ~/.ssh/id_rsa_legacy
    IdentitiesOnly yes
```

##### **Cryptographic Recommendations**

**Current Best Practices (2025):**
1. **Primary Choice**: ED25519 for all new deployments
2. **Legacy Support**: RSA-4096 minimum (RSA-2048 deprecated)
3. **Transition Period**: Maintain both key types during migration
4. **Hardware Tokens**: ED25519 where supported, RSA-4096 otherwise
5. **Compliance**: Verify ED25519 acceptance with security frameworks

**Future-Proofing Strategy:**
- **Post-Quantum Preparedness**: Monitor NIST PQC standardization
- **Algorithm Agility**: Design systems for cryptographic algorithm updates
- **Key Rotation**: Implement automated key lifecycle management
- **Quantum Timeline**: Plan migration before cryptographically relevant quantum computers

```bash
# Key Comparison Script with Cryptographic Analysis
#!/bin/bash
# crypto-analysis.sh - Detailed SSH key cryptographic comparison

analyze_key_strength() {
    local key_type=$1
    
    case $key_type in
        ed25519)
            echo "ED25519 Cryptographic Profile:"
            echo "  Mathematical Foundation: Twisted Edwards Curves"
            echo "  Security Assumption: Elliptic Curve Discrete Logarithm Problem"
            echo "  Equivalent Symmetric Security: ~128-bit"
            echo "  Quantum Security: ~64-bit (square root attack)"
            echo "  Side-Channel Resistance: Excellent (constant-time by design)"
            echo "  Implementation Complexity: Low"
            echo "  Standardization: RFC 8032, FIPS 186-5 approved"
            ;;
        rsa)
            echo "RSA-4096 Cryptographic Profile:"
            echo "  Mathematical Foundation: Integer Factorization Problem"
            echo "  Security Assumption: Difficulty of factoring large semiprimes"
            echo "  Equivalent Symmetric Security: ~140-bit"
            echo "  Quantum Security: ~0-bit (Shor's algorithm)"
            echo "  Side-Channel Resistance: Requires careful implementation"
            echo "  Implementation Complexity: High"
            echo "  Standardization: FIPS 186-5, extensive historical validation"
            ;;
    esac
    echo
}

analyze_key_strength ed25519
analyze_key_strength rsa
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

### Comprehensive Enterprise SSH Security Framework

#### Advanced Cryptographic Implementation and Quantum Resistance Preparation
```bash
#!/bin/bash
# Enterprise SSH Security Hardening Framework
# Implements SOC 2, ISO 27001, and NIST Cybersecurity Framework compliance
# Version: 3.0 - Production Ready with Quantum Resistance Preparation

set -euo pipefail

# Configuration Variables
SSHD_CONFIG="/etc/ssh/sshd_config"
SSHD_CONFIG_BACKUP="/etc/ssh/sshd_config.backup.$(date +%Y%m%d_%H%M%S)"
LOG_FILE="/var/log/ssh_hardening.log"
COMPLIANCE_MODE="SOC2"  # Options: SOC2, ISO27001, NIST, HIPAA

# Quantum-Resistant Algorithm Preparation
QR_ALGORITHMS_ENABLED=true
POST_QUANTUM_KEX="sntrup761x25519-sha512@openssh.com"
HYBRID_SIGNATURE_ALGS="ssh-rsa-cert-v01@openssh.com,ecdsa-sha2-nistp256-cert-v01@openssh.com"

# Logging Function
log_action() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

# Backup Current Configuration
backup_ssh_config() {
    log_action "Creating backup of SSH configuration..."
    cp "$SSHD_CONFIG" "$SSHD_CONFIG_BACKUP"
    log_action "Backup created: $SSHD_CONFIG_BACKUP"
}

# Configure Modern and Post-Quantum Cryptographic Algorithms
configure_advanced_crypto() {
    log_action "Configuring advanced cryptographic algorithms with quantum resistance preparation..."
    
    cat >> "$SSHD_CONFIG" << EOF

# === ADVANCED CRYPTOGRAPHIC CONFIGURATION ===
# Modern Key Exchange Algorithms (Post-Quantum Resistant Preparation)
EOF

    if [[ "$QR_ALGORITHMS_ENABLED" == "true" ]]; then
        cat >> "$SSHD_CONFIG" << EOF
# Hybrid Post-Quantum Key Exchange (when available)
KexAlgorithms ${POST_QUANTUM_KEX},curve25519-sha256,curve25519-sha256@libssh.org,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256
EOF
    else
        cat >> "$SSHD_CONFIG" << EOF
# Standard Modern Key Exchange
KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256
EOF
    fi

    cat >> "$SSHD_CONFIG" << EOF

# Host Key Algorithms (Modern, Secure)
HostKeyAlgorithms rsa-sha2-512,rsa-sha2-256,ssh-ed25519,ecdsa-sha2-nistp521,ecdsa-sha2-nistp384,ecdsa-sha2-nistp256

# Ciphers (AES-GCM preferred for authenticated encryption)
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr

# MAC Algorithms (Authenticated Encryption preferred)
MACs umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512

# Certificate Types (Quantum-Resistant Preparation)
PubkeyAcceptedKeyTypes ${HYBRID_SIGNATURE_ALGS},ssh-ed25519,ecdsa-sha2-nistp521,ecdsa-sha2-nistp384,ecdsa-sha2-nistp256,rsa-sha2-512,rsa-sha2-256
EOF

    log_action "Advanced cryptographic algorithms configured with quantum resistance preparation"
}

# Generate Secure Host Keys with Multiple Algorithms
generate_enterprise_host_keys() {
    log_action "Generating enterprise-grade host keys..."
    
    # Remove old host keys
    rm -f /etc/ssh/ssh_host_*
    
    # Generate ED25519 host key (preferred for post-quantum transition)
    ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N "" -C "$(hostname)-ed25519-$(date +%Y%m%d)"
    
    # Generate RSA host key (4096-bit for compatibility and quantum resistance)
    ssh-keygen -t rsa -b 4096 -f /etc/ssh/ssh_host_rsa_key -N "" -C "$(hostname)-rsa4096-$(date +%Y%m%d)"
    
    # Generate ECDSA host key (521-bit curve for maximum security)
    ssh-keygen -t ecdsa -b 521 -f /etc/ssh/ssh_host_ecdsa_key -N "" -C "$(hostname)-ecdsa521-$(date +%Y%m%d)"
    
    # Set proper permissions and ownership
    chmod 600 /etc/ssh/ssh_host_*_key
    chmod 644 /etc/ssh/ssh_host_*_key.pub
    chown root:root /etc/ssh/ssh_host_*
    
    # Generate host key fingerprints for verification
    for key in /etc/ssh/ssh_host_*_key.pub; do
        log_action "Host key fingerprint: $(ssh-keygen -l -f "$key")"
    done
    
    log_action "Enterprise host keys generated successfully"
}

# Enhanced Security Configuration with Compliance Framework
configure_enterprise_security_policies() {
    log_action "Applying enterprise security policies for $COMPLIANCE_MODE compliance..."
    
    cat >> "$SSHD_CONFIG" << EOF

# === ENTERPRISE SECURITY POLICIES ===
# Authentication and Access Control
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys .ssh/authorized_keys2
PermitRootLogin no
AllowUsers sshuser admin devops
DenyUsers root nobody guest
MaxAuthTries 3
MaxSessions 4
MaxStartups 10:30:60
LoginGraceTime 30

# Multi-Factor Authentication Support
AuthenticationMethods publickey,keyboard-interactive:pam
ChallengeResponseAuthentication yes
UsePAM yes

# Network Security
Protocol 2
Port 2222
AddressFamily inet
ListenAddress 0.0.0.0
TCPKeepAlive no
ClientAliveInterval 300
ClientAliveCountMax 2

# Session Security and Restrictions
PermitEmptyPasswords no
PermitUserEnvironment no
AllowAgentForwarding yes
AllowTcpForwarding local
GatewayPorts no
X11Forwarding no
X11UseLocalhost yes
PrintMotd no
PrintLastLog yes
Compression delayed
UseDNS no
PermitTunnel no

# Connection and Performance Limits
MaxAuthTries 3
MaxSessions 10
MaxStartups 10:30:100
LoginGraceTime 30
ClientAliveInterval 300
ClientAliveCountMax 2

# Advanced Security Features
StrictModes yes
IgnoreRhosts yes
IgnoreUserKnownHosts yes
HostbasedAuthentication no
RhostsRSAAuthentication no
PermitTty yes
EOF

    # Apply compliance-specific configurations
    case "$COMPLIANCE_MODE" in
        "SOC2")
            cat >> "$SSHD_CONFIG" << EOF

# === SOC 2 COMPLIANCE SETTINGS ===
LogLevel VERBOSE
SyslogFacility AUTHPRIV
Banner /etc/ssh/soc2_banner
RekeyLimit 1G 1h
FingerprintHash sha256
EOF
            create_compliance_banner "SOC2"
            ;;
        "ISO27001")
            cat >> "$SSHD_CONFIG" << EOF

# === ISO 27001 COMPLIANCE SETTINGS ===
LogLevel INFO
SyslogFacility AUTH
Banner /etc/ssh/iso27001_banner
DebianBanner no
RekeyLimit 512M 30m
FingerprintHash sha256
EOF
            create_compliance_banner "ISO27001"
            ;;
        "NIST")
            cat >> "$SSHD_CONFIG" << EOF

# === NIST CYBERSECURITY FRAMEWORK SETTINGS ===
LogLevel VERBOSE
SyslogFacility AUTHPRIV
Banner /etc/ssh/nist_banner
FingerprintHash sha256
RekeyLimit 1G 1h
DisableForwarding no
EOF
            create_compliance_banner "NIST"
            ;;
        "HIPAA")
            cat >> "$SSHD_CONFIG" << EOF

# === HIPAA COMPLIANCE SETTINGS ===
LogLevel VERBOSE
SyslogFacility AUTHPRIV
Banner /etc/ssh/hipaa_banner
RekeyLimit 512M 15m
FingerprintHash sha256
AllowTcpForwarding no
AllowAgentForwarding no
X11Forwarding no
EOF
            create_compliance_banner "HIPAA"
            ;;
    esac
    
    log_action "Enterprise security policies applied for $COMPLIANCE_MODE compliance"
}

# Create compliance-specific login banners
create_compliance_banner() {
    local framework="$1"
    local banner_file="/etc/ssh/${framework,,}_banner"
    
    case "$framework" in
        "SOC2")
            cat > "$banner_file" << 'EOF'
********************************************************************************
                           AUTHORIZED ACCESS ONLY
                          SOC 2 COMPLIANT ENVIRONMENT
********************************************************************************

This system is for authorized users only. All activities may be monitored
and recorded. By accessing this system, you consent to monitoring and agree
to comply with all applicable security policies and procedures.

Unauthorized access is strictly prohibited and may result in prosecution
to the full extent of the law.

All connections are logged and monitored for compliance purposes.
********************************************************************************
EOF
            ;;
        "ISO27001")
            cat > "$banner_file" << 'EOF'
********************************************************************************
                           AUTHORIZED ACCESS ONLY
                        ISO 27001 COMPLIANT ENVIRONMENT
********************************************************************************

This information system is provided for authorized use only. Usage may be
monitored, recorded, and subject to audit. Unauthorized use is prohibited
and may result in criminal and civil penalties.

Information Security Management System (ISMS) controls are in effect.
All activities are subject to security monitoring and compliance auditing.
********************************************************************************
EOF
            ;;
        "NIST")
            cat > "$banner_file" << 'EOF'
********************************************************************************
                           AUTHORIZED ACCESS ONLY
                  NIST CYBERSECURITY FRAMEWORK ENVIRONMENT
********************************************************************************

This system implements NIST Cybersecurity Framework controls. Access is
restricted to authorized personnel only. All activities are monitored,
logged, and may be audited for security and compliance purposes.

Unauthorized access attempts will be prosecuted to the full extent of the law.
By continuing, you acknowledge compliance with all security policies.
********************************************************************************
EOF
            ;;
        "HIPAA")
            cat > "$banner_file" << 'EOF'
********************************************************************************
                           AUTHORIZED ACCESS ONLY
                         HIPAA COMPLIANT ENVIRONMENT
********************************************************************************

This system contains Protected Health Information (PHI) and is subject to
HIPAA Security Rule requirements. Access is restricted to authorized
individuals with legitimate business need.

All activities are monitored, logged, and audited for HIPAA compliance.
Unauthorized access is strictly prohibited and may result in civil and
criminal penalties under HIPAA regulations.
********************************************************************************
EOF
            ;;
    esac
    
    chmod 644 "$banner_file"
    log_action "Compliance banner created: $banner_file"
}

# Performance Optimization with Security Focus
optimize_enterprise_performance() {
    log_action "Applying enterprise performance optimizations..."
    
    cat >> "$SSHD_CONFIG" << EOF

# === ENTERPRISE PERFORMANCE OPTIMIZATION ===
# Connection Multiplexing and Resource Management
MaxSessions 10
MaxStartups 10:30:100

# Compression Settings (Security vs Performance Balance)
Compression delayed

# Keep-Alive Optimization (Security-focused)
TCPKeepAlive no
ClientAliveInterval 300
ClientAliveCountMax 2

# DNS and Network Optimization
UseDNS no
AddressFamily inet

# Process and Resource Limits
UsePrivilegeSeparation sandbox
ChrootDirectory none

# Subsystem Configuration
Subsystem sftp internal-sftp
EOF

    log_action "Enterprise performance optimizations applied"
}

# Comprehensive Monitoring and Alerting Setup
setup_enterprise_monitoring() {
    log_action "Setting up comprehensive SSH monitoring and alerting..."
    
    # Create comprehensive SSH monitoring script
    cat > /usr/local/bin/ssh_enterprise_monitor.sh << 'EOF'
#!/bin/bash
# Enterprise SSH Connection Monitoring and Alerting System
# Supports multiple compliance frameworks and advanced threat detection

set -euo pipefail

LOG_FILE="/var/log/ssh_enterprise_monitor.log"
ALERT_LOG="/var/log/ssh_alerts.log"
METRICS_LOG="/var/log/ssh_metrics.log"
CONFIG_FILE="/etc/ssh/monitoring.conf"

# Default thresholds (can be overridden in config file)
CONN_THRESHOLD=20
FAILED_AUTH_THRESHOLD=10
FAILED_AUTH_TIME_WINDOW=3600  # 1 hour
BRUTE_FORCE_THRESHOLD=5
BRUTE_FORCE_TIME_WINDOW=300   # 5 minutes
ANOMALY_DETECTION_ENABLED=true

# Load configuration if exists
[[ -f "$CONFIG_FILE" ]] && source "$CONFIG_FILE"

# Logging function
log_event() {
    local level="$1"
    local message="$2"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    echo "[$timestamp] [$level] $message" | tee -a "$LOG_FILE"
    
    if [[ "$level" == "ALERT" || "$level" == "CRITICAL" ]]; then
        echo "[$timestamp] [$level] $message" >> "$ALERT_LOG"
        # Send to syslog for SIEM integration
        logger -p auth.warning "SSH_MONITOR: [$level] $message"
    fi
}

# Monitor active SSH connections
monitor_ssh_connections() {
    local current_connections
    current_connections=$(ss -tn state established '( dport = :2222 or sport = :2222 )' | grep -c "^ESTAB" || true)
    
    # Log metrics
    echo "$(date '+%Y-%m-%d %H:%M:%S'),connections,$current_connections" >> "$METRICS_LOG"
    
    log_event "INFO" "Active SSH connections: $current_connections"
    
    # Alert if threshold exceeded
    if [[ "$current_connections" -gt "$CONN_THRESHOLD" ]]; then
        log_event "ALERT" "Active SSH connections ($current_connections) exceed threshold ($CONN_THRESHOLD)"
        send_alert "connection_threshold" "Active connections: $current_connections"
    fi
}

# Monitor failed authentication attempts
monitor_failed_auth() {
    local failed_attempts
    local time_window_start
    
    time_window_start=$(date -d "$FAILED_AUTH_TIME_WINDOW seconds ago" '+%Y-%m-%d %H:%M:%S')
    
    # Count failed attempts in time window
    failed_attempts=$(journalctl --since "$time_window_start" -u sshd | 
                     grep -c "Failed password\|Failed publickey\|Invalid user" || true)
    
    # Log metrics
    echo "$(date '+%Y-%m-%d %H:%M:%S'),failed_auth,$failed_attempts" >> "$METRICS_LOG"
    
    log_event "INFO" "Failed authentication attempts in last hour: $failed_attempts"
    
    if [[ "$failed_attempts" -gt "$FAILED_AUTH_THRESHOLD" ]]; then
        log_event "ALERT" "Failed authentication attempts ($failed_attempts) exceed threshold ($FAILED_AUTH_THRESHOLD)"
        send_alert "failed_auth_threshold" "Failed attempts: $failed_attempts"
    fi
}

# Brute force detection
detect_brute_force() {
    local time_window_start
    local brute_force_ips
    
    time_window_start=$(date -d "$BRUTE_FORCE_TIME_WINDOW seconds ago" '+%Y-%m-%d %H:%M:%S')
    
    # Detect IPs with multiple failed attempts
    brute_force_ips=$(journalctl --since "$time_window_start" -u sshd | 
                     grep "Failed password\|Failed publickey" | 
                     awk '{print $(NF-3)}' | sort | uniq -c | 
                     awk -v threshold="$BRUTE_FORCE_THRESHOLD" '$1 >= threshold {print $2}')
    
    if [[ -n "$brute_force_ips" ]]; then
        while IFS= read -r ip; do
            log_event "CRITICAL" "Brute force attack detected from IP: $ip"
            send_alert "brute_force_attack" "Source IP: $ip"
            
            # Auto-block if fail2ban is not running
            if ! systemctl is-active --quiet fail2ban; then
                iptables -A INPUT -s "$ip" -j DROP
                log_event "INFO" "Auto-blocked IP: $ip"
            fi
        done <<< "$brute_force_ips"
    fi
}

# Anomaly detection (basic behavioral analysis)
detect_anomalies() {
    if [[ "$ANOMALY_DETECTION_ENABLED" != "true" ]]; then
        return 0
    fi
    
    local current_hour
    local typical_connections
    local current_connections
    
    current_hour=$(date '+%H')
    current_connections=$(ss -tn state established '( dport = :2222 or sport = :2222 )' | grep -c "^ESTAB" || true)
    
    # Calculate typical connections for this hour (last 7 days average)
    typical_connections=$(grep ",$current_hour:.*,connections," "$METRICS_LOG" | 
                         tail -7 | awk -F',' '{sum+=$3} END {print int(sum/NR)}' || echo "0")
    
    # Alert if current connections are significantly higher than typical
    if [[ "$typical_connections" -gt 0 ]] && [[ "$current_connections" -gt $((typical_connections * 3)) ]]; then
        log_event "ALERT" "Anomaly detected: Current connections ($current_connections) significantly exceed typical ($typical_connections)"
        send_alert "anomaly_detection" "Current: $current_connections, Typical: $typical_connections"
    fi
}

# Send alerts (customize for your alerting system)
send_alert() {
    local alert_type="$1"
    local details="$2"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Email alert (requires mailutils)
    if command -v mail >/dev/null 2>&1; then
        echo "SSH Security Alert: $alert_type at $timestamp. Details: $details" | 
        mail -s "SSH Security Alert: $alert_type" security@example.com
    fi
    
    # Slack/Teams webhook (customize URL)
    if [[ -n "${SLACK_WEBHOOK_URL:-}" ]]; then
        curl -X POST -H 'Content-type: application/json' \
             --data "{\"text\":\"SSH Security Alert: $alert_type\\nTime: $timestamp\\nDetails: $details\"}" \
             "$SLACK_WEBHOOK_URL" >/dev/null 2>&1 || true
    fi
    
    # SNMP trap (customize for your monitoring system)
    if command -v snmptrap >/dev/null 2>&1; then
        snmptrap -v2c -c public localhost '' 1.3.6.1.4.1.8072.2.3.0.1 \
                 1.3.6.1.4.1.8072.2.3.2.1 s "$alert_type: $details" >/dev/null 2>&1 || true
    fi
}

# Generate compliance report
generate_compliance_report() {
    local report_file="/var/log/ssh_compliance_report_$(date +%Y%m%d).txt"
    
    cat > "$report_file" << EOF
SSH Compliance Monitoring Report
Generated: $(date)
Monitoring Period: Last 24 hours

=== CONNECTION METRICS ===
Total Connections Today: $(grep "$(date +%Y-%m-%d)" "$METRICS_LOG" | grep "connections" | wc -l)
Peak Connections: $(grep "$(date +%Y-%m-%d)" "$METRICS_LOG" | grep "connections" | awk -F',' '{print $3}' | sort -n | tail -1)
Average Connections: $(grep "$(date +%Y-%m-%d)" "$METRICS_LOG" | grep "connections" | awk -F',' '{sum+=$3; count++} END {print int(sum/count)}')

=== SECURITY EVENTS ===
Failed Authentication Attempts: $(grep "$(date +%Y-%m-%d)" "$LOG_FILE" | grep -c "Failed authentication" || echo "0")
Brute Force Attempts: $(grep "$(date +%Y-%m-%d)" "$ALERT_LOG" | grep -c "Brute force" || echo "0")
Anomalies Detected: $(grep "$(date +%Y-%m-%d)" "$ALERT_LOG" | grep -c "Anomaly detected" || echo "0")

=== COMPLIANCE STATUS ===
Monitoring System: Active
Alert System: Active
Log Retention: $(find /var/log -name "ssh_*" -mtime -30 | wc -l) files (last 30 days)
Configuration Compliance: $(sshd -t && echo "PASS" || echo "FAIL")

=== RECOMMENDATIONS ===
EOF

    # Add recommendations based on findings
    local failed_auth_count
    failed_auth_count=$(grep "$(date +%Y-%m-%d)" "$LOG_FILE" | grep -c "Failed authentication" || echo "0")
    
    if [[ "$failed_auth_count" -gt 50 ]]; then
        echo "- Consider implementing additional brute force protection" >> "$report_file"
    fi
    
    if [[ ! -f /etc/fail2ban/jail.local ]]; then
        echo "- Consider implementing fail2ban for automated threat response" >> "$report_file"
    fi
    
    echo "- Regular security configuration review recommended" >> "$report_file"
    echo "- Ensure log monitoring integration with SIEM systems" >> "$report_file"
    
    log_event "INFO" "Compliance report generated: $report_file"
}

# Main monitoring function
main() {
    log_event "INFO" "Starting SSH enterprise monitoring cycle"
    
    monitor_ssh_connections
    monitor_failed_auth
    detect_brute_force
    detect_anomalies
    
    # Generate daily compliance report at 6 AM
    if [[ "$(date +%H)" == "06" ]] && [[ "$(date +%M)" -lt 5 ]]; then
        generate_compliance_report
    fi
    
    log_event "INFO" "SSH enterprise monitoring cycle completed"
}

# Execute main function
main "$@"
EOF

    chmod +x /usr/local/bin/ssh_enterprise_monitor.sh
    
    # Create monitoring configuration file
    cat > /etc/ssh/monitoring.conf << 'EOF'
# SSH Enterprise Monitoring Configuration

# Connection thresholds
CONN_THRESHOLD=25
FAILED_AUTH_THRESHOLD=15
FAILED_AUTH_TIME_WINDOW=3600

# Brute force detection
BRUTE_FORCE_THRESHOLD=5
BRUTE_FORCE_TIME_WINDOW=300

# Anomaly detection
ANOMALY_DETECTION_ENABLED=true

# Alert configuration
SLACK_WEBHOOK_URL=""
EMAIL_RECIPIENTS="security@example.com"

# Compliance settings
RETENTION_DAYS=90
REPORT_FREQUENCY="daily"
EOF

    # Add to crontab for regular monitoring (every 5 minutes)
    (crontab -l 2>/dev/null; echo "*/5 * * * * /usr/local/bin/ssh_enterprise_monitor.sh") | crontab -
    
    # Add log rotation configuration
    cat > /etc/logrotate.d/ssh-enterprise << 'EOF'
/var/log/ssh_enterprise_monitor.log /var/log/ssh_alerts.log /var/log/ssh_metrics.log {
    daily
    rotate 90
    compress
    delaycompress
    missingok
    notifempty
    copytruncate
    postrotate
        /bin/systemctl reload rsyslog > /dev/null 2>&1 || true
    endscript
}
EOF
    
    log_action "Enterprise SSH monitoring and alerting configured"
}

# Configuration validation with comprehensive checks
validate_enterprise_config() {
    log_action "Performing comprehensive SSH configuration validation..."
    
    local validation_errors=0
    local validation_warnings=0
    
    # Syntax validation
    if ! sshd -t -f "$SSHD_CONFIG" 2>/dev/null; then
        log_action "ERROR: SSH configuration syntax validation failed"
        sshd -t -f "$SSHD_CONFIG"
        ((validation_errors++))
    else
        log_action "✓ SSH configuration syntax validation passed"
    fi
    
    # Security configuration validation
    local required_settings=(
        "PasswordAuthentication no"
        "PermitRootLogin no"
        "Protocol 2"
        "MaxAuthTries 3"
    )
    
    for setting in "${required_settings[@]}"; do
        if ! grep -q "^${setting}$" "$SSHD_CONFIG"; then
            log_action "WARNING: Required security setting not found: $setting"
            ((validation_warnings++))
        else
            log_action "✓ Security setting validated: $setting"
        fi
    done
    
    # Algorithm strength validation
    if grep -q "ssh-rsa" "$SSHD_CONFIG" && ! grep -q "rsa-sha2" "$SSHD_CONFIG"; then
        log_action "WARNING: Legacy RSA algorithms detected, consider RSA-SHA2"
        ((validation_warnings++))
    fi
    
    # Compliance-specific validation
    case "$COMPLIANCE_MODE" in
        "SOC2"|"HIPAA")
            if ! grep -q "LogLevel VERBOSE" "$SSHD_CONFIG"; then
                log_action "WARNING: $COMPLIANCE_MODE requires VERBOSE logging"
                ((validation_warnings++))
            fi
            ;;
    esac
    
    # Host key validation
    for key_file in /etc/ssh/ssh_host_*_key; do
        if [[ -f "$key_file" ]]; then
            local key_perms
            key_perms=$(stat -c %a "$key_file")
            if [[ "$key_perms" != "600" ]]; then
                log_action "ERROR: Incorrect permissions on $key_file: $key_perms (should be 600)"
                ((validation_errors++))
            else
                log_action "✓ Host key permissions validated: $key_file"
            fi
        fi
    done
    
    # Report validation results
    log_action "Validation completed: $validation_errors errors, $validation_warnings warnings"
    
    if [[ "$validation_errors" -eq 0 ]]; then
        return 0
    else
        log_action "Configuration validation failed with $validation_errors errors"
        return 1
    fi
}

# Main execution function
main() {
    log_action "Starting Enterprise SSH Security Hardening Process..."
    log_action "Compliance mode: $COMPLIANCE_MODE"
    log_action "Quantum resistance preparation: $QR_ALGORITHMS_ENABLED"
    
    # Check if running as root
    if [[ $EUID -ne 0 ]]; then
        echo "This script must be run as root" >&2
        exit 1
    fi
    
    # Create log directory
    mkdir -p "$(dirname "$LOG_FILE")"
    
    # Execute hardening steps
    backup_ssh_config
    configure_advanced_crypto
    generate_enterprise_host_keys
    configure_enterprise_security_policies
    optimize_enterprise_performance
    setup_enterprise_monitoring
    
    if validate_enterprise_config; then
        log_action "Restarting SSH service..."
        systemctl restart sshd
        systemctl enable sshd
        
        # Verify service status
        if systemctl is-active --quiet sshd; then
            log_action "✓ SSH service restarted successfully"
        else
            log_action "ERROR: SSH service failed to start"
            log_action "Restoring backup configuration..."
            cp "$SSHD_CONFIG_BACKUP" "$SSHD_CONFIG"
            systemctl restart sshd
            exit 1
        fi
        
        log_action "SSH Enterprise hardening completed successfully!"
        log_action "New SSH port: 2222"
        log_action "Test connection: ssh -p 2222 user@$(hostname -I | awk '{print $1}')"
        log_action "Monitoring enabled: /usr/local/bin/ssh_enterprise_monitor.sh"
        log_action "Configuration backup: $SSHD_CONFIG_BACKUP"
        
        # Display summary
        echo
        echo "=== Enterprise SSH Hardening Summary ==="
        echo "Compliance Framework: $COMPLIANCE_MODE"
        echo "Quantum Resistance: $QR_ALGORITHMS_ENABLED"
        echo "SSH Port: 2222"
        echo "Host Keys Generated: ED25519, RSA-4096, ECDSA-521"
        echo "Monitoring: Enabled (5-minute intervals)"
        echo "Backup Location: $SSHD_CONFIG_BACKUP"
        echo "Log File: $LOG_FILE"
        echo "========================================="
        
    else
        log_action "SSH enterprise hardening failed during validation"
        exit 1
    fi
}

# Handle script interruption gracefully
trap 'log_action "Script interrupted, restoring backup..."; cp "$SSHD_CONFIG_BACKUP" "$SSHD_CONFIG" 2>/dev/null || true; exit 1' INT TERM

# Execute main function with all arguments
main "$@"
```

#### Enterprise SSH Certificate Authority Implementation
```bash
#!/bin/bash
# Enterprise SSH Certificate Authority (CA) Implementation
# Production-ready SSH certificate management system with HSM support
# Supports multiple certificate types and enterprise workflows

set -euo pipefail

# Configuration
CA_DIR="/etc/ssh/ca"
CA_KEY="$CA_DIR/ssh_ca"
CA_CERT="$CA_DIR/ssh_ca.pub"
USER_CA_KEY="$CA_DIR/ssh_user_ca"
USER_CA_CERT="$CA_DIR/ssh_user_ca.pub"
HOST_CA_KEY="$CA_DIR/ssh_host_ca"
HOST_CA_CERT="$CA_DIR/ssh_host_ca.pub"

# Certificate settings
DEFAULT_USER_VALIDITY="52w"  # 1 year
DEFAULT_HOST_VALIDITY="104w" # 2 years
SHORT_TERM_VALIDITY="1d"     # 1 day for temporary access

# Directories
ISSUED_DIR="$CA_DIR/issued"
REVOKED_DIR="$CA_DIR/revoked"
REQUESTS_DIR="$CA_DIR/requests"
TEMPLATES_DIR="$CA_DIR/templates"
AUDIT_DIR="$CA_DIR/audit"

# Logging
LOG_FILE="/var/log/ssh_ca.log"
AUDIT_LOG="/var/log/ssh_ca_audit.log"

# HSM Configuration (optional)
HSM_ENABLED=false
HSM_PKCS11_MODULE="/usr/lib/opensc-pkcs11.so"
HSM_TOKEN_LABEL="SSH_CA_Token"

# Logging function
log_action() {
    local level="$1"
    local message="$2"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    echo "[$timestamp] [$level] $message" | tee -a "$LOG_FILE"
    
    # Audit log for sensitive operations
    if [[ "$level" == "AUDIT" ]]; then
        echo "[$timestamp] $message" >> "$AUDIT_LOG"
    fi
}

# Initialize SSH Certificate Authority
initialize_ca() {
    log_action "INFO" "Initializing SSH Certificate Authority..."
    
    # Create directory structure
    mkdir -p "$CA_DIR"/{issued/{user,host},revoked/{user,host},requests/{user,host},templates,audit,backup}
    chmod 700 "$CA_DIR"
    chmod 750 "$CA_DIR"/{issued,revoked,requests,templates,audit}
    
    # Initialize audit tracking
    echo "# SSH CA Audit Log - Initialized $(date)" > "$AUDIT_LOG"
    chmod 600 "$AUDIT_LOG"
    
    if [[ "$HSM_ENABLED" == "true" ]]; then
        initialize_hsm_ca
    else
        initialize_software_ca
    fi
    
    # Create certificate templates
    create_certificate_templates
    
    # Initialize revocation list
    touch "$CA_DIR/revoked_keys"
    chmod 644 "$CA_DIR/revoked_keys"
    
    log_action "AUDIT" "SSH CA initialized successfully"
    echo "SSH Certificate Authority initialized successfully"
    echo "User CA public key: $USER_CA_CERT"
    echo "Host CA public key: $HOST_CA_CERT"
}

# Initialize software-based CA
initialize_software_ca() {
    log_action "INFO" "Initializing software-based CA keys..."
    
    # Generate User CA key pair
    ssh-keygen -t ed25519 -f "$USER_CA_KEY" -N "" -C "SSH-User-CA-$(hostname)-$(date +%Y%m%d)"
    chmod 600 "$USER_CA_KEY"
    chmod 644 "$USER_CA_CERT"
    
    # Generate Host CA key pair  
    ssh-keygen -t ed25519 -f "$HOST_CA_KEY" -N "" -C "SSH-Host-CA-$(hostname)-$(date +%Y%m%d)"
    chmod 600 "$HOST_CA_KEY"
    chmod 644 "$HOST_CA_CERT"
    
    log_action "INFO" "Software CA keys generated successfully"
}

# Initialize HSM-based CA (requires PKCS#11)
initialize_hsm_ca() {
    log_action "INFO" "Initializing HSM-based CA keys..."
    
    if ! command -v pkcs11-tool >/dev/null 2>&1; then
        log_action "ERROR" "pkcs11-tool not found. Install opensc package."
        exit 1
    fi
    
    # This is a simplified example - real HSM integration requires detailed configuration
    log_action "WARNING" "HSM integration requires manual configuration"
    log_action "INFO" "Please configure PKCS#11 module: $HSM_PKCS11_MODULE"
    log_action "INFO" "Token label: $HSM_TOKEN_LABEL"
    
    # Fallback to software keys for this example
    initialize_software_ca
}

# Create certificate templates for different use cases
create_certificate_templates() {
    log_action "INFO" "Creating certificate templates..."
    
    # Admin template
    cat > "$TEMPLATES_DIR/admin.template" << 'EOF'
# Admin Certificate Template
VALIDITY="52w"
PRINCIPALS="admin,root,sudo"
PERMISSIONS="permit-X11-forwarding,permit-agent-forwarding,permit-port-forwarding,permit-pty,permit-user-rc"
FORCE_COMMAND=""
SOURCE_ADDRESS=""
EXTENSIONS="permit-X11-forwarding,permit-agent-forwarding,permit-port-forwarding,permit-pty,permit-user-rc"
EOF

    # Developer template
    cat > "$TEMPLATES_DIR/developer.template" << 'EOF'
# Developer Certificate Template
VALIDITY="26w"
PRINCIPALS="developer,dev,deploy"
PERMISSIONS="permit-pty,permit-user-rc"
FORCE_COMMAND=""
SOURCE_ADDRESS=""
EXTENSIONS="permit-pty,permit-user-rc"
EOF

    # Service account template
    cat > "$TEMPLATES_DIR/service.template" << 'EOF'
# Service Account Certificate Template
VALIDITY="8w"
PRINCIPALS="service,automation"
PERMISSIONS="permit-pty"
FORCE_COMMAND="/opt/scripts/service-wrapper.sh"
SOURCE_ADDRESS=""
EXTENSIONS="permit-pty"
EOF

    # Temporary access template
    cat > "$TEMPLATES_DIR/temporary.template" << 'EOF'
# Temporary Access Certificate Template
VALIDITY="8h"
PRINCIPALS="temp,contractor"
PERMISSIONS="permit-pty"
FORCE_COMMAND=""
SOURCE_ADDRESS="192.168.1.0/24"
EXTENSIONS="permit-pty"
EOF

    # Host certificate template
    cat > "$TEMPLATES_DIR/host.template" << 'EOF'
# Host Certificate Template
VALIDITY="104w"
PRINCIPALS=""
PERMISSIONS=""
FORCE_COMMAND=""
SOURCE_ADDRESS=""
EXTENSIONS=""
EOF

    log_action "INFO" "Certificate templates created"
}

# Sign user certificate
sign_user_certificate() {
    local username="$1"
    local public_key_file="$2"
    local template="${3:-developer}"
    local custom_principals="$4"
    local custom_validity="$5"
    
    log_action "INFO" "Signing user certificate for: $username (template: $template)"
    
    # Validate inputs
    if [[ ! -f "$public_key_file" ]]; then
        log_action "ERROR" "Public key file not found: $public_key_file"
        return 1
    fi
    
    if [[ ! -f "$TEMPLATES_DIR/$template.template" ]]; then
        log_action "ERROR" "Certificate template not found: $template"
        return 1
    fi
    
    # Load template
    source "$TEMPLATES_DIR/$template.template"
    
    # Override with custom values if provided
    [[ -n "$custom_principals" ]] && PRINCIPALS="$custom_principals"
    [[ -n "$custom_validity" ]] && VALIDITY="$custom_validity"
    
    # Generate certificate serial number
    local serial=$(date +%s)
    local cert_id="$username-$(date +%Y%m%d%H%M%S)"
    local signed_cert="$ISSUED_DIR/user/${username}-${serial}.cert"
    
    # Prepare signing command
    local sign_cmd="ssh-keygen -s $USER_CA_KEY -I $cert_id -n $PRINCIPALS -V +$VALIDITY -z $serial"
    
    # Add extensions if specified
    if [[ -n "$EXTENSIONS" ]]; then
        sign_cmd="$sign_cmd -O $EXTENSIONS"
    fi
    
    # Add force command if specified
    if [[ -n "$FORCE_COMMAND" ]]; then
        sign_cmd="$sign_cmd -O force-command=$FORCE_COMMAND"
    fi
    
    # Add source address restriction if specified
    if [[ -n "$SOURCE_ADDRESS" ]]; then
        sign_cmd="$sign_cmd -O source-address=$SOURCE_ADDRESS"
    fi
    
    # Sign the certificate
    cp "$public_key_file" "/tmp/${username}_temp_key.pub"
    $sign_cmd "/tmp/${username}_temp_key.pub"
    
    # Move to issued directory
    mv "/tmp/${username}_temp_key-cert.pub" "$signed_cert"
    rm "/tmp/${username}_temp_key.pub"
    
    # Create certificate metadata
    cat > "$signed_cert.meta" << EOF
Certificate ID: $cert_id
Username: $username
Template: $template
Serial: $serial
Issued: $(date)
Validity: $VALIDITY
Principals: $PRINCIPALS
Extensions: $EXTENSIONS
Force Command: $FORCE_COMMAND
Source Address: $SOURCE_ADDRESS
CA Key: $USER_CA_KEY
Issued By: $(whoami)@$(hostname)
EOF
    
    log_action "AUDIT" "User certificate issued - User: $username, Serial: $serial, Template: $template, Principals: $PRINCIPALS"
    
    echo "Certificate signed successfully: $signed_cert"
    echo "Certificate details:"
    ssh-keygen -L -f "$signed_cert"
}

# Sign host certificate
sign_host_certificate() {
    local hostname="$1"
    local public_key_file="$2"
    local host_principals="$3"
    local validity="${4:-$DEFAULT_HOST_VALIDITY}"
    
    log_action "INFO" "Signing host certificate for: $hostname"
    
    # Validate inputs
    if [[ ! -f "$public_key_file" ]]; then
        log_action "ERROR" "Host public key file not found: $public_key_file"
        return 1
    fi
    
    # Default principals if not specified
    if [[ -z "$host_principals" ]]; then
        host_principals="$hostname,$(hostname -f),$(hostname -I | tr -d ' \n')"
    fi
    
    # Generate certificate serial number
    local serial=$(date +%s)
    local cert_id="$hostname-$(date +%Y%m%d%H%M%S)"
    local signed_cert="$ISSUED_DIR/host/${hostname}-${serial}.cert"
    
    # Sign the host certificate
    cp "$public_key_file" "/tmp/${hostname}_temp_key.pub"
    ssh-keygen -s "$HOST_CA_KEY" \
        -I "$cert_id" \
        -h \
        -n "$host_principals" \
        -V "+$validity" \
        -z "$serial" \
        "/tmp/${hostname}_temp_key.pub"
    
    # Move to issued directory
    mv "/tmp/${hostname}_temp_key-cert.pub" "$signed_cert"
    rm "/tmp/${hostname}_temp_key.pub"
    
    # Create certificate metadata
    cat > "$signed_cert.meta" << EOF
Certificate ID: $cert_id
Hostname: $hostname
Serial: $serial
Issued: $(date)
Validity: $validity
Principals: $host_principals
CA Key: $HOST_CA_KEY
Issued By: $(whoami)@$(hostname)
EOF
    
    log_action "AUDIT" "Host certificate issued - Host: $hostname, Serial: $serial, Principals: $host_principals"
    
    echo "Host certificate signed successfully: $signed_cert"
    echo "Certificate details:"
    ssh-keygen -L -f "$signed_cert"
}

# Configure server to trust CA
configure_server_trust() {
    local sshd_config="/etc/ssh/sshd_config"
    local backup_config="/etc/ssh/sshd_config.backup.ca.$(date +%Y%m%d_%H%M%S)"
    
    log_action "INFO" "Configuring server to trust SSH CA..."
    
    # Backup current configuration
    cp "$sshd_config" "$backup_config"
    
    # Remove existing CA configuration
    sed -i '/^TrustedUserCAKeys\|^HostCertificate\|^AuthorizedPrincipalsFile/d' "$sshd_config"
    
    # Add CA trust configuration
    cat >> "$sshd_config" << EOF

# === SSH CERTIFICATE AUTHORITY CONFIGURATION ===
# Trust user certificates signed by our CA
TrustedUserCAKeys $USER_CA_CERT

# Use host certificate for this server
HostCertificate /etc/ssh/ssh_host_ed25519_key-cert.pub

# Principal-based authorization
AuthorizedPrincipalsFile /etc/ssh/auth_principals/%u

# Certificate revocation list
RevokedKeys $CA_DIR/revoked_keys
EOF
    
    # Create principals directory
    mkdir -p /etc/ssh/auth_principals
    chmod 755 /etc/ssh/auth_principals
    
    # Test configuration
    if sshd -t -f "$sshd_config"; then
        log_action "INFO" "SSH configuration test passed"
        systemctl restart sshd
        log_action "AUDIT" "Server configured to trust SSH CA"
        echo "Server configured to trust SSH CA successfully"
    else
        log_action "ERROR" "SSH configuration test failed, restoring backup"
        cp "$backup_config" "$sshd_config"
        return 1
    fi
}

# Create user principals file
create_user_principals() {
    local username="$1"
    local principals="$2"
    
    local principals_file="/etc/ssh/auth_principals/$username"
    
    echo "$principals" | tr ',' '\n' > "$principals_file"
    chmod 644 "$principals_file"
    
    log_action "INFO" "Created principals file for user: $username"
    log_action "AUDIT" "User principals created - User: $username, Principals: $principals"
}

# Revoke certificate
revoke_certificate() {
    local cert_file="$1"
    local reason="${2:-unspecified}"
    
    log_action "INFO" "Revoking certificate: $cert_file"
    
    if [[ ! -f "$cert_file" ]]; then
        log_action "ERROR" "Certificate file not found: $cert_file"
        return 1
    fi
    
    # Extract public key from certificate and add to revocation list
    ssh-keygen -L -f "$cert_file" | grep "Public key:" | cut -d' ' -f3- >> "$CA_DIR/revoked_keys"
    
    # Move certificate to revoked directory
    local cert_basename=$(basename "$cert_file")
    local revoked_cert="$REVOKED_DIR/${cert_basename%.cert}.revoked.$(date +%Y%m%d%H%M%S)"
    mv "$cert_file" "$revoked_cert"
    
    # Move metadata if exists
    if [[ -f "$cert_file.meta" ]]; then
        mv "$cert_file.meta" "$revoked_cert.meta"
        echo "Revocation Date: $(date)" >> "$revoked_cert.meta"
        echo "Revocation Reason: $reason" >> "$revoked_cert.meta"
    fi
    
    log_action "AUDIT" "Certificate revoked - File: $cert_file, Reason: $reason"
    
    # Reload SSH configuration to update revocation list
    systemctl reload sshd
    
    echo "Certificate revoked successfully: $revoked_cert"
}

# List issued certificates
list_certificates() {
    local cert_type="${1:-all}"  # user, host, or all
    
    echo "=== SSH Certificate Authority - Issued Certificates ==="
    echo "CA Directory: $CA_DIR"
    echo "Generated: $(date)"
    echo
    
    case "$cert_type" in
        "user"|"all")
            echo "--- User Certificates ---"
            for cert in "$ISSUED_DIR/user"/*.cert; do
                if [[ -f "$cert" ]]; then
                    echo "Certificate: $(basename "$cert")"
                    if [[ -f "$cert.meta" ]]; then
                        grep -E "Username:|Issued:|Validity:|Principals:" "$cert.meta" | sed 's/^/  /'
                    fi
                    ssh-keygen -L -f "$cert" | grep -E "Valid:|Principals:|Critical Options:|Extensions:" | sed 's/^/  /'
                    echo
                fi
            done
            ;;
    esac
    
    case "$cert_type" in
        "host"|"all")
            echo "--- Host Certificates ---"
            for cert in "$ISSUED_DIR/host"/*.cert; do
                if [[ -f "$cert" ]]; then
                    echo "Certificate: $(basename "$cert")"
                    if [[ -f "$cert.meta" ]]; then
                        grep -E "Hostname:|Issued:|Validity:|Principals:" "$cert.meta" | sed 's/^/  /'
                    fi
                    ssh-keygen -L -f "$cert" | grep -E "Valid:|Principals:|Critical Options:|Extensions:" | sed 's/^/  /'
                    echo
                fi
            done
            ;;
    esac
}

# Generate CA status report
generate_ca_report() {
    local report_file="/tmp/ssh_ca_report_$(date +%Y%m%d).txt"
    
    cat > "$report_file" << EOF
SSH Certificate Authority Status Report
Generated: $(date)
CA Directory: $CA_DIR

=== CA CONFIGURATION ===
User CA Public Key: $USER_CA_CERT
Host CA Public Key: $HOST_CA_CERT
HSM Enabled: $HSM_ENABLED

=== CERTIFICATE STATISTICS ===
Total User Certificates Issued: $(find "$ISSUED_DIR/user" -name "*.cert" 2>/dev/null | wc -l)
Total Host Certificates Issued: $(find "$ISSUED_DIR/host" -name "*.cert" 2>/dev/null | wc -l)
Total Revoked Certificates: $(find "$REVOKED_DIR" -name "*.revoked.*" 2>/dev/null | wc -l)

=== RECENT ACTIVITY (Last 7 Days) ===
Recent Issuances: $(find "$ISSUED_DIR" -name "*.cert" -mtime -7 2>/dev/null | wc -l)
Recent Revocations: $(find "$REVOKED_DIR" -name "*.revoked.*" -mtime -7 2>/dev/null | wc -l)

=== EXPIRING CERTIFICATES (Next 30 Days) ===
EOF

    # Check for expiring certificates
    local expiring_count=0
    for cert in "$ISSUED_DIR"/*/*.cert; do
        if [[ -f "$cert" ]]; then
            local valid_until
            valid_until=$(ssh-keygen -L -f "$cert" | grep "Valid:" | awk '{print $4}')
            if [[ -n "$valid_until" ]]; then
                local exp_timestamp
                exp_timestamp=$(date -d "$valid_until" +%s 2>/dev/null || echo "0")
                local current_timestamp
                current_timestamp=$(date +%s)
                local thirty_days_from_now
                thirty_days_from_now=$((current_timestamp + 2592000))  # 30 days in seconds
                
                if [[ "$exp_timestamp" -gt 0 ]] && [[ "$exp_timestamp" -lt "$thirty_days_from_now" ]]; then
                    echo "  $(basename "$cert"): expires $valid_until" >> "$report_file"
                    ((expiring_count++))
                fi
            fi
        fi
    done
    
    if [[ "$expiring_count" -eq 0 ]]; then
        echo "  No certificates expiring in the next 30 days" >> "$report_file"
    fi
    
    cat >> "$report_file" << EOF

=== SECURITY RECOMMENDATIONS ===
- Regular CA key rotation (recommended annually)
- Monitor certificate usage and revoke unused certificates
- Implement automated certificate renewal for hosts
- Regular audit of issued certificates and principals
- Backup CA keys securely (preferably offline)

=== AUDIT SUMMARY ===
Audit Log Location: $AUDIT_LOG
Recent Audit Entries: $(tail -10 "$AUDIT_LOG" 2>/dev/null | wc -l)
EOF

    echo "CA status report generated: $report_file"
    cat "$report_file"
}

# Backup CA data
backup_ca() {
    local backup_dir="/var/backups/ssh_ca"
    local backup_file="$backup_dir/ssh_ca_backup_$(date +%Y%m%d_%H%M%S).tar.gz"
    
    log_action "INFO" "Creating CA backup..."
    
    mkdir -p "$backup_dir"
    chmod 700 "$backup_dir"
    
    # Create encrypted backup
    tar -czf "$backup_file" -C "$(dirname "$CA_DIR")" "$(basename "$CA_DIR")"
    chmod 600 "$backup_file"
    
    log_action "AUDIT" "CA backup created: $backup_file"
    echo "CA backup created: $backup_file"
    
    # Clean old backups (keep last 10)
    ls -t "$backup_dir"/ssh_ca_backup_*.tar.gz | tail -n +11 | xargs rm -f 2>/dev/null || true
}

# Main command interface
case "${1:-help}" in
    "init")
        initialize_ca
        ;;
    "sign-user")
        sign_user_certificate "$2" "$3" "${4:-developer}" "$5" "$6"
        ;;
    "sign-host")
        sign_host_certificate "$2" "$3" "$4" "$5"
        ;;
    "trust")
        configure_server_trust
        ;;
    "principals")
        create_user_principals "$2" "$3"
        ;;
    "revoke")
        revoke_certificate "$2" "$3"
        ;;
    "list")
        list_certificates "$2"
        ;;
    "report")
        generate_ca_report
        ;;
    "backup")
        backup_ca
        ;;
    *)
        echo "SSH Certificate Authority Management Tool"
        echo "Usage: $0 {command} [options]"
        echo
        echo "Commands:"
        echo "  init                                    - Initialize SSH CA"
        echo "  sign-user <user> <pubkey> [template] [principals] [validity] - Sign user certificate"
        echo "  sign-host <hostname> <pubkey> [principals] [validity] - Sign host certificate"
        echo "  trust                                   - Configure server to trust CA"
        echo "  principals <user> <principals>          - Create user principals file"
        echo "  revoke <cert_file> [reason]             - Revoke certificate"
        echo "  list [user|host|all]                    - List issued certificates"
        echo "  report                                  - Generate CA status report"
        echo "  backup                                  - Create CA backup"
        echo
        echo "Templates: admin, developer, service, temporary"
        echo "Examples:"
        echo "  $0 sign-user alice /tmp/alice.pub admin"
        echo "  $0 sign-host server1 /tmp/server1.pub"
        echo "  $0 principals alice admin,developer"
        ;;
esac
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
