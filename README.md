# raspi-smarthub
Raspberry Pi monitoring stack with prometheus and grafana using ansible.

> This is mainly a documentation for me on what to install but it might be useful for someone else too. 

## What you'll get
This installs prometheus and grafana on a Raspberry PI 4 (arm64) with some dashboards (displaying smart plug measures, displaying speedtest results).

To see documentation for each role see `role/<rolename>/README.md`. 

### Prometheus + Pushgateway
Sets up prometheus and pushgateway to scrape metrics and push metrics from bash jobs

### Grafana
Sets up grafana to view the metrics stored in prometheus.

### smartmeter
Sets up a the targets to monitor smart plugs with the tasmota firmware (e.g. sonoff basic)

### speedtest
Sets up speedtest-cli for measuring dsl speed

### node-exporter
Sets up node-exporter to monitor the raspberry pi itself (Currently not yet included in ansible, see `docs/node-exporter/node-exporter.md`)

## Running ansible
```
vagrant up
vagrant ssh
```

```shell script
ansible-playbook -i /vagrant/hosts.yml /vagrant/playbook.yml
```