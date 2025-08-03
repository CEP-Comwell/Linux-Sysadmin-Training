# Module 7: Networking Fundamentals

## Overview
This module covers Linux networking fundamentals including network configuration, troubleshooting, firewalls, and network services. You'll learn to configure network interfaces, manage routing, and secure network communications.

## Learning Objectives
By the end of this module, you will be able to:
- Configure network interfaces and routing
- Troubleshoot network connectivity issues
- Implement firewall rules and network security
- Configure and manage network services
- Monitor network traffic and performance
- Understand network protocols and services

## Topics

### 7.1 Network Fundamentals
- OSI model and TCP/IP stack
- IP addressing and subnetting
- Network interfaces and devices
- Network configuration files
- Network namespaces

### 7.2 Network Interface Configuration
- Static vs DHCP configuration
- NetworkManager and systemd-networkd
- Legacy network tools vs modern alternatives
- Bonding and bridging
- VLAN configuration

### 7.3 Routing and Gateway Management
- Routing tables and routes
- Default gateway configuration
- Static routing
- Policy-based routing
- Route troubleshooting

### 7.4 Network Troubleshooting Tools
- Connectivity testing: `ping`, `traceroute`
- Port scanning: `nmap`, `netstat`, `ss`
- DNS resolution: `dig`, `nslookup`, `host`
- Network analysis: `tcpdump`, `wireshark`
- Bandwidth testing: `iperf`, `speedtest`

### 7.5 Firewall Management
- iptables fundamentals
- UFW (Uncomplicated Firewall)
- firewalld for Red Hat systems
- Network security best practices
- Port forwarding and NAT

### 7.6 Network Services
- SSH configuration and security
- DNS server configuration
- Web server networking
- Network Time Protocol (NTP)
- Network file systems (NFS, CIFS)

## Practical Examples

### Network Interface Configuration

#### Using NetworkManager (Modern Systems)
```bash
# List network connections
nmcli connection show

# Show device status
nmcli device status

# Create static IP connection
sudo nmcli connection add type ethernet con-name static-eth0 \
    ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1

# Set DNS servers
sudo nmcli connection modify static-eth0 ipv4.dns "8.8.8.8 8.8.4.4"

# Activate connection
sudo nmcli connection up static-eth0

# Configure DHCP connection
sudo nmcli connection add type ethernet con-name dhcp-eth0 ifname eth0
```

#### Using systemd-networkd
```bash
# Create network configuration file
sudo tee /etc/systemd/network/eth0.network << EOF
[Match]
Name=eth0

[Network]
DHCP=yes
EOF

# Enable systemd-networkd
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
```

#### Legacy ifconfig Method
```bash
# Configure IP address
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0

# Add default route
sudo route add default gw 192.168.1.1

# Make permanent (Debian/Ubuntu)
sudo tee /etc/network/interfaces << EOF
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
EOF
```

### Routing Configuration
```bash
# Show routing table
ip route show
route -n

# Add static route
sudo ip route add 10.0.0.0/8 via 192.168.1.1

# Delete route
sudo ip route del 10.0.0.0/8

# Add persistent route (Red Hat/CentOS)
echo "10.0.0.0/8 via 192.168.1.1" | sudo tee -a /etc/sysconfig/network-scripts/route-eth0

# Show ARP table
ip neighbor show
arp -a
```

### Network Troubleshooting
```bash
# Test connectivity
ping google.com
ping -c 4 8.8.8.8

# Trace route to destination
traceroute google.com
mtr google.com

# Test specific ports
telnet google.com 80
nc -zv google.com 80-443

# DNS lookup
dig google.com
nslookup google.com
host google.com

# Show network connections
ss -tulpn
netstat -tulpn

# Show network statistics
ss -s
netstat -i

# Capture network traffic
sudo tcpdump -i eth0 -n
sudo tcpdump -i any port 80

# Network scanning
nmap -sP 192.168.1.0/24
nmap -sS -O 192.168.1.1
```

### Firewall Configuration

