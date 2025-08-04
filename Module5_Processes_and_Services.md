# Module 5: Processes & Services

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [5.1 Process Basics](#51-process-basics)
  - [5.2 Process Monitoring](#52-process-monitoring)
  - [5.3 Process Control](#53-process-control)
  - [5.4 Basic Service Management](#54-basic-service-management)
  - [5.5 Essential Systemd Operations](#55-essential-systemd-operations)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
- [Lab Exercises](#lab-exercises)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Summary](#summary)

## Overview
Learn the essential skills for managing processes and services in Linux systems. This module covers the fundamental commands and concepts needed to monitor running processes, control system services, and troubleshoot basic performance issues.

**What You'll Learn:**
- How to view and monitor running processes
- Basic process control and management
- Understanding Linux services and systemd
- Common troubleshooting techniques
- Essential command-line tools for system monitoring

## Learning Objectives
By the end of this module, you will be able to:

1. **View Running Processes**: Use `ps`, `top`, and `htop` to see what's running on your system
2. **Monitor System Activity**: Check CPU and memory usage with basic monitoring tools
3. **Control Processes**: Start, stop, and manage processes safely
4. **Manage Services**: Start, stop, and check the status of system services
5. **Use Systemd Basics**: Understand and use basic systemd commands
6. **Troubleshoot Issues**: Find and fix common process and service problems

## Topics

### 5.1 Process Basics
- What is a process and how it works
- Process identification (PID) and process states
- Parent and child processes
- Foreground vs background processes
- Understanding process hierarchy

### 5.2 Process Monitoring
- Using `ps` command to list processes
- Real-time monitoring with `top` and `htop`
- Finding processes with `pgrep` and `pidof`
- Checking process resource usage
- Basic performance monitoring

### 5.3 Process Control
- Starting and stopping processes
- Using signals to control processes (`kill`, `killall`)
- Background job control (`&`, `jobs`, `fg`, `bg`)
- Keeping processes running with `nohup`
- Basic process priority with `nice`

### 5.4 Basic Service Management
- Understanding Linux services and daemons
- What is systemd and why it's important
- Service states: active, inactive, failed
- Common system services (web servers, databases, etc.)

### 5.5 Essential Systemd Operations
- Starting and stopping services with `systemctl`
- Checking service status and logs
- Enabling and disabling services at boot
- Restarting and reloading services
- Basic troubleshooting with `journalctl`

## Essential Command Reference

### Process Monitoring Commands

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `ps` | List running processes | `ps aux`, `ps -ef` |
| `top` | Real-time process monitor | `top`, `top -u username` |
| `htop` | Enhanced process monitor | `htop` (interactive) |
| `pgrep` | Find process by name | `pgrep nginx`, `pgrep -u user` |
| `pidof` | Get PID of process | `pidof nginx` |

### Process Control Commands

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `kill` | Terminate process by PID | `kill 1234`, `kill -9 1234` |
| `killall` | Kill processes by name | `killall firefox` |
| `pkill` | Kill processes by pattern | `pkill -f "java.*tomcat"` |
| `nohup` | Run process immune to hangups | `nohup command &` |
| `jobs` | List background jobs | `jobs`, `jobs -l` |
| `fg` | Bring job to foreground | `fg`, `fg %1` |
| `bg` | Send job to background | `bg %1` |

### Service Management Commands

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `systemctl status` | Check service status | `systemctl status nginx` |
| `systemctl start` | Start a service | `systemctl start apache2` |
| `systemctl stop` | Stop a service | `systemctl stop mysql` |
| `systemctl restart` | Restart a service | `systemctl restart sshd` |
| `systemctl enable` | Enable service at boot | `systemctl enable nginx` |
| `systemctl disable` | Disable service at boot | `systemctl disable apache2` |
| `journalctl` | View service logs | `journalctl -u nginx`, `journalctl -f` |

### System Monitoring Commands

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `uptime` | System load and uptime | `uptime` |
| `free` | Memory usage | `free -h` |
| `df` | Disk usage | `df -h` |
| `who` | Who is logged in | `who`, `w` |

## Lab Exercises

### Lab 1: Basic Process Monitoring
**Objective:** Learn to monitor and understand running processes.

**Tasks:**
1. Use `ps aux` to view all running processes
2. Use `top` to monitor processes in real-time
3. Install and use `htop` for enhanced monitoring
4. Find processes by name using `pgrep` and `pidof`
5. Practice sorting processes by CPU and memory usage

**Exercises:**
```bash
# View all processes
ps aux

# Find your own processes
ps ux

# Find Firefox processes
pgrep firefox
ps aux | grep firefox

# Monitor system in real-time
top
htop

# Sort processes by CPU usage
ps aux --sort=-%cpu | head -10

# Sort processes by memory usage
ps aux --sort=-%mem | head -10
```

**Deliverables:**
- Screenshots of `ps`, `top`, and `htop` output
- List of the top 5 CPU and memory consuming processes
- Documentation of what each process does

### Lab 2: Process Control Practice
**Objective:** Learn to control processes safely.

**Tasks:**
1. Start processes in the background
2. Practice job control (`jobs`, `fg`, `bg`)
3. Use `kill` to terminate processes safely
4. Use `nohup` to run persistent processes
5. Practice graceful vs forceful process termination

**Exercises:**
```bash
# Start a long-running process in background
sleep 300 &

# Check background jobs
jobs

# Bring job to foreground
fg %1

# Send job back to background (Ctrl+Z, then bg)
bg %1

# Kill the process gracefully
kill %1

# Start a persistent process
nohup sleep 600 &

# Kill it when done
kill $(pgrep sleep)
```

**Deliverables:**
- Command history showing job control
- Examples of graceful process termination
- Documentation of when to use `kill` vs `kill -9`

### Lab 3: Basic Service Management
**Objective:** Learn to manage system services with systemd.

**Tasks:**
1. Check status of common services
2. Practice starting and stopping services
3. Enable and disable services at boot
4. View service logs with `journalctl`
5. Troubleshoot a failing service

**Exercises:**
```bash
# Check service status
systemctl status nginx
systemctl status ssh
systemctl status cron

# List all active services
systemctl list-units --type=service --state=active

# List failed services
systemctl list-units --type=service --state=failed

# Start/stop a service (if installed)
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx

# Enable/disable service at boot
sudo systemctl enable nginx
sudo systemctl disable nginx
systemctl is-enabled nginx

# View service logs
journalctl -u nginx
journalctl -u nginx -f
journalctl -u nginx --since "1 hour ago"
```

**Deliverables:**
- List of active services on your system
- Examples of starting/stopping services
- Service log analysis for at least one service
- Documentation of enabled vs disabled services

## Best Practices

### Process Management Best Practices

1. **Monitor Regularly**
   - Check system load with `uptime` and `top`
   - Look for processes using too much CPU or memory
   - Be aware of what's running on your system

2. **Kill Processes Safely**
   - Try `kill PID` first (graceful termination)
   - Use `kill -9 PID` only when necessary (forceful kill)
   - Always check if the process actually stopped

3. **Use Background Jobs Wisely**
   - Use `&` for long-running commands
   - Use `nohup` for processes that should survive logout
   - Keep track of background jobs with `jobs`

4. **Keep It Simple**
   - Don't run unnecessary processes
   - Close applications you're not using
   - Monitor system resources regularly

### Service Management Best Practices

1. **Check Before Making Changes**
   - Always check service status before starting/stopping
   - Understand what a service does before disabling it
   - Check dependencies before making changes

2. **Use Proper Commands**
   - Use `systemctl` for service management
   - Use `journalctl` to check logs when troubleshooting
   - Always use `sudo` when starting/stopping services

3. **Document Changes**
   - Keep track of what services you enable/disable
   - Document why you made specific changes
   - Test changes in a safe environment first

4. **Security Awareness**
   - Don't run unnecessary services
   - Keep services updated
   - Monitor service logs for unusual activity
   - Use socket activation for on-demand services
   - Configure appropriate resource limits
   - Optimize startup dependencies
   - Implement efficient logging strategies

### Signal Management Guidelines

1. **Signal Selection**
   - Use SIGTERM for graceful shutdown requests
   - Reserve SIGKILL for unresponsive processes
   - Use SIGHUP for configuration reloading
   - Implement custom signal handlers for application-specific needs

2. **Timeout Management**
   - Allow reasonable time for graceful shutdown
   - Implement escalation procedures (TERM → KILL)
   - Monitor signal response times
   - Log signal handling events

## Troubleshooting

### Common Process Problems

#### System Running Slow
**Problem:** Computer feels sluggish or unresponsive
**Solutions:**
```bash
# Check what's using CPU
top
ps aux --sort=-%cpu | head -10

# Check memory usage
free -h
ps aux --sort=-%mem | head -10

# Check system load
uptime
```

#### Process Won't Stop
**Problem:** Can't kill a process with normal `kill` command
**Solutions:**
```bash
# Try graceful kill first
kill PID

# If that doesn't work, force kill
kill -9 PID

# For processes by name
killall process_name
pkill process_name
```

#### Process Using Too Much Memory
**Problem:** A process is consuming excessive memory
**Solutions:**
```bash
# Find memory-hungry processes
ps aux --sort=-%mem | head -10

# Monitor specific process
top -p PID

# If safe to do so, restart the process
kill PID
# Then restart the application
```

### Common Service Problems

#### Service Won't Start
**Problem:** `systemctl start` fails
**Solutions:**
```bash
# Check detailed status
systemctl status service-name

# Check recent logs
journalctl -u service-name -n 20

# Common fixes:
# 1. Check if another service is using the same port
# 2. Verify configuration files
# 3. Check file permissions
# 4. Ensure dependencies are running
```

#### Service Keeps Stopping
**Problem:** Service starts but stops shortly after
**Solutions:**
```bash
# Monitor logs in real-time
journalctl -u service-name -f

# Check for error messages
journalctl -u service-name | grep -i error

# Check configuration
systemctl status service-name
```

#### Can't Connect to Service
**Problem:** Service appears running but can't connect
**Solutions:**
```bash
# Verify service is actually running
systemctl status service-name
ps aux | grep service-name

# Check if service is listening on expected port
ss -tulpn | grep port-number

# Try restarting the service
sudo systemctl restart service-name
```

### General Troubleshooting Steps

1. **Identify the Problem**
   - What exactly is not working?
   - When did it start happening?
   - What changed recently?

2. **Gather Information**
   - Check system load: `uptime`
   - Check memory: `free -h`
   - Check disk space: `df -h`
   - Check processes: `ps aux`

3. **Check Logs**
   - System logs: `journalctl`
   - Service logs: `journalctl -u service-name`
   - Check recent entries: `journalctl --since "1 hour ago"`

4. **Try Simple Fixes First**
   - Restart the problematic service
   - Check configuration files
   - Verify permissions

5. **Document and Learn**
   - Note what worked
   - Keep track of common problems
   - Remember solutions for next time

## Summary

This module covered the essential skills for managing processes and services in Linux systems. You learned:

### Key Concepts Covered
- **Process Monitoring**: Using `ps`, `top`, and `htop` to monitor system activity
- **Process Control**: Starting, stopping, and managing processes safely
- **Service Management**: Using systemd to control system services
- **Basic Troubleshooting**: Finding and fixing common process and service issues

### Essential Commands Mastered
- `ps aux` - List all running processes
- `top` and `htop` - Real-time system monitoring
- `kill`, `killall`, `pkill` - Process termination
- `systemctl` - Service management (start, stop, status, enable, disable)
- `journalctl` - View service logs
- `jobs`, `fg`, `bg` - Job control

### Best Practices Applied
- Always try graceful process termination before force killing
- Monitor system resources regularly
- Check service logs when troubleshooting
- Use proper commands for service management
- Document changes and solutions

## Next Steps

Continue building your Linux administration skills with:

- **Module 6: Users, Groups & Authentication** - Learn user and permission management
- **Module 7: Networking Fundamentals** - Understand network configuration
- **Module 8: Logging and Monitoring** - Advanced system monitoring and log analysis

The process and service management skills from this module are fundamental for maintaining stable Linux systems and will be used throughout your system administration career.
# Basic top usage
top

# Show processes for specific user
top -u username

# Sort by memory usage (press 'M' while in top)
# Sort by CPU usage (press 'P' while in top)
# Quit top (press 'q')
```

#### Using htop (Enhanced Process Monitor)
```bash
# Install htop if not available
sudo apt install htop    # Ubuntu/Debian
sudo yum install htop    # CentOS/RHEL

# Run htop
htop

# htop shortcuts:
# F1 - Help
# F9 - Kill process
# F10 - Quit
# Arrow keys to navigate
# Space to tag processes
```

### Finding Processes

#### Find Process by Name
```bash
# Find process by name
pgrep firefox
pgrep -l firefox    # Show name and PID

# Find process ID by exact name
pidof firefox

# Search for processes containing a pattern
ps aux | grep apache
```

### Basic Process Control

#### Starting and Stopping Processes
```bash
# Start a process in background
command &

# Example: Start a long-running process
sleep 300 &

# Check background jobs
jobs

# Bring a job to foreground
fg %1

# Send a job to background
bg %1
```

#### Killing Processes
```bash
# Kill process by PID (graceful)
kill 1234

# Force kill process (when normal kill doesn't work)
kill -9 1234

# Kill all processes with a specific name
killall firefox

# Kill processes by name pattern
pkill -f "java.*tomcat"
```

#### Using nohup for Persistent Processes
```bash
# Run a command that continues after logout
nohup long-running-command &

# Check the output
tail -f nohup.out
```

### Basic Service Management

#### Checking Service Status
```bash
# Check if a service is running
systemctl status nginx
systemctl status apache2
systemctl status ssh

# List all active services
systemctl list-units --type=service --state=active

# List all failed services
systemctl list-units --type=service --state=failed
```

#### Starting and Stopping Services
```bash
# Start a service
sudo systemctl start nginx

# Stop a service
sudo systemctl stop nginx

# Restart a service
sudo systemctl restart nginx

# Reload service configuration (without stopping)
sudo systemctl reload nginx
```

#### Managing Services at Boot
```bash
# Enable service to start at boot
sudo systemctl enable nginx

# Disable service from starting at boot
sudo systemctl disable nginx

# Check if service is enabled
systemctl is-enabled nginx
```

### Viewing Service Logs

#### Using journalctl
```bash
# View logs for a specific service
journalctl -u nginx

# Follow logs in real-time
journalctl -u nginx -f

# View logs from the last hour
journalctl -u nginx --since "1 hour ago"

# View logs from today
journalctl -u nginx --since today

# View last 50 lines of logs
journalctl -u nginx -n 50
```

### Simple System Monitoring

#### Check System Load and Memory
```bash
# Show system uptime and load
uptime

# Show memory usage
free -h

# Show disk usage
df -h

# Show who is logged in
who
w
```

#### Quick Process Information
```bash
# Show top 10 CPU-using processes
ps aux --sort=-%cpu | head -10

# Show top 10 memory-using processes
ps aux --sort=-%mem | head -10

# Count total number of processes
ps aux | wc -l
```

### Common Troubleshooting Examples

#### Find High CPU Usage
```bash
# Find processes using most CPU
top -n 1 | head -20

# Or using ps
ps aux --sort=-%cpu | head -10
```

#### Find High Memory Usage
```bash
# Find processes using most memory
ps aux --sort=-%mem | head -10

# Show memory usage summary
free -h
```

#### Check if a Service is Running
```bash
# Multiple ways to check nginx
systemctl status nginx
pgrep nginx
ps aux | grep nginx
```

#### Restart a Stuck Service
```bash
# Try graceful restart first
sudo systemctl restart nginx

# If that fails, stop and start
sudo systemctl stop nginx
sudo systemctl start nginx

# Check status after restart
systemctl status nginx
```
    echo "High Memory Usage (>80%):"
    ps aux | awk '$4 > 80 {printf "PID: %-6s User: %-8s MEM: %-6s%% Command: %s\n", $2, $1, $4, $11}'
    echo ""
    
    # Zombie processes
    echo "Zombie Processes:"
    ps aux | awk '$8 ~ /^Z/ {printf "PID: %-6s PPID: %-6s User: %-8s Command: %s\n", $2, $3, $1, $11}'
    echo ""
    
    # Processes in uninterruptible sleep
    echo "Processes in Uninterruptible Sleep (possible I/O issues):"
    ps aux | awk '$8 ~ /^D/ {printf "PID: %-6s User: %-8s Command: %s\n", $2, $1, $11}'
    echo ""
    
    # Processes with many open files
    echo "Processes with High File Descriptor Count (>1000):"
    for pid in $(ps -eo pid --no-headers); do
        if [[ -d "/proc/$pid/fd" ]]; then
            local fd_count=$(ls /proc/$pid/fd 2>/dev/null | wc -l)
            if [[ $fd_count -gt 1000 ]]; then
                local cmd=$(ps -p "$pid" -o comm --no-headers 2>/dev/null)
                echo "PID: $pid FDs: $fd_count Command: $cmd"
            fi
        fi
    done
    echo ""
}

# Process tree visualization
show_process_tree() {
    local root_pid="${1:-1}"
    
    echo "=== Process Tree (starting from PID $root_pid) ==="
    
    # Enhanced pstree with additional information
    if command -v pstree &>/dev/null; then
        pstree -p -a "$root_pid"
    else
        # Fallback to ps-based tree
        ps -eo pid,ppid,user,comm --sort=ppid | awk -v root="$root_pid" '
        BEGIN { indent[root] = 0 }
        $2 in indent {
            pid = $1; ppid = $2; user = $3; comm = $4
            level = indent[ppid] + 1
            indent[pid] = level
            for(i=0; i<level; i++) printf "  "
            printf "├─ %s(%s) - %s\n", comm, pid, user
        }'
    fi
}

# Usage examples
case "${1:-help}" in
    "analyze")
        analyze_system_processes
        ;;
    "monitor")
        monitor_process "$2" "$3" "$4"
        ;;
    "problems")
        find_problematic_processes
        ;;
    "tree")
        show_process_tree "$2"
        ;;
    "help")
        echo "Usage: $0 {analyze|monitor|problems|tree} [arguments]"
        echo "  analyze                    - System-wide process analysis"
        echo "  monitor <PID> [dur] [int]  - Monitor specific process"
        echo "  problems                   - Find problematic processes"
        echo "  tree [PID]                 - Show process tree"
        ;;
esac
```

#### Real-time Process Monitoring Dashboard
```bash
#!/bin/bash
# process-dashboard.sh - Real-time process monitoring dashboard

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[0;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# Dashboard refresh rate
REFRESH_INTERVAL=2

# Clear screen and move cursor to top
clear_screen() {
    clear
    tput cup 0 0
}

# Display system overview
show_system_overview() {
    echo -e "${BLUE}=== SYSTEM OVERVIEW ===${NC}"
    echo "Hostname: $(hostname)"
    echo "Uptime: $(uptime -p)"
    echo "Load: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
    echo ""
    
    # CPU information
    local cpu_count=$(nproc)
    local cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | sed 's/%us,//')
    echo -e "CPU Cores: $cpu_count | Usage: ${YELLOW}${cpu_usage}%${NC}"
    
    # Memory information
    local mem_info=$(free -h | grep Mem)
    local mem_used=$(echo "$mem_info" | awk '{print $3}')
    local mem_total=$(echo "$mem_info" | awk '{print $2}')
    local mem_percent=$(echo "$mem_info" | awk '{printf "%.1f", $3/$2*100}')
    echo -e "Memory: ${YELLOW}${mem_used}${NC}/${mem_total} (${mem_percent}%)"
    
    # Disk usage for root
    local disk_info=$(df -h / | tail -1)
    local disk_used=$(echo "$disk_info" | awk '{print $3}')
    local disk_total=$(echo "$disk_info" | awk '{print $2}')
    local disk_percent=$(echo "$disk_info" | awk '{print $5}')
    echo -e "Disk (/): ${YELLOW}${disk_used}${NC}/${disk_total} (${disk_percent})"
    echo ""
}

# Display top processes
show_top_processes() {
    echo -e "${GREEN}=== TOP 10 PROCESSES BY CPU ===${NC}"
    printf "%-8s %-6s %-6s %-6s %-8s %s\n" "USER" "PID" "CPU%" "MEM%" "TIME" "COMMAND"
    echo "--------------------------------------------------------------"
    ps aux --sort=-%cpu | head -11 | tail -10 | while read line; do
        local user=$(echo "$line" | awk '{print $1}')
        local pid=$(echo "$line" | awk '{print $2}')
        local cpu=$(echo "$line" | awk '{print $3}')
        local mem=$(echo "$line" | awk '{print $4}')
        local time=$(echo "$line" | awk '{print $10}')
        local cmd=$(echo "$line" | awk '{for(i=11;i<=NF;i++) printf "%s ", $i; print ""}' | cut -c1-30)
        
        # Color coding based on CPU usage
        if (( $(echo "$cpu > 80" | bc -l) )); then
            printf "${RED}%-8s %-6s %-6s %-6s %-8s %s${NC}\n" "$user" "$pid" "$cpu" "$mem" "$time" "$cmd"
        elif (( $(echo "$cpu > 50" | bc -l) )); then
            printf "${YELLOW}%-8s %-6s %-6s %-6s %-8s %s${NC}\n" "$user" "$pid" "$cpu" "$mem" "$time" "$cmd"
        else
            printf "%-8s %-6s %-6s %-6s %-8s %s\n" "$user" "$pid" "$cpu" "$mem" "$time" "$cmd"
        fi
    done
    echo ""
}

# Display service status
show_service_status() {
    echo -e "${BLUE}=== CRITICAL SERVICES STATUS ===${NC}"
    
    local services=("sshd" "nginx" "apache2" "mysql" "postgresql" "docker" "network")
    
    for service in "${services[@]}"; do
        if systemctl list-unit-files | grep -q "^${service}"; then
            local status=$(systemctl is-active "$service" 2>/dev/null)
            local enabled=$(systemctl is-enabled "$service" 2>/dev/null)
            
            case "$status" in
                "active")
                    echo -e "${service}: ${GREEN}Active${NC} (${enabled})"
                    ;;
                "inactive")
                    echo -e "${service}: ${YELLOW}Inactive${NC} (${enabled})"
                    ;;
                "failed")
                    echo -e "${service}: ${RED}Failed${NC} (${enabled})"
                    ;;
                *)
                    echo -e "${service}: ${RED}Unknown${NC} (${enabled})"
                    ;;
            esac
        fi
    done
    echo ""
}

# Display network connections
show_network_activity() {
    echo -e "${GREEN}=== ACTIVE NETWORK CONNECTIONS ===${NC}"
    echo "Listening Services:"
    ss -tulpn | grep LISTEN | head -8 | while read line; do
        local proto=$(echo "$line" | awk '{print $1}')
        local local_addr=$(echo "$line" | awk '{print $5}')
        local process=$(echo "$line" | awk '{print $7}' | sed 's/users:((//' | sed 's/))//' | cut -d',' -f1)
        printf "%-6s %-20s %s\n" "$proto" "$local_addr" "$process"
    done
    echo ""
}

# Main dashboard loop
run_dashboard() {
    while true; do
        clear_screen
        
        echo -e "${BLUE}╔══════════════════════════════════════════════════════════════╗${NC}"
        echo -e "${BLUE}║                    PROCESS MONITORING DASHBOARD              ║${NC}"
        echo -e "${BLUE}║                    Press Ctrl+C to exit                      ║${NC}"
        echo -e "${BLUE}╚══════════════════════════════════════════════════════════════╝${NC}"
        echo ""
        
        show_system_overview
        show_top_processes
        show_service_status
        show_network_activity
        
        echo -e "${BLUE}Last updated: $(date)${NC}"
        echo -e "${BLUE}Next refresh in ${REFRESH_INTERVAL} seconds...${NC}"
        
        sleep "$REFRESH_INTERVAL"
    done
}

# Handle command line arguments
case "${1:-dashboard}" in
    "dashboard")
        run_dashboard
        ;;
    "overview")
        show_system_overview
        ;;
    "processes")
        show_top_processes
        ;;
    "services")
        show_service_status
        ;;
    "network")
        show_network_activity
        ;;
    "help")
        echo "Usage: $0 {dashboard|overview|processes|services|network}"
        ;;
esac
```

### Signal Management and Process Control

#### Comprehensive Signal Management
```bash
#!/bin/bash
# signal-manager.sh - Advanced signal handling and process control

# Signal information
declare -A SIGNALS=(
    ["TERM"]="15"    # Graceful termination
    ["KILL"]="9"     # Force kill
    ["HUP"]="1"      # Hangup/reload config
    ["INT"]="2"      # Interrupt (Ctrl+C)
    ["QUIT"]="3"     # Quit (Ctrl+\)
    ["STOP"]="19"    # Stop process
    ["CONT"]="18"    # Continue process
    ["USR1"]="10"    # User signal 1
    ["USR2"]="12"    # User signal 2
    ["PIPE"]="13"    # Broken pipe
    ["ALRM"]="14"    # Alarm signal
    ["CHLD"]="17"    # Child status changed
)

# Graceful process termination
graceful_terminate() {
    local target="$1"
    local timeout="${2:-30}"
    
    if [[ -z "$target" ]]; then
        echo "Usage: graceful_terminate <PID|process_name> [timeout]"
        return 1
    fi
    
    # Determine if target is PID or process name
    if [[ "$target" =~ ^[0-9]+$ ]]; then
        local pids=("$target")
    else
        readarray -t pids < <(pgrep -f "$target")
    fi
    
    if [[ ${#pids[@]} -eq 0 ]]; then
        echo "No processes found matching: $target"
        return 1
    fi
    
    echo "Found ${#pids[@]} process(es) to terminate gracefully:"
    for pid in "${pids[@]}"; do
        if [[ -d "/proc/$pid" ]]; then
            local cmd=$(ps -p "$pid" -o comm --no-headers 2>/dev/null)
            echo "  PID: $pid Command: $cmd"
        fi
    done
    
    # Step 1: Send TERM signal
    echo "Sending SIGTERM..."
    for pid in "${pids[@]}"; do
        if [[ -d "/proc/$pid" ]]; then
            kill -TERM "$pid" 2>/dev/null
        fi
    done
    
    # Wait for graceful shutdown
    local waited=0
    while [[ $waited -lt $timeout ]]; do
        local remaining_pids=()
        for pid in "${pids[@]}"; do
            if [[ -d "/proc/$pid" ]]; then
                remaining_pids+=("$pid")
            fi
        done
        
        if [[ ${#remaining_pids[@]} -eq 0 ]]; then
            echo "All processes terminated gracefully"
            return 0
        fi
        
        sleep 1
        ((waited++))
        
        if [[ $((waited % 5)) -eq 0 ]]; then
            echo "Waiting for graceful shutdown... (${waited}s/${timeout}s)"
        fi
    done
    
    # Step 2: Force termination if needed
    echo "Timeout reached. Force terminating remaining processes..."
    for pid in "${remaining_pids[@]}"; do
        if [[ -d "/proc/$pid" ]]; then
            echo "Force killing PID: $pid"
            kill -KILL "$pid" 2>/dev/null
        fi
    done
    
    # Final check
    sleep 1
    local still_running=()
    for pid in "${pids[@]}"; do
        if [[ -d "/proc/$pid" ]]; then
            still_running+=("$pid")
        fi
    done
    
    if [[ ${#still_running[@]} -eq 0 ]]; then
        echo "All processes terminated successfully"
        return 0
    else
        echo "Warning: Some processes still running: ${still_running[*]}"
        return 1
    fi
}

# Process signal monitoring
monitor_signals() {
    local pid="$1"
    local duration="${2:-60}"
    
    if [[ -z "$pid" ]]; then
        echo "Usage: monitor_signals <PID> [duration]"
        return 1
    fi
    
    echo "Monitoring signals for PID $pid (duration: ${duration}s)"
    echo "Signal monitoring requires strace..."
    
    if ! command -v strace &>/dev/null; then
        echo "strace not found. Install with: apt install strace (Debian/Ubuntu) or yum install strace (RHEL/CentOS)"
        return 1
    fi
    
    # Monitor system calls related to signal handling
    timeout "$duration" strace -p "$pid" -e signal=all -o /tmp/signal_trace_$$.txt 2>&1 &
    local strace_pid=$!
    
    echo "Monitoring started (PID: $strace_pid). Press Ctrl+C to stop early."
    
    # Wait for completion or interruption
    wait "$strace_pid" 2>/dev/null
    
    if [[ -f "/tmp/signal_trace_$$.txt" ]]; then
        echo "Signal trace results:"
        grep -E "(killed by|SIGTERM|SIGKILL|SIGHUP|SIGINT)" "/tmp/signal_trace_$$.txt" || echo "No significant signals detected"
        rm -f "/tmp/signal_trace_$$.txt"
    fi
}

# Process control with job management
advanced_job_control() {
    echo "=== Advanced Job Control Demo ==="
    
    # Start some background jobs
    echo "Starting background jobs..."
    
    # Long-running background job 1
    (sleep 300; echo "Job 1 completed") &
    local job1_pid=$!
    echo "Started job 1 (PID: $job1_pid)"
    
    # Long-running background job 2
    (while true; do echo "Job 2 heartbeat: $(date)"; sleep 10; done) &
    local job2_pid=$!
    echo "Started job 2 (PID: $job2_pid)"
    
    # Show job status
    echo ""
    echo "Current jobs:"
    jobs -l
    
    echo ""
    echo "Job control commands:"
    echo "  jobs -l           # List all jobs with PIDs"
    echo "  fg %1             # Bring job 1 to foreground"
    echo "  bg %2             # Send job 2 to background"
    echo "  kill %1           # Kill job 1"
    echo "  kill $job1_pid    # Kill by PID"
    echo "  disown %2         # Remove job from shell's job table"
    
    # Cleanup demonstration jobs
    echo ""
    echo "Cleaning up demo jobs..."
    kill "$job1_pid" "$job2_pid" 2>/dev/null
    wait "$job1_pid" "$job2_pid" 2>/dev/null
    echo "Demo complete"
}

# Signal testing and validation
test_signal_handling() {
    local target_program="$1"
    
    if [[ -z "$target_program" ]]; then
        echo "Usage: test_signal_handling <program_or_script>"
        return 1
    fi
    
    echo "=== Signal Handling Test for: $target_program ==="
    
    # Start the target program
    echo "Starting target program..."
    "$target_program" &
    local target_pid=$!
    
    if ! kill -0 "$target_pid" 2>/dev/null; then
        echo "Failed to start target program"
        return 1
    fi
    
    echo "Target program started (PID: $target_pid)"
    
    # Test various signals
    local signals_to_test=("USR1" "USR2" "HUP" "TERM")
    
    for signal in "${signals_to_test[@]}"; do
        echo ""
        echo "Testing signal: SIG$signal"
        
        if kill -0 "$target_pid" 2>/dev/null; then
            kill -"$signal" "$target_pid"
            sleep 2
            
            if kill -0 "$target_pid" 2>/dev/null; then
                echo "  Process survived SIG$signal"
            else
                echo "  Process terminated by SIG$signal"
                break
            fi
        else
            echo "  Process no longer running"
            break
        fi
    done
    
    # Final cleanup
    if kill -0 "$target_pid" 2>/dev/null; then
        echo ""
        echo "Cleaning up: sending SIGTERM"
        kill -TERM "$target_pid"
        sleep 2
        
        if kill -0 "$target_pid" 2>/dev/null; then
            echo "Force killing with SIGKILL"
            kill -KILL "$target_pid"
        fi
    fi
    
    echo "Signal handling test complete"
}

# Usage
case "${1:-help}" in
    "terminate")
        graceful_terminate "$2" "$3"
        ;;
    "monitor")
        monitor_signals "$2" "$3"
        ;;
    "jobs")
        advanced_job_control
        ;;
    "test")
        test_signal_handling "$2"
        ;;
    "help")
        echo "Usage: $0 {terminate|monitor|jobs|test} [arguments]"
        echo "  terminate <PID|name> [timeout] - Graceful process termination"
        echo "  monitor <PID> [duration]       - Monitor signals for process"
        echo "  jobs                           - Demonstrate job control"
        echo "  test <program>                 - Test signal handling"
        ;;
esac
```

### Systemd Service Operations

#### Advanced Systemd Management
```bash
#!/bin/bash
# systemd-manager.sh - Comprehensive systemd service management

# Service analysis and diagnostics
analyze_service() {
    local service="$1"
    
    if [[ -z "$service" ]]; then
        echo "Usage: analyze_service <service_name>"
        return 1
    fi
    
    # Ensure .service suffix
    [[ "$service" != *.service ]] && service="${service}.service"
    
    echo "=== Service Analysis: $service ==="
    echo ""
    
    # Basic service information
    echo "=== Basic Information ==="
    systemctl show "$service" --property=LoadState,ActiveState,SubState,UnitFileState,ExecMainPID 2>/dev/null
    echo ""
    
    # Service status
    echo "=== Detailed Status ==="
    systemctl status "$service" --no-pager -l
    echo ""
    
    # Service dependencies
    echo "=== Dependencies ==="
    echo "Required by:"
    systemctl list-dependencies --reverse "$service" --plain | head -10
    echo ""
    echo "Requires:"
    systemctl list-dependencies "$service" --plain | head -10
    echo ""
    
    # Recent logs
    echo "=== Recent Logs (last 20 entries) ==="
    journalctl -u "$service" -n 20 --no-pager
    echo ""
    
    # Resource usage
    echo "=== Resource Usage ==="
    local main_pid=$(systemctl show "$service" --property=MainPID --value 2>/dev/null)
    if [[ -n "$main_pid" && "$main_pid" != "0" ]]; then
        echo "Main PID: $main_pid"
        ps -p "$main_pid" -o pid,ppid,%cpu,%mem,vsz,rss,etime,cmd --no-headers 2>/dev/null
        
        # Memory details
        if [[ -f "/proc/$main_pid/status" ]]; then
            echo ""
            echo "Memory details:"
            grep -E "(VmPeak|VmSize|VmRSS|VmData|VmStk)" "/proc/$main_pid/status" 2>/dev/null
        fi
    else
        echo "Service not running or no main PID"
    fi
    echo ""
    
    # Unit file content
    echo "=== Unit File ==="
    systemctl cat "$service" 2>/dev/null || echo "Unit file not found"
}

# Service health check
health_check() {
    local service="$1"
    local check_type="${2:-basic}"
    
    if [[ -z "$service" ]]; then
        echo "Usage: health_check <service_name> [basic|detailed|continuous]"
        return 1
    fi
    
    [[ "$service" != *.service ]] && service="${service}.service"
    
    echo "=== Health Check: $service ($check_type) ==="
    
    # Basic health indicators
    local load_state=$(systemctl show "$service" --property=LoadState --value 2>/dev/null)
    local active_state=$(systemctl show "$service" --property=ActiveState --value 2>/dev/null)
    local sub_state=$(systemctl show "$service" --property=SubState --value 2>/dev/null)
    local main_pid=$(systemctl show "$service" --property=MainPID --value 2>/dev/null)
    
    echo "Load State: $load_state"
    echo "Active State: $active_state"
    echo "Sub State: $sub_state"
    echo "Main PID: $main_pid"
    echo ""
    
    # Health score calculation
    local health_score=0
    local max_score=100
    
    # Service states (40 points)
    case "$active_state" in
        "active") health_score=$((health_score + 40)) ;;
        "activating") health_score=$((health_score + 20)) ;;
        "inactive") health_score=$((health_score + 0)) ;;
        "failed") health_score=$((health_score - 20)) ;;
    esac
    
    # Process check (30 points)
    if [[ -n "$main_pid" && "$main_pid" != "0" ]]; then
        if kill -0 "$main_pid" 2>/dev/null; then
            health_score=$((health_score + 30))
            echo "✓ Main process is running"
        else
            echo "✗ Main process not responding"
        fi
    else
        echo "✗ No main process"
    fi
    
    # Recent failures check (30 points)
    local recent_failures=$(journalctl -u "$service" --since "1 hour ago" -p err --no-pager -q --lines=0 2>/dev/null; echo $?)
    if [[ $recent_failures -eq 0 ]]; then
        local error_count=$(journalctl -u "$service" --since "1 hour ago" -p err --no-pager | wc -l)
        if [[ $error_count -eq 0 ]]; then
            health_score=$((health_score + 30))
            echo "✓ No recent errors"
        else
            health_score=$((health_score + 10))
            echo "⚠ $error_count recent errors"
        fi
    fi
    
    echo ""
    echo "Health Score: $health_score/$max_score"
    
    if [[ $health_score -ge 80 ]]; then
        echo "Status: ✓ HEALTHY"
    elif [[ $health_score -ge 50 ]]; then
        echo "Status: ⚠ WARNING"
    else
        echo "Status: ✗ CRITICAL"
    fi
    
    # Detailed checks
    if [[ "$check_type" == "detailed" || "$check_type" == "continuous" ]]; then
        echo ""
        echo "=== Detailed Health Metrics ==="
        
        # Memory usage
        if [[ -n "$main_pid" && "$main_pid" != "0" && -f "/proc/$main_pid/status" ]]; then
            local vm_rss=$(awk '/VmRSS:/ {print $2}' "/proc/$main_pid/status" 2>/dev/null)
            echo "Memory Usage: ${vm_rss}kB"
        fi
        
        # File descriptor usage
        if [[ -n "$main_pid" && "$main_pid" != "0" && -d "/proc/$main_pid/fd" ]]; then
            local fd_count=$(ls "/proc/$main_pid/fd" 2>/dev/null | wc -l)
            echo "Open File Descriptors: $fd_count"
        fi
        
        # Service restarts
        local restart_count=$(journalctl -u "$service" --since "24 hours ago" --no-pager | grep -c "Started\|Stopped" 2>/dev/null)
        echo "Restarts (24h): $restart_count"
        
        # Last restart time
        local last_start=$(journalctl -u "$service" --no-pager --reverse -o short-iso | grep "Started" | head -1 | awk '{print $1}' 2>/dev/null)
        echo "Last Started: ${last_start:-Never}"
    fi
    
    # Continuous monitoring
    if [[ "$check_type" == "continuous" ]]; then
        echo ""
        echo "Starting continuous monitoring (Ctrl+C to stop)..."
        
        while true; do
            sleep 5
            echo "$(date): Health Score: $(health_check "$service" "basic" | grep "Health Score:" | awk '{print $3}')"
        done
    fi
}

# Service dependency mapper
map_dependencies() {
    local service="$1"
    local depth="${2:-2}"
    
    if [[ -z "$service" ]]; then
        echo "Usage: map_dependencies <service_name> [depth]"
        return 1
    fi
    
    [[ "$service" != *.service ]] && service="${service}.service"
    
    echo "=== Dependency Map: $service (depth: $depth) ==="
    echo ""
    
    # Forward dependencies (what this service needs)
    echo "=== Forward Dependencies (Requires/Wants) ==="
    systemctl list-dependencies "$service" --plain --no-pager | head -$((depth * 10))
    echo ""
    
    # Reverse dependencies (what needs this service)
    echo "=== Reverse Dependencies (Required/Wanted by) ==="
    systemctl list-dependencies --reverse "$service" --plain --no-pager | head -$((depth * 10))
    echo ""
    
    # Conflicting services
    echo "=== Conflicts ==="
    local conflicts=$(systemctl show "$service" --property=Conflicts --value 2>/dev/null)
    if [[ -n "$conflicts" ]]; then
        echo "$conflicts"
    else
        echo "No conflicts defined"
    fi
    echo ""
    
    # Services that must start before this one
    echo "=== Before/After Ordering ==="
    echo "Must start after:"
    local after=$(systemctl show "$service" --property=After --value 2>/dev/null)
    echo "${after:-None}"
    echo ""
    echo "Must start before:"
    local before=$(systemctl show "$service" --property=Before --value 2>/dev/null)
    echo "${before:-None}"
}

# Service performance analysis
performance_analysis() {
    local service="$1"
    local duration="${2:-300}"  # 5 minutes default
    
    if [[ -z "$service" ]]; then
        echo "Usage: performance_analysis <service_name> [duration_seconds]"
        return 1
    fi
    
    [[ "$service" != *.service ]] && service="${service}.service"
    
    echo "=== Performance Analysis: $service ==="
    echo "Duration: ${duration} seconds"
    echo ""
    
    local main_pid=$(systemctl show "$service" --property=MainPID --value 2>/dev/null)
    
    if [[ -z "$main_pid" || "$main_pid" == "0" ]]; then
        echo "Service not running or no main PID"
        return 1
    fi
    
    echo "Monitoring PID: $main_pid"
    echo "Starting performance collection..."
    
    # Create temporary files for data collection
    local cpu_file="/tmp/cpu_${service}_$$.dat"
    local mem_file="/tmp/mem_${service}_$$.dat"
    local io_file="/tmp/io_${service}_$$.dat"
    
    # Background monitoring
    {
        local end_time=$(($(date +%s) + duration))
        while [[ $(date +%s) -lt $end_time ]] && kill -0 "$main_pid" 2>/dev/null; do
            local timestamp=$(date +%s)
            
            # CPU and memory stats
            local stats=$(ps -p "$main_pid" -o %cpu,%mem,vsz,rss --no-headers 2>/dev/null)
            if [[ -n "$stats" ]]; then
                echo "$timestamp $stats" >> "$cpu_file"
            fi
            
            # I/O stats (if available)
            if [[ -f "/proc/$main_pid/io" ]]; then
                local read_bytes=$(awk '/read_bytes:/ {print $2}' "/proc/$main_pid/io" 2>/dev/null)
                local write_bytes=$(awk '/write_bytes:/ {print $2}' "/proc/$main_pid/io" 2>/dev/null)
                echo "$timestamp $read_bytes $write_bytes" >> "$io_file"
            fi
            
            sleep 5
        done
    } &
    
    local monitor_pid=$!
    
    # Wait for monitoring to complete
    wait "$monitor_pid"
    
    # Analyze collected data
    echo ""
    echo "=== Performance Analysis Results ==="
    
    if [[ -f "$cpu_file" && -s "$cpu_file" ]]; then
        echo "CPU Usage Statistics:"
        awk '{cpu+=$2; mem+=$3; count++} END {
            if(count>0) {
                printf "  Average CPU: %.2f%%\n", cpu/count;
                printf "  Average Memory: %.2f%%\n", mem/count;
            }
        }' "$cpu_file"
        
        echo "  Peak CPU: $(awk 'BEGIN{max=0} {if($2>max) max=$2} END{printf "%.2f%%", max}' "$cpu_file")"
        echo "  Peak Memory: $(awk 'BEGIN{max=0} {if($3>max) max=$3} END{printf "%.2f%%", max}' "$cpu_file")"
        echo ""
    fi
    
    if [[ -f "$io_file" && -s "$io_file" ]]; then
        echo "I/O Statistics:"
        local first_line=$(head -1 "$io_file")
        local last_line=$(tail -1 "$io_file")
        
        if [[ -n "$first_line" && -n "$last_line" ]]; then
            local start_read=$(echo "$first_line" | awk '{print $2}')
            local start_write=$(echo "$first_line" | awk '{print $3}')
            local end_read=$(echo "$last_line" | awk '{print $2}')
            local end_write=$(echo "$last_line" | awk '{print $3}')
            
            local read_diff=$((end_read - start_read))
            local write_diff=$((end_write - start_write))
            
            echo "  Total Read: $(numfmt --to=iec "$read_diff")B"
            echo "  Total Write: $(numfmt --to=iec "$write_diff")B"
            echo "  Read Rate: $(numfmt --to=iec $((read_diff / duration)))B/s"
            echo "  Write Rate: $(numfmt --to=iec $((write_diff / duration)))B/s"
        fi
        echo ""
    fi
    
    # Cleanup temporary files
    rm -f "$cpu_file" "$mem_file" "$io_file"
    
    echo "Performance analysis complete"
}

# Usage
case "${1:-help}" in
    "analyze")
        analyze_service "$2"
        ;;
    "health")
        health_check "$2" "$3"
        ;;
    "deps")
        map_dependencies "$2" "$3"
        ;;
    "perf")
        performance_analysis "$2" "$3"
        ;;
    "help")
        echo "Usage: $0 {analyze|health|deps|perf} [arguments]"
        echo "  analyze <service>              - Comprehensive service analysis"
        echo "  health <service> [type]        - Health check (basic|detailed|continuous)"
        echo "  deps <service> [depth]         - Map service dependencies"
        echo "  perf <service> [duration]      - Performance analysis"
        ;;
esac
```

## Comprehensive Systemd Unit Files

### Service Unit Files (.service)
```ini
# /etc/systemd/system/webapp.service
[Unit]
Description=Web Application Server
Documentation=https://example.com/docs/webapp
After=network.target postgresql.service redis.service
Wants=network-online.target
Requires=postgresql.service
Conflicts=apache2.service

[Service]
Type=notify
User=webapp
Group=webapp
WorkingDirectory=/opt/webapp
Environment=NODE_ENV=production
Environment=PORT=3000
EnvironmentFile=/etc/webapp/environment
ExecStartPre=/opt/webapp/scripts/pre-start.sh
ExecStart=/opt/webapp/bin/webapp --config /etc/webapp/config.json
ExecStartPost=/opt/webapp/scripts/post-start.sh
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -TERM $MAINPID
ExecStopPost=/opt/webapp/scripts/cleanup.sh
Restart=always
RestartSec=5
TimeoutStartSec=60
TimeoutStopSec=30
KillMode=mixed
KillSignal=SIGTERM

# Security and Resource Controls
PrivateTmp=true
PrivateDevices=true
NoNewPrivileges=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/lib/webapp /var/log/webapp
MemoryLimit=512M
CPUQuota=50%

[Install]
WantedBy=multi-user.target
Also=webapp-backup.timer
```

### Socket Unit Files (.socket)
```ini
# /etc/systemd/system/webapp.socket
[Unit]
Description=Web Application Socket
PartOf=webapp.service

[Socket]
ListenStream=3000
ListenStream=[::]:3000
BindIPv6Only=both
SocketUser=webapp
SocketGroup=webapp
SocketMode=0600
Accept=false
MaxConnections=1000
KeepAlive=true

[Install]
WantedBy=sockets.target
```

### Timer Unit Files (.timer)
```ini
# /etc/systemd/system/webapp-backup.timer
[Unit]
Description=Web Application Backup Timer
Requires=webapp-backup.service

[Timer]
OnCalendar=daily
OnCalendar=*-*-* 02:00:00
Persistent=true
AccuracySec=1min
RandomizedDelaySec=30min

[Install]
WantedBy=timers.target
```

```ini
# /etc/systemd/system/webapp-backup.service
[Unit]
Description=Web Application Backup
After=webapp.service

[Service]
Type=oneshot
User=backup
Group=backup
ExecStart=/opt/webapp/scripts/backup.sh
WorkingDirectory=/opt/webapp
Environment=BACKUP_DIR=/var/backups/webapp
StandardOutput=journal
StandardError=journal
```

### Target Unit Files (.target)
```ini
# /etc/systemd/system/webapp-stack.target
[Unit]
Description=Complete Web Application Stack
Documentation=https://example.com/docs/deployment
Wants=postgresql.service redis.service nginx.service webapp.service
After=postgresql.service redis.service
AllowIsolate=true

[Install]
WantedBy=multi-user.target
```

### Mount Unit Files (.mount)
```ini
# /etc/systemd/system/opt-webapp-data.mount
[Unit]
Description=Web Application Data Mount
Before=webapp.service

[Mount]
What=/dev/disk/by-uuid/12345678-1234-1234-1234-123456789abc
Where=/opt/webapp/data
Type=ext4
Options=defaults,noatime

[Install]
WantedBy=webapp.service
```

### Path Unit Files (.path)
```ini
# /etc/systemd/system/webapp-config-reload.path
[Unit]
Description=Monitor webapp configuration changes
After=webapp.service

[Path]
PathChanged=/etc/webapp/config.json
PathChanged=/etc/webapp/environment
Unit=webapp-config-reload.service

[Install]
WantedBy=multi-user.target
```

```ini
# /etc/systemd/system/webapp-config-reload.service
[Unit]
Description=Reload webapp configuration
After=webapp.service

[Service]
Type=oneshot
ExecStart=/bin/systemctl reload webapp.service
```

### Service Management Commands for Custom Units
```bash
# Install and activate custom service
sudo cp webapp.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable webapp.service
sudo systemctl start webapp.service

# Check custom service status
systemctl status webapp.service
journalctl -u webapp.service -f

# Enable socket activation
sudo systemctl enable webapp.socket
sudo systemctl start webapp.socket
systemctl list-sockets

# Enable and start timer
sudo systemctl enable webapp-backup.timer
sudo systemctl start webapp-backup.timer
systemctl list-timers

# Test timer execution
sudo systemctl start webapp-backup.service

# Work with targets
sudo systemctl enable webapp-stack.target
sudo systemctl start webapp-stack.target
sudo systemctl isolate webapp-stack.target

# Validate unit file syntax
systemd-analyze verify /etc/systemd/system/webapp.service

# Show unit file dependencies
systemctl list-dependencies webapp.service
systemctl list-dependencies --reverse webapp.service

# Edit service with automatic validation
sudo systemctl edit --full webapp.service

# Create drop-in override
sudo systemctl edit webapp.service
# This creates /etc/systemd/system/webapp.service.d/override.conf
```

## Process States

| State | Symbol | Description |
|-------|--------|-------------|
| Running | R | Currently executing |
| Sleeping | S | Waiting for event |
| Uninterruptible | D | Waiting for I/O |
| Zombie | Z | Finished but not cleaned up |
| Stopped | T | Suspended by signal |

## Monitoring System Resources

### CPU and Memory Usage
```bash
# Show CPU usage per process
top -o %CPU

# Show memory usage
free -h

# Show detailed memory info
cat /proc/meminfo

# Monitor I/O usage
iotop

# System activity report
sar -u 1 5
```

### Advanced Monitoring
```bash
# Process file descriptors
lsof -p 1234

# Network connections by process
netstat -tulpn
ss -tulpn

# Process system calls
strace -p 1234

# Process library dependencies
ldd /usr/bin/nginx
```

## Comprehensive Troubleshooting Guide

### Systematic Process Troubleshooting

#### High CPU Usage Diagnosis
```bash
# Identify CPU-intensive processes
top -o %CPU -n 1
htop --sort-key PERCENT_CPU

# Detailed CPU analysis per process
pidstat -u 1 5                    # CPU usage over time
ps -eo pid,ppid,cmd,pcpu --sort=-pcpu | head -10

# Check system load and CPU utilization
uptime                             # Load averages
vmstat 1 5                        # System statistics
iostat -c 1 5                     # CPU utilization details
sar -u 1 5                        # CPU usage report

# Analyze specific process CPU usage
top -p $(pgrep problematic_process)
strace -c -p $(pgrep problematic_process)    # System call analysis
perf top -p $(pgrep problematic_process)     # Performance profiling

# Check for CPU-bound vs I/O-bound processes
ps -eo pid,stat,pcpu,cmd | grep -E '^[[:space:]]*[0-9]+[[:space:]]+[RD]'
```

#### Memory Issues Diagnosis
```bash
# System memory overview
free -h
cat /proc/meminfo

# Find memory-intensive processes
ps aux --sort=-%mem | head -10
ps -eo pid,ppid,cmd,pmem --sort=-pmem

# Detailed memory analysis
pmap -d $(pgrep process_name)      # Process memory map
smem -r                           # Memory usage by process (if available)
slabtop                           # Kernel slab allocator info

# Check for memory leaks
valgrind --leak-check=full command
ps -o pid,etime,pmem,comm -p $(pgrep process_name)

# Out of Memory (OOM) investigation
dmesg | grep -i "killed process"
journalctl -k | grep -i "out of memory"
cat /proc/sys/vm/oom_score_adj    # OOM score adjustment

# Swap usage analysis
swapon --show
cat /proc/swaps
```

#### I/O Performance Issues
```bash
# Monitor I/O usage
iotop -o                          # I/O usage by process
iostat -x 1 5                     # Extended I/O statistics
pidstat -d 1 5                    # I/O statistics per process

# Check disk utilization
df -h                             # Disk space usage
du -sh /*                         # Directory space usage
lsof +D /path/to/directory        # Files open in directory

# Find processes with high I/O
iotop -p $(pgrep process_name)
cat /proc/$(pgrep process_name)/io # Process I/O statistics
```

### Service Troubleshooting Methodologies

#### Service Startup Failures
```bash
# Comprehensive service status check
systemctl status service_name --no-pager -l

# Check service logs
journalctl -u service_name --no-pager
journalctl -u service_name --since "1 hour ago"
journalctl -u service_name -p err  # Error level only

# Verify service configuration
systemctl cat service_name
systemd-analyze verify /etc/systemd/system/service_name.service

# Check dependencies
systemctl list-dependencies service_name
systemctl list-dependencies --reverse service_name

# Test service manually
sudo -u service_user /path/to/service/binary --config /path/to/config

# Check file permissions and ownership
ls -la /path/to/service/
namei -l /path/to/service/binary

# Verify network dependencies
ss -tulpn | grep port_number
systemctl status network.target
```

#### Service Runtime Issues
```bash
# Monitor service resources in real-time
systemd-cgtop
systemctl show service_name --property=MainPID
top -p $(systemctl show service_name --property=MainPID --value)

# Check service environment
systemctl show-environment
systemctl show service_name --property=Environment

# Analyze service crashes
coredumpctl list
coredumpctl info service_name
journalctl -u service_name | grep -i "segfault\|core\|crash"

# Service dependency issues
systemctl list-jobs
systemctl list-dependencies --failed

# Check resource limits
systemctl show service_name --property=LimitNOFILE
systemctl show service_name --property=MemoryLimit
ulimit -a  # For manual testing
```

#### Performance Bottleneck Analysis
```bash
# Comprehensive system performance overview
vmstat 1 5                        # Memory, I/O, CPU overview
mpstat 1 5                        # Multi-processor statistics
sar -A 1 5                        # Complete system activity report

# Network performance issues
ss -i                             # Socket statistics with details
netstat -i                        # Network interface statistics
iftop                             # Network bandwidth usage
nload                             # Network load monitor

# Process communication analysis
lsof -i :port_number              # Network connections on port
lsof -p $(pgrep process_name)     # Files opened by process
strace -e network -p $(pgrep process_name)  # Network system calls

# Database and application specific
# PostgreSQL
journalctl -u postgresql
sudo -u postgres psql -c "SELECT * FROM pg_stat_activity;"

# Web servers
curl -I http://localhost/health   # Health check
ab -n 100 -c 10 http://localhost/  # Simple load test
```

### Advanced Diagnostic Techniques

#### System Call Tracing
```bash
# Trace system calls for debugging
strace -o trace.log -tt -T command
strace -p $(pgrep process_name) -o running_trace.log

# Trace specific system calls
strace -e open,read,write -p $(pgrep process_name)
strace -e network -p $(pgrep process_name)

# Statistical system call analysis
strace -c -p $(pgrep process_name)
```

#### Performance Profiling
```bash
# CPU profiling with perf
perf record -g -p $(pgrep process_name)
perf report

# Memory profiling
perf record -e cache-misses -p $(pgrep process_name)
valgrind --tool=massif command

# I/O profiling
perf record -e block:block_rq_insert,block:block_rq_complete -p $(pgrep process_name)
```

#### Log Analysis Techniques
```bash
# Centralized log analysis
journalctl --since "2025-01-01" --until "2025-01-02" | grep ERROR
journalctl -p warning --since "1 hour ago"

# Application log patterns
tail -f /var/log/application.log | grep -E "(ERROR|WARN|EXCEPTION)"
grep -c "ERROR" /var/log/application.log  # Count errors
awk '/ERROR/ {print $1, $2, $NF}' /var/log/application.log  # Extract error info

# Log rotation and cleanup issues
logrotate -d /etc/logrotate.d/application  # Debug logrotate
du -sh /var/log/*                          # Log directory sizes
```

## Advanced Best Practices

### Process Management Best Practices
- **Use appropriate signals**: Always try SIGTERM before SIGKILL for graceful shutdown
- **Monitor resource usage**: Regularly check CPU, memory, and I/O consumption
- **Implement proper logging**: Ensure all services log to appropriate destinations
- **Set resource limits**: Use systemd resource controls to prevent resource exhaustion
- **Plan for failure**: Implement health checks and automatic recovery mechanisms
- **Document dependencies**: Clearly define service dependencies and startup order

### Service Configuration Best Practices
- **Security hardening**: Use PrivateTmp, NoNewPrivileges, and ProtectSystem directives
- **Resource isolation**: Implement memory and CPU limits for critical services
- **Monitoring integration**: Configure services for easy monitoring and alerting
- **Backup strategies**: Ensure service data and configurations are backed up
- **Testing procedures**: Always test service configurations in non-production environments
- **Version control**: Track service unit file changes with version control systems

### Performance Optimization Guidelines
- **CPU scheduling**: Use appropriate nice values for different process priorities
- **I/O scheduling**: Configure I/O schedulers based on workload characteristics
- **Memory management**: Tune kernel parameters for specific workloads
- **Network optimization**: Configure network settings for service requirements
- **Regular monitoring**: Implement continuous monitoring for early problem detection

## Comprehensive Lab Exercises

### Lab 1: Advanced Process Monitoring and Analysis
**Objective**: Master process monitoring techniques for diagnosing system performance issues.

**Tasks**:
1. Create a high-CPU consuming process and identify it using multiple monitoring tools
2. Analyze memory usage patterns of running services
3. Use `strace` to trace system calls of a problematic process
4. Create a monitoring script that alerts when processes exceed resource thresholds
5. Practice using `perf` for performance profiling

**Deliverables**:
- Process monitoring script with threshold alerting
- Performance analysis report comparing different monitoring tools
- Troubleshooting methodology document

### Lab 2: Custom Systemd Service Creation and Management
**Objective**: Create, deploy, and manage a complete custom service with all unit types.

**Tasks**:
1. Create a simple web application service with proper security settings
2. Implement socket activation for the service
3. Create a timer unit for periodic maintenance tasks
4. Set up a target unit that coordinates multiple related services
5. Configure service monitoring and log management
6. Test service failure scenarios and recovery

**Deliverables**:
- Complete set of systemd unit files (.service, .socket, .timer, .target)
- Service deployment and management documentation
- Testing and validation procedures

### Lab 3: Service Troubleshooting and Performance Optimization
**Objective**: Develop systematic troubleshooting skills for service issues.

**Tasks**:
1. Diagnose and fix a service that fails to start due to dependency issues
2. Troubleshoot a service with memory leaks using appropriate tools
3. Optimize a service configuration for better performance
4. Implement comprehensive logging and monitoring
5. Create automated health checks and recovery procedures

**Deliverables**:
- Troubleshooting playbook with step-by-step procedures
- Performance optimization report with before/after metrics
- Automated monitoring and alerting scripts

### Lab 4: Init System Migration Simulation
**Objective**: Understand differences between init systems and migration procedures.

**Tasks**:
1. Create equivalent service configurations for SysV, Upstart, and systemd
2. Compare startup times and dependency handling between systems
3. Migrate a legacy SysV init script to systemd
4. Document compatibility considerations and migration challenges
5. Create automated testing procedures for service functionality

**Deliverables**:
- Service configurations for all three init systems
- Migration documentation and procedures
- Compatibility testing framework

### Lab 5: Enterprise Service Monitoring Dashboard
**Objective**: Create a comprehensive monitoring solution for service management.

**Tasks**:
1. Develop a script that monitors critical services and their dependencies
2. Implement alerting for service failures and performance issues
3. Create a web dashboard showing service status and metrics
4. Set up automated service recovery procedures
5. Implement historical tracking and reporting

**Deliverables**:
- Service monitoring framework with web interface
- Automated alerting and recovery system
- Historical reporting and analysis tools

## Practical Assessment Scenarios

### Scenario 1: Production Service Failure
You're managing a web application stack where the main application service keeps crashing. Using the troubleshooting methodologies learned, diagnose and resolve the issue systematically.

### Scenario 2: Performance Degradation
A database service is experiencing performance issues with high I/O wait times. Identify the root cause and implement optimization strategies.

### Scenario 3: Service Dependency Chain Issues
Multiple services are failing to start due to complex dependency relationships. Redesign the service architecture for better reliability.

### Scenario 4: Resource Exhaustion
A service is consuming excessive memory and affecting other system processes. Implement resource controls and monitoring to prevent future issues.

### Scenario 5: Security Hardening
Harden existing service configurations to follow security best practices while maintaining functionality.

## Next Steps
With process and service management skills, you're ready to explore Users, Groups & Authentication in Module 6, where you'll learn to manage user accounts and system security.
