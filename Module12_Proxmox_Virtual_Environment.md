# Module 12: Proxmox Virtual Environment

## Overview

Master enterprise-grade virtualization infrastructure with Proxmox Virtual Environment (PVE), the complete open-source virtualization platform that combines KVM hypervisor capabilities with LXC containers, advanced storage management, and high-availability clustering. This module provides comprehensive coverage of designing, deploying, and managing scalable virtualization infrastructure for production environments.

Proxmox VE delivers enterprise virtualization features including live migration, automated backups, software-defined networking, and integrated storage management with ZFS and Ceph support. Learn to build resilient, high-performance virtualization clusters that can scale from single-node deployments to large multi-datacenter infrastructures.

**Enterprise Capabilities Covered:**
- Production-grade virtualization infrastructure design and implementation
- Advanced storage backends with ZFS, Ceph, and software-defined storage
- High-availability clustering with automated failover and load balancing
- Enterprise networking with VLANs, SDN, and micro-segmentation
- Comprehensive backup strategies with Proxmox Backup Server integration
- API-driven automation and infrastructure-as-code practices

## Learning Objectives

By completing this module, you will be able to:

1. **Design and Deploy Enterprise Virtualization Infrastructure**
   - Plan hardware requirements and validate compatibility for production deployments
   - Install and configure Proxmox VE clusters with optimal storage and networking
   - Implement security hardening and access control for enterprise environments

2. **Manage Advanced Storage and Networking**
   - Configure and optimize storage backends including ZFS pools and Ceph clusters
   - Design and implement software-defined networking with VLANs and security zones
   - Implement high-performance storage solutions with proper IOPS and latency optimization

3. **Orchestrate Virtual Machines and Containers**
   - Create and manage KVM virtual machines with enterprise-grade configurations
   - Deploy and orchestrate LXC containers for microservices and application hosting
   - Implement resource management, NUMA optimization, and performance tuning

4. **Build High-Availability Clusters**
   - Design and implement multi-node clusters with shared storage and automated failover
   - Configure fencing mechanisms, quorum management, and split-brain prevention
   - Perform live migrations and maintain zero-downtime operations during maintenance

5. **Implement Enterprise Backup and Disaster Recovery**
   - Design comprehensive backup strategies with automated scheduling and retention
   - Deploy and manage Proxmox Backup Server for enterprise-grade data protection
   - Implement disaster recovery procedures and validate restore capabilities

6. **Automate Infrastructure Operations**
   - Leverage Proxmox REST API for infrastructure automation and monitoring integration
   - Implement infrastructure-as-code practices with Ansible and Terraform
   - Build custom automation tools and integration with external systems

## Table of Contents

### [12.1 Enterprise Installation and Storage Architecture](#121-enterprise-installation-and-storage-architecture)
- Hardware planning and compatibility validation
- Production installation procedures and post-deployment hardening
- Storage backend selection and enterprise architecture design
- ZFS and Ceph configuration for high-performance workloads
- Security hardening and compliance configuration

### [12.2 Advanced Networking and SDN](#122-advanced-networking-and-sdn)
- Enterprise network architecture design and VLAN planning
- Software-Defined Networking (SDN) implementation and management
- Network security zones and micro-segmentation strategies
- High-availability networking with bonding and redundancy
- Performance optimization and troubleshooting network issues

### [12.3 KVM Virtual Machine Management](#123-kvm-virtual-machine-management)
- Enterprise VM templates and automated provisioning workflows
- Advanced resource management and NUMA optimization
- GPU passthrough and specialized hardware configuration
- Performance monitoring, tuning, and capacity planning
- VM lifecycle management and automated scaling

### [12.4 LXC Container Orchestration](#124-lxc-container-orchestration)
- Container architecture design and use case optimization
- Advanced container networking and storage integration
- Resource isolation and security container management
- Container templates and automated deployment pipelines
- Integration with container orchestration platforms

### [12.5 High-Availability Clustering](#125-high-availability-clustering)
- Multi-node cluster design and implementation strategies
- Corosync configuration and network redundancy planning
- Fencing mechanisms and STONITH device configuration
- Quorum management and cluster maintenance procedures
- Disaster recovery and geographic distribution

### [12.6 Live Migration and Maintenance](#126-live-migration-and-maintenance)
- Migration strategies and performance optimization
- Automated load balancing and resource optimization
- Zero-downtime maintenance procedures and planning
- Troubleshooting migration issues and performance problems
- Cross-datacenter migration and DR procedures

### [12.7 Enterprise Backup and Recovery](#127-enterprise-backup-and-recovery)
- Backup architecture design and storage planning
- Proxmox Backup Server deployment and configuration
- Automated backup policies and retention management
- Disaster recovery testing and validation procedures
- Integration with enterprise backup solutions

### [12.8 API Automation and Infrastructure as Code](#128-api-automation-and-infrastructure-as-code)
- REST API integration and authentication management
- Infrastructure automation with Python and Bash scripting
- Ansible playbooks for Proxmox infrastructure management
- Terraform integration for infrastructure provisioning
- Monitoring integration and custom dashboard development

## Essential Command Reference

### Proxmox VE System Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Cluster Management** | `pvecm create <cluster-name>` | Create new cluster | `pvecm create production-cluster` |
| | `pvecm add <node-ip>` | Add node to cluster | `pvecm add 10.0.1.101` |
| | `pvecm nodes` | List cluster nodes | `pvecm nodes` |
| | `pvecm status` | Show cluster status | `pvecm status` |
| | `pvecm delnode <node>` | Remove node from cluster | `pvecm delnode pve-node-02` |
| **Node Management** | `pveversion` | Show version information | `pveversion -v` |
| | `pvesh` | Proxmox shell interface | `pvesh ls /nodes` |
| | `pvenode config <node>` | Show node configuration | `pvenode config pve-node-01` |
| | `systemctl status pve-cluster` | Check cluster service | `systemctl status pve-cluster` |

### Storage Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Storage Backend** | `pvesm add <type> <id>` | Add storage backend | `pvesm add zfspool zfs-vm --pool vmdata` |
| | `pvesm list <storage>` | List storage contents | `pvesm list local-zfs` |
| | `pvesm status` | Show storage status | `pvesm status` |
| | `pvesm remove <storage>` | Remove storage backend | `pvesm remove old-storage` |
| **ZFS Integration** | `zpool status` | Check ZFS pool status | `zpool status vmdata` |
| | `zfs list` | List ZFS datasets | `zfs list -r vmdata` |
| | `pvesm zfsscan` | Scan for ZFS pools | `pvesm zfsscan` |
| **Ceph Integration** | `pveceph status` | Show Ceph cluster status | `pveceph status` |
| | `pveceph pool create <name>` | Create Ceph pool | `pveceph pool create vmpool` |
| | `pveceph pool destroy <name>` | Remove Ceph pool | `pveceph pool destroy oldpool` |

### Virtual Machine Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **VM Operations** | `qm create <vmid>` | Create new VM | `qm create 100 --memory 4096 --cores 2` |
| | `qm start <vmid>` | Start virtual machine | `qm start 100` |
| | `qm stop <vmid>` | Stop virtual machine | `qm stop 100` |
| | `qm shutdown <vmid>` | Graceful shutdown | `qm shutdown 100` |
| | `qm reboot <vmid>` | Reboot virtual machine | `qm reboot 100` |
| | `qm destroy <vmid>` | Delete virtual machine | `qm destroy 100` |
| **VM Configuration** | `qm config <vmid>` | Show VM configuration | `qm config 100` |
| | `qm set <vmid> <option>` | Modify VM settings | `qm set 100 --memory 8192` |
| | `qm resize <vmid> <disk> <size>` | Resize VM disk | `qm resize 100 virtio0 +10G` |
| | `qm monitor <vmid>` | Enter VM monitor | `qm monitor 100` |
| **VM Templates** | `qm template <vmid>` | Convert VM to template | `qm template 9000` |
| | `qm clone <vmid> <newid>` | Clone VM or template | `qm clone 9000 100 --name web-server-01` |
| | `qm list` | List all VMs | `qm list` |
| **VM Migration** | `qm migrate <vmid> <node>` | Migrate VM to node | `qm migrate 100 pve-node-02` |
| | `qm migrate <vmid> <node> --online` | Live migration | `qm migrate 100 pve-node-02 --online` |

### Container Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Container Operations** | `pct create <vmid> <template>` | Create container | `pct create 200 ubuntu-20.04-standard_20.04-1_amd64.tar.gz` |
| | `pct start <vmid>` | Start container | `pct start 200` |
| | `pct stop <vmid>` | Stop container | `pct stop 200` |
| | `pct shutdown <vmid>` | Graceful shutdown | `pct shutdown 200` |
| | `pct destroy <vmid>` | Delete container | `pct destroy 200` |
| | `pct enter <vmid>` | Enter container console | `pct enter 200` |
| **Container Configuration** | `pct config <vmid>` | Show container config | `pct config 200` |
| | `pct set <vmid> <option>` | Modify container settings | `pct set 200 --memory 2048` |
| | `pct resize <vmid> <disk> <size>` | Resize container disk | `pct resize 200 rootfs +5G` |
| | `pct list` | List all containers | `pct list` |
| **Container Templates** | `pveam update` | Update template list | `pveam update` |
| | `pveam download <storage> <template>` | Download template | `pveam download local ubuntu-20.04-standard_20.04-1_amd64.tar.gz` |
| | `pveam list <storage>` | List available templates | `pveam list local` |
| **Container Migration** | `pct migrate <vmid> <node>` | Migrate container | `pct migrate 200 pve-node-02` |
| | `pct migrate <vmid> <node> --restart` | Migrate with restart | `pct migrate 200 pve-node-02 --restart` |

### Backup Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Backup Operations** | `vzdump <vmid>` | Create VM/CT backup | `vzdump 100 --storage backup-storage` |
| | `vzdump --all` | Backup all VMs/CTs | `vzdump --all --storage backup-storage` |
| | `qmrestore <backup> <vmid>` | Restore VM backup | `qmrestore /backup/vzdump-qemu-100.vma 101` |
| | `pct restore <vmid> <backup>` | Restore container backup | `pct restore 201 /backup/vzdump-lxc-200.tar.gz` |
| **Backup Scheduling** | `vzdump --schedule` | Show backup schedule | `cat /etc/pve/vzdump.cron` |
| | `pvesh create /cluster/backup` | Create backup job | `pvesh create /cluster/backup --vmid 100 --storage backup` |
| **PBS Integration** | `proxmox-backup-client` | PBS client operations | `proxmox-backup-client backup vm.conf /path/to/vm` |
| | `proxmox-backup-manager` | PBS server management | `proxmox-backup-manager datastore list` |

### Network Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **Bridge Management** | `ip link show` | Show network interfaces | `ip link show type bridge` |
| | `brctl show` | Show bridge information | `brctl show vmbr0` |
| | `pvesh get /nodes/<node>/network` | Get network config | `pvesh get /nodes/pve-node-01/network` |
| **VLAN Configuration** | `ip link add vmbr0.100 type vlan` | Create VLAN interface | `ip link add vmbr0.100 type vlan id 100 link vmbr0` |
| | `pvesh set /nodes/<node>/network/<iface>` | Configure interface | `pvesh set /nodes/pve-node-01/network/vmbr0` |
| **SDN Management** | `pvesh get /cluster/sdn` | Show SDN configuration | `pvesh get /cluster/sdn/zones` |
| | `pvesh create /cluster/sdn/zones` | Create SDN zone | `pvesh create /cluster/sdn/zones --zone lab --type simple` |

### High Availability Management

| Command Category | Command | Description | Example |
|------------------|---------|-------------|---------|
| **HA Configuration** | `ha-manager config` | Show HA configuration | `ha-manager config` |
| | `ha-manager add <vmid>` | Add VM to HA | `ha-manager add vm:100 --state started --group production` |
| | `ha-manager remove <vmid>` | Remove VM from HA | `ha-manager remove vm:100` |
| | `ha-manager status` | Show HA status | `ha-manager status` |
| **Resource Groups** | `ha-manager groupadd <group>` | Create HA group | `ha-manager groupadd production --nodes pve-node-01:2,pve-node-02:1` |
| | `ha-manager groupdel <group>` | Delete HA group | `ha-manager groupdel production` |
| **Fencing** | `stonith_admin --list` | List STONITH devices | `stonith_admin --list` |
| | `stonith_admin --fence <node>` | Fence node manually | `stonith_admin --fence pve-node-02` |

| **Fencing** | `stonith_admin --list` | List STONITH devices | `stonith_admin --list` |
| | `stonith_admin --fence <node>` | Fence node manually | `stonith_admin --fence pve-node-02` |

## Comprehensive Practical Examples

### 12.1 Enterprise Installation and Storage Architecture

