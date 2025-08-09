# Module 9: Shell Scripting Fundamentals

## Table of Contents

- [Module 9: Shell Scripting Fundamentals](#module-9-shell-scripting-fundamentals)
  - [Table of Contents](#table-of-contents)
  - [Table of Contents](#table-of-contents-1)
  - [Overview](#overview)
  - [Practical Examples](#practical-examples)
    - [1. Hello World Script (Beginner)](#1-hello-world-script-beginner)
    - [2. Greeting Script with Arguments (Beginner)](#2-greeting-script-with-arguments-beginner)
    - [3. Service Status Checker (Beginner)](#3-service-status-checker-beginner)
    - [4. File Line Counter (Beginner)](#4-file-line-counter-beginner)
    - [5. Disk Space Warning (Intermediate)](#5-disk-space-warning-intermediate)
    - [6. Batch File Renamer (Intermediate)](#6-batch-file-renamer-intermediate)
    - [7. Service Manager (Intermediate)](#7-service-manager-intermediate)
    - [8. Log File Analyzer (Intermediate)](#8-log-file-analyzer-intermediate)
    - [9. Interactive Confirmation (Intermediate)](#9-interactive-confirmation-intermediate)
    - [10. Robust Script Template (Intermediate)](#10-robust-script-template-intermediate)
  - [Best Practices](#best-practices)
    - [Script Development Standards](#script-development-standards)
    - [Performance Optimization](#performance-optimization)
    - [Security Considerations](#security-considerations)
  - [Troubleshooting](#troubleshooting)
    - [Common Scripting Issues](#common-scripting-issues)
    - [Debugging Techniques](#debugging-techniques)
    - [Quick Fixes for Common Problems](#quick-fixes-for-common-problems)
    - [Example: Debugging a Script](#example-debugging-a-script)
    - [When to Ask for Help](#when-to-ask-for-help)
  - [Lab Exercises](#lab-exercises)
  - [Lab Exercises](#lab-exercises-1)
    - [1. Backup Script with Rotation](#1-backup-script-with-rotation)
    - [2. System Monitoring Script with Alerting](#2-system-monitoring-script-with-alerting)
    - [3. User Management Automation Script](#3-user-management-automation-script)
    - [4. Log Analysis and Reporting Script](#4-log-analysis-and-reporting-script)
    - [5. Deployment Automation Script](#5-deployment-automation-script)
  - [Next Steps](#next-steps)


## Table of Contents


## Overview


This module introduces the fundamentals of shell scripting in Linux using bash. You will learn how to write, execute, and debug basic scripts, use variables, control flow, and functions, and automate common system administration tasks. The focus is on practical, beginner to intermediate skills for everyday Linux scripting.

**Module Focus Areas:**

By the end of this module, you will be able to:
1. Write and execute basic bash scripts
2. Use variables, parameters, and simple data manipulation
3. Implement control flow with if/else, case, and loops
4. Create and use functions for modular code
5. Handle basic errors and debug scripts
6. Automate simple system administration tasks

## Practical Examples

Below are practical shell scripting examples, ordered from beginner to intermediate. Each example builds on concepts covered earlier in this module, such as variables, control flow, functions, error handling, and file operations.

### 1. Hello World Script (Beginner)
**Concepts:** Script anatomy, echo, running scripts

```bash
#!/bin/bash
echo "Hello, world!"
```
This script demonstrates the basics: shebang, echo, and running a script. Try editing the message or adding your name.

---

### 2. Greeting Script with Arguments (Beginner)
**Concepts:** Variables, command-line arguments

```bash
#!/bin/bash
name="${1:-Guest}"
echo "Welcome, $name!"
```
This script uses a variable and command-line argument. Run with `./script.sh Alice` or just `./script.sh`.

---

### 3. Service Status Checker (Beginner)
**Concepts:** If/else, command substitution

```bash
#!/bin/bash
service="nginx"
if systemctl is-active --quiet "$service"; then
    echo "$service is running"
else
    echo "$service is not running"
fi
```
This example checks if a service is running, using an if/else statement and command substitution.

---

### 4. File Line Counter (Beginner)
**Concepts:** Reading files, loops

```bash
#!/bin/bash
file="/etc/passwd"
count=0
while IFS= read -r line; do
    ((count++))
done < "$file"
echo "Total lines: $count"
```
This script reads a file line by line and counts the lines, demonstrating loops and file input.

---

### 5. Disk Space Warning (Intermediate)
**Concepts:** Functions, numeric comparison, error handling

```bash
#!/bin/bash
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
check_disk_space 75
```
This function checks disk usage and prints a warning if usage exceeds the threshold. It uses numeric comparison and a function for modularity.

---

### 6. Batch File Renamer (Intermediate)
**Concepts:** For loop, string manipulation

```bash
#!/bin/bash
for file in *.txt; do
    [[ -f "$file" ]] || continue
    mv "$file" "${file%.txt}.bak"
    echo "Renamed $file to ${file%.txt}.bak"
done
```
This script renames all `.txt` files to `.bak`, using a for loop and string manipulation.

---

### 7. Service Manager (Intermediate)
**Concepts:** Case statement, functions, command-line arguments

```bash
#!/bin/bash
service_action() {
    local action="$1"
    local service_name="${2:-nginx}"
    case "$action" in
        start)
            systemctl start "$service_name" && echo "Started $service_name"
            ;;
        stop)
            systemctl stop "$service_name" && echo "Stopped $service_name"
            ;;
        status)
            systemctl status "$service_name"
            ;;
        *)
            echo "Usage: $0 {start|stop|status} [service_name]"
            return 1
            ;;
    esac
}
service_action "$@"
```
This script uses a case statement and function to manage a service, demonstrating modular code and argument parsing.

---

### 8. Log File Analyzer (Intermediate)
**Concepts:** Functions, loops, string matching

```bash
#!/bin/bash
analyze_log() {
    local logfile="$1"
    local errors=0
    local warnings=0
    while IFS= read -r line; do
        [[ "$line" == *ERROR* ]] && ((errors++))
        [[ "$line" == *WARN* ]] && ((warnings++))
    done < "$logfile"
    echo "Errors: $errors"
    echo "Warnings: $warnings"
}
analyze_log "/var/log/syslog"
```
This function analyzes a log file and counts error and warning lines, using loops and string matching.
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

---

### 9. Interactive Confirmation (Intermediate)
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
**Concepts:** Functions, user input

```bash
#!/bin/bash
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
else
    echo "Cancelled."
fi
```
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
This script asks the user for confirmation before proceeding, using a function and user input.

---

    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
### 10. Robust Script Template (Intermediate)
**Concepts:** Strict mode, error handling, functions, logging

    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
```bash
#!/usr/bin/env bash
set -euo pipefail

log() {
    local level="$1"
    shift
    echo "[$level] $*"
}

main() {
    log INFO "Script started"
    # Add your main logic here
    log INFO "Script completed"
}

trap 'log ERROR "An error occurred on line $LINENO"; exit 1' ERR
main "$@"
```
This template demonstrates best practices: strict mode, error handling, functions, and logging.

---

These examples reinforce the concepts covered in this module and provide a foundation for building more advanced scripts. Try modifying and combining them to automate your own tasks.

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

Troubleshooting is an essential skill for shell scripters. Here are common issues, practical debugging tips, and solutions for problems you may encounter as a beginner or intermediate user.

### Common Scripting Issues

| Issue                       | Symptoms                        | Resolution                                      |
|-----------------------------|----------------------------------|-------------------------------------------------|
| Variable Expansion Problems | Unexpected values or empty vars  | Use proper quoting and parameter expansion      |
| Permission Errors           | "Permission denied" errors      | Check file permissions and user privileges      |
| Path Issues                 | "Command not found" errors      | Verify PATH and use full paths for commands     |
| Array Handling              | Index errors or odd behavior     | Properly declare and reference arrays           |
| Signal Handling             | Scripts not cleaning up properly | Implement proper trap handlers                  |

### Debugging Techniques

- **Enable Debug Mode:**
    ```bash
    set -x  # Show each command as it runs
    set +x  # Turn off debug mode
    ```
    You can enable debug mode for the whole script or just a section.

- **Print Variable Values:**
    Use `echo` or `printf` to display variable values at key points.

- **Check Exit Codes:**
    ```bash
    if ! command; then
            echo "Command failed"
            exit 1
    fi
    ```

- **Function Tracing:**
    ```bash
    PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]:+${FUNCNAME[0]}():} '
    set -x
    ```
    This makes debug output more informative.

- **Log Output to a File:**
    Redirect debug output for later review:
    ```bash
    set -x
    # ...commands...
    set +x
    ```
    Run your script as: `bash -x script.sh 2>debug.log`

### Quick Fixes for Common Problems

- **Unquoted Variables:** Always quote variables, especially in file paths and arguments.
- **File Permissions:** Use `chmod +x script.sh` to make scripts executable.
- **PATH Issues:** Use absolute paths for commands if unsure, or check your PATH variable.
- **Temporary Files:** Use `mktemp` for safe temp file creation and clean up with `trap`.
- **Array Syntax:** Use `declare -a` for indexed arrays and `declare -A` for associative arrays.

### Example: Debugging a Script

Suppose your script isn't working as expected:
```bash
#!/bin/bash
name=$1
echo "Hello, $name!"
```
If you run `./script.sh` and see "Hello, !", try adding debug output:
```bash
set -x
name=$1
echo "Hello, $name!"
set +x
```
Or provide a default value:
```bash
name="${1:-Guest}"
```

### When to Ask for Help

If you get stuck, check:
- The error message (read it carefully)
- Your variable quoting and expansion
- File permissions and paths
- The script's shebang (`#!/bin/bash`)

If you still can't solve it, ask a colleague or search online for the error message.


[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

## Lab Exercises
## Lab Exercises

These hands-on exercises reinforce the core skills covered in this module. Each project is designed to help you practice real-world shell scripting tasks and build confidence for system administration work.

### 1. Backup Script with Rotation
**Goal:** Automate directory backups and manage old backups.
**Skills:** File operations, loops, error handling, scheduling.
**Challenge:** Create a script that backs up a directory, compresses the backup, and keeps only the last N backups.

### 2. System Monitoring Script with Alerting
**Goal:** Monitor system resources and send alerts when thresholds are exceeded.
**Skills:** Process management, resource monitoring, notifications.
**Challenge:** Write a script that checks CPU, memory, and disk usage, and sends an alert (e.g., email or log) if limits are reached.

### 3. User Management Automation Script
**Goal:** Automate user and group management tasks.
**Skills:** User/group commands, input validation, reporting.
**Challenge:** Develop a script to add, remove, or list users and groups, and generate a summary report.

### 4. Log Analysis and Reporting Script
**Goal:** Analyze log files and generate useful statistics.
**Skills:** Text processing, pattern matching, summary statistics.
**Challenge:** Build a script that parses a log file, counts error/warning/info entries, and outputs a summary report.

### 5. Deployment Automation Script
**Goal:** Automate application or service deployment steps.
**Skills:** Modular scripting, service management, repeatable tasks.
**Challenge:** Create a script that installs packages, configures services, and verifies successful deployment.

---
Try these exercises to apply your knowledge and prepare for real-world Linux administration tasks. Each project can be expanded as your skills grow.

## Next Steps
With shell scripting fundamentals mastered, you're ready to explore Storage & Filesystem Management in Module 10, where you'll learn advanced storage concepts and filesystem administration.
