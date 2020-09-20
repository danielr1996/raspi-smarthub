# Node exporter
Node exporter is used to expose system metrics of the raspi in prometheus format.

###[Install go](https://www.e-tinkers.com/2019/06/better-way-to-install-golang-go-on-raspberry-pi/)

Download go from the [official website](https://golang.org/dl/) (armv6l package). If there is a newer version you might download that newer version.
```
curl -O https://dl.google.com/go/go1.15.2.linux-armv6l.tar.gz
sudo groupadd go
sudo useradd go -g go -s /usr/sbin/nologin
sudo tar -xzf go1.15.2.linux-arvm6l.tar.gz -C /opt
sudo chown -R go:go /opt/go
rm go1.15.2.linux-arvm6l.tar.gz
sudo ln -s /opt/go/bin/go* /opt/bin/
```

### [Build and Install node exporter](https://github.com/prometheus/node_exporter#building-and-running)
Create directories and user/group
```
sudo groupadd node-exporter
sudo useradd node-exporter -g node-exporter -s /usr/sbin/nologin
sudo mkdir -p /opt/node-exporter/bin
sudo chown node-exporter:node-exporter /opt/node-exporter/
```

Build
```
go get github.com/prometheus/node_exporter
cd ${GOPATH-$HOME/go}/src/github.com/prometheus/node_exporter
make
```

Copy to /opt/bin
```
sudo -u node-exporter cp node_exporter /opt/node-exporter/bin/node-exporter
```

Create a systemd service file
```
sudo tee /etc/systemd/system/node-exporter.service <<"EOF"
[Unit]
Description=Node Exporter
Documentation=https://github.com/prometheus/node_exporter#building-and-running
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=node-exporter
Group=node-exporter
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/opt/node-exporter/bin/node-exporter

SyslogIdentifier=node-exporter
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```

Start and enable service with `sudo systemctl start node-exporter && sudo systemctl enable node-exporter`
