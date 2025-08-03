# Module 3: Command-Line Essentials

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [3.1 Shell Basics and Environment](#31-shell-basics-and-environment)
  - [3.2 Navigation and File Operations](#32-navigation-and-file-operations)
  - [3.3 File Content Management](#33-file-content-management)
  - [3.4 Text Processing and Data Manipulation](#34-text-processing-and-data-manipulation)
  - [3.5 Pipes, Redirection, and Command Chaining](#35-pipes-redirection-and-command-chaining)
  - [3.6 File Searching and Pattern Matching](#36-file-searching-and-pattern-matching)
  - [3.7 Shell Customization and Productivity](#37-shell-customization-and-productivity)
  - [3.8 Debugging and Error Handling](#38-debugging-and-error-handling)
  - [3.9 Archives and Compression](#39-archives-and-compression)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Navigation and File Management](#navigation-and-file-management)
  - [Text Processing Pipelines](#text-processing-pipelines)
  - [Shell Customization and Functions](#shell-customization-and-functions)
  - [Advanced Command Combinations](#advanced-command-combinations)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: File System Navigation and Management](#lab-1-file-system-navigation-and-management)
  - [Lab 2: Text Processing and Data Analysis](#lab-2-text-processing-and-data-analysis)
  - [Lab 3: Shell Customization and Productivity](#lab-3-shell-customization-and-productivity)
  - [Lab 4: Command-Line Automation and Scripting](#lab-4-command-line-automation-and-scripting)
- [Best Practices Summary](#best-practices-summary)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
This module covers essential command-line skills that every Linux system administrator needs. Students will master filesystem navigation, file manipulation, text processing, and shell customization to build a foundation for efficient system administration. The focus is on practical, real-world command-line operations that form the backbone of Linux administration workflows.

**Key Learning Outcomes:**
- Navigate the Linux filesystem efficiently using command-line tools
- Create, modify, and manage files and directories with confidence
- Build powerful command pipelines using pipes and redirection
- Process and analyze text data using command-line tools
- Customize shell environments for enhanced productivity
- Debug command sequences and handle errors effectively
- Automate repetitive tasks with aliases, functions, and scripts

## Learning Objectives
By the end of this module, you will be able to:

1. **Master Shell Environment**: Navigate shell types, command structure, and environment configuration
2. **Efficient File Operations**: Create, modify, and manage files and directories with advanced techniques
3. **Text Processing Mastery**: Extract, transform, and analyze data using command-line text processing tools
4. **Pipeline Construction**: Combine commands into powerful one-liners using pipes, redirection, and chaining
5. **Shell Customization**: Create custom aliases, functions, and prompts to streamline workflows
6. **Error Handling**: Debug command sequences, interpret exit codes, and implement error handling
7. **Archive Management**: Work with various archive and compression formats efficiently
8. **Productivity Optimization**: Implement keyboard shortcuts, history management, and automation techniques

## Topics

### 3.1 Shell Basics and Environment
- **Shell Types and Features**: bash, zsh, dash, and shell compatibility
- **Command Structure**: Syntax, arguments, options, and command parsing
- **Environment Variables**: System and user variables, PATH management
- **Command History**: History expansion, searching, and management
- **Tab Completion**: Completion systems and customization
- **Shell Options**: Set options for behavior modification and debugging

### 3.2 Navigation and File Operations
- **Filesystem Navigation**: `pwd`, `cd`, absolute vs relative paths
- **File Listing**: `ls` variations, hidden files, detailed information
- **Directory Management**: `mkdir`, `rmdir`, directory structure creation
- **File Operations**: `cp`, `mv`, `rm` with safety and efficiency
- **File Creation**: `touch`, file timestamps, and bulk operations
- **Symbolic and Hard Links**: `ln` command, link management

### 3.3 File Content Management
- **File Viewing**: `cat`, `less`, `more`, `head`, `tail` with options
- **File Editing**: Command-line editors (nano, vim), file modification
- **File Comparison**: `diff`, `cmp`, `comm` for file analysis
- **File Content Searching**: `grep` family with regular expressions
- **File Information**: `file`, `stat`, metadata examination

### 3.4 Text Processing and Data Manipulation
- **Pattern Searching**: `grep`, `egrep`, `fgrep` with advanced patterns
- **Text Transformation**: `sed` for stream editing and substitution
- **Data Processing**: `awk` for structured data manipulation
- **Sorting and Filtering**: `sort`, `uniq`, `shuf` for data organization
- **Text Analysis**: `wc`, `cut`, `paste`, `join` for data extraction
- **Character Processing**: `tr`, `rev`, character translation and manipulation

### 3.5 Pipes, Redirection, and Command Chaining
- **Stream Management**: stdin, stdout, stderr understanding and manipulation
- **Output Redirection**: `>`, `>>`, `&>` for output control
- **Input Redirection**: `<`, `<<` for input sourcing
- **Pipes**: `|` for command chaining and data flow
- **Command Chaining**: `;`, `&&`, `||` for conditional execution
- **Process Substitution**: `<()`, `>()` for advanced piping

### 3.6 File Searching and Pattern Matching
- **File Finding**: `find` with complex criteria and actions
- **Command Location**: `which`, `whereis`, `locate`, `type` for command discovery
- **Pattern Matching**: Wildcards, globbing, and pattern expansion
- **Regular Expressions**: POSIX and extended regex in command-line tools
- **Search Optimization**: Efficient searching strategies and indexing

### 3.7 Shell Customization and Productivity
- **Environment Configuration**: `.bashrc`, `.profile`, configuration management
- **Alias Creation**: Simple and complex aliases for command shortcuts
- **Function Development**: Shell functions for reusable command sequences
- **Prompt Customization**: PS1 configuration, color coding, dynamic content
- **Keyboard Shortcuts**: Command-line editing, history navigation
- **Completion Systems**: Custom completion, programmable completion

### 3.8 Debugging and Error Handling
- **Exit Code Management**: Understanding and utilizing exit codes
- **Error Detection**: Identifying command failures and error conditions
- **Debugging Options**: `set -x`, `set -e`, `set -u` for script debugging
- **Error Handling**: Conditional execution, error recovery, logging
- **Troubleshooting**: Common command-line issues and resolution strategies

### 3.9 Archives and Compression
- **Archive Creation**: `tar` with various options and formats
- **Compression Tools**: `gzip`, `bzip2`, `xz`, `zip` and their usage
- **Archive Extraction**: Safe extraction practices and verification
- **Archive Management**: Listing, updating, and manipulating archives
- **Compression Strategy**: Choosing appropriate compression for different scenarios

## Essential Command Reference

| Command | Description | Common Options | Example |
|---------|-------------|----------------|---------|
| `ls` | List directory contents | `-la`, `-h`, `-t`, `-r` | `ls -la /etc/` |
| `cd` | Change directory | N/A | `cd /var/log` |
| `pwd` | Print working directory | N/A | `pwd` |
| `mkdir` | Create directories | `-p`, `-m` | `mkdir -p /path/to/dir` |
| `rm` | Remove files/directories | `-r`, `-f`, `-i` | `rm -rf directory/` |
| `cp` | Copy files/directories | `-r`, `-p`, `-u` | `cp -r src/ dest/` |
| `mv` | Move/rename files | N/A | `mv old.txt new.txt` |
| `find` | Search for files | `-name`, `-type`, `-size` | `find /var -name "*.log"` |
| `grep` | Search text patterns | `-r`, `-i`, `-v`, `-n` | `grep -r "error" /var/log/` |
| `sed` | Stream editor | `-i`, `-e`, `-n` | `sed 's/old/new/g' file.txt` |
| `awk` | Text processing | `-F`, `-v` | `awk '{print $1}' file.txt` |
| `sort` | Sort lines | `-n`, `-r`, `-k` | `sort -nr numbers.txt` |
| `uniq` | Remove duplicates | `-c`, `-d`, `-u` | `sort file.txt \| uniq -c` |
| `tar` | Archive files | `-czf`, `-xzf`, `-tzf` | `tar -czf backup.tar.gz dir/` |
| `head` | Show file beginning | `-n`, `-c` | `head -n 20 file.txt` |
| `tail` | Show file end | `-n`, `-f` | `tail -f /var/log/syslog` |

## Practical Examples
- Pipes: `|`
- Command chaining: `;`, `&&`, `||`

### 3.6 File Searching
- Finding files: `find`
- Locating commands: `which`, `whereis`, `locate`
- Pattern matching with wildcards

### 3.7 Shell Customization and Environment
- Environment variables and their usage
- Creating and managing aliases
- Writing shell functions
- Customizing shell prompts (PS1)
- Shell configuration files (.bashrc, .profile)
- Command history management

### 3.8 Debugging and Exit Codes
- Understanding exit codes ($?)
- Debugging command sequences
- Error handling in command chains
- Using `set` options for debugging
- Troubleshooting failed commands

### 3.9 Archives and Compression
- Creating archives: `tar`
- Compression tools: `gzip`, `gunzip`, `zip`, `unzip`
- Working with compressed archives

### Navigation and File Management

#### Advanced File Operations
```bash
# Create complex directory structures
mkdir -p projects/{web/{frontend,backend},mobile/{ios,android},docs}
tree projects/  # Visualize structure

# Bulk file operations
touch file{1..10}.txt                    # Create multiple files
cp file{1..5}.txt backup/                # Copy multiple files
rename 's/\.txt$/.bak/' *.txt           # Rename with pattern

# Safe file operations
cp important.conf{,.backup}             # Create backup before editing
mv /etc/important.conf{,.backup}        # Backup with move
rm -i *.tmp                             # Interactive deletion

# Advanced file copying
cp -p source.txt dest.txt               # Preserve timestamps and permissions
cp -u source/ dest/                     # Update only newer files
rsync -av source/ dest/                 # Advanced synchronization
```

#### Efficient Navigation Techniques
```bash
# Quick directory navigation
cd -                    # Go to previous directory
pushd /var/log         # Push directory to stack and change
popd                   # Pop directory from stack and change
dirs                   # Show directory stack

# Bookmark directories with environment variables
export WEBROOT="/var/www/html"
export LOGS="/var/log"
export CONFIGS="/etc"
cd $WEBROOT            # Quick navigation to bookmarked locations

# Find and navigate to directories
cd $(find / -name "nginx" -type d 2>/dev/null | head -1)
```

#### File Information and Analysis
```bash
#!/bin/bash
# file-analysis.sh - Comprehensive file analysis tool

analyze_file() {
    local file="$1"
    
    if [[ ! -e "$file" ]]; then
        echo "File does not exist: $file"
        return 1
    fi
    
    echo "=== File Analysis: $file ==="
    echo "Type: $(file "$file")"
    echo "Size: $(du -h "$file" | cut -f1)"
    echo "Permissions: $(stat -c "%A" "$file")"
    echo "Owner: $(stat -c "%U:%G" "$file")"
    echo "Modified: $(stat -c "%y" "$file")"
    echo "Inode: $(stat -c "%i" "$file")"
    
    if [[ -f "$file" ]]; then
        echo "Lines: $(wc -l < "$file")"
        echo "Words: $(wc -w < "$file")"
        echo "Characters: $(wc -c < "$file")"
        
        # Show file preview
        echo ""
        echo "=== File Preview (first 10 lines) ==="
        head -10 "$file"
    fi
}

# Usage: analyze_file /path/to/file
analyze_file "$1"
```

### Text Processing Pipelines

#### Advanced Text Processing Chains
```bash
# Log analysis pipeline
tail -1000 /var/log/apache2/access.log | \
awk '{print $1}' | \
sort | \
uniq -c | \
sort -nr | \
head -10
# Shows top 10 IP addresses from last 1000 log entries

# System monitoring pipeline
ps aux | \
awk 'NR>1 {cpu+=$3; mem+=$4; count++} END {printf "Avg CPU: %.2f%%, Avg MEM: %.2f%%, Processes: %d\n", cpu/count, mem/count, count}'

# File processing pipeline
find /var/log -name "*.log" -type f | \
xargs grep -l "ERROR" | \
xargs ls -lt | \
head -5
# Find the 5 most recently modified log files containing "ERROR"

# Data extraction and formatting
cat /etc/passwd | \
awk -F: '{print $1, $3, $5}' | \
sort -k2 -n | \
column -t
# Format user information in columns, sorted by UID
```

#### Advanced grep and Pattern Matching
```bash
# Complex pattern searching
grep -E "(error|warning|critical)" /var/log/syslog    # Multiple patterns
grep -r --include="*.log" "failed" /var/log/          # Specific file types
grep -B 3 -A 3 "exception" app.log                   # Context lines
grep -v "^#\|^$" /etc/ssh/sshd_config                # Exclude comments and empty lines

# Grep with file operations
grep -l "TODO" *.py                                   # List files containing pattern
grep -c "error" *.log                                 # Count occurrences per file
grep -o -E "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b" file.txt  # Extract emails
```

#### Advanced sed Operations
```bash
# Text substitution and manipulation
sed 's/old/new/g' file.txt                           # Global replace
sed '1,5s/pattern/replacement/' file.txt              # Replace in specific lines
sed '/pattern/d' file.txt                            # Delete lines containing pattern
sed -n '10,20p' file.txt                             # Print specific line range
sed 's/.*=//' config.txt                             # Remove everything before =

# In-place editing with backup
sed -i.backup 's/old/new/g' file.txt

# Multiple operations
sed -e 's/foo/bar/g' -e 's/hello/world/g' file.txt

# Advanced sed script example
sed '
    /^#/d                    # Delete comment lines
    /^$/d                    # Delete empty lines
    s/\s\+$//                # Remove trailing whitespace
    s/\t/    /g              # Convert tabs to spaces
' input.txt > output.txt
```

#### Advanced awk Programming
```bash
# AWK for data processing
awk '{sum += $1} END {print "Total:", sum}' numbers.txt
awk -F: '{print "User " $1 " has UID " $3}' /etc/passwd
awk 'length($0) > 80' file.txt                       # Lines longer than 80 characters
awk '/pattern/ {count++} END {print count}' file.txt # Count pattern occurrences

# Complex AWK script for log analysis
awk '
BEGIN { 
    print "Log Analysis Report"
    print "==================="
}
/ERROR/ { 
    errors++
    print "Error at line " NR ": " $0
}
/WARNING/ { 
    warnings++
}
END {
    print "Summary:"
    print "Errors: " errors
    print "Warnings: " warnings
    print "Total lines: " NR
}' /var/log/application.log
```

### Shell Customization and Functions

#### Advanced Shell Configuration
```bash
# ~/.bashrc - Comprehensive configuration
# History settings
export HISTSIZE=50000
export HISTFILESIZE=100000
export HISTCONTROL=ignoredups:ignorespace:erasedups
export HISTTIMEFORMAT='%F %T '
shopt -s histappend
shopt -s cmdhist

# Shell options for better experience
shopt -s checkwinsize    # Check window size after each command
shopt -s globstar        # Enable ** pattern matching
shopt -s nocaseglob      # Case-insensitive globbing
shopt -s cdspell         # Minor spelling corrections for cd
shopt -s dirspell        # Spelling corrections for directory names

# Enhanced prompt with git support
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

get_git_status() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        local status=$(git status --porcelain 2>/dev/null)
        if [[ -n $status ]]; then
            echo "*"  # Uncommitted changes
        fi
    fi
}

# Dynamic prompt with color and git info
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[01;33m\]$(get_git_status)\[\033[00m\]\$ '

# Environment variables
export EDITOR='vim'
export PAGER='less -R'
export LESS='-i -M -R -S -w -z-4'
export GREP_OPTIONS='--color=auto'
```

#### Powerful Shell Functions
```bash
#!/bin/bash
# ~/.bash_functions - Advanced shell functions

# Multi-purpose extraction function
extract() {
    if [[ -f "$1" ]]; then
        case "$1" in
            *.tar.bz2)   tar xjf "$1"       ;;
            *.tar.gz)    tar xzf "$1"       ;;
            *.tar.xz)    tar xJf "$1"       ;;
            *.bz2)       bunzip2 "$1"       ;;
            *.rar)       unrar x "$1"       ;;
            *.gz)        gunzip "$1"        ;;
            *.tar)       tar xf "$1"        ;;
            *.tbz2)      tar xjf "$1"       ;;
            *.tgz)       tar xzf "$1"       ;;
            *.zip)       unzip "$1"         ;;
            *.Z)         uncompress "$1"    ;;
            *.7z)        7z x "$1"          ;;
            *.deb)       ar x "$1"          ;;
            *.rpm)       rpm2cpio "$1" | cpio -idmv ;;
            *)           echo "Don't know how to extract '$1'" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}

# Create directory and enter it
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Find and kill processes by name
killps() {
    local process="$1"
    if [[ -z "$process" ]]; then
        echo "Usage: killps <process_name>"
        return 1
    fi
    
    local pids=$(pgrep "$process")
    if [[ -n "$pids" ]]; then
        echo "Killing processes matching '$process':"
        ps -p $pids
        kill $pids
    else
        echo "No processes found matching '$process'"
    fi
}

# Show directory sizes sorted
dirsize() {
    local dir="${1:-.}"
    du -sh "$dir"/* 2>/dev/null | sort -hr
}

# Quick backup function
backup() {
    local file="$1"
    if [[ -f "$file" ]]; then
        cp "$file" "${file}.backup.$(date +%Y%m%d_%H%M%S)"
        echo "Backup created: ${file}.backup.$(date +%Y%m%d_%H%M%S)"
    else
        echo "File not found: $file"
    fi
}

# Network information function
netinfo() {
    echo "Network Information:"
    echo "==================="
    echo "Hostname: $(hostname)"
    echo "IP Address: $(ip route get 8.8.8.8 | awk '{print $7; exit}')"
    echo "Gateway: $(ip route | awk '/default/ {print $3}')"
    echo "DNS Servers: $(grep nameserver /etc/resolv.conf | awk '{print $2}' | tr '\n' ' ')"
    echo "Open Ports: $(ss -tuln | grep LISTEN | wc -l)"
}

# System information function
sysinfo() {
    echo "System Information:"
    echo "=================="
    echo "OS: $(lsb_release -d | cut -f2)"
    echo "Kernel: $(uname -r)"
    echo "Uptime: $(uptime -p)"
    echo "Load: $(uptime | awk -F'load average:' '{print $2}')"
    echo "Memory: $(free -h | grep Mem | awk '{print $3"/"$2}')"
    echo "Disk: $(df -h / | tail -1 | awk '{print $3"/"$2" ("$5" used)"}')"
    echo "CPU: $(nproc) cores"
}

# Log monitoring function
logwatch() {
    local logfile="${1:-/var/log/syslog}"
    local pattern="${2:-.*}"
    
    echo "Monitoring $logfile for pattern: $pattern"
    echo "Press Ctrl+C to stop"
    tail -f "$logfile" | grep --color=always "$pattern"
}
```

#### Production-Ready Aliases
```bash
# ~/.bash_aliases - Professional alias collection

# Enhanced basic commands
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Safety aliases
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# System administration aliases
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias ps='ps auxf'
alias pstree='pstree -p'

# Network aliases
alias ports='netstat -tulanp'
alias listening='ss -tuln'
alias iptlist='iptables -L -n -v --line-numbers'
alias ping='ping -c 5'
alias wget='wget -c'

# Process management
alias psmem='ps auxf | sort -nr -k 4'
alias pscpu='ps auxf | sort -nr -k 3'
alias top='htop'

# Git aliases (if git is used)
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias gd='git diff'
alias glog='git log --oneline --graph --decorate'

# Archive aliases
alias tardir='tar -czf'
alias untar='tar -xzf'
alias tarlist='tar -tzf'

# Date and time
alias now='date +"%T"'
alias today='date +"%d-%m-%Y"'
alias timestamp='date +"%Y%m%d_%H%M%S"'

# Directory navigation
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias .....='cd ../../../..'

# Quick edits
alias bashrc='$EDITOR ~/.bashrc'
alias vimrc='$EDITOR ~/.vimrc'
alias hosts='sudo $EDITOR /etc/hosts'

# System monitoring
alias meminfo='free -m -l -t'
alias cpuinfo='lscpu'
alias diskinfo='lsblk'
alias temperature='sensors'
alias processes='ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head'
```

### Advanced Command Combinations

#### System Monitoring One-Liners
```bash
# Real-time monitoring commands
watch -n 1 'cat /proc/loadavg'                       # CPU load monitoring
watch -n 1 'free -m'                                 # Memory monitoring
watch -n 1 'df -h'                                   # Disk space monitoring
watch -n 1 'ss -tuln | wc -l'                       # Network connections count

# Process analysis
ps aux --sort=-%cpu | head -10                       # Top CPU consumers
ps aux --sort=-%mem | head -10                       # Top memory consumers
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head    # Detailed process info

# Network monitoring
ss -tuln | awk 'NR>1 {count[$1]++} END {for(i in count) print i, count[i]}' # Protocol counts
netstat -i | awk 'NR>2 {print $1, $3+$7}'          # Interface traffic summary
```

#### File and Directory Analysis
```bash
# Disk usage analysis
find /var/log -type f -size +100M -exec ls -lh {} \; # Large log files
du -sh /var/* | sort -hr | head -10                  # Largest directories
find / -type f -size +1G 2>/dev/null                # Files larger than 1GB

# File age analysis
find /tmp -type f -mtime +7 -exec rm {} \;          # Remove files older than 7 days
find /var/log -type f -mtime -1 -exec ls -lt {} \;  # Files modified in last 24 hours
find /home -type f -atime +30 -exec ls -lu {} \;    # Files not accessed in 30 days

# Permission analysis
find /var/www -type f ! -perm 644 -exec ls -l {} \; # Files with non-standard permissions
find /usr/bin -perm -4000 -exec ls -l {} \;         # SUID files
find /tmp -type d ! -perm 1777 -exec ls -ld {} \;   # Directories without sticky bit
```

#### Data Processing Pipelines
```bash
# Log analysis pipelines
grep "404" /var/log/apache2/access.log | \
awk '{print $7}' | \
sort | \
uniq -c | \
sort -nr | \
head -10
# Top 10 404 pages

# System inventory
dpkg -l | awk '/^ii/ {print $2, $3}' | sort > installed_packages.txt
lsmod | awk 'NR>1 {print $1}' | sort > loaded_modules.txt
systemctl list-units --type=service --state=running | \
awk 'NR>1 && !/^$/ {print $1}' | \
sort > running_services.txt

# Performance monitoring
iostat -x 1 5 | awk '/^[a-z]/ {print $1, $10}' | \
sort -k2 -nr | \
head -5
# Top 5 busiest disks
```

## Lab Exercises

### Lab 1: File System Navigation and Management
**Objective:** Master efficient filesystem navigation and file operations.

**Tasks:**
1. Create a complex directory structure for a multi-tier application
2. Practice bulk file operations using brace expansion and wildcards
3. Implement safe file operations with backups and verification
4. Use symbolic and hard links to create reference structures
5. Develop navigation shortcuts using aliases and environment variables

**Deliverables:**
- Complex directory structure documentation
- File operation safety scripts
- Navigation efficiency improvements

### Lab 2: Text Processing and Data Analysis
**Objective:** Build expertise in command-line text processing and data analysis.

**Tasks:**
1. Analyze system log files to extract meaningful information
2. Create complex pipelines for data transformation and analysis
3. Use grep, sed, and awk for advanced text manipulation
4. Process CSV data using command-line tools
5. Generate reports from unstructured text data

**Deliverables:**
- Log analysis scripts and reports
- Data processing pipelines
- Text manipulation examples

### Lab 3: Shell Customization and Productivity
**Objective:** Customize shell environment for maximum productivity.

**Tasks:**
1. Configure comprehensive bash environment with advanced features
2. Create a library of useful aliases and functions
3. Implement dynamic prompts with git integration
4. Set up efficient history management and completion
5. Develop productivity-enhancing keyboard shortcuts

**Deliverables:**
- Complete shell configuration files
- Function and alias library
- Productivity measurement and improvements

### Lab 4: Command-Line Automation and Scripting
**Objective:** Automate repetitive tasks using command-line tools and techniques.

**Tasks:**
1. Create automation scripts for system maintenance tasks
2. Implement error handling and logging in command sequences
3. Develop monitoring and alerting using command-line tools
4. Build data processing workflows for regular operations
5. Create interactive command-line tools for common tasks

**Deliverables:**
- Automation script collection
- Error handling examples
- Monitoring and alerting implementations

## Best Practices Summary

### Command-Line Efficiency Guidelines

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| **Navigation** | Use absolute paths in scripts | `/usr/local/bin/script` vs `../bin/script` |
| **File Operations** | Always backup before modifications | `cp file{,.backup}` |
| **Text Processing** | Use appropriate tools for tasks | `awk` for structured data, `sed` for substitution |
| **Piping** | Validate each step of complex pipelines | Test commands individually first |
| **Error Handling** | Check exit codes in scripts | `command && echo "success" \|\| echo "failed"` |
| **History** | Use descriptive commands for searchability | Avoid overly abbreviated commands |
| **Safety** | Use interactive mode for destructive operations | `rm -i`, `mv -i` |

### Performance Optimization

1. **Command Selection**
   - Use `grep -F` for fixed strings (faster than regex)
   - Use `sort -u` instead of `sort | uniq`
   - Use `find` with `-exec` instead of `xargs` when order matters

2. **Pipeline Optimization**
   - Filter early in pipelines to reduce data volume
   - Use `cut` before `sort` to reduce sort load
   - Consider `--parallel` options for applicable commands

3. **Resource Management**
   - Use `nice` for CPU-intensive operations
   - Limit memory usage with `ulimit`
   - Monitor long-running processes with `nohup`

### Security Considerations

1. **Command Safety**
   - Quote variables to prevent word splitting
   - Use full paths for commands in scripts
   - Validate user input in interactive scripts

2. **File Handling**
   - Set appropriate umask for created files
   - Use secure temporary files with `mktemp`
   - Avoid processing untrusted data with shell expansion

## Troubleshooting Common Issues

### Command Not Found
```bash
# Diagnose command location issues
which command_name         # Check if command is in PATH
whereis command_name       # Find command locations
type command_name          # Check command type (builtin, alias, function)
echo $PATH                 # Verify PATH contents

# Fix PATH issues
export PATH="/usr/local/bin:$PATH"  # Add directory to PATH
hash -r                            # Clear command cache
```

### Permission Denied
```bash
# Check file permissions and ownership
ls -la file_or_directory
stat file_or_directory
namei -mo /full/path/to/file

# Check user permissions
groups                     # Show current user groups
id                        # Show user and group IDs
sudo -l                   # Show sudo permissions
```

### Output Issues
```bash
# Handle different output scenarios
command 2>/dev/null        # Suppress error messages
command >/dev/null 2>&1    # Suppress all output
command | tee output.log   # Show and save output
command | less             # Page through output
```

### Pipeline Failures
```bash
# Debug pipeline issues
set -o pipefail           # Exit on any pipeline failure
command1 | command2 | command3
echo ${PIPESTATUS[@]}     # Check exit codes of all pipeline commands

# Test pipeline components individually
command1 > temp1.txt
command2 < temp1.txt > temp2.txt
command3 < temp2.txt
```

## Assessment Criteria

Students will be evaluated on their ability to:

| Criteria | Proficient (4) | Developing (3) | Beginning (2) | Inadequate (1) |
|----------|----------------|----------------|---------------|----------------|
| **Command Mastery** | Uses commands efficiently with appropriate options and combinations | Good command usage with minor inefficiencies | Basic command knowledge with guided usage | Limited command knowledge |
| **Pipeline Construction** | Builds complex, efficient pipelines with proper error handling | Creates functional pipelines with good structure | Basic pipeline construction with assistance | Difficulty creating effective pipelines |
| **Shell Customization** | Implements comprehensive, well-organized customizations | Good customization with useful features | Basic customization with simple improvements | Minimal or ineffective customization |
| **Problem Solving** | Efficiently solves complex problems using command-line tools | Good problem-solving with systematic approach | Basic problem-solving with guidance | Struggles to approach problems systematically |

## Next Steps

After mastering command-line essentials, proceed to:

- **Module 4: Package Management** - Apply command-line skills to software installation and management
- **Module 5: Processes & Services** - Use command-line tools for system process and service management
- **Module 9: Shell Scripting Fundamentals** - Build on command-line knowledge to create automation scripts

The command-line proficiency developed in this module is fundamental to all subsequent Linux administration tasks and provides the foundation for efficient system management and automation.
