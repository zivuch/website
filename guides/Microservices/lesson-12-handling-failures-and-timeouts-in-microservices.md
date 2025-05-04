---
title: Handling Failures and Timeouts in Microservices
menu_order: 12
post_status: publish
post_excerpt: Build fault-tolerant systems with retries, timeouts, circuit breakers, and fallback strategies.
taxonomy:
  category:
    - microservices
  post_tag:
    - resilience
    - timeouts
    - retries
    - circuit breaker
    - fallback
    - failure isolation
---

<div class="toc" markdown="1">

<div class="otp" markdown="1">

## On this Page

- [Failure Is Inevitable](#failure-is-inevitable)
- [Timeouts and Why They Matter](#timeouts-and-why-they-matter)
- [Retries (and Backoff)](#retries-and-backoff)
- [Circuit Breaker Pattern](#circuit-breaker-pattern)
- [Fallback Strategies](#fallback-strategies)
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

## Failure Is Inevitable

In a microservice architecture:

- Networks are unreliable
- Services crash or restart
- Dependencies become temporarily unavailable

Instead of avoiding failure, **design for it**.

---

## Timeouts and Why They Matter

If Service A calls Service B with no timeout:

- A single hanging request could **exhaust threads**
- Latency piles up downstream
- Leads to **cascading failures**

### Set timeouts for:

- HTTP/gRPC calls
- DB queries
- Queue consumers

Example in Axios (JS):

```ts
axios.get("/users", { timeout: 3000 });
```

Tip: Start with conservative timeouts (2–5 seconds).

---

## Retries (and Backoff)

Some failures are transient (e.g., network blips, rate limits).  
A retry may succeed — but too many retries can make things worse.

### Best Practices:

- Retry **only idempotent** operations (e.g., GET, PUT)
- Use **exponential backoff** with jitter
- Add a **retry cap** (e.g., 3 attempts)

Example:

```text
1st try → wait 100ms
2nd try → wait 400ms
3rd try → give up
```

Use libraries:

- `axios-retry` (JS)
- `retry` (Node, Python)
- `resilience4j` (Java)

---

## Circuit Breaker Pattern

Circuit breakers prevent repeated failures from overloading systems.

It works like an electrical switch:

- Closed (normal traffic)
- Open (requests are rejected)
- Half-open (test to see if recovery occurred)

Use when:

- A service starts failing rapidly
- You want to fail fast and recover gracefully

Tools:

- `resilience4j`
- `Hystrix` (deprecated but famous)
- Service mesh (Istio, Linkerd)

---

## Fallback Strategies

When all else fails — fallback.

✅ Fallbacks return **cached**, **default**, or **stubbed** data instead of erroring out.

Examples:

- Return cached product catalog if DB is down
- Send user to retry page with a helpful message
- Queue request for retry instead of dropping it

> “A degraded user experience is better than none.”

---

## Summary

Failures are normal in distributed systems.  
Use **timeouts** to avoid waiting forever, **retries** for transient issues, **circuit breakers** to isolate faults, and **fallbacks** to protect the user.

---

🎉 You’ve completed the **Advanced Guide to Microservices!**

Next up:  
**Lesson 13 – Designing a Real-World Microservice System (start of the Practical Guide)**

</div>
