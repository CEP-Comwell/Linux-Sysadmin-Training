# Module 11: ZFS Fundamentals

## Overview
Introduces ZFS's pooled storage model, end-to-end checksums, snapshots, and self-healing data integrity. This module covers ZFS (Zettabyte File System), a next-generation filesystem that combines traditional filesystem and volume manager functionality with revolutionary features like copy-on-write architecture, automatic data integrity verification, and advanced storage management capabilities.

## Learning Objectives
By the end of this module, you will be able to:
1. **Create, expand, and destroy ZFS pools and associated datasets/zvols** - Master ZFS pool architecture, understand vdev types, and manage storage pools with different redundancy levels and performance characteristics
2. **Automate snapshot lifecycles with scripts or cron jobs; perform rollbacks** - Implement comprehensive snapshot strategies, automate retention policies, and execute point-in-time recovery procedures
3. **Use `zfs send/receive` to replicate datasets and implement offsite backups** - Configure efficient incremental replication, implement disaster recovery solutions, and manage cross-platform data migration
4. **Configure quotas, reservations, and dataset delegation for multi-tenant use** - Implement hierarchical storage management, configure space allocation policies, and delegate administrative privileges for enterprise environments
5. **Tune ZFS parameters (recordsize, cache settings, log devices) for workload optimization** - Optimize performance through ARC/L2ARC configuration, recordsize tuning, and ZIL device placement for specific workload requirements

## Topics

### 11.1 ZFS Architecture and Copy-on-Write Fundamentals
- **Copy-on-Write (COW) architecture**: Transaction-based filesystem design and atomic operations
- **End-to-end data integrity**: Automatic checksumming, silent corruption detection, and self-healing
- **Pooled storage model**: Virtual devices (vdevs), storage pools (zpools), and dynamic allocation
- **ZFS vs traditional filesystems**: Integrated volume management and advanced feature comparison
- **Feature flags and compatibility**: OpenZFS evolution and cross-platform considerations