#### Production Hardware Planning and Validation
```bash
#!/bin/bash
# proxmox-hardware-validator.sh - Enterprise hardware validation and planning

VALIDATION_LOG="/var/log/proxmox-hardware-validation.log"
REQUIREMENTS_CONFIG="/etc/proxmox/hardware-requirements.conf"

log_validation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$VALIDATION_LOG"
}

# Create hardware requirements configuration
create_hardware_requirements() {
    log_validation "Creating hardware requirements configuration"
    
    mkdir -p "$(dirname "$REQUIREMENTS_CONFIG")"
    cat > "$REQUIREMENTS_CONFIG" << 'EOF'
# Proxmox VE Hardware Requirements Configuration
# Format: component:minimum:recommended:enterprise

# CPU Requirements
cpu_cores:4:8:16
cpu_frequency:2000:2400:3000
cpu_features:vmx,svm:vmx,svm,aes:vmx,svm,aes,avx2

# Memory Requirements (GB)
memory_total:8:32:128
memory_ecc:optional:recommended:required

# Storage Requirements
storage_system:20:100:500
storage_vm:100:1000:10000
storage_type:sata:ssd:nvme

# Network Requirements
network_ports:1:2:4
network_speed:1000:10000:25000
network_redundancy:single:bonded:lacp

EOF
    
    log_validation "Hardware requirements configuration created"
}

# Validate hardware compatibility
validate_hardware_compatibility() {
    log_validation "Starting hardware compatibility validation"
    
    # CPU validation
    local cpu_cores=$(nproc)
    local cpu_flags=$(grep flags /proc/cpuinfo | head -1 | cut -d: -f2)
    local cpu_model=$(grep "model name" /proc/cpuinfo | head -1 | cut -d: -f2 | xargs)
    
    log_validation "CPU Information:"
    log_validation "  Cores: $cpu_cores"
    log_validation "  Model: $cpu_model"
    log_validation "  Virtualization Support: $(echo "$cpu_flags" | grep -o -E "(vmx|svm)" | head -1)"
    
    # Check for required CPU features
    local required_features=("vmx" "svm")
    local virtualization_support=false
    
    for feature in "${required_features[@]}"; do
        if echo "$cpu_flags" | grep -q "$feature"; then
            log_validation "  ✓ Virtualization feature found: $feature"
            virtualization_support=true
            break
        fi
    done
    
    if [[ "$virtualization_support" == "false" ]]; then
        log_validation "  ✗ ERROR: No virtualization support found (VMX/SVM required)"
        return 1
    fi
    
    # Memory validation
    local memory_total_kb=$(grep MemTotal /proc/meminfo | awk '{print $2}')
    local memory_total_gb=$((memory_total_kb / 1024 / 1024))
    
    log_validation "Memory Information:"
    log_validation "  Total RAM: ${memory_total_gb}GB"
    
    # Check for ECC memory
    local ecc_status="Not detected"
    if dmidecode -t memory 2>/dev/null | grep -q "Error Correction Type.*ECC"; then
        ecc_status="Supported"
    fi
    log_validation "  ECC Support: $ecc_status"
    
    # Storage validation
    log_validation "Storage Information:"
    lsblk -d -o NAME,SIZE,TYPE,ROTA | while read -r name size type rota; do
        [[ "$name" == "NAME" ]] && continue
        local storage_type="HDD"
        [[ "$rota" == "0" ]] && storage_type="SSD"
        log_validation "  Device: $name, Size: $size, Type: $storage_type"
    done
    
    # Network validation
    log_validation "Network Information:"
    ip link show | grep -E "^[0-9]+:" | while read -r line; do
        local interface=$(echo "$line" | cut -d: -f2 | xargs)
        [[ "$interface" == "lo" ]] && continue
        
        local speed="Unknown"
        local speed_file="/sys/class/net/$interface/speed"
        if [[ -r "$speed_file" ]]; then
            local speed_mbps=$(cat "$speed_file" 2>/dev/null || echo "0")
            [[ "$speed_mbps" != "-1" ]] && speed="${speed_mbps}Mbps"
        fi
        
        log_validation "  Interface: $interface, Speed: $speed"
    done
    
    log_validation "Hardware compatibility validation completed"
}

# Install Proxmox VE with enterprise configuration
install_proxmox_enterprise() {
    log_validation "Starting Proxmox VE enterprise installation"
    
    # Validate prerequisites
    if ! validate_hardware_compatibility; then
        log_validation "Hardware validation failed, aborting installation"
        return 1
    fi
    
    # Configure APT repositories for enterprise
    log_validation "Configuring Proxmox VE repositories"
    
    # Add Proxmox VE repository
    echo "deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-install-repo.list
    
    # Add repository key
    wget https://enterprise.proxmox.com/debian/proxmox-release-bullseye.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bullseye.gpg
    
    # Update package lists
    apt update
    
    # Install Proxmox VE packages
    log_validation "Installing Proxmox VE packages"
    DEBIAN_FRONTEND=noninteractive apt-get install -y proxmox-ve postfix open-iscsi
    
    # Configure Postfix for system notifications
    debconf-set-selections <<< "postfix postfix/mailname string $(hostname -f)"
    debconf-set-selections <<< "postfix postfix/main_mailer_type string 'Internet Site'"
    
    # Remove enterprise repository if not licensed
    rm -f /etc/apt/sources.list.d/pve-enterprise.list
    
    # Configure system settings
    configure_system_optimization
    
    log_validation "Proxmox VE installation completed"
}

# Configure system optimization for production
configure_system_optimization() {
    log_validation "Configuring system optimization for production"
    
    # Kernel parameters for virtualization
    cat >> /etc/sysctl.conf << 'EOF'
# Proxmox VE Optimization Settings
# Network optimization
net.core.rmem_max = 134217728
net.core.wmem_max = 134217728
net.ipv4.tcp_rmem = 4096 87380 134217728
net.ipv4.tcp_wmem = 4096 65536 134217728
net.core.netdev_max_backlog = 30000
net.ipv4.tcp_no_metrics_save = 1
net.ipv4.tcp_congestion_control = bbr

# Memory management
vm.swappiness = 10
vm.vfs_cache_pressure = 50
vm.dirty_background_ratio = 5
vm.dirty_ratio = 10

# KVM optimization
kernel.sched_migration_cost_ns = 5000000
kernel.sched_autogroup_enabled = 0

EOF
    
    # Apply kernel parameters
    sysctl -p
    
    # Configure CPU governor for performance
    echo "performance" | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
    
    # Disable unnecessary services
    systemctl disable bluetooth
    systemctl disable cups
    systemctl disable avahi-daemon
    
    # Configure log rotation for Proxmox
    cat > /etc/logrotate.d/proxmox << 'EOF'
/var/log/pve/*.log {
    daily
    rotate 30
    compress
    delaycompress
    missingok
    notifempty
    create 640 root adm
    postrotate
        systemctl reload pveproxy
    endscript
}
EOF
    
    log_validation "System optimization configuration completed"
}

# Enterprise storage backend configuration
configure_enterprise_storage() {
    local storage_type="$1"  # zfs, ceph, lvm-thin
    local pool_name="$2"
    local devices="$3"      # space-separated device list
    
    log_validation "Configuring enterprise storage backend: $storage_type"
    
    case "$storage_type" in
        "zfs")
            configure_zfs_storage "$pool_name" "$devices"
            ;;
        "ceph")
            configure_ceph_storage "$pool_name" "$devices"
            ;;
        "lvm-thin")
            configure_lvm_thin_storage "$pool_name" "$devices"
            ;;
        *)
            log_validation "ERROR: Unknown storage type: $storage_type"
            return 1
            ;;
    esac
}

# Configure ZFS storage for high performance
configure_zfs_storage() {
    local pool_name="$1"
    local devices="$2"
    
    log_validation "Configuring ZFS storage pool: $pool_name"
    
    # Parse devices into array
    local device_array=($devices)
    local device_count=${#device_array[@]}
    
    # Determine optimal RAID configuration based on device count
    if [[ $device_count -eq 2 ]]; then
        # Mirror for 2 devices
        zpool create -o ashift=12 "$pool_name" mirror "${device_array[@]}"
        log_validation "Created ZFS mirror pool with 2 devices"
    elif [[ $device_count -eq 4 ]]; then
        # RAID-10 for 4 devices
        zpool create -o ashift=12 "$pool_name" \
            mirror "${device_array[0]}" "${device_array[1]}" \
            mirror "${device_array[2]}" "${device_array[3]}"
        log_validation "Created ZFS RAID-10 pool with 4 devices"
    elif [[ $device_count -ge 6 ]]; then
        # RAID-Z2 for 6+ devices
        zpool create -o ashift=12 "$pool_name" raidz2 "${device_array[@]}"
        log_validation "Created ZFS RAID-Z2 pool with $device_count devices"
    else
        log_validation "ERROR: Invalid device count for ZFS: $device_count"
        return 1
    fi
    
    # Configure ZFS optimization for virtualization
    zfs set compression=lz4 "$pool_name"
    zfs set atime=off "$pool_name"
    zfs set sync=standard "$pool_name"
    zfs set primarycache=all "$pool_name"
    zfs set secondarycache=all "$pool_name"
    zfs set logbias=latency "$pool_name"
    
    # Create datasets for different workloads
    zfs create "$pool_name/vm-disks"
    zfs create "$pool_name/ct-volumes"
    zfs create "$pool_name/backups"
    zfs create "$pool_name/templates"
    
    # Optimize datasets for specific workloads
    zfs set recordsize=64K "$pool_name/vm-disks"
    zfs set recordsize=128K "$pool_name/ct-volumes"
    zfs set recordsize=1M "$pool_name/backups"
    zfs set compression=zstd "$pool_name/backups"
    
    # Add to Proxmox storage configuration
    pvesm add zfspool "$pool_name" --pool "$pool_name" --content images,rootdir
    
    log_validation "ZFS storage configuration completed"
}

# Configure Ceph cluster storage
configure_ceph_storage() {
    local cluster_name="$1"
    local devices="$2"
    
    log_validation "Configuring Ceph cluster storage: $cluster_name"
    
    # Install Ceph packages
    pveceph install --repository no-subscription
    
    # Initialize Ceph cluster
    pveceph init --network $(ip route | grep "$(hostname -I | awk '{print $1}')" | grep -oE '([0-9]{1,3}\.){3}[0-9]{1,3}/[0-9]{1,2}' | head -1)
    
    # Create monitor
    pveceph mon create
    
    # Create manager
    pveceph mgr create
    
    # Create OSDs for each device
    local device_array=($devices)
    for device in "${device_array[@]}"; do
        log_validation "Creating OSD on device: $device"
        pveceph osd create "$device"
    done
    
    # Create pools for Proxmox
    pveceph pool create vm-pool --size 3 --min_size 2
    pveceph pool create ct-pool --size 3 --min_size 2
    
    # Add Ceph storage to Proxmox
    pvesm add cephfs cephfs --monhost $(hostname -I | awk '{print $1}') --content vztmpl,iso,backup
    pvesm add rbd vm-pool --monhost $(hostname -I | awk '{print $1}') --pool vm-pool --content images
    pvesm add rbd ct-pool --monhost $(hostname -I | awk '{print $1}') --pool ct-pool --content rootdir
    
    log_validation "Ceph storage configuration completed"
}

# Configure LVM-thin storage
configure_lvm_thin_storage() {
    local vg_name="$1"
    local devices="$2"
    
    log_validation "Configuring LVM-thin storage: $vg_name"
    
    # Parse devices into array
    local device_array=($devices)
    
    # Create physical volumes
    for device in "${device_array[@]}"; do
        pvcreate "$device"
    done
    
    # Create volume group
    vgcreate "$vg_name" "${device_array[@]}"
    
    # Create thin pool (use 90% of VG space)
    local vg_size=$(vgdisplay "$vg_name" | grep "VG Size" | awk '{print $3}' | sed 's/\..*//')
    local thin_size=$((vg_size * 90 / 100))
    
    lvcreate -L "${thin_size}G" -T "$vg_name/thin-pool"
    
    # Add to Proxmox storage configuration
    pvesm add lvmthin "$vg_name" --vgname "$vg_name" --thinpool thin-pool --content images,rootdir
    
    log_validation "LVM-thin storage configuration completed"
}

# Post-installation security hardening
implement_security_hardening() {
    log_validation "Implementing security hardening"
    
    # Configure firewall
    cat > /etc/pve/firewall/cluster.fw << 'EOF'
[OPTIONS]
enable: 1
policy_in: DROP
policy_out: ACCEPT

[RULES]
# Proxmox Web Interface
IN ACCEPT -p tcp -dport 8006 -source +management_net

# Proxmox Cluster Communication
IN ACCEPT -p udp -dport 5404:5412 -source +cluster_net
IN ACCEPT -p tcp -dport 22 -source +management_net

# Ceph Communication (if using Ceph)
IN ACCEPT -p tcp -dport 6789 -source +cluster_net
IN ACCEPT -p tcp -dport 6800:7300 -source +cluster_net

# Migration Traffic
IN ACCEPT -p tcp -dport 60000:60050 -source +cluster_net

# VNC/SPICE Console
IN ACCEPT -p tcp -dport 5900:5999 -source +management_net

EOF
    
    # Create IP sets for management
    cat > /etc/pve/firewall/ipset.fw << 'EOF'
[ipset management_net]
10.0.1.0/24
192.168.1.0/24

[ipset cluster_net]
10.0.1.0/24

EOF
    
    # Configure SSH hardening
    sed -i 's/#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
    echo "AllowUsers pve-admin" >> /etc/ssh/sshd_config
    
    # Restart SSH service
    systemctl restart sshd
    
    # Configure automatic updates for security patches
    cat > /etc/apt/apt.conf.d/50unattended-upgrades << 'EOF'
Unattended-Upgrade::Allowed-Origins {
    "${distro_id}:${distro_codename}-security";
    "Proxmox:${distro_codename}";
};

Unattended-Upgrade::AutoFixInterruptedDpkg "true";
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Automatic-Reboot "false";

EOF
    
    echo 'APT::Periodic::Update-Package-Lists "1";' > /etc/apt/apt.conf.d/20auto-upgrades
    echo 'APT::Periodic::Unattended-Upgrade "1";' >> /etc/apt/apt.conf.d/20auto-upgrades
    
    # Enable and start unattended-upgrades
    systemctl enable unattended-upgrades
    systemctl start unattended-upgrades
    
    log_validation "Security hardening completed"
}

# Example usage and main execution
create_hardware_requirements
validate_hardware_compatibility

# Example enterprise storage configurations
# configure_enterprise_storage "zfs" "vmdata" "/dev/sdb /dev/sdc /dev/sdd /dev/sde"
# configure_enterprise_storage "ceph" "ceph-cluster" "/dev/sdb /dev/sdc /dev/sdd"
# configure_enterprise_storage "lvm-thin" "vm-storage" "/dev/sdb /dev/sdc"

implement_security_hardening

log_validation "Enterprise Proxmox VE installation and configuration completed"
```

