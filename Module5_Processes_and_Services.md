# Module 5: Processes & Services

## Overview
Learn how Linux starts, monitors, and controls both one-off processes and long-running daemons—critical for reliable service delivery. This module covers comprehensive process management and service administration, from basic process monitoring to advanced systemd service configuration and troubleshooting.

## Learning Objectives
By the end of this module, you will be able to:
1. List and filter processes to diagnose CPU, memory, and I/O usage using `ps`, `top`, and `htop`
2. Terminate or reprioritize runaway processes safely using signals, `kill`, `pkill`, and priority controls
3. Query and follow service logs using `journalctl` for effective troubleshooting
4. Enable or disable services at boot and on-demand using `systemctl` commands
5. Write and test a custom systemd service unit with proper dependencies and error handling
6. Understand init systems: SysV init scripts vs. Upstart vs. systemd architecture
7. Structure systemd unit files including `.service`, `.socket`, `.timer`, and `.target` types
8. Manage process priorities with `nice` and `renice` for optimal system performance
9. Troubleshoot process and service issues using systematic diagnostic approaches
10. Implement service monitoring and automated recovery strategies

## Topics

### 5.1 Process Fundamentals
- What are processes?
- Process lifecycle and states
- Process IDs (PID) and Parent Process IDs (PPID)
- Process trees and relationships
- Foreground vs background processes
- Daemons and system processes

### 5.2 Advanced Process Monitoring
- `ps` command variations for filtering and sorting
- Real-time monitoring with `top` and `htop`
- Process searching with `pgrep` and `pkill`
- `/proc` filesystem exploration and analysis
- Process resource usage monitoring (CPU, memory, I/O)
- Identifying performance bottlenecks

### 5.3 Process Control and Signal Management
- Starting processes in background
- Job control: `jobs`, `fg`, `bg`
- Process signals and safe termination methods
- `kill` and `pkill` for process management
- `nohup` for persistent processes
- Signal handling and graceful shutdowns

### 5.4 Init Systems Evolution
- Understanding Linux boot process
- SysV init scripts: structure and limitations
- Upstart: event-driven initialization
- systemd: modern service management
- Comparing init system architectures
- Migration considerations and compatibility

### 5.5 Systemd Service Management
- Understanding systemd architecture and components
- Service discovery and dependency resolution
- Starting, stopping, and restarting services with `systemctl`
- Enabling and disabling services at boot
- Service status monitoring and health checks
- Using `journalctl` for service log analysis

### 5.6 Systemd Unit Files
- Service unit files (`.service`) structure and configuration
- Socket activation with `.socket` units
- Timer units (`.timer`) for scheduled tasks
- Target units (`.target`) for system states
- Mount and device units
- Creating custom unit files with proper dependencies

### 5.7 Process Priority and Scheduling
- Understanding process nice values and scheduling
- `nice` and `renice` commands for priority management
- Real-time scheduling classes and policies
- CPU affinity with `taskset`
- Resource limits and cgroups integration
- CPU affinity with `taskset`
- Process scheduling classes

### 5.6 Advanced Process Management
- Process groups and sessions
- Screen and tmux for session management
- Monitoring system resources
- Process troubleshooting techniques

## Init Systems Comparison

### SysV Init (Traditional)
```bash
# SysV init script structure
#!/bin/bash
# /etc/init.d/myservice
# chkconfig: 35 80 20
# description: My custom service

. /etc/rc.d/init.d/functions

USER="myuser"
DAEMON="myservice"
ROOT_DIR="/var/lib/myservice"
PID_FILE="/var/run/myservice.pid"

case "$1" in
    start)
        echo -n "Starting $DAEMON: "
        daemon --user $USER --pidfile $PID_FILE $ROOT_DIR/$DAEMON
        echo
        ;;
    stop)
        echo -n "Shutting down $DAEMON: "
        pid=$(ps -aefw | grep "$DAEMON" | grep -v " grep " | awk '{print $2}')
        kill -9 $pid > /dev/null 2>&1
        echo
        ;;
    restart)
        $0 stop
        $0 start
        ;;
    status)
        status $DAEMON
        ;;
    *)
        echo "Usage: $0 {start|stop|restart|status}"
        exit 1
esac
```

**SysV Characteristics:**
- Sequential startup (slow boot times)
- Shell script-based configuration
- Manual dependency management
- Simple but limited functionality
- Still used in some embedded systems

### Upstart (Ubuntu Legacy)
```bash
# /etc/init/myservice.conf
description "My custom service"
author "System Administrator"

start on runlevel [2345]
stop on runlevel [!2345]

respawn
respawn limit 10 5

setuid myuser
setgid mygroup

chdir /opt/myservice

exec /opt/myservice/bin/myservice
```

**Upstart Characteristics:**
- Event-driven initialization
- Better dependency handling
- Automatic respawning
- Job-based rather than script-based
- Bridged gap between SysV and systemd

### Systemd (Modern Standard)
```ini
# /etc/systemd/system/myservice.service
[Unit]
Description=My Custom Service
Documentation=https://example.com/docs
After=network.target
Wants=network-online.target
Requires=postgresql.service

[Service]
Type=notify
User=myuser
Group=mygroup
WorkingDirectory=/opt/myservice
ExecStart=/opt/myservice/bin/myservice --config /etc/myservice/config.conf
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -TERM $MAINPID
Restart=always
RestartSec=5
TimeoutStopSec=30
KillMode=mixed
PrivateTmp=true
NoNewPrivileges=true
ProtectSystem=strict
ReadWritePaths=/var/lib/myservice

[Install]
WantedBy=multi-user.target
```