**🔗 Practical Examples**: [ZFS Architecture Deep Dive](#zfs-architecture-deep-dive) | [Data Integrity Verification](#data-integrity-verification)

### 11.2 Pool Management and Storage Hierarchies
- **Pool creation and expansion**: Vdev types, redundancy levels, and growth strategies
- **RAID-Z implementation**: RAIDZ, RAIDZ2, RAIDZ3 configurations and performance characteristics
- **Mirror and stripe configurations**: Performance vs redundancy trade-offs
- **Hot spares and fault tolerance**: Automatic replacement and resilver operations
- **Pool properties and tuning**: Feature flags, compression, and performance optimization

**🔗 Practical Examples**: [Pool Creation and Management](#pool-creation-and-management) | [Advanced Pool Configurations](#advanced-pool-configurations)

### 11.3 Datasets, Zvols, and Hierarchical Management
- **Dataset types**: Filesystems, volumes (zvols), and their use cases
- **Hierarchical quotas and reservations**: Space management and allocation policies
- **Dataset delegation and permissions**: Multi-tenant administration and security
- **Property inheritance**: Configuration management and policy enforcement
- **Mountpoint management**: Automatic mounting and sharing configurations

**🔗 Practical Examples**: [Dataset Hierarchy Management](#dataset-hierarchy-management) | [Multi-tenant Configuration](#multi-tenant-configuration)

### 11.4 Advanced Features: Compression, Deduplication, and Optimization
- **Compression algorithms**: LZ4, GZIP, ZSTD comparison and workload optimization
- **Deduplication strategies**: Block-level dedup, memory requirements, and performance impact
- **Recordsize tuning**: Workload-specific optimization for databases, VMs, and file servers
- **Transparent compression**: Real-time compression and space efficiency
- **Feature interaction**: Compression + deduplication synergies and trade-offs

**🔗 Practical Examples**: [Compression and Deduplication](#compression-and-deduplication) | [Recordsize Optimization](#recordsize-optimization)

### 11.5 Snapshot and Clone Workflows
- **Snapshot lifecycle management**: Automated creation, retention policies, and cleanup strategies
- **Clone operations**: Instant dataset cloning and promotion workflows
- **Rollback procedures**: Point-in-time recovery and data restoration
- **Snapshot automation**: Cron-based scheduling and enterprise-grade management
- **Space-efficient snapshots**: Copy-on-write efficiency and storage optimization

**🔗 Practical Examples**: [Automated Snapshot Management](#automated-snapshot-management) | [Clone and Rollback Operations](#clone-and-rollback-operations)

### 11.6 Replication and Performance Tuning
- **ZFS send/receive workflows**: Incremental replication and backup strategies
- **Offsite backup implementation**: Cross-platform replication and disaster recovery
- **ARC/L2ARC optimization**: Adaptive Replacement Cache tuning and SSD acceleration
- **ZIL and log devices**: Write performance optimization and consistency guarantees
- **Performance monitoring**: Workload analysis and bottleneck identification

**🔗 Practical Examples**: [Send/Receive Replication](#send-receive-replication) | [Performance Optimization](#performance-optimization)

## Practical Examples

### ZFS Installation and Setup

#### Installing ZFS (Ubuntu/Debian)
```bash
# Install ZFS utilities
sudo apt update
sudo apt install zfsutils-linux

# Load ZFS kernel module
sudo modprobe zfs

# Verify installation
zfs version
zpool version
```

#### Installing ZFS (CentOS/RHEL)
```bash
# Install ZFS repository
sudo yum install -y https://zfsonlinux.org/epel/zfs-release.el8.noarch.rpm

# Import GPG key
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux

# Install ZFS
sudo yum install -y zfs

# Load kernel module
sudo modprobe zfs
```

### Basic ZFS Pool Operations

#### Creating ZFS Pools
```bash
# Simple pool with single disk
sudo zpool create mypool /dev/sdb

# Mirror pool
sudo zpool create mypool mirror /dev/sdb /dev/sdc

# RAIDZ pool
sudo zpool create mypool raidz /dev/sdb /dev/sdc /dev/sdd

# RAIDZ2 pool with hot spare
sudo zpool create mypool raidz2 /dev/sdb /dev/sdc /dev/sdd /dev/sde \
    spare /dev/sdf

# Pool with cache and log devices
sudo zpool create mypool mirror /dev/sdb /dev/sdc \
    cache /dev/nvme0n1 \
    log /dev/nvme1n1

# List pools
zpool list

# Show pool status
zpool status mypool

# Show detailed pool information
zpool get all mypool
```

#### Pool Management Operations
```bash
# Add devices to pool
sudo zpool add mypool mirror /dev/sdd /dev/sde

# Add cache device
sudo zpool add mypool cache /dev/nvme0n1

# Add log device
sudo zpool add mypool log /dev/nvme1n1

# Remove device from pool
sudo zpool remove mypool /dev/sde

# Replace failed device
sudo zpool replace mypool /dev/sdb /dev/sdg

# Attach device to existing vdev (convert to mirror)
sudo zpool attach mypool /dev/sdb /dev/sdc

# Detach device from mirror
sudo zpool detach mypool /dev/sdc

# Scrub pool for errors
sudo zpool scrub mypool

# Export pool
sudo zpool export mypool

# Import pool
sudo zpool import mypool

# Import pool with different name
sudo zpool import mypool newpoolname
```

### ZFS Dataset Management

#### Creating and Managing Datasets
```bash
# Create filesystem dataset
sudo zfs create mypool/data

# Create dataset with properties
sudo zfs create -o compression=lz4 -o atime=off mypool/web

# Create volume (block device)
sudo zfs create -V 10G mypool/volume1

# List datasets
zfs list

# Show dataset properties
zfs get all mypool/data

# Set dataset properties
sudo zfs set compression=gzip mypool/data
sudo zfs set quota=100G mypool/web
sudo zfs set reservation=50G mypool/database

# Inherit property from parent
sudo zfs inherit compression mypool/data

# Destroy dataset
sudo zfs destroy mypool/data
```

#### Dataset Properties and Inheritance
```bash
# Common dataset properties
sudo zfs set mountpoint=/var/www mypool/web
sudo zfs set readonly=on mypool/backup
sudo zfs set exec=off mypool/data
sudo zfs set devices=off mypool/uploads

# Compression options
sudo zfs set compression=lz4 mypool/data        # Fast compression
sudo zfs set compression=gzip-9 mypool/backup   # High compression
sudo zfs set compression=zstd mypool/logs       # Balanced compression

# Deduplication (use carefully)
sudo zfs set dedup=on mypool/vms

# Show property inheritance
zfs get -s local,inherited compression mypool/data
```

### ZFS Snapshots and Clones

#### Snapshot Management
```bash
# Create snapshot
sudo zfs snapshot mypool/data@backup-$(date +%Y%m%d)

# List snapshots
zfs list -t snapshot

# Create recursive snapshot
sudo zfs snapshot -r mypool@full-backup-$(date +%Y%m%d)

# Rollback to snapshot
sudo zfs rollback mypool/data@backup-20241201

# Destroy snapshot
sudo zfs destroy mypool/data@backup-20241201

# Destroy range of snapshots
sudo zfs destroy mypool/data@backup-20241201%backup-20241210
```

#### Automated Snapshots Script
```bash
#!/bin/bash
# zfs-snapshot.sh - Automated ZFS snapshot management

DATASET="mypool/data"
SNAPSHOT_PREFIX="auto"
RETENTION_DAYS=30

# Create timestamp-based snapshot
create_snapshot() {
    local timestamp=$(date +%Y%m%d-%H%M%S)
    local snapshot_name="${DATASET}@${SNAPSHOT_PREFIX}-${timestamp}"
    
    echo "Creating snapshot: $snapshot_name"
    if sudo zfs snapshot "$snapshot_name"; then
        echo "Snapshot created successfully"
    else
        echo "Failed to create snapshot"
        exit 1
    fi
}

# Cleanup old snapshots
cleanup_snapshots() {
    echo "Cleaning up snapshots older than $RETENTION_DAYS days"
    
    # Get snapshots older than retention period
    local cutoff_date=$(date -d "$RETENTION_DAYS days ago" +%Y%m%d)
    
    zfs list -H -o name -t snapshot | grep "${DATASET}@${SNAPSHOT_PREFIX}" | while read snapshot; do
        local snap_date=$(echo "$snapshot" | sed "s/.*${SNAPSHOT_PREFIX}-\([0-9]\{8\}\).*/\1/")
        
        if [[ "$snap_date" < "$cutoff_date" ]]; then
            echo "Destroying old snapshot: $snapshot"
            sudo zfs destroy "$snapshot"
        fi
    done
}

# Main execution
main() {
    create_snapshot
    cleanup_snapshots
}

main "$@"
```

#### Clone Management
```bash
# Create clone from snapshot
sudo zfs clone mypool/data@backup-20241201 mypool/data-clone

# Promote clone (make it independent)
sudo zfs promote mypool/data-clone

# List clones
zfs list -t all | grep clone

# Show clone relationships
zfs list -o name,clones mypool/data
```

### ZFS Send/Receive for Replication

#### Basic Send/Receive
```bash
# Send snapshot to file
sudo zfs send mypool/data@backup-20241201 > /backup/data-snapshot.zfs

# Receive snapshot from file
sudo zfs receive backup-pool/data < /backup/data-snapshot.zfs

# Send over network
sudo zfs send mypool/data@backup-20241201 | \
    ssh backup-server "sudo zfs receive backup-pool/data"

# Incremental send
sudo zfs send -i mypool/data@backup-20241201 mypool/data@backup-20241202 | \
    ssh backup-server "sudo zfs receive backup-pool/data"

# Resume interrupted send
sudo zfs send -t $(sudo zfs get -H -o value receive_resume_token backup-pool/data)
```

#### Replication Script
```bash
#!/bin/bash
# zfs-replicate.sh - ZFS replication script

SOURCE_DATASET="mypool/data"
TARGET_HOST="backup-server"
TARGET_DATASET="backup-pool/data"

# Get latest snapshot
get_latest_snapshot() {
    zfs list -H -o name -t snapshot -s creation | \
        grep "^${SOURCE_DATASET}@" | tail -1
}

# Get last replicated snapshot
get_last_replicated() {
    ssh "$TARGET_HOST" "zfs list -H -o name -t snapshot -s creation" | \
        grep "^${TARGET_DATASET}@" | tail -1 | \
        sed "s|${TARGET_DATASET}@|${SOURCE_DATASET}@|"
}

# Perform replication
replicate() {
    local latest_snap=$(get_latest_snapshot)
    local last_replicated=$(get_last_replicated)
    
    if [[ -z "$latest_snap" ]]; then
        echo "No snapshots found on source"
        exit 1
    fi
    
    if [[ -z "$last_replicated" ]]; then
        # Initial replication
        echo "Performing initial replication of $latest_snap"
        sudo zfs send "$latest_snap" | \
            ssh "$TARGET_HOST" "sudo zfs receive $TARGET_DATASET"
    else
        # Incremental replication
        echo "Performing incremental replication from $last_replicated to $latest_snap"
        sudo zfs send -i "$last_replicated" "$latest_snap" | \
            ssh "$TARGET_HOST" "sudo zfs receive $TARGET_DATASET"
    fi
}

replicate
```

### ZFS Monitoring and Maintenance

#### Pool Health Monitoring
```bash
# Check pool status
zpool status -v

# Show pool I/O statistics
zpool iostat 1 5

# Show detailed pool history
zpool history mypool

# Check for pool errors
zpool status | grep -E "(DEGRADED|FAULTED|OFFLINE|errors)"

# Monitor pool events
zpool events -v

# Clear pool errors
sudo zpool clear mypool
```

#### Performance Monitoring
```bash
# ARC statistics
cat /proc/spl/kstat/zfs/arcstats

# ZFS statistics script
#!/bin/bash
echo "=== ZFS ARC Statistics ==="
awk '
/^size/ { print "ARC Size: " $3/1024/1024 " MB" }
/^c_max/ { print "ARC Max: " $3/1024/1024 " MB" }
/^hits/ { print "ARC Hits: " $3 }
/^misses/ { print "ARC Misses: " $3 }
' /proc/spl/kstat/zfs/arcstats

echo -e "\n=== Pool I/O ==="
zpool iostat -v 1 1
```

#### ZFS Tuning Parameters
```bash
# ARC tuning (add to /etc/modprobe.d/zfs.conf)
options zfs zfs_arc_max=8589934592  # 8GB max ARC
options zfs zfs_arc_min=1073741824  # 1GB min ARC

# Prefetch tuning
options zfs zfs_prefetch_disable=0

# Transaction group timeout
options zfs zfs_txg_timeout=5

# Apply changes (requires reboot or module reload)
sudo update-initramfs -u
```

## ZFS Best Practices

| Category | Best Practice |
|----------|---------------|
| Pool Design | Use RAIDZ2 for capacity, mirrors for performance |
| Dataset Organization | Create separate datasets for different workloads |
| Snapshots | Automate snapshot creation and cleanup |
| Monitoring | Regularly check pool health and errors |
| Performance | Size ARC appropriately for workload |
| Backup | Use send/receive for offsite replication |
| Maintenance | Schedule regular scrubs |

## ZFS vs Traditional Storage

| Feature | ZFS | Traditional (ext4+LVM) |
|---------|-----|------------------------|
| Data Integrity | Built-in checksumming | Depends on hardware |
| Snapshots | Copy-on-write, instant | LVM snapshots with overhead |
| Compression | Native support | File-level tools only |
| RAID | Software RAID-Z | Hardware or mdadm |
| Volume Management | Integrated | Separate LVM layer |
| Replication | Built-in send/receive | rsync or custom scripts |

## Troubleshooting Common Issues

### Pool Import Issues
```bash
# Force import pool
sudo zpool import -f mypool

# Import pool from different directory
sudo zpool import -d /dev/disk/by-id mypool

# Show importable pools
sudo zpool import

# Import read-only
sudo zpool import -o readonly=on mypool
```

### Performance Issues
```bash
# Check for fragmentation
zpool list -o fragmentation

# Monitor I/O patterns
zpool iostat -v 1

# Check ARC hit ratio
awk '/^hits/ {h=$3} /^misses/ {m=$3} END {print "Hit ratio: " h/(h+m)*100 "%"}' \
    /proc/spl/kstat/zfs/arcstats
```

### Dataset Issues
```bash
# Check dataset space usage
zfs list -o space

# Find datasets using most space
zfs list -S used

# Check for hung datasets
zfs list | grep -E "(UNAVAIL|FAULTED)"
```

## Lab Exercises
1. Create a ZFS pool with different redundancy levels
2. Implement automated snapshot management
3. Set up ZFS replication between systems
4. Configure ZFS for different workload types
5. Monitor and tune ZFS performance

## Next Steps
With ZFS fundamentals mastered, you're ready to explore Proxmox Virtual Environment in Module 12, where you'll learn to deploy and manage virtualized infrastructure using ZFS as the storage backend.
