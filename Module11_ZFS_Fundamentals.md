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

### ZFS Architecture Deep Dive

#### Understanding Copy-on-Write and Data Integrity
```bash
# Demonstrate ZFS copy-on-write behavior
sudo zfs create tank/demo
echo "Original data" | sudo tee /tank/demo/file1.txt

# Create snapshot to preserve original state
sudo zfs snapshot tank/demo@original

# Modify file (triggers COW)
echo "Modified data" | sudo tee -a /tank/demo/file1.txt

# Show space usage - original blocks preserved in snapshot
zfs list -o space tank/demo
zfs list -t snapshot tank/demo@original

# Verify data integrity with checksums
sudo zpool scrub tank
zpool status -v tank  # Shows checksum errors if any

# Force checksum verification
sudo dd if=/dev/zero of=/tank/demo/largefile bs=1M count=100
sudo zfs set checksum=sha256 tank/demo  # Enhanced checksumming
sync && sudo zpool scrub tank
```

#### Data Integrity Verification
```bash
# Monitor checksum verification in real-time
#!/bin/bash
# checksum-monitor.sh

while true; do
    echo "=== ZFS Integrity Status $(date) ==="
    
    # Pool-level integrity
    zpool status -x
    
    # Detailed error counts
    zpool status -v | grep -E "(errors|cksum|read|write)"
    
    # ARC statistics relevant to integrity
    awk '
    /^hash_collisions/ { print "Hash Collisions: " $3 }
    /^checksum_errors/ { print "Checksum Errors: " $3 }
    ' /proc/spl/kstat/zfs/arcstats
    
    sleep 60
done
```

### Pool Creation and Management

#### Advanced Pool Configurations
```bash
# High-performance pool with different vdev types
sudo zpool create performance-pool \
    mirror /dev/nvme0n1 /dev/nvme1n1 \
    mirror /dev/nvme2n1 /dev/nvme3n1 \
    cache /dev/nvme4n1 \
    log mirror /dev/nvme5n1 /dev/nvme6n1

# Capacity-optimized pool with RAIDZ2
sudo zpool create capacity-pool \
    raidz2 /dev/sda /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf \
    spare /dev/sdg /dev/sdh

# Mixed workload pool
sudo zpool create mixed-pool \
    raidz2 /dev/sdi /dev/sdj /dev/sdk /dev/sdl /dev/sdm \
    raidz2 /dev/sdn /dev/sdo /dev/sdp /dev/sdq /dev/sdr \
    cache /dev/nvme7n1 \
    log /dev/nvme8n1

# Show detailed pool layout
zpool status -v performance-pool
zpool list -v performance-pool

# Pool expansion strategies
sudo zpool add performance-pool mirror /dev/nvme9n1 /dev/nvme10n1
sudo zpool add capacity-pool raidz2 /dev/sds /dev/sdt /dev/sdu /dev/sdv /dev/sdw
```

#### Pool Management Operations
```bash
# Online pool expansion
sudo zpool online -e tank /dev/sdb  # Expand after growing underlying device

# Device replacement with resilver
sudo zpool replace tank /dev/sdc /dev/sdx
watch zpool status tank  # Monitor resilver progress

# Fault simulation and recovery
sudo zpool offline tank /dev/sdd  # Simulate failure
zpool status tank
sudo zpool online tank /dev/sdd   # Bring back online

# Pool-wide scrub with progress monitoring
sudo zpool scrub tank
while zpool status tank | grep -q "scrub in progress"; do
    zpool status tank | grep "scanned\|repaired\|errors"
    sleep 30
done

# Pool performance statistics
zpool iostat -v tank 5  # 5-second intervals
zpool iostat -P -v tank 1 10  # Per-vdev stats for 10 intervals
```

### Dataset Hierarchy Management

#### Comprehensive Dataset Structure
```bash
# Create hierarchical dataset structure
sudo zfs create tank/production
sudo zfs create tank/production/databases
sudo zfs create tank/production/databases/mysql
sudo zfs create tank/production/databases/postgresql
sudo zfs create tank/production/webservers
sudo zfs create tank/production/webservers/nginx
sudo zfs create tank/production/webservers/apache

sudo zfs create tank/development
sudo zfs create tank/development/databases
sudo zfs create tank/development/webservers

# Set inherited properties at hierarchy levels
sudo zfs set compression=lz4 tank/production
sudo zfs set compression=gzip tank/production/databases  # Higher compression for DB
sudo zfs set recordsize=8K tank/production/databases/mysql  # Optimized for MySQL
sudo zfs set recordsize=8K tank/production/databases/postgresql  # Optimized for PostgreSQL
sudo zfs set recordsize=128K tank/production/webservers  # Optimized for web content

# Create zvols for virtual machines
sudo zfs create -V 50G tank/production/vms/vm1
sudo zfs create -V 100G tank/production/vms/vm2
sudo zfs set volblocksize=16K tank/production/vms/vm1  # Optimized for VM storage

# Show inheritance chain
zfs get -s local,inherited compression tank/production/databases/mysql
zfs get -s local,inherited recordsize tank/production/databases/mysql
```

### Multi-tenant Configuration

