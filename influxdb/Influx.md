# influxdb
influxdb is used to provide a datasource for grafana

## Installation
Create the required dirs and users
```
sudo groupadd influx
sudo useradd influx -g influx -s /usr/sbin/nologin
sudo mkdir -p /opt/influx/bin
sudo chown -R influx:influx /opt/influx
```

Download [influxdb](https://docs.influxdata.com/influxdb/v2.0/get-started/#start-with-influxdb-oss)
```
curl -O https://dl.influxdata.com/influxdb/releases/influxdb_2.0.0-beta.16_linux_arm64.tar.gz
```

Install influx to /opt/influx
```
tar -xzf influxdb_2.0.0-beta.16_linux_arm64.tar.gz
sudo -u influx cp influxdb_2.0.0-beta.16_linux_arm64/influx* /opt/influx/bin/

rm influxdb_2.0.0-beta.16_linux_arm64*
```
