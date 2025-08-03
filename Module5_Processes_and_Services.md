# Module 5: Processes & Services

## Overview
This module covers process management and service administration in Linux. You'll learn to monitor running processes, manage system services, and understand process scheduling and priority management.

## Learning Objectives
By the end of this module, you will be able to:
- Monitor and manage Linux processes
- Control system services using systemd
- Understand process states and signals
- Manage process priorities and scheduling
- Troubleshoot process and service issues
- Configure service startup and dependencies

## Topics

### 5.1 Process Fundamentals
- What are processes?
- Process lifecycle and states
- Process IDs (PID) and Parent Process IDs (PPID)
- Process trees and relationships
- Foreground vs background processes
- Daemons and system processes

### 5.2 Process Monitoring
- `ps` command variations
- `top` and `htop` for real-time monitoring
- `pgrep` and `pkill` for process searching
- `/proc` filesystem exploration
- Process resource usage monitoring

### 5.3 Process Control
- Starting processes in background
- Job control: `jobs`, `fg`, `bg`
- Process signals and `kill` command
- `nohup` for persistent processes
- Process termination methods

### 5.4 Systemd Service Management
- Understanding systemd architecture
- Service units and unit files
- Starting, stopping, and restarting services
- Enabling and disabling services
- Service status and logs
- Creating custom service units

### 5.5 Process Priority and Scheduling
- Process nice values
- `nice` and `renice` commands
- Real-time scheduling
- CPU affinity with `taskset`
- Process scheduling classes

### 5.6 Advanced Process Management
- Process groups and sessions
- Screen and tmux for session management
- Monitoring system resources
- Process troubleshooting techniques

## Practical Examples

### Basic Process Monitoring
```bash
# Show all processes
ps aux

# Show process tree
ps auxf
# or
pstree

# Show processes for specific user
ps -u username

# Real-time process monitoring
top

# Enhanced process monitor (if installed)
htop

# Show specific process info
ps -p 1234

# Find processes by name
pgrep nginx
ps aux | grep nginx
```

### Process Control
```bash
# Start process in background
command &

# List background jobs
jobs

# Bring job to foreground
fg %1

# Send job to background
bg %1

# Start process immune to hangups
nohup long-running-command &

# Kill process by PID
kill 1234

# Kill process by name
pkill nginx

# Force kill process
kill -9 1234
kill -KILL 1234
```

### Systemd Service Management
```bash
# Start a service
sudo systemctl start nginx

# Stop a service
sudo systemctl stop nginx

# Restart a service
sudo systemctl restart nginx

# Reload service configuration
sudo systemctl reload nginx

# Check service status
systemctl status nginx

# Enable service at boot
sudo systemctl enable nginx

# Disable service at boot
sudo systemctl disable nginx

# List all services
systemctl list-units --type=service

# List failed services
systemctl --failed

# Show service logs
journalctl -u nginx

# Follow service logs in real-time
journalctl -u nginx -f
```

### Process Priority Management
```bash
# Start process with lower priority
nice -n 10 command

# Change priority of running process
renice 5 -p 1234

# Show current nice values
ps -eo pid,ppid,ni,comm

# Set CPU affinity
taskset -c 0,1 command

# Show CPU affinity
taskset -p 1234
```

## Signal Types and Usage

| Signal | Number | Description | Usage |
|--------|--------|-------------|-------|
| SIGTERM | 15 | Graceful termination | `kill 1234` |
| SIGKILL | 9 | Force termination | `kill -9 1234` |
| SIGHUP | 1 | Reload configuration | `kill -HUP 1234` |
| SIGSTOP | 19 | Pause process | `kill -STOP 1234` |
| SIGCONT | 18 | Resume process | `kill -CONT 1234` |
| SIGUSR1 | 10 | User-defined signal | `kill -USR1 1234` |

## Creating Custom Systemd Service

### Service Unit File Example
```ini
# /etc/systemd/system/myapp.service
[Unit]
Description=My Application
After=network.target

[Service]
Type=simple
User=myuser
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/bin/myapp
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

### Service Management Commands
```bash
# Reload systemd configuration
sudo systemctl daemon-reload

# Enable and start custom service
sudo systemctl enable myapp.service
sudo systemctl start myapp.service

# Check service status
systemctl status myapp.service
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

## Troubleshooting Common Issues

### High CPU Usage
```bash
# Find CPU-intensive processes
top -o %CPU

# Check load average
uptime

# Detailed CPU analysis
iostat -c 1 5
```

### Memory Issues
```bash
# Check memory usage
free -h

# Find memory-intensive processes
ps aux --sort=-%mem | head

# Check for memory leaks
valgrind --leak-check=full command
```

### Service Startup Issues
```bash
# Check service logs
journalctl -u servicename

# Check service dependencies
systemctl list-dependencies servicename

# Verify service configuration
systemctl cat servicename
```

## Best Practices
- Use appropriate signals for process termination
- Monitor system resources regularly
- Create proper service unit files with dependencies
- Use process priorities judiciously
- Implement proper logging for custom services
- Test service configurations before deployment

## Lab Exercises
1. Monitor system processes during high load
2. Create a custom systemd service
3. Practice process priority management
4. Troubleshoot a failing service
5. Set up process monitoring scripts

## Next Steps
With process and service management skills, you're ready to explore Users, Groups & Authentication in Module 6, where you'll learn to manage user accounts and system security.
