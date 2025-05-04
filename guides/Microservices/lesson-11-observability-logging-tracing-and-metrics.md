---
title: Observability – Logging, Tracing, and Metrics
menu_order: 11
post_status: publish
post_excerpt: Make your microservices observable with structured logs, distributed tracing, and actionable metrics.
taxonomy:
  category:
    - microservices
  post_tag:
    - observability
    - logging
    - tracing
    - metrics
    - jaeger
    - prometheus
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Why Observability Is Critical in Microservices](#why-observability-is-critical-in-microservices)
- [Structured Logging](#structured-logging)
- [Distributed Tracing](#distributed-tracing)
- [Service Metrics](#service-metrics)
- [Popular Observability Tools](#popular-observability-tools)
- [Summary](#summary)

</div>

<div class="otg" markdown="1">

## On this Guide

- [Lesson 07: Service Discovery and API Gateways](./lesson-07-service-discovery-and-api-gateways)
- [Lesson 08: Service Mesh – Traffic Management, Observability, and Security](./lesson-08-service-mesh-traffic-management-observability-and-security)
- [Lesson 09: Securing Microservices – Authentication, Authorization, and mTLS](./lesson-09-securing-microservices-authentication-authorization-and-mtls)
- [Lesson 10: Continuous Integration and Deployment for Microservices](./lesson-10-continuous-integration-and-deployment-for-microservices)
- [Lesson 11: Observability – Logging, Tracing, and Metrics](./lesson-11-observability-logging-tracing-and-metrics)
- [Lesson 12: Handling Failures and Timeouts in Microservices](./lesson-12-handling-failures-and-timeouts-in-microservices)

</div>

</div>

<div class="guru-main" markdown="1">

## Why Observability Is Critical in Microservices

In a monolith, a single log might tell you everything.

In microservices, a single user request may pass through 5–10 services.  
To understand what's going on, you need:

- Logs
- Traces
- Metrics

Together, these form the **three pillars of observability**.

---

## Structured Logging

Every service should log **in a structured format** (JSON, not plain text).

### Include:

- `timestamp`
- `service name`
- `request id`
- `log level` (info, warn, error)
- `context` (user ID, order ID, etc.)

Centralize logs in a platform like:

- **ELK Stack** (Elasticsearch + Logstash + Kibana)
- **Loki** (Grafana Labs)
- **Datadog Logs**

```json
{
  "level": "error",
  "service": "user-service",
  "message": "User not found",
  "userId": "abc123",
  "timestamp": "2025-04-30T15:47:00Z"
}
```

---

## Distributed Tracing

Traces show how a request flows across services.

### Use cases:

- Debug latency issues
- Identify bottlenecks
- Spot failed spans across multiple services

Each request carries a **trace ID** and **span ID**.

Popular tools:

- **Jaeger** (open source, CNCF)
- **Zipkin**
- **OpenTelemetry** (standard for instrumentation)
- **Datadog Tracing**

Example flow:

```
Client → API Gateway → OrderService → PaymentService → NotificationService
```

Each service logs a span under the same trace ID.

---

## Service Metrics

Metrics give you **quantitative data** about performance and health.

Examples:

- `http_requests_total`
- `request_duration_seconds`
- `active_db_connections`
- `queue_depth`

Emit custom metrics per service, expose via `/metrics` endpoint, and scrape using:

- **Prometheus** (most popular)
- **Grafana** (for dashboards)
- **Datadog / New Relic / AWS CloudWatch** (hosted)

Use metrics to:

- Trigger alerts
- Set auto-scaling thresholds
- Report SLAs

---

## Popular Observability Tools

| Tool              | Role              | Notes                              |
| ----------------- | ----------------- | ---------------------------------- |
| **Prometheus**    | Metrics collector | Widely adopted, great with K8s     |
| **Grafana**       | Visualization     | Dashboards for metrics and logs    |
| **Jaeger**        | Tracing           | Free, open source, easy to start   |
| **OpenTelemetry** | Standard lib      | One SDK for metrics, logs, tracing |
| **ELK Stack**     | Logging           | Powerful, but resource-intensive   |

---

## Summary

Observability is essential for operating microservices at scale.  
Use structured logs, distributed tracing, and metrics together to detect issues, monitor health, and improve performance.

---

Next:  
**Lesson 12 – Handling Failures and Timeouts in Microservices**

</div>
