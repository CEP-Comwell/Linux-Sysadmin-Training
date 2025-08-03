# Module 7: Networking Fundamentals

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics Covered](#topics-covered)
  - [7.1 Network Interface Management](#71-network-interface-management)
  - [7.2 IP Configuration and Routing](#72-ip-configuration-and-routing)
  - [7.3 DNS and Name Resolution](#73-dns-and-name-resolution)
  - [7.4 Network Diagnostics and Troubleshooting](#74-network-diagnostics-and-troubleshooting)
  - [7.5 Firewall Configuration and Management](#75-firewall-configuration-and-management)
  - [7.6 SSH Security and Remote Access](#76-ssh-security-and-remote-access)
  - [7.7 Network Monitoring and Performance](#77-network-monitoring-and-performance)
  - [7.8 VPN and Secure Tunneling](#78-vpn-and-secure-tunneling)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Network Interface Management](#network-interface-management)
  - [Advanced IP Configuration](#advanced-ip-configuration)
  - [DNS and Name Resolution](#dns-and-name-resolution)
  - [Network Troubleshooting Tools](#network-troubleshooting-tools)
  - [Enterprise Firewall Management](#enterprise-firewall-management)
  - [SSH Security Hardening](#ssh-security-hardening)
  - [Network Monitoring and Analysis](#network-monitoring-and-analysis)
  - [VPN Configuration and Management](#vpn-configuration-and-management)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Network Configuration and Management](#lab-1-network-configuration-and-management)
  - [Lab 2: Firewall Security Implementation](#lab-2-firewall-security-implementation)
  - [Lab 3: SSH Infrastructure Hardening](#lab-3-ssh-infrastructure-hardening)
  - [Lab 4: Network Monitoring and Troubleshooting](#lab-4-network-monitoring-and-troubleshooting)
  - [Lab 5: VPN and Secure Remote Access](#lab-5-vpn-and-secure-remote-access)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview

This module provides comprehensive coverage of Linux networking fundamentals, from basic interface configuration to advanced security implementations. Students will master modern network management tools, implement enterprise-grade security measures, and develop skills for maintaining robust network infrastructure in production environments.

**Module Focus Areas:**
- Modern network interface management with NetworkManager and systemd-networkd
- Advanced IP configuration, routing, and VLAN management
- DNS infrastructure and name resolution troubleshooting
- Enterprise firewall configuration with multiple management systems
- SSH security hardening and key management at scale
- Network monitoring, performance analysis, and capacity planning
- VPN implementations for secure remote access

## Learning Objectives

By the end of this module, you will be able to:

1. **Configure Network Interfaces**: Master modern tools like NetworkManager, systemd-networkd, and legacy configurations
2. **Implement IP Management**: Configure static/dynamic IP addressing, routing tables, and VLAN networking
3. **Manage DNS Infrastructure**: Configure resolvers, implement caching, and troubleshoot name resolution
4. **Diagnose Network Issues**: Use advanced diagnostic tools to identify and resolve connectivity problems
5. **Secure Network Access**: Implement comprehensive firewall rules and SSH security hardening
6. **Monitor Network Performance**: Deploy monitoring solutions and analyze network traffic patterns
7. **Design Secure Architecture**: Plan and implement enterprise-grade network security measures
8. **Automate Network Tasks**: Create scripts for network management, monitoring, and incident response

## Topics Covered

### 7.1 Network Interface Management
- Modern interface naming conventions (predictable network interface names)
- NetworkManager command-line and configuration management
- systemd-networkd configuration and integration
- Legacy ifconfig and network scripts (backward compatibility)
- Bonding, bridging, and VLAN configuration
- Wireless interface management and enterprise authentication

### 7.2 IP Configuration and Routing
- Static and dynamic IP address assignment
- Advanced routing configuration and policy routing
- Network namespaces and container networking
- IPv6 configuration and dual-stack implementations
- DHCP client and server configuration
- Network address translation (NAT) and port forwarding

### 7.3 DNS and Name Resolution
- DNS resolver configuration and optimization
- Local DNS caching with systemd-resolved
- DNS over HTTPS (DoH) and DNS over TLS (DoT)
- Host file management and local name resolution
- DNS troubleshooting and query analysis
- Split-horizon DNS for complex environments

### 7.4 Network Diagnostics and Troubleshooting
- Layer 2 and Layer 3 connectivity testing
- Advanced packet analysis with tcpdump and Wireshark
- Network performance testing and bandwidth analysis
- MTU discovery and path optimization
- Network latency and jitter measurement
- Automated network health monitoring

### 7.5 Firewall Configuration and Management
- iptables/netfilter framework and rule management
- firewalld zone-based configuration for enterprise environments
- UFW simplified firewall management for Ubuntu systems
- Application-level firewall rules and service management
- Connection tracking and stateful inspection
- DDoS protection and rate limiting implementations

### 7.6 SSH Security and Remote Access
- SSH server hardening and security best practices
- Key-based authentication and certificate management
- SSH tunneling, port forwarding, and jump hosts
- Multi-factor authentication integration
- SSH session monitoring and audit logging
- Automated SSH security compliance checking

### 7.7 Network Monitoring and Performance
- Real-time network traffic analysis and alerting
- Bandwidth monitoring and capacity planning
- Network protocol analysis and optimization
- Performance metrics collection and visualization
- Network inventory and asset management
- Incident response and escalation procedures

### 7.8 VPN and Secure Tunneling
- OpenVPN server and client configuration
- WireGuard modern VPN implementation
- IPSec VPN tunnels for site-to-site connectivity
- SSL/TLS VPN solutions for remote access
- VPN performance optimization and troubleshooting
- Certificate management for VPN infrastructure
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

**🔗 Practical Examples**: [Viewing Interface Information](Module7_Networking_Fundamentals.md#viewing-interface-information) | [Interface State Management](Module7_Networking_Fundamentals.md#interface-state-management)

### 7.2 IP Address Configuration and Management
- Static vs dynamic IP addressing strategies
- Configuring addresses via CLI tools and configuration files
- NetworkManager and systemd-networkd management
- Persistent network configuration across reboots
- DHCP client configuration and troubleshooting

**🔗 Practical Examples**: [NetworkManager Configuration](Module7_Networking_Fundamentals.md#static-ip-configuration-with-networkmanager) | [systemd-networkd Setup](Module7_Networking_Fundamentals.md#using-systemd-networkd) | [Legacy Methods](Module7_Networking_Fundamentals.md#legacy-network-configuration)

### 7.3 DNS Resolution and Host Management
- DNS resolution configuration in `/etc/resolv.conf`
- Local host resolution with `/etc/hosts`
- DNS troubleshooting with `dig`, `nslookup`, and `host`
- systemd-resolved configuration and management

**🔗 Practical Examples**: [DNS Configuration and Testing](Module7_Networking_Fundamentals.md#dns-configuration-and-testing)

### 7.4 Network Connectivity Diagnostics
- Connectivity testing with `ping` and advanced options
- Path tracing with `traceroute` and `mtr`
- Port and service checking with `netstat`, `ss`, and `nmap`
- Network performance analysis and bandwidth testing

**🔗 Practical Examples**: [Comprehensive Connectivity Testing](Module7_Networking_Fundamentals.md#comprehensive-connectivity-testing)

### 7.5 SSH Security and Hardening
- SSH server configuration and `/etc/ssh/sshd_config` hardening
- Key-based authentication setup and management
- Disabling password authentication and changing default ports
- SSH client configuration and connection management
- Advanced SSH features: tunneling, port forwarding, and agent forwarding

**🔗 Practical Examples**: [SSH Server Hardening](Module7_Networking_Fundamentals.md#ssh-server-configuration-and-hardening) | [SSH Key Management](Module7_Networking_Fundamentals.md#ssh-key-management)

### 7.6 Comprehensive Firewall Management
- Zone-based firewall management with `firewalld`
- Legacy firewall tools: `iptables` and `nftables`
- UFW (Uncomplicated Firewall) for simplified management
- Rich rules and advanced filtering techniques
- NAT, port forwarding, and traffic redirection

**🔗 Practical Examples**: [firewalld Management](Module7_Networking_Fundamentals.md#firewalld-zone-based-management) | [iptables Configuration](Module7_Networking_Fundamentals.md#iptables-legacy-firewall-management) | [UFW Setup](Module7_Networking_Fundamentals.md#ufw-simplified-firewall-management)

### 7.7 Network Security Best Practices
- Host-level security implementations
- Network service hardening
- Intrusion detection and prevention
- Security monitoring and log analysis

**🔗 Practical Examples**: [Host-Level Security Implementation](Module7_Networking_Fundamentals.md#host-level-security-implementation) | [Security Monitoring](Module7_Networking_Fundamentals.md#network-security-monitoring)

## Essential Command Reference

### Network Interface Management
| Command | Description | Example |
|---------|-------------|---------|
| `ip a` | Show all network interfaces and addresses | `ip a show eth0` |
| `ip link show` | Display interface link status | `ip link show` |
| `ip link set` | Configure interface state | `ip link set eth0 up` |
| `nmcli device` | NetworkManager device management | `nmcli device status` |
| `nmcli connection` | NetworkManager connection management | `nmcli connection show` |

### IP Configuration and Routing
| Command | Description | Example |
|---------|-------------|---------|
| `ip addr add` | Add IP address to interface | `ip addr add 192.168.1.10/24 dev eth0` |
| `ip route show` | Display routing table | `ip route show` |
| `ip route add` | Add route to routing table | `ip route add 10.0.0.0/8 via 192.168.1.1` |
| `dhclient` | DHCP client configuration | `dhclient eth0` |
| `systemd-resolve` | Resolve DNS queries | `systemd-resolve --status` |

### Network Diagnostics
| Command | Description | Example |
|---------|-------------|---------|
| `ping` | Test network connectivity | `ping -c 4 google.com` |
| `traceroute` | Trace packet path | `traceroute 8.8.8.8` |
| `mtr` | Network diagnostic tool | `mtr --report google.com` |
| `ss` | Socket statistics | `ss -tulpn` |
| `netstat` | Network connections (legacy) | `netstat -tulpn` |
| `tcpdump` | Packet capture and analysis | `tcpdump -i eth0 port 80` |
| `nmap` | Network scanning and discovery | `nmap -sn 192.168.1.0/24` |

### DNS and Name Resolution
| Command | Description | Example |
|---------|-------------|---------|
| `dig` | DNS lookup utility | `dig google.com A` |
| `nslookup` | DNS query tool | `nslookup google.com` |
| `host` | DNS lookup utility | `host google.com` |
| `systemd-resolve` | Modern DNS resolver | `systemd-resolve google.com` |
| `resolvectl` | Resolve configuration | `resolvectl status` |

### Firewall Management
| Command | Description | Example |
|---------|-------------|---------|
| `firewall-cmd` | firewalld management | `firewall-cmd --list-all` |
| `iptables` | Legacy firewall rules | `iptables -L -n` |
| `ufw` | Uncomplicated Firewall | `ufw status verbose` |
| `nft` | nftables management | `nft list tables` |

### SSH and Remote Access
| Command | Description | Example |
|---------|-------------|---------|
| `ssh` | Secure shell client | `ssh user@hostname` |
| `ssh-keygen` | Generate SSH keys | `ssh-keygen -t ed25519` |
| `ssh-copy-id` | Copy SSH keys | `ssh-copy-id user@hostname` |
| `scp` | Secure copy | `scp file.txt user@host:/path/` |
| `rsync` | Remote synchronization | `rsync -av /local/ user@host:/remote/` |

### Network Monitoring
| Command | Description | Example |
|---------|-------------|---------|
| `iftop` | Network bandwidth monitor | `iftop -i eth0` |
| `nethogs` | Process network usage | `nethogs eth0` |
| `vnstat` | Network statistics | `vnstat -i eth0` |
| `iotop` | I/O monitor | `iotop -o` |
| `lsof` | List open files/network connections | `lsof -i :80` |

## Practical Examples

### Network Interface Management

#### Modern Interface Management Script
```bash
#!/bin/bash
# network-interface.sh - Comprehensive network interface management

# Function to display interface information
show_interface_info() {
    local interface="$1"
    
    if [[ -z "$interface" ]]; then
        echo "Usage: show_interface_info <interface>"
        return 1
    fi
    
    echo "=== Interface Information for $interface ==="
    
    # Basic interface information
    echo "Link Status:"
    ip link show "$interface" 2>/dev/null || { echo "Interface $interface not found"; return 1; }
    
    echo ""
    echo "IP Addresses:"
    ip addr show "$interface" | grep -E "inet6?|link"
    
    echo ""
    echo "Interface Statistics:"
    ip -s link show "$interface" | grep -A2 "RX:\|TX:"
    
    echo ""
    echo "Interface Speed and Duplex:"
    if [[ -f "/sys/class/net/$interface/speed" ]]; then
        local speed=$(cat "/sys/class/net/$interface/speed" 2>/dev/null)
        local duplex=$(cat "/sys/class/net/$interface/duplex" 2>/dev/null)
        echo "Speed: ${speed:-Unknown} Mbps"
        echo "Duplex: ${duplex:-Unknown}"
    else
        echo "Speed/Duplex information not available"
    fi
    
    echo ""
    echo "Driver Information:"
    if command -v ethtool &>/dev/null; then
        ethtool -i "$interface" 2>/dev/null | head -5
    else
        echo "ethtool not available"
    fi
    
    # NetworkManager information if available
    if command -v nmcli &>/dev/null; then
        echo ""
        echo "NetworkManager Status:"
        nmcli device show "$interface" 2>/dev/null | head -10
    fi
}

# Function to configure interface with NetworkManager
configure_interface_nm() {
    local interface="$1"
    local ip_address="$2"
    local gateway="$3"
    local dns="$4"
    local connection_name="${5:-$interface-static}"
    
    if [[ -z "$interface" || -z "$ip_address" ]]; then
        echo "Usage: configure_interface_nm <interface> <ip/prefix> [gateway] [dns] [connection_name]"
        echo "Example: configure_interface_nm eth0 192.168.1.100/24 192.168.1.1 8.8.8.8"
        return 1
    fi
    
    echo "Configuring interface $interface with NetworkManager..."
    
    # Remove existing connections for this interface
    local existing_connections=$(nmcli -t -f NAME,DEVICE connection show | grep ":$interface$" | cut -d: -f1)
    for conn in $existing_connections; do
        echo "Removing existing connection: $conn"
        nmcli connection delete "$conn" 2>/dev/null
    done
    
    # Create new connection
    local cmd="nmcli connection add type ethernet con-name '$connection_name' ifname '$interface' ip4 '$ip_address'"
    
    if [[ -n "$gateway" ]]; then
        cmd+=" gw4 '$gateway'"
    fi
    
    if [[ -n "$dns" ]]; then
        cmd+=" ipv4.dns '$dns'"
    fi
    
    cmd+=" ipv4.method manual"
    
    echo "Executing: $cmd"
    eval "$cmd"
    
    if [[ $? -eq 0 ]]; then
        echo "Activating connection..."
        nmcli connection up "$connection_name"
        echo "Interface $interface configured successfully"
        
        # Display configuration
        echo ""
        echo "New Configuration:"
        nmcli connection show "$connection_name" | grep -E "ipv4\.(addresses|gateway|dns)"
    else
        echo "Failed to configure interface"
        return 1
    fi
}

# Function to configure interface with ip command (temporary)
configure_interface_ip() {
    local interface="$1"
    local ip_address="$2"
    local gateway="$3"
    
    if [[ -z "$interface" || -z "$ip_address" ]]; then
        echo "Usage: configure_interface_ip <interface> <ip/prefix> [gateway]"
        echo "Example: configure_interface_ip eth0 192.168.1.100/24 192.168.1.1"
        return 1
    fi
    
    echo "Configuring interface $interface with ip command (temporary)..."
    
    # Configure IP address
    sudo ip addr flush dev "$interface"
    sudo ip addr add "$ip_address" dev "$interface"
    sudo ip link set "$interface" up
    
    # Configure gateway if provided
    if [[ -n "$gateway" ]]; then
        # Remove existing default routes for this interface
        sudo ip route del default dev "$interface" 2>/dev/null || true
        sudo ip route add default via "$gateway" dev "$interface"
    fi
    
    echo "Interface $interface configured with IP: $ip_address"
    if [[ -n "$gateway" ]]; then
        echo "Gateway: $gateway"
    fi
    
    # Show current configuration
    echo ""
    echo "Current Configuration:"
    ip addr show "$interface"
    echo ""
    echo "Routing Table:"
    ip route show dev "$interface"
}

# Function to create network bridge
create_bridge() {
    local bridge_name="$1"
    local interface="$2"
    local bridge_ip="$3"
    
    if [[ -z "$bridge_name" || -z "$interface" ]]; then
        echo "Usage: create_bridge <bridge_name> <interface> [bridge_ip]"
        echo "Example: create_bridge br0 eth0 192.168.1.50/24"
        return 1
    fi
    
    echo "Creating bridge $bridge_name with interface $interface..."
    
    # Create bridge
    sudo ip link add name "$bridge_name" type bridge
    sudo ip link set "$bridge_name" up
    
    # Add interface to bridge
    sudo ip link set "$interface" master "$bridge_name"
    sudo ip link set "$interface" up
    
    # Configure bridge IP if provided
    if [[ -n "$bridge_ip" ]]; then
        sudo ip addr add "$bridge_ip" dev "$bridge_name"
    fi
    
    echo "Bridge $bridge_name created successfully"
    echo "Bridge configuration:"
    ip addr show "$bridge_name"
    
    echo ""
    echo "Bridge details:"
    sudo bridge link show
}

# Function to create VLAN interface
create_vlan() {
    local parent_interface="$1"
    local vlan_id="$2"
    local vlan_ip="$3"
    
    if [[ -z "$parent_interface" || -z "$vlan_id" ]]; then
        echo "Usage: create_vlan <parent_interface> <vlan_id> [vlan_ip]"
        echo "Example: create_vlan eth0 100 192.168.100.10/24"
        return 1
    fi
    
    local vlan_interface="${parent_interface}.${vlan_id}"
    
    echo "Creating VLAN $vlan_id on interface $parent_interface..."
    
    # Create VLAN interface
    sudo ip link add link "$parent_interface" name "$vlan_interface" type vlan id "$vlan_id"
    sudo ip link set "$vlan_interface" up
    
    # Configure VLAN IP if provided
    if [[ -n "$vlan_ip" ]]; then
        sudo ip addr add "$vlan_ip" dev "$vlan_interface"
    fi
    
    echo "VLAN interface $vlan_interface created successfully"
    echo "VLAN configuration:"
    ip addr show "$vlan_interface"
}

# Function to monitor interface traffic
monitor_interface() {
    local interface="$1"
    local duration="${2:-10}"
    
    if [[ -z "$interface" ]]; then
        echo "Usage: monitor_interface <interface> [duration_seconds]"
        echo "Example: monitor_interface eth0 30"
        return 1
    fi
    
    if ! ip link show "$interface" &>/dev/null; then
        echo "Interface $interface not found"
        return 1
    fi
    
    echo "Monitoring interface $interface for $duration seconds..."
    echo "Press Ctrl+C to stop"
    
    # Get initial statistics
    local stats_file="/sys/class/net/$interface/statistics"
    local rx_bytes_start=$(cat "$stats_file/rx_bytes")
    local tx_bytes_start=$(cat "$stats_file/tx_bytes")
    local rx_packets_start=$(cat "$stats_file/rx_packets")
    local tx_packets_start=$(cat "$stats_file/tx_packets")
    
    sleep "$duration"
    
    # Get final statistics
    local rx_bytes_end=$(cat "$stats_file/rx_bytes")
    local tx_bytes_end=$(cat "$stats_file/tx_bytes")
    local rx_packets_end=$(cat "$stats_file/rx_packets")
    local tx_packets_end=$(cat "$stats_file/tx_packets")
    
    # Calculate differences
    local rx_bytes_diff=$((rx_bytes_end - rx_bytes_start))
    local tx_bytes_diff=$((tx_bytes_end - tx_bytes_start))
    local rx_packets_diff=$((rx_packets_end - rx_packets_start))
    local tx_packets_diff=$((tx_packets_end - tx_packets_start))
    
    # Convert bytes to human readable format
    local rx_mbps=$(echo "scale=2; $rx_bytes_diff * 8 / $duration / 1000000" | bc -l)
    local tx_mbps=$(echo "scale=2; $tx_bytes_diff * 8 / $duration / 1000000" | bc -l)
    
    echo ""
    echo "=== Traffic Statistics for $interface ($duration seconds) ==="
    echo "Received: $rx_packets_diff packets, $(numfmt --to=iec $rx_bytes_diff)B (${rx_mbps} Mbps)"
    echo "Transmitted: $tx_packets_diff packets, $(numfmt --to=iec $tx_bytes_diff)B (${tx_mbps} Mbps)"
}

# Usage function
usage() {
    echo "Usage: $0 {show|configure-nm|configure-ip|bridge|vlan|monitor} [arguments]"
    echo ""
    echo "Commands:"
    echo "  show <interface>                              - Show interface information"
    echo "  configure-nm <interface> <ip/prefix> [gw] [dns] [name] - Configure with NetworkManager"
    echo "  configure-ip <interface> <ip/prefix> [gw]     - Configure with ip command (temporary)"
    echo "  bridge <bridge_name> <interface> [bridge_ip] - Create network bridge"
    echo "  vlan <parent_interface> <vlan_id> [vlan_ip]  - Create VLAN interface"
    echo "  monitor <interface> [duration]               - Monitor interface traffic"
    echo ""
    echo "Examples:"
    echo "  $0 show eth0"
    echo "  $0 configure-nm eth0 192.168.1.100/24 192.168.1.1 8.8.8.8"
    echo "  $0 configure-ip eth0 192.168.1.100/24 192.168.1.1"
    echo "  $0 bridge br0 eth0 192.168.1.50/24"
    echo "  $0 vlan eth0 100 192.168.100.10/24"
    echo "  $0 monitor eth0 30"
}

# Main script logic
case "${1:-help}" in
    "show")
        show_interface_info "$2"
        ;;
    "configure-nm")
        configure_interface_nm "$2" "$3" "$4" "$5" "$6"
        ;;
    "configure-ip")
        configure_interface_ip "$2" "$3" "$4"
        ;;
    "bridge")
        create_bridge "$2" "$3" "$4"
        ;;
    "vlan")
        create_vlan "$2" "$3" "$4"
        ;;
    "monitor")
        monitor_interface "$2" "$3"
        ;;
    "help"|*)
        usage
        ;;
esac
```

### DNS and Name Resolution

#### DNS Management and Testing Script
```bash
#!/bin/bash
# dns-management.sh - Comprehensive DNS management and testing

# Function to configure DNS servers
configure_dns() {
    local method="$1"
    shift
    local dns_servers=("$@")
    
    if [[ -z "$method" || ${#dns_servers[@]} -eq 0 ]]; then
        echo "Usage: configure_dns <method> <dns1> [dns2] [dns3] ..."
        echo "Methods: systemd-resolved, resolvconf, manual"
        echo "Example: configure_dns systemd-resolved 8.8.8.8 8.8.4.4 1.1.1.1"
        return 1
    fi
    
    case "$method" in
        "systemd-resolved")
            echo "Configuring DNS using systemd-resolved..."
            
            # Configure global DNS
            local dns_config="/etc/systemd/resolved.conf"
            sudo cp "$dns_config" "${dns_config}.backup"
            
            cat > /tmp/resolved.conf << EOF
[Resolve]
DNS=${dns_servers[*]}
FallbackDNS=8.8.8.8 8.8.4.4
Domains=~.
DNSSEC=yes
DNSOverTLS=opportunistic
Cache=yes
DNSStubListener=yes
EOF
            
            sudo mv /tmp/resolved.conf "$dns_config"
            
            # Restart systemd-resolved
            sudo systemctl restart systemd-resolved
            
            # Update /etc/resolv.conf symlink
            sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
            
            echo "DNS configuration completed using systemd-resolved"
            ;;
            
        "resolvconf")
            echo "Configuring DNS using resolvconf..."
            
            if ! command -v resolvconf &>/dev/null; then
                echo "resolvconf not available, installing..."
                if command -v apt &>/dev/null; then
                    sudo apt update && sudo apt install -y resolvconf
                elif command -v yum &>/dev/null; then
                    sudo yum install -y openresolv
                else
                    echo "Cannot install resolvconf automatically"
                    return 1
                fi
            fi
            
            # Configure DNS servers
            for i in "${!dns_servers[@]}"; do
                echo "nameserver ${dns_servers[$i]}" | sudo resolvconf -a "lo.dns$((i+1))"
            done
            
            echo "DNS configuration completed using resolvconf"
            ;;
            
        "manual")
            echo "Configuring DNS manually in /etc/resolv.conf..."
            
            # Backup original resolv.conf
            sudo cp /etc/resolv.conf /etc/resolv.conf.backup
            
            # Create new resolv.conf
            cat > /tmp/resolv.conf << EOF
# Generated by dns-management.sh
# Date: $(date)
EOF
            
            for dns_server in "${dns_servers[@]}"; do
                echo "nameserver $dns_server" >> /tmp/resolv.conf
            done
            
            # Add search domains
            echo "search local" >> /tmp/resolv.conf
            echo "options timeout:2 attempts:3" >> /tmp/resolv.conf
            
            sudo mv /tmp/resolv.conf /etc/resolv.conf
            
            echo "DNS configuration completed manually"
            ;;
            
        *)
            echo "Unknown method: $method"
            return 1
            ;;
    esac
    
    echo ""
    echo "Current DNS configuration:"
    cat /etc/resolv.conf
}

# Function to test DNS resolution
test_dns() {
    local domain="$1"
    local record_type="${2:-A}"
    local dns_server="$3"
    
    if [[ -z "$domain" ]]; then
        echo "Usage: test_dns <domain> [record_type] [dns_server]"
        echo "Record types: A, AAAA, MX, TXT, NS, CNAME, PTR"
        echo "Example: test_dns google.com A 8.8.8.8"
        return 1
    fi
    
    echo "Testing DNS resolution for $domain (type: $record_type)"
    if [[ -n "$dns_server" ]]; then
        echo "Using DNS server: $dns_server"
    fi
    
    echo ""
    
    # Test with dig
    if command -v dig &>/dev/null; then
        echo "=== dig results ==="
        local dig_cmd="dig"
        if [[ -n "$dns_server" ]]; then
            dig_cmd+=" @$dns_server"
        fi
        dig_cmd+=" $domain $record_type +short"
        
        eval "$dig_cmd"
        echo ""
        
        # Detailed dig output
        echo "=== Detailed dig output ==="
        dig_cmd="dig"
        if [[ -n "$dns_server" ]]; then
            dig_cmd+=" @$dns_server"
        fi
        dig_cmd+=" $domain $record_type"
        
        eval "$dig_cmd"
    fi
    
    echo ""
    
    # Test with nslookup
    if command -v nslookup &>/dev/null; then
        echo "=== nslookup results ==="
        if [[ -n "$dns_server" ]]; then
            nslookup "$domain" "$dns_server"
        else
            nslookup "$domain"
        fi
    fi
    
    echo ""
    
    # Test with host
    if command -v host &>/dev/null; then
        echo "=== host results ==="
        local host_cmd="host -t $record_type $domain"
        if [[ -n "$dns_server" ]]; then
            host_cmd+=" $dns_server"
        fi
        
        eval "$host_cmd"
    fi
    
    echo ""
    
    # Test with systemd-resolve
    if command -v systemd-resolve &>/dev/null; then
        echo "=== systemd-resolve results ==="
        systemd-resolve "$domain"
    fi
}

# Function to perform comprehensive DNS benchmarking
benchmark_dns() {
    local domains=("${@:-google.com cloudflare.com github.com stackoverflow.com}")
    local dns_servers=("8.8.8.8" "8.8.4.4" "1.1.1.1" "1.0.0.1" "9.9.9.9")
    
    echo "Benchmarking DNS servers..."
    echo "Testing domains: ${domains[*]}"
    echo "DNS servers: ${dns_servers[*]}"
    echo ""
    
    # Create results file
    local results_file="/tmp/dns_benchmark_$(date +%Y%m%d_%H%M%S).txt"
    echo "DNS Benchmark Results - $(date)" > "$results_file"
    echo "===============================" >> "$results_file"
    echo "" >> "$results_file"
    
    for dns_server in "${dns_servers[@]}"; do
        echo "Testing DNS server: $dns_server"
        local total_time=0
        local successful_queries=0
        
        for domain in "${domains[@]}"; do
            local start_time=$(date +%s.%N)
            
            if dig @"$dns_server" "$domain" A +short +time=3 &>/dev/null; then
                local end_time=$(date +%s.%N)
                local query_time=$(echo "$end_time - $start_time" | bc -l)
                total_time=$(echo "$total_time + $query_time" | bc -l)
                ((successful_queries++))
                
                printf "  %-20s: %.3fs\n" "$domain" "$query_time"
            else
                printf "  %-20s: FAILED\n" "$domain"
            fi
        done
        
        if [[ $successful_queries -gt 0 ]]; then
            local avg_time=$(echo "scale=3; $total_time / $successful_queries" | bc -l)
            printf "  Average time: %.3fs (%d/%d successful)\n" "$avg_time" "$successful_queries" "${#domains[@]}"
            
            # Log to results file
            echo "$dns_server: Average ${avg_time}s (${successful_queries}/${#domains[@]} successful)" >> "$results_file"
        else
            echo "  No successful queries"
            echo "$dns_server: No successful queries" >> "$results_file"
        fi
        
        echo ""
    done
    
    echo "Benchmark results saved to: $results_file"
}

# Function to configure DNS caching
configure_dns_cache() {
    local cache_type="$1"
    
    case "$cache_type" in
        "systemd-resolved")
            echo "Configuring DNS caching with systemd-resolved..."
            
            cat > /tmp/resolved.conf << 'EOF'
[Resolve]
DNS=8.8.8.8 8.8.4.4 1.1.1.1
Cache=yes
CacheFromLocalhost=yes
DNSStubListener=yes
ReadEtcHosts=yes
EOF
            
            sudo mv /tmp/resolved.conf /etc/systemd/resolved.conf
            sudo systemctl restart systemd-resolved
            
            echo "systemd-resolved DNS caching configured"
            ;;
            
        "dnsmasq")
            echo "Installing and configuring dnsmasq..."
            
            # Install dnsmasq
            if command -v apt &>/dev/null; then
                sudo apt update && sudo apt install -y dnsmasq
            elif command -v yum &>/dev/null; then
                sudo yum install -y dnsmasq
            else
                echo "Cannot install dnsmasq automatically"
                return 1
            fi
            
            # Configure dnsmasq
            cat > /tmp/dnsmasq.conf << 'EOF'
# Listen on localhost only
listen-address=127.0.0.1
bind-interfaces

# Cache size
cache-size=1000

# Upstream DNS servers
server=8.8.8.8
server=8.8.4.4
server=1.1.1.1

# Don't read /etc/hosts
no-hosts

# Log queries
log-queries
log-facility=/var/log/dnsmasq.log
EOF
            
            sudo mv /tmp/dnsmasq.conf /etc/dnsmasq.conf
            
            # Configure to use local dnsmasq
            echo "nameserver 127.0.0.1" | sudo tee /etc/resolv.conf
            
            # Start and enable dnsmasq
            sudo systemctl enable dnsmasq
            sudo systemctl start dnsmasq
            
            echo "dnsmasq DNS caching configured"
            ;;
            
        "unbound")
            echo "Installing and configuring unbound..."
            
            # Install unbound
            if command -v apt &>/dev/null; then
                sudo apt update && sudo apt install -y unbound
            elif command -v yum &>/dev/null; then
                sudo yum install -y unbound
            else
                echo "Cannot install unbound automatically"
                return 1
            fi
            
            # Configure unbound
            cat > /tmp/unbound.conf << 'EOF'
server:
    verbosity: 1
    interface: 127.0.0.1
    port: 53
    do-ip4: yes
    do-ip6: yes
    do-udp: yes
    do-tcp: yes
    
    # Cache settings
    cache-min-ttl: 300
    cache-max-ttl: 86400
    msg-cache-size: 50m
    rrset-cache-size: 100m
    
    # Security
    hide-identity: yes
    hide-version: yes
    harden-glue: yes
    harden-dnssec-stripped: yes
    use-caps-for-id: yes
    
    # Prefetch
    prefetch: yes
    prefetch-key: yes

forward-zone:
    name: "."
    forward-addr: 8.8.8.8
    forward-addr: 8.8.4.4
    forward-addr: 1.1.1.1
EOF
            
            sudo mv /tmp/unbound.conf /etc/unbound/unbound.conf
            
            # Configure to use local unbound
            echo "nameserver 127.0.0.1" | sudo tee /etc/resolv.conf
            
            # Start and enable unbound
            sudo systemctl enable unbound
            sudo systemctl start unbound
            
            echo "unbound DNS caching configured"
            ;;
            
        *)
            echo "Available cache types: systemd-resolved, dnsmasq, unbound"
            return 1
            ;;
    esac
    
    echo ""
    echo "Testing DNS cache..."
    test_dns google.com A
}

# Function to manage hosts file
manage_hosts() {
    local action="$1"
    local hostname="$2"
    local ip_address="$3"
    
    case "$action" in
        "add")
            if [[ -z "$hostname" || -z "$ip_address" ]]; then
                echo "Usage: manage_hosts add <hostname> <ip_address>"
                echo "Example: manage_hosts add myserver.local 192.168.1.100"
                return 1
            fi
            
            # Check if entry already exists
            if grep -q "^$ip_address[[:space:]]*$hostname" /etc/hosts; then
                echo "Entry already exists: $ip_address $hostname"
                return 0
            fi
            
            # Add entry
            echo "$ip_address $hostname" | sudo tee -a /etc/hosts
            echo "Added hosts entry: $ip_address $hostname"
            ;;
            
        "remove")
            if [[ -z "$hostname" ]]; then
                echo "Usage: manage_hosts remove <hostname>"
                return 1
            fi
            
            sudo sed -i "/[[:space:]]$hostname$/d" /etc/hosts
            echo "Removed hosts entry for: $hostname"
            ;;
            
        "list")
            echo "Current hosts file entries:"
            grep -v "^#" /etc/hosts | grep -v "^$"
            ;;
            
        "backup")
            local backup_file="/etc/hosts.backup.$(date +%Y%m%d_%H%M%S)"
            sudo cp /etc/hosts "$backup_file"
            echo "Hosts file backed up to: $backup_file"
            ;;
            
        *)
            echo "Available actions: add, remove, list, backup"
            return 1
            ;;
    esac
}

# Function to troubleshoot DNS issues
troubleshoot_dns() {
    local domain="${1:-google.com}"
    
    echo "=== DNS Troubleshooting for $domain ==="
    echo ""
    
    # Check current DNS configuration
    echo "1. Current DNS Configuration:"
    echo "   /etc/resolv.conf:"
    cat /etc/resolv.conf | grep -v "^#" | head -5
    echo ""
    
    # Check systemd-resolved status
    if command -v systemd-resolve &>/dev/null; then
        echo "2. systemd-resolved Status:"
        systemd-resolve --status | head -20
        echo ""
    fi
    
    # Test DNS resolution with different tools
    echo "3. DNS Resolution Tests:"
    
    # Test with ping
    echo "   Ping test:"
    if ping -c 1 -W 2 "$domain" &>/dev/null; then
        local ip=$(ping -c 1 "$domain" | head -1 | grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+')
        echo "   ✓ Ping successful: $domain -> $ip"
    else
        echo "   ✗ Ping failed"
    fi
    
    # Test with different DNS servers
    echo ""
    echo "   DNS Server Tests:"
    local test_servers=("8.8.8.8" "8.8.4.4" "1.1.1.1")
    
    for server in "${test_servers[@]}"; do
        if dig @"$server" "$domain" A +short +time=3 &>/dev/null; then
            local result=$(dig @"$server" "$domain" A +short | head -1)
            echo "   ✓ $server: $result"
        else
            echo "   ✗ $server: Failed"
        fi
    done
    
    # Check for DNS issues
    echo ""
    echo "4. Common Issues Check:"
    
    # Check if DNS port is open
    if ss -tuln | grep -q ":53 "; then
        echo "   ✓ DNS port 53 is listening"
    else
        echo "   ⚠ DNS port 53 not listening locally"
    fi
    
    # Check DNS response time
    echo ""
    echo "5. DNS Response Time:"
    local start_time=$(date +%s.%N)
    dig "$domain" A +short &>/dev/null
    local end_time=$(date +%s.%N)
    local response_time=$(echo "$end_time - $start_time" | bc -l)
    printf "   Response time: %.3fs\n" "$response_time"
    
    if (( $(echo "$response_time > 1.0" | bc -l) )); then
        echo "   ⚠ Slow DNS response (>1s)"
    else
        echo "   ✓ Good DNS response time"
    fi
}

# Usage function
usage() {
    echo "Usage: $0 {configure|test|benchmark|cache|hosts|troubleshoot} [arguments]"
    echo ""
    echo "Commands:"
    echo "  configure <method> <dns1> [dns2] [dns3] ...     - Configure DNS servers"
    echo "  test <domain> [record_type] [dns_server]        - Test DNS resolution"
    echo "  benchmark [domain1] [domain2] ...               - Benchmark DNS servers"
    echo "  cache <systemd-resolved|dnsmasq|unbound>        - Configure DNS caching"
    echo "  hosts <add|remove|list|backup> [hostname] [ip] - Manage hosts file"
    echo "  troubleshoot [domain]                           - Troubleshoot DNS issues"
    echo ""
    echo "Examples:"
    echo "  $0 configure systemd-resolved 8.8.8.8 8.8.4.4"
    echo "  $0 test google.com A 8.8.8.8"
    echo "  $0 benchmark google.com github.com"
    echo "  $0 cache systemd-resolved"
    echo "  $0 hosts add myserver.local 192.168.1.100"
    echo "  $0 troubleshoot google.com"
}

# Main script logic
case "${1:-help}" in
    "configure")
        shift
        configure_dns "$@"
        ;;
    "test")
        test_dns "$2" "$3" "$4"
        ;;
    "benchmark")
        shift
        benchmark_dns "$@"
        ;;
    "cache")
        configure_dns_cache "$2"
        ;;
    "hosts")
        manage_hosts "$2" "$3" "$4"
        ;;
    "troubleshoot")
        troubleshoot_dns "$2"
        ;;
    "help"|*)
        usage
        ;;
esac
``` ### Advanced IP Configuration

#### IP Address Management Script
```bash
#!/bin/bash
# ip-management.sh - Advanced IP address and routing management

# Function to configure static IP with NetworkManager
configure_static_ip() {
    local interface="$1"
    local ip_address="$2" 
    local gateway="$3"
    local dns1="${4:-8.8.8.8}"
    local dns2="${5:-8.8.4.4}"
    local connection_name="${6:-Static-$interface}"
    
    if [[ -z "$interface" || -z "$ip_address" || -z "$gateway" ]]; then
        echo "Usage: configure_static_ip <interface> <ip/prefix> <gateway> [dns1] [dns2] [connection_name]"
        echo "Example: configure_static_ip eth0 192.168.1.100/24 192.168.1.1 8.8.8.8 8.8.4.4"
        return 1
    fi
    
    echo "Configuring static IP for $interface..."
    
    # Create new connection
    nmcli connection add \
        type ethernet \
        con-name "$connection_name" \
        ifname "$interface" \
        ipv4.method manual \
        ipv4.addresses "$ip_address" \
        ipv4.gateway "$gateway" \
        ipv4.dns "$dns1,$dns2" \
        ipv4.dns-search "local" \
        connection.autoconnect yes
    
    # Activate the connection
    nmcli connection up "$connection_name"
    
    echo "Static IP configuration completed for $interface"
    echo "IP: $ip_address"
    echo "Gateway: $gateway" 
    echo "DNS: $dns1, $dns2"
}

# Function to configure DHCP with NetworkManager
configure_dhcp() {
    local interface="$1"
    local connection_name="${2:-DHCP-$interface}"
    
    if [[ -z "$interface" ]]; then
        echo "Usage: configure_dhcp <interface> [connection_name]"
        return 1
    fi
    
    echo "Configuring DHCP for $interface..."
    
    nmcli connection add \
        type ethernet \
        con-name "$connection_name" \
        ifname "$interface" \
        ipv4.method auto \
        connection.autoconnect yes
    
    nmcli connection up "$connection_name"
    
    echo "DHCP configuration completed for $interface"
}

# Function to manage routing table
manage_routes() {
    local action="$1"
    local destination="$2"
    local gateway="$3"
    local interface="$4"
    local metric="${5:-100}"
    
    case "$action" in
        "add")
            if [[ -z "$destination" || -z "$gateway" ]]; then
                echo "Usage: manage_routes add <destination> <gateway> [interface] [metric]"
                echo "Example: manage_routes add 10.0.0.0/8 192.168.1.1 eth0 100"
                return 1
            fi
            
            local route_cmd="sudo ip route add $destination via $gateway"
            if [[ -n "$interface" ]]; then
                route_cmd+=" dev $interface"
            fi
            if [[ -n "$metric" ]]; then
                route_cmd+=" metric $metric"
            fi
            
            echo "Adding route: $route_cmd"
            eval "$route_cmd"
            ;;
            
        "delete")
            if [[ -z "$destination" ]]; then
                echo "Usage: manage_routes delete <destination>"
                echo "Example: manage_routes delete 10.0.0.0/8"
                return 1
            fi
            
            echo "Deleting route: $destination"
            sudo ip route del "$destination"
            ;;
            
        "show")
            echo "Current routing table:"
            ip route show
            ;;
            
        "default")
            if [[ -z "$gateway" ]]; then
                echo "Usage: manage_routes default <gateway> [interface]"
                return 1
            fi
            
            echo "Setting default gateway: $gateway"
            sudo ip route del default 2>/dev/null || true
            
            local default_cmd="sudo ip route add default via $gateway"
            if [[ -n "$interface" ]]; then
                default_cmd+=" dev $interface"
            fi
            
            eval "$default_cmd"
            ;;
            
        *)
            echo "Available actions: add, delete, show, default"
            return 1
            ;;
    esac
}

# Function to configure multiple IP addresses on one interface
configure_multiple_ips() {
    local interface="$1"
    shift
    local ip_addresses=("$@")
    
    if [[ -z "$interface" || ${#ip_addresses[@]} -eq 0 ]]; then
        echo "Usage: configure_multiple_ips <interface> <ip1/prefix> [ip2/prefix] [ip3/prefix] ..."
        echo "Example: configure_multiple_ips eth0 192.168.1.100/24 192.168.1.101/24"
        return 1
    fi
    
    echo "Configuring multiple IP addresses on $interface..."
    
    # Remove existing IP addresses
    sudo ip addr flush dev "$interface"
    
    # Add each IP address
    for ip_addr in "${ip_addresses[@]}"; do
        echo "Adding IP: $ip_addr"
        sudo ip addr add "$ip_addr" dev "$interface"
    done
    
    # Ensure interface is up
    sudo ip link set "$interface" up
    
    echo "Multiple IP configuration completed for $interface"
    echo "Current addresses:"
    ip addr show "$interface" | grep -E "inet6?|link"
}

# Function to create network aliases (IP aliases)
create_ip_alias() {
    local base_interface="$1"
    local alias_number="$2"
    local ip_address="$3"
    
    if [[ -z "$base_interface" || -z "$alias_number" || -z "$ip_address" ]]; then
        echo "Usage: create_ip_alias <base_interface> <alias_number> <ip/prefix>"
        echo "Example: create_ip_alias eth0 1 192.168.1.101/24"
        return 1
    fi
    
    local alias_interface="${base_interface}:${alias_number}"
    
    echo "Creating IP alias $alias_interface with IP $ip_address..."
    
    # Create alias using ip command
    sudo ip addr add "$ip_address" dev "$base_interface" label "$alias_interface"
    
    echo "IP alias $alias_interface created successfully"
    echo "Interface information:"
    ip addr show "$base_interface" | grep -A1 "$alias_interface"
}

# Function to configure IPv6
configure_ipv6() {
    local interface="$1"
    local action="$2"
    local ipv6_address="$3"
    
    case "$action" in
        "enable")
            echo "Enabling IPv6 on $interface..."
            sudo sysctl -w net.ipv6.conf."$interface".disable_ipv6=0
            sudo ip link set "$interface" up
            ;;
            
        "disable")
            echo "Disabling IPv6 on $interface..."
            sudo sysctl -w net.ipv6.conf."$interface".disable_ipv6=1
            ;;
            
        "add")
            if [[ -z "$ipv6_address" ]]; then
                echo "Usage: configure_ipv6 <interface> add <ipv6_address/prefix>"
                echo "Example: configure_ipv6 eth0 add 2001:db8::1/64"
                return 1
            fi
            
            echo "Adding IPv6 address $ipv6_address to $interface..."
            sudo ip -6 addr add "$ipv6_address" dev "$interface"
            ;;
            
        "show")
            echo "IPv6 configuration for $interface:"
            ip -6 addr show "$interface"
            echo ""
            echo "IPv6 routing table:"
            ip -6 route show dev "$interface"
            ;;
            
        *)
            echo "Available actions: enable, disable, add, show"
            return 1
            ;;
    esac
}

# Function to configure network namespaces
manage_netns() {
    local action="$1"
    local namespace="$2"
    local interface="$3"
    
    case "$action" in
        "create")
            if [[ -z "$namespace" ]]; then
                echo "Usage: manage_netns create <namespace>"
                return 1
            fi
            
            echo "Creating network namespace: $namespace"
            sudo ip netns add "$namespace"
            
            # Enable loopback in namespace
            sudo ip netns exec "$namespace" ip link set lo up
            
            echo "Network namespace $namespace created"
            ;;
            
        "delete")
            if [[ -z "$namespace" ]]; then
                echo "Usage: manage_netns delete <namespace>"
                return 1
            fi
            
            echo "Deleting network namespace: $namespace"
            sudo ip netns del "$namespace"
            ;;
            
        "move")
            if [[ -z "$namespace" || -z "$interface" ]]; then
                echo "Usage: manage_netns move <namespace> <interface>"
                return 1
            fi
            
            echo "Moving interface $interface to namespace $namespace"
            sudo ip link set "$interface" netns "$namespace"
            ;;
            
        "exec")
            if [[ -z "$namespace" ]]; then
                echo "Usage: manage_netns exec <namespace> <command>"
                return 1
            fi
            
            shift 2
            echo "Executing in namespace $namespace: $*"
            sudo ip netns exec "$namespace" "$@"
            ;;
            
        "list")
            echo "Available network namespaces:"
            ip netns list
            ;;
            
        *)
            echo "Available actions: create, delete, move, exec, list"
            return 1
            ;;
    esac
}

# Function to test network connectivity
test_connectivity() {
    local target="$1"
    local test_type="${2:-ping}"
    local interface="$3"
    
    if [[ -z "$target" ]]; then
        echo "Usage: test_connectivity <target> [ping|trace|port] [interface]"
        return 1
    fi
    
    case "$test_type" in
        "ping")
            echo "Testing ping connectivity to $target..."
            local ping_cmd="ping -c 4 -W 3"
            if [[ -n "$interface" ]]; then
                ping_cmd+=" -I $interface"
            fi
            ping_cmd+=" $target"
            
            eval "$ping_cmd"
            ;;
            
        "trace")
            echo "Tracing route to $target..."
            local trace_cmd="traceroute"
            if [[ -n "$interface" ]]; then
                trace_cmd+=" -i $interface"
            fi
            trace_cmd+=" $target"
            
            eval "$trace_cmd"
            ;;
            
        "port")
            local port="${4:-80}"
            echo "Testing port connectivity to $target:$port..."
            if command -v nc &>/dev/null; then
                timeout 5 nc -zv "$target" "$port"
            elif command -v telnet &>/dev/null; then
                timeout 5 telnet "$target" "$port"
            else
                echo "Neither nc nor telnet available for port testing"
                return 1
            fi
            ;;
            
        *)
            echo "Available test types: ping, trace, port"
            return 1
            ;;
    esac
}

# Usage function
usage() {
    echo "Usage: $0 {static|dhcp|routes|multi-ip|alias|ipv6|netns|test} [arguments]"
    echo ""
    echo "Commands:"
    echo "  static <interface> <ip/prefix> <gateway> [dns1] [dns2]  - Configure static IP"
    echo "  dhcp <interface>                                        - Configure DHCP"
    echo "  routes <add|delete|show|default> [args]                - Manage routing table"
    echo "  multi-ip <interface> <ip1/prefix> [ip2/prefix] ...     - Configure multiple IPs"
    echo "  alias <interface> <alias_num> <ip/prefix>              - Create IP alias"
    echo "  ipv6 <interface> <enable|disable|add|show> [ipv6]     - Configure IPv6"
    echo "  netns <create|delete|move|exec|list> [args]            - Manage network namespaces"
    echo "  test <target> [ping|trace|port] [interface]           - Test connectivity"
    echo ""
    echo "Examples:"
    echo "  $0 static eth0 192.168.1.100/24 192.168.1.1"
    echo "  $0 routes add 10.0.0.0/8 192.168.1.1 eth0"
    echo "  $0 multi-ip eth0 192.168.1.100/24 192.168.1.101/24"
    echo "  $0 alias eth0 1 192.168.2.100/24"
    echo "  $0 ipv6 eth0 add 2001:db8::1/64"
    echo "  $0 netns create test-ns"
    echo "  $0 test google.com ping"
}

# Main script logic
case "${1:-help}" in
    "static")
        configure_static_ip "$2" "$3" "$4" "$5" "$6" "$7"
        ;;
    "dhcp")
        configure_dhcp "$2" "$3"
        ;;
    "routes")
        manage_routes "$2" "$3" "$4" "$5" "$6"
        ;;
    "multi-ip")
        shift
        configure_multiple_ips "$@"
        ;;
    "alias")
        create_ip_alias "$2" "$3" "$4"
        ;;
    "ipv6")
        configure_ipv6 "$2" "$3" "$4"
        ;;
    "netns")
        shift
        manage_netns "$@"
        ;;
    "test")
        test_connectivity "$2" "$3" "$4" "$5"
        ;;
    "help"|*)
        usage
        ;;
esac
```
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

## Lab Exercises

### Lab 1: Network Configuration and Management
**Objective**: Master comprehensive network interface configuration and management across different systems.

**Tasks**:
1. Interface configuration automation:
   - Create scripts for static and dynamic IP configuration
   - Implement VLAN and bridge setup automation
   - Configure network bonding for redundancy
   - Test IPv6 dual-stack configurations

2. Network service management:
   - Configure DHCP server with reservations
   - Set up local DNS caching and forwarding
   - Implement network monitoring and alerting
   - Create network documentation and diagrams

**Deliverables**:
- Network configuration automation scripts
- DHCP and DNS server configurations
- Network monitoring dashboard
- Comprehensive network documentation

**Success Criteria**:
- All network configurations work reliably
- Automation scripts handle error conditions
- Monitoring detects and alerts on issues
- Documentation is complete and accurate

### Lab 2: Firewall Security Implementation
**Objective**: Implement comprehensive firewall security across multiple systems and use cases.

**Tasks**:
1. Multi-platform firewall deployment:
   - Configure iptables rules for complex scenarios
   - Implement firewalld zones for enterprise environments
   - Set up UFW for simplified Ubuntu management
   - Create firewall rule management automation

2. Advanced security features:
   - Implement connection tracking and stateful rules
   - Configure DDoS protection and rate limiting
   - Set up network segmentation and DMZ zones
   - Deploy intrusion detection integration

**Deliverables**:
- Firewall rule sets for different environments
- Automated firewall management system
- Security testing and validation reports
- Incident response procedures

**Success Criteria**:
- Firewall rules block unauthorized access
- Legitimate traffic flows without issues
- Automation maintains security posture
- Security tests validate protection effectiveness

### Lab 3: SSH Infrastructure Hardening
**Objective**: Deploy enterprise-grade SSH security infrastructure with comprehensive hardening measures.

**Tasks**:
1. SSH security implementation:
   - Configure SSH servers with security hardening
   - Implement certificate-based authentication
   - Set up SSH jump hosts and bastion architecture
   - Deploy SSH session monitoring and logging

2. Key management and automation:
   - Create automated SSH key rotation system
   - Implement centralized key management
   - Configure SSH agent forwarding controls
   - Set up emergency access procedures

**Deliverables**:
- Hardened SSH configurations for all systems
- Automated key management system
- SSH monitoring and alerting solution
- Security compliance documentation

**Success Criteria**:
- SSH passes security compliance scans
- Key rotation works without service disruption
- Monitoring detects unauthorized access attempts
- Emergency procedures are tested and documented

### Lab 4: Network Monitoring and Troubleshooting
**Objective**: Implement comprehensive network monitoring and develop advanced troubleshooting capabilities.

**Tasks**:
1. Monitoring infrastructure:
   - Deploy network traffic analysis tools
   - Implement bandwidth monitoring and alerting
   - Set up performance metrics collection
   - Create network health dashboards

2. Troubleshooting capabilities:
   - Develop network diagnostic automation
   - Create packet capture and analysis procedures
   - Implement automated connectivity testing
   - Design escalation and response workflows

**Deliverables**:
- Complete network monitoring solution
- Automated diagnostic and testing tools
- Network performance analysis reports
- Troubleshooting runbooks and procedures

**Success Criteria**:
- Monitoring provides real-time network visibility
- Automated tools accurately diagnose issues
- Performance baselines are established
- Response times for issues are minimized

### Lab 5: VPN and Secure Remote Access
**Objective**: Design and implement secure remote access solutions using multiple VPN technologies.

**Tasks**:
1. VPN infrastructure deployment:
   - Configure OpenVPN for site-to-site connectivity
   - Implement WireGuard for modern client access
   - Set up IPSec tunnels for enterprise connections
   - Deploy SSL/TLS VPN for web-based access

2. Security and management:
   - Implement certificate management for VPN
   - Configure multi-factor authentication
   - Set up VPN monitoring and logging
   - Create user access management procedures

**Deliverables**:
- Multi-protocol VPN infrastructure
- Certificate management system
- VPN monitoring and reporting tools
- User access management procedures

**Success Criteria**:
- VPN connections are stable and secure
- Certificate management is automated
- User access is properly controlled
- Performance meets business requirements

## Best Practices

### Network Configuration Best Practices

#### Interface Management
- **Consistent Naming**: Use predictable interface naming conventions
- **Documentation**: Maintain accurate network configuration documentation
- **Version Control**: Track network configuration changes in version control
- **Testing**: Test network changes in non-production environments first
- **Rollback Plans**: Always have rollback procedures for network changes

#### IP Address Management
- **IPAM Strategy**: Implement proper IP address management and documentation
- **Subnet Planning**: Plan IP addressing schemes for future growth
- **DHCP Reservations**: Use DHCP reservations for servers and infrastructure
- **IPv6 Preparation**: Plan for IPv6 implementation in network designs
- **Network Segmentation**: Segment networks based on security and functional requirements

#### DNS Configuration
- **Redundancy**: Configure multiple DNS servers for reliability
- **Caching**: Implement local DNS caching for performance
- **Security**: Use DNS over HTTPS/TLS where appropriate
- **Monitoring**: Monitor DNS resolution performance and availability
- **Split-Horizon**: Implement split-horizon DNS for internal/external resolution

### Security Best Practices

#### Firewall Management
- **Default Deny**: Implement default deny policies with explicit allow rules
- **Principle of Least Privilege**: Grant minimum necessary network access
- **Regular Reviews**: Conduct periodic firewall rule reviews and cleanup
- **Logging**: Enable comprehensive firewall logging for security monitoring
- **Testing**: Regularly test firewall rules and security effectiveness

#### SSH Security
- **Key-Based Authentication**: Disable password authentication in favor of keys
- **Regular Key Rotation**: Implement automated SSH key rotation procedures
- **Session Monitoring**: Monitor and log SSH sessions for security analysis
- **Jump Hosts**: Use jump hosts/bastions for secure administrative access
- **Rate Limiting**: Implement connection rate limiting to prevent brute force attacks

#### Network Monitoring
- **Comprehensive Coverage**: Monitor all critical network components and services
- **Baseline Establishment**: Establish performance baselines for anomaly detection
- **Automated Alerting**: Configure intelligent alerting to minimize false positives
- **Capacity Planning**: Use monitoring data for network capacity planning
- **Incident Response**: Integrate monitoring with incident response procedures

### Operational Best Practices

#### Change Management
- **Documentation**: Document all network changes with justification and procedures
- **Testing**: Test changes in lab environments before production deployment
- **Approval Process**: Implement change approval processes for critical systems
- **Rollback Planning**: Always have tested rollback procedures available
- **Communication**: Communicate changes to affected stakeholders

#### Automation
- **Infrastructure as Code**: Manage network configurations as code
- **Automated Testing**: Implement automated testing for network configurations
- **Deployment Automation**: Automate network deployment and configuration management
- **Monitoring Integration**: Integrate automation with monitoring and alerting systems
- **Error Handling**: Implement robust error handling in automation scripts

#### Disaster Recovery
- **Network Redundancy**: Design networks with appropriate redundancy levels
- **Backup Configurations**: Regularly backup network device configurations
- **Recovery Procedures**: Document and test network recovery procedures
- **Geographic Distribution**: Consider geographic distribution for critical services
- **Regular Testing**: Conduct regular disaster recovery testing exercises

## Troubleshooting

### Network Connectivity Issues

#### No Network Connectivity
**Symptoms**: Complete loss of network access, cannot reach any destinations

**Diagnostic Steps**:
1. Check physical connectivity:
   ```bash
   # Check link status
   ip link show
   ethtool eth0
   
   # Check for cable issues
   dmesg | grep -i "link\|carrier"
   ```

2. Verify interface configuration:
   ```bash
   # Check IP configuration
   ip addr show
   ip route show
   
   # Test local connectivity
   ping -c 4 $(ip route | grep default | awk '{print $3}')
   ```

3. Check DNS resolution:
   ```bash
   # Test DNS
   nslookup google.com
   dig google.com
   
   # Check DNS configuration
   cat /etc/resolv.conf
   systemd-resolve --status
   ```

**Solutions**:
- Verify cable connections and switch ports
- Check interface configuration and bring up if needed
- Verify IP addressing and routing configuration
- Fix DNS configuration if resolution fails
- Restart network services if configuration is correct

#### Intermittent Connectivity
**Symptoms**: Network works sometimes but fails intermittently

**Diagnostic Steps**:
1. Monitor interface statistics:
   ```bash
   # Watch for errors
   watch -n 1 'ip -s link show eth0'
   
   # Check system logs
   journalctl -f -u NetworkManager
   dmesg -w
   ```

2. Test connectivity patterns:
   ```bash
   # Continuous ping test
   ping -i 0.2 8.8.8.8
   
   # MTR for path analysis
   mtr --report --cycles 100 8.8.8.8
   ```

3. Analyze network performance:
   ```bash
   # Check for packet loss
   ss -i
   netstat -i
   
   # Monitor bandwidth usage
   iftop -i eth0
   nethogs
   ```

**Solutions**:
- Replace faulty cables or network hardware
- Adjust network interface settings (duplex, speed)
- Update network drivers
- Configure Quality of Service (QoS) if needed
- Investigate and resolve bandwidth saturation

### DNS Resolution Problems

#### Slow DNS Resolution
**Symptoms**: Web browsing and network services are slow due to DNS delays

**Diagnostic Steps**:
1. Measure DNS response times:
   ```bash
   # Test multiple DNS servers
   for server in 8.8.8.8 8.8.4.4 1.1.1.1; do
       echo "Testing $server:"
       time dig @$server google.com A +short
   done
   ```

2. Check local DNS configuration:
   ```bash
   # Check systemd-resolved
   systemd-resolve --status
   systemd-resolve --statistics
   
   # Check for local DNS cache
   ss -tuln | grep :53
   ```

**Solutions**:
- Switch to faster DNS servers (1.1.1.1, 8.8.8.8)
- Configure local DNS caching (systemd-resolved, dnsmasq)
- Fix network connectivity to DNS servers
- Implement DNS over HTTPS/TLS for better performance

#### DNS Resolution Failures
**Symptoms**: Cannot resolve domain names, but IP addresses work

**Diagnostic Steps**:
1. Test DNS servers directly:
   ```bash
   # Test current DNS servers
   dig google.com
   nslookup google.com
   
   # Test with different DNS servers
   dig @8.8.8.8 google.com
   dig @1.1.1.1 google.com
   ```

2. Check DNS configuration:
   ```bash
   # Check resolv.conf
   cat /etc/resolv.conf
   
   # Check systemd-resolved configuration
   cat /etc/systemd/resolved.conf
   systemctl status systemd-resolved
   ```

**Solutions**:
- Fix /etc/resolv.conf configuration
- Restart systemd-resolved service
- Configure working DNS servers
- Check firewall rules for DNS traffic (port 53)

### Firewall Configuration Issues

#### Services Inaccessible After Firewall Changes
**Symptoms**: Network services become inaccessible after firewall rule changes

**Diagnostic Steps**:
1. Check current firewall rules:
   ```bash
   # Check active rules
   iptables -L -n -v
   firewall-cmd --list-all
   ufw status verbose
   ```

2. Test specific connections:
   ```bash
   # Test from client
   telnet server_ip port
   nc -zv server_ip port
   
   # Check if service is listening
   ss -tuln | grep :port
   ```

3. Analyze blocked connections:
   ```bash
   # Check firewall logs
   journalctl -f -g "REJECT\|DROP"
   tail -f /var/log/ufw.log
   dmesg | grep -i firewall
   ```

**Solutions**:
- Add explicit allow rules for required services
- Check rule order and precedence
- Verify source and destination addresses in rules
- Temporarily disable firewall to confirm it's the issue

#### Firewall Rules Not Working
**Symptoms**: Firewall rules are configured but not blocking unwanted traffic

**Diagnostic Steps**:
1. Verify rule syntax and order:
   ```bash
   # Check rule order
   iptables -L -n --line-numbers
   
   # Test rule matching
   iptables -L -n -v
   ```

2. Test rule effectiveness:
   ```bash
   # Monitor rule hits
   watch -n 1 'iptables -L -n -v'
   
   # Check for conflicting rules
   iptables-save | grep -E "ACCEPT|REJECT|DROP"
   ```

**Solutions**:
- Fix rule syntax and ordering
- Remove conflicting rules
- Ensure rules are persistent across reboots
- Test rules thoroughly after implementation

### SSH Connection Problems

#### SSH Connection Refused
**Symptoms**: Cannot connect to SSH server, connection refused error

**Diagnostic Steps**:
1. Check SSH service status:
   ```bash
   # Check if SSH is running
   systemctl status ssh
   systemctl status sshd
   
   # Check if SSH is listening
   ss -tuln | grep :22
   netstat -tuln | grep :22
   ```

2. Check SSH configuration:
   ```bash
   # Test SSH configuration
   sshd -T
   
   # Check SSH logs
   journalctl -u ssh -f
   tail -f /var/log/auth.log
   ```

3. Test network connectivity:
   ```bash
   # Test port connectivity
   telnet ssh_server 22
   nc -zv ssh_server 22
   ```

**Solutions**:
- Start SSH service if not running
- Fix SSH configuration errors
- Open SSH port in firewall
- Check if SSH is bound to correct interfaces

#### SSH Authentication Failures
**Symptoms**: SSH connection established but authentication fails

**Diagnostic Steps**:
1. Check SSH authentication methods:
   ```bash
   # Test with verbose output
   ssh -v user@hostname
   
   # Check authorized keys
   ls -la ~/.ssh/authorized_keys
   cat ~/.ssh/authorized_keys
   ```

2. Verify key permissions:
   ```bash
   # Check SSH directory permissions
   ls -la ~/.ssh/
   
   # Fix permissions if needed
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

3. Check SSH server configuration:
   ```bash
   # Check authentication settings
   grep -E "PubkeyAuthentication|PasswordAuthentication|PermitRootLogin" /etc/ssh/sshd_config
   ```

**Solutions**:
- Fix SSH key permissions
- Verify public key is correctly installed
- Check SSH server authentication settings
- Regenerate SSH keys if corrupted

## Assessment Criteria

### Knowledge Assessment

#### Theoretical Understanding (25 points)
- **Network Fundamentals** (5 points): OSI model, TCP/IP stack, addressing schemes
- **Interface Management** (5 points): Modern tools (NetworkManager, systemd-networkd) and legacy methods
- **DNS and Name Resolution** (5 points): DNS hierarchy, caching, security considerations
- **Firewall Technologies** (5 points): iptables, firewalld, UFW, and rule management concepts
- **Security Principles** (5 points): Network security best practices and threat mitigation

#### Practical Implementation (50 points)
- **Network Configuration** (15 points):
  - Configure static and dynamic IP addressing
  - Implement VLANs and network bridging
  - Set up IPv6 dual-stack networking
  - Configure routing and network namespaces

- **DNS Infrastructure** (10 points):
  - Configure DNS servers and caching
  - Implement secure DNS (DoH/DoT)
  - Manage hosts files and local resolution
  - Troubleshoot DNS resolution issues

- **Firewall Implementation** (15 points):
  - Configure iptables rules for complex scenarios
  - Implement firewalld zones and policies
  - Set up UFW for simplified management
  - Deploy DDoS protection and rate limiting

- **SSH Security** (10 points):
  - Harden SSH server configuration
  - Implement key-based authentication
  - Configure SSH tunneling and forwarding
  - Set up monitoring and audit logging

#### Problem-Solving and Troubleshooting (15 points)
- **Diagnostic Skills** (5 points): Systematic approach to network problem diagnosis
- **Tool Proficiency** (5 points): Effective use of network diagnostic and monitoring tools
- **Resolution Techniques** (5 points): Ability to implement lasting solutions to network issues

#### Documentation and Automation (10 points)
- **Technical Documentation** (5 points): Clear network diagrams, configuration documentation
- **Automation Scripts** (5 points): Functional scripts for network management and monitoring

### Practical Evaluation Rubric

#### Excellent (90-100%)
- Demonstrates mastery of all networking concepts and technologies
- Implements comprehensive security measures with enterprise-grade hardening
- Creates robust, scalable automation solutions with proper error handling
- Provides detailed documentation and follows all security best practices
- Troubleshoots complex network issues efficiently and systematically

#### Proficient (80-89%)
- Shows solid understanding of networking fundamentals and management
- Implements most security measures correctly with minor gaps
- Creates functional automation with basic error handling
- Provides adequate documentation covering essential elements
- Handles most networking scenarios with minimal guidance

#### Developing (70-79%)
- Understands basic networking concepts with some limitations
- Implements fundamental security measures inconsistently
- Creates basic functional solutions with limited automation
- Documentation covers core requirements but lacks detail
- Requires guidance for complex networking scenarios

#### Needs Improvement (Below 70%)
- Limited understanding of networking fundamentals
- Inconsistent or ineffective security implementations
- Solutions lack robustness and have significant functional issues
- Minimal or incomplete documentation
- Cannot troubleshoot effectively without significant assistance

### Certification Requirements

To receive certification for Module 7, candidates must:

1. **Score 80% or higher** on the practical assessment
2. **Complete all lab exercises** with satisfactory results
3. **Demonstrate proficiency** in network troubleshooting scenarios
4. **Submit comprehensive documentation** of network implementations
5. **Pass a practical evaluation** demonstrating real-world networking skills

### Continuing Education

#### Advanced Topics for Further Study
- Software-Defined Networking (SDN)
- Network automation with Ansible/Terraform
- Container networking (Docker, Kubernetes)
- Advanced VPN technologies (DMVPN, SD-WAN)
- Network security monitoring and threat hunting

#### Recommended Certifications
- CompTIA Network+
- Cisco CCNA (Routing and Switching)
- Linux Professional Institute Certification (LPIC-2)
- Red Hat Certified Engineer (RHCE)
- Certified Ethical Hacker (CEH)

#### Industry Resources
- RFC documents for networking standards
- NIST Cybersecurity Framework
- CIS Critical Security Controls
- Linux networking documentation
- Vendor-specific networking guides

## Next Steps

With comprehensive networking fundamentals mastered, you're ready to advance to **Module 8: Logging and Monitoring**. This next module will build upon your network troubleshooting skills by covering:

- System log management and analysis
- Performance monitoring and alerting
- Log aggregation and centralization
- Monitoring infrastructure and automation
- Incident response and escalation procedures

The networking skills learned in this module are essential for understanding how distributed systems communicate and for implementing effective monitoring and logging strategies across network infrastructure.
