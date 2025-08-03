# Module 3: Command-Line Essentials

## Overview
This module covers essential command-line skills that every Linux system administrator needs. You'll learn to navigate the filesystem, manipulate files and directories, and use powerful command-line tools effectively.

## Learning Objectives
By the end of this module, you will be able to:
- Navigate the Linux filesystem efficiently using command-line tools
- Create, modify, and manage files and directories
- Combine commands into powerful one-liners using pipes and redirection
- Use text-processing tools to extract, transform, and summarize data
- Create custom aliases and shell functions to streamline workflows
- Customize your shell prompt and environment for context-aware feedback
- Debug command sequences and inspect exit codes
- Work with archives and compression
- Automate repetitive tasks with environment variables and functions

## Topics

### 3.1 Shell Basics
- Understanding the shell environment
- Shell types (bash, zsh, sh)
- Command structure and syntax
- Command history and shortcuts
- Tab completion

### 3.2 Navigation and File Operations
- `pwd`, `cd`, `ls` commands
- Absolute vs relative paths
- Hidden files and directories
- Creating directories: `mkdir`
- Removing files and directories: `rm`, `rmdir`
- Copying and moving: `cp`, `mv`

### 3.3 File Content Management
- Viewing file contents: `cat`, `less`, `more`, `head`, `tail`
- Creating and editing files: `touch`, `nano`, `vim`
- File comparison: `diff`, `cmp`

### 3.4 Text Processing
- Searching text: `grep`, `egrep`, `fgrep`
- Text manipulation: `sed`, `awk`
- Sorting and uniqueness: `sort`, `uniq`
- Counting: `wc`
- Cut and paste: `cut`, `paste`

### 3.5 Pipes and Redirection
- Standard input, output, and error streams
- Output redirection: `>`, `>>`
- Input redirection: `<`
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

## Practical Examples

### Basic Navigation
```bash
# Show current directory
pwd

# List files with details
ls -la

# Change to home directory
cd ~

# Go up one directory
cd ..

# Create nested directories
mkdir -p projects/web/frontend
```

### File Operations
```bash
# Create empty file
touch newfile.txt

# Copy file
cp source.txt destination.txt

# Move/rename file
mv oldname.txt newname.txt

# Remove file (careful!)
rm unwanted.txt

# Remove directory and contents
rm -rf directory/
```

### Text Processing Pipeline
```bash
# Count unique users logged in
who | cut -d' ' -f1 | sort | uniq | wc -l

# Find large files
find /var/log -type f -size +100M -exec ls -lh {} \;

# Search for pattern in multiple files
grep -r "error" /var/log/ | head -10
```

### Working with Archives
```bash
# Create tar archive
tar -czf backup.tar.gz /home/user/documents/

# Extract tar archive
tar -xzf backup.tar.gz

# List archive contents
tar -tzf backup.tar.gz
```

### Shell Customization and Productivity

#### Environment Variables
```bash
# Set environment variables
export PATH="/usr/local/bin:$PATH"
export EDITOR="vim"
export BROWSER="firefox"

# Use variables in commands
echo "Home directory: $HOME"
echo "Current user: $USER"
echo "System hostname: $HOSTNAME"

# Custom variables for scripts
export PROJECT_DIR="/home/user/projects"
cd $PROJECT_DIR
```

#### Creating Aliases
```bash
# Common aliases for productivity
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'

# System administration aliases
alias ports='netstat -tulanp'
alias meminfo='free -m -l -t'
alias psmem='ps auxf | sort -nr -k 4'
alias pscpu='ps auxf | sort -nr -k 3'

# Git aliases
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'

# Make aliases permanent by adding to ~/.bashrc
echo "alias ll='ls -alF'" >> ~/.bashrc
```

#### Shell Functions
```bash
# Create reusable functions
# Function to create and enter directory
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Function to extract various archive types
extract() {
    if [ -f "$1" ]; then
        case "$1" in
            *.tar.bz2)   tar xjf "$1"     ;;
            *.tar.gz)    tar xzf "$1"     ;;
            *.bz2)       bunzip2 "$1"     ;;
            *.rar)       unrar x "$1"     ;;
            *.gz)        gunzip "$1"      ;;
            *.tar)       tar xf "$1"      ;;
            *.tbz2)      tar xjf "$1"     ;;
            *.tgz)       tar xzf "$1"     ;;
            *.zip)       unzip "$1"       ;;
            *.Z)         uncompress "$1"  ;;
            *.7z)        7z x "$1"        ;;
            *)           echo "Don't know how to extract '$1'" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}

# Function to find and kill processes
killps() {
    local process="$1"
    ps aux | grep "$process" | grep -v grep | awk '{print $2}' | xargs kill -9
}

# Function to show directory sizes
dirsize() {
    du -sh "${1:-.}"/* | sort -hr
}
```