### 12.2 Advanced Networking and SDN

#### Enterprise Network Architecture Design
```bash
#!/bin/bash
# proxmox-network-manager.sh - Enterprise network configuration for Proxmox VE

NETWORK_LOG="/var/log/proxmox-network.log"
NETWORK_CONFIG="/etc/pve/network-architecture.conf"

log_network() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$NETWORK_LOG"
}

# Create network architecture configuration
create_network_architecture() {
    log_network "Creating network architecture configuration"
    
    cat > "$NETWORK_CONFIG" << 'EOF'
# Proxmox VE Network Architecture Configuration
# Format: network_type:vlan_id:subnet:description:security_zone

# Management Networks
management:100:10.0.100.0/24:Proxmox Management Network:trusted
cluster:101:10.0.101.0/24:Cluster Communication:trusted
storage:102:10.0.102.0/24:Storage Network (Ceph/iSCSI):trusted

# Production Networks
production:200:10.0.200.0/24:Production VMs:dmz
database:201:10.0.201.0/24:Database Servers:secure
web:202:10.0.202.0/24:Web Servers:dmz

# Development Networks
development:300:10.0.300.0/24:Development Environment:development
testing:301:10.0.301.0/24:Testing Environment:development
staging:302:10.0.302.0/24:Staging Environment:staging

# Guest Networks
guest:400:10.0.400.0/24:Guest Access:guest
iot:401:10.0.401.0/24:IoT Devices:iot

EOF
    
    log_network "Network architecture configuration created"
}

# Configure enterprise bridge networking with VLANs
configure_enterprise_bridges() {
    log_network "Configuring enterprise bridge networking"
    
    # Backup current network configuration
    cp /etc/network/interfaces /etc/network/interfaces.backup.$(date +%Y%m%d_%H%M%S)
    
    # Create enterprise network configuration
    cat > /etc/network/interfaces << 'EOF'
# Enterprise Proxmox VE Network Configuration
# Generated by proxmox-network-manager.sh

auto lo
iface lo inet loopback

# Primary physical interfaces with bonding for redundancy
auto bond0
iface bond0 inet manual
    bond-slaves eno1 eno2
    bond-miimon 100
    bond-mode 802.3ad
    bond-xmit-hash-policy layer2+3
    bond-lacp-rate 1

# Management bridge (untagged)
auto vmbr0
iface vmbr0 inet static
    address 10.0.100.10/24
    gateway 10.0.100.1
    bridge-ports bond0
    bridge-stp off
    bridge-fd 0
    bridge-vlan-aware yes
    bridge-vids 100-499

# VLAN interfaces for different networks
auto vmbr0.101
iface vmbr0.101 inet static
    address 10.0.101.10/24
    vlan-raw-device vmbr0

auto vmbr0.102
iface vmbr0.102 inet static
    address 10.0.102.10/24
    vlan-raw-device vmbr0

# Dedicated storage network bridge (if separate NICs available)
auto vmbr1
iface vmbr1 inet static
    address 10.0.102.10/24
    bridge-ports eno3
    bridge-stp off
    bridge-fd 0
    # High MTU for storage traffic
    mtu 9000
    post-up echo 9000 > /sys/class/net/vmbr1/mtu

EOF
    
    log_network "Enterprise bridge configuration created"
}

# Configure Software-Defined Networking (SDN)
configure_sdn() {
    log_network "Configuring Software-Defined Networking"
    
    # Create SDN zones configuration
    cat > /etc/pve/sdn/zones.cfg << 'EOF'
# SDN Zones Configuration

# Simple zone for basic isolation
simple: development
    bridge vmbr0
    ipam pve

simple: production
    bridge vmbr0
    ipam pve

# VXLAN zone for advanced networking
vxlan: overlay-prod
    peers 10.0.101.10,10.0.101.11,10.0.101.12
    bridge vmbr0
    ipam pve

# EVPN zone for enterprise networking
evpn: enterprise-evpn
    vrf-vxlan 1000
    controller evpn-controller
    mac-learning 1
    ipam pve

EOF
    
    # Create VNets configuration
    cat > /etc/pve/sdn/vnets.cfg << 'EOF'
# VNets Configuration

# Development networks
vnet: dev-network
    zone development
    tag 300

vnet: test-network
    zone development
    tag 301

# Production networks
vnet: prod-web
    zone production
    tag 202

vnet: prod-db
    zone production
    tag 201

# Overlay networks
vnet: overlay-app
    zone overlay-prod
    tag 1000
    alias Application Overlay Network

EOF
    
    # Create IP address management (IPAM) configuration
    cat > /etc/pve/sdn/ipams.cfg << 'EOF'
# IPAM Configuration

# Built-in PVE IPAM
pve: pve-ipam
    
# External IPAM (example for future integration)
# netbox: netbox-ipam
#     url https://netbox.company.com
#     token your-api-token

EOF
    
    # Apply SDN configuration
    pvesh set /cluster/sdn --apply 1
    
    log_network "SDN configuration completed"
}

# Configure network security and micro-segmentation
configure_network_security() {
    log_network "Configuring network security and micro-segmentation"
    
    # Create security zones firewall rules
    cat > /etc/pve/firewall/cluster.fw << 'EOF'
[OPTIONS]
enable: 1
policy_in: DROP
policy_out: ACCEPT
log_level_in: info

[ALIASES]
management_net 10.0.100.0/24
cluster_net 10.0.101.0/24
storage_net 10.0.102.0/24
production_net 10.0.200.0/24
database_net 10.0.201.0/24
web_net 10.0.202.0/24
development_net 10.0.300.0/24
guest_net 10.0.400.0/24

[RULES]
# Management access
IN ACCEPT -p tcp -dport 22 -source management_net -log nolog
IN ACCEPT -p tcp -dport 8006 -source management_net -log nolog

# Cluster communication
IN ACCEPT -source cluster_net -log nolog

# Storage network access
IN ACCEPT -source storage_net -dest storage_net -log nolog

# Inter-zone communication rules
IN ACCEPT -source web_net -dest database_net -p tcp -dport 3306,5432 -log enable
IN ACCEPT -source production_net -dest storage_net -p tcp -dport 3260,6789 -log nolog

# Block guest network from internal networks
IN DROP -source guest_net -dest management_net,cluster_net,storage_net,production_net,database_net -log enable

# Development network isolation
IN DROP -source development_net -dest production_net,database_net -log enable

EOF
    
    # Create VM-specific security groups
    mkdir -p /etc/pve/firewall/
    
    # Web server security group
    cat > /etc/pve/firewall/web-servers.fw << 'EOF'
[OPTIONS]
enable: 1

[RULES]
IN ACCEPT -p tcp -dport 80,443 -log nolog
IN ACCEPT -p tcp -dport 22 -source management_net -log nolog
IN DROP -log enable

EOF
    
    # Database server security group
    cat > /etc/pve/firewall/database-servers.fw << 'EOF'
[OPTIONS]
enable: 1

[RULES]
IN ACCEPT -p tcp -dport 3306 -source web_net -log nolog
IN ACCEPT -p tcp -dport 5432 -source web_net -log nolog
IN ACCEPT -p tcp -dport 22 -source management_net -log nolog
IN DROP -log enable

EOF
    
    log_network "Network security configuration completed"
}

# Implement Quality of Service (QoS) for different traffic types
configure_network_qos() {
    log_network "Configuring network Quality of Service (QoS)"
    
    # Traffic classification and shaping script
    cat > /usr/local/bin/proxmox-qos.sh << 'EOF'
#!/bin/bash
# Proxmox VE QoS Configuration

# Clear existing rules
tc qdisc del dev vmbr0 root 2>/dev/null || true

# Create HTB root qdisc
tc qdisc add dev vmbr0 root handle 1: htb default 30

# Create classes for different traffic types
# Total bandwidth: 10Gbps
tc class add dev vmbr0 parent 1: classid 1:1 htb rate 10gbit

# Management traffic (guaranteed 1Gbps, max 2Gbps)
tc class add dev vmbr0 parent 1:1 classid 1:10 htb rate 1gbit ceil 2gbit prio 1

# Storage traffic (guaranteed 4Gbps, max 6Gbps)
tc class add dev vmbr0 parent 1:1 classid 1:20 htb rate 4gbit ceil 6gbit prio 2

# VM traffic (guaranteed 3Gbps, max 8Gbps)
tc class add dev vmbr0 parent 1:1 classid 1:30 htb rate 3gbit ceil 8gbit prio 3

# Guest traffic (guaranteed 1Gbps, max 2Gbps)
tc class add dev vmbr0 parent 1:1 classid 1:40 htb rate 1gbit ceil 2gbit prio 4

# Create filters to classify traffic
# Management traffic (VLAN 100)
tc filter add dev vmbr0 protocol 802.1Q parent 1: prio 1 u32 match u16 0x0064 0x0fff at -4 flowid 1:10

# Storage traffic (VLAN 102)
tc filter add dev vmbr0 protocol 802.1Q parent 1: prio 1 u32 match u16 0x0066 0x0fff at -4 flowid 1:20

# Web traffic (VLAN 202)
tc filter add dev vmbr0 protocol 802.1Q parent 1: prio 2 u32 match u16 0x00ca 0x0fff at -4 flowid 1:30

# Database traffic (VLAN 201)
tc filter add dev vmbr0 protocol 802.1Q parent 1: prio 2 u32 match u16 0x00c9 0x0fff at -4 flowid 1:30

# Guest traffic (VLAN 400)
tc filter add dev vmbr0 protocol 802.1Q parent 1: prio 3 u32 match u16 0x0190 0x0fff at -4 flowid 1:40

echo "QoS configuration applied successfully"

EOF
    
    chmod +x /usr/local/bin/proxmox-qos.sh
    
    # Create systemd service for QoS
    cat > /etc/systemd/system/proxmox-qos.service << 'EOF'
[Unit]
Description=Proxmox VE QoS Configuration
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/proxmox-qos.sh
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

EOF
    
    systemctl enable proxmox-qos.service
    systemctl start proxmox-qos.service
    
    log_network "QoS configuration completed"
}

# Monitor network performance and utilization
monitor_network_performance() {
    log_network "Setting up network performance monitoring"
    
    # Create network monitoring script
    cat > /usr/local/bin/proxmox-network-monitor.sh << 'EOF'
#!/bin/bash
# Proxmox VE Network Performance Monitor

MONITOR_LOG="/var/log/proxmox-network-monitor.log"

log_monitor() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$MONITOR_LOG"
}

# Monitor bridge statistics
monitor_bridge_stats() {
    local bridge="$1"
    
    # Get interface statistics
    local rx_bytes=$(cat "/sys/class/net/$bridge/statistics/rx_bytes")
    local tx_bytes=$(cat "/sys/class/net/$bridge/statistics/tx_bytes")
    local rx_packets=$(cat "/sys/class/net/$bridge/statistics/rx_packets")
    local tx_packets=$(cat "/sys/class/net/$bridge/statistics/tx_packets")
    local rx_errors=$(cat "/sys/class/net/$bridge/statistics/rx_errors")
    local tx_errors=$(cat "/sys/class/net/$bridge/statistics/tx_errors")
    
    log_monitor "Bridge $bridge stats: RX: ${rx_bytes}B/${rx_packets}p TX: ${tx_bytes}B/${tx_packets}p Errors: RX:${rx_errors} TX:${tx_errors}"
}

# Monitor VLAN utilization
monitor_vlan_utilization() {
    local bridge="$1"
    
    # Get VLAN information
    bridge vlan show dev "$bridge" | while read line; do
        if [[ "$line" =~ ^[[:space:]]*([0-9]+) ]]; then
            local vlan_id="${BASH_REMATCH[1]}"
            # Monitor VLAN-specific traffic (simplified)
            log_monitor "VLAN $vlan_id on $bridge: Active"
        fi
    done
}

# Monitor QoS statistics
monitor_qos_stats() {
    local interface="$1"
    
    # Get QoS statistics
    tc -s class show dev "$interface" | grep -A5 "class htb" | while read line; do
        if [[ "$line" =~ class[[:space:]]+htb[[:space:]]+([0-9:]+) ]]; then
            local class_id="${BASH_REMATCH[1]}"
            log_monitor "QoS class $class_id statistics available"
        fi
    done
}

# Main monitoring loop
main() {
    log_monitor "Starting network performance monitoring"
    
    # Monitor primary bridges
    for bridge in vmbr0 vmbr1; do
        if ip link show "$bridge" &>/dev/null; then
            monitor_bridge_stats "$bridge"
            monitor_vlan_utilization "$bridge"
        fi
    done
    
    # Monitor QoS if configured
    if tc qdisc show dev vmbr0 | grep -q htb; then
        monitor_qos_stats "vmbr0"
    fi
    
    log_monitor "Network monitoring cycle completed"
}

main
EOF
    
    chmod +x /usr/local/bin/proxmox-network-monitor.sh
    
    # Schedule regular monitoring
    echo "*/5 * * * * /usr/local/bin/proxmox-network-monitor.sh" | crontab -
    
    log_network "Network performance monitoring setup completed"
}

# Main execution
create_network_architecture
configure_enterprise_bridges
configure_sdn
configure_network_security
configure_network_qos
monitor_network_performance

log_network "Enterprise network configuration completed"
```

### 12.3 KVM Virtual Machine Management

