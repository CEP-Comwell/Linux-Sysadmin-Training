# Module 10: Storage & Filesystem Management

## Overview
This module covers advanced storage management and filesystem administration in Linux. You'll learn to manage disk partitions, filesystems, LVM, RAID, and implement comprehensive storage solutions for enterprise environments.

## Learning Objectives
By the end of this module, you will be able to:
- Manage disk partitions and filesystems
- Configure and manage LVM (Logical Volume Manager)
- Implement software RAID solutions
- Monitor and optimize filesystem performance
- Configure filesystem quotas and access controls
- Implement backup and disaster recovery strategies

## Topics

### 10.1 Storage Fundamentals
- Block devices and storage hierarchy
- Partition types: MBR vs GPT
- Filesystem types and selection criteria
- Storage device naming conventions
- Device mapping and identification

### 10.2 Partition Management
- Creating and managing partitions with fdisk
- Using parted for advanced partitioning
- GPT partitioning with gdisk
- Partition alignment and optimization
- Resizing and moving partitions

### 10.3 Filesystem Creation and Management
- Creating filesystems (ext4, xfs, btrfs)
- Mounting and unmounting filesystems
- Filesystem checking and repair
- Filesystem tuning and optimization
- UUID and label management

### 10.4 Logical Volume Manager (LVM)
- LVM concepts: PV, VG, LV
- Creating and managing physical volumes
- Volume group administration
- Logical volume operations
- LVM snapshots and backup strategies

### 10.5 Software RAID
- RAID levels and use cases
- Creating and managing mdadm RAID arrays
- RAID monitoring and maintenance
- Hot spare configuration
- RAID recovery procedures

### 10.6 Advanced Storage Topics
- Filesystem quotas
- Access control lists (ACLs)
- Encrypted filesystems (LUKS)
- Network filesystems (NFS, CIFS)
- Storage performance monitoring

## Practical Examples

### Disk and Partition Management

#### Viewing Storage Information
```bash
# List all block devices
lsblk

# Show disk information
fdisk -l
parted -l

# Display device details
blkid
lshw -class disk

# Show filesystem usage
df -h
du -sh /path/to/directory

# Check device names and sizes
cat /proc/partitions
ls -la /dev/disk/by-*
```

#### Partitioning with fdisk
```bash
# Start fdisk on a device
sudo fdisk /dev/sdb

# fdisk commands:
# p - print partition table
# n - create new partition
# d - delete partition
# t - change partition type
# w - write changes and exit
# q - quit without saving

# Example: Create a new partition
sudo fdisk /dev/sdb << EOF
n
p
1


w
EOF
```

#### Advanced Partitioning with parted
```bash
# Create GPT partition table
sudo parted /dev/sdb mklabel gpt

# Create partition
sudo parted /dev/sdb mkpart primary ext4 1MiB 100%

# Set partition flags
sudo parted /dev/sdb set 1 boot on

# Resize partition
sudo parted /dev/sdb resizepart 1 50GB

# Show partition information
sudo parted /dev/sdb print
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

### LVM Management

#### Setting up LVM
```bash
# Create physical volume
sudo pvcreate /dev/sdb /dev/sdc

# Create volume group
sudo vgcreate vg_data /dev/sdb /dev/sdc

# Create logical volume
sudo lvcreate -L 10G -n lv_web vg_data
sudo lvcreate -l 100%FREE -n lv_backup vg_data

# Display LVM information
pvdisplay
vgdisplay
lvdisplay

# Short format
pvs
vgs
lvs
```

#### LVM Operations
```bash
# Extend volume group
sudo pvcreate /dev/sdd
sudo vgextend vg_data /dev/sdd

# Extend logical volume
sudo lvextend -L +5G /dev/vg_data/lv_web
sudo resize2fs /dev/vg_data/lv_web

# Reduce logical volume (careful!)
sudo umount /dev/vg_data/lv_backup
sudo e2fsck -f /dev/vg_data/lv_backup
sudo resize2fs /dev/vg_data/lv_backup 5G
sudo lvreduce -L 5G /dev/vg_data/lv_backup

# Remove logical volume
sudo umount /dev/vg_data/lv_backup
sudo lvremove /dev/vg_data/lv_backup
```

#### LVM Snapshots
```bash
# Create snapshot
sudo lvcreate -L 1G -s -n lv_web_snap /dev/vg_data/lv_web

# Mount snapshot
sudo mkdir /mnt/snapshot
sudo mount /dev/vg_data/lv_web_snap /mnt/snapshot

# Merge snapshot back
sudo umount /mnt/snapshot
sudo lvconvert --merge /dev/vg_data/lv_web_snap

# Remove snapshot
sudo lvremove /dev/vg_data/lv_web_snap
```

### Software RAID Configuration

#### Creating RAID Arrays
```bash
# RAID 1 (mirror)
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc

# RAID 5
sudo mdadm --create /dev/md1 --level=5 --raid-devices=3 /dev/sdd /dev/sde /dev/sdf

# RAID 10
sudo mdadm --create /dev/md2 --level=10 --raid-devices=4 /dev/sdg /dev/sdh /dev/sdi /dev/sdj

# Check RAID status
cat /proc/mdstat
sudo mdadm --detail /dev/md0

# Save RAID configuration
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```

#### RAID Management
```bash
# Add hot spare
sudo mdadm --add /dev/md0 /dev/sdk

# Remove device from array
sudo mdadm --remove /dev/md0 /dev/sdb

# Stop RAID array
sudo mdadm --stop /dev/md0

# Assemble RAID array
sudo mdadm --assemble /dev/md0 /dev/sdb /dev/sdc

# Monitor RAID
sudo mdadm --monitor --daemonise --mail=admin@example.com /dev/md0
```

#### RAID Recovery
```bash
# Mark device as failed
sudo mdadm --manage /dev/md0 --fail /dev/sdb

# Replace failed device
sudo mdadm --manage /dev/md0 --remove /dev/sdb
# Replace physical device
sudo mdadm --manage /dev/md0 --add /dev/sdb

# Check rebuild progress
watch cat /proc/mdstat
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

## Storage Best Practices

| Practice | Description |
|----------|-------------|
| Regular Backups | Implement automated backup strategies |
| Monitor Health | Use SMART monitoring for disk health |
| Plan Capacity | Monitor disk usage and plan expansion |
| Use Labels/UUIDs | Avoid device name dependencies |
| Document Changes | Keep records of storage modifications |
| Test Recovery | Regularly test backup and recovery procedures |
| Performance Tuning | Optimize for workload requirements |

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
1. Set up LVM with snapshots for backup
2. Configure software RAID with monitoring
3. Implement filesystem quotas and ACLs
4. Create encrypted storage solution
5. Develop comprehensive storage monitoring

## Next Steps
With storage and filesystem management mastered, you're ready to explore advanced DevOps concepts starting with ZFS Fundamentals in Module 11, where you'll learn about enterprise-grade filesystem features.
