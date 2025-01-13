
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






scrape_duration_seconds



https://sbcode.net/prometheus/delete-timeseries/