**Systemd Advantages:**
- Parallel service startup (faster boot)
- Advanced dependency management
- Socket activation and on-demand starting
- Comprehensive logging with journald
- Resource management and security features
- Consistent interface across all distributions

### Init System Comparison Table

| Feature | SysV Init | Upstart | systemd |
|---------|-----------|---------|---------|
| Boot Speed | Slow (sequential) | Medium | Fast (parallel) |
| Dependency Management | Manual | Event-driven | Automatic |
| Service Monitoring | Basic | Good | Excellent |
| Logging | Syslog | Syslog | journald |
| Socket Activation | No | Limited | Yes |
| Resource Control | No | Limited | cgroups |
| Security Features | Basic | Medium | Advanced |
| Configuration | Shell scripts | Job files | Unit files |

## Practical Examples

### Advanced Process Monitoring and Filtering
```bash
# Show all processes with detailed information
ps aux

# Show process tree with relationships
ps auxf
pstree -p

# Show processes for specific user
ps -u username
ps -U username  # by real user ID

# Filter processes by CPU usage (top consumers)
ps aux --sort=-%cpu | head -10

# Filter processes by memory usage
ps aux --sort=-%mem | head -10

# Show processes with custom output format
ps -eo pid,ppid,cmd,%cpu,%mem,etime,user

# Show processes with specific state
ps aux | awk '$8 ~ /^Z/ {print}' # Zombie processes
ps aux | awk '$8 ~ /^D/ {print}' # Uninterruptible sleep

# Real-time process monitoring
top -p $(pgrep nginx | tr '\n' ',' | sed 's/,$//')

# Enhanced process monitor with filtering
htop -u nginx  # Show only nginx user processes

# Show specific process details
ps -p 1234 -o pid,ppid,cmd,stat,etime,%cpu,%mem

# Find processes by name with detailed info
pgrep -a nginx      # Show command line
pgrep -f "python.*script"  # Match full command line
pgrep -l -u www-data       # List with names for user

# Monitor process resource usage over time
pidstat -p 1234 1 5    # Monitor PID 1234 every 1 second for 5 times
pidstat -u 1 5         # Monitor CPU usage
pidstat -r 1 5         # Monitor memory usage
pidstat -d 1 5         # Monitor I/O usage

# Find processes using specific files
lsof /var/log/nginx/access.log
fuser -v /var/log/nginx/access.log

# Show processes listening on network ports
ss -tulpn | grep :80
netstat -tulpn | grep :80

# Find processes using the most file descriptors
lsof | awk '{print $2}' | sort | uniq -c | sort -nr | head -10
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

### Comprehensive Systemd Service Management
```bash
# Service Control Operations
sudo systemctl start nginx          # Start service
sudo systemctl stop nginx           # Stop service  
sudo systemctl restart nginx        # Restart service
sudo systemctl reload nginx         # Reload configuration without restart
sudo systemctl try-restart nginx    # Restart only if running
sudo systemctl reload-or-restart nginx  # Reload if possible, otherwise restart

# Service Status and Information
systemctl status nginx              # Detailed service status
systemctl is-active nginx           # Check if service is running
systemctl is-enabled nginx          # Check if service is enabled
systemctl is-failed nginx           # Check if service failed
systemctl show nginx                # Show all service properties
systemctl cat nginx                 # Show service unit file

# Service Enable/Disable Operations
sudo systemctl enable nginx         # Enable at boot
sudo systemctl disable nginx        # Disable at boot
sudo systemctl mask nginx           # Prevent service from starting
sudo systemctl unmask nginx         # Remove mask
sudo systemctl reenable nginx       # Disable then enable (refresh links)

# Listing and Filtering Services
systemctl list-units --type=service                    # All loaded services
systemctl list-units --type=service --state=active    # Active services
systemctl list-units --type=service --state=failed    # Failed services
systemctl list-unit-files --type=service              # All available services
systemctl list-dependencies nginx                      # Service dependencies
systemctl list-dependencies --reverse nginx           # What depends on nginx

# Advanced Service Queries
systemctl --failed                                     # Show failed services
systemctl --failed --type=service                     # Failed services only
systemctl list-jobs                                   # Show active jobs
systemctl list-sockets                                # Show socket units
systemctl list-timers                                 # Show timer units

# System State Management
systemctl get-default                                 # Show default target
sudo systemctl set-default multi-user.target         # Set default target
systemctl list-units --type=target                   # List all targets
sudo systemctl isolate rescue.target                 # Switch to rescue mode

# Service Logs with journalctl
journalctl -u nginx                                   # Show service logs
journalctl -u nginx -f                               # Follow logs in real-time
journalctl -u nginx --since "2025-01-01"             # Logs since date
journalctl -u nginx --since "1 hour ago"             # Logs since 1 hour ago
journalctl -u nginx -n 50                            # Last 50 log entries
journalctl -u nginx -p err                           # Error level logs only
journalctl -u nginx -o json-pretty                   # JSON formatted output
journalctl -u nginx --no-pager                       # Don't use pager
journalctl -u nginx --reverse                        # Show newest first

# System-wide Journal Operations
journalctl --disk-usage                              # Show journal disk usage
journalctl --vacuum-time=2weeks                      # Clean logs older than 2 weeks
journalctl --vacuum-size=500M                        # Keep only 500MB of logs
journalctl --list-boots                              # Show boot records
journalctl -b 0                                      # Current boot logs
journalctl -b -1                                     # Previous boot logs

# Performance and Resource Monitoring
systemd-analyze                                      # Boot time analysis
systemd-analyze blame                                # Show slow-starting services
systemd-analyze critical-chain                       # Show critical boot path
systemd-analyze plot > bootchart.svg                # Generate boot chart
systemd-cgtop                                        # Live cgroup resource monitor
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