#### Custom Shell Prompts
```bash
# Simple colored prompt
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Advanced prompt with git branch
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '

# Prompt with timestamp and exit code
export PS1='\[\033[0;37m\][\t]\[\033[0m\] \[\033[0;32m\]\u@\h\[\033[0m\]:\[\033[0;34m\]\w\[\033[0m\] [\$?]\$ '
```

### Debugging and Error Handling

#### Exit Codes and Error Checking
```bash
# Check exit code of last command
echo $?

# Command chaining with error handling
command1 && echo "Success" || echo "Failed"

# More complex error handling
if command1; then
    echo "Command succeeded"
    command2
else
    echo "Command failed with exit code $?"
    exit 1
fi

# Set options for debugging
set -e  # Exit on any command failure
set -u  # Exit on undefined variables
set -x  # Print commands before executing
set -o pipefail  # Exit if any command in pipeline fails

# Debug specific sections
set -x
complex_command_sequence
set +x
```

#### Advanced Command Combinations
```bash
# Monitor system resources in real-time
watch 'ps aux --sort=-%cpu | head -10'

# Find and replace across multiple files
find . -name "*.txt" -exec sed -i 's/old_text/new_text/g' {} \;

# Create backup before editing
cp file.txt{,.backup} && vim file.txt

# Show top 10 largest files
find /var/log -type f -exec ls -lh {} \; | sort -k5 -hr | head -10

# Network troubleshooting one-liner
ping -c 1 google.com && echo "Internet OK" || echo "No internet connection"

# System info summary
echo "System: $(uname -a)"; echo "Uptime: $(uptime)"; echo "Disk: $(df -h / | tail -1)"
```

## Common Command Combinations

| Task | Command |
|------|---------|
| Find recently modified files | `find . -mtime -1 -type f` |
| Display running processes | `ps aux \| grep process_name` |
| Monitor file changes | `tail -f /var/log/syslog` |
| Count lines in files | `wc -l *.txt` |
| Search and replace in files | `sed 's/old/new/g' file.txt` |
| Show top CPU processes | `ps aux --sort=-%cpu \| head -10` |
| Find large files | `find /var -size +100M -type f 2>/dev/null` |
| Archive with date | `tar -czf backup-$(date +%Y%m%d).tar.gz /home/user` |
| Monitor disk usage | `watch -n 1 'df -h'` |
| Network connectivity test | `ping -c 1 8.8.8.8 && echo "Connected" \|\| echo "No connection"` |

## Shell Configuration Best Practices

### ~/.bashrc Configuration Example
```bash
# ~/.bashrc - Personal shell configuration

# History settings
HISTSIZE=10000
HISTFILESIZE=20000
HISTCONTROL=ignoredups:ignorespace
shopt -s histappend

# Shell options
shopt -s checkwinsize
shopt -s globstar

# Custom aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# System aliases
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias ports='netstat -tulanp'

# Custom functions
source ~/.bash_functions

# Custom prompt
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Environment variables
export EDITOR='vim'
export PAGER='less'
export BROWSER='firefox'
```

## Best Practices
- Always use absolute paths in scripts
- Test destructive commands with `-n` (dry run) when available
- Use `less` instead of `cat` for large files
- Learn keyboard shortcuts for efficiency
- Use tab completion to avoid typos
- Keep command history clean and useful
- Create meaningful aliases for frequently used commands
- Use functions for complex, reusable command sequences
- Always check exit codes in scripts and automation
- Customize your environment to match your workflow
- Use descriptive variable names in scripts
- Comment complex command combinations for future reference

## Productivity Tips and Tricks

### Keyboard Shortcuts
| Shortcut | Action |
|----------|--------|
| `Ctrl+A` | Move to beginning of line |
| `Ctrl+E` | Move to end of line |
| `Ctrl+L` | Clear screen |
| `Ctrl+R` | Search command history |
| `Ctrl+C` | Cancel current command |
| `Ctrl+Z` | Suspend current process |
| `Alt+.` | Insert last argument from previous command |
| `!!` | Repeat last command |
| `!$` | Last argument of previous command |

### History Management
```bash
# Search history
history | grep "search_term"

# Execute command from history
!123  # Execute command number 123
!ssh  # Execute last command starting with "ssh"

# History expansion
^old^new  # Replace "old" with "new" in last command
!:1-3     # Arguments 1-3 from last command

## Lab Exercises
1. Create a directory structure for a web project
2. Find all files modified in the last 24 hours
3. Create a pipeline to find the most common words in a text file
4. Set up a backup script using tar and compression
5. Practice text processing with log files
6. **NEW**: Create custom aliases for your most frequently used commands
7. **NEW**: Write a shell function that creates a project directory structure
8. **NEW**: Customize your shell prompt to show current git branch and exit codes
9. **NEW**: Create a debugging session using `set -x` to trace command execution
10. **NEW**: Build a one-liner to monitor system resources and alert on high usage

## Next Steps
After mastering these command-line essentials, you'll be ready to tackle Package Management in Module 4, where you'll learn to install and manage software packages on different Linux distributions.
