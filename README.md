# monitoring-stack

Production-ready observability stack on Docker Compose: **Prometheus + Grafana + Loki + Promtail + node_exporter + Alertmanager**.

## Stack

| Service | Port | Purpose |
|---------|------|---------|
| Prometheus | 9090 | Metrics collection & storage |
| Grafana | 3000 | Dashboards & visualization |
| Loki | 3100 | Log aggregation |
| Promtail | — | Log shipper (Docker + syslog) |
| node_exporter | 9100 | Host metrics (CPU, RAM, disk) |
| Alertmanager | 9093 | Alert routing (Telegram, email) |

## Quick Start

```bash
cp .env.example .env
# edit .env — set passwords and Telegram token
docker compose up -d
```

Grafana opens at `http://localhost:3000` (admin / your password).  
Datasources (Prometheus, Loki) and dashboard folder are provisioned automatically.

## Alert channels

Alertmanager is pre-configured for **Telegram** and **email** (SMTP).  
Set `TELEGRAM_BOT_TOKEN` and `TELEGRAM_CHAT_ID` in `.env`, alerts go there on critical events.

Built-in alert rules:
- CPU > 85% for 5m
- RAM > 90% for 5m
- Disk < 15% free
- Any target `up == 0` for 1m
- HTTP 5xx error rate > 5%

## nginx reverse proxy (optional)

```nginx
location /grafana/ {
    proxy_pass http://127.0.0.1:3000/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

## Scraping your app

Add to `prometheus/prometheus.yml` under `scrape_configs`:

```yaml
- job_name: myapp
  static_configs:
    - targets: [myapp:8000]
  metrics_path: /metrics
```
