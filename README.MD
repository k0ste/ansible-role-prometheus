ansible-prometheus
======================

Deploy [Prometheus](//prometheus.io/) monitoring system and time series
database.

Requirements
---------------

* Ansible 2.2;

Extra
---------

Configuration pass as-is from yaml to pretty yaml with validation via promtool.


Example configuration
-----------------------

```yaml
---
# Enable Prometheus after deploy.
prometheus_enable: 'true'
# Reload Prometheus after deploy.
prometheus_restart: 'true'
# Install Prometheus package.
prometheus_install_package: 'true'

prometheus:
  global:
    scrape_interval: 15s
    evaluation_interval: 15s
  scrape_configs:
  - job_name: 'example'
    static_configs:
    - targets:
      - '192.168.1.1:9283'
```
