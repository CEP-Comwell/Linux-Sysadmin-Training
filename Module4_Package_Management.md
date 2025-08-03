# Module 4: Package Management

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [4.1 Package Management Fundamentals](#41-package-management-fundamentals)
  - [4.2 Debian/Ubuntu Package Management (APT)](#42-debianubuntu-package-management-apt)
  - [4.3 Red Hat/CentOS Package Management (YUM/DNF)](#43-red-hatcentos-package-management-yumdnf)
  - [4.4 SUSE Package Management (Zypper)](#44-suse-package-management-zypper)
  - [4.5 Arch Linux Package Management (Pacman)](#45-arch-linux-package-management-pacman)
  - [4.6 Universal Package Managers](#46-universal-package-managers)
  - [4.7 Repository Management and Security](#47-repository-management-and-security)
  - [4.8 Source Compilation and Custom Packages](#48-source-compilation-and-custom-packages)
  - [4.9 Package Automation and Scripting](#49-package-automation-and-scripting)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Distribution-Specific Package Management](#distribution-specific-package-management)
  - [Repository Configuration and Management](#repository-configuration-and-management)
  - [Advanced Package Operations](#advanced-package-operations)
  - [Automation and Maintenance Scripts](#automation-and-maintenance-scripts)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Multi-Distribution Package Management](#lab-1-multi-distribution-package-management)
  - [Lab 2: Repository Management and Security](#lab-2-repository-management-and-security)
  - [Lab 3: Source Compilation and Custom Packages](#lab-3-source-compilation-and-custom-packages)
  - [Lab 4: Package Automation and Maintenance](#lab-4-package-automation-and-maintenance)
- [Best Practices Summary](#best-practices-summary)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
This module provides comprehensive coverage of package management across different Linux distributions. Students will master the installation, updating, removal, and management of software packages using various package managers including APT, YUM/DNF, Zypper, Pacman, and modern universal package systems. The focus is on practical, enterprise-ready package management strategies that ensure system security, stability, and maintainability.

**Key Learning Outcomes:**
- Master package management across major Linux distribution families
- Implement secure repository management and package verification
- Automate package operations for system maintenance and deployment
- Handle complex dependency scenarios and package conflicts
- Compile and package software from source when necessary
- Integrate modern containerized package solutions into existing workflows

## Learning Objectives
By the end of this module, you will be able to:

1. **Understand Package Ecosystems**: Navigate different package management systems and their philosophies
2. **Master Package Operations**: Install, update, remove, and query packages efficiently across distributions
3. **Manage Repositories**: Configure, secure, and maintain package repositories
4. **Handle Dependencies**: Resolve complex dependency chains and conflicts
5. **Implement Security**: Verify package integrity and manage trusted sources
6. **Automate Operations**: Create scripts for package management automation
7. **Build Custom Packages**: Compile from source and create distribution packages
8. **Integrate Modern Solutions**: Use Snap, Flatpak, and AppImage effectively

## Topics

### 4.1 Package Management Fundamentals
- **Package Concepts**: Packages, dependencies, conflicts, and provides relationships
- **Package Formats**: .deb, .rpm, .pkg.tar.xz, .snap, .flatpak formats and structures
- **Repository Architecture**: Package repositories, mirrors, and distribution systems
- **Digital Signatures**: Package verification, GPG keys, and security chains
- **Dependency Resolution**: Algorithms, strategies, and conflict resolution
- **Version Management**: Semantic versioning, epoch handling, and version pinning

### 4.2 Debian/Ubuntu Package Management (APT)
- **APT Ecosystem**: apt, apt-get, aptitude, dpkg relationships and use cases
- **Package Operations**: Installation, removal, upgrading, and configuration
- **Repository Management**: sources.list, PPAs, and third-party repositories
- **Advanced Features**: Package holding, pinning, and policy management
- **Troubleshooting**: Broken packages, dependency issues, and recovery
- **Security Features**: Package verification, secure APT, and vulnerability scanning

### 4.3 Red Hat/CentOS Package Management (YUM/DNF)
- **YUM vs DNF**: Legacy YUM and modern DNF comparison and migration
- **Package Operations**: Installation, removal, updating, and querying
- **Repository Management**: .repo files, GPG keys, and repository priorities
- **Groups and Modules**: Package groups, modules, and stream management
- **History and Rollback**: Transaction history and system rollback capabilities
- **Enterprise Features**: Satellite integration, custom repositories, and compliance

### 4.4 SUSE Package Management (Zypper)
- **Zypper Fundamentals**: Command structure, patterns, and package management
- **Repository Management**: Service management, priorities, and refresh policies
- **Pattern Management**: Software patterns and meta-packages
- **Patch Management**: Security updates, patch management, and maintenance windows
- **Lock Management**: Package and pattern locking for system stability
- **Integration**: YaST integration and enterprise management features

### 4.5 Arch Linux Package Management (Pacman)
- **Pacman Operations**: Package installation, removal, and system updates
- **AUR Integration**: Arch User Repository and helper tools (yay, paru)
- **Package Building**: PKGBUILD creation and makepkg usage
- **System Maintenance**: Orphan cleanup, cache management, and optimization
- **Rolling Release Management**: Partial upgrades, downgrade strategies
- **Custom Repositories**: Creating and maintaining custom repositories

### 4.6 Universal Package Managers
- **Snap Packages**: Containerized applications, channels, and confinement
- **Flatpak**: Application distribution, runtimes, and sandboxing
- **AppImage**: Portable applications and integration strategies
- **Container Integration**: Docker-based package distribution
- **Performance Considerations**: Resource usage, startup times, and optimization
- **Enterprise Deployment**: Management tools and enterprise considerations

### 4.7 Repository Management and Security
- **Repository Configuration**: Mirror selection, failover, and load balancing
- **Security Implementation**: GPG verification, HTTPS enforcement, and key management
- **Custom Repositories**: Creating, maintaining, and distributing custom repositories
- **Proxy Configuration**: Corporate proxies, caching, and bandwidth optimization
- **Compliance Management**: License tracking, vulnerability scanning, and auditing
- **Backup and Recovery**: Repository backup strategies and disaster recovery

### 4.8 Source Compilation and Custom Packages
- **Build Environment**: Development tools, build dependencies, and environments
- **Configuration Systems**: autotools, CMake, meson, and custom build systems
- **Package Creation**: Creating .deb, .rpm, and other distribution packages
- **Dependency Management**: Build-time vs runtime dependencies
- **Testing and Quality**: Package testing, linting, and quality assurance
- **Distribution**: Package signing, repository inclusion, and maintenance

### 4.9 Package Automation and Scripting
- **Automated Installation**: Deployment scripts and configuration management
- **Update Automation**: Automated patching, testing, and rollback strategies
- **Monitoring Integration**: Package change monitoring and alerting
- **CI/CD Integration**: Package management in continuous integration pipelines
- **Inventory Management**: Package inventory tracking and compliance reporting
- **Performance Optimization**: Caching strategies, parallel operations, and efficiency

## Essential Command Reference

| Distribution | Package Manager | Install | Remove | Update | Search | List Installed |
|--------------|----------------|---------|---------|---------|---------|----------------|
| **Debian/Ubuntu** | APT | `apt install pkg` | `apt remove pkg` | `apt update && apt upgrade` | `apt search term` | `apt list --installed` |
| **Red Hat/CentOS** | DNF/YUM | `dnf install pkg` | `dnf remove pkg` | `dnf update` | `dnf search term` | `dnf list installed` |
| **SUSE** | Zypper | `zypper install pkg` | `zypper remove pkg` | `zypper update` | `zypper search term` | `zypper pa -i` |
| **Arch** | Pacman | `pacman -S pkg` | `pacman -R pkg` | `pacman -Syu` | `pacman -Ss term` | `pacman -Q` |
| **Universal** | Snap | `snap install pkg` | `snap remove pkg` | `snap refresh` | `snap find term` | `snap list` |

### Advanced Command Reference

| Operation | APT | DNF/YUM | Zypper | Pacman |
|-----------|-----|---------|---------|---------|
| **Show package info** | `apt show pkg` | `dnf info pkg` | `zypper info pkg` | `pacman -Si pkg` |
| **Download only** | `apt download pkg` | `dnf download pkg` | `zypper download pkg` | `pacman -Sw pkg` |
| **Reinstall package** | `apt reinstall pkg` | `dnf reinstall pkg` | `zypper install -f pkg` | `pacman -S pkg` |
| **Clean cache** | `apt autoclean` | `dnf clean all` | `zypper clean` | `pacman -Sc` |
| **Fix broken** | `apt --fix-broken install` | `dnf distro-sync` | `zypper verify` | `pacman -Dk` |

## Practical Examples
### Distribution-Specific Package Management

#### Advanced APT Operations (Debian/Ubuntu)
```bash
# Comprehensive APT workflow
sudo apt update                              # Update package lists
sudo apt list --upgradable                   # Check available updates
sudo apt upgrade                             # Upgrade installed packages
sudo apt full-upgrade                        # Upgrade with dependency changes

# Package installation with options
sudo apt install nginx                       # Basic installation
sudo apt install nginx=1.18.0-6             # Install specific version
sudo apt install --no-install-recommends vim # Skip recommended packages
sudo apt install -y curl wget               # Non-interactive installation

# Package removal strategies
sudo apt remove nginx                        # Remove package, keep config
sudo apt purge nginx                         # Remove package and config
sudo apt autoremove                         # Remove orphaned dependencies
sudo apt autoremove --purge                 # Remove orphans and their configs

# Advanced package queries
apt list --installed | grep nginx           # Find installed packages
apt search --names-only web                 # Search in package names only
apt show nginx                              # Detailed package information
apt depends nginx                           # Show dependencies
apt rdepends nginx                          # Show reverse dependencies

# Package management policies
apt policy nginx                            # Show version policy
sudo apt-mark hold nginx                    # Prevent package updates
sudo apt-mark unhold nginx                  # Allow package updates
apt-mark showhold                           # List held packages

# Cache and repository management
sudo apt update --fix-missing               # Fix missing packages
sudo apt clean                              # Clear downloaded package cache
sudo apt autoclean                          # Clear outdated cached packages
```

#### Comprehensive DNF/YUM Operations (Red Hat/CentOS)
```bash
# Modern DNF operations (preferred on newer systems)
sudo dnf update                             # Update all packages
sudo dnf upgrade                            # Same as update (for clarity)
sudo dnf install nginx                      # Install package
sudo dnf install nginx-1.20.*              # Install with version wildcard
sudo dnf reinstall nginx                    # Reinstall package

# Package removal and cleanup
sudo dnf remove nginx                       # Remove package
sudo dnf autoremove                         # Remove orphaned dependencies
sudo dnf clean all                          # Clean all cached data

# Advanced querying and information
dnf search nginx                            # Search for packages
dnf info nginx                              # Package information
dnf provides */nginx                        # Find package providing file
dnf history                                 # Transaction history
dnf history info 5                          # Details of transaction 5
dnf history undo 5                          # Undo transaction 5

# Group and module management
dnf group list                              # List package groups
sudo dnf group install "Development Tools"  # Install package group
dnf module list                             # List available modules
sudo dnf module install nginx:1.20         # Install specific module stream

# Repository management
dnf repolist                                # List enabled repositories
sudo dnf config-manager --disable epel      # Disable repository
sudo dnf config-manager --enable epel       # Enable repository
```

#### Zypper Operations (SUSE)
```bash
# Basic zypper operations
sudo zypper refresh                         # Refresh repositories
sudo zypper update                          # Update packages
sudo zypper install nginx                   # Install package
sudo zypper remove nginx                    # Remove package

# Advanced features
zypper search -d nginx                      # Detailed search
zypper info nginx                           # Package information
zypper what-provides nginx                  # Find providing packages

# Pattern management (SUSE-specific)
zypper search -t pattern                    # List patterns
sudo zypper install -t pattern lamp_server  # Install pattern

# Repository and service management
zypper repos                                # List repositories
sudo zypper addrepo URL alias               # Add repository
sudo zypper removerepo alias                # Remove repository
zypper services                             # List services
```

#### Pacman Operations (Arch Linux)
```bash
# System maintenance
sudo pacman -Syu                            # Update system (sync, refresh, upgrade)
sudo pacman -Syyu                           # Force refresh and upgrade
pacman -Qtdq | sudo pacman -Rns -           # Remove orphaned packages

# Package operations
sudo pacman -S nginx                        # Install package
sudo pacman -S extra/nginx                  # Install from specific repository
sudo pacman -U package.pkg.tar.xz          # Install local package
sudo pacman -R nginx                        # Remove package
sudo pacman -Rns nginx                      # Remove package with dependencies

# Querying packages
pacman -Ss nginx                            # Search repositories
pacman -Qs nginx                            # Search installed packages
pacman -Si nginx                            # Repository package info
pacman -Qi nginx                            # Installed package info
pacman -Ql nginx                            # List package files
pacman -Qo /usr/bin/nginx                   # Find package owning file

# AUR helper integration (using yay)
yay -S aur-package                          # Install from AUR
yay -Sua                                    # Update AUR packages
yay -Yc                                     # Clean unneeded dependencies
```

### Repository Configuration and Management

#### APT Repository Management
```bash
#!/bin/bash
# apt-repo-manager.sh - Comprehensive APT repository management

# Add PPAs safely
add_ppa() {
    local ppa="$1"
    echo "Adding PPA: $ppa"
    sudo add-apt-repository -y "ppa:$ppa"
    sudo apt update
}

# Add custom repository with GPG key
add_custom_repo() {
    local repo_url="$1"
    local key_url="$2"
    local repo_name="$3"
    
    echo "Adding custom repository: $repo_name"
    
    # Add GPG key
    wget -qO - "$key_url" | sudo apt-key add -
    
    # Add repository
    echo "deb $repo_url $(lsb_release -cs) main" | \
        sudo tee "/etc/apt/sources.list.d/$repo_name.list"
    
    sudo apt update
}

# Docker repository example
add_docker_repo() {
    # Add Docker's official GPG key
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    
    # Add Docker repository
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    sudo apt update
}

# Repository audit and cleanup
audit_repositories() {
    echo "=== Repository Audit ==="
    echo "Active repositories:"
    grep -h '^deb' /etc/apt/sources.list /etc/apt/sources.list.d/*.list 2>/dev/null | sort -u
    
    echo ""
    echo "PPAs installed:"
    grep -h '^deb.*ppa\.launchpad\.net' /etc/apt/sources.list.d/*.list 2>/dev/null
    
    echo ""
    echo "Third-party repositories:"
    grep -h '^deb' /etc/apt/sources.list.d/*.list 2>/dev/null | grep -v 'ppa\.launchpad\.net' | grep -v 'ubuntu\.com'
}

# Remove PPA
remove_ppa() {
    local ppa="$1"
    echo "Removing PPA: $ppa"
    sudo add-apt-repository --remove -y "ppa:$ppa"
    sudo apt update
}

# Usage examples
case "${1:-help}" in
    "add-ppa")
        add_ppa "$2"
        ;;
    "remove-ppa")
        remove_ppa "$2"
        ;;
    "add-docker")
        add_docker_repo
        ;;
    "audit")
        audit_repositories
        ;;
    "help")
        echo "Usage: $0 {add-ppa|remove-ppa|add-docker|audit} [arguments]"
        ;;
esac
```

#### YUM/DNF Repository Configuration
```bash
#!/bin/bash
# dnf-repo-manager.sh - DNF/YUM repository management

# Add EPEL repository
add_epel() {
    echo "Adding EPEL repository"
    sudo dnf install -y epel-release
    sudo dnf config-manager --set-enabled epel
}

# Add custom repository
add_custom_repo() {
    local name="$1"
    local baseurl="$2"
    local gpgkey="$3"
    
    cat << EOF | sudo tee "/etc/yum.repos.d/$name.repo"
[$name]
name=$name Repository
baseurl=$baseurl
enabled=1
gpgcheck=1
gpgkey=$gpgkey
EOF
    
    echo "Added repository: $name"
    sudo dnf makecache
}

# Docker repository for CentOS/RHEL
add_docker_repo() {
    sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    echo "Docker repository added"
}

# Repository management
manage_repo() {
    local action="$1"
    local repo="$2"
    
    case "$action" in
        "enable")
            sudo dnf config-manager --set-enabled "$repo"
            ;;
        "disable")
            sudo dnf config-manager --set-disabled "$repo"
            ;;
        "list")
            dnf repolist all
            ;;
    esac
}

# Clean up repositories
cleanup_repos() {
    echo "Cleaning repository cache"
    sudo dnf clean all
    sudo dnf makecache
}

# Usage
case "${1:-help}" in
    "add-epel")
        add_epel
        ;;
    "add-docker")
        add_docker_repo
        ;;
    "enable")
        manage_repo "enable" "$2"
        ;;
    "disable")
        manage_repo "disable" "$2"
        ;;
    "list")
        manage_repo "list"
        ;;
    "cleanup")
        cleanup_repos
        ;;
    "help")
        echo "Usage: $0 {add-epel|add-docker|enable|disable|list|cleanup} [repo-name]"
        ;;
esac
```

### Advanced Package Operations

#### Package Dependency Analysis
```bash
#!/bin/bash
# package-analyzer.sh - Advanced package dependency analysis

analyze_dependencies() {
    local package="$1"
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    
    echo "=== Dependency Analysis for: $package ==="
    
    case "$distro" in
        "ubuntu"|"debian")
            echo "Direct dependencies:"
            apt depends "$package" 2>/dev/null | grep "Depends:"
            
            echo ""
            echo "Reverse dependencies:"
            apt rdepends "$package" 2>/dev/null | head -10
            
            echo ""
            echo "Package size and installation impact:"
            apt show "$package" 2>/dev/null | grep -E "(Size|Installed-Size)"
            ;;
            
        "centos"|"rhel"|"fedora")
            echo "Direct dependencies:"
            dnf deplist "$package" 2>/dev/null | grep "dependency:"
            
            echo ""
            echo "What requires this package:"
            dnf repoquery --whatrequires "$package" 2>/dev/null | head -10
            
            echo ""
            echo "Package information:"
            dnf info "$package" 2>/dev/null | grep -E "(Size|Installed size)"
            ;;
            
        "arch")
            echo "Direct dependencies:"
            pacman -Si "$package" 2>/dev/null | grep "Depends On"
            
            echo ""
            echo "Optional dependencies:"
            pacman -Si "$package" 2>/dev/null | grep "Optional Deps" -A 10
            
            echo ""
            echo "Required by:"
            pacman -Sii "$package" 2>/dev/null | grep "Required By"
            ;;
    esac
}

# Find packages by file
find_package_by_file() {
    local filepath="$1"
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    
    echo "Finding package that provides: $filepath"
    
    case "$distro" in
        "ubuntu"|"debian")
            dpkg -S "$filepath" 2>/dev/null || apt-file search "$filepath" 2>/dev/null
            ;;
        "centos"|"rhel"|"fedora")
            rpm -qf "$filepath" 2>/dev/null || dnf provides "$filepath" 2>/dev/null
            ;;
        "arch")
            pacman -Qo "$filepath" 2>/dev/null || pacman -F "$filepath" 2>/dev/null
            ;;
    esac
}

# Security vulnerability check
check_vulnerabilities() {
    local package="$1"
    
    echo "=== Security Check for: $package ==="
    
    # Check for known vulnerabilities (requires additional tools)
    if command -v vulners-lookup &> /dev/null; then
        vulners-lookup "$package"
    else
        echo "Install vulners-lookup or similar tool for vulnerability scanning"
    fi
    
    # Check package signatures
    case "$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)" in
        "ubuntu"|"debian")
            apt-cache policy "$package" | grep -A 5 "Version table"
            ;;
        "centos"|"rhel"|"fedora")
            dnf info "$package" | grep -E "(Signature|From repo)"
            ;;
    esac
}

# Usage
case "${1:-help}" in
    "deps")
        analyze_dependencies "$2"
        ;;
    "file")
        find_package_by_file "$2"
        ;;
    "security")
        check_vulnerabilities "$2"
        ;;
    "help")
        echo "Usage: $0 {deps|file|security} <package-name|file-path>"
        ;;
esac
```

#### Source Compilation Management
```bash
#!/bin/bash
# source-compiler.sh - Automated source compilation and packaging

compile_from_source() {
    local source_url="$1"
    local package_name="$2"
    local install_prefix="${3:-/usr/local}"
    
    # Create build directory
    local build_dir="/tmp/build-$package_name-$$"
    mkdir -p "$build_dir"
    cd "$build_dir"
    
    echo "=== Compiling $package_name from source ==="
    echo "Source URL: $source_url"
    echo "Install prefix: $install_prefix"
    echo "Build directory: $build_dir"
    
    # Download and extract source
    echo "Downloading source..."
    if [[ "$source_url" =~ \.git$ ]]; then
        git clone "$source_url" "$package_name"
        cd "$package_name"
    else
        wget "$source_url" -O source.tar.gz
        tar -xzf source.tar.gz
        cd */
    fi
    
    # Install build dependencies
    install_build_deps "$package_name"
    
    # Configure build
    echo "Configuring build..."
    if [[ -f "configure" ]]; then
        ./configure --prefix="$install_prefix"
    elif [[ -f "CMakeLists.txt" ]]; then
        mkdir build && cd build
        cmake .. -DCMAKE_INSTALL_PREFIX="$install_prefix"
    elif [[ -f "meson.build" ]]; then
        meson setup build --prefix="$install_prefix"
        cd build
    else
        echo "Unknown build system"
        return 1
    fi
    
    # Compile
    echo "Compiling..."
    make -j$(nproc)
    
    # Install or create package
    if command -v checkinstall &> /dev/null; then
        echo "Creating package with checkinstall..."
        sudo checkinstall --pkgname="$package_name" --pkgversion="custom" --pakdir="$HOME/packages" -y
    else
        echo "Installing directly..."
        sudo make install
    fi
    
    # Cleanup
    cd /
    rm -rf "$build_dir"
    
    echo "=== Compilation complete ==="
}

install_build_deps() {
    local package_name="$1"
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    
    echo "Installing build dependencies..."
    
    case "$distro" in
        "ubuntu"|"debian")
            sudo apt update
            sudo apt install -y build-essential cmake meson pkg-config git wget
            
            # Try to install package build dependencies
            if apt-cache show "${package_name}" &>/dev/null; then
                sudo apt build-dep -y "$package_name" 2>/dev/null || true
            fi
            ;;
            
        "centos"|"rhel"|"fedora")
            sudo dnf groupinstall -y "Development Tools"
            sudo dnf install -y cmake meson pkgconfig git wget
            
            # Try to install package build dependencies
            sudo dnf builddep -y "$package_name" 2>/dev/null || true
            ;;
            
        "arch")
            sudo pacman -S --needed base-devel cmake meson pkgconf git wget
            ;;
    esac
}

# Create simple package
create_simple_package() {
    local name="$1"
    local version="$2"
    local description="$3"
    local files="$4"  # Space-separated list of files
    
    echo "Creating simple package: $name"
    
    case "$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)" in
        "ubuntu"|"debian")
            create_deb_package "$name" "$version" "$description" "$files"
            ;;
        "centos"|"rhel"|"fedora")
            create_rpm_package "$name" "$version" "$description" "$files"
            ;;
    esac
}

# Usage
case "${1:-help}" in
    "compile")
        compile_from_source "$2" "$3" "$4"
        ;;
    "package")
        create_simple_package "$2" "$3" "$4" "$5"
        ;;
    "help")
        echo "Usage: $0 {compile|package} <arguments>"
        echo "  compile <source_url> <package_name> [install_prefix]"
        echo "  package <name> <version> <description> <files>"
        ;;
esac
```

### Automation and Maintenance Scripts

#### Comprehensive Package Maintenance
```bash
#!/bin/bash
# package-maintenance.sh - Automated package maintenance and security updates

# Configuration
LOG_FILE="/var/log/package-maintenance.log"
BACKUP_DIR="/var/backups/packages"
EMAIL_REPORT="admin@example.com"

log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

create_package_snapshot() {
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    local snapshot_file="$BACKUP_DIR/packages-$(date +%Y%m%d_%H%M%S).txt"
    
    mkdir -p "$BACKUP_DIR"
    
    case "$distro" in
        "ubuntu"|"debian")
            dpkg -l > "$snapshot_file"
            ;;
        "centos"|"rhel"|"fedora")
            rpm -qa > "$snapshot_file"
            ;;
        "arch")
            pacman -Q > "$snapshot_file"
            ;;
    esac
    
    log_message "Package snapshot created: $snapshot_file"
}

update_system() {
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    local update_count=0
    
    log_message "Starting system update process"
    
    case "$distro" in
        "ubuntu"|"debian")
            apt update
            update_count=$(apt list --upgradable 2>/dev/null | wc -l)
            if [[ $update_count -gt 1 ]]; then
                log_message "Updates available: $((update_count - 1)) packages"
                DEBIAN_FRONTEND=noninteractive apt upgrade -y
                apt autoremove -y
                apt autoclean
            fi
            ;;
            
        "centos"|"rhel"|"fedora")
            update_count=$(dnf check-update | wc -l)
            if [[ $update_count -gt 0 ]]; then
                log_message "Updates available: $update_count packages"
                dnf update -y
                dnf autoremove -y
                dnf clean all
            fi
            ;;
            
        "arch")
            pacman -Syu --noconfirm
            pacman -Qtdq | pacman -Rns --noconfirm - 2>/dev/null || true
            ;;
    esac
    
    log_message "System update completed"
}

security_scan() {
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    
    log_message "Starting security scan"
    
    case "$distro" in
        "ubuntu"|"debian")
            # Check for security updates
            apt list --upgradable 2>/dev/null | grep -i security || log_message "No security updates found"
            
            # Check for vulnerable packages (requires debsecan)
            if command -v debsecan &> /dev/null; then
                debsecan --suite $(lsb_release -cs) --format detail > /tmp/security_report.txt
                if [[ -s /tmp/security_report.txt ]]; then
                    log_message "Security vulnerabilities found - see /tmp/security_report.txt"
                fi
            fi
            ;;
            
        "centos"|"rhel"|"fedora")
            # Check for security updates
            dnf updateinfo list security 2>/dev/null || log_message "No security updates found"
            ;;
    esac
}

generate_report() {
    local report_file="/tmp/package_maintenance_report.txt"
    
    cat > "$report_file" << EOF
Package Maintenance Report
Generated: $(date)
System: $(hostnamectl | grep "Operating System" | cut -d: -f2)

=== Package Statistics ===
$(get_package_stats)

=== Recent Log Entries ===
$(tail -20 "$LOG_FILE")

=== Disk Usage ===
$(df -h / /var)

=== System Load ===
$(uptime)
EOF

    if [[ -n "$EMAIL_REPORT" ]]; then
        mail -s "Package Maintenance Report - $(hostname)" "$EMAIL_REPORT" < "$report_file"
    fi
    
    log_message "Report generated: $report_file"
}

get_package_stats() {
    local distro=$(cat /etc/os-release | grep "^ID=" | cut -d'=' -f2)
    
    case "$distro" in
        "ubuntu"|"debian")
            echo "Installed packages: $(dpkg -l | grep "^ii" | wc -l)"
            echo "Available updates: $(apt list --upgradable 2>/dev/null | wc -l)"
            ;;
        "centos"|"rhel"|"fedora")
            echo "Installed packages: $(rpm -qa | wc -l)"
            echo "Available updates: $(dnf check-update 2>/dev/null | wc -l)"
            ;;
        "arch")
            echo "Installed packages: $(pacman -Q | wc -l)"
            echo "Orphaned packages: $(pacman -Qtdq 2>/dev/null | wc -l)"
            ;;
    esac
}

# Main execution
main() {
    local action="${1:-full}"
    
    case "$action" in
        "update")
            create_package_snapshot
            update_system
            ;;
        "security")
            security_scan
            ;;
        "report")
            generate_report
            ;;
        "full")
            create_package_snapshot
            update_system
            security_scan
            generate_report
            ;;
        "help")
            echo "Usage: $0 {update|security|report|full}"
            ;;
    esac
}

main "$@"
```

## Lab Exercises

### Lab 1: Multi-Distribution Package Management
**Objective:** Master package management across different Linux distributions.

**Tasks:**
1. Set up virtual machines with Ubuntu, CentOS, and Arch Linux
2. Install identical software stacks using each distribution's package manager
3. Compare package versions, dependencies, and installation processes
4. Document differences in package naming conventions and repositories
5. Create cross-distribution package management scripts

**Deliverables:**
- Multi-distribution package management comparison
- Cross-platform installation scripts
- Package ecosystem analysis report

### Lab 2: Repository Management and Security
**Objective:** Implement secure repository management and package verification.

**Tasks:**
1. Configure custom repositories with proper GPG key management
2. Set up repository priorities and pinning policies
3. Implement automated repository health monitoring
4. Create security scanning procedures for packages
5. Establish package verification and integrity checking workflows

**Deliverables:**
- Secure repository configuration documentation
- Automated monitoring scripts
- Security verification procedures

### Lab 3: Source Compilation and Custom Packages
**Objective:** Master source compilation and custom package creation.

**Tasks:**
1. Compile complex software from source with custom configurations
2. Create distribution-specific packages (.deb, .rpm) from compiled software
3. Set up automated build environments with dependency management
4. Implement package testing and quality assurance procedures
5. Create custom repository for distributing custom packages

**Deliverables:**
- Custom package build automation
- Package testing frameworks
- Custom repository setup

### Lab 4: Package Automation and Maintenance
**Objective:** Implement comprehensive package automation and maintenance strategies.

**Tasks:**
1. Create automated update and patching workflows
2. Implement rollback procedures for failed updates
3. Set up package inventory and compliance monitoring
4. Create automated security scanning and vulnerability management
5. Integrate package management with configuration management tools

**Deliverables:**
- Automated maintenance workflows
- Rollback and recovery procedures
- Compliance monitoring system

## Best Practices Summary

### Package Management Security

| Practice | Implementation | Rationale |
|----------|----------------|-----------|
| **Verify Signatures** | Always check GPG signatures | Prevent malicious packages |
| **Use HTTPS** | Configure HTTPS repositories | Protect against MITM attacks |
| **Regular Updates** | Automated security patching | Minimize vulnerability exposure |
| **Repository Audit** | Regular third-party repo review | Maintain trusted sources |
| **Backup Before Updates** | System snapshots before major updates | Enable quick recovery |

### Performance Optimization

1. **Repository Configuration**
   - Use geographically close mirrors
   - Configure repository priorities
   - Enable repository caching for multiple systems

2. **Package Operations**
   - Use parallel downloads when available
   - Clean package caches regularly
   - Remove orphaned packages periodically

3. **Automation Strategy**
   - Schedule updates during maintenance windows
   - Use unattended upgrades for security patches
   - Implement staged rollouts for major updates

### Enterprise Considerations

1. **Change Management**
   - Test updates in staging environments
   - Document all package changes
   - Implement approval workflows for major updates

2. **Compliance**
   - Maintain package inventories
   - Track license compliance
   - Monitor security vulnerabilities

3. **Standardization**
   - Use consistent package sets across environments
   - Standardize repository configurations
   - Implement configuration management integration

## Troubleshooting Common Issues

### Dependency Conflicts
```bash
# APT dependency issues
sudo apt --fix-broken install        # Fix broken dependencies
sudo dpkg --configure -a             # Configure unconfigured packages
sudo apt clean && sudo apt update    # Clean and refresh cache

# DNF dependency issues
sudo dnf distro-sync                  # Synchronize with repositories
sudo dnf history undo last           # Undo last transaction
sudo dnf autoremove                   # Remove orphaned dependencies

# Pacman dependency issues
sudo pacman -Dk                       # Check database consistency
sudo pacman -Syyu                     # Force refresh and upgrade
```

### Repository Problems
```bash
# GPG key issues
sudo apt-key update                   # Update APT keys
sudo rpm --import GPG-KEY-FILE        # Import RPM GPG key

# Repository corruption
sudo rm -rf /var/lib/apt/lists/*      # Clear APT cache
sudo apt update                       # Rebuild cache

sudo dnf clean all                    # Clear DNF cache
sudo dnf makecache                    # Rebuild cache
```

### Package Database Corruption
```bash
# APT database issues
sudo dpkg --configure -a             # Configure packages
sudo apt-get install -f              # Fix broken installs

# RPM database issues
sudo rpm --rebuilddb                  # Rebuild RPM database

# Pacman database issues
sudo pacman -Dk                       # Check database
sudo pacman-db-upgrade                # Upgrade database format
```

## Assessment Criteria

Students will be evaluated on their ability to:

| Criteria | Proficient (4) | Developing (3) | Beginning (2) | Inadequate (1) |
|----------|----------------|----------------|---------------|----------------|
| **Multi-Distribution Proficiency** | Masters package management across all major distributions | Good proficiency with most distributions | Basic knowledge with some distributions | Limited to one distribution |
| **Security Implementation** | Implements comprehensive security practices | Good security awareness with minor gaps | Basic security practices | Poor security practices |
| **Automation Skills** | Creates sophisticated automation solutions | Good automation with functional scripts | Basic automation capabilities | Manual operations only |
| **Troubleshooting Ability** | Efficiently resolves complex package issues | Good problem-solving with systematic approach | Basic troubleshooting with guidance | Struggles with problem resolution |

## Next Steps

After mastering package management, proceed to:

- **Module 5: Processes & Services** - Apply package management knowledge to service installation and management
- **Module 6: Users, Groups & Authentication** - Use packages to implement authentication and security systems
- **Module 9: Shell Scripting Fundamentals** - Create advanced package management automation scripts

The package management expertise developed in this module is essential for maintaining secure, up-to-date systems and forms the foundation for advanced system administration and automation tasks.
