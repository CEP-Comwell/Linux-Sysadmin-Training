# Module 9: Shell Scripting Fundamentals

## Overview
This module covers shell scripting essentials for Linux system administration. You'll learn to write effective bash scripts, automate routine tasks, handle errors, and create robust automation solutions for system management.

## Learning Objectives
By the end of this module, you will be able to:
- Write effective bash scripts for system administration
- Use variables, functions, and control structures
- Handle command-line arguments and user input
- Implement error handling and logging in scripts
- Create automated system maintenance scripts
- Debug and optimize shell scripts

## Topics

### 9.1 Shell Scripting Basics
- Shebang and script execution
- Variables and parameter expansion
- Quoting and escaping
- Comments and documentation
- Script permissions and execution

### 9.2 Control Structures
- Conditional statements (if/then/else)
- Case statements
- Loops (for, while, until)
- Break and continue
- Function definitions and usage

### 9.3 Input/Output and File Operations
- Reading user input
- Command-line arguments
- File testing and manipulation
- Redirections and pipes in scripts
- Here documents and here strings

### 9.4 Advanced Scripting Techniques
- Arrays and associative arrays
- Regular expressions in scripts
- Process substitution
- Signal handling and traps
- Background processes and job control

### 9.5 Error Handling and Debugging
- Exit codes and error checking
- Logging and debugging techniques
- Script validation and testing
- Error recovery strategies
- Best practices for robust scripts

### 9.6 System Administration Scripts
- Backup and restore scripts
- User management automation
- System monitoring scripts
- Log analysis automation
- Maintenance and cleanup scripts

## Practical Examples

### Basic Script Structure
```bash
#!/bin/bash
# Script: basic-example.sh
# Purpose: Demonstrate basic script structure
# Author: System Administrator
# Date: $(date)

# Set script options
set -euo pipefail  # Exit on error, undefined vars, pipe failures

# Variables
SCRIPT_NAME=$(basename "$0")
LOG_FILE="/var/log/${SCRIPT_NAME%.sh}.log"

# Functions
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

main() {
    log_message "Script started"
    
    # Script logic here
    echo "Hello, World!"
    
    log_message "Script completed successfully"
}

# Execute main function
main "$@"
```

### Variables and Parameter Expansion
```bash
#!/bin/bash
# Demonstrate variables and parameter expansion

# Basic variables
NAME="John Doe"
AGE=30
readonly CONSTANT="unchangeable"

# Environment variables
export PATH="/usr/local/bin:$PATH"

# Command substitution
CURRENT_DATE=$(date)
USER_COUNT=`who | wc -l`

# Parameter expansion examples
FILE="/path/to/file.txt.bak"
echo "Filename: ${FILE##*/}"           # file.txt.bak
echo "Directory: ${FILE%/*}"           # /path/to
echo "Name without extension: ${FILE%%.*}"  # file
echo "Extension: ${FILE##*.}"          # bak

# Default values
USERNAME=${1:-"default_user"}
DEBUG=${DEBUG:-"false"}

# String manipulation
TEXT="Hello World"
echo "${TEXT,,}"    # hello world (lowercase)
echo "${TEXT^^}"    # HELLO WORLD (uppercase)
echo "${TEXT/o/O}"  # HellO World (first replacement)
echo "${TEXT//o/O}" # HellO WOrld (all replacements)
```

### Control Structures
```bash
#!/bin/bash
# Control structure examples

# If statements
check_file() {
    local file="$1"
    
    if [[ -f "$file" ]]; then
        echo "$file exists and is a regular file"
    elif [[ -d "$file" ]]; then
        echo "$file exists and is a directory"
    else
        echo "$file does not exist"
    fi
}

# Case statement
process_option() {
    case "$1" in
        start)
            echo "Starting service..."
            ;;
        stop)
            echo "Stopping service..."
            ;;
        restart)
            echo "Restarting service..."
            ;;
        status)
            echo "Checking service status..."
            ;;
        *)
            echo "Usage: $0 {start|stop|restart|status}"
            exit 1
            ;;
    esac
}

# For loops
echo "Files in current directory:"
for file in *; do
    if [[ -f "$file" ]]; then
        echo "File: $file"
    fi
done

# While loop
counter=1
while [[ $counter -le 5 ]]; do
    echo "Count: $counter"
    ((counter++))
done

# Until loop
number=1
until [[ $number -gt 3 ]]; do
    echo "Number: $number"
    ((number++))
done
```

