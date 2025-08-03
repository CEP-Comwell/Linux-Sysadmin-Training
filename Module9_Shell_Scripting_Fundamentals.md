# Module 9: Shell Scripting Fundamentals

## Overview
You'll get comfortable writing scripts that automate your daily shell workflows, understanding how to pass arguments, handle errors, and structure reusable code with functions. This module covers shell scripting essentials for Linux system administration, teaching you to write effective bash scripts, automate routine tasks, and create robust automation solutions for system management.

## Learning Objectives
By the end of this module, you will be able to:
- Write a basic shell script with proper shebang and executable permissions
- Use variables and parameter expansion to manipulate inputs and defaults
- Control flow with if/else and case to branch logic cleanly
- Iterate over data using for, while, and until loops
- Create and invoke shell functions for modular, readable scripts
- Parse flags and options using getopts for robust user interfaces
- Incorporate error handling (set -e, set -u) and debug scripts with set -x
- Handle command-line arguments and user input effectively
- Create automated system maintenance scripts
- Debug and optimize shell scripts for production use

## Topics

### 9.1 Shell Scripting Basics
- Start scripts with shebang (#!/usr/bin/env bash) and make them executable
- Variables and parameter expansion, including default values
- Quoting and escaping for proper string handling
- Comments and documentation for maintainable code
- Script permissions and execution methods

### 9.2 Control Structures and Logic
- Conditional statements (if/then/else) for decision making
- Case statements for multi-branch logic
- Loops: for, while, and until constructs
- Break and continue for loop control
- Comparison operators and test conditions

### 9.3 Functions and Modular Code
- Function definitions and usage for code reusability
- Local variables and scope management
- Passing arguments to functions
- Return values and exit codes
- Sourcing external scripts and libraries

### 9.4 Command-Line Interface Design
- Parsing command-line options with getopts
- Handling positional parameters
- Creating flexible script interfaces
- Usage messages and help documentation
- Input validation and error handling

### 9.5 Advanced Parameter Handling
- Parameter expansion and substitution techniques
- Default values and conditional assignments
- Array handling and manipulation
- Environment variable management
- Configuration file processing

### 9.6 Error Handling and Debugging
- Enable error handling and debugging with set -e, set -u, and set -x
- Exit codes and error checking strategies
- Logging and debugging techniques
- Script validation and testing methods
- Error recovery and graceful failure handling
- Best practices for robust, production-ready scripts

### 9.7 Advanced Scripting Techniques
- Arrays and associative arrays
- Regular expressions in scripts
- Process substitution and advanced I/O
- Signal handling and trap mechanisms
- Background processes and job control

### 9.6 System Administration Scripts
- Backup and restore scripts
- User management automation
- System monitoring scripts
- Log analysis automation
- Maintenance and cleanup scripts

## Practical Examples

### Script Basics: Shebang and Permissions
```bash
#!/usr/bin/env bash
# Using env for portability - finds bash in PATH
# Alternative: #!/bin/bash (direct path)

# Make script executable
chmod +x myscript.sh

# Execute script
./myscript.sh
# or
bash myscript.sh
```

### Control Structure Comparison

| Loop Type | Syntax | When to Use |
|-----------|--------|-------------|
| for | `for item in list; do … done` | Iterating over a known set of values |
| while | `while [ condition ]; do … done` | Repeating until a condition changes |
| until | `until [ condition ]; do … done` | Running until a condition becomes true |

### Basic Script Structure with Best Practices
```bash
#!/usr/bin/env bash
# Script: basic-example.sh
# Purpose: Demonstrate basic script structure with best practices
# Author: System Administrator
# Date: $(date)

# Enable strict error handling
set -euo pipefail  # Exit on error, undefined vars, pipe failures

# Variables with defaults
SCRIPT_NAME=$(basename "$0")
LOG_FILE="${LOG_FILE:-/var/log/${SCRIPT_NAME%.sh}.log}"
DEBUG="${DEBUG:-false}"

# Enable debugging if requested
[[ "$DEBUG" == "true" ]] && set -x

# Functions
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" | tee -a "$LOG_FILE"
}

usage() {
    cat << EOF
Usage: $0 [OPTIONS]

OPTIONS:
    -h, --help      Show this help message
    -v, --verbose   Enable verbose output
    -d, --debug     Enable debug mode

EXAMPLES:
    $0 --verbose
    DEBUG=true $0
EOF
}

main() {
    log_message "Script started"
    
    # Script logic here
    echo "Hello, World!"
    
    log_message "Script completed successfully"
}

# Execute main function with all arguments
main "$@"
```

### Variables and Parameter Expansion with Defaults
```bash
#!/usr/bin/env bash
# Demonstrate variables and parameter expansion with defaults

# Basic variables with meaningful names
USER_NAME="John Doe"
USER_AGE=30
readonly SCRIPT_VERSION="1.0.0"

# Environment variables
export PATH="/usr/local/bin:$PATH"
export EDITOR="${EDITOR:-vim}"

# Command substitution (modern syntax preferred)
CURRENT_DATE=$(date)
ACTIVE_USERS=$(who | wc -l)
SYSTEM_LOAD=$(uptime | awk -F'load average:' '{print $2}')

# Parameter expansion techniques
FILE_PATH="/path/to/document.txt.bak"
echo "Full path: $FILE_PATH"
echo "Filename: ${FILE_PATH##*/}"           # document.txt.bak
echo "Directory: ${FILE_PATH%/*}"           # /path/to  
echo "Name without extension: ${FILE_PATH%%.*}"  # document
echo "Extension: ${FILE_PATH##*.}"          # bak
echo "Remove first extension: ${FILE_PATH%.*}"   # /path/to/document.txt

# Default values and conditional assignment
USERNAME="${1:-default_user}"              # Use $1 or default
CONFIG_FILE="${CONFIG_FILE:-/etc/myapp.conf}"
DEBUG_MODE="${DEBUG:-false}"
LOG_LEVEL="${LOG_LEVEL:-INFO}"

# Advanced parameter expansion
GREETING="Hello World"
echo "Original: $GREETING"
echo "Lowercase: ${GREETING,,}"             # hello world
echo "Uppercase: ${GREETING^^}"             # HELLO WORLD  
echo "First char upper: ${GREETING^}"       # Hello world
echo "Replace first 'o': ${GREETING/o/O}"   # HellO World
echo "Replace all 'o': ${GREETING//o/O}"    # HellO WOrld
echo "Length: ${#GREETING}"                 # 11

# Conditional assignment
: ${TEMP_DIR:="/tmp"}                       # Set if unset
DATABASE_URL="${DATABASE_URL:?Error: DATABASE_URL not set}"  # Required var
```

### Control Structures: if/else and case
```bash
#!/bin/bash
# Control structure examples

# If statements
```bash
#!/usr/bin/env bash
# Demonstrate control structures with clean logic branching

# If/else statements with proper test conditions
check_file_type() {
    local file="$1"
    
    if [[ -f "$file" ]]; then
        echo "$file is a regular file"
        return 0
    elif [[ -d "$file" ]]; then
        echo "$file is a directory" 
        return 0
    elif [[ -L "$file" ]]; then
        echo "$file is a symbolic link"
        return 0
    else
        echo "$file does not exist or is not accessible"
        return 1
    fi
}

# Numeric comparisons
check_disk_space() {
    local threshold="${1:-80}"
    local usage=$(df / | awk 'NR==2 {print int($5)}')
    
    if [[ $usage -gt $threshold ]]; then
        echo "WARNING: Disk usage is ${usage}% (threshold: ${threshold}%)"
        return 1
    else
        echo "Disk usage is acceptable: ${usage}%"
        return 0
    fi
}

# Case statement for clean multi-branch logic
process_service_action() {
    local action="$1"
    local service_name="${2:-nginx}"
    
    case "$action" in
        start)
            echo "Starting $service_name service..."
            systemctl start "$service_name"
            ;;
        stop)
            echo "Stopping $service_name service..."
            systemctl stop "$service_name"
            ;;
        restart)
            echo "Restarting $service_name service..."
            systemctl restart "$service_name"
            ;;
        status)
            echo "Checking $service_name service status..."
            systemctl status "$service_name"
            ;;
        enable)
            echo "Enabling $service_name service..."
            systemctl enable "$service_name"
            ;;
        disable)
            echo "Disabling $service_name service..."
            systemctl disable "$service_name"
            ;;
        *)
            echo "Usage: $0 {start|stop|restart|status|enable|disable} [service_name]"
            echo "Available actions:"
            echo "  start    - Start the service"
            echo "  stop     - Stop the service" 
            echo "  restart  - Restart the service"
            echo "  status   - Show service status"
            echo "  enable   - Enable service at boot"
            echo "  disable  - Disable service at boot"
            return 1
            ;;
    esac
}