#### Quotas, Reservations, and Delegation
```bash
# Configure hierarchical quotas
sudo zfs set quota=500G tank/production
sudo zfs set quota=200G tank/production/databases
sudo zfs set quota=300G tank/production/webservers
sudo zfs set quota=100G tank/development

# Set reservations for guaranteed space
sudo zfs set reservation=150G tank/production/databases/mysql
sudo zfs set reservation=50G tank/production/databases/postgresql

# Implement dataset delegation for multi-tenant management
sudo zfs allow dbadmin create,destroy,mount,snapshot tank/production/databases
sudo zfs allow webadmin create,destroy,mount,snapshot tank/production/webservers
sudo zfs allow devteam create,destroy,mount,snapshot,rollback tank/development

# Create user-specific datasets with quotas
for user in alice bob charlie; do
    sudo zfs create tank/home/$user
    sudo zfs set quota=50G tank/home/$user
    sudo zfs set canmount=on tank/home/$user
    sudo zfs set mountpoint=/home/$user tank/home/$user
    sudo chown $user:$user /home/$user
done

# Refquota for space accounting without snapshots
sudo zfs set refquota=40G tank/home/alice
sudo zfs set refquota=40G tank/home/bob
sudo zfs set refquota=40G tank/home/charlie

# Show quota and space usage
zfs list -o name,used,avail,refer,quota,refquota tank/home
zfs get -t filesystem quota,refquota,reservation tank/home
```

#### Advanced Permission Management
```bash
# Create role-based permission sets
sudo zfs allow -s @dbadmin create,destroy,snapshot,rollback,mount,share tank/production/databases
sudo zfs allow -s @webadmin create,destroy,snapshot,mount tank/production/webservers
sudo zfs allow -s @backup send tank/production

# Assign permissions to users and groups
sudo zfs allow @dbadmin tank/production/databases
sudo zfs allow @webadmin tank/production/webservers
sudo zfs allow backupuser @backup tank/production

# Show delegation permissions
zfs allow tank/production/databases
zfs allow tank/production

# Remove specific permissions
sudo zfs unallow alice snapshot tank/home/alice
sudo zfs unallow -s @dbadmin tank/production/databases
```

### Compression and Deduplication

#### Compression Strategy Implementation
```bash
# Workload-specific compression settings
sudo zfs set compression=lz4 tank/general        # Fast, good ratio
sudo zfs set compression=gzip-6 tank/backups     # High compression
sudo zfs set compression=zstd tank/databases     # Balanced performance
sudo zfs set compression=gzip-9 tank/archives    # Maximum compression

# Test compression effectiveness
sudo zfs create tank/compression-test
for algo in off lz4 gzip-1 gzip-6 gzip-9 zstd; do
    sudo zfs set compression=$algo tank/compression-test
    echo "Testing $algo compression..."
    
    # Create test data
    sudo dd if=/dev/urandom of=/tank/compression-test/random.dat bs=1M count=100
    sudo cp /var/log/messages /tank/compression-test/text.log
    sudo tar -cf /tank/compression-test/archive.tar /etc
    
    # Measure compression
    zfs get compressratio,used,logicalused tank/compression-test
    
    # Cleanup for next test
    sudo rm -f /tank/compression-test/*
done

# Show compression statistics
zfs get compressratio,compression tank
zfs list -o name,used,refer,compressratio tank
```

#### Deduplication Implementation and Monitoring
```bash
# Enable deduplication (requires significant RAM)
sudo zfs set dedup=on tank/dedup-test

# Check deduplication requirements
echo "RAM requirement estimate:"
zdb -D tank | grep "DDT-sha256"

# Monitor deduplication effectiveness
zfs get dedupratio tank/dedup-test
zpool status -D tank

# Create test data to demonstrate dedup
sudo zfs create tank/dedup-test/vm-images
for i in {1..5}; do
    sudo cp /path/to/base-image.qcow2 /tank/dedup-test/vm-images/vm$i.qcow2
done

# Show space savings
zfs list -o name,used,refer,dedupratio tank/dedup-test
```

### Recordsize Optimization

#### Workload-Specific Recordsize Tuning
```bash
# Database optimization (MySQL/PostgreSQL)
sudo zfs create tank/mysql
sudo zfs set recordsize=8K tank/mysql       # Match DB page size
sudo zfs set primarycache=metadata tank/mysql  # Reduce ARC usage for large DB

# Large file optimization (Video/Backup)
sudo zfs create tank/media
sudo zfs set recordsize=1M tank/media       # Large sequential files

# Virtual machine optimization
sudo zfs create tank/vms
sudo zfs set recordsize=64K tank/vms        # Balance for VM workloads
sudo zfs set volblocksize=16K tank/vms      # For zvols

# Small file optimization (Web content)
sudo zfs create tank/web
sudo zfs set recordsize=8K tank/web         # Small web files

# Test recordsize impact
#!/bin/bash
# recordsize-test.sh

test_recordsize() {
    local rs=$1
    local dataset="tank/test-$rs"
    
    sudo zfs create $dataset
    sudo zfs set recordsize=$rs $dataset
    
    echo "Testing recordsize $rs..."
    
    # Sequential write test
    time sudo dd if=/dev/zero of=/$dataset/seq.dat bs=1M count=1000 oflag=direct
    
    # Random write test
    time sudo fio --name=random --rw=randwrite --bs=4k --size=1G --filename=/$dataset/random.dat --direct=1
    
    # Show space usage
    zfs list -o name,used,refer $dataset
    
    sudo zfs destroy $dataset
}

for rs in 4K 8K 16K 32K 64K 128K 1M; do
    test_recordsize $rs
done
```

### Automated Snapshot Management