#### Enterprise VM Template System and Mass Deployment
```bash
#!/bin/bash
# proxmox-vm-manager.sh - Enterprise VM management and automation

VM_LOG="/var/log/proxmox-vm-manager.log"
TEMPLATE_CONFIG="/etc/pve/vm-templates.conf"
VM_INVENTORY="/var/lib/pve/vm-inventory.json"

log_vm() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$VM_LOG"
}

# Create VM template configuration
create_vm_template_config() {
    log_vm "Creating VM template configuration"
    
    cat > "$TEMPLATE_CONFIG" << 'EOF'
# VM Template Configuration
# Format: template_name:vmid:memory:cores:disk_size:network:description

# Base Templates
ubuntu-20.04-template:9000:2048:2:20G:vmbr0:Ubuntu 20.04 LTS Base Template
ubuntu-22.04-template:9001:2048:2:20G:vmbr0:Ubuntu 22.04 LTS Base Template
centos-8-template:9002:2048:2:20G:vmbr0:CentOS 8 Base Template
windows-2019-template:9010:4096:4:60G:vmbr0:Windows Server 2019 Template
windows-10-template:9011:4096:2:60G:vmbr0:Windows 10 Enterprise Template

# Application Templates
web-server-template:9020:4096:4:40G:vmbr0:Web Server Template (Nginx/Apache)
database-template:9021:8192:8:100G:vmbr0:Database Server Template (MySQL/PostgreSQL)
docker-host-template:9022:8192:4:80G:vmbr0:Docker Host Template
kubernetes-node-template:9023:8192:4:60G:vmbr0:Kubernetes Node Template

# Security Templates
firewall-template:9030:1024:2:20G:vmbr0:pfSense/OPNsense Template
proxy-template:9031:2048:2:40G:vmbr0:Proxy Server Template

EOF
    
    log_vm "VM template configuration created"
}

# Create enterprise VM template with cloud-init
create_enterprise_template() {
    local template_name="$1"
    local vmid="$2"
    local memory="$3"
    local cores="$4"
    local disk_size="$5"
    local network="$6"
    local iso_path="$7"
    
    log_vm "Creating enterprise VM template: $template_name (ID: $vmid)"
    
    # Create VM
    qm create "$vmid" \
        --name "$template_name" \
        --memory "$memory" \
        --cores "$cores" \
        --net0 "virtio,bridge=$network" \
        --scsihw virtio-scsi-pci \
        --scsi0 "local-zfs:$disk_size" \
        --ide2 "local:iso/$iso_path,media=cdrom" \
        --ostype l26 \
        --cpu cputype=host \
        --agent enabled=1 \
        --bios ovmf \
        --efidisk0 local-zfs:1 \
        --boot c \
        --bootdisk scsi0
    
    # Add cloud-init drive
    qm set "$vmid" --ide0 local-zfs:cloudinit
    
    # Configure cloud-init settings
    qm set "$vmid" \
        --ciuser sysadmin \
        --sshkey ~/.ssh/id_rsa.pub \
        --ipconfig0 ip=dhcp \
        --nameserver 8.8.8.8 \
        --searchdomain company.local
    
    # Install and configure the VM (manual step)
    log_vm "Template VM $vmid created. Manual installation required before conversion to template."
    
    # After manual installation, convert to template:
    # qm template $vmid
}

# Automated VM provisioning with cloud-init
provision_vm_from_template() {
    local template_id="$1"
    local new_vmid="$2"
    local vm_name="$3"
    local memory="$4"
    local cores="$5"
    local ip_config="$6"
    local purpose="$7"
    
    log_vm "Provisioning VM: $vm_name (ID: $new_vmid) from template $template_id"
    
    # Clone template to new VM
    qm clone "$template_id" "$new_vmid" \
        --name "$vm_name" \
        --full 1 \
        --storage local-zfs
    
    # Customize new VM
    qm set "$new_vmid" \
        --memory "$memory" \
        --cores "$cores" \
        --ipconfig0 "$ip_config" \
        --description "VM Purpose: $purpose | Created: $(date) | Template: $template_id"
    
    # Add VM to inventory
    update_vm_inventory "$new_vmid" "$vm_name" "$purpose" "provisioned"
    
    # Start VM
    qm start "$new_vmid"
    
    log_vm "VM $vm_name provisioned and started successfully"
}

# Mass VM deployment for specific purposes
mass_deploy_vms() {
    local purpose="$1"
    local template_id="$2"
    local count="$3"
    local base_vmid="$4"
    local network_base="$5"
    
    log_vm "Starting mass deployment of $count VMs for purpose: $purpose"
    
    for ((i=1; i<=count; i++)); do
        local vmid=$((base_vmid + i))
        local vm_name="${purpose}-node-$(printf "%02d" "$i")"
        local ip_address="${network_base}.$((100 + i))"
        
        case "$purpose" in
            "web-cluster")
                provision_vm_from_template "$template_id" "$vmid" "$vm_name" 4096 4 "ip=${ip_address}/24,gw=${network_base}.1" "$purpose"
                configure_web_server "$vmid"
                ;;
            "kubernetes-cluster")
                local memory=8192
                local cores=4
                [[ $i -eq 1 ]] && memory=16384 && cores=8  # Master node gets more resources
                provision_vm_from_template "$template_id" "$vmid" "$vm_name" "$memory" "$cores" "ip=${ip_address}/24,gw=${network_base}.1" "$purpose"
                configure_kubernetes_node "$vmid" "$i"
                ;;
            "database-cluster")
                provision_vm_from_template "$template_id" "$vmid" "$vm_name" 16384 8 "ip=${ip_address}/24,gw=${network_base}.1" "$purpose"
                configure_database_server "$vmid"
                ;;
        esac
        
        sleep 30  # Wait between deployments to avoid resource contention
    done
    
    log_vm "Mass deployment completed: $count VMs for $purpose"
}

# Configure VM for specific workloads
configure_web_server() {
    local vmid="$1"
    
    log_vm "Configuring web server on VM $vmid"
    
    # Wait for VM to be ready
    while ! qm guest ping "$vmid" >/dev/null 2>&1; do
        sleep 5
    done
    
    # Execute configuration via qemu-guest-agent
    qm guest exec "$vmid" -- /bin/bash -c "
        apt update && apt install -y nginx
        systemctl enable nginx
        systemctl start nginx
        ufw allow 'Nginx Full'
        echo 'Web server configured on $(hostname)' > /var/www/html/index.html
    "
    
    log_vm "Web server configuration completed on VM $vmid"
}

# Configure Kubernetes node
configure_kubernetes_node() {
    local vmid="$1"
    local node_number="$2"
    
    log_vm "Configuring Kubernetes node on VM $vmid (node $node_number)"
    
    # Wait for VM to be ready
    while ! qm guest ping "$vmid" >/dev/null 2>&1; do
        sleep 5
    done
    
    # Install Docker and Kubernetes
    qm guest exec "$vmid" -- /bin/bash -c "
        # Install Docker
        curl -fsSL https://get.docker.com -o get-docker.sh
        sh get-docker.sh
        usermod -aG docker sysadmin
        
        # Install Kubernetes components
        curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
        echo 'deb https://apt.kubernetes.io/ kubernetes-xenial main' > /etc/apt/sources.list.d/kubernetes.list
        apt update
        apt install -y kubelet kubeadm kubectl
        apt-mark hold kubelet kubeadm kubectl
        
        # Configure cgroup driver
        echo 'Environment=\"KUBELET_EXTRA_ARGS=--cgroup-driver=systemd\"' >> /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
        systemctl daemon-reload
        systemctl restart kubelet
    "
    
    if [[ $node_number -eq 1 ]]; then
        # Initialize master node
        qm guest exec "$vmid" -- /bin/bash -c "
            kubeadm init --pod-network-cidr=10.244.0.0/16
            mkdir -p /home/sysadmin/.kube
            cp -i /etc/kubernetes/admin.conf /home/sysadmin/.kube/config
            chown sysadmin:sysadmin /home/sysadmin/.kube/config
        "
        log_vm "Kubernetes master node initialized on VM $vmid"
    fi
    
    log_vm "Kubernetes node configuration completed on VM $vmid"
}

# Configure database server
configure_database_server() {
    local vmid="$1"
    
    log_vm "Configuring database server on VM $vmid"
    
    # Wait for VM to be ready
    while ! qm guest ping "$vmid" >/dev/null 2>&1; do
        sleep 5
    done
    
    # Install and configure MySQL/PostgreSQL
    qm guest exec "$vmid" -- /bin/bash -c "
        # Install MySQL
        apt update
        DEBIAN_FRONTEND=noninteractive apt install -y mysql-server
        
        # Secure MySQL installation
        mysql -e \"ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'SecurePass123!';\"
        mysql -u root -pSecurePass123! -e \"DELETE FROM mysql.user WHERE User='';\"
        mysql -u root -pSecurePass123! -e \"DROP DATABASE IF EXISTS test;\"
        mysql -u root -pSecurePass123! -e \"FLUSH PRIVILEGES;\"
        
        # Configure for production
        echo '[mysqld]
        bind-address = 0.0.0.0
        max_connections = 1000
        innodb_buffer_pool_size = 8G
        innodb_log_file_size = 256M
        slow_query_log = 1
        long_query_time = 2' >> /etc/mysql/mysql.conf.d/mysqld.cnf
        
        systemctl restart mysql
        ufw allow 3306
    "
    
    log_vm "Database server configuration completed on VM $vmid"
}

# VM performance optimization and NUMA configuration
optimize_vm_performance() {
    local vmid="$1"
    local workload_type="$2"  # cpu-intensive, memory-intensive, io-intensive, balanced
    
    log_vm "Optimizing VM $vmid for $workload_type workload"
    
    case "$workload_type" in
        "cpu-intensive")
            qm set "$vmid" \
                --cpu cputype=host \
                --numa 1 \
                --vcpus 1
            ;;
        "memory-intensive")
            qm set "$vmid" \
                --balloon 0 \
                --cpu cputype=host \
                --numa 1
            ;;
        "io-intensive")
            qm set "$vmid" \
                --scsi0 "local-zfs:vm-${vmid}-disk-0,cache=none,iothread=1" \
                --cpu cputype=host
            ;;
        "balanced")
            qm set "$vmid" \
                --cpu cputype=host \
                --balloon 0 \
                --numa 1
            ;;
    esac
    
    log_vm "Performance optimization completed for VM $vmid"
}

# VM inventory management
update_vm_inventory() {
    local vmid="$1"
    local vm_name="$2"
    local purpose="$3"
    local status="$4"
    
    # Initialize inventory file if it doesn't exist
    [[ ! -f "$VM_INVENTORY" ]] && echo '{"vms": []}' > "$VM_INVENTORY"
    
    # Create VM entry
    local vm_entry=$(cat << EOF
{
    "vmid": $vmid,
    "name": "$vm_name",
    "purpose": "$purpose",
    "status": "$status",
    "created": "$(date -Iseconds)",
    "last_updated": "$(date -Iseconds)"
}
EOF
)
    
    # Update inventory (simplified - in production use proper JSON manipulation)
    log_vm "Updated inventory for VM $vmid: $vm_name"
}

# Automated VM lifecycle management
manage_vm_lifecycle() {
    local action="$1"
    local vmid="$2"
    
    case "$action" in
        "start")
            qm start "$vmid"
            log_vm "Started VM $vmid"
            ;;
        "stop")
            qm shutdown "$vmid"
            log_vm "Gracefully stopped VM $vmid"
            ;;
        "restart")
            qm reboot "$vmid"
            log_vm "Restarted VM $vmid"
            ;;
        "backup")
            vzdump "$vmid" --storage backup-storage --compress gzip
            log_vm "Backup created for VM $vmid"
            ;;
        "snapshot")
            qm snapshot "$vmid" "auto-snapshot-$(date +%Y%m%d_%H%M%S)"
            log_vm "Snapshot created for VM $vmid"
            ;;
    esac
}

# Example usage and deployment scenarios
create_vm_template_config

# Example: Create Ubuntu web server template
# create_enterprise_template "ubuntu-web-template" 9020 4096 4 "40G" "vmbr0" "ubuntu-20.04.3-live-server-amd64.iso"

# Example: Mass deploy web cluster
# mass_deploy_vms "web-cluster" 9020 3 200 "10.0.202"

# Example: Deploy Kubernetes cluster
# mass_deploy_vms "kubernetes-cluster" 9023 3 300 "10.0.203"

log_vm "VM management system initialized"
```

### 12.4 LXC Container Orchestration