### Functions and Arrays
```bash
#!/bin/bash
# Functions and arrays demonstration

# Function with return value
is_service_running() {
    local service="$1"
    if systemctl is-active --quiet "$service"; then
        return 0  # true
    else
        return 1  # false
    fi
}

# Function with multiple return values
get_system_info() {
    local -n info_array=$1  # nameref to array
    
    info_array[hostname]=$(hostname)
    info_array[kernel]=$(uname -r)
    info_array[uptime]=$(uptime -p)
    info_array[load]=$(uptime | awk -F'load average:' '{print $2}')
}

# Array examples
declare -a services=("nginx" "apache2" "mysql")
declare -A system_info

# Populate associative array
get_system_info system_info

# Process arrays
echo "Checking services:"
for service in "${services[@]}"; do
    if is_service_running "$service"; then
        echo "✓ $service is running"
    else
        echo "✗ $service is not running"
    fi
done

echo -e "\nSystem Information:"
for key in "${!system_info[@]}"; do
    echo "$key: ${system_info[$key]}"
done
```

### Command-Line Arguments and Input
```bash
#!/bin/bash
# Handle command-line arguments and user input

# Script usage function
usage() {
    cat << EOF
Usage: $0 [OPTIONS] <command>

OPTIONS:
    -h, --help      Show this help message
    -v, --verbose   Enable verbose output
    -f, --file      Specify input file
    -d, --debug     Enable debug mode

COMMANDS:
    backup          Perform backup operation
    restore         Perform restore operation
    check           Check system status

Examples:
    $0 -v backup
    $0 --file /path/to/file restore
EOF
}

# Parse command-line arguments
VERBOSE=false
DEBUG=false
INPUT_FILE=""

while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            usage
            exit 0
            ;;
        -v|--verbose)
            VERBOSE=true
            shift
            ;;
        -f|--file)
            INPUT_FILE="$2"
            shift 2
            ;;
        -d|--debug)
            DEBUG=true
            set -x  # Enable debug output
            shift
            ;;
        -*)
            echo "Unknown option: $1"
            usage
            exit 1
            ;;
        *)
            COMMAND="$1"
            shift
            ;;
    esac
done

# Validate required arguments
if [[ -z "${COMMAND:-}" ]]; then
    echo "Error: Command is required"
    usage
    exit 1
fi

# Interactive input example
read_user_confirmation() {
    local prompt="$1"
    local response
    
    while true; do
        read -p "$prompt (y/N): " response
        case $response in
            [Yy]*)
                return 0
                ;;
            [Nn]*|"")
                return 1
                ;;
            *)
                echo "Please answer yes or no."
                ;;
        esac
    done
}

# Use the functions
if [[ "$VERBOSE" == true ]]; then
    echo "Verbose mode enabled"
fi

if read_user_confirmation "Proceed with $COMMAND operation?"; then
    echo "Proceeding with $COMMAND..."
else
    echo "Operation cancelled"
    exit 0
fi
```

