# Metrics Monitoring

## Dashboard

The Grafana dashboard is available at [disqt.com/metrics](https://disqt.com/metrics).

- **Public access**: Read-only dashboards are available without login.
- **Admin access**: Login required for editing dashboards and configuring data sources.

## Stack

| Component | Version | Port | Purpose |
|-----------|---------|------|---------|
| Node Exporter | 1.10.2 | 9100 | System metrics (CPU, RAM, disk, network) |
| Process Exporter | 0.8.7 | 9256 | Per-process CPU and memory metrics |
| Prometheus | 3.9.1 | 9090 | Scrapes exporters, stores time series data |
| Grafana | 12.3.2 | 3000 | Dashboards and visualization |

All components are installed as native binaries (no Docker).

## Data Flow

```
Exporters (9100, 9256)  -->  Prometheus (9090)  -->  Grafana (3000)  -->  nginx  -->  Browser
                              (15s scrape)            (dashboards)       (/metrics/)
```

- Prometheus scrapes exporters every **15 seconds**.
- Data retention is **30 days**.
- All components bind to **localhost only**; Grafana is exposed through the nginx reverse proxy at `/metrics/`.

## Directory Structure

```
/home/dev/metrics/
  bin/                          # node_exporter, process-exporter, prometheus, promtool
  prometheus/prometheus.yml     # Scrape configuration
  prometheus/data/              # Time series storage (30-day retention)
  process-exporter/config.yml   # Process name matchers
  grafana/                      # Grafana data (database, provisioning)
  grafana-dist/                 # Grafana distribution (binaries + assets)
  grafana.ini                   # Grafana configuration
```

## Tracked Processes

The Process Exporter monitors the following services:

| Process | Match Method |
|---------|-------------|
| CS2 | comm: `cs2` |
| Minecraft | cmdline: `.*paper\.jar.*` |
| Xonotic | cmdline: `.*xonotic.*` |
| Discord bot | cmdline: `.*bot\.py.*` |
| lgsm-info-api | cmdline: `.*lgsm-info-api.*` |
| miaro-scheduler-api | cmdline: `.*miaro.*` |
| nginx | comm: `nginx` |
| Prometheus | comm: `prometheus` |
| Grafana | comm: `grafana` |

!!! note
    `comm` matches the binary name (first 15 characters of `/proc/PID/comm`). `cmdline` uses regex against the full command line. When both are specified, both must match (AND logic).

## Service Management

All monitoring components run as systemd services:

```bash
sudo systemctl restart node-exporter
sudo systemctl restart process-exporter
sudo systemctl restart prometheus
sudo systemctl restart grafana
```
