# Module 10: Storage & Filesystem Management

## Overview
Focuses on disk partitioning, LVM, RAID, and advanced filesystem tuning to optimize performance and resilience. This module covers advanced storage management and filesystem administration in Linux, providing hands-on experience with enterprise-grade storage solutions that balance performance and data integrity.

## Learning Objectives
By the end of this module, you will be able to:
1. **Design and implement RAID configurations, and recover from disk failures** - Master software and hardware RAID concepts, implement various RAID levels, and perform complete disaster recovery procedures
2. **Create, extend, and shrink LVM volumes and snapshots on a live system** - Manage Logical Volume Manager operations including dynamic resizing, snapshot management, and live system modifications without downtime
3. **Partition disks, format filesystems, and manage partition tables (GPT/MBR)** - Utilize fdisk/gdisk for partitioning, understand partition types, and make informed decisions between GPT and MBR partition schemes
4. **Tune filesystem and mount options to strike the right balance between performance and data integrity** - Optimize ext4/XFS parameters and mount options (noatime, barriers, etc.) for specific workloads and performance requirements

## Topics

### 10.1 Storage Fundamentals and Partition Management
- **Block devices and storage hierarchy**: Understanding device mapping, identification, and naming conventions
- **Partition types and schemes**: MBR vs GPT comparison, partition alignment, and optimization strategies
- **fdisk vs gdisk**: Command-line partitioning tools for MBR and GPT partition tables
- **Advanced partitioning with parted**: Cross-platform partitioning for complex layouts
- **Partition table recovery**: Disaster recovery techniques for corrupted partition tables

**🔗 Practical Examples**: [Partitioning with fdisk/gdisk](#partitioning-with-fdisk-and-gdisk) | [Advanced Partitioning Scenarios](#advanced-partitioning-scenarios)

### 10.2 Filesystem Creation and Advanced Tuning
- **Filesystem selection criteria**: ext4, XFS, Btrfs comparison and use case analysis
- **Filesystem parameters**: Block sizes, inode ratios, journal configurations
- **Performance tuning**: Mount options (noatime, barriers, data modes) for optimization
- **UUID and label management**: Persistent device identification and naming
- **Filesystem maintenance**: Checking, repair, and optimization procedures

**🔗 Practical Examples**: [Filesystem Performance Tuning](#filesystem-performance-tuning) | [Mount Options Optimization](#mount-options-optimization)

### 10.3 Logical Volume Manager (LVM) Deep Dive
- **LVM architecture**: Physical Volumes (PV), Volume Groups (VG), and Logical Volumes (LV)
- **Live system operations**: Creating, extending, and shrinking volumes without downtime
- **LVM snapshots**: Backup strategies, snapshot management, and live system backups
- **Advanced LVM features**: Thin provisioning, RAID LVs, and cache volumes
- **LVM troubleshooting**: Recovery procedures and common issue resolution

**🔗 Practical Examples**: [Live LVM Operations](#live-lvm-operations) | [LVM Snapshot Management](#lvm-snapshot-management)

### 10.4 Software and Hardware RAID Implementation
- **RAID levels comparison**: RAID 0, 1, 5, 6, 10 - performance vs resilience trade-offs
- **Software vs Hardware RAID**: Implementation differences and use case analysis
- **mdadm RAID management**: Creating, monitoring, and maintaining arrays
- **RAID failure recovery**: Hot spare configuration and disk replacement procedures
- **RAID performance optimization**: Chunk sizes, read-ahead, and stripe optimization

**🔗 Practical Examples**: [RAID Implementation](#raid-implementation-and-management) | [RAID Disaster Recovery](#raid-disaster-recovery)

### 10.5 Advanced Storage Performance and Monitoring
- **I/O performance analysis**: iostat, iotop, and sar for storage monitoring
- **Filesystem benchmarking**: Performance testing and bottleneck identification
- **SSD optimization**: TRIM, over-provisioning, and wear leveling
- **Storage capacity planning**: Trend analysis and growth prediction
- **Performance troubleshooting**: Identifying and resolving storage bottlenecks

**🔗 Practical Examples**: [Storage Performance Monitoring](#storage-performance-monitoring) | [SSD Optimization](#ssd-optimization-techniques)

### 10.6 Security and Access Control
- **Filesystem quotas**: User and group quota implementation and management
- **Access Control Lists (ACLs)**: Extended permissions and inheritance
- **Encrypted filesystems (LUKS)**: Full disk encryption and key management
- **Network filesystems**: NFS, CIFS configuration and security
- **Storage security best practices**: Data protection and compliance

**🔗 Practical Examples**: [Filesystem Quotas](#filesystem-quotas-implementation) | [LUKS Encryption](#luks-encryption-setup)

## Practical Examples

### Disk Information and Analysis

#### Comprehensive Storage Discovery
```bash
# Complete storage overview
lsblk -f -o NAME,SIZE,FSTYPE,MOUNTPOINT,UUID,LABEL
tree /dev/disk/

# Detailed block device information
sudo blkid -o list
sudo lshw -class disk -short
sudo hwinfo --disk --short

# Show all storage devices with detailed info
sudo fdisk -l
sudo parted -l
cat /proc/partitions

# Display filesystem usage and performance
df -h -T
sudo dumpe2fs /dev/sda1 | grep -E "(Block count|Block size|Free blocks)"
findmnt -D  # Show mount propagation

# Check device health and performance
sudo smartctl -a /dev/sda
sudo hdparm -I /dev/sda
sudo hdparm -tT /dev/sda  # Performance test
```

### Partitioning with fdisk and gdisk

#### MBR Partitioning with fdisk
```bash
# Interactive fdisk session for MBR
sudo fdisk /dev/sdb

# Automated fdisk partitioning
sudo fdisk /dev/sdb << EOF
o      # Create new DOS partition table
n      # New partition
p      # Primary partition
1      # Partition number
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
