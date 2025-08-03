# Module 10: Storage & Filesystem Management

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [10.1 Storage Fundamentals and Partition Management](#101-storage-fundamentals-and-partition-management)
  - [10.2 Filesystem Creation and Advanced Tuning](#102-filesystem-creation-and-advanced-tuning)
  - [10.3 Logical Volume Manager (LVM) Deep Dive](#103-logical-volume-manager-lvm-deep-dive)
  - [10.4 Software and Hardware RAID Implementation](#104-software-and-hardware-raid-implementation)
  - [10.5 Storage Performance Optimization](#105-storage-performance-optimization)
  - [10.6 Backup and Recovery Strategies](#106-backup-and-recovery-strategies)
  - [10.7 Network Storage and Clustering](#107-network-storage-and-clustering)
  - [10.8 Storage Security and Encryption](#108-storage-security-and-encryption)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Partition Management](#partition-management)
  - [Filesystem Operations](#filesystem-operations)
  - [LVM Administration](#lvm-administration)
  - [RAID Configuration](#raid-configuration)
  - [Performance Optimization](#performance-optimization)
  - [Storage Security](#storage-security)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Advanced Partitioning and Filesystem Management](#lab-1-advanced-partitioning-and-filesystem-management)
  - [Lab 2: LVM Implementation and Management](#lab-2-lvm-implementation-and-management)
  - [Lab 3: RAID Configuration and Recovery](#lab-3-raid-configuration-and-recovery)
  - [Lab 4: Storage Performance Optimization](#lab-4-storage-performance-optimization)
  - [Lab 5: Enterprise Storage Infrastructure](#lab-5-enterprise-storage-infrastructure)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
This module provides comprehensive coverage of enterprise-grade storage management and filesystem administration in Linux. Students will master advanced storage technologies including software and hardware RAID, Logical Volume Manager (LVM), and filesystem optimization techniques. The curriculum emphasizes hands-on experience with real-world scenarios, balancing performance optimization with data integrity and disaster recovery capabilities.

**Key Learning Outcomes:**
- Design and implement resilient storage architectures using RAID and LVM
- Optimize filesystem performance for specific workloads and use cases
- Manage live storage operations without system downtime
- Implement comprehensive backup and recovery strategies
- Configure network storage solutions and clustering technologies
- Secure storage systems with encryption and access controls

## Learning Objectives
By the end of this module, you will be able to:

1. **Master Partition Management**: Create, modify, and recover partition tables using fdisk, gdisk, and parted across MBR and GPT schemes
2. **Optimize Filesystem Performance**: Select appropriate filesystems and configure mount options for maximum performance and reliability
3. **Implement LVM Solutions**: Design and manage logical volumes with snapshots, thin provisioning, and live resizing capabilities
4. **Configure RAID Arrays**: Build and maintain software and hardware RAID configurations with comprehensive failure recovery procedures
5. **Optimize Storage Performance**: Analyze and tune storage subsystems for specific workload requirements and performance characteristics
6. **Design Backup Strategies**: Implement enterprise backup and disaster recovery solutions with automated testing and validation

## Topics

### 10.1 Storage Fundamentals and Partition Management
- Block device architecture and storage hierarchy mapping
- Partition table comparison: MBR vs GPT advantages and limitations
- Advanced partitioning tools: fdisk, gdisk, parted, and cfdisk
- Partition alignment and performance optimization strategies
- Partition table recovery and disaster recovery procedures
- Device naming conventions and persistent identification methods

### 10.2 Filesystem Creation and Advanced Tuning
- Comprehensive filesystem comparison: ext4, XFS, Btrfs, and ZFS
- Filesystem creation parameters and optimization techniques
- Mount options for performance: noatime, barriers, data modes, and compression
- UUID and label management for persistent device identification
- Filesystem maintenance: checking, repair, defragmentation, and optimization
- Performance monitoring and capacity planning strategies

### 10.3 Logical Volume Manager (LVM) Deep Dive
- LVM architecture: Physical Volumes, Volume Groups, and Logical Volumes
- Live system operations: extending, shrinking, and migrating volumes
- LVM snapshots: creation, management, and backup integration
- Advanced features: thin provisioning, cache volumes, and RAID LVs
- LVM troubleshooting and recovery procedures
- Performance optimization and capacity management

### 10.4 Software and Hardware RAID Implementation
- RAID level analysis: RAID 0, 1, 5, 6, 10 performance and resilience characteristics
- Software RAID with mdadm: creation, monitoring, and maintenance
- Hardware RAID configuration and management interfaces
- RAID failure detection, hot spare configuration, and replacement procedures
- RAID performance optimization: chunk sizes, read-ahead, and stripe configuration
- RAID disaster recovery and data reconstruction techniques

### 10.5 Storage Performance Optimization
- I/O pattern analysis and workload characterization
- Storage subsystem tuning: scheduler selection and queue optimization
- SSD optimization: TRIM support, over-provisioning, and wear leveling
- Cache configuration and buffer management
- Performance monitoring tools and metrics analysis
- Capacity planning and growth prediction modeling

### 10.6 Backup and Recovery Strategies
- Backup architecture design and strategy development
- Snapshot-based backup systems and point-in-time recovery
- Incremental and differential backup implementations
- Disaster recovery planning and testing procedures
- Backup validation and integrity verification
- Cloud backup integration and hybrid storage strategies

### 10.7 Network Storage and Clustering
- NFS configuration and performance optimization
- iSCSI target and initiator setup and management
- Shared storage clustering with GFS2 and OCFS2
- Storage area network (SAN) integration and management
- High availability storage configurations
- Load balancing and failover mechanisms

### 10.8 Storage Security and Encryption
- Full disk encryption with LUKS and dm-crypt
- File-level encryption and secure key management
- Access control and permission management
- Storage audit logging and compliance monitoring
- Secure erasure and data destruction procedures
- Regulatory compliance and data protection standards

## Essential Command Reference

### Storage Discovery and Analysis

| Command | Description | Example |
|---------|-------------|---------|
| `lsblk` | List block devices in tree format | `lsblk -f` |
| `blkid` | Display block device attributes | `blkid /dev/sda1` |
| `fdisk -l` | List disk partition tables | `fdisk -l /dev/sda` |
| `parted -l` | List partition information | `parted -l` |
| `lshw -class disk` | Show hardware disk information | `lshw -class disk -short` |
| `df -h` | Display filesystem disk space usage | `df -h` |
| `du -sh` | Show directory space usage | `du -sh /var/log` |

### Partitioning Operations

| Command | Description | Example |
|---------|-------------|---------|
| `fdisk /dev/sdX` | Interactive disk partitioning (MBR) | `fdisk /dev/sda` |
| `gdisk /dev/sdX` | Interactive disk partitioning (GPT) | `gdisk /dev/sda` |
| `parted /dev/sdX` | GNU parted partitioning tool | `parted /dev/sda print` |
| `cfdisk /dev/sdX` | Curses-based disk partitioning | `cfdisk /dev/sda` |
| `sfdisk -l` | Script-friendly disk partitioning | `sfdisk -l /dev/sda` |
| `partprobe` | Inform kernel of partition changes | `partprobe /dev/sda` |

### Filesystem Operations

| Command | Description | Example |
|---------|-------------|---------|
| `mkfs.ext4` | Create ext4 filesystem | `mkfs.ext4 /dev/sda1` |
| `mkfs.xfs` | Create XFS filesystem | `mkfs.xfs /dev/sda1` |
| `mkfs.btrfs` | Create Btrfs filesystem | `mkfs.btrfs /dev/sda1` |
| `mount` | Mount filesystem | `mount /dev/sda1 /mnt` |
| `umount` | Unmount filesystem | `umount /mnt` |
| `fsck` | Check and repair filesystem | `fsck.ext4 /dev/sda1` |
| `tune2fs` | Adjust ext2/3/4 parameters | `tune2fs -l /dev/sda1` |
| `xfs_admin` | Adjust XFS parameters | `xfs_admin -l /dev/sda1` |

### LVM Commands

| Command | Description | Example |
|---------|-------------|---------|
| `pvcreate` | Create physical volume | `pvcreate /dev/sda1` |
| `vgcreate` | Create volume group | `vgcreate vg01 /dev/sda1` |
| `lvcreate` | Create logical volume | `lvcreate -L 10G -n lv01 vg01` |
| `pvdisplay` | Show physical volume information | `pvdisplay /dev/sda1` |
| `vgdisplay` | Show volume group information | `vgdisplay vg01` |
| `lvdisplay` | Show logical volume information | `lvdisplay /dev/vg01/lv01` |
| `lvextend` | Extend logical volume | `lvextend -L +5G /dev/vg01/lv01` |
| `lvcreate -s` | Create LVM snapshot | `lvcreate -s -L 1G -n snap01 /dev/vg01/lv01` |

### RAID Management

| Command | Description | Example |
|---------|-------------|---------|
| `mdadm --create` | Create RAID array | `mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda1 /dev/sdb1` |
| `mdadm --detail` | Show RAID array details | `mdadm --detail /dev/md0` |
| `mdadm --examine` | Examine RAID superblock | `mdadm --examine /dev/sda1` |
| `mdadm --add` | Add device to array | `mdadm --add /dev/md0 /dev/sdc1` |
| `mdadm --remove` | Remove device from array | `mdadm --remove /dev/md0 /dev/sda1` |
| `mdadm --fail` | Mark device as failed | `mdadm --fail /dev/md0 /dev/sda1` |
| `cat /proc/mdstat` | Show RAID status | `cat /proc/mdstat` |

### Performance Monitoring

| Command | Description | Example |
|---------|-------------|---------|
| `iostat` | I/O statistics for devices | `iostat -x 1` |
| `iotop` | I/O usage by processes | `iotop -o` |
| `sar -d` | Disk activity report | `sar -d 1 5` |
| `hdparm` | Get/set disk parameters | `hdparm -I /dev/sda` |
| `smartctl` | Control SMART monitoring | `smartctl -a /dev/sda` |
| `fio` | Flexible I/O tester | `fio --name=test --rw=read --size=1G` |

### Storage Security

| Command | Description | Example |
|---------|-------------|---------|
| `cryptsetup` | LUKS encryption management | `cryptsetup luksFormat /dev/sda1` |
| `setfacl` | Set file access control lists | `setfacl -m u:user:rw file.txt` |
| `getfacl` | Get file access control lists | `getfacl file.txt` |
| `quotacheck` | Build quota database files | `quotacheck -cug /home` |
| `quotaon` | Enable filesystem quotas | `quotaon /home` |
| `edquota` | Edit user quotas | `edquota username` |
| `shred` | Securely delete files | `shred -vfz -n 3 file.txt` |

## Practical Examples

### Partition Management

#### Advanced GPT Partitioning with gdisk
```bash
#!/bin/bash
# advanced-partitioning.sh - Enterprise disk partitioning script

DISK="/dev/sdb"
LOG_FILE="/var/log/partition-setup.log"

log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

create_gpt_layout() {
    local disk="$1"
    
    log_message "Starting GPT partitioning on $disk"
    
    # Backup existing partition table
    sudo sgdisk --backup="/tmp/$(basename $disk).backup" "$disk"
    
    # Create new GPT partition table
    sudo sgdisk --zap-all "$disk"
    
    # Create partitions with optimal alignment
    sudo sgdisk --new=1:2048:+512M --typecode=1:ef00 --change-name=1:"EFI System" "$disk"
    sudo sgdisk --new=2:0:+1G --typecode=2:8300 --change-name=2:"Boot" "$disk"
    sudo sgdisk --new=3:0:+2G --typecode=3:8200 --change-name=3:"Swap" "$disk"
    sudo sgdisk --new=4:0:0 --typecode=4:8e00 --change-name=4:"LVM" "$disk"
    
    # Verify partition alignment
    sudo sgdisk --verify "$disk"
    
    # Display final layout
    sudo sgdisk --print "$disk"
    
    log_message "GPT partitioning completed successfully"
}

# Partition alignment verification
check_alignment() {
    local disk="$1"
    
    log_message "Checking partition alignment for $disk"
    
    for partition in ${disk}[1-9]; do
        if [[ -e "$partition" ]]; then
            start_sector=$(sudo sgdisk --info=1 "$disk" | grep "First sector" | awk '{print $3}')
            if (( start_sector % 2048 == 0 )); then
                log_message "Partition $partition: Properly aligned (start: $start_sector)"
            else
                log_message "WARNING: Partition $partition: Misaligned (start: $start_sector)"
            fi
        fi
    done
}

# Performance optimization setup
optimize_partitions() {
    local disk="$1"
    
    log_message "Applying performance optimizations"
    
    # Set optimal I/O scheduler for SSDs
    if sudo smartctl -a "$disk" | grep -q "Solid State"; then
        echo "none" | sudo tee "/sys/block/$(basename $disk)/queue/scheduler"
        log_message "Set 'none' scheduler for SSD $disk"
    else
        echo "mq-deadline" | sudo tee "/sys/block/$(basename $disk)/queue/scheduler"
        log_message "Set 'mq-deadline' scheduler for HDD $disk"
    fi
    
    # Optimize read-ahead settings
    sudo blockdev --setra 256 "$disk"
    log_message "Set read-ahead to 256 sectors for $disk"
}

# Execute partitioning workflow
if [[ -b "$DISK" ]]; then
    create_gpt_layout "$DISK"
    check_alignment "$DISK"
    optimize_partitions "$DISK"
    
    # Update kernel partition table
    sudo partprobe "$DISK"
    sleep 2
    
    log_message "Partition setup workflow completed"
else
    log_message "ERROR: Disk $DISK not found or not a block device"
    exit 1
fi
```

#### MBR to GPT Conversion
```bash
#!/bin/bash
# mbr-to-gpt-conversion.sh - Safe MBR to GPT conversion

DISK="/dev/sdc"
BACKUP_DIR="/backup/partition-tables"

perform_conversion() {
    local disk="$1"
    
    # Create backup directory
    sudo mkdir -p "$BACKUP_DIR"
    
    # Backup MBR and partition table
    sudo dd if="$disk" of="$BACKUP_DIR/$(basename $disk)-mbr.backup" bs=512 count=1
    sudo sfdisk -d "$disk" > "$BACKUP_DIR/$(basename $disk)-layout.backup"
    
    echo "Backing up current MBR and partition layout..."
    
    # Check if conversion is safe
    if sudo sgdisk --verify "$disk" 2>/dev/null; then
        echo "Disk already has GPT partition table"
        exit 0
    fi
    
    # Perform conversion
    echo "Converting MBR to GPT..."
    sudo sgdisk --mbrtogpt "$disk"
    
    # Verify conversion
    if sudo sgdisk --verify "$disk"; then
        echo "Conversion successful!"
        sudo sgdisk --print "$disk"
    else
        echo "Conversion failed! Restoring from backup..."
        sudo dd if="$BACKUP_DIR/$(basename $disk)-mbr.backup" of="$disk" bs=512 count=1
        exit 1
    fi
}

perform_conversion "$DISK"
```

### Filesystem Operations

#### Advanced Filesystem Creation and Tuning
```bash
#!/bin/bash
# filesystem-optimization.sh - Optimized filesystem creation

create_optimized_ext4() {
    local device="$1"
    local mount_point="$2"
    local workload="$3"  # database, web, general
    
    case "$workload" in
        "database")
            # Database optimizations: larger block size, fewer inodes
            sudo mkfs.ext4 -b 4096 -i 16384 -E stride=32,stripe-width=64 \
                          -O ^has_journal,extent,flex_bg \
                          -L "database" "$device"
            mount_opts="noatime,nodev,data=writeback,barrier=0,nobh"
            ;;
        "web")
            # Web server optimizations: balanced performance
            sudo mkfs.ext4 -b 4096 -i 8192 -E stride=16,stripe-width=32 \
                          -O extent,flex_bg \
                          -L "webserver" "$device"
            mount_opts="noatime,nodev,data=ordered,barrier=1"
            ;;
        "general"|*)
            # General purpose optimizations
            sudo mkfs.ext4 -b 4096 -i 4096 -E stride=8,stripe-width=16 \
                          -O extent,flex_bg,dir_index \
                          -L "general" "$device"
            mount_opts="noatime,data=ordered,barrier=1"
            ;;
    esac
    
    # Create mount point and mount with optimized options
    sudo mkdir -p "$mount_point"
    echo "$device $mount_point ext4 $mount_opts 0 2" | sudo tee -a /etc/fstab
    sudo mount "$mount_point"
    
    echo "Created optimized ext4 filesystem for $workload workload"
    sudo tune2fs -l "$device" | grep -E "(Block size|Inode size|Journal|Features)"
}

create_optimized_xfs() {
    local device="$1"
    local mount_point="$2"
    local raid_setup="$3"  # none, raid0, raid10
    
    case "$raid_setup" in
        "raid0")
            # RAID 0 optimizations
            sudo mkfs.xfs -f -d agcount=8,sunit=64,swidth=128 \
                         -l size=128m -n size=64k \
                         -L "xfs_raid0" "$device"
            mount_opts="noatime,largeio,swalloc,allocsize=16m"
            ;;
        "raid10")
            # RAID 10 optimizations  
            sudo mkfs.xfs -f -d agcount=16,sunit=64,swidth=256 \
                         -l size=256m -n size=64k \
                         -L "xfs_raid10" "$device"
            mount_opts="noatime,largeio,swalloc,allocsize=32m"
            ;;
        "none"|*)
            # Single disk optimizations
            sudo mkfs.xfs -f -d agcount=4 -l size=64m -n size=64k \
                         -L "xfs_single" "$device"
            mount_opts="noatime,largeio"
            ;;
    esac
    
    # Mount with optimized options
    sudo mkdir -p "$mount_point"
    echo "$device $mount_point xfs $mount_opts 0 2" | sudo tee -a /etc/fstab
    sudo mount "$mount_point"
    
    echo "Created optimized XFS filesystem for $raid_setup configuration"
    sudo xfs_info "$mount_point"
}

# Example usage
create_optimized_ext4 "/dev/sdb1" "/var/lib/mysql" "database"
create_optimized_xfs "/dev/md0" "/data" "raid10"
```

#### Filesystem Performance Analysis
```bash
#!/bin/bash
# filesystem-benchmark.sh - Comprehensive filesystem performance testing

MOUNT_POINT="/data"
TEST_SIZE="1G"
RESULTS_DIR="/tmp/benchmark-results"

run_filesystem_benchmark() {
    local mount_point="$1"
    local test_size="$2"
    
    mkdir -p "$RESULTS_DIR"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    local results_file="$RESULTS_DIR/benchmark_${timestamp}.txt"
    
    echo "=== Filesystem Benchmark Results ===" > "$results_file"
    echo "Mount Point: $mount_point" >> "$results_file"
    echo "Test Size: $test_size" >> "$results_file"
    echo "Date: $(date)" >> "$results_file"
    echo "" >> "$results_file"
    
    # Sequential read/write performance
    echo "Running sequential I/O tests..." | tee -a "$results_file"
    
    # Sequential write
    echo "Sequential Write Test:" >> "$results_file"
    dd if=/dev/zero of="$mount_point/test_seq_write" bs=1M count=1024 conv=fsync 2>&1 | \
        grep -E "(copied|MB/s)" >> "$results_file"
    
    # Sequential read
    echo "Sequential Read Test:" >> "$results_file"
    dd if="$mount_point/test_seq_write" of=/dev/null bs=1M 2>&1 | \
        grep -E "(copied|MB/s)" >> "$results_file"
    
    # Random I/O performance with fio
    echo "Running random I/O tests..." | tee -a "$results_file"
    
    # Random read
    fio --name=random_read --directory="$mount_point" --rw=randread \
        --bs=4k --size="$test_size" --numjobs=4 --runtime=60 \
        --group_reporting --output-format=normal >> "$results_file"
    
    # Random write
    fio --name=random_write --directory="$mount_point" --rw=randwrite \
        --bs=4k --size="$test_size" --numjobs=4 --runtime=60 \
        --group_reporting --output-format=normal >> "$results_file"
    
    # Mixed workload
    fio --name=mixed_workload --directory="$mount_point" --rw=randrw \
        --bs=4k --size="$test_size" --numjobs=4 --runtime=60 \
        --rwmixread=70 --group_reporting --output-format=normal >> "$results_file"
    
    # Cleanup test files
    rm -f "$mount_point"/test_*
    rm -f "$mount_point"/*.fio.*
    
    echo "Benchmark completed. Results saved to: $results_file"
    
    # Display summary
    echo ""
    echo "=== Performance Summary ==="
    grep -E "(WRITE:|READ:|mixed)" "$results_file" | tail -10
}

# Filesystem-specific optimizations analysis
analyze_filesystem_performance() {
    local mount_point="$1"
    
    echo "=== Filesystem Analysis ==="
    
    # Get filesystem type and mount options
    local fs_info=$(findmnt -n -o FSTYPE,OPTIONS "$mount_point")
    echo "Filesystem: $fs_info"
    
    # Check for performance-impacting mount options
    if echo "$fs_info" | grep -q "noatime"; then
        echo "✓ noatime option detected (good for performance)"
    else
        echo "⚠ atime updates enabled (may impact performance)"
    fi
    
    if echo "$fs_info" | grep -q "barrier=0"; then
        echo "⚠ Write barriers disabled (performance gain but data risk)"
    else
        echo "✓ Write barriers enabled (safer but slower)"
    fi
    
    # Check I/O scheduler
    local device=$(findmnt -n -o SOURCE "$mount_point" | sed 's/[0-9]*$//')
    local scheduler=$(cat "/sys/block/$(basename $device)/queue/scheduler" 2>/dev/null)
    echo "I/O Scheduler: $scheduler"
    
    # Check read-ahead settings
    local readahead=$(blockdev --getra "$device" 2>/dev/null)
    echo "Read-ahead: $readahead sectors"
}

# Execute comprehensive benchmark
run_filesystem_benchmark "$MOUNT_POINT" "$TEST_SIZE"
analyze_filesystem_performance "$MOUNT_POINT"
```

### LVM Administration

#### Advanced LVM Operations
```bash
#!/bin/bash
# advanced-lvm-operations.sh - Enterprise LVM management

VG_NAME="vg_data"
SNAPSHOT_SIZE="10G"
LOG_FILE="/var/log/lvm-operations.log"

log_operation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

# Create comprehensive LVM setup
create_lvm_infrastructure() {
    local disks=("$@")
    
    log_operation "Starting LVM infrastructure creation"
    
    # Create physical volumes with optimal alignment
    for disk in "${disks[@]}"; do
        log_operation "Creating PV on $disk"
        sudo pvcreate --dataalignment 1M "$disk"
        
        # Verify PV creation
        if sudo pvdisplay "$disk" &>/dev/null; then
            log_operation "PV created successfully on $disk"
        else
            log_operation "ERROR: Failed to create PV on $disk"
            exit 1
        fi
    done
    
    # Create volume group with optimal extent size
    log_operation "Creating volume group $VG_NAME"
    sudo vgcreate -s 32M "$VG_NAME" "${disks[@]}"
    
    # Display VG information
    sudo vgdisplay "$VG_NAME"
    log_operation "Volume group $VG_NAME created successfully"
}

# Advanced logical volume creation with thin provisioning
create_thin_provisioned_volumes() {
    local vg_name="$1"
    local pool_size="$2"
    
    log_operation "Creating thin provisioning setup"
    
    # Create thin pool
    sudo lvcreate -L "$pool_size" --thinpool thinpool01 "$vg_name"
    
    # Create thin volumes (overprovisioned)
    sudo lvcreate -V 50G --thin "$vg_name/thinpool01" -n web01
    sudo lvcreate -V 50G --thin "$vg_name/thinpool01" -n web02
    sudo lvcreate -V 100G --thin "$vg_name/thinpool01" -n database01
    
    # Monitor thin pool usage
    sudo lvs -o +thin_count,pool_lv,data_percent,metadata_percent "$vg_name"
    
    log_operation "Thin provisioning setup completed"
}

# Live filesystem extension without downtime
extend_filesystem_online() {
    local lv_path="$1"
    local extend_size="$2"
    local mount_point="$3"
    
    log_operation "Starting online filesystem extension for $lv_path"
    
    # Check current sizes
    local current_lv_size=$(sudo lvdisplay "$lv_path" | grep "LV Size" | awk '{print $3 $4}')
    local current_fs_size=$(df -h "$mount_point" | tail -1 | awk '{print $2}')
    
    log_operation "Current LV size: $current_lv_size, FS size: $current_fs_size"
    
    # Extend logical volume
    sudo lvextend -L "+$extend_size" "$lv_path"
    
    # Extend filesystem based on type
    local fs_type=$(findmnt -n -o FSTYPE "$mount_point")
    
    case "$fs_type" in
        "ext4"|"ext3"|"ext2")
            sudo resize2fs "$lv_path"
            ;;
        "xfs")
            sudo xfs_growfs "$mount_point"
            ;;
        "btrfs")
            sudo btrfs filesystem resize max "$mount_point"
            ;;
        *)
            log_operation "ERROR: Unsupported filesystem type: $fs_type"
            exit 1
            ;;
    esac
    
    # Verify extension
    local new_lv_size=$(sudo lvdisplay "$lv_path" | grep "LV Size" | awk '{print $3 $4}')
    local new_fs_size=$(df -h "$mount_point" | tail -1 | awk '{print $2}')
    
    log_operation "New LV size: $new_lv_size, FS size: $new_fs_size"
    log_operation "Online filesystem extension completed successfully"
}

# Automated snapshot management with rotation
manage_lvm_snapshots() {
    local lv_path="$1"
    local retention_days="$2"
    
    local lv_name=$(basename "$lv_path")
    local vg_name=$(dirname "$lv_path" | xargs basename)
    local timestamp=$(date +%Y%m%d_%H%M%S)
    local snapshot_name="${lv_name}_snap_${timestamp}"
    
    log_operation "Creating snapshot $snapshot_name for $lv_path"
    
    # Create snapshot
    sudo lvcreate -L "$SNAPSHOT_SIZE" -s -n "$snapshot_name" "$lv_path"
    
    # Verify snapshot creation
    if sudo lvdisplay "/dev/$vg_name/$snapshot_name" &>/dev/null; then
        log_operation "Snapshot $snapshot_name created successfully"
        
        # Mount snapshot for backup access
        local snap_mount="/mnt/snapshots/$snapshot_name"
        sudo mkdir -p "$snap_mount"
        sudo mount "/dev/$vg_name/$snapshot_name" "$snap_mount" -o ro,nouuid 2>/dev/null
        
        log_operation "Snapshot mounted at $snap_mount for backup access"
    else
        log_operation "ERROR: Failed to create snapshot $snapshot_name"
        exit 1
    fi
    
    # Cleanup old snapshots
    log_operation "Cleaning up snapshots older than $retention_days days"
    
    while IFS= read -r old_snapshot; do
        local snap_date=$(echo "$old_snapshot" | grep -o '[0-9]\{8\}_[0-9]\{6\}')
        local snap_epoch=$(date -d "${snap_date:0:8} ${snap_date:9:2}:${snap_date:11:2}:${snap_date:13:2}" +%s)
        local cutoff_epoch=$(date -d "$retention_days days ago" +%s)
        
        if [[ $snap_epoch -lt $cutoff_epoch ]]; then
            log_operation "Removing old snapshot: $old_snapshot"
            
            # Unmount if mounted
            local old_snap_mount="/mnt/snapshots/$old_snapshot"
            if mountpoint -q "$old_snap_mount" 2>/dev/null; then
                sudo umount "$old_snap_mount"
                sudo rmdir "$old_snap_mount"
            fi
            
            # Remove snapshot
            sudo lvremove -f "/dev/$vg_name/$old_snapshot"
        fi
    done <<< "$(sudo lvs --noheadings -o lv_name "$vg_name" | grep "${lv_name}_snap_" | tr -d ' ')"
}

# Performance monitoring and optimization
monitor_lvm_performance() {
    local vg_name="$1"
    
    echo "=== LVM Performance Analysis ==="
    
    # VG performance metrics
    echo "Volume Group Statistics:"
    sudo vgdisplay "$vg_name" | grep -E "(VG Size|PE Size|Alloc PE|Free PE)"
    
    # LV performance metrics
    echo ""
    echo "Logical Volume Statistics:"
    sudo lvs -o +stripes,stripesize,chunksize "$vg_name"
    
    # Physical volume performance
    echo ""
    echo "Physical Volume Performance:"
    for pv in $(sudo vgdisplay "$vg_name" | grep "PV Name" | awk '{print $3}'); do
        echo "PV: $pv"
        sudo pvs -o +pv_used,pv_free "$pv"
        
        # Check underlying device performance
        local device=$(echo "$pv" | sed 's/[0-9]*$//')
        iostat -x 1 1 "$device" | tail -1
    done
    
    # Thin pool monitoring (if exists)
    if sudo lvs --noheadings -o pool_lv "$vg_name" | grep -q "thinpool"; then
        echo ""
        echo "Thin Pool Statistics:"
        sudo lvs -o +data_percent,metadata_percent,pool_lv "$vg_name" | grep thinpool
    fi
}

# Example usage
DISKS=("/dev/sdb" "/dev/sdc" "/dev/sdd")
create_lvm_infrastructure "${DISKS[@]}"
create_thin_provisioned_volumes "$VG_NAME" "200G"
extend_filesystem_online "/dev/$VG_NAME/web01" "10G" "/var/www"
manage_lvm_snapshots "/dev/$VG_NAME/database01" "7"
monitor_lvm_performance "$VG_NAME"
```

### RAID Configuration

#### Comprehensive RAID Management System
```bash
#!/bin/bash
# enterprise-raid-manager.sh - Complete RAID management solution

RAID_CONFIG_DIR="/etc/mdadm"
LOG_FILE="/var/log/raid-operations.log"
ALERT_EMAIL="admin@company.com"

log_raid_operation() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

send_alert() {
    local subject="$1"
    local message="$2"
    
    echo "$message" | mail -s "$subject" "$ALERT_EMAIL"
    log_raid_operation "Alert sent: $subject"
}

# Create RAID array with optimal settings
create_raid_array() {
    local raid_level="$1"
    local array_name="$2"
    shift 2
    local devices=("$@")
    
    log_raid_operation "Creating RAID $raid_level array $array_name with devices: ${devices[*]}"
    
    # Validate devices
    for device in "${devices[@]}"; do
        if [[ ! -b "$device" ]]; then
            log_raid_operation "ERROR: Device $device is not a valid block device"
            exit 1
        fi
        
        # Check if device is already in use
        if sudo mdadm --examine "$device" &>/dev/null; then
            log_raid_operation "WARNING: Device $device appears to contain RAID metadata"
        fi
    done
    
    # Calculate optimal chunk size based on RAID level
    local chunk_size
    case "$raid_level" in
        "0"|"10")
            chunk_size="512"  # Optimal for performance
            ;;
        "1")
            chunk_size=""     # Not applicable for RAID 1
            ;;
        "5"|"6")
            chunk_size="256"  # Balance between performance and parity overhead
            ;;
        *)
            log_raid_operation "ERROR: Unsupported RAID level: $raid_level"
            exit 1
            ;;
    esac
    
    # Create array with optimal parameters
    local create_cmd="sudo mdadm --create $array_name --level=$raid_level"
    create_cmd+=" --raid-devices=${#devices[@]}"
    
    if [[ -n "$chunk_size" ]]; then
        create_cmd+=" --chunk=$chunk_size"
    fi
    
    create_cmd+=" --metadata=1.2 --assume-clean ${devices[*]}"
    
    log_raid_operation "Executing: $create_cmd"
    eval "$create_cmd"
    
    # Wait for array to become active
    sleep 5
    
    # Verify array creation
    if sudo mdadm --detail "$array_name" &>/dev/null; then
        log_raid_operation "RAID array $array_name created successfully"
        
        # Add to mdadm.conf for persistence
        sudo mkdir -p "$RAID_CONFIG_DIR"
        sudo mdadm --detail --scan >> "$RAID_CONFIG_DIR/mdadm.conf"
        sudo update-initramfs -u
        
        # Display array information
        sudo mdadm --detail "$array_name"
        
        send_alert "RAID Array Created" "RAID $raid_level array $array_name has been created successfully"
    else
        log_raid_operation "ERROR: Failed to create RAID array $array_name"
        exit 1
    fi
}

# Advanced RAID monitoring and alerting
monitor_raid_arrays() {
    local check_interval="$1"  # in minutes
    
    log_raid_operation "Starting RAID monitoring with $check_interval minute intervals"
    
    while true; do
        # Check all RAID arrays
        while IFS= read -r array; do
            if [[ -n "$array" ]]; then
                local array_name=$(echo "$array" | awk '{print $1}')
                local array_status=$(sudo mdadm --detail "$array_name" | grep "State :" | awk '{print $3}')
                
                case "$array_status" in
                    "clean")
                        log_raid_operation "Array $array_name: Status OK ($array_status)"
                        ;;
                    "active")
                        log_raid_operation "Array $array_name: Status OK ($array_status)"
                        ;;
                    "degraded")
                        log_raid_operation "WARNING: Array $array_name is degraded"
                        send_alert "RAID Degraded" "RAID array $array_name is in degraded state. Immediate attention required."
                        ;;
                    "failed")
                        log_raid_operation "CRITICAL: Array $array_name has failed"
                        send_alert "RAID Failed" "RAID array $array_name has failed. Data loss possible. Immediate intervention required."
                        ;;
                    *)
                        log_raid_operation "WARNING: Array $array_name has unknown status: $array_status"
                        send_alert "RAID Unknown Status" "RAID array $array_name has unknown status: $array_status"
                        ;;
                esac
                
                # Check individual device health
                sudo mdadm --detail "$array_name" | grep -E "(Faulty|Spare)" | while read -r line; do
                    log_raid_operation "Device issue in $array_name: $line"
                done
                
                # Monitor rebuild progress
                if sudo cat /proc/mdstat | grep -q "recovery\|resync\|reshape"; then
                    local progress=$(sudo cat /proc/mdstat | grep -E "recovery|resync|reshape" | tail -1)
                    log_raid_operation "Rebuild in progress for $array_name: $progress"
                fi
            fi
        done <<< "$(cat /proc/mdstat | grep '^md' | awk '{print "/dev/" $1}')"
        
        sleep $((check_interval * 60))
    done
}

# Automated RAID recovery procedures
handle_disk_failure() {
    local array_name="$1"
    local failed_device="$2"
    local replacement_device="$3"
    
    log_raid_operation "Handling disk failure: $failed_device in array $array_name"
    
    # Mark device as failed (if not already)
    sudo mdadm --manage "$array_name" --fail "$failed_device" 2>/dev/null
    
    # Remove failed device
    log_raid_operation "Removing failed device $failed_device from $array_name"
    sudo mdadm --manage "$array_name" --remove "$failed_device"
    
    # Add replacement device
    if [[ -n "$replacement_device" ]] && [[ -b "$replacement_device" ]]; then
        log_raid_operation "Adding replacement device $replacement_device to $array_name"
        
        # Copy partition table if necessary
        local source_device=$(sudo mdadm --detail "$array_name" | grep "active sync" | head -1 | awk '{print $7}')
        if [[ -n "$source_device" ]]; then
            sudo sfdisk -d "$source_device" | sudo sfdisk "$replacement_device" 2>/dev/null || true
        fi
        
        # Add to array
        sudo mdadm --manage "$array_name" --add "$replacement_device"
        
        # Monitor rebuild progress
        log_raid_operation "Rebuild started for $array_name with replacement device $replacement_device"
        send_alert "RAID Rebuild Started" "RAID rebuild started for $array_name with replacement device $replacement_device"
        
        # Wait for rebuild to complete
        while sudo cat /proc/mdstat | grep -q "recovery\|resync"; do
            local progress=$(sudo cat /proc/mdstat | grep -E "recovery|resync" | tail -1)
            log_raid_operation "Rebuild progress: $progress"
            sleep 300  # Check every 5 minutes
        done
        
        log_raid_operation "Rebuild completed for $array_name"
        send_alert "RAID Rebuild Complete" "RAID rebuild completed successfully for $array_name"
    else
        log_raid_operation "No replacement device specified or device not available"
        send_alert "RAID Manual Intervention Required" "Failed device removed from $array_name. Manual replacement required."
    fi
}

# Performance optimization for RAID arrays
optimize_raid_performance() {
    local array_name="$1"
    local workload_type="$2"  # random, sequential, mixed
    
    log_raid_operation "Optimizing RAID performance for $array_name (workload: $workload_type)"
    
    # Get underlying devices
    local devices=($(sudo mdadm --detail "$array_name" | grep "active sync" | awk '{print $7}'))
    
    # Set optimal read-ahead based on RAID level and workload
    local raid_level=$(sudo mdadm --detail "$array_name" | grep "Raid Level" | awk '{print $4}')
    local read_ahead
    
    case "$raid_level" in
        "raid0")
            read_ahead=$((512 * ${#devices[@]}))  # Multiply by number of devices
            ;;
        "raid1")
            read_ahead=512
            ;;
        "raid5"|"raid6")
            read_ahead=$((256 * (${#devices[@]} - 1)))  # Account for parity
            ;;
        "raid10")
            read_ahead=$((512 * (${#devices[@]} / 2)))  # Account for mirroring
            ;;
        *)
            read_ahead=512
            ;;
    esac
    
    # Apply read-ahead settings
    sudo blockdev --setra "$read_ahead" "$array_name"
    log_raid_operation "Set read-ahead to $read_ahead for $array_name"
    
    # Optimize underlying devices
    for device in "${devices[@]}"; do
        local base_device=$(echo "$device" | sed 's/[0-9]*$//')
        
        # Set appropriate I/O scheduler
        if sudo smartctl -a "$base_device" | grep -q "Solid State"; then
            echo "none" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
            log_raid_operation "Set 'none' scheduler for SSD $base_device"
        else
            echo "mq-deadline" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
            log_raid_operation "Set 'mq-deadline' scheduler for HDD $base_device"
        fi
        
        # Optimize queue settings
        case "$workload_type" in
            "random")
                echo 1 | sudo tee "/sys/block/$(basename $base_device)/queue/rq_affinity" >/dev/null
                echo 32 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
                ;;
            "sequential")
                echo 2 | sudo tee "/sys/block/$(basename $base_device)/queue/rq_affinity" >/dev/null
                echo 128 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
                ;;
            "mixed"|*)
                echo 1 | sudo tee "/sys/block/$(basename $base_device)/queue/rq_affinity" >/dev/null
                echo 64 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
                ;;
        esac
    done
    
    log_raid_operation "Performance optimization completed for $array_name"
}

# Comprehensive RAID testing and validation
test_raid_functionality() {
    local array_name="$1"
    
    log_raid_operation "Starting comprehensive RAID functionality test for $array_name"
    
    # Create test filesystem and mount point
    local test_mount="/mnt/raid_test_$(date +%s)"
    sudo mkdir -p "$test_mount"
    
    # Create test filesystem
    sudo mkfs.ext4 -F "$array_name" >/dev/null 2>&1
    sudo mount "$array_name" "$test_mount"
    
    # Performance baseline test
    log_raid_operation "Running performance baseline test"
    
    # Sequential write test
    local write_speed=$(dd if=/dev/zero of="$test_mount/testfile" bs=1M count=1024 conv=fsync 2>&1 | \
                       grep "MB/s" | awk '{print $(NF-1)}')
    log_raid_operation "Sequential write speed: $write_speed MB/s"
    
    # Sequential read test
    local read_speed=$(dd if="$test_mount/testfile" of=/dev/null bs=1M 2>&1 | \
                      grep "MB/s" | awk '{print $(NF-1)}')
    log_raid_operation "Sequential read speed: $read_speed MB/s"
    
    # Cleanup test environment
    sudo umount "$test_mount"
    sudo rmdir "$test_mount"
    
    # Simulated failure test (if safe to do so)
    local device_count=$(sudo mdadm --detail "$array_name" | grep "active sync" | wc -l)
    local raid_level=$(sudo mdadm --detail "$array_name" | grep "Raid Level" | awk '{print $4}')
    
    if [[ "$device_count" -gt 2 ]] && [[ "$raid_level" =~ raid[56] ]]; then
        log_raid_operation "RAID configuration supports failure simulation - skipping for safety"
        # In production, you might want to implement controlled failure testing
    fi
    
    log_raid_operation "RAID functionality test completed for $array_name"
}

# Example usage for different RAID configurations
setup_enterprise_raid() {
    # RAID 1 for OS (high availability)
    create_raid_array "1" "/dev/md0" "/dev/sdb1" "/dev/sdc1"
    optimize_raid_performance "/dev/md0" "mixed"
    
    # RAID 5 for data (balance of performance and redundancy)
    create_raid_array "5" "/dev/md1" "/dev/sdd1" "/dev/sde1" "/dev/sdf1" "/dev/sdg1"
    optimize_raid_performance "/dev/md1" "sequential"
    
    # RAID 10 for databases (high performance and redundancy)
    create_raid_array "10" "/dev/md2" "/dev/sdh1" "/dev/sdi1" "/dev/sdj1" "/dev/sdk1"
    optimize_raid_performance "/dev/md2" "random"
    
    # Start monitoring
    monitor_raid_arrays 15 &  # Check every 15 minutes
    
    # Test all arrays
    test_raid_functionality "/dev/md0"
    test_raid_functionality "/dev/md1"
    test_raid_functionality "/dev/md2"
}

# Disaster recovery procedures
raid_disaster_recovery() {
    local array_name="$1"
    local backup_metadata_file="$2"
    
    log_raid_operation "Starting disaster recovery for $array_name"
    
    # Stop array if running
    sudo mdadm --stop "$array_name" 2>/dev/null || true
    
    # Attempt to reassemble array
    if [[ -f "$backup_metadata_file" ]]; then
        log_raid_operation "Attempting recovery using metadata backup"
        sudo mdadm --assemble "$array_name" --backup-file="$backup_metadata_file"
    else
        log_raid_operation "Attempting auto-assembly of array"
        sudo mdadm --assemble --scan
    fi
    
    # Force assembly if necessary (last resort)
    if ! sudo mdadm --detail "$array_name" &>/dev/null; then
        log_raid_operation "Normal assembly failed, attempting force assembly"
        sudo mdadm --assemble --force "$array_name" /dev/sd*
    fi
    
    # Check filesystem after recovery
    if sudo mdadm --detail "$array_name" &>/dev/null; then
        log_raid_operation "Array recovery successful, checking filesystem"
        sudo fsck -y "$array_name" || log_raid_operation "Filesystem check completed with errors"
    else
        log_raid_operation "CRITICAL: Array recovery failed"
        send_alert "RAID Recovery Failed" "Failed to recover RAID array $array_name. Manual intervention required."
    fi
}

# Start enterprise RAID setup
setup_enterprise_raid
```

### Performance Optimization

#### Storage Performance Analysis and Tuning
```bash
#!/bin/bash
# storage-performance-optimizer.sh - Comprehensive storage performance optimization

PERFORMANCE_LOG="/var/log/storage-performance.log"
BENCHMARK_DIR="/tmp/storage-benchmarks"

log_performance() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$PERFORMANCE_LOG"
}

# Comprehensive I/O performance analysis
analyze_storage_performance() {
    local device="$1"
    local duration="$2"  # in seconds
    
    log_performance "Starting performance analysis for $device"
    
    mkdir -p "$BENCHMARK_DIR"
    local report_file="$BENCHMARK_DIR/performance_$(basename $device)_$(date +%Y%m%d_%H%M%S).txt"
    
    echo "=== Storage Performance Analysis Report ===" > "$report_file"
    echo "Device: $device" >> "$report_file"
    echo "Analysis Duration: $duration seconds" >> "$report_file"
    echo "Timestamp: $(date)" >> "$report_file"
    echo "" >> "$report_file"
    
    # Device information
    echo "=== Device Information ===" >> "$report_file"
    lsblk "$device" >> "$report_file" 2>/dev/null
    echo "" >> "$report_file"
    
    # Current I/O scheduler and queue settings
    local base_device=$(echo "$device" | sed 's/[0-9]*$//')
    echo "=== Current Settings ===" >> "$report_file"
    echo "I/O Scheduler: $(cat /sys/block/$(basename $base_device)/queue/scheduler 2>/dev/null)" >> "$report_file"
    echo "Queue Depth: $(cat /sys/block/$(basename $base_device)/queue/nr_requests 2>/dev/null)" >> "$report_file"
    echo "Read-ahead: $(blockdev --getra $device 2>/dev/null) sectors" >> "$report_file"
    echo "" >> "$report_file"
    
    # Real-time I/O monitoring
    echo "=== Real-time I/O Analysis ===" >> "$report_file"
    iostat -x "$device" 1 "$duration" >> "$report_file" 2>/dev/null &
    local iostat_pid=$!
    
    # Concurrent workload simulation
    echo "=== Workload Simulation Results ===" >> "$report_file"
    
    # Sequential read test
    echo "Sequential Read Performance:" >> "$report_file"
    dd if="$device" of=/dev/null bs=1M count=1024 2>&1 | grep -E "(copied|MB/s)" >> "$report_file"
    
    # Random read test with multiple threads
    echo "Random Read Performance (4K blocks, 4 threads):" >> "$report_file"
    fio --name=random_read_test --filename="$device" --rw=randread --bs=4k \
        --numjobs=4 --runtime=30 --group_reporting --direct=1 \
        --output-format=normal 2>/dev/null | grep -E "(read:|IOPS)" >> "$report_file"
    
    # Mixed workload test
    echo "Mixed Workload Performance (70% read, 30% write):" >> "$report_file"
    fio --name=mixed_test --filename="$device" --rw=randrw --rwmixread=70 \
        --bs=4k --numjobs=2 --runtime=30 --group_reporting --direct=1 \
        --output-format=normal 2>/dev/null | grep -E "(read:|write:|IOPS)" >> "$report_file"
    
    # Wait for iostat to complete
    wait $iostat_pid 2>/dev/null || true
    
    # SMART data analysis (if available)
    if command -v smartctl &>/dev/null; then
        echo "=== SMART Health Analysis ===" >> "$report_file"
        smartctl -H "$base_device" 2>/dev/null >> "$report_file" || echo "SMART data not available" >> "$report_file"
    fi
    
    log_performance "Performance analysis completed. Report: $report_file"
    
    # Display summary
    echo ""
    echo "=== Performance Summary ==="
    grep -E "(MB/s|IOPS)" "$report_file" | head -10
}

# Optimize I/O scheduler and queue settings
optimize_io_settings() {
    local device="$1"
    local workload_type="$2"  # ssd, hdd, mixed
    local io_pattern="$3"     # random, sequential, mixed
    
    local base_device=$(echo "$device" | sed 's/[0-9]*$//')
    log_performance "Optimizing I/O settings for $device (type: $workload_type, pattern: $io_pattern)"
    
    # Set optimal I/O scheduler
    case "$workload_type" in
        "ssd")
            echo "none" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
            log_performance "Set 'none' scheduler for SSD"
            ;;
        "hdd")
            case "$io_pattern" in
                "random")
                    echo "mq-deadline" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
                    ;;
                "sequential")
                    echo "mq-deadline" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
                    ;;
                *)
                    echo "mq-deadline" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
                    ;;
            esac
            log_performance "Set 'mq-deadline' scheduler for HDD"
            ;;
        "mixed"|*)
            echo "mq-deadline" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
            log_performance "Set 'mq-deadline' scheduler for mixed workload"
            ;;
    esac
    
    # Optimize queue depth
    case "$io_pattern" in
        "random")
            echo 32 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
            ;;
        "sequential")
            echo 128 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
            ;;
        "mixed"|*)
            echo 64 | sudo tee "/sys/block/$(basename $base_device)/queue/nr_requests" >/dev/null
            ;;
    esac
    
    # Optimize read-ahead
    case "$io_pattern" in
        "random")
            sudo blockdev --setra 128 "$device"
            ;;
        "sequential")
            sudo blockdev --setra 1024 "$device"
            ;;
        "mixed"|*)
            sudo blockdev --setra 512 "$device"
            ;;
    esac
    
    # Set CPU affinity for better NUMA performance
    echo 1 | sudo tee "/sys/block/$(basename $base_device)/queue/rq_affinity" >/dev/null
    
    log_performance "I/O optimization completed for $device"
}

# SSD-specific optimizations
optimize_ssd_performance() {
    local device="$1"
    
    log_performance "Applying SSD-specific optimizations for $device"
    
    local base_device=$(echo "$device" | sed 's/[0-9]*$//')
    
    # Enable TRIM support
    if sudo fstrim -v "$(findmnt -n -o TARGET $device)" 2>/dev/null; then
        log_performance "TRIM operation completed for $device"
        
        # Enable periodic TRIM via systemd timer
        sudo systemctl enable fstrim.timer
        sudo systemctl start fstrim.timer
        log_performance "Enabled periodic TRIM via systemd timer"
    else
        log_performance "TRIM not supported or device not mounted"
    fi
    
    # Disable write cache if battery backup not available
    if ! sudo smartctl -a "$base_device" | grep -q "Power"; then
        sudo hdparm -W 0 "$base_device" 2>/dev/null || true
        log_performance "Disabled write cache (no battery backup detected)"
    fi
    
    # Optimize for SSD characteristics
    echo "none" | sudo tee "/sys/block/$(basename $base_device)/queue/scheduler" >/dev/null
    echo 1 | sudo tee "/sys/block/$(basename $base_device)/queue/nomerges" >/dev/null
    echo 1 | sudo tee "/sys/block/$(basename $base_device)/queue/rq_affinity" >/dev/null
    
    log_performance "SSD optimizations applied for $device"
}

# Network storage optimization
optimize_network_storage() {
    local mount_point="$1"
    local storage_type="$2"  # nfs, iscsi, cifs
    
    log_performance "Optimizing network storage at $mount_point (type: $storage_type)"
    
    case "$storage_type" in
        "nfs")
            # NFS-specific optimizations
            local current_opts=$(findmnt -n -o OPTIONS "$mount_point")
            
            if ! echo "$current_opts" | grep -q "rsize="; then
                log_performance "Consider remounting with larger rsize (e.g., rsize=1048576)"
            fi
            
            if ! echo "$current_opts" | grep -q "wsize="; then
                log_performance "Consider remounting with larger wsize (e.g., wsize=1048576)"
            fi
            
            if ! echo "$current_opts" | grep -q "timeo="; then
                log_performance "Consider setting appropriate timeout (e.g., timeo=600)"
            fi
            ;;
            
        "iscsi")
            # iSCSI-specific optimizations
            local iscsi_device=$(findmnt -n -o SOURCE "$mount_point")
            if [[ -n "$iscsi_device" ]]; then
                optimize_io_settings "$iscsi_device" "mixed" "mixed"
                
                # Increase iSCSI session parameters
                echo 32 | sudo tee /sys/module/libiscsi/parameters/iscsi_max_lun >/dev/null 2>&1 || true
                log_performance "Applied iSCSI optimizations"
            fi
            ;;
            
        "cifs")
            # CIFS/SMB-specific optimizations
            local current_opts=$(findmnt -n -o OPTIONS "$mount_point")
            
            if ! echo "$current_opts" | grep -q "cache="; then
                log_performance "Consider using cache=strict for better performance"
            fi
            
            if ! echo "$current_opts" | grep -q "rsize="; then
                log_performance "Consider setting larger rsize (e.g., rsize=1048576)"
            fi
            ;;
    esac
    
    log_performance "Network storage optimization completed for $mount_point"
}

# Continuous performance monitoring
monitor_storage_performance() {
    local devices=("$@")
    local monitoring_duration=300  # 5 minutes
    
    log_performance "Starting continuous performance monitoring for devices: ${devices[*]}"
    
    while true; do
        for device in "${devices[@]}"; do
            # Check for performance anomalies
            local current_util=$(iostat -x "$device" 1 2 | tail -1 | awk '{print $10}')
            local current_await=$(iostat -x "$device" 1 2 | tail -1 | awk '{print $9}')
            
            # Alert on high utilization (>90%)
            if (( $(echo "$current_util > 90" | bc -l) )); then
                log_performance "WARNING: High utilization ($current_util%) on $device"
            fi
            
            # Alert on high average wait time (>50ms)
            if (( $(echo "$current_await > 50" | bc -l) )); then
                log_performance "WARNING: High average wait time (${current_await}ms) on $device"
            fi
            
            # Check for SMART warnings
            if command -v smartctl &>/dev/null; then
                local base_device=$(echo "$device" | sed 's/[0-9]*$//')
                if smartctl -H "$base_device" 2>/dev/null | grep -q "FAILED"; then
                    log_performance "CRITICAL: SMART health check failed for $device"
                fi
            fi
        done
        
        sleep "$monitoring_duration"
    done
}

# Example usage
STORAGE_DEVICES=("/dev/sda" "/dev/md0" "/dev/vg01/lv_data")

for device in "${STORAGE_DEVICES[@]}"; do
    analyze_storage_performance "$device" 60
    
    # Apply optimizations based on device type detection
    if sudo smartctl -a "$(echo $device | sed 's/[0-9]*$//')" 2>/dev/null | grep -q "Solid State"; then
        optimize_ssd_performance "$device"
        optimize_io_settings "$device" "ssd" "mixed"
    else
        optimize_io_settings "$device" "hdd" "mixed"
    fi
done

# Start continuous monitoring in background
monitor_storage_performance "${STORAGE_DEVICES[@]}" &

log_performance "Storage performance optimization workflow completed"
```

### Storage Security

#### LUKS Encryption Implementation
```bash
#!/bin/bash
# luks-encryption-manager.sh - Enterprise LUKS encryption management

ENCRYPTION_LOG="/var/log/encryption-operations.log"
KEY_BACKUP_DIR="/secure/key-backups"

log_encryption() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$ENCRYPTION_LOG"
}

# Comprehensive LUKS setup with multiple authentication methods
setup_luks_encryption() {
    local device="$1"
    local container_name="$2"
    local key_file="$3"
    
    log_encryption "Setting up LUKS encryption for $device"
    
    # Securely wipe device (optional but recommended)
    read -p "Perform secure wipe of $device? This will take time (y/N): " -n 1 -r
    echo
    if [[ $REPLY =~ ^[Yy]$ ]]; then
        log_encryption "Performing secure wipe of $device"
        sudo shred -vfz -n 3 "$device" || {
            log_encryption "WARNING: Secure wipe failed or interrupted"
        }
    fi
    
    # Generate secure key file if not provided
    if [[ -z "$key_file" ]]; then
        key_file="/tmp/luks_${container_name}_$(date +%s).key"
        sudo dd if=/dev/urandom of="$key_file" bs=512 count=1
        sudo chmod 600 "$key_file"
        log_encryption "Generated random key file: $key_file"
    fi
    
    # Format LUKS container with strong parameters
    log_encryption "Creating LUKS container with advanced parameters"
    sudo cryptsetup luksFormat \
        --type luks2 \
        --cipher aes-xts-plain64 \
        --key-size 512 \
        --hash sha512 \
        --iter-time 5000 \
        --use-random \
        --verify-passphrase \
        "$device" "$key_file"
    
    if [[ $? -eq 0 ]]; then
        log_encryption "LUKS container created successfully"
        
        # Open the container
        sudo cryptsetup luksOpen "$device" "$container_name" --key-file "$key_file"
        
        # Backup LUKS header
        sudo mkdir -p "$KEY_BACKUP_DIR"
        sudo cryptsetup luksHeaderBackup "$device" \
            --header-backup-file "$KEY_BACKUP_DIR/${container_name}_header.backup"
        log_encryption "LUKS header backed up to $KEY_BACKUP_DIR"
        
        # Add additional key slots for redundancy
        setup_additional_key_slots "$device" "$key_file"
        
        # Create filesystem on encrypted device
        create_encrypted_filesystem "/dev/mapper/$container_name" "$container_name"
        
    else
        log_encryption "ERROR: Failed to create LUKS container"
        exit 1
    fi
}

# Setup multiple authentication methods
setup_additional_key_slots() {
    local device="$1"
    local primary_key="$2"
    
    log_encryption "Setting up additional key slots for $device"
    
    # Add passphrase-based slot
    echo "Setting up passphrase authentication (slot 1):"
    sudo cryptsetup luksAddKey "$device" --key-file "$primary_key"
    
    # Add secondary key file
    local secondary_key="/tmp/luks_secondary_$(date +%s).key"
    sudo dd if=/dev/urandom of="$secondary_key" bs=512 count=1
    sudo chmod 600 "$secondary_key"
    
    sudo cryptsetup luksAddKey "$device" "$secondary_key" --key-file "$primary_key"
    log_encryption "Added secondary key file: $secondary_key"
    
    # Backup all key files securely
    sudo cp "$primary_key" "$KEY_BACKUP_DIR/"
    sudo cp "$secondary_key" "$KEY_BACKUP_DIR/"
    
    # Display key slot information
    sudo cryptsetup luksDump "$device" | grep -A2 "Key Slot"
}

# Create optimized filesystem on encrypted device
create_encrypted_filesystem() {
    local encrypted_device="$1"
    local label="$2"
    
    log_encryption "Creating filesystem on encrypted device $encrypted_device"
    
    # Create ext4 with encryption-optimized parameters
    sudo mkfs.ext4 \
        -F \
        -L "encrypted_$label" \
        -O encrypt \
        -E stride=32,stripe-width=64 \
        "$encrypted_device"
    
    # Set filesystem mount options for encrypted storage
    local mount_point="/mnt/encrypted_$label"
    sudo mkdir -p "$mount_point"
    
    # Add to fstab with secure mount options
    echo "$encrypted_device $mount_point ext4 nodev,nosuid,noexec,noatime 0 2" | \
        sudo tee -a /etc/fstab
    
    log_encryption "Encrypted filesystem created and configured"
}

# Automated encryption key rotation
rotate_luks_keys() {
    local device="$1"
    local old_key_slot="$2"
    
    log_encryption "Starting key rotation for $device (slot $old_key_slot)"
    
    # Generate new key
    local new_key="/tmp/luks_rotated_$(date +%s).key"
    sudo dd if=/dev/urandom of="$new_key" bs=512 count=1
    sudo chmod 600 "$new_key"
    
    # Add new key to available slot
    sudo cryptsetup luksAddKey "$device" "$new_key"
    
    if [[ $? -eq 0 ]]; then
        # Remove old key slot
        sudo cryptsetup luksRemoveKey "$device" --key-slot "$old_key_slot"
        log_encryption "Key rotation completed successfully"
        
        # Update backup
        sudo cryptsetup luksHeaderBackup "$device" \
            --header-backup-file "$KEY_BACKUP_DIR/$(basename $device)_header_$(date +%s).backup"
        
        # Secure deletion of old key
        sudo shred -vfz -n 3 "$new_key"
    else
        log_encryption "ERROR: Key rotation failed"
        sudo rm -f "$new_key"
        exit 1
    fi
}

# Performance monitoring for encrypted storage
monitor_encryption_performance() {
    local encrypted_device="$1"
    
    log_encryption "Monitoring encryption performance for $encrypted_device"
    
    # Baseline performance without encryption overhead measurement
    echo "=== Encryption Performance Analysis ==="
    
    # CPU usage during encryption operations
    echo "CPU encryption capability:"
    openssl speed -evp aes-256-xts 2>/dev/null | tail -1
    
    # I/O performance on encrypted device
    echo "Encrypted device I/O performance:"
    dd if=/dev/zero of="$encrypted_device" bs=1M count=100 conv=fsync 2>&1 | \
        grep -E "(copied|MB/s)"
    
    # Memory usage
    echo "Current memory usage for encryption:"
    ps aux | grep -E "(cryptsetup|dm-crypt)" | grep -v grep
    
    log_encryption "Performance monitoring completed"
}

# Disaster recovery procedures
luks_disaster_recovery() {
    local device="$1"
    local header_backup="$2"
    local container_name="$3"
    
    log_encryption "Starting LUKS disaster recovery for $device"
    
    # Restore LUKS header from backup
    if [[ -f "$header_backup" ]]; then
        log_encryption "Restoring LUKS header from backup: $header_backup"
        sudo cryptsetup luksHeaderRestore "$device" --header-backup-file "$header_backup"
        
        if [[ $? -eq 0 ]]; then
            log_encryption "LUKS header restored successfully"
            
            # Attempt to open the container
            echo "Please provide the passphrase to unlock the recovered container:"
            sudo cryptsetup luksOpen "$device" "$container_name"
            
            if [[ $? -eq 0 ]]; then
                log_encryption "Container opened successfully after recovery"
                
                # Check filesystem integrity
                sudo fsck -y "/dev/mapper/$container_name"
                log_encryption "Filesystem check completed"
            else
                log_encryption "ERROR: Failed to open recovered container"
            fi
        else
            log_encryption "ERROR: Failed to restore LUKS header"
        fi
    else
        log_encryption "ERROR: Header backup file not found: $header_backup"
    fi
}

# Security audit for encrypted storage
audit_encryption_security() {
    local device="$1"
    
    log_encryption "Starting security audit for encrypted device $device"
    
    echo "=== LUKS Security Audit ==="
    
    # Check LUKS version and parameters
    echo "LUKS Configuration:"
    sudo cryptsetup luksDump "$device" | grep -E "(Version|Cipher|Hash|Key size)"
    
    # Check active key slots
    echo "Active Key Slots:"
    sudo cryptsetup luksDump "$device" | grep -A5 "Key Slot"
    
    # Verify cipher strength
    local cipher=$(sudo cryptsetup luksDump "$device" | grep "Cipher:" | awk '{print $2}')
    local key_size=$(sudo cryptsetup luksDump "$device" | grep "MK bits:" | awk '{print $3}')
    
    if [[ "$cipher" == "aes-xts-plain64" ]] && [[ "$key_size" -ge 256 ]]; then
        echo "✓ Strong encryption configuration detected"
    else
        echo "⚠ Weak encryption configuration - consider upgrading"
    fi
    
    # Check for backup files
    echo "Backup Status:"
    if [[ -d "$KEY_BACKUP_DIR" ]]; then
        ls -la "$KEY_BACKUP_DIR"/*.backup 2>/dev/null || echo "No backup files found"
    else
        echo "⚠ Backup directory not found"
    fi
    
    log_encryption "Security audit completed"
}

# Example usage
DEVICE="/dev/sdb1"
CONTAINER="secure_data"
KEY_FILE="/secure/keys/primary.key"

# Setup comprehensive encryption
setup_luks_encryption "$DEVICE" "$CONTAINER" "$KEY_FILE"

# Monitor performance
monitor_encryption_performance "/dev/mapper/$CONTAINER"

# Perform security audit
audit_encryption_security "$DEVICE"

# Schedule key rotation (monthly)
echo "0 2 1 * * /path/to/rotate_luks_keys.sh $DEVICE 0" | sudo crontab -

log_encryption "LUKS encryption setup and monitoring completed"
```

#### Access Control and Quotas Management
```bash
#!/bin/bash
# storage-access-control.sh - Comprehensive storage security management

ACL_LOG="/var/log/acl-operations.log"
QUOTA_LOG="/var/log/quota-operations.log"

log_acl() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$ACL_LOG"
}

log_quota() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$QUOTA_LOG"
}

# Advanced ACL implementation
setup_advanced_acls() {
    local directory="$1"
    local security_profile="$2"  # high, medium, low
    
    log_acl "Setting up advanced ACLs for $directory (profile: $security_profile)"
    
    # Ensure ACL support is enabled
    if ! mount | grep "$(df --output=source "$directory" | tail -1)" | grep -q "acl"; then
        log_acl "WARNING: ACL support not enabled. Remounting with ACL support"
        local mount_point=$(df --output=target "$directory" | tail -1)
        sudo mount -o remount,acl "$mount_point"
    fi
    
    case "$security_profile" in
        "high")
            # High security: Restrictive permissions with detailed logging
            sudo setfacl -R -m d:g:wheel:rx "$directory"
            sudo setfacl -R -m d:o::--- "$directory"
            sudo setfacl -R -m d:u::rwx "$directory"
            
            # Enable audit logging for this directory
            sudo auditctl -w "$directory" -p warx -k filesystem_access
            log_acl "High security profile applied with audit logging"
            ;;
            
        "medium")
            # Medium security: Balanced permissions for collaboration
            sudo setfacl -R -m d:g:users:rx "$directory"
            sudo setfacl -R -m d:g:staff:rwx "$directory"
            sudo setfacl -R -m d:o::r-- "$directory"
            log_acl "Medium security profile applied"
            ;;
            
        "low")
            # Low security: Open permissions for public areas
            sudo setfacl -R -m d:g:users:rwx "$directory"
            sudo setfacl -R -m d:o::r-x "$directory"
            log_acl "Low security profile applied"
            ;;
    esac
    
    # Set up automatic inheritance
    sudo setfacl -R -d -m u::rwx,g::rx,o::--- "$directory"
    
    # Display current ACL configuration
    log_acl "Current ACL configuration for $directory:"
    getfacl "$directory" >> "$ACL_LOG"
}

# Comprehensive quota system implementation
setup_filesystem_quotas() {
    local filesystem="$1"
    local quota_type="$2"  # user, group, project
    
    log_quota "Setting up $quota_type quotas for $filesystem"
    
    # Enable quota support
    local mount_options=$(findmnt -n -o OPTIONS "$filesystem")
    if ! echo "$mount_options" | grep -q "quota"; then
        log_quota "Enabling quota support for $filesystem"
        
        # Add quota options to fstab
        local device=$(findmnt -n -o SOURCE "$filesystem")
        sudo sed -i "s|\($device.*\)\(defaults\)|\1\2,usrquota,grpquota|" /etc/fstab
        
        # Remount with quota support
        sudo mount -o remount "$filesystem"
    fi
    
    # Create quota database files
    case "$quota_type" in
        "user")
            sudo quotacheck -cug "$filesystem"
            sudo quotaon -u "$filesystem"
            log_quota "User quotas enabled for $filesystem"
            ;;
        "group")
            sudo quotacheck -cug "$filesystem"
            sudo quotaon -g "$filesystem"
            log_quota "Group quotas enabled for $filesystem"
            ;;
        "project")
            # Project quotas (XFS only)
            if df -T "$filesystem" | grep -q "xfs"; then
                sudo xfs_quota -x -c "project -s" "$filesystem"
                log_quota "Project quotas enabled for XFS filesystem $filesystem"
            else
                log_quota "WARNING: Project quotas only supported on XFS"
            fi
            ;;
    esac
}

# Automated quota management with policies
manage_quota_policies() {
    local filesystem="$1"
    local policy_file="$2"
    
    log_quota "Applying quota policies from $policy_file to $filesystem"
    
    # Read policy file and apply quotas
    while IFS=',' read -r user_type name soft_limit hard_limit grace_period; do
        # Skip comments and empty lines
        [[ "$user_type" =~ ^#.*$ ]] && continue
        [[ -z "$user_type" ]] && continue
        
        case "$user_type" in
            "user")
                sudo setquota -u "$name" "$soft_limit" "$hard_limit" 0 0 "$filesystem"
                log_quota "Set user quota for $name: soft=$soft_limit, hard=$hard_limit"
                ;;
            "group")
                sudo setquota -g "$name" "$soft_limit" "$hard_limit" 0 0 "$filesystem"
                log_quota "Set group quota for $name: soft=$soft_limit, hard=$hard_limit"
                ;;
        esac
        
        # Set grace period if specified
        if [[ -n "$grace_period" ]]; then
            sudo setquota -t -u "$grace_period" "$grace_period" "$filesystem"
        fi
        
    done < "$policy_file"
    
    log_quota "Quota policies applied successfully"
}

# Quota monitoring and alerting
monitor_quota_usage() {
    local filesystem="$1"
    local alert_threshold="$2"  # percentage
    
    log_quota "Starting quota monitoring for $filesystem (alert at $alert_threshold%)"
    
    # Check user quotas
    while IFS= read -r quota_line; do
        if [[ "$quota_line" =~ ^[^#] ]] && [[ -n "$quota_line" ]]; then
            local username=$(echo "$quota_line" | awk '{print $1}')
            local used=$(echo "$quota_line" | awk '{print $3}')
            local soft_limit=$(echo "$quota_line" | awk '{print $4}')
            
            if [[ "$soft_limit" -gt 0 ]]; then
                local usage_percent=$(( (used * 100) / soft_limit ))
                
                if [[ "$usage_percent" -ge "$alert_threshold" ]]; then
                    log_quota "ALERT: User $username at $usage_percent% quota usage"
                    
                    # Send notification to user
                    echo "Quota Alert: You are using $usage_percent% of your allocated space." | \
                        mail -s "Quota Warning" "$username@$(hostname -d)" 2>/dev/null || true
                fi
            fi
        fi
    done <<< "$(sudo repquota -u "$filesystem" 2>/dev/null)"
    
    # Check group quotas
    while IFS= read -r quota_line; do
        if [[ "$quota_line" =~ ^[^#] ]] && [[ -n "$quota_line" ]]; then
            local groupname=$(echo "$quota_line" | awk '{print $1}')
            local used=$(echo "$quota_line" | awk '{print $3}')
            local soft_limit=$(echo "$quota_line" | awk '{print $4}')
            
            if [[ "$soft_limit" -gt 0 ]]; then
                local usage_percent=$(( (used * 100) / soft_limit ))
                
                if [[ "$usage_percent" -ge "$alert_threshold" ]]; then
                    log_quota "ALERT: Group $groupname at $usage_percent% quota usage"
                fi
            fi
        fi
    done <<< "$(sudo repquota -g "$filesystem" 2>/dev/null)"
}

# Security audit for storage access
audit_storage_access() {
    local directory="$1"
    
    log_acl "Starting storage access audit for $directory"
    
    echo "=== Storage Access Security Audit ===" > "/tmp/storage_audit_$(date +%s).txt"
    local audit_file="/tmp/storage_audit_$(date +%s).txt"
    
    # Check file permissions
    echo "=== Permission Analysis ===" >> "$audit_file"
    find "$directory" -type f -perm /o+w -exec ls -la {} \; >> "$audit_file" 2>/dev/null
    
    # Check for SUID/SGID files
    echo "=== SUID/SGID Files ===" >> "$audit_file"
    find "$directory" -type f \( -perm -4000 -o -perm -2000 \) -exec ls -la {} \; >> "$audit_file" 2>/dev/null
    
    # Check ACL configurations
    echo "=== ACL Configurations ===" >> "$audit_file"
    find "$directory" -type d -exec getfacl {} \; >> "$audit_file" 2>/dev/null
    
    # Check quota status
    echo "=== Quota Status ===" >> "$audit_file"
    local filesystem=$(df --output=target "$directory" | tail -1)
    repquota -a 2>/dev/null >> "$audit_file" || echo "Quotas not enabled" >> "$audit_file"
    
    # Check for world-writable files
    echo "=== World-Writable Files ===" >> "$audit_file"
    find "$directory" -type f -perm -o+w >> "$audit_file" 2>/dev/null
    
    log_acl "Storage access audit completed. Report: $audit_file"
    echo "Audit report generated: $audit_file"
}

# Automated compliance checking
check_compliance_standards() {
    local filesystem="$1"
    local standard="$2"  # pci, hipaa, sox
    
    log_acl "Checking compliance for $filesystem against $standard standards"
    
    case "$standard" in
        "pci")
            # PCI DSS requirements
            echo "=== PCI DSS Compliance Check ==="
            
            # Check encryption status
            if cryptsetup status "$(basename $filesystem)" &>/dev/null; then
                echo "✓ Encryption: PASS (Data encrypted at rest)"
            else
                echo "✗ Encryption: FAIL (Data not encrypted)"
            fi
            
            # Check access controls
            if mount | grep "$filesystem" | grep -q "nodev,nosuid"; then
                echo "✓ Mount Security: PASS (Secure mount options)"
            else
                echo "✗ Mount Security: FAIL (Insecure mount options)"
            fi
            ;;
            
        "hipaa")
            # HIPAA requirements
            echo "=== HIPAA Compliance Check ==="
            
            # Check audit logging
            if auditctl -l | grep -q "$filesystem"; then
                echo "✓ Audit Logging: PASS (Access logging enabled)"
            else
                echo "✗ Audit Logging: FAIL (No access logging)"
            fi
            
            # Check user access controls
            if getfacl "$filesystem" | grep -q "group:"; then
                echo "✓ Access Control: PASS (Group-based access)"
            else
                echo "✗ Access Control: FAIL (No group access controls)"
            fi
            ;;
            
        "sox")
            # SOX requirements
            echo "=== SOX Compliance Check ==="
            
            # Check data retention
            if [[ -f "/etc/logrotate.d/$(basename $filesystem)" ]]; then
                echo "✓ Data Retention: PASS (Rotation configured)"
            else
                echo "✗ Data Retention: FAIL (No retention policy)"
            fi
            ;;
    esac
    
    log_acl "Compliance check completed for $standard"
}

# Example usage and policy implementation
SECURE_DIR="/data/secure"
PUBLIC_DIR="/data/public"
FILESYSTEM="/data"

# Create quota policy file
cat > /tmp/quota_policy.csv << 'EOF'
# user_type,name,soft_limit_kb,hard_limit_kb,grace_period
user,alice,1048576,1153024,7days
user,bob,2097152,2306048,7days
group,developers,10485760,11534336,14days
group,staff,5242880,5767168,14days
EOF

# Setup comprehensive storage security
setup_advanced_acls "$SECURE_DIR" "high"
setup_advanced_acls "$PUBLIC_DIR" "low"

setup_filesystem_quotas "$FILESYSTEM" "user"
setup_filesystem_quotas "$FILESYSTEM" "group"
manage_quota_policies "$FILESYSTEM" "/tmp/quota_policy.csv"

# Start monitoring
monitor_quota_usage "$FILESYSTEM" 80 &

# Perform audits
audit_storage_access "$SECURE_DIR"
check_compliance_standards "$FILESYSTEM" "pci"

log_acl "Storage security setup completed"
log_quota "Quota management setup completed"
```

## Lab Exercises

### Lab 1: Advanced Partitioning and Filesystem Management

**Objective**: Master advanced partitioning techniques and filesystem optimization for enterprise storage requirements.

**Tasks**:
1. Create a comprehensive partitioning scheme using both MBR and GPT on different devices
2. Implement filesystem optimization for different workload types (database, web, general)
3. Configure and test filesystem mount options for performance and security
4. Implement filesystem monitoring and maintenance procedures
5. Design and test filesystem backup and recovery strategies

**Deliverables**:
- Complete partitioning documentation with performance benchmarks
- Filesystem optimization report comparing different configurations
- Automated maintenance scripts with scheduling
- Backup and recovery test results with validation procedures

**Assessment Criteria**:
- Partitioning accuracy and optimization (25%)
- Filesystem performance tuning effectiveness (25%)
- Monitoring and maintenance automation (25%)
- Backup and recovery reliability (25%)

### Lab 2: LVM Implementation and Management

**Objective**: Design and implement enterprise LVM infrastructure with advanced features and automation.

**Tasks**:
1. Create complex LVM hierarchy with multiple volume groups and logical volumes
2. Implement thin provisioning with monitoring and alerting
3. Design and test live volume expansion and contraction procedures
4. Create automated snapshot management with retention policies
5. Develop LVM performance monitoring and optimization procedures

**Deliverables**:
- Complete LVM infrastructure design documentation
- Thin provisioning implementation with monitoring dashboards
- Live operation procedures with testing validation
- Automated snapshot management system with rotation
- Performance optimization report with before/after metrics

**Assessment Criteria**:
- LVM architecture design and implementation (30%)
- Thin provisioning and monitoring effectiveness (25%)
- Live operations reliability and safety (25%)
- Automation quality and error handling (20%)

### Lab 3: RAID Configuration and Recovery

**Objective**: Build comprehensive RAID infrastructure with failure recovery and performance optimization.

**Tasks**:
1. Design and implement multiple RAID levels for different use cases
2. Create automated RAID monitoring and alerting systems
3. Test and document complete failure recovery procedures
4. Implement RAID performance optimization for different workloads
5. Develop disaster recovery and business continuity procedures

**Deliverables**:
- Multi-level RAID infrastructure with performance benchmarks
- Comprehensive monitoring and alerting system
- Complete failure recovery documentation with test results
- Performance optimization guide with workload-specific recommendations
- Disaster recovery plan with tested procedures

**Assessment Criteria**:
- RAID implementation complexity and reliability (30%)
- Monitoring and alerting effectiveness (25%)
- Recovery procedures thoroughness and testing (25%)
- Performance optimization results (20%)

### Lab 4: Storage Performance Optimization

**Objective**: Analyze and optimize storage performance for enterprise workloads with comprehensive monitoring.

**Tasks**:
1. Conduct baseline performance analysis across different storage types
2. Implement I/O optimization for SSD and HDD configurations
3. Design and deploy storage performance monitoring infrastructure
4. Optimize network storage configurations (NFS, iSCSI)
5. Create performance capacity planning and prediction models

**Deliverables**:
- Comprehensive performance baseline report
- I/O optimization implementation with measurable improvements
- Complete monitoring infrastructure with dashboards and alerting
- Network storage optimization guide with performance metrics
- Capacity planning model with growth predictions

**Assessment Criteria**:
- Performance analysis depth and accuracy (30%)
- Optimization implementation and effectiveness (25%)
- Monitoring infrastructure completeness (25%)
- Capacity planning accuracy and usefulness (20%)

### Lab 5: Enterprise Storage Infrastructure

**Objective**: Design and implement complete enterprise storage infrastructure with security, compliance, and automation.

**Tasks**:
1. Design comprehensive storage architecture for enterprise requirements
2. Implement storage security with encryption, access controls, and auditing
3. Create automated provisioning and management workflows
4. Develop compliance monitoring for industry standards (PCI, HIPAA, SOX)
5. Build complete disaster recovery and business continuity infrastructure

**Deliverables**:
- Enterprise storage architecture design with scalability planning
- Complete security implementation with compliance documentation
- Automated provisioning and management system
- Compliance monitoring and reporting infrastructure
- Tested disaster recovery and business continuity procedures

**Assessment Criteria**:
- Architecture design quality and scalability (25%)
- Security implementation and compliance coverage (25%)
- Automation effectiveness and reliability (25%)
- Disaster recovery completeness and testing (25%)

## Best Practices

### Storage Architecture Design
- **Capacity Planning**: Plan for 3-5 years growth with 20% buffer for unexpected expansion
- **Performance Requirements**: Match storage technology to workload IOPS and throughput needs
- **Redundancy Strategy**: Implement appropriate RAID levels based on availability and performance requirements
- **Scalability Design**: Use LVM and modular architecture for easy expansion
- **Network Integration**: Design storage networks with adequate bandwidth and redundancy

### Performance Optimization
- **I/O Scheduler Selection**: Use appropriate schedulers (none for SSDs, mq-deadline for HDDs)
- **Filesystem Tuning**: Optimize mount options and filesystem parameters for workload types
- **Cache Configuration**: Implement appropriate caching strategies at multiple levels
- **Alignment Optimization**: Ensure proper partition and filesystem alignment for performance
- **Monitoring Integration**: Implement comprehensive performance monitoring with trend analysis

### Security Implementation
- **Encryption Strategy**: Use LUKS for data at rest and secure key management
- **Access Controls**: Implement ACLs and quotas for granular access management
- **Audit Logging**: Enable comprehensive audit logging for compliance requirements
- **Network Security**: Secure storage networks with proper segmentation and authentication
- **Regular Security Audits**: Perform periodic security assessments and vulnerability scans

### Operational Excellence
- **Automation**: Automate routine tasks including monitoring, backups, and maintenance
- **Documentation**: Maintain comprehensive documentation of all storage configurations
- **Change Management**: Implement proper change control procedures for storage modifications
- **Testing Procedures**: Regular testing of backup, recovery, and disaster recovery procedures
- **Staff Training**: Ensure staff are trained on storage technologies and emergency procedures

## Troubleshooting

### Common Storage Issues

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| **Partition Table Corruption** | Device not recognized, boot failures | Use gdisk/fdisk recovery, restore from backup |
| **Filesystem Corruption** | I/O errors, mount failures | Run fsck, restore from backup if necessary |
| **LVM Volume Issues** | Cannot access logical volumes | Check PV/VG status, use vgchange to activate |
| **RAID Degradation** | Performance issues, error messages | Replace failed drives, monitor rebuild process |
| **Performance Problems** | Slow I/O, high wait times | Check I/O scheduler, optimize mount options |
| **Quota Exceeded** | Write failures, application errors | Increase quotas or clean up space |
| **Encryption Problems** | Cannot unlock containers | Check key files, verify passphrase |

### Diagnostic Techniques
```bash
# Storage health monitoring
smartctl -a /dev/sda              # Check drive health
hdparm -I /dev/sda               # Drive information
iostat -x 1                      # I/O performance monitoring
iotop -o                         # Process I/O usage

# Filesystem diagnostics
fsck.ext4 -n /dev/sda1           # Check filesystem (read-only)
tune2fs -l /dev/sda1             # Filesystem parameters
xfs_info /mount/point            # XFS filesystem info
btrfs fi show                    # Btrfs filesystem status

# LVM diagnostics
pvdisplay -v                     # Physical volume details
vgdisplay -v                     # Volume group details
lvdisplay -v                     # Logical volume details
dmsetup info                     # Device mapper status

# RAID diagnostics
cat /proc/mdstat                 # RAID status
mdadm --detail /dev/md0          # Detailed RAID info
mdadm --examine /dev/sda1        # Examine RAID member
```

### Recovery Procedures
```bash
# Partition table recovery
gdisk /dev/sda                   # Use recovery options
testdisk                         # Advanced recovery tool
ddrescue /dev/sda /backup/sda.img # Image damaged drive

# Filesystem recovery
fsck -y /dev/sda1               # Automatic repair
debugfs /dev/sda1               # Advanced ext filesystem debugging
xfs_repair /dev/sda1            # XFS filesystem repair

# LVM recovery
vgchange -ay                    # Activate volume groups
vgscan --mknodes               # Recreate device nodes
vgcfgrestore                   # Restore VG configuration

# RAID recovery
mdadm --assemble --scan         # Auto-assemble arrays
mdadm --create --assume-clean   # Recreate array without sync
```

## Assessment Criteria

Students will be evaluated on their ability to:

| Criteria | Proficient (4) | Developing (3) | Beginning (2) | Inadequate (1) |
|----------|----------------|----------------|---------------|----------------|
| **Technical Implementation** | Implements complex storage solutions with advanced features and optimization | Implements storage solutions with good understanding of concepts | Basic implementation with some understanding gaps | Struggles with basic storage concepts |
| **Performance Optimization** | Achieves measurable performance improvements through systematic optimization | Shows good understanding of performance factors with some optimization | Basic performance awareness with limited optimization | Little understanding of performance optimization |
| **Security Implementation** | Implements comprehensive security with encryption, access controls, and compliance | Good security implementation with most controls in place | Basic security implementation with some gaps | Inadequate security implementation |
| **Problem Solving** | Systematically diagnoses and resolves complex storage issues | Good problem-solving skills with most issues resolved | Basic troubleshooting with some assistance needed | Struggles with basic troubleshooting |
| **Automation and Documentation** | Creates comprehensive automation with detailed documentation | Good automation with adequate documentation | Basic automation with minimal documentation | Little automation or documentation |

## Next Steps

After mastering storage and filesystem management, proceed to:

- **Module 11: ZFS Fundamentals** - Learn advanced filesystem features with ZFS including snapshots, compression, and data integrity
- **Module 12: Proxmox Virtual Environment** - Apply storage skills in virtualization contexts with advanced storage backends
- **Module 14: Proxmox Infrastructure Automation** - Integrate storage management into infrastructure automation workflows

The storage management skills developed in this module form the foundation for all enterprise infrastructure implementations, from virtualization platforms to container orchestration and cloud deployments.

---

**Module 10 Complete**: You have successfully mastered enterprise storage and filesystem management, from basic partitioning to advanced RAID configurations, LVM administration, and storage security. These skills provide the foundation for all enterprise infrastructure storage requirements.
       # First sector (default)
+10G   # Size
n      # New partition  
p      # Primary partition
2      # Partition number
       # First sector (default)
       # Last sector (use remaining space)
t      # Change partition type
2      # Partition number
8e     # Linux LVM type
p      # Print partition table
w      # Write changes
EOF

# Verify partition alignment (should be multiple of 4096)
sudo fdisk -l /dev/sdb | grep "^/dev"
sudo parted /dev/sdb align-check optimal 1
```

#### GPT Partitioning with gdisk
```bash
# Interactive gdisk session for GPT
sudo gdisk /dev/sdc

# Automated gdisk partitioning
sudo gdisk /dev/sdc << EOF
o      # Create new GPT partition table
y      # Confirm
n      # New partition
1      # Partition number
       # First sector (default - 2048 for alignment)
+512M  # Size for EFI System Partition
ef00   # EFI System partition type
n      # New partition
2      # Partition number
       # First sector (default)
+2G    # Size for boot partition
8300   # Linux filesystem type
n      # New partition
3      # Partition number
       # First sector (default)
       # Last sector (use remaining space)
8e00   # Linux LVM type
p      # Print partition table
w      # Write changes
y      # Confirm
EOF

# Verify GPT partition table
sudo gdisk -l /dev/sdc
sudo sgdisk --print /dev/sdc
```

### Advanced Partitioning Scenarios

#### Complex Partitioning with parted
```bash
# Create GPT table and aligned partitions
sudo parted /dev/sdd mklabel gpt

# Create EFI System Partition (aligned to 1MiB)
sudo parted /dev/sdd mkpart "EFI System" fat32 1MiB 513MiB
sudo parted /dev/sdd set 1 esp on

# Create boot partition
sudo parted /dev/sdd mkpart "Boot" ext4 513MiB 1537MiB
sudo parted /dev/sdd set 2 boot on

# Create root partition
sudo parted /dev/sdd mkpart "Root" ext4 1537MiB 51537MiB

# Create LVM partition for remaining space
sudo parted /dev/sdd mkpart "LVM" 51537MiB 100%
sudo parted /dev/sdd set 4 lvm on

# Verify optimal alignment
sudo parted /dev/sdd align-check optimal 1
sudo parted /dev/sdd align-check optimal 2
sudo parted /dev/sdd align-check optimal 3
sudo parted /dev/sdd align-check optimal 4

# Display detailed partition information
sudo parted /dev/sdd print
sudo parted /dev/sdd unit s print  # Show in sectors
```

#### Partition Resizing and Recovery
```bash
# Extend partition (parted)
sudo parted /dev/sdb resizepart 2 100%

# Shrink partition (requires unmounting first)
sudo umount /dev/sdb2
sudo e2fsck -f /dev/sdb2
sudo resize2fs /dev/sdb2 20G
sudo parted /dev/sdb resizepart 2 21GB

# Recover corrupted partition table
sudo testdisk /dev/sdb    # Interactive recovery tool
sudo photorec /dev/sdb    # File recovery

# Backup and restore partition table
sudo sfdisk -d /dev/sdb > sdb_partition_backup.txt
sudo sfdisk /dev/sdb < sdb_partition_backup.txt
```

### Filesystem Performance Tuning

#### ext4 Performance Optimization
```bash
# Create ext4 with performance optimizations
sudo mkfs.ext4 \
  -b 4096 \          # 4K block size
  -E stride=32,stripe-width=64 \  # RAID optimization
  -O ^has_journal \   # Disable journal for SSD
  -m 1 \             # 1% reserved blocks
  -L FAST_DATA \     # Filesystem label
  /dev/sdb1

# Tune existing ext4 filesystem
sudo tune2fs -o journal_data_writeback /dev/sdb1  # Fastest journaling
sudo tune2fs -O ^has_journal /dev/sdb1            # Remove journal
sudo tune2fs -c 0 -i 0 /dev/sdb1                 # Disable forced checks
sudo tune2fs -m 1 /dev/sdb1                      # Reduce reserved blocks

# Enable ext4 features for performance
sudo tune2fs -O extent /dev/sdb1                 # Enable extents
sudo tune2fs -O dir_index /dev/sdb1              # Enable directory indexing
```

#### XFS Performance Optimization
```bash
# Create XFS with performance optimizations
sudo mkfs.xfs \
  -b size=4096 \     # 4K block size
  -d su=64k,sw=4 \   # RAID stripe unit and width
  -l size=128m \     # Large log for performance
  -n size=8192 \     # Directory block size
  -L FAST_XFS \      # Filesystem label
  /dev/sdb2

# XFS performance tuning
sudo xfs_admin -L PERFORMANCE_XFS /dev/sdb2  # Set label
sudo xfs_admin -U generate /dev/sdb2         # Generate new UUID

# XFS-specific mount options for performance
mount -t xfs -o noatime,nobarrier,logbufs=8,logbsize=256k /dev/sdb2 /mnt/xfs
```

### Mount Options Optimization

#### Performance-Oriented Mount Options
```bash
# High-performance mount options for different workloads

# Database workload (consistency important)
sudo mount -o rw,noatime,data=ordered,barrier=1,commit=5 /dev/sdb1 /var/lib/mysql

# Web server workload (performance priority)
sudo mount -o rw,noatime,data=writeback,nobarrier,commit=60 /dev/sdb2 /var/www

# SSD optimization
sudo mount -o rw,noatime,discard,data=ordered /dev/sdb3 /mnt/ssd

# Network storage caching
sudo mount -o rw,noatime,_netdev,cache=strict /dev/sdb4 /mnt/network

# /etc/fstab examples with performance tuning
cat >> /etc/fstab << 'EOF'
# High-performance database storage
UUID=db-volume-uuid /var/lib/mysql ext4 rw,noatime,data=ordered,barrier=1,commit=5 0 2

# Web content with writeback for speed
UUID=web-volume-uuid /var/www ext4 rw,noatime,data=writeback,nobarrier,commit=60 0 2

# SSD with TRIM support
UUID=ssd-volume-uuid /mnt/ssd ext4 rw,noatime,discard 0 2

# Temporary storage (performance over safety)
tmpfs /tmp tmpfs rw,nosuid,nodev,noexec,relatime,size=2G 0 0
EOF
```

#### I/O Scheduler Optimization
```bash
# Check current I/O scheduler
cat /sys/block/sdb/queue/scheduler

# Set I/O scheduler for different storage types
# SSD: none (for NVMe) or mq-deadline
echo none | sudo tee /sys/block/nvme0n1/queue/scheduler

# HDD: mq-deadline or bfq
echo mq-deadline | sudo tee /sys/block/sdb/queue/scheduler

# Make scheduler changes persistent
echo 'ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/scheduler}="mq-deadline"' | \
  sudo tee /etc/udev/rules.d/60-ioschedulers.rules

echo 'ACTION=="add|change", KERNEL=="nvme[0-9]n[0-9]", ATTR{queue/scheduler}="none"' | \
  sudo tee -a /etc/udev/rules.d/60-ioschedulers.rules
```

### Filesystem Management

#### Creating Filesystems
```bash
# Create ext4 filesystem
sudo mkfs.ext4 /dev/sdb1

# Create ext4 with custom options
sudo mkfs.ext4 -L DATA -m 1 -O ^has_journal /dev/sdb1

# Create XFS filesystem
sudo mkfs.xfs -L BACKUP /dev/sdb2

# Create Btrfs filesystem
sudo mkfs.btrfs -L STORAGE /dev/sdb3

# View filesystem information
sudo dumpe2fs /dev/sdb1 | head -20
sudo xfs_info /dev/sdb2
```

#### Mounting and /etc/fstab
```bash
# Manual mounting
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data

# Mount with options
sudo mount -o rw,noatime,user_xattr /dev/sdb1 /mnt/data

# Unmount filesystem
sudo umount /mnt/data

# /etc/fstab example
UUID=12345678-1234-1234-1234-123456789012 /mnt/data ext4 defaults,noatime 0 2

# Test fstab entries
sudo mount -a
sudo findmnt --verify

# Mount by UUID
sudo mount UUID=12345678-1234-1234-1234-123456789012 /mnt/data
```

#### Filesystem Maintenance
```bash
# Check filesystem
sudo fsck /dev/sdb1
sudo fsck.ext4 -f /dev/sdb1

# Force check on next reboot
sudo tune2fs -c 1 /dev/sdb1

# Resize filesystem
# First resize partition, then filesystem
sudo resize2fs /dev/sdb1

# XFS filesystem growth
sudo xfs_growfs /mnt/data

# Check and repair XFS
sudo xfs_repair /dev/sdb2
```

### Live LVM Operations

#### Advanced LVM Setup and Management
```bash
# Initialize physical volumes with optimal alignment
sudo pvcreate --dataalignment 1m /dev/sdb /dev/sdc /dev/sdd

# Create volume group with specific PE size
sudo vgcreate --physicalextentsize 32M vg_production /dev/sdb /dev/sdc

# Create logical volumes with different strategies
sudo lvcreate --size 20G --name lv_database vg_production
sudo lvcreate --extents 100%FREE --name lv_storage vg_production

# Create striped LV for performance
sudo lvcreate --size 50G --stripes 2 --stripesize 64K --name lv_fast vg_production

# Display detailed LVM information
sudo pvdisplay -v
sudo vgdisplay -v vg_production
sudo lvdisplay -v /dev/vg_production/lv_database
```

#### Live Volume Operations (No Downtime)
```bash
# Extend volume group with new physical volume
sudo pvcreate /dev/sde
sudo vgextend vg_production /dev/sde

# Online logical volume extension
sudo lvextend --size +10G /dev/vg_production/lv_database
sudo resize2fs /dev/vg_production/lv_database  # For ext4
# OR for XFS:
sudo xfs_growfs /mnt/database

# Online logical volume reduction (ext4 only - requires downtime for safety)
sudo umount /mnt/storage
sudo e2fsck -f /dev/vg_production/lv_storage
sudo resize2fs /dev/vg_production/lv_storage 30G
sudo lvreduce --size 30G /dev/vg_production/lv_storage
sudo mount /dev/vg_production/lv_storage /mnt/storage

# Move data between physical volumes (online)
sudo pvmove /dev/sdb /dev/sde  # Move all data from sdb to sde
sudo pvmove /dev/sdb:1000-2000 /dev/sde  # Move specific extents

# Remove physical volume from volume group
sudo vgreduce vg_production /dev/sdb
sudo pvremove /dev/sdb
```

#### LVM Performance Optimization
```bash
# Create RAID logical volumes for performance and redundancy
sudo lvcreate --type raid1 --mirrors 1 --size 20G --name lv_raid1 vg_production
sudo lvcreate --type raid5 --stripes 3 --size 100G --name lv_raid5 vg_production
sudo lvcreate --type raid10 --stripes 2 --mirrors 1 --size 50G --name lv_raid10 vg_production

# Monitor RAID LV status
sudo lvs -a -o name,copy_percent,sync_percent,lv_attr

# Create thin-provisioned volumes for storage efficiency
sudo lvcreate --type thin-pool --size 200G --name thin_pool vg_production
sudo lvcreate --thin vg_production/thin_pool --virtualsize 50G --name thin_vol1
sudo lvcreate --thin vg_production/thin_pool --virtualsize 30G --name thin_vol2

# Monitor thin pool usage
sudo lvs -o name,data_percent,metadata_percent vg_production
```

### LVM Snapshot Management

#### Comprehensive Snapshot Operations
```bash
# Create snapshot with sufficient space for changes
sudo lvcreate --size 5G --snapshot --name lv_database_snap /dev/vg_production/lv_database

# Create snapshot with automatic sizing (10% of origin)
sudo lvcreate --extents 10%ORIGIN --snapshot --name lv_auto_snap /dev/vg_production/lv_storage

# Mount snapshot for backup or testing
sudo mkdir /mnt/backup_snapshot
sudo mount /dev/vg_production/lv_database_snap /mnt/backup_snapshot

# Perform backup from snapshot (consistent point-in-time)
sudo tar -czf /backup/database-$(date +%Y%m%d).tar.gz -C /mnt/backup_snapshot .
sudo rsync -av /mnt/backup_snapshot/ /backup/snapshot_copy/

# Monitor snapshot usage
sudo lvs -o name,origin,snap_percent vg_production

# Extend snapshot if running out of space
sudo lvextend --size +2G /dev/vg_production/lv_database_snap

# Merge snapshot back to origin (reverts origin to snapshot state)
sudo umount /mnt/backup_snapshot
sudo umount /mnt/database  # Unmount origin
sudo lvconvert --merge /dev/vg_production/lv_database_snap
# Note: Merge completes on next activation of origin

# Remove snapshot
sudo umount /mnt/backup_snapshot
sudo lvremove /dev/vg_production/lv_database_snap
```

#### Automated Snapshot Script
```bash
#!/bin/bash
# Advanced LVM snapshot backup script

LV_PATH="/dev/vg_production/lv_database"
SNAP_NAME="lv_database_backup_$(date +%Y%m%d_%H%M%S)"
SNAP_SIZE="5G"
MOUNT_POINT="/mnt/snapshot_backup"
BACKUP_DIR="/backup/lvm_snapshots"
RETENTION_DAYS=7

create_snapshot() {
    echo "Creating snapshot: $SNAP_NAME"
    sudo lvcreate --size $SNAP_SIZE --snapshot --name "$SNAP_NAME" "$LV_PATH"
    
    if [ $? -eq 0 ]; then
        echo "Snapshot created successfully"
        return 0
    else
        echo "Failed to create snapshot"
        return 1
    fi
}

mount_snapshot() {
    sudo mkdir -p "$MOUNT_POINT"
    sudo mount "/dev/vg_production/$SNAP_NAME" "$MOUNT_POINT"
    
    if [ $? -eq 0 ]; then
        echo "Snapshot mounted at $MOUNT_POINT"
        return 0
    else
        echo "Failed to mount snapshot"
        return 1
    fi
}

backup_data() {
    local backup_file="$BACKUP_DIR/backup_$(date +%Y%m%d_%H%M%S).tar.gz"
    sudo mkdir -p "$BACKUP_DIR"
    
    echo "Creating backup: $backup_file"
    sudo tar -czf "$backup_file" -C "$MOUNT_POINT" .
    
    if [ $? -eq 0 ]; then
        echo "Backup completed: $backup_file"
        return 0
    else
        echo "Backup failed"
        return 1
    fi
}

cleanup_snapshot() {
    sudo umount "$MOUNT_POINT" 2>/dev/null
    sudo lvremove -f "/dev/vg_production/$SNAP_NAME" 2>/dev/null
    sudo rmdir "$MOUNT_POINT" 2>/dev/null
    echo "Snapshot cleanup completed"
}

cleanup_old_backups() {
    echo "Cleaning up backups older than $RETENTION_DAYS days"
    find "$BACKUP_DIR" -name "backup_*.tar.gz" -mtime +$RETENTION_DAYS -delete
}

# Main execution
main() {
    if create_snapshot && mount_snapshot && backup_data; then
        echo "Backup process completed successfully"
        cleanup_old_backups
        cleanup_snapshot
        exit 0
    else
        echo "Backup process failed"
        cleanup_snapshot
        exit 1
    fi
}

main "$@"
```

### RAID Implementation and Management

#### Software vs Hardware RAID Analysis
```bash
# Check for hardware RAID controllers
sudo lspci | grep -i raid
sudo lshw -class storage
sudo dmidecode -t system

# Hardware RAID information (if available)
sudo megacli -AdpAllInfo -aALL  # LSI MegaRAID
sudo hpssacli ctrl all show config  # HP Smart Array

# Software RAID advantages: flexibility, cost, transparency
# Hardware RAID advantages: performance, CPU offload, battery backup
```

#### RAID Level Implementation and Performance
```bash
# RAID 0 - Striping (Performance, No Redundancy)
sudo mdadm --create /dev/md0 \
  --level=0 \
  --raid-devices=2 \
  --chunk=64 \
  /dev/sdb /dev/sdc

# RAID 1 - Mirroring (Redundancy, Read Performance)
sudo mdadm --create /dev/md1 \
  --level=1 \
  --raid-devices=2 \
  /dev/sdd /dev/sde

# RAID 5 - Distributed Parity (Balance of Performance/Redundancy)
sudo mdadm --create /dev/md2 \
  --level=5 \
  --raid-devices=3 \
  --chunk=64 \
  --spare-devices=1 \
  /dev/sdf /dev/sdg /dev/sdh /dev/sdi

# RAID 6 - Double Parity (High Redundancy)
sudo mdadm --create /dev/md3 \
  --level=6 \
  --raid-devices=4 \
  --chunk=64 \
  /dev/sdj /dev/sdk /dev/sdl /dev/sdm

# RAID 10 - Striped Mirrors (High Performance + Redundancy)
sudo mdadm --create /dev/md4 \
  --level=10 \
  --raid-devices=4 \
  --chunk=64 \
  /dev/sdn /dev/sdo /dev/sdp /dev/sdq

# Check RAID creation progress
watch cat /proc/mdstat
sudo mdadm --detail /dev/md0
```

#### Advanced RAID Configuration
```bash
# Create RAID with custom parameters
sudo mdadm --create /dev/md5 \
  --level=5 \
  --raid-devices=4 \
  --spare-devices=2 \
  --chunk=128 \
  --bitmap=internal \
  --assume-clean \
  /dev/sdr /dev/sds /dev/sdt /dev/sdu /dev/sdv /dev/sdw

# RAID performance tuning
echo 8192 | sudo tee /sys/block/md5/md/stripe_cache_size  # RAID 5/6 cache
echo 1024 | sudo tee /sys/block/md5/queue/read_ahead_kb   # Read-ahead
echo mq-deadline | sudo tee /sys/block/md5/queue/scheduler

# Set RAID synchronization speed
echo 200000 | sudo tee /proc/sys/dev/raid/speed_limit_min
echo 500000 | sudo tee /proc/sys/dev/raid/speed_limit_max

# Configure RAID monitoring
sudo mdadm --monitor --daemon --mail=admin@example.com --delay=300 /dev/md0 /dev/md1 /dev/md2

# Save RAID configuration
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
sudo update-initramfs -u
```

#### RAID Performance Analysis
```bash
# RAID performance testing
sudo hdparm -tT /dev/md0  # Raw throughput test
sudo dd if=/dev/zero of=/dev/md0 bs=1M count=1000 oflag=direct  # Write test
sudo dd if=/dev/md0 of=/dev/null bs=1M count=1000 iflag=direct  # Read test

# Advanced performance testing with fio
sudo fio --name=raid_test \
  --ioengine=libaio \
  --iodepth=32 \
  --rw=randwrite \
  --bs=4k \
  --direct=1 \
  --size=1G \
  --numjobs=4 \
  --runtime=300 \
  --group_reporting \
  --filename=/dev/md0

# Monitor RAID I/O statistics
iostat -x 1 5
sar -d 1 5
sudo iotop -o -d 1
```

### RAID Disaster Recovery

#### Complete RAID Failure Recovery Procedures
```bash
# Simulate disk failure for testing
sudo mdadm --manage /dev/md1 --fail /dev/sde
sudo mdadm --manage /dev/md1 --remove /dev/sde

# Check RAID status after failure
cat /proc/mdstat
sudo mdadm --detail /dev/md1

# Replace failed disk (hot swap scenario)
# 1. Physically replace the disk
# 2. Partition the new disk identically
sudo sfdisk -d /dev/sdd | sudo sfdisk /dev/sde  # Copy partition table

# Add new disk to RAID array
sudo mdadm --manage /dev/md1 --add /dev/sde1

# Monitor rebuild progress
watch -n 1 'cat /proc/mdstat'
sudo mdadm --detail /dev/md1

# Force RAID assembly if metadata is corrupted
sudo mdadm --assemble --force /dev/md1 /dev/sdd1 /dev/sde1

# Rebuild array from partial information
sudo mdadm --create /dev/md1 \
  --level=1 \
  --raid-devices=2 \
  --force \
  /dev/sdd1 missing

# Add second device after array is functional
sudo mdadm --manage /dev/md1 --add /dev/sde1
```

#### RAID Recovery Scripts
```bash
#!/bin/bash
# RAID monitoring and automated recovery script

RAID_DEVICES=("/dev/md0" "/dev/md1" "/dev/md2")
EMAIL="admin@example.com"
LOG_FILE="/var/log/raid_monitor.log"

check_raid_status() {
    local md_device="$1"
    local status=$(cat /proc/mdstat | grep -A 3 $(basename $md_device))
    local failed_count=$(sudo mdadm --detail $md_device | grep -c "failed")
    
    if [ "$failed_count" -gt 0 ]; then
        echo "$(date): RAID failure detected on $md_device" | tee -a $LOG_FILE
        return 1
    fi
    
    # Check for degraded state
    if echo "$status" | grep -q "_"; then
        echo "$(date): RAID $md_device is degraded" | tee -a $LOG_FILE
        return 2
    fi
    
    return 0
}

send_alert() {
    local message="$1"
    echo "$message" | mail -s "RAID Alert - $(hostname)" $EMAIL
    echo "$(date): Alert sent - $message" >> $LOG_FILE
}

auto_recovery() {
    local md_device="$1"
    
    # Attempt to re-add any removed devices
    local spare_devices=$(sudo mdadm --detail $md_device | grep "spare" | awk '{print $7}')
    
    for spare in $spare_devices; do
        echo "$(date): Attempting auto-recovery with spare $spare" >> $LOG_FILE
        sudo mdadm --manage $md_device --re-add $spare
    done
}

main() {
    for raid_device in "${RAID_DEVICES[@]}"; do
        if [ -e "$raid_device" ]; then
            check_raid_status "$raid_device"
            status=$?
            
            case $status in
                1)  # Failed
                    send_alert "CRITICAL: RAID failure on $raid_device"
                    auto_recovery "$raid_device"
                    ;;
                2)  # Degraded
                    send_alert "WARNING: RAID $raid_device is degraded"
                    ;;
                0)  # OK
                    echo "$(date): $raid_device status OK" >> $LOG_FILE
                    ;;
            esac
        fi
    done
}

# Run main function
main "$@"
```

### Storage Performance Monitoring

#### Comprehensive I/O Analysis
```bash
# Real-time I/O monitoring
sudo iotop -a -o -d 1  # Show accumulated I/O and processes causing I/O
sudo iotop -P -d 1     # Show processes instead of threads

# Historical I/O statistics
sar -d 1 5             # Device utilization
sar -b 1 5             # I/O and transfer rate statistics
iostat -x 1 5          # Extended I/O statistics

# Detailed block device statistics
cat /proc/diskstats
cat /sys/block/sda/stat

# I/O latency analysis
sudo ioping -c 10 /dev/sda        # Simple latency test
sudo ioping -RL /dev/sda          # Latency and request size analysis

# Advanced I/O tracing
sudo blktrace -d /dev/sda -o trace
sudo blkparse trace.blktrace.0    # Parse trace data

# Memory and cache impact
cat /proc/meminfo | grep -E "(Dirty|Writeback|Cached)"
sudo sysctl vm.dirty_ratio vm.dirty_background_ratio vm.dirty_expire_centisecs
```

#### Storage Benchmarking Suite
```bash
#!/bin/bash
# Comprehensive storage performance testing

DEVICE="/dev/sdb"
MOUNT_POINT="/mnt/test"
RESULTS_DIR="/tmp/storage_benchmark_$(date +%Y%m%d_%H%M%S)"

setup_test_environment() {
    mkdir -p "$RESULTS_DIR"
    echo "Starting storage benchmark for $DEVICE" | tee "$RESULTS_DIR/benchmark.log"
    
    # Ensure device is not mounted
    sudo umount "$DEVICE" 2>/dev/null || true
    
    # Create test filesystem
    sudo mkfs.ext4 -F "$DEVICE"
    sudo mkdir -p "$MOUNT_POINT"
    sudo mount "$DEVICE" "$MOUNT_POINT"
}

sequential_performance() {
    echo "Testing sequential performance..." | tee -a "$RESULTS_DIR/benchmark.log"
    
    # Sequential write
    sudo fio --name=seq_write \
        --ioengine=libaio \
        --iodepth=32 \
        --rw=write \
        --bs=1M \
        --direct=1 \
        --size=2G \
        --numjobs=1 \
        --runtime=60 \
        --group_reporting \
        --filename="$MOUNT_POINT/seq_write_test" \
        --output="$RESULTS_DIR/seq_write.json" \
        --output-format=json
    
    # Sequential read
    sudo fio --name=seq_read \
        --ioengine=libaio \
        --iodepth=32 \
        --rw=read \
        --bs=1M \
        --direct=1 \
        --size=2G \
        --numjobs=1 \
        --runtime=60 \
        --group_reporting \
        --filename="$MOUNT_POINT/seq_read_test" \
        --output="$RESULTS_DIR/seq_read.json" \
        --output-format=json
}

random_performance() {
    echo "Testing random I/O performance..." | tee -a "$RESULTS_DIR/benchmark.log"
    
    # Random write IOPS
    sudo fio --name=rand_write \
        --ioengine=libaio \
        --iodepth=64 \
        --rw=randwrite \
        --bs=4k \
        --direct=1 \
        --size=1G \
        --numjobs=4 \
        --runtime=60 \
        --group_reporting \
        --filename="$MOUNT_POINT/rand_write_test" \
        --output="$RESULTS_DIR/rand_write.json" \
        --output-format=json
    
    # Random read IOPS
    sudo fio --name=rand_read \
        --ioengine=libaio \
        --iodepth=64 \
        --rw=randread \
        --bs=4k \
        --direct=1 \
        --size=1G \
        --numjobs=4 \
        --runtime=60 \
        --group_reporting \
        --filename="$MOUNT_POINT/rand_read_test" \
        --output="$RESULTS_DIR/rand_read.json" \
        --output-format=json
}

latency_testing() {
    echo "Testing I/O latency..." | tee -a "$RESULTS_DIR/benchmark.log"
    
    # Low queue depth latency test
    sudo fio --name=latency_test \
        --ioengine=libaio \
        --iodepth=1 \
        --rw=randread \
        --bs=4k \
        --direct=1 \
        --size=100M \
        --numjobs=1 \
        --runtime=30 \
        --group_reporting \
        --filename="$MOUNT_POINT/latency_test" \
        --output="$RESULTS_DIR/latency.json" \
        --output-format=json
}

cleanup_test() {
    sudo umount "$MOUNT_POINT"
    echo "Benchmark completed. Results stored in: $RESULTS_DIR"
}

# Main execution
setup_test_environment
sequential_performance
random_performance
latency_testing
cleanup_test
```

### SSD Optimization Techniques

#### SSD-Specific Configuration
```bash
# Check if device is SSD
sudo lsblk -d -o name,rota
cat /sys/block/sda/queue/rotational  # 0 = SSD, 1 = HDD

# Enable TRIM support
sudo fstrim -v /                      # Manual TRIM
sudo systemctl enable fstrim.timer    # Automatic weekly TRIM

# SSD-optimized filesystem creation
sudo mkfs.ext4 \
  -O ^has_journal \     # Disable journal for SSD
  -E discard \          # Enable TRIM during format
  -m 1 \               # Reduce reserved blocks
  /dev/sdb1

# SSD mount options
sudo mount -o rw,noatime,discard,data=ordered /dev/sdb1 /mnt/ssd

# /etc/fstab for SSD
UUID=ssd-uuid /mnt/ssd ext4 rw,noatime,discard 0 2

# I/O scheduler optimization for SSD
echo none | sudo tee /sys/block/sdb/queue/scheduler      # For NVMe
echo mq-deadline | sudo tee /sys/block/sdb/queue/scheduler  # For SATA SSD

# Disable write cache if UPS protection unavailable
sudo hdparm -W 0 /dev/sdb  # Disable write cache
sudo hdparm -W 1 /dev/sdb  # Enable write cache (default)

# Monitor SSD health and wear
sudo smartctl -a /dev/sdb | grep -E "(Wear_Leveling|SSD_Life_Left|Total_LBAs)"
sudo nvme smart-log /dev/nvme0n1  # For NVMe drives
```

#### SSD Performance Optimization
```bash
# NVMe-specific optimizations
echo none | sudo tee /sys/block/nvme0n1/queue/scheduler
echo 1 | sudo tee /sys/block/nvme0n1/queue/nomerges
echo 256 | sudo tee /sys/block/nvme0n1/queue/nr_requests

# Reduce swappiness for SSD longevity
echo 'vm.swappiness=1' | sudo tee -a /etc/sysctl.conf

# Optimize dirty page writeback for SSD
echo 'vm.dirty_background_ratio=5' | sudo tee -a /etc/sysctl.conf
echo 'vm.dirty_ratio=10' | sudo tee -a /etc/sysctl.conf
echo 'vm.dirty_expire_centisecs=3000' | sudo tee -a /etc/sysctl.conf

# Apply immediately
sudo sysctl -p

# SSD over-provisioning check
sudo hdparm -I /dev/sdb | grep -i "max.*LBA"
# Compare with actual usable space to determine over-provisioning
```

### Filesystem Quotas

#### Setting up Quotas
```bash
# Add quota options to /etc/fstab
/dev/sdb1 /home ext4 defaults,usrquota,grpquota 0 2

# Remount with quota options
sudo mount -o remount /home

# Create quota files
sudo quotacheck -cum /home

# Turn on quotas
sudo quotaon /home

# Set user quota
sudo edquota -u username

# Set group quota
sudo edquota -g groupname

# Check quota usage
quota -u username
sudo repquota /home
```

### Access Control Lists (ACLs)

#### ACL Management
```bash
# View ACLs
getfacl filename

# Set ACL for user
setfacl -m u:username:rw filename

# Set ACL for group
setfacl -m g:groupname:r filename

# Set default ACL for directory
setfacl -d -m u:username:rwx directory/

# Remove ACL
setfacl -x u:username filename

# Remove all ACLs
setfacl -b filename

# Copy ACLs
getfacl source_file | setfacl --set-file=- target_file
```

### Encrypted Filesystems (LUKS)

#### Setting up LUKS Encryption
```bash
# Format device with LUKS
sudo cryptsetup luksFormat /dev/sdb1

# Open encrypted device
sudo cryptsetup luksOpen /dev/sdb1 encrypted_data

# Create filesystem on encrypted device
sudo mkfs.ext4 /dev/mapper/encrypted_data

# Mount encrypted filesystem
sudo mount /dev/mapper/encrypted_data /mnt/encrypted

# Add to /etc/crypttab for auto-mounting
echo "encrypted_data /dev/sdb1 none luks" | sudo tee -a /etc/crypttab

# Close encrypted device
sudo umount /mnt/encrypted
sudo cryptsetup luksClose encrypted_data
```

## Storage Monitoring and Performance

### Performance Monitoring
```bash
# I/O statistics
iostat -x 1 5
sar -d 1 5

# Real-time I/O monitoring
iotop
sudo iotop -a

# Disk usage analysis
ncdu /
baobab  # GUI tool

# Check for disk errors
sudo dmesg | grep -i error
sudo smartctl -a /dev/sda

# Monitor RAID health
watch -n 1 cat /proc/mdstat
```

### Performance Optimization
```bash
# Tune filesystem for performance
sudo tune2fs -o journal_data_writeback /dev/sdb1

# Set I/O scheduler
echo deadline | sudo tee /sys/block/sdb/queue/scheduler

# Mount options for performance
mount -o noatime,nodiratime,data=writeback /dev/sdb1 /mnt/data

# SSD optimization
# Enable TRIM
sudo fstrim /
# Add to crontab for weekly TRIM
echo "0 2 * * 0 root /sbin/fstrim /" | sudo tee -a /etc/crontab
```

## Storage Best Practices and Performance Tuning

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| **Partition Alignment** | Align partitions to 1MiB boundaries | Use `parted` with 1MiB start sector |
| **Filesystem Selection** | Match filesystem to workload | ext4 for general use, XFS for large files, Btrfs for snapshots |
| **Mount Options** | Optimize for performance vs safety | `noatime` for performance, `data=ordered` for safety |
| **I/O Scheduler** | Match scheduler to storage type | `none` for NVMe, `mq-deadline` for SSD, `bfq` for HDD |
| **RAID Level Selection** | Balance performance and redundancy | RAID 10 for databases, RAID 5 for general storage |
| **LVM Design** | Plan logical volume layout | Separate VGs for different performance requirements |
| **Monitoring** | Implement proactive monitoring | SMART monitoring, capacity alerts, performance baselines |
| **Backup Strategy** | Regular, tested backups | LVM snapshots for consistency, offsite replication |
| **Capacity Planning** | Monitor growth trends | Alert at 80% capacity, plan expansion in advance |
| **Security** | Encrypt sensitive data | LUKS for full disk encryption, secure key management |

## Advanced Troubleshooting Guide

### Performance Issues

#### Identifying Storage Bottlenecks
```bash
# Real-time performance analysis
sudo iotop -a -o -d 1     # Show accumulated I/O by process
sudo iostat -x 1 5        # Extended device statistics
sudo sar -d 1 5          # Historical I/O patterns

# Check for I/O wait
top                       # Look for high %wa (I/O wait)
vmstat 1 5               # Monitor I/O statistics
cat /proc/loadavg        # Check load average

# Analyze slow queries (if database server)
sudo pt-query-digest /var/log/mysql/slow.log  # MySQL
sudo pg_stat_statements;  # PostgreSQL

# Storage latency investigation
sudo ioping /dev/sda      # Test storage latency
sudo fio --name=latency --ioengine=libaio --iodepth=1 --rw=randread --bs=4k --direct=1 --size=100M --runtime=30 --filename=/dev/sda

# Memory and caching analysis
free -h                   # Check available memory
cat /proc/meminfo | grep -E "(Dirty|Writeback|Cached)"
sync; echo 3 | sudo tee /proc/sys/vm/drop_caches  # Clear caches for testing
```

#### Storage Performance Tuning Solutions
```bash
# Optimize I/O scheduler
echo mq-deadline | sudo tee /sys/block/sda/queue/scheduler

# Adjust read-ahead
sudo blockdev --setra 4096 /dev/sda  # Set read-ahead to 2MB

# Tune filesystem parameters
sudo tune2fs -o journal_data_writeback /dev/sda1  # Fastest ext4 journaling
sudo mount -o remount,noatime,data=writeback /dev/sda1

# Optimize dirty page handling
echo 'vm.dirty_background_ratio=5' >> /etc/sysctl.conf
echo 'vm.dirty_ratio=10' >> /etc/sysctl.conf
echo 'vm.dirty_expire_centisecs=3000' >> /etc/sysctl.conf
sudo sysctl -p

# RAID performance tuning
echo 8192 | sudo tee /sys/block/md0/md/stripe_cache_size  # RAID 5/6
echo 200000 | sudo tee /proc/sys/dev/raid/speed_limit_min
```

### RAID Issues

#### RAID Failure Diagnosis and Recovery
```bash
# Comprehensive RAID health check
cat /proc/mdstat
sudo mdadm --detail /dev/md0
sudo mdadm --examine /dev/sdb1 /dev/sdc1

# Check for disk errors
sudo dmesg | grep -i "error\|fail"
sudo journalctl -u mdmonitor
sudo smartctl -a /dev/sdb

# Force RAID consistency check
echo check | sudo tee /sys/block/md0/md/sync_action
echo repair | sudo tee /sys/block/md0/md/sync_action

# RAID emergency recovery
sudo mdadm --assemble --force /dev/md0 /dev/sdb1 /dev/sdc1
sudo mdadm --create /dev/md0 --assume-clean --level=1 --raid-devices=2 /dev/sdb1 missing

# Recover RAID metadata
sudo mdadm --examine --scan >> /etc/mdadm/mdadm.conf.new
sudo mdadm --assemble --scan
```

### LVM Issues

#### LVM Recovery and Troubleshooting
```bash
# LVM metadata backup and recovery
sudo vgcfgbackup vg_production  # Backup LVM metadata
sudo vgcfgrestore -l vg_production  # List available backups
sudo vgcfgrestore -f /etc/lvm/backup/vg_production vg_production  # Restore

# Recover from missing physical volume
sudo vgreduce --removemissing vg_production
sudo vgextend vg_production /dev/new_disk

# LVM debugging
sudo vgscan -v
sudo pvscan -v
sudo lvscan -v

# Activate inactive volumes
sudo vgchange -ay vg_production
sudo lvchange -ay /dev/vg_production/lv_database

# Repair corrupted LVM metadata
sudo vgck vg_production
sudo pvck /dev/sdb1
```

### Filesystem Corruption

#### Filesystem Repair and Recovery
```bash
# ext4 filesystem repair
sudo umount /dev/sdb1
sudo e2fsck -f -y /dev/sdb1     # Force check and auto-fix
sudo e2fsck -c /dev/sdb1        # Check for bad blocks
sudo e2fsck -fDy /dev/sdb1      # Optimize directories and fix

# XFS filesystem repair
sudo umount /dev/sdb2
sudo xfs_repair -v /dev/sdb2
sudo xfs_repair -L /dev/sdb2    # Force log zeroing (data loss possible)

# Check filesystem superblock
sudo dumpe2fs /dev/sdb1 | grep -i superblock
sudo fsck.ext4 -b 32768 /dev/sdb1  # Use backup superblock

# Recover deleted files
sudo testdisk /dev/sdb           # Interactive recovery
sudo photorec /dev/sdb           # Automated file recovery
sudo debugfs /dev/sdb1           # Manual ext4 debugging
```

### Mount and Access Issues

#### Mount Problem Resolution
```bash
# Identify processes using mount point
sudo lsof +D /mnt/data
sudo fuser -v /mnt/data
sudo fuser -k /mnt/data          # Kill processes (careful!)

# Force unmount
sudo umount -f /mnt/data         # Force unmount
sudo umount -l /mnt/data         # Lazy unmount

# Debug mount failures
sudo mount -v /dev/sdb1 /mnt/data
sudo dmesg | tail -20
sudo journalctl -xe

# Check filesystem type
sudo blkid /dev/sdb1
sudo file -s /dev/sdb1

# Repair fstab issues
sudo mount -a                   # Test all fstab entries
sudo findmnt --verify           # Verify fstab syntax
```

### Storage Security Issues

#### Security Troubleshooting
```bash
# Check permissions and ownership
ls -la /mnt/data/
sudo lsattr /mnt/data/          # Check extended attributes
getfacl /mnt/data/              # Check ACLs

# SELinux context issues (if applicable)
ls -Z /mnt/data/
sudo restorecon -Rv /mnt/data/

# LUKS encryption issues
sudo cryptsetup luksDump /dev/sdb1
sudo cryptsetup luksOpen --test-passphrase /dev/sdb1
sudo cryptsetup repair /dev/sdb1
```

## Disaster Recovery Procedures

### Complete System Recovery Script
```bash
#!/bin/bash
# Comprehensive storage disaster recovery script

BACKUP_DIR="/backup/system"
LOG_FILE="/var/log/disaster_recovery.log"
DATE=$(date +%Y%m%d_%H%M%S)

log_message() {
    echo "$(date): $1" | tee -a "$LOG_FILE"
}

backup_partition_tables() {
    log_message "Backing up partition tables..."
    
    for disk in $(lsblk -d -n -o NAME | grep -E '^sd|^nvme'); do
        sudo sfdisk -d /dev/$disk > "$BACKUP_DIR/partition_table_${disk}_${DATE}.txt"
        sudo gdisk -l /dev/$disk > "$BACKUP_DIR/gpt_info_${disk}_${DATE}.txt" 2>/dev/null
    done
}

backup_lvm_metadata() {
    log_message "Backing up LVM metadata..."
    
    sudo vgcfgbackup
    sudo cp -r /etc/lvm/backup "$BACKUP_DIR/lvm_backup_$DATE"
    sudo pvs > "$BACKUP_DIR/pv_list_$DATE.txt"
    sudo vgs > "$BACKUP_DIR/vg_list_$DATE.txt"
    sudo lvs > "$BACKUP_DIR/lv_list_$DATE.txt"
}

backup_raid_config() {
    log_message "Backing up RAID configuration..."
    
    sudo mdadm --detail --scan > "$BACKUP_DIR/mdadm_config_$DATE.conf"
    cat /proc/mdstat > "$BACKUP_DIR/mdstat_$DATE.txt"
    
    for md in $(ls /dev/md* 2>/dev/null); do
        sudo mdadm --detail $md > "$BACKUP_DIR/raid_detail_$(basename $md)_$DATE.txt"
    done
}

backup_filesystem_info() {
    log_message "Backing up filesystem information..."
    
    sudo blkid > "$BACKUP_DIR/blkid_$DATE.txt"
    mount > "$BACKUP_DIR/mount_info_$DATE.txt"
    cp /etc/fstab "$BACKUP_DIR/fstab_$DATE.txt"
    df -h > "$BACKUP_DIR/disk_usage_$DATE.txt"
}

main() {
    mkdir -p "$BACKUP_DIR"
    log_message "Starting disaster recovery backup..."
    
    backup_partition_tables
    backup_lvm_metadata
    backup_raid_config
    backup_filesystem_info
    
    log_message "Disaster recovery backup completed successfully"
}

main "$@"
```

## Backup Strategies

### Backup Script Example
```bash
#!/bin/bash
# Advanced backup script with LVM snapshots

BACKUP_SOURCE="/var/www"
LV_PATH="/dev/vg_data/lv_web"
SNAPSHOT_NAME="lv_web_backup"
BACKUP_DEST="/backup"
DATE=$(date +%Y%m%d-%H%M%S)

# Create LVM snapshot
create_snapshot() {
    echo "Creating LVM snapshot..."
    sudo lvcreate -L 1G -s -n "$SNAPSHOT_NAME" "$LV_PATH"
    
    # Mount snapshot
    sudo mkdir -p /mnt/snapshot
    sudo mount "/dev/vg_data/$SNAPSHOT_NAME" /mnt/snapshot
}

# Perform backup
perform_backup() {
    echo "Starting backup..."
    
    tar -czf "$BACKUP_DEST/backup-$DATE.tar.gz" \
        -C /mnt/snapshot .
    
    echo "Backup completed: backup-$DATE.tar.gz"
}

# Cleanup snapshot
cleanup_snapshot() {
    echo "Cleaning up snapshot..."
    sudo umount /mnt/snapshot
    sudo lvremove -f "/dev/vg_data/$SNAPSHOT_NAME"
    sudo rmdir /mnt/snapshot
}

# Main execution
main() {
    create_snapshot
    perform_backup
    cleanup_snapshot
}

main "$@"
```

## Troubleshooting Common Issues

### Disk Issues
```bash
# Check filesystem errors
sudo dmesg | grep -i "file system"
sudo journalctl -u systemd-fsck*

# Repair filesystem
sudo fsck -y /dev/sdb1

# Check bad blocks
sudo badblocks -v /dev/sdb1

# SMART health check
sudo smartctl -H /dev/sda
sudo smartctl -a /dev/sda
```

### Mount Issues
```bash
# Check what's using a mount point
sudo lsof +D /mnt/data
sudo fuser -v /mnt/data

# Force unmount
sudo umount -f /mnt/data
sudo umount -l /mnt/data  # lazy unmount

# Check mount options
findmnt /mnt/data
mount | grep sdb1
```

## Lab Exercises

### Lab 1: Advanced Partitioning and Filesystem Tuning
**Objective**: Master fdisk/gdisk partitioning and filesystem performance optimization

**Tasks**:
1. Create a GPT partition table using gdisk with optimal alignment
2. Implement different filesystem types (ext4, XFS) with performance tuning
3. Compare mount options impact on performance using benchmarking tools
4. Configure I/O schedulers for different storage types (SSD vs HDD)

**Deliverables**: 
- Partition tables with 1MiB alignment
- Performance benchmark comparisons
- Optimized mount option configurations

### Lab 2: RAID Implementation and Disaster Recovery
**Objective**: Design and implement RAID configurations with failure recovery procedures

**Tasks**:
1. Create RAID 1, 5, and 10 arrays with hot spares
2. Simulate disk failures and perform recovery procedures
3. Implement RAID performance tuning and monitoring
4. Document complete disaster recovery procedures

**Deliverables**:
- Functional RAID arrays with monitoring
- Tested failure recovery procedures
- Performance optimization documentation

### Lab 3: Live LVM Operations and Snapshot Management
**Objective**: Perform LVM operations on live systems without downtime

**Tasks**:
1. Create LVM setup with multiple physical volumes and volume groups
2. Perform live volume extensions and reductions
3. Implement automated snapshot backup strategies
4. Test LVM disaster recovery scenarios

**Deliverables**:
- Live LVM operations without service interruption
- Automated backup scripts using snapshots
- LVM recovery procedures documentation

### Lab 4: Storage Performance Analysis and Optimization
**Objective**: Analyze and optimize storage performance for different workloads

**Tasks**:
1. Benchmark storage performance using multiple tools (fio, iostat, iotop)
2. Identify performance bottlenecks and implement optimizations
3. Tune filesystem parameters for database vs web server workloads
4. Implement SSD-specific optimizations including TRIM

**Deliverables**:
- Comprehensive performance analysis reports
- Workload-specific optimization configurations
- Before/after performance comparisons

### Lab 5: Enterprise Storage Security and Compliance
**Objective**: Implement enterprise-grade storage security and compliance

**Tasks**:
1. Configure LUKS encryption with key management
2. Implement filesystem quotas and ACLs for multi-user environments
3. Set up automated compliance monitoring and reporting
4. Create comprehensive backup and disaster recovery procedures

**Deliverables**:
- Encrypted storage with secure key management
- Multi-user access control implementation
- Automated compliance monitoring system

## Next Steps
With advanced storage and filesystem management mastered, you're ready to explore enterprise-grade filesystem features in Module 11: ZFS Fundamentals. ZFS builds upon these foundational concepts with advanced features like built-in RAID, snapshots, compression, and data integrity verification, providing the perfect progression from traditional Linux storage management to next-generation filesystem technologies.