### Loop Constructs: for, while, until

# For loop - iterating over known values
echo "Processing configuration files:"
for config_file in /etc/nginx/conf.d/*.conf; do
    if [[ -f "$config_file" ]]; then
        echo "Found config: $(basename "$config_file")"
        # Validate configuration
        nginx -t -c "$config_file" 2>/dev/null && echo "  ✓ Valid" || echo "  ✗ Invalid"
    fi
done

# For loop with range
echo "Checking ports 80-85:"
for port in {80..85}; do
    if ss -tln | grep -q ":$port "; then
        echo "Port $port is in use"
    else
        echo "Port $port is available"  
    fi
done

# For loop with array
declare -a services=("nginx" "apache2" "mysql" "postgresql")
echo "Checking service status:"
for service in "${services[@]}"; do
    if systemctl is-active --quiet "$service"; then
        echo "✓ $service is running"
    else
        echo "✗ $service is not running"
    fi
done

# While loop - repeating until condition changes
echo "Waiting for service to start..."
counter=0
max_attempts=30
while ! systemctl is-active --quiet nginx && [[ $counter -lt $max_attempts ]]; do
    echo "Attempt $((counter + 1)): Service not ready, waiting..."
    sleep 2
    ((counter++))
done

if systemctl is-active --quiet nginx; then
    echo "Service started successfully!"
else
    echo "Service failed to start after $max_attempts attempts"
    exit 1
fi

# Until loop - running until condition becomes true
echo "Monitoring log file..."
until [[ -f "/var/log/myapp.log" ]]; do
    echo "Waiting for log file to be created..."
    sleep 1
done
echo "Log file found!"

# Reading file line by line
while IFS= read -r line; do
    echo "Processing: $line"
done < "/etc/hosts"
```

### Functions for Modular, Readable Code
```bash
#!/usr/bin/env bash
# Demonstrate function creation and usage

# Simple function definition
greet_user() {
    local username="$1"
    local time_of_day="${2:-day}"
    
    echo "Good $time_of_day, $username!"
}

# Function with return values
check_port() {
    local port="$1"
    local host="${2:-localhost}"
    
    if nc -z "$host" "$port" 2>/dev/null; then
        return 0  # Port is open
    else
        return 1  # Port is closed
    fi
}

# Function with multiple return types
get_system_info() {
    local info_type="$1"
    
    case "$info_type" in
        "hostname")
            hostname
            ;;
        "uptime")
            uptime -p
            ;;
        "load")
            uptime | awk -F'load average:' '{print $2}' | sed 's/^ *//'
            ;;
        "memory")
            free -h | awk '/^Mem:/ {print $3 "/" $2}'
            ;;
        "disk")
            df -h / | awk 'NR==2 {print $3 "/" $2 " (" $5 " used)"}'
            ;;
        *)
            echo "Unknown info type: $info_type"
            return 1
            ;;
    esac
}

