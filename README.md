# Monitoring Stack with Prometheus, Node Exporter and Grafana



A simple local monitoring stack built using Docker Compose.



This project collects system metrics using Node Exporter, stores and queries them using Prometheus, and displays them using Grafana.



\---



## 📌 Project Overview



The monitoring stack contains three main components:



1\. \*\*Node Exporter\*\* – provides system metrics.

2\. \*\*Prometheus\*\* – collects and stores the metrics.

3\. \*\*Grafana\*\* – displays the metrics using dashboards.



Everything runs locally using Docker Compose.



\---



## 🏗️ Architecture



```text

+-------------------+

|   Node Exporter   |

|      :9100        |

+---------+---------+

&#x20;         |

&#x20;         | Metrics

&#x20;         v

+-------------------+

|    Prometheus     |

|      :9090        |

+---------+---------+

&#x20;         |

&#x20;         | PromQL

&#x20;         v

+-------------------+

|      Grafana      |

|      :3000        |

+-------------------+

&#x20;         |

&#x20;         v

&#x20;  System Dashboard



Data Flow

Node Exporter

&#x20;     ↓

Prometheus

&#x20;     ↓

PromQL Queries

&#x20;     ↓

Grafana Dashboard



🛠️ Technologies Used

\- Docker

\- Docker Compose

\- Prometheus

\- Node Exporter

\- Grafana

\- PromQL

\- Git

\- GitHub



📁 Project Structuremonitoring-stack/

│

├── dashboards/

│   └── system-overview.json

│

├── docker-compose.yml

├── prometheus.yml

├── README.md

└── .gitignore



🐳 Docker Compose

The docker-compose.yml file runs three containers:

Node Exporter

Port: 9100



Prometheus

Port: 9090



Grafana

Port: 3000



Start the complete stack using:

docker compose up -d



Check running containers:

docker ps



Stop the stack:

docker compose down



🔎 Prometheus Configuration

Prometheus is configured in:

prometheus.yml



Scrape interval:

scrape\_interval: 15s



Prometheus collects metrics from:

prometheus:9090

node\_exporter:9100



📊 Grafana Dashboard

The project contains a dashboard named:

System overview



Dashboard file:

dashboards/system-overview.json



The dashboard contains:

\- CPU Usage

\- Memory Usage

\- Disk Usage

\- Network Traffic

\- System Uptime

\- Targets Up



s📈 PromQL Queries

CPU Usage

100 - (avg(rate(node\_cpu\_seconds\_total{mode="idle"}\[5m])) \* 100)



Memory Usage

(1 - node\_memory\_MemAvailable\_bytes / node\_memory\_MemTotal\_bytes) \* 100



Disk Usage

(1 - node\_filesystem\_avail\_bytes{mountpoint="/",fstype="ext4"} / node\_filesystem\_size\_bytes{mountpoint="/",fstype="ext4"}) \* 100



Network Receive

rate(node\_network\_receive\_bytes\_total{device="eth0"}\[5m])



Network Transmit

rate(node\_network\_transmit\_bytes\_total{device="eth0"}\[5m])



System Uptime

time() - node\_boot\_time\_seconds



Targets Up

sum(up)



🌐 Access the Services

After starting Docker Compose:

Grafana

http://localhost:3000



Prometheus

http://localhost:9090



Prometheus Targets

http://localhost:9090/targets



Node Exporter Metrics

http://localhost:9100/metrics



✅ Testing

The monitoring stack was tested by:

1\. Starting all containers using Docker Compose.

2\. Checking that all three containers are running.

3\. Opening Prometheus.

4\. Checking Prometheus targets.

5\. Confirming Prometheus and Node Exporter targets are UP.

6\. Connecting Grafana to Prometheus.

7\. Running PromQL queries.

8\. Confirming CPU, memory, disk, network and uptime data appears in Grafana.

9\. Saving the Grafana dashboard.

10\. Validating the exported dashboard JSON.



🔄 Node Exporter Failure Test

Node Exporter availability was tested by stopping the exporter and checking the Prometheus up metric.



Expected behavior:

Node Exporter running:

up = 1



Node Exporter stopped:

up = 0



After starting Node Exporter again:

up = 1



This confirms that Prometheus detects the availability of the target.



🔀 Git Workflow

The project uses feature branches:

main

│

├── feature/node-exporter

├── feature/prometheus-config

├── feature/grafana-datasource

└── feature/system-dashboard



The repository was initialized locally using Git and connected to GitHub.



Remote repository:

SG-Intern/monitoring-stack



Feature branches were pushed to GitHub before merging into the main development branch.



🔐 Security

The project does not store passwords, tokens or other secrets in the repository.



The .gitignore file excludes:

.env

.env.\*

\*.log

\_\_pycache\_\_/

\*.pyc



🎯 Learning Outcomes

Through this project, the following concepts were practiced:

\- Docker Compose

\- Container networking

\- Prometheus configuration

\- Metrics collection

\- PromQL

\- Node Exporter

\- Grafana data sources

\- Grafana dashboards

\- Git branches

\- GitHub repository management

\- Monitoring and troubleshooting



⚠️ Important Note

This setup is designed for local learning and development.



The Dockerized Node Exporter configuration monitors the environment available to the Node Exporter container. It should not be treated as a complete Windows host monitoring solution.



For dedicated Windows host monitoring, a Windows-specific exporter can be used.





🚀 Final Result

The final monitoring stack provides a simple local monitoring environment:

Docker Compose

&#x20;     ↓

Node Exporter

&#x20;     ↓

Prometheus

&#x20;     ↓

Grafana

&#x20;     ↓

System Monitoring Dashboard

The project demonstrates how metrics can be collected, stored, queried and visualized using a modern monitoring stack.