#### Enterprise Container Management and Automation
```bash
#!/bin/bash
# proxmox-container-manager.sh - Enterprise LXC container management

CONTAINER_LOG="/var/log/proxmox-container.log"
CONTAINER_CONFIG="/etc/pve/container-profiles.conf"

log_container() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$CONTAINER_LOG"
}

# Create container profile configuration
create_container_profiles() {
    log_container "Creating container profile configuration"
    
    cat > "$CONTAINER_CONFIG" << 'EOF'
# Container Profile Configuration
# Format: profile_name:template:memory:cores:disk:network:privileged:features

# Microservice Containers
web-service:ubuntu-20.04-standard:512:1:8G:vmbr0:0:nesting=1
api-service:ubuntu-20.04-standard:1024:2:16G:vmbr0:0:nesting=1
database-service:ubuntu-20.04-standard:2048:4:32G:vmbr0:0:nesting=1

# Development Containers
dev-environment:ubuntu-20.04-standard:2048:2:20G:vmbr0:0:nesting=1,mount=nfs
docker-dev:ubuntu-20.04-standard:4096:4:40G:vmbr0:0:nesting=1,keyctl=1

# System Services
monitoring:ubuntu-20.04-standard:1024:2:16G:vmbr0:0:nesting=1
logging:ubuntu-20.04-standard:512:1:20G:vmbr0:0:nesting=1
proxy:ubuntu-20.04-standard:512:1:8G:vmbr0:0:nesting=1

# Privileged Containers (use sparingly)
system-admin:ubuntu-20.04-standard:1024:2:16G:vmbr0:1:nesting=1,mount=nfs

EOF
    
    log_container "Container profile configuration created"
}

# Deploy container from profile
deploy_container_from_profile() {
    local profile="$1"
    local container_id="$2"
    local container_name="$3"
    local ip_config="$4"
    
    log_container "Deploying container $container_name (ID: $container_id) from profile: $profile"
    
    # Read profile configuration
    local profile_line=$(grep "^$profile:" "$CONTAINER_CONFIG")
    if [[ -z "$profile_line" ]]; then
        log_container "ERROR: Profile $profile not found"
        return 1
    fi
    
    IFS=':' read -r profile_name template memory cores disk network privileged features <<< "$profile_line"
    
    # Download template if not available
    if ! pveam list local | grep -q "$template"; then
        pveam download local "$template"
    fi
    
    # Create container
    pct create "$container_id" local:vztmpl/"$template" \
        --hostname "$container_name" \
        --memory "$memory" \
        --cores "$cores" \
        --rootfs "local-zfs:$disk" \
        --net0 "name=eth0,bridge=$network,ip=$ip_config" \
        --unprivileged "$((1 - privileged))" \
        --features "$features" \
        --onboot 1 \
        --startup order=1
    
    # Configure container post-creation
    configure_container_environment "$container_id" "$profile"
    
    # Start container
    pct start "$container_id"
    
    log_container "Container $container_name deployed and started successfully"
}

# Configure container environment based on profile
configure_container_environment() {
    local container_id="$1"
    local profile="$2"
    
    log_container "Configuring environment for container $container_id (profile: $profile)"
    
    # Wait for container to start
    while ! pct status "$container_id" | grep -q "status: running"; do
        sleep 2
    done
    
    case "$profile" in
        "web-service")
            pct exec "$container_id" -- bash -c "
                apt update && apt install -y nginx
                systemctl enable nginx
                echo 'Microservice running on container $container_id' > /var/www/html/index.html
            "
            ;;
        "api-service")
            pct exec "$container_id" -- bash -c "
                apt update && apt install -y nodejs npm
                npm install -g pm2
                useradd -m apiuser
            "
            ;;
        "database-service")
            pct exec "$container_id" -- bash -c "
                apt update && apt install -y mysql-server
                systemctl enable mysql
            "
            ;;
        "docker-dev")
            pct exec "$container_id" -- bash -c "
                apt update && apt install -y docker.io docker-compose
                systemctl enable docker
                usermod -aG docker root
            "
            ;;
        "monitoring")
            pct exec "$container_id" -- bash -c "
                apt update && apt install -y prometheus node-exporter grafana
                systemctl enable prometheus node-exporter grafana-server
            "
            ;;
    esac
    
    log_container "Container environment configuration completed for $container_id"
}

# Mass container deployment for microservices
deploy_microservice_stack() {
    local stack_name="$1"
    local base_container_id="$2"
    local network_base="$3"
    
    log_container "Deploying microservice stack: $stack_name"
    
    # Deploy web service containers
    for i in {1..3}; do
        local container_id=$((base_container_id + i))
        local ip_address="${network_base}.$((10 + i))"
        deploy_container_from_profile "web-service" "$container_id" "${stack_name}-web-${i}" "${ip_address}/24,gw=${network_base}.1"
    done
    
    # Deploy API service containers
    for i in {1..2}; do
        local container_id=$((base_container_id + 10 + i))
        local ip_address="${network_base}.$((20 + i))"
        deploy_container_from_profile "api-service" "$container_id" "${stack_name}-api-${i}" "${ip_address}/24,gw=${network_base}.1"
    done
    
    # Deploy database service
    local db_container_id=$((base_container_id + 20))
    local db_ip="${network_base}.30"
    deploy_container_from_profile "database-service" "$db_container_id" "${stack_name}-db" "${db_ip}/24,gw=${network_base}.1"
    
    # Deploy monitoring
    local monitor_container_id=$((base_container_id + 21))
    local monitor_ip="${network_base}.40"
    deploy_container_from_profile "monitoring" "$monitor_container_id" "${stack_name}-monitor" "${monitor_ip}/24,gw=${network_base}.1"
    
    log_container "Microservice stack $stack_name deployment completed"
}

# Example deployment
create_container_profiles
# deploy_microservice_stack "production" 400 "10.0.202"

log_container "Container orchestration system initialized"
```

### 12.5 High-Availability Clustering

#### Enterprise HA Cluster Setup and Management
```bash
#!/bin/bash
# proxmox-ha-cluster.sh - Enterprise HA cluster management

HA_LOG="/var/log/proxmox-ha-cluster.log"
CLUSTER_CONFIG="/etc/pve/ha-cluster.conf"

log_ha() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$HA_LOG"
}

# Initialize HA cluster
initialize_ha_cluster() {
    local cluster_name="$1"
    local cluster_network="$2"
    
    log_ha "Initializing HA cluster: $cluster_name"
    
    # Create cluster on first node
    pvecm create "$cluster_name" --ring0_addr "$cluster_network"
    
    # Configure corosync for redundancy
    cat >> /etc/pve/corosync.conf << EOF
totem {
    cluster_name: $cluster_name
    config_version: 2
    interface {
        ringnumber: 0
        bindnetaddr: $cluster_network
        mcastaddr: 239.255.1.1
        mcastport: 5405
    }
    interface {
        ringnumber: 1
        bindnetaddr: $cluster_network
        mcastaddr: 239.255.1.2
        mcastport: 5407
    }
}

quorum {
    provider: corosync_votequorum
    expected_votes: 3
    two_node: 0
}

logging {
    to_syslog: yes
    syslog_facility: daemon
}
EOF
    
    systemctl restart corosync
    systemctl restart pve-cluster
    
    log_ha "HA cluster $cluster_name initialized"
}

# Add node to existing cluster
add_cluster_node() {
    local existing_node_ip="$1"
    
    log_ha "Adding node to cluster via $existing_node_ip"
    
    # Join cluster
    pvecm add "$existing_node_ip"
    
    log_ha "Node added to cluster successfully"
}

# Configure HA resources and groups
configure_ha_resources() {
    log_ha "Configuring HA resources and groups"
    
    # Create HA groups for different service tiers
    ha-manager groupadd critical-services \
        --nodes pve-node-01:3,pve-node-02:2,pve-node-03:1 \
        --restricted 1
    
    ha-manager groupadd production-services \
        --nodes pve-node-01:2,pve-node-02:3,pve-node-03:1
    
    ha-manager groupadd development-services \
        --nodes pve-node-02:1,pve-node-03:2,pve-node-01:1
    
    # Configure HA resources
    # Critical VMs - auto-start with highest priority
    ha-manager add vm:100 \
        --state started \
        --group critical-services \
        --max_restart 3 \
        --max_relocate 3
    
    ha-manager add vm:101 \
        --state started \
        --group critical-services \
        --max_restart 3 \
        --max_relocate 3
    
    # Production VMs - conditional start
    ha-manager add vm:200 \
        --state started \
        --group production-services \
        --max_restart 2 \
        --max_relocate 2
    
    log_ha "HA resources and groups configured"
}

# Configure fencing (STONITH)
configure_fencing() {
    log_ha "Configuring fencing mechanisms"
    
    # Example: Configure IPMI fencing
    cat > /etc/pve/ha/fencing.cfg << 'EOF'
# Fencing Configuration

# IPMI-based fencing
fence_ipmilan {
    ipaddr: 10.0.100.11
    login: admin
    passwd: secure-ipmi-password
    method: cycle
}

# Network-based fencing for VMs
fence_virsh {
    uri: qemu+ssh://pve-node-01/system
    method: reboot
}

EOF
    
    # Test fencing configuration
    stonith_admin --list
    
    log_ha "Fencing configuration completed"
}

# Monitor cluster health
monitor_cluster_health() {
    log_ha "Monitoring cluster health"
    
    # Check cluster status
    local cluster_status=$(pvecm status)
    local quorum_votes=$(echo "$cluster_status" | grep "Expected votes" | awk '{print $3}')
    local total_votes=$(echo "$cluster_status" | grep "Total votes" | awk '{print $3}')
    
    if [[ "$total_votes" -lt "$((quorum_votes / 2 + 1))" ]]; then
        log_ha "ALERT: Cluster has lost quorum ($total_votes/$quorum_votes)"
    else
        log_ha "Cluster quorum is healthy ($total_votes/$quorum_votes)"
    fi
    
    # Check HA status
    ha-manager status | while read line; do
        if echo "$line" | grep -q "ERROR\|FAILED"; then
            log_ha "ALERT: HA issue detected - $line"
        fi
    done
    
    log_ha "Cluster health monitoring completed"
}

# Example usage
# initialize_ha_cluster "production-cluster" "10.0.101.0/24"
# configure_ha_resources
# configure_fencing

log_ha "HA cluster management system initialized"
```

## Lab Exercises

### Lab 1: Enterprise Proxmox Installation and Storage Architecture
**Objective**: Deploy a production-ready Proxmox VE cluster with optimized storage backend.

**Tasks**:
1. **Hardware Validation and Planning**:
   ```bash
   # Run hardware compatibility check
   ./proxmox-hardware-validator.sh
   
   # Plan storage architecture based on requirements:
   # - Database VMs: High IOPS, low latency
   # - File servers: High capacity, moderate performance
   # - Backup storage: Maximum capacity, compression
   ```

2. **Install and Configure Proxmox VE**:
   ```bash
   # Install Proxmox VE with enterprise settings
   ./install_proxmox_enterprise
   
   # Configure ZFS storage for VM workloads
   ./configure_enterprise_storage "zfs" "vmdata" "/dev/sdb /dev/sdc /dev/sdd /dev/sde"
   
   # Implement security hardening
   ./implement_security_hardening
   ```

3. **Verification**:
   ```bash
   # Verify installation
   pveversion -v
   zpool status vmdata
   pvesm status
   
   # Check security configuration
   ufw status
   systemctl status pve-firewall
   ```

### Lab 2: Advanced Networking and SDN Implementation
**Objective**: Design and implement enterprise networking with VLANs, SDN, and security zones.

**Tasks**:
1. **Configure Enterprise Network Architecture**:
   ```bash
   # Set up bonded interfaces and VLANs
   ./configure_enterprise_bridges
   
   # Implement SDN zones
   ./configure_sdn
   
   # Apply network security policies
   ./configure_network_security
   ```

2. **Quality of Service Configuration**:
   ```bash
   # Implement traffic shaping
   ./configure_network_qos
   
   # Monitor network performance
   ./monitor_network_performance
   ```

### Lab 3: VM and Container Orchestration
**Objective**: Deploy and manage enterprise VM and container infrastructure.

**Tasks**:
1. **VM Template Creation and Mass Deployment**:
   ```bash
   # Create enterprise VM templates
   ./create_enterprise_template "ubuntu-web-template" 9020 4096 4 "40G" "vmbr0" "ubuntu-20.04.iso"
   
   # Deploy web server cluster
   ./mass_deploy_vms "web-cluster" 9020 3 200 "10.0.202"
   
   # Deploy Kubernetes cluster
   ./mass_deploy_vms "kubernetes-cluster" 9023 3 300 "10.0.203"
   ```

2. **Container Microservices Deployment**:
   ```bash
   # Deploy microservice stack
   ./deploy_microservice_stack "production" 400 "10.0.202"
   
   # Verify deployments
   pct list
   qm list
   ```

### Lab 4: High-Availability Cluster Setup
**Objective**: Build a multi-node HA cluster with automated failover.

**Tasks**:
1. **Cluster Initialization and Node Addition**:
   ```bash
   # On first node
   ./initialize_ha_cluster "production-cluster" "10.0.101.0/24"
   
   # On additional nodes
   ./add_cluster_node "10.0.101.10"
   ```

2. **HA Configuration and Testing**:
   ```bash
   # Configure HA resources
   ./configure_ha_resources
   
   # Set up fencing
   ./configure_fencing
   
   # Test failover scenarios
   qm stop 100  # Test automatic restart
   systemctl stop pve-cluster  # Test node failure
   ```

### Lab 5: Backup and Disaster Recovery
**Objective**: Implement comprehensive backup strategies and test disaster recovery procedures.

**Tasks**:
1. **Backup Infrastructure Setup**:
   ```bash
   # Configure automated backups
   vzdump --all --storage backup-storage --compress gzip --mode snapshot
   
   # Set up Proxmox Backup Server integration
   pvesh create /cluster/backup --vmid all --storage pbs-storage
   ```

2. **Disaster Recovery Testing**:
   ```bash
   # Test VM restore procedures
   qmrestore /backup/vzdump-qemu-100.vma 101
   
   # Test cluster recovery scenarios
   # Simulate node failures and recovery procedures
   ```

## Best Practices

### Infrastructure Design
- **Hardware Selection**: Use enterprise-grade hardware with ECC memory and redundant components
- **Storage Planning**: Separate system, VM, and backup storage with appropriate performance characteristics
- **Network Design**: Implement redundant network paths and separate traffic types (management, storage, VM)
- **Security Implementation**: Apply defense-in-depth with firewalls, access controls, and monitoring

### Operational Excellence
- **Monitoring and Alerting**: Implement comprehensive monitoring for all cluster components
- **Backup Strategy**: Maintain multiple backup copies with regular restore testing
- **Documentation**: Keep detailed documentation of configurations, procedures, and troubleshooting guides
- **Change Management**: Use version control for configuration changes and implement testing procedures

### Performance Optimization
- **Resource Allocation**: Right-size VMs and containers based on actual usage patterns
- **Storage Optimization**: Use appropriate storage types and configurations for different workloads
- **Network Tuning**: Optimize network settings for specific traffic patterns and requirements
- **Regular Maintenance**: Perform regular updates, cleanups, and performance reviews

