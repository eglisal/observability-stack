#  Observability Stack: Prometheus + Grafana + Loki

This repository provides a **ready-to-use observability stack** built with Docker Compose.  
It integrates **Prometheus** for metrics, **Loki** for logs, and **Grafana** for dashboards and alerts — giving you a local sandbox to explore observability beyond basic monitoring.  

 This project is part of a broader **Observability Series** published on [TechOpsGuide](https://www.techopsguide.com/).  
Check out the blog for articles that combine theory, practice, and real-world DevOps insights.  

---

##  Why This Stack?

- **Monitoring = detecting symptoms.**  
- **Observability = understanding causes.**  

Traditional monitoring only tells you *that something is wrong*.  
Observability tells you *why*.  

This stack implements two of the **three pillars of observability**:  

-  **Metrics** → Prometheus collects and queries system metrics.  
-  **Logs** → Loki ingests logs and makes them queryable with LogQL.  
-  **Dashboards + Alerts** → Grafana visualizes metrics & logs together, and manages alerts.  

---

##  Quick Start

### 1. Prerequisites
- [Docker](https://docs.docker.com/get-docker/) installed  
- [Docker Compose](https://docs.docker.com/compose/install/) available  
- Free ports:  
  - `3000` → Grafana  
  - `9090` → Prometheus  
  - `3100` → Loki  

### 2. Clone the Repo
```bash
git clone https://github.com/your-org/observability-stack.git
cd observability-stack
```

### 3. Start the Stack
```bash
docker-compose up -d
```

### 4. Access the Services
- **Prometheus** → [http://localhost:9090](http://localhost:9090)  
- **Grafana** → [http://localhost:3000](http://localhost:3000)  
  - Default login: `admin / admin`  
- **Loki** → [http://localhost:3100](http://localhost:3100)  

---

##  Configuration

### Prometheus (`prometheus.yml`)
Basic self-scraping job is included:
```yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]
```

Extend this file to add exporters (Node Exporter, SQL Exporter, etc).  

---

##  First Steps in Grafana

1. Log in to Grafana at [http://localhost:3000](http://localhost:3000).  
2. Add Prometheus as a data source:  
   ```
   URL: http://prometheus:9090
   ```  
3. Add Loki as a data source:  
   ```
   URL: http://loki:3100
   ```  
4. Import dashboard **ID 1860** from Grafana’s community library.  

Now you’ll see both **metrics and logs in one place**.  

---

##  Alerts with Grafana

Grafana includes a **unified alerting system**.  
- Define thresholds in any panel (e.g., latency > 500ms).  
- Grafana continuously evaluates the condition.  
- Alerts can be sent to Slack, Teams, email, PagerDuty, and more.  

---

##  Troubleshooting

 **Grafana → Prometheus connection refused**  
- If Grafana is in Docker, set the Prometheus datasource to:  
  ```
  http://prometheus:9090
  ```
  (use the service name, not `localhost`).  

 **Prometheus not responding**  
- Run `docker ps` to confirm the container is up.  
- Check logs:  
  ```bash
  docker logs <prometheus_container>
  ```  

---

##  Next Steps

- Add **Promtail** to ship container or host logs into Loki.  
- Add **Node Exporter** for system metrics.  
- Configure **alerts and SLAs** in Grafana.  
- Explore traces with **Tempo or Jaeger** for full 3-pillar observability.  

---

##  Resources
- [Prometheus Docs](https://prometheus.io/docs/introduction/overview/)  
- [Grafana Docs](https://grafana.com/docs/grafana/latest/)  
- [Loki Docs](https://grafana.com/docs/loki/latest/)  
- [TechOpsGuide Blog](https://www.techopsguide.com/) ← *for related articles and tutorials*  

---

✍️ *Maintained by Eglis Alvarez / TechOpsGuide.com*  
💡 Contributions welcome!  
