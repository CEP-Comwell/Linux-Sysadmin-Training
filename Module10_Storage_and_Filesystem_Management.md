# Module 10: Storage and Filesystem Management

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [10.1 Storage Fundamentals and Basic Partitioning](#101-storage-fundamentals-and-basic-partitioning)
  - [10.2 Ext4 and Xfs Filesystem Management](#102-ext4-and-xfs-filesystem-management)
  - [10.3 Lvm Fundamentals and Benefits](#103-lvm-fundamentals-and-benefits)
  - [10.4 Storage Security and Backup Basics](#104-storage-security-and-backup-basics)
  - [10.5 Looking Ahead Zfs Overview](#105-looking-ahead-zfs-overview)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Basic Partitioning](#basic-partitioning)
  - [Filesystem Creation and Management](#filesystem-creation-and-management)
  - [Lvm Basics](#lvm-basics)
  - [Storage Maintenance](#storage-maintenance)
- [Hands-on Labs](#hands-on-labs)
  - [Lab 1: Basic Partitioning and Filesystem Management](#lab-1-basic-partitioning-and-filesystem-management)
  - [Lab 2: LVM Basics](#lab-2-lvm-basics)
  - [Lab 3: Basic Storage Security](#lab-3-basic-storage-security)
  - [Lab 4: Storage Monitoring](#lab-4-storage-monitoring)
  - [Lab Solutions and Expected Outcomes](#lab-solutions-and-expected-outcomes)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)


## Overview

**[Back to Top](#module-10-storage-and-filesystem-management)** ⬆️ | **[Main Index](README.md)** 🏠

Learn essential Linux storage and filesystem management skills for system administrators. This module covers practical filesystem creation and management using EXT4 and XFS, basic partitioning, and an introduction to Logical Volume Manager (LVM). You'll gain hands-on experience with the most common storage tasks that system administrators perform daily.

This module focuses on practical skills rather than advanced performance tuning, preparing you for real-world storage administration with current best practices and safe procedures.

**Core Skills You'll Learn:**
- Create and manage EXT4 and XFS filesystems
- Understand basic partitioning with fdisk and parted
- Learn LVM fundamentals and when to use it
- Implement basic storage security and backup practices
- Troubleshoot common filesystem issues
- Prepare for advanced storage concepts in Module 11 (ZFS)


## Learning Objectives

**[Back to Top](#module-10-storage-and-filesystem-management)** ⬆️ | **[Main Index](README.md)** 🏠

By completing this module, you will be able to:

1. **Create and Manage Filesystems**
   - Create EXT4 and XFS filesystems with appropriate settings
   - Understand when to choose EXT4 vs XFS for different use cases
   - Mount filesystems with secure and efficient options
   - Perform basic filesystem maintenance and repair

2. **Handle Basic Partitioning**
   - Create and modify partitions using fdisk and parted
   - Understand MBR vs GPT partition tables
   - Use proper partition alignment for modern storage
   - Work with UUIDs and labels for persistent mounting

3. **Understand LVM Fundamentals**
   - Grasp the benefits of using LVM vs traditional partitions
   - Create basic LVM setups with physical volumes, volume groups, and logical volumes
   - Perform simple LVM operations like extending volumes
   - Understand when LVM is the right choice for your environment

4. **Implement Storage Best Practices**
   - Configure secure mount options and file permissions
   - Perform basic backup and recovery procedures
   - Monitor filesystem usage and health
   - Apply security practices for storage management


## Topics

**[Back to Top](#module-10-storage-and-filesystem-management)** ⬆️ | **[Main Index](README.md)** 🏠

### 10.1 Storage Fundamentals and Basic Partitioning
- Understanding Linux storage hierarchy and device naming
- Partition table basics: MBR vs GPT
- Using fdisk and parted for basic partitioning tasks
- Proper partition alignment for modern disks
- UUID and label usage for reliable mounting
- Safe partitioning practices

### 10.2 Ext4 and Xfs Filesystem Management
- EXT4 vs XFS: when to choose each filesystem
- Creating filesystems with appropriate settings
- Essential mount options for security and performance
- Basic filesystem maintenance and repair
- Monitoring filesystem usage and health
- Filesystem resizing basics

### 10.3 Lvm Fundamentals and Benefits
- Why use LVM vs traditional partitions
- LVM architecture: Physical Volumes, Volume Groups, Logical Volumes
- Basic LVM operations: create, extend, monitor
- Simple LVM scenarios and use cases
- When LVM is (and isn't) the right choice
- Basic troubleshooting and recovery

### 10.4 Storage Security and Backup Basics
- Secure mount options and file permissions
- Basic backup strategies and tools
- Understanding storage-related security risks
- Simple encryption concepts
- Monitoring and alerting for storage issues

### 10.5 Looking Ahead Zfs Overview
- Introduction to ZFS concepts and benefits
- How ZFS differs from traditional Linux filesystems
- When to consider ZFS (covered in detail in Module 11)
- Migration considerations and compatibility
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

**[Back to Top](#module-10-storage-and-filesystem-management)** ⬆️ | **[Main Index](README.md)** 🏠

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

## Essential Command Reference

### Storage Discovery and Information

| Command | Description | Example |
|---------|-------------|---------|
| `lsblk` | List block devices in tree format | `lsblk -f` |
| `blkid` | Display block device attributes | `blkid /dev/sda1` |
| `df -h` | Display filesystem disk space usage | `df -h` |
| `du -sh` | Show directory space usage | `du -sh /var/log` |
| `fdisk -l` | List disk partition tables | `fdisk -l /dev/sda` |
| `parted -l` | List partition information | `parted -l` |

### Basic Partitioning

| Command | Description | Example |
|---------|-------------|---------|
| `fdisk /dev/sdX` | Interactive disk partitioning (MBR) | `fdisk /dev/sda` |
| `parted /dev/sdX` | GNU parted partitioning tool | `parted /dev/sda print` |
| `partprobe` | Inform kernel of partition changes | `partprobe /dev/sda` |

### Filesystem Operations

| Command | Description | Example |
|---------|-------------|---------|
| `mkfs.ext4` | Create ext4 filesystem | `mkfs.ext4 /dev/sda1` |
| `mkfs.xfs` | Create XFS filesystem | `mkfs.xfs /dev/sda1` |
| `mount` | Mount filesystem | `mount /dev/sda1 /mnt` |
| `umount` | Unmount filesystem | `umount /mnt` |
| `fsck.ext4` | Check and repair ext4 filesystem | `fsck.ext4 /dev/sda1` |
| `xfs_repair` | Repair XFS filesystem | `xfs_repair /dev/sda1` |
| `tune2fs` | Display/modify ext4 parameters | `tune2fs -l /dev/sda1` |
| `resize2fs` | Resize ext4 filesystem | `resize2fs /dev/sda1` |
| `xfs_growfs` | Grow XFS filesystem | `xfs_growfs /mnt/data` |

### Basic LVM Commands

| Command | Description | Example |
|---------|-------------|---------|
| `pvcreate` | Create physical volume | `pvcreate /dev/sda1` |
| `vgcreate` | Create volume group | `vgcreate vg01 /dev/sda1` |
| `lvcreate` | Create logical volume | `lvcreate -L 10G -n data vg01` |
| `pvs` | Show physical volume summary | `pvs` |
| `vgs` | Show volume group summary | `vgs` |
| `lvs` | Show logical volume summary | `lvs` |
| `lvextend` | Extend logical volume | `lvextend -L +5G /dev/vg01/data` |

### Storage Monitoring

| Command | Description | Example |
|---------|-------------|---------|
| `iostat` | I/O statistics for devices | `iostat -x 1` |
| `smartctl` | Check disk health | `smartctl -a /dev/sda` |

---

## 10.1 Storage Fundamentals and Basic Partitioning

### Understanding Linux Storage Hierarchy

Linux treats all storage as files under the `/dev` directory. Here's what you need to know:

#### Device Naming Conventions
```bash
# Common device names
/dev/sda    # First SATA/SCSI disk
/dev/sdb    # Second SATA/SCSI disk
/dev/sda1   # First partition on first disk
/dev/sda2   # Second partition on first disk

# Virtual machines often use
/dev/vda    # First virtual disk
/dev/xvda   # Xen virtual disk

# NVMe SSDs use
/dev/nvme0n1    # First NVMe disk
/dev/nvme0n1p1  # First partition on first NVMe disk
```

#### Checking Available Storage
```bash
# See all block devices
lsblk

# See mounted filesystems
df -h

# Get detailed device information
lsblk -f

# Check partition table type
sudo parted /dev/sda print
```

### Partition Tables: MBR vs GPT

#### MBR (Master Boot Record)
- **Limitations**: Maximum 4 primary partitions, 2TB disk size limit
- **Use when**: Legacy systems, older BIOS, small disks
- **Tool**: `fdisk`

#### GPT (GUID Partition Table)
- **Advantages**: 128 partitions, larger than 2TB disks, more reliable
- **Use when**: Modern systems, UEFI, larger disks (recommended)
- **Tool**: `parted` or `gdisk`

### Basic Partitioning with fdisk

#### Creating Basic Partitions
```bash
# Start fdisk on a disk (WARNING: This modifies the disk!)
sudo fdisk /dev/sdb

# Basic fdisk commands:
# p - print partition table
# n - create new partition
# d - delete partition
# t - change partition type
# w - write changes and exit
# q - quit without saving

# Example session:
sudo fdisk /dev/sdb
# Press 'n' for new partition
# Press 'p' for primary
# Press '1' for partition number
# Press Enter for default start sector
# Type '+10G' for 10GB partition
# Press 'w' to write changes
```

#### Safe Partitioning Example
```bash
# 1. Always check what's on the disk first
sudo fdisk -l /dev/sdb
lsblk /dev/sdb

# 2. Create partition table if needed (destroys all data!)
sudo parted /dev/sdb mklabel gpt

# 3. Create a partition using parted (safer for beginners)
sudo parted /dev/sdb mkpart primary ext4 1MiB 10GiB

# 4. Verify the partition was created
sudo parted /dev/sdb print
lsblk /dev/sdb
```

### Working with UUIDs and Labels

#### Why Use UUIDs?
Device names like `/dev/sda1` can change between reboots. UUIDs are permanent identifiers.

```bash
# See UUIDs of all devices
blkid

# See specific device UUID
blkid /dev/sdb1

# Mount by UUID (in /etc/fstab)
UUID=12345678-1234-1234-1234-123456789abc /data ext4 defaults 0 2

# Set a filesystem label
sudo e2label /dev/sdb1 "data-disk"

# Mount by label
LABEL=data-disk /data ext4 defaults 0 2
```

### Partition Alignment Best Practices

Modern disks work best when partitions are properly aligned:

```bash
# For parted, always start at 1MiB for optimal alignment
sudo parted /dev/sdb mkpart primary ext4 1MiB 100%

# Check alignment
sudo parted /dev/sdb align-check optimal 1

# fdisk automatically aligns partitions in modern versions
```

---

## 10.2 EXT4 and XFS Filesystem Management

### Choosing Between EXT4 and XFS

Both are excellent filesystems, but they have different strengths:

#### EXT4 (Fourth Extended Filesystem)
- **Best for**: General purpose, smaller files, legacy compatibility
- **Strengths**: Very stable, well-tested, good with many small files
- **Max file size**: 16TB
- **Max filesystem size**: 1 exabyte
- **Good for**: Root partitions, home directories, general data storage

#### XFS (High-performance journaling filesystem)
- **Best for**: Large files, high-performance applications, databases
- **Strengths**: Excellent with large files, scales well, fast metadata operations
- **Max file size**: 8 exabytes
- **Max filesystem size**: 8 exabytes
- **Good for**: Video storage, databases, large file repositories

### Creating Filesystems

#### Creating EXT4 Filesystems
```bash
# Basic EXT4 creation
sudo mkfs.ext4 /dev/sdb1

# EXT4 with custom label
sudo mkfs.ext4 -L "data-drive" /dev/sdb1

# EXT4 with custom block size (usually not needed)
sudo mkfs.ext4 -b 4096 /dev/sdb1

# Check EXT4 filesystem information
sudo tune2fs -l /dev/sdb1
```

#### Creating XFS Filesystems
```bash
# Basic XFS creation
sudo mkfs.xfs /dev/sdb1

# XFS with custom label
sudo mkfs.xfs -L "data-drive" /dev/sdb1

# Force creation (overwrites existing filesystem)
sudo mkfs.xfs -f /dev/sdb1

# Check XFS filesystem information
sudo xfs_info /dev/sdb1
```

### Essential Mount Options

#### Security and Performance Mount Options
```bash
# Basic secure mounting
sudo mount -o nodev,nosuid,noexec /dev/sdb1 /mnt/data

# Performance optimization
sudo mount -o noatime,relatime /dev/sdb1 /mnt/data

# Combining options
sudo mount -o defaults,noatime,nodev /dev/sdb1 /mnt/data
```

#### Important Mount Options Explained
- **noatime**: Don't update access times (improves performance)
- **relatime**: Update access times only when necessary (good compromise)
- **nodev**: Don't allow device files on this filesystem
- **nosuid**: Don't allow SUID programs
- **noexec**: Don't allow execution of programs

### Configuring /etc/fstab

#### Basic fstab Entry
```bash
# Edit fstab
sudo nano /etc/fstab

# Add entry using UUID (recommended)
UUID=12345678-1234-1234-1234-123456789abc /data ext4 defaults,noatime 0 2

# Add entry using label
LABEL=data-drive /data ext4 defaults,noatime 0 2

# Test fstab entries without rebooting
sudo mount -a
```

#### fstab Field Explanation
```bash
# Device        Mount Point    FS Type    Options         Dump    Pass
UUID=...       /data          ext4       defaults,noatime 0       2

# Dump: 0=no backup, 1=backup
# Pass: 0=no check, 1=check first (root), 2=check after root
```

### Filesystem Maintenance

#### Checking and Repairing EXT4
```bash
# Check filesystem (unmount first!)
sudo umount /dev/sdb1
sudo fsck.ext4 /dev/sdb1

# Force check even if filesystem seems clean
sudo fsck.ext4 -f /dev/sdb1

# Auto-repair minor issues
sudo fsck.ext4 -p /dev/sdb1

# Check filesystem that's currently mounted (read-only check)
sudo fsck.ext4 -n /dev/sdb1
```

#### Checking and Repairing XFS
```bash
# Check XFS filesystem (unmount first!)
sudo umount /dev/sdb1
sudo xfs_repair /dev/sdb1

# Check without making changes
sudo xfs_repair -n /dev/sdb1

# Note: XFS has very robust journaling, rarely needs repair
```

### Resizing Filesystems

#### Extending EXT4 Filesystems
```bash
# First, extend the partition (if needed)
sudo parted /dev/sdb resizepart 1 100%

# Then extend the filesystem
sudo resize2fs /dev/sdb1

# Can be done while mounted!
```

#### Growing XFS Filesystems
```bash
# First, extend the partition (if needed)
sudo parted /dev/sdb resizepart 1 100%

# Grow XFS filesystem (must be mounted)
sudo xfs_growfs /mnt/data

# Note: XFS cannot be shrunk, only grown
```

### Monitoring Filesystem Usage

#### Basic Usage Commands
```bash
# Check disk usage by filesystem
df -h

# Check specific filesystem
df -h /data

# Check inode usage
df -i

# Check directory sizes
du -sh /data/*

# Find large files
find /data -type f -size +100M -exec ls -lh {} \;
```

#### Setting Up Basic Monitoring
```bash
# Check filesystem usage in a script
#!/bin/bash
USAGE=$(df /data | tail -1 | awk '{print $5}' | sed 's/%//')
if [ $USAGE -gt 80 ]; then
    echo "Warning: /data is ${USAGE}% full"
fi

# Add to crontab for regular monitoring
# 0 */6 * * * /path/to/disk-check.sh
```

---

## 10.3 LVM Fundamentals and Benefits

### What is LVM?

LVM (Logical Volume Manager) is a powerful storage abstraction layer that sits between your physical storage devices and your filesystems. Think of it as a flexible way to manage storage that gives you more options than traditional partitioning.

#### Traditional Partitioning vs LVM

**Traditional Partitioning:**
- Fixed partition sizes
- Difficult to resize
- Limited flexibility
- Direct partition → filesystem relationship

**LVM Benefits:**
- Dynamic volume resizing
- Easy to add more storage
- Snapshot capabilities
- Better storage utilization
- Separation of physical and logical storage

### LVM Architecture

LVM has three main components:

#### Physical Volumes (PV)
- Your actual storage devices (disks, partitions)
- The foundation of your LVM setup

#### Volume Groups (VG)  
- Collection of physical volumes
- Think of it as a "storage pool"

#### Logical Volumes (LV)
- Virtual partitions created from volume groups
- Where you create your filesystems

```
[Physical Disk] → [Physical Volume] → [Volume Group] → [Logical Volume] → [Filesystem]
```

### Basic LVM Setup

#### Step 1: Create Physical Volumes
```bash
# Check available disks
lsblk

# Create physical volumes (initialize disks for LVM)
sudo pvcreate /dev/sdb
sudo pvcreate /dev/sdc

# View physical volumes
sudo pvdisplay
sudo pvs
```

#### Step 2: Create Volume Group
```bash
# Create volume group named "data-vg" from both disks
sudo vgcreate data-vg /dev/sdb /dev/sdc

# View volume group information
sudo vgdisplay data-vg
sudo vgs
```

#### Step 3: Create Logical Volumes
```bash
# Create a logical volume for web data (50GB)
sudo lvcreate -L 50G -n web-data data-vg

# Create a logical volume for backups (100GB)
sudo lvcreate -L 100G -n backups data-vg

# Create a logical volume using remaining space
sudo lvcreate -l 100%FREE -n storage data-vg

# View logical volumes
sudo lvdisplay
sudo lvs
```

#### Step 4: Create Filesystems and Mount
```bash
# Create filesystems on logical volumes
sudo mkfs.ext4 /dev/data-vg/web-data
sudo mkfs.ext4 /dev/data-vg/backups
sudo mkfs.xfs /dev/data-vg/storage

# Create mount points
sudo mkdir -p /data/web /data/backups /data/storage

# Mount the volumes
sudo mount /dev/data-vg/web-data /data/web
sudo mount /dev/data-vg/backups /data/backups
sudo mount /dev/data-vg/storage /data/storage

# Add to /etc/fstab for permanent mounting
echo "/dev/data-vg/web-data /data/web ext4 defaults 0 2" | sudo tee -a /etc/fstab
echo "/dev/data-vg/backups /data/backups ext4 defaults 0 2" | sudo tee -a /etc/fstab
echo "/dev/data-vg/storage /data/storage xfs defaults 0 2" | sudo tee -a /etc/fstab
```

### Common LVM Operations

#### Extending Logical Volumes
```bash
# Add more space to an existing logical volume
sudo lvextend -L +20G /dev/data-vg/web-data

# Extend the filesystem (EXT4 - can be done while mounted)
sudo resize2fs /dev/data-vg/web-data

# For XFS (must be mounted)
sudo xfs_growfs /data/storage
```

#### Adding More Storage
```bash
# When you add a new disk, create PV and add to VG
sudo pvcreate /dev/sdd
sudo vgextend data-vg /dev/sdd

# Now you have more space available for logical volumes
sudo vgs  # Check available space
```

#### Basic Snapshots
```bash
# Create a snapshot for backup purposes (10GB snapshot space)
sudo lvcreate -L 10G -s -n web-data-backup /dev/data-vg/web-data

# Mount the snapshot to access point-in-time data
sudo mkdir /mnt/snapshot
sudo mount /dev/data-vg/web-data-backup /mnt/snapshot

# Remove snapshot when done
sudo umount /mnt/snapshot
sudo lvremove /dev/data-vg/web-data-backup
```

### When to Use LVM

#### Good Use Cases:
- **Server environments** where you need flexibility
- **Growing storage needs** that may change over time
- **Multiple disk setups** where you want to combine space
- **Backup scenarios** where snapshots are useful
- **Development systems** where you need to test different setups

#### When Traditional Partitioning Might Be Better:
- **Simple single-disk setups** with fixed requirements
- **Boot partitions** (though LVM can work, traditional is simpler)
- **Embedded systems** with minimal storage needs
- **High-performance scenarios** where simplicity is preferred

### LVM Best Practices

#### Naming Conventions
```bash
# Use descriptive names for volume groups and logical volumes
sudo vgcreate web-servers-vg /dev/sdb
sudo lvcreate -L 50G -n apache-logs web-servers-vg
sudo lvcreate -L 100G -n database web-servers-vg
```

#### Leave Some Free Space
```bash
# Don't allocate 100% immediately - keep some space for growth
# Instead of using all space:
sudo lvcreate -l 100%FREE -n data data-vg

# Better to leave some space:
sudo lvcreate -L 80G -n data data-vg  # if VG has 100G total
```

#### Monitor Usage
```bash
# Check volume group space
sudo vgs

# Check logical volume usage
sudo lvs

# Check filesystem usage
df -h
```

### Simple LVM Monitoring Script
```bash
#!/bin/bash
# lvm-check.sh - Basic LVM space monitoring

echo "=== LVM Space Report ==="
echo ""

echo "Volume Groups:"
sudo vgs

echo ""
echo "Logical Volumes:"
sudo lvs

echo ""
echo "Filesystem Usage:"
df -h | grep "/dev/mapper"

# Alert if any filesystem > 80% full
echo ""
echo "Storage Alerts:"
df -h | grep "/dev/mapper" | awk '{
    usage = int($5)
    if (usage > 80) {
        print "WARNING: " $6 " is " $5 " full"
    }
}'
```

---

## 10.4 Storage Security and Backup Basics

### Essential Storage Security

#### File Permissions and Ownership
```bash
# Set secure permissions for sensitive data
sudo chmod 700 /data/private     # Owner only
sudo chmod 750 /data/shared      # Owner + group
sudo chmod 755 /data/public      # Everyone can read

# Set proper ownership
sudo chown alice:developers /data/shared
sudo chown -R www-data:www-data /var/www

# Find and fix problematic permissions
find /data -type f -perm 777 -exec chmod 644 {} \;
find /data -type d -perm 777 -exec chmod 755 {} \;
```

#### Basic Access Control Lists (ACLs)
```bash
# Install ACL support
sudo apt update && sudo apt install acl

# Enable ACL on filesystem (if not already enabled)
sudo mount -o remount,acl /data

# Set specific user permissions
sudo setfacl -m u:alice:rw /data/project-files
sudo setfacl -m g:developers:rx /data/source-code

# View ACL permissions
getfacl /data/project-files

# Remove ACL entry
sudo setfacl -x u:alice /data/project-files
```

#### Basic Filesystem Quotas
```bash
# Enable quotas in /etc/fstab (add usrquota,grpquota)
UUID=... /data ext4 defaults,usrquota,grpquota 0 2

# Remount filesystem
sudo mount -o remount /data

# Initialize quota database
sudo quotacheck -cum /data
sudo quotaon /data

# Set user quotas (soft limit: 1GB, hard limit: 1.2GB)
sudo setquota -u alice 1000000 1200000 0 0 /data

# Check quota usage
quota -u alice
sudo repquota /data
```

### Simple Backup Strategies

#### Basic File-Level Backups
```bash
# Simple tar backup
sudo tar -czf /backup/data-$(date +%Y%m%d).tar.gz /data

# Incremental backup using rsync
sudo rsync -av --delete /data/ /backup/data/

# Backup with exclusions
sudo rsync -av --delete --exclude='*.tmp' --exclude='*.log' /data/ /backup/data/
```

#### LVM Snapshots for Backups
```bash
# Create snapshot before backup
sudo lvcreate -L 10G -s -n data-backup /dev/data-vg/data

# Mount snapshot
sudo mkdir /mnt/backup
sudo mount /dev/data-vg/data-backup /mnt/backup

# Backup from snapshot (consistent point-in-time)
sudo tar -czf /backup/data-snapshot-$(date +%Y%m%d).tar.gz -C /mnt/backup .

# Cleanup
sudo umount /mnt/backup
sudo lvremove /dev/data-vg/data-backup
```

#### Simple Backup Script
```bash
#!/bin/bash
# simple-backup.sh - Basic backup script

BACKUP_SOURCE="/data"
BACKUP_DEST="/backup"
DATE=$(date +%Y%m%d_%H%M%S)

# Create backup directory
mkdir -p "$BACKUP_DEST"

# Perform backup
echo "Starting backup at $(date)"
tar -czf "$BACKUP_DEST/backup_$DATE.tar.gz" "$BACKUP_SOURCE"

if [ $? -eq 0 ]; then
    echo "Backup completed successfully: backup_$DATE.tar.gz"
    
    # Keep only last 7 backups
    cd "$BACKUP_DEST"
    ls -t backup_*.tar.gz | tail -n +8 | xargs rm -f
    echo "Old backups cleaned up"
else
    echo "Backup failed!"
    exit 1
fi
```

### Storage Monitoring

#### Basic Disk Space Monitoring
```bash
# Check disk usage
df -h

# Check for large files
find /data -type f -size +100M -exec ls -lh {} \;

# Monitor disk usage script
#!/bin/bash
# disk-monitor.sh
THRESHOLD=80

df -h | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{ print $5 " " $1 }' | while read output;
do
    usage=$(echo $output | awk '{ print $1}' | cut -d'%' -f1)
    partition=$(echo $output | awk '{ print $2 }')
    
    if [ $usage -ge $THRESHOLD ]; then
        echo "WARNING: $partition is ${usage}% full"
    fi
done
```

#### Simple SMART Monitoring
```bash
# Install smartmontools
sudo apt install smartmontools

# Check disk health
sudo smartctl -H /dev/sda

# View SMART attributes
sudo smartctl -A /dev/sda

# Run short self-test
sudo smartctl -t short /dev/sda

# Check test results
sudo smartctl -l selftest /dev/sda
```

---

## 10.5 Looking Ahead: ZFS Overview

### What is ZFS?

ZFS (Zettabyte File System) is an advanced filesystem that will be covered in detail in Module 11. Here's a brief overview of why it's worth learning:

#### ZFS Key Features
- **Snapshots and Clones**: Instant, space-efficient snapshots
- **Data Integrity**: Checksums and self-healing
- **Compression**: Transparent data compression
- **Deduplication**: Eliminates duplicate data blocks

#### How ZFS Differs from Traditional Storage
```
Traditional Approach:

ZFS Approach:
[Disk] → [ZFS Pool] → [ZFS Dataset] → [Application]
```

### ZFS Use Cases

#### When ZFS Excels:
- **Data integrity is critical** (databases, file servers)
- **Need frequent snapshots** (development, testing)
- **Large storage pools** (multiple TB/PB of data)
- **Virtual machine storage** (Proxmox, VMware)
- **NAS and file sharing** environments

#### Simple ZFS Example (Preview)
```bash
# Create ZFS pool (covered in Module 11)
sudo zpool create datapool /dev/sdb /dev/sdc

# Create dataset
sudo zfs create datapool/documents

# Take snapshot
sudo zfs snapshot datapool/documents@backup-2024-01-15

# List snapshots
sudo zfs list -t snapshot
```

### Preparing for Module 11

To get ready for ZFS training:

2. **Practice with LVM** to understand storage abstraction
3. **Learn basic pool and volume concepts**
4. **Familiarize yourself with snapshot concepts**

### EXT4/XFS vs ZFS Comparison

| Feature | EXT4 | XFS | ZFS |
|---------|------|-----|-----|
| Maturity | Very High | High | High |
| Max File Size | 16TB | 8EB | 16EB |
| Snapshots | No | No | Yes |
| Compression | No | No | Yes |
| Checksums | No | No | Yes |
| Complexity | Low | Low | Medium |

### When to Use Each Filesystem

#### Choose EXT4 when:
- Simple, single-disk setups
- Maximum compatibility needed
- Learning Linux fundamentals
- Limited system resources

#### Choose XFS when:
- Large files (video, databases)
- High-performance requirements
- Growing filesystems
- Enterprise environments

#### Choose ZFS when:
- Data integrity is paramount
- Need snapshots and clones
- Managing large storage pools
- Advanced features required

---

## Simple Practical Labs

### Lab 1: Basic Partitioning and Filesystem Management

**Objective**: Practice fundamental storage operations with EXT4 and XFS

**Prerequisites**: Virtual machine with at least one additional virtual disk

#### Exercise 1: Create and Use EXT4 Filesystem
```bash
# 1. Check available disks
lsblk

# 2. Create partition on second disk
sudo fdisk /dev/sdb
# - Press 'n' for new partition
# - Accept defaults for primary partition
# - Press 'w' to write changes

# 3. Create EXT4 filesystem
sudo mkfs.ext4 -L "lab-data" /dev/sdb1

# 4. Create mount point and mount
sudo mkdir /mnt/lab-data
sudo mount /dev/sdb1 /mnt/lab-data

# 5. Test filesystem
echo "Hello from EXT4!" | sudo tee /mnt/lab-data/test.txt
cat /mnt/lab-data/test.txt

# 6. Check filesystem information
sudo tune2fs -l /dev/sdb1 | head -20
```

**Related Commands/Topics:** [Partitioning Operations](#partitioning-operations), [Filesystem Operations](#filesystem-operations) 📑

#### Exercise 2: Add to fstab and Test
```bash
# 1. Get UUID of the filesystem
sudo blkid /dev/sdb1

# 2. Add to fstab (replace UUID with actual value)
echo "UUID=your-uuid-here /mnt/lab-data ext4 defaults,noatime 0 2" | sudo tee -a /etc/fstab

# 3. Test fstab entry
sudo umount /mnt/lab-data
sudo mount -a
df -h | grep lab-data
```

**Related Commands/Topics:** [Working with UUIDs and Labels](#working-with-uuids-and-labels), [Configuring etc-fstab](#configuring-etc-fstab) 📑

#### Exercise 3: Compare with XFS
```bash
# 1. Create another partition for XFS
sudo fdisk /dev/sdb
# - Create second partition

# 2. Create XFS filesystem
sudo mkfs.xfs -L "lab-xfs" /dev/sdb2

# 3. Mount and test
sudo mkdir /mnt/lab-xfs
sudo mount /dev/sdb2 /mnt/lab-xfs
echo "Hello from XFS!" | sudo tee /mnt/lab-xfs/test.txt

# 4. Compare filesystem info
sudo xfs_info /mnt/lab-xfs
```

**Related Commands/Topics:** [Filesystem Operations](#filesystem-operations) 📑

### Lab 2: LVM Basics

**Objective**: Create and manage LVM logical volumes

#### Exercise 1: Create LVM Setup
```bash
# 1. Create physical volume
sudo pvcreate /dev/sdb3

# 2. Create volume group
sudo vgcreate lab-vg /dev/sdb3

# 3. Create logical volumes
sudo lvcreate -L 1G -n web-data lab-vg
sudo lvcreate -L 500M -n logs lab-vg

# 4. Check what we created
sudo pvs
sudo vgs
sudo lvs
```

**Related Commands/Topics:** [Basic LVM Commands](#basic-lvm-commands) 📑

#### Exercise 2: Create Filesystems and Mount
```bash
# 1. Create filesystems
sudo mkfs.ext4 /dev/lab-vg/web-data
sudo mkfs.ext4 /dev/lab-vg/logs

# 2. Create mount points
sudo mkdir -p /srv/web /var/log/app

# 3. Mount logical volumes
sudo mount /dev/lab-vg/web-data /srv/web
sudo mount /dev/lab-vg/logs /var/log/app

# 4. Test
echo "Web content" | sudo tee /srv/web/index.html
echo "Application logs" | sudo tee /var/log/app/app.log
```

**Related Commands/Topics:** [Filesystem Operations](#filesystem-operations), [Basic LVM Commands](#basic-lvm-commands) 📑

#### Exercise 3: Extend Logical Volume
```bash
# 1. Add more space to web-data
sudo lvextend -L +500M /dev/lab-vg/web-data

# 2. Extend the filesystem
sudo resize2fs /dev/lab-vg/web-data

# 3. Verify the change
df -h | grep web-data
```

**Related Commands/Topics:** [Basic LVM Commands](#basic-lvm-commands), [Resizing Filesystems](#resizing-filesystems) 📑

### Lab 3: Basic Storage Security

**Objective**: Practice file permissions, ACLs, and basic quotas

#### Exercise 1: File Permissions
```bash
# 1. Create test directories
sudo mkdir -p /data/{public,private,shared}

# 2. Set different permission levels
sudo chmod 755 /data/public    # Everyone can read
sudo chmod 700 /data/private   # Owner only
sudo chmod 750 /data/shared    # Owner and group

# 3. Test permissions
ls -la /data/
```

**Related Commands/Topics:** [Essential Storage Security](#essential-storage-security) 📑

#### Exercise 2: Basic ACLs
```bash
# 1. Install ACL tools
sudo apt update && sudo apt install acl

# 2. Enable ACLs on filesystem
sudo mount -o remount,acl /data

# 3. Set specific user permissions
sudo setfacl -m u:$(whoami):rw /data/shared/
sudo setfacl -m g:users:r /data/shared/

# 4. View ACL settings
getfacl /data/shared/
```

**Related Commands/Topics:** [Basic Access Control Lists (ACLs)](#basic-access-control-lists-acls) 📑

#### Exercise 3: Simple Backup
```bash
# 1. Create backup script
cat > ~/simple-backup.sh << 'EOF'
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
sudo tar -czf /tmp/data-backup-$DATE.tar.gz /data
echo "Backup created: /tmp/data-backup-$DATE.tar.gz"
EOF

# 2. Make it executable and run
chmod +x ~/simple-backup.sh
~/simple-backup.sh

# 3. Verify backup
ls -la /tmp/data-backup-*
```

**Related Commands/Topics:** [Simple Backup Strategies](#simple-backup-strategies) 📑

### Lab 4: Storage Monitoring

**Objective**: Monitor storage usage and health

#### Exercise 1: Disk Usage Monitoring
```bash
# 1. Check current disk usage
df -h

# 2. Find large files
find /data -type f -size +1M -exec ls -lh {} \; 2>/dev/null

# 3. Create usage monitoring script
cat > ~/disk-check.sh << 'EOF'
#!/bin/bash
THRESHOLD=80

echo "=== Disk Usage Report ==="
date
echo ""

df -h | grep -vE '^Filesystem|tmpfs|cdrom' | while read output; do
    usage=$(echo $output | awk '{ print $5}' | cut -d'%' -f1)
    partition=$(echo $output | awk '{ print $6 }')
    
    if [ $usage -ge $THRESHOLD ]; then
        echo "WARNING: $partition is ${usage}% full"
    else
        echo "OK: $partition is ${usage}% full"
    fi
done
EOF

chmod +x ~/disk-check.sh
~/disk-check.sh
```

**Related Commands/Topics:** [Monitoring Filesystem Usage](#monitoring-filesystem-usage), [Setting Up Basic Monitoring](#setting-up-basic-monitoring) 📑

#### Exercise 2: SMART Monitoring
```bash
# 1. Install SMART tools
sudo apt install smartmontools

# 2. Check disk health
sudo smartctl -H /dev/sda

# 3. View SMART attributes
sudo smartctl -A /dev/sda | grep -E "(Raw_Read_Error_Rate|Reallocated_Sector|Power_On_Hours)"
```

**Related Commands/Topics:** [Simple SMART Monitoring](#simple-smart-monitoring) 📑

### Lab Solutions and Expected Outcomes

After completing these labs, you should have:

1. **Partitioned disks** and created both EXT4 and XFS filesystems
2. **Working LVM setup** with logical volumes and filesystems
3. **Basic security** with permissions and ACLs configured
4. **Monitoring scripts** for disk usage and health checks
5. **Simple backup** procedures in place

**Related Commands/Topics:** [Essential Command Reference](#essential-command-reference) 📑

These hands-on exercises provide practical experience with the storage management concepts covered in this module and prepare you for the advanced ZFS topics in Module 11.

---

*This concludes Module 10: Storage and Filesystem Management. You now have the foundational knowledge needed to manage Linux storage systems effectively, from basic partitioning through LVM and security considerations. In Module 11, we'll explore ZFS as an advanced storage solution with built-in features that simplify many of the tasks covered here.*
```bash
#!/bin/bash

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