#### Enterprise Snapshot Automation
```bash
#!/bin/bash
# enterprise-snapshot.sh - Comprehensive snapshot management

POOL="tank"
CONFIG_FILE="/etc/zfs/snapshot-config.conf"
LOG_FILE="/var/log/zfs-snapshots.log"

# Configuration format:
# dataset:frequency:retention:prefix
# Example: tank/production/databases:hourly:168:prod-db
# tank/development:daily:30:dev

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

create_snapshot() {
    local dataset=$1
    local prefix=$2
    local timestamp=$(date +%Y%m%d-%H%M%S)
    local snapshot_name="${dataset}@${prefix}-${timestamp}"
    
    log "Creating snapshot: $snapshot_name"
    
    if sudo zfs snapshot "$snapshot_name"; then
        log "SUCCESS: Snapshot created - $snapshot_name"
        return 0
    else
        log "ERROR: Failed to create snapshot - $snapshot_name"
        return 1
    fi
}

cleanup_snapshots() {
    local dataset=$1
    local prefix=$2
    local retention_hours=$3
    
    log "Cleaning up snapshots for $dataset (retention: ${retention_hours}h)"
    
    local cutoff=$(date -d "$retention_hours hours ago" +%Y%m%d-%H%M%S)
    
    zfs list -H -o name -t snapshot | grep "^${dataset}@${prefix}-" | while read snapshot; do
        local snap_time=$(echo "$snapshot" | sed "s/.*${prefix}-\([0-9]\{8\}-[0-9]\{6\}\).*/\1/")
        
        if [[ "$snap_time" < "$cutoff" ]]; then
            log "Destroying old snapshot: $snapshot"
            if sudo zfs destroy "$snapshot"; then
                log "SUCCESS: Destroyed $snapshot"
            else
                log "ERROR: Failed to destroy $snapshot"
            fi
        fi
    done
}

process_config() {
    if [[ ! -f "$CONFIG_FILE" ]]; then
        log "ERROR: Configuration file not found: $CONFIG_FILE"
        exit 1
    fi
    
    while IFS=: read -r dataset frequency retention prefix; do
        # Skip comments and empty lines
        [[ "$dataset" =~ ^#.*$ ]] && continue
        [[ -z "$dataset" ]] && continue
        
        # Verify dataset exists
        if ! zfs list "$dataset" >/dev/null 2>&1; then
            log "WARNING: Dataset $dataset does not exist, skipping"
            continue
        fi
        
        # Create snapshot
        create_snapshot "$dataset" "$prefix"
        
        # Cleanup old snapshots
        cleanup_snapshots "$dataset" "$prefix" "$retention"
        
    done < "$CONFIG_FILE"
}

# Health check function
health_check() {
    log "Running ZFS health check..."
    
    # Check pool status
    if ! zpool status -x | grep -q "all pools are healthy"; then
        log "WARNING: Pool health issues detected"
        zpool status -x | tee -a "$LOG_FILE"
    fi
    
    # Check for snapshot errors
    local error_count=$(zfs list -t snapshot -o name 2>&1 | grep -c "error\|cannot")
    if [[ $error_count -gt 0 ]]; then
        log "WARNING: $error_count snapshot errors detected"
    fi
    
    # Check available space
    zfs list -o name,avail | awk '$2 ~ /[0-9]+G/ && $2+0 < 10 {print "WARNING: Low space on " $1 ": " $2}' | tee -a "$LOG_FILE"
}

# Main execution
main() {
    log "Starting automated snapshot management"
    health_check
    process_config
    log "Automated snapshot management completed"
}

# Run based on frequency argument
case "${1:-manual}" in
    hourly|daily|weekly|monthly)
        main
        ;;
    manual)
        main
        ;;
    *)
        echo "Usage: $0 [hourly|daily|weekly|monthly|manual]"
        exit 1
        ;;
esac
```

#### Crontab Integration
```bash
# /etc/crontab entries for automated snapshots
# Hourly snapshots for critical data
0 * * * * root /usr/local/bin/enterprise-snapshot.sh hourly

# Daily snapshots for general data
0 2 * * * root /usr/local/bin/enterprise-snapshot.sh daily

# Weekly snapshots for development
0 3 * * 0 root /usr/local/bin/enterprise-snapshot.sh weekly

# Monthly archive snapshots
0 4 1 * * root /usr/local/bin/enterprise-snapshot.sh monthly

# Configuration file example
cat > /etc/zfs/snapshot-config.conf << 'EOF'
# Dataset:Frequency:Retention(hours):Prefix
tank/production/databases:hourly:168:prod-db
tank/production/webservers:hourly:72:prod-web
tank/development:daily:720:dev
tank/backups:weekly:4320:backup
EOF
```

### Clone and Rollback Operations

#### Advanced Clone Management
```bash
# Create base snapshot for cloning
sudo zfs snapshot tank/production/template@golden-master

# Create multiple clones for testing/development
for env in test staging dev; do
    sudo zfs clone tank/production/template@golden-master tank/environments/$env
    sudo zfs set mountpoint=/opt/$env tank/environments/$env
done

# Clone with different properties
sudo zfs clone -o compression=gzip-9 -o quota=50G \
    tank/production/template@golden-master tank/environments/compressed-test

# Show clone relationships
zfs list -t all -o name,origin,clones
zfs get origin tank/environments/test

# Promote clone to become independent
sudo zfs promote tank/environments/test
# Original template can now be destroyed if desired

# Clone from remote snapshot
sudo zfs clone receiving-pool/backup@daily-20241201 receiving-pool/restore-point
```

