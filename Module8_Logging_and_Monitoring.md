# Module 8: Logging & Monitoring

## Overview
This module covers comprehensive logging and monitoring strategies for Linux systems. You'll learn to configure system logging, implement monitoring solutions, set up alerting, and analyze system performance and security events.

## Learning Objectives
By the end of this module, you will be able to:
- Configure and manage system logging with rsyslog and journald
- Implement comprehensive monitoring solutions
- Set up alerting and notification systems
- Analyze logs for troubleshooting and security
- Monitor system performance and resource usage
- Create custom monitoring scripts and dashboards

## Topics

### 8.1 System Logging Fundamentals
- Understanding syslog protocol and facilities
- Log levels and priorities
- rsyslog vs journald
- Log rotation and retention
- Centralized logging concepts

### 8.2 rsyslog Configuration
- rsyslog.conf structure and syntax
- Filtering and routing logs
- Remote logging setup
- Custom log formats
- Performance tuning

### 8.3 systemd Journal (journald)
- Journal storage and configuration
- Querying logs with journalctl
- Persistent vs volatile storage
- Journal forwarding to syslog
- Journal maintenance

### 8.4 Log Analysis and Troubleshooting
- Log file locations and organization
- Text processing tools for log analysis
- Common log patterns and signatures
- Automated log parsing
- Security event correlation

### 8.5 System Monitoring
- Performance metrics and KPIs
- Monitoring tools: top, htop, iostat, vmstat
- Process and resource monitoring
- Network monitoring
- Disk and filesystem monitoring

### 8.6 Advanced Monitoring Solutions
- Nagios/Icinga monitoring
- Zabbix implementation
- Prometheus and Grafana stack
- ELK stack (Elasticsearch, Logstash, Kibana)
- Custom monitoring scripts

## Practical Examples

### rsyslog Configuration

#### Basic rsyslog.conf
```bash
# /etc/rsyslog.conf

# Global directives
$ModLoad imuxsock # provides support for local system logging
$ModLoad imklog   # provides kernel logging support

# Include all config files in /etc/rsyslog.d/
$IncludeConfig /etc/rsyslog.d/*.conf

# Log all kernel messages to kern.log
kern.*                                           /var/log/kern.log

# Log authentication messages
auth,authpriv.*                                  /var/log/auth.log

# Log mail system messages
mail.*                                           /var/log/mail.log

# Emergency messages to all users
*.emerg                                          :omusrmsg:*

# Critical messages to console
*.crit                                           /dev/console
```

#### Advanced rsyslog Configuration
```bash
# Custom log filtering
# /etc/rsyslog.d/50-custom.conf

# Filter by program name
:programname, isequal, "nginx" /var/log/nginx-rsyslog.log
& stop

# Filter by message content
:msg, contains, "Failed password" /var/log/failed-logins.log
& stop

# Remote logging
*.* @@log-server.example.com:514

# Log to database
$ModLoad ommysql
*.* :ommysql:localhost,Syslog,rsyslog,password

# High precision timestamps
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat
```

### journald Configuration
```bash
# /etc/systemd/journald.conf
[Journal]
Storage=persistent
Compress=yes
Seal=yes
SplitMode=uid
SyncIntervalSec=5m
RateLimitInterval=30s
RateLimitBurst=1000
SystemMaxUse=4G
SystemKeepFree=1G
SystemMaxFileSize=128M
RuntimeMaxUse=1G
MaxRetentionSec=1month
```

### journalctl Usage Examples
```bash
# Show all journal entries
journalctl

# Show entries since last boot
journalctl -b

# Show entries for specific service
journalctl -u nginx.service

# Follow log in real-time
journalctl -f

# Show entries from last hour
journalctl --since "1 hour ago"

# Show entries between specific times
journalctl --since "2024-01-01" --until "2024-01-02"

# Show only error messages
journalctl -p err

# Show kernel messages
journalctl -k

# Show logs for specific user
journalctl _UID=1000

# Export logs in JSON format
journalctl -o json --since today

# Clear old logs (keep last 2 days)
sudo journalctl --vacuum-time=2d

# Verify journal integrity
sudo journalctl --verify
```

### Log Analysis Tools

#### Using grep and awk
```bash
# Find failed SSH login attempts
grep "Failed password" /var/log/auth.log

# Count failed attempts per IP
grep "Failed password" /var/log/auth.log | \
    awk '{print $(NF-3)}' | sort | uniq -c | sort -nr

# Find large files in logs
find /var/log -type f -size +100M -exec ls -lh {} \;

# Parse Apache access logs
awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -nr

# Extract specific time range
awk '/Jan 15 09:/ && /Jan 15 10:/' /var/log/syslog
```

