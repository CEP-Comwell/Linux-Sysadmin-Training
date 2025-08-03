# Module 5: Processes & Services

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [5.1 Process Fundamentals](#51-process-fundamentals)
  - [5.2 Advanced Process Monitoring](#52-advanced-process-monitoring)
  - [5.3 Process Control and Signal Management](#53-process-control-and-signal-management)
  - [5.4 Init Systems Evolution](#54-init-systems-evolution)
  - [5.5 Systemd Service Management](#55-systemd-service-management)
  - [5.6 Systemd Unit Files](#56-systemd-unit-files)
  - [5.7 Process Priority and Scheduling](#57-process-priority-and-scheduling)
  - [5.8 Advanced Service Configuration](#58-advanced-service-configuration)
  - [5.9 Performance Monitoring and Troubleshooting](#59-performance-monitoring-and-troubleshooting)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [Process Management and Monitoring](#process-management-and-monitoring)
  - [Signal Management and Process Control](#signal-management-and-process-control)
  - [Systemd Service Operations](#systemd-service-operations)
  - [Custom Service Creation](#custom-service-creation)
  - [Performance Analysis Scripts](#performance-analysis-scripts)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Process Monitoring and Management](#lab-1-process-monitoring-and-management)
  - [Lab 2: Systemd Service Configuration](#lab-2-systemd-service-configuration)
  - [Lab 3: Custom Service Development](#lab-3-custom-service-development)
  - [Lab 4: Performance Analysis and Optimization](#lab-4-performance-analysis-and-optimization)
- [Best Practices Summary](#best-practices-summary)
- [Troubleshooting Guide](#troubleshooting-guide)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)

## Overview
Master Linux process management and service administration—critical skills for maintaining reliable, high-performance systems. This module covers everything from basic process monitoring to advanced systemd service configuration, performance optimization, and enterprise-grade troubleshooting methodologies.

**Key Learning Outcomes:**
- Monitor and analyze system processes using advanced filtering and diagnostic techniques
- Implement comprehensive service management strategies with systemd
- Create and deploy custom services with proper dependency management and error handling
- Optimize system performance through process prioritization and resource management
- Troubleshoot complex process and service issues using systematic methodologies
- Design automated monitoring and recovery solutions for production environments

## Learning Objectives
By the end of this module, you will be able to:

1. **Master Process Analysis**: Use `ps`, `top`, `htop`, and `/proc` filesystem to diagnose system performance issues
2. **Control Process Execution**: Manage process lifecycle using signals, job control, and priority adjustment
3. **Implement Service Management**: Configure and manage services using systemd with advanced dependency handling
4. **Create Custom Services**: Design and deploy custom systemd unit files with proper security and resource controls
5. **Optimize Performance**: Apply process prioritization, CPU affinity, and resource limits for optimal system performance
6. **Troubleshoot Systematically**: Diagnose and resolve complex process and service issues using structured methodologies
7. **Monitor Proactively**: Implement automated monitoring and alerting for critical system processes and services
8. **Ensure High Availability**: Design service configurations with automatic recovery and failover capabilities

## Topics

### 5.1 Process Fundamentals
- Process lifecycle: creation, execution, termination, and zombie processes
- Process identification: PID, PPID, process groups, and sessions
- Process states: running, sleeping, stopped, zombie, and uninterruptible sleep
- Process relationships: parent-child hierarchies and process trees
- Foreground vs background execution models
- Daemon processes and service architecture patterns

### 5.2 Advanced Process Monitoring
- Comprehensive process listing with `ps` command variations and custom formatting
- Real-time monitoring using `top`, `htop`, and specialized process monitors
- Process searching and filtering with `pgrep`, `pkill`, and pattern matching
- `/proc` filesystem exploration for detailed process information
- Resource usage analysis: CPU, memory, I/O, and network utilization
- Performance bottleneck identification and capacity planning

### 5.3 Process Control and Signal Management
- Job control mechanisms: background execution, job management, and session control
- Signal types and handling: termination, interruption, and custom signals
- Safe process termination strategies and graceful shutdown procedures
- Process persistence with `nohup`, `screen`, and `tmux`
- Advanced signal handling and inter-process communication
- Process debugging and core dump analysis

### 5.4 Init Systems Evolution
- Linux boot process: kernel initialization to user space
- SysV init: runlevels, init scripts, and sequential service startup
- Upstart: event-driven initialization and dependency management
- systemd: modern service management with parallel startup and advanced features
- Init system comparison: performance, complexity, and feature analysis
- Migration strategies and compatibility considerations

### 5.5 Systemd Service Management
- systemd architecture: units, targets, and dependency resolution
- Service lifecycle management: start, stop, restart, reload operations
- Service status monitoring and health checking mechanisms
- Boot-time service configuration: enable, disable, and mask operations
- Log analysis with `journalctl`: filtering, following, and structured logging
- Service discovery and inter-service communication

### 5.6 Systemd Unit Files
- Service unit structure: [Unit], [Service], and [Install] sections
- Socket activation: on-demand service startup and resource optimization
- Timer units: systemd-based scheduling and cron replacement
- Target units: system state management and dependency grouping
- Mount and device units: filesystem and hardware integration
- Template units: parameterized services and instance management

### 5.7 Process Priority and Scheduling
- Linux scheduler: Completely Fair Scheduler (CFS) and scheduling classes
- Process nice values: priority adjustment and impact on scheduling
- Real-time scheduling: FIFO, Round Robin, and deadline scheduling
- CPU affinity: binding processes to specific cores for performance
- Resource limits: memory, CPU time, and file descriptor constraints
- Control groups (cgroups): resource allocation and limits

### 5.8 Advanced Service Configuration
- Security hardening: user isolation, capability restrictions, and sandboxing
- Resource management: memory limits, CPU quotas, and I/O throttling
- Network configuration: socket activation, firewall integration, and service mesh
- Environment management: variable injection, secret handling, and configuration
- Dependency modeling: complex service relationships and startup ordering
- Health checking: readiness probes, liveness checks, and automatic recovery

### 5.9 Performance Monitoring and Troubleshooting
- System-wide performance analysis: CPU, memory, I/O, and network metrics
- Process-specific diagnostics: profiling, tracing, and resource utilization
- Service troubleshooting: log analysis, dependency checking, and state validation
- Automated monitoring: alerting, metrics collection, and trend analysis
- Capacity planning: resource forecasting and scaling strategies
- Incident response: systematic troubleshooting and root cause analysis

## Essential Command Reference

### Process Monitoring Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `ps` | List processes | `aux`, `-ef`, `-eo format` | `ps aux --sort=-%cpu` |
| `top` | Real-time process monitor | `-p PID`, `-u user` | `top -p 1234` |
| `htop` | Enhanced process monitor | `-u user`, `-p PID` | `htop -u nginx` |
| `pgrep` | Find processes by pattern | `-f`, `-u user`, `-l` | `pgrep -f nginx` |
| `pidstat` | Process statistics | `-u`, `-r`, `-d` | `pidstat -u 1 5` |
| `lsof` | List open files | `-p PID`, `-u user` | `lsof -p 1234` |

### Process Control Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `kill` | Send signal to process | `-TERM`, `-KILL`, `-HUP` | `kill -TERM 1234` |
| `pkill` | Kill processes by pattern | `-f`, `-u user`, `-TERM` | `pkill -f nginx` |
| `killall` | Kill by process name | `-TERM`, `-KILL` | `killall nginx` |
| `nohup` | Run immune to hangups | `&` for background | `nohup command &` |
| `jobs` | List background jobs | `-l`, `-p` | `jobs -l` |
| `fg` | Bring job to foreground | `%jobnum` | `fg %1` |
| `bg` | Send job to background | `%jobnum` | `bg %1` |

### Systemd Service Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `systemctl` | Service management | `start`, `stop`, `restart`, `status` | `systemctl status nginx` |
| `journalctl` | Log analysis | `-u unit`, `-f`, `--since` | `journalctl -u nginx -f` |
| `systemd-analyze` | Boot analysis | `blame`, `critical-chain` | `systemd-analyze blame` |
| `systemd-cgls` | Control group tree | `-u unit` | `systemd-cgls` |
| `systemd-cgtop` | Control group monitor | Real-time resource usage | `systemd-cgtop` |

### Process Priority Commands

| Command | Purpose | Key Options | Example |
|---------|---------|-------------|---------|
| `nice` | Start with priority | `-n priority` | `nice -n 10 command` |
| `renice` | Change process priority | `-n priority -p PID` | `renice 5 -p 1234` |
| `taskset` | Set CPU affinity | `-c cores -p PID` | `taskset -c 0,1 command` |
| `ionice` | Set I/O priority | `-c class -n level` | `ionice -c 2 -n 7 command` |

### Custom Service Creation

#### Complete Custom Service Development
```bash
#!/bin/bash
# service-creator.sh - Automated custom service creation and deployment

create_basic_service() {
    local service_name="$1"
    local executable_path="$2"
    local user="${3:-nobody}"
    local description="${4:-Custom service created by service-creator}"
    
    if [[ -z "$service_name" || -z "$executable_path" ]]; then
        echo "Usage: create_basic_service <service_name> <executable_path> [user] [description]"
        return 1
    fi
    
    echo "Creating basic service: $service_name"
    
    # Create service unit file
    cat > "/tmp/${service_name}.service" << EOF
[Unit]
Description=$description
Documentation=man:${service_name}(8)
After=network.target
Wants=network-online.target

[Service]
Type=simple
User=$user
Group=$user
ExecStart=$executable_path
Restart=always
RestartSec=5
TimeoutStartSec=30
TimeoutStopSec=30
KillMode=mixed

# Security settings
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/lib/$service_name

[Install]
WantedBy=multi-user.target
EOF

    echo "Service unit file created: /tmp/${service_name}.service"
    echo "To install: sudo cp /tmp/${service_name}.service /etc/systemd/system/"
    echo "Then run: sudo systemctl daemon-reload && sudo systemctl enable $service_name"
}

create_advanced_service() {
    local service_name="$1"
    local executable_path="$2"
    local config_file="$3"
    local user="${4:-$service_name}"
    
    if [[ -z "$service_name" || -z "$executable_path" ]]; then
        echo "Usage: create_advanced_service <service_name> <executable_path> [config_file] [user]"
        return 1
    fi
    
    echo "Creating advanced service: $service_name"
    
    # Create comprehensive service unit file
    cat > "/tmp/${service_name}.service" << EOF
[Unit]
Description=Advanced $service_name Service
Documentation=https://example.com/docs/$service_name
After=network.target network-online.target
Wants=network-online.target
Before=nginx.service
PartOf=application.target

[Service]
Type=notify
User=$user
Group=$user
WorkingDirectory=/opt/$service_name

# Main service configuration
ExecStartPre=/usr/bin/test -f $executable_path
ExecStart=$executable_path ${config_file:+--config $config_file}
ExecReload=/bin/kill -HUP \$MAINPID
ExecStop=/bin/kill -TERM \$MAINPID
TimeoutStartSec=60
TimeoutStopSec=30
TimeoutReloadSec=10

# Restart configuration
Restart=always
RestartSec=10
StartLimitInterval=300
StartLimitBurst=5

# Process management
KillMode=mixed
KillSignal=SIGTERM
SendSIGKILL=yes
FinalKillSignal=SIGKILL

# Resource limits
LimitNOFILE=65536
LimitNPROC=4096
MemoryMax=1G
CPUQuota=200%

# Security hardening
NoNewPrivileges=true
PrivateTmp=true
PrivateDevices=true
ProtectSystem=strict
ProtectHome=true
ProtectKernelTunables=true
ProtectKernelModules=true
ProtectKernelLogs=true
ProtectControlGroups=true
RestrictNamespaces=true
RestrictRealtime=true
RestrictSUIDSGID=true
LockPersonality=true
RemoveIPC=true

# Filesystem access
ReadWritePaths=/var/lib/$service_name
ReadWritePaths=/var/log/$service_name
ReadOnlyPaths=/etc/$service_name

# Network security
PrivateNetwork=false
RestrictAddressFamilies=AF_INET AF_INET6 AF_UNIX

# System calls
SystemCallFilter=@system-service
SystemCallFilter=~@debug @mount @cpu-emulation @obsolete @privileged @reboot @swap @raw-io
SystemCallErrorNumber=EPERM

[Install]
WantedBy=multi-user.target
Also=application.target
EOF

    echo "Advanced service unit file created: /tmp/${service_name}.service"
    
    # Create matching socket unit if needed
    if [[ "$5" == "socket" ]]; then
        cat > "/tmp/${service_name}.socket" << EOF
[Unit]
Description=$service_name Socket
PartOf=$service_name.service

[Socket]
ListenStream=8080
BindIPv6Only=both
ReusePort=true
FreeBind=true
Transparent=true
DeferAcceptSec=1

[Install]
WantedBy=sockets.target
EOF
        echo "Socket unit file created: /tmp/${service_name}.socket"
    fi
    
    # Create timer unit if needed
    if [[ "$6" == "timer" ]]; then
        cat > "/tmp/${service_name}.timer" << EOF
[Unit]
Description=Run $service_name periodically
Requires=$service_name.service

[Timer]
OnBootSec=15min
OnUnitActiveSec=1h
RandomizedDelaySec=300
Persistent=true

[Install]
WantedBy=timers.target
EOF
        echo "Timer unit file created: /tmp/${service_name}.timer"
    fi
}

# Service template generator
create_service_template() {
    local template_name="$1"
    local base_path="$2"
    
    if [[ -z "$template_name" || -z "$base_path" ]]; then
        echo "Usage: create_service_template <template_name> <base_path>"
        return 1
    fi
    
    echo "Creating service template: $template_name"
    
    # Create template unit file
    cat > "/tmp/${template_name}@.service" << EOF
[Unit]
Description=$template_name instance %i
Documentation=man:${template_name}(8)
After=network.target
BindsTo=${template_name}.service

[Service]
Type=simple
User=%i
Group=%i
WorkingDirectory=$base_path/%i
ExecStart=$base_path/bin/$template_name --instance %i
Environment=INSTANCE_NAME=%i
Environment=INSTANCE_ID=%i

# Instance-specific configuration
EnvironmentFile=-/etc/$template_name/%i.conf
ExecStartPre=/bin/mkdir -p /var/lib/$template_name/%i
ExecStartPre=/bin/chown %i:%i /var/lib/$template_name/%i

# Standard service options
Restart=always
RestartSec=5
TimeoutStartSec=30

# Security
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ReadWritePaths=/var/lib/$template_name/%i

[Install]
WantedBy=multi-user.target
EOF

    echo "Service template created: /tmp/${template_name}@.service"
    echo "Usage: systemctl enable ${template_name}@instance1.service"
    echo "       systemctl start ${template_name}@instance2.service"
}

# Service validation and testing
validate_service() {
    local service_file="$1"
    
    if [[ -z "$service_file" || ! -f "$service_file" ]]; then
        echo "Usage: validate_service <service_file_path>"
        return 1
    fi
    
    echo "=== Validating Service File: $service_file ==="
    
    # Check syntax
    echo "Checking syntax..."
    if systemd-analyze verify "$service_file" 2>/dev/null; then
        echo "✓ Syntax is valid"
    else
        echo "✗ Syntax errors found:"
        systemd-analyze verify "$service_file"
        return 1
    fi
    
    # Check required sections
    echo ""
    echo "Checking required sections..."
    
    local has_unit=$(grep -q "^\[Unit\]" "$service_file" && echo "yes" || echo "no")
    local has_service=$(grep -q "^\[Service\]" "$service_file" && echo "yes" || echo "no")
    local has_install=$(grep -q "^\[Install\]" "$service_file" && echo "yes" || echo "no")
    
    echo "  [Unit] section: $([[ $has_unit == "yes" ]] && echo "✓" || echo "✗")"
    echo "  [Service] section: $([[ $has_service == "yes" ]] && echo "✓" || echo "✗")"
    echo "  [Install] section: $([[ $has_install == "yes" ]] && echo "✓" || echo "✗")"
    
    # Check essential fields
    echo ""
    echo "Checking essential fields..."
    
    local has_description=$(grep -q "^Description=" "$service_file" && echo "yes" || echo "no")
    local has_execstart=$(grep -q "^ExecStart=" "$service_file" && echo "yes" || echo "no")
    local has_wantedby=$(grep -q "^WantedBy=" "$service_file" && echo "yes" || echo "no")
    
    echo "  Description: $([[ $has_description == "yes" ]] && echo "✓" || echo "✗")"
    echo "  ExecStart: $([[ $has_execstart == "yes" ]] && echo "✓" || echo "✗")"
    echo "  WantedBy: $([[ $has_wantedby == "yes" ]] && echo "✓" || echo "✗")"
    
    # Security analysis
    echo ""
    echo "Security analysis..."
    
    local security_options=(
        "NoNewPrivileges"
        "PrivateTmp"
        "ProtectSystem"
        "ProtectHome"
        "User"
    )
    
    for option in "${security_options[@]}"; do
        if grep -q "^$option=" "$service_file"; then
            echo "  $option: ✓"
        else
            echo "  $option: ⚠ (recommended)"
        fi
    done
    
    echo ""
    echo "Validation complete"
}

# Service deployment automation
deploy_service() {
    local service_file="$1"
    local enable_service="${2:-yes}"
    local start_service="${3:-no}"
    
    if [[ -z "$service_file" || ! -f "$service_file" ]]; then
        echo "Usage: deploy_service <service_file> [enable:yes/no] [start:yes/no]"
        return 1
    fi
    
    local service_name=$(basename "$service_file")
    
    echo "=== Deploying Service: $service_name ==="
    
    # Validate first
    if ! validate_service "$service_file"; then
        echo "Service validation failed. Aborting deployment."
        return 1
    fi
    
    # Copy to system directory
    echo "Installing service file..."
    if sudo cp "$service_file" "/etc/systemd/system/"; then
        echo "✓ Service file installed"
    else
        echo "✗ Failed to install service file"
        return 1
    fi
    
    # Reload systemd
    echo "Reloading systemd daemon..."
    if sudo systemctl daemon-reload; then
        echo "✓ Systemd daemon reloaded"
    else
        echo "✗ Failed to reload systemd daemon"
        return 1
    fi
    
    # Enable service if requested
    if [[ "$enable_service" == "yes" ]]; then
        echo "Enabling service..."
        if sudo systemctl enable "$service_name"; then
            echo "✓ Service enabled"
        else
            echo "✗ Failed to enable service"
            return 1
        fi
    fi
    
    # Start service if requested
    if [[ "$start_service" == "yes" ]]; then
        echo "Starting service..."
        if sudo systemctl start "$service_name"; then
            echo "✓ Service started"
            
            # Show status
            echo ""
            echo "Service status:"
            systemctl status "$service_name" --no-pager
        else
            echo "✗ Failed to start service"
            echo "Check logs with: journalctl -u $service_name"
            return 1
        fi
    fi
    
    echo ""
    echo "Deployment complete!"
    echo "Useful commands:"
    echo "  systemctl status $service_name"
    echo "  journalctl -u $service_name -f"
    echo "  systemctl enable $service_name"
    echo "  systemctl start $service_name"
}

# Usage
case "${1:-help}" in
    "basic")
        create_basic_service "$2" "$3" "$4" "$5"
        ;;
    "advanced")
        create_advanced_service "$2" "$3" "$4" "$5"
        ;;
    "template")
        create_service_template "$2" "$3"
        ;;
    "validate")
        validate_service "$2"
        ;;
    "deploy")
        deploy_service "$2" "$3" "$4"
        ;;
    "help")
        echo "Usage: $0 {basic|advanced|template|validate|deploy} [arguments]"
        echo ""
        echo "Commands:"
        echo "  basic <name> <exec> [user] [desc]     - Create basic service"
        echo "  advanced <name> <exec> [config] [user] - Create advanced service"
        echo "  template <name> <path>                - Create service template"
        echo "  validate <service_file>               - Validate service file"
        echo "  deploy <service_file> [enable] [start] - Deploy service"
        ;;
esac
```

### Performance Analysis Scripts

#### System Performance Monitor
```bash
#!/bin/bash
# performance-monitor.sh - Comprehensive system and process performance monitoring

# Global configuration
MONITOR_INTERVAL=5
LOG_DIR="/var/log/performance"
ALERT_THRESHOLDS=(
    "cpu:80"
    "memory:85"
    "disk:90"
    "load:4.0"
)

# Initialize monitoring
init_monitoring() {
    echo "Initializing performance monitoring..."
    
    # Create log directory
    sudo mkdir -p "$LOG_DIR"
    sudo chmod 755 "$LOG_DIR"
    
    # Create log files
    local timestamp=$(date +%Y%m%d_%H%M%S)
    export CPU_LOG="$LOG_DIR/cpu_$timestamp.log"
    export MEM_LOG="$LOG_DIR/memory_$timestamp.log"
    export DISK_LOG="$LOG_DIR/disk_$timestamp.log"
    export PROC_LOG="$LOG_DIR/processes_$timestamp.log"
    export ALERT_LOG="$LOG_DIR/alerts_$timestamp.log"
    
    # Initialize log files
    echo "timestamp,user,nice,system,idle,iowait,irq,softirq,steal" > "$CPU_LOG"
    echo "timestamp,total,used,free,shared,buff_cache,available,used_percent" > "$MEM_LOG"
    echo "timestamp,filesystem,size,used,avail,use_percent,mount" > "$DISK_LOG"
    echo "timestamp,pid,user,cpu,mem,vsz,rss,tty,stat,start,time,command" > "$PROC_LOG"
    echo "timestamp,alert_type,value,threshold,message" > "$ALERT_LOG"
    
    echo "Performance monitoring initialized"
    echo "Logs will be written to: $LOG_DIR"
}

# Collect CPU statistics
collect_cpu_stats() {
    local timestamp=$(date +%s)
    
    # Get CPU statistics from /proc/stat
    local cpu_stats=$(awk '/^cpu / {print $2,$3,$4,$5,$6,$7,$8,$9}' /proc/stat)
    echo "$timestamp,$cpu_stats" >> "$CPU_LOG"
    
    # Calculate CPU usage percentage
    local cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | sed 's/%us,//')
    
    # Check CPU threshold
    if (( $(echo "$cpu_usage > 80" | bc -l) )); then
        log_alert "cpu" "$cpu_usage" "80" "High CPU usage detected"
    fi
}

# Collect memory statistics
collect_memory_stats() {
    local timestamp=$(date +%s)
    
    # Get memory information
    local mem_info=$(free -b | grep Mem)
    local total=$(echo "$mem_info" | awk '{print $2}')
    local used=$(echo "$mem_info" | awk '{print $3}')
    local free=$(echo "$mem_info" | awk '{print $4}')
    local shared=$(echo "$mem_info" | awk '{print $5}')
    local buff_cache=$(echo "$mem_info" | awk '{print $6}')
    local available=$(echo "$mem_info" | awk '{print $7}')
    local used_percent=$(echo "scale=2; $used * 100 / $total" | bc)
    
    echo "$timestamp,$total,$used,$free,$shared,$buff_cache,$available,$used_percent" >> "$MEM_LOG"
    
    # Check memory threshold
    if (( $(echo "$used_percent > 85" | bc -l) )); then
        log_alert "memory" "$used_percent" "85" "High memory usage detected"
    fi
}

# Collect disk statistics
collect_disk_stats() {
    local timestamp=$(date +%s)
    
    # Get disk usage for all mounted filesystems
    df -B1 | grep -vE '^Filesystem|tmpfs|cdrom|udev' | while read line; do
        local filesystem=$(echo "$line" | awk '{print $1}')
        local size=$(echo "$line" | awk '{print $2}')
        local used=$(echo "$line" | awk '{print $3}')
        local avail=$(echo "$line" | awk '{print $4}')
        local use_percent=$(echo "$line" | awk '{print $5}' | sed 's/%//')
        local mount=$(echo "$line" | awk '{print $6}')
        
        echo "$timestamp,$filesystem,$size,$used,$avail,$use_percent,$mount" >> "$DISK_LOG"
        
        # Check disk threshold
        if [[ $use_percent -gt 90 ]]; then
            log_alert "disk" "$use_percent" "90" "High disk usage on $mount ($filesystem)"
        fi
    done
}

# Collect process statistics
collect_process_stats() {
    local timestamp=$(date +%s)
    
    # Get top 10 CPU consuming processes
    ps aux --sort=-%cpu | head -11 | tail -10 | while read line; do
        local user=$(echo "$line" | awk '{print $1}')
        local pid=$(echo "$line" | awk '{print $2}')
        local cpu=$(echo "$line" | awk '{print $3}')
        local mem=$(echo "$line" | awk '{print $4}')
        local vsz=$(echo "$line" | awk '{print $5}')
        local rss=$(echo "$line" | awk '{print $6}')
        local tty=$(echo "$line" | awk '{print $7}')
        local stat=$(echo "$line" | awk '{print $8}')
        local start=$(echo "$line" | awk '{print $9}')
        local time=$(echo "$line" | awk '{print $10}')
        local command=$(echo "$line" | awk '{for(i=11;i<=NF;i++) printf "%s ", $i; print ""}' | tr ',' '_')
        
        echo "$timestamp,$pid,$user,$cpu,$mem,$vsz,$rss,$tty,$stat,$start,$time,$command" >> "$PROC_LOG"
    done
}

# Log alert
log_alert() {
    local alert_type="$1"
    local value="$2"
    local threshold="$3"
    local message="$4"
    local timestamp=$(date +%s)
    
    echo "$timestamp,$alert_type,$value,$threshold,$message" >> "$ALERT_LOG"
    
    # Also log to syslog
    logger -t "performance-monitor" "ALERT: $message (value: $value, threshold: $threshold)"
    
    # Display alert if running interactively
    if [[ -t 1 ]]; then
        echo "ALERT [$(date)]: $message (value: $value, threshold: $threshold)"
    fi
}

# Generate performance report
generate_report() {
    local report_file="${1:-/tmp/performance_report_$(date +%Y%m%d_%H%M%S).html}"
    
    echo "Generating performance report: $report_file"
    
    cat > "$report_file" << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>System Performance Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .header { background-color: #f0f0f0; padding: 10px; border-radius: 5px; }
        .section { margin: 20px 0; }
        .alert { background-color: #ffe6e6; padding: 10px; border-left: 5px solid #ff0000; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
        .metric { display: inline-block; margin: 10px; padding: 10px; border: 1px solid #ccc; border-radius: 5px; }
    </style>
</head>
<body>
    <div class="header">
        <h1>System Performance Report</h1>
        <p>Generated: REPORT_TIMESTAMP</p>
        <p>Hostname: HOSTNAME</p>
    </div>
EOF

    # Replace placeholders
    sed -i "s/REPORT_TIMESTAMP/$(date)/" "$report_file"
    sed -i "s/HOSTNAME/$(hostname)/" "$report_file"
    
    # Add system overview
    cat >> "$report_file" << EOF
    <div class="section">
        <h2>System Overview</h2>
        <div class="metric">
            <strong>Uptime:</strong> $(uptime -p)
        </div>
        <div class="metric">
            <strong>Load Average:</strong> $(cat /proc/loadavg | awk '{print $1, $2, $3}')
        </div>
        <div class="metric">
            <strong>CPU Cores:</strong> $(nproc)
        </div>
        <div class="metric">
            <strong>Total Memory:</strong> $(free -h | grep Mem | awk '{print $2}')
        </div>
    </div>
EOF

    # Add alerts if any
    if [[ -f "$ALERT_LOG" && -s "$ALERT_LOG" ]]; then
        echo '    <div class="section">' >> "$report_file"
        echo '        <h2>Alerts</h2>' >> "$report_file"
        
        tail -20 "$ALERT_LOG" | while IFS=',' read timestamp alert_type value threshold message; do
            if [[ "$timestamp" != "timestamp" ]]; then
                local alert_time=$(date -d "@$timestamp" "+%Y-%m-%d %H:%M:%S")
                echo "        <div class=\"alert\">[$alert_time] $message (value: $value, threshold: $threshold)</div>" >> "$report_file"
            fi
        done
        
        echo '    </div>' >> "$report_file"
    fi
    
    # Close HTML
    echo '</body></html>' >> "$report_file"
    
    echo "Report generated: $report_file"
}

# Real-time monitoring dashboard
run_dashboard() {
    local duration="${1:-continuous}"
    
    echo "Starting performance monitoring dashboard..."
    echo "Press Ctrl+C to stop"
    
    # Initialize
    init_monitoring
    
    local start_time=$(date +%s)
    local iteration=0
    
    while true; do
        # Clear screen for dashboard display
        clear
        
        echo "╔══════════════════════════════════════════════════════════════╗"
        echo "║                    PERFORMANCE MONITOR                       ║"
        echo "║                    $(date '+%Y-%m-%d %H:%M:%S')                    ║"
        echo "╚══════════════════════════════════════════════════════════════╝"
        echo ""
        
        # System overview
        echo "=== SYSTEM OVERVIEW ==="
        echo "Hostname: $(hostname)"
        echo "Uptime: $(uptime -p)"
        echo "Load: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
        echo ""
        
        # Current metrics
        echo "=== CURRENT METRICS ==="
        local cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | sed 's/%us,//')
        local mem_usage=$(free | grep Mem | awk '{printf "%.1f", $3/$2 * 100.0}')
        local load1=$(cat /proc/loadavg | awk '{print $1}')
        
        printf "CPU Usage: %6.1f%%  " "$cpu_usage"
        printf "Memory Usage: %6.1f%%  " "$mem_usage"
        printf "Load (1m): %6.2f\n" "$load1"
        echo ""
        
        # Top processes
        echo "=== TOP PROCESSES (CPU) ==="
        ps aux --sort=-%cpu | head -6 | tail -5 | awk '{printf "%-8s %6s %6.1f%% %6.1f%% %.30s\n", $1, $2, $3, $4, $11}'
        echo ""
        
        # Collect stats
        collect_cpu_stats
        collect_memory_stats
        collect_disk_stats
        collect_process_stats
        
        # Check if duration is reached
        if [[ "$duration" != "continuous" ]]; then
            local current_time=$(date +%s)
            local elapsed=$((current_time - start_time))
            
            if [[ $elapsed -ge $duration ]]; then
                echo "Monitoring duration reached: ${duration}s"
                break
            fi
            
            echo "Elapsed: ${elapsed}s / ${duration}s"
        fi
        
        ((iteration++))
        echo "Iteration: $iteration"
        
        sleep "$MONITOR_INTERVAL"
    done
    
    echo ""
    echo "Monitoring stopped. Generating report..."
    generate_report
}

# Batch monitoring (non-interactive)
run_batch_monitoring() {
    local duration="${1:-3600}"  # 1 hour default
    local interval="${2:-$MONITOR_INTERVAL}"
    
    echo "Starting batch performance monitoring..."
    echo "Duration: ${duration}s, Interval: ${interval}s"
    
    init_monitoring
    
    local start_time=$(date +%s)
    local end_time=$((start_time + duration))
    
    while [[ $(date +%s) -lt $end_time ]]; do
        collect_cpu_stats
        collect_memory_stats
        collect_disk_stats
        collect_process_stats
        
        sleep "$interval"
    done
    
    echo "Batch monitoring completed"
    generate_report
}

# Usage
case "${1:-help}" in
    "dashboard")
        run_dashboard "$2"
        ;;
    "batch")
        run_batch_monitoring "$2" "$3"
        ;;
    "report")
        generate_report "$2"
        ;;
    "init")
        init_monitoring
        ;;
    "help")
        echo "Usage: $0 {dashboard|batch|report|init} [arguments]"
        echo ""
        echo "Commands:"
        echo "  dashboard [duration]       - Run interactive dashboard"
        echo "  batch [duration] [interval] - Run batch monitoring"
        echo "  report [output_file]       - Generate HTML report"
        echo "  init                       - Initialize monitoring"
        ;;
esac
```

## Lab Exercises

### Lab 1: Process Monitoring and Management
**Objective:** Master advanced process monitoring, analysis, and control techniques.

**Tasks:**
1. Implement comprehensive process monitoring scripts using `ps`, `top`, and `/proc` filesystem
2. Create automated detection systems for problematic processes (high CPU, memory leaks, zombies)
3. Develop graceful process termination procedures with fallback mechanisms
4. Build process performance analysis tools with trend tracking
5. Implement automated process recovery and alerting systems

**Deliverables:**
- Process monitoring dashboard with real-time metrics
- Automated problem detection and alert system
- Process performance analysis reports
- Graceful termination and recovery procedures

### Lab 2: Systemd Service Configuration
**Objective:** Configure and optimize systemd services for production environments.

**Tasks:**
1. Analyze existing services for performance and security improvements
2. Configure service dependencies, ordering, and conflict resolution
3. Implement advanced logging and monitoring for critical services
4. Optimize service startup times and resource utilization
5. Create service health checking and automatic recovery mechanisms

**Deliverables:**
- Service optimization report with before/after metrics
- Advanced service configuration templates
- Health monitoring and recovery automation
- Service dependency mapping and optimization

### Lab 3: Custom Service Development
**Objective:** Design and deploy custom systemd services with enterprise-grade features.

**Tasks:**
1. Create custom services with comprehensive security hardening
2. Implement socket activation and on-demand service startup
3. Design service templates for multi-instance deployments
4. Configure resource limits and performance optimization
5. Develop automated testing and validation procedures

**Deliverables:**
- Custom service implementations with security features
- Socket activation and template configurations
- Automated deployment and testing frameworks
- Performance optimization and resource management

### Lab 4: Performance Analysis and Optimization
**Objective:** Implement comprehensive system performance monitoring and optimization.

**Tasks:**
1. Deploy system-wide performance monitoring with alerting
2. Analyze process and service performance bottlenecks
3. Implement automated performance tuning recommendations
4. Create capacity planning and trend analysis reports
5. Design automated remediation for common performance issues

**Deliverables:**
- Performance monitoring dashboard with alerting
- Bottleneck analysis and optimization recommendations
- Automated tuning and remediation systems
- Capacity planning and trend analysis reports

## Best Practices Summary

### Process Management Best Practices

| Practice | Implementation | Benefits |
|----------|----------------|----------|
| **Graceful Termination** | Always try SIGTERM before SIGKILL | Prevents data corruption and resource leaks |
| **Resource Monitoring** | Regular monitoring of CPU, memory, I/O | Early detection of performance issues |
| **Process Isolation** | Use proper user accounts and permissions | Enhanced security and stability |
| **Automated Recovery** | Implement monitoring and restart mechanisms | Improved system reliability |
| **Documentation** | Document process dependencies and requirements | Easier troubleshooting and maintenance |

### Systemd Service Best Practices

1. **Security Hardening**
   - Use `NoNewPrivileges=true`
   - Implement filesystem restrictions (`ProtectSystem`, `PrivateTmp`)
   - Set resource limits (`MemoryMax`, `CPUQuota`)
   - Use minimal user privileges

2. **Reliability Configuration**
   - Configure appropriate restart policies
   - Set reasonable timeout values
   - Implement proper dependency management
   - Use health checking mechanisms

3. **Performance Optimization**
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

## Troubleshooting Guide

### Common Process Issues

#### High CPU Usage
```bash
# Identify high CPU processes
ps aux --sort=-%cpu | head -10

# Monitor process CPU usage over time
pidstat -u -p PID 1 10

# Check process threads
ps -T -p PID

# Analyze with profiling tools
perf top -p PID
strace -p PID -c
```

#### Memory Leaks
```bash
# Monitor memory usage
ps -p PID -o pid,ppid,%mem,vsz,rss,etime

# Check memory maps
cat /proc/PID/maps
cat /proc/PID/smaps

# Monitor over time
watch -n 1 'ps -p PID -o pid,%mem,vsz,rss'

# Use memory debugging tools
valgrind --tool=memcheck --leak-check=full program
```

#### Zombie Processes
```bash
# Find zombie processes
ps aux | awk '$8 ~ /^Z/ { print $2, $3, $11 }'

# Check parent process
ps -o pid,ppid,stat,comm -p ZOMBIE_PID

# Kill parent to clean zombies
kill -TERM PARENT_PID
```

### Systemd Service Issues

#### Service Won't Start
```bash
# Check service status
systemctl status service-name.service

# Check logs
journalctl -u service-name.service -n 50

# Check dependencies
systemctl list-dependencies service-name.service

# Verify unit file
systemd-analyze verify /etc/systemd/system/service-name.service

# Check file permissions
ls -la /etc/systemd/system/service-name.service
```

#### Service Keeps Restarting
```bash
# Check restart configuration
systemctl show service-name.service | grep Restart

# Monitor restart events
journalctl -u service-name.service -f

# Check resource limits
systemctl show service-name.service | grep -E "(Memory|CPU|Limit)"

# Analyze exit codes
journalctl -u service-name.service | grep "code=exited"
```

### Performance Issues

#### System Slow Response
```bash
# Check system load
uptime
cat /proc/loadavg

# Identify resource bottlenecks
iostat -x 1 5
sar -u 1 5
free -m

# Find blocking processes
ps aux | awk '$8 ~ /^D/ { print $2, $11 }'

# Check disk I/O
iotop -o
```

#### Service Performance Problems
```bash
# Monitor service resource usage
systemd-cgtop

# Check service limits
systemctl show service-name.service | grep -E "(CPU|Memory|IO)"

# Analyze service performance
journalctl -u service-name.service --since "1 hour ago" | grep -i "slow\|timeout\|error"

# Profile service execution
perf record -p PID sleep 10
perf report
```

## Assessment Criteria

Students will be evaluated on their ability to:

| Criteria | Proficient (4) | Developing (3) | Beginning (2) | Inadequate (1) |
|----------|----------------|----------------|---------------|----------------|
| **Process Analysis** | Expertly analyzes complex process hierarchies and resource usage patterns | Good process analysis with minor gaps | Basic process monitoring capabilities | Limited understanding of process concepts |
| **Service Management** | Masters advanced systemd configurations with security and performance optimization | Good systemd skills with functional services | Basic service management operations | Struggles with basic service concepts |
| **Troubleshooting** | Efficiently diagnoses and resolves complex process and service issues | Good problem-solving with systematic approach | Basic troubleshooting with guidance | Poor diagnostic and resolution skills |
| **Automation** | Creates sophisticated monitoring and automation solutions | Good automation with functional scripts | Basic automation capabilities | Manual operations only |

## Next Steps

After mastering processes and services, proceed to:

- **Module 6: Users, Groups & Authentication** - Apply process knowledge to user session management and authentication services
- **Module 8: Logging and Monitoring** - Integrate process monitoring with comprehensive system logging strategies
- **Module 14: Proxmox Infrastructure Automation** - Use service management skills for virtualized infrastructure automation

The process and service management expertise developed in this module is fundamental to maintaining stable, secure, and high-performance Linux systems in enterprise environments.

## Practical Examples

### Process Management and Monitoring

#### Advanced Process Analysis Scripts
```bash
#!/bin/bash
# process-analyzer.sh - Comprehensive process analysis and monitoring

# System-wide process analysis
analyze_system_processes() {
    echo "=== System Process Analysis ==="
    echo "Generated: $(date)"
    echo ""
    
    # Overall system statistics
    echo "=== System Overview ==="
    echo "Total processes: $(ps aux | wc -l)"
    echo "Running processes: $(ps aux | awk '$8 ~ /^R/ {count++} END {print count+0}')"
    echo "Sleeping processes: $(ps aux | awk '$8 ~ /^S/ {count++} END {print count+0}')"
    echo "Zombie processes: $(ps aux | awk '$8 ~ /^Z/ {count++} END {print count+0}')"
    echo "System load: $(uptime | awk -F'load average:' '{print $2}')"
    echo "Memory usage: $(free -h | grep Mem | awk '{print $3"/"$2" ("$3/$2*100"%)"}')"
    echo ""
    
    # Top CPU consumers
    echo "=== Top 10 CPU Consumers ==="
    ps aux --sort=-%cpu | head -11 | tail -10 | awk '{printf "%-8s %-6s %-6.1f%% %-6.1f%% %s\n", $1, $2, $3, $4, $11}'
    echo ""
    
    # Top memory consumers
    echo "=== Top 10 Memory Consumers ==="
    ps aux --sort=-%mem | head -11 | tail -10 | awk '{printf "%-8s %-6s %-6.1f%% %-6.1f%% %s\n", $1, $2, $3, $4, $11}'
    echo ""
    
    # Long-running processes
    echo "=== Long-Running Processes (>1 day) ==="
    ps -eo pid,ppid,user,etime,cmd --sort=-etime | awk 'NR==1 || $4 ~ /-/ {print}'
    echo ""
    
    # Network-connected processes
    echo "=== Network-Connected Processes ==="
    ss -tulpn | grep LISTEN | awk '{print $5, $7}' | sort -u
    echo ""
}

# Monitor specific process performance
monitor_process() {
    local pid="$1"
    local duration="${2:-60}"
    local interval="${3:-1}"
    
    if [[ -z "$pid" ]]; then
        echo "Usage: monitor_process <PID> [duration] [interval]"
        return 1
    fi
    
    echo "=== Monitoring Process $pid for $duration seconds ==="
    
    # Process information
    if [[ -d "/proc/$pid" ]]; then
        echo "Process: $(cat /proc/$pid/comm 2>/dev/null)"
        echo "Command: $(cat /proc/$pid/cmdline 2>/dev/null | tr '\0' ' ')"
        echo "Parent PID: $(awk '/PPid:/ {print $2}' /proc/$pid/status 2>/dev/null)"
        echo "Start time: $(ps -o lstart= -p $pid 2>/dev/null)"
        echo ""
    else
        echo "Process $pid not found"
        return 1
    fi
    
    # Monitor resource usage
    local end_time=$(($(date +%s) + duration))
    
    echo "Time     CPU%   MEM%   VSZ(MB)  RSS(MB)  Threads  FDs"
    echo "========================================================"
    
    while [[ $(date +%s) -lt $end_time ]]; do
        if [[ -d "/proc/$pid" ]]; then
            local stats=$(ps -p "$pid" -o %cpu,%mem,vsz,rss,nlwp --no-headers 2>/dev/null)
            local fd_count=$(ls /proc/$pid/fd 2>/dev/null | wc -l)
            
            if [[ -n "$stats" ]]; then
                local cpu=$(echo "$stats" | awk '{print $1}')
                local mem=$(echo "$stats" | awk '{print $2}')
                local vsz=$(echo "$stats" | awk '{printf "%.1f", $3/1024}')
                local rss=$(echo "$stats" | awk '{printf "%.1f", $4/1024}')
                local threads=$(echo "$stats" | awk '{print $5}')
                
                printf "%-8s %-6s %-6s %-8s %-8s %-8s %s\n" \
                    "$(date +%H:%M:%S)" "$cpu" "$mem" "$vsz" "$rss" "$threads" "$fd_count"
            fi
        else
            echo "Process $pid terminated"
            break
        fi
        
        sleep "$interval"
    done
}

# Find problematic processes
find_problematic_processes() {
    echo "=== Problematic Process Detection ==="
    
    # High CPU usage processes
    echo "High CPU Usage (>80%):"
    ps aux | awk '$3 > 80 {printf "PID: %-6s User: %-8s CPU: %-6s%% Command: %s\n", $2, $1, $3, $11}'
    echo ""
    
    # High memory usage processes
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