#### Point-in-Time Recovery Procedures
```bash
#!/bin/bash
# rollback-manager.sh - Automated rollback procedures

DATASET="$1"
TARGET_SNAPSHOT="$2"
BACKUP_SNAPSHOT=""

validate_rollback() {
    local dataset="$1"
    local snapshot="$2"
    
    # Verify dataset exists
    if ! zfs list "$dataset" >/dev/null 2>&1; then
        echo "ERROR: Dataset $dataset does not exist"
        return 1
    fi
    
    # Verify snapshot exists
    if ! zfs list -t snapshot "$snapshot" >/dev/null 2>&1; then
        echo "ERROR: Snapshot $snapshot does not exist"
        return 1
    fi
    
    # Check if there are newer snapshots that will be destroyed
    local newer_snapshots=$(zfs list -H -o name -t snapshot | \
        awk -v target="$snapshot" -v dataset="$dataset" '
        $0 ~ dataset"@" && $0 > target {print}')
    
    if [[ -n "$newer_snapshots" ]]; then
        echo "WARNING: The following newer snapshots will be destroyed:"
        echo "$newer_snapshots"
        read -p "Continue? (y/N): " -n 1 -r
        echo
        if [[ ! $REPLY =~ ^[Yy]$ ]]; then
            return 1
        fi
    fi
    
    return 0
}

create_safety_snapshot() {
    local dataset="$1"
    BACKUP_SNAPSHOT="${dataset}@emergency-backup-$(date +%Y%m%d-%H%M%S)"
    
    echo "Creating safety snapshot: $BACKUP_SNAPSHOT"
    if sudo zfs snapshot "$BACKUP_SNAPSHOT"; then
        echo "Safety snapshot created successfully"
        return 0
    else
        echo "ERROR: Failed to create safety snapshot"
        return 1
    fi
}

perform_rollback() {
    local dataset="$1"
    local snapshot="$2"
    
    echo "Performing rollback of $dataset to $snapshot..."
    
    # Unmount if mounted
    if findmnt "/$dataset" >/dev/null 2>&1; then
        echo "Unmounting $dataset..."
        sudo umount "/$dataset" || {
            echo "ERROR: Failed to unmount $dataset"
            return 1
        }
    fi
    
    # Perform rollback
    if sudo zfs rollback -r "$snapshot"; then
        echo "Rollback completed successfully"
        
        # Remount if needed
        sudo zfs mount "$dataset" 2>/dev/null
        
        return 0
    else
        echo "ERROR: Rollback failed"
        return 1
    fi
}

# Main rollback procedure
main() {
    if [[ $# -ne 2 ]]; then
        echo "Usage: $0 <dataset> <snapshot>"
        echo "Example: $0 tank/production tank/production@backup-20241201"
        exit 1
    fi
    
    echo "=== ZFS Rollback Procedure ==="
    echo "Dataset: $DATASET"
    echo "Target Snapshot: $TARGET_SNAPSHOT"
    echo
    
    if validate_rollback "$DATASET" "$TARGET_SNAPSHOT" && \
       create_safety_snapshot "$DATASET" && \
       perform_rollback "$DATASET" "$TARGET_SNAPSHOT"; then
        echo "Rollback completed successfully!"
        echo "Safety snapshot available at: $BACKUP_SNAPSHOT"
    else
        echo "Rollback failed!"
        if [[ -n "$BACKUP_SNAPSHOT" ]]; then
            echo "Safety snapshot available at: $BACKUP_SNAPSHOT"
        fi
        exit 1
    fi
}

main "$@"
```

### Send/Receive Replication