# Advanced function with local variables
backup_directory() {
    local source_dir="$1"
    local backup_base="${2:-/backup}"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    local backup_name="backup_${timestamp}"
    local backup_path="$backup_base/$backup_name"
    
    # Validate source directory
    if [[ ! -d "$source_dir" ]]; then
        echo "Error: Source directory '$source_dir' does not exist"
        return 1
    fi
    
    # Create backup directory
    mkdir -p "$backup_base"
    
    # Perform backup
    echo "Creating backup of '$source_dir' to '$backup_path'"
    if tar -czf "${backup_path}.tar.gz" -C "$(dirname "$source_dir")" "$(basename "$source_dir")"; then
        echo "Backup completed successfully: ${backup_path}.tar.gz"
        return 0
    else
        echo "Backup failed"
        return 1
    fi
}

# Function usage examples
greet_user "Admin" "morning"
greet_user "User"

if check_port 80; then
    echo "Web server is running"
else
    echo "Web server is not accessible"
fi

echo "System hostname: $(get_system_info hostname)"
echo "System uptime: $(get_system_info uptime)"
echo "Memory usage: $(get_system_info memory)"
```

### Command-Line Option Parsing with getopts
```bash
#!/usr/bin/env bash
# Robust command-line option parsing

# Script configuration
SCRIPT_NAME="$(basename "$0")"
DEFAULT_LOG_LEVEL="info"
DEFAULT_OUTPUT_FILE="/tmp/output.log"

