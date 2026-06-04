# Detrudr Deployment Documentation

**Detrudr** is a traffic anomaly detection and DDoS counter engine that has been deployed on the
**FitCall(Personal Trainer)** project. It operates as a host-level security daemon that sits
alongside Nginx to provide real-time security monitoring and automated threat mitigation.

The opensource project code for the Detrudr project can be found here:
[https://github.com/Okpainmo/detrudr](https://github.com/Okpainmo/detrudr)

## Overview

Detrudr tails Nginx JSON access logs in real time, learns rolling request baselines, and detects
suspicious traffic spikes. Key features include:

- **Anomaly Detection:** Real-time learning of request baselines.

- **DDoS Countering:** Optional blocking of abusive source IPs using `iptables`.

- **Auditing & Notifications:** Writes a durable audit trail and sends alerts via Slack.

- **Live Dashboard:** Provides a web-based interface for operators to monitor the provided metrics
  and traffic statistics.

## Purposes

The deployment on the FitCall project server serves three primary functions:

1. **Security:** Automated DDoS countering and IP blocking.

2. **Traffic Anomaly Detection:** Identifying irregular patterns in incoming requests.

3. **Monitoring:** Real-time visibility into server health and traffic distribution.

## Infrastructure

The daemon runs on port `8090` and is deployed behind Nginx.

- **Admin Access:** All requests made to the server's base IP (`http://16.170.96.186`) are proxied
  to the Detrudr daemon on port `8090` for administrative access and monitoring.
- **Nginx Config:** A dedicated virtual host configuration named `detrudr` handles the proxying.

## Nginx configuration

Detrudr requires a specific JSON log format to parse traffic data accurately. This format must be
declared within the `http` block of the global Nginx configuration:

```nginx
log_format detrudr_json escape=json '{'
    '"source_ip":"$remote_addr",'
    '"timestamp":"$time_iso8601",'
    '"method":"$request_method",'
    '"path":"$request_uri",'
    '"status":$status,'
    '"response_size":$body_bytes_sent'
'}';
```

## Deployment and persistence

Following the project's requirements to avoid Docker, the **direct binary deployment** method was
used. The process is managed and persisted using `systemd`.

### Service management

The system service is named `detrudr`. You can manage it using the following commands:

- **Check status:**

  ```bash
  sudo systemctl status detrudr
  ```

  _Expected outcome: The output should show `Active: active (running)` and the most recent log
  entries._

- **Restart service:**
  ```bash
  sudo systemctl restart detrudr
  ```

## Configuration files

The deployment relies on the following configuration and environment files:

- **Main Configuration:** `/etc/detrudr/config.yaml`
- **Environment Variables:** `/etc/detrudr/secrets.env` (contains Slack webhooks and other sensitive
  data)