#### Comprehensive Replication Strategy
```bash
#!/bin/bash
# zfs-replication-manager.sh - Enterprise replication system

SOURCE_POOL="tank"
TARGET_HOST="backup-server.example.com"
TARGET_POOL="backup"
SSH_KEY="/root/.ssh/zfs-backup"
LOG_FILE="/var/log/zfs-replication.log"

# Configuration for different replication policies
declare -A REPLICATION_CONFIG=(
    ["tank/production/databases"]="hourly:24:critical"
    ["tank/production/webservers"]="daily:7:important"
    ["tank/development"]="weekly:4:normal"
    ["tank/testing"]="monthly:3:low"
)

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

create_replication_snapshot() {
    local dataset="$1"
    local timestamp=$(date +%Y%m%d-%H%M%S)
    local snapshot="${dataset}@repl-${timestamp}"
    
    log "Creating replication snapshot: $snapshot"
    
    if sudo zfs snapshot "$snapshot"; then
        log "SUCCESS: Snapshot created - $snapshot"
        echo "$snapshot"
        return 0
    else
        log "ERROR: Failed to create snapshot - $snapshot"
        return 1
    fi
}

get_last_replicated_snapshot() {
    local dataset="$1"
    local target_dataset="${TARGET_POOL}/${dataset#*/}"
    
    ssh -i "$SSH_KEY" root@"$TARGET_HOST" \
        "zfs list -H -o name -t snapshot -s creation" 2>/dev/null | \
        grep "^${target_dataset}@repl-" | tail -1 | \
        sed "s|${target_dataset}@|${dataset}@|"
}

perform_initial_replication() {
    local dataset="$1"
    local snapshot="$2"
    local target_dataset="${TARGET_POOL}/${dataset#*/}"
    
    log "Performing initial replication: $dataset -> $target_dataset"
    
    # Create target dataset parent if needed
    local parent_dataset=$(dirname "$target_dataset")
    ssh -i "$SSH_KEY" root@"$TARGET_HOST" \
        "zfs list '$parent_dataset' >/dev/null 2>&1 || zfs create -p '$parent_dataset'"
    
    # Send initial snapshot
    if sudo zfs send "$snapshot" | \
       ssh -i "$SSH_KEY" root@"$TARGET_HOST" "zfs receive '$target_dataset'"; then
        log "SUCCESS: Initial replication completed - $snapshot"
        return 0
    else
        log "ERROR: Initial replication failed - $snapshot"
        return 1
    fi
}

perform_incremental_replication() {
    local dataset="$1"
    local last_snapshot="$2"
    local new_snapshot="$3"
    local target_dataset="${TARGET_POOL}/${dataset#*/}"
    
    log "Performing incremental replication: $last_snapshot -> $new_snapshot"
    
    if sudo zfs send -i "$last_snapshot" "$new_snapshot" | \
       ssh -i "$SSH_KEY" root@"$TARGET_HOST" "zfs receive '$target_dataset'"; then
        log "SUCCESS: Incremental replication completed - $new_snapshot"
        return 0
    else
        log "ERROR: Incremental replication failed - $new_snapshot"
        return 1
    fi
}

cleanup_old_snapshots() {
    local dataset="$1"
    local retention="$2"
    
    log "Cleaning up old replication snapshots for $dataset (retention: $retention)"
    
    # Local cleanup
    zfs list -H -o name -t snapshot | grep "^${dataset}@repl-" | \
        head -n -"$retention" | while read snapshot; do
        log "Destroying old local snapshot: $snapshot"
        sudo zfs destroy "$snapshot"
    done
    
    # Remote cleanup
    local target_dataset="${TARGET_POOL}/${dataset#*/}"
    ssh -i "$SSH_KEY" root@"$TARGET_HOST" \
        "zfs list -H -o name -t snapshot | grep '^${target_dataset}@repl-' | head -n -$retention" | \
        while read snapshot; do
            log "Destroying old remote snapshot: $snapshot"
            ssh -i "$SSH_KEY" root@"$TARGET_HOST" "zfs destroy '$snapshot'"
        done
}

replicate_dataset() {
    local dataset="$1"
    local config="$2"
    
    IFS=':' read -r frequency retention priority <<< "$config"
    
    log "Starting replication for $dataset (frequency: $frequency, retention: $retention, priority: $priority)"
    
    # Create new snapshot
    local new_snapshot
    if ! new_snapshot=$(create_replication_snapshot "$dataset"); then
        return 1
    fi
    
    # Get last replicated snapshot
    local last_snapshot=$(get_last_replicated_snapshot "$dataset")
    
    if [[ -z "$last_snapshot" ]]; then
        # Initial replication
        perform_initial_replication "$dataset" "$new_snapshot"
    else
        # Incremental replication
        perform_incremental_replication "$dataset" "$last_snapshot" "$new_snapshot"
    fi
    
    # Cleanup old snapshots
    cleanup_old_snapshots "$dataset" "$retention"
}

verify_replication() {
    local dataset="$1"
    local snapshot="$2"
    local target_dataset="${TARGET_POOL}/${dataset#*/}"
    local target_snapshot="${target_dataset}@${snapshot#*@}"
    
    log "Verifying replication: $snapshot -> $target_snapshot"
    
    # Check if target snapshot exists
    if ssh -i "$SSH_KEY" root@"$TARGET_HOST" "zfs list '$target_snapshot' >/dev/null 2>&1"; then
        log "SUCCESS: Replication verified - $target_snapshot exists"
        return 0
    else
        log "ERROR: Replication verification failed - $target_snapshot not found"
        return 1
    fi
}

# Main replication loop
main() {
    log "Starting ZFS replication cycle"
    
    # Check connectivity
    if ! ssh -i "$SSH_KEY" -o ConnectTimeout=10 root@"$TARGET_HOST" "echo 'Connection OK'" >/dev/null 2>&1; then
        log "ERROR: Cannot connect to target host $TARGET_HOST"
        exit 1
    fi
    
    # Process each dataset
    for dataset in "${!REPLICATION_CONFIG[@]}"; do
        if zfs list "$dataset" >/dev/null 2>&1; then
            replicate_dataset "$dataset" "${REPLICATION_CONFIG[$dataset]}"
        else
            log "WARNING: Dataset $dataset not found, skipping"
        fi
    done
    
    log "ZFS replication cycle completed"
}

# Command line options
case "${1:-replicate}" in
    replicate)
        main
        ;;
    verify)
        verify_replication "$2" "$3"
        ;;
    cleanup)
        cleanup_old_snapshots "$2" "$3"
        ;;
    *)
        echo "Usage: $0 [replicate|verify|cleanup]"
        exit 1
        ;;
esac
```

#### Cross-Platform Replication
```bash
# Replication to different platforms (FreeBSD, Linux, Solaris)
#!/bin/bash
# cross-platform-repl.sh

replicate_to_freebsd() {
    local dataset="$1"
    local snapshot="$2"
    local target="$3"
    
    # FreeBSD compatibility considerations
    sudo zfs send -p "$snapshot" | \
        ssh "$target" "zfs receive -F tank/linux-backup/${dataset#*/}"
}

replicate_to_solaris() {
    local dataset="$1"
    local snapshot="$2"
    local target="$3"
    
    # Solaris compatibility - may need feature flag considerations
    sudo zfs send -e "$snapshot" | \
        ssh "$target" "zfs receive tank/linux-data/${dataset#*/}"
}

# Feature flag compatibility check
check_compatibility() {
    local target="$1"
    
    echo "Checking ZFS feature compatibility with $target..."
    
    # Local features
    zpool get feature@* tank | grep active
    
    # Remote features
    ssh "$target" "zpool get feature@* tank" | grep active
}
```