# Initialize variables
verbose=false
log_level="$DEFAULT_LOG_LEVEL"
output_file="$DEFAULT_OUTPUT_FILE"
config_file=""
dry_run=false

# Usage function
usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS] [ARGUMENTS]

A demonstration script for getopts command-line parsing.

OPTIONS:
    -h, --help              Show this help message and exit
    -v, --verbose           Enable verbose output
    -l, --log-level LEVEL   Set log level (debug|info|warn|error) [default: $DEFAULT_LOG_LEVEL]
    -o, --output FILE       Set output file [default: $DEFAULT_OUTPUT_FILE]
    -c, --config FILE       Specify configuration file
    -n, --dry-run           Show what would be done without executing
    -V, --version           Show version information

EXAMPLES:
    $SCRIPT_NAME -v -l debug -o /tmp/my-output.log
    $SCRIPT_NAME --config /etc/myapp.conf --dry-run
    $SCRIPT_NAME -vn -l warn

EOF
}

# Version function
version() {
    echo "$SCRIPT_NAME version 1.0.0"
}

# Parse command-line options
while getopts ":hvl:o:c:nV-:" opt; do
    case ${opt} in
        h )
            usage
            exit 0
            ;;
        v )
            verbose=true
            ;;
        l )
            log_level="$OPTARG"
            # Validate log level
            case "$log_level" in
                debug|info|warn|error) ;;
                *)
                    echo "Error: Invalid log level '$log_level'"
                    echo "Valid levels: debug, info, warn, error"
                    exit 1
                    ;;
            esac
            ;;
        o )
            output_file="$OPTARG"
            ;;
        c )
            config_file="$OPTARG"
            if [[ ! -f "$config_file" ]]; then
                echo "Error: Configuration file '$config_file' not found"
                exit 1
            fi
            ;;
        n )
            dry_run=true
            ;;
        V )
            version
            exit 0
            ;;
        - )
            # Handle long options
            case "${OPTARG}" in
                help )
                    usage
                    exit 0
                    ;;
                verbose )
                    verbose=true
                    ;;
                log-level )
                    log_level="${!OPTIND}"; OPTIND=$(( $OPTIND + 1 ))
                    ;;
                output )
                    output_file="${!OPTIND}"; OPTIND=$(( $OPTIND + 1 ))
                    ;;
                config )
                    config_file="${!OPTIND}"; OPTIND=$(( $OPTIND + 1 ))
                    ;;
                dry-run )
                    dry_run=true
                    ;;
                version )
                    version
                    exit 0
                    ;;
                * )
                    echo "Error: Unknown option --${OPTARG}"
                    usage
                    exit 1
                    ;;
            esac
            ;;
        \? )
            echo "Error: Unknown option -$OPTARG"
            usage
            exit 1
            ;;
        : )
            echo "Error: Option -$OPTARG requires an argument"
            usage
            exit 1
            ;;
    esac
