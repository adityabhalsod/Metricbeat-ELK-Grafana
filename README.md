ELK + Metricbeat + Grafana

This setup provides a minimal local stack using Docker Compose:

Services:
- Elasticsearch 7.17
- Kibana 7.17
- Logstash 7.17
- Metricbeat 7.17 (sends to Logstash)
- Grafana 9 (connected to Elasticsearch)

How to run (from repository root):

```bash
# start
docker-compose up -d

# view logs
docker-compose logs -f

# stop
docker-compose down -v
```

Notes:
- Metricbeat is configured to ship to Logstash on port 5044.
- Logstash ingests beats and writes to Elasticsearch using the index pattern: <beat>-YYYY.MM.DD
- Grafana is provisioned with an Elasticsearch datasource and one simple dashboard located at `/var/lib/grafana/dashboards` inside the container.

Next steps / improvements:
- Add Metricbeat ILM/Template setup to load Kibana dashboards automatically
- Harden security and enable credentials
- Add sample data and more Grafana panels
