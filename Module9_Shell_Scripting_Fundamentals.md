# Module 9: Shell Scripting Fundamentals

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics Covered](#topics-covered)
  - [9.1 Shell Scripting Foundations](#91-shell-scripting-foundations)
  - [9.2 Variables and Parameter Management](#92-variables-and-parameter-management)
  - [9.3 Control Structures and Flow Control](#93-control-structures-and-flow-control)
  - [9.4 Functions and Modular Programming](#94-functions-and-modular-programming)
  - [9.5 Advanced InputOutput Operations](#95-advanced-inputoutput-operations)
  - [9.6 Error Handling and Debugging](#96-error-handling-and-debugging)
  - [9.7 System Integration and Automation](#97-system-integration-and-automation)
  - [9.8 Enterprise Script Development](#98-enterprise-script-development)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Script Foundation and Best Practices](#script-foundation-and-best-practices)
  - [Variable and Parameter Techniques](#variable-and-parameter-techniques)
  - [Control Flow and Logic Implementation](#control-flow-and-logic-implementation)
  - [Functions for Modular, Readable Code](#functions-for-modular-readable-code)
  - [Command-Line Option Parsing with getopts](#command-line-option-parsing-with-getopts)
  - [Error Handling and Debugging](#error-handling-and-debugging)
- [Lab Exercises](#lab-exercises)
  - [Lab 1 Advanced Script Development](#lab-1-advanced-script-development)
  - [Lab 2 System Automation Framework](#lab-2-system-automation-framework)
  - [Lab 3 Enterprise Monitoring Solutions](#lab-3-enterprise-monitoring-solutions)
  - [Lab 4 Database Management Automation](#lab-4-database-management-automation)
  - [Lab 5 Infrastructure Orchestration](#lab-5-infrastructure-orchestration)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview

This module provides comprehensive coverage of shell scripting for enterprise Linux environments, from fundamental concepts to advanced automation frameworks. Students will master bash scripting techniques, create robust system administration tools, and develop enterprise-grade automation solutions for production infrastructure management.

**Module Focus Areas:**
- Professional shell script development with security and error handling
- Advanced parameter processing and configuration management
- Complex control structures and algorithmic programming
- Modular function libraries and reusable code frameworks
- System integration, service orchestration, and infrastructure automation
- Enterprise monitoring, alerting, and incident response automation
- Database management, backup automation, and disaster recovery scripts
- Performance optimization and script security best practices

## Learning Objectives

By the end of this module, you will be able to:

1. **Master Script Foundations**: Create professional shell scripts with proper structure, security, and error handling
2. **Implement Advanced Logic**: Design complex control structures, algorithms, and data processing workflows
3. **Develop Modular Code**: Build reusable function libraries and configurable automation frameworks
4. **Create System Automation**: Automate system administration tasks with enterprise-grade reliability
5. **Design Monitoring Solutions**: Implement comprehensive monitoring, alerting, and incident response systems
6. **Build Database Tools**: Create database management, backup, and recovery automation scripts
7. **Optimize Performance**: Write efficient, secure, and maintainable shell scripts for production environments
8. **Integrate Systems**: Develop orchestration scripts for complex infrastructure management workflows

## Topics Covered

### 9.1 Shell Scripting Foundations
- Script structure, shebang lines, and execution environments
- Variables, arrays, and data types in bash
- Parameter expansion, substitution, and string manipulation
- Input/output redirection and pipe programming
- Script permissions, security considerations, and best practices
- Environment setup and configuration management

### 9.2 Variables and Parameter Management
- Advanced variable techniques and scope management
- Command-line argument processing with getopts and manual parsing
- Configuration file parsing and environment variable handling
- Array manipulation and associative arrays
- Dynamic variable creation and indirect references
- Parameter validation and sanitization

### 9.3 Control Structures and Flow Control
- Conditional statements and complex boolean logic
- Case statements and pattern matching
- Loop constructs: for, while, until, and select
- Break and continue statements for flow control
- Signal handling and trap mechanisms
- Parallel processing and background jobs

### 9.4 Functions and Modular Programming
- Function definition, scope, and parameter passing
- Return values and exit codes
- Library creation and source management
- Recursive functions and advanced algorithms
- Function testing and debugging techniques
- Code organization and maintainability

### 9.5 Advanced InputOutput Operations
- File processing and stream manipulation
- Network operations and API interactions
- Database connectivity and query execution
- Log parsing and data extraction
- Report generation and formatting
- Binary file handling and encoding

### 9.6 Error Handling and Debugging
- Comprehensive error detection and handling strategies
- Debugging techniques and troubleshooting methods
- Logging and audit trail implementation
- Exception handling and recovery procedures
- Script testing and validation frameworks
- Performance monitoring and optimization

### 9.7 System Integration and Automation
- Service management and process control
- System monitoring and health checks
- Backup and recovery automation
- Security scanning and compliance checking
- Package management and software deployment
- Network configuration and management

### 9.8 Enterprise Script Development
- Code quality standards and documentation
- Version control integration and deployment pipelines
- Security scanning and vulnerability assessment
- Performance testing and optimization
- Maintenance and support procedures
- Enterprise integration patterns

## Essential Command Reference

### Core Shell Scripting Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `bash` | Execute bash scripts | `bash script.sh` or `bash -x script.sh` |
| `source` / `.` | Execute script in current shell | `source config.sh` or `. ./functions.sh` |
| `chmod` | Set script permissions | `chmod +x script.sh` |
| `which` | Find command location | `which bash` |
| `type` | Display command type | `type -a function_name` |

### Variable and Parameter Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `declare` | Declare variables/arrays | `declare -a array_name` |
| `readonly` | Make variables read-only | `readonly VAR=value` |
| `unset` | Remove variables | `unset variable_name` |
| `export` | Export environment variables | `export PATH=$PATH:/new/path` |
| `env` | Display environment | `env | grep VAR` |

### Control Flow and Testing Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `test` / `[` | Conditional testing | `test -f file` or `[ -f file ]` |
| `[[` | Extended test operator | `[[ $var =~ regex ]]` |
| `expr` | Arithmetic expressions | `expr $a + $b` |
| `(( ))` | Arithmetic evaluation | `(( var++ ))` |
| `case` | Pattern matching | `case $var in pattern) ... ;;` |

### String and Array Manipulation
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `cut` | Extract fields from text | `cut -d: -f1 /etc/passwd` |
| `awk` | Text processing | `awk '{print $1}' file` |
| `sed` | Stream editor | `sed 's/old/new/g' file` |
| `grep` | Pattern searching | `grep -E "pattern" file` |
| `sort` | Sort lines | `sort -n file` |
| `tr` | Character translation | `tr '[:lower:]' '[:upper:]'` |

### File and Directory Operations
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `find` | Search files/directories | `find /path -name "*.sh"` |
| `xargs` | Execute commands on input | `find . -name "*.log" | xargs rm` |
| `basename` | Extract filename | `basename /path/to/file.txt` |
| `dirname` | Extract directory path | `dirname /path/to/file.txt` |
| `realpath` | Get absolute path | `realpath relative/path` |

### Process and Signal Management
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `ps` | Show processes | `ps aux | grep script` |
| `kill` | Send signals | `kill -TERM $PID` |
| `trap` | Handle signals | `trap 'cleanup' EXIT` |
| `nohup` | Run without hangup | `nohup long_script.sh &` |
| `jobs` | List background jobs | `jobs -l` |

### Debugging and Testing Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `set` | Set shell options | `set -euo pipefail` |
| `bash -x` | Debug mode | `bash -x script.sh` |
| `shellcheck` | Static analysis | `shellcheck script.sh` |
| `time` | Measure execution time | `time ./script.sh` |
| `strace` | System call tracing | `strace -f ./script.sh` |

**[Back to Top](#module9-shell-scripting-fundamentals)** ⬆️ | **[Main Index](README.md)** 📚

## Practical Examples

### Script Foundation and Best Practices

#### Professional Script Template
```bash
#!/usr/bin/env bash
# script_template.sh - Professional bash script template
# Description: Template for enterprise-grade shell scripts
# Author: System Administrator
# Version: 1.0
# Created: $(date +%Y-%m-%d)

# Strict error handling
set -euo pipefail

# Script configuration
readonly SCRIPT_NAME="$(basename "$0")"
readonly SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
readonly SCRIPT_VERSION="1.0"

# Default configuration
DEFAULT_CONFIG_FILE="/etc/${SCRIPT_NAME%.sh}/config.conf"
DEFAULT_LOG_LEVEL="INFO"
DEFAULT_DRY_RUN="false"

# Global variables
declare -g CONFIG_FILE="${DEFAULT_CONFIG_FILE}"
declare -g LOG_LEVEL="${DEFAULT_LOG_LEVEL}"
declare -g DRY_RUN="${DEFAULT_DRY_RUN}"
declare -g VERBOSE="false"

# Colors for output
readonly RED='\033[0;31m'
readonly GREEN='\033[0;32m'
readonly YELLOW='\033[1;33m'
readonly BLUE='\033[0;34m'
readonly NC='\033[0m' # No Color

# Function: Display usage information
usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS] [ARGUMENTS]

Description:
    Professional script template with enterprise features

Options:
    -c, --config FILE    Configuration file (default: $DEFAULT_CONFIG_FILE)
    -l, --log-level LVL  Log level: DEBUG, INFO, WARN, ERROR (default: $DEFAULT_LOG_LEVEL)
    -d, --dry-run        Show what would be done without executing
    -v, --verbose        Enable verbose output
    -h, --help           Display this help message
    -V, --version        Display version information

Examples:
    $SCRIPT_NAME --config /custom/config.conf
    $SCRIPT_NAME --dry-run --verbose
    $SCRIPT_NAME --log-level DEBUG

EOF
}

# Function: Display version information
version() {
    echo "$SCRIPT_NAME version $SCRIPT_VERSION"
}

# Function: Logging with levels
log() {
    local level="$1"
    shift
    local message="$*"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Check if we should log this level
    case "$LOG_LEVEL" in
        "DEBUG") levels="DEBUG INFO WARN ERROR" ;;
        "INFO")  levels="INFO WARN ERROR" ;;
        "WARN")  levels="WARN ERROR" ;;
        "ERROR") levels="ERROR" ;;
    esac
    
    if [[ " $levels " =~ " $level " ]]; then
        case "$level" in
            "DEBUG") echo -e "${BLUE}[$timestamp] DEBUG: $message${NC}" >&2 ;;
            "INFO")  echo -e "${GREEN}[$timestamp] INFO: $message${NC}" >&2 ;;
            "WARN")  echo -e "${YELLOW}[$timestamp] WARN: $message${NC}" >&2 ;;
            "ERROR") echo -e "${RED}[$timestamp] ERROR: $message${NC}" >&2 ;;
        esac
    fi
}

# Function: Cleanup on exit
cleanup() {
    local exit_code=$?
    log "INFO" "Script cleanup initiated"
    
    # Add cleanup tasks here
    # Remove temporary files, close connections, etc.
    
    if [[ $exit_code -eq 0 ]]; then
        log "INFO" "Script completed successfully"
    else
        log "ERROR" "Script failed with exit code: $exit_code"
    fi
    
    exit $exit_code
}

# Function: Validate prerequisites
validate_prerequisites() {
    log "DEBUG" "Validating prerequisites"
    
    # Check required commands
    local required_commands=("awk" "sed" "grep" "find")
    for cmd in "${required_commands[@]}"; do
        if ! command -v "$cmd" &> /dev/null; then
            log "ERROR" "Required command not found: $cmd"
            exit 1
        fi
    done
    
    # Check configuration file
    if [[ ! -f "$CONFIG_FILE" ]] && [[ "$CONFIG_FILE" != "$DEFAULT_CONFIG_FILE" ]]; then
        log "ERROR" "Configuration file not found: $CONFIG_FILE"
        exit 1
    fi
    
    # Validate log level
    case "$LOG_LEVEL" in
        "DEBUG"|"INFO"|"WARN"|"ERROR") ;;
        *) log "ERROR" "Invalid log level: $LOG_LEVEL"; exit 1 ;;
    esac
    
    log "DEBUG" "Prerequisites validation completed"
}

# Function: Load configuration
load_configuration() {
    if [[ -f "$CONFIG_FILE" ]]; then
        log "DEBUG" "Loading configuration from: $CONFIG_FILE"
        # Source configuration file safely
        if source "$CONFIG_FILE"; then
            log "INFO" "Configuration loaded successfully"
        else
            log "ERROR" "Failed to load configuration file"
            exit 1
        fi
    else
        log "DEBUG" "No configuration file found, using defaults"
    fi
}

# Function: Parse command line arguments
parse_arguments() {
    while [[ $# -gt 0 ]]; do
        case $1 in
            -c|--config)
                CONFIG_FILE="$2"
                shift 2
                ;;
            -l|--log-level)
                LOG_LEVEL="$2"
                shift 2
                ;;
            -d|--dry-run)
                DRY_RUN="true"
                shift
                ;;
            -v|--verbose)
                VERBOSE="true"
                shift
                ;;
            -h|--help)
                usage
                exit 0
                ;;
            -V|--version)
                version
                exit 0
                ;;
            -*)
                log "ERROR" "Unknown option: $1"
                usage
                exit 1
                ;;
            *)
                # Store positional arguments
                POSITIONAL_ARGS+=("$1")
                shift
                ;;
        esac
    done
}

# Function: Main execution logic
main() {
    log "INFO" "Starting $SCRIPT_NAME execution"
    
    # Your main script logic goes here
    if [[ "$DRY_RUN" == "true" ]]; then
        log "INFO" "DRY RUN MODE - No changes will be made"
    fi
    
    if [[ "$VERBOSE" == "true" ]]; then
        log "DEBUG" "Verbose mode enabled"
    fi
    
    # Example operations
    log "INFO" "Executing main functionality..."
    
    # Add your script logic here
    
    log "INFO" "Main execution completed successfully"
}

# Set up signal handlers
trap cleanup EXIT
trap 'log "ERROR" "Script interrupted"; exit 130' INT TERM

# Initialize positional arguments array
declare -a POSITIONAL_ARGS=()

# Parse command line arguments
parse_arguments "$@"

# Set remaining positional arguments
set -- "${POSITIONAL_ARGS[@]}"

# Load configuration and validate
load_configuration
validate_prerequisites

# Execute main logic
main "$@"
```
**Related Commands/Topics:** [Debugging and Testing Commands](#debugging-and-testing-commands) 🟥

#### Advanced Error Handling Framework
```bash
#!/usr/bin/env bash
# error_handling_framework.sh - Advanced error handling and recovery

# Strict error handling with custom error function
set -euo pipefail

# Error handling configuration
readonly ERROR_LOG="/var/log/script_errors.log"
readonly MAX_RETRIES=3
readonly RETRY_DELAY=5

# Error tracking
declare -g ERROR_COUNT=0
declare -A ERROR_HISTORY=()

# Function: Advanced error handler
error_handler() {
    local exit_code=$?
    local line_number=$1
    local bash_lineno=$2
    local last_command=$3
    local function_stack=("${FUNCNAME[@]}")
    
    ((ERROR_COUNT++))
    
    local error_id="ERR_$(date +%Y%m%d_%H%M%S)_$$"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Create detailed error report
    local error_report=$(cat << EOF
=== ERROR REPORT ===
Error ID: $error_id
Timestamp: $timestamp
Exit Code: $exit_code
Line Number: $line_number
Last Command: $last_command
Function Stack: ${function_stack[*]}
Script: $0
PID: $$
User: $(whoami)
Working Directory: $(pwd)
Environment: $(env | grep -E '^(PATH|HOME|USER)=' | tr '\n' ' ')
EOF
)
    
    # Log error
    echo "$error_report" >> "$ERROR_LOG"
    echo "$error_report" >&2
    
    # Store error in history
    ERROR_HISTORY["$error_id"]="$exit_code:$line_number:$last_command"
    
    # Attempt recovery based on error type
    case $exit_code in
        1)
            log "WARN" "General error detected, attempting recovery"
            attempt_recovery "$error_id" "$exit_code"
            ;;
        2)
            log "ERROR" "Syntax error detected, cannot recover"
            send_alert "CRITICAL" "Syntax error in script $0"
            ;;
        126)
            log "ERROR" "Permission denied, checking file permissions"
            check_permissions
            ;;
        127)
            log "ERROR" "Command not found, checking dependencies"
            check_dependencies
            ;;
        *)
            log "ERROR" "Unknown error code: $exit_code"
            ;;
    esac
}

# Function: Retry mechanism with exponential backoff
retry_with_backoff() {
    local max_attempts="$1"
    local delay="$2"
    local command="$3"
    shift 3
    local args=("$@")
    
    local attempt=1
    local current_delay="$delay"
    
    while [[ $attempt -le $max_attempts ]]; do
        log "DEBUG" "Attempt $attempt of $max_attempts: $command ${args[*]}"
        
        if "$command" "${args[@]}"; then
            log "INFO" "Command succeeded on attempt $attempt"
            return 0
        else
            local exit_code=$?
            log "WARN" "Command failed on attempt $attempt with exit code: $exit_code"
            
            if [[ $attempt -lt $max_attempts ]]; then
                log "INFO" "Waiting ${current_delay}s before retry..."
                sleep "$current_delay"
                # Exponential backoff
                current_delay=$((current_delay * 2))
            fi
        fi
        
        ((attempt++))
    done
    
    log "ERROR" "Command failed after $max_attempts attempts"
    return 1
}

# Function: Safe command execution
safe_execute() {
    local description="$1"
    local command="$2"
    shift 2
    local args=("$@")
    
    log "INFO" "Executing: $description"
    log "DEBUG" "Command: $command ${args[*]}"
    
    if [[ "$DRY_RUN" == "true" ]]; then
        log "INFO" "DRY RUN: Would execute: $command ${args[*]}"
        return 0
    fi
    
    # Execute with timeout and error handling
    if timeout 300 "$command" "${args[@]}"; then
        log "INFO" "Successfully completed: $description"
        return 0
    else
        local exit_code=$?
        log "ERROR" "Failed to execute: $description (exit code: $exit_code)"
        return $exit_code
    fi
}

# Function: Validate critical resources
validate_resources() {
    log "DEBUG" "Validating critical resources"
    
    # Check disk space
    local disk_usage=$(df / | awk 'NR==2 {print $5}' | sed 's/%//')
    if [[ $disk_usage -gt 90 ]]; then
        log "ERROR" "Disk usage critical: ${disk_usage}%"
        return 1
    fi
    
    # Check memory
    local mem_available=$(free | awk 'NR==2{printf "%.2f", $7/$2*100}')
    if (( $(echo "$mem_available < 10" | bc -l) )); then
        log "WARN" "Low memory available: ${mem_available}%"
    fi
    
    # Check load average
    local load_avg=$(uptime | awk -F'load average:' '{print $2}' | awk '{print $1}' | sed 's/,//')
    local cpu_count=$(nproc)
    if (( $(echo "$load_avg > $cpu_count * 2" | bc -l) )); then
        log "WARN" "High load average: $load_avg (CPUs: $cpu_count)"
    fi
    
    log "DEBUG" "Resource validation completed"
    return 0
}

# Function: Send alerts
send_alert() {
    local severity="$1"
    local message="$2"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Log the alert
    log "$severity" "ALERT: $message"
    
    # Send email if configured
    if [[ -n "${ALERT_EMAIL:-}" ]]; then
        echo "[$timestamp] $severity: $message" | \
            mail -s "Script Alert: $SCRIPT_NAME" "$ALERT_EMAIL"
    fi
    
    # Send to syslog
    logger -p user.err "SCRIPT_ALERT: $SCRIPT_NAME - $severity: $message"
    
    # Send to monitoring system (if configured)
    if [[ -n "${MONITORING_WEBHOOK:-}" ]]; then
        curl -X POST -H "Content-Type: application/json" \
             -d "{\"severity\":\"$severity\",\"message\":\"$message\",\"script\":\"$SCRIPT_NAME\"}" \
             "$MONITORING_WEBHOOK" || true
    fi
}

# Set up error handling
trap 'error_handler $LINENO $BASH_LINENO "$BASH_COMMAND"' ERR

# Export functions for use in subshells
export -f log safe_execute retry_with_backoff validate_resources send_alert

log "INFO" "Error handling framework initialized"
```

### Variable and Parameter Techniques

#### Advanced Variable Management
```bash
#!/usr/bin/env bash
# advanced_variables.sh - Comprehensive variable handling techniques

# Different types of variable declarations
declare -r READONLY_VAR="Cannot be modified"    # Read-only variable
declare -i INTEGER_VAR=42                       # Integer variable
declare -a INDEXED_ARRAY=()                     # Indexed array
declare -A ASSOCIATIVE_ARRAY=()                 # Associative array
declare -x EXPORTED_VAR="Available to subshells" # Exported variable

# Array manipulation examples
populate_arrays() {
    # Indexed array operations
    INDEXED_ARRAY=("apple" "banana" "cherry" "date")
    INDEXED_ARRAY+=("elderberry")  # Append element
    
    # Associative array operations
    ASSOCIATIVE_ARRAY[name]="John Doe"
    ASSOCIATIVE_ARRAY[age]=30
    ASSOCIATIVE_ARRAY[department]="Engineering"
    ASSOCIATIVE_ARRAY[location]="Remote"
    
    # Dynamic array population
    local files=($(find /etc -maxdepth 1 -name "*.conf" 2>/dev/null))
    echo "Found ${#files[@]} configuration files"
}

# Advanced parameter expansion techniques
parameter_expansion_demo() {
    local input_string="  Hello, World!  "
    local filename="/path/to/document.pdf"
    local version="1.2.3-beta"
    
    # String manipulation
    echo "=== String Manipulation ==="
    echo "Original: '$input_string'"
    echo "Trimmed: '${input_string// /}'"                    # Remove all spaces
    echo "Left trim: '${input_string#"${input_string%%[![:space:]]*}"}'" # Remove leading whitespace
    echo "Right trim: '${input_string%"${input_string##*[![:space:]]}"}'" # Remove trailing whitespace
    echo
    
    # Path manipulation
    echo "=== Path Manipulation ==="
    echo "Full path: $filename"
    echo "Directory: ${filename%/*}"           # Extract directory
    echo "Filename: ${filename##*/}"           # Extract filename
    echo "Extension: ${filename##*.}"          # Extract extension
    echo "Basename: ${filename%.*}"            # Remove extension
    echo
    
    # Version manipulation
    echo "=== Version Parsing ==="
    echo "Full version: $version"
    echo "Major: ${version%%.*}"               # Extract major version
    echo "Minor: ${version#*.}"; echo "Minor: ${version#*.}" | cut -d. -f1
    echo "Patch: ${version%%-*}"               # Remove pre-release suffix
    echo
    
    # Default value handling
    local undefined_var
    echo "=== Default Values ==="
    echo "Undefined with default: ${undefined_var:-'default_value'}"
    echo "Undefined with assignment: ${undefined_var:='assigned_default'}"
    echo "Now defined: $undefined_var"
    echo "Length check: ${#undefined_var}"
}

# Configuration file parsing
parse_config_file() {
    local config_file="$1"
    local -A config=()
    
    if [[ ! -f "$config_file" ]]; then
        log "ERROR" "Configuration file not found: $config_file"
        return 1
    fi
    
    # Parse key=value pairs, ignoring comments and empty lines
    while IFS='=' read -r key value; do
        # Skip comments and empty lines
        [[ $key =~ ^[[:space:]]*# ]] && continue
        [[ -z $key ]] && continue
        
        # Clean up key and value
        key=$(echo "$key" | sed 's/^[[:space:]]*//' | sed 's/[[:space:]]*$//')
        value=$(echo "$value" | sed 's/^[[:space:]]*//' | sed 's/[[:space:]]*$//')
        
        # Remove quotes from value if present
        value="${value%\"}"
        value="${value#\"}"
        value="${value%\'}"
        value="${value#\'}"
        
        config["$key"]="$value"
        
    done < "$config_file"
    
    # Display parsed configuration
    echo "=== Parsed Configuration ==="
    for key in "${!config[@]}"; do
        echo "$key = ${config[$key]}"
    done
}

# Variable validation and sanitization
validate_and_sanitize() {
    local input="$1"
    local type="$2"
    
    case "$type" in
        "email")
            if [[ $input =~ ^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$ ]]; then
                echo "Valid email: $input"
                return 0
            else
                echo "Invalid email format: $input"
                return 1
            fi
            ;;
        "ip")
            if [[ $input =~ ^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$ ]]; then
                # Validate IP ranges
                IFS='.' read -ra ADDR <<< "$input"
                for i in "${ADDR[@]}"; do
                    if [[ $i -gt 255 ]]; then
                        echo "Invalid IP address: $input"
                        return 1
                    fi
                done
                echo "Valid IP address: $input"
                return 0
            else
                echo "Invalid IP format: $input"
                return 1
            fi
            ;;
        "path")
            # Sanitize path by removing dangerous characters
            local sanitized=$(echo "$input" | sed 's/[^a-zA-Z0-9/_.-]//g')
            echo "Sanitized path: $sanitized"
            ;;
        "alphanumeric")
            # Keep only alphanumeric characters
            local sanitized=$(echo "$input" | sed 's/[^a-zA-Z0-9]//g')
            echo "Sanitized string: $sanitized"
            ;;
        *)
            echo "Unknown validation type: $type"
            return 1
            ;;
    esac
}
```
**Related Commands/Topics:** [Control Flow and Testing Commands](#control-flow-and-testing-commands) 🟧
**Related Commands/Topics:** [Variable and Parameter Commands](#variable-and-parameter-commands) 🟦

### Control Flow and Logic Implementation

#### Advanced Control Structures
```bash
#!/usr/bin/env bash
# advanced_control_flow.sh - Comprehensive control flow examples

# Advanced conditional logic with multiple conditions
advanced_conditionals() {
    local age="$1"
    local status="$2"
    local department="$3"
    
    echo "=== Advanced Conditional Logic ==="
    
    # Complex boolean logic
    if [[ $age -ge 18 && $age -le 65 ]] && \
       [[ "$status" == "active" || "$status" == "pending" ]] && \
       [[ "$department" =~ ^(IT|Engineering|DevOps)$ ]]; then
        echo "✓ Eligible for technical role"
    elif [[ $age -gt 65 ]] && [[ "$status" == "active" ]]; then
        echo "✓ Eligible for senior consultant role"
    elif [[ $age -lt 18 ]]; then
        echo "✗ Too young for employment"
    else
        echo "✗ Does not meet criteria"
    fi
    
    # Pattern matching with case statement
    case "$department" in
        "IT"|"Information Technology")
            echo "Department: Information Technology"
            ;;
        "Engineering"|"DevOps"|"SRE")
            echo "Department: Technical Operations"
            ;;
        "HR"|"Human Resources")
            echo "Department: Human Resources"
            ;;
        *)
            echo "Department: Other ($department)"
            ;;
    esac
}

# Advanced loop constructs and flow control
advanced_loops() {
    echo "=== Advanced Loop Constructs ==="
    
    # Loop with continue and break
    echo "Processing numbers 1-20:"
    for i in {1..20}; do
        # Skip even numbers
        if (( i % 2 == 0 )); then
            continue
        fi
        
        # Stop at 15
        if (( i > 15 )); then
            echo "Stopping at $i"
            break
        fi
        
        echo "Processing odd number: $i"
    done
    
    echo
    
    # While loop with multiple conditions
    local counter=1
    local max_attempts=5
    local success=false
    
    while [[ $counter -le $max_attempts ]] && [[ $success == false ]]; do
        echo "Attempt $counter of $max_attempts"
        
        # Simulate random success (50% chance)
        if (( RANDOM % 2 == 0 )); then
            echo "✓ Operation successful!"
            success=true
        else
            echo "✗ Operation failed, retrying..."
            sleep 1
        fi
        
        ((counter++))
    done
    
    if [[ $success == false ]]; then
        echo "Failed after $max_attempts attempts"
    fi
}

# Parallel processing with background jobs
parallel_processing() {
    echo "=== Parallel Processing Demo ==="
    
    # Function to simulate work
    work_task() {
        local task_id="$1"
        local duration="$2"
        
        echo "Starting task $task_id (duration: ${duration}s)"
        sleep "$duration"
        echo "✓ Task $task_id completed"
        
        return 0
    }
    
    # Start multiple background jobs
    local pids=()
    local start_time=$(date +%s)
    
    for i in {1..5}; do
        local duration=$((RANDOM % 5 + 1))
        work_task "$i" "$duration" &
        pids+=($!)
    done
    
    echo "Started ${#pids[@]} background tasks"
    echo "PIDs: ${pids[*]}"
    
    # Wait for all jobs to complete
    local completed=0
    for pid in "${pids[@]}"; do
        if wait "$pid"; then
            ((completed++))
            echo "Job $pid completed successfully ($completed/${#pids[@]})"
        else
            echo "Job $pid failed"
        fi
    done
    
    local end_time=$(date +%s)
    local total_time=$((end_time - start_time))
    
    echo "All jobs completed in ${total_time} seconds"
}
```
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

**Related Commands/Topics:** [Core Shell Scripting Commands](#core-shell-scripting-commands), [Variable and Parameter Commands](#variable-and-parameter-commands) 🟩🟦

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
**Related Commands/Topics:** [Variable and Parameter Commands](#variable-and-parameter-commands), [Core Shell Scripting Commands](#core-shell-scripting-commands) 🟦🟩

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

**[⬆️ Back to Top](#module9-shell-scripting-fundamentals)** | **[�� Main Index](README.md)**

## Lab Exercises

### Lab 1: Advanced Script Development

**Objective**: Develop enterprise-grade shell scripts with comprehensive error handling and logging

**Tasks**:
1. Create a multi-function script library with advanced error handling
2. Implement configuration file parsing and validation
3. Build a command-line interface with both short and long options
4. Add comprehensive logging with multiple levels and output destinations
5. Implement signal handling and cleanup procedures

**Deliverables**:
- Complete script library with modular functions
- Configuration system with validation and defaults
- Professional command-line interface with help documentation
- Comprehensive test suite with error scenarios

**Assessment Criteria**:
- Code quality and organization (25%)
- Error handling and robustness (25%)
- User interface design (25%)
- Documentation and testing (25%)

### Lab 2: System Automation Framework

**Objective**: Build a comprehensive system automation framework for infrastructure management

**Tasks**:
1. Develop server health monitoring with automated alerts
2. Create user management automation with security validation
3. Implement backup and recovery automation with verification
4. Build package management and security update automation
5. Design service management and deployment automation

**Deliverables**:
- Complete automation framework with multiple modules
- Health monitoring system with alerting capabilities
- Backup and recovery procedures with testing validation
- Security automation with compliance reporting

**Assessment Criteria**:
- Automation coverage and reliability (30%)
- Security implementation (25%)
- Error handling and recovery (25%)
- Performance and optimization (20%)

### Lab 3: Enterprise Monitoring Solutions

**Objective**: Create enterprise monitoring and alerting systems with comprehensive reporting

**Tasks**:
1. Build system resource monitoring with trend analysis
2. Implement application performance monitoring and alerting
3. Create log analysis and security event detection
4. Design custom metrics collection and visualization
5. Develop incident response and escalation automation

**Deliverables**:
- Complete monitoring framework with dashboards
- Automated alerting system with escalation procedures
- Security monitoring with threat detection capabilities
- Performance reporting and capacity planning tools

**Assessment Criteria**:
- Monitoring comprehensiveness (30%)
- Alert accuracy and relevance (25%)
- Security monitoring effectiveness (25%)
- Reporting and visualization (20%)

### Lab 4: Database Management Automation

**Objective**: Develop comprehensive database management and backup automation

**Tasks**:
1. Create database backup automation with encryption and compression
2. Implement database health monitoring and performance analysis
3. Build user management and security auditing for databases
4. Design disaster recovery and point-in-time recovery procedures
5. Create automated database maintenance and optimization scripts

**Deliverables**:
- Complete database management automation suite
- Backup and recovery procedures with testing validation
- Security auditing and compliance reporting
- Performance monitoring and optimization tools

**Assessment Criteria**:
- Backup reliability and recovery testing (30%)
- Security implementation and auditing (25%)
- Performance monitoring and optimization (25%)
- Documentation and procedures (20%)

### Lab 5: Infrastructure Orchestration

**Objective**: Build infrastructure orchestration and deployment automation

**Tasks**:
1. Create multi-server deployment and configuration management
2. Implement load balancer and service discovery automation
3. Build container orchestration and management scripts
4. Design network configuration and security automation
5. Create infrastructure testing and validation frameworks

**Deliverables**:
- Complete infrastructure orchestration platform
- Multi-environment deployment procedures
- Service discovery and load balancing automation
- Infrastructure testing and validation tools

**Assessment Criteria**:
- Orchestration complexity and reliability (30%)
- Multi-environment support (25%)
- Network and security automation (25%)
- Testing and validation coverage (20%)

## Best Practices

### Script Development Standards
- **Structure and Organization**: Use consistent script structure with clear sections for configuration, functions, and main logic
- **Error Handling**: Implement comprehensive error handling with set -euo pipefail and custom error functions
- **Logging**: Provide multiple logging levels with timestamps and structured output
- **Documentation**: Include comprehensive inline comments and usage documentation
- **Testing**: Develop test suites for all critical functions and error scenarios
- **Security**: Validate all inputs, sanitize data, and follow security best practices

### Performance Optimization
- **Efficient Algorithms**: Use appropriate data structures and algorithms for performance
- **Resource Management**: Monitor and optimize memory and CPU usage
- **Parallel Processing**: Leverage background jobs and parallel execution where appropriate
- **Caching**: Implement caching for expensive operations and repeated calculations
- **Profiling**: Use timing and profiling tools to identify bottlenecks
- **Optimization**: Minimize external command calls and use bash built-ins when possible

### Security Considerations
- **Input Validation**: Validate and sanitize all user inputs and external data
- **Privilege Management**: Run with minimal required privileges and escalate only when necessary
- **Data Protection**: Encrypt sensitive data and secure temporary files
- **Audit Trails**: Maintain comprehensive logs for security auditing
- **Access Control**: Implement proper file permissions and access controls
- **Vulnerability Management**: Regular security reviews and dependency updates

## Troubleshooting

### Common Scripting Issues

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| **Variable Expansion Problems** | Unexpected values or empty variables | Use proper quoting and parameter expansion |
| **Permission Errors** | "Permission denied" errors | Check file permissions and user privileges |
| **Path Issues** | "Command not found" errors | Verify PATH and use full paths for commands |
| **Array Handling** | Index errors or unexpected behavior | Properly declare and reference arrays |
| **Signal Handling** | Scripts not cleaning up properly | Implement proper trap handlers |

### Debugging Techniques
```bash
# Enable debug mode
set -x

# Debug specific sections
{
    set -x
    # Debug this section
    complex_function
    set +x
} 2>/tmp/debug.log

# Conditional debugging
if [[ "${DEBUG:-}" == "true" ]]; then
    set -x
fi

# Function tracing
PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]:+${FUNCNAME[0]}():} '
```

### Performance Analysis
```bash
# Timing script execution
time ./script.sh

# Profiling with detailed timing
TIMEFORMAT='%3R seconds'
time {
    # Operations to time
}

# Memory usage monitoring
/usr/bin/time -v ./script.sh

# System call tracing
strace -c ./script.sh
```

**[⬆️ Back to Top](#module9-shell-scripting-fundamentals)** | **[📚 Main Index](README.md)**

## Assessment Criteria

### Technical Proficiency (40%)
- **Script Architecture**: Well-organized, modular code with clear separation of concerns
- **Error Handling**: Comprehensive error detection, handling, and recovery procedures
- **Performance**: Efficient algorithms and optimized resource utilization
- **Security**: Proper input validation, security controls, and vulnerability management

### Problem-Solving Skills (30%)
- **Requirements Analysis**: Understanding and translating requirements into functional scripts
- **Algorithm Design**: Developing efficient solutions for complex automation challenges
- **Debugging Proficiency**: Systematic approach to identifying and resolving issues
- **Integration Capabilities**: Successful integration with existing systems and workflows

### Code Quality and Maintainability (20%)
- **Documentation**: Clear, comprehensive documentation and inline comments
- **Code Standards**: Adherence to coding standards and best practices
- **Modularity**: Reusable functions and libraries with clear interfaces
- **Testing**: Comprehensive test coverage and validation procedures

### Innovation and Automation (10%)
- **Creative Solutions**: Innovative approaches to automation challenges
- **Process Improvement**: Demonstrating efficiency gains through automation
- **Advanced Techniques**: Use of advanced shell scripting features and techniques
- **Continuous Improvement**: Ongoing optimization and enhancement of automation solutions

## Next Steps

### Advanced Scripting Topics
- **Advanced Text Processing**: awk, sed, and regex mastery for complex data manipulation
- **Network Programming**: Socket programming and network automation scripts
- **API Integration**: REST API consumption and webhook automation
- **Database Scripting**: Advanced database automation and data processing
- **Container Automation**: Docker and Kubernetes automation scripts

### Professional Development
- **DevOps Integration**: CI/CD pipeline scripting and infrastructure as code
- **Monitoring Integration**: Advanced monitoring and observability automation
- **Security Automation**: Security scanning, compliance, and incident response automation
- **Cloud Automation**: Multi-cloud automation and infrastructure management
- **Configuration Management**: Integration with Ansible, Puppet, and other CM tools

### Integration with Module 10
The next module covers Storage and Filesystem Management, which will utilize the shell scripting skills developed here for automating storage operations, filesystem monitoring, and backup procedures.

---

**Module 9 Complete**: You have successfully mastered enterprise-grade shell scripting fundamentals, from basic script development to advanced automation frameworks. These skills provide the foundation for all Linux system administration automation and infrastructure management tasks.
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

### Exercise 4: PostgreSQL Database Backup Script
Develop a comprehensive PostgreSQL database backup script with advanced features.

**Requirements:**
- Support multiple databases and backup types
- Implement backup rotation and compression
- Include restoration capabilities
- Add monitoring and alerting
- Configuration file support with encryption options

**Complete Implementation:**
```bash
#!/usr/bin/env bash
# postgresql_backup.sh - Comprehensive PostgreSQL backup script
# Author: System Administrator
# Purpose: Automated PostgreSQL database backup with rotation and monitoring

set -euo pipefail

# Script configuration
readonly SCRIPT_NAME="$(basename "$0")"
readonly CONFIG_FILE="/etc/postgresql-backup/config.conf"
readonly LOG_FILE="/var/log/postgresql-backup.log"
readonly LOCK_FILE="/var/run/postgresql-backup.lock"

# Default configuration (can be overridden by config file)
BACKUP_DIR="/backup/postgresql"
BACKUP_RETENTION_DAYS=30
BACKUP_RETENTION_COUNT=7
PG_HOST="localhost"
PG_PORT="5432"
PG_USER="postgres"
DATABASES="all"  # "all" or space-separated list
BACKUP_TYPE="full"  # full, schema, data
COMPRESSION="gzip"  # gzip, bzip2, xz, none
ENCRYPTION_ENABLED="false"
ENCRYPTION_KEY_FILE=""
MONITORING_ENABLED="true"
EMAIL_ALERTS="admin@example.com"
SLACK_WEBHOOK_URL=""
S3_BACKUP_ENABLED="false"
S3_BUCKET=""
PARALLEL_JOBS=1

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
log_debug() { [[ "${DEBUG:-false}" == true ]] && log "DEBUG" "$@"; }

# Load configuration file
load_config() {
    if [[ -f "$CONFIG_FILE" ]]; then
        log_info "Loading configuration from $CONFIG_FILE"
        # shellcheck source=/dev/null
        source "$CONFIG_FILE"
    else
        log_warn "Configuration file not found: $CONFIG_FILE, using defaults"
    fi
}

# Usage and help
usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS] [COMMAND]

PostgreSQL Database Backup Script with advanced features.

COMMANDS:
    backup          Perform database backup (default)
    restore         Restore from backup
    list            List available backups
    cleanup         Clean old backups
    test            Test backup configuration
    config          Show current configuration

OPTIONS:
    -h, --help              Show this help message
    -c, --config FILE       Use custom configuration file
    -d, --database DB       Backup specific database(s)
    -t, --type TYPE         Backup type (full|schema|data)
    -o, --output DIR        Output directory
    -v, --verbose           Verbose output
    -n, --dry-run           Show what would be done
    --compression TYPE      Compression (gzip|bzip2|xz|none)
    --encrypt              Enable encryption
    --no-monitoring        Disable monitoring
    --parallel JOBS        Number of parallel jobs

EXAMPLES:
    $SCRIPT_NAME backup
    $SCRIPT_NAME -d "mydb1 mydb2" -t schema backup
    $SCRIPT_NAME --compression bzip2 --encrypt backup
    $SCRIPT_NAME restore /backup/postgresql/mydb_20250802_120000.sql.gz
    $SCRIPT_NAME list
    $SCRIPT_NAME cleanup

CONFIG FILE EXAMPLE:
    # /etc/postgresql-backup/config.conf
    BACKUP_DIR="/backup/postgresql"
    PG_HOST="localhost"
    PG_USER="backup_user"
    DATABASES="mydb1 mydb2 mydb3"
    BACKUP_TYPE="full"
    COMPRESSION="gzip"
    ENCRYPTION_ENABLED="true"
    ENCRYPTION_KEY_FILE="/etc/postgresql-backup/backup.key"
    EMAIL_ALERTS="dba@company.com"

EOF
}

# Check prerequisites
check_prerequisites() {
    local missing_deps=()
    
    # Check required commands
    local required_commands=("pg_dump" "pg_dumpall" "psql" "date")
    for cmd in "${required_commands[@]}"; do
        if ! command -v "$cmd" >/dev/null 2>&1; then
            missing_deps+=("$cmd")
        fi
    done
    
    # Check compression tools
    case "$COMPRESSION" in
        gzip) command -v gzip >/dev/null 2>&1 || missing_deps+=("gzip") ;;
        bzip2) command -v bzip2 >/dev/null 2>&1 || missing_deps+=("bzip2") ;;
        xz) command -v xz >/dev/null 2>&1 || missing_deps+=("xz") ;;
    esac
    
    # Check encryption tools
    if [[ "$ENCRYPTION_ENABLED" == "true" ]]; then
        command -v gpg >/dev/null 2>&1 || missing_deps+=("gpg")
    fi
    
    if [[ ${#missing_deps[@]} -gt 0 ]]; then
        log_error "Missing required dependencies: ${missing_deps[*]}"
        log_error "Please install missing packages and try again"
        exit 1
    fi
}

# Test database connectivity
test_connection() {
    log_info "Testing PostgreSQL connection..."
    
    local conn_params=()
    [[ -n "$PG_HOST" ]] && conn_params+=("-h" "$PG_HOST")
    [[ -n "$PG_PORT" ]] && conn_params+=("-p" "$PG_PORT")
    [[ -n "$PG_USER" ]] && conn_params+=("-U" "$PG_USER")
    
    if ! psql "${conn_params[@]}" -d postgres -c "SELECT version();" >/dev/null 2>&1; then
        log_error "Failed to connect to PostgreSQL server"
        log_error "Check connection parameters: host=$PG_HOST, port=$PG_PORT, user=$PG_USER"
        return 1
    fi
    
    log_info "PostgreSQL connection successful"
    return 0
}

# Get list of databases
get_database_list() {
    local conn_params=()
    [[ -n "$PG_HOST" ]] && conn_params+=("-h" "$PG_HOST")
    [[ -n "$PG_PORT" ]] && conn_params+=("-p" "$PG_PORT")
    [[ -n "$PG_USER" ]] && conn_params+=("-U" "$PG_USER")
    
    if [[ "$DATABASES" == "all" ]]; then
        psql "${conn_params[@]}" -d postgres -t -c "SELECT datname FROM pg_database WHERE NOT datistemplate AND datname != 'postgres';" | sed 's/^[ \t]*//' | grep -v '^$'
    else
        echo "$DATABASES" | tr ' ' '\n'
    fi
}

# Create backup filename
create_backup_filename() {
    local database="$1"
    local timestamp="$2"
    local backup_type="$3"
    
    local filename="${database}_${backup_type}_${timestamp}"
    
    case "$COMPRESSION" in
        gzip) filename+=".sql.gz" ;;
        bzip2) filename+=".sql.bz2" ;;
        xz) filename+=".sql.xz" ;;
        none) filename+=".sql" ;;
    esac
    
    [[ "$ENCRYPTION_ENABLED" == "true" ]] && filename+=".gpg"
    
    echo "$filename"
}

# Compress backup file
compress_backup() {
    local input_file="$1"
    local output_file="$2"
    
    case "$COMPRESSION" in
        gzip)
            gzip -c "$input_file" > "$output_file"
            ;;
        bzip2)
            bzip2 -c "$input_file" > "$output_file"
            ;;
        xz)
            xz -c "$input_file" > "$output_file"
            ;;
        none)
            cp "$input_file" "$output_file"
            ;;
    esac
}

# Encrypt backup file
encrypt_backup() {
    local input_file="$1"
    local output_file="$2"
    
    if [[ "$ENCRYPTION_ENABLED" == "true" ]]; then
        if [[ -f "$ENCRYPTION_KEY_FILE" ]]; then
            gpg --batch --yes --cipher-algo AES256 --compress-algo 1 \
                --symmetric --passphrase-file "$ENCRYPTION_KEY_FILE" \
                --output "$output_file" "$input_file"
        else
            log_error "Encryption key file not found: $ENCRYPTION_KEY_FILE"
            return 1
        fi
    else
        cp "$input_file" "$output_file"
    fi
}

# Backup single database
backup_database() {
    local database="$1"
    local timestamp="$2"
    local temp_dir="$3"
    
    log_info "Starting backup of database: $database"
    
    local temp_file="$temp_dir/${database}_${timestamp}.sql"
    local final_filename
    final_filename=$(create_backup_filename "$database" "$timestamp" "$BACKUP_TYPE")
    local final_path="$BACKUP_DIR/$final_filename"
    
    # Build pg_dump command
    local dump_cmd=("pg_dump")
    [[ -n "$PG_HOST" ]] && dump_cmd+=("-h" "$PG_HOST")
    [[ -n "$PG_PORT" ]] && dump_cmd+=("-p" "$PG_PORT")
    [[ -n "$PG_USER" ]] && dump_cmd+=("-U" "$PG_USER")
    
    case "$BACKUP_TYPE" in
        schema)
            dump_cmd+=("--schema-only")
            ;;
        data)
            dump_cmd+=("--data-only")
            ;;
        full)
            # Default: full backup
            ;;
    esac
    
    dump_cmd+=("--verbose" "--file=$temp_file" "$database")
    
    # Execute backup
    log_debug "Executing: ${dump_cmd[*]}"
    if "${dump_cmd[@]}"; then
        log_info "Database dump completed: $database"
    else
        log_error "Database dump failed: $database"
        return 1
    fi
    
    # Process backup file (compression + encryption)
    local processed_file="$temp_dir/processed_${database}_${timestamp}"
    
    # Compress
    if [[ "$COMPRESSION" != "none" ]]; then
        log_debug "Compressing backup with $COMPRESSION"
        compress_backup "$temp_file" "${processed_file}.compressed"
        mv "${processed_file}.compressed" "$processed_file"
    else
        mv "$temp_file" "$processed_file"
    fi
    
    # Encrypt
    if [[ "$ENCRYPTION_ENABLED" == "true" ]]; then
        log_debug "Encrypting backup"
        encrypt_backup "$processed_file" "${processed_file}.encrypted"
        mv "${processed_file}.encrypted" "$processed_file"
    fi
    
    # Move to final location
    mv "$processed_file" "$final_path"
    
    # Verify backup
    if [[ -f "$final_path" ]]; then
        local size
        size=$(du -h "$final_path" | cut -f1)
        log_info "Backup completed: $final_filename (Size: $size)"
        
        # Calculate checksum
        local checksum
        checksum=$(sha256sum "$final_path" | cut -d' ' -f1)
        echo "$checksum  $final_filename" >> "$BACKUP_DIR/checksums.txt"
        log_debug "Checksum: $checksum"
        
        return 0
    else
        log_error "Backup file not found after processing: $final_path"
        return 1
    fi
}

# Main backup function
perform_backup() {
    log_info "Starting PostgreSQL backup process"
    
    # Create backup directory
    mkdir -p "$BACKUP_DIR"
    
    # Create temporary directory
    local temp_dir
    temp_dir=$(mktemp -d)
    trap "rm -rf '$temp_dir'" EXIT
    
    local timestamp
    timestamp=$(date +%Y%m%d_%H%M%S)
    
    # Get database list
    local databases
    readarray -t databases < <(get_database_list)
    
    if [[ ${#databases[@]} -eq 0 ]]; then
        log_error "No databases found to backup"
        return 1
    fi
    
    log_info "Found ${#databases[@]} database(s) to backup: ${databases[*]}"
    
    # Backup each database
    local failed_backups=()
    local successful_backups=()
    
    for database in "${databases[@]}"; do
        if backup_database "$database" "$timestamp" "$temp_dir"; then
            successful_backups+=("$database")
        else
            failed_backups+=("$database")
        fi
    done
    
    # Report results
    log_info "Backup completed - Success: ${#successful_backups[@]}, Failed: ${#failed_backups[@]}"
    
    if [[ ${#successful_backups[@]} -gt 0 ]]; then
        log_info "Successful backups: ${successful_backups[*]}"
    fi
    
    if [[ ${#failed_backups[@]} -gt 0 ]]; then
        log_error "Failed backups: ${failed_backups[*]}"
        return 1
    fi
    
    return 0
}

# Cleanup old backups
cleanup_old_backups() {
    log_info "Cleaning up old backups..."
    
    # Remove backups older than retention period
    if [[ $BACKUP_RETENTION_DAYS -gt 0 ]]; then
        log_info "Removing backups older than $BACKUP_RETENTION_DAYS days"
        find "$BACKUP_DIR" -name "*.sql*" -type f -mtime +$BACKUP_RETENTION_DAYS -delete
    fi
    
    # Keep only the latest N backups per database
    if [[ $BACKUP_RETENTION_COUNT -gt 0 ]]; then
        log_info "Keeping only the latest $BACKUP_RETENTION_COUNT backups per database"
        
        local databases
        readarray -t databases < <(get_database_list)
        
        for database in "${databases[@]}"; do
            # Find backup files for this database and remove old ones
            find "$BACKUP_DIR" -name "${database}_*" -type f | \
                sort -r | \
                tail -n +$((BACKUP_RETENTION_COUNT + 1)) | \
                xargs -r rm -f
        done
    fi
    
    log_info "Cleanup completed"
}

# Send notifications
send_notification() {
    local status="$1"
    local message="$2"
    
    [[ "$MONITORING_ENABLED" != "true" ]] && return 0
    
    local subject="PostgreSQL Backup $status - $(hostname)"
    
    # Email notification
    if [[ -n "$EMAIL_ALERTS" ]] && command -v mail >/dev/null 2>&1; then
        echo "$message" | mail -s "$subject" "$EMAIL_ALERTS"
        log_debug "Email notification sent to $EMAIL_ALERTS"
    fi
    
    # Slack notification
    if [[ -n "$SLACK_WEBHOOK_URL" ]] && command -v curl >/dev/null 2>&1; then
        local payload
        payload=$(cat << EOF
{
    "text": "$subject",
    "attachments": [
        {
            "color": "$([[ "$status" == "SUCCESS" ]] && echo "good" || echo "danger")",
            "text": "$message"
        }
    ]
}
EOF
        )
        
        curl -X POST -H 'Content-type: application/json' \
             --data "$payload" "$SLACK_WEBHOOK_URL" >/dev/null 2>&1
        log_debug "Slack notification sent"
    fi
}

# Parse command line arguments
parse_arguments() {
    while [[ $# -gt 0 ]]; do
        case $1 in
            -h|--help)
                usage
                exit 0
                ;;
            -c|--config)
                CONFIG_FILE="$2"
                shift 2
                ;;
            -d|--database)
                DATABASES="$2"
                shift 2
                ;;
            -t|--type)
                BACKUP_TYPE="$2"
                shift 2
                ;;
            -o|--output)
                BACKUP_DIR="$2"
                shift 2
                ;;
            -v|--verbose)
                DEBUG=true
                shift
                ;;
            -n|--dry-run)
                DRY_RUN=true
                shift
                ;;
            --compression)
                COMPRESSION="$2"
                shift 2
                ;;
            --encrypt)
                ENCRYPTION_ENABLED=true
                shift
                ;;
            --no-monitoring)
                MONITORING_ENABLED=false
                shift
                ;;
            --parallel)
                PARALLEL_JOBS="$2"
                shift 2
                ;;
            backup|restore|list|cleanup|test|config)
                COMMAND="$1"
                shift
                ;;
            *)
                log_error "Unknown option: $1"
                usage
                exit 1
                ;;
        esac
    done
}

# Main function
main() {
    local COMMAND="backup"
    
    # Parse arguments
    parse_arguments "$@"
    
    # Load configuration
    load_config
    
    # Check prerequisites
    check_prerequisites
    
    # Test connection
    test_connection || exit 1
    
    # Execute command
    case "$COMMAND" in
        backup)
            if perform_backup; then
                cleanup_old_backups
                send_notification "SUCCESS" "PostgreSQL backup completed successfully"
                log_info "All backup operations completed successfully"
            else
                send_notification "FAILED" "PostgreSQL backup failed. Check logs for details."
                log_error "Backup operation failed"
                exit 1
            fi
            ;;
        test)
            log_info "Configuration test passed"
            ;;
        config)
            echo "Current configuration:"
            echo "  Backup directory: $BACKUP_DIR"
            echo "  PostgreSQL host: $PG_HOST:$PG_PORT"
            echo "  PostgreSQL user: $PG_USER"
            echo "  Databases: $DATABASES"
            echo "  Backup type: $BACKUP_TYPE"
            echo "  Compression: $COMPRESSION"
            echo "  Encryption: $ENCRYPTION_ENABLED"
            ;;
        *)
            log_error "Unknown command: $COMMAND"
            usage
            exit 1
            ;;
    esac
}

# Execute main function
main "$@"
```

**Configuration File Example (`/etc/postgresql-backup/config.conf`):**
```bash
# PostgreSQL connection settings
PG_HOST="localhost"
PG_PORT="5432"
PG_USER="backup_user"
PGPASSWORD="secure_password"  # Or use .pgpass file

# Backup settings
BACKUP_DIR="/backup/postgresql"
DATABASES="production_db analytics_db user_db"  # or "all" for all databases
BACKUP_TYPE="full"  # full, schema, data
COMPRESSION="gzip"  # gzip, bzip2, xz, none

# Retention settings
BACKUP_RETENTION_DAYS=30
BACKUP_RETENTION_COUNT=7

# Security settings
ENCRYPTION_ENABLED="true"
ENCRYPTION_KEY_FILE="/etc/postgresql-backup/backup.key"

# Monitoring and alerting
MONITORING_ENABLED="true"
EMAIL_ALERTS="dba@company.com ops@company.com"
SLACK_WEBHOOK_URL="https://hooks.slack.com/services/YOUR/SLACK/WEBHOOK"

# Performance settings
PARALLEL_JOBS=2

# Cloud storage (optional)
S3_BACKUP_ENABLED="false"
S3_BUCKET="company-postgresql-backups"
```

**Usage Examples:**
```bash
# Basic backup of all databases
./postgresql_backup.sh backup

# Backup specific databases with custom settings
./postgresql_backup.sh -d "mydb1 mydb2" -t schema --compression bzip2 backup

# Backup with encryption enabled
./postgresql_backup.sh --encrypt backup

# Test configuration
./postgresql_backup.sh test

# List current configuration
./postgresql_backup.sh config

# Cleanup old backups manually
./postgresql_backup.sh cleanup
```

**Cron Job Setup:**
```bash
# Add to crontab for automated backups
# Daily backup at 2 AM
0 2 * * * /usr/local/bin/postgresql_backup.sh backup >/dev/null 2>&1

# Weekly full backup on Sundays
0 1 * * 0 /usr/local/bin/postgresql_backup.sh -t full backup

# Monthly cleanup
0 3 1 * * /usr/local/bin/postgresql_backup.sh cleanup
```

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
