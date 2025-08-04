# Module 8: Logging and Monitoring

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics Covered](#topics-covered)
  - [8.1 System Logging Architecture](#81-system-logging-architecture)
  - [8.2 Log Management and Rotation](#82-log-management-and-rotation)
  - [8.3 System Resource Monitoring](#83-system-resource-monitoring)
  - [8.4 Performance Metrics and Analysis](#84-performance-metrics-and-analysis)
  - [8.5 Centralized Logging Solutions](#85-centralized-logging-solutions)
  - [8.6 Monitoring Infrastructure and Alerting](#86-monitoring-infrastructure-and-alerting)
  - [8.7 Security and Audit Logging](#87-security-and-audit-logging)
  - [8.8 Enterprise Monitoring and Observability](#88-enterprise-monitoring-and-observability)
- [Essential Command Reference](#essential-command-reference)
- [Practical Examples](#practical-examples)
  - [System Logging Configuration](#system-logging-configuration)
  - [Log Analysis and Processing](#log-analysis-and-processing)
  - [Performance Monitoring Tools](#performance-monitoring-tools)
  - [Centralized Logging Implementation](#centralized-logging-implementation)
  - [Monitoring Infrastructure Deployment](#monitoring-infrastructure-deployment)
  - [Alerting and Notification Systems](#alerting-and-notification-systems)
  - [Security Monitoring and SIEM](#security-monitoring-and-siem)
  - [Custom Monitoring Solutions](#custom-monitoring-solutions)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Log Management and Analysis](#lab-1-log-management-and-analysis)
  - [Lab 2: Performance Monitoring Implementation](#lab-2-performance-monitoring-implementation)
  - [Lab 3: Centralized Logging Infrastructure](#lab-3-centralized-logging-infrastructure)
  - [Lab 4: Monitoring and Alerting Systems](#lab-4-monitoring-and-alerting-systems)
  - [Lab 5: Security Monitoring and Incident Response](#lab-5-security-monitoring-and-incident-response)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Assessment Criteria](#assessment-criteria)
- [Next Steps](#next-steps)


## Overview
[⬆️ Back to Top](#table-of-contents)

This module provides comprehensive coverage of Linux logging and monitoring systems, from basic log management to enterprise-grade observability platforms. Students will master log analysis, implement performance monitoring, deploy centralized logging solutions, and create comprehensive monitoring infrastructure for production environments.

**Module Focus Areas:**
- Advanced system logging with rsyslog, journald, and syslog-ng
- Log rotation, retention policies, and automated management
- Real-time performance monitoring and resource analysis
- Centralized logging architectures (ELK Stack, Fluentd, Graylog)
- Monitoring infrastructure with Prometheus, Grafana, and alerting systems
- Security event monitoring and SIEM integration
- Custom monitoring solutions and automation
- Enterprise observability and incident response workflows


## Learning Objectives
[⬆️ Back to Top](#table-of-contents)

By the end of this module, you will be able to:

1. **Master System Logging**: Configure and manage advanced logging systems with rsyslog, journald, and centralized solutions
2. **Implement Log Management**: Design log rotation policies, retention strategies, and automated log processing workflows
3. **Deploy Performance Monitoring**: Configure comprehensive system monitoring with real-time alerting and analysis
4. **Build Monitoring Infrastructure**: Deploy Prometheus, Grafana, and associated tools for enterprise monitoring
5. **Create Centralized Logging**: Implement ELK Stack or similar solutions for log aggregation and analysis
6. **Design Alerting Systems**: Configure intelligent alerting with escalation policies and notification systems
7. **Implement Security Monitoring**: Deploy security event monitoring, audit logging, and SIEM integration
8. **Automate Monitoring Tasks**: Create custom monitoring solutions and automated incident response workflows


## Topics Covered
[⬆️ Back to Top](#table-of-contents)

### 8.1 System Logging Architecture
- Modern logging architectures and design patterns
- rsyslog advanced configuration and filtering
- systemd journal (journald) configuration and optimization
- Syslog protocol standards and facilities/priorities
- Log format standardization and structured logging
- High-availability logging and failover mechanisms

### 8.2 Log Management and Rotation
- Comprehensive log rotation with logrotate
- Log retention policies and compliance requirements
- Log compression and archival strategies
- Automated log processing and parsing
- Log shipping and forwarding mechanisms
- Performance optimization for high-volume logging

### 8.3 System Resource Monitoring
- Real-time system performance monitoring
- CPU, memory, disk, and network analysis
- Process and service monitoring
- Resource utilization trending and capacity planning
- Performance bottleneck identification
- System health checks and automated diagnostics

### 8.4 Performance Metrics and Analysis
- Metrics collection and aggregation strategies
- Time-series databases and data retention
- Performance baseline establishment
- Anomaly detection and alerting
- Capacity planning and trend analysis
- Performance optimization recommendations

### 8.5 Centralized Logging Solutions
- ELK Stack (Elasticsearch, Logstash, Kibana) deployment
- Fluentd and Fluent Bit for log collection
- Graylog and other centralized logging platforms
- Log parsing, enrichment, and correlation
- Search and analysis capabilities
- Log-based alerting and monitoring

### 8.6 Monitoring Infrastructure and Alerting
- Prometheus and Grafana ecosystem deployment
- Time-series metrics collection and storage
- Dashboard creation and visualization
- Alerting rules and notification systems
- Service discovery and dynamic configuration
- High-availability monitoring architectures

### 8.7 Security and Audit Logging
- Security event monitoring and correlation
- Audit trail management and compliance
- Intrusion detection and response
- Log-based security analysis
- SIEM integration and threat intelligence
- Incident response and forensic analysis

### 8.8 Enterprise Monitoring and Observability
- Application performance monitoring (APM)
- Distributed tracing and microservices monitoring
- Infrastructure as Code for monitoring
- Monitoring automation and self-healing systems
- Business metrics and SLA monitoring
- Multi-cloud and hybrid monitoring strategies
- Log file locations and naming conventions
- Security and audit logging considerations

**🔗 Practical Examples**: [Basic rsyslog Configuration](#basic-rsyslog-configuration) | [Log File Analysis](#log-analysis-tools)

### 8.2 rsyslog Configuration
- rsyslog.conf structure and advanced syntax
- Filtering, routing, and forwarding logs
- Remote logging setup and secure transport
- Custom log formats and templates
- Performance tuning and troubleshooting

**🔗 Practical Examples**: [Advanced rsyslog Configuration](#advanced-rsyslog-configuration) | [Remote Logging Setup](#remote-logging-configuration)

### 8.3 systemd Journal (journald)
- Journal storage mechanisms and configuration options
- Advanced querying with journalctl filters and options
- Persistent vs volatile storage management
- Journal forwarding to traditional syslog
- Journal maintenance and integrity verification

**🔗 Practical Examples**: [journald Configuration](#journald-configuration) | [journalctl Usage Examples](#journalctl-usage-examples)

### 8.4 Log Rotation and Management
- logrotate configuration files in `/etc/logrotate.d/`
- Rotation policies: size, time, and retention strategies
- Compression and archival strategies
- Custom post-rotation scripts and hooks
- Automated log cleanup and maintenance

**🔗 Practical Examples**: [Log Rotation Configuration](#log-rotation-configuration) | [Custom Rotation Scripts](#custom-log-management)

### 8.5 Resource Monitoring Fundamentals
- Core monitoring tools: `top`/`htop`, `vmstat`, `iostat`, `free`, `df`, `du`
- CPU, memory, disk, and network performance metrics
- Process and service monitoring techniques
- Real-time monitoring and historical analysis
- Performance baseline establishment

**🔗 Practical Examples**: [Performance Monitoring Commands](#performance-monitoring-commands) | [System Resource Scripts](#system-resource-scripts)

### 8.6 Prometheus and Node Exporter
- Prometheus architecture and data model
- Installing and configuring `node_exporter` for host metrics
- Prometheus configuration and service discovery
- Custom exporters and metric creation
- Time-series data collection and storage

**🔗 Practical Examples**: [Prometheus Configuration](#prometheus-configuration) | [Node Exporter Setup](#node-exporter-deployment)

### 8.7 Grafana Visualization
- Grafana installation and initial configuration
- Creating dashboards for CPU, memory, disk, and network metrics
- Alert rules and notification channels
- Data source integration and query optimization
- Dashboard sharing and template management

**🔗 Practical Examples**: [Grafana Dashboard Configuration](#grafana-dashboard-configuration) | [Alert Setup](#grafana-alerting)

### 8.8 Centralized Logging Solutions
- ELK stack (Elasticsearch, Logstash, Kibana) architecture
- Fluentd and Graylog alternatives
- Secure log forwarding over TLS
- Log aggregation and correlation strategies
- Scalability and high availability considerations

**🔗 Practical Examples**: [ELK Stack Setup](#elk-stack-configuration) | [Secure Log Forwarding](#secure-log-transport)


## Essential Command Reference
[⬆️ Back to Top](#table-of-contents)

### Log Management Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `journalctl` | Query systemd journal | `journalctl -u service -f --since "2 hours ago"` |
| `logger` | Send messages to syslog | `logger -p local0.info "Custom log message"` |
| `logrotate` | Rotate and compress logs | `logrotate -d /etc/logrotate.conf` |
| `rsyslog` | System logging daemon | `systemctl status rsyslog` |
| `tail` | Monitor log files in real-time | `tail -f /var/log/syslog` |

### System Monitoring Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `top` / `htop` | Process monitoring | `htop -u username` |
| `vmstat` | Virtual memory statistics | `vmstat 1 5` |
| `iostat` | I/O statistics | `iostat -x 1` |
| `sar` | System activity reporter | `sar -u 1 10` |
| `netstat` / `ss` | Network connections | `ss -tuln` |
| `lsof` | List open files | `lsof -i :80` |
| `iotop` | I/O usage by process | `iotop -o` |
| `nload` | Network interface monitoring | `nload eth0` |

### Performance Analysis Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `perf` | Performance analysis | `perf top` |
| `strace` | System call tracing | `strace -p PID` |
| `tcpdump` | Network packet analysis | `tcpdump -i eth0 port 80` |
| `dstat` | Versatile system statistics | `dstat -cdngy` |
| `atop` | Advanced system monitor | `atop -R` |

### Log Analysis Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `grep` | Pattern searching | `grep "ERROR" /var/log/syslog` |
| `awk` | Text processing | `awk '/ERROR/ {print $1, $3}' logfile` |
| `sed` | Stream editor | `sed -n '100,200p' logfile` |
| `sort` | Sort log entries | `sort -k1,1 -k2,2n logfile` |
| `uniq` | Remove duplicates | `uniq -c` |
| `cut` | Extract fields | `cut -d' ' -f1,4 logfile` |

### Monitoring Infrastructure Commands
| Command | Purpose | Common Usage |
|---------|---------|--------------|
| `prometheus` | Metrics server | `./prometheus --config.file=prometheus.yml` |
| `node_exporter` | System metrics exporter | `./node_exporter --web.listen-address=:9100` |
| `grafana-server` | Visualization platform | `systemctl start grafana-server` |
| `alertmanager` | Alert handling | `./alertmanager --config.file=alertmanager.yml` |


## Practical Examples
[⬆️ Back to Top](#table-of-contents)

### System Logging Configuration
[Related Commands/Topics: ](#log-management-commands)Log Management Commands 🟢

#### Advanced rsyslog Configuration
```bash
#!/bin/bash
# Advanced rsyslog configuration for enterprise environments

# Create comprehensive rsyslog configuration
create_rsyslog_config() {
    cat > /etc/rsyslog.d/99-custom.conf << 'EOF'
# Custom rsyslog configuration for enterprise logging

# Load modules
module(load="imudp")
module(load="imtcp")
module(load="omfwd")
module(load="omrelp")

# UDP syslog reception
input(type="imudp" port="514")

# TCP syslog reception
input(type="imtcp" port="514")

# Custom log formats
template(name="CustomFormat" type="string"
         string="%timestamp:::date-rfc3339% %hostname% %syslogtag% %msg%\n")

template(name="JSONFormat" type="string"
         string="{\"timestamp\":\"%timestamp:::date-rfc3339%\",\"hostname\":\"%hostname%\",\"tag\":\"%syslogtag%\",\"message\":\"%msg%\"}\n")

# Application-specific logging
if $programname == 'nginx' then {
    action(type="omfile" file="/var/log/nginx/nginx-syslog.log" template="CustomFormat")
    stop
}

if $programname == 'mysql' then {
    action(type="omfile" file="/var/log/mysql/mysql-syslog.log" template="CustomFormat")
    stop
}

# Security event logging
if $syslogfacility-text == 'authpriv' then {
    action(type="omfile" file="/var/log/security/auth.log" template="JSONFormat")
    # Forward to central SIEM
    action(type="omfwd" target="siem.company.com" port="514" protocol="tcp")
}

# High-priority alerts
if $syslogseverity <= 3 then {
    action(type="omfwd" target="logserver.company.com" port="514" protocol="tcp")
}

# Rate limiting
$SystemLogRateLimitInterval 2
$SystemLogRateLimitBurst 50
EOF

    # Restart rsyslog service
    systemctl restart rsyslog
    systemctl enable rsyslog
}

# Configure log directories with proper permissions
setup_log_directories() {
    local directories=(
        "/var/log/nginx"
        "/var/log/mysql"
        "/var/log/security"
        "/var/log/applications"
        "/var/log/monitoring"
    )
    
    for dir in "${directories[@]}"; do
        mkdir -p "$dir"
        chown syslog:adm "$dir"
        chmod 755 "$dir"
    done
}

# Implement structured logging for applications
configure_structured_logging() {
    # Create rsyslog configuration for JSON logging
    cat > /etc/rsyslog.d/50-json-logs.conf << 'EOF'
# JSON structured logging configuration

template(name="JSONTemplate" type="string"
         string="{\"@timestamp\":\"%timestamp:::date-rfc3339%\",\"host\":\"%hostname%\",\"severity\":\"%syslogseverity-text%\",\"facility\":\"%syslogfacility-text%\",\"tag\":\"%syslogtag%\",\"message\":\"%msg%\"}\n")

# Route JSON logs to separate files
*.* action(type="omfile" file="/var/log/structured/json.log" template="JSONTemplate")
EOF

    mkdir -p /var/log/structured
    chown syslog:adm /var/log/structured
    chmod 755 /var/log/structured
    
    systemctl restart rsyslog
}

# Log shipping configuration
configure_log_shipping() {
    cat > /etc/rsyslog.d/60-log-shipping.conf << 'EOF'
# Secure log forwarding with TLS

# Load required modules
module(load="omfwd")

# Define action for secure forwarding
action(type="omfwd"
       target="central-log-server.company.com"
       port="6514"
       protocol="tcp"
       StreamDriver="gtls"
       StreamDriverMode="1"
       StreamDriverAuthMode="x509/name"
       StreamDriverPermittedPeers="central-log-server.company.com"
       queue.filename="fwdRule1"
       queue.maxdiskspace="1g"
       queue.saveonshutdown="on"
       queue.type="LinkedList"
       action.resumeRetryCount="-1")
EOF
}

# Execute configuration functions
create_rsyslog_config
setup_log_directories
configure_structured_logging
configure_log_shipping

echo "Advanced rsyslog configuration completed successfully"
```

#### systemd Journal Configuration and Optimization
```bash
#!/bin/bash
# systemd journal configuration and optimization

# Configure journald for enterprise environments
configure_journald() {
    # Backup original configuration
    cp /etc/systemd/journald.conf /etc/systemd/journald.conf.backup
    
    # Create optimized journald configuration
    cat > /etc/systemd/journald.conf << 'EOF'
[Journal]
# Storage configuration
Storage=persistent
Compress=yes
Seal=yes

# Size limits
SystemMaxUse=2G
SystemKeepFree=500M
SystemMaxFileSize=128M
SystemMaxFiles=100

# Runtime journal settings
RuntimeMaxUse=200M
RuntimeKeepFree=100M
RuntimeMaxFileSize=32M
RuntimeMaxFiles=10

# Forward to syslog
ForwardToSyslog=yes
ForwardToKMsg=no
ForwardToConsole=no
ForwardToWall=yes

# Rate limiting
RateLimitInterval=30s
RateLimitBurst=10000

# Maximum retention
MaxRetentionSec=30day
MaxFileSec=1day

# Sync settings
SyncIntervalSec=5m
EOF

    # Restart journald
    systemctl restart systemd-journald
    
    # Verify configuration
    journalctl --verify
}

# Journal maintenance and optimization
optimize_journal() {
    # Vacuum old journals
    journalctl --vacuum-time=30d
    journalctl --vacuum-size=1G
    
    # Verify journal integrity
    journalctl --verify
    
    # Display journal disk usage
    journalctl --disk-usage
}

# Create journal analysis scripts
create_journal_analysis() {
    cat > /usr/local/bin/journal-analysis.sh << 'EOF'
#!/bin/bash
# Journal analysis and reporting script

# Function to analyze boot times
analyze_boot_times() {
    echo "=== Boot Time Analysis ==="
    systemd-analyze
    echo
    systemd-analyze blame | head -20
    echo
}

# Function to analyze critical errors
analyze_critical_errors() {
    echo "=== Critical Errors (Last 24 Hours) ==="
    journalctl --since "24 hours ago" --priority=0..3 --no-pager
    echo
}

# Function to analyze service failures
analyze_service_failures() {
    echo "=== Failed Services ==="
    systemctl --failed --no-pager
    echo
    
    echo "=== Service Restart Analysis ==="
    journalctl --since "24 hours ago" -u "*.service" --grep="started|stopped|failed" --no-pager
    echo
}

# Function to analyze security events
analyze_security_events() {
    echo "=== Security Events (Last 24 Hours) ==="
    journalctl --since "24 hours ago" _TRANSPORT=audit --no-pager
    echo
    
    echo "=== Authentication Events ==="
    journalctl --since "24 hours ago" -u ssh.service -u systemd-logind.service --no-pager
    echo
}

# Function to generate system health report
generate_health_report() {
    local report_file="/var/log/system-health-$(date +%Y%m%d_%H%M%S).report"
    
    {
        echo "System Health Report - $(date)"
        echo "================================"
        analyze_boot_times
        analyze_critical_errors
        analyze_service_failures
        analyze_security_events
    } > "$report_file"
    
    echo "Health report generated: $report_file"
}

# Main execution
case "${1:-health}" in
    boot)
        analyze_boot_times
        ;;
    errors)
        analyze_critical_errors
        ;;
    services)
        analyze_service_failures
        ;;
    security)
        analyze_security_events
        ;;
    health|*)
        generate_health_report
        ;;
esac
EOF

    chmod +x /usr/local/bin/journal-analysis.sh
}

# Execute configuration
configure_journald
optimize_journal
create_journal_analysis

echo "systemd journal configuration completed"
```
### Log Analysis and Processing
[Related Commands/Topics: ](#log-analysis-commands)Log Analysis Commands 🟢

#### Advanced Log Analysis Toolkit
```bash
#!/bin/bash
# Comprehensive log analysis and processing toolkit

# Function to analyze Apache/Nginx access logs
analyze_web_logs() {
    local logfile="$1"
    local output_dir="/tmp/log-analysis-$(date +%Y%m%d)"
    
    mkdir -p "$output_dir"
    
    echo "Analyzing web server logs: $logfile"
    
    # Top IP addresses
    echo "=== Top 20 IP Addresses ===" > "$output_dir/top_ips.txt"
    awk '{print $1}' "$logfile" | sort | uniq -c | sort -nr | head -20 >> "$output_dir/top_ips.txt"
    
    # Top requested URLs
    echo "=== Top 20 Requested URLs ===" > "$output_dir/top_urls.txt"
    awk '{print $7}' "$logfile" | sort | uniq -c | sort -nr | head -20 >> "$output_dir/top_urls.txt"
    
    # HTTP status code distribution
    echo "=== HTTP Status Code Distribution ===" > "$output_dir/status_codes.txt"
    awk '{print $9}' "$logfile" | sort | uniq -c | sort -nr >> "$output_dir/status_codes.txt"
    
    # Error analysis (4xx and 5xx responses)
    echo "=== Error Analysis ===" > "$output_dir/errors.txt"
    awk '$9 ~ /^[45]/ {print $0}' "$logfile" > "$output_dir/error_lines.txt"
    awk '$9 ~ /^[45]/ {print $9}' "$logfile" | sort | uniq -c | sort -nr >> "$output_dir/errors.txt"
    
    # Bandwidth analysis
    echo "=== Bandwidth Analysis ===" > "$output_dir/bandwidth.txt"
    awk '{sum += $10} END {print "Total bytes transferred:", sum; print "Average per request:", sum/NR}' "$logfile" >> "$output_dir/bandwidth.txt"
    
    # Time-based analysis
    echo "=== Hourly Request Distribution ===" > "$output_dir/hourly_stats.txt"
    awk '{print substr($4, 14, 2)}' "$logfile" | sort | uniq -c | sort -k2n >> "$output_dir/hourly_stats.txt"
    
    echo "Analysis complete. Results saved in: $output_dir"
}

# Function to analyze system logs for security events
analyze_security_logs() {
    local timeframe="${1:-24 hours ago}"
    local output_file="/tmp/security-analysis-$(date +%Y%m%d_%H%M%S).txt"
    
    {
        echo "Security Log Analysis - $(date)"
        echo "Timeframe: Since $timeframe"
        echo "======================================="
        
        echo -e "\n=== Failed SSH Login Attempts ==="
        journalctl --since "$timeframe" | grep -i "failed password\|authentication failure" | 
        awk '{for(i=1;i<=NF;i++) if($i~/from/) print $(i+1)}' | sort | uniq -c | sort -nr | head -10
        
        echo -e "\n=== Successful SSH Logins ==="
        journalctl --since "$timeframe" | grep -i "accepted password\|accepted publickey" |
        awk '{for(i=1;i<=NF;i++) if($i~/from/) print $(i+1)}' | sort | uniq -c | sort -nr
        
        echo -e "\n=== Sudo Command Usage ==="
        journalctl --since "$timeframe" | grep -i "sudo.*command" | head -20
        
        echo -e "\n=== Service Start/Stop Events ==="
        journalctl --since "$timeframe" | grep -E "(started|stopped|failed)" | 
        grep -v "session\|slice" | head -20
        
        echo -e "\n=== Unusual Process Activity ==="
        journalctl --since "$timeframe" | grep -E "(killed|segfault|core dump)" | head -10
        
        echo -e "\n=== Network Connection Anomalies ==="
        ss -tuln | awk 'NR>1 {print $1, $5}' | sort | uniq -c | sort -nr | head -10
        
    } > "$output_file"
    
    echo "Security analysis completed: $output_file"
    
    # Generate alerts for critical events
    local critical_events=$(journalctl --since "$timeframe" --priority=0..2 | wc -l)
    if [ "$critical_events" -gt 0 ]; then
        echo "WARNING: $critical_events critical events found in the specified timeframe"
    fi
}

# Function for real-time log monitoring with alerts
real_time_log_monitor() {
    local logfile="${1:-/var/log/syslog}"
    local alert_patterns=(
        "ERROR"
        "CRITICAL"
        "Failed password"
        "authentication failure"
        "segfault"
        "Out of memory"
    )
    
    echo "Starting real-time monitoring of: $logfile"
    echo "Alert patterns: ${alert_patterns[*]}"
    echo "Press Ctrl+C to stop"
    
    tail -f "$logfile" | while read line; do
        for pattern in "${alert_patterns[@]}"; do
            if echo "$line" | grep -qi "$pattern"; then
                echo "ALERT [$(date)]: $line"
                # Optional: Send notification
                # echo "$line" | mail -s "Log Alert: $pattern" admin@example.com
                break
            fi
        done
    done
}

# Function to generate comprehensive log report
generate_log_report() {
    local report_file="/var/log/reports/daily-log-report-$(date +%Y%m%d).html"
    
    mkdir -p "$(dirname "$report_file")"
    
    cat > "$report_file" << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>Daily Log Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        h2 { color: #333; border-bottom: 2px solid #333; }
        .critical { color: red; }
        .warning { color: orange; }
        .info { color: blue; }
        pre { background: #f4f4f4; padding: 10px; overflow-x: auto; }
    </style>
</head>
<body>
EOF

    echo "<h1>Daily System Log Report - $(date)</h1>" >> "$report_file"
    
    # System overview
    echo "<h2>System Overview</h2>" >> "$report_file"
    echo "<pre>" >> "$report_file"
    uptime >> "$report_file"
    echo "</pre>" >> "$report_file"
    
    # Critical events
    echo "<h2 class='critical'>Critical Events (Last 24 Hours)</h2>" >> "$report_file"
    echo "<pre>" >> "$report_file"
    journalctl --since "24 hours ago" --priority=0..2 --no-pager | head -50 >> "$report_file"
    echo "</pre>" >> "$report_file"
    
    # Service status
    echo "<h2>Service Status</h2>" >> "$report_file"
    echo "<pre>" >> "$report_file"
    systemctl --failed --no-pager >> "$report_file"
    echo "</pre>" >> "$report_file"
    
    # Disk usage
    echo "<h2>Disk Usage</h2>" >> "$report_file"
    echo "<pre>" >> "$report_file"
    df -h >> "$report_file"
    echo "</pre>" >> "$report_file"
    
    echo "</body></html>" >> "$report_file"
    
    echo "Log report generated: $report_file"
}

# Main execution based on arguments
case "${1:-help}" in
    web)
        analyze_web_logs "$2"
        ;;
    security)
        analyze_security_logs "${2:-24 hours ago}"
        ;;
    monitor)
        real_time_log_monitor "$2"
        ;;
    report)
        generate_log_report
        ;;
    help|*)
        echo "Usage: $0 {web|security|monitor|report} [arguments]"
        echo "  web <logfile>         - Analyze web server logs"
        echo "  security [timeframe]  - Analyze security events"
        echo "  monitor [logfile]     - Real-time log monitoring"
        echo "  report               - Generate comprehensive report"
        ;;
esac
```

### Performance Monitoring Tools
[Related Commands/Topics: ](#system-monitoring-commands)System Monitoring Commands 🟢

#### Comprehensive System Performance Monitor
```bash
#!/bin/bash
# Enterprise-grade system performance monitoring

# Function to collect CPU metrics
collect_cpu_metrics() {
    local output_file="$1"
    
    {
        echo "=== CPU Metrics ==="
        echo "Timestamp: $(date)"
        echo
        
        # CPU usage by core
        echo "CPU Usage by Core:"
        mpstat -P ALL 1 3 | grep Average
        echo
        
        # Load averages
        echo "Load Averages:"
        uptime
        echo
        
        # CPU frequency
        echo "CPU Frequency:"
        cpufreq-info 2>/dev/null || echo "cpufreq-info not available"
        echo
        
        # Context switches and interrupts
        echo "Context Switches and Interrupts:"
        sar -w 1 1 | grep Average
        echo
        
    } >> "$output_file"
}

# Function to collect memory metrics
collect_memory_metrics() {
    local output_file="$1"
    
    {
        echo "=== Memory Metrics ==="
        echo "Timestamp: $(date)"
        echo
        
        # Memory usage summary
        echo "Memory Usage Summary:"
        free -h
        echo
        
        # Detailed memory information
        echo "Detailed Memory Information:"
        cat /proc/meminfo | grep -E "(MemTotal|MemFree|MemAvailable|Buffers|Cached|SwapTotal|SwapFree)"
        echo
        
        # Memory usage by process
        echo "Top Memory Consumers:"
        ps aux --sort=-%mem | head -11
        echo
        
        # Virtual memory statistics
        echo "Virtual Memory Statistics:"
        vmstat 1 3 | tail -2
        echo
        
    } >> "$output_file"
}

# Function to collect disk I/O metrics
collect_disk_metrics() {
    local output_file="$1"
    
    {
        echo "=== Disk I/O Metrics ==="
        echo "Timestamp: $(date)"
        echo
        
        # Disk usage
        echo "Disk Usage:"
        df -h
        echo
        
        # I/O statistics
        echo "I/O Statistics:"
        iostat -x 1 3 | grep -A 20 "Device"
        echo
        
        # Top I/O processes
        echo "Top I/O Processes:"
        iotop -b -n 1 -o 2>/dev/null | head -15 || echo "iotop not available"
        echo
        
        # Disk health
        echo "Disk Health (SMART status):"
        for disk in $(lsblk -d -n -o NAME | grep -E "sd[a-z]|nvme"); do
            echo "=== /dev/$disk ==="
            smartctl -H "/dev/$disk" 2>/dev/null || echo "SMART data not available for $disk"
        done
        echo
        
    } >> "$output_file"
}

# Function to collect network metrics
collect_network_metrics() {
    local output_file="$1"
    
    {
        echo "=== Network Metrics ==="
        echo "Timestamp: $(date)"
        echo
        
        # Network interface statistics
        echo "Network Interface Statistics:"
        cat /proc/net/dev
        echo
        
        # Network connections summary
        echo "Network Connections Summary:"
        ss -s
        echo
        
        # Active connections
        echo "Active Network Connections:"
        ss -tuln | head -20
        echo
        
        # Network traffic by interface
        echo "Network Traffic:"
        sar -n DEV 1 3 | grep Average
        echo
        
    } >> "$output_file"
}

# Function to generate performance baseline
generate_performance_baseline() {
    local baseline_dir="/var/log/performance/baseline"
    local timestamp=$(date +%Y%m%d_%H%M%S)
    
    mkdir -p "$baseline_dir"
    
    local baseline_file="$baseline_dir/baseline_$timestamp.txt"
    
    echo "Generating performance baseline: $baseline_file"
    
    collect_cpu_metrics "$baseline_file"
    collect_memory_metrics "$baseline_file"
    collect_disk_metrics "$baseline_file"
    collect_network_metrics "$baseline_file"
    
    # System information
    {
        echo "=== System Information ==="
        echo "Hostname: $(hostname)"
        echo "Kernel: $(uname -r)"
        echo "Distribution: $(lsb_release -d 2>/dev/null | cut -d: -f2 | trim || cat /etc/os-release | grep PRETTY_NAME)"
        echo "Hardware: $(dmidecode -s system-product-name 2>/dev/null || echo "N/A")"
        echo "CPU: $(lscpu | grep "Model name" | cut -d: -f2 | sed 's/^[[:space:]]*//')"
        echo "Memory: $(free -h | grep Mem | awk '{print $2}')"
        echo "Uptime: $(uptime)"
        echo
    } >> "$baseline_file"
    
    echo "Performance baseline completed: $baseline_file"
}

# Function for continuous performance monitoring
continuous_monitoring() {
    local monitoring_dir="/var/log/performance/monitoring"
    local interval="${1:-60}"  # Default 60 seconds
    
    mkdir -p "$monitoring_dir"
    
    echo "Starting continuous performance monitoring (interval: ${interval}s)"
    echo "Press Ctrl+C to stop"
    
    while true; do
        local timestamp=$(date +%Y%m%d_%H%M%S)
        local metrics_file="$monitoring_dir/metrics_$timestamp.txt"
        
        collect_cpu_metrics "$metrics_file"
        collect_memory_metrics "$metrics_file"
        collect_disk_metrics "$metrics_file"
        collect_network_metrics "$metrics_file"
        
        echo "Metrics collected: $metrics_file"
        sleep "$interval"
    done
}

# Function to analyze performance trends
analyze_performance_trends() {
    local baseline_file="$1"
    local current_file="$2"
    local analysis_file="/tmp/performance_analysis_$(date +%Y%m%d_%H%M%S).txt"
    
    {
        echo "Performance Trend Analysis"
        echo "Baseline: $baseline_file"
        echo "Current: $current_file"
        echo "Analysis Date: $(date)"
        echo "=========================="
        echo
        
        # Compare CPU usage
        echo "=== CPU Usage Comparison ==="
        echo "Baseline Load Average:"
        grep "load average" "$baseline_file" | tail -1
        echo "Current Load Average:"
        grep "load average" "$current_file" | tail -1
        echo
        
        # Compare memory usage
        echo "=== Memory Usage Comparison ==="
        echo "Baseline Memory:"
        grep -A 1 "Memory Usage Summary" "$baseline_file" | tail -1
        echo "Current Memory:"
        grep -A 1 "Memory Usage Summary" "$current_file" | tail -1
        echo
        
        # Compare disk usage
        echo "=== Disk Usage Comparison ==="
        echo "Baseline Disk Usage:"
        grep -A 10 "Disk Usage:" "$baseline_file" | grep -E "(/dev/|Filesystem)"
        echo "Current Disk Usage:"
        grep -A 10 "Disk Usage:" "$current_file" | grep -E "(/dev/|Filesystem)"
        echo
        
    } > "$analysis_file"
    
    echo "Performance analysis completed: $analysis_file"
}

# Main execution
case "${1:-help}" in
    baseline)
        generate_performance_baseline
        ;;
    monitor)
        continuous_monitoring "${2:-60}"
        ;;
    analyze)
        analyze_performance_trends "$2" "$3"
        ;;
    cpu)
        collect_cpu_metrics "/tmp/cpu_metrics_$(date +%Y%m%d_%H%M%S).txt"
        ;;
    memory)
        collect_memory_metrics "/tmp/memory_metrics_$(date +%Y%m%d_%H%M%S).txt"
        ;;
    disk)
        collect_disk_metrics "/tmp/disk_metrics_$(date +%Y%m%d_%H%M%S).txt"
        ;;
    network)
        collect_network_metrics "/tmp/network_metrics_$(date +%Y%m%d_%H%M%S).txt"
        ;;
    help|*)
        echo "Usage: $0 {baseline|monitor|analyze|cpu|memory|disk|network} [options]"
        echo "  baseline              - Generate performance baseline"
        echo "  monitor [interval]    - Continuous monitoring (default: 60s)"
        echo "  analyze <base> <curr> - Compare baseline with current metrics"
        echo "  cpu|memory|disk|network - Collect specific metrics"
        ;;
esac
```

### Centralized Logging Implementation
[Related Commands/Topics: ](#monitoring-infrastructure-commands)Monitoring Infrastructure Commands 🟡

#### ELK Stack Deployment
```bash
#!/bin/bash
# Complete ELK Stack deployment script

# Install Java (required for Elasticsearch and Logstash)
install_java() {
    echo "Installing OpenJDK 11..."
    apt-get update
    apt-get install -y openjdk-11-jdk
    
    # Set JAVA_HOME
    echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> /etc/environment
    source /etc/environment
}

# Install and configure Elasticsearch
install_elasticsearch() {
    echo "Installing Elasticsearch..."
    
    # Add Elastic repository
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -
    echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" > /etc/apt/sources.list.d/elastic-8.x.list
    
    apt-get update
    apt-get install -y elasticsearch
    
    # Configure Elasticsearch
    cat > /etc/elasticsearch/elasticsearch.yml << 'EOF'
cluster.name: logging-cluster
node.name: node-1
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: localhost
http.port: 9200
discovery.type: single-node

# Security settings
xpack.security.enabled: false
xpack.monitoring.collection.enabled: true
EOF

    # Enable and start Elasticsearch
    systemctl daemon-reload
    systemctl enable elasticsearch
    systemctl start elasticsearch
    
    # Wait for Elasticsearch to start
    sleep 30
    
    # Test Elasticsearch
    curl -X GET "localhost:9200/"
}

# Install and configure Logstash
install_logstash() {
    echo "Installing Logstash..."
    
    apt-get install -y logstash
    
    # Create Logstash configuration
    cat > /etc/logstash/conf.d/syslog.conf << 'EOF'
input {
  beats {
    port => 5044
  }
  
  syslog {
    port => 5514
  }
}

filter {
  if [fields][log_type] == "syslog" {
    grok {
      match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{IPORHOST:host} %{DATA:program}(?:\[%{POSINT:pid}\])?: %{GREEDYDATA:message}" }
    }
    
    date {
      match => [ "timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
    }
  }
  
  if [fields][log_type] == "nginx" {
    grok {
      match => { "message" => "%{NGINXACCESS}" }
    }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "logs-%{+YYYY.MM.dd}"
  }
  
  stdout { codec => rubydebug }
}
EOF

    # Enable and start Logstash
    systemctl enable logstash
    systemctl start logstash
}

# Install and configure Kibana
install_kibana() {
    echo "Installing Kibana..."
    
    apt-get install -y kibana
    
    # Configure Kibana
    cat > /etc/kibana/kibana.yml << 'EOF'
server.port: 5601
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]
logging.dest: /var/log/kibana/kibana.log
EOF

    # Create log directory
    mkdir -p /var/log/kibana
    chown kibana:kibana /var/log/kibana
    
    # Enable and start Kibana
    systemctl enable kibana
    systemctl start kibana
}

# Configure Filebeat for log shipping
install_filebeat() {
    echo "Installing Filebeat..."
    
    apt-get install -y filebeat
    
    # Configure Filebeat
    cat > /etc/filebeat/filebeat.yml << 'EOF'
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log
    - /var/log/syslog
    - /var/log/auth.log
  fields:
    logtype: system
  fields_under_root: true

- type: log
  enabled: true
  paths:
    - /var/log/nginx/*.log
  fields:
    logtype: nginx
  fields_under_root: true

- type: log
  enabled: true
  paths:
    - /var/log/apache2/*.log
  fields:
    logtype: apache
  fields_under_root: true

output.logstash:
  hosts: ["localhost:5044"]

processors:
  - add_host_metadata:
      when.not.contains.tags: forwarded
  - add_docker_metadata: ~
  - add_kubernetes_metadata: ~

logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
EOF

    # Enable and start Filebeat
    systemctl enable filebeat
    systemctl start filebeat
}

# Main installation
echo "Starting ELK Stack installation..."
install_java
install_elasticsearch
install_logstash
install_kibana
install_filebeat

echo "ELK Stack installation completed!"
echo "Access Kibana at: http://localhost:5601"
echo "Elasticsearch API: http://localhost:9200"
```

### Monitoring Infrastructure Deployment
[Related Commands/Topics: ](#monitoring-infrastructure-commands)Monitoring Infrastructure Commands 🟡

#### Complete Prometheus and Grafana Setup
```bash
#!/bin/bash
# Complete monitoring infrastructure deployment

# Install Prometheus
install_prometheus() {
    echo "Installing Prometheus..."
    
    # Create prometheus user
    useradd --no-create-home --shell /bin/false prometheus
    
    # Create directories
    mkdir -p /etc/prometheus /var/lib/prometheus
    chown prometheus:prometheus /etc/prometheus /var/lib/prometheus
    
    # Download and install Prometheus
    cd /tmp
    wget https://github.com/prometheus/prometheus/releases/download/v2.45.0/prometheus-2.45.0.linux-amd64.tar.gz
    tar xzf prometheus-2.45.0.linux-amd64.tar.gz
    
    cp prometheus-2.45.0.linux-amd64/prometheus /usr/local/bin/
    cp prometheus-2.45.0.linux-amd64/promtool /usr/local/bin/
    cp -r prometheus-2.45.0.linux-amd64/consoles /etc/prometheus/
    cp -r prometheus-2.45.0.linux-amd64/console_libraries /etc/prometheus/
    
    chown -R prometheus:prometheus /etc/prometheus/consoles /etc/prometheus/console_libraries
    chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool
    
    # Create Prometheus configuration
    cat > /etc/prometheus/prometheus.yml << 'EOF'
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    monitor: 'production'

rule_files:
  - "/etc/prometheus/alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'alertmanager'
    static_configs:
      - targets: ['localhost:9093']

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - localhost:9093
EOF

    # Create alert rules
    cat > /etc/prometheus/alert_rules.yml << 'EOF'
groups:
  - name: system_alerts
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Instance {{ $labels.instance }} down"
          description: "{{ $labels.instance }} has been down for more than 5 minutes."

      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage on {{ $labels.instance }}"
          description: "CPU usage is above 80% for more than 5 minutes."

      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100 > 85
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage on {{ $labels.instance }}"
          description: "Memory usage is above 85% for more than 5 minutes."
EOF

    chown prometheus:prometheus /etc/prometheus/prometheus.yml /etc/prometheus/alert_rules.yml
    
    # Create systemd service
    cat > /etc/systemd/system/prometheus.service << 'EOF'
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries \
    --web.listen-address=0.0.0.0:9090 \
    --web.external-url=

[Install]
WantedBy=multi-user.target
EOF

    systemctl daemon-reload
    systemctl enable prometheus
    systemctl start prometheus
}

# Install Alertmanager
install_alertmanager() {
    echo "Installing Alertmanager..."
    
    # Create alertmanager user
    useradd --no-create-home --shell /bin/false alertmanager
    
    # Create directories
    mkdir -p /etc/alertmanager /var/lib/alertmanager
    chown alertmanager:alertmanager /etc/alertmanager /var/lib/alertmanager
    
    # Download and install Alertmanager
    cd /tmp
    wget https://github.com/prometheus/alertmanager/releases/download/v0.25.0/alertmanager-0.25.0.linux-amd64.tar.gz
    tar xzf alertmanager-0.25.0.linux-amd64.tar.gz
    
    cp alertmanager-0.25.0.linux-amd64/alertmanager /usr/local/bin/
    cp alertmanager-0.25.0.linux-amd64/amtool /usr/local/bin/
    
    chown alertmanager:alertmanager /usr/local/bin/alertmanager /usr/local/bin/amtool
    
    # Create Alertmanager configuration
    cat > /etc/alertmanager/alertmanager.yml << 'EOF'
global:
  smtp_smarthost: 'localhost:587'
  smtp_from: 'alertmanager@example.com'

route:
  group_by: ['alertname']
  group_wait: 10s
  group_interval: 10s
  repeat_interval: 1h
  receiver: 'web.hook'

receivers:
- name: 'web.hook'
  email_configs:
  - to: 'admin@example.com'
    subject: 'Alert: {{ .GroupLabels.alertname }}'
    body: |
      {{ range .Alerts }}
      Alert: {{ .Annotations.summary }}
      Description: {{ .Annotations.description }}
      {{ end }}

inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'instance']
EOF

    chown alertmanager:alertmanager /etc/alertmanager/alertmanager.yml
    
    # Create systemd service
    cat > /etc/systemd/system/alertmanager.service << 'EOF'
[Unit]
Description=Alertmanager
Wants=network-online.target
After=network-online.target

[Service]
User=alertmanager
Group=alertmanager
Type=simple
ExecStart=/usr/local/bin/alertmanager \
    --config.file=/etc/alertmanager/alertmanager.yml \
    --storage.path=/var/lib/alertmanager/

[Install]
WantedBy=multi-user.target
EOF

    systemctl daemon-reload
    systemctl enable alertmanager
    systemctl start alertmanager
}

# Install Grafana
install_grafana() {
    echo "Installing Grafana..."
    
    # Add Grafana repository
    apt-get install -y software-properties-common
    wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -
    echo "deb https://packages.grafana.com/oss/deb stable main" > /etc/apt/sources.list.d/grafana.list
    
    apt-get update
    apt-get install -y grafana
    
    # Configure Grafana
    cat > /etc/grafana/grafana.ini << 'EOF'
[server]
http_port = 3000
domain = localhost

[security]
admin_user = admin
admin_password = admin123

[users]
allow_sign_up = false

[auth.anonymous]
enabled = false

[alerting]
enabled = true

[log]
mode = file
level = info
EOF

    systemctl daemon-reload
    systemctl enable grafana-server
    systemctl start grafana-server
}

# Main installation
install_prometheus
install_alertmanager
install_grafana

echo "Monitoring infrastructure installation completed!"
echo "Prometheus: http://localhost:9090"
echo "Alertmanager: http://localhost:9093"
echo "Grafana: http://localhost:3000 (admin/admin123)"
```

### Alerting and Notification Systems
[Related Commands/Topics: ](#monitoring-infrastructure-commands)Monitoring Infrastructure Commands 🟡

#### Setting up Grafana Alerts
```bash
# Install Grafana
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt update
sudo apt install grafana

# Configure Grafana
sudo systemctl enable grafana-server
sudo systemctl start grafana-server

# Install plugins
sudo grafana-cli plugins install grafana-piechart-panel
sudo grafana-cli plugins install grafana-worldmap-panel
sudo systemctl restart grafana-server

# Grafana notification channels configuration
# Access Grafana at http://localhost:3000 (admin/admin)
```

### Security Monitoring and SIEM
[Related Commands/Topics: ](#log-management-commands)Log Management Commands 🟡

#### Elasticsearch Setup
```yaml
# /etc/elasticsearch/elasticsearch.yml
cluster.name: logging-cluster
node.name: node-1
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: localhost
http.port: 9200
discovery.type: single-node

# Security settings
xpack.security.enabled: false
xpack.monitoring.collection.enabled: true
```

#### Logstash Configuration
```ruby
# /etc/logstash/conf.d/syslog.conf
input {
  beats {
    port => 5044
  }
  
  syslog {
    port => 5514
  }
}

filter {
  if [fields][log_type] == "syslog" {
    grok {
      match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{IPORHOST:host} %{DATA:program}(?:\[%{POSINT:pid}\])?: %{GREEDYDATA:message}" }
    }
    
    date {
      match => [ "timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
    }
  }
  
  if [fields][log_type] == "nginx" {
    grok {
      match => { "message" => "%{NGINXACCESS}" }
    }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "logs-%{+YYYY.MM.dd}"
  }
  
  stdout { codec => rubydebug }
}
```

#### TLS Configuration for rsyslog
```bash
# Generate certificates for secure logging
sudo mkdir -p /etc/ssl/rsyslog
cd /etc/ssl/rsyslog

# Create CA certificate
sudo openssl genrsa -out ca-key.pem 2048
sudo openssl req -new -x509 -key ca-key.pem -out ca-cert.pem -days 365

# Create server certificate
sudo openssl genrsa -out server-key.pem 2048
sudo openssl req -new -key server-key.pem -out server-req.pem
sudo openssl x509 -req -in server-req.pem -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -out server-cert.pem -days 365

# Create client certificate
sudo openssl genrsa -out client-key.pem 2048
sudo openssl req -new -key client-key.pem -out client-req.pem
sudo openssl x509 -req -in client-req.pem -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -out client-cert.pem -days 365

# Set permissions
sudo chown syslog:syslog /etc/ssl/rsyslog/*
sudo chmod 600 /etc/ssl/rsyslog/*-key.pem
sudo chmod 644 /etc/ssl/rsyslog/*-cert.pem

# Configure rsyslog server for TLS
sudo tee /etc/rsyslog.d/gtls.conf << EOF
# TLS Configuration
\$ModLoad imtcp
\$DefaultNetstreamDriver gtls
\$DefaultNetstreamDriverCAFile /etc/ssl/rsyslog/ca-cert.pem
\$DefaultNetstreamDriverCertFile /etc/ssl/rsyslog/server-cert.pem
\$DefaultNetstreamDriverKeyFile /etc/ssl/rsyslog/server-key.pem
\$InputTCPServerStreamDriverMode 1
\$InputTCPServerStreamDriverAuthMode x509/name
\$InputTCPServerStreamDriverPermittedPeer *.example.com
\$InputTCPServerRun 6514
EOF
```

## Custom Monitoring Scripts

### Disk Space Alert Script
```bash
#!/bin/bash
# disk-alert.sh

THRESHOLD=85
EMAIL="admin@example.com"

df -h | awk 'NR>1 {print $5 " " $6}' | while read line; do
    usage=$(echo $line | awk '{print $1}' | sed 's/%//g')
    partition=$(echo $line | awk '{print $2}')
    
    if [ $usage -ge $THRESHOLD ]; then
        echo "WARNING: Disk usage on $partition is ${usage}%" | \
            mail -s "Disk Space Alert" $EMAIL
    fi
done
```

### Process Monitoring Script
```bash
#!/bin/bash
# process-monitor.sh

PROCESS="nginx"
RESTART_CMD="systemctl start nginx"
EMAIL="admin@example.com"

if ! pgrep $PROCESS > /dev/null; then
    echo "Process $PROCESS not running. Attempting restart..."
    $RESTART_CMD
    
    if pgrep $PROCESS > /dev/null; then
        echo "Process $PROCESS restarted successfully" | \
            mail -s "Process Restart Success" $EMAIL
    else
        echo "Failed to restart $PROCESS" | \
            mail -s "Process Restart Failed" $EMAIL
    fi
fi
```
### Centralized Logging Implementation

#### ELK Stack Deployment
```bash
#!/bin/bash
# Complete ELK Stack deployment script

# Install Java (required for Elasticsearch and Logstash)
install_java() {
    echo "Installing OpenJDK 11..."
    apt-get update
    apt-get install -y openjdk-11-jdk
    
    # Set JAVA_HOME
    echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> /etc/environment
    source /etc/environment
}

# Install and configure Elasticsearch
install_elasticsearch() {
    echo "Installing Elasticsearch..."
    
    # Add Elastic repository
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -
    echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" > /etc/apt/sources.list.d/elastic-8.x.list
    
    apt-get update
    apt-get install -y elasticsearch
    
    # Configure Elasticsearch
    cat > /etc/elasticsearch/elasticsearch.yml << 'EOF'
cluster.name: logging-cluster
node.name: node-1
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: localhost
http.port: 9200
discovery.type: single-node

# Security settings
xpack.security.enabled: false
xpack.monitoring.collection.enabled: true
EOF

    # Enable and start Elasticsearch
    systemctl daemon-reload
    systemctl enable elasticsearch
    systemctl start elasticsearch
    
    # Wait for Elasticsearch to start
    sleep 30
    
    # Test Elasticsearch
    curl -X GET "localhost:9200/"
}

# Install and configure Logstash
install_logstash() {
    echo "Installing Logstash..."
    
    apt-get install -y logstash
    
    # Create Logstash configuration
    cat > /etc/logstash/conf.d/syslog.conf << 'EOF'
input {
  beats {
    port => 5044
  }
  
  syslog {
    port => 5514
  }
}

filter {
  if [fields][log_type] == "syslog" {
    grok {
      match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{IPORHOST:host} %{DATA:program}(?:\[%{POSINT:pid}\])?: %{GREEDYDATA:message}" }
    }
    
    date {
      match => [ "timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
    }
  }
  
  if [fields][log_type] == "nginx" {
    grok {
      match => { "message" => "%{NGINXACCESS}" }
    }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "logs-%{+YYYY.MM.dd}"
  }
  
  stdout { codec => rubydebug }
}
EOF

    # Enable and start Logstash
    systemctl enable logstash
    systemctl start logstash
}

# Install and configure Kibana
install_kibana() {
    echo "Installing Kibana..."
    
    apt-get install -y kibana
    
    # Configure Kibana
    cat > /etc/kibana/kibana.yml << 'EOF'
server.port: 5601
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]
logging.dest: /var/log/kibana/kibana.log
EOF

    # Create log directory
    mkdir -p /var/log/kibana
    chown kibana:kibana /var/log/kibana
    
    # Enable and start Kibana
    systemctl enable kibana
    systemctl start kibana
}

# Configure Filebeat for log shipping
install_filebeat() {
    echo "Installing Filebeat..."
    
    apt-get install -y filebeat
    
    # Configure Filebeat
    cat > /etc/filebeat/filebeat.yml << 'EOF'
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log
    - /var/log/syslog
    - /var/log/auth.log
  fields:
    logtype: system
  fields_under_root: true

- type: log
  enabled: true
  paths:
    - /var/log/nginx/*.log
  fields:
    logtype: nginx
  fields_under_root: true

- type: log
  enabled: true
  paths:
    - /var/log/apache2/*.log
  fields:
    logtype: apache
  fields_under_root: true

output.logstash:
  hosts: ["localhost:5044"]

processors:
  - add_host_metadata:
      when.not.contains.tags: forwarded
  - add_docker_metadata: ~
  - add_kubernetes_metadata: ~

logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0644
EOF

    # Enable and start Filebeat
    systemctl enable filebeat
    systemctl start filebeat
}

# Main installation
echo "Starting ELK Stack installation..."
install_java
install_elasticsearch
install_logstash
install_kibana
install_filebeat

echo "ELK Stack installation completed!"
echo "Access Kibana at: http://localhost:5601"
echo "Elasticsearch API: http://localhost:9200"
```

### Monitoring Infrastructure Deployment
[Related Commands/Topics: Monitoring Infrastructure Commands](#monitoring-infrastructure-commands) 🟡

#### Complete Prometheus and Grafana Setup
```bash
#!/bin/bash
# Complete monitoring infrastructure deployment

# Install Prometheus
install_prometheus() {
    echo "Installing Prometheus..."
    
    # Create prometheus user
    useradd --no-create-home --shell /bin/false prometheus
    
    # Create directories
    mkdir -p /etc/prometheus /var/lib/prometheus
    chown prometheus:prometheus /etc/prometheus /var/lib/prometheus
    
    # Download and install Prometheus
    cd /tmp
    wget https://github.com/prometheus/prometheus/releases/download/v2.45.0/prometheus-2.45.0.linux-amd64.tar.gz
    tar xzf prometheus-2.45.0.linux-amd64.tar.gz
    
    cp prometheus-2.45.0.linux-amd64/prometheus /usr/local/bin/
    cp prometheus-2.45.0.linux-amd64/promtool /usr/local/bin/
    cp -r prometheus-2.45.0.linux-amd64/consoles /etc/prometheus/
    cp -r prometheus-2.45.0.linux-amd64/console_libraries /etc/prometheus/
    
    chown -R prometheus:prometheus /etc/prometheus/consoles /etc/prometheus/console_libraries
    chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool
    
    # Create Prometheus configuration
    cat > /etc/prometheus/prometheus.yml << 'EOF'
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    monitor: 'production'

rule_files:
  - "/etc/prometheus/alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'alertmanager'
    static_configs:
      - targets: ['localhost:9093']

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - localhost:9093
EOF

    # Create alert rules
    cat > /etc/prometheus/alert_rules.yml << 'EOF'
groups:
  - name: system_alerts
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Instance {{ $labels.instance }} down"
          description: "{{ $labels.instance }} has been down for more than 5 minutes."

      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage on {{ $labels.instance }}"
          description: "CPU usage is above 80% for more than 5 minutes."

      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100 > 85
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage on {{ $labels.instance }}"
          description: "Memory usage is above 85% for more than 5 minutes."
EOF

    chown prometheus:prometheus /etc/prometheus/prometheus.yml /etc/prometheus/alert_rules.yml
    
    # Create systemd service
    cat > /etc/systemd/system/prometheus.service << 'EOF'
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries \
    --web.listen-address=0.0.0.0:9090 \
    --web.external-url=

[Install]
WantedBy=multi-user.target
EOF

    systemctl daemon-reload
    systemctl enable prometheus
    systemctl start prometheus
}

# Install Alertmanager
install_alertmanager() {
    echo "Installing Alertmanager..."
    
    # Create alertmanager user
    useradd --no-create-home --shell /bin/false alertmanager
    
    # Create directories
    mkdir -p /etc/alertmanager /var/lib/alertmanager
    chown alertmanager:alertmanager /etc/alertmanager /var/lib/alertmanager
    
    # Download and install Alertmanager
    cd /tmp
    wget https://github.com/prometheus/alertmanager/releases/download/v0.25.0/alertmanager-0.25.0.linux-amd64.tar.gz
    tar xzf alertmanager-0.25.0.linux-amd64.tar.gz
    
    cp alertmanager-0.25.0.linux-amd64/alertmanager /usr/local/bin/
    cp alertmanager-0.25.0.linux-amd64/amtool /usr/local/bin/
    
    chown alertmanager:alertmanager /usr/local/bin/alertmanager /usr/local/bin/amtool
    
    # Create Alertmanager configuration
    cat > /etc/alertmanager/alertmanager.yml << 'EOF'
global:
  smtp_smarthost: 'localhost:587'
  smtp_from: 'alertmanager@example.com'

route:
  group_by: ['alertname']
  group_wait: 10s
  group_interval: 10s
  repeat_interval: 1h
  receiver: 'web.hook'

receivers:
- name: 'web.hook'
  email_configs:
  - to: 'admin@example.com'
    subject: 'Alert: {{ .GroupLabels.alertname }}'
    body: |
      {{ range .Alerts }}
      Alert: {{ .Annotations.summary }}
      Description: {{ .Annotations.description }}
      {{ end }}

inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'instance']
EOF

    chown alertmanager:alertmanager /etc/alertmanager/alertmanager.yml
    
    # Create systemd service
    cat > /etc/systemd/system/alertmanager.service << 'EOF'
[Unit]
Description=Alertmanager
Wants=network-online.target
After=network-online.target

[Service]
User=alertmanager
Group=alertmanager
Type=simple
ExecStart=/usr/local/bin/alertmanager \
    --config.file=/etc/alertmanager/alertmanager.yml \
    --storage.path=/var/lib/alertmanager/

[Install]
WantedBy=multi-user.target
EOF

    systemctl daemon-reload
    systemctl enable alertmanager
    systemctl start alertmanager
}

# Install Grafana
install_grafana() {
    echo "Installing Grafana..."
    
    # Add Grafana repository
    apt-get install -y software-properties-common
    wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -
    echo "deb https://packages.grafana.com/oss/deb stable main" > /etc/apt/sources.list.d/grafana.list
    
    apt-get update
    apt-get install -y grafana
    
    # Configure Grafana
    cat > /etc/grafana/grafana.ini << 'EOF'
[server]
http_port = 3000
domain = localhost

[security]
admin_user = admin
admin_password = admin123

[users]
allow_sign_up = false

[auth.anonymous]
enabled = false

[alerting]
enabled = true

[log]
mode = file
level = info
EOF

    systemctl daemon-reload
    systemctl enable grafana-server
    systemctl start grafana-server
}

# Main installation
install_prometheus
install_alertmanager
install_grafana

echo "Monitoring infrastructure installation completed!"
echo "Prometheus: http://localhost:9090"
echo "Alertmanager: http://localhost:9093"
echo "Grafana: http://localhost:3000 (admin/admin123)"
```

### Alerting and Notification Systems
[Related Commands/Topics: Monitoring Infrastructure Commands](#monitoring-infrastructure-commands) 🟡

#### Advanced Alerting Configuration
```bash
#!/bin/bash
# Advanced alerting and notification system

# Create multi-channel notification script
create_notification_system() {
    cat > /usr/local/bin/alert-dispatcher.sh << 'EOF'
#!/bin/bash
# Multi-channel alert dispatcher

ALERT_TYPE="$1"
SEVERITY="$2"
MESSAGE="$3"
SOURCE="$4"

# Configuration
EMAIL_RECIPIENTS="admin@example.com ops@example.com"
SLACK_WEBHOOK="https://hooks.slack.com/services/YOUR/SLACK/WEBHOOK"
SMS_API_KEY="your_sms_api_key"
TELEGRAM_TOKEN="your_telegram_bot_token"
TELEGRAM_CHAT_ID="your_chat_id"

# Function to send email alerts
send_email() {
    local subject="[$SEVERITY] $ALERT_TYPE Alert from $SOURCE"
    local body="Alert Details:\n\nType: $ALERT_TYPE\nSeverity: $SEVERITY\nSource: $SOURCE\nMessage: $MESSAGE\n\nTimestamp: $(date)"
    
    echo -e "$body" | mail -s "$subject" $EMAIL_RECIPIENTS
}

# Function to send Slack notifications
send_slack() {
    local color="good"
    case "$SEVERITY" in
        "critical") color="danger" ;;
        "warning") color="warning" ;;
        "info") color="good" ;;
    esac
    
    local payload=$(cat <<EOF
{
    "attachments": [
        {
            "color": "$color",
            "title": "$ALERT_TYPE Alert",
            "fields": [
                {
                    "title": "Severity",
                    "value": "$SEVERITY",
                    "short": true
                },
                {
                    "title": "Source",
                    "value": "$SOURCE",
                    "short": true
                },
                {
                    "title": "Message",
                    "value": "$MESSAGE",
                    "short": false
                }
            ],
            "footer": "System Monitor",
            "ts": $(date +%s)
        }
    ]
}
EOF
)
    
    curl -X POST -H 'Content-type: application/json' --data "$payload" "$SLACK_WEBHOOK"
}

# Function to send Telegram notifications
send_telegram() {
    local text="🚨 *$SEVERITY Alert*\n\n*Type:* $ALERT_TYPE\n*Source:* $SOURCE\n*Message:* $MESSAGE\n\n*Time:* $(date)"
    
    curl -s -X POST "https://api.telegram.org/bot$TELEGRAM_TOKEN/sendMessage" \
        -d chat_id="$TELEGRAM_CHAT_ID" \
        -d text="$text" \
        -d parse_mode="Markdown"
}

# Function to send SMS (using example SMS API)
send_sms() {
    local phone_numbers="1234567890,0987654321"  # Add your phone numbers
    local sms_text="ALERT: $SEVERITY $ALERT_TYPE from $SOURCE: $MESSAGE"
    
    # Example SMS API call (adjust for your provider)
    curl -X POST "https://api.sms-provider.com/send" \
        -H "Authorization: Bearer $SMS_API_KEY" \
        -d "to=$phone_numbers" \
        -d "message=$sms_text"
}

# Function to create incident ticket
create_incident_ticket() {
    local ticket_data=$(cat <<EOF
{
    "title": "$ALERT_TYPE Alert - $SEVERITY",
    "description": "Alert from $SOURCE\n\nDetails:\n$MESSAGE\n\nTimestamp: $(date)",
    "priority": "$SEVERITY",
    "tags": ["monitoring", "automated", "$ALERT_TYPE"]
}
EOF
)
    
    # Example ticket creation (adjust for your ticketing system)
    curl -X POST "https://your-ticketing-system.com/api/tickets" \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer your_api_token" \
        -d "$ticket_data"
}

# Escalation logic based on severity
case "$SEVERITY" in
    "critical")
        send_email
        send_slack
        send_telegram
        send_sms
        create_incident_ticket
        ;;
    "warning")
        send_email
        send_slack
        send_telegram
        ;;
    "info")
        send_slack
        ;;
    *)
        send_email
        ;;
esac

# Log the alert
echo "$(date): Alert dispatched - Type: $ALERT_TYPE, Severity: $SEVERITY, Source: $SOURCE" >> /var/log/alert-dispatcher.log
EOF

    chmod +x /usr/local/bin/alert-dispatcher.sh
}

# Create escalation policies
create_escalation_policies() {
    cat > /etc/alerting/escalation-policies.conf << 'EOF'
# Escalation Policies Configuration

# Critical alerts - immediate escalation
CRITICAL_ESCALATION_TIMEOUT=300  # 5 minutes
CRITICAL_ESCALATION_LEVELS=(
    "primary-oncall@example.com"
    "secondary-oncall@example.com"
    "manager@example.com"
    "director@example.com"
)

# Warning alerts - delayed escalation
WARNING_ESCALATION_TIMEOUT=1800  # 30 minutes
WARNING_ESCALATION_LEVELS=(
    "team-lead@example.com"
    "senior-engineer@example.com"
)

# Info alerts - no escalation
INFO_ESCALATION=false
EOF
}

# Create alert routing script
create_alert_router() {
    cat > /usr/local/bin/alert-router.sh << 'EOF'
#!/bin/bash
# Intelligent alert routing system

source /etc/alerting/escalation-policies.conf

ALERT_ID="$1"
ALERT_TYPE="$2"
SEVERITY="$3"
MESSAGE="$4"
SOURCE="$5"

ALERT_DIR="/var/lib/alerting"
ALERT_FILE="$ALERT_DIR/alert_$ALERT_ID.state"

mkdir -p "$ALERT_DIR"

# Function to check if alert is acknowledged
is_acknowledged() {
    [ -f "$ALERT_FILE" ] && grep -q "acknowledged" "$ALERT_FILE"
}

# Function to get escalation level
get_escalation_level() {
    if [ -f "$ALERT_FILE" ]; then
        grep "escalation_level=" "$ALERT_FILE" | cut -d'=' -f2
    else
        echo "0"
    fi
}

# Function to escalate alert
escalate_alert() {
    local current_level=$(get_escalation_level)
    local next_level=$((current_level + 1))
    
    case "$SEVERITY" in
        "critical")
            if [ $next_level -lt ${#CRITICAL_ESCALATION_LEVELS[@]} ]; then
                local recipient="${CRITICAL_ESCALATION_LEVELS[$next_level]}"
                echo "escalation_level=$next_level" > "$ALERT_FILE"
                echo "escalated_at=$(date)" >> "$ALERT_FILE"
                
                # Send escalated notification
                /usr/local/bin/alert-dispatcher.sh "$ALERT_TYPE" "$SEVERITY" "ESCALATED: $MESSAGE" "$SOURCE"
                
                # Schedule next escalation
                echo "sleep $CRITICAL_ESCALATION_TIMEOUT && /usr/local/bin/alert-router.sh $ALERT_ID $ALERT_TYPE $SEVERITY '$MESSAGE' $SOURCE" | at now
            fi
            ;;
        "warning")
            if [ $next_level -lt ${#WARNING_ESCALATION_LEVELS[@]} ]; then
                local recipient="${WARNING_ESCALATION_LEVELS[$next_level]}"
                echo "escalation_level=$next_level" > "$ALERT_FILE"
                echo "escalated_at=$(date)" >> "$ALERT_FILE"
                
                /usr/local/bin/alert-dispatcher.sh "$ALERT_TYPE" "$SEVERITY" "ESCALATED: $MESSAGE" "$SOURCE"
                
                echo "sleep $WARNING_ESCALATION_TIMEOUT && /usr/local/bin/alert-router.sh $ALERT_ID $ALERT_TYPE $SEVERITY '$MESSAGE' $SOURCE" | at now
            fi
            ;;
    esac
}

# Main logic
if ! is_acknowledged; then
    # Initial alert
    if [ ! -f "$ALERT_FILE" ]; then
        echo "alert_id=$ALERT_ID" > "$ALERT_FILE"
        echo "created_at=$(date)" >> "$ALERT_FILE"
        echo "escalation_level=0" >> "$ALERT_FILE"
        
        # Send initial alert
        /usr/local/bin/alert-dispatcher.sh "$ALERT_TYPE" "$SEVERITY" "$MESSAGE" "$SOURCE"
        
        # Schedule escalation for critical and warning alerts
        if [ "$SEVERITY" = "critical" ] || [ "$SEVERITY" = "warning" ]; then
            case "$SEVERITY" in
                "critical")
                    echo "sleep $CRITICAL_ESCALATION_TIMEOUT && /usr/local/bin/alert-router.sh $ALERT_ID $ALERT_TYPE $SEVERITY '$MESSAGE' $SOURCE" | at now
                    ;;
                "warning")
                    echo "sleep $WARNING_ESCALATION_TIMEOUT && /usr/local/bin/alert-router.sh $ALERT_ID $ALERT_TYPE $SEVERITY '$MESSAGE' $SOURCE" | at now
                    ;;
            esac
        fi
    else
        # Escalate existing alert
        escalate_alert
    fi
fi
EOF

    chmod +x /usr/local/bin/alert-router.sh
}

# Execute setup
create_notification_system
create_escalation_policies
create_alert_router

echo "Advanced alerting system configured successfully"
```

## Lab Exercises

### Lab 1: Log Management and Analysis

**Objective**: Configure comprehensive logging and implement log analysis procedures

**Tasks**:
1. Configure rsyslog for centralized logging with custom templates
2. Set up log rotation policies for system and application logs
3. Implement structured logging with JSON format
4. Create log analysis scripts for security event detection
5. Configure log shipping to remote servers with TLS encryption

**Deliverables**:
- Custom rsyslog configuration with security event filtering
- Logrotate policies for all system components
- Log analysis report with security findings
- Performance impact assessment of logging changes

**Assessment Criteria**:
- Log configuration accuracy and security (25%)
- Analysis script effectiveness (25%)
- Performance optimization (25%)
- Documentation quality (25%)

### Lab 2: Performance Monitoring Implementation

**Objective**: Deploy comprehensive performance monitoring infrastructure

**Tasks**:
1. Install and configure Prometheus with custom metrics
2. Deploy Node Exporter with additional collectors
3. Create performance baseline and trending analysis
4. Implement custom monitoring scripts for application metrics
5. Configure alerting rules for performance thresholds

**Deliverables**:
- Complete Prometheus monitoring setup
- Custom metrics collection scripts
- Performance baseline documentation
- Alert rule configuration with testing results

**Assessment Criteria**:
- Monitoring coverage completeness (30%)
- Alert rule effectiveness (25%)
- Custom metrics implementation (25%)
- Baseline analysis quality (20%)

### Lab 3: Centralized Logging Infrastructure

**Objective**: Implement enterprise-grade centralized logging solution

**Tasks**:
1. Deploy ELK Stack (Elasticsearch, Logstash, Kibana)
2. Configure log parsing and enrichment pipelines
3. Create Kibana dashboards for different log types
4. Implement log-based alerting and monitoring
5. Configure high-availability and backup procedures

**Deliverables**:
- Fully functional ELK Stack deployment
- Log parsing configurations for multiple sources
- Interactive Kibana dashboards
- Backup and recovery procedures documentation

**Assessment Criteria**:
- Infrastructure deployment quality (30%)
- Dashboard design and functionality (25%)
- Log parsing accuracy (25%)
- High availability implementation (20%)

### Lab 4: Monitoring and Alerting Systems

**Objective**: Create comprehensive monitoring and alerting infrastructure

**Tasks**:
1. Deploy Grafana with multiple data sources
2. Create monitoring dashboards for system and application metrics
3. Configure Alertmanager with multi-channel notifications
4. Implement escalation policies and incident management
5. Create automated response scripts for common issues

**Deliverables**:
- Grafana monitoring dashboards
- Multi-channel alerting configuration
- Escalation policy documentation
- Automated response procedures

**Assessment Criteria**:
- Dashboard design and usability (25%)
- Alerting accuracy and relevance (30%)
- Escalation policy effectiveness (25%)
- Automation implementation (20%)

### Lab 5: Security Monitoring and Incident Response

**Objective**: Implement security-focused monitoring and incident response capabilities

**Tasks**:
1. Configure security event monitoring and correlation
2. Implement intrusion detection and log analysis
3. Create security dashboards and alerting
4. Develop incident response procedures
5. Configure automated threat response mechanisms

**Deliverables**:
- Security monitoring configuration
- Incident response playbooks
- Automated threat detection scripts
- Security metrics and reporting dashboards

**Assessment Criteria**:
- Security monitoring effectiveness (30%)
- Incident response procedures (25%)
- Threat detection accuracy (25%)
- Automation and integration (20%)

## Best Practices

### Logging Best Practices
- **Centralized Architecture**: Implement centralized logging for scalability and management
- **Structured Formats**: Use consistent, parseable log formats (JSON, CEF)
- **Security Considerations**: Protect log integrity, encrypt transport, control access
- **Retention Policies**: Balance compliance requirements with storage costs
- **Performance Impact**: Monitor logging overhead and optimize for production
- **Real-time Analysis**: Implement streaming log analysis for immediate threat detection
- **Correlation Capabilities**: Enable cross-system log correlation and analysis

### Monitoring Best Practices
- **Comprehensive Coverage**: Monitor all critical system and application components
- **Baseline Establishment**: Understand normal behavior patterns for accurate alerting
- **Layered Monitoring**: Implement infrastructure, application, and business metrics
- **Alert Quality**: Focus on actionable alerts, minimize noise and false positives
- **Escalation Procedures**: Define clear escalation paths and response procedures
- **Capacity Planning**: Use monitoring data for proactive capacity management
- **Documentation**: Maintain comprehensive runbooks and troubleshooting guides

### Performance Optimization
- **Resource Allocation**: Right-size monitoring infrastructure for your environment
- **Data Retention**: Implement appropriate retention policies for different metric types
- **Query Optimization**: Optimize dashboard queries and alert expressions
- **High Availability**: Design monitoring systems for high availability and redundancy
- **Automation**: Automate routine monitoring tasks and response procedures

## Troubleshooting

### Common Logging Issues

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| **Logs not rotating** | Disk space filling up | Check logrotate configuration and cron jobs |
| **Missing log entries** | Gaps in log files | Verify rsyslog service status and configuration |
| **High log volume** | Performance degradation | Implement log filtering and sampling |
| **Permission errors** | Log files not writable | Correct file permissions and ownership |
| **Remote logging failure** | Logs not reaching destination | Check network connectivity and firewall rules |

### Common Monitoring Issues

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| **Metrics not collecting** | Missing data in dashboards | Check exporter status and configuration |
| **High memory usage** | Prometheus consuming excessive memory | Adjust retention settings and query optimization |
| **Alert fatigue** | Too many false alerts | Refine alert rules and thresholds |
| **Dashboard performance** | Slow loading dashboards | Optimize queries and reduce time ranges |
| **Storage issues** | Running out of disk space | Implement proper retention and cleanup policies |

### Diagnostic Commands
```bash
# Check logging services
systemctl status rsyslog
systemctl status systemd-journald
journalctl -xe

# Verify log file permissions
ls -la /var/log/
lsof /var/log/syslog

# Check monitoring services
systemctl status prometheus
systemctl status grafana-server
systemctl status node_exporter

# Monitor resource usage
iostat -x 1
free -h
df -h

# Network connectivity tests
nc -zv logserver.example.com 514
telnet prometheus-server 9090
```

## Assessment Criteria

### Technical Proficiency (40%)
- **Configuration Accuracy**: Correct implementation of logging and monitoring configurations
- **Security Implementation**: Proper security controls and access management
- **Performance Optimization**: Efficient resource utilization and optimization
- **Integration Capabilities**: Successful integration between different monitoring components

### Problem-Solving Skills (30%)
- **Troubleshooting Methodology**: Systematic approach to identifying and resolving issues
- **Root Cause Analysis**: Ability to identify underlying causes of problems
- **Creative Solutions**: Innovative approaches to monitoring and alerting challenges
- **Preventive Measures**: Implementation of proactive monitoring and alerting

### Documentation and Communication (20%)
- **Technical Documentation**: Clear, comprehensive documentation of configurations and procedures
- **Runbook Quality**: Detailed operational procedures and troubleshooting guides
- **Knowledge Transfer**: Ability to explain complex concepts and procedures
- **Best Practices Application**: Demonstration of industry best practices

### Automation and Innovation (10%)
- **Process Automation**: Implementation of automated monitoring and response procedures
- **Custom Solutions**: Development of custom monitoring scripts and tools
- **Continuous Improvement**: Ongoing optimization and enhancement of monitoring systems
- **Future Planning**: Consideration of scalability and future requirements

## Next Steps
With comprehensive logging and monitoring mastered, you're ready to explore Shell Scripting Fundamentals in Module 9, where you'll automate system administration tasks with powerful shell scripts that integrate with the monitoring and logging infrastructure you've built.
