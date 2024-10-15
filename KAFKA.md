# Kafka

# Install Kafka

# Install Prometheus

Visit https://prometheus.io/download/ for latest version of prometheus

Change to a directory where to download the binary
```
cd ~/Download
```

For version 2.51.1 and Macos
```
curl -O 'https://github.com/prometheus/prometheus/releases/download/v2.51.1/prometheus-2.51.1.darwin-amd64.tar.gz'
```

Choose a directory where to install the application. For example:
```
cd /usr/local/bin
```

Unpack the application
```
sudo tar -zxf ~/Downloads/prometheus-2.51.1.darwin-amd64.tar.gz
```

Change ownership of application files
```
sudo chown -R root:wheel prometheus-2.51.1.darwin-amd64
```

Create a symbolic link 
```
sudo ln -s /usr/local/bin/prometheus-2.51.1.darwin-amd64 /opt/prometheus
```

## Node exporter
Node Exporter is used to export metrics that Prometheus can scrape

Download the application
```
curl -O 'https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.darwin-amd64.tar.gz'
```

```
cd /usr/local/bin
```

```
sudo tar -zxf ~/Downloads/node_exporter-1.7.0.darwin-amd64.tar.gz
```


```
sudo chown -R root:wheel node_exporter-1.7.0.darwin-amd64
```

```
sudo ln -s /usr/local/bin/node_exporter-1.7.0.darwin-amd64 /opt/node_exporter
```

### Start up node exporter 
```
cd /opt/node_exporter
./node_exporter
```

### Test the service is up
```
curl http://localhost:9100/metrics
```

# Install Grafana

Download latest version of Grafana
```
curl -O https://dl.grafana.com/enterprise/release/grafana-enterprise-10.4.1.darwin-amd64.tar.gz
```

Change to install directory
```
cd /usr/local/bin
```

Unpack the application
```
sudo tar -zxf ~/Downloads/grafana-enterprise-10.4.1.darwin-amd64.tar.gz
```

Create symbolic link
```
sudo ln -s /usr/local/bin/grafana-v10.4.1 /opt/grafana
```
## Run Prometheus
```
cd /opt/prometheus/
./prometheus
```
## Run Grafana

cd /opt/grafana/
./grafana-server

## Edit prometheus.yaml

Add Node Exporter to prometheus by updating prometheus.yml with:
```
  - job_name: "Node Exporter"
    scrape_interval: 5s
    static_configs:
      - targets: ["localhost:9100"]
```

## Restart prometheus

Update 01