## Assessment Criteria

### Technical Implementation (40%)
- Correct installation and configuration of Proxmox VE cluster
- Proper storage backend selection and optimization
- Functional networking with appropriate security controls
- Successful HA configuration and failover testing

### Security and Compliance (25%)
- Implementation of security hardening measures
- Proper access control and user management
- Network segmentation and firewall configuration
- Backup encryption and secure storage practices

### Automation and Efficiency (20%)
- Use of automation scripts and templates
- Infrastructure as code implementation
- Monitoring and alerting system integration
- Efficient resource utilization and optimization

### Documentation and Procedures (15%)
- Clear installation and configuration documentation
- Troubleshooting guides and runbooks
- Disaster recovery procedures and testing results
- Performance baselines and optimization recommendations

## Next Steps

### Advanced Topics
- GPU passthrough and specialized hardware virtualization
- Multi-datacenter clustering and WAN optimization
- Integration with external storage systems (SAN, NAS)
- Advanced SDN configurations with EVPN and VXLAN

### Integration Opportunities
- **Module 13**: OpenSSH Best Practices for secure remote management
- **Module 14**: Proxmox Infrastructure Automation with Terraform and Ansible
- Container orchestration platform integration (Kubernetes, Docker Swarm)
- CI/CD pipeline integration for automated deployments

---

*This completes Module 12: Proxmox Virtual Environment. Students should now have comprehensive knowledge of enterprise virtualization infrastructure, from basic installation to advanced clustering, automation, and disaster recovery capabilities.*
pveceph mon create

# Create OSDs (Object Storage Daemons)
pveceph osd create /dev/sdb
pveceph osd create /dev/sdc

# Create Ceph pools
pveceph pool create vmdata --size 3 --min_size 2
pvesm add cephfs cephfs --monhost 10.0.0.1:6789,10.0.0.2:6789,10.0.0.3:6789

# LVM Storage Backend - Traditional but reliable
# Advantages: Mature, well-understood, good performance
pvcreate /dev/sdb /dev/sdc
vgcreate vmdata /dev/sdb /dev/sdc
pvesm add lvm vmdata --vgname vmdata --content images
```

#### Storage Performance Optimization
```bash
# ZFS performance tuning
echo 8589934592 > /sys/module/zfs/parameters/zfs_arc_max  # 8GB ARC
zfs set recordsize=64K vmdata/vm-disks  # Optimal for VMs
zfs set logbias=throughput vmdata/vm-disks
zfs set primarycache=metadata vmdata/vm-disks

# Ceph performance tuning
# /etc/ceph/ceph.conf
[osd]
osd_op_threads = 8
osd_disk_threads = 4
osd_journal_size = 10240
osd_max_write_size = 512

# LVM performance tuning
# Use dedicated SSD for LVM metadata
pvcreate --metadatasize 1G /dev/nvme0n1p1
vgcreate --physicalextentsize 32M vmdata /dev/sdb /dev/sdc /dev/nvme0n1p1
```

### Proxmox Installation and Upgrade Procedures

#### Bare-metal Installation Planning
```bash
# Check hardware compatibility
lscpu | grep -E "(vmx|svm)"  # Verify virtualization support
cat /proc/meminfo | grep MemTotal  # Check available RAM (min 2GB, recommended 8GB+)
lsblk  # Review storage devices
dmidecode -t memory | grep -E "(Size|Speed|Type)"  # Memory details

# Network planning for production
ip addr show  # Current network configuration
ip route show  # Current routing table
ethtool ens18 | grep "Link detected"  # Check link status
```

#### Installation and Initial Setup
```bash
# Download Proxmox VE ISO
wget https://enterprise.proxmox.com/iso/proxmox-ve_8.1-2.iso

# Create bootable USB (Linux)
sudo dd if=proxmox-ve_8.1-2.iso of=/dev/sdX bs=1M status=progress

# Post-installation repository configuration
# Disable enterprise repository if unlicensed
sed -i 's/^deb/#deb/' /etc/apt/sources.list.d/pve-enterprise.list

# Enable no-subscription repository
echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > \
    /etc/apt/sources.list.d/pve-no-subscription.list

# Update system
apt update && apt full-upgrade -y

# Install additional useful packages
apt install -y htop iotop iftop ncdu tree git curl wget
```

#### Network Configuration with VLANs and SDN
```bash
# Advanced network configuration with VLANs
# /etc/network/interfaces
auto lo
iface lo inet loopback

# Physical interfaces
iface eno1 inet manual
iface eno2 inet manual

# Bond for redundancy
auto bond0
iface bond0 inet manual
    bond-slaves eno1 eno2
    bond-mode 802.3ad
    bond-miimon 100
    bond-lacp-rate fast

# Management bridge
auto vmbr0
iface vmbr0 inet static
    address 192.168.1.100/24
    gateway 192.168.1.1
    bridge-ports bond0
    bridge-stp off
    bridge-fd 0

# VLAN bridges for VM isolation
auto vmbr0.100
iface vmbr0.100 inet manual
    vlan-raw-device vmbr0

auto vmbr100
iface vmbr100 inet manual
    bridge-ports vmbr0.100
    bridge-stp off
    bridge-fd 0

# Apply network configuration
systemctl restart networking

# Configure Software-Defined Networking (SDN)
# Enable SDN in datacenter configuration
pvesh set /cluster/sdn --apply 1

# Create SDN zones
pvesh create /cluster/sdn/zones --zone production --type simple
pvesh create /cluster/sdn/zones --zone dmz --type vlan --tag 100

# Create virtual networks (VNets)
pvesh create /cluster/sdn/vnets --vnet prod-net --zone production
pvesh create /cluster/sdn/vnets --vnet dmz-net --zone dmz --tag 100

# Apply SDN configuration
pvesh set /cluster/sdn --apply 1
```

### KVM Virtual Machine Management with `qm`

#### Advanced VM Creation and Configuration
```bash
# Create VM with optimal settings for different workloads
# Database server VM with NUMA optimization
qm create 100 --name db-server --memory 8192 --cores 4 --numa 1 \
    --net0 virtio,bridge=vmbr0,firewall=1 \
    --scsi0 vmdata:64,cache=writeback,discard=on,ssd=1 \
    --scsihw virtio-scsi-pci --boot order=scsi0 \
    --agent enabled=1,fstrim_cloned_disks=1

# Web server VM with ballooning memory
qm create 101 --name web-server --memory 4096 --balloon 2048 --cores 2 \
    --net0 virtio,bridge=vmbr100,tag=100 \
    --scsi0 vmdata:32,cache=writethrough \
    --ide2 local:iso/ubuntu-22.04-server-amd64.iso,media=cdrom \
    --boot order=ide2,scsi0 --agent enabled=1

# High-performance VM with CPU pinning
qm create 102 --name compute-node --memory 16384 --cores 8 \
    --cpu host,flags=+aes \
    --affinity 0,1,2,3,4,5,6,7 \
    --net0 virtio,bridge=vmbr0,queues=4 \
    --scsi0 vmdata:100,cache=none,aio=native \
    --machine type=q35 --bios ovmf

# Configure VM hardware after creation
qm set 100 --memory 16384 --cores 8
qm set 100 --net1 virtio,bridge=vmbr100,tag=200  # Add second NIC
qm set 100 --scsi1 vmdata:32  # Add additional disk
qm set 100 --args '-cpu host,+kvm_pv_eoi,+kvm_pv_unhalt'  # CPU optimization

# VM template creation and management
qm create 9000 --name ubuntu-template --memory 2048 --cores 1 \
    --net0 virtio,bridge=vmbr0 --scsi0 vmdata:32 \
    --ide2 local:iso/ubuntu-22.04-server-amd64.iso,media=cdrom

# After OS installation and configuration
qm shutdown 9000
qm template 9000  # Convert to template

# Deploy VMs from template
qm clone 9000 110 --name web01 --full --target local-zfs
qm clone 9000 111 --name web02 --full --target ceph-storage
qm clone 9000 112 --name web03 --linked  # Linked clone for faster deployment

# Mass deployment script
#!/bin/bash
for i in {201..210}; do
    qm clone 9000 $i --name "worker-$i" --full
    qm set $i --memory 4096 --cores 2
    qm set $i --ipconfig0 ip=192.168.1.$i/24,gw=192.168.1.1
    qm start $i
done
```

#### VM Performance Monitoring and Tuning
```bash
# Monitor VM performance
qm monitor 100  # Enter monitor console
info cpus       # CPU information
info memory     # Memory usage
info block      # Block device stats
info network    # Network statistics

# Performance tuning commands
qm set 100 --cpu host,flags=+aes,+avx2  # Enable CPU features
qm set 100 --numa 1  # Enable NUMA
qm set 100 --vcpus 4  # Set vCPU count different from cores

# Disk performance optimization
qm set 100 --scsi0 vmdata:64,cache=none,aio=native,discard=on
qm set 100 --scsi0 vmdata:64,iothread=1  # Enable IO thread

# Network performance optimization
qm set 100 --net0 virtio,bridge=vmbr0,queues=4,mtu=9000  # Jumbo frames

# Memory optimization
qm set 100 --balloon 2048  # Enable memory ballooning
qm set 100 --shares 1000    # CPU shares for prioritization
```

### LXC Container Management with `pct`

#### Advanced Container Creation and Configuration
```bash
# Download and list available templates
pveam update
pveam available | grep -E "(ubuntu|debian|centos)"

# Download specific templates
pveam download local ubuntu-22.04-standard_22.04-1_amd64.tar.xz
pveam download local debian-12-standard_12.0-1_amd64.tar.xz

# Create privileged container for system services
pct create 200 local:vztmpl/ubuntu-22.04-standard_22.04-1_amd64.tar.xz \
    --hostname web-container --memory 2048 --cores 2 --storage vmdata \
    --net0 name=eth0,bridge=vmbr0,ip=192.168.1.200/24,gw=192.168.1.1 \
    --ostype ubuntu --arch amd64 --onboot 1

# Create unprivileged container for security
pct create 201 local:vztmpl/ubuntu-22.04-standard_22.04-1_amd64.tar.xz \
    --hostname app-container --memory 1024 --cores 1 --storage vmdata \
    --net0 name=eth0,bridge=vmbr100,tag=100,ip=dhcp \
    --unprivileged 1 --features nesting=1

# Create container with mount points
pct create 202 local:vztmpl/debian-12-standard_12.0-1_amd64.tar.xz \
    --hostname file-server --memory 4096 --cores 2 --storage vmdata \
    --net0 name=eth0,bridge=vmbr0,ip=192.168.1.202/24,gw=192.168.1.1 \
    --mp0 /srv/data,mp=/data,backup=0 \
    --mp1 /srv/backups,mp=/backups,ro=1

# Container resource management
pct set 200 --memory 4096 --swap 1024  # Adjust memory and swap
pct set 200 --cores 4 --cpulimit 2      # Set CPU limits
pct set 200 --cpuunits 1024             # CPU weight/priority

# Container cgroup configuration
pct set 200 --cmode shell  # Console mode
pct set 200 --protection 1  # Protect from deletion
pct set 200 --startup order=1,up=30,down=60  # Startup configuration
```

#### Container Network and Storage Management
```bash
# Advanced networking for containers
pct set 200 --net0 name=eth0,bridge=vmbr0,ip=192.168.1.200/24,gw=192.168.1.1,type=veth
pct set 200 --net1 name=eth1,bridge=vmbr100,tag=100,type=veth  # Additional interface

# Configure container DNS
pct set 200 --nameserver 8.8.8.8,1.1.1.1
pct set 200 --searchdomain example.com

# Mount additional storage
pct set 200 --mp0 /mnt/data,mp=/data,size=100G,backup=0
pct set 200 --mp1 /dev/disk/by-id/ata-SSD,mp=/fast-storage,backup=0

# Container user namespace mapping for unprivileged containers
echo "root:100000:65536" >> /etc/subuid
echo "root:100000:65536" >> /etc/subgid

# Restart container for changes to take effect
pct reboot 201
```

### Backup Strategies with vzdump and Proxmox Backup Server

#### Advanced vzdump Configuration
```bash
# Create comprehensive backup with all options
vzdump 100 --storage vmdata-backups --mode snapshot --compress zstd \
    --notes "Production database backup before upgrade" \
    --protected 1 --remove 0

# Backup multiple VMs with specific retention
vzdump 100,101,102 --storage backups --mode suspend \
    --maxfiles 7 --prune-backups keep-last=7,keep-weekly=4,keep-monthly=6

# Container backup with specific options
vzdump 200 --storage backups --mode snapshot --compress gzip \
    --exclude-path /tmp --exclude-path /var/cache

# Full cluster backup script
#!/bin/bash
# cluster-backup.sh - Comprehensive backup strategy

BACKUP_STORAGE="vmdata-backups"
LOG_FILE="/var/log/cluster-backup.log"
RETENTION_POLICY="keep-last=14,keep-weekly=8,keep-monthly=12,keep-yearly=2"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

# Backup all VMs with different priorities
backup_critical_vms() {
    CRITICAL_VMS="100,101,102"  # Database, primary web, auth
    log "Starting backup of critical VMs: $CRITICAL_VMS"
    
    vzdump $CRITICAL_VMS --storage $BACKUP_STORAGE --mode snapshot \
        --compress zstd --notes "Critical systems backup" \
        --prune-backups $RETENTION_POLICY \
        --quiet 1 --mailnotification failure
}

backup_standard_vms() {
    STANDARD_VMS="110,111,112,113"  # Web servers, app servers
    log "Starting backup of standard VMs: $STANDARD_VMS"
    
    vzdump $STANDARD_VMS --storage $BACKUP_STORAGE --mode suspend \
        --compress lzo --maxfiles 7 \
        --quiet 1 --mailnotification failure
}

