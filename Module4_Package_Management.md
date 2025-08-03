# Module 4: Package Management

## Overview
This module covers package management across different Linux distributions. You'll learn how to install, update, remove, and manage software packages using various package managers including apt, yum/dnf, pacman, and snap.

## Learning Objectives
By the end of this module, you will be able to:
- Understand different package management systems
- Install and remove software packages
- Update system packages and handle dependencies
- Manage package repositories
- Compile software from source when needed
- Use containerized package solutions

## Topics

### 4.1 Package Management Fundamentals
- What are packages and package managers?
- Package dependencies and conflicts
- Repository concepts
- Package formats: .deb, .rpm, .pkg.tar.xz
- Digital signatures and package verification

### 4.2 Debian/Ubuntu Package Management (APT)
- `apt` vs `apt-get` vs `aptitude`
- Installing packages: `apt install`
- Removing packages: `apt remove`, `apt purge`
- Updating package lists: `apt update`
- Upgrading packages: `apt upgrade`, `apt full-upgrade`
- Searching packages: `apt search`, `apt show`
- Managing repositories: `/etc/apt/sources.list`

### 4.3 Red Hat/CentOS Package Management
- YUM (Yellow Dog Updater Modified)
- DNF (Dandified YUM) - modern replacement
- Installing packages: `yum install`, `dnf install`
- Removing packages: `yum remove`, `dnf remove`
- Updating: `yum update`, `dnf update`
- Searching: `yum search`, `dnf search`
- Repository management: `/etc/yum.repos.d/`

### 4.4 Arch Linux Package Management (Pacman)
- Pacman basics
- Installing packages: `pacman -S`
- Removing packages: `pacman -R`, `pacman -Rns`
- Updating system: `pacman -Syu`
- Searching: `pacman -Ss`, `pacman -Qs`
- AUR (Arch User Repository) and helpers

### 4.5 Universal Package Managers
- Snap packages
- Flatpak
- AppImage
- Advantages and disadvantages

### 4.6 Compiling from Source
- When and why to compile from source
- Build dependencies
- Configure, make, make install process
- Using checkinstall for package creation

## Practical Examples

### APT (Debian/Ubuntu)
```bash
# Update package list
sudo apt update

# Install a package
sudo apt install nginx

# Install multiple packages
sudo apt install vim git curl

# Remove package but keep config files
sudo apt remove nginx

# Remove package and config files
sudo apt purge nginx

# Search for packages
apt search "web server"

# Show package information
apt show nginx

# List installed packages
apt list --installed

# Upgrade all packages
sudo apt upgrade

# Clean package cache
sudo apt autoremove && sudo apt autoclean
```

### YUM/DNF (Red Hat/CentOS)
```bash
# Install package
sudo yum install httpd
# or
sudo dnf install httpd

# Remove package
sudo yum remove httpd

# Update all packages
sudo yum update

# Search for packages
yum search nginx

# List installed packages
yum list installed

# Show package info
yum info nginx

# List available updates
yum check-update

# Clean cache
yum clean all
```

### Pacman (Arch Linux)
```bash
# Update package database and upgrade system
sudo pacman -Syu

# Install package
sudo pacman -S nginx

# Remove package
sudo pacman -R nginx

# Remove package with dependencies
sudo pacman -Rns nginx

# Search packages
pacman -Ss nginx

# List installed packages
pacman -Q

# Show package info
pacman -Si nginx
```

### Snap Packages
```bash
# Install snap package
sudo snap install code --classic

# List installed snaps
snap list

# Update all snaps
sudo snap refresh

# Remove snap
sudo snap remove code

# Find snaps
snap find "text editor"
```

## Repository Management

### Adding PPAs (Ubuntu)
```bash
# Add PPA
sudo add-apt-repository ppa:ondrej/php

# Remove PPA
sudo add-apt-repository --remove ppa:ondrej/php

# Update after adding repository
sudo apt update
```

### Adding RPM Repositories
```bash
# Add EPEL repository (CentOS/RHEL)
sudo yum install epel-release

# Add custom repository
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

## Source Compilation Example
```bash
# Download source
wget https://example.com/software-1.0.tar.gz

# Extract
tar -xzf software-1.0.tar.gz
cd software-1.0

# Install build dependencies (Ubuntu example)
sudo apt install build-essential

# Configure build
./configure --prefix=/usr/local

# Compile
make

# Install
sudo make install

# Or use checkinstall to create package
sudo checkinstall
```

## Package Management Best Practices

| Practice | Description |
|----------|-------------|
| Regular Updates | Keep system updated with security patches |
| Backup Before Major Updates | Create system snapshots before major upgrades |
| Use Official Repositories | Avoid untrusted third-party repositories |
| Clean Package Cache | Regularly clean downloaded package files |
| Document Custom Software | Keep track of manually compiled software |
| Test Updates | Test updates in non-production environments first |

## Troubleshooting Common Issues

### Broken Dependencies
```bash
# Fix broken packages (Ubuntu/Debian)
sudo apt --fix-broken install

# Force package configuration
sudo dpkg --configure -a

# Clean and rebuild package cache
sudo apt clean && sudo apt update
```

### Repository Issues
```bash
# Fix repository key issues
sudo apt-key update

# Reset repository cache
sudo rm -rf /var/lib/apt/lists/*
sudo apt update
```

## Security Considerations
- Always verify package signatures
- Use HTTPS repositories when possible
- Regularly update security patches
- Be cautious with third-party repositories
- Monitor installed packages for vulnerabilities

## Lab Exercises
1. Set up package repositories for your distribution
2. Install a web server and required dependencies
3. Practice compiling software from source
4. Create a script to automate system updates
5. Troubleshoot package dependency conflicts

## Next Steps
With package management skills mastered, you're ready to learn about Processes & Services in Module 5, where you'll manage running services and system processes.
