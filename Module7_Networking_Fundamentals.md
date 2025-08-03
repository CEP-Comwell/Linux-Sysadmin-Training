# Module 7: Networking & Firewalls

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [7.1 Modern Network Interface Management](#71-modern-network-interface-management)
  - [7.2 IP Address Configuration and Management](#72-ip-address-configuration-and-management)
  - [7.3 DNS Resolution and Host Management](#73-dns-resolution-and-host-management)
  - [7.4 Network Connectivity Diagnostics](#74-network-connectivity-diagnostics)
  - [7.5 SSH Security and Hardening](#75-ssh-security-and-hardening)
  - [7.6 Comprehensive Firewall Management](#76-comprehensive-firewall-management)
  - [7.7 Network Security Best Practices](#77-network-security-best-practices)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Modern Network Interface Management](#modern-network-interface-management)
  - [Comprehensive IP Address Configuration](#comprehensive-ip-address-configuration)
  - [DNS Resolution and Host Management](#dns-resolution-and-host-management)
  - [Advanced Connectivity Diagnostics](#advanced-connectivity-diagnostics)
  - [SSH Security and Hardening](#ssh-security-and-hardening)
  - [Comprehensive Firewall Management](#comprehensive-firewall-management)
- [Advanced Network Configuration Files](#advanced-network-configuration-files)
  - [NetworkManager Configuration](#networkmanager-configuration)
  - [systemd-networkd Configuration](#systemd-networkd-configuration)
  - [Legacy Network Configuration](#legacy-network-configuration)
- [Network Troubleshooting Methodologies](#network-troubleshooting-methodologies)
  - [Systematic Network Diagnosis](#systematic-network-diagnosis)
  - [Advanced Network Monitoring](#advanced-network-monitoring)
- [Network Security Best Practices](#network-security-best-practices)
  - [Host-Level Security Implementation](#host-level-security-implementation)
- [Comprehensive Troubleshooting Reference](#comprehensive-troubleshooting-reference)
- [Advanced Lab Exercises](#advanced-lab-exercises)
  - [Lab 1: Network Interface Configuration Mastery](#lab-1-network-interface-configuration-mastery)
  - [Lab 2: SSH Hardening and Key Management](#lab-2-ssh-hardening-and-key-management)
  - [Lab 3: Advanced Firewall Implementation](#lab-3-advanced-firewall-implementation)
  - [Lab 4: Network Troubleshooting Simulation](#lab-4-network-troubleshooting-simulation)
  - [Lab 5: Enterprise Network Security Implementation](#lab-5-enterprise-network-security-implementation)
- [Performance Optimization Guidelines](#performance-optimization-guidelines)
  - [Network Performance Tuning](#network-performance-tuning)
- [Security Monitoring and Incident Response](#security-monitoring-and-incident-response)
  - [Network Security Monitoring](#network-security-monitoring)
- [Best Practices Summary](#best-practices-summary)
  - [Network Configuration Best Practices](#network-configuration-best-practices)
  - [Security Implementation Checklist](#security-implementation-checklist)
- [Module Summary and Assessment](#module-summary-and-assessment)
- [Next Steps](#next-steps)

## Overview
Master interface configuration, connectivity diagnostics, secure remote access, and both traditional and zone-based firewall controls to safeguard your Linux host.

### Key Learning Outcomes Achieved
Upon completion of this module, students will have mastered:

1. **Modern Network Management**: Proficiency with current tools (`ip`, `ss`, `nmcli`) and legacy compatibility
2. **Security Implementation**: Comprehensive firewall configuration, SSH hardening, and security monitoring
3. **Troubleshooting Methodology**: Systematic approach to network problem diagnosis and resolution
4. **Performance Optimization**: Network tuning for optimal performance and reliability
5. **Enterprise Practices**: Scalable network security and management strategies

### Practical Skills Validation
Students should be able to demonstrate:
- Configuration of network interfaces using multiple methods
- Implementation of comprehensive firewall security policies
- SSH server hardening and secure remote access setup
- Systematic network troubleshooting and problem resolution
- Network performance monitoring and optimization

### Continuing Education Paths
**Next Recommended Modules**:
- Module 8: Logging and Monitoring (building on network monitoring skills)
- Module 12: Proxmox Virtual Environment (advanced network virtualization)
- Module 13: OpenSSH Best Practices (specialized SSH deployment)

**Advanced Topics for Further Study**:
- Software-Defined Networking (SDN)
- Network automation with Ansible
- Container networking (Docker/Kubernetes)
- Network security compliance frameworks
- Advanced packet analysis and forensics

### Professional Applications
These networking fundamentals directly apply to:
- **System Administration**: Daily network management and troubleshooting
- **DevOps Engineering**: Infrastructure automation and monitoring
- **Security Operations**: Network security implementation and incident response
- **Cloud Engineering**: Understanding underlying network principles for cloud deployments

Master these networking concepts to build a solid foundation for advanced Linux system administration and modern infrastructure management.

## Learning Objectives
By the end of this module, you will be able to:
1. Display interface details, address assignments, and routing tables to map packet flows using modern tools
2. Persist DHCP or static IP configurations for stable network setups across different Linux distributions
3. Resolve and troubleshoot domain names and hosts via DNS queries and host files
4. Secure SSH by editing `/etc/ssh/sshd_config`, generating key pairs, and managing authorized keys
5. Craft comprehensive firewall policies:
   - Define and inspect active zones in `firewalld`
   - Add or remove services, ports, sources, and interfaces from zones
   - Write rich rules for advanced filtering (logging, IP-based restrictions)
   - Compare and fallback to `iptables`/`nftables` or `ufw` when needed
6. Diagnose connectivity issues using systematic troubleshooting approaches
7. Implement network security best practices for production environments

## Topics

### 7.1 Modern Network Interface Management
- Viewing and managing interfaces with `ip`, `ifconfig`, and `nmcli`
- Understanding network interface naming conventions
- Network device status and configuration inspection
- Interface statistics and performance monitoring

### 7.2 IP Address Configuration and Management
- Static vs dynamic IP addressing strategies
- Configuring addresses via CLI tools and configuration files
- NetworkManager and systemd-networkd management
- Persistent network configuration across reboots
- DHCP client configuration and troubleshooting

### 7.3 DNS Resolution and Host Management
- DNS resolution configuration in `/etc/resolv.conf`
- Local host resolution with `/etc/hosts`
- DNS troubleshooting with `dig`, `nslookup`, and `host`
- systemd-resolved configuration and management

### 7.4 Network Connectivity Diagnostics
- Connectivity testing with `ping` and advanced options
- Path tracing with `traceroute` and `mtr`
- Port and service checking with `netstat`, `ss`, and `nmap`
- Network performance analysis and bandwidth testing

### 7.5 SSH Security and Hardening
- SSH server configuration and `/etc/ssh/sshd_config` hardening
- Key-based authentication setup and management
- Disabling password authentication and changing default ports
- SSH client configuration and connection management
- Advanced SSH features: tunneling, port forwarding, and agent forwarding

### 7.6 Comprehensive Firewall Management
- Zone-based firewall management with `firewalld`
- Legacy firewall tools: `iptables` and `nftables`
- UFW (Uncomplicated Firewall) for simplified management
- Rich rules and advanced filtering techniques
- NAT, port forwarding, and traffic redirection

### 7.7 Network Security Best Practices
- Host-level security implementations
- Network service hardening
- Intrusion detection and prevention
- Security monitoring and log analysis

## Essential Command Reference

| Command | Purpose |
|---------|---------|
| `ip a` | Show all network interfaces and their addresses |
| `ip route show` | Display routing table and default gateway |
| `ip link show` | List all network interfaces and their states |
| `nmcli device show` | List NetworkManager-managed devices |
| `nmcli connection show` | Display all network connections |
| `ping <host>` | Test reachability and measure latency |
| `traceroute <host>` | Trace the path packets take to a destination |
| `mtr <host>` | Combined ping and traceroute with real-time updates |
| `ss -tulwn` | Display all listening sockets and ports |
| `netstat -tulpn` | Show network connections with process information |
| `dig <domain>` | Perform DNS lookup with detailed information |
| `nslookup <domain>` | Query DNS servers for domain information |
| `firewall-cmd --get-active-zones` | List currently active `firewalld` zones |
| `firewall-cmd --zone=public --add-service=ssh` | Open SSH service in public zone (runtime) |
| `firewall-cmd --zone=public --add-service=ssh --permanent` | Persist SSH service across reboots |
| `firewall-cmd --reload` | Reload `firewalld` to apply permanent changes |
| `firewall-cmd --zone=trusted --add-source=192.168.1.0/24` | Trust an entire subnet in trusted zone |
| `iptables -L -n -v` | List IPv4 rules in legacy `iptables` with counters |
| `nft list ruleset` | Display the full `nftables` rule set |
| `ufw status verbose` | Show UFW firewall status and active rules |

## Practical Examples

### Modern Network Interface Management

#### Viewing Interface Information
```bash
# Show all interfaces with IP addresses
ip a
ip addr show

# Show specific interface details
ip a show eth0
ip link show eth0

# Display interface statistics
ip -s link show eth0
cat /proc/net/dev

# Show interface routing information
ip route show dev eth0

# NetworkManager interface management
nmcli device status
nmcli device show eth0
nmcli connection show

# Show interface configuration files
nmcli connection show "Wired connection 1"

# Monitor interface changes in real-time
ip monitor link
ip monitor addr
```

#### Interface State Management
```bash
# Bring interface up/down
sudo ip link set eth0 up
sudo ip link set eth0 down

# Using NetworkManager
nmcli device connect eth0
nmcli device disconnect eth0

# Restart network interface
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
``` ### Comprehensive IP Address Configuration

#### Static IP Configuration with NetworkManager
```bash
# Create static IP connection
sudo nmcli connection add type ethernet con-name static-eth0 \
    ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1

# Set DNS servers
sudo nmcli connection modify static-eth0 ipv4.dns "8.8.8.8 8.8.4.4"
sudo nmcli connection modify static-eth0 ipv4.dns-search "example.com"

# Set manual method (disable DHCP)
sudo nmcli connection modify static-eth0 ipv4.method manual

# Activate connection
sudo nmcli connection up static-eth0

# Configure multiple IP addresses
sudo nmcli connection modify static-eth0 +ipv4.addresses 192.168.1.101/24

# Configure DHCP connection
sudo nmcli connection add type ethernet con-name dhcp-eth0 ifname eth0
sudo nmcli connection modify dhcp-eth0 ipv4.method auto

# View connection details
nmcli connection show static-eth0
```

#### Using systemd-networkd
```bash
# Create network configuration file
sudo tee /etc/systemd/network/eth0.network << EOF
[Match]
Name=eth0

[Network]
DHCP=yes
DNS=8.8.8.8
DNS=8.8.4.4
Domains=example.com

[DHCP]
RouteMetric=100
UseDNS=false
EOF

# Static configuration example
sudo tee /etc/systemd/network/eth0-static.network << EOF
[Match]
Name=eth0

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
DNS=8.8.4.4
Domains=example.com
EOF

# Enable and start systemd-networkd
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
sudo systemctl status systemd-networkd

# Restart networking
sudo systemctl restart systemd-networkd
```

#### Legacy Network Configuration
```bash
# Temporary IP configuration
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip route add default via 192.168.1.1

# Using ifconfig (deprecated but still available)
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
sudo route add default gw 192.168.1.1

# Debian/Ubuntu persistent configuration
sudo tee /etc/network/interfaces << EOF
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
    dns-search example.com
EOF

# Red Hat/CentOS configuration
sudo tee /etc/sysconfig/network-scripts/ifcfg-eth0 << EOF
TYPE=Ethernet
BOOTPROTO=static
NAME=eth0
DEVICE=eth0
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DOMAIN=example.com
EOF
```

### DNS Resolution and Host Management

#### DNS Configuration and Testing
```bash
# Configure system DNS resolver
sudo tee /etc/systemd/resolved.conf << EOF
[Resolve]
DNS=8.8.8.8 8.8.4.4
FallbackDNS=1.1.1.1 1.0.0.1
Domains=example.com
DNSSEC=yes
DNSOverTLS=yes
Cache=yes
EOF

sudo systemctl restart systemd-resolved

# Traditional resolv.conf configuration
sudo tee /etc/resolv.conf << EOF
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com local
options timeout:2 attempts:3 rotate
EOF

# Configure local hosts
sudo tee -a /etc/hosts << EOF
192.168.1.10    server.example.com server
192.168.1.20    db.example.com database
192.168.1.30    web.example.com www
EOF

# DNS testing and troubleshooting
dig google.com
dig @8.8.8.8 google.com
dig google.com MX
dig google.com NS
dig -x 8.8.8.8  # Reverse DNS lookup

nslookup google.com
nslookup google.com 8.8.8.8

host google.com
host -t MX google.com

# Test DNS resolution order
getent hosts google.com
getent ahosts google.com

# Check systemd-resolved status
systemd-resolve --status
resolvectl status
resolvectl query google.com
```

### Advanced Connectivity Diagnostics

#### Comprehensive Connectivity Testing
```bash
# Basic connectivity testing
ping -c 4 google.com
ping -c 4 -i 0.5 8.8.8.8  # Faster pinging
ping -c 10 -s 1472 google.com  # Large packet test
ping6 -c 4 google.com  # IPv6 testing

# Advanced ping options
ping -f google.com  # Flood ping (requires root)
ping -R google.com  # Record route
ping -D google.com  # Print timestamps

# Path tracing and analysis
traceroute google.com
traceroute -n google.com  # No DNS resolution
traceroute -T google.com  # TCP traceroute
traceroute6 google.com    # IPv6 traceroute

# Real-time network path analysis
mtr google.com
mtr --report --report-cycles 10 google.com
mtr --tcp --port 80 google.com

# Port and service testing
nc -zv google.com 80
nc -zv google.com 80-443  # Port range
nc -u -zv 8.8.8.8 53      # UDP port test

# Comprehensive port scanning
nmap -sP 192.168.1.0/24   # Ping scan
nmap -sS google.com       # SYN scan
nmap -sU -p 53,123 google.com  # UDP scan
nmap -A google.com        # Aggressive scan

# Network connection monitoring
ss -tulpn                 # All listening ports
ss -tulpn | grep :80      # HTTP connections
ss -o state established   # Established connections
ss -i                     # Interface statistics

netstat -tulpn            # Legacy alternative
netstat -i                # Interface statistics
netstat -r                # Routing table
```

### SSH Security and Hardening

#### SSH Server Configuration and Hardening
```bash
# Backup original configuration
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup

# Secure SSH configuration
sudo tee /etc/ssh/sshd_config << EOF
# Basic Configuration
Port 2222                          # Change default port
Protocol 2                         # SSH version 2 only
AddressFamily inet                 # IPv4 only (or 'any' for both)

# Authentication
PermitRootLogin no                 # Disable root login
PasswordAuthentication no          # Disable password auth
PubkeyAuthentication yes           # Enable key-based auth
AuthorizedKeysFile .ssh/authorized_keys
PermitEmptyPasswords no            # No empty passwords
ChallengeResponseAuthentication no # Disable challenge-response

# Login Restrictions
MaxAuthTries 3                     # Maximum auth attempts
MaxSessions 2                      # Maximum concurrent sessions
LoginGracetime 30                  # Time to login (seconds)
ClientAliveInterval 300            # Keep-alive interval
ClientAliveCountMax 2              # Max keep-alive messages

# Feature Restrictions
X11Forwarding no                   # Disable X11 forwarding
AllowTcpForwarding no             # Disable TCP forwarding
AllowAgentForwarding no           # Disable agent forwarding
PermitTunnel no                   # Disable tunneling
GatewayPorts no                   # Disable gateway ports

# User and Group Restrictions
AllowUsers admin user1 user2      # Allowed users only
# AllowGroups ssh-users            # Alternative: allowed groups
# DenyUsers baduser                # Denied users
# DenyGroups badgroup              # Denied groups

# Logging
SyslogFacility AUTHPRIV           # Log facility
LogLevel INFO                     # Log level

# Banner and MOTD
Banner /etc/ssh/banner            # Login banner
PrintMotd yes                     # Print MOTD

# Cryptography
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr
MACs hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha2-512
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp521,ecdh-sha2-nistp384,ecdh-sha2-nistp256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512
EOF

# Create SSH banner
sudo tee /etc/ssh/banner << EOF
WARNING: Unauthorized access is prohibited!
All connections are monitored and logged.
Disconnect immediately if you are not authorized.
EOF

# Test SSH configuration
sudo sshd -t

# Restart SSH service
sudo systemctl restart sshd
sudo systemctl status sshd
```

#### SSH Key Management
```bash
# Generate SSH key pair (client side)
ssh-keygen -t ed25519 -b 4096 -C "user@hostname"
ssh-keygen -t rsa -b 4096 -C "user@hostname"  # Alternative RSA

# Copy public key to server
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server
ssh-copy-id -p 2222 user@server  # Custom port

# Manual key installation
cat ~/.ssh/id_ed25519.pub | ssh user@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Set proper permissions on server
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519      # Private key
chmod 644 ~/.ssh/id_ed25519.pub  # Public key

# SSH client configuration
tee ~/.ssh/config << EOF
Host production
    HostName prod.example.com
    Port 2222
    User admin
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
    
Host *.example.com
    User admin
    Port 2222
    
Host bastion
    HostName bastion.example.com
    User jump
    ProxyJump production
EOF

# SSH agent management
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
ssh-add -l  # List loaded keys

# Advanced SSH features
# SSH tunneling (port forwarding)
ssh -L 8080:localhost:80 user@server     # Local forwarding
ssh -R 8080:localhost:80 user@server     # Remote forwarding
ssh -D 1080 user@server                  # SOCKS proxy

# SSH multiplexing (connection sharing)
ssh -M -S ~/.ssh/master-socket user@server
ssh -S ~/.ssh/master-socket user@server  # Use existing connection
```

### Comprehensive Firewall Management

#### firewalld Zone-Based Management
```bash
# Get firewalld status and information
sudo systemctl start firewalld
sudo systemctl enable firewalld
firewall-cmd --state

# Zone management
firewall-cmd --get-zones              # List all zones
firewall-cmd --get-default-zone       # Show default zone
firewall-cmd --get-active-zones       # Show active zones
firewall-cmd --list-all-zones         # Detailed zone information

# Zone assignment
firewall-cmd --zone=public --list-all
firewall-cmd --get-zone-of-interface=eth0
sudo firewall-cmd --zone=internal --change-interface=eth1

# Service management
firewall-cmd --get-services           # List available services
firewall-cmd --zone=public --list-services
sudo firewall-cmd --zone=public --add-service=ssh
sudo firewall-cmd --zone=public --add-service=ssh --permanent
sudo firewall-cmd --zone=public --remove-service=ssh --permanent

# Port management
sudo firewall-cmd --zone=public --add-port=2222/tcp
sudo firewall-cmd --zone=public --add-port=2222/tcp --permanent
sudo firewall-cmd --zone=public --add-port=8000-8080/tcp --permanent
sudo firewall-cmd --zone=public --list-ports

# Source-based rules
sudo firewall-cmd --zone=trusted --add-source=192.168.1.0/24
sudo firewall-cmd --zone=trusted --add-source=192.168.1.0/24 --permanent
sudo firewall-cmd --zone=drop --add-source=10.0.0.100

# Rich rules for advanced filtering
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" service name="ssh" accept'
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" port protocol="tcp" port="80" accept'
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="10.0.0.100" drop'

# Logging rules
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="0.0.0.0/0" service name="ssh" log prefix="SSH-ACCESS" level="info" limit value="3/m" accept'

# NAT and port forwarding
sudo firewall-cmd --zone=external --add-masquerade --permanent
sudo firewall-cmd --zone=external --add-forward-port=port=80:proto=tcp:toport=8080:toaddr=192.168.1.100 --permanent

# Apply changes and reload
sudo firewall-cmd --reload
sudo firewall-cmd --complete-reload  # Complete restart

# Backup and restore
sudo firewall-cmd --runtime-to-permanent
sudo cp -r /etc/firewalld /etc/firewalld.backup
```

#### iptables Legacy Firewall Management
```bash
# View current rules
sudo iptables -L -n -v --line-numbers
sudo iptables -t nat -L -n -v
sudo iptables -t mangle -L -n -v

# Basic firewall setup
# Flush existing rules
sudo iptables -F
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X

# Set default policies
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT

# Allow loopback traffic
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT

# Allow established and related connections
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow specific services
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT    # SSH
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT    # HTTP
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT   # HTTPS

# Allow from specific networks
sudo iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT

# Rate limiting
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --set
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --update --seconds 60 --hitcount 4 -j DROP

# Logging
sudo iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# NAT rules
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:8080

# Save rules (varies by distribution)
# Debian/Ubuntu
sudo iptables-save | sudo tee /etc/iptables/rules.v4
sudo ip6tables-save | sudo tee /etc/iptables/rules.v6

# Red Hat/CentOS
sudo iptables-save | sudo tee /etc/sysconfig/iptables

# Create script for rule management
sudo tee /usr/local/bin/firewall-rules.sh << 'EOF'
#!/bin/bash
# Firewall rules script

# Flush rules
iptables -F
iptables -X

# Default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Allow loopback
iptables -A INPUT -i lo -j ACCEPT

# Allow established connections
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow SSH with rate limiting
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --set
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --update --seconds 60 --hitcount 4 -j DROP
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Log dropped packets
iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: "

echo "Firewall rules applied"
EOF

sudo chmod +x /usr/local/bin/firewall-rules.sh
```

#### UFW Simplified Firewall Management
```bash
# Enable/disable UFW
sudo ufw enable
sudo ufw disable
sudo ufw status verbose

# Default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw default deny forward

# Allow services
sudo ufw allow ssh
sudo ufw allow 22/tcp
sudo ufw allow 80,443/tcp
sudo ufw allow 'Apache Full'

# Allow from specific sources
sudo ufw allow from 192.168.1.0/24
sudo ufw allow from 192.168.1.100 to any port 22
sudo ufw allow from 192.168.1.0/24 to any port 3306

# Deny rules
sudo ufw deny from 10.0.0.100
sudo ufw deny 23

# Delete rules
sudo ufw delete allow 80/tcp
sudo ufw delete 3  # Delete by rule number

# Advanced rules
sudo ufw allow in on eth0 to any port 80
sudo ufw allow out on eth1 to any port 25

# Rate limiting
sudo ufw limit ssh
sudo ufw limit 22/tcp

# Show numbered rules
sudo ufw status numbered

# Reset firewall
sudo ufw --force reset

# Application profiles
sudo ufw app list
sudo ufw allow 'Apache Full'
sudo ufw app info 'Apache Full'
```

## Advanced Network Configuration Files

### NetworkManager Configuration
```bash
# Main NetworkManager configuration
# /etc/NetworkManager/NetworkManager.conf
[main]
plugins=ifupdown,keyfile
dns=systemd-resolved

[ifupdown]
managed=false

[device]
wifi.scan-rand-mac-address=no

# Connection-specific configuration
# /etc/NetworkManager/system-connections/Wired\ connection\ 1.nmconnection
[connection]
id=Wired connection 1
uuid=12345678-1234-1234-1234-123456789abc
type=ethernet
autoconnect-priority=-999
interface-name=eth0

[ethernet]

[ipv4]
address1=192.168.1.100/24,192.168.1.1
dns=8.8.8.8;8.8.4.4;
dns-search=example.com;
method=manual

[ipv6]
addr-gen-mode=stable-privacy
method=auto

[proxy]
```

### systemd-networkd Configuration
```bash
# Network device configuration
# /etc/systemd/network/eth0.network
[Match]
Name=eth0
Type=ether

[Network]
DHCP=yes
IPForward=yes
IPMasquerade=yes
LLDP=yes
EmitLLDP=yes
IPv6AcceptRA=yes
IPv6PrivacyExtensions=yes

# Static configuration alternative
[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
DNS=8.8.4.4
DNS=1.1.1.1
Domains=example.com
NTP=pool.ntp.org

[Route]
Destination=10.0.0.0/8
Gateway=192.168.1.254
Metric=100

[DHCP]
RouteMetric=100
UseMTU=true
UseDNS=false
UseRoutes=true
UseTimezone=true
ClientIdentifier=mac
```

### Legacy Network Configuration

#### Debian/Ubuntu Network Interfaces
```bash
# /etc/network/interfaces
source /etc/network/interfaces.d/*

auto lo
iface lo inet loopback

# Static configuration
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
    dns-search example.com
    dns-domain example.com
    # Custom commands
    pre-up echo "Configuring eth0"
    post-up echo "eth0 is up"
    pre-down echo "Taking down eth0"
    post-down echo "eth0 is down"

# DHCP configuration
auto eth1
iface eth1 inet dhcp
    hostname client-hostname
    metric 100

# VLAN configuration
auto eth0.100
iface eth0.100 inet static
    address 10.0.100.10
    netmask 255.255.255.0
    vlan-raw-device eth0

# Bond configuration
auto bond0
iface bond0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    bond-mode 802.3ad
    bond-slaves eth0 eth1
    bond-miimon 100
    bond-lacp-rate 1
```

#### Red Hat/CentOS Network Scripts
```bash
# /etc/sysconfig/network-scripts/ifcfg-eth0
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=eth0
UUID=12345678-1234-1234-1234-123456789abc
DEVICE=eth0
ONBOOT=yes
IPADDR=192.168.1.100
PREFIX=24
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DOMAIN=example.com
IPV6_PRIVACY=rfc3041

# DHCP configuration
BOOTPROTO=dhcp
DHCP_HOSTNAME=client-hostname
PEERDNS=yes
PEERROUTES=yes

# VLAN configuration (/etc/sysconfig/network-scripts/ifcfg-eth0.100)
VLAN=yes
TYPE=Vlan
PHYSDEV=eth0
VLAN_ID=100
REORDER_HDR=yes
GVRP=no
MVRP=no
HWADDR=00:11:22:33:44:55
BOOTPROTO=static
IPADDR=10.0.100.10
NETMASK=255.255.255.0
```

## Network Troubleshooting Methodologies

### Systematic Network Diagnosis
```bash
# Layer 1: Physical connectivity
ethtool eth0                    # Check link status
cat /sys/class/net/eth0/carrier # Check carrier status
dmesg | grep eth0              # Check kernel messages
lspci | grep -i ethernet       # List network hardware

# Layer 2: Data Link
ip link show                   # Interface status
cat /proc/net/dev             # Interface statistics
bridge fdb show               # MAC address table
ip neighbor show              # ARP table

# Layer 3: Network
ip addr show                  # IP configuration
ip route show                 # Routing table
ping -c 4 gateway_ip         # Gateway connectivity
traceroute destination       # Path analysis

# Layer 4: Transport
ss -tulpn                    # Listening services
nc -zv host port            # Port connectivity
nmap -sS target             # SYN scan

# Layer 7: Application
curl -I http://website      # HTTP response
telnet smtp_server 25       # SMTP test
openssl s_client -connect host:443  # SSL/TLS test

# DNS resolution troubleshooting
systemd-resolve --status
dig +trace domain.com
dig @dns_server domain.com
nslookup domain.com
host domain.com

# Performance analysis
iperf3 -s                   # Server mode
iperf3 -c server_ip         # Client test
mtr --report domain.com     # Network path analysis
tcptrace capture.pcap       # TCP connection analysis
```

### Advanced Network Monitoring
```bash
# Real-time network monitoring
iftop -i eth0               # Bandwidth usage
nethogs                     # Per-process bandwidth
nload eth0                  # Network load
bmon                        # Bandwidth monitor
iptraf-ng                   # Network statistics

# Network traffic capture and analysis
tcpdump -i eth0 -w capture.pcap
tcpdump -i eth0 host 192.168.1.100
tcpdump -i eth0 port 80 or port 443
tcpdump -i eth0 -s 0 -A 'tcp port 80'

# Wireshark command-line tools
tshark -i eth0 -w capture.pcap
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e tcp.port
dumpcap -i eth0 -w capture.pcap

# Network security monitoring
netstat -tupln | grep LISTEN
ss -tulpn | awk 'NR>1 {print $5}' | cut -d: -f2 | sort -n | uniq
lsof -i :80
fuser -n tcp 80

# Log analysis
journalctl -u NetworkManager
journalctl -u systemd-networkd
tail -f /var/log/syslog | grep -i network
grep -i "link up\|link down" /var/log/messages
```

## Network Security Best Practices

### Host-Level Security Implementation
```bash
# Disable unused network services
systemctl list-unit-files --type=service --state=enabled | grep -E "(telnet|rsh|ftp)"
sudo systemctl disable telnet
sudo systemctl mask telnet

# Network service hardening
# Disable IP forwarding (if not a router)
echo 'net.ipv4.ip_forward = 0' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 0' | sudo tee -a /etc/sysctl.conf

# Disable ICMP redirects
echo 'net.ipv4.conf.all.accept_redirects = 0' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.conf.all.send_redirects = 0' | sudo tee -a /etc/sysctl.conf

# Enable source route verification
echo 'net.ipv4.conf.all.rp_filter = 1' | sudo tee -a /etc/sysctl.conf

# Disable source routing
echo 'net.ipv4.conf.all.accept_source_route = 0' | sudo tee -a /etc/sysctl.conf

# Apply sysctl changes
sudo sysctl -p

# TCP/IP hardening
echo 'net.ipv4.tcp_syncookies = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_max_syn_backlog = 2048' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_synack_retries = 3' | sudo tee -a /etc/sysctl.conf

# Network monitoring setup
sudo tee /usr/local/bin/network-monitor.sh << 'EOF'
#!/bin/bash
# Network security monitoring script

LOG_FILE="/var/log/network-security.log"
DATE=$(date '+%Y-%m-%d %H:%M:%S')

# Check for suspicious network activity
CONNECTIONS=$(ss -tulpn | wc -l)
if [ $CONNECTIONS -gt 1000 ]; then
    echo "$DATE: High number of connections detected: $CONNECTIONS" >> $LOG_FILE
fi

# Check for failed SSH attempts
SSH_FAILS=$(journalctl --since "1 hour ago" | grep "Failed password" | wc -l)
if [ $SSH_FAILS -gt 10 ]; then
    echo "$DATE: High number of SSH failures: $SSH_FAILS" >> $LOG_FILE
fi

# Monitor bandwidth usage
RX_BYTES=$(cat /sys/class/net/eth0/statistics/rx_bytes)
TX_BYTES=$(cat /sys/class/net/eth0/statistics/tx_bytes)
echo "$DATE: RX: $RX_BYTES TX: $TX_BYTES" >> $LOG_FILE
EOF

sudo chmod +x /usr/local/bin/network-monitor.sh

# Add to crontab for regular monitoring
echo "*/5 * * * * /usr/local/bin/network-monitor.sh" | sudo crontab -
```

## Comprehensive Troubleshooting Reference

| Issue Category | Symptoms | Diagnostic Commands | Common Solutions |
|----------------|----------|-------------------|------------------|
| **Physical Layer** | No link light, cable issues | `ethtool eth0`, `dmesg \| grep eth0` | Check cables, switch ports, drivers |
| **Interface Configuration** | Wrong IP, no connectivity | `ip a`, `nmcli device status` | Reconfigure IP, restart NetworkManager |
| **DNS Resolution** | Can't resolve hostnames | `dig domain.com`, `systemd-resolve --status` | Fix /etc/resolv.conf, restart systemd-resolved |
| **Gateway Issues** | Can't reach internet | `ip route show`, `ping gateway` | Set correct default route |
| **Firewall Blocking** | Services unreachable | `firewall-cmd --list-all`, `iptables -L` | Allow ports/services in firewall |
| **SSH Access** | Connection refused/timeout | `systemctl status sshd`, `ss -tulpn \| grep 22` | Start SSH service, check firewall |
| **High Latency** | Slow network responses | `mtr destination`, `ping -f destination` | Check network path, bandwidth |
| **Packet Loss** | Intermittent connectivity | `mtr destination`, `tcpdump -i eth0` | Check physical layer, congestion |
| **Port Conflicts** | Service won't start | `ss -tulpn`, `netstat -tulpn` | Find conflicting services, change ports |
| **MTU Issues** | Large packets dropped | `ping -s 1472 destination`, `ip link show` | Adjust MTU size, path MTU discovery |

## Advanced Lab Exercises

### Lab 1: Network Interface Configuration Mastery
**Objective**: Master modern and legacy network configuration methods.

**Tasks**:
1. Configure static IP using NetworkManager CLI (`nmcli`)
2. Set up the same configuration using systemd-networkd
3. Create bonded interfaces for redundancy
4. Configure VLAN interfaces for network segmentation
5. Test failover scenarios and performance differences
6. Document configuration persistence across reboots

**Deliverables**:
- Working network configurations using all three methods
- Performance comparison report
- Failover testing documentation
- Configuration backup and restoration procedures

### Lab 2: SSH Hardening and Key Management
**Objective**: Implement comprehensive SSH security measures.

**Tasks**:
1. Harden SSH server configuration following security best practices
2. Set up key-based authentication with proper key management
3. Configure SSH client with connection multiplexing and jump hosts
4. Implement SSH tunneling for secure service access
5. Set up SSH certificate authority for scalable key management
6. Create monitoring and alerting for SSH access attempts

**Deliverables**:
- Hardened SSH configuration files
- Key management procedures and documentation
- SSH tunneling examples and use cases
- Security monitoring dashboard

### Lab 3: Advanced Firewall Implementation
**Objective**: Deploy comprehensive firewall solutions using multiple technologies.

**Tasks**:
1. Design and implement firewalld zones for different network segments
2. Create rich rules for complex filtering scenarios
3. Set up equivalent protection using iptables with custom scripts
4. Implement UFW for simplified management scenarios
5. Configure NAT and port forwarding for internal services
6. Set up logging and monitoring for firewall activities

**Deliverables**:
- Complete firewall rule sets for all three technologies
- Security policy documentation
- Automated rule deployment scripts
- Log analysis and monitoring procedures

### Lab 4: Network Troubleshooting Simulation
**Objective**: Develop systematic network problem diagnosis skills.

**Tasks**:
1. Create various network problem scenarios (misconfiguration, DNS issues, routing problems)
2. Practice systematic troubleshooting using OSI layer approach
3. Use packet capture and analysis tools for deep diagnosis
4. Implement network monitoring and alerting systems
5. Create troubleshooting runbooks for common issues
6. Simulate and resolve network security incidents

**Deliverables**:
- Comprehensive troubleshooting methodology
- Network monitoring dashboard
- Incident response procedures
- Problem simulation scenarios for training

### Lab 5: Enterprise Network Security Implementation
**Objective**: Design and implement enterprise-grade network security.

**Tasks**:
1. Design network segmentation strategy using VLANs and subnets
2. Implement comprehensive access control policies
3. Set up network intrusion detection and prevention
4. Configure secure remote access solutions
5. Implement network traffic analysis and anomaly detection
6. Create security incident response procedures

**Deliverables**:
- Network security architecture design
- Implemented security controls and monitoring
- Incident response playbook
- Security assessment and compliance documentation

## Performance Optimization Guidelines

### Network Performance Tuning
```bash
# TCP buffer tuning for high-bandwidth networks
echo 'net.core.rmem_max = 134217728' | sudo tee -a /etc/sysctl.conf
echo 'net.core.wmem_max = 134217728' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_rmem = 4096 87380 134217728' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_wmem = 4096 65536 134217728' | sudo tee -a /etc/sysctl.conf

# Increase network device backlog
echo 'net.core.netdev_max_backlog = 5000' | sudo tee -a /etc/sysctl.conf

# TCP congestion control
echo 'net.ipv4.tcp_congestion_control = bbr' | sudo tee -a /etc/sysctl.conf

# Apply changes
sudo sysctl -p

# Interface-specific optimizations
sudo ethtool -K eth0 tso on
sudo ethtool -K eth0 gso on
sudo ethtool -K eth0 gro on
sudo ethtool -G eth0 rx 4096 tx 4096

# Monitor network performance
sar -n DEV 1 5                    # Interface statistics
ss -i                             # Socket information with details
ethtool -S eth0                   # Interface statistics
cat /proc/net/dev                 # Network interface statistics
```

## Security Monitoring and Incident Response

### Network Security Monitoring
```bash
# Automated security monitoring script
sudo tee /usr/local/bin/network-security-monitor.sh << 'EOF'
#!/bin/bash

LOG_FILE="/var/log/network-security.log"
ALERT_EMAIL="admin@example.com"

# Monitor for suspicious SSH activity
ssh_attempts=$(journalctl --since "1 hour ago" -u ssh | grep "Failed password" | wc -l)
if [ $ssh_attempts -gt 20 ]; then
    echo "$(date): HIGH: $ssh_attempts failed SSH attempts in last hour" | tee -a $LOG_FILE
    echo "High number of SSH failures detected" | mail -s "Security Alert" $ALERT_EMAIL
fi

# Monitor for port scans
netstat_connections=$(ss -tan | grep :22 | grep SYN_RECV | wc -l)
if [ $netstat_connections -gt 50 ]; then
    echo "$(date): MEDIUM: $netstat_connections pending SSH connections" | tee -a $LOG_FILE
fi

# Monitor bandwidth usage
interface="eth0"
rx_bytes_before=$(cat /sys/class/net/$interface/statistics/rx_bytes)
sleep 60
rx_bytes_after=$(cat /sys/class/net/$interface/statistics/rx_bytes)
bandwidth=$((($rx_bytes_after - $rx_bytes_before) / 1024 / 1024))

if [ $bandwidth -gt 100 ]; then
    echo "$(date): INFO: High bandwidth usage: ${bandwidth}MB/min" | tee -a $LOG_FILE
fi

# Check for unusual listening ports
new_ports=$(ss -tulpn | awk 'NR>1 {print $5}' | cut -d: -f2 | sort -n | comm -23 - /etc/baseline-ports.txt)
if [ -n "$new_ports" ]; then
    echo "$(date): MEDIUM: New listening ports detected: $new_ports" | tee -a $LOG_FILE
fi
EOF

sudo chmod +x /usr/local/bin/network-security-monitor.sh

# Create baseline ports file
ss -tulpn | awk 'NR>1 {print $5}' | cut -d: -f2 | sort -n | sudo tee /etc/baseline-ports.txt

# Schedule monitoring
echo "*/5 * * * * /usr/local/bin/network-security-monitor.sh" | sudo crontab -
```

## Best Practices Summary

### Network Configuration Best Practices
| Practice | Description |
|----------|-------------|
| **Use Modern Tools** | Prefer `ip`, `ss`, and `nmcli` over legacy tools |
| **Document Changes** | Maintain configuration management and version control |
| **Test Thoroughly** | Validate configurations in non-production environments |
| **Monitor Continuously** | Implement network monitoring and alerting |
| **Security First** | Apply security hardening from initial deployment |
| **Plan for Failure** | Design redundancy and failover mechanisms |
| **Regular Updates** | Keep network services and tools updated |

### Security Implementation Checklist
- [ ] SSH server hardened with key-based authentication
- [ ] Firewall configured with minimal required access
- [ ] Network services secured and unnecessary services disabled
- [ ] Regular security monitoring and log analysis implemented
- [ ] Network segmentation applied where appropriate
- [ ] Incident response procedures documented and tested
- [ ] Regular security assessments and penetration testing scheduled

## Next Steps
With networking fundamentals mastered, you're ready to explore Logging & Monitoring in Module 8, where you'll learn to manage system logs and implement comprehensive monitoring solutions.