done

# Shift processed options
shift $((OPTIND -1))

# Remaining arguments are now in $@
remaining_args=("$@")

# Display parsed options (for demonstration)
echo "=== Parsed Configuration ==="
echo "Verbose: $verbose"
echo "Log Level: $log_level"
echo "Output File: $output_file"
echo "Config File: ${config_file:-'(none)'}"
echo "Dry Run: $dry_run"
echo "Remaining Arguments: ${remaining_args[*]}"
echo

# Example of using the parsed options
if [[ "$verbose" == true ]]; then
    echo "Verbose mode enabled - showing detailed output"
fi

if [[ "$dry_run" == true ]]; then
    echo "DRY RUN MODE - No actual changes will be made"
fi

# Load configuration if specified
if [[ -n "$config_file" ]]; then
    echo "Loading configuration from: $config_file"
    # source "$config_file"  # Uncomment to actually load
fi
```

### Error Handling and Debugging
```bash
#!/usr/bin/env bash
# Comprehensive error handling and debugging

# Strict mode for better error handling
set -euo pipefail  # Exit on error, undefined vars, pipe failures

# Enable debugging when needed
# set -x  # Uncomment to trace execution

# Custom error handler
error_handler() {
    local line_number="$1"
    local command="$2"
    local error_code="$3"
    
    echo "ERROR occurred in script at:"
    echo "  Line: $line_number"
    echo "  Command: $command"
    echo "  Exit Code: $error_code"
    echo "  Function Call Stack:"
    
    # Print call stack
    local frame=0
    while [[ ${FUNCNAME[frame]} ]]; do
        echo "    [$frame] ${FUNCNAME[frame]}() in ${BASH_SOURCE[frame]} at line ${BASH_LINENO[frame-1]}"
        ((frame++))
    done
    
    cleanup_on_exit
    exit "$error_code"
}

# Cleanup function
cleanup_on_exit() {
    echo "Performing cleanup..."
    # Remove temporary files
    [[ -n "${temp_dir:-}" && -d "$temp_dir" ]] && rm -rf "$temp_dir"
    # Close file descriptors
    [[ -n "${log_fd:-}" ]] && exec {log_fd}>&-
    echo "Cleanup completed"
}

# Set error trap
trap 'error_handler ${LINENO} "$BASH_COMMAND" $?' ERR
trap cleanup_on_exit EXIT

# Logging functions
log_debug() { [[ "${LOG_LEVEL:-info}" == "debug" ]] && echo "DEBUG: $*" >&2; }
log_info() { echo "INFO: $*" >&2; }
log_warn() { echo "WARN: $*" >&2; }
log_error() { echo "ERROR: $*" >&2; }

# Safe command execution
safe_execute() {
    local cmd="$1"
    local description="${2:-Running command}"
    
    log_info "$description..."
    
    if ! eval "$cmd"; then
        log_error "Failed to execute: $cmd"
        return 1
    fi
    
    log_info "Successfully completed: $description"
}

# File operations with error checking
safe_read_file() {
    local file="$1"
    
    if [[ ! -f "$file" ]]; then
        log_error "File not found: $file"
        return 1
    fi
    
    if [[ ! -r "$file" ]]; then
        log_error "File not readable: $file"
        return 1
    fi
    
    cat "$file"
}

safe_write_file() {
    local file="$1"
    local content="$2"
    local backup="${3:-false}"
    
    # Create backup if requested
    if [[ "$backup" == true && -f "$file" ]]; then
        local backup_file="${file}.backup.$(date +%Y%m%d_%H%M%S)"
        log_info "Creating backup: $backup_file"
        cp "$file" "$backup_file"
    fi
    
    # Write content
    echo "$content" > "$file" || {
        log_error "Failed to write to file: $file"
        return 1
    }
    
    log_info "Successfully wrote to file: $file"
}