### Error Handling and Logging
```bash
#!/bin/bash
# Comprehensive error handling and logging

# Script configuration
readonly SCRIPT_NAME=$(basename "$0")
readonly LOG_DIR="/var/log"
readonly LOG_FILE="$LOG_DIR/${SCRIPT_NAME%.sh}.log"
readonly LOCK_FILE="/var/run/${SCRIPT_NAME%.sh}.lock"

# Logging functions
log() {
    local level="$1"
    shift
    local message="$*"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    echo "[$timestamp] [$level] $message" | tee -a "$LOG_FILE"
}

log_info() { log "INFO" "$@"; }
log_warn() { log "WARN" "$@"; }
log_error() { log "ERROR" "$@"; }
log_debug() { 
    [[ "${DEBUG:-false}" == true ]] && log "DEBUG" "$@"
}

# Error handling function
handle_error() {
    local exit_code=$?
    local line_number=$1
    
    log_error "Script failed at line $line_number with exit code $exit_code"
    cleanup
    exit $exit_code
}

# Cleanup function
cleanup() {
    log_info "Performing cleanup..."
    
    # Remove lock file
    [[ -f "$LOCK_FILE" ]] && rm -f "$LOCK_FILE"
    
    # Kill background processes
    [[ -n "${BACKGROUND_PID:-}" ]] && kill $BACKGROUND_PID 2>/dev/null
    
    log_info "Cleanup completed"
}

# Signal handlers
trap 'handle_error $LINENO' ERR
trap 'log_info "Script interrupted"; cleanup; exit 130' INT TERM

# Lock file mechanism
create_lock() {
    if [[ -f "$LOCK_FILE" ]]; then
        local pid=$(cat "$LOCK_FILE")
        if kill -0 "$pid" 2>/dev/null; then
            log_error "Script is already running (PID: $pid)"
            exit 1
        else
            log_warn "Removing stale lock file"
            rm -f "$LOCK_FILE"
        fi
    fi
    
    echo $$ > "$LOCK_FILE"
    log_info "Lock file created"
}

# Validate environment
validate_environment() {
    # Check if running as root when required
    if [[ $EUID -ne 0 && "${REQUIRE_ROOT:-false}" == true ]]; then
        log_error "This script must be run as root"
        exit 1
    fi
    
    # Check required commands
    local required_commands=("systemctl" "curl" "jq")
    for cmd in "${required_commands[@]}"; do
        if ! command -v "$cmd" >/dev/null 2>&1; then
            log_error "Required command not found: $cmd"
            exit 1
        fi
    done
    
    # Check disk space
    local available_space=$(df "$LOG_DIR" | awk 'NR==2 {print $4}')
    if [[ $available_space -lt 100000 ]]; then  # Less than ~100MB
        log_warn "Low disk space in $LOG_DIR"
    fi
}

# Main script logic
main() {
    log_info "Script $SCRIPT_NAME started"
    
    create_lock
    validate_environment
    
    # Your script logic here
    log_info "Performing main operations..."
    
    # Example of handling command failures
    if ! some_command_that_might_fail; then
        log_error "Command failed, but continuing..."
        # Handle the error appropriately
    fi
    
    log_info "Script completed successfully"
}

# Execute main function
main "$@"
```

## System Administration Scripts

### Backup Script
```bash
#!/bin/bash
# System backup script

# Configuration
BACKUP_SOURCE="/home /etc /var/www"
BACKUP_DEST="/backup"
BACKUP_NAME="system-backup-$(date +%Y%m%d-%H%M%S)"
RETENTION_DAYS=30
EMAIL="admin@example.com"

# Create backup
create_backup() {
    local backup_file="$BACKUP_DEST/$BACKUP_NAME.tar.gz"
    
    log_info "Starting backup to $backup_file"
    
    if tar -czf "$backup_file" $BACKUP_SOURCE; then
        log_info "Backup created successfully"
        
        # Calculate and log size
        local size=$(du -h "$backup_file" | cut -f1)
        log_info "Backup size: $size"
        
        return 0
    else
        log_error "Backup failed"
        return 1
    fi
}

# Cleanup old backups
cleanup_old_backups() {
    log_info "Cleaning up backups older than $RETENTION_DAYS days"
    
    find "$BACKUP_DEST" -name "system-backup-*.tar.gz" \
        -mtime +$RETENTION_DAYS -delete
}

# Send notification
send_notification() {
    local status="$1"
    local subject="Backup $status - $(hostname)"
    
    if [[ "$status" == "SUCCESS" ]]; then
        echo "Backup completed successfully on $(date)" | \
            mail -s "$subject" "$EMAIL"
    else
        echo "Backup failed on $(date). Check logs for details." | \
            mail -s "$subject" "$EMAIL"
    fi
}

# Main backup function
main() {
    if create_backup; then
        cleanup_old_backups
        send_notification "SUCCESS"
    else
        send_notification "FAILED"
        exit 1
    fi
}

main "$@"
```

