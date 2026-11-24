# Monitoring Stack with Prometheus, Node Exporter and Grafana

A simple local monitoring stack built using Docker Compose.

This project collects system metrics using Node Exporter, stores and queries them using Prometheus, and displays them using Grafana.

---

## 📌 Project Overview

The monitoring stack contains three main components:

1. **Node Exporter** - provides system metrics.
2. **Prometheus** - collects and stores the metrics.
3. **Grafana** - displays the metrics using dashboards.

Everything runs locally using Docker Compose.

---

## 🏗️ Architecture

```text
+-------------------+
|   Node Exporter   |
|      :9100        |
+---------+---------+
          |
          | Metrics
          v
+-------------------+
|    Prometheus     |
|      :9090        |
+---------+---------+
          |
          | PromQL
          v
+-------------------+
|      Grafana      |
|      :3000        |
+---------+---------+
          |
          v
   System Dashboard
```

### Data Flow

```text
Node Exporter
      |
      v
Prometheus
      |
      v
PromQL Queries
      |
      v
Grafana Dashboard
```

---

## 🛠️ Technologies Used

- Docker
- Docker Compose
- Prometheus
- Node Exporter
- Grafana
- PromQL
- Git
- GitHub

---

## 📁 Project Structure

```text
monitoring-stack/
|
+-- dashboards/
|   +-- system-overview.json
|
+-- docker-compose.yml
+-- prometheus.yml
+-- README.md
+-- .gitignore
```

---

## 🐳 Docker Compose

The `docker-compose.yml` file runs three containers.

### Node Exporter

```text
Port: 9100
```

### Prometheus

```text
Port: 9090
```

### Grafana

```text
Port: 3000
```

Start the complete stack:

```powershell
docker compose up -d
```

Check running containers:

```powershell
docker ps
```

Stop the stack:

```powershell
docker compose down
```

---

## 🔎 Prometheus Configuration

Prometheus is configured in:

```text
prometheus.yml
```

Scrape interval:

```yaml
scrape_interval: 15s
```

Prometheus collects metrics from:

```text
prometheus:9090
node_exporter:9100
```

---

## 📊 Grafana Dashboard

The project contains a dashboard named:

```text
System overview
```

Dashboard file:

```text
dashboards/system-overview.json
```

The dashboard contains:

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic
- System Uptime
- Targets Up

---

## 📈 PromQL Queries

### CPU Usage

```promql
100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

### Memory Usage

```promql
(1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes) * 100
```

### Disk Usage

```promql
(1 - node_filesystem_avail_bytes{mountpoint="/",fstype="ext4"} / node_filesystem_size_bytes{mountpoint="/",fstype="ext4"}) * 100
```

### Network Receive

```promql
rate(node_network_receive_bytes_total{device="eth0"}[5m])
```

### Network Transmit

```promql
rate(node_network_transmit_bytes_total{device="eth0"}[5m])
```

### System Uptime

```promql
time() - node_boot_time_seconds
```

### Targets Up

```promql
sum(up)
```

---

## 🌐 Access the Services

### Grafana

```text
http://localhost:3000
```

### Prometheus

```text
http://localhost:9090
```

### Prometheus Targets

```text
http://localhost:9090/targets
```

### Node Exporter Metrics

```text
http://localhost:9100/metrics
```

---

## ✅ Testing

The monitoring stack was tested by:

1. Starting all containers using Docker Compose.
2. Checking that all three containers are running.
3. Opening Prometheus.
4. Checking Prometheus targets.
5. Confirming Prometheus and Node Exporter targets are UP.
6. Connecting Grafana to Prometheus.
7. Running PromQL queries.
8. Confirming CPU, memory, disk, network and uptime data appears in Grafana.
9. Saving the Grafana dashboard.
10. Validating the exported dashboard JSON.

---

## 🔄 Node Exporter Failure Test

Node Exporter availability was tested by stopping the exporter and checking the Prometheus `up` metric.

Expected behavior:

```text
Node Exporter running:
up = 1

Node Exporter stopped:
up = 0
```

After starting Node Exporter again:

```text
up = 1
```

This confirms that Prometheus detects the availability of the target.

---

## 🔀 Git Workflow

The project uses feature branches:

```text
main
|
+-- feature/node-exporter
+-- feature/prometheus-config
+-- feature/grafana-datasource
+-- feature/system-dashboard
```

The repository was initialized locally using Git and connected to GitHub.

Remote repository:

```text
SG-Intern/monitoring-stack
```

Feature branches were created and pushed to GitHub.

---

## 🔐 Security

The project does not store passwords, tokens or other secrets in the repository.

The `.gitignore` file excludes:

```text
.env
.env.*
*.log
__pycache__/
*.pyc
```

---

## 🎯 Learning Outcomes

Through this project, the following concepts were practiced:

- Docker Compose
- Container networking
- Prometheus configuration
- Metrics collection
- PromQL
- Node Exporter
- Grafana data sources
- Grafana dashboards
- Git branches
- GitHub repository management
- Monitoring and troubleshooting

---

## ⚠️ Important Note

This setup is designed for local learning and development.

The Dockerized Node Exporter configuration monitors the environment available to the Node Exporter container. It should not be treated as a complete Windows host monitoring solution.

For dedicated Windows host monitoring, a Windows-specific exporter can be used.

---

## 🚀 Final Result

The final monitoring stack provides a simple local monitoring environment.

```text
Docker Compose
      |
      v
Node Exporter
      |
      v
Prometheus
      |
      v
Grafana
      |
      v
System Monitoring Dashboard
```

The project demonstrates how metrics can be collected, stored, queried and visualized using a modern monitoring stack.
