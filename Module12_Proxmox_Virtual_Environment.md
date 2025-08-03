# Module 12: Proxmox Virtual Environment

## Overview
This module covers Proxmox VE (Virtual Environment), a complete open-source platform for enterprise virtualization. You'll learn to deploy, configure, and manage virtual machines and containers using Proxmox's web-based interface and command-line tools.

## Learning Objectives
By the end of this module, you will be able to:
- Install and configure Proxmox VE
- Create and manage virtual machines and containers
- Configure networking and storage in Proxmox
- Implement backup and disaster recovery strategies
- Set up Proxmox clustering for high availability
- Monitor and optimize virtualized infrastructure

## Topics

### 12.1 Proxmox VE Fundamentals
- Proxmox architecture and components
- KVM and LXC virtualization technologies
- Web interface vs command-line management
- Storage backends and integration
- Network configuration concepts

### 12.2 Proxmox Installation and Initial Setup
- Hardware requirements and planning
- Installation methods and options
- Initial network configuration
- Web interface setup and access
- Security hardening and best practices

### 12.3 Storage Configuration
- Storage types and backends
- ZFS integration and configuration
- Shared storage setup (NFS, iSCSI, Ceph)
- Storage performance optimization
- Backup storage configuration

### 12.4 Virtual Machine Management
- Creating and configuring VMs
- VM templates and cloning
- Resource allocation and limits
- VM migration and snapshots
- Performance monitoring and tuning

### 12.5 Container Management (LXC)
- Understanding LXC containers
- Container templates and creation
- Resource management for containers
- Container networking and storage
- Security considerations

### 12.6 Advanced Features
- High Availability (HA) clustering
- Live migration and fault tolerance
- Backup and restore strategies
- API integration and automation
- Monitoring and alerting

## Practical Examples

### Proxmox Installation and Setup

#### Pre-installation Planning
```bash
# Check hardware compatibility
lscpu | grep -E "(vmx|svm)"  # Verify virtualization support
cat /proc/meminfo | grep MemTotal  # Check available RAM
lsblk  # Review storage devices

# Network planning
ip addr show  # Current network configuration
ip route show  # Current routing table
```

#### Installation Process
```bash
# Download Proxmox VE ISO
wget https://www.proxmox.com/en/downloads/proxmox-virtual-environment/iso

# Create bootable USB (Linux)
sudo dd if=proxmox-ve_*.iso of=/dev/sdX bs=1M status=progress

# Post-installation updates
apt update && apt full-upgrade

# Configure enterprise repository (if licensed)
# Or disable enterprise repo and enable no-subscription repo
echo "deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription" > \
    /etc/apt/sources.list.d/pve-no-subscription.list

# Update package lists
apt update
```

#### Initial Configuration
```bash
# Configure network interfaces
# /etc/network/interfaces example
auto lo
iface lo inet loopback

iface eno1 inet manual

auto vmbr0
iface vmbr0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    bridge-ports eno1
    bridge-stp off
    bridge-fd 0

# Restart networking
systemctl restart networking

# Configure firewall
pve-firewall status
```

### Storage Configuration

#### ZFS Storage Setup
```bash
# Create ZFS pool for VM storage
zpool create -o ashift=12 vmdata mirror /dev/sdb /dev/sdc

# Create ZFS datasets
zfs create vmdata/vm-disks
zfs create vmdata/backups
zfs create vmdata/templates

# Add ZFS storage to Proxmox
pvesm add zfspool vmdata --pool vmdata

# Configure ZFS properties for VMs
zfs set compression=lz4 vmdata/vm-disks
zfs set sync=disabled vmdata/vm-disks  # Only if UPS protected
zfs set primarycache=metadata vmdata/vm-disks
```

#### Shared Storage Configuration
```bash
# Add NFS storage
pvesm add nfs shared-nfs --server 192.168.1.200 --export /srv/nfs/proxmox

# Add iSCSI storage
pvesm add iscsi iscsi-storage --portal 192.168.1.201 --target iqn.2021-01.com.example:storage

# Add CIFS/SMB storage
pvesm add cifs cifs-storage --server 192.168.1.202 --share proxmox-storage \
    --username proxmox --password

# List configured storages
pvesm status
```

### Virtual Machine Management

#### Creating VMs via Command Line
```bash
# Create VM
qm create 100 --name ubuntu-server --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0

# Add disk to VM
qm set 100 --scsi0 vmdata:32

# Set boot device
qm set 100 --boot c --bootdisk scsi0

# Add CD-ROM with ISO
qm set 100 --ide2 local:iso/ubuntu-20.04.iso,media=cdrom

# Start VM
qm start 100

# Connect to VM console
qm monitor 100

# VM status and information
qm status 100
qm config 100
```

