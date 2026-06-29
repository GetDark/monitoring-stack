[English](#english) | [Русский](#русский)

---

<a name="english"></a>
# monitoring-stack

Production-ready monitoring stack in Docker Compose: metrics, logs, alerts, and dashboards — all pre-configured and ready to run.

## Stack

| Service | Version | Purpose | Port |
|---------|---------|---------|------|
| Prometheus | v2.53.0 | Metrics collection & storage | 9090 |
| Grafana | 11.1.0 | Dashboards & visualization | 3000 |
| Loki | v3.1.0 | Log aggregation | 3100 |
| Promtail | v3.1.0 | Log shipping from host & Docker | — |
| node-exporter | v1.8.1 | Host system metrics | 9100 |
| Alertmanager | v0.27.0 | Alert routing & notifications | 9093 |

All ports are bound to `127.0.0.1` — expose externally via nginx reverse proxy.

## Quick Start

```bash
git clone https://github.com/GetDark/monitoring-stack.git
cd monitoring-stack

cp .env.example .env
nano .env  # set GRAFANA_PASSWORD and GRAFANA_ROOT_URL

docker compose up -d
```

## Features

- **30-day** Prometheus data retention
- Pre-provisioned Grafana datasources (Prometheus + Loki)
- Dashboard auto-provisioning via `grafana/provisioning/`
- Alert rules in `prometheus/rules/alerts.yml`
- Promtail collects both `/var/log` and Docker container logs

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `GRAFANA_USER` | `admin` | Grafana admin username |
| `GRAFANA_PASSWORD` | `changeme` | Grafana admin password |
| `GRAFANA_ROOT_URL` | `http://localhost:3000` | Grafana public URL |

---

<a name="русский"></a>
# monitoring-stack

Production-ready стек мониторинга в Docker Compose: метрики, логи, алерты и дашборды — всё преднастроено и готово к запуску.

## Стек

| Сервис | Версия | Назначение | Порт |
|--------|--------|-----------|------|
| Prometheus | v2.53.0 | Сбор и хранение метрик | 9090 |
| Grafana | 11.1.0 | Дашборды и визуализация | 3000 |
| Loki | v3.1.0 | Агрегация логов | 3100 |
| Promtail | v3.1.0 | Отправка логов с хоста и Docker | — |
| node-exporter | v1.8.1 | Системные метрики хоста | 9100 |
| Alertmanager | v0.27.0 | Маршрутизация и отправка алертов | 9093 |

Все порты привязаны к `127.0.0.1` — проксировать наружу через nginx.

## Быстрый старт

```bash
git clone https://github.com/GetDark/monitoring-stack.git
cd monitoring-stack

cp .env.example .env
nano .env  # задать GRAFANA_PASSWORD и GRAFANA_ROOT_URL

docker compose up -d
```

## Возможности

- Хранение данных Prometheus **30 дней**
- Предварительно настроенные источники данных Grafana (Prometheus + Loki)
- Автоматическое добавление дашбордов через `grafana/provisioning/`
- Правила алертов в `prometheus/rules/alerts.yml`
- Promtail собирает логи из `/var/log` и Docker-контейнеров

## Переменные окружения

| Переменная | По умолчанию | Описание |
|------------|-------------|----------|
| `GRAFANA_USER` | `admin` | Имя пользователя Grafana |
| `GRAFANA_PASSWORD` | `changeme` | Пароль администратора Grafana |
| `GRAFANA_ROOT_URL` | `http://localhost:3000` | Публичный URL Grafana |