#### Log Rotation Configuration
```bash
# /etc/logrotate.d/nginx
/var/log/nginx/*.log {
    daily
    missingok
    rotate 52
    compress
    delaycompress
    notifempty
    create 644 nginx nginx
    postrotate
        if [ -f /var/run/nginx.pid ]; then
            kill -USR1 `cat /var/run/nginx.pid`
        fi
    endscript
}

# Test logrotate configuration
sudo logrotate -d /etc/logrotate.conf

# Force log rotation
sudo logrotate -f /etc/logrotate.conf
```

## System Monitoring

### Performance Monitoring Commands
```bash
# CPU monitoring
top
htop
vmstat 1 5
iostat -c 1 5
sar -u 1 5

# Memory monitoring
free -h
vmstat -s
cat /proc/meminfo
ps aux --sort=-%mem | head

# Disk I/O monitoring
iostat -x 1 5
iotop
lsof +D /path/to/directory

# Network monitoring
netstat -i
ss -s
iftop
nload

# Process monitoring
ps auxf
pstree
lsof -p PID
strace -p PID
```

### System Resource Scripts
```bash
#!/bin/bash
# system-monitor.sh

# System monitoring script
echo "=== System Monitor Report ==="
echo "Date: $(date)"
echo

# CPU Load
echo "CPU Load:"
uptime
echo

# Memory Usage
echo "Memory Usage:"
free -h
echo

# Disk Usage
echo "Disk Usage:"
df -h
echo

# Top Processes by CPU
echo "Top CPU Processes:"
ps aux --sort=-%cpu | head -6
echo

# Top Processes by Memory
echo "Top Memory Processes:"
ps aux --sort=-%mem | head -6
echo

# Network Connections
echo "Network Connections:"
ss -s
```

## Advanced Monitoring Solutions

### Prometheus Configuration
```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'nginx'
    static_configs:
      - targets: ['localhost:9113']

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - localhost:9093
```

### Grafana Dashboard Configuration
```json
{
  "dashboard": {
    "title": "System Monitoring",
    "panels": [
      {
        "title": "CPU Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "100 - (avg(irate(node_cpu_seconds_total{mode=\"idle\"}[5m])) * 100)"
          }
        ]
      },
      {
        "title": "Memory Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100"
          }
        ]
      }
    ]
  }
}
```

### Nagios Host Configuration
```bash
# /etc/nagios/objects/servers.cfg
define host {
    use                     linux-server
    host_name               web-server-01
    alias                   Web Server 01
    address                 192.168.1.100
    check_command           check-host-alive
    max_check_attempts      5
    check_period            24x7
    notification_interval   30
    notification_period     24x7
}

define service {
    use                     generic-service
    host_name               web-server-01
    service_description     HTTP
    check_command           check_http
    notifications_enabled   1
}
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

## Log Management Best Practices

| Practice | Description |
|----------|-------------|
| Centralized Logging | Aggregate logs from multiple systems |
| Log Rotation | Prevent logs from filling disk space |
| Retention Policies | Define how long to keep logs |
| Security Logging | Monitor authentication and access events |
| Performance Logging | Track system performance metrics |
| Alerting | Set up notifications for critical events |
| Regular Analysis | Review logs proactively |

## Monitoring Metrics to Track

| Category | Metrics |
|----------|---------|
| CPU | Load average, CPU utilization, wait time |
| Memory | Usage, available, swap usage |
| Disk | Space usage, I/O rates, queue depth |
| Network | Bandwidth, packet loss, connections |
| Services | Availability, response time, error rates |
| Security | Failed logins, privilege escalations |

## Troubleshooting Common Issues

### Log Issues
```bash
# Check log file permissions
ls -la /var/log/

# Verify rsyslog is running
systemctl status rsyslog

# Test log generation
logger "Test message"

# Check journal status
systemctl status systemd-journald

# Verify disk space
df -h /var/log
```

### Performance Issues
```bash
# Check system load
uptime
cat /proc/loadavg

# Identify resource-heavy processes
top -o %CPU
top -o %MEM

# Check I/O wait
iostat -x 1 5

# Monitor real-time activity
htop
iotop
```

## Lab Exercises
1. Configure centralized logging with rsyslog
2. Set up Prometheus and Grafana monitoring
3. Create custom monitoring scripts with alerting
4. Implement log analysis and reporting
5. Design a comprehensive monitoring strategy

## Next Steps
With logging and monitoring skills mastered, you're ready to explore Shell Scripting Fundamentals in Module 9, where you'll automate system administration tasks with powerful shell scripts.