### Performance Optimization

#### ARC and L2ARC Tuning
```bash
# Monitor ARC statistics
#!/bin/bash
# arc-monitor.sh - Comprehensive ARC monitoring

display_arc_stats() {
    local arc_stats="/proc/spl/kstat/zfs/arcstats"
    
    echo "=== ZFS ARC Statistics ==="
    awk '
    /^size/ { arc_size = $3 }
    /^c_max/ { arc_max = $3 }
    /^c_min/ { arc_min = $3 }
    /^hits/ { hits = $3 }
    /^misses/ { misses = $3 }
    /^demand_data_hits/ { data_hits = $3 }
    /^demand_data_misses/ { data_misses = $3 }
    /^demand_metadata_hits/ { meta_hits = $3 }
    /^demand_metadata_misses/ { meta_misses = $3 }
    /^mfu_hits/ { mfu_hits = $3 }
    /^mru_hits/ { mru_hits = $3 }
    /^l2_hits/ { l2_hits = $3 }
    /^l2_misses/ { l2_misses = $3 }
    /^l2_size/ { l2_size = $3 }
    END {
        printf "ARC Size: %.2f GB (%.1f%% of max)\n", arc_size/1024/1024/1024, (arc_size/arc_max)*100
        printf "ARC Max: %.2f GB\n", arc_max/1024/1024/1024
        printf "ARC Min: %.2f GB\n", arc_min/1024/1024/1024
        printf "Hit Ratio: %.2f%%\n", (hits/(hits+misses))*100
        printf "Data Hit Ratio: %.2f%%\n", (data_hits/(data_hits+data_misses))*100
        printf "Metadata Hit Ratio: %.2f%%\n", (meta_hits/(meta_hits+meta_misses))*100
        printf "MFU vs MRU: %.2f%% vs %.2f%%\n", (mfu_hits/(mfu_hits+mru_hits))*100, (mru_hits/(mfu_hits+mru_hits))*100
        if (l2_size > 0) {
            printf "L2ARC Size: %.2f GB\n", l2_size/1024/1024/1024
            printf "L2ARC Hit Ratio: %.2f%%\n", (l2_hits/(l2_hits+l2_misses))*100
        }
    }' "$arc_stats"
}

# ARC tuning recommendations
analyze_arc_performance() {
    local hit_ratio=$(awk '/^hits/ {h=$3} /^misses/ {m=$3} END {print (h/(h+m))*100}' /proc/spl/kstat/zfs/arcstats)
    local arc_size=$(awk '/^size/ {print $3}' /proc/spl/kstat/zfs/arcstats)
    local arc_max=$(awk '/^c_max/ {print $3}' /proc/spl/kstat/zfs/arcstats)
    
    echo "=== ARC Performance Analysis ==="
    
    if (( $(echo "$hit_ratio < 85" | bc -l) )); then
        echo "WARNING: Low ARC hit ratio ($hit_ratio%). Consider:"
        echo "  - Increasing ARC size if memory available"
        echo "  - Adding L2ARC device for larger cache"
        echo "  - Analyzing workload patterns"
    else
        echo "Good ARC hit ratio: $hit_ratio%"
    fi
    
    local arc_usage=$(echo "scale=1; $arc_size * 100 / $arc_max" | bc)
    if (( $(echo "$arc_usage < 80" | bc -l) )); then
        echo "INFO: ARC not fully utilized ($arc_usage%). Workload may not benefit from larger cache."
    fi
}

# Display and analyze
display_arc_stats
analyze_arc_performance
```

