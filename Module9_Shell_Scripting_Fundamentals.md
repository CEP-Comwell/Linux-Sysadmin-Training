# Module 9: Shell Scripting Fundamentals

---

## Learning Objectives

- Understand the basics of writing and running Bash scripts
- Use variables, quoting, and parameter expansion safely
- Apply basic conditionals and control flow
- Follow best practices: shebang, `set -euo pipefail`, quoting, safe loops
- Recognize and avoid common pitfalls
- Build, debug, and automate tasks with scripts
- Practice with hands-on labs and real-world examples

---




## Table of Contents

- [Module 9: Shell Scripting Fundamentals](#module-9-shell-scripting-fundamentals)
  - [Learning Objectives](#learning-objectives)
  - [Table of Contents](#table-of-contents)
  - [9.1 Shell Scripting Foundations](#91-shell-scripting-foundations)
    - [Hello World Script (Beginner)](#hello-world-script-beginner)
    - [9. Interactive Confirmation (Intermediate)](#9-interactive-confirmation-intermediate)
  - [9.2 Variables and Parameter Management](#92-variables-and-parameter-management)
    - [Greeting Script with Arguments (Beginner)](#greeting-script-with-arguments-beginner)
- [Run with: ./script.sh Alice](#run-with-scriptsh-alice)
- [Or: ./script.sh](#or-scriptsh)
  - [9.3 Control Structures and Flow Control](#93-control-structures-and-flow-control)
    - [Conditionals: `if`, `elif`, `else`](#conditionals-if-elif-else)
    - [Why Prefer `[[ ... ]]` Over `[ ... ]`](#why-prefer----over---)
    - [`case` Statement for Subcommands](#case-statement-for-subcommands)
    - [Safe Loop Patterns](#safe-loop-patterns)
      - [Iterate Arrays](#iterate-arrays)
      - [Read Lines Safely](#read-lines-safely)
      - [File Iteration with `nullglob` or `find`](#file-iteration-with-nullglob-or-find)
    - [Real-World Example: Summarize Top 5 Log Messages](#real-world-example-summarize-top-5-log-messages)
  - [9.4 Functions and Modular Programming](#94-functions-and-modular-programming)
    - [Function Definitions and Calls](#function-definitions-and-calls)
    - [Handling Arguments: `$1`, `$@`, `"$@"`, Arrays](#handling-arguments-1---arrays)
    - [Returning Data: `echo`/`printf` and Capturing Output](#returning-data-echoprintf-and-capturing-output)
    - [Return Codes vs Data](#return-codes-vs-data)
    - [Reusable Helpers](#reusable-helpers)
    - [Modular Script Structure](#modular-script-structure)
    - [Argument Parsing with `getopts`](#argument-parsing-with-getopts)
    - [Example: Function Reuse Across Two Tasks](#example-function-reuse-across-two-tasks)
    - [Lab: Modularize a Script](#lab-modularize-a-script)
  - [9.5 Error Handling and Debugging](#95-error-handling-and-debugging)
    - [Strict Mode: `set -euo pipefail`](#strict-mode-set--euo-pipefail)
    - [Traps for Cleanup](#traps-for-cleanup)
    - [Inspecting Exit Codes and Pipeline Failures](#inspecting-exit-codes-and-pipeline-failures)
    - [Debugging Techniques](#debugging-techniques)
    - [ShellCheck: Lint Your Scripts](#shellcheck-lint-your-scripts)
    - [Minimal Example: Temp Dir, Trap, Failure, Cleanup](#minimal-example-temp-dir-trap-failure-cleanup)
    - [Lab: Add Robust Error Handling](#lab-add-robust-error-handling)
  - [](#)
    - [4. File Line Counter (Beginner)](#4-file-line-counter-beginner)
    - [5. Disk Space Warning (Intermediate)](#5-disk-space-warning-intermediate)
    - [6. Batch File Renamer (Intermediate)](#6-batch-file-renamer-intermediate)
    - [7. Service Manager (Intermediate)](#7-service-manager-intermediate)
    - [8. Log File Analyzer (Intermediate)](#8-log-file-analyzer-intermediate)
    - [9. Interactive Confirmation (Intermediate)](#9-interactive-confirmation-intermediate-1)
    - [10. Robust Script Template (Intermediate)](#10-robust-script-template-intermediate)
  - [Best Practices](#best-practices)
    - [1. Script Development Standards](#1-script-development-standards)
      - [Script Development Standards: Checklist](#script-development-standards-checklist)
    - [2. Error Handling \& Logging](#2-error-handling--logging)
    - [3. Security \& Maintainability](#3-security--maintainability)
    - [Script Development Standards](#script-development-standards)
    - [Performance Optimization](#performance-optimization)
      - [Performance Optimization: Efficient Bash Scripting](#performance-optimization-efficient-bash-scripting)
    - [Security Considerations](#security-considerations)
      - [Security Considerations: Safe Bash Patterns](#security-considerations-safe-bash-patterns)
  - [Troubleshooting](#troubleshooting)
    - [Common Scripting Issues](#common-scripting-issues)
    - [Debugging Techniques](#debugging-techniques-1)
    - [Quick Fixes for Common Problems](#quick-fixes-for-common-problems)
    - [Example: Debugging a Script](#example-debugging-a-script)
      - [1. The Buggy Script](#1-the-buggy-script)
      - [2. Reproduce the Issue](#2-reproduce-the-issue)
      - [3. Add Debugging](#3-add-debugging)
      - [4. Apply Guards and Quoting](#4-apply-guards-and-quoting)
      - [5. Verify the Fix](#5-verify-the-fix)
    - [When to Ask for Help](#when-to-ask-for-help)
  - [Lab Exercises](#lab-exercises)
    - [1. Backup Script with Rotation](#1-backup-script-with-rotation)
    - [2. System Monitoring Script with Alerting](#2-system-monitoring-script-with-alerting)
    - [3. User Management Automation Script](#3-user-management-automation-script)
    - [4. Log Analysis and Reporting Script](#4-log-analysis-and-reporting-script)
    - [5. Deployment Automation Script](#5-deployment-automation-script)
  - [Next Steps](#next-steps)
  - [Quick Reference Cheat Sheet](#quick-reference-cheat-sheet)
  - [Resources for Further Study](#resources-for-further-study)
  - [Glossary](#glossary)

## 9.1 Shell Scripting Foundations


Welcome to Shell Scripting Foundations! This section introduces the basics of shell scripting in Linux using Bash. You'll start with a simple Hello World script, then learn about variables, quoting, and basic conditionals. Each example includes a one-line purpose and inline comments. Best practices are emphasized from the start.

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

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

### 9. Interactive Confirmation (Intermediate)

**What does this script do?**
Prompts users for confirmation (yes/no) safely, handling stdin, tty, and non-interactive modes. Useful before destructive actions like deleting files.

```bash
#!/usr/bin/env bash
set -euo pipefail

confirm() {
    local prompt="${1:-Are you sure? [y/N]}"
    local timeout="${2:-}" # Optional timeout in seconds
    local answer=""
    if [[ "${CONFIRM_YES:-}" == "1" ]]; then
        return 0
    fi
    if [[ -t 0 ]]; then
        if [[ -n "$timeout" ]]; then
            read -r -t "$timeout" -p "$prompt " answer || answer=""
        else
            read -r -p "$prompt " answer
        fi
    else
        # stdin is not a tty (e.g., piped), read from /dev/tty if possible
        if [[ -e /dev/tty ]]; then
            if [[ -n "$timeout" ]]; then
                read -r -t "$timeout" -p "$prompt " answer < /dev/tty || answer=""
            else
                read -r -p "$prompt " answer < /dev/tty
            fi
        else
            echo "$prompt (no tty, defaulting to No)" >&2
            return 1
        fi
    fi
    case "${answer,,}" in
        y|yes) return 0;;
        *) return 1;;
    esac
}

# Parse -y/--yes flag for non-interactive CI
CONFIRM_YES=0
while [[ $# -gt 0 ]]; do
    case "$1" in
        -y|--yes) CONFIRM_YES=1; shift;;
        *) break;;
    esac
done

# Example usage before deleting files
files=("file1.txt" "file2.txt")
echo "About to delete: ${files[*]}"
if confirm "Delete these files? [y/N]" 10; then
    rm -v -- "${files[@]}"
else
    echo "Aborted. No files deleted."
fi
```

**How do I use it?**
1. Save as `confirm_demo.sh`.
2. Make it executable: `chmod +x confirm_demo.sh`
3. Run:
     - `./confirm_demo.sh` (interactive prompt)
     - `./confirm_demo.sh -y` (skip prompt, auto-confirm)

**Tips for customization:**
- Adjust the prompt text for different actions.
- Set a timeout to default to No if no answer is given.
- Use the function before any destructive or critical operation.

**Common Pitfalls:**
- Not handling non-interactive (piped) input.
- Not defaulting to No on timeout or invalid input.
- Not supporting CI automation with a skip flag.

**Check Your Understanding:**
1. Why use `/dev/tty` when stdin is not a tty?
2. How does the `-y` flag help in automation?
3. What happens if the user does not respond within the timeout?

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

## 9.2 Variables and Parameter Management

**Beginner Section**


Variables and parameters are the building blocks of any shell script. In this section, you’ll learn how to store and use data, pass information to scripts, and manipulate values for automation.

**Best Practices:**
- Always use a shebang (`#!/usr/bin/env bash`) at the top.
- Use `set -euo pipefail` for safety.
- Quote all variable expansions: `"$var"`.

**Learning Objectives:**
- Understand how to declare and use variables in bash
- Use command-line arguments and special parameters
- Apply basic data manipulation techniques in scripts

**Why Variables Matter:**
Variables let you store information, reuse values, and make your scripts flexible. Parameters allow scripts to accept input and behave differently based on user needs.

---

### Greeting Script with Arguments (Beginner)

**Purpose:** Print a personalized greeting using a variable and command-line argument.

```bash
#!/usr/bin/env bash          # Shebang: use bash
set -euo pipefail            # Best practice: strict mode
name="${1:-Guest}"           # Set 'name' to first argument, or 'Guest' if none
echo "Welcome, $name!"        # Print a welcome message
```
# Run with: ./script.sh Alice
# Or: ./script.sh

**Common Pitfalls:**

**Common Pitfalls:**
- Forgetting to use quotes around variables (e.g., "$name")
- Not providing a default value for arguments
- Using `$1` without checking if it exists
- Using `set -euo pipefail` without understanding its effect (script exits on error/unset variable)

**Check Your Understanding:**
1. What does `${1:-Guest}` mean in this script?
2. How would you change the script to greet multiple names?
3. Why is it important to quote variables in bash?

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

## 9.3 Control Structures and Flow Control


Control structures let your scripts make decisions, repeat actions, and handle multiple scenarios. Mastering these patterns is essential for safe, reliable automation.

### Conditionals: `if`, `elif`, `else`

Use conditionals to test values, files, and strings. Prefer `[[ ... ]]` for Bash scripts—it supports regex, globbing, and avoids many quoting pitfalls.

**Numeric, string, and file tests:**

**Beginner Section**
**Purpose:** Demonstrate numeric, string, and file tests using conditionals.

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
num=5                         # Numeric variable
str="hello"                   # String variable
file="/etc/passwd"            # File path variable

if [[ $num -gt 3 ]]; then     # Numeric test
    echo "Number is greater than 3"
elif [[ -z "$str" ]]; then    # String test: empty
    echo "String is empty"
elif [[ -f "$file" && -r "$file" ]]; then  # File test: exists and readable
    echo "File exists and is readable"
else
    echo "No conditions met"
fi
```

- `-f` (file exists), `-d` (directory), `-x` (executable), `-n` (non-empty string), `-z` (empty string).

**Common Pitfalls:**
- Forgetting to quote variables in tests (e.g., `-z $str`)
- Using `[ ... ]` instead of `[[ ... ]]` for complex tests
- Not checking file readability before reading
- Using `=` for numeric comparison instead of `-eq`, `-gt`, etc.

### Why Prefer `[[ ... ]]` Over `[ ... ]`


**Beginner Section**
**Purpose:** Show why `[[ ... ]]` is safer and more powerful for regex and glob matching.

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
input="error42"               # Example input string
if [[ $input =~ ^error[0-9]+$ ]]; then  # Regex match
    echo "Input matches error pattern"
fi

file="notes.txt"              # Example file name
if [[ $file == *.txt ]]; then  # Glob match
    echo "It's a text file"
fi
```

### `case` Statement for Subcommands


**Intermediate Section**
**Purpose:** Use `case` to handle multiple actions or subcommands cleanly.

**Subcommand handler:**
```bash
#!/usr/bin/env bash
action="${1:-status}"
case "$action" in
    start) echo "Starting service...";;
    stop) echo "Stopping service...";;
    status) echo "Checking status...";;
    *) echo "Usage: $0 {start|stop|status}";;
esac
```

### Safe Loop Patterns

**Beginner Section**
**Purpose:** Show safe ways to loop over arrays and files in Bash.

#### Iterate Arrays
Always quote `"${arr[@]}"` to avoid word-splitting.

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
arr=("one" "two" "three")      # Array of items
for item in "${arr[@]}"; do     # Safe array iteration
    echo "Item: $item"           # Print each item
done
```

**Common Pitfalls:**
- Forgetting to quote `"${arr[@]}"` (can break on spaces)
- Using `for item in $arr` instead of `for item in "${arr[@]}"`

#### Read Lines Safely


**Purpose:** Safely read lines from a file, handling all edge cases.

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
while IFS= read -r line || [[ -n "$line" ]]; do  # Safe line reading
    echo "Line: $line"           # Print each line
done < "/etc/passwd"
```

**Common Pitfalls:**
- Not using `IFS= read -r` (can break on spaces/backslashes)
- Loop misses last line if file doesn't end with newline

#### File Iteration with `nullglob` or `find`


**Purpose:** Safely iterate over files in a directory.

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
shopt -s nullglob             # Avoid errors if no files match
for f in /var/log/*.log; do   # Loop over .log files
    echo "Log file: $f"        # Print file name
done
```

Or with `find` and `-print0` for robust handling:

```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Best practice: strict mode
find /var/log -name "*.log" -print0 | while IFS= read -r -d '' file; do
    echo "Found: $file"        # Print file name
done
```

**Common Pitfalls:**
- Not enabling `nullglob` (loop runs with literal '*.log' if no files)
- Not quoting `$f` if filenames have spaces

### Real-World Example: Summarize Top 5 Log Messages

This script counts and displays the top 5 most frequent messages in all `/var/log/*.log` files.

```bash
#!/usr/bin/env bash
shopt -s nullglob
declare -A msg_count

for logfile in /var/log/*.log; do
    while IFS= read -r line; do
        msg="${line:0:50}"  # Use first 50 chars as summary
        ((msg_count["$msg"]++))
    done < "$logfile"
done

for msg in "${!msg_count[@]}"; do
    echo "${msg_count[$msg]} $msg"
done | sort -rn | head -5
```
- Uses associative arrays, safe line reading, and sorts by frequency.
- Demonstrates loops, conditionals, and quoting.

## 9.4 Functions and Modular Programming


> **Beginner/Intermediate**

**Purpose:** Functions let you reuse code, encapsulate logic, and structure scripts for clarity and reliability. Modular scripts are easier to maintain and debug.

**Best Practices:**
- Use functions for repeated logic.
- Use `local` for variables inside functions to avoid polluting global scope.
- Use clear, descriptive function names.
- Keep functions short and focused.

**Common Pitfalls:**
- Forgetting to quote arguments (`"$1"`, `"$@"`).
- Not using `local` for function variables (can cause bugs).

### Function Definitions and Calls


Define a function with a name and curly braces. Use `local` for variables that should not leak outside the function.

```bash
#!/usr/bin/env bash           # Shebang: use bash
greet() {
    local name="$1"           # Only visible inside greet
    echo "Hello, $name!"      # Print greeting
}
greet "Sysadmin"              # Call function with argument
```

### Handling Arguments: `$1`, `$@`, `"$@"`, Arrays


Functions can accept arguments like scripts. Use `$1`, `$2`, or `"$@"` for all arguments. Arrays are useful for lists.

```bash
print_args() {
    for arg in "$@"; do         # Loop over all arguments
        echo "Arg: $arg"         # Print each argument
    done
}
print_args one two three         # Call with multiple args

arr=("apple" "banana" "cherry")
print_args "${arr[@]}"           # Call with array
```

### Returning Data: `echo`/`printf` and Capturing Output


Use `echo` or `printf` to return data. Capture with command substitution.

```bash
add() {
    echo "$(( $1 + $2 ))"      # Output result
}
result="$(add 2 3)"             # Capture output
echo "Sum: $result"              # Print sum
```

### Return Codes vs Data


Use `return` for status codes (0=success, nonzero=failure). Use output for data.

```bash
is_file() {
    [[ -f "$1" ]]                # Returns 0 if file exists
}
if is_file "/etc/passwd"; then
    echo "File exists"
else
    echo "File missing"
fi
```

### Reusable Helpers

**Logging with timestamps and levels:**
```bash
log() {
    local level="$1"; shift
    printf '%s [%s] %s\n' "$(date '+%Y-%m-%d %H:%M:%S')" "$level" "$*"
}
log INFO "Script started"
log WARN "Low disk space"
log ERROR "Fatal error occurred"
```

**Fatal error helper:**
```bash
die() {
    log ERROR "$*" >&2
    exit 1
}
# die "Missing required argument"
```

### Modular Script Structure


Organize scripts into sections: constants, globals, functions, main logic.

```bash
#!/usr/bin/env bash           # Shebang: use bash
# Constants
readonly DEFAULT_FILE="/etc/passwd"

# Globals
VERBOSE=0

# Functions
log() { local level="$1"; shift; printf '%s [%s] %s\n' "$(date '+%H:%M:%S')" "$level" "$*"; }
die() { log ERROR "$*" >&2; exit 1; }

main() {
    log INFO "Main logic starts"
    # ...main script code...
}

# Entry point
main "$@"
```

### Argument Parsing with `getopts`


Use `getopts` for flags and options. This example parses `-f file -t threshold -v`.

```bash
#!/usr/bin/env bash           # Shebang: use bash
file=""
threshold=80
VERBOSE=0

while getopts ":f:t:v" opt; do
    case "$opt" in
        f) file="$OPTARG";;        # -f: file argument
        t) threshold="$OPTARG";;   # -t: threshold argument
        v) VERBOSE=1;;              # -v: verbose flag
        *) die "Usage: $0 [-f file] [-t threshold] [-v]";;
    esac
done
shift $((OPTIND-1))

log INFO "File: $file, Threshold: $threshold, Verbose: $VERBOSE"
```

### Example: Function Reuse Across Two Tasks

```bash
#!/usr/bin/env bash           # Shebang: use bash
log() { local level="$1"; shift; printf '%s [%s] %s\n' "$(date '+%H:%M:%S')" "$level" "$*"; }

count_lines() {
    local file="$1"
    local count=0
    while IFS= read -r _; do ((count++)); done < "$file"
    echo "$count"
}

main() {
    log INFO "Counting lines in /etc/passwd"
    lines="$(count_lines /etc/passwd)"
    log INFO "Line count: $lines"

    log INFO "Counting lines in /etc/group"
    lines="$(count_lines /etc/group)"
    log INFO "Line count: $lines"
}

main "$@"
```

---

### Lab: Modularize a Script

**Objective:** Refactor a script to use functions for clarity and reuse.

**Steps:**
1. Write a script that prints the number of lines in two files.
2. Refactor the logic into a reusable function.
3. Add logging for each step.

**Hint:** Use a function that takes a filename and returns the line count.

<details>
<summary>Solution</summary>

```bash
#!/usr/bin/env bash
log() { local level="$1"; shift; printf '%s [%s] %s\n' "$(date '+%H:%M:%S')" "$level" "$*"; }

count_lines() {
    local file="$1"
    local count=0
    while IFS= read -r _; do ((count++)); done < "$file"
    echo "$count"
}

main() {
    log INFO "Counting lines in /etc/passwd"
    lines="$(count_lines /etc/passwd)"
    log INFO "Line count: $lines"

    log INFO "Counting lines in /etc/group"
    lines="$(count_lines /etc/group)"
    log INFO "Line count: $lines"
}

main "$@"
```

</details>

---

## 9.5 Error Handling and Debugging


> **Beginner/Intermediate**

**Purpose:** Error handling and debugging make scripts reliable and safe for automation. Bash provides strict modes, traps, and tracing tools to help you catch and fix problems early.

**Best Practices:**
- Always enable strict mode (`set -euo pipefail`) at the top of scripts.
- Use `trap` to clean up resources on exit or interruption.
- Check exit codes and handle errors explicitly.
- Use logging for errors and important events.

**Common Pitfalls:**
- Forgetting to set strict mode (silent failures, hard-to-find bugs).
- Not cleaning up temporary files or resources.
- Not quoting variables (can cause unexpected errors).

### Strict Mode: `set -euo pipefail`


Enable strict mode at the top of your script:
```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Strict mode: safer scripts
# -e: exit on error
# -u: error on unset variables
# -o pipefail: fail if any command in a pipeline fails
```

**Caveats:**
- In `if` statements, use `if command; then ...` (don't rely on `set -e` inside `if`).
- Use `|| true` to ignore errors intentionally: `command || true`.
- In subshells, strict mode may not propagate; set it inside subshells if needed.

### Traps for Cleanup


Use `trap` to clean up resources on exit or interruption.
```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Strict mode
tmpdir="$(mktemp -d)"         # Create temp directory
trap 'rm -rf "$tmpdir"; echo "Cleaned up $tmpdir"' EXIT INT TERM  # Cleanup on exit
echo "Working in $tmpdir"      # Main logic
false                         # Intentional failure
# On exit, trap runs and cleans up temp dir
```

### Inspecting Exit Codes and Pipeline Failures


Check the exit code of the last command with `$?`.
```bash
#!/usr/bin/env bash           # Shebang: use bash
ls /notfound                  # Command that fails
code=$?                       # Capture exit code
echo "ls exited with code $code"  # Print exit code
```
With `set -o pipefail`, failures in any part of a pipeline are surfaced:
```bash
#!/usr/bin/env bash           # Shebang: use bash
set -o pipefail               # Fail if any command in pipeline fails
grep "foo" /notfound | sort   # Will exit nonzero if grep fails
# Will exit nonzero if grep fails
```

### Debugging Techniques


Enable tracing for the whole script or just a function:
```bash
#!/usr/bin/env bash           # Shebang: use bash
set -x                        # Trace all commands
echo "Debugging..."           # Debug output
set +x                        # Stop tracing
```
Or run with tracing:
```bash
bash -x script.sh             # Run script with tracing
```
Targeted tracing inside a function:
```bash
myfunc() {
    set -x                    # Enable tracing
    echo "Inside function"     # Debug output
    set +x                    # Disable tracing
}
myfunc
```

### ShellCheck: Lint Your Scripts


Install ShellCheck (if not present):
```bash
sudo apt-get install shellcheck  # Debian/Ubuntu
# or
brew install shellcheck          # macOS
```
Run ShellCheck to find issues:
```bash
shellcheck script.sh             # Lint script for errors
```
Address warnings for safer scripts.

### Minimal Example: Temp Dir, Trap, Failure, Cleanup


```bash
#!/usr/bin/env bash           # Shebang: use bash
set -euo pipefail             # Strict mode
tmpdir="$(mktemp -d)"         # Create temp directory
trap 'rm -rf "$tmpdir"; echo "Cleaned up $tmpdir"' EXIT  # Cleanup on exit
echo "Created $tmpdir"         # Main logic
false                         # Simulate failure
```

---

### Lab: Add Robust Error Handling

**Objective:** Refactor a script to use strict mode, traps, and logging for error handling.

**Steps:**
1. Write a script that creates a temp file and writes to it.
2. Add strict mode and a trap to clean up the temp file on exit.
3. Add logging for each step and error.

**Hint:** Use `set -euo pipefail`, `trap`, and a `log` function.

<details>
<summary>Solution</summary>

```bash
#!/usr/bin/env bash
set -euo pipefail
tmpfile="$(mktemp)"
trap 'rm -f "$tmpfile"; echo "Cleaned up $tmpfile"' EXIT INT TERM

log() { local level="$1"; shift; printf '%s [%s] %s\n' "$(date '+%H:%M:%S')" "$level" "$*"; }

log INFO "Writing to $tmpfile"
echo "Hello, world!" > "$tmpfile"
log INFO "Contents: $(cat "$tmpfile")"

# Simulate error
false || log ERROR "An error occurred"

# On exit, trap runs and cleans up temp file
```

</details>
---

### 4. File Line Counter (Beginner)



**What does this script do?**
This script safely counts the number of lines in a file provided by `-f <file>` or as the first argument. It validates input and handles errors gracefully.

```bash
#!/usr/bin/env bash
set -euo pipefail

usage() {
    echo "Usage: $0 -f <file>" >&2
    exit 1
}

# Parse -f or positional argument
file=""
if [[ "${1:-}"" == "-f" ]]; then
    file="${2:-}"
    shift 2
elif [[ -n "${1:-}" ]]; then
    file="$1"
    shift
else
    usage
fi

if [[ ! -r "$file" || ! -f "$file" ]]; then
    echo "Error: File '$file' does not exist or is not readable." >&2
    usage
fi

lines=$(wc -l < "$file")
echo "Total lines: $lines"
```

**How do I use it?**
1. Save as `count_lines.sh`.
2. Make it executable: `chmod +x count_lines.sh`
3. Run: `./count_lines.sh -f /etc/passwd` or `./count_lines.sh /etc/passwd`

**Sample Output:**
```
Total lines: 42
```

**Check Your Understanding:**
1. Why do we check both `-f` and `-r` for the file?
2. What does `wc -l < "$file"` do?
3. How does the script handle missing or unreadable files?

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

---

### 5. Disk Space Warning (Intermediate)


or

**What does this script do?**
Checks disk usage for one or more mount points and warns if usage exceeds a threshold.

```bash
#!/usr/bin/env bash
set -euo pipefail

log() { local level="$1"; shift; echo "[$level] $*"; }
die() { log ERROR "$*" >&2; exit 1; }

mounts=("/")
threshold=80
quiet=0

# Parse flags: -m mount1,mount2 -t threshold -q
while getopts ":m:t:q" opt; do
    case "$opt" in
        m) IFS=',' read -r -a mounts <<< "$OPTARG";;
        t) threshold="$OPTARG";;
        q) quiet=1;;
        *) die "Usage: $0 [-m mount1,mount2] [-t threshold] [-q]";;
    esac
done
shift $((OPTIND-1))

exceeded=0
for mnt in "${mounts[@]}"; do
    usage=$(df -P "$mnt" | awk 'NR==2 {gsub("%",""); print $5}')
    if [[ "$usage" =~ ^[0-9]+$ ]] && (( usage > threshold )); then
        ((quiet==0)) && log WARN "$mnt usage is ${usage}% (threshold: $threshold%)"
        exceeded=1
    else
        ((quiet==0)) && log INFO "$mnt usage is ${usage}% (OK)"
    fi
done

exit $exceeded
```

**How do I use it?**
1. Save as `disk_space_check.sh`.
2. Make it executable: `chmod +x disk_space_check.sh`
3. Run:
     - `./disk_space_check.sh` (checks `/` at 80%)
     - `./disk_space_check.sh -m /,/home -t 75` (checks `/` and `/home` at 75%)
     - `./disk_space_check.sh -q` (quiet mode)

**Sample Output:**
```
[INFO] / usage is 42% (OK)
[WARN] /home usage is 82% (threshold: 75%)
```

**Check Your Understanding:**
1. How does the script handle multiple mount points?
2. What does the `exceeded` variable do?
3. Why use `df -P` and `awk` for extracting usage?

---

### 6. Batch File Renamer (Intermediate)



**What does this script do?**
Renames files in a directory by adding a prefix, suffix, or changing extension. Supports dry-run mode and safe file iteration.

```bash
#!/usr/bin/env bash
set -euo pipefail

usage() {
    echo "Usage: $0 [-d dir] [-p prefix] [-s suffix] [-e new_ext] [-n]" >&2
    exit 1
}

dir="."
prefix=""
suffix=""
new_ext=""
dryrun=0

while getopts ":d:p:s:e:n" opt; do
    case "$opt" in
        d) dir="$OPTARG";;
        p) prefix="$OPTARG";;
        s) suffix="$OPTARG";;
        e) new_ext="$OPTARG";;
        n) dryrun=1;;
        *) usage;;
    esac
done
shift $((OPTIND-1))

if [[ ! -d "$dir" ]]; then
    echo "Error: Directory '$dir' does not exist." >&2
    usage
fi

log() { echo "[INFO] $*"; }
die() { echo "[ERROR] $*" >&2; exit 1; }

find "$dir" -maxdepth 1 -type f -print0 | while IFS= read -r -d '' file; do
    base="$(basename "$file")"
    ext=""
    name="$base"
    if [[ "$base" == *.* ]]; then
        ext=".${base##*.}"
        name="${base%$ext}"
    fi
    newname="$prefix$name$suffix"
    if [[ -n "$new_ext" ]]; then
        newname+=".$new_ext"
    else
        newname+="$ext"
    fi
    src="$file"
    dst="$dir/$newname"
    if [[ "$src" == "$dst" ]]; then
        log "Skipping $src (no change)"
        continue
    fi
    if (( dryrun )); then
        log "Would rename '$src' -> '$dst'"
    else
        mv -- "$src" "$dst"
        log "Renamed '$src' -> '$dst'"
    fi
done
```

**How do I use it?**
1. Save as `batch_rename.sh`.
2. Make it executable: `chmod +x batch_rename.sh`
3. Run:
     - `./batch_rename.sh -d . -p new_` (add prefix)
     - `./batch_rename.sh -d . -s _bak` (add suffix)
     - `./batch_rename.sh -d . -e bak` (change extension)
     - `./batch_rename.sh -d . -p new_ -s _bak -e txt` (all options)
     - `./batch_rename.sh -d . -e bak -n` (dry-run)

**Sample Output:**
```
[INFO] Would rename './notes.txt' -> './new_notes_bak.txt'
[INFO] Renamed './data.txt' -> './new_data_bak.txt'
```

**Check Your Understanding:**
1. Why use `find ... -print0` and `while IFS= read -r -d ''`?
2. How does dry-run mode help prevent mistakes?
3. What happens if the source and destination names are the same?


### 7. Service Manager (Intermediate)

**What does this script do?**
Checks and manages a systemd service (default: `ssh`). Supports status, start, stop, and restart subcommands with robust error handling and clear output.

```bash
#!/usr/bin/env bash
set -euo pipefail

usage() {
    echo "Usage: $0 [-s service] {status|start|stop|restart}" >&2
    echo "  -s service   Service name (default: ssh)" >&2
    echo "  Subcommands: status, start, stop, restart" >&2
    echo "Examples:" >&2
    echo "  $0 status" >&2
    echo "  $0 -s nginx restart" >&2
    exit 1
}

service="ssh"

while getopts ":s:" opt; do
    case "$opt" in
        s) service="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

if [[ $# -ne 1 ]]; then
    usage
fi

cmd="$1"

case "$cmd" in
    status)
        if systemctl --quiet is-active "$service"; then
            echo "[OK] Service '$service' is active."
            systemctl status "$service"
        else
            echo "[FAIL] Service '$service' is not active." >&2
            systemctl status "$service" || true
            exit 3
        fi
        ;;
    start|stop|restart)
        if sudo systemctl "$cmd" "$service"; then
            echo "[OK] '$cmd' succeeded for service '$service'."
        else
            echo "[FAIL] '$cmd' failed for service '$service'." >&2
            exit 2
        fi
        ;;
    *)
        usage
        ;;
esac
```

**How do I use it?**
1. Save as `service_manager.sh`.
2. Make it executable: `chmod +x service_manager.sh`
3. Run:
     - `./service_manager.sh status` (check status of ssh)
     - `./service_manager.sh -s nginx restart` (restart nginx)
     - `./service_manager.sh -s cron stop` (stop cron)

**Notes:**
- Some actions (start/stop/restart) may require `sudo` privileges.
- Service names are case-sensitive and must exist.
- Exit codes: 0=success, 2=action failed, 3=service not active.

**Sample Output:**
```
[OK] Service 'ssh' is active.
● ssh.service - OpenSSH server daemon
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since ...

[OK] 'restart' succeeded for service 'nginx'.
```

**Check Your Understanding:**
1. Why use `systemctl --quiet is-active` before showing status?
2. What exit code signals a failed action?
3. Why might you need `sudo` for some subcommands?

 [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

### 8. Log File Analyzer (Intermediate)

**What does this script do?**
Scans a log file for patterns (default: error|failed), summarizes counts by hour or top offenders, and displays results in columns. Robust input validation and fallback for missing hour tokens.

```bash
#!/usr/bin/env bash
set -euo pipefail

usage() {
    echo "Usage: $0 -f file [-p 'pattern'] [-n top]" >&2
    echo "  -f file     Log file to analyze (required)" >&2
    echo "  -p pattern  Pattern to match (default: error|failed)" >&2
    echo "  -n top      Show top N results (default: 10)" >&2
    echo "Examples:" >&2
    echo "  $0 -f /var/log/auth.log -p 'invalid|fail' -n 5" >&2
    exit 1
}

file=""
pattern="error|failed"
top=10

while getopts ":f:p:n:" opt; do
    case "$opt" in
        f) file="$OPTARG";;
        p) pattern="$OPTARG";;
        n) top="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

if [[ -z "$file" || ! -r "$file" ]]; then
    echo "Error: Must specify a readable log file with -f." >&2
    usage
fi

# Try to extract hour token (field 3) or fallback to full line
grep -Ei "$pattern" "$file" | awk '{if (NF>=3) print $3; else print $0}' | \
    sort | uniq -c | sort -nr | head -n "$top" | awk '{printf "%-8s %s\n", $1, $2}'

# If log format is not standard, fallback to top offenders (IP, user, etc.)
# Example: grep -Ei "$pattern" "$file" | awk '{print $NF}' | sort | uniq -c | sort -nr | head -n "$top"
```

**How do I use it?**
1. Save as `log_analyzer.sh`.
2. Make it executable: `chmod +x log_analyzer.sh`
3. Run:
     - `./log_analyzer.sh -f /var/log/syslog` (default pattern)
     - `./log_analyzer.sh -f /var/log/auth.log -p 'invalid|fail' -n 5` (custom pattern/top)

**Sample Output:**
```
12       10:00
5        11:00
2        12:00
```

**Tips for customization:**
- Change the pattern to match other keywords (e.g., "warning", "denied").
- Summarize by user/IP: change awk field to `$NF` or another relevant field.
- Adjust column formatting in the final awk for readability.

**Common Pitfalls:**
- Log file format may vary; field positions may change.
- Not all logs have a timestamp in the third field—fallback prints the whole line.

**Check Your Understanding:**
1. What does `awk '{if (NF>=3) print $3; else print $0}'` do?
2. How would you change the pattern to match "denied"?
3. Why is it important to validate the log file before processing?

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

---

### 9. Interactive Confirmation (Intermediate)

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

**A Guide to Customizing This Template:**
Start every new script with this template! It provides strict error handling, safe input parsing, logging, cleanup, and a clear main() entry point. Fill in the TODOs and adjust functions as needed for your task.

```bash
#!/usr/bin/env bash
# Robust Script Template (Intermediate)
# -------------------------------------
# - Strict mode: safer scripts
# - Usage, logging, error handling, cleanup
# - getopts scaffolding for flags
# - main() entry point
# - Passes shellcheck with zero errors
#
# How to use:
# 1. Copy this template to start a new script.
# 2. Fill in TODOs for your logic, input validation, and safe patterns.
# 3. Use functions for organization and maintainability.

set -euo pipefail
IFS=$'\n\t' # Safer word splitting for arrays/loops

usage() {
    cat <<EOF
Usage: $0 [-f file] [-v] [-h]
    -f file   Input file (required)
    -v        Verbose output
    -h        Show this help
EOF
    exit 1
}

log() {
    # Usage: log LEVEL MESSAGE
    local level="$1"; shift
    printf '[%s] %s\n' "$level" "$*"
}

die() {
    log ERROR "$*" >&2
    exit 1
}

cleanup() {
    # Cleanup resources on exit or error
    log INFO "Cleaning up..."
    # TODO: Remove temp files, close FDs, etc.
}
trap cleanup EXIT

# Argument parsing scaffold
file=""
verbose=0
while getopts ":f:vh" opt; do
    case "$opt" in
        f) file="$OPTARG";;
        v) verbose=1;;
        h) usage;;
        *) usage;;
    esac
done
shift $((OPTIND-1))

# Input validation example
if [[ -z "$file" ]]; then
    die "Input file (-f) is required."
fi
if [[ ! -r "$file" ]]; then
    die "File '$file' is not readable."
fi

main() {
    log INFO "Script started"

    # Safe loop example: read lines from file
    while IFS= read -r line || [[ -n "$line" ]]; do
        # TODO: Process each line safely
        [[ $verbose -eq 1 ]] && log INFO "Line: $line"
    done < "$file"

    # Safe conditional example
    if [[ $verbose -eq 1 ]]; then
        log INFO "Verbose mode enabled"
    fi

    log INFO "Script completed"
}

main "$@"
```

**Common Pitfalls:**
- Forgetting strict mode (`set -euo pipefail`, `IFS`)
- Not validating inputs before use
- Not using functions for organization
- Not handling errors and cleanup with traps

**Check Your Understanding:**
1. What does `set -euo pipefail` do?
2. Why use `IFS=$'\n\t'`?
3. How does the `trap cleanup EXIT` pattern help?
4. Why is input validation important?

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

 [Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

These examples reinforce the concepts covered in this module and provide a foundation for building more advanced scripts. Try modifying and combining them to automate your own tasks.

## Best Practices


Writing readable, safe, and maintainable Bash scripts is essential for reliability, security, and teamwork. Best practices help prevent bugs, make scripts easier to review, and protect systems from mistakes. See earlier sections for practical examples: [Robust Script Template](#10-robust-script-template-intermediate), [Error Handling](#95-error-handling-and-debugging), [Functions](#94-functions-and-modular-programming), and [Safe Loops](#safe-loop-patterns).

---

### 1. Script Development Standards
#### Script Development Standards: Checklist

- **Shebang:** Always use `#!/usr/bin/env bash` as the first line.
- **Strict Mode:** Add `set -euo pipefail` and `IFS=$'\n\t'` after the shebang.
- **Structure:**
    - Place constants/globals at the top.
    - Define all functions next.
    - End with a `main()` function and call: `main "$@"`
- **Naming Conventions:**
    - Use lowercase_with_underscores for variables.
    - Use descriptive names for functions; always use `local` for function variables.
        ```bash
        my_func() {
            local result=""
            # ...
        }
        ```
- **Documentation:**
    - Add a header comment with purpose, usage, author, last updated.
    - Use inline comments for non-obvious logic.
        ```bash
        # Purpose: Cleans up temp files
        # Usage: ./cleanup.sh /tmp/file
        # Author: Your Name, Last updated: 2025-08-09
        ```
- **Tooling:**
    - Run `shellcheck` for linting and optionally `shfmt` for formatting.

### 2. Error Handling & Logging
- **Strict Mode:** Always use `set -euo pipefail` and safe IFS. See [Error Handling](#95-error-handling-and-debugging).
- **Traps:** Use `trap cleanup EXIT` for resource cleanup.
    ```bash
    trap cleanup EXIT
    cleanup() { rm -f "$tmpfile"; }
    ```
- **Logging:** Use a `log()` function for info and errors.
    ```bash
    log() { printf '[%s] %s\n' "$1" "$2"; }
    log INFO "Starting..."
    ```
- **Exit Codes:** Return non-zero exit codes on failure.

### 3. Security & Maintainability
- **Quoting:** Always quote variables: `"$var"`.
- **Safe Loops:** Use `while IFS= read -r` for reading files. See [Safe Loop Patterns](#safe-loop-patterns).
- **Least Privilege:** Avoid running scripts as root unless necessary.
- **Sanitize Inputs:** Validate and sanitize user input.
- **ShellCheck:** Lint scripts with `shellcheck` before use.
- **Version Control:** Track scripts in git for history and collaboration.

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

### Script Development Standards
- **Structure and Organization**: Use consistent script structure with clear sections for configuration, functions, and main logic
- **Error Handling**: Implement comprehensive error handling with set -euo pipefail and custom error functions
- **Logging**: Provide multiple logging levels with timestamps and structured output
- **Documentation**: Include comprehensive inline comments and usage documentation
- **Testing**: Develop test suites for all critical functions and error scenarios
- **Security**: Validate all inputs, sanitize data, and follow security best practices

### Performance Optimization

#### Performance Optimization: Efficient Bash Scripting

- **Prefer Built-ins:** Use Bash built-ins and arrays for speed.
    - Before: `cat file | while read ...`  
        After: `while read ... < file`
    - Before: `for f in $(ls *.txt); do ...`  
        After: `for f in *.txt; do ...`
- **Use `mapfile -t` for Large Inputs:**
    ```bash
    mapfile -t lines < bigfile.txt
    for line in "${lines[@]}"; do ...; done
    ```
- **Avoid UUOC (Useless Use of Cat):**
    - Before: `cat file | grep pattern`
        After: `grep pattern file`
- **Combine grep/awk/sed:**
    - Before: `grep pattern file | awk '{print $1}' | sort | uniq`
        After: `awk '/pattern/ {print $1}' file | sort | uniq`
- **NUL-safe Pipelines for Large File Sets:**
    ```bash
    find . -type f -print0 | xargs -0 rm
    ```
- **Batch Operations:**
    - Before: `for f in *.log; do gzip "$f"; done`
        After: `gzip *.log`
- **Avoid Subshells in Tight Loops:**
    - Before: `for f in *.txt; do echo $(basename "$f"); done`
        After: `for f in *.txt; do basename "$f"; done`

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

### Security Considerations

#### Security Considerations: Safe Bash Patterns

- **Always Quote Variables:**
    - Caution: Unquoted variables can cause word-splitting and globbing bugs.
        ```bash
        rm -- "$filename"   # Safe
        # rm -- $filename   # Unsafe
        ```
- **Avoid `eval`:**
    - Caution: `eval` can execute unintended code. Prefer explicit logic.
- **Validate User Input and Filenames:**
    - Example: Check for valid characters and existence.
        ```bash
        [[ "$user" =~ ^[a-zA-Z0-9_-]+$ ]] || die "Invalid username"
        [[ -f "$file" ]] || die "File not found"
        ```
- **Restrictive File Permissions:**
    - Example: Create temp files/dirs securely.
        ```bash
        tmpdir="$(mktemp -d)"   # Secure temp dir
        touch "$tmpdir/log" && chmod 600 "$tmpdir/log"
        ```
- **Handle Secrets Securely:**
    - Caution: Never hardcode secrets. Use environment variables or external secret stores.
        ```bash
        api_key="${API_KEY:-}"   # From environment
        ```
- **Avoid Globbing/Word-Splitting Pitfalls:**
    - Prefer arrays and safe IFS.
        ```bash
        IFS=$'\n\t'
        files=("*.log")
        for f in "${files[@]}"; do ...; done
        ```

[Back to Top](#table-of-contents)⬆️ | [Main Index](README.md)📚

## Troubleshooting


Effective troubleshooting means systematically reproducing, isolating, instrumenting, fixing, and verifying issues. Start by reproducing the problem, isolate the cause, add debug output or use `set -x`, apply a fix, and verify the result. For specific tactics and examples, see the subsections below: Common Scripting Issues and Debugging Techniques.

### Common Scripting Issues


- **Unset Variables:**
    - Problem:
        ```bash
        echo $not_set   # Expands to empty, may cause bugs
        ```
    - Fix:
        ```bash
        set -u          # Error on unset variables
        echo "${not_set:-default}"  # Provide a default
        ```

- **Unquoted Expansions:**
    - Problem:
        ```bash
        rm $file        # Fails if $file contains spaces
        ```
    - Fix:
        ```bash
        rm -- "$file"  # Always quote expansions
        ```

- **Globbing Surprises:**
    - Problem:
        ```bash
        for f in $dir/*; do ...; done  # Fails if no matches
        ```
    - Fix:
        ```bash
        shopt -s nullglob
        for f in "$dir"/*; do ...; done
        ```

- **Incorrect Tests (`=` vs `-eq`):**
    - Problem:
        ```bash
        if [ "$count" = 5 ]; then ...  # Wrong for numbers
        ```
    - Fix:
        ```bash
        if [ "$count" -eq 5 ]; then ...  # Use -eq for numbers
        ```

- **Broken Loops:**
    - Problem:
        ```bash
        while read line; do ...; done < file  # Loses last line if no newline
        ```
    - Fix:
        ```bash
        while IFS= read -r line || [[ -n "$line" ]]; do ...; done < file
        ```

- **Subshell Gotchas:**
    - Problem:
        ```bash
        echo "foo" | while read line; do var=1; done
        echo $var  # var is unset (set in subshell)
        ```
    - Fix:
        ```bash
        while read line; do var=1; done < <(echo "foo")
        echo $var  # var is set (no subshell)
        ```

### Debugging Techniques


- **Selective Debug Mode:**
    ```bash
    set -x         # Enable debug for next lines
    do_work        # Trace this function
    set +x         # Disable debug
    ```

- **Custom PS4 for Richer Traces:**
    ```bash
    export PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]:+${FUNCNAME[0]}():} '
    set -x
    run_task
    set +x
    ```

- **Print Variable States Safely:**
    ```bash
    printf '%q\n' "$var"   # Shows value with escapes
    declare -p arr           # Print array contents
    ```

- **Trap for Error Reporting:**
    ```bash
    trap 'echo "err at line $LINENO"' ERR
    # Pros: Immediate error location; Cons: May not catch all failures in pipelines
    ```

- **Test Functions in Isolation:**
    ```bash
    my_func() { echo "Hello $1"; }
    my_func "World"   # Run just this function
    ```

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


- **Argument with spaces:**
    - Fix: `echo "$1"`
- **Script not executable:**
    - Fix: `chmod +x script.sh`
- **Command not found:**
    - Fix: Use full path: `/usr/bin/awk ...` or check `echo $PATH`
- **Permission denied:**
    - Fix: `sudo ...` or `chmod 600 file`
- **Temporary file safety:**
    - Fix: `tmpfile="$(mktemp)"`
- **Forgotten cleanup:**
    - Fix: `trap 'rm -f "$tmpfile"' EXIT`
- **Array declaration:**
    - Fix: `declare -a arr=(one two)`
- **Associative array:**
    - Fix: `declare -A map=([key]=val)`
- **Unset variable error:**
    - Fix: `set -u` or use default: `${var:-default}`
- **Loop loses last line:**
    - Fix: `while IFS= read -r line || [[ -n "$line" ]]; do ...; done < file`
- **Debugging:**
    - Fix: `set -x` (enable), `set +x` (disable)

### Example: Debugging a Script


Let's debug a script with several common mistakes. We'll walk through reproducing the issue, tracing with `set -x`, inspecting exit codes, and applying fixes.

#### 1. The Buggy Script
```bash
#!/usr/bin/env bash
file=$1
grep error $file | awk '{print $2}' | sort | uniq -c > summary.txt
echo "Summary written to summary.txt"
cat summary.txt
```
**Problems:**
- Unquoted `$file` (fails on spaces)
- No file existence/readability check
- Pipeline fails silently if `grep` finds nothing

#### 2. Reproduce the Issue
Run with a missing or unreadable file, or a filename with spaces:
```bash
$ ./buggy.sh "my log.txt"
grep: my: No such file or directory
grep: log.txt: No such file or directory
cat: summary.txt: No such file or directory
```

#### 3. Add Debugging
Enable tracing and inspect exit codes:
```bash
set -x
file=$1
grep error $file | awk '{print $2}' | sort | uniq -c > summary.txt
rc=$?
echo "Exit code: $rc"
cat summary.txt
set +x
```
Output shows where the failure occurs.

#### 4. Apply Guards and Quoting
Add file checks and quote variables:
```bash
#!/usr/bin/env bash
set -euo pipefail
file=${1:-}
if [[ -z "$file" || ! -r "$file" ]]; then
    echo "Error: Must provide a readable file." >&2
    exit 1
fi
grep error "$file" | awk '{print $2}' | sort | uniq -c > summary.txt || {
    echo "No errors found."; exit 2;
}
echo "Summary written to summary.txt"
cat summary.txt
```

#### 5. Verify the Fix
Run again with a valid file:
```bash
$ ./fixed.sh "my log.txt"
Summary written to summary.txt
2 error1
1 error2
```
If no errors are found:
```bash
$ ./fixed.sh empty.txt
No errors found.
```

**Learning Points:**
- Always quote variables and check file existence.
- Use `set -x` and exit codes to trace failures.
- Guard pipelines and handle empty results.

**Common Pitfalls:**
- Not providing a default value for arguments
- Forgetting to enable debug mode when troubleshooting
- Not quoting variables in echo statements

**Check Your Understanding:**
1. What does `set -x` do in a script?
2. How can you make sure your script always greets someone, even if no argument is given?
3. Why is quoting variables important in echo statements?

### When to Ask for Help


When seeking help, provide clear diagnostics and context. Include:

- Script snippet (relevant lines, not the whole file)
- Exact command used to run the script
- OS and Bash version (`uname -a`, `bash --version`)
- Full, exact error messages (copy-paste)
- What you tried already (fixes, changes)
- Sanitized logs or sample input/output
- Output from `shellcheck` (if available)

This helps others diagnose your issue quickly and provide effective solutions.


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


**Practical Example: Backup Script with Rotation**

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

usage() {
    echo "Usage: $0 -s src_dir -d dest_dir [-k keep_count]" >&2
    exit 1
}

log() { printf '[%s] %s\n' "$(date +%F\ %T)" "$*"; }
die() { log "ERROR: $*" >&2; exit 1; }

src=""
dest=""
keep=5
while getopts ":s:d:k:" opt; do
    case "$opt" in
        s) src="$OPTARG";;
        d) dest="$OPTARG";;
        k) keep="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

[[ -z "$src" || -z "$dest" ]] && usage
[[ ! -d "$src" ]] && die "Source directory not found: $src"
mkdir -p "$dest"

ts="$(date +%Y%m%d_%H%M%S)"
archive="$dest/backup_${ts}.tar.gz"

log "Starting backup of '$src' to '$archive'"
tar -czf "$archive" -C "$src" . || die "Backup failed"
log "Backup complete: $archive"

# Rotate old backups, keep only $keep most recent
backups=("$dest"/backup_*.tar.gz)
if (( ${#backups[@]} > keep )); then
    to_delete=("${backups[@]:0:${#backups[@]}-keep}")
    for old in "${to_delete[@]}"; do
        log "Deleting old backup: $old"
        rm -f -- "$old"
    done
fi

log "Rotation complete. Remaining backups:"
ls -1 "$dest"/backup_*.tar.gz
exit 0
```

**Key Points:**
- Uses arrays and quoting for safety.
- Logs all actions with timestamps.
- Rotates backups, keeping only the last N.
- Exits 0 on success, errors are logged and exit non-zero.
- Add `trap` for temp files if you extend with exclusions or staging.

### 2. System Monitoring Script with Alerting


**Practical Example: System Monitoring Script with Alerting**

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

usage() {
    echo "Usage: $0 [-c cpu%%] [-m mem%%] [-t disk%%] [-l logfile]" >&2
    exit 1
}

log() { printf '[%s] %s\n' "$(date +%F\ %T)" "$*"; }

cpu_thresh=90
mem_thresh=90
disk_thresh=90
logfile=""

while getopts ":c:m:t:l:" opt; do
    case "$opt" in
        c) cpu_thresh="$OPTARG";;
        m) mem_thresh="$OPTARG";;
        t) disk_thresh="$OPTARG";;
        l) logfile="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

alerted=0

check_cpu() {
    local usage
    usage=$(top -b -n1 | awk '/^%?Cpu/ {print $2}' | head -1)
    usage=${usage%.*}
    [[ -z "$usage" ]] && usage=0
    log "CPU usage: $usage%%"
    (( usage > cpu_thresh )) && log "ALERT: CPU usage $usage%% > $cpu_thresh%%" && alerted=1
}

check_mem() {
    local usage
    usage=$(free | awk '/Mem:/ {printf("%.0f", $3/$2*100)}')
    log "Memory usage: $usage%%"
    (( usage > mem_thresh )) && log "ALERT: Memory usage $usage%% > $mem_thresh%%" && alerted=1
}

check_disk() {
    local usage
    usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
    log "Disk usage: $usage%%"
    (( usage > disk_thresh )) && log "ALERT: Disk usage $usage%% > $disk_thresh%%" && alerted=1
}

check_procs() {
    local count
    count=$(ps -e --no-headers | wc -l)
    log "Process count: $count"
}

main() {
    check_cpu
    check_mem
    check_disk
    check_procs
    if (( alerted )); then
        [[ -n "$logfile" ]] && log "Alert written to $logfile" && logger "System alert: threshold exceeded" && log "See syslog for details." && echo "ALERT" >> "$logfile"
        exit 2
    fi
    log "All metrics within thresholds."
    [[ -n "$logfile" ]] && echo "OK" >> "$logfile"
    exit 0
}

main "$@"
```

**Key Points:**
- Modular functions for each metric.
- Flags for thresholds and optional log file.
- Human-readable summary and alerting.
- Exits non-zero if any metric exceeds threshold.
- Integrates with `logger` for syslog.

### 3. User Management Automation Script


**Practical Example: Batch User Creation from CSV**

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

usage() {
    echo "Usage: $0 -f users.csv [-n]" >&2
    echo "  -f file   CSV file: username,full_name,shell" >&2
    echo "  -n        Dry-run (show actions, no changes)" >&2
    exit 1
}

log() { printf '[%s] %s\n' "$(date +%F\ %T)" "$*"; }
die() { log "ERROR: $*" >&2; exit 1; }

file=""
dryrun=0
while getopts ":f:n" opt; do
    case "$opt" in
        f) file="$OPTARG";;
        n) dryrun=1;;
        *) usage;;
    esac
done
shift $((OPTIND-1))

[[ -z "$file" || ! -r "$file" ]] && usage

while IFS=, read -r username full_name shell; do
    # Input validation
    [[ -z "$username" || -z "$shell" ]] && log "Skipping invalid line: $username,$full_name,$shell" && continue
    [[ ! "$username" =~ ^[a-zA-Z0-9_-]+$ ]] && log "Invalid username: $username" && continue
    id "$username" &>/dev/null && log "User exists: $username" && continue
    log "Creating user: $username ($full_name) with shell $shell"
    if (( dryrun )); then
        log "[DRY-RUN] Would run: useradd -m -c '$full_name' -s '$shell' '$username'"
    else
        sudo useradd -m -c "$full_name" -s "$shell" "$username"
        log "User created: $username"
    fi
done < "$file"

log "Batch user creation complete."
```

**Key Points:**
- Uses `IFS=,` and safe read loop for CSV parsing.
- Validates input and username format.
- Idempotent: skips existing users.
- Logs all actions; supports dry-run mode.
- Use `sudo` for user creation (note: script must be run with appropriate privileges).

### 4. Log Analysis and Reporting Script


**Practical Example: Log Analysis and Reporting Script**

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

usage() {
    echo "Usage: $0 -f log -p pattern [-o report.txt]" >&2
    exit 1
}

logfile=""
pattern="error|failed|warn"
outfile="report.txt"
while getopts ":f:p:o:" opt; do
    case "$opt" in
        f) logfile="$OPTARG";;
        p) pattern="$OPTARG";;
        o) outfile="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

[[ -z "$logfile" || ! -r "$logfile" ]] && usage

# Summary counts
summary=$(grep -Eio "$pattern" "$logfile" | sort | uniq -c | sort -nr)

# Top N errors (by message)
top_errors=$(grep -Ei "$pattern" "$logfile" | awk '{for(i=1;i<=NF;i++) if($i~/'"$pattern"'/) print $i}' | sort | uniq -c | sort -nr | head -10)

# Hourly histogram
hour_hist=$(grep -Ei "$pattern" "$logfile" | awk '{if($3~/^[0-9:]+$/) split($3,a,":"); print a[1]}' | sort | uniq -c | sort -k2,2n)

# Write report
{
    echo "==== Log Analysis Report ===="
    echo "File: $logfile"
    echo "Pattern: $pattern"
    echo
    echo "-- Summary Counts --"
    echo "$summary"
    echo
    echo "-- Top 10 Errors --"
    echo "$top_errors"
    echo
    echo "-- Hourly Histogram --"
    echo "$hour_hist"
} > "$outfile"

# Print short summary to screen
echo "Report written to $outfile"
echo "Top 3 error types:"
echo "$summary" | head -3
echo "Hourly error trend:"
echo "$hour_hist" | head -5
```

**Key Points:**
- Accepts log file, pattern, and output file as flags.
- Produces summary counts, top errors, and hourly histogram using `awk` and stable sorting.
- Saves full report to file and prints a short summary to screen.

### 5. Deployment Automation Script


**Practical Example: Deployment Automation Script**

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

usage() {
    echo "Usage: $0 -p package -a artifact -d deploy_dir [-h health_cmd]" >&2
    exit 1
}

log() { printf '[%s] %s\n' "$(date +%F\ %T)" "$*"; }
die() { log "ERROR: $*" >&2; exit 1; }

pkg=""; artifact=""; deploy_dir=""; health_cmd=""
while getopts ":p:a:d:h:" opt; do
    case "$opt" in
        p) pkg="$OPTARG";;
        a) artifact="$OPTARG";;
        d) deploy_dir="$OPTARG";;
        h) health_cmd="$OPTARG";;
        *) usage;;
    esac
done
shift $((OPTIND-1))

[[ -z "$pkg" || -z "$artifact" || -z "$deploy_dir" ]] && usage
[[ ! -f "$artifact" ]] && die "Artifact not found: $artifact"
mkdir -p "$deploy_dir"

backup="$deploy_dir/backup_$(date +%Y%m%d_%H%M%S)"
rollback() {
    log "Rolling back to previous version..."
    [[ -d "$backup" ]] && cp -a "$backup/." "$deploy_dir/" && log "Rollback complete."
}
trap rollback ERR

main() {
    log "Validating package: $pkg"
    if ! dpkg -s "$pkg" &>/dev/null; then
        log "Installing package: $pkg"
        sudo apt-get install -y "$pkg"
    else
        log "Package $pkg already installed."
    fi

    log "Backing up current deployment to $backup"
    cp -a "$deploy_dir" "$backup"

    log "Deploying new artifact: $artifact"
    cp -a "$artifact" "$deploy_dir/"

    log "Verifying health..."
    if [[ -n "$health_cmd" ]]; then
        if ! eval "$health_cmd"; then
            die "Health check failed after deployment."
        fi
        log "Health check passed."
    else
        log "No health check provided; assuming success."
    fi

    log "Deployment successful."
    trap - ERR
}

main "$@"
```

**Key Points:**
- Validates package and artifact before deploying.
- Backs up current version and uses trap for rollback on error.
- Deploys new artifact and verifies health.
- Logs all steps; idempotent checks for package install.
- Successful deploy leaves health check passing; failures revert state.

---
Try these exercises to apply your knowledge and prepare for real-world Linux administration tasks. Each project can be expanded as your skills grow.

## Next Steps



---

## Quick Reference Cheat Sheet

**Shebang:**
```bash
#!/usr/bin/env bash
```

**Strict Mode:**
```bash
set -euo pipefail
```

**Variables:**
```bash
name="value"
echo "$name"
```

**Read Lines Safely:**
```bash
while IFS= read -r line || [[ -n "$line" ]]; do
    echo "$line"
done < "file.txt"
```

**For Loop (Files):**
```bash
shopt -s nullglob
for f in *.txt; do
    echo "$f"
done
```

**Functions:**
```bash
myfunc() {
    local arg="$1"
    echo "Arg: $arg"
}
myfunc "hello"
```

**Argument Parsing:**
```bash
while getopts ":f:v" opt; do
    case "$opt" in
        f) file="$OPTARG";;
        v) verbose=1;;
    esac
done
shift $((OPTIND-1))
```

**Logging Helper:**
```bash
log() { local level="$1"; shift; printf '%s [%s] %s\n' "$(date '+%H:%M:%S')" "$level" "$*"; }
```

**Error Handling:**
```bash
die() { log ERROR "$*" >&2; exit 1; }
```

**Trap for Cleanup:**
```bash
trap 'rm -f "$tmpfile"' EXIT
```

**Check Exit Code:**
```bash
command
code=$?
echo "Exit code: $code"
```

**Debugging:**
```bash
set -x   # Enable tracing
set +x   # Disable tracing
```

**Linting:**
```bash
shellcheck script.sh
```

---

Congratulations on completing the Shell Scripting Fundamentals module! Here are some ways to continue your learning and grow as a Linux sysadmin:

- **Learn advanced shell tools:**
    - `jq` for JSON parsing ([link])
    - `yq` for YAML processing ([link])
- **Parallelization:**
    - Use `xargs -P` or [GNU parallel]([link]) to run jobs in parallel
- **Automate with systemd timers:**
    - Replace cron jobs with [systemd timers]([link]) for better reliability
- **Integrate with CI/CD:**
    - Run scripts in CI pipelines (GitHub Actions, GitLab CI, etc.) ([link])
- **Contribute to scripts:**
    - Add features, refactor for clarity, and share improvements
- **Add tests:**
    - Write test scripts or use [bats]([link]) for automated testing
- **Use version control workflows:**
    - Work in branches, open pull requests, and review code ([link])

With shell scripting fundamentals mastered, you're ready to explore Storage & Filesystem Management in Module 10, where you'll learn advanced storage concepts and filesystem administration.

## Resources for Further Study


- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html) — Official, comprehensive Bash documentation; use for syntax and built-in details.
- [ShellCheck Wiki](https://github.com/koalaman/shellcheck/wiki) — Linter documentation and best practices; use to understand and fix script warnings.
- [Bash Hackers Wiki](https://wiki.bash-hackers.org/) — Deep dives into Bash internals and scripting patterns; use for advanced topics and troubleshooting.
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/) — Extensive scripting examples and explanations; use for learning by example.
- [man bash](https://man7.org/linux/man-pages/man1/bash.1.html) — Manual page for Bash; use for quick reference on options and built-ins.
- [`help` command](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html) — Run `help` in Bash for built-in command usage; use for immediate, interactive help.

## Glossary


- **Control Structure**: Constructs like if/else, loops, and case statements that control script flow.
- **Debug Mode**: A mode (`set -x`) that prints each command before executing it for troubleshooting.
- **Exit Code**: Numeric value returned by a command or script indicating success (0) or failure (non-zero).
- **Function**: A reusable block of code within a script, called by name.
- **Globbing**: Pattern matching for filenames using wildcards like `*`, `?`, and `[]`.
- **Here-doc**: A multi-line string input to a command, delimited by a marker (e.g., `<<EOF`).
- **Here-string**: A single string input to a command, using `<<<` (e.g., `cat <<< "text"`).
- **IFS**: Internal Field Separator; determines how Bash splits words (default: space, tab, newline).
- **Parameter Expansion**: Expanding variables or parameters (e.g., `${var}`, `${1:-default}`).
- **Pipeline**: A sequence of commands connected by `|`, passing output from one to the next.
- **Shebang**: The `#!/usr/bin/env bash` line at the top of a script specifying the interpreter.
- **Strict Mode**: Using `set -euo pipefail` to make scripts safer and more predictable.
- **Subshell**: A child shell created by parentheses or pipelines, with its own environment.
- **Trap**: A shell feature to catch signals or errors and run code in response.
- **Variable**: A named storage location for data in a script.
- **Word Splitting**: Breaking a string into words based on IFS, often occurs during variable expansion.
