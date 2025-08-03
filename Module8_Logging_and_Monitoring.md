# Module 8: Logging & Monitoring

## Table of Contents
- [Overview](#overview)
- [Learning Objectives](#learning-objectives)
- [Topics](#topics)
  - [8.1 System Logging Fundamentals](#81-system-logging-fundamentals)
  - [8.2 rsyslog Configuration](#82-rsyslog-configuration)
  - [8.3 systemd Journal (journald)](#83-systemd-journal-journald)
  - [8.4 Log Rotation and Management](#84-log-rotation-and-management)
  - [8.5 Resource Monitoring Fundamentals](#85-resource-monitoring-fundamentals)
  - [8.6 Prometheus and Node Exporter](#86-prometheus-and-node-exporter)
  - [8.7 Grafana Visualization](#87-grafana-visualization)
  - [8.8 Centralized Logging Solutions](#88-centralized-logging-solutions)
- [Command & Tool Reference](#command--tool-reference)
- [Practical Examples](#practical-examples)
- [Advanced Monitoring Solutions](#advanced-monitoring-solutions)
- [Custom Monitoring Scripts](#custom-monitoring-scripts)
- [Best Practices Summary](#best-practices-summary)
- [Lab Exercises](#lab-exercises)
- [Next Steps](#next-steps)

## Overview
Collect, rotate, analyze, and visualize system logs and metrics to maintain visibility and proactively address issues. This module covers comprehensive logging and monitoring strategies for Linux systems, from basic log management to enterprise-grade monitoring solutions with Prometheus, Grafana, and centralized logging platforms.

**Key Focus Areas:**
- System logging: `/var/log/` hierarchy, `rsyslog`/`syslog-ng`, and `journalctl`
- Log rotation: `logrotate` configuration files in `/etc/logrotate.d/`
- Resource monitoring: `top`/`htop`, `vmstat`, `iostat`, `free`, `df`, `du`
- Metrics export: Prometheus `node_exporter` and custom exporters
- Visualization and alerting: Grafana dashboards and Prometheus Alertmanager
- Centralized logging options: ELK stack (Elasticsearch, Logstash, Kibana) or Fluentd/Graylog

## Learning Objectives
By the end of this module, you will be able to:
1. **Query and filter systemd logs** with `journalctl` for specific services or timeframes
2. **Configure `logrotate` policies** to compress, rotate, and purge old log files automatically
3. **Deploy and configure Prometheus `node_exporter`** on Linux hosts for metrics collection
4. **Build Grafana dashboards** to display CPU, memory, disk, and network metrics with alerting
5. **Define Prometheus alerting rules** and route notifications through Alertmanager
6. **Explore centralized logging solutions** and forward logs securely over TLS
7. **Implement comprehensive monitoring strategies** for production environments
8. **Analyze logs for troubleshooting** and security event correlation

## Topics

### 8.1 System Logging Fundamentals
- Understanding the `/var/log/` hierarchy and log file organization
- Syslog protocol, facilities, and severity levels
- rsyslog vs syslog-ng vs journald comparison
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

## Command & Tool Reference

| Tool/Command | Purpose | Key Options |
|--------------|---------|-------------|
| `journalctl -u <service>` | Show logs for specific systemd service | `-f` (follow), `-n` (lines), `--since` (time) |
| `journalctl -f` | Follow new log entries in real time | `--lines=50` (show last 50 lines) |
| `journalctl --since "1 hour ago"` | Query logs by timeframe | `--until`, `-b` (since boot) |
| `tail -F /var/log/syslog` | Continuously follow a log file | `-n` (lines), `-f` (follow) |
| `logrotate /etc/logrotate.conf --debug` | Test logrotate configurations | `--force` (force rotation) |
| `free -h` | Display human-readable memory usage | `-s` (interval), `-c` (count) |
| `vmstat 5` | Virtual memory/CPU stats every 5 seconds | `-a` (active/inactive), `-s` (summary) |
| `iostat -xz 1` | Extended I/O statistics per second | `-c` (CPU), `-d` (disk), `-p` (partition) |
| `htop` | Interactive process viewer | `F6` (sort), `F4` (filter), `F9` (kill) |
| `iotop` | Real-time I/O usage by process | `-o` (only active), `-a` (accumulated) |
| `node_exporter --web.listen-address=":9100"` | Expose host metrics to Prometheus | `--collector.*` (enable/disable collectors) |
| `grafana-cli plugins install <plugin-id>` | Install Grafana plugins | `list`, `update`, `remove` |
| `promtool check rules alert.rules.yml` | Validate Prometheus alerting rules | `check config`, `query` |
| `systemctl status rsyslog` | Check rsyslog service status | `restart`, `reload`, `enable` |
| `logger "test message"` | Send test message to syslog | `-p` (priority), `-t` (tag) |
| `lsof +D /var/log` | Show processes using log directory | `-p` (PID), `-u` (user) |

## Practical Examples

### Basic rsyslog Configuration

#### Standard rsyslog.conf Structure
```bash
# /etc/rsyslog.conf

# Global directives
$ModLoad imuxsock # provides support for local system logging
$ModLoad imklog   # provides kernel logging support
$ModLoad imjournal # provides access to systemd journal

# Include all config files in /etc/rsyslog.d/
$IncludeConfig /etc/rsyslog.d/*.conf

# Standard log file destinations
kern.*                                           /var/log/kern.log
auth,authpriv.*                                  /var/log/auth.log
mail.*                                           /var/log/mail.log
daemon.*                                         /var/log/daemon.log
user.*                                           /var/log/user.log
local0,local1,local2,local3,local4,local5,local6,local7.*    /var/log/local.log

# Emergency messages to all users
*.emerg                                          :omusrmsg:*

# Critical messages to console
*.crit                                           /dev/console

# Debug messages to separate file
*.debug                                          /var/log/debug.log
```

### Advanced rsyslog Configuration

#### Custom Filtering and Remote Logging
```bash
# /etc/rsyslog.d/50-custom.conf

# High precision timestamps
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat

# Filter by program name
:programname, isequal, "nginx" /var/log/nginx-rsyslog.log
& stop

# Filter by message content
:msg, contains, "Failed password" /var/log/failed-logins.log
& stop

# Filter by facility and severity
mail.info /var/log/mail-info.log
mail.warn /var/log/mail-warn.log
mail.err  /var/log/mail-error.log

# Remote logging (UDP)
*.* @log-server.example.com:514

# Remote logging (TCP with compression)
*.* @@log-server.example.com:514

# Secure remote logging (TLS)
$DefaultNetstreamDriver gtls
$DefaultNetstreamDriverCAFile /etc/ssl/certs/ca-cert.pem
$DefaultNetstreamDriverCertFile /etc/ssl/certs/client-cert.pem
$DefaultNetstreamDriverKeyFile /etc/ssl/private/client-key.pem
$ActionSendStreamDriverAuthMode x509/name
$ActionSendStreamDriverPermittedPeer log-server.example.com
$ActionSendStreamDriverMode 1
*.* @@log-server.example.com:6514
```

### Remote Logging Configuration

#### Server-side Configuration
```bash
# /etc/rsyslog.d/10-remote.conf (Log Server)

# Enable UDP reception
$ModLoad imudp
$UDPServerRun 514
$UDPServerAddress 0.0.0.0

# Enable TCP reception
$ModLoad imtcp
$InputTCPServerRun 514

# Template for remote logs
$template RemoteLog,"/var/log/remote/%HOSTNAME%/%programname%.log"
*.* ?RemoteLog
& stop

# Separate remote logs by date
$template DynFile,"/var/log/remote/%HOSTNAME%/%$YEAR%-%$MONTH%-%$DAY%.log"
*.* ?DynFile
```

### journald Configuration

#### Comprehensive journald Setup
```bash
# /etc/systemd/journald.conf
[Journal]
# Storage configuration
Storage=persistent
Compress=yes
Seal=yes
SplitMode=uid

# Rate limiting
RateLimitInterval=30s
RateLimitBurst=10000
SyncIntervalSec=5m

# Size and retention limits
SystemMaxUse=4G
SystemKeepFree=1G
SystemMaxFileSize=128M
SystemMaxFiles=100
RuntimeMaxUse=1G
RuntimeKeepFree=100M
RuntimeMaxFileSize=64M
RuntimeMaxFiles=50

# Retention policies
MaxRetentionSec=1month
MaxFileSec=1week

# Forward to syslog
ForwardToSyslog=yes
ForwardToKMsg=no
ForwardToConsole=no
ForwardToWall=yes

# Additional options
MaxLevelStore=debug
MaxLevelSyslog=info
MaxLevelKMsg=notice
MaxLevelConsole=info
MaxLevelWall=emerg
```

### journalctl Usage Examples

#### Advanced journalctl Queries
```bash
# Basic log viewing
journalctl                              # Show all entries
journalctl -e                           # Jump to end
journalctl -r                           # Reverse chronological order

# Service-specific logs
journalctl -u nginx.service            # Specific service
journalctl -u nginx.service -f         # Follow service logs
journalctl -u nginx.service --since today

# Time-based queries
journalctl --since "2024-01-01 00:00:00"
journalctl --since "1 hour ago"
journalctl --since yesterday --until now
journalctl --since "30 min ago" --until "20 min ago"

# Boot-specific logs
journalctl -b                          # Current boot
journalctl -b -1                       # Previous boot
journalctl --list-boots                # List all boots

# Priority filtering
journalctl -p err                      # Error level and above
journalctl -p warning..err             # Warning to error range
journalctl -p 0..3                     # Emergency to error (numeric)

# Field-based filtering
journalctl _UID=1000                   # Specific user
journalctl _PID=1234                   # Specific process
journalctl _COMM=nginx                 # Specific command
journalctl _SYSTEMD_UNIT=nginx.service

# Kernel messages
journalctl -k                          # Kernel messages only
journalctl -k --since "10 min ago"

# Output formats
journalctl -o json                     # JSON format
journalctl -o json-pretty              # Pretty JSON
journalctl -o verbose                  # All fields
journalctl -o cat                      # Messages only

# Search and grep
journalctl | grep "error"
journalctl -u nginx.service | grep "404"

# Journal maintenance
sudo journalctl --vacuum-time=2d       # Keep last 2 days
sudo journalctl --vacuum-size=1G       # Keep last 1GB
sudo journalctl --vacuum-files=10      # Keep last 10 files
sudo journalctl --verify               # Verify integrity
```

### Log Rotation Configuration

#### Standard Log Rotation Policies
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
    sharedscripts
    postrotate
        if [ -f /var/run/nginx.pid ]; then
            kill -USR1 `cat /var/run/nginx.pid`
        fi
    endscript
}

# /etc/logrotate.d/apache2
/var/log/apache2/*.log {
    weekly
    missingok
    rotate 52
    compress
    delaycompress
    notifempty
    create 640 root adm
    sharedscripts
    postrotate
        if /bin/systemctl status apache2 > /dev/null ; then \
            /bin/systemctl reload apache2 > /dev/null; \
        fi;
    endscript
}

# /etc/logrotate.d/rsyslog
/var/log/syslog {
    rotate 7
    daily
    missingok
    notifempty
    delaycompress
    compress
    postrotate
        /usr/lib/rsyslog/rsyslog-rotate
    endscript
}

# Custom application logs
/var/log/myapp/*.log {
    size 100M
    rotate 5
    compress
    delaycompress
    copytruncate
    notifempty
    missingok
}

# Test and debug logrotate
sudo logrotate -d /etc/logrotate.conf          # Debug mode
sudo logrotate -f /etc/logrotate.conf          # Force rotation
sudo logrotate -v /etc/logrotate.d/nginx       # Verbose mode
```

### Custom Log Management

#### Advanced Log Cleanup Script
```bash
#!/bin/bash
# advanced-log-cleanup.sh

LOG_DIR="/var/log"
RETENTION_DAYS=30
SIZE_LIMIT="1G"
EMAIL="admin@example.com"

# Function to log actions
log_action() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> /var/log/log-cleanup.log
}

# Clean old logs
find $LOG_DIR -type f -name "*.log" -mtime +$RETENTION_DAYS -exec rm -f {} \;
log_action "Cleaned logs older than $RETENTION_DAYS days"

# Compress large logs
find $LOG_DIR -type f -name "*.log" -size +$SIZE_LIMIT -exec gzip {} \;
log_action "Compressed logs larger than $SIZE_LIMIT"

# Check disk usage
USAGE=$(df $LOG_DIR | awk 'NR==2 {print $5}' | sed 's/%//')
if [ $USAGE -gt 85 ]; then
    echo "WARNING: Log directory usage is ${USAGE}%" | mail -s "Log Disk Usage Alert" $EMAIL
    log_action "Disk usage alert sent: ${USAGE}%"
fi

# Generate summary report
echo "Log cleanup completed on $(date)" | mail -s "Log Cleanup Report" $EMAIL
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

### Node Exporter Deployment

#### Installing and Configuring Node Exporter
```bash
# Download and install node_exporter
cd /tmp
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
tar xzf node_exporter-1.6.1.linux-amd64.tar.gz
sudo mv node_exporter-1.6.1.linux-amd64/node_exporter /usr/local/bin/

# Create node_exporter user
sudo useradd --no-create-home --shell /bin/false node_exporter

# Create systemd service
sudo tee /etc/systemd/system/node_exporter.service << EOF
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter \
    --web.listen-address=:9100 \
    --collector.systemd \
    --collector.processes \
    --collector.diskstats.ignored-devices="^(ram|loop|fd|(h|s|v|xv)d[a-z]|nvme\\d+n\\d+p)\\d+$"
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
EOF

# Enable and start service
sudo systemctl daemon-reload
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
sudo systemctl status node_exporter

# Test metrics endpoint
curl http://localhost:9100/metrics | head -20
```

### Prometheus Configuration

#### Complete Prometheus Setup
```yaml
# /etc/prometheus/prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    monitor: 'production'

# Load alerting rules
rule_files:
  - "/etc/prometheus/alert_rules.yml"
  - "/etc/prometheus/node_rules.yml"

# Scrape configuration
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
    scrape_interval: 5s

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']
    scrape_interval: 15s
    metrics_path: /metrics

  - job_name: 'nginx-exporter'
    static_configs:
      - targets: ['localhost:9113']
    scrape_interval: 30s

  - job_name: 'mysql-exporter'
    static_configs:
      - targets: ['localhost:9104']
    scrape_interval: 30s

# Alerting configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - localhost:9093
      scheme: http
      timeout: 10s
```

#### Prometheus Alert Rules
```yaml
# /etc/prometheus/alert_rules.yml
groups:
  - name: system_alerts
    rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage detected"
          description: "CPU usage is above 80% for more than 5 minutes on {{ $labels.instance }}"

      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100 > 85
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage detected"
          description: "Memory usage is above 85% for more than 5 minutes on {{ $labels.instance }}"

      - alert: DiskSpaceLow
        expr: (node_filesystem_size_bytes - node_filesystem_free_bytes) / node_filesystem_size_bytes * 100 > 90
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "Disk space is running low"
          description: "Disk usage is above 90% on {{ $labels.instance }} filesystem {{ $labels.mountpoint }}"

      - alert: NodeDown
        expr: up == 0
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "Node is down"
          description: "{{ $labels.instance }} has been down for more than 1 minute"

      - alert: HighLoadAverage
        expr: node_load1 > (count by(instance)(node_cpu_seconds_total{mode="idle"}) * 0.8)
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High load average"
          description: "Load average is high on {{ $labels.instance }}"

# Validate rules
# promtool check rules /etc/prometheus/alert_rules.yml
```

### Grafana Dashboard Configuration

#### System Overview Dashboard
```json
{
  "dashboard": {
    "id": null,
    "title": "System Monitoring Dashboard",
    "tags": ["system", "monitoring"],
    "timezone": "browser",
    "refresh": "30s",
    "time": {
      "from": "now-1h",
      "to": "now"
    },
    "panels": [
      {
        "id": 1,
        "title": "CPU Usage",
        "type": "stat",
        "gridPos": {"h": 8, "w": 6, "x": 0, "y": 0},
        "targets": [
          {
            "expr": "100 - (avg(irate(node_cpu_seconds_total{mode=\"idle\"}[5m])) * 100)",
            "legendFormat": "CPU Usage %"
          }
        ],
        "fieldConfig": {
          "defaults": {
            "thresholds": {
              "steps": [
                {"color": "green", "value": null},
                {"color": "yellow", "value": 70},
                {"color": "red", "value": 85}
              ]
            }
          }
        }
      },
      {
        "id": 2,
        "title": "Memory Usage",
        "type": "stat",
        "gridPos": {"h": 8, "w": 6, "x": 6, "y": 0},
        "targets": [
          {
            "expr": "(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100",
            "legendFormat": "Memory Usage %"
          }
        ]
      },
      {
        "id": 3,
        "title": "Disk Usage",
        "type": "bargauge",
        "gridPos": {"h": 8, "w": 12, "x": 12, "y": 0},
        "targets": [
          {
            "expr": "(node_filesystem_size_bytes - node_filesystem_free_bytes) / node_filesystem_size_bytes * 100",
            "legendFormat": "{{ mountpoint }}"
          }
        ]
      },
      {
        "id": 4,
        "title": "Network Traffic",
        "type": "graph",
        "gridPos": {"h": 8, "w": 24, "x": 0, "y": 8},
        "targets": [
          {
            "expr": "irate(node_network_receive_bytes_total{device!=\"lo\"}[5m])",
            "legendFormat": "{{ device }} - Inbound"
          },
          {
            "expr": "irate(node_network_transmit_bytes_total{device!=\"lo\"}[5m])",
            "legendFormat": "{{ device }} - Outbound"
          }
        ]
      }
    ]
  }
}
```

### Grafana Alerting

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

### ELK Stack Configuration

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

### Secure Log Transport

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

## Best Practices Summary

### Logging Best Practices
| Practice | Description | Implementation |
|----------|-------------|----------------|
| **Centralized Logging** | Aggregate logs from multiple systems | Use rsyslog, Fluentd, or ELK stack |
| **Log Rotation** | Prevent logs from filling disk space | Configure logrotate with appropriate retention |
| **Structured Logging** | Use consistent log formats | Implement JSON or syslog format standards |
| **Security Logging** | Monitor authentication and access events | Enable auth logs, audit trails |
| **Performance Logging** | Track system performance metrics | Log resource usage, response times |
| **Log Integrity** | Protect logs from tampering | Use log signing, secure transport |
| **Retention Policies** | Define how long to keep logs | Balance compliance needs with storage costs |
| **Real-time Analysis** | Monitor logs for immediate issues | Implement alerting and correlation |

### Monitoring Best Practices
| Practice | Description | Implementation |
|----------|-------------|----------------|
| **Comprehensive Metrics** | Monitor all critical system components | CPU, memory, disk, network, services |
| **Baseline Establishment** | Know normal system behavior | Collect historical data for comparison |
| **Proactive Alerting** | Detect issues before they become critical | Set meaningful thresholds and escalation |
| **Visualization** | Make data easy to understand | Use dashboards and graphs effectively |
| **Automation** | Reduce manual monitoring overhead | Implement automated responses where appropriate |
| **Documentation** | Maintain monitoring procedures | Document alert meanings and response procedures |
| **Regular Review** | Continuously improve monitoring | Regularly review and update thresholds |
| **Redundancy** | Ensure monitoring system reliability | Monitor the monitoring systems |

### Security Monitoring Checklist
- [ ] Failed authentication attempts monitoring
- [ ] Privilege escalation detection
- [ ] File integrity monitoring
- [ ] Network intrusion detection
- [ ] Log tampering protection
- [ ] Automated incident response
- [ ] Regular security audit log review
- [ ] Compliance reporting capabilities

### Performance Monitoring Metrics

#### System Level Metrics
| Category | Key Metrics | Normal Ranges | Alert Thresholds |
|----------|-------------|---------------|------------------|
| **CPU** | Load average, utilization, wait time | Load < cores, util < 70% | Load > cores*1.5, util > 85% |
| **Memory** | Usage, available, swap usage | Usage < 80%, minimal swap | Usage > 90%, active swap |
| **Disk** | Space usage, I/O rates, queue depth | Usage < 85%, low queue | Usage > 95%, high I/O wait |
| **Network** | Bandwidth, packet loss, connections | Normal baseline patterns | High loss, unusual traffic |

#### Application Level Metrics
| Category | Key Metrics | Monitoring Tools |
|----------|-------------|------------------|
| **Services** | Availability, response time, error rates | systemctl, custom checks |
| **Databases** | Connection count, query performance, locks | Database-specific exporters |
| **Web Servers** | Request rate, response codes, latency | nginx/apache exporters |
| **Custom Apps** | Business metrics, transaction rates | Application-specific metrics |

## Lab Exercises

### Lab 1: Centralized Logging with rsyslog
**Objective**: Set up centralized logging infrastructure with secure transport.

**Tasks**:
1. Configure rsyslog server to receive logs from multiple clients
2. Set up TLS encryption for secure log transport
3. Implement log filtering and routing based on sources
4. Configure log rotation and retention policies
5. Create custom log analysis scripts
6. Test failover scenarios and log integrity

**Deliverables**:
- Working centralized logging infrastructure
- TLS-secured log transport configuration
- Automated log rotation and cleanup procedures
- Log analysis and reporting scripts
- Documentation of troubleshooting procedures

### Lab 2: Prometheus and Grafana Monitoring Stack
**Objective**: Deploy comprehensive monitoring solution with visualization and alerting.

**Tasks**:
1. Install and configure Prometheus server
2. Deploy node_exporter on multiple systems
3. Create custom exporters for specific applications
4. Build comprehensive Grafana dashboards
5. Configure alerting rules and notification channels
6. Implement alert escalation and on-call procedures

**Deliverables**:
- Complete Prometheus monitoring infrastructure
- Professional Grafana dashboards with alerting
- Custom exporter for specific use case
- Alert rule documentation and response procedures
- Monitoring strategy documentation

### Lab 3: Log Analysis and Security Monitoring
**Objective**: Implement advanced log analysis for security and troubleshooting.

**Tasks**:
1. Set up automated log parsing and correlation
2. Create security event detection rules
3. Implement real-time alerting for security incidents
4. Build log analysis dashboard with key metrics
5. Create automated reporting for compliance
6. Test incident response procedures

**Deliverables**:
- Automated security monitoring system
- Custom log analysis tools and scripts
- Security incident detection and alerting
- Compliance reporting automation
- Incident response playbook

### Lab 4: Custom Monitoring Solution
**Objective**: Design and implement monitoring for specific business requirements.

**Tasks**:
1. Assess monitoring requirements for given scenario
2. Design monitoring architecture and data flow
3. Implement custom monitoring scripts and collectors
4. Create automated alerting and response systems
5. Build executive dashboard for business metrics
6. Document monitoring procedures and maintenance

**Deliverables**:
- Custom monitoring architecture design
- Implemented monitoring solution with automation
- Business metrics dashboard
- Comprehensive documentation
- Training materials for operators

### Lab 5: High Availability Monitoring Infrastructure
**Objective**: Design resilient monitoring infrastructure for production environments.

**Tasks**:
1. Design highly available logging and monitoring architecture
2. Implement redundancy and failover mechanisms
3. Set up monitoring for the monitoring infrastructure
4. Create backup and disaster recovery procedures
5. Test failure scenarios and recovery procedures
6. Optimize performance for large-scale environments

**Deliverables**:
- High availability architecture design
- Implemented redundant monitoring infrastructure
- Disaster recovery procedures and testing results
- Performance optimization documentation
- Operational runbooks for maintenance

## Troubleshooting Common Issues

### Logging Issues
```bash
# Check log file permissions and ownership
ls -la /var/log/
sudo find /var/log -type f ! -readable -ls

# Verify rsyslog configuration
sudo rsyslog -N1                              # Test configuration
sudo systemctl status rsyslog                 # Check service status
sudo journalctl -u rsyslog                    # Check service logs

# Test log generation
logger "Test message from $(whoami)"
tail -f /var/log/syslog | grep "Test message"

# Check journal status and integrity
sudo systemctl status systemd-journald
sudo journalctl --verify                      # Verify journal integrity
sudo journalctl --disk-usage                  # Check disk usage

# Monitor log rotation
sudo logrotate -d /etc/logrotate.conf         # Debug logrotate
sudo cat /var/lib/logrotate/status            # Check rotation status
```

### Monitoring Issues
```bash
# Check Prometheus targets
curl http://localhost:9090/api/v1/targets

# Verify node_exporter metrics
curl http://localhost:9100/metrics | grep node_cpu

# Check Grafana connectivity
sudo systemctl status grafana-server
sudo journalctl -u grafana-server

# Monitor system performance
top -b -n 1 | head -20                        # System snapshot
vmstat 1 5                                    # System activity
iostat -x 1 5                                 # Disk I/O
free -h                                       # Memory usage

# Check disk space and inodes
df -h                                          # Disk space
df -i                                          # Inode usage
```

### Performance Optimization
```bash
# Optimize journal performance
sudo tee -a /etc/systemd/journald.conf << EOF
RateLimitInterval=0
SyncIntervalSec=1s
EOF

# Optimize rsyslog performance
sudo tee -a /etc/rsyslog.conf << EOF
\$MainMsgQueueSize 50000
\$MainMsgQueueTimeoutEnqueue 0
\$MainMsgQueueType LinkedList
\$MainMsgQueueSaveOnShutdown on
EOF

# Monitor monitoring overhead
top -p $(pgrep -d',' prometheus)              # Prometheus CPU usage
iotop -p $(pgrep prometheus)                  # Prometheus I/O usage
```

## Next Steps
With comprehensive logging and monitoring mastered, you're ready to explore Shell Scripting Fundamentals in Module 9, where you'll automate system administration tasks with powerful shell scripts that integrate with the monitoring and logging infrastructure you've built.
