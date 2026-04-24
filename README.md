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
# 📈 Grafana – Visualization & Monitoring Dashboard

<p align="center">
<img src="https://skillicons.dev/icons?i=grafana" width="120">
</p>

<p align="center">

![Grafana](https://img.shields.io/badge/Grafana-Monitoring-orange?logo=grafana)
![DevOps](https://img.shields.io/badge/DevOps-Observability-blue)
![Dashboards](https://img.shields.io/badge/Dashboards-Visualization-green)
![Metrics](https://img.shields.io/badge/Metrics-Alerting-red)

</p>

---

# 📌 What is Grafana?

Grafana is an **open-source analytics and monitoring platform** used to:

- Visualize metrics from multiple data sources (Prometheus, InfluxDB, Elasticsearch, CloudWatch, etc.)
- Create interactive dashboards
- Set up alerts on specific metrics
- Track application, server, and infrastructure performance

It is widely used in DevOps for **observability and monitoring**.

---

# 🚀 Why Grafana is Used

Manual monitoring lacks visibility and centralization. Grafana provides:

- Centralized dashboards for metrics
- Real-time visualization of system and application data
- Integration with Prometheus, Loki, and other data sources
- Alerting for threshold breaches
- Customizable, interactive dashboards

Benefits:

- Open-source and extensible
- Supports multiple data sources
- Real-time monitoring
- Powerful visualizations
- Alerts & notifications

---

# 🏗 Grafana Architecture

```
+-------------------+
| Data Sources       |
| Prometheus, Loki,  |
| InfluxDB, Cloud    |
| Monitoring         |
+---------+---------+
          │ Query Metrics
          ▼
+---------+---------+
|    Grafana        |
|    Dashboard      |
|    Visualization  |
+---------+---------+
          │
          ▼
+---------+---------+
| Alerts & Notification |
| Slack, Email, Webhook |
+----------------------+
```

Components:

- **Data Sources** – Prometheus, InfluxDB, ElasticSearch, MySQL, CloudWatch
- **Grafana Server** – Runs dashboards & queries
- **Dashboards** – Visualization panels
- **Alerting** – Send notifications when metrics breach thresholds

---

# ⚡ Installation (Ubuntu)

Add Grafana repository:

```bash
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install grafana
```

Start Grafana:

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

Access UI:

```
http://localhost:3000
```

Default login:

- Username: `admin`
- Password: `admin`

---

# 📂 Adding Data Sources

Steps:

1. Open Grafana web UI
2. Go to **Configuration → Data Sources**
3. Click **Add data source**
4. Select type (e.g., Prometheus)
5. Configure URL (e.g., `http://localhost:9090`)
6. Save & Test

---

# 📊 Creating Dashboards

1. Go to **Dashboard → New Dashboard**
2. Add **Panels**
3. Choose **Visualization** (Graph, Gauge, Table, etc.)
4. Select **Metric query** from data source
5. Customize panel with labels, thresholds, and units
6. Save dashboard

---

# 🧩 Panels & Visualizations

| Panel Type | Use Case |
|------------|----------|
| Graph | Time-series metrics |
| Gauge | Single-value metrics with thresholds |
| Table | Tabular data visualization |
| Heatmap | Density or frequency analysis |
| Stat | Highlight single metric value |
| Logs | Visualize logs from Loki or ElasticSearch |

---

# 🔔 Alerting in Grafana

1. Configure alert rules for panels
2. Set **conditions** (e.g., CPU > 80%)
3. Define **notification channels** (Slack, Email, Webhook)
4. Receive real-time alerts

Example alert condition:

```
WHEN avg() OF query(A, 5m, now) IS ABOVE 80
```

---

# 🌿 Integration with Prometheus

- Prometheus collects metrics
- Grafana queries Prometheus using PromQL
- Dashboards visualize metrics in real-time
- Alerts can be triggered from Prometheus or Grafana

---

# 🧰 Grafana Use Cases in DevOps

- Monitor Kubernetes cluster (CPU, memory, pods)
- Visualize Docker container metrics
- Track application performance
- Monitor cloud resources (AWS, Azure, GCP)
- Set up automated alerts for incidents
- Build dashboards for CI/CD pipelines

---

# 🌟 Grafana Best Practices

- Group dashboards by service or application
- Use variables for dynamic dashboards
- Use panels wisely for meaningful visualization
- Secure Grafana UI with authentication & roles
- Integrate with Prometheus for metrics and Loki for logs
- Use alerting to reduce downtime and incidents

---

# 🎯 Interview Definition

**Grafana is an open-source visualization and monitoring platform that allows DevOps engineers to create interactive dashboards, visualize metrics from multiple data sources, and set up alerts for monitoring applications, infrastructure, and cloud resources.**

---