#### ZIL and Performance Optimization
```bash
# ZIL (ZFS Intent Log) optimization
configure_zil_optimization() {
    local pool="$1"
    local workload="$2"
    
    case "$workload" in
        database)
            echo "Configuring ZIL for database workload..."
            # Databases benefit from fast ZIL for transaction consistency
            sudo zfs set sync=always "$pool"
            sudo zfs set logbias=throughput "$pool"
            ;;
        vm)
            echo "Configuring ZIL for VM workload..."
            # VMs need balanced performance
            sudo zfs set sync=standard "$pool"
            sudo zfs set logbias=latency "$pool"
            ;;
        bulk)
            echo "Configuring ZIL for bulk operations..."
            # Bulk operations can trade consistency for speed
            sudo zfs set sync=disabled "$pool"  # Use with caution!
            ;;
    esac
}

# Performance testing suite
performance_test_suite() {
    local dataset="$1"
    local test_dir="/$dataset/performance-test"
    
    echo "=== ZFS Performance Test Suite ==="
    sudo mkdir -p "$test_dir"
    
    # Sequential write test
    echo "Testing sequential write performance..."
    sudo dd if=/dev/zero of="$test_dir/seq_write.dat" bs=1M count=1000 oflag=direct 2>&1 | \
        grep -E "(copied|MB/s)"
    
    # Sequential read test
    echo "Testing sequential read performance..."
    sudo dd if="$test_dir/seq_write.dat" of=/dev/null bs=1M iflag=direct 2>&1 | \
        grep -E "(copied|MB/s)"
    
    # Random I/O test with fio
    if command -v fio >/dev/null; then
        echo "Testing random I/O performance..."
        sudo fio --name=random_rw \
            --ioengine=libaio \
            --iodepth=32 \
            --rw=randrw \
            --bs=4k \
            --direct=1 \
            --size=1G \
            --numjobs=4 \
            --runtime=60 \
            --group_reporting \
            --filename="$test_dir/fio_test" | \
            grep -E "(read|write).*iops"
    fi
    
    # Cleanup
    sudo rm -rf "$test_dir"
}

# Workload-specific optimization
optimize_for_workload() {
    local dataset="$1"
    local workload="$2"
    
    case "$workload" in
        database)
            echo "Optimizing for database workload..."
            sudo zfs set recordsize=8K "$dataset"
            sudo zfs set primarycache=metadata "$dataset"
            sudo zfs set compression=lz4 "$dataset"
            sudo zfs set logbias=throughput "$dataset"
            ;;
        vm)
            echo "Optimizing for VM workload..."
            sudo zfs set recordsize=64K "$dataset"
            sudo zfs set primarycache=all "$dataset"
            sudo zfs set compression=lz4 "$dataset"
            sudo zfs set volblocksize=16K "$dataset"  # For zvols
            ;;
        media)
            echo "Optimizing for media/large files..."
            sudo zfs set recordsize=1M "$dataset"
            sudo zfs set primarycache=metadata "$dataset"
            sudo zfs set compression=off "$dataset"
            ;;
        web)
            echo "Optimizing for web server workload..."
            sudo zfs set recordsize=128K "$dataset"
            sudo zfs set compression=gzip "$dataset"
            sudo zfs set atime=off "$dataset"
            ;;
    esac
}

# System-wide ZFS tuning
tune_zfs_system() {
    local total_ram=$(free -b | awk '/^Mem:/ {print $2}')
    local arc_max=$((total_ram / 2))  # 50% of RAM for ARC
    local arc_min=$((total_ram / 8))  # 12.5% minimum
    
    cat > /etc/modprobe.d/zfs.conf << EOF
# ZFS Performance Tuning
options zfs zfs_arc_max=$arc_max
options zfs zfs_arc_min=$arc_min
options zfs zfs_prefetch_disable=0
options zfs zfs_txg_timeout=5
options zfs zfs_vdev_scheduler=deadline
options zfs zfs_top_maxinflight=32
EOF
    
    echo "ZFS tuning applied. Reboot required for full effect."
    echo "ARC Max: $(echo "scale=2; $arc_max/1024/1024/1024" | bc) GB"
    echo "ARC Min: $(echo "scale=2; $arc_min/1024/1024/1024" | bc) GB"
}
```

#### Advanced Performance Monitoring
```bash
#!/bin/bash
# zfs-performance-monitor.sh - Real-time performance monitoring

monitor_zfs_performance() {
    local interval="${1:-5}"
    local pool="${2:-tank}"
    
    echo "Monitoring ZFS performance (interval: ${interval}s, pool: $pool)"
    echo "Press Ctrl+C to stop"
    
    while true; do
        clear
        echo "=== ZFS Performance Monitor - $(date) ==="
        echo
        
        # Pool I/O statistics
        echo "Pool I/O Statistics:"
        zpool iostat -v "$pool" 1 1 | tail -n +3
        echo
        
        # ARC hit ratio
        local hit_ratio=$(awk '/^hits/ {h=$3} /^misses/ {m=$3} END {printf "%.2f", (h/(h+m))*100}' /proc/spl/kstat/zfs/arcstats)
        echo "ARC Hit Ratio: $hit_ratio%"
        
        # L2ARC statistics
        local l2_hits=$(awk '/^l2_hits/ {print $3}' /proc/spl/kstat/zfs/arcstats)
        local l2_misses=$(awk '/^l2_misses/ {print $3}' /proc/spl/kstat/zfs/arcstats)
        if [[ $((l2_hits + l2_misses)) -gt 0 ]]; then
            local l2_ratio=$(echo "scale=2; $l2_hits * 100 / ($l2_hits + $l2_misses)" | bc)
            echo "L2ARC Hit Ratio: $l2_ratio%"
        fi
        
        # Transaction Group statistics
        echo
        echo "Transaction Group Info:"
        awk '/^txg_/ {print $1 ": " $3}' /proc/spl/kstat/zfs/arcstats | head -5
        
        # Dataset space usage
        echo
        echo "Top 5 Datasets by Space Usage:"
        zfs list -o name,used,available -s used | tail -5
        
        sleep "$interval"
    done
}

# Bottleneck analysis
analyze_bottlenecks() {
    local pool="$1"
    
    echo "=== ZFS Bottleneck Analysis for $pool ==="
    
    # Check pool fragmentation
    local fragmentation=$(zpool list -o frag "$pool" | tail -1)
    echo "Pool Fragmentation: $fragmentation"
    if [[ "${fragmentation%\%}" -gt 30 ]]; then
        echo "WARNING: High fragmentation detected. Consider defragmentation."
    fi
    
    # Check ARC efficiency
    local arc_stats="/proc/spl/kstat/zfs/arcstats"
    local arc_size=$(awk '/^size/ {print $3}' "$arc_stats")
    local arc_max=$(awk '/^c_max/ {print $3}' "$arc_stats")
    local hit_ratio=$(awk '/^hits/ {h=$3} /^misses/ {m=$3} END {print (h/(h+m))*100}' "$arc_stats")
    
    echo "ARC Utilization: $(echo "scale=1; $arc_size * 100 / $arc_max" | bc)%"
    echo "ARC Hit Ratio: $hit_ratio%"
    
    if (( $(echo "$hit_ratio < 80" | bc -l) )); then
        echo "RECOMMENDATION: Consider adding L2ARC or increasing ARC size"
    fi
    
    # Check I/O patterns
    echo
    echo "I/O Pattern Analysis:"
    zpool iostat -v "$pool" 1 5 | awk '
    /^$/ {next}
    /pool/ {next}
    /^[[:space:]]*$/ {next}
    NR > 3 {
        if ($2 ~ /^[0-9]/) {
            read_ops += $2; write_ops += $3
            read_bw += $4; write_bw += $5
            count++
        }
    }
    END {
        if (count > 0) {
            printf "Average Read IOPS: %.0f\n", read_ops/count
            printf "Average Write IOPS: %.0f\n", write_ops/count
            printf "Average Read BW: %.2f MB/s\n", read_bw/count/1024/1024
            printf "Average Write BW: %.2f MB/s\n", write_bw/count/1024/1024
        }
    }'
}

# Usage examples
case "${1:-monitor}" in
    monitor)
        monitor_zfs_performance "${2:-5}" "${3:-tank}"
        ;;
    analyze)
        analyze_bottlenecks "${2:-tank}"
        ;;
    test)
        performance_test_suite "${2:-tank/test}"
        ;;
    tune)
        optimize_for_workload "${2}" "${3}"
        ;;
    *)
        echo "Usage: $0 [monitor|analyze|test|tune] [parameters...]"
        echo "  monitor [interval] [pool] - Real-time performance monitoring"
        echo "  analyze [pool] - Bottleneck analysis"
        echo "  test [dataset] - Performance testing suite"
        echo "  tune [dataset] [workload] - Workload optimization"
        ;;
esac
```