#### VM Template Creation
```bash
# Convert VM to template
qm template 100

# Clone template to new VM
qm clone 100 101 --name web-server-01

# Full clone with different storage
qm clone 100 102 --name web-server-02 --full --target local-zfs

# Start cloned VM
qm start 101
```

#### VM Migration
```bash
# Migrate VM to another node
qm migrate 100 pve-node2

# Live migration with storage
qm migrate 100 pve-node2 --targetstorage shared-nfs

# Offline migration
qm migrate 100 pve-node2 --online 0
```

### Container Management (LXC)

#### Creating and Managing Containers
```bash
# Download container template
pveam update
pveam available | grep ubuntu
pveam download local ubuntu-20.04-standard_20.04-1_amd64.tar.gz

# Create container
pct create 200 local:vztmpl/ubuntu-20.04-standard_20.04-1_amd64.tar.gz \
    --hostname web-container --memory 1024 --cores 1 \
    --net0 name=eth0,bridge=vmbr0,ip=192.168.1.150/24,gw=192.168.1.1 \
    --storage vmdata

# Start container
pct start 200

# Enter container
pct enter 200

# Container status
pct status 200
pct config 200

# Stop container
pct stop 200

# Container snapshots
pct snapshot 200 before-update
pct rollback 200 before-update
pct delsnapshot 200 before-update
```

#### Container Configuration
```bash
# Mount host directory in container
pct set 200 --mp0 /srv/web,mp=/var/www/html

# Set container resources
pct set 200 --memory 2048 --cores 2
pct set 200 --swap 512

# Configure container networking
pct set 200 --net0 name=eth0,bridge=vmbr0,ip=dhcp

# Container startup options
pct set 200 --onboot 1
pct set 200 --startup order=1,up=30
```

### Backup and Restore

#### Backup Configuration
```bash
# Create backup job via CLI
vzdump 100 --storage backups --mode snapshot --compress gzip

# Restore from backup
qmrestore /var/lib/vz/dump/vzdump-qemu-100-2024_01_15-21_30_00.vma.gz 101

# Container backup
vzdump 200 --storage backups --mode snapshot

# Container restore
pct restore 201 /var/lib/vz/dump/vzdump-lxc-200-2024_01_15-21_30_00.tar.gz \
    --storage vmdata
```

#### Automated Backup Script
```bash
#!/bin/bash
# proxmox-backup.sh - Automated backup script

BACKUP_STORAGE="backups"
RETENTION_DAYS=30
LOG_FILE="/var/log/proxmox-backup.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

# Backup all VMs and containers
backup_all() {
    log "Starting backup of all VMs and containers"
    
    # Get list of VMs
    for vmid in $(qm list | awk 'NR>1 {print $1}'); do
        log "Backing up VM $vmid"
        if vzdump "$vmid" --storage "$BACKUP_STORAGE" --mode snapshot \
           --compress gzip --quiet 1; then
            log "VM $vmid backup completed successfully"
        else
            log "VM $vmid backup failed"
        fi
    done
    
    # Get list of containers
    for ctid in $(pct list | awk 'NR>1 {print $1}'); do
        log "Backing up container $ctid"
        if vzdump "$ctid" --storage "$BACKUP_STORAGE" --mode snapshot \
           --compress gzip --quiet 1; then
            log "Container $ctid backup completed successfully"
        else
            log "Container $ctid backup failed"
        fi
    done
}

# Cleanup old backups
cleanup_backups() {
    log "Cleaning up backups older than $RETENTION_DAYS days"
    
    find /var/lib/vz/dump/ -name "vzdump-*" -mtime +$RETENTION_DAYS -delete
    
    log "Backup cleanup completed"
}

# Main execution
main() {
    backup_all
    cleanup_backups
    log "Backup process completed"
}

main "$@"
```

### High Availability Clustering

#### Cluster Setup
```bash
# Initialize cluster on first node
pvecm create my-cluster

# Add nodes to cluster (run on additional nodes)
pvecm add 192.168.1.100

# Check cluster status
pvecm status
pvecm nodes

# Configure corosync
# /etc/pve/corosync.conf example
totem {
    version: 2
    cluster_name: my-cluster
    config_version: 1
    ip_version: ipv4
    secauth: on
    transport: udpu
}

nodelist {
    node {
        name: pve-node1
        nodeid: 1
        quorum_votes: 1
        ring0_addr: 192.168.1.100
    }
    node {
        name: pve-node2
        nodeid: 2
        quorum_votes: 1
        ring0_addr: 192.168.1.101
    }
    node {
        name: pve-node3
        nodeid: 3
        quorum_votes: 1
        ring0_addr: 192.168.1.102
    }
}

quorum {
    provider: corosync_votequorum
}
```

