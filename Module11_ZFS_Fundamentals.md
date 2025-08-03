# Module 11: ZFS Fundamentals

## Overview
This module introduces ZFS (Zettabyte File System), a next-generation filesystem that combines traditional filesystem and volume manager functionality. You'll learn ZFS concepts, pool management, dataset administration, and advanced features like snapshots, clones, and data protection.

## Learning Objectives
By the end of this module, you will be able to:
- Understand ZFS architecture and concepts
- Create and manage ZFS pools and datasets
- Implement ZFS snapshots and clones
- Configure ZFS data protection features
- Monitor and maintain ZFS storage systems
- Optimize ZFS performance for different workloads

## Topics

### 11.1 ZFS Architecture and Concepts
- ZFS vs traditional filesystems
- Copy-on-Write (COW) architecture
- Storage pools (zpools) and datasets
- Virtual devices (vdevs) and redundancy
- ZFS feature flags and compatibility

### 11.2 ZFS Pool Management
- Creating and destroying pools
- Pool layouts and redundancy levels
- Adding and removing devices
- Pool properties and tuning
- Pool scrubbing and resilver operations

### 11.3 ZFS Dataset Management
- Filesystems, volumes, and snapshots
- Dataset properties and inheritance
- Mountpoints and sharing
- Compression and deduplication
- Encryption and security

### 11.4 ZFS Snapshots and Clones
- Creating and managing snapshots
- Snapshot automation and retention
- Rolling back to snapshots
- Creating and using clones
- Send/receive for replication

### 11.5 ZFS Data Protection
- Checksumming and data integrity
- RAID-Z levels (RAIDZ, RAIDZ2, RAIDZ3)
- Mirror configurations
- Hot spares and fault tolerance
- Pool health monitoring

### 11.6 ZFS Performance and Tuning
- ARC (Adaptive Replacement Cache)
- L2ARC and ZIL configuration
- Performance monitoring tools
- Workload-specific optimizations
- Best practices for production

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
