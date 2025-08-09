# Module 9: Shell Scripting Fundamentals




## Table of Contents

- [Module 9: Shell Scripting Fundamentals](#module-9-shell-scripting-fundamentals)
  - [Table of Contents](#table-of-contents)
  - [9.1 Shell Scripting Foundations](#91-shell-scripting-foundations)
    - [Hello World Script (Beginner)](#hello-world-script-beginner)
  - [9.2 Variables and Parameter Management](#92-variables-and-parameter-management)
    - [Greeting Script with Arguments (Beginner)](#greeting-script-with-arguments-beginner)
  - [9.3 Control Structures and Flow Control](#93-control-structures-and-flow-control)
    - [Service Status Checker (Beginner)](#service-status-checker-beginner)
    - [File Line Counter (Beginner)](#file-line-counter-beginner)
    - [Disk Space Warning (Intermediate)](#disk-space-warning-intermediate)
    - [Batch File Renamer (Intermediate)](#batch-file-renamer-intermediate)
    - [Service Manager (Intermediate)](#service-manager-intermediate)
  - [9.4 Functions and Modular Programming](#94-functions-and-modular-programming)
    - [Log File Analyzer (Intermediate)](#log-file-analyzer-intermediate)
    - [Interactive Confirmation (Intermediate)](#interactive-confirmation-intermediate)
    - [Robust Script Template (Intermediate)](#robust-script-template-intermediate)
  - [9.5 Error Handling and Debugging](#95-error-handling-and-debugging)
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
    - [1. Backup Script with Rotation](#1-backup-script-with-rotation)
    - [2. System Monitoring Script with Alerting](#2-system-monitoring-script-with-alerting)
    - [3. User Management Automation Script](#3-user-management-automation-script)
    - [4. Log Analysis and Reporting Script](#4-log-analysis-and-reporting-script)
    - [5. Deployment Automation Script](#5-deployment-automation-script)
  - [Next Steps](#next-steps)
  - [Resources for Further Study](#resources-for-further-study)
  - [Glossary](#glossary)

## 9.1 Shell Scripting Foundations


Welcome to Shell Scripting Foundations! This section introduces the basics of shell scripting in Linux using bash. You’ll learn how scripts work, how to write and run your first script, and why scripting is a powerful tool for sysadmins.

**Learning Objectives:**
- Understand what a shell script is and how it works
- Write and execute a simple bash script
- Recognize the structure and anatomy of a basic script

**Why Learn Shell Scripting?**
Shell scripting lets you automate repetitive tasks, manage systems efficiently, and solve problems quickly. Even simple scripts can save hours of manual work.

---

### Hello World Script (Beginner)
**Example:**

```bash
#!/bin/bash              # Shebang: tells the system to use bash to run this script
echo "Hello, world!"     # Prints a message to the terminal
```
This script demonstrates the basics: shebang, echo, and running a script. Try editing the message or adding your name.

**Common Pitfalls:**
- Forgetting the shebang (`#!/bin/bash`) at the top of your script
- Not making the script executable (`chmod +x script.sh`)
- Using incorrect quotes or missing quotes around strings

**Check Your Understanding:**
1. What does the shebang (`#!/bin/bash`) do?
2. How do you run a script after saving it?
3. What happens if you forget to make your script executable?

## 9.2 Variables and Parameter Management


Variables and parameters are the building blocks of any shell script. In this section, you’ll learn how to store and use data, pass information to scripts, and manipulate values for automation.

**Learning Objectives:**
- Understand how to declare and use variables in bash
- Use command-line arguments and special parameters
- Apply basic data manipulation techniques in scripts

**Why Variables Matter:**
Variables let you store information, reuse values, and make your scripts flexible. Parameters allow scripts to accept input and behave differently based on user needs.

---

### Greeting Script with Arguments (Beginner)
**Example:**

```bash
#!/bin/bash                  # Use bash to run this script
name="${1:-Guest}"           # Set 'name' to the first argument, or 'Guest' if none provided
echo "Welcome, $name!"        # Print a welcome message
```
This script uses a variable and command-line argument. Run with `./script.sh Alice` or just `./script.sh`.

**Common Pitfalls:**
- Forgetting to use quotes around variables (e.g., `$name`)
- Not providing a default value for arguments
- Using `$1` without checking if it exists

**Check Your Understanding:**
1. What does `${1:-Guest}` mean in this script?
2. How would you change the script to greet multiple names?
3. Why is it important to quote variables in bash?

## 9.3 Control Structures and Flow Control


Control structures are how scripts make decisions and repeat actions. This section teaches you to use if/else statements, loops, and case statements to control the flow of your scripts.

**Learning Objectives:**
- Use if/else statements to make decisions in scripts
- Write loops to repeat actions efficiently
- Apply case statements for multi-way branching

**Why Control Structures Matter:**
Control structures let your scripts respond to different situations, automate repetitive tasks, and handle complex logic with ease.

---

### Service Status Checker (Beginner)
### File Line Counter (Beginner)
### Disk Space Warning (Intermediate)
### Batch File Renamer (Intermediate)
### Service Manager (Intermediate)

**What does this script do?**
This script checks if a specific system service (like nginx, ssh, or apache2) is running and prints a message to the user. It’s useful for quickly verifying service status during troubleshooting or automation.

**How does it work?**
```bash
#!/bin/bash
service="nginx"                                 # Set the service name to check
if systemctl is-active --quiet "$service"; then # Check if the service is running
    echo "$service is running"                   # Print running message
else
    echo "$service is not running"               # Print not running message
fi
```
- The script sets the service name in the `service` variable.
- It uses `systemctl is-active --quiet "$service"` to check if the service is running (returns 0 if active).
- If the service is running, it prints a confirmation; otherwise, it prints a warning.

**How do I use it?**
1. Save the script as `check_service.sh`.
2. Make it executable: `chmod +x check_service.sh`
3. Run it: `./check_service.sh`
4. To check a different service, change the value of `service` (e.g., `service="ssh"`).

**Sample Output:**
```
nginx is running
```
or
```
nginx is not running
```

**Tips for customization:**
- Accept the service name as a command-line argument: `service="${1:-nginx}"`
- Add more detailed output or logging for troubleshooting.
- Combine with other scripts to automate service checks across multiple servers.

**Common Pitfalls:**
- Misspelling the service name (e.g., 'ngnix' instead of 'nginx')
- Not using quotes around variables
- Forgetting to use `systemctl` on systems that use a different init system

**Check Your Understanding:**
1. What does `systemctl is-active --quiet "$service"` do?
2. How would you modify the script to check a different service?
3. What happens if you run this script on a system without systemd?

## 9.4 Functions and Modular Programming


Functions help you organize your scripts, avoid repetition, and build reusable code blocks. This section shows how to write functions and structure scripts for maintainability and scalability.

**Learning Objectives:**
- Define and use functions in bash scripts
- Organize code into modular, reusable components
- Apply script templates for best practices

**Why Functions Matter:**
Functions make scripts easier to read, debug, and extend. Modular programming is key to writing professional, maintainable scripts.

---

### Log File Analyzer (Intermediate)
### Interactive Confirmation (Intermediate)
### Robust Script Template (Intermediate)
...existing code...

## 9.5 Error Handling and Debugging


No script is perfect on the first try! This section teaches you how to handle errors, debug scripts, and troubleshoot common problems so your automation is reliable and safe.

**Learning Objectives:**
- Implement error handling in bash scripts
- Use debugging tools and techniques
- Troubleshoot and fix common scripting issues

**Why Error Handling Matters:**
Good error handling and debugging save time, prevent mistakes, and make your scripts robust for real-world use.

---

...existing code...
if systemctl is-active --quiet "$service"; then
    echo "$service is running"
else
    echo "$service is not running"
fi
```
This example checks if a service is running, using an if/else statement and command substitution.

---

### 4. File Line Counter (Beginner)


**What does this script do?**
This script counts the number of lines in a specified file. It’s useful for quickly checking file size, log file growth, or validating data files.

**How does it work?**
```bash
#!/bin/bash
file="/etc/passwd"           # File to read
count=0                      # Initialize line counter
while IFS= read -r line; do  # Read each line from the file
    ((count++))              # Increment counter for each line
done < "$file"               # Redirect file into the loop
echo "Total lines: $count"    # Print the total number of lines
```
- The script sets the file path in the `file` variable.
- It initializes a counter variable `count` to zero.
- It reads each line from the file and increments the counter for each line.
- Finally, it prints the total number of lines.

**How do I use it?**
1. Save the script as `count_lines.sh`.
2. Make it executable: `chmod +x count_lines.sh`
3. Run it: `./count_lines.sh`
4. To count lines in a different file, change the value of `file` (e.g., `file="mydata.txt"`).

**Sample Output:**
```
Total lines: 42
```

**Tips for customization:**
- Accept the file name as a command-line argument: `file="${1:-/etc/passwd}"`
- Add error checking to handle missing or unreadable files.
- Use `wc -l "$file"` for a simpler alternative (but less flexible for processing each line).

**Common Pitfalls:**
- Not checking if the file exists before reading
- Forgetting to quote the file variable
- Using the wrong file path

**Check Your Understanding:**
1. What does `IFS= read -r line` do?
2. How would you modify the script to count lines in a different file?
3. What happens if the file does not exist?

---

### 5. Disk Space Warning (Intermediate)


**What does this script do?**
This script checks the disk usage of your root filesystem and warns you if it exceeds a specified threshold. It’s useful for monitoring disk space and preventing outages due to full disks.

**How does it work?**
```bash
#!/bin/bash
check_disk_space() {
    local threshold="${1:-80}"                # Set threshold, default to 80%
    local usage=$(df / | awk 'NR==2 {print int($5)}') # Get disk usage percentage
    if [[ $usage -gt $threshold ]]; then      # Compare usage to threshold
        echo "WARNING: Disk usage is ${usage}% (threshold: ${threshold}%)"
        return 1
    else
        echo "Disk usage is acceptable: ${usage}%"
        return 0
    fi
}
check_disk_space 75                          # Call function with threshold 75%
```
- The function `check_disk_space` takes a threshold value (default 80%).
- It uses `df /` to get disk usage for the root filesystem and `awk` to extract the percentage.
- If usage exceeds the threshold, it prints a warning and returns 1; otherwise, it prints an OK message and returns 0.

**How do I use it?**
1. Save the script as `disk_space_check.sh`.
2. Make it executable: `chmod +x disk_space_check.sh`
3. Run it: `./disk_space_check.sh 75` (or any threshold you want)
4. To check a different mount point, change `/` to another path (e.g., `/home`).

**Sample Output:**
```
WARNING: Disk usage is 82% (threshold: 75%)
```
or
```
Disk usage is acceptable: 42%
```

**Tips for customization:**
- Schedule this script with cron to monitor disk space automatically.
- Send email alerts or log warnings for proactive monitoring.
- Check multiple mount points in a loop for comprehensive coverage.

**Common Pitfalls:**
- Not using `int($5)` in `awk` (may cause string comparison issues)
- Forgetting to quote variables
- Not handling cases where `df` output format changes

**Check Your Understanding:**
1. What does `local threshold="${1:-80}"` do?
2. How would you change the script to check a different mount point?
3. Why is error handling important in disk space scripts?

---

### 6. Batch File Renamer (Intermediate)


**What does this script do?**
This script renames all `.txt` files in the current directory to `.bak` files. It’s useful for batch processing, archiving, or preparing files for backup.

**How does it work?**
```bash
#!/bin/bash
for file in *.txt; do                       # Loop through all .txt files in the directory
    [[ -f "$file" ]] || continue           # Skip if not a regular file
    mv "$file" "${file%.txt}.bak"           # Rename file by changing extension to .bak
    echo "Renamed $file to ${file%.txt}.bak" # Print what was renamed
done
```
- The script loops through all files ending in `.txt`.
- It checks if each item is a regular file before renaming.
- It uses string manipulation `${file%.txt}.bak` to change the extension.
- It prints a message for each file renamed.

**How do I use it?**
1. Save the script as `rename_txt_to_bak.sh`.
2. Make it executable: `chmod +x rename_txt_to_bak.sh`
3. Run it in the directory with your `.txt` files: `./rename_txt_to_bak.sh`
4. To rename `.log` files, change `*.txt` to `*.log` and `.bak` to your desired extension.

**Sample Output:**
```
Renamed notes.txt to notes.bak
Renamed data.txt to data.bak
```

**Tips for customization:**
- Add error checking to avoid overwriting existing files.
- Use a backup directory for renamed files.
- Extend the script to handle multiple file types or patterns.

**Common Pitfalls:**
- Not checking if files exist before renaming
- Accidentally overwriting files with the same name
- Forgetting to escape special characters in filenames

**Check Your Understanding:**
1. What does `${file%.txt}.bak` do?
2. How would you modify the script to rename `.log` files instead?
3. Why is it important to check if a file exists before renaming?

---

### 7. Service Manager (Intermediate)


**What does this script do?**
This script lets you start, stop, or check the status of a system service (like nginx, ssh, etc.) using a single command. It’s useful for automating service management and reducing manual errors.

**How does it work?**
```bash
#!/bin/bash
service_action() {
    local action="$1"                        # First argument: action to perform
    local service_name="${2:-nginx}"         # Second argument: service name, default to nginx
    case "$action" in
        start)
            systemctl start "$service_name" && echo "Started $service_name" # Start service
            ;;
        stop)
            systemctl stop "$service_name" && echo "Stopped $service_name" # Stop service
            ;;
        status)
            systemctl status "$service_name" # Show service status
            ;;
        *)
            echo "Usage: $0 {start|stop|status} [service_name]" # Print usage info
            return 1
            ;;
    esac
}
service_action "$@"                         # Call function with all script arguments
```
- The function `service_action` takes two arguments: the action (start, stop, status) and the service name (default: nginx).
- It uses a case statement to perform the requested action.
- It prints feedback for each action and usage info for invalid actions.

**How do I use it?**
1. Save the script as `service_manager.sh`.
2. Make it executable: `chmod +x service_manager.sh`
3. Run it: `./service_manager.sh start nginx` or `./service_manager.sh status ssh`
4. To add more actions (like restart), add another case to the statement.

**Sample Output:**
```
Started nginx
Stopped ssh
Usage: ./service_manager.sh {start|stop|status} [service_name]
```

**Tips for customization:**
- Add logging for each action performed.
- Accept multiple services as arguments for batch management.
- Add error handling for failed service commands.

**Common Pitfalls:**
- Not providing a default service name
- Misspelling actions (e.g., 'strat' instead of 'start')
- Not handling invalid actions gracefully

**Check Your Understanding:**
1. What does `${2:-nginx}` do in this script?
2. How would you add a 'restart' action to the case statement?
3. Why is it useful to use functions for service management scripts?

---

### 8. Log File Analyzer (Intermediate)
**Concepts:** Functions, loops, string matching

```bash
#!/bin/bash
analyze_log() {
    local logfile="$1"                # Log file to analyze
    local errors=0                    # Counter for error lines
    local warnings=0                  # Counter for warning lines
    while IFS= read -r line; do       # Read each line from the log file
        [[ "$line" == *ERROR* ]] && ((errors++))   # Increment error counter if line contains 'ERROR'
        [[ "$line" == *WARN* ]] && ((warnings++))  # Increment warning counter if line contains 'WARN'
    done < "$logfile"                # Redirect log file into the loop
    echo "Errors: $errors"            # Print error count
    echo "Warnings: $warnings"        # Print warning count
}
analyze_log "/var/log/syslog"         # Call function with log file path
```
This function analyzes a log file and counts error and warning lines, using loops and string matching.

**Common Pitfalls:**
- Not checking if the log file exists before reading
- Case sensitivity: 'error' vs 'ERROR'
- Not handling empty or very large log files

**Check Your Understanding:**
1. What does `[[ "$line" == *ERROR* ]]` do?
2. How would you modify the script to count 'INFO' lines?
3. Why is it important to check if the log file exists before analyzing?
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

---

### 9. Interactive Confirmation (Intermediate)
    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
**Concepts:** Functions, user input

```bash
#!/bin/bash
confirm_action() {
    read -p "Are you sure you want to proceed? (y/n): " answer # Prompt user for confirmation
    if [[ "$answer" =~ ^[Yy]$ ]]; then                        # Check if answer is 'y' or 'Y'
        echo "Proceeding..."                                   # Proceed if confirmed
    else
        echo "Cancelled."                                      # Cancel if not confirmed
    fi
}
confirm_action
```
This script asks the user for confirmation before proceeding, using a function and user input.

**Common Pitfalls:**
- Not handling uppercase and lowercase responses
- Forgetting to prompt the user clearly
- Not validating user input

**Check Your Understanding:**
1. What does `read -p` do in this script?
2. How would you modify the script to accept 'yes' or 'no' as valid responses?
3. Why is input validation important in interactive scripts?

---

    [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚
### 10. Robust Script Template (Intermediate)
**Concepts:** Strict mode, error handling, functions, logging

```bash
#!/usr/bin/env bash
set -euo pipefail                      # Enable strict mode: exit on error, unset vars, pipefail

log() {
    local level="$1"                  # Log level (INFO, ERROR, etc.)
    shift
    echo "[$level] $*"                 # Print log message with level
}

main() {
    log INFO "Script started"          # Log script start
    # Add your main logic here         # Placeholder for main script logic
    log INFO "Script completed"        # Log script completion
}

trap 'log ERROR "An error occurred on line $LINENO"; exit 1' ERR # Trap errors and log them
main "$@"                            # Run main function with all arguments
```
This template demonstrates best practices: strict mode, error handling, functions, and logging.

**Common Pitfalls:**
- Forgetting to use `set -euo pipefail` for strict mode
- Not using functions for organization
- Not handling errors with traps

**Check Your Understanding:**
1. What does `set -euo pipefail` do?
2. How does the `trap` command help with error handling?
3. Why is logging important in scripts?

---

These examples reinforce the concepts covered in this module and provide a foundation for building more advanced scripts. Try modifying and combining them to automate your own tasks.

## Best Practices

Professional shell scripts follow best practices for reliability, security, and maintainability. This section covers standards and tips to help you write scripts like a pro.

**Learning Objectives:**
- Apply development standards for shell scripts
- Optimize performance and resource usage
- Implement security best practices

---

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
name=$1                  # Get first argument, may be empty
echo "Hello, $name!"      # Print greeting
```
If you run `./script.sh` and see "Hello, !", try adding debug output:

```bash
set -x                    # Enable debug mode (shows commands as they run)
name=$1
echo "Hello, $name!"
set +x                    # Disable debug mode
```
Or provide a default value:

```bash
name="${1:-Guest}"        # Use 'Guest' if no argument is provided
```

**Common Pitfalls:**
- Not providing a default value for arguments
- Forgetting to enable debug mode when troubleshooting
- Not quoting variables in echo statements

**Check Your Understanding:**
1. What does `set -x` do in a script?
2. How can you make sure your script always greets someone, even if no argument is given?
3. Why is quoting variables important in echo statements?

### When to Ask for Help

If you get stuck, check:
- The error message (read it carefully)
- Your variable quoting and expansion
- File permissions and paths
- The script's shebang (`#!/bin/bash`)

If you still can't solve it, ask a colleague or search online for the error message.


[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

## Lab Exercises

Practice is the best way to learn shell scripting! These hands-on labs reinforce your skills and prepare you for real-world sysadmin tasks.

**Learning Objectives:**
- Apply scripting concepts to solve practical problems
- Automate common system administration tasks
- Build confidence through hands-on experience

---

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

Congratulations on completing the Shell Scripting Fundamentals module! You’re now ready to tackle more advanced Linux administration topics.

**Learning Objectives:**
- Identify next steps in your Linux sysadmin journey
- Connect shell scripting skills to broader system management
- Prepare for advanced modules and real-world scenarios

With shell scripting fundamentals mastered, you're ready to explore Storage & Filesystem Management in Module 10, where you'll learn advanced storage concepts and filesystem administration.

---

## Resources for Further Study

- [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [ShellCheck Online Shell Script Linter](https://www.shellcheck.net/)
- [LinuxCommand.org Bash Scripting Tutorial](http://linuxcommand.org/lc3_writing_shell_scripts.php)
- [Bash Beginner's Guide (The Linux Documentation Project)](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)

## Glossary

- **Shebang**: The `#!/bin/bash` line at the top of a script that tells the system which interpreter to use.
- **Variable**: A named storage location for data in a script.
- **Parameter**: Input passed to a script or function, such as `$1`, `$2`, etc.
- **Control Structure**: Programming constructs like if/else, loops, and case statements that control script flow.
- **Function**: A reusable block of code within a script.
- **Pipefail**: A shell option that causes a pipeline to return the exit status of the last command to fail.
- **Trap**: A shell feature to catch signals or errors and run code in response.
- **Debug Mode**: A mode (`set -x`) that prints each command before executing it, useful for troubleshooting.
- **Strict Mode**: Using `set -euo pipefail` to make scripts safer and more predictable.