#### UFW (Ubuntu Firewall)
```bash
# Enable UFW
sudo ufw enable

# Default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow specific services
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Allow from specific IP
sudo ufw allow from 192.168.1.100

# Block specific IP
sudo ufw deny from 192.168.1.200

# Delete rule
sudo ufw delete allow 80/tcp

# Show status
sudo ufw status verbose

# Reset to defaults
sudo ufw --force reset
```

#### iptables
```bash
# List current rules
sudo iptables -L -n -v

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP and HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Allow established connections
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Drop all other input
sudo iptables -P INPUT DROP

# Save rules (Ubuntu/Debian)
sudo iptables-save | sudo tee /etc/iptables/rules.v4

# Restore rules
sudo iptables-restore < /etc/iptables/rules.v4
```

#### firewalld (Red Hat/CentOS)
```bash
# Start and enable firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld

# Show zones
sudo firewall-cmd --get-zones

# Show active zones
sudo firewall-cmd --get-active-zones

# Add service to zone
sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=https --permanent

# Add port to zone
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent

# Reload firewall
sudo firewall-cmd --reload

# Show configuration
sudo firewall-cmd --list-all
```

## Network Configuration Files

### Debian/Ubuntu
```bash
# /etc/network/interfaces
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4

# /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
```

### Red Hat/CentOS
```bash
# /etc/sysconfig/network-scripts/ifcfg-eth0
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
```

## Network Services Configuration

### SSH Server Hardening
```bash
# /etc/ssh/sshd_config
Port 2222
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
ClientAliveInterval 600
ClientAliveCountMax 0
X11Forwarding no

# Restart SSH service
sudo systemctl restart sshd
```

### DNS Configuration
```bash
# Configure DNS resolver
sudo tee /etc/systemd/resolved.conf << EOF
[Resolve]
DNS=8.8.8.8 8.8.4.4
FallbackDNS=1.1.1.1 1.0.0.1
Domains=example.com
EOF

sudo systemctl restart systemd-resolved
```

## Network Monitoring and Analysis

### Bandwidth Monitoring
```bash
# Monitor interface traffic
watch -n 1 cat /proc/net/dev

# Use iftop for real-time monitoring
sudo iftop -i eth0

# Network statistics
sar -n DEV 1 5

# Bandwidth testing
iperf3 -s  # Server mode
iperf3 -c server_ip  # Client mode
```

### Traffic Analysis
```bash
# Capture HTTP traffic
sudo tcpdump -i eth0 -A 'port 80'

# Capture and save to file
sudo tcpdump -i eth0 -w capture.pcap

# Monitor specific host
sudo tcpdump -i eth0 host 192.168.1.100

# Monitor DNS queries
sudo tcpdump -i eth0 port 53
```

## Common Network Issues and Solutions

| Issue | Symptoms | Troubleshooting Steps |
|-------|----------|----------------------|
| No Internet | Can't reach external sites | Check cable, IP config, gateway, DNS |
| Slow Network | High latency, low throughput | Check bandwidth, congestion, MTU |
| DNS Issues | Sites unreachable by name | Test DNS servers, check /etc/resolv.conf |
| Port Blocked | Service unreachable | Check firewall, service status, listening ports |
| Wrong IP | Unexpected IP address | Check DHCP, static config, conflicts |

## Network Security Best Practices

| Practice | Description |
|----------|-------------|
| Change Default Ports | Use non-standard ports for services |
| Enable Firewall | Block unnecessary ports and services |
| Use SSH Keys | Disable password authentication |
| Monitor Traffic | Log and analyze network activity |
| Segment Networks | Use VLANs and subnets |
| Regular Updates | Keep network services updated |
| Strong Encryption | Use secure protocols (SSH, HTTPS, VPN) |

## Lab Exercises
1. Configure static network settings and test connectivity
2. Set up firewall rules for a web server
3. Troubleshoot network connectivity issues
4. Configure network bonding or bridging
5. Implement network monitoring and alerting

## Next Steps
With networking fundamentals mastered, you're ready to explore Logging & Monitoring in Module 8, where you'll learn to manage system logs and implement comprehensive monitoring solutions.
