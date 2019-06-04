# ansible-prometheus

Deploy [Prometheus](//prometheus.io/) monitoring system and time series
database.

## Requirements

* Ansible 2.8+;

## Extra

Configuration pass as-is from yaml to pretty yaml with validation via promtool.


## Example configuration

```yaml
---
prometheus:
# Enable prometheus service or not.
- enable: 'true'
# Restart prometheus service after deploy or not.
  restart: 'true'
# Install prometheus package or not.
  install_package: 'true'
# Startup options.
  options:
# Prometheus configuration file path.
  - config_file: 'prometheus.yml'
# Address to listen on for UI, API, and telemetry.
    web_listen_address: '0.0.0.0:9090'
# Maximum duration before timing out read of the request, and closing idle
# connections.
    web_read_timeout: '5m'
# Maximum number of simultaneous connections.
    web_max_connections: '512'
# The URL under which Prometheus is externally reachable (for example, if
# Prometheus is served via a reverse proxy). Used for generating relative and
# absolute links back to Prometheus itself. If the URL has a path portion, it
# will be used to prefix all HTTP endpoints served by Prometheus. If omitted,
# relevant URL components will be derived automatically.
    web_external_url: ''
# Prefix for the internal routes of web endpoints. Defaults to path of
# 'web_external_url'.
    web_route_prefix: ''
# Path to static asset directory, available at '/user'.
    web_user_assets: ''
# Enable shutdown and reload via HTTP request.
    web_enable_lifecycle: 'false'
# Enable API endpoints for admin control actions.
    web_enable_admin_api: 'true'
# Path to the console template directory, available at '/consoles'.
    web_console_templates: 'consoles'
# Path to the console library directory.
    web_console_libraries: 'console_libraries'
# Base path for metrics storage.
    storage_tsdb_path: 'data/'
# How long to retain samples in storage.
    storage_tsdb_retention: '15d'
# Do not create lockfile in data directory.
    storage_tsdb_no_lockfile: 'false'
# How long to wait flushing sample on shutdown or config reload.
    storage_remote_flush_deadline: ''
# The capacity of the queue for pending Alertmanager notifications.
    alertmanager_notification_queue_capacity: '10000'
# Timeout for sending alerts to Alertmanager.
    alertmanager_timeout: '10s'
# The delta difference allowed for retrieving metrics during expression evaluations.
    query_lookback_delta: '5m'
# Maximum time a query may take before being aborted.
    query_timeout: '2m'
# Maximum number of queries executed concurrently.
    query_max_concurrency: '20'
# Only log messages with the given severity or above.
# One of: debug, info, warn, error.
    log_level: 'info'
  settings:
    global:
      scrape_interval: 15s
      evaluation_interval: 15s
    scrape_configs:
    - job_name: 'example'
      static_configs:
      - targets:
        - '192.168.1.1:9283'
```