#### HA Resource Management
```bash
# Enable HA for VM
ha-manager add vm:100 --state started --group group1

# Set HA groups
pvesh create /cluster/ha/groups/group1 --nodes pve-node1:2,pve-node2:1

# Check HA status
ha-manager status

# Disable HA for resource
ha-manager remove vm:100
```

### Monitoring and Performance

#### System Monitoring
```bash
# Check node resources
pvesh get /nodes/pve-node1/status

# VM resource usage
qm monitor 100 info cpus
qm monitor 100 info memory

# Storage usage
pvesm status

# Network statistics
cat /proc/net/dev
```

#### Performance Optimization
```bash
# CPU governor for performance
echo performance | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Kernel parameters for virtualization
# /etc/sysctl.d/99-proxmox.conf
vm.swappiness=10
vm.dirty_ratio=5
vm.dirty_background_ratio=2
net.core.somaxconn=65536

# Apply changes
sysctl -p /etc/sysctl.d/99-proxmox.conf

# Optimize ZFS ARC
echo 8589934592 > /sys/module/zfs/parameters/zfs_arc_max  # 8GB
```

### API Integration and Automation

#### Using Proxmox API
```bash
# Get API ticket
curl -k -d "username=root@pam&password=yourpassword" \
    https://192.168.1.100:8006/api2/json/access/ticket

# API call with ticket
curl -k -H "CSRFPreventionToken: $CSRF" \
    -H "Cookie: PVEAuthCookie=$TICKET" \
    https://192.168.1.100:8006/api2/json/nodes

# Python API example
#!/usr/bin/env python3
import requests
import json

# API connection
api_url = "https://192.168.1.100:8006/api2/json"
auth_data = {"username": "root@pam", "password": "yourpassword"}

# Get ticket
response = requests.post(f"{api_url}/access/ticket", 
                        data=auth_data, verify=False)
ticket_data = response.json()["data"]

# Set headers
headers = {
    "CSRFPreventionToken": ticket_data["CSRFPreventionToken"],
    "Cookie": f"PVEAuthCookie={ticket_data['ticket']}"
}

# List VMs
response = requests.get(f"{api_url}/nodes/pve-node1/qemu", 
                       headers=headers, verify=False)
vms = response.json()["data"]

for vm in vms:
    print(f"VM {vm['vmid']}: {vm['name']} - {vm['status']}")
```

## Proxmox Best Practices

| Category | Best Practice |
|----------|---------------|
| Hardware | Use ECC RAM, enterprise SSDs, redundant PSUs |
| Storage | Implement ZFS with redundancy, separate boot/VM storage |
| Networking | Use bonded interfaces, separate management network |
| Backup | Schedule regular backups, test restore procedures |
| Security | Enable firewall, use strong passwords, limit access |
| Monitoring | Monitor resources, set up alerting |
| Updates | Plan maintenance windows, test updates |

## Security Considerations

### Firewall Configuration
```bash
# Enable Proxmox firewall
pve-firewall enable

# Configure datacenter firewall
# /etc/pve/firewall/cluster.fw
[OPTIONS]
enable: 1
policy_in: DROP
policy_out: ACCEPT

[RULES]
IN SSH(ACCEPT) -source 192.168.1.0/24
IN 8006(ACCEPT) -source 192.168.1.0/24  # Proxmox web interface
```

### SSL Certificate Setup
```bash
# Generate self-signed certificate
openssl req -x509 -newkey rsa:4096 -keyout /etc/pve/local/pve-ssl.key \
    -out /etc/pve/local/pve-ssl.pem -days 365 -nodes

# Restart proxy service
systemctl restart pveproxy
```

## Troubleshooting Common Issues

### Storage Issues
```bash
# Check storage status
pvesm status

# Verify ZFS pool health
zpool status

# Check disk space
df -h
zfs list
```

### Network Issues
```bash
# Check bridge configuration
brctl show

# Verify VLAN configuration
cat /proc/net/vlan/config

# Test connectivity
ping -c 4 192.168.1.1
```

### VM/Container Issues
```bash
# Check VM logs
journalctl -u qemu-server@100

# Container logs
journalctl -u lxc@200

# Check resource usage
qm monitor 100 info status
pct exec 200 -- df -h
```

## Lab Exercises
1. Install and configure Proxmox VE cluster
2. Create VM and container templates
3. Implement automated backup strategy
4. Configure high availability for critical VMs
5. Set up monitoring and alerting system

## Next Steps
With Proxmox VE mastered, you're ready to explore OpenSSH Best Practices in Module 13, where you'll learn to secure remote access and implement advanced SSH configurations for your infrastructure.
