---
title: Service Discovery and API Gateways
menu_order: 7
post_status: publish
post_excerpt: Learn how services find and talk to each other in production using discovery mechanisms and gateways.
taxonomy:
  category:
    - microservices
  post_tag:
    - service discovery
    - api gateway
    - load balancing
    - envoy
    - consul
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [What Is Service Discovery?](#what-is-service-discovery)
- [Static vs Dynamic Discovery](#static-vs-dynamic-discovery)
- [Using a Service Registry](#using-a-service-registry)
- [What Is an API Gateway?](#what-is-an-api-gateway)
- [Popular Tools](#popular-tools)
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

## What Is Service Discovery?

In a microservice system, services often come and go dynamically (due to auto-scaling, deployments, or failures). So…  
**how does Service A know how to reach Service B?**

**Service discovery** solves this by allowing services to register themselves and query other services dynamically.

---

## Static vs Dynamic Discovery

### 🔹 Static Discovery

- IPs or URLs are hardcoded
- Simple, but fragile and not scalable

### 🔹 Dynamic Discovery

- Services **register themselves** on startup
- Others **query** the registry to get healthy instances

Example:

```
Service A → DNS / registry → find Service B's IPs → connect
```

---

## Using a Service Registry

A **service registry** keeps track of live service instances and their metadata (e.g., version, zone, port).

Popular tools:

- 🔸 **Consul** (by HashiCorp)
- 🔸 **Eureka** (by Netflix)
- 🔸 **Etcd** (used by Kubernetes)
- 🔸 **Zookeeper** (legacy systems)

Services register and deregister automatically.

---

## What Is an API Gateway?

An **API Gateway** sits in front of your services and:

- Routes traffic to the right service
- Enforces authentication and rate limits
- Performs logging, caching, and load balancing
- Can transform requests/responses (e.g., GraphQL → REST)

It’s your **central access point**.

Example:

```
Client → API Gateway → routes to UserService or OrderService
```

---

## Popular Tools

| Tool        | Type                | Description                                 |
| ----------- | ------------------- | ------------------------------------------- |
| **Kong**    | API Gateway         | Plugin-based, high performance              |
| **Envoy**   | Proxy + Discovery   | Modern L7 proxy, built-in service discovery |
| **NGINX**   | Reverse Proxy       | Can serve as a simple gateway               |
| **Istio**   | Service Mesh        | Adds policy, security, routing, telemetry   |
| **Traefik** | Gateway + Discovery | Dynamic config with Docker/Kubernetes       |

Use gateways to centralize concerns — but avoid turning them into **monolith bottlenecks**.

---

## Summary

Microservices rely on **dynamic service discovery** to stay flexible and resilient. API gateways help manage traffic, security, and monitoring across all services. Together, they keep your distributed system connected and reliable.

---

Next:  
**Lesson 08 – Service Mesh: Traffic Management, Observability, and Security**

</div>