backup_containers() {
    CONTAINERS="200,201,202"
    log "Starting backup of containers: $CONTAINERS"
    
    vzdump $CONTAINERS --storage $BACKUP_STORAGE --mode snapshot \
        --compress gzip --maxfiles 14 \
        --exclude-path /tmp --exclude-path /var/cache \
        --quiet 1
}

# Verify backup integrity
verify_backups() {
    log "Verifying backup integrity"
    
    for backup in $(find /var/lib/vz/dump/ -name "vzdump-*.vma*" -mtime -1); do
        if vma verify "$backup" > /dev/null 2>&1; then
            log "Backup verified: $(basename $backup)"
        else
            log "ERROR: Backup verification failed: $(basename $backup)"
        fi
    done
}

# Main execution
main() {
    log "Starting cluster backup process"
    backup_critical_vms
    backup_standard_vms  
    backup_containers
    verify_backups
    log "Cluster backup process completed"
}

main "$@"

# Schedule via cron
# 0 2 * * * /usr/local/bin/cluster-backup.sh
```

#### Proxmox Backup Server Integration
```bash
# Install Proxmox Backup Server
wget https://enterprise.proxmox.com/iso/proxmox-backup-server_3.1-1.iso

# Add PBS storage to Proxmox VE cluster
pvesm add pbs pbs-storage --server 192.168.1.200 --datastore vmbackups \
    --username backup@pbs --password secret --fingerprint ABC123...

# Configure backup job to PBS
vzdump 100 --storage pbs-storage --mode snapshot --notes "Automated PBS backup"

# Advanced PBS backup with encryption
vzdump 100,101 --storage pbs-storage --mode snapshot \
    --notes "Encrypted production backup" \
    --protected 1 --prune-backups keep-last=30

# Verify PBS backups
proxmox-backup-client list --repository backup@pbs@192.168.1.200:vmbackups

# Restore from PBS
qmrestore pbs-storage:backup/vm/100/2024-01-15T10:30:00Z 110 \
    --storage vmdata --unique 1

# PBS pruning and maintenance
proxmox-backup-client prune --repository backup@pbs@192.168.1.200:vmbackups \
    --prefix vm/100/ --keep-last 14 --keep-weekly 8 --keep-monthly 6

# PBS garbage collection
proxmox-backup-client garbage-collect --repository backup@pbs@192.168.1.200:vmbackups
```

#### Disaster Recovery and Restore Procedures
```bash
# Full VM restore from backup
qmrestore /var/lib/vz/dump/vzdump-qemu-100-2024_01_15-02_30_00.vma.zst 100 \
    --storage vmdata --unique 0 --format qcow2

# Restore to different storage
qmrestore /var/lib/vz/dump/vzdump-qemu-100-2024_01_15-02_30_00.vma.zst 110 \
    --storage ceph-storage --format raw

# Container restore
pct restore 201 /var/lib/vz/dump/vzdump-lxc-200-2024_01_15-02_30_00.tar.zst \
    --storage vmdata --hostname restored-container

# Selective file restore from VM backup
# Mount backup and extract specific files
mkdir /mnt/backup-mount
vma extract /var/lib/vz/dump/vzdump-qemu-100-*.vma /mnt/backup-mount/
mount -o loop /mnt/backup-mount/disk-drive-scsi0.raw /mnt/vm-disk/
cp -a /mnt/vm-disk/etc/important-config.conf /tmp/

# Cross-cluster migration with backup
vzdump 100 --storage nfs-shared --mode suspend
# On destination cluster:
qmrestore /mnt/nfs/vzdump-qemu-100-*.vma.zst 100 --storage local-zfs

# Automated disaster recovery script
#!/bin/bash
# disaster-recovery.sh - Automated DR procedures

DR_SITE="dr-cluster.example.com"
BACKUP_LOCATION="/mnt/shared-backups"
CRITICAL_VMS="100,101,102"

restore_critical_systems() {
    echo "Starting disaster recovery procedures..."
    
    for vmid in $(echo $CRITICAL_VMS | tr ',' ' '); do
        latest_backup=$(ls -t $BACKUP_LOCATION/vzdump-qemu-$vmid-*.vma* | head -1)
        
        if [ -f "$latest_backup" ]; then
            echo "Restoring VM $vmid from $latest_backup"
            qmrestore "$latest_backup" $vmid --storage vmdata
            qm start $vmid
            
            # Wait for VM to be ready
            while ! qm status $vmid | grep -q "running"; do
                sleep 10
            done
            echo "VM $vmid restored and started"
        else
            echo "ERROR: No backup found for VM $vmid"
        fi
    done
}

restore_critical_systems
```

### High Availability Clustering with Fencing and Quorum

#### Multi-node Cluster Setup
```bash
# Initialize cluster on first node (pve-node1)
pvecm create production-cluster --ring0_addr 10.0.0.10 --ring1_addr 10.0.1.10

# Add second node (run on pve-node2)
pvecm add 10.0.0.10 --ring0_addr 10.0.0.11 --ring1_addr 10.0.1.11

# Add third node (run on pve-node3)
pvecm add 10.0.0.10 --ring0_addr 10.0.0.12 --ring1_addr 10.0.1.12

# Verify cluster status
pvecm status
pvecm nodes
corosync-quorumtool -s

# Check cluster network connectivity
pvecm mtunnel -migration_network 10.0.1.0/24
```

#### Advanced Corosync Configuration
```bash
# /etc/pve/corosync.conf - Production cluster configuration
totem {
    version: 2
    cluster_name: production-cluster
    config_version: 3
    ip_version: ipv4
    secauth: on
    transport: udpu
    clear_node_high_bit: yes
    
    # Optimize for network latency
    token: 3000
    token_retransmits_before_loss_const: 10
    join: 60
    consensus: 3600
    max_messages: 20
    
    # Dual-ring configuration for redundancy
    interface {
        ringnumber: 0
        bindnetaddr: 10.0.0.0
        mcastport: 5405
        ttl: 1
    }
    
    interface {
        ringnumber: 1
        bindnetaddr: 10.0.1.0
        mcastport: 5406
        ttl: 1
    }
}

logging {
    to_logfile: yes
    logfile: /var/log/corosync/corosync.log
    to_syslog: yes
    debug: off
    timestamp: on
    logger_subsys {
        subsys: QUORUM
        debug: off
    }
}

nodelist {
    node {
        name: pve-node1
        nodeid: 1
        quorum_votes: 1
        ring0_addr: 10.0.0.10
        ring1_addr: 10.0.1.10
    }
    node {
        name: pve-node2
        nodeid: 2
        quorum_votes: 1
        ring0_addr: 10.0.0.11
        ring1_addr: 10.0.1.11
    }
    node {
        name: pve-node3
        nodeid: 3
        quorum_votes: 1
        ring0_addr: 10.0.0.12
        ring1_addr: 10.0.1.12
    }
}

quorum {
    provider: corosync_votequorum
    expected_votes: 3
    two_node: 0
    wait_for_all: 0
}
```

#### Fencing Configuration (STONITH)
```bash
# Configure IPMI fencing for bare-metal nodes
ha-manager add fence-device ipmi-node1 --type ipmi --options "ip=192.168.0.101,username=admin,password=secret"
ha-manager add fence-device ipmi-node2 --type ipmi --options "ip=192.168.0.102,username=admin,password=secret"
ha-manager add fence-device ipmi-node3 --type ipmi --options "ip=192.168.0.103,username=admin,password=secret"

# Configure SSH fencing as backup
ha-manager add fence-device ssh-node1 --type ssh --options "ip=10.0.0.10,username=root,identity_file=/etc/pve/priv/known_hosts"

# Configure PDU (Power Distribution Unit) fencing
ha-manager add fence-device pdu-outlet1 --type pdu --options "ip=192.168.0.200,outlet=1,username=admin,password=secret"

# Test fencing devices
stonith_admin --list
stonith_admin --fence pve-node2 --confirm

# Configure fencing policies
# /etc/pve/ha/fence.cfg
fence: ipmi-node1
    type ipmi
    ip 192.168.0.101
    username admin
    password secret
    
fence: watchdog-node1
    type watchdog
    device /dev/watchdog
```

#### Quorum Management and Split-brain Prevention
```bash
# Check current quorum status
corosync-quorumtool -s
corosync-quorumtool -l  # List nodes

# Configure expected votes for maintenance
corosync-quorumtool -e 2  # Temporarily reduce expected votes

# Add QDevice for tie-breaking in even-node clusters
apt install corosync-qdevice
corosync-qdevice-tool -s

# Configure QNet for external quorum device
pvecm qdevice setup 192.168.0.254

# Emergency cluster recovery (split-brain resolution)
# On the node with majority/most recent data:
systemctl stop pve-cluster
systemctl stop corosync

# Reset cluster configuration
rm /etc/pve/corosync.conf
rm /etc/corosync/corosync.conf

# Recreate cluster
pvecm create recovery-cluster
pvecm expected 1  # Force single node operation

# Monitor cluster health
#!/bin/bash
# cluster-monitor.sh
while true; do
    echo "=== Cluster Status $(date) ==="
    pvecm status | grep -E "(Cluster|Node|Quorum)"
    echo "=== HA Resources ==="
    ha-manager status
    echo "=== Fence Devices ==="
    stonith_admin --list
    echo "========================="
    sleep 60
done
```

#### HA Resource Management
```bash
# Create HA groups with priority and fencing
pvesh create /cluster/ha/groups/database --nodes pve-node1:3,pve-node2:2,pve-node3:1 \
    --restricted 0 --nofailback 0

pvesh create /cluster/ha/groups/webservers --nodes pve-node2:2,pve-node3:2,pve-node1:1 \
    --restricted 1

# Add VMs to HA with specific policies
ha-manager add vm:100 --state started --group database --max_restart 3 --max_relocate 1
ha-manager add vm:101 --state started --group webservers --max_restart 2

# Add containers to HA
ha-manager add ct:200 --state started --group webservers

# Configure HA policies
ha-manager set vm:100 --state started --max_restart 5 --max_relocate 2

# Emergency HA operations
ha-manager set vm:100 --state disabled  # Disable HA for maintenance
ha-manager relocate vm:100 pve-node2    # Force migration
ha-manager set vm:100 --state started   # Re-enable HA

# Monitor HA status
ha-manager status
ha-manager config
watch -n 5 'ha-manager status'
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

### API Integration and Automation with Scripts and Ansible

#### Proxmox REST API Fundamentals
```bash
# Authentication and token management
# Get authentication ticket
curl -k -d "username=root@pam&password=yourpassword" \
    https://192.168.1.100:8006/api2/json/access/ticket

# Create API token for automation
pvesh create /access/users/automation@pve/token/backup --privsep=0
# Store token: PVEAPIToken=automation@pve!backup=abc123-def456-ghi789

# Using API token for authentication
curl -k -H "Authorization: PVEAPIToken=automation@pve!backup=abc123-def456-ghi789" \
    https://192.168.1.100:8006/api2/json/nodes

# Comprehensive API client script
#!/usr/bin/env python3
"""
Proxmox VE API Client for Infrastructure Automation
"""
import requests
import json
import sys
from urllib3 import disable_warnings
from urllib3.exceptions import InsecureRequestWarning

disable_warnings(InsecureRequestWarning)

class ProxmoxAPI:
    def __init__(self, host, token):
        self.host = host
        self.base_url = f"https://{host}:8006/api2/json"
        self.headers = {
            "Authorization": f"PVEAPIToken={token}",
            "Content-Type": "application/json"
        }
    
    def get(self, endpoint):
        """GET request to Proxmox API"""
        response = requests.get(f"{self.base_url}{endpoint}", 
                              headers=self.headers, verify=False)
        return response.json()
    
    def post(self, endpoint, data=None):
        """POST request to Proxmox API"""
        response = requests.post(f"{self.base_url}{endpoint}", 
                               headers=self.headers, json=data, verify=False)
        return response.json()
    
    def put(self, endpoint, data=None):
        """PUT request to Proxmox API"""
        response = requests.put(f"{self.base_url}{endpoint}", 
                              headers=self.headers, json=data, verify=False)
        return response.json()
    
    def delete(self, endpoint):
        """DELETE request to Proxmox API"""
        response = requests.delete(f"{self.base_url}{endpoint}", 
                                 headers=self.headers, verify=False)
        return response.json()

    def list_nodes(self):
        """List all cluster nodes"""
        return self.get("/nodes")["data"]
    
    def list_vms(self, node):
        """List VMs on a specific node"""
        return self.get(f"/nodes/{node}/qemu")["data"]
    
    def list_containers(self, node):
        """List containers on a specific node"""
        return self.get(f"/nodes/{node}/lxc")["data"]
    
    def create_vm(self, node, vmid, config):
        """Create a new VM"""
        return self.post(f"/nodes/{node}/qemu", {"vmid": vmid, **config})
    
    def clone_vm(self, node, vmid, newid, name, full=True):
        """Clone an existing VM"""
        data = {"newid": newid, "name": name, "full": 1 if full else 0}
        return self.post(f"/nodes/{node}/qemu/{vmid}/clone", data)
    
    def start_vm(self, node, vmid):
        """Start a VM"""
        return self.post(f"/nodes/{node}/qemu/{vmid}/status/start")
    
    def stop_vm(self, node, vmid):
        """Stop a VM"""
        return self.post(f"/nodes/{node}/qemu/{vmid}/status/stop")
    
    def migrate_vm(self, node, vmid, target_node, online=True):
        """Migrate VM to another node"""
        data = {"target": target_node, "online": 1 if online else 0}
        return self.post(f"/nodes/{node}/qemu/{vmid}/migrate", data)

# Example usage
if __name__ == "__main__":
    # Initialize API client
    pve = ProxmoxAPI("192.168.1.100", "automation@pve!backup=abc123-def456-ghi789")
    
    # List all nodes and their VMs
    nodes = pve.list_nodes()
    print("Cluster Nodes:")
    for node in nodes:
        print(f"  {node['node']}: {node['status']} (Load: {node['cpu']:.2%})")
        
        # List VMs on this node
        vms = pve.list_vms(node['node'])
        for vm in vms:
            print(f"    VM {vm['vmid']}: {vm['name']} - {vm['status']}")
```

