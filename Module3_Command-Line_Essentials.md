# Module 3: Command-Line Essentials

## Overview
This module covers essential command-line skills that every Linux system administrator needs. You'll learn to navigate the filesystem, manipulate files and directories, and use powerful command-line tools effectively.

## Learning Objectives
By the end of this module, you will be able to:
- Navigate the Linux filesystem efficiently using command-line tools
- Create, modify, and manage files and directories
- Use pipes, redirection, and command chaining
- Search for files and content using various tools
- Understand and use text processing utilities
- Work with archives and compression

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

### 3.7 Archives and Compression
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

## Common Command Combinations

| Task | Command |
|------|---------|
| Find recently modified files | `find . -mtime -1 -type f` |
| Display running processes | `ps aux \| grep process_name` |
| Monitor file changes | `tail -f /var/log/syslog` |
| Count lines in files | `wc -l *.txt` |
| Search and replace in files | `sed 's/old/new/g' file.txt` |

## Best Practices
- Always use absolute paths in scripts
- Test destructive commands with `-n` (dry run) when available
- Use `less` instead of `cat` for large files
- Learn keyboard shortcuts for efficiency
- Use tab completion to avoid typos
- Keep command history clean and useful

## Lab Exercises
1. Create a directory structure for a web project
2. Find all files modified in the last 24 hours
3. Create a pipeline to find the most common words in a text file
4. Set up a backup script using tar and compression
5. Practice text processing with log files

## Next Steps
After mastering these command-line essentials, you'll be ready to tackle Package Management in Module 4, where you'll learn to install and manage software packages on different Linux distributions.