# Network operations with retry logic
check_connectivity() {
    local host="$1"
    local port="${2:-80}"
    local timeout="${3:-5}"
    local max_retries="${4:-3}"
    
    local retry=0
    while [[ $retry -lt $max_retries ]]; do
        if timeout "$timeout" nc -z "$host" "$port" 2>/dev/null; then
            log_info "Successfully connected to $host:$port"
            return 0
        fi
        
        ((retry++))
        log_warn "Connection attempt $retry failed for $host:$port"
        [[ $retry -lt $max_retries ]] && sleep 2
    done
    
    log_error "Failed to connect to $host:$port after $max_retries attempts"
    return 1
}

# Example usage of error handling
main() {
    local temp_dir
    temp_dir=$(mktemp -d)
    
    log_info "Starting script execution"
    log_debug "Temporary directory: $temp_dir"
    
    # Example operations that might fail
    safe_execute "echo 'Hello World' > '$temp_dir/test.txt'" "Creating test file"
    
    local content
    content=$(safe_read_file "$temp_dir/test.txt")
    log_info "File content: $content"
    
    check_connectivity "google.com" 80 5 2
    
    log_info "Script completed successfully"
}

# Run main function
main "$@"
```

## Exercises and Projects

### Exercise 1: System Information Script
Create a script that gathers and displays system information in a formatted report.

**Requirements:**
- Use functions for modular code
- Implement command-line options with getopts
- Include error handling
- Generate both console and file output

```bash
#!/usr/bin/env bash
# system_info.sh - System information gathering script

set -euo pipefail

# Script variables
SCRIPT_NAME="$(basename "$0")"
OUTPUT_FILE=""
VERBOSE=false
FORMAT="text"

usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS]

Generate a system information report.

OPTIONS:
    -h, --help      Show this help message
    -o, --output    Output file (default: stdout)
    -v, --verbose   Verbose output
    -f, --format    Output format (text|json) [default: text]

EXAMPLES:
    $SCRIPT_NAME -v -o system_report.txt
    $SCRIPT_NAME -f json -o system_info.json
EOF
}

# Your implementation here...
```

### Exercise 2: Log File Analyzer
Build a script that analyzes log files and generates statistics.

**Requirements:**
- Parse command-line arguments for log file path and date range
- Count different types of log entries (ERROR, WARN, INFO)
- Generate summary statistics
- Support multiple log formats

### Exercise 3: Backup Automation Script
Create an automated backup script with rotation.

**Requirements:**
- Backup specified directories
- Implement rotation (keep last N backups)
- Support compression options
- Email notifications on success/failure
- Configuration file support

### Project: Server Monitoring Dashboard
Develop a comprehensive server monitoring script that:

1. **System Metrics Collection:**
   - CPU usage and load averages
   - Memory utilization
   - Disk space and I/O statistics
   - Network interface statistics

2. **Service Monitoring:**
   - Check critical services status
   - Monitor specific ports
   - Validate configuration files

3. **Alert System:**
   - Threshold-based alerts
   - Multiple notification methods (email, Slack, etc.)
   - Alert suppression and escalation

4. **Reporting:**
   - Generate HTML reports
   - Historical data tracking
   - Performance trending

## Best Practices and Common Pitfalls

### Shell Scripting Best Practices

1. **Use Strict Mode:**
   ```bash
   set -euo pipefail  # Exit on error, undefined vars, pipe failures
   ```

2. **Quote Variables:**
   ```bash
   # Good
   echo "Hello $name"
   cp "$source" "$destination"
   
   # Bad
   echo Hello $name
   cp $source $destination
   ```

3. **Use Meaningful Variable Names:**
   ```bash
   # Good
   user_config_file="/etc/myapp/user.conf"
   max_retry_attempts=3
   
   # Bad
   f="/etc/myapp/user.conf"
   n=3
   ```

4. **Check Dependencies:**
   ```bash
   # Check if required commands exist
   command -v curl >/dev/null 2>&1 || {
       echo "Error: curl is required but not installed"
       exit 1
   }
   ```

5. **Use Functions for Reusable Code:**
   ```bash
   validate_file() {
       local file="$1"
       [[ -f "$file" && -r "$file" ]] || {
           echo "Error: File '$file' not found or not readable"
           return 1
       }
   }
   ```

### Common Pitfalls to Avoid

1. **Unquoted Variables:**
   ```bash
   # Problematic with spaces in filenames
   rm $file  # Bad
   rm "$file"  # Good
   ```

2. **Not Checking Exit Codes:**
   ```bash
   # Bad
   wget https://example.com/file.tar.gz
   tar -xzf file.tar.gz
   
   # Good
   if ! wget https://example.com/file.tar.gz; then
       echo "Download failed"
       exit 1
   fi
   ```

3. **Parsing ls Output:**
   ```bash
   # Bad
   for file in $(ls *.txt); do
       echo "$file"
   done
   
   # Good
   for file in *.txt; do
       [[ -f "$file" ]] || continue
       echo "$file"
   done
   ```

4. **Unsafe Temporary Files:**
   ```bash
   # Bad
   temp_file="/tmp/myapp_$$"
   
   # Good
   temp_file=$(mktemp)
   trap 'rm -f "$temp_file"' EXIT
   ```

## Advanced Topics

### Process Management and Job Control
```bash
# Background processes
long_running_task &
pid=$!

