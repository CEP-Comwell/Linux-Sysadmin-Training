# Module 12: Proxmox Virtual Environment

## Overview
Covers deploying, configuring, and clustering Proxmox VE for integrated virtual machine and container management. This module focuses on enterprise-grade virtualization infrastructure including storage backend selection, network configuration with SDN plugins, high-availability clustering, and comprehensive backup strategies using both vzdump and Proxmox Backup Server.

**Key Points:**
- Installing and upgrading Proxmox VE, choosing storage backends (ZFS, Ceph, LVM)
- Network setup: Linux bridges, VLANs, and SDN plugins
- Managing KVM VMs with `qm` and LXC containers with `pct`
- High-availability clustering, fencing, and quorum maintenance
- Live migration of VMs and containers between nodes
- Backup strategies using vzdump and Proxmox Backup Server

## Learning Objectives
By the end of this module, you will be able to:
1. Install Proxmox VE on bare-metal hosts and configure primary storage and networking
2. Create, configure, and manage KVM virtual machines and LXC containers via CLI and GUI
3. Build a multi-node Proxmox cluster with shared storage and configure HA and fencing
4. Perform live migrations and plan for node maintenance without downtime
5. Implement backup and restore workflows using vzdump and integrate Proxmox Backup Server
6. Automate common tasks by invoking the Proxmox REST API from scripts or Ansible

## Topics

### 12.1 Proxmox VE Installation and Storage Backend Selection
- Hardware requirements and bare-metal installation planning
- Installation methods and upgrade procedures
- Storage backend comparison and selection (ZFS, Ceph, LVM)
- Initial storage configuration and optimization
- Web interface setup and security hardening

### 12.2 Network Configuration and SDN Integration
- Linux bridge configuration and management
- VLAN setup and trunk port configuration
- Software-Defined Networking (SDN) plugins
- Network isolation and security zones
- Advanced networking with OVS and EVPN

### 12.3 KVM Virtual Machine Management with `qm`
- Creating and configuring VMs via CLI and GUI
- VM templates, cloning, and mass deployment
- Resource allocation, limits, and NUMA optimization
- Performance monitoring and tuning parameters
- VM migration strategies and troubleshooting

### 12.4 LXC Container Management with `pct`
- Understanding LXC containers vs VMs
- Container templates and creation workflows
- Resource management and cgroup configuration
- Container networking and storage mounting
- Security considerations and privilege management

### 12.5 High-Availability Clustering and Fencing
- Multi-node cluster design and implementation
- Shared storage configuration for clustering
- Corosync and pacemaker integration
- Fencing mechanisms and STONITH configuration
- Quorum maintenance and split-brain prevention

### 12.6 Live Migration and Maintenance Planning
- Live migration requirements and limitations
- Migration strategies for VMs and containers
- Node maintenance workflows without downtime
- Resource balancing and automated migration
- Troubleshooting migration failures

### 12.7 Backup Strategies and Proxmox Backup Server
- vzdump configuration and automation
- Backup storage planning and retention policies
- Proxmox Backup Server deployment and integration
- Incremental backup strategies and deduplication
- Restore procedures and disaster recovery testing

### 12.8 API Integration and Automation
- Proxmox REST API fundamentals
- Authentication and security tokens
- Scripting common tasks with Python/Bash
- Ansible integration for infrastructure automation
- Monitoring integration and custom dashboards

## Practical Examples

### Storage Backend Selection and Configuration

#### Comparing Storage Backends
```bash
# ZFS Storage Backend - Best for single-node or small clusters
# Advantages: Snapshots, compression, deduplication, data integrity
zpool create -o ashift=12 vmdata mirror /dev/sdb /dev/sdc
zfs set compression=lz4 vmdata
zfs set sync=standard vmdata  # Use 'disabled' only with UPS
pvesm add zfspool vmdata --pool vmdata --content images,rootdir

# Ceph Storage Backend - Best for large clusters with shared storage
# Advantages: Distributed, highly available, scalable
# Install Ceph on cluster nodes
pveceph install --repository no-subscription
pveceph init --network 10.0.0.0/24 --cluster-network 10.0.1.0/24

# Create Ceph monitors (run on 3+ nodes)
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
