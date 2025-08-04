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

## Practical Examples

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

### Service Management Examples

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

#### Example 3: Regular Maintenance Tasks
```bash
# List all failed services
systemctl --failed

# List all enabled services
systemctl list-unit-files --type=service --state=enabled

# Restart a service safely
sudo systemctl restart ssh
```

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
