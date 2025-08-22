# Metricbeat System Dashboard - Import Instructions

## Dashboard File
The comprehensive Grafana dashboard is located at:
```
metricbeat-system-dashboard.json
```

## How to Import into Grafana

### Method 1: Direct Import (Recommended)
1. Open Grafana in your browser: http://localhost:3000
2. Login with credentials: `admin` / `admin`
3. Click the "+" icon in the left sidebar
4. Select "Import"
5. Click "Upload JSON file" and select `metricbeat-system-dashboard.json`
6. Configure the datasource to use "Elasticsearch" (should be auto-detected)
7. Click "Import"

### Method 2: Copy-Paste
1. Open the `metricbeat-system-dashboard.json` file
2. Copy the entire contents
3. In Grafana, go to "+" → "Import"
4. Paste the JSON content
5. Click "Load" and then "Import"

## Dashboard Features

The dashboard includes 11 panels:

### Time Series Panels
- **CPU Usage**: System CPU utilization percentage
- **Memory Usage**: System memory utilization percentage  
- **Network Traffic**: Network in/out bytes
- **Filesystem Usage**: Filesystem utilization percentage

### Stat Panels
- **Total Processes**: Current number of running processes
- **Load Average (1m)**: System load average over 1 minute
- **Memory Used**: Total memory used in bytes
- **Total Memory**: Total system memory in bytes

### Visualization Panels
- **Disk Usage by Mount Point**: Pie chart showing disk usage per mount point
- **Top Processes by CPU Usage**: Table showing processes consuming most CPU

## Data Requirements

The dashboard expects data from Metricbeat system module with these metricsets:
- `cpu`
- `memory` 
- `network`
- `process`
- `process_summary`
- `filesystem`

## Customization

You can customize the dashboard by:
- Adjusting time ranges (default: last 30 minutes)
- Modifying refresh intervals (default: 10 seconds)
- Adding filters for specific hosts
- Creating variables for dynamic host selection

## Troubleshooting

If panels show "No data":
1. Verify Metricbeat is sending data: `docker-compose logs metricbeat`
2. Check Elasticsearch has metricbeat indices: `curl localhost:9200/_cat/indices`
3. Ensure Grafana datasource is configured correctly
4. Check that the index pattern matches `metricbeat-*`

## Data Source Configuration

The dashboard expects an Elasticsearch datasource named "Elasticsearch" with:
- URL: http://elasticsearch:9200
- Index pattern: `metricbeat-*`
- Time field: `@timestamp`
- Version: 7.x
