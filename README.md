# 📊 Prometheus – Monitoring & Alerting Tool

<p align="center">
<img src="https://skillicons.dev/icons?i=prometheus" width="120">
</p>

<p align="center">

![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-orange?logo=prometheus)
![DevOps](https://img.shields.io/badge/DevOps-Observability-blue)
![Metrics](https://img.shields.io/badge/Metrics-Monitoring-green)
![Alerting](https://img.shields.io/badge/Alerting-Automation-red)

</p>

---

# 📌 What is Prometheus?

Prometheus is an **open-source monitoring and alerting toolkit** widely used in DevOps for:

- Collecting metrics from servers, applications, and services
- Storing metrics as time series data
- Querying metrics using **PromQL**
- Alerting via email, Slack, or custom webhooks
- Integrating with visualization tools like Grafana

---

# 🚀 Why Prometheus is Used

Manual monitoring is inefficient. Prometheus provides:

- Real-time metrics collection
- Powerful query language (PromQL)
- Time-series database for metrics
- Integration with Kubernetes, Docker, and cloud-native apps
- Alerting and notifications

Benefits:

- Open-source & widely adopted
- Scalable monitoring
- Works well with containerized environments
- Flexible data model

---

# 🏗 Prometheus Architecture

```
+-------------------+
|    Target Apps    |
| (Node Exporter,   |
|  App Metrics)     |
+---------+---------+
          │ Pull Metrics
          ▼
+---------+---------+
|   Prometheus      |
|   Server          |
|   TSDB Storage    |
+---------+---------+
          │
          ▼
+---------+---------+
| Alertmanager      |
| (Alerts & Routing)|
+---------+---------+
          │
          ▼
+---------+---------+
| Notification       |
| Channels (Slack,   |
| Email, Webhook)    |
+-------------------+
          │
          ▼
+-------------------+
| Grafana / Dashboard|
+-------------------+
```

Components:

- **Prometheus Server** – Scrapes and stores metrics
- **Exporters** – Applications exposing metrics (Node Exporter, cAdvisor)
- **Alertmanager** – Manages alerts and notifications
- **Time-Series Database** – Stores metrics efficiently
- **Grafana** – Visualization dashboard

---

# ⚡ Installation (Ubuntu)

Add Prometheus user:

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```

Download Prometheus:

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz
tar xvf prometheus-2.46.0.linux-amd64.tar.gz
cd prometheus-2.46.0.linux-amd64
```

Start Prometheus:

```bash
./prometheus --config.file=prometheus.yml
```

Access web UI:

```
http://localhost:9090
```

---

# 📂 Prometheus Configuration (`prometheus.yml`)

Example:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```

Key Points:

- `scrape_interval` – How often metrics are scraped
- `job_name` – Name of the metric job
- `targets` – Endpoints to scrape metrics from

---

# 🧩 Prometheus Exporters

Prometheus collects metrics via exporters:

| Exporter | Purpose |
|----------|---------|
| Node Exporter | Server & OS metrics |
| cAdvisor | Container metrics |
| Blackbox Exporter | Network checks / endpoint monitoring |
| MySQL Exporter | Database metrics |
| Pushgateway | Short-lived jobs metrics |

---

# 🔍 PromQL – Query Language

Prometheus uses **PromQL** to query metrics.

Examples:

- Current CPU usage:

```promql
node_cpu_seconds_total
```

- CPU usage rate:

```promql
rate(node_cpu_seconds_total[5m])
```

- Memory usage percentage:

```promql
100 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100)
```

- Disk usage:

```promql
node_filesystem_avail_bytes / node_filesystem_size_bytes * 100
```

---

# 🔔 Alerting with Alertmanager

Define alert rules (`alert.rules`):

```yaml
groups:
  - name: example-alert
    rules:
      - alert: HighCPUUsage
        expr: node_cpu_seconds_total > 80
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "CPU usage is above 80% for 5 minutes"
          description: "Check server CPU usage."
```

Alertmanager handles:

- Routing alerts
- Deduplication
- Sending notifications (Slack, Email, Webhook)

---

# 📊 Integration with Grafana

- Add Prometheus as a data source in Grafana
- Create dashboards using queries from Prometheus
- Visualize metrics: CPU, Memory, Disk, Network, Application Metrics

---

# 🧰 Prometheus Use Cases in DevOps

- Monitoring Kubernetes clusters
- Monitoring Docker containers
- Server health & metrics tracking
- Alerting on resource thresholds
- Application performance monitoring
- Integrating with CI/CD pipelines for metrics

---

# 🌟 Prometheus Best Practices

- Use node_exporter for system metrics
- Scrape metrics at appropriate intervals (15-30s)
- Use recording rules for heavy queries
- Separate alerting rules from metrics configuration
- Use Grafana dashboards for visualization
- Secure Prometheus endpoints

---

# 🎯 Interview Definition

**Prometheus is an open-source monitoring and alerting toolkit that collects metrics from targets, stores them in a time-series database, and allows querying with PromQL, with integration for alerting and visualization in DevOps environments.**

---
