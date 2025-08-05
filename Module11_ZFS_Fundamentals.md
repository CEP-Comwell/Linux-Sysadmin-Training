
# Module 11: ZFS Fundamentals

[⬅️ Main Index](#table-of-contents)  



## Table of Contents
* [Overview](#overview)
* [Learning Objectives](#learning-objectives)
* [Topics](#topics)
    * [11.1 ZFS Architecture and Copy-on-Write Fundamentals](#111-zfs-architecture-and-copy-on-write-fundamentals)
    * [11.2 Pool Management and Storage Hierarchies](#112-pool-management-and-storage-hierarchies)
    * [11.3 Datasets, Zvols, and Hierarchical Management](#113-datasets-zvols-and-hierarchical-management)
    * [11.4 Advanced Features: Compression, Deduplication, and Optimization](#114-advanced-features-compression-deduplication-and-optimization)
    * [11.5 Snapshot and Clone Management](#115-snapshot-and-clone-management)
    * [11.6 Replication and Backup Strategies](#116-replication-and-backup-strategies)
    * [11.7 Performance Tuning and Caching](#117-performance-tuning-and-caching)
    * [11.8 Monitoring and Troubleshooting](#118-monitoring-and-troubleshooting)
* [Essential Command Reference](#essential-command-reference)
* [Practical Examples](#practical-examples)
    * [Pool Creation and Management](#pool-creation-and-management)
    * [Dataset Operations](#dataset-operations)
    * [Snapshot Management](#snapshot-management)
    * [Replication Setup](#replication-setup)
    * [Performance Optimization](#performance-optimization)
    * [Monitoring and Diagnostics](#monitoring-and-diagnostics)
* [Lab Exercises](#lab-exercises)
    * [Lab 1: ZFS Pool Architecture and Management](#lab-1-zfs-pool-architecture-and-management)
    * [Lab 2: Advanced Dataset and Snapshot Operations](#lab-2-advanced-dataset-and-snapshot-operations)
    * [Lab 3: Replication and Backup Implementation](#lab-3-replication-and-backup-implementation)
    * [Lab 4: Performance Optimization and Tuning](#lab-4-performance-optimization-and-tuning)
    * [Lab 5: Enterprise ZFS Infrastructure](#lab-5-enterprise-zfs-infrastructure)
* [Best Practices](#best-practices)
* [Troubleshooting](#troubleshooting)
* [Assessment Criteria](#assessment-criteria)
* [Next Steps](#next-steps)

[⬆️ Back to Top](#module-11-zfs-fundamentals)

## Overview
This module provides comprehensive coverage of ZFS (Zettabyte File System), a revolutionary storage platform that combines traditional filesystem and volume manager functionality with advanced features including copy-on-write architecture, automatic data integrity verification, and enterprise-grade storage management capabilities. Students will master ZFS implementation from basic pool creation to advanced replication and performance optimization strategies.

**Key Learning Outcomes:**
- Design and implement ZFS storage pools with appropriate redundancy and performance characteristics
- Master snapshot and clone management for backup, development, and testing workflows
- Configure automated replication and disaster recovery solutions using zfs send/receive
- Optimize ZFS performance through compression, caching, and workload-specific tuning
- Implement enterprise-grade monitoring, troubleshooting, and maintenance procedures
- Deploy multi-tenant ZFS environments with delegation and quota management

## Learning Objectives
By the end of this module, you will be able to:

1. **Master ZFS Architecture**: Understand copy-on-write fundamentals, pooled storage concepts, and end-to-end data integrity mechanisms
2. **Design Storage Pools**: Create and manage ZFS pools with appropriate vdev configurations, redundancy levels, and performance characteristics
3. **Manage Datasets and Zvols**: Implement hierarchical dataset structures with quotas, reservations, and delegation for multi-tenant environments
4. **Implement Snapshot Strategies**: Design automated snapshot lifecycles with retention policies and efficient rollback procedures
5. **Configure Replication**: Set up zfs send/receive replication for disaster recovery and cross-site data synchronization
6. **Optimize Performance**: Tune ZFS parameters including compression, caching, and recordsize for specific workload requirements

## Topics

### 11.1 ZFS Architecture and Copy-on-Write Fundamentals
- Copy-on-Write (COW) transaction model and atomic operations
- End-to-end data integrity with automatic checksumming and self-healing
- Pooled storage architecture with virtual devices (vdevs) and dynamic allocation
- ZFS vs traditional filesystems: integrated volume management advantages
- Feature flags, compatibility matrices, and OpenZFS ecosystem
- Memory requirements and system architecture considerations

### 11.2 Pool Management and Storage Hierarchies
- Pool creation strategies and vdev type selection (stripe, mirror, raidz)
- RAID-Z implementation: RAIDZ1, RAIDZ2, RAIDZ3 trade-offs and recommendations
- Pool expansion techniques: adding vdevs and replacing devices
- Hot spare configuration and automatic resilver operations
- Pool properties: feature flags, compression algorithms, and performance settings
- Pool import/export procedures and cross-platform compatibility

### 11.3 Datasets, Zvols, and Hierarchical Management
- Dataset types: filesystems, volumes (zvols), and snapshots
- Hierarchical namespace management and property inheritance
- Quota and reservation implementation for space management
- Dataset delegation and administrative privilege distribution
- Mountpoint management: automatic mounting and sharing protocols
- Property management: local vs inherited settings and policy enforcement

### 11.4 Advanced Features: Compression, Deduplication, and Optimization
- Compression algorithm selection: LZ4, GZIP, ZSTD performance and efficiency analysis
- Deduplication implementation: block-level dedup, memory overhead, and performance impact
- Recordsize optimization for different workloads: databases, VMs, and file servers
- Transparent encryption with native ZFS encryption features
- Feature interaction optimization: compression + deduplication synergies

### 11.5 Snapshot and Clone Management
- Snapshot creation, management, and automated retention policies
- Clone creation and management for development and testing environments
- Incremental snapshot strategies and space-efficient storage
- Snapshot-based backup workflows and point-in-time recovery
- Scripted snapshot management with lifecycle automation
- Performance considerations for high-frequency snapshot environments

### 11.6 Replication and Backup Strategies
- ZFS send/receive fundamentals: full and incremental streams
- Cross-platform replication and disaster recovery implementation
- Automated replication scripting with error handling and monitoring
- Bandwidth optimization and compression for remote replication
- Multi-site replication topologies and failover procedures
- Integration with backup software and enterprise backup workflows

### 11.7 Performance Tuning and Caching
- ARC (Adaptive Replacement Cache) tuning and memory allocation
- L2ARC (Level 2 ARC) implementation with SSD cache devices
- ZIL (ZFS Intent Log) optimization with dedicated log devices
- Recordsize tuning for workload-specific performance optimization
- Compression algorithm selection for performance vs efficiency balance
- System-level tuning: kernel parameters and hardware optimization

### 11.8 Monitoring and Troubleshooting
- ZFS health monitoring and error detection systems
- Performance monitoring tools and metrics analysis
- Troubleshooting common ZFS issues and error conditions
- Pool scrubbing strategies and integrity verification
- Disaster recovery procedures and data reconstruction techniques
- Capacity planning and growth prediction methodologies

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

## Essential Command Reference

### Pool Management

| Command | Description | Example |
|---------|-------------|---------|
| `zpool create` | Create new ZFS pool | `zpool create tank raidz /dev/sdb /dev/sdc /dev/sdd` |
| `zpool status` | Show pool status and health | `zpool status tank` |
| `zpool list` | List all pools with space usage | `zpool list` |
| `zpool add` | Add vdev to existing pool | `zpool add tank cache /dev/sde` |
| `zpool remove` | Remove vdev from pool | `zpool remove tank /dev/sde` |
| `zpool replace` | Replace failed device | `zpool replace tank /dev/sdb /dev/sdf` |
| `zpool scrub` | Start pool scrub operation | `zpool scrub tank` |
| `zpool export` | Export pool for migration | `zpool export tank` |
| `zpool import` | Import existing pool | `zpool import tank` |

### Dataset and Filesystem Operations

| Command | Description | Example |
|---------|-------------|---------|
| `zfs create` | Create dataset or zvol | `zfs create tank/data` |
| `zfs destroy` | Destroy dataset | `zfs destroy tank/data` |
| `zfs list` | List datasets with properties | `zfs list -o name,used,avail` |
| `zfs mount` | Mount dataset | `zfs mount tank/data` |
| `zfs umount` | Unmount dataset | `zfs umount tank/data` |
| `zfs set` | Set dataset property | `zfs set compression=lz4 tank/data` |
| `zfs get` | Get dataset properties | `zfs get all tank/data` |
| `zfs inherit` | Inherit property from parent | `zfs inherit compression tank/data` |

### Snapshot and Clone Management

| Command | Description | Example |
|---------|-------------|---------|
| `zfs snapshot` | Create snapshot | `zfs snapshot tank/data@backup-2025-08-02` |
| `zfs destroy` | Destroy snapshot | `zfs destroy tank/data@backup-2025-08-02` |
| `zfs rollback` | Rollback to snapshot | `zfs rollback tank/data@backup-2025-08-02` |
| `zfs clone` | Create clone from snapshot | `zfs clone tank/data@snap tank/clone` |
| `zfs promote` | Promote clone to dataset | `zfs promote tank/clone` |
| `zfs diff` | Show differences between snapshots | `zfs diff tank/data@snap1 tank/data@snap2` |

### Replication and Backup

| Command | Description | Example |
|---------|-------------|---------|
| `zfs send` | Send snapshot stream | `zfs send tank/data@snap1 > backup.zfs` |
| `zfs receive` | Receive snapshot stream | `zfs receive tank/restore < backup.zfs` |
| `zfs send -i` | Incremental send | `zfs send -i @snap1 tank/data@snap2` |
| `zfs send -R` | Recursive send with all snapshots | `zfs send -R tank/data@snap` |
| `zfs bookmark` | Create bookmark for incremental sends | `zfs bookmark tank/data@snap tank/data#mark1` |

### Quota and Reservation Management

| Command | Description | Example |
|---------|-------------|---------|
| `zfs set quota` | Set space quota | `zfs set quota=10G tank/data` |
| `zfs set reservation` | Set space reservation | `zfs set reservation=5G tank/data` |
| `zfs set refquota` | Set quota excluding snapshots | `zfs set refquota=8G tank/data` |
| `zfs set refreservation` | Set reservation excluding snapshots | `zfs set refreservation=3G tank/data` |
| `zfs userspace` | Show user space usage | `zfs userspace tank/data` |
| `zfs groupspace` | Show group space usage | `zfs groupspace tank/data` |

### Delegation and Security

| Command | Description | Example |
|---------|-------------|---------|
| `zfs allow` | Delegate ZFS permissions | `zfs allow user1 snapshot,mount tank/data` |
| `zfs unallow` | Remove delegated permissions | `zfs unallow user1 tank/data` |
| `zfs set sharenfs` | Enable NFS sharing | `zfs set sharenfs=on tank/data` |
| `zfs set sharesmb` | Enable SMB sharing | `zfs set sharesmb=on tank/data` |

### Performance and Monitoring

| Command | Description | Example |
|---------|-------------|---------|
| `zpool iostat` | Show pool I/O statistics | `zpool iostat tank 1` |
| `zfs get compressratio` | Show compression ratio | `zfs get compressratio tank/data` |
| `zpool history` | Show pool command history | `zpool history tank` |
| `zpool events` | Show pool events | `zpool events tank` |
| `arc_summary` | Show ARC statistics | `arc_summary` |

## Practical Examples

### Pool Creation and Management

#### Enterprise Pool Architecture Design
```bash
#!/bin/bash
# enterprise-zfs-setup.sh - Enterprise ZFS pool configuration

ZFS_LOG="/var/log/zfs-operations.log"

log_zfs_operation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$ZFS_LOG"
}

# Create enterprise storage pools with different performance characteristics
create_enterprise_pools() {
    log_zfs_operation "Starting enterprise ZFS pool creation"
    
    # High-performance pool for databases (RAID-10 equivalent)
    log_zfs_operation "Creating high-performance database pool"
    sudo zpool create db-pool \
        mirror /dev/sdb /dev/sdc \
        mirror /dev/sdd /dev/sde \
        -o ashift=12 \
        -o autoexpand=on \
        -O compression=lz4 \
        -O recordsize=8K \
        -O primarycache=metadata \
        -O logbias=throughput \
        -O sync=disabled
    
    # Add dedicated ZIL device for synchronous writes
    sudo zpool add db-pool log /dev/nvme0n1p1
    
    # Add L2ARC cache device
    sudo zpool add db-pool cache /dev/nvme0n1p2
    
    # Balanced pool for general storage (RAID-Z2)
    log_zfs_operation "Creating balanced general storage pool"
    sudo zpool create storage-pool \
        raidz2 /dev/sdf /dev/sdg /dev/sdh /dev/sdi /dev/sdj /dev/sdk \
        -o ashift=12 \
        -o autoexpand=on \
        -O compression=zstd \
        -O recordsize=128K \
        -O atime=off \
        -O xattr=sa \
        -O dnodesize=auto
    
    # Backup pool for long-term retention (RAID-Z3)
    log_zfs_operation "Creating backup retention pool"
    sudo zpool create backup-pool \
        raidz3 /dev/sdl /dev/sdm /dev/sdn /dev/sdo /dev/sdp /dev/sdq /dev/sdr /dev/sds \
        -o ashift=12 \
        -o autoexpand=on \
        -O compression=zstd-19 \
        -O recordsize=1M \
        -O atime=off \
        -O dedup=on
    
    # Configure hot spares
    sudo zpool add db-pool spare /dev/sdt
    sudo zpool add storage-pool spare /dev/sdu /dev/sdv
    sudo zpool add backup-pool spare /dev/sdw /dev/sdx
    
    # Display pool configurations
    log_zfs_operation "Pool creation completed successfully"
    zpool status
    zpool list -v
}

# Advanced pool management and monitoring
manage_pool_health() {
    local pool_name="$1"
    
    log_zfs_operation "Starting health management for pool: $pool_name"
    
    # Check pool health
    local pool_health=$(zpool list -H -o health "$pool_name")
    log_zfs_operation "Pool $pool_name health status: $pool_health"
    
    case "$pool_health" in
        "ONLINE")
            log_zfs_operation "Pool $pool_name is healthy"
            ;;
        "DEGRADED")
            log_zfs_operation "WARNING: Pool $pool_name is degraded"
            send_alert "ZFS Pool Degraded" "Pool $pool_name is in degraded state"
            ;;
        "FAULTED"|"UNAVAIL")
            log_zfs_operation "CRITICAL: Pool $pool_name is faulted"
            send_alert "ZFS Pool Critical" "Pool $pool_name is faulted or unavailable"
            ;;
    esac
    
    # Check for resilver operations
    if zpool status "$pool_name" | grep -q "resilver"; then
        local resilver_progress=$(zpool status "$pool_name" | grep "resilver" | awk '{print $5}')
        log_zfs_operation "Resilver in progress for $pool_name: $resilver_progress"
    fi
    
    # Check for scrub operations
    if zpool status "$pool_name" | grep -q "scrub in progress"; then
        local scrub_progress=$(zpool status "$pool_name" | grep "scanned" | awk '{print $8}')
        log_zfs_operation "Scrub in progress for $pool_name: $scrub_progress"
    fi
    
    # Monitor pool capacity
    local pool_capacity=$(zpool list -H -o capacity "$pool_name" | tr -d '%')
    if [[ "$pool_capacity" -gt 80 ]]; then
        log_zfs_operation "WARNING: Pool $pool_name is $pool_capacity% full"
        send_alert "ZFS Pool Capacity Warning" "Pool $pool_name is $pool_capacity% full"
    fi
}

# Automated pool expansion
expand_pool_capacity() {
    local pool_name="$1"
    local new_devices=("${@:2}")
    
    log_zfs_operation "Expanding pool $pool_name with devices: ${new_devices[*]}"
    
    # Get current pool configuration
    local pool_config=$(zpool status "$pool_name" | grep -E "(mirror|raidz)")
    
    if echo "$pool_config" | grep -q "mirror"; then
        # Add mirror vdev
        sudo zpool add "$pool_name" mirror "${new_devices[@]}"
        log_zfs_operation "Added mirror vdev to pool $pool_name"
    elif echo "$pool_config" | grep -q "raidz"; then
        # Add raidz vdev (matching existing configuration)
        local raidz_type=$(echo "$pool_config" | grep -o "raidz[0-9]*" | head -1)
        sudo zpool add "$pool_name" "$raidz_type" "${new_devices[@]}"
        log_zfs_operation "Added $raidz_type vdev to pool $pool_name"
    else
        # Add stripe vdev
        sudo zpool add "$pool_name" "${new_devices[@]}"
        log_zfs_operation "Added stripe vdev to pool $pool_name"
    fi
    
    # Verify expansion
    zpool list -v "$pool_name"
    log_zfs_operation "Pool expansion completed for $pool_name"
}

# Performance optimization based on workload
optimize_pool_performance() {
    local pool_name="$1"
    local workload_type="$2"  # database, fileserver, backup, vm
    
    log_zfs_operation "Optimizing pool $pool_name for $workload_type workload"
    
    case "$workload_type" in
        "database")
            # Database optimizations: small recordsize, metadata caching
            sudo zfs set recordsize=8K "$pool_name"
            sudo zfs set primarycache=metadata "$pool_name"
            sudo zfs set logbias=throughput "$pool_name"
            sudo zfs set sync=disabled "$pool_name"  # Only for non-critical data
            log_zfs_operation "Applied database optimizations to $pool_name"
            ;;
        "fileserver")
            # File server optimizations: balanced settings
            sudo zfs set recordsize=128K "$pool_name"
            sudo zfs set compression=lz4 "$pool_name"
            sudo zfs set atime=off "$pool_name"
            sudo zfs set xattr=sa "$pool_name"
            log_zfs_operation "Applied file server optimizations to $pool_name"
            ;;
        "backup")
            # Backup optimizations: maximum compression
            sudo zfs set recordsize=1M "$pool_name"
            sudo zfs set compression=zstd-19 "$pool_name"
            sudo zfs set dedup=on "$pool_name"
            sudo zfs set atime=off "$pool_name"
            log_zfs_operation "Applied backup optimizations to $pool_name"
            ;;
        "vm")
            # Virtual machine optimizations: zvol settings
            sudo zfs set recordsize=64K "$pool_name"
            sudo zfs set compression=lz4 "$pool_name"
            sudo zfs set sync=always "$pool_name"
            sudo zfs set volblocksize=16K "$pool_name"  # For new zvols
            log_zfs_operation "Applied VM optimizations to $pool_name"
            ;;
    esac
    
    # Display current settings
    zfs get recordsize,compression,primarycache,logbias,sync "$pool_name"
}

# Execute enterprise setup
create_enterprise_pools

# Monitor all pools
for pool in $(zpool list -H -o name); do
    manage_pool_health "$pool"
done

# Optimize pools based on intended use
optimize_pool_performance "db-pool" "database"
optimize_pool_performance "storage-pool" "fileserver"
optimize_pool_performance "backup-pool" "backup"

log_zfs_operation "Enterprise ZFS setup completed successfully"
```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Pool Management and Performance. 🔗

#### Pool Import/Export and Migration
```bash
#!/bin/bash
# zfs-migration.sh - ZFS pool migration and disaster recovery

# Safe pool export for migration
export_pool_safely() {
    local pool_name="$1"
    local export_reason="$2"
    
    echo "Preparing to export pool: $pool_name"
    echo "Reason: $export_reason"
    
    # Verify pool health before export
    if ! zpool status "$pool_name" | grep -q "state: ONLINE"; then
        echo "ERROR: Pool $pool_name is not in ONLINE state"
        zpool status "$pool_name"
        return 1
    fi
    
    # Ensure all datasets are unmounted
    echo "Unmounting all datasets in pool $pool_name..."
    zfs list -H -o name -r "$pool_name" | while read dataset; do
        if zfs get -H mounted "$dataset" | grep -q "yes"; then
            echo "Unmounting: $dataset"
            sudo zfs unmount "$dataset" || echo "Warning: Failed to unmount $dataset"
        fi
    done
    
    # Create export backup information
    echo "Creating export documentation..."
    zpool status "$pool_name" > "/tmp/${pool_name}_export_status.txt"
    zpool history "$pool_name" > "/tmp/${pool_name}_export_history.txt"
    zfs list -r "$pool_name" > "/tmp/${pool_name}_export_datasets.txt"
    
    # Export the pool
    echo "Exporting pool $pool_name..."
    sudo zpool export "$pool_name"
    
    if [[ $? -eq 0 ]]; then
        echo "Pool $pool_name exported successfully"
        echo "Export documentation saved to /tmp/${pool_name}_export_*"
    else
        echo "ERROR: Failed to export pool $pool_name"
        return 1
    fi
}

# Import pool with verification
import_pool_safely() {
    local pool_name="$1"
    local import_directory="$2"
    local new_pool_name="$3"
    
    echo "Importing ZFS pool: $pool_name"
    
    # Scan for importable pools
    echo "Scanning for importable pools..."
    if [[ -n "$import_directory" ]]; then
        sudo zpool import -d "$import_directory"
    else
        sudo zpool import
    fi
    
    # Import the pool
    if [[ -n "$new_pool_name" ]]; then
        echo "Importing $pool_name as $new_pool_name..."
        sudo zpool import "$pool_name" "$new_pool_name"
    else
        echo "Importing $pool_name..."
        sudo zpool import "$pool_name"
    fi
    
    if [[ $? -eq 0 ]]; then
        local imported_name="${new_pool_name:-$pool_name}"
        echo "Pool imported successfully as: $imported_name"
        
        # Verify import
        zpool status "$imported_name"
        zfs list -r "$imported_name"
        
        # Check and fix any mount issues
        echo "Checking dataset mount points..."
        zfs mount -a
        
    else
        echo "ERROR: Failed to import pool $pool_name"
        return 1
    fi
}

# Cross-platform pool migration
migrate_pool_cross_platform() {
    local source_pool="$1"
    local target_system="$2"
    local migration_method="$3"  # export-import, send-receive
    
    case "$migration_method" in
        "export-import")
            echo "Using export-import method for migration"
            export_pool_safely "$source_pool" "Cross-platform migration"
            
            # Instructions for target system
            cat << EOF > "/tmp/${source_pool}_migration_instructions.txt"
Migration Instructions for $source_pool
=====================================

1. Copy the physical drives to the target system
2. On the target system, run:
   sudo zpool import $source_pool

3. If pool name conflicts exist:
   sudo zpool import $source_pool new-pool-name

4. Verify all datasets mounted correctly:
   zfs mount -a
   zfs list -r $source_pool

5. Test pool functionality before going live
EOF
            echo "Migration instructions created: /tmp/${source_pool}_migration_instructions.txt"
            ;;
            
        "send-receive")
            echo "Using send-receive method for migration"
            # This method requires the target system to already have a ZFS pool
            echo "Creating migration snapshots..."
            
            # Create consistent snapshots
            zfs list -H -o name -t filesystem -r "$source_pool" | while read dataset; do
                snapshot_name="${dataset}@migration-$(date +%Y%m%d_%H%M%S)"
                echo "Creating snapshot: $snapshot_name"
                sudo zfs snapshot "$snapshot_name"
            done
            
            # Generate send commands for each dataset
            echo "Creating send-receive script..."
            cat > "/tmp/${source_pool}_send_script.sh" << 'EOF'
#!/bin/bash
# Generated migration script - run on source system

TARGET_HOST="$1"
TARGET_POOL="$2"

if [[ -z "$TARGET_HOST" ]] || [[ -z "$TARGET_POOL" ]]; then
    echo "Usage: $0 <target-host> <target-pool>"
    exit 1
fi

EOF
            
            zfs list -H -o name -t filesystem -r "$source_pool" | while read dataset; do
                snapshot=$(zfs list -H -o name -t snapshot -s creation "$dataset" | tail -1)
                echo "sudo zfs send $snapshot | ssh $TARGET_HOST sudo zfs receive $TARGET_POOL/$(basename $dataset)" >> "/tmp/${source_pool}_send_script.sh"
            done
            
            chmod +x "/tmp/${source_pool}_send_script.sh"
            echo "Send script created: /tmp/${source_pool}_send_script.sh"
            ;;
    esac
}

# Example usage
# export_pool_safely "storage-pool" "Hardware maintenance"
# import_pool_safely "storage-pool"
# migrate_pool_cross_platform "old-pool" "new-server.example.com" "send-receive"
```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Pool Management and Replication. 🔗

### Dataset Operations

#### Hierarchical Dataset Management
```bash
#!/bin/bash
# zfs-dataset-management.sh - Enterprise dataset hierarchy management

DATASET_LOG="/var/log/zfs-datasets.log"

log_dataset_operation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$DATASET_LOG"
}

# Create comprehensive dataset hierarchy for enterprise use
create_enterprise_hierarchy() {
    local pool_name="$1"
    
    log_dataset_operation "Creating enterprise dataset hierarchy for pool: $pool_name"
    
    # Root organizational datasets
    sudo zfs create "$pool_name/corporate"
    sudo zfs create "$pool_name/projects"
    sudo zfs create "$pool_name/users"
    sudo zfs create "$pool_name/shared"
    sudo zfs create "$pool_name/backups"
    
    # Corporate datasets with different retention policies
    sudo zfs create "$pool_name/corporate/finance"
    sudo zfs create "$pool_name/corporate/hr"
    sudo zfs create "$pool_name/corporate/legal"
    sudo zfs create "$pool_name/corporate/it"
    
    # Project-based datasets
    sudo zfs create "$pool_name/projects/development"
    sudo zfs create "$pool_name/projects/testing"
    sudo zfs create "$pool_name/projects/production"
    sudo zfs create "$pool_name/projects/archive"
    
    # User home directories
    sudo zfs create "$pool_name/users/homes"
    sudo zfs create "$pool_name/users/profiles"
    sudo zfs create "$pool_name/users/temp"
    
    # Shared resources
    sudo zfs create "$pool_name/shared/software"
    sudo zfs create "$pool_name/shared/templates"
    sudo zfs create "$pool_name/shared/public"
    
    # Backup categories
    sudo zfs create "$pool_name/backups/daily"
    sudo zfs create "$pool_name/backups/weekly"
    sudo zfs create "$pool_name/backups/monthly"
    sudo zfs create "$pool_name/backups/archive"
    
    log_dataset_operation "Enterprise hierarchy created successfully"
}

# Configure dataset properties based on business requirements
configure_dataset_policies() {
    local pool_name="$1"
    
    log_dataset_operation "Configuring dataset policies for pool: $pool_name"
    
    # Finance: High security, compliance retention
    sudo zfs set recordsize=32K "$pool_name/corporate/finance"
    sudo zfs set compression=zstd "$pool_name/corporate/finance"
    sudo zfs set copies=2 "$pool_name/corporate/finance"
    sudo zfs set atime=on "$pool_name/corporate/finance"  # Compliance requirement
    sudo zfs set quota=500G "$pool_name/corporate/finance"
    sudo zfs set encryption=on "$pool_name/corporate/finance" 2>/dev/null || true
    
    # Development: Fast access, frequent snapshots
    sudo zfs set recordsize=128K "$pool_name/projects/development"
    sudo zfs set compression=lz4 "$pool_name/projects/development"
    sudo zfs set atime=off "$pool_name/projects/development"
    sudo zfs set quota=2T "$pool_name/projects/development"
    sudo zfs set com.sun:auto-snapshot=true "$pool_name/projects/development"
    
    # Production: Balanced performance and reliability
    sudo zfs set recordsize=64K "$pool_name/projects/production"
    sudo zfs set compression=lz4 "$pool_name/projects/production"
    sudo zfs set copies=2 "$pool_name/projects/production"
    sudo zfs set sync=standard "$pool_name/projects/production"
    sudo zfs set quota=5T "$pool_name/projects/production"
    
    # User homes: Individual quotas, personal snapshots
    sudo zfs set recordsize=128K "$pool_name/users/homes"
    sudo zfs set compression=lz4 "$pool_name/users/homes"
    sudo zfs set atime=off "$pool_name/users/homes"
    sudo zfs set quota=10T "$pool_name/users/homes"  # Total for all users
    
    # Temp: Fast access, automatic cleanup
    sudo zfs set recordsize=64K "$pool_name/users/temp"
    sudo zfs set compression=lz4 "$pool_name/users/temp"
    sudo zfs set atime=off "$pool_name/users/temp"
    sudo zfs set quota=500G "$pool_name/users/temp"
    sudo zfs set com.sun:auto-snapshot=false "$pool_name/users/temp"
    
    # Backups: Maximum compression, no access time
    sudo zfs set recordsize=1M "$pool_name/backups"
    sudo zfs set compression=zstd-19 "$pool_name/backups"
    sudo zfs set atime=off "$pool_name/backups"
    sudo zfs set readonly=on "$pool_name/backups" 2>/dev/null || true
    
    log_dataset_operation "Dataset policies configured successfully"
}

# Create individual user datasets with quotas
create_user_datasets() {
    local pool_name="$1"
    local users_file="$2"  # File containing username:quota pairs
    
    log_dataset_operation "Creating user datasets from file: $users_file"
    
    while IFS=':' read -r username quota; do
        # Skip comments and empty lines
        [[ "$username" =~ ^#.*$ ]] && continue
        [[ -z "$username" ]] && continue
        
        local user_dataset="$pool_name/users/homes/$username"
        
        # Create user dataset
        sudo zfs create "$user_dataset"
        
        # Set user-specific properties
        sudo zfs set quota="$quota" "$user_dataset"
        sudo zfs set compression=lz4 "$user_dataset"
        sudo zfs set atime=off "$user_dataset"
        
        # Set mount point and permissions
        sudo zfs set mountpoint="/home/$username" "$user_dataset"
        
        # Create user if doesn't exist
        if ! id "$username" &>/dev/null; then
            sudo useradd -m -d "/home/$username" "$username"
        fi
        
        # Set ownership
        sudo chown "$username:$username" "/home/$username"
        sudo chmod 750 "/home/$username"
        
        log_dataset_operation "Created user dataset for $username with quota $quota"
        
    done < "$user_file"
}

# Implement dataset delegation for departmental administration
setup_dataset_delegation() {
    local pool_name="$1"
    
    log_dataset_operation "Setting up dataset delegation for pool: $pool_name"
    
    # Finance department delegation
    sudo zfs allow finance_admin snapshot,mount,create,destroy "$pool_name/corporate/finance"
    sudo zfs allow finance_users mount "$pool_name/corporate/finance"
    
    # Development team delegation
    sudo zfs allow dev_lead snapshot,rollback,mount,create,destroy "$pool_name/projects/development"
    sudo zfs allow developers snapshot,mount "$pool_name/projects/development"
    
    # IT team gets broader permissions
    sudo zfs allow it_admin snapshot,rollback,mount,create,destroy,send,receive "$pool_name/corporate/it"
    sudo zfs allow it_admin snapshot,mount "$pool_name/users"
    
    # HR delegation with restricted permissions
    sudo zfs allow hr_admin snapshot,mount "$pool_name/corporate/hr"
    
    log_dataset_operation "Dataset delegation configured successfully"
}

# Monitor dataset usage and send alerts
monitor_dataset_usage() {
    local pool_name="$1"
    local alert_threshold="$2"  # Percentage
    
    log_dataset_operation "Monitoring dataset usage for pool: $pool_name (threshold: $alert_threshold%)"
    
    # Check each dataset with quota
    zfs list -H -o name,quota,used -r "$pool_name" | while IFS=$'\t' read -r dataset quota used; do
        # Skip datasets without quotas
        [[ "$quota" == "-" ]] && continue
        
        # Convert to bytes for calculation
        local quota_bytes=$(echo "$quota" | numfmt --from=iec)
        local used_bytes=$(echo "$used" | numfmt --from=iec)
        
        if [[ $quota_bytes -gt 0 ]]; then
            local usage_percent=$(( (used_bytes * 100) / quota_bytes ))
            
            if [[ $usage_percent -ge $alert_threshold ]]; then
                log_dataset_operation "ALERT: Dataset $dataset at $usage_percent% capacity ($used / $quota)"
                
                # Send notification (implement your notification method)
                echo "Dataset Usage Alert: $dataset is $usage_percent% full" | \
                    mail -s "ZFS Quota Alert" admin@company.com 2>/dev/null || true
            fi
        fi
    done
}

# Example usage files
cat > /tmp/users_quota.txt << 'EOF'
# username:quota
alice:50G
bob:100G
charlie:25G
development_shared:500G
EOF

# Execute dataset management workflow
POOL_NAME="corporate-pool"

create_enterprise_hierarchy "$POOL_NAME"
configure_dataset_policies "$POOL_NAME"
create_user_datasets "$POOL_NAME" "/tmp/users_quota.txt"
setup_dataset_delegation "$POOL_NAME"

# Start monitoring
monitor_dataset_usage "$POOL_NAME" 80

log_dataset_operation "Enterprise dataset management setup completed"
```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Dataset and Filesystem Operations, Delegation, and Quota Management. 🔗

### Snapshot Management

#### Automated Snapshot Lifecycle Management
```bash
#!/bin/bash
# zfs-snapshot-manager.sh - Enterprise snapshot lifecycle management

SNAPSHOT_LOG="/var/log/zfs-snapshots.log"
SNAPSHOT_CONFIG="/etc/zfs/snapshot-policies.conf"

log_snapshot_operation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$SNAPSHOT_LOG"
}

# Create snapshot policy configuration
create_snapshot_policies() {
    log_snapshot_operation "Creating snapshot policy configuration"
    
    sudo mkdir -p "$(dirname "$SNAPSHOT_CONFIG")"
    cat > "$SNAPSHOT_CONFIG" << 'EOF'
# ZFS Snapshot Policies Configuration
# Format: dataset_pattern:frequency:retention:prefix

# Corporate data - frequent snapshots with long retention
corporate-pool/corporate:hourly:720:hourly
corporate-pool/corporate:daily:90:daily
corporate-pool/corporate:weekly:52:weekly
corporate-pool/corporate:monthly:24:monthly

# Development - frequent snapshots with shorter retention
corporate-pool/projects/development:15min:96:dev
corporate-pool/projects/development:hourly:168:hourly
corporate-pool/projects/development:daily:30:daily

# Production - balanced approach
corporate-pool/projects/production:hourly:168:prod-hourly
corporate-pool/projects/production:daily:60:prod-daily
corporate-pool/projects/production:weekly:26:prod-weekly

# User homes - daily snapshots
corporate-pool/users/homes:daily:30:user-daily
corporate-pool/users/homes:weekly:12:user-weekly

# Backups - minimal snapshots (they are backups themselves)
corporate-pool/backups:weekly:4:backup-weekly

EOF
    
    log_snapshot_operation "Snapshot policies configuration created: $SNAPSHOT_CONFIG"
}

# Execute snapshot creation based on policies
create_scheduled_snapshots() {
    local frequency="$1"  # hourly, daily, weekly, monthly, 15min
    
    log_snapshot_operation "Creating $frequency snapshots"
    
    # Read policy configuration
    while IFS=':' read -r dataset_pattern freq retention prefix; do
        # Skip comments and empty lines
        [[ "$dataset_pattern" =~ ^#.*$ ]] && continue
        [[ -z "$dataset_pattern" ]] && continue
        
        # Process only matching frequency
        [[ "$freq" != "$frequency" ]] && continue
        
        # Find matching datasets
        zfs list -H -o name | grep "^$dataset_pattern" | while read -r dataset; do
            local timestamp=$(date +%Y%m%d_%H%M%S)
            local snapshot_name="${dataset}@${prefix}_${timestamp}"
            
            log_snapshot_operation "Creating snapshot: $snapshot_name"
            
            # Create snapshot with error handling
            if sudo zfs snapshot "$snapshot_name"; then
                log_snapshot_operation "Successfully created snapshot: $snapshot_name"
                
                # Apply retention policy
                cleanup_old_snapshots "$dataset" "$prefix" "$retention"
            else
                log_snapshot_operation "ERROR: Failed to create snapshot: $snapshot_name"
            fi
        done
        
    done < "$SNAPSHOT_CONFIG"
}

# Cleanup old snapshots based on retention policy
cleanup_old_snapshots() {
    local dataset="$1"
    local prefix="$2"
    local retention_count="$3"
    
    log_snapshot_operation "Cleaning up old snapshots for $dataset (prefix: $prefix, keep: $retention_count)"
    
    # Get snapshots matching prefix, sorted by creation time (oldest first)
    local snapshots=($(zfs list -H -t snapshot -o name -S creation "$dataset" | grep "@${prefix}_" | tail -n +$((retention_count + 1))))
    
    for snapshot in "${snapshots[@]}"; do
        log_snapshot_operation "Removing old snapshot: $snapshot"
        
        if sudo zfs destroy "$snapshot"; then
            log_snapshot_operation "Successfully removed snapshot: $snapshot"
        else
            log_snapshot_operation "ERROR: Failed to remove snapshot: $snapshot"
        fi
    done
}

# Advanced snapshot operations
perform_recursive_snapshots() {
    local parent_dataset="$1"
    local snapshot_suffix="$2"
    local recursive="$3"  # true/false
    
    log_snapshot_operation "Creating snapshots for $parent_dataset with suffix: $snapshot_suffix"
    
    if [[ "$recursive" == "true" ]]; then
        # Recursive snapshot - creates snapshots for all child datasets atomically
        local snapshot_name="${parent_dataset}@${snapshot_suffix}"
        sudo zfs snapshot -r "$snapshot_name"
        log_snapshot_operation "Created recursive snapshots: $snapshot_name"
    else
        # Individual snapshots for each dataset
        zfs list -H -o name -r "$parent_dataset" | while read -r dataset; do
            local snapshot_name="${dataset}@${snapshot_suffix}"
            sudo zfs snapshot "$snapshot_name"
            log_snapshot_operation "Created individual snapshot: $snapshot_name"
        done
    fi
}

# Snapshot rollback with safety checks
safe_snapshot_rollback() {
    local dataset="$1"
    local snapshot_name="$2"
    local backup_current="$3"  # true/false
    
    log_snapshot_operation "Preparing rollback for $dataset to snapshot: $snapshot_name"
    
    # Verify snapshot exists
    if ! zfs list -t snapshot "$snapshot_name" &>/dev/null; then
        log_snapshot_operation "ERROR: Snapshot $snapshot_name does not exist"
        return 1
    fi
    
    # Create backup of current state if requested
    if [[ "$backup_current" == "true" ]]; then
        local backup_snapshot="${dataset}@rollback_backup_$(date +%Y%m%d_%H%M%S)"
        log_snapshot_operation "Creating backup snapshot before rollback: $backup_snapshot"
        sudo zfs snapshot "$backup_snapshot"
    fi
    
    # Check for newer snapshots that will be destroyed
    local newer_snapshots=($(zfs list -H -t snapshot -o name "$dataset" | awk -F'@' "/$snapshot_name/{found=1; next} found" | head -5))
    
    if [[ ${#newer_snapshots[@]} -gt 0 ]]; then
        log_snapshot_operation "WARNING: Rollback will destroy ${#newer_snapshots[@]} newer snapshots:"
        printf '%s\n' "${newer_snapshots[@]}" | while read snapshot; do
            log_snapshot_operation "  - $snapshot"
        done
        
        # In production, you might want to require confirmation here
        read -p "Continue with rollback? This will destroy newer snapshots [y/N]: " -r
        if [[ ! $REPLY =~ ^[Yy]$ ]]; then
            log_snapshot_operation "Rollback cancelled by user"
            return 1
        fi
    fi
    
    # Perform rollback
    log_snapshot_operation "Executing rollback to: $snapshot_name"
    if sudo zfs rollback -r "$snapshot_name"; then
        log_snapshot_operation "Rollback completed successfully"
    else
        log_snapshot_operation "ERROR: Rollback failed"
        return 1
    fi
}

# Clone management for development environments
manage_development_clones() {
    local source_snapshot="$1"
    local clone_name="$2"
    local purpose="$3"  # development, testing, staging
    
    log_snapshot_operation "Creating development clone: $clone_name from $source_snapshot"
    
    # Create clone
    sudo zfs clone "$source_snapshot" "$clone_name"
    
    # Configure clone based on purpose
    case "$purpose" in
        "development")
            sudo zfs set compression=lz4 "$clone_name"
            sudo zfs set atime=off "$clone_name"
            sudo zfs set sync=disabled "$clone_name"  # Performance over safety for dev
            sudo zfs set quota=100G "$clone_name"
            ;;
        "testing")
            sudo zfs set compression=lz4 "$clone_name"
            sudo zfs set atime=off "$clone_name"
            sudo zfs set sync=standard "$clone_name"
            sudo zfs set quota=200G "$clone_name"
            ;;
        "staging")
            # Mirror production settings
            sudo zfs set compression=zstd "$clone_name"
            sudo zfs set sync=always "$clone_name"
            sudo zfs set quota=500G "$clone_name"
            ;;
    esac
    
    # Set expiration metadata for cleanup
    local expiration_date=$(date -d "+30 days" +%Y-%m-%d)
    sudo zfs set com.company:expires="$expiration_date" "$clone_name"
    sudo zfs set com.company:purpose="$purpose" "$clone_name"
    
    log_snapshot_operation "Development clone $clone_name created and configured for $purpose"
}

# Automated clone cleanup based on expiration
cleanup_expired_clones() {
    log_snapshot_operation "Checking for expired development clones"
    
    local current_date=$(date +%Y-%m-%d)
    
    # Find clones with expiration metadata
    zfs list -H -o name,com.company:expires | while IFS=$'\t' read -r dataset expires; do
        [[ "$expires" == "-" ]] && continue
        
        # Check if expired
        if [[ "$expires" < "$current_date" ]]; then
            log_snapshot_operation "Found expired clone: $dataset (expired: $expires)"
            
            # Get clone purpose for logging
            local purpose=$(zfs get -H -o value com.company:purpose "$dataset" 2>/dev/null || echo "unknown")
            
            # Destroy expired clone
            log_snapshot_operation "Destroying expired $purpose clone: $dataset"
            sudo zfs destroy "$dataset"
            
            if [[ $? -eq 0 ]]; then
                log_snapshot_operation "Successfully destroyed expired clone: $dataset"
            else
                log_snapshot_operation "ERROR: Failed to destroy clone: $dataset"
            fi
        fi
    done
}

# Create cron jobs for automated snapshot management
setup_snapshot_automation() {
    log_snapshot_operation "Setting up automated snapshot scheduling"
    
    # Create cron entries
    cat > /tmp/zfs-snapshot-crontab << 'EOF'
# ZFS Automated Snapshot Management
# 15-minute snapshots for development datasets
*/15 * * * * /usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots 15min

# Hourly snapshots
0 * * * * /usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots hourly

# Daily snapshots at 2 AM
0 2 * * * /usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots daily

# Weekly snapshots on Sunday at 3 AM
0 3 * * 0 /usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots weekly

# Monthly snapshots on the 1st at 4 AM
0 4 1 * * /usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots monthly

# Cleanup expired clones daily at 5 AM
0 5 * * * /usr/local/bin/zfs-snapshot-manager.sh cleanup_expired_clones

EOF
    
    # Install cron job
    sudo crontab /tmp/zfs-snapshot-crontab
    log_snapshot_operation "Automated snapshot scheduling configured"
}

# Example usage
create_snapshot_policies
setup_snapshot_automation

# Manual operations examples
# create_scheduled_snapshots "daily"
# safe_snapshot_rollback "corporate-pool/projects/development" "corporate-pool/projects/development@daily_20250802_020000" "true"
# manage_development_clones "corporate-pool/projects/production@prod-daily_20250802_020000" "corporate-pool/projects/dev-clone-001" "development"

log_snapshot_operation "Snapshot management system initialized"

```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Snapshot and Clone Management. 🔗

### Replication Setup

#### Enterprise ZFS Replication Infrastructure
```bash
#!/bin/bash
# zfs-replication-manager.sh - Enterprise ZFS replication and disaster recovery

REPLICATION_LOG="/var/log/zfs-replication.log"
REPLICATION_CONFIG="/etc/zfs/replication-config.conf"
BANDWIDTH_LIMIT="100M"  # Bandwidth limit for remote transfers

log_replication() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$REPLICATION_LOG"
}

# Configure replication topology
setup_replication_config() {
    log_replication "Setting up replication configuration"
    
    sudo mkdir -p "$(dirname "$REPLICATION_CONFIG")"
    cat > "$REPLICATION_CONFIG" << 'EOF'
# ZFS Replication Configuration
# Format: source_dataset:target_host:target_dataset:frequency:compression:bandwidth_limit

# Primary to DR site replication
corporate-pool/corporate:dr-site.company.com:dr-pool/corporate:daily:gzip:50M
corporate-pool/projects/production:dr-site.company.com:dr-pool/production:hourly:lz4:100M

# Offsite backup replication
corporate-pool/corporate:backup.company.com:backup-pool/corporate:weekly:gzip-9:20M
corporate-pool/projects:backup.company.com:backup-pool/projects:daily:gzip:30M

# Branch office replication
corporate-pool/shared:branch.company.com:branch-pool/shared:daily:lz4:25M

EOF
    
    log_replication "Replication configuration created: $REPLICATION_CONFIG"
}

# Initial full replication setup
perform_initial_replication() {
    local source_dataset="$1"
    local target_host="$2"
    local target_dataset="$3"
    local compression="$4"
    local bandwidth_limit="$5"
    
    log_replication "Starting initial replication: $source_dataset -> $target_host:$target_dataset"
    
    # Create initial snapshot for replication
    local initial_snapshot="${source_dataset}@initial_replication_$(date +%Y%m%d_%H%M%S)"
    sudo zfs snapshot -r "$initial_snapshot"
    
    # Prepare send command with options
    local send_cmd="sudo zfs send -R"
    
    # Add compression if specified
    case "$compression" in
        "gzip"|"gzip-1"|"gzip-2"|"gzip-3"|"gzip-4"|"gzip-5"|"gzip-6"|"gzip-7"|"gzip-8"|"gzip-9")
            send_cmd+=" | gzip"
            [[ "$compression" != "gzip" ]] && send_cmd+=" -${compression#gzip-}"
            ;;
        "lz4")
            send_cmd+=" | lz4 -c"
            ;;
        "zstd")
            send_cmd+=" | zstd -c"
            ;;
    esac
    
    # Add bandwidth limiting
    if [[ -n "$bandwidth_limit" ]]; then
        send_cmd+=" | pv -L $bandwidth_limit"
    fi
    
    # Add SSH transport and receive command
    local receive_cmd="ssh $target_host"
    
    # Handle decompression on target if compression was used
    case "$compression" in
        "gzip"|"gzip-"*)
            receive_cmd+=" 'gunzip | sudo zfs receive $target_dataset'"
            ;;
        "lz4")
            receive_cmd+=" 'lz4 -d | sudo zfs receive $target_dataset'"
            ;;
        "zstd")
            receive_cmd+=" 'zstd -d | sudo zfs receive $target_dataset'"
            ;;
        *)
            receive_cmd+=" 'sudo zfs receive $target_dataset'"
            ;;
    esac
    
    # Execute initial replication
    local full_command="$send_cmd $initial_snapshot | $receive_cmd"
    log_replication "Executing: $full_command"
    
    if eval "$full_command"; then
        log_replication "Initial replication completed successfully"
        
        # Record replication state
        echo "$source_dataset:$target_host:$target_dataset:$initial_snapshot" >> "/var/lib/zfs/replication-state"
        
    else
        log_replication "ERROR: Initial replication failed"
        return 1
    fi
}

# Incremental replication
perform_incremental_replication() {
    local source_dataset="$1"
    local target_host="$2"
    local target_dataset="$3"
    local compression="$4"
    local bandwidth_limit="$5"
    
    log_replication "Starting incremental replication: $source_dataset -> $target_host:$target_dataset"
    
    # Find last replicated snapshot
    local last_snapshot=$(grep "^$source_dataset:$target_host:$target_dataset:" "/var/lib/zfs/replication-state" | tail -1 | cut -d':' -f4)
    
    if [[ -z "$last_snapshot" ]]; then
        log_replication "No previous replication found, performing initial replication"
        perform_initial_replication "$source_dataset" "$target_host" "$target_dataset" "$compression" "$bandwidth_limit"
        return $?
    fi
    
    # Create new snapshot for incremental replication
    local new_snapshot="${source_dataset}@incremental_$(date +%Y%m%d_%H%M%S)"
    sudo zfs snapshot -r "$new_snapshot"
    
    # Build incremental send command
    local send_cmd="sudo zfs send -R -i $last_snapshot $new_snapshot"
    
    # Add compression
    case "$compression" in
        "gzip"|"gzip-"*)
            send_cmd+=" | gzip"
            [[ "$compression" != "gzip" ]] && send_cmd+=" -${compression#gzip-}"
            ;;
        "lz4")
            send_cmd+=" | lz4 -c"
            ;;
        "zstd")
            send_cmd+=" | zstd -c"
            ;;
    esac
    
    # Add bandwidth limiting
    if [[ -n "$bandwidth_limit" ]]; then
        send_cmd+=" | pv -L $bandwidth_limit"
    fi
    
    # Build receive command
    local receive_cmd="ssh $target_host"
    
    case "$compression" in
        "gzip"|"gzip-"*)
            receive_cmd+=" 'gunzip | sudo zfs receive -F $target_dataset'"
            ;;
        "lz4")
            receive_cmd+=" 'lz4 -d | sudo zfs receive -F $target_dataset'"
            ;;
        "zstd")
            receive_cmd+=" 'zstd -d | sudo zfs receive -F $target_dataset'"
            ;;
        *)
            receive_cmd+=" 'sudo zfs receive -F $target_dataset'"
            ;;
    esac
    
    # Execute incremental replication
    local full_command="$send_cmd | $receive_cmd"
    log_replication "Executing incremental: $full_command"
    
    if eval "$full_command"; then
        log_replication "Incremental replication completed successfully"
        
        # Update replication state
        sed -i "s|^$source_dataset:$target_host:$target_dataset:.*|$source_dataset:$target_host:$target_dataset:$new_snapshot|" "/var/lib/zfs/replication-state"
        
        # Cleanup old local snapshots (keep last 3 replication snapshots)
        cleanup_replication_snapshots "$source_dataset" 3
        
    else
        log_replication "ERROR: Incremental replication failed"
        return 1
    fi
}

# Cleanup old replication snapshots
cleanup_replication_snapshots() {
    local dataset="$1"
    local keep_count="$2"
    
    log_replication "Cleaning up old replication snapshots for $dataset (keeping $keep_count)"
    
    # Get replication snapshots sorted by creation time
    local snapshots=($(zfs list -H -t snapshot -o name -S creation "$dataset" | grep "@.*replication_\|@initial_replication_\|@incremental_" | tail -n +$((keep_count + 1))))
    
    for snapshot in "${snapshots[@]}"; do
        log_replication "Removing old replication snapshot: $snapshot"
        sudo zfs destroy -r "$snapshot" || log_replication "Warning: Failed to destroy $snapshot"
    done
}

# Automated replication based on schedule
run_scheduled_replication() {
    local frequency="$1"  # hourly, daily, weekly
    
    log_replication "Running scheduled $frequency replication"
    
    while IFS=':' read -r source target_host target freq compression bandwidth; do
        # Skip comments and empty lines
        [[ "$source" =~ ^#.*$ ]] && continue
        [[ -z "$source" ]] && continue
        
        # Process only matching frequency
        [[ "$freq" != "$frequency" ]] && continue
        
        log_replication "Processing replication: $source -> $target_host:$target"
        
        # Verify SSH connectivity
        if ! ssh -o ConnectTimeout=10 "$target_host" "echo 'SSH OK'" &>/dev/null; then
            log_replication "ERROR: Cannot connect to $target_host via SSH"
            continue
        fi
        
        # Perform incremental replication
        perform_incremental_replication "$source" "$target_host" "$target" "$compression" "$bandwidth"
        
    done < "$REPLICATION_CONFIG"
}

# Disaster recovery failover procedure
perform_disaster_failover() {
    local failed_site="$1"
    local recovery_site="$2"
    local dataset_pattern="$3"
    
    log_replication "Starting disaster recovery failover from $failed_site to $recovery_site"
    
    # Find datasets to promote on recovery site
    ssh "$recovery_site" "zfs list -H -o name | grep '$dataset_pattern'" | while read -r dataset; do
        log_replication "Promoting dataset for production use: $dataset"
        
        # Make dataset writable and accessible
        ssh "$recovery_site" "sudo zfs set readonly=off $dataset"
        ssh "$recovery_site" "sudo zfs mount $dataset"
        
        # Update any application configurations as needed
        # This would be customized based on your environment
        
        log_replication "Dataset $dataset promoted successfully"
    done
    
    log_replication "Disaster recovery failover completed"
}

# Monitoring and alerting for replication
monitor_replication_health() {
    log_replication "Monitoring replication health"
    
    local current_time=$(date +%s)
    local alert_threshold=86400  # 24 hours in seconds
    
    while IFS=':' read -r source target_host target last_snapshot; do
        [[ "$source" =~ ^#.*$ ]] && continue
        [[ -z "$source" ]] && continue
        
        # Extract timestamp from snapshot name
        local snapshot_timestamp=$(echo "$last_snapshot" | grep -o '[0-9]\{8\}_[0-9]\{6\}')
        
        if [[ -n "$snapshot_timestamp" ]]; then
            local snapshot_time=$(date -d "${snapshot_timestamp:0:8} ${snapshot_timestamp:9:2}:${snapshot_timestamp:11:2}:${snapshot_timestamp:13:2}" +%s)
            local time_diff=$((current_time - snapshot_time))
            
            if [[ $time_diff -gt $alert_threshold ]]; then
                log_replication "ALERT: Replication lag detected for $source -> $target_host:$target (last: $snapshot_timestamp)"
                # Send alert (implement your notification method)
                echo "Replication lag alert: $source to $target_host" | mail -s "ZFS Replication Alert" admin@company.com 2>/dev/null || true
            fi
        fi
        
    done < "/var/lib/zfs/replication-state"
}

# Example automated replication setup
setup_replication_config

# Initialize replication state tracking
sudo mkdir -p /var/lib/zfs
sudo touch /var/lib/zfs/replication-state

# Set up cron jobs for automated replication
cat > /tmp/zfs-replication-crontab << 'EOF'
# ZFS Automated Replication
# Hourly replication
0 * * * * /usr/local/bin/zfs-replication-manager.sh run_scheduled_replication hourly

# Daily replication at 1 AM
0 1 * * * /usr/local/bin/zfs-replication-manager.sh run_scheduled_replication daily

# Weekly replication on Sunday at 2 AM
0 2 * * 0 /usr/local/bin/zfs-replication-manager.sh run_scheduled_replication weekly

# Monitor replication health every 4 hours
0 */4 * * * /usr/local/bin/zfs-replication-manager.sh monitor_replication_health

EOF

sudo crontab /tmp/zfs-replication-crontab

log_replication "Replication infrastructure setup completed"
```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Replication and Backup. 🔗

### Performance Optimization

#### ZFS Performance Tuning and Monitoring
```bash
#!/bin/bash
# zfs-performance-optimizer.sh - Enterprise ZFS performance optimization

PERF_LOG="/var/log/zfs-performance.log"
TUNING_CONFIG="/etc/zfs/performance-tuning.conf"

log_performance() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$PERF_LOG"
}

# Create performance tuning configuration
create_performance_config() {
    log_performance "Creating performance tuning configuration"
    
    sudo mkdir -p "$(dirname "$TUNING_CONFIG")"
    cat > "$TUNING_CONFIG" << 'EOF'
# ZFS Performance Tuning Configuration
# Format: parameter:value:description

# ARC (Adaptive Replacement Cache) Settings
zfs_arc_max:17179869184:Maximum ARC size (16GB for 32GB system)
zfs_arc_min:2147483648:Minimum ARC size (2GB)
zfs_arc_meta_limit_percent:75:Metadata limit as percentage of ARC

# L2ARC (Level 2 ARC) Settings
l2arc_write_max:134217728:L2ARC write throughput (128MB/s)
l2arc_write_boost:268435456:L2ARC initial write boost (256MB/s)
l2arc_headroom:2:L2ARC headroom multiplier

# ZIL (ZFS Intent Log) Settings
zfs_immediate_write_sz:32768:Immediate write size threshold (32KB)
zfs_sync_pass_deferred_free:2:Deferred free passes for sync
zil_slog_bulk:786432:SLOG bulk write threshold (768KB)

# Transaction Group Settings
zfs_txg_timeout:5:Transaction group timeout (seconds)
zfs_dirty_data_max:4294967296:Maximum dirty data (4GB)
zfs_dirty_data_max_percent:10:Maximum dirty data percentage

# I/O Scheduler Settings
zfs_vdev_max_active:1000:Maximum active I/O per vdev
zfs_vdev_sync_read_min_active:10:Minimum sync read I/O
zfs_vdev_sync_read_max_active:10:Maximum sync read I/O
zfs_vdev_sync_write_min_active:10:Minimum sync write I/O
zfs_vdev_sync_write_max_active:10:Maximum sync write I/O
zfs_vdev_async_read_min_active:1:Minimum async read I/O
zfs_vdev_async_read_max_active:3:Maximum async read I/O
zfs_vdev_async_write_min_active:1:Minimum async write I/O
zfs_vdev_async_write_max_active:10:Maximum async write I/O

EOF
    
    log_performance "Performance tuning configuration created: $TUNING_CONFIG"
}

# Apply system-level ZFS tuning parameters
apply_kernel_tuning() {
    log_performance "Applying kernel-level ZFS tuning parameters"
    
    # Read and apply tuning parameters
    while IFS=':' read -r param value description; do
        # Skip comments and empty lines
        [[ "$param" =~ ^#.*$ ]] && continue
        [[ -z "$param" ]] && continue
        
        log_performance "Setting $param = $value ($description)"
        
        # Apply parameter
        if echo "$value" | sudo tee "/sys/module/zfs/parameters/$param" >/dev/null 2>&1; then
            log_performance "Successfully set $param"
        else
            log_performance "Warning: Failed to set $param (may not exist on this system)"
        fi
        
    done < "$TUNING_CONFIG"
    
    # Make tuning persistent across reboots
    create_persistent_tuning
}

# Create persistent tuning configuration
create_persistent_tuning() {
    log_performance "Creating persistent tuning configuration"
    
    # Create modprobe configuration for ZFS
    cat > /tmp/zfs-tuning.conf << 'EOF'
# ZFS Performance Tuning - Persistent Configuration
options zfs zfs_arc_max=17179869184
options zfs zfs_arc_min=2147483648
options zfs zfs_arc_meta_limit_percent=75
options zfs l2arc_write_max=134217728
options zfs l2arc_write_boost=268435456
options zfs l2arc_headroom=2
options zfs zfs_immediate_write_sz=32768
options zfs zfs_sync_pass_deferred_free=2
options zfs zil_slog_bulk=786432
options zfs zfs_txg_timeout=5
options zfs zfs_dirty_data_max=4294967296
options zfs zfs_dirty_data_max_percent=10
options zfs zfs_vdev_max_active=1000
options zfs zfs_vdev_sync_read_min_active=10
options zfs zfs_vdev_sync_read_max_active=10
options zfs zfs_vdev_sync_write_min_active=10
options zfs zfs_vdev_sync_write_max_active=10
options zfs zfs_vdev_async_read_min_active=1
options zfs zfs_vdev_async_read_max_active=3
options zfs zfs_vdev_async_write_min_active=1
options zfs zfs_vdev_async_write_max_active=10

EOF
    
    sudo mv /tmp/zfs-tuning.conf /etc/modprobe.d/zfs-performance.conf
    log_performance "Persistent tuning configuration created: /etc/modprobe.d/zfs-performance.conf"
}

# Optimize dataset properties for specific workloads
optimize_dataset_for_workload() {
    local dataset="$1"
    local workload_type="$2"  # database, fileserver, backup, vms, development
    
    log_performance "Optimizing $dataset for $workload_type workload"
    
    case "$workload_type" in
        "database")
            # Database optimization: small random I/O, low latency
            sudo zfs set recordsize=8K "$dataset"
            sudo zfs set primarycache=metadata "$dataset"
            sudo zfs set secondarycache=metadata "$dataset"
            sudo zfs set sync=always "$dataset"
            sudo zfs set compression=lz4 "$dataset"
            sudo zfs set atime=off "$dataset"
            sudo zfs set logbias=latency "$dataset"
            log_performance "Database optimization applied to $dataset"
            ;;
            
        "fileserver")
            # File server optimization: large sequential I/O
            sudo zfs set recordsize=1M "$dataset"
            sudo zfs set primarycache=all "$dataset"
            sudo zfs set secondarycache=all "$dataset"
            sudo zfs set sync=standard "$dataset"
            sudo zfs set compression=zstd "$dataset"
            sudo zfs set atime=off "$dataset"
            sudo zfs set logbias=throughput "$dataset"
            log_performance "File server optimization applied to $dataset"
            ;;
            
        "backup")
            # Backup optimization: maximum compression, lower performance
            sudo zfs set recordsize=1M "$dataset"
            sudo zfs set primarycache=metadata "$dataset"
            sudo zfs set secondarycache=none "$dataset"
            sudo zfs set sync=disabled "$dataset"
            sudo zfs set compression=zstd-19 "$dataset"
            sudo zfs set atime=off "$dataset"
            sudo zfs set redundant_metadata=most "$dataset"
            log_performance "Backup optimization applied to $dataset"
            ;;
            
        "vms")
            # Virtual machine optimization: balanced approach
            sudo zfs set recordsize=64K "$dataset"
            sudo zfs set primarycache=all "$dataset"
            sudo zfs set secondarycache=all "$dataset"
            sudo zfs set sync=always "$dataset"
            sudo zfs set compression=lz4 "$dataset"
            sudo zfs set atime=off "$dataset"
            sudo zfs set volblocksize=16K "$dataset" 2>/dev/null || true  # For zvols
            log_performance "Virtual machine optimization applied to $dataset"
            ;;
            
        "development")
            # Development optimization: performance over safety
            sudo zfs set recordsize=128K "$dataset"
            sudo zfs set primarycache=all "$dataset"
            sudo zfs set secondarycache=all "$dataset"
            sudo zfs set sync=disabled "$dataset"
            sudo zfs set compression=lz4 "$dataset"
            sudo zfs set atime=off "$dataset"
            sudo zfs set logbias=throughput "$dataset"
            log_performance "Development optimization applied to $dataset"
            ;;
            
        *)
            log_performance "Unknown workload type: $workload_type"
            return 1
            ;;
    esac
}

# Performance monitoring and analysis
monitor_zfs_performance() {
    local duration="${1:-300}"  # Default 5 minutes
    local interval="${2:-5}"    # Default 5 seconds
    
    log_performance "Starting ZFS performance monitoring for ${duration}s (interval: ${interval}s)"
    
    local monitor_file="/tmp/zfs-performance-$(date +%Y%m%d_%H%M%S).log"
    local end_time=$(($(date +%s) + duration))
    
    # Initialize monitoring
    echo "# ZFS Performance Monitor - $(date)" > "$monitor_file"
    echo "# Timestamp,ARC_Hit_Rate,ARC_Size_MB,L2ARC_Hit_Rate,TXG_Sync_Time,Read_IOPS,Write_IOPS" >> "$monitor_file"
    
    while [[ $(date +%s) -lt $end_time ]]; do
        local timestamp=$(date +%Y-%m-%d_%H:%M:%S)
        
        # ARC statistics
        local arc_hits=$(awk '/hits/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
        local arc_misses=$(awk '/misses/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
        local arc_size=$(awk '/^size/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
        local arc_hit_rate=$(echo "scale=2; $arc_hits / ($arc_hits + $arc_misses) * 100" | bc -l 2>/dev/null || echo "0")
        local arc_size_mb=$(echo "scale=0; $arc_size / 1048576" | bc -l)
        
        # L2ARC statistics
        local l2arc_hits=$(awk '/l2_hits/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
        local l2arc_misses=$(awk '/l2_misses/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
        local l2arc_hit_rate=$(echo "scale=2; $l2arc_hits / ($l2arc_hits + $l2arc_misses) * 100" | bc -l 2>/dev/null || echo "0")
        
        # Transaction group statistics
        local txg_sync_time=$(awk '/txg_sync_time/ {print $3; exit}' /proc/spl/kstat/zfs/*/txgs 2>/dev/null || echo "0")
        
        # I/O statistics (simplified)
        local read_iops=$(iostat -x 1 1 | awk '/^[sz]d/ {reads += $4} END {print reads}' 2>/dev/null || echo "0")
        local write_iops=$(iostat -x 1 1 | awk '/^[sz]d/ {writes += $5} END {print writes}' 2>/dev/null || echo "0")
        
        # Log current statistics
        echo "$timestamp,$arc_hit_rate,$arc_size_mb,$l2arc_hit_rate,$txg_sync_time,$read_iops,$write_iops" >> "$monitor_file"
        
        # Display real-time stats
        printf "\r[%s] ARC: %0.1f%% (%dMB) L2ARC: %0.1f%% TXG: %dns R/W IOPS: %d/%d" \
            "$timestamp" "$arc_hit_rate" "$arc_size_mb" "$l2arc_hit_rate" "$txg_sync_time" "$read_iops" "$write_iops"
        
        sleep "$interval"
    done
    
    echo  # New line after monitoring
    log_performance "Performance monitoring completed. Data saved to: $monitor_file"
    
    # Generate summary report
    generate_performance_report "$monitor_file"
}

# Generate performance analysis report
generate_performance_report() {
    local monitor_file="$1"
    local report_file="${monitor_file%.log}-report.txt"
    
    log_performance "Generating performance analysis report: $report_file"
    
    cat > "$report_file" << EOF
# ZFS Performance Analysis Report
Generated: $(date)
Monitor Data: $monitor_file

## Summary Statistics

EOF
    
    # Calculate averages and statistics using awk
    awk -F',' '
    NR > 2 {  # Skip header lines
        count++
        arc_hit_sum += $2
        arc_size_sum += $3
        l2arc_hit_sum += $4
        txg_sync_sum += $5
        read_iops_sum += $6
        write_iops_sum += $7
        
        if ($2 < arc_hit_min || NR == 3) arc_hit_min = $2
        if ($2 > arc_hit_max || NR == 3) arc_hit_max = $2
    }
    END {
        if (count > 0) {
            printf "Average ARC Hit Rate: %.2f%% (Min: %.2f%%, Max: %.2f%%)\n", 
                   arc_hit_sum/count, arc_hit_min, arc_hit_max
            printf "Average ARC Size: %.0f MB\n", arc_size_sum/count
            printf "Average L2ARC Hit Rate: %.2f%%\n", l2arc_hit_sum/count
            printf "Average TXG Sync Time: %.0f ns\n", txg_sync_sum/count
            printf "Average Read IOPS: %.0f\n", read_iops_sum/count
            printf "Average Write IOPS: %.0f\n", write_iops_sum/count
        }
    }' "$monitor_file" >> "$report_file"
    
    # Add recommendations
    cat >> "$report_file" << 'EOF'

## Performance Recommendations

### ARC Tuning
- ARC hit rate should be > 90% for optimal performance
- If hit rate is low, consider increasing zfs_arc_max
- Monitor for memory pressure on the system

### L2ARC Optimization
- L2ARC effective when hit rate > 10%
- Use fast SSDs for L2ARC devices
- Size L2ARC at 5-10x the ARC size

### Transaction Group Performance
- TXG sync times > 1 second indicate potential bottlenecks
- Consider faster storage or more SLOG devices
- Check for I/O scheduler conflicts

### General Recommendations
- Use appropriate record sizes for workload
- Enable compression for space and performance benefits
- Monitor disk utilization and plan for expansion

EOF
    
    log_performance "Performance analysis report generated: $report_file"
}

# Automated performance alerting
setup_performance_alerts() {
    log_performance "Setting up performance monitoring alerts"
    
    cat > /tmp/zfs-performance-monitor.sh << 'EOF'
#!/bin/bash
# ZFS Performance Alert Monitor

ALERT_THRESHOLD_ARC=85  # Alert if ARC hit rate below 85%
ALERT_THRESHOLD_TXG=2000000000  # Alert if TXG sync > 2 seconds (in ns)

check_performance_alerts() {
    # Check ARC hit rate
    local arc_hits=$(awk '/hits/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
    local arc_misses=$(awk '/misses/ {print $3; exit}' /proc/spl/kstat/zfs/arcstats)
    local arc_hit_rate=$(echo "scale=2; $arc_hits / ($arc_hits + $arc_misses) * 100" | bc -l)
    
    if (( $(echo "$arc_hit_rate < $ALERT_THRESHOLD_ARC" | bc -l) )); then
        echo "ALERT: ZFS ARC hit rate is ${arc_hit_rate}% (threshold: ${ALERT_THRESHOLD_ARC}%)" | \
        mail -s "ZFS Performance Alert - Low ARC Hit Rate" admin@company.com 2>/dev/null || \
        logger "ZFS ALERT: Low ARC hit rate ${arc_hit_rate}%"
    fi
    
    # Check TXG sync time
    local txg_sync_time=$(awk '/txg_sync_time/ {print $3; exit}' /proc/spl/kstat/zfs/*/txgs 2>/dev/null || echo "0")
    
    if (( txg_sync_time > ALERT_THRESHOLD_TXG )); then
        local txg_seconds=$(echo "scale=2; $txg_sync_time / 1000000000" | bc -l)
        echo "ALERT: ZFS TXG sync time is ${txg_seconds}s (threshold: 2s)" | \
        mail -s "ZFS Performance Alert - High TXG Sync Time" admin@company.com 2>/dev/null || \
        logger "ZFS ALERT: High TXG sync time ${txg_seconds}s"
    fi
}

check_performance_alerts
EOF
    
    sudo mv /tmp/zfs-performance-monitor.sh /usr/local/bin/zfs-performance-monitor.sh
    sudo chmod +x /usr/local/bin/zfs-performance-monitor.sh
    
    # Add to cron for regular monitoring
    echo "*/15 * * * * /usr/local/bin/zfs-performance-monitor.sh" | sudo crontab -
    
    log_performance "Performance alerting configured"
}

# Example usage and initialization
create_performance_config
apply_kernel_tuning
setup_performance_alerts

# Example workload optimizations
# optimize_dataset_for_workload "corporate-pool/databases" "database"
# optimize_dataset_for_workload "corporate-pool/fileserver" "fileserver"
# optimize_dataset_for_workload "corporate-pool/backups" "backup"

log_performance "ZFS performance optimization setup completed"
```

**Related Commands/Topics:** See [Essential Command Reference](#essential-command-reference) → Performance and Monitoring. 🔗

### Monitoring and Diagnostics

#### Comprehensive ZFS Health Monitoring
```bash
#!/bin/bash
# zfs-monitoring-system.sh - Enterprise ZFS monitoring and diagnostics

MONITOR_LOG="/var/log/zfs-monitoring.log"
STATUS_DIR="/var/lib/zfs/status"
ALERT_CONFIG="/etc/zfs/monitoring-alerts.conf"

log_monitor() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$MONITOR_LOG"
}

# Initialize monitoring system
initialize_monitoring() {
    log_monitor "Initializing ZFS monitoring system"
    
    sudo mkdir -p "$STATUS_DIR"
    sudo mkdir -p "$(dirname "$ALERT_CONFIG")"
    
    # Create monitoring configuration
    cat > "$ALERT_CONFIG" << 'EOF'
# ZFS Monitoring Alert Configuration
# Format: metric:threshold:severity:action

# Pool health monitoring
pool_status:DEGRADED:CRITICAL:email,sms
pool_status:FAULTED:CRITICAL:email,sms,page
pool_errors:10:WARNING:email
pool_errors:100:CRITICAL:email,sms

# Capacity monitoring
pool_capacity:80:WARNING:email
pool_capacity:90:CRITICAL:email,sms
dataset_quota_usage:90:WARNING:email

# Performance monitoring
arc_hit_rate:85:WARNING:email
txg_sync_time:2000000000:WARNING:email
scrub_age:604800:WARNING:email

# Hardware monitoring
disk_errors:5:WARNING:email
disk_errors:20:CRITICAL:email,sms

EOF
    
    log_monitor "Monitoring system initialized"
}

# Comprehensive pool health check
check_pool_health() {
    log_monitor "Performing comprehensive pool health check"
    
    local health_report="$STATUS_DIR/pool-health-$(date +%Y%m%d_%H%M%S).json"
    
    # Initialize health report
    echo "{" > "$health_report"
    echo "  \"timestamp\": \"$(date -Iseconds)\"," >> "$health_report"
    echo "  \"pools\": [" >> "$health_report"
    
    local first_pool=true
    
    # Check each pool
    zpool list -H -o name | while read -r pool; do
        [[ "$first_pool" != "true" ]] && echo "    }," >> "$health_report"
        first_pool=false
        
        echo "    {" >> "$health_report"
        echo "      \"name\": \"$pool\"," >> "$health_report"
        
        # Basic pool information
        local status=$(zpool status "$pool" | head -1 | awk '{print $2}')
        local health=$(zpool list -H -o health "$pool")
        local capacity=$(zpool list -H -o cap "$pool" | tr -d '%')
        local size=$(zpool list -H -o size "$pool")
        local alloc=$(zpool list -H -o alloc "$pool")
        local free=$(zpool list -H -o free "$pool")
        
        echo "      \"status\": \"$status\"," >> "$health_report"
        echo "      \"health\": \"$health\"," >> "$health_report"
        echo "      \"capacity_percent\": $capacity," >> "$health_report"
        echo "      \"size\": \"$size\"," >> "$health_report"
        echo "      \"allocated\": \"$alloc\"," >> "$health_report"
        echo "      \"free\": \"$free\"," >> "$health_report"
        
        # Error counts
        local read_errors=$(zpool status "$pool" | awk '/errors:/ {print $2; exit}')
        local write_errors=$(zpool status "$pool" | awk '/errors:/ {getline; print $2; exit}')
        local cksum_errors=$(zpool status "$pool" | awk '/errors:/ {getline; getline; print $2; exit}')
        
        echo "      \"errors\": {" >> "$health_report"
        echo "        \"read\": \"$read_errors\"," >> "$health_report"
        echo "        \"write\": \"$write_errors\"," >> "$health_report"
        echo "        \"checksum\": \"$cksum_errors\"" >> "$health_report"
        echo "      }," >> "$health_report"
        
        # Scrub information
        local scrub_status=$(zpool status "$pool" | grep -A1 "scan:" | tail -1 | sed 's/^[[:space:]]*//')
        local last_scrub_date="unknown"
        
        if echo "$scrub_status" | grep -q "completed"; then
            last_scrub_date=$(echo "$scrub_status" | grep -o '[A-Z][a-z][a-z] [A-Z][a-z][a-z] [0-9]* [0-9]*:[0-9]*:[0-9]* [0-9]*')
        fi
        
        echo "      \"scrub\": {" >> "$health_report"
        echo "        \"status\": \"$scrub_status\"," >> "$health_report"
        echo "        \"last_completed\": \"$last_scrub_date\"" >> "$health_report"
        echo "      }," >> "$health_report"
        
        # Device information
        echo "      \"devices\": [" >> "$health_report"
        
        local first_device=true
        zpool status "$pool" | grep -E '^\s+[a-zA-Z0-9/\-_]+' | while read -r device state read write cksum; do
            [[ "$first_device" != "true" ]] && echo "        }," >> "$health_report"
            first_device=false
            
            echo "        {" >> "$health_report"
            echo "          \"name\": \"$device\"," >> "$health_report"
            echo "          \"state\": \"$state\"," >> "$health_report"
            echo "          \"read_errors\": \"$read\"," >> "$health_report"
            echo "          \"write_errors\": \"$write\"," >> "$health_report"
            echo "          \"checksum_errors\": \"$cksum\"" >> "$health_report"
        done
        
        echo "        }" >> "$health_report"
        echo "      ]" >> "$health_report"
    done
    
    echo "    }" >> "$health_report"
    echo "  ]" >> "$health_report"
    echo "}" >> "$health_report"
    
    # Process alerts based on health data
    process_health_alerts "$health_report"
    
    log_monitor "Pool health check completed: $health_report"
}

# Process alerts based on monitoring data
process_health_alerts() {
    local health_file="$1"
    
    log_monitor "Processing health alerts from: $health_file"
    
    # Read alert configuration and check against health data
    while IFS=':' read -r metric threshold severity action; do
        [[ "$metric" =~ ^#.*$ ]] && continue
        [[ -z "$metric" ]] && continue
        
        case "$metric" in
            "pool_capacity")
                # Check pool capacity alerts
                local pools_over_threshold=$(jq -r ".pools[] | select(.capacity_percent > $threshold) | .name" "$health_file" 2>/dev/null)
                for pool in $pools_over_threshold; do
                    local capacity=$(jq -r ".pools[] | select(.name == \"$pool\") | .capacity_percent" "$health_file")
                    send_alert "$severity" "$action" "Pool $pool capacity at ${capacity}% (threshold: ${threshold}%)"
                done
                ;;
                
            "pool_status")
                # Check pool status alerts
                local degraded_pools=$(jq -r ".pools[] | select(.health == \"$threshold\") | .name" "$health_file" 2>/dev/null)
                for pool in $degraded_pools; do
                    send_alert "$severity" "$action" "Pool $pool status: $threshold"
                done
                ;;
                
            "pool_errors")
                # Check error count alerts
                local error_pools=$(jq -r ".pools[] | select((.errors.read | tonumber) + (.errors.write | tonumber) + (.errors.checksum | tonumber) > $threshold) | .name" "$health_file" 2>/dev/null)
                for pool in $error_pools; do
                    local total_errors=$(jq -r ".pools[] | select(.name == \"$pool\") | (.errors.read | tonumber) + (.errors.write | tonumber) + (.errors.checksum | tonumber)" "$health_file")
                    send_alert "$severity" "$action" "Pool $pool has $total_errors total errors (threshold: $threshold)"
                done
                ;;
        esac
        
    done < "$ALERT_CONFIG"
}

# Send alerts based on configuration
send_alert() {
    local severity="$1"
    local actions="$2"
    local message="$3"
    
    log_monitor "ALERT [$severity]: $message"
    
    # Process each action
    IFS=',' read -ra ACTION_LIST <<< "$actions"
    for action in "${ACTION_LIST[@]}"; do
        case "$action" in
            "email")
                echo "$message" | mail -s "ZFS Alert [$severity]" admin@company.com 2>/dev/null || \
                log_monitor "Warning: Failed to send email alert"
                ;;
            "sms")
                # Implement SMS alerting (example using SMS gateway)
                curl -X POST "https://api.sms-gateway.com/send" \
                     -d "to=+1234567890" \
                     -d "message=ZFS Alert: $message" 2>/dev/null || \
                log_monitor "Warning: Failed to send SMS alert"
                ;;
            "page")
                # Implement pager alerting
                log_monitor "PAGER ALERT: $message"
                ;;
            "webhook")
                # Send to monitoring system webhook
                curl -X POST "http://monitoring.company.com/webhook/zfs" \
                     -H "Content-Type: application/json" \
                     -d "{\"severity\":\"$severity\",\"message\":\"$message\"}" 2>/dev/null || \
                log_monitor "Warning: Failed to send webhook alert"
                ;;
        esac
    done
}

# Dataset monitoring and quota management
monitor_dataset_usage() {
    log_monitor "Monitoring dataset usage and quotas"
    
    local usage_report="$STATUS_DIR/dataset-usage-$(date +%Y%m%d_%H%M%S).json"
    
    echo "{" > "$usage_report"
    echo "  \"timestamp\": \"$(date -Iseconds)\"," >> "$usage_report"
    echo "  \"datasets\": [" >> "$usage_report"
    
    local first_dataset=true
    
    # Get all datasets with quotas
    zfs list -H -o name,used,avail,quota,refquota,usedsnap,usedrefreserv | while IFS=$'\t' read -r name used avail quota refquota usedsnap usedrefreserv; do
        # Skip if no quota set
        [[ "$quota" == "-" && "$refquota" == "-" ]] && continue
        
        [[ "$first_dataset" != "true" ]] && echo "    }," >> "$usage_report"
        first_dataset=false
        
        echo "    {" >> "$usage_report"
        echo "      \"name\": \"$name\"," >> "$usage_report"
        echo "      \"used\": \"$used\"," >> "$usage_report"
        echo "      \"available\": \"$avail\"," >> "$usage_report"
        echo "      \"quota\": \"$quota\"," >> "$usage_report"
        echo "      \"refquota\": \"$refquota\"," >> "$usage_report"
        echo "      \"snapshot_usage\": \"$usedsnap\"," >> "$usage_report"
        echo "      \"reservation_usage\": \"$usedrefreserv\"" >> "$usage_report"
        
        # Calculate usage percentage
        if [[ "$quota" != "-" ]]; then
            local quota_bytes=$(numfmt --from=iec "$quota" 2>/dev/null || echo "0")
            local used_bytes=$(numfmt --from=iec "$used" 2>/dev/null || echo "0")
            if [[ $quota_bytes -gt 0 ]]; then
                local usage_percent=$(echo "scale=2; $used_bytes / $quota_bytes * 100" | bc -l)
                echo "      \"quota_usage_percent\": $usage_percent" >> "$usage_report"
            fi
        fi
    done
    
    echo "    }" >> "$usage_report"
    echo "  ]" >> "$usage_report"
    echo "}" >> "$usage_report"
    
    log_monitor "Dataset usage monitoring completed: $usage_report"
}

# Performance metrics collection
collect_performance_metrics() {
    log_monitor "Collecting ZFS performance metrics"
    
    local metrics_file="$STATUS_DIR/performance-metrics-$(date +%Y%m%d_%H%M%S).json"
    
    # ARC statistics
    local arc_stats=$(awk '
    /^hits/ {hits = $3}
    /^misses/ {misses = $3}
    /^size/ {size = $3}
    /^c_max/ {c_max = $3}
    /^mru_size/ {mru_size = $3}
    /^mfu_size/ {mfu_size = $3}
    END {
        hit_rate = (hits + misses > 0) ? hits / (hits + misses) * 100 : 0
        printf "{\"hits\":%d,\"misses\":%d,\"hit_rate\":%.2f,\"size\":%d,\"max_size\":%d,\"mru_size\":%d,\"mfu_size\":%d}", 
               hits, misses, hit_rate, size, c_max, mru_size, mfu_size
    }' /proc/spl/kstat/zfs/arcstats)
    
    # L2ARC statistics
    local l2arc_stats=$(awk '
    /^l2_hits/ {l2_hits = $3}
    /^l2_misses/ {l2_misses = $3}
    /^l2_size/ {l2_size = $3}
    END {
        l2_hit_rate = (l2_hits + l2_misses > 0) ? l2_hits / (l2_hits + l2_misses) * 100 : 0
        printf "{\"hits\":%d,\"misses\":%d,\"hit_rate\":%.2f,\"size\":%d}", 
               l2_hits, l2_misses, l2_hit_rate, l2_size
    }' /proc/spl/kstat/zfs/arcstats)
    
    # Create metrics JSON
    cat > "$metrics_file" << EOF
{
  "timestamp": "$(date -Iseconds)",
  "arc": $arc_stats,
  "l2arc": $l2arc_stats,
  "system": {
    "memory_total": $(grep MemTotal /proc/meminfo | awk '{print $2 * 1024}'),
    "memory_available": $(grep MemAvailable /proc/meminfo | awk '{print $2 * 1024}'),
    "load_average": "$(uptime | awk -F'load average:' '{print $2}' | sed 's/^[[:space:]]*//')"
  }
}
EOF
    
    log_monitor "Performance metrics collected: $metrics_file"
}

# Automated monitoring setup
setup_monitoring_automation() {
    log_monitor "Setting up automated monitoring"
    
    # Create comprehensive monitoring script
    cat > /tmp/zfs-monitor-runner.sh << 'EOF'
#!/bin/bash
# ZFS Automated Monitoring Runner

/usr/local/bin/zfs-monitoring-system.sh check_pool_health
/usr/local/bin/zfs-monitoring-system.sh monitor_dataset_usage
/usr/local/bin/zfs-monitoring-system.sh collect_performance_metrics

# Cleanup old monitoring files (keep 30 days)
find /var/lib/zfs/status -name "*.json" -mtime +30 -delete
find /var/log -name "zfs-*.log" -mtime +30 -delete
EOF
    
    sudo mv /tmp/zfs-monitor-runner.sh /usr/local/bin/zfs-monitor-runner.sh
    sudo chmod +x /usr/local/bin/zfs-monitor-runner.sh
    
    # Create cron jobs
    cat > /tmp/zfs-monitoring-crontab << 'EOF'
# ZFS Comprehensive Monitoring
# Health check every 15 minutes
*/15 * * * * /usr/local/bin/zfs-monitoring-system.sh check_pool_health

# Dataset usage monitoring every hour
0 * * * * /usr/local/bin/zfs-monitoring-system.sh monitor_dataset_usage

# Performance metrics every 5 minutes
*/5 * * * * /usr/local/bin/zfs-monitoring-system.sh collect_performance_metrics

# Comprehensive monitoring run daily at 6 AM
0 6 * * * /usr/local/bin/zfs-monitor-runner.sh

EOF
    
    sudo crontab /tmp/zfs-monitoring-crontab
    
    log_monitor "Automated monitoring setup completed"
}

# Initialize monitoring system
initialize_monitoring
setup_monitoring_automation

log_monitor "ZFS monitoring and diagnostics system ready"
```

## Lab Exercises

### Lab 1: Enterprise ZFS Pool Architecture
**Objective**: Design and implement a multi-tier ZFS storage architecture for a corporate environment.

**Scenario**: You are implementing storage for a company with the following requirements:
- High-performance database storage (10TB)
- General file server storage (50TB)
- Backup storage with maximum compression (100TB)
- Development environment storage (20TB)

**Tasks**:
1. **Plan Pool Architecture**:
   ```bash
   # Document your pool design decisions
   # Consider RAID levels, device types, and performance characteristics
   
   # Database pool - RAID-10 for performance
   # File server pool - RAID-Z2 for capacity and redundancy
   # Backup pool - RAID-Z3 for maximum data protection
   # Development pool - RAID-Z1 for cost efficiency
   ```

2. **Create Storage Pools**:
   ```bash
   # Create database pool with NVMe devices
   sudo zpool create db-pool mirror \
       /dev/nvme0n1 /dev/nvme1n1 \
       mirror /dev/nvme2n1 /dev/nvme3n1
   
   # Create file server pool with large drives
   sudo zpool create fileserver-pool raidz2 \
       /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg
   
   # Create backup pool with maximum redundancy
   sudo zpool create backup-pool raidz3 \
       /dev/sdh /dev/sdi /dev/sdj /dev/sdk /dev/sdl /dev/sdm /dev/sdn
   
   # Create development pool
   sudo zpool create dev-pool raidz \
       /dev/sdo /dev/sdp /dev/sdq /dev/sdr
   ```

3. **Configure Pool Properties**:
   ```bash
   # Database pool optimization
   sudo zfs set ashift=12 db-pool
   sudo zfs set compression=lz4 db-pool
   sudo zfs set atime=off db-pool
   
   # File server optimization
   sudo zfs set compression=zstd fileserver-pool
   sudo zfs set atime=off fileserver-pool
   
   # Backup pool optimization
   sudo zfs set compression=zstd-19 backup-pool
   sudo zfs set atime=off backup-pool
   
   # Development pool optimization
   sudo zfs set compression=lz4 dev-pool
   sudo zfs set sync=disabled dev-pool
   ```

4. **Add Hot Spares and Cache Devices**:
   ```bash
   # Add hot spares to critical pools
   sudo zpool add db-pool spare /dev/nvme4n1
   sudo zpool add fileserver-pool spare /dev/sds /dev/sdt
   
   # Add L2ARC cache devices
   sudo zpool add db-pool cache /dev/nvme5n1
   sudo zpool add fileserver-pool cache /dev/sdu
   
   # Add SLOG devices for synchronous writes
   sudo zpool add db-pool log mirror /dev/nvme6n1 /dev/nvme7n1
   ```

**Verification**:
```bash
# Verify pool configuration
zpool list
zpool status -v
zfs list

# Test performance characteristics
dd if=/dev/zero of=/db-pool/test-db bs=8K count=10000 oflag=sync
dd if=/dev/zero of=/fileserver-pool/test-file bs=1M count=1000
```

### Lab 2: Advanced Dataset Management and Delegation
**Objective**: Implement a hierarchical dataset structure with user quotas and administrative delegation.

**Tasks**:
1. **Create Corporate Dataset Hierarchy**:
   ```bash
   # Corporate structure
   sudo zfs create fileserver-pool/corporate
   sudo zfs create fileserver-pool/corporate/departments
   sudo zfs create fileserver-pool/corporate/departments/engineering
   sudo zfs create fileserver-pool/corporate/departments/marketing
   sudo zfs create fileserver-pool/corporate/departments/finance
   sudo zfs create fileserver-pool/corporate/departments/hr
   
   # Project structure
   sudo zfs create fileserver-pool/projects
   sudo zfs create fileserver-pool/projects/active
   sudo zfs create fileserver-pool/projects/archived
   sudo zfs create fileserver-pool/projects/development
   
   # User homes
   sudo zfs create fileserver-pool/users
   sudo zfs create fileserver-pool/users/homes
   sudo zfs create fileserver-pool/users/profiles
   
   # Shared resources
   sudo zfs create fileserver-pool/shared
   sudo zfs create fileserver-pool/shared/templates
   sudo zfs create fileserver-pool/shared/software
   ```

2. **Configure Quotas and Reservations**:
   ```bash
   # Department quotas
   sudo zfs set quota=10G fileserver-pool/corporate/departments/engineering
   sudo zfs set quota=5G fileserver-pool/corporate/departments/marketing
   sudo zfs set quota=3G fileserver-pool/corporate/departments/finance
   sudo zfs set quota=2G fileserver-pool/corporate/departments/hr
   
   # Project quotas
   sudo zfs set quota=50G fileserver-pool/projects/active
   sudo zfs set quota=100G fileserver-pool/projects/archived
   sudo zfs set quota=20G fileserver-pool/projects/development
   
   # User quota template
   sudo zfs set quota=1G fileserver-pool/users/homes
   sudo zfs set refquota=500M fileserver-pool/users/profiles
   
   # Reserve space for critical data
   sudo zfs set reservation=5G fileserver-pool/corporate/departments/finance
   ```

3. **Implement Administrative Delegation**:
   ```bash
   # Create departmental admin users
   sudo useradd -m engadmin
   sudo useradd -m mktadmin
   sudo useradd -m finadmin
   
   # Grant department-specific permissions
   sudo zfs allow -u engadmin create,destroy,mount,snapshot,rollback,clone,promote,rename fileserver-pool/corporate/departments/engineering
   sudo zfs allow -u mktadmin create,destroy,mount,snapshot,rollback fileserver-pool/corporate/departments/marketing
   sudo zfs allow -u finadmin create,mount,snapshot fileserver-pool/corporate/departments/finance
   
   # Grant project management permissions
   sudo zfs allow -g projectmanagers create,destroy,mount,snapshot,rollback,clone fileserver-pool/projects
   
   # Create user management delegation
   sudo zfs allow -u useradmin create,destroy,mount,quota,refquota fileserver-pool/users/homes
   ```

4. **Create User Datasets with Automated Provisioning**:
   ```bash
   # User provisioning script
   #!/bin/bash
   # provision-user.sh
   
   USERNAME="$1"
   QUOTA="${2:-1G}"
   
   # Create user dataset
   sudo zfs create "fileserver-pool/users/homes/$USERNAME"
   sudo zfs set quota="$QUOTA" "fileserver-pool/users/homes/$USERNAME"
   sudo zfs set mountpoint="/home/$USERNAME" "fileserver-pool/users/homes/$USERNAME"
   
   # Set ownership
   sudo chown "$USERNAME:$USERNAME" "/home/$USERNAME"
   sudo chmod 750 "/home/$USERNAME"
   
   # Create initial snapshot
   sudo zfs snapshot "fileserver-pool/users/homes/$USERNAME@initial"
   
   echo "User $USERNAME provisioned with $QUOTA quota"
   ```

**Verification**:
```bash
# Test delegation
sudo -u engadmin zfs create fileserver-pool/corporate/departments/engineering/test-project
sudo -u engadmin zfs snapshot fileserver-pool/corporate/departments/engineering/test-project@milestone1

# Check quotas
zfs list -o name,used,quota,refquota -r fileserver-pool

# Verify permissions
zfs allow fileserver-pool/corporate/departments/engineering
```

### Lab 3: Snapshot Management and Recovery Procedures
**Objective**: Implement automated snapshot policies and practice disaster recovery scenarios.

**Tasks**:
1. **Implement Automated Snapshot Policies**:
   ```bash
   # Create snapshot policy configuration
   sudo mkdir -p /etc/zfs/snapshot-policies
   
   cat > /etc/zfs/snapshot-policies/corporate.conf << 'EOF'
   # Corporate data snapshots
   fileserver-pool/corporate:hourly:24:corp-hourly
   fileserver-pool/corporate:daily:30:corp-daily
   fileserver-pool/corporate:weekly:12:corp-weekly
   fileserver-pool/corporate:monthly:12:corp-monthly
   EOF
   
   cat > /etc/zfs/snapshot-policies/projects.conf << 'EOF'
   # Project data snapshots
   fileserver-pool/projects/active:15min:96:proj-15min
   fileserver-pool/projects/active:hourly:48:proj-hourly
   fileserver-pool/projects/active:daily:14:proj-daily
   fileserver-pool/projects/development:hourly:24:dev-hourly
   fileserver-pool/projects/development:daily:7:dev-daily
   EOF
   
   # Create snapshot automation script
   sudo cp /usr/local/bin/zfs-snapshot-manager.sh /usr/local/bin/
   sudo chmod +x /usr/local/bin/zfs-snapshot-manager.sh
   ```

2. **Test Snapshot Operations**:
   ```bash
   # Create test data
   sudo zfs create fileserver-pool/test-recovery
   sudo mkdir /fileserver-pool/test-recovery/documents
   echo "Original data v1" | sudo tee /fileserver-pool/test-recovery/documents/file1.txt
   echo "Original data v1" | sudo tee /fileserver-pool/test-recovery/documents/file2.txt
   
   # Create baseline snapshot
   sudo zfs snapshot fileserver-pool/test-recovery@baseline
   
   # Modify data
   echo "Modified data v2" | sudo tee /fileserver-pool/test-recovery/documents/file1.txt
   echo "Modified data v2" | sudo tee /fileserver-pool/test-recovery/documents/file3.txt
   sudo rm /fileserver-pool/test-recovery/documents/file2.txt
   
   # Create second snapshot
   sudo zfs snapshot fileserver-pool/test-recovery@after-changes
   
   # Practice point-in-time recovery
   sudo zfs rollback fileserver-pool/test-recovery@baseline
   
   # Verify recovery
   ls -la /fileserver-pool/test-recovery/documents/
   cat /fileserver-pool/test-recovery/documents/file1.txt
   ```

3. **Implement Snapshot Browsing**:
   ```bash
   # Enable snapshot visibility
   sudo zfs set snapdir=visible fileserver-pool/test-recovery
   
   # Browse snapshots
   ls /fileserver-pool/test-recovery/.zfs/snapshot/
   ls /fileserver-pool/test-recovery/.zfs/snapshot/baseline/documents/
   
   # Selective file recovery
   sudo cp /fileserver-pool/test-recovery/.zfs/snapshot/after-changes/documents/file3.txt \
          /fileserver-pool/test-recovery/documents/
   ```

4. **Clone Management for Development**:
   ```bash
   # Create development clone from production snapshot
   sudo zfs clone fileserver-pool/projects/active@proj-daily_$(date +%Y%m%d) \
                 fileserver-pool/projects/development/test-clone-$(date +%Y%m%d)
   
   # Configure clone for development use
   sudo zfs set quota=5G fileserver-pool/projects/development/test-clone-$(date +%Y%m%d)
   sudo zfs set sync=disabled fileserver-pool/projects/development/test-clone-$(date +%Y%m%d)
   
   # Set expiration for automatic cleanup
   sudo zfs set com.company:expires="$(date -d '+7 days' +%Y-%m-%d)" \
       fileserver-pool/projects/development/test-clone-$(date +%Y%m%d)
   ```

**Verification**:
```bash
# Verify snapshot policies
/usr/local/bin/zfs-snapshot-manager.sh create_scheduled_snapshots daily

# Check snapshot history
zfs list -t snapshot -r fileserver-pool/test-recovery

# Verify clone functionality
zfs list -t filesystem -r fileserver-pool/projects/development
```

### Lab 4: ZFS Replication and Disaster Recovery
**Objective**: Set up cross-site replication and practice disaster recovery failover procedures.

**Prerequisites**: Two systems or VMs representing primary and DR sites.

**Tasks**:
1. **Configure SSH Key Authentication**:
   ```bash
   # On primary site
   ssh-keygen -t ed25519 -f ~/.ssh/zfs-replication
   ssh-copy-id -i ~/.ssh/zfs-replication.pub root@dr-site
   
   # Test connectivity
   ssh -i ~/.ssh/zfs-replication root@dr-site "zfs list"
   ```

2. **Perform Initial Replication Setup**:
   ```bash
   # Create initial snapshot on primary
   sudo zfs snapshot -r fileserver-pool/corporate@initial-replication
   
   # Send initial replication to DR site
   sudo zfs send -R fileserver-pool/corporate@initial-replication | \
   ssh root@dr-site "zfs receive -F dr-pool/corporate"
   
   # Verify replication
   ssh root@dr-site "zfs list -r dr-pool/corporate"
   ```

3. **Set Up Incremental Replication**:
   ```bash
   # Create automation script for incremental replication
   cat > /usr/local/bin/replicate-to-dr.sh << 'EOF'
   #!/bin/bash
   
   DATASETS=("fileserver-pool/corporate" "fileserver-pool/projects/active")
   DR_HOST="dr-site"
   DR_POOL="dr-pool"
   
   for dataset in "${DATASETS[@]}"; do
       # Find last common snapshot
       LAST_SNAP=$(zfs list -H -t snapshot -o name "$dataset" | \
                   grep "@repl-" | tail -1)
       
       # Create new replication snapshot
       NEW_SNAP="${dataset}@repl-$(date +%Y%m%d_%H%M%S)"
       zfs snapshot "$NEW_SNAP"
       
       # Send incremental
       if [[ -n "$LAST_SNAP" ]]; then
           zfs send -i "$LAST_SNAP" "$NEW_SNAP" | \
           ssh "$DR_HOST" "zfs receive -F ${DR_POOL}/${dataset#*/}"
       else
           zfs send "$NEW_SNAP" | \
           ssh "$DR_HOST" "zfs receive -F ${DR_POOL}/${dataset#*/}"
       fi
       
       echo "Replicated $dataset to DR site"
   done
   EOF
   
   sudo chmod +x /usr/local/bin/replicate-to-dr.sh
   ```

4. **Practice Disaster Recovery Failover**:
   ```bash
   # Simulate primary site failure
   # On DR site, promote replicated datasets for production use
   
   ssh root@dr-site << 'EOF'
   # Make datasets writable
   zfs set readonly=off dr-pool/corporate
   zfs set readonly=off dr-pool/projects/active
   
   # Update mount points for production use
   zfs set mountpoint=/corporate dr-pool/corporate
   zfs set mountpoint=/projects/active dr-pool/projects/active
   
   # Mount datasets
   zfs mount dr-pool/corporate
   zfs mount dr-pool/projects/active
   
   # Verify data accessibility
   ls -la /corporate/
   ls -la /projects/active/
   EOF
   ```

5. **Practice Failback Procedures**:
   ```bash
   # When primary site is restored, reverse replication
   # This would be done after fixing the primary site
   
   # From DR site, send latest data back to primary
   ssh root@dr-site "zfs snapshot -r dr-pool/corporate@failback-$(date +%Y%m%d)"
   ssh root@dr-site "zfs send -R dr-pool/corporate@failback-$(date +%Y%m%d)" | \
   zfs receive -F fileserver-pool/corporate-restored
   
   # Compare and merge data as needed
   ```

**Verification**:
```bash
# Verify replication lag
./usr/local/bin/zfs-replication-manager.sh monitor_replication_health

# Test incremental replication
/usr/local/bin/replicate-to-dr.sh

# Verify DR site data integrity
ssh root@dr-site "zfs list -t snapshot -r dr-pool"
```

### Lab 5: Performance Optimization and Monitoring
**Objective**: Implement comprehensive performance monitoring and optimize ZFS for different workloads.

**Tasks**:
1. **Baseline Performance Testing**:
   ```bash
   # Install performance testing tools
   sudo apt-get install fio sysbench

   # Test database workload simulation
   sudo fio --name=db-test --filename=/db-pool/fio-test \
            --rw=randrw --bs=8k --iodepth=32 --numjobs=4 \
            --runtime=300 --group_reporting --size=10G
   
   # Test file server workload
   sudo fio --name=fileserver-test --filename=/fileserver-pool/fio-test \
            --rw=read --bs=1M --iodepth=8 --numjobs=2 \
            --runtime=300 --group_reporting --size=50G
   
   # Test backup workload
   sudo fio --name=backup-test --filename=/backup-pool/fio-test \
            --rw=write --bs=1M --iodepth=1 --numjobs=1 \
            --runtime=300 --group_reporting --size=100G
   ```

2. **Monitor ZFS Performance Metrics**:
   ```bash
   # Run comprehensive performance monitoring
   /usr/local/bin/zfs-performance-optimizer.sh monitor_zfs_performance 600 10
   
   # Monitor ARC efficiency
   watch -n 5 'echo "ARC Stats:"; arcstat 1 1'
   
   # Monitor I/O patterns
   zpool iostat -v 5
   
   # Monitor transaction group performance
   echo "TXG Statistics:"
   cat /proc/spl/kstat/zfs/*/txgs
   ```

3. **Apply Workload-Specific Optimizations**:
   ```bash
   # Optimize for database workload
   /usr/local/bin/zfs-performance-optimizer.sh optimize_dataset_for_workload \
       "db-pool/mysql" "database"
   
   # Optimize for file server workload
   /usr/local/bin/zfs-performance-optimizer.sh optimize_dataset_for_workload \
       "fileserver-pool/shared" "fileserver"
   
   # Optimize for backup workload
   /usr/local/bin/zfs-performance-optimizer.sh optimize_dataset_for_workload \
       "backup-pool/archives" "backup"
   
   # Optimize for VM workload
   /usr/local/bin/zfs-performance-optimizer.sh optimize_dataset_for_workload \
       "fileserver-pool/vms" "vms"
   ```

4. **Implement Performance Alerting**:
   ```bash
   # Set up automated performance monitoring
   /usr/local/bin/zfs-performance-optimizer.sh setup_performance_alerts
   
   # Configure custom alert thresholds
   sudo sed -i 's/ALERT_THRESHOLD_ARC=85/ALERT_THRESHOLD_ARC=90/' \
       /usr/local/bin/zfs-performance-monitor.sh
   
   # Test alert system
   # Temporarily set very high threshold to trigger alert
   echo "Testing alert system..."
   ```

5. **Performance Tuning Validation**:
   ```bash
   # Re-run performance tests after optimization
   sudo fio --name=db-test-optimized --filename=/db-pool/mysql/fio-test \
            --rw=randrw --bs=8k --iodepth=32 --numjobs=4 \
            --runtime=300 --group_reporting --size=10G
   
   # Compare before and after results
   echo "Performance improvement analysis:"
   echo "Before optimization: [record baseline results]"
   echo "After optimization: [record optimized results]"
   
   # Generate performance report
   /usr/local/bin/zfs-performance-optimizer.sh generate_performance_report \
       /tmp/zfs-performance-*.log
   ```

**Verification**:
```bash
# Verify applied optimizations
zfs get all db-pool/mysql | grep -E "(recordsize|primarycache|sync|compression)"
zfs get all fileserver-pool/shared | grep -E "(recordsize|primarycache|sync|compression)"

# Check performance monitoring setup
crontab -l | grep performance
systemctl status zfs-performance-monitor

# Validate ARC settings
cat /sys/module/zfs/parameters/zfs_arc_max
cat /sys/module/zfs/parameters/zfs_arc_min
```

## Best Practices

### ZFS Pool Design
- **RAID Level Selection**: Use RAID-10 for high-performance workloads, RAID-Z2 for balanced capacity/performance, RAID-Z3 for maximum data protection
- **Device Sizing**: Use identically sized devices within each vdev for optimal space utilization
- **Hot Spares**: Configure at least one hot spare per pool, preferably matching the largest device size
- **L2ARC Sizing**: Size L2ARC devices at 5-10x the ARC size for optimal caching effectiveness

### Dataset Management
- **Hierarchy Planning**: Design dataset hierarchies to match organizational structure and access patterns
- **Quota Strategy**: Implement quotas proactively to prevent runaway disk usage
- **Compression Settings**: Enable compression on all datasets unless specifically contraindicated
- **Record Size Optimization**: Match record sizes to application I/O patterns (8K for databases, 1M for file servers)

### Snapshot and Backup Strategy
- **Automated Snapshots**: Implement automated snapshot policies based on data criticality and change frequency
- **Retention Policies**: Define clear retention policies balancing storage costs with recovery requirements
- **Replication Planning**: Set up regular replication to geographically separate locations
- **Recovery Testing**: Regularly test recovery procedures to ensure they work when needed

### Performance Optimization
- **ARC Tuning**: Size ARC appropriately for your workload, typically 50-75% of system RAM
- **Workload Matching**: Configure dataset properties to match specific workload characteristics
- **I/O Scheduler**: Use appropriate I/O schedulers (typically deadline or noop for SSDs)
- **Monitoring Integration**: Implement comprehensive monitoring to detect performance issues early

### Security and Access Control
- **Delegation Model**: Use ZFS delegation features to distribute administrative responsibilities
- **Encryption**: Enable encryption for sensitive datasets, especially on portable storage
- **Access Auditing**: Monitor and audit access to critical datasets
- **Network Security**: Secure replication channels with SSH keys and network restrictions

## Troubleshooting

### Common Issues and Solutions

#### Pool Performance Issues
**Symptoms**: Slow I/O performance, high latency
**Diagnosis**:
```bash
zpool iostat -v 5
iostat -x 1
cat /proc/spl/kstat/zfs/arcstats
```
**Solutions**:
- Check for device failures or high error rates
- Verify ARC hit rates (should be >90%)
- Consider adding L2ARC or SLOG devices
- Review record size settings for workload

#### Pool Import/Export Problems
**Symptoms**: Cannot import pool after system migration
**Diagnosis**:
```bash
zpool import
zpool import -f poolname
zdb -l /dev/device
```
**Solutions**:
- Use force import if pool was not cleanly exported
- Check device paths and update if necessary
- Verify all pool devices are accessible
- Use device IDs instead of device names for portability

#### Snapshot and Replication Issues
**Symptoms**: Replication failures, missing snapshots
**Diagnosis**:
```bash
zfs list -t snapshot
zfs send -n dataset@snapshot
ssh remotehost "zfs list -t snapshot"
```
**Solutions**:
- Verify network connectivity and SSH key authentication
- Check available space on destination pool
- Ensure consistent snapshot names across sites
- Validate incremental snapshot chains

#### Dataset Access Problems
**Symptoms**: Cannot access datasets, permission denied
**Diagnosis**:
```bash
zfs get mounted,mountpoint dataset
zfs mount
zfs allow dataset
mount | grep zfs
```
**Solutions**:
- Verify dataset is mounted
- Check mount point permissions
- Review ZFS delegation permissions
- Ensure no conflicting mount points

### Emergency Procedures

#### Pool Recovery
1. **Assess pool status**: `zpool status -v poolname`
2. **Attempt automatic repair**: `zpool clear poolname`
3. **Replace failed devices**: `zpool replace poolname old-device new-device`
4. **Force import if necessary**: `zpool import -f poolname`
5. **Restore from backup if pool is unrecoverable**

#### Data Recovery
1. **Check for available snapshots**: `zfs list -t snapshot`
2. **Browse snapshot contents**: `ls dataset/.zfs/snapshot/`
3. **Selective file restore**: Copy files from `.zfs/snapshot/`
4. **Full rollback if necessary**: `zfs rollback dataset@snapshot`
5. **Clone for investigation**: `zfs clone snapshot dataset/investigation`

## Assessment Criteria

### Knowledge Assessment
- **Pool Architecture**: Can design appropriate pool layouts for different use cases
- **Dataset Management**: Understands hierarchical dataset organization and quota management
- **Snapshot Strategy**: Can implement comprehensive snapshot and backup policies
- **Performance Tuning**: Knows how to optimize ZFS for different workloads
- **Replication Setup**: Can configure and manage ZFS replication infrastructure

### Practical Skills
- **Command Proficiency**: Demonstrates fluency with ZFS commands and options
- **Troubleshooting Ability**: Can diagnose and resolve common ZFS issues
- **Automation Implementation**: Can create scripts for ZFS management tasks
- **Monitoring Setup**: Can implement comprehensive ZFS monitoring solutions
- **Recovery Procedures**: Can execute disaster recovery and data restoration procedures

### Advanced Topics Understanding
- **Enterprise Integration**: Understands how ZFS fits into enterprise storage architectures
- **Scaling Considerations**: Knows limitations and scaling strategies for ZFS
- **Hybrid Storage**: Can implement hybrid storage solutions with ZFS
- **Performance Analysis**: Can analyze and optimize ZFS performance metrics
- **Security Implementation**: Understands ZFS security features and access control

## Next Steps

### Intermediate Topics
- ZFS on Linux (ZoL) specific features and limitations
- Integration with virtualization platforms (Proxmox, VMware)
- ZFS encryption and security hardening
- Advanced replication topologies and strategies
- ZFS performance benchmarking and analysis

### Advanced Topics
- ZFS storage clustering and distributed storage
- Integration with backup solutions (Bacula, Bareos, Veeam)
- ZFS tuning for specific applications (databases, virtualization)
- Custom ZFS monitoring and alerting solutions
- ZFS in cloud environments and hybrid storage

### Related Technologies
- **Module 12**: Proxmox Virtual Environment (ZFS integration)
- **Module 14**: Proxmox Infrastructure Automation (ZFS automation)
- BTRFS comparison and migration strategies
- Software-defined storage solutions
- Enterprise backup and disaster recovery planning

---

*This completes Module 11: ZFS Fundamentals. Students should now have comprehensive knowledge of ZFS storage management, from basic pool operations to enterprise-grade infrastructure implementation with monitoring, replication, and disaster recovery capabilities.*
    
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