#### Infrastructure Automation Scripts
```bash
#!/bin/bash
# mass-deployment.sh - Deploy multiple VMs from template

TEMPLATE_ID=9000
NODE="pve-node1"
STORAGE="vmdata"
NETWORK="vmbr0"

deploy_vm() {
    local vm_id=$1
    local vm_name=$2
    local memory=$3
    local cores=$4
    local ip_address=$5
    
    echo "Deploying VM $vm_id ($vm_name)..."
    
    # Clone from template
    qm clone $TEMPLATE_ID $vm_id --name $vm_name --full --target $STORAGE
    
    # Configure resources
    qm set $vm_id --memory $memory --cores $cores
    qm set $vm_id --net0 virtio,bridge=$NETWORK
    qm set $vm_id --ipconfig0 ip=$ip_address/24,gw=192.168.1.1
    
    # Start VM
    qm start $vm_id
    
    # Wait for VM to be ready
    while ! qm status $vm_id | grep -q "running"; do
        sleep 5
    done
    
    echo "VM $vm_id deployed and started successfully"
}

# Deploy web server cluster
deploy_vm 201 "web01" 4096 2 "192.168.1.201"
deploy_vm 202 "web02" 4096 2 "192.168.1.202"
deploy_vm 203 "web03" 4096 2 "192.168.1.203"

# Deploy database cluster
deploy_vm 210 "db01" 8192 4 "192.168.1.210"
deploy_vm 211 "db02" 8192 4 "192.168.1.211"

echo "All VMs deployed successfully"
```

#### Ansible Integration for Proxmox Management
```yaml
# ansible-playbook.yml - Proxmox infrastructure automation
---
- name: Proxmox Infrastructure Management
  hosts: localhost
  gather_facts: no
  vars:
    proxmox_host: "192.168.1.100"
    proxmox_user: "automation@pve"
    proxmox_token: "backup"
    proxmox_secret: "abc123-def456-ghi789"
    
  tasks:
    - name: Create web server VMs
      proxmox:
        api_host: "{{ proxmox_host }}"
        api_user: "{{ proxmox_user }}"
        api_token_id: "{{ proxmox_token }}"
        api_token_secret: "{{ proxmox_secret }}"
        node: pve-node1
        vmid: "{{ item.vmid }}"
        name: "{{ item.name }}"
        clone: ubuntu-template
        storage: vmdata
        memory: "{{ item.memory }}"
        cores: "{{ item.cores }}"
        net0: "virtio,bridge=vmbr0"
        ipconfig0: "ip={{ item.ip }}/24,gw=192.168.1.1"
        state: started
      loop:
        - { vmid: 301, name: "ansible-web01", memory: 2048, cores: 2, ip: "192.168.1.231" }
        - { vmid: 302, name: "ansible-web02", memory: 2048, cores: 2, ip: "192.168.1.232" }
        - { vmid: 303, name: "ansible-web03", memory: 2048, cores: 2, ip: "192.168.1.233" }
    
    - name: Configure HA for critical VMs
      proxmox_ha:
        api_host: "{{ proxmox_host }}"
        api_user: "{{ proxmox_user }}"
        api_token_id: "{{ proxmox_token }}"
        api_token_secret: "{{ proxmox_secret }}"
        resource: "vm:{{ item }}"
        state: started
        group: webservers
        max_restart: 3
        max_relocate: 1
      loop:
        - 301
        - 302
        - 303
    
    - name: Schedule backups for all VMs
      proxmox_backup:
        api_host: "{{ proxmox_host }}"
        api_user: "{{ proxmox_user }}"
        api_token_id: "{{ proxmox_token }}"
        api_token_secret: "{{ proxmox_secret }}"
        vmid: "{{ item }}"
        storage: vmdata-backups
        schedule: "0 2 * * *"  # Daily at 2 AM
        retention: "keep-last=7,keep-weekly=4,keep-monthly=3"
      loop:
        - 301
        - 302
        - 303
```

#### Monitoring and Alerting Integration
```python
#!/usr/bin/env python3
"""
Proxmox Monitoring and Alerting System
Integrates with Prometheus, Grafana, and PagerDuty
"""
import requests
import time
import json
from prometheus_client import Gauge, start_http_server

class ProxmoxMonitor:
    def __init__(self, host, token):
        self.api = ProxmoxAPI(host, token)
        
        # Prometheus metrics
        self.node_cpu = Gauge('proxmox_node_cpu_usage', 'Node CPU usage', ['node'])
        self.node_memory = Gauge('proxmox_node_memory_usage', 'Node memory usage', ['node'])
        self.vm_cpu = Gauge('proxmox_vm_cpu_usage', 'VM CPU usage', ['node', 'vmid', 'name'])
        self.vm_memory = Gauge('proxmox_vm_memory_usage', 'VM memory usage', ['node', 'vmid', 'name'])
        self.cluster_quorum = Gauge('proxmox_cluster_quorum', 'Cluster quorum status')
        
    def collect_metrics(self):
        """Collect metrics from Proxmox cluster"""
        nodes = self.api.list_nodes()
        
        for node in nodes:
            node_name = node['node']
            
            # Node metrics
            self.node_cpu.labels(node=node_name).set(node['cpu'])
            self.node_memory.labels(node=node_name).set(node['mem'] / node['maxmem'])
            
            # VM metrics
            vms = self.api.list_vms(node_name)
            for vm in vms:
                if vm['status'] == 'running':
                    vm_stats = self.api.get(f"/nodes/{node_name}/qemu/{vm['vmid']}/status/current")['data']
                    self.vm_cpu.labels(node=node_name, vmid=vm['vmid'], name=vm['name']).set(vm_stats.get('cpu', 0))
                    self.vm_memory.labels(node=node_name, vmid=vm['vmid'], name=vm['name']).set(vm_stats.get('mem', 0) / vm_stats.get('maxmem', 1))
        
        # Cluster quorum status
        cluster_status = self.api.get("/cluster/status")['data']
        quorum_info = next((item for item in cluster_status if item['type'] == 'quorum'), None)
        if quorum_info:
            self.cluster_quorum.set(1 if quorum_info['quorate'] else 0)
    
    def check_alerts(self):
        """Check for alert conditions"""
        alerts = []
        nodes = self.api.list_nodes()
        
        for node in nodes:
            # High CPU usage alert
            if node['cpu'] > 0.9:
                alerts.append(f"HIGH CPU: Node {node['node']} CPU usage: {node['cpu']:.1%}")
            
            # High memory usage alert
            memory_usage = node['mem'] / node['maxmem']
            if memory_usage > 0.9:
                alerts.append(f"HIGH MEMORY: Node {node['node']} memory usage: {memory_usage:.1%}")
            
            # Node offline alert
            if node['status'] != 'online':
                alerts.append(f"NODE OFFLINE: Node {node['node']} is {node['status']}")
        
        return alerts
    
    def send_alert(self, message):
        """Send alert to PagerDuty or Slack"""
        # PagerDuty integration
        pagerduty_url = "https://events.pagerduty.com/v2/enqueue"
        pagerduty_data = {
            "routing_key": "your-integration-key",
            "event_action": "trigger",
            "payload": {
                "summary": message,
                "source": "proxmox-monitor",
                "severity": "error"
            }
        }
        
        # Slack integration
        slack_webhook = "https://hooks.slack.com/services/YOUR/SLACK/WEBHOOK"
        slack_data = {
            "text": f"🚨 Proxmox Alert: {message}",
            "channel": "#infrastructure"
        }
        
        # Send alerts
        requests.post(pagerduty_url, json=pagerduty_data)
        requests.post(slack_webhook, json=slack_data)

if __name__ == "__main__":
    monitor = ProxmoxMonitor("192.168.1.100", "automation@pve!backup=abc123-def456-ghi789")
    
    # Start Prometheus metrics server
    start_http_server(8000)
    
    # Monitoring loop
    while True:
        monitor.collect_metrics()
        alerts = monitor.check_alerts()
        
        for alert in alerts:
            print(f"ALERT: {alert}")
            monitor.send_alert(alert)
        
        time.sleep(60)  # Check every minute
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

### Lab 1: Proxmox VE Installation and Storage Backend Configuration
**Objective:** Install Proxmox VE on bare-metal hosts and configure primary storage and networking

**Tasks:**
1. Perform bare-metal installation of Proxmox VE 8.x
2. Configure storage backends:
   - Set up ZFS pool with mirror configuration
   - Configure LVM thin provisioning
   - Evaluate Ceph distributed storage (if multiple nodes available)
3. Configure network bridges and VLAN support
4. Set up enterprise repository or no-subscription repository
5. Implement basic security hardening

**Deliverables:**
- Functional Proxmox VE installation with optimized storage
- Network configuration supporting VM isolation
- Documentation of storage backend performance characteristics

### Lab 2: KVM and LXC Management via CLI and GUI
**Objective:** Create, configure, and manage KVM virtual machines and LXC containers via CLI and GUI

**Tasks:**
1. Create VM templates using `qm` commands:
   - Ubuntu Server template with cloud-init
   - Windows Server template with VirtIO drivers
2. Deploy containers using `pct` commands:
   - Privileged container for system services
   - Unprivileged container for applications
3. Implement resource management and optimization:
   - Configure CPU pinning and NUMA
   - Set up memory ballooning
   - Optimize disk I/O with proper cache settings
4. Create automation scripts for mass deployment

**Deliverables:**
- Production-ready VM and container templates
- Resource optimization documentation
- Automated deployment scripts

### Lab 3: Multi-node Cluster with HA and Fencing
**Objective:** Build a multi-node Proxmox cluster with shared storage and configure HA and fencing

**Tasks:**
1. Create 3-node Proxmox cluster with dual-ring configuration
2. Configure shared storage (NFS, iSCSI, or Ceph)
3. Implement fencing mechanisms:
   - IPMI-based STONITH devices
   - Watchdog fencing as backup
4. Configure HA groups and resource policies
5. Test failover scenarios and quorum behavior
6. Implement QDevice for tie-breaking

**Deliverables:**
- Functional 3-node cluster with HA
- Documented fencing configuration
- Tested disaster recovery procedures

### Lab 4: Live Migration and Maintenance Planning
**Objective:** Perform live migrations and plan for node maintenance without downtime

**Tasks:**
1. Configure live migration prerequisites:
   - Shared storage setup
   - Network optimization for migration traffic
2. Perform various migration scenarios:
   - VM live migration between nodes
   - Container migration with minimal downtime
   - Storage migration with running VMs
3. Plan and execute node maintenance:
   - Drain node of running resources
   - Apply updates without service interruption
   - Validate cluster integrity after maintenance

**Deliverables:**
- Migration performance benchmarks
- Maintenance runbooks and procedures
- Zero-downtime maintenance demonstration

### Lab 5: Backup Strategy with vzdump and Proxmox Backup Server
**Objective:** Implement backup and restore workflows using vzdump and integrate Proxmox Backup Server

**Tasks:**
1. Design comprehensive backup strategy:
   - Critical vs. standard system classification
   - Retention policies and storage planning
2. Configure vzdump automation:
   - Scheduled backups with different compression
   - Backup verification and integrity checking
3. Deploy and integrate Proxmox Backup Server:
   - PBS installation and configuration
   - Encrypted backup implementation
   - Deduplication and incremental backup testing
4. Test disaster recovery procedures:
   - Full system restore from backup
   - Selective file recovery
   - Cross-cluster restoration

**Deliverables:**
- Automated backup system with monitoring
- Tested disaster recovery procedures
- PBS integration with deduplication metrics

### Lab 6: API Automation with Scripts and Ansible
**Objective:** Automate common tasks by invoking the Proxmox REST API from scripts or Ansible

**Tasks:**
1. Create API authentication tokens and test access
2. Develop Python automation scripts:
   - Infrastructure monitoring and alerting
   - Mass VM deployment and configuration
   - Resource usage reporting and optimization
3. Implement Ansible playbooks:
   - VM lifecycle management
   - Cluster configuration management
   - Backup job automation
4. Integrate with external monitoring systems:
   - Prometheus metrics export
   - Grafana dashboard creation
   - Alert manager configuration

**Deliverables:**
- Complete API automation toolkit
- Ansible playbooks for infrastructure management
- Monitoring and alerting system integration
- Performance dashboard and reporting system

## Assessment Criteria

Each lab will be evaluated based on:

| Criteria | Weight | Description |
|----------|---------|-------------|
| Technical Implementation | 40% | Correct configuration and functionality |
| Security Best Practices | 20% | Proper security hardening and access control |
| Documentation | 20% | Clear procedures and troubleshooting guides |
| Automation and Efficiency | 20% | Effective use of automation and optimization |

## Advanced Challenges

For additional learning, consider these advanced scenarios:

1. **Multi-datacenter Setup:** Configure WAN clustering with corosync over VPN
2. **GPU Passthrough:** Implement GPU virtualization for compute workloads
3. **Software-Defined Networking:** Deploy complex SDN with EVPN and VXLAN
4. **Container Orchestration:** Integrate with Kubernetes for container workloads
5. **Compliance Integration:** Implement LDAP/AD integration with role-based access

## Next Steps
With Proxmox VE mastered, you're ready to explore OpenSSH Best Practices in Module 13, where you'll learn to secure remote access and implement advanced SSH configurations for your infrastructure.
