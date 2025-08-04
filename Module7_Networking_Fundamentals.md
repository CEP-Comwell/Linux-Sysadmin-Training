# Module 7: Networking Fundamentals

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics Covered](#topics-covered)
  - [7.1 Network Interface Management](#71-network-interface-management)
  - [7.2 IP Configuration with Netplan](#72-ip-configuration-with-netplan)
  - [7.3 Legacy Network Configuration](#73-legacy-network-configuration)
  - [7.4 DNS and Name Resolution](#74-dns-and-name-resolution)
  - [7.5 Basic Network Troubleshooting](#75-basic-network-troubleshooting)
  - [7.6 Firewall Basics](#76-firewall-basics)
  - [7.7 SSH Configuration](#77-ssh-configuration)
  - [7.8 VPN Setup (WireGuard)](#78-vpn-setup-wireguard)
- [Essential Commands](#essential-commands)
- [Practical Examples](#practical-examples)
- [Lab Exercises](#lab-exercises)
- [Next Steps](#next-steps)


## Overview
[⬆️ Back to Top](#table-of-contents)

This module covers practical Linux networking fundamentals for daily system administration. You'll learn to configure network interfaces, manage IP addressing, troubleshoot connectivity issues, and implement basic security measures using modern tools and best practices.

**What you'll learn:**
- Network interface management with modern tools (`ip`, `nmcli`)
- Static and DHCP configuration using Netplan and legacy methods
- Basic DNS configuration and troubleshooting
- Essential network troubleshooting techniques
- Firewall configuration with `ufw` and `firewalld`
- SSH server configuration and security
- WireGuard VPN basics


## Learning Objectives
[⬆️ Back to Top](#table-of-contents)

By the end of this module, you will be able to:

1. **Manage Network Interfaces**: View and configure network interfaces using `ip` and NetworkManager
2. **Configure IP Addressing**: Set up static and DHCP configurations with Netplan and legacy methods
3. **Troubleshoot DNS**: Configure DNS settings and resolve name resolution issues
4. **Diagnose Network Issues**: Use essential tools like `ping`, `traceroute`, and `ss` for troubleshooting
5. **Configure Basic Firewalls**: Set up host-based firewalls with `ufw` and `firewalld`
6. **Secure SSH**: Configure SSH server for secure remote access
7. **Set Up Basic VPNs**: Configure WireGuard for secure connections


## Topics Covered
[⬆️ Back to Top](#table-of-contents)

### 7.1 Network Interface Management
- Modern interface naming conventions (eth0, enp0s3, etc.)
- Viewing interface information with `ip` and `nmcli`
- Interface status and basic configuration
- Understanding interface states (up/down, link detection)

### 7.2 IP Configuration with Netplan
- Static IP configuration with Netplan YAML files
- DHCP configuration with Netplan
- Creating network bridges with Netplan
- Netplan configuration validation and application

### 7.3 Legacy Network Configuration
- Using `/etc/network/interfaces` on Debian-based systems
- Sourcing configuration from `interfaces.d/` directory
- Basic systemd-networkd configuration
- NetworkManager with `nmcli` for desktop environments

### 7.4 DNS and Name Resolution
- Configuring DNS servers in `/etc/resolv.conf`
- Local hostname resolution with `/etc/hosts`
- Basic DNS troubleshooting with `dig` and `nslookup`
- Understanding systemd-resolved basics

### 7.5 Basic Network Troubleshooting
- Connectivity testing with `ping` and `traceroute`
- Port checking with `nc` (netcat) and `telnet`
- Viewing network connections with `ss` and `netstat`
- Basic packet capture with `tcpdump`

### 7.6 Firewall Basics
- UFW (Uncomplicated Firewall) for simple configurations
- Basic `firewalld` zone management
- Essential `iptables` commands for troubleshooting
- Allowing/denying services and ports

### 7.7 SSH Configuration
- Basic SSH server configuration in `/etc/ssh/sshd_config`
- SSH key generation and management
- Disabling password authentication
- Basic SSH security practices

### 7.8 VPN Setup (WireGuard)
- WireGuard installation and basic configuration
- Creating WireGuard peer connections


## Essential Commands
[⬆️ Back to Top](#table-of-contents)

### Network Interface Management
| Command | Description | Example |
|---------|-------------|---------|
| `ip a` | Show all network interfaces | `ip a` |
| `ip link show` | Display interface status | `ip link show eth0` |
| `ip link set` | Change interface state | `ip link set eth0 up` |
| `nmcli device` | NetworkManager device info | `nmcli device status` |

### IP Configuration
| Command | Description | Example |
|---------|-------------|---------|
| `ip addr add` | Add IP address | `ip addr add 192.168.1.10/24 dev eth0` |
| `ip route show` | Display routing table | `ip route show` |
| `dhclient` | Request DHCP lease | `dhclient eth0` |
| `netplan apply` | Apply Netplan configuration | `netplan apply` |

### Network Diagnostics
| Command | Description | Example |
|---------|-------------|---------|
| `ping` | Test connectivity | `ping -c 4 google.com` |
| `traceroute` | Trace network path | `traceroute google.com` |
| `ss` | Show network connections | `ss -tulpn` |
| `nc` | Netcat port testing | `nc -zv google.com 80` |

### DNS Tools
| Command | Description | Example |
|---------|-------------|---------|
| `dig` | DNS lookup | `dig google.com` |
| `nslookup` | DNS query | `nslookup google.com` |
| `host` | Simple DNS lookup | `host google.com` |

### Firewall Management
| Command | Description | Example |
|---------|-------------|---------|
| `ufw` | Ubuntu firewall | `ufw enable` |
| `firewall-cmd` | Firewalld management | `firewall-cmd --list-all` |
| `iptables` | Direct firewall rules | `iptables -L` |

### SSH
| Command | Description | Example |
|---------|-------------|---------|
| `ssh` | Connect to remote host | `ssh user@hostname` |
| `ssh-keygen` | Generate SSH keys | `ssh-keygen -t ed25519` |
| `ssh-copy-id` | Copy public key | `ssh-copy-id user@host` |
|---------|-------------|---------|
| `iftop` | Network bandwidth monitor | `iftop -i eth0` |
| `nethogs` | Process network usage | `nethogs eth0` |
| `vnstat` | Network statistics | `vnstat -i eth0` |
| `iotop` | I/O monitor | `iotop -o` |
| `lsof` | List open files/network connections | `lsof -i :80` |


## Practical Examples
[⬆️ Back to Top](#table-of-contents)

[Related Commands/Topics: Network Interface Management](#71-network-interface-management) 🟢

[Related Commands/Topics: Network Interface Management](#71-network-interface-management) 🟢
```bash
# Show all network interfaces
ip a

# Show specific interface
ip a show eth0

# Show interface status
ip link show

# Check NetworkManager status
nmcli device status

# Show detailed interface information
nmcli device show eth0
```

[Related Commands/Topics: Network Interface Management](#71-network-interface-management) 🟢
```bash
# Bring interface up/down
sudo ip link set eth0 up
sudo ip link set eth0 down

# Temporarily add IP address
sudo ip addr add 192.168.1.100/24 dev eth0

# Remove IP address
sudo ip addr del 192.168.1.100/24 dev eth0

# Show routing table
ip route show
```
[Related Commands/Topics: IP Configuration with Netplan](#72-ip-configuration-with-netplan) 🟡

#### Static IP Configuration
Create `/etc/netplan/01-static.yaml`:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: false
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
        search:
          - example.com
```

#### DHCP Configuration
Create `/etc/netplan/01-dhcp.yaml`:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
      dhcp6: false
```

#### Bridge Configuration
Create `/etc/netplan/01-bridge.yaml`:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: false
  bridges:
    br0:
      interfaces:
        - eth0
      dhcp4: true
```

#### Apply Netplan Configuration
```bash
# Test configuration
sudo netplan try

# Apply configuration
sudo netplan apply

# Debug configuration
sudo netplan --debug apply
```

[Related Commands/Topics: Legacy Network Configuration](#73-legacy-network-configuration) 🟡

#### Using /etc/network/interfaces (Debian/Ubuntu)
```bash
# Main configuration file
sudo nano /etc/network/interfaces

# Static IP configuration
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4

# DHCP configuration
auto eth0
iface eth0 inet dhcp
```

#### Using interfaces.d Directory
```bash
# Create interface-specific file
sudo nano /etc/network/interfaces.d/eth0

# Content of eth0 file
auto eth0
iface eth0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1

# Include in main interfaces file
echo "source /etc/network/interfaces.d/*" >> /etc/network/interfaces
```

#### NetworkManager with nmcli
```bash
# Create static connection
sudo nmcli con add type ethernet con-name static-eth0 \
    ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1

# Set DNS
sudo nmcli con modify static-eth0 ipv4.dns "8.8.8.8,8.8.4.4"

# Activate connection
sudo nmcli con up static-eth0

# Create DHCP connection
sudo nmcli con add type ethernet con-name dhcp-eth0 ifname eth0

# Show connections
nmcli con show
```

[Related Commands/Topics: DNS and Name Resolution](#74-dns-and-name-resolution) 🟡

#### Basic DNS Setup
```bash
# Edit resolv.conf (temporary)
sudo nano /etc/resolv.conf

nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com

# Configure systemd-resolved
sudo nano /etc/systemd/resolved.conf

[Resolve]
DNS=8.8.8.8 8.8.4.4
FallbackDNS=1.1.1.1
Domains=example.com

sudo systemctl restart systemd-resolved
```

#### DNS Testing
```bash
# Test DNS resolution
dig google.com
nslookup google.com
host google.com

# Check DNS configuration
systemd-resolve --status
cat /etc/resolv.conf

# Test specific DNS server
dig @8.8.8.8 google.com
```

#### Local Hosts File
```bash
# Edit hosts file
sudo nano /etc/hosts

# Add local entries
192.168.1.10    server.local
192.168.1.20    database.local
10.0.0.5        internal.example.com
```

[Related Commands/Topics: Basic Network Troubleshooting](#75-basic-network-troubleshooting) 🟡

#### Connectivity Testing
```bash
# Basic ping test
ping -c 4 google.com
ping -c 4 192.168.1.1

# Trace network path
traceroute google.com
mtr google.com

# Test specific ports
nc -zv google.com 80
nc -zv google.com 443
telnet google.com 80
```

#### Connection Analysis
```bash
# Show all network connections
ss -tulpn

# Show listening ports only
ss -tln

# Show established connections
ss -to state established

# Check specific port
ss -tlnp | grep :80

# Legacy netstat
netstat -tulpn
```

#### Packet Capture
```bash
# Basic packet capture
sudo tcpdump -i eth0

# Capture specific traffic
sudo tcpdump -i eth0 port 80
sudo tcpdump -i eth0 host google.com

# Save to file
sudo tcpdump -i eth0 -w capture.pcap

# Read from file
tcpdump -r capture.pcap
```

[Related Commands/Topics: Firewall Basics](#76-firewall-basics) 🟡

#### UFW (Ubuntu Firewall)
```bash
# Enable UFW
sudo ufw enable

# Basic rules
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Allow from specific network
sudo ufw allow from 192.168.1.0/24

# Deny specific port
sudo ufw deny 23

# Show status
sudo ufw status verbose

# Reset firewall
sudo ufw --force reset
```

#### Firewalld
```bash
# Start and enable firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld

# Show zones
sudo firewall-cmd --list-all-zones

# Add service to default zone
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https

# Add port
sudo firewall-cmd --permanent --add-port=8080/tcp

# Reload configuration
sudo firewall-cmd --reload

# Show current configuration
sudo firewall-cmd --list-all
```

#### Basic iptables
```bash
# View current rules
sudo iptables -L -n

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Drop all other input
sudo iptables -P INPUT DROP

# Save rules (Ubuntu/Debian)
sudo iptables-save > /etc/iptables/rules.v4
```

[Related Commands/Topics: SSH Configuration](#77-ssh-configuration) 🟡

#### Basic SSH Server Setup
```bash
# Edit SSH configuration
sudo nano /etc/ssh/sshd_config

# Key settings
Port 22
PermitRootLogin no
PasswordAuthentication yes  # Change to 'no' for key-only
PubkeyAuthentication yes
AllowUsers youruser

# Restart SSH service
sudo systemctl restart sshd
```

#### SSH Key Management
```bash
# Generate SSH key pair
ssh-keygen -t ed25519 -C "your.email@example.com"

# Copy public key to server
ssh-copy-id user@server

# Manual key copy
cat ~/.ssh/id_ed25519.pub | ssh user@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Test key authentication
ssh -i ~/.ssh/id_ed25519 user@server
```

#### SSH Security Hardening
```bash
# Enhanced SSH configuration
sudo nano /etc/ssh/sshd_config

Protocol 2
Port 2222  # Change default port
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
X11Forwarding no
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2

# Allow specific users only
AllowUsers alice bob

# Restart SSH
sudo systemctl restart sshd
```

[Related Commands/Topics: VPN Setup (WireGuard)](#78-vpn-setup-wireguard) 🟡

#### WireGuard Setup
```bash
# Install WireGuard
sudo apt install wireguard

# Generate server keys
wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey

# Server configuration
sudo nano /etc/wireguard/wg0.conf

[Interface]
PrivateKey = SERVER_PRIVATE_KEY
Address = 10.0.0.1/24
ListenPort = 51820
SaveConfig = true

[Peer]
PublicKey = CLIENT_PUBLIC_KEY
AllowedIPs = 10.0.0.2/32

# Start WireGuard
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0

# Client configuration
[Interface]
PrivateKey = CLIENT_PRIVATE_KEY
Address = 10.0.0.2/24
DNS = 8.8.8.8

[Peer]
PublicKey = SERVER_PUBLIC_KEY
Endpoint = server.example.com:51820
AllowedIPs = 0.0.0.0/0
```


## Lab Exercises
[⬆️ Back to Top](#table-of-contents)

### Lab 1: Basic Network Configuration

**Objective**: Configure network interfaces using different methods

**Tasks**:
1. **Interface Management**:
   - Use `ip a` to view current network interfaces
   - Bring an interface down and back up using `ip link`
   - Check interface status with `nmcli device status`

2. **Netplan Configuration**:
   - Create a static IP configuration using Netplan
   - Test the configuration with `netplan try`
   - Apply the configuration with `netplan apply`

3. **NetworkManager Setup**:
   - Create a connection using `nmcli`
   - Modify DNS settings
   - Switch between DHCP and static configurations

**Expected Results**:
- Successfully configure network interfaces
- Understand different configuration methods
- Verify connectivity after changes

### Lab 2: DNS and Network Troubleshooting

**Objective**: Configure DNS and troubleshoot network issues

**Tasks**:
1. **DNS Configuration**:
   - Configure DNS servers in `/etc/resolv.conf`
   - Add local entries to `/etc/hosts`
   - Test DNS resolution with `dig` and `nslookup`

2. **Troubleshooting**:
   - Use `ping` to test connectivity
   - Use `traceroute` to trace network paths
   - Use `ss` to check listening ports
   - Capture packets with `tcpdump`

3. **Connection Analysis**:
   - Monitor network connections with `ss -tulpn`
   - Test specific ports with `nc`
   - Identify network issues and their solutions

**Expected Results**:
- Configure and test DNS resolution
- Use troubleshooting tools effectively
- Diagnose and resolve connectivity issues

### Lab 3: Firewall Configuration

**Objective**: Set up basic firewall protection

**Tasks**:
1. **UFW Setup**:
   - Enable UFW firewall
   - Allow SSH, HTTP, and HTTPS
   - Allow connections from specific networks
   - Test firewall rules

2. **Firewalld Basic Configuration**:
   - Install and enable firewalld
   - Configure default zone
   - Add services and ports
   - Verify configurations

3. **Basic iptables**:
   - View current iptables rules
   - Add basic rules manually
   - Save and restore rules

**Expected Results**:
- Implement basic firewall security
- Understand different firewall tools
- Verify firewall functionality

### Lab 4: SSH Configuration and Security

**Objective**: Configure secure SSH access

**Tasks**:
1. **SSH Server Setup**:
   - Configure SSH server settings
   - Change default port (optional)
   - Disable root login
   - Restart SSH service

2. **SSH Key Management**:
   - Generate SSH key pairs
   - Copy public keys to servers
   - Test key-based authentication
   - Disable password authentication

3. **SSH Security**:
   - Implement additional security measures
   - Configure client connection settings
   - Test secure connections

**Expected Results**:
- Configure secure SSH server
- Implement key-based authentication
- Apply SSH security best practices

### Lab 5: VPN Setup (Optional Advanced Lab)

**Objective**: Set up basic WireGuard VPN

**Tasks**:
1. **WireGuard Configuration**:
   - Install WireGuard
   - Generate keys for server and client
   - Configure server and client
   - Test VPN connection

2. **WireGuard Management**:
   - Start and stop WireGuard connections
   - Monitor VPN status
   - Troubleshoot connection issues

**Expected Results**:
- Understand VPN concepts
- Configure basic WireGuard VPN connectivity
- Test secure tunneled connections


## Next Steps
[⬆️ Back to Top](#table-of-contents)

**Continue Learning**:
- **Advanced Networking**: Explore VLAN, bonding, and advanced routing
- **Network Automation**: Learn Ansible for network management
- **Monitoring**: Study network monitoring tools like Nagios or Zabbix
- **Security**: Dive deeper into network security practices

**Recommended Follow-up Modules**:
- Module 8: Logging and Monitoring
- Module 9: Shell Scripting (for network automation)
- Module 13: OpenSSH Best Practices

**Real-world Applications**:
- Configure production servers with secure networking
- Implement monitoring and alerting
- Automate network configuration tasks
- Troubleshoot network issues in enterprise environments

**Additional Resources**:
- Linux networking documentation
- Netplan documentation
- NetworkManager guides
- Firewall best practices guides

Master these networking fundamentals to build a solid foundation for Linux system administration and network management.