### System Maintenance Script
```bash
#!/bin/bash
# Automated system maintenance

# Maintenance tasks
update_packages() {
    log_info "Updating package lists..."
    
    if command -v apt >/dev/null 2>&1; then
        apt update && apt upgrade -y
    elif command -v yum >/dev/null 2>&1; then
        yum update -y
    elif command -v dnf >/dev/null 2>&1; then
        dnf update -y
    fi
}

clean_logs() {
    log_info "Cleaning old log files..."
    
    # Clean journal logs older than 30 days
    journalctl --vacuum-time=30d
    
    # Clean old log files
    find /var/log -type f -name "*.log" -mtime +30 -delete
    
    # Clean package caches
    if command -v apt >/dev/null 2>&1; then
        apt autoremove -y && apt autoclean
    elif command -v yum >/dev/null 2>&1; then
        yum clean all
    fi
}

check_disk_space() {
    log_info "Checking disk space..."
    
    df -h | awk 'NR>1 {
        usage = $5
        gsub(/%/, "", usage)
        if (usage > 85) {
            print "WARNING: " $6 " is " $5 " full"
        }
    }'
}

check_services() {
    log_info "Checking critical services..."
    
    local services=("sshd" "nginx" "mysql")
    
    for service in "${services[@]}"; do
        if systemctl is-active --quiet "$service"; then
            log_info "✓ $service is running"
        else
            log_warn "✗ $service is not running"
            
            # Attempt to restart
            if systemctl start "$service"; then
                log_info "Successfully restarted $service"
            else
                log_error "Failed to restart $service"
            fi
        fi
    done
}

# Execute maintenance tasks
main() {
    log_info "Starting system maintenance"
    
    update_packages
    clean_logs
    check_disk_space
    check_services
    
    log_info "System maintenance completed"
}

main "$@"
```

## Script Best Practices

| Practice | Description |
|----------|-------------|
| Use `set -euo pipefail` | Exit on errors, undefined variables, pipe failures |
| Validate inputs | Check arguments and environment before proceeding |
| Include usage/help | Provide clear documentation for script usage |
| Implement logging | Track script execution and errors |
| Handle signals | Cleanup resources on interruption |
| Use functions | Organize code into reusable functions |
| Quote variables | Prevent word splitting and glob expansion |
| Check dependencies | Verify required commands and files exist |

## Debugging Techniques

### Debug Options
```bash
# Enable debug output
set -x          # Print commands before execution
set -v          # Print input lines as they are read

# Conditional debugging
[[ "${DEBUG:-false}" == true ]] && set -x

# Debug specific sections
set -x
# code to debug
set +x
```

### Testing Scripts
```bash
# Syntax checking
bash -n script.sh

# Dry run mode
if [[ "${DRY_RUN:-false}" == true ]]; then
    echo "Would execute: command"
else
    command
fi

# Test with different inputs
./script.sh --help
./script.sh --version
./script.sh invalid_option
```

## Lab Exercises
1. Create a comprehensive backup script with rotation
2. Write a system monitoring script with alerting
3. Develop a user management automation script
4. Build a log analysis and reporting script
5. Create a deployment automation script

## Next Steps
With shell scripting fundamentals mastered, you're ready to explore Storage & Filesystem Management in Module 10, where you'll learn advanced storage concepts and filesystem administration.
