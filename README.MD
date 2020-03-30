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
# Document title of Prometheus instance.
    web_page_title: 'Prometheus Time Series Collection and Processing Server'
# Regex for CORS origin. It is fully anchored.
# Example: 'https?://(domain1|domain2)\.com'
    web_cors_origin: '.*'
# Base path for metrics storage.
    storage_tsdb_path: 'data/'
# How long to retain samples in storage. Defaults to 15d. Units supported:
# y, w, d, h, m, s, ms.
    storage_tsdb_retention_time: '15d'
# Maximum number of bytes that can be stored for blocks. Units supported:
# KB, MB, GB, TB, PB. This flag is experimental and can be changed in future
# releases.
    storage_tsdb_retention_size: '100GB'
# Do not create lockfile in data directory.
    storage_tsdb_no_lockfile: 'false'
# Allow overlapping blocks, which in turn enables vertical compaction and
# vertical query merge.
    storage_tsdb_allow_overlapping_blocks: 'false'
# Compress the tsdb WAL.
    storage_tsdb_wal_compression: 'false'
# How long to wait flushing sample on shutdown or config reload.
    storage_remote_flush_deadline: ''
# Maximum overall number of samples to return via the remote read interface, in
# a single query. '0' means no limit. This limit is ignored for streamed
# response types.
    storage_remote_read_sample_limit: '5e7'
# Maximum number of concurrent remote read calls. 0 means no limit.
    storage_remote_read_concurrent_limit: '10'
# Maximum number of bytes in a single frame for streaming remote read response
# types before marshalling. Note that client might have limit on frame size as
# well. 1MB as recommended by protobuf by default.
    storage_remote_read_max_bytes_in_frame: '1048576'  
# Max time to tolerate prometheus outage for restoring "for" state of alert.
    rules_alert_for_outage_tolerance: '1h'  
# Minimum duration between alert and restored "for" state. This is maintained
# only for alerts with configured "for" time greater than grace period.
    rules_alert_for_grace_period: '10m'  
# Minimum amount of time to wait before resending an alert to Alertmanager.
    rules_alert_resend_delay: '1m'  
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
# Maximum number of samples a single query can load into memory. Note that
# queries will fail if they try to load more samples than this into memory, so
# this also limits the number of samples a query can return.
    query_max_samples: '50000000'
# Only log messages with the given severity or above.
# One of: debug, info, warn, error.
    log_level: 'info'
# Output format of log messages. One of: 'logfmt' or 'json'.
    log_format: 'logfmt'
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