## ZFS Best Practices and Enterprise Configuration

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| **Pool Design** | Use mirrors for performance, RAIDZ2 for capacity | `zpool create perf mirror sda sdb` vs `zpool create capacity raidz2 sdc sdd sde sdf` |
| **Dataset Hierarchy** | Organize by function and delegation | `/tank/production/databases`, `/tank/development/testing` |
| **Snapshot Strategy** | Automate with retention policies | Hourly (24h), Daily (7d), Weekly (4w), Monthly (12m) |
| **Compression** | Use LZ4 by default, GZIP for archives | `zfs set compression=lz4 tank` |
| **Recordsize Tuning** | Match workload patterns | 8K (databases), 64K (VMs), 1M (media) |
| **ARC Sizing** | 50-75% of RAM for dedicated storage | `zfs_arc_max` in `/etc/modprobe.d/zfs.conf` |
| **Monitoring** | Implement comprehensive monitoring | Pool health, performance metrics, capacity alerts |
| **Replication** | Automate offsite backups | `zfs send/receive` with incremental updates |
| **Performance** | Use dedicated log and cache devices | NVMe for ZIL, SSD for L2ARC |
| **Security** | Enable encryption and delegation | `zfs create -o encryption=on`, user permissions |

## Lab Exercises

### Lab 1: ZFS Pool Architecture and Management
**Objective**: Create, expand, and destroy ZFS pools with different vdev configurations

**Tasks**:
1. Create pools with different redundancy levels (mirror, RAIDZ, RAIDZ2)
2. Add cache and log devices to improve performance
3. Simulate disk failures and perform replacements
4. Expand pools by adding new vdevs
5. Monitor pool health and performance

**Deliverables**:
- Functional pools with multiple vdev types
- Documented failure recovery procedures
- Performance comparison between configurations

### Lab 2: Automated Snapshot Lifecycle Management
**Objective**: Implement comprehensive snapshot automation with retention policies

**Tasks**:
1. Create hierarchical dataset structure with different snapshot needs
2. Develop automated snapshot scripts with configurable retention
3. Implement rollback procedures with safety mechanisms
4. Set up monitoring and alerting for snapshot failures
5. Test point-in-time recovery scenarios

**Deliverables**:
- Automated snapshot management system
- Tested rollback procedures
- Comprehensive monitoring solution

### Lab 3: ZFS Send/Receive Replication and Disaster Recovery
**Objective**: Implement offsite backup and disaster recovery using zfs send/receive

**Tasks**:
1. Configure incremental replication between systems
2. Implement cross-platform replication (Linux to FreeBSD/Solaris)
3. Create disaster recovery procedures with documented RTOs
4. Test full system restore from replicated data
5. Automate replication monitoring and error handling

**Deliverables**:
- Automated replication system
- Tested disaster recovery procedures
- Cross-platform compatibility documentation

### Lab 4: Multi-tenant ZFS Configuration
**Objective**: Configure quotas, reservations, and delegation for enterprise use

**Tasks**:
1. Create hierarchical dataset structure for multiple tenants
2. Implement quotas and reservations for capacity management
3. Configure delegation for distributed administration
4. Set up monitoring for quota utilization and violations
5. Test delegation permissions and security boundaries

**Deliverables**:
- Multi-tenant ZFS configuration
- Delegation and permission documentation
- Capacity management automation

### Lab 5: ZFS Performance Optimization and Tuning
**Objective**: Optimize ZFS performance for specific workloads

**Tasks**:
1. Benchmark different recordsize settings for various workloads
2. Configure and tune ARC/L2ARC for optimal cache performance
3. Implement ZIL optimization for write-heavy workloads
4. Compare compression algorithm performance and efficiency
5. Create workload-specific optimization profiles

**Deliverables**:
- Performance benchmarking results
- Workload-specific optimization configurations
- Comprehensive tuning documentation

## Next Steps
With ZFS fundamentals mastered, you're ready to explore Proxmox Virtual Environment in Module 12, where you'll learn to deploy and manage virtualized infrastructure using ZFS as the storage backend. Proxmox leverages ZFS's advanced features like snapshots, replication, and high performance to provide enterprise-grade virtualization with built-in backup and disaster recovery capabilities.
