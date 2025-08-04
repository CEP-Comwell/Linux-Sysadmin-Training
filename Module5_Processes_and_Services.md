# Module 5: Processes & Services

**📍 Module Progress: 5/15 Complete**  
**⏱️ Estimated Time: 2-3 hours**  
**📋 Prerequisites: Modules 1-4 (Command Line, Permissions, Package Management)**  
**🎯 Difficulty Level: ⭐⭐⭐ (Intermediate)**

## Table of Contents
- [🔍 Overview](#overview)
- [🎯 Learning Objectives](#learning-objectives)
- [📚 Topics](#topics)
  - [5.1 Process Basics](#51-process-basics-beginner)
  - [5.2 Process Monitoring](#52-process-monitoring-intermediate)
  - [5.3 Process Control](#53-process-control-intermediate)
  - [5.4 Basic Service Management](#54-basic-service-management-intermediate)
  - [5.5 Essential Systemd Operations](#55-essential-systemd-operations-advanced)
- [⚡ Essential Command Reference](#essential-command-reference)
  - [Process Monitoring Commands](#process-monitoring-commands)
  - [Process Control Commands](#process-control-commands)
  - [Service Management Commands](#service-management-commands)
  - [System Monitoring Commands](#system-monitoring-commands)
- [🚀 Quick Start Commands](#quick-start-commands)
- [🔄 Understanding Linux Service Management Evolution](#understanding-linux-service-management-evolution)
  - [From init.d to systemd: A Brief History](#from-initd-to-systemd-a-brief-history)
  - [Understanding systemd Service States](#understanding-systemd-service-states)
- [🛠️ Practical Examples](#practical-examples)
  - [Basic Process Monitoring Examples](#basic-process-monitoring-examples)
  - [Understanding Background Processes and SSH](#understanding-background-processes-and-ssh)
  - [Service Management Examples](#service-management-examples)
- [🧪 Lab Exercises](#lab-exercises-45-minutes-total)
  - [Lab 1: Basic Process Monitoring](#lab-1-basic-process-monitoring-15-minutes)
  - [Lab 2: Process Control and SSH Management](#lab-2-process-control-and-ssh-management-20-minutes)
  - [Lab 3: Mastering Systemd Service Management](#lab-3-mastering-systemd-service-management-10-minutes)
- [✅ Best Practices](#best-practices)
  - [Process Management Best Practices](#process-management-best-practices)
  - [SSH and Remote Process Management](#ssh-and-remote-process-management)
  - [Service Management Best Practices](#service-management-best-practices)
- [🔧 Troubleshooting](#troubleshooting)
  - [Understanding Error Codes and Exit Status](#understanding-error-codes-and-exit-status)
  - [Common Process Problems](#common-process-problems)
  - [SSH-Related Process Issues](#ssh-related-process-issues)
  - [Common Service Problems](#common-service-problems)
  - [General Troubleshooting Steps](#general-troubleshooting-steps)
- [📋 Summary](#summary)
- [➡️ Next Steps](#next-steps)

## 🔍 Overview
Learn the essential skills for managing processes and services in Linux systems. This module covers the fundamental commands and concepts needed to monitor running processes, control system services, and troubleshoot basic performance issues.
#
**What You'll Learn:**
- How to view and monitor running processes
- Basic process control and management
- Understanding Linux services and systemd
- Common troubleshooting techniques
- Essential command-line tools for system monitoring

[↑ Back to Top](#table-of-contents)

## 🎯 Learning Objectives
By the end of this module, you will be able to:

1. **View Running Processes**: Use `ps`, `top`, and `htop` to see what's running on your system
2. **Monitor System Activity**: Check CPU and memory usage with basic monitoring tools
3. **Control Processes**: Start, stop, and manage processes safely
4. **Manage Services**: Start, stop, and check the status of system services
5. **Use Systemd Basics**: Understand and use basic systemd commands
6. **Troubleshoot Issues**: Find and fix common process and service problems

[↑ Back to Top](#table-of-contents)

## 📚 Topics

### 🟢 5.1 Process Basics (Beginner)
- What is a process and how it works
- Process identification (PID) and process states
- Parent and child processes
- Foreground vs background processes
- Understanding process hierarchy

**📖 Related Commands:** [Process Monitoring Commands](#process-monitoring-commands)
#
### 🟡 5.2 Process Monitoring (Intermediate)
- Using `ps` command to list processes
- Real-time monitoring with `top` and `htop`
- Finding processes with `pgrep` and `pidof`
- Checking process resource usage
- Basic performance monitoring

**📖 Related Commands:** [Process Monitoring Commands](#process-monitoring-commands) | [System Monitoring Commands](#system-monitoring-commands)

### 🟡 5.3 Process Control (Intermediate)
- Starting and stopping processes
- Using signals to control processes (`kill`, `killall`)
- Background job control (`&`, `jobs`, `fg`, `bg`)
- Keeping processes running with `nohup`
- Basic process priority with `nice`
- **Critical importance of background processes for SSH sessions**
- **Preventing process termination when SSH disconnects**

**📖 Related Commands:** [Process Control Commands](#process-control-commands) | [Quick Start Commands](#quick-start-commands)

### 🟡 5.4 Basic Service Management (Intermediate)
- **Historical context: From init.d to systemd evolution**
- **Understanding why systemd replaced traditional init systems**
- Understanding Linux services and daemons
- What is systemd and why it's important
- Service states: active, inactive, failed
- Common system services (web servers, databases, etc.)
- **Service state management vs boot configuration**

**📖 Related Commands:** [Service Management Commands](#service-management-commands) | [Quick Start Commands](#quick-start-commands)

### 🔴 5.5 Essential Systemd Operations (Advanced)
- **Understanding systemd service states in detail**
- Starting and stopping services with `systemctl`
- **The difference between start/stop and enable/disable**
- Checking service status and logs
- Enabling and disabling services at boot
- Restarting and reloading services
- **Common systemctl troubleshooting commands**
- Basic troubleshooting with `journalctl`
- **Reading and interpreting service status output**

**📖 Related Commands:** [Service Management Commands](#service-management-commands) | [System Monitoring Commands](#system-monitoring-commands)

[↑ Back to Top](#table-of-contents)

## ⚡ Essential Command Reference

### 🔹 Process Monitoring Commands
**📚 Related Topics:** [5.1 Process Basics](#51-process-basics-beginner) | [5.2 Process Monitoring](#52-process-monitoring-intermediate)

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `ps` | List running processes | `ps aux`, `ps -ef` |
| `top` | Real-time process monitor | `top`, `top -u username` |
| `htop` | Enhanced process monitor | `htop` (interactive) |
| `pgrep` | Find process by name | `pgrep nginx`, `pgrep -u user` |
| `pidof` | Get PID of process | `pidof nginx` |

### 🔹 Process Control Commands
**📚 Related Topics:** [5.3 Process Control](#53-process-control-intermediate)

| Command | Purpose | Common Examples | SSH Usage Notes |
|---------|---------|-----------------|-----------------|
| `kill` | Terminate process by PID | `kill 1234`, `kill -9 1234` | Safe to use remotely |
| `killall` | Kill processes by name | `killall firefox` | Safe to use remotely |
| `pkill` | Kill processes by pattern | `pkill -f "java.*tomcat"` | Safe to use remotely |
| `nohup` | Run process immune to hangups | `nohup command &` | **Essential for SSH sessions** |
| `jobs` | List background jobs | `jobs`, `jobs -l` | Shows current session jobs only |
| `fg` | Bring job to foreground | `fg`, `fg %1` | Can be interrupted by SSH disconnect |
| `bg` | Send job to background | `bg %1` | **Important for SSH stability** |
| `screen` | Create persistent sessions | `screen -S name` | **Best for long SSH tasks** |
| `tmux` | Terminal multiplexer | `tmux new -s name` | **Alternative to screen** |

### 🔹 Service Management Commands
**📚 Related Topics:** [5.4 Basic Service Management](#54-basic-service-management-intermediate) | [5.5 Essential Systemd Operations](#55-essential-systemd-operations-advanced)

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `systemctl status` | Check service status | `systemctl status nginx` |
| `systemctl start` | Start a service | `systemctl start apache2` |
| `systemctl stop` | Stop a service | `systemctl stop mysql` |
| `systemctl restart` | Restart a service | `systemctl restart sshd` |
| `systemctl enable` | Enable service at boot | `systemctl enable nginx` |
| `systemctl disable` | Disable service at boot | `systemctl disable apache2` |
| `journalctl` | View service logs | `journalctl -u nginx`, `journalctl -f` |

### 🔹 System Monitoring Commands
**📚 Related Topics:** [5.2 Process Monitoring](#52-process-monitoring-intermediate) | [5.5 Essential Systemd Operations](#55-essential-systemd-operations-advanced)

| Command | Purpose | Common Examples |
|---------|---------|-----------------|
| `uptime` | System load and uptime | `uptime` |
| `free` | Memory usage | `free -h` |
| `df` | Disk usage | `df -h` |
| `who` | Who is logged in | `who`, `w` |

## 🚀 Quick Start Commands
**📚 Related Topics:** [5.3 Process Control](#53-process-control-intermediate) | [5.4 Basic Service Management](#54-basic-service-management-intermediate)

| Task | Command | Example |
|------|---------|---------|
| List processes | `ps aux` | `ps aux \| grep nginx` |
| Kill process | `kill PID` | `kill 1234` |
| Start service | `systemctl start` | `systemctl start nginx` |
| Check logs | `journalctl -u` | `journalctl -u nginx` |
| Background task | `nohup command &` | `nohup rsync /data/ backup/ &` |

[↑ Back to Top](#table-of-contents)

## 🔄 Understanding Linux Service Management Evolution

### From init.d to systemd: A Brief History

#### Traditional init.d System (Legacy)
```bash
# Old way (still works on some systems)
/etc/init.d/apache2 start
/etc/init.d/apache2 stop
/etc/init.d/apache2 status

# Enable at boot (complex)
update-rc.d apache2 enable
chkconfig apache2 on  # On RedHat systems
```

**Problems with init.d:**
- Sequential startup (slow boot times)
- Shell script-based (unreliable)
- No dependency management
- Difficult to troubleshoot
- No built-in logging
- Process tracking was manual

#### Modern systemd System (Current Standard)
```bash
# Modern way (standardized across distributions)
systemctl start apache2
systemctl stop apache2
systemctl status apache2

# Enable at boot (simple)
systemctl enable apache2
```

**Benefits of systemd:**
- Parallel startup (faster boots)
- Binary-based (more reliable)
- Advanced dependency management
- Built-in logging with journalctl
- Process tracking and monitoring
- Socket and timer activation
- Standardized across Linux distributions

### Understanding systemd Service States

#### Service State vs Boot Configuration

**Important Concept:** These are two separate things:
1. **Current State** (running now or not)
2. **Boot Configuration** (starts automatically or not)

```bash
# Current state commands
systemctl start service    # Start now
systemctl stop service     # Stop now
systemctl restart service  # Restart now
systemctl status service   # Check current state

# Boot configuration commands
systemctl enable service   # Start at boot
systemctl disable service  # Don't start at boot
systemctl is-enabled service  # Check boot setting
```

#### Complete Service State Matrix

| Current State | Boot Setting | What This Means |
|---------------|--------------|-----------------|
| **Active** | **Enabled** | Service is running AND will start at boot |
| **Active** | **Disabled** | Service is running BUT won't start at boot |
| **Inactive** | **Enabled** | Service is stopped BUT will start at boot |
| **Inactive** | **Disabled** | Service is stopped AND won't start at boot |

#### Detailed Service States

```bash
# Check comprehensive service status
systemctl status nginx
```

**Output Explanation:**
```
● nginx.service - A high performance web server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2025-08-03 10:30:15 UTC; 2h 15min ago
     Docs: man:nginx(8)
  Process: 1234 ExitCode=0 (success)
 Main PID: 1234 (nginx)
    Tasks: 2 (limit: 4915)
   Memory: 6.8M
   CGroup: /system.slice/nginx.service
           ├─1234 nginx: master process /usr/sbin/nginx
           └─1235 nginx: worker process
```

**Key Status Indicators:**
- **Loaded**: Service definition found and parsed
- **enabled/disabled**: Boot configuration status
- **Active (running)**: Service is currently running
- **Active (exited)**: Service completed successfully
- **Inactive (dead)**: Service is stopped
- **Failed**: Service failed to start or crashed
- **Main PID**: Primary process ID
- **Tasks**: Number of processes/threads
- **Memory**: Current memory usage

[↑ Back to Top](#table-of-contents)

## 🛠️ Practical Examples

### Basic Process Monitoring Examples

#### Example 1: Finding a Slow Process
```bash
# Check what's using the most CPU
ps aux --sort=-%cpu | head -5

# Monitor in real-time
top

# Find a specific process
pgrep firefox
ps aux | grep firefox
```

#### Example 2: Checking System Resources
```bash
# Quick system overview
uptime
free -h
df -h

# Find memory-hungry processes
ps aux --sort=-%mem | head -5
```

#### Example 3: Background Job Management
```bash
# Start a long process in background
ping google.com > /tmp/ping.log &

# Check background jobs
jobs

# Bring job to foreground
fg %1

# Put it back in background (Ctrl+Z, then bg)
bg %1

# Kill the background job
kill %1
```

### Understanding Background Processes and SSH

#### Why Background Processes Matter for Remote Systems

When you connect to a remote system via SSH, all processes you start are tied to your SSH session by default. If your SSH connection drops (network issues, laptop sleep, etc.), all running processes will be terminated. This is where background process management becomes critical.

> ⚠️ **SSH Safety Warning**: Always use `nohup` for long-running processes over SSH connections to prevent termination when your session disconnects.

> 🚨 **Critical**: Never run important long-term tasks in the foreground over SSH - they will be killed if your connection drops.

#### Example 4: SSH-Safe Process Management
```bash
# WRONG: This will stop if SSH disconnects
rsync -av /large/directory/ user@remote:/backup/

# BETTER: Run in background
rsync -av /large/directory/ user@remote:/backup/ &

# BEST: Use nohup for long-running tasks
nohup rsync -av /large/directory/ user@remote:/backup/ &

# Check the process is running
jobs
ps aux | grep rsync

# Monitor progress
tail -f nohup.out
```

#### Example 5: Long-Running Tasks on Remote Servers
```bash
# Starting a database backup (could take hours)
nohup mysqldump --all-databases > /backup/full_backup.sql &

# Starting a system update
nohup apt update && apt upgrade -y > /tmp/update.log 2>&1 &

# Running a log analysis script
nohup ./analyze_logs.sh > /tmp/analysis.log &

# Check all background jobs
jobs -l

# Monitor a specific process
tail -f /tmp/update.log
```

#### Example 6: Using Screen/Tmux for Advanced Session Management
```bash
# Install screen (if not available)
sudo apt install screen

# Start a screen session
screen -S backup_session

# Run your long command
rsync -av /data/ user@backup-server:/backups/

# Detach from screen (Ctrl+A, then D)
# Your process continues running even if SSH disconnects

# Later, reconnect to the session
screen -r backup_session

# List all screen sessions
screen -ls
```

#### Example 7: Process Management Best Practices for SSH
```bash
# Always check what's running before starting new processes
ps aux | grep your_username

# Start critical processes with nohup
nohup ./critical_script.sh &

# Keep track of background jobs
jobs
echo $! > /tmp/last_job_pid.txt  # Save PID of last background job

# Check if process is still running
ps -p $(cat /tmp/last_job_pid.txt)

# Properly terminate when done
kill $(cat /tmp/last_job_pid.txt)
```

### Service Management Examples

#### Example 1: Complete Service Lifecycle Management
```bash
# Check current state and boot configuration
systemctl status nginx
systemctl is-enabled nginx

# Scenario 1: Start service now and enable for boot
sudo systemctl start nginx      # Start immediately
sudo systemctl enable nginx     # Enable for boot
systemctl status nginx          # Verify both settings

# Scenario 2: Stop service but keep boot setting
sudo systemctl stop nginx       # Stop now
systemctl is-enabled nginx      # Still enabled for boot
systemctl status nginx          # Shows inactive but enabled

# Scenario 3: Disable from boot but keep running
sudo systemctl start nginx      # Make sure it's running
sudo systemctl disable nginx    # Disable from boot
systemctl status nginx          # Shows active but disabled

# Scenario 4: Complete shutdown
sudo systemctl stop nginx       # Stop now
sudo systemctl disable nginx    # Disable from boot
systemctl status nginx          # Shows inactive and disabled
```

#### Example 2: Understanding Service Dependencies
```bash
# See what services depend on this one
systemctl list-dependencies nginx

# See what this service depends on
systemctl list-dependencies nginx --reverse

# Check if dependencies are running
systemctl status network.target
systemctl status multi-user.target
```

#### Example 3: Advanced Status Checking
```bash
# Quick status of multiple services
systemctl status nginx apache2 mysql

# List all failed services
systemctl --failed

# List all active services
systemctl list-units --type=service --state=active

# List all enabled services
systemctl list-unit-files --type=service --state=enabled

# Check specific service properties
systemctl show nginx --property=MainPID,ActiveState,LoadState
```

#### Example 1: Managing a Web Server
```bash
# Check if nginx is running
systemctl status nginx

# Start nginx if stopped
sudo systemctl start nginx

# Enable nginx to start at boot
sudo systemctl enable nginx

# Check logs if there's a problem
journalctl -u nginx -n 20
```

#### Example 2: Troubleshooting a Service
```bash
# Service won't start - let's investigate
systemctl status apache2

# Check recent logs
journalctl -u apache2 --since "10 minutes ago"

# Try starting manually to see errors
sudo systemctl start apache2

# Check if port is already in use
ss -tulpn | grep :80
```

#### Example 4: Comprehensive Service Troubleshooting
```bash
# Step 1: Check detailed status
systemctl status problematic-service --no-pager -l

# Step 2: Check logs for errors
journalctl -u problematic-service --since "1 hour ago" --no-pager

# Step 3: Check configuration file
systemctl cat problematic-service

# Step 4: Check if port conflicts exist
ss -tulpn | grep :80  # Replace 80 with your service's port

# Step 5: Check dependencies
systemctl list-dependencies problematic-service
systemctl list-dependencies problematic-service --failed

# Step 6: Try manual start with verbose output
sudo systemctl start problematic-service
journalctl -u problematic-service -f  # Follow logs in real-time

# Step 7: Reset failed state if needed
sudo systemctl reset-failed problematic-service
```

#### Example 5: Common Service Patterns
```bash
# Web server pattern
sudo systemctl enable --now nginx    # Enable and start in one command
sudo systemctl reload nginx          # Reload config without stopping

# Database pattern
sudo systemctl start mysql
sudo systemctl enable mysql
systemctl is-active mysql            # Just check if running

# SSH server (critical service)
sudo systemctl restart sshd          # Restart SSH (be careful!)
systemctl status sshd                # Verify it's running

# Check boot time impact
systemd-analyze blame | head -10     # See slowest services
```

#### Example 3: Regular Maintenance Tasks
```bash
# List all failed services
systemctl --failed

# List all enabled services
systemctl list-unit-files --type=service --state=enabled

# Restart a service safely
sudo systemctl restart ssh
```

[↑ Back to Top](#table-of-contents)

## 🧪 Lab Exercises **(~45 minutes total)**

### Lab 1: Basic Process Monitoring **(~15 minutes)**
**🎯 Objective:** Learn to monitor and understand running processes.

**📝 Practice Checklist:**
- [ ] View all running processes with `ps aux`
- [ ] Monitor system in real-time with `top`
- [ ] Install and use `htop` for enhanced monitoring
- [ ] Find processes by name using `pgrep` and `pidof`
- [ ] Sort processes by CPU and memory usage

**Tasks:**
1. Use `ps aux` to view all running processes
2. Use `top` to monitor processes in real-time
3. Install and use `htop` for enhanced monitoring
4. Find processes by name using `pgrep` and `pidof`
5. Practice sorting processes by CPU and memory usage

**Exercises:**
```bash
# 🔹 Basic Process Monitoring
ps aux                          # View all processes
ps ux                          # Find your own processes
pgrep firefox                  # Find Firefox processes
ps aux | grep firefox          # Alternative process search
top                           # Monitor system in real-time
htop                          # Enhanced monitoring (if installed)

# 🔹 Performance Analysis
ps aux --sort=-%cpu | head -10  # Top CPU consumers
ps aux --sort=-%mem | head -10  # Top memory consumers
```

> 💡 **Pro Tip**: Use `htop` instead of `top` for a more user-friendly interface with colors and mouse support.

**Deliverables:**
- Screenshots of `ps`, `top`, and `htop` output
- List of the top 5 CPU and memory consuming processes
- Documentation of what each process does

<details>
<summary>🔍 <strong>Error Codes to Research</strong></summary>

**Common Error Codes:**
- **Exit Code 1**: General process errors (command not found, permission denied)
- **Exit Code 127**: Command not found in PATH
- **Exit Code 130**: Process terminated by Ctrl+C (SIGINT)
- **ENOENT**: No such file or directory when looking for processes
- **Permission denied**: Trying to view processes you don't own without sudo

**Lab-Specific Error Scenarios:**
- **"htop: command not found"**: Package not installed - research `apt install htop`
- **"ps: user does not exist"**: Invalid username in `ps -u baduser`
- **"top: failed tty get attr"**: Permission issue when running top as different user
- **Process shows `<defunct>`**: Zombie process - research parent process cleanup
- **"Cannot allocate memory"**: System resource exhaustion - research system limits

</details>

### Lab 2: Process Control and SSH Management **(~20 minutes)**
**🎯 Objective:** Learn to control processes safely, especially in SSH environments.

> ⚠️ **SSH Safety Warning**: This lab teaches critical skills for managing processes over SSH connections safely.

**📝 Practice Checklist:**
- [ ] Start processes in the background
- [ ] Practice job control (`jobs`, `fg`, `bg`)
- [ ] Use `kill` to terminate processes safely
- [ ] Use `nohup` to run persistent processes
- [ ] Practice graceful vs forceful process termination
- [ ] Learn SSH-safe process management
- [ ] Practice using screen or tmux for persistent sessions

**Tasks:**
1. Start processes in the background
2. Practice job control (`jobs`, `fg`, `bg`)
3. Use `kill` to terminate processes safely
4. Use `nohup` to run persistent processes
5. Practice graceful vs forceful process termination
6. **Learn SSH-safe process management**
7. **Practice using screen or tmux for persistent sessions**

**Exercises:**
```bash
# 🔹 Basic Background Job Control
sleep 300 &                    # Start background job
jobs                          # List background jobs
fg %1                         # Bring to foreground
# Press Ctrl+Z to suspend
bg %1                         # Send back to background
kill %1                       # Terminate the job

# 🔹 SSH-Safe Process Management
nohup sleep 600 &             # Start persistent process
echo $! > sleep.pid           # Save the PID
ps -p $(cat sleep.pid)        # Verify it's running
jobs                          # May not show nohup processes

# 🔹 Long-Running Task Simulation
nohup ping -c 1000 google.com > ping.log &
tail -f ping.log              # Monitor progress
# Press Ctrl+C to stop monitoring (not the process)
ps aux | grep ping            # Check process status
pgrep ping                    # Alternative status check

# 🔹 Cleanup
kill $(cat sleep.pid)         # Clean termination
pkill ping                    # Kill ping processes

# 🔹 Advanced: Using Screen (if available)
screen -S test_session        # Create named session
# Inside screen: run a long command
ping google.com
# Detach: Ctrl+A, then D
# Reconnect: screen -r test_session
# List sessions: screen -ls
```

> 💡 **Pro Tip**: Always use `nohup` or `screen`/`tmux` for any process that might take longer than your SSH session.

**Deliverables:**
- Command history showing job control
- Examples of graceful process termination
- Documentation of when to use `kill` vs `kill -9`
- **Demonstration of nohup usage for SSH scenarios**
- **Examples of finding and managing detached processes**
- **Screen/tmux session management examples**

<details>
<summary>🔍 <strong>Error Codes to Research</strong></summary>

**Common Error Codes:**
- **SIGHUP (Signal 1)**: Process terminated when SSH connection drops (without nohup)
- **Exit Code 129**: Process terminated by SIGHUP signal
- **"Broken pipe"**: Output redirected to a terminal that closed
- **"No such process" (ESRCH)**: Trying to kill a PID that doesn't exist
- **Exit Code 143**: Process terminated by SIGTERM (graceful kill)
- **Exit Code 137**: Process terminated by SIGKILL (kill -9)
- **"Operation not permitted"**: Trying to kill processes you don't own
- **"screen: command not found"**: Screen not installed (apt install screen)
- **"There is no screen to be resumed"**: No detached screen sessions exist

**SSH + rsync + nohup Error Scenarios:**
- **"rsync: connection unexpectedly closed"**: Network drop during transfer - research connection stability
- **"rsync error: error in rsync protocol data stream (code 12)"**: SSH disconnection mid-transfer
- **"rsync: writefd_unbuffered failed to write: Broken pipe (32)"**: SSH session terminated abruptly
- **"rsync terminated by signal 1 (SIGHUP)"**: Process killed by SSH disconnect (needed nohup)
- **"Permission denied (publickey)"**: SSH key authentication failure - research ssh-copy-id
- **"Host key verification failed"**: SSH host key changed - research ssh-keygen -R
- **"nohup: ignoring input and appending output to 'nohup.out'"**: Normal nohup behavior (not an error)
- **"rsync: failed to connect to host: Connection refused"**: SSH service not running or port blocked
- **Background job [1] terminated**: Process died after SSH disconnect (forgot nohup)
- **"Cannot create directory: Permission denied"**: Remote directory permissions issue

</details>

### Lab 3: Mastering Systemd Service Management **(~10 minutes)**
**🎯 Objective:** Understand systemd service states, troubleshooting, and the difference between current state and boot configuration.

**📝 Practice Checklist:**
- [ ] Understand service state vs boot configuration
- [ ] Practice all combinations of start/stop and enable/disable
- [ ] Read and interpret systemctl status output
- [ ] Master troubleshooting with journalctl
- [ ] Practice systematic service troubleshooting

**Tasks:**
1. **Understand service state vs boot configuration**
2. Practice all combinations of start/stop and enable/disable
3. Learn to read and interpret systemctl status output
4. Master troubleshooting with journalctl
5. **Practice systematic service troubleshooting**

> 🚨 **Critical Concept**: Service **current state** (running/stopped) and **boot configuration** (enabled/disabled) are separate settings!

**Part A: Service State Management**
```bash
# Choose a service to work with (e.g., nginx, apache2, or ssh)
SERVICE="nginx"  # Replace with available service

# Check initial state
systemctl status $SERVICE
systemctl is-enabled $SERVICE

# Practice state combinations
# 1. Running + Enabled (production ready)
sudo systemctl start $SERVICE
sudo systemctl enable $SERVICE
systemctl status $SERVICE  # Note: active + enabled

# 2. Running + Disabled (temporary test)
sudo systemctl disable $SERVICE
systemctl status $SERVICE  # Note: active + disabled

# 3. Stopped + Enabled (will start at boot)
sudo systemctl stop $SERVICE
systemctl status $SERVICE  # Note: inactive + enabled

# 4. Stopped + Disabled (completely off)
sudo systemctl disable $SERVICE
systemctl status $SERVICE  # Note: inactive + disabled

# Convenient commands
sudo systemctl enable --now $SERVICE  # Enable and start
sudo systemctl disable --now $SERVICE # Disable and stop
```

**Part B: Reading Service Status**
```bash
# Detailed status analysis
systemctl status nginx --no-pager -l

# Identify these elements in the output:
# - Service description
# - Loaded status and file location
# - Active status and uptime
# - Main process ID
# - Memory usage
# - Recent log entries

# Check specific properties
systemctl show nginx --property=ActiveState,LoadState,UnitFileState
systemctl is-active nginx    # Just active state
systemctl is-enabled nginx   # Just enabled state
systemctl is-failed nginx    # Failed status
```

**Part C: Troubleshooting Practice**
```bash
# List all services by state
systemctl list-units --type=service --state=active
systemctl list-units --type=service --state=failed
systemctl list-units --type=service --state=inactive

# Check dependencies
systemctl list-dependencies nginx
systemctl list-dependencies nginx --reverse

# Log analysis
journalctl -u nginx --since "today"
journalctl -u nginx --since "1 hour ago" --until "30 minutes ago"
journalctl -u nginx -p err  # Error level only
journalctl -u nginx -f      # Follow mode
```

**Part D: Simulated Troubleshooting**
```bash
# If nginx is available, try this troubleshooting scenario:

# 1. Stop nginx and try to start another web server on port 80
sudo systemctl stop nginx
sudo python3 -m http.server 80  # This should fail or conflict

# 2. In another terminal, try to start nginx
sudo systemctl start nginx

# 3. Check what happened
systemctl status nginx
journalctl -u nginx --since "5 minutes ago"

# 4. Find the port conflict
ss -tulpn | grep :80

# 5. Resolve and verify
# Stop the python server (Ctrl+C)
sudo systemctl start nginx
systemctl status nginx
```

**Deliverables:**
- Examples showing all four state combinations (active/inactive + enabled/disabled)
- Screenshots of systemctl status output with explanations
- **Service dependency analysis for at least one service**
- **Log analysis showing how to find and interpret errors**
- **Documentation of a complete troubleshooting scenario**
- Summary of when to use start/stop vs enable/disable

<details>
<summary>🔍 <strong>Error Codes to Research</strong></summary>

**Common Error Codes:**
- **Exit Code 1 (systemctl)**: General service start failure
- **Exit Code 2**: Invalid service name or command syntax
- **Exit Code 3**: Service not found (unit file doesn't exist)
- **Exit Code 4**: Service operation not supported
- **Exit Code 5**: Service not loaded or failed to load
- **"Job failed" (systemd)**: Service failed to start, check journalctl
- **"Unit not found"**: Service name misspelled or not installed
- **"Permission denied"**: Need sudo for start/stop/enable/disable operations
- **"Address already in use"**: Port conflict (common with web servers)
- **"Failed to start" + exit status 127**: Service binary not found
- **"Dependency failed"**: Required service dependencies aren't running
- **"Connection refused"**: Service running but not accepting connections
- **"masked" status**: Service is completely disabled (systemctl unmask needed)

**Real Service Failure Scenarios:**
- **nginx: "nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)"**: Port 80 taken by apache2
- **apache2: "Job for apache2.service failed because the control process exited with error code"**: Config syntax error
- **mysql: "Unit mysql.service could not be found"**: Wrong service name (try mysql.service vs mysqld.service)
- **sshd: "sshd: no hostkeys available -- exiting"**: Missing SSH host keys after fresh install
- **"Failed to reload daemon: Access denied"**: Need sudo for systemctl daemon-reload
- **"systemctl: command not found"**: Not using systemd (older system with init.d)
- **"Service has no installation config"**: Service can't be enabled (no [Install] section)
- **"A dependency job for X failed"**: Check systemctl list-dependencies --failed
- **nginx: "configuration file test failed"**: Run nginx -t to check config syntax
- **"Timeout: service did not start within expected time"**: Service startup hangs, check logs

</details>

[↑ Back to Top](#table-of-contents)

## ✅ Best Practices

### Process Management Best Practices

1. **Monitor Regularly**
   - Check system load with `uptime` and `top`
   - Look for processes using too much CPU or memory
   - Be aware of what's running on your system

2. **Kill Processes Safely**
   - Try `kill PID` first (graceful termination)
   - Use `kill -9 PID` only when necessary (forceful kill)
   - Always check if the process actually stopped

> 🚨 **Critical**: Never use `kill -9` on system services without trying graceful shutdown first. This can cause data corruption.

3. **Use Background Jobs Wisely**
   - Use `&` for long-running commands
   - Use `nohup` for processes that should survive logout
   - Keep track of background jobs with `jobs`

4. **Keep It Simple**
   - Don't run unnecessary processes
   - Close applications you're not using
   - Monitor system resources regularly

### SSH and Remote Process Management

1. **Always Use Background Processes for Long Tasks**
   - Use `&` to run commands in background: `command &`
   - Use `nohup` for critical tasks: `nohup command &`
   - Never run long processes in foreground over SSH

2. **Understand Process Persistence**
   - Foreground processes die when SSH disconnects
   - Background processes survive if started with `nohup`
   - Screen/tmux sessions persist even after disconnection

3. **Best Practices for SSH Sessions**
   ```bash
   # Good: Long backup process that survives disconnection
   nohup rsync -av /data/ backup-server:/backups/ &
   
   # Better: Using screen for interactive long tasks
   screen -S maintenance
   # Run your commands inside screen
   # Detach with Ctrl+A, D
   
   # Best: Combine nohup with logging
   nohup ./long-script.sh > script.log 2>&1 &
   ```

4. **Monitor Remote Processes**
   - Always check if your background processes are running
   - Save important process PIDs: `echo $! > process.pid`
   - Use `ps aux | grep your_command` to verify processes
   - Monitor logs: `tail -f logfile.log`

### Service Management Best Practices

1. **Understand the Difference: State vs Configuration**
   - **Current State**: Is the service running right now?
   - **Boot Configuration**: Will the service start automatically at boot?
   - Always check both: `systemctl status service` and `systemctl is-enabled service`

2. **Use Appropriate Commands for Your Goal**
   ```bash
   # To start a service now only
   sudo systemctl start service
   
   # To start a service now AND at boot
   sudo systemctl enable --now service
   
   # To stop a service but keep it enabled for boot
   sudo systemctl stop service
   
   # To permanently disable a service
   sudo systemctl disable --now service
   ```

3. **Check Before Making Changes**
   - Always check service status before starting/stopping
   - Understand what a service does before disabling it
   - Check dependencies before making changes: `systemctl list-dependencies service`

4. **Use Proper Troubleshooting Sequence**
   ```bash
   # 1. Check status first
   systemctl status service
   
   # 2. Check logs for errors
   journalctl -u service --since "10 minutes ago"
   
   # 3. Check dependencies
   systemctl list-dependencies service --failed
   
   # 4. Check configuration
   systemctl cat service
   
   # 5. Check resource conflicts (ports, files)
   ss -tulpn | grep :port_number
   ```

5. **Use Proper Commands**
   - Use `systemctl` for service management
   - Use `journalctl` to check logs when troubleshooting
   - Always use `sudo` when starting/stopping services

6. **Document Changes**
   - Keep track of what services you enable/disable
   - Document why you made specific changes
   - Test changes in a safe environment first

7. **Security Awareness**
   - Don't run unnecessary services
   - Keep services updated
   - Monitor service logs for unusual activity
   - Use `systemctl mask` to completely prevent a service from starting

[↑ Back to Top](#table-of-contents)

## 🔧 Troubleshooting

### Understanding Error Codes and Exit Status

Before diving into specific problems, it's important to understand how Linux communicates errors:

#### Process Exit Codes
```bash
# Check the exit code of the last command
echo $?

# Common exit codes:
# 0 = Success
# 1 = General error
# 2 = Misuse of shell command
# 126 = Command cannot execute
# 127 = Command not found
# 128 = Invalid argument to exit
# 130 = Script terminated by Ctrl+C
# 137 = Process killed by SIGKILL (kill -9)
# 143 = Process killed by SIGTERM (kill)
```

#### Signal Numbers (for kill commands)
```bash
# Common signals you'll encounter:
# SIGHUP (1) = Hangup, often when SSH disconnects
# SIGINT (2) = Interrupt (Ctrl+C)
# SIGKILL (9) = Force kill (cannot be caught)
# SIGTERM (15) = Graceful termination request (default kill)

# Check what signal killed a process
journalctl -u service-name | grep -i signal
```

#### SSH-Related Error Patterns
```bash
# These indicate processes died from SSH disconnect:
"Broken pipe"
"Connection reset by peer"  
"SIGHUP received"
"Process terminated with signal 1"

# Prevention research topics:
# - nohup command usage
# - screen/tmux persistent sessions
# - systemd user services
# - disown built-in command
```

#### Service Error Categories
```bash
# Configuration errors (fix config files):
"Unit not found"
"Failed to parse"
"Invalid configuration"

# Permission errors (check sudo/ownership):
"Permission denied"
"Operation not permitted"
"Access denied"

# Resource conflicts (check ports/files):
"Address already in use"
"Resource busy"
"File exists"

# Dependency errors (check required services):
"Dependency failed"
"Job dependency failed"
"Unit xxx is not loaded"
```

#### How to Research Error Codes
```bash
# 1. Check the exact error message
systemctl status service-name -l --no-pager

# 2. Look up exit codes
man systemd.exec  # For systemd service exit codes
man bash          # For shell exit codes

# 3. Search logs for patterns
journalctl -u service-name | grep -i "error\|failed\|exit"

# 4. Use online resources
# - Search: "linux exit code 127"
# - Search: "systemd unit not found"
# - Search: "SIGHUP ssh disconnect"

# 5. Check system documentation
man kill          # For signal numbers
man systemctl     # For systemctl exit codes
```

#### Practice Error Research
When you encounter an error code in the labs, research it using these steps:
1. **Note the exact error message and code**
2. **Use `man` pages to understand what it means**
3. **Search online for "linux [error message]"**
4. **Look for solutions in forums like Stack Overflow**
5. **Test the solution in a safe environment**
6. **Document what worked for future reference**

#### Systematic Error Investigation Method
```bash
# Step 1: Capture the complete error
command_that_failed 2>&1 | tee error.log

# Step 2: Check exit code immediately
echo "Exit code: $?"

# Step 3: Research the specific error
man command_name  # Look for exit codes section
apropos "error keyword"  # Find related man pages

# Step 4: Check system context
dmesg | tail -20  # System messages
journalctl --since "5 minutes ago"  # Recent system logs

# Step 5: Search for patterns
grep -r "error message" /var/log/  # Look in logs
```

#### Error Code Categories and Research Strategies

**SSH/Network Errors** - Focus on connection and authentication:
```bash
# Research these patterns:
ssh -v user@host  # Verbose SSH debug output
ping -c 3 hostname  # Basic connectivity
telnet hostname 22  # Port accessibility
ssh-keygen -l -f keyfile  # Key fingerprints
```

**Process Management Errors** - Focus on signals and permissions:
```bash
# Research these patterns:
kill -l  # List all signal numbers
ps aux | grep process_name  # Find actual process state
pstree  # Show process relationships
lsof -p PID  # What files process has open
```

**Service Errors** - Focus on dependencies and configuration:
```bash
# Research these patterns:
journalctl -u service_name --since "1 hour ago"  # Service logs
systemctl cat service_name  # View service definition
systemctl list-dependencies service_name  # Check dependencies
service_name -t  # Test configuration (nginx, apache)
```

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

### SSH-Related Process Issues

#### Process Died When SSH Disconnected
**Problem:** Long-running process stopped when SSH session ended
**Why This Happens:** Processes started in foreground are tied to the SSH session
**Solutions:**
```bash
# Prevention: Always use nohup for long tasks
nohup command &

# Or use screen/tmux
screen -S session_name
# Run your command
# Detach: Ctrl+A, D

# Recovery: Check if process actually stopped
ps aux | grep your_command
jobs  # Won't show if SSH session ended

# Restart properly
nohup ./your-command > output.log 2>&1 &
```

#### Can't Find Background Process After Reconnecting
**Problem:** Started process with `&` but can't see it after reconnecting SSH
**Why This Happens:** `jobs` command only shows current session jobs
**Solutions:**
```bash
# Find process by name
ps aux | grep process_name
pgrep process_name

# Find by command pattern
ps aux | grep "part_of_command"

# Check if process is still writing to log files
lsof | grep your_logfile
tail -f your_logfile
```

#### Process Running But Can't Control It
**Problem:** Process started in previous SSH session, need to stop it
**Solutions:**
```bash
# Find the process ID
ps aux | grep process_name
pgrep -f "command_pattern"

# Kill by PID
kill 1234

# Kill by name
killall process_name
pkill -f "command_pattern"

# For stubborn processes
kill -9 1234
```

### Common Service Problems

#### Service Won't Start - Systematic Troubleshooting
**Problem:** `systemctl start` fails

**Step-by-Step Diagnosis:**
```bash
# Step 1: Get detailed status
systemctl status service-name --no-pager -l

# Step 2: Check what the status tells you
# Look for:
# - "Loaded: failed" = configuration problem
# - "Active: failed" = runtime problem  
# - "Active: inactive (dead)" = stopped normally

# Step 3: Check recent logs
journalctl -u service-name --since "10 minutes ago" --no-pager

# Step 4: Check for common issues
# Port conflicts
ss -tulpn | grep :80  # Replace 80 with your service port

# Permission issues
ls -la /etc/service-name/
systemctl cat service-name  # Check service file

# Dependency issues
systemctl list-dependencies service-name --failed

# Step 5: Try starting with live log monitoring
sudo systemctl start service-name
journalctl -u service-name -f
```

**Common Error Patterns:**
```bash
# "Address already in use" - Port conflict
ss -tulpn | grep :port_number
systemctl status other-web-server

# "Permission denied" - File permissions
ls -la /path/to/service/files
# Check service user in: systemctl cat service-name

# "No such file or directory" - Missing files
systemctl cat service-name  # Check ExecStart path
which command_name

# "Failed to start" with exit code
journalctl -u service-name | grep "code=exited"
# Common codes: 1=general error, 2=invalid argument, 127=command not found
```

#### Service Keeps Stopping/Restarting
**Problem:** Service starts but stops shortly after or keeps restarting

**Diagnosis Process:**
```bash
# Monitor in real-time
journalctl -u service-name -f

# Check restart configuration
systemctl show service-name | grep Restart

# Look for crash patterns
journalctl -u service-name | grep -E "signal|killed|dumped|exit"

# Check resource limits
systemctl show service-name | grep -E "Memory|CPU|Limit"

# Check configuration validity
# Web servers: nginx -t, apache2ctl configtest
# Database: mysql --help (tests config parsing)
```

#### Service Status Shows "Failed"
**Problem:** Service status shows failed state

**Recovery Steps:**
```bash
# Reset the failed state
sudo systemctl reset-failed service-name

# Check what caused the failure
journalctl -u service-name --since "1 hour ago"

# Try starting again
sudo systemctl start service-name

# If it fails again, check dependencies
systemctl list-dependencies service-name
systemctl status dependency-service
```

#### Can't Connect to Service
**Problem:** Service appears running but can't connect

**Network Troubleshooting:**
```bash
# Verify service is actually running
systemctl status service-name
ps aux | grep service-name

# Check if service is listening on expected port
ss -tulpn | grep port-number

# Check firewall (if applicable)
sudo ufw status  # Ubuntu
sudo iptables -L  # General Linux

# Test local connection
telnet localhost port-number
curl -I http://localhost:port-number

# Try restarting the service
sudo systemctl restart service-name
```

#### Understanding systemctl Status Output
```bash
# Example output explanation:
systemctl status nginx

● nginx.service - A high performance web server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2025-08-03 10:30:15 UTC; 2h 15min ago
     Docs: man:nginx(8)
  Process: 1234 ExitCode=0 (success)
 Main PID: 1234 (nginx)
    Tasks: 2 (limit: 4915)
   Memory: 6.8M
   CGroup: /system.slice/nginx.service
           ├─1234 nginx: master process /usr/sbin/nginx
           └─1235 nginx: worker process

# Key indicators:
# ● = running (● green dot), ○ = stopped, × = failed
# Loaded: loaded = config OK, error = config problem
# enabled = starts at boot, disabled = doesn't start at boot
# Active: active (running) = working, inactive (dead) = stopped, failed = crashed
# Main PID = main process ID
# Tasks = number of processes/threads
# Memory = current memory usage
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

[↑ Back to Top](#table-of-contents)

## 📋 Summary

This module covered the essential skills for managing processes and services in Linux systems. You learned:

## ✅ Self-Assessment Checklist
After completing this module, you should be able to:
- [ ] Explain the difference between processes and services
- [ ] Monitor system performance using command-line tools
- [ ] Safely manage processes in SSH sessions using `nohup` and `screen`
- [ ] Troubleshoot basic service startup issues
- [ ] Understand systemd service states (active/inactive + enabled/disabled)
- [ ] Use `systemctl` commands confidently
- [ ] Read and interpret `journalctl` logs
- [ ] Implement SSH-safe process management practices

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

## ➡️ Next Steps

Continue building your Linux administration skills with:

- **Module 6: Users, Groups & Authentication** - Learn user and permission management
- **Module 7: Networking Fundamentals** - Understand network configuration
- **Module 8: Logging and Monitoring** - Advanced system monitoring and log analysis

## 📖 Additional Resources
- 📘 **Man Pages**: `man ps`, `man systemctl`, `man kill`, `man journalctl`
- 🌐 **Documentation**: [systemd.io](https://systemd.io/) - Official systemd documentation
- 📋 **Quick Reference**: [Linux Process Management Cheat Sheet](https://www.gnu.org/software/coreutils/manual/)
- 🎥 **Further Learning**: Search for "Linux systemd tutorial" and "SSH process management"

> 💡 **Remember**: The process and service management skills from this module are fundamental for maintaining stable Linux systems and will be used throughout your system administration career.

[↑ Back to Top](#table-of-contents)
