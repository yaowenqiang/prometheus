
# install

> apt install prometheus

> localhost:9090/metrics
> localhost:9100/metrics # Node Exporter


> service prometheus status

> service prometheus-node-exporter status

> ps -u prometheus
apt install prometheus-node-exporter
apt install nginx


> vim /etc/prometheus/prometheus.yml

> promtool check config /etc/prometheus/prometheus.yml


promQl
promQl{job="node"}
node_cpu_seconds_total{mode=~"irq"}

## Data types

+ Scalar 1,0, 0.1234
+ Instent vector  scrape_duration_seconds{instance="localhost:9100"}
+ Range Vector 

node_netstat_Tcp_InSegs{instance="localhost:9100"}[5m]
node_netstat_Tcp_InSegs{instance="localhost:9100"}[5m:15s]
rate(node_netstat_Tcp_InSegs{instance="localhost:9100"}[5m:15s])

rate(node_netstat_Tcp_InSegs[5m])

sum(go_threads)

deriv(ceil(rate(node_netstat_Tcp_InSegs{instance="localhost:9100"}[1m]))[1m:])



https://prometheus.io/docs/prometheus/latest/querying/functions/


## Recording Rules

vim /etc/prometheus/prometheus_rules.yml
```yml

groups:
  - name: custom_rules
    rules:
      - record: node_memory_MemFree_percent
        expr: 100 - (100 * node_memory_MemFree_bytes / node_memory_MemTotal_bytes)
      - record: node_filesystem_free_percent
        expr: 100 * node_filesystem_free_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"}

```

vim /etc/prometheus/prometheus.yml

add prometheus_rules.yml to the rules section 

promtool check rules prometheus_rules.yml


promtool check prometheus.yml








scrape_duration_seconds



https://sbcode.net/prometheus/delete-timeseries/


## Alert rules


```yml
  - name: alert_rules
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 1m
        labels:
            severity: critical
        annotations:
            summary: 'Instance {{ $labels.instance }} down'
            description: '{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 1 minute.'

```
## Alert Manager

apt install prometheus-alertmanager

```yml

route:
    receiver: smtp
receivers:
    - name: smtp
      email_configs:
          - smarthost: mail.your-email-service-domain:port
            hello: your-email-service-domain
            to: 'to@example.com'
            from: 'from@example.com'
            auth_username: 'from@example.com'
            auth_password: 'your-password'
            send_resolved: true
            require_tls: false


```

## Grafana

sudo apt-get install -y adduser libfontconfig1 musl
wget https://dl.grafana.com/oss/release/grafana_11.4.0_amd64.deb
sudo dpkg -i grafana_11.4.0_amd64.deb


sudo /bin/systemctl start grafana-server

local address

localhost:3000

admin
admin


## install dashboards

dashboard id : 11074

中文版本: 8919