# Wait for specific process
wait $pid

# Process monitoring
if kill -0 $pid 2>/dev/null; then
    echo "Process $pid is running"
else
    echo "Process $pid is not running"
fi

# Job control
jobs                    # List jobs
fg %1                   # Bring job 1 to foreground
bg %2                   # Send job 2 to background
kill %1                 # Kill job 1
```

### Signal Handling
```bash
#!/usr/bin/env bash
# Signal handling example

cleanup() {
    echo "Received signal, cleaning up..."
    [[ -n "${temp_file:-}" ]] && rm -f "$temp_file"
    exit 0
}

# Trap signals
trap cleanup SIGINT SIGTERM

temp_file=$(mktemp)
echo "Working with temporary file: $temp_file"

# Simulate long-running process
while true; do
    echo "Working... (Press Ctrl+C to stop)"
    sleep 2
done
```

### Advanced Text Processing
```bash
# Complex pattern matching
process_log_entry() {
    local line="$1"
    
    # Extract timestamp, level, and message
    if [[ $line =~ ^([0-9-]+\ [0-9:]+)\ \[([A-Z]+)\]\ (.+)$ ]]; then
        local timestamp="${BASH_REMATCH[1]}"
        local level="${BASH_REMATCH[2]}"
        local message="${BASH_REMATCH[3]}"
        
        echo "Time: $timestamp, Level: $level, Message: $message"
    fi
}

# Process substitution
while IFS= read -r line; do
    process_log_entry "$line"
done < <(grep "ERROR\|WARN" /var/log/application.log)
```

## Summary

This module covered the essential aspects of shell scripting for Linux system administration:

- **Script Structure:** Proper shebang usage, comments, and organization
- **Variables and Expansion:** Advanced parameter expansion and substitution
- **Control Structures:** Conditional logic, loops, and case statements
- **Functions:** Modular, reusable code design
- **Command-Line Parsing:** Professional option handling with getopts
- **Error Handling:** Robust scripts with proper error management
- **Best Practices:** Industry-standard scripting conventions

### Key Takeaways:
1. Always use strict mode (`set -euo pipefail`) for production scripts
2. Quote variables and check exit codes consistently
3. Implement proper error handling and cleanup procedures
4. Use functions to create modular, maintainable code
5. Follow established naming conventions and documentation practices

### Next Steps:
- Practice with the provided exercises and projects
- Study existing system scripts in `/usr/local/bin` and `/etc/init.d`
- Explore advanced topics like process management and signal handling
- Consider learning additional tools like `awk`, `sed`, and `jq` for text processing

Shell scripting is a powerful tool for automation and system administration. With these fundamentals, you can create robust, maintainable scripts that enhance your Linux environment's efficiency and reliability.
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
