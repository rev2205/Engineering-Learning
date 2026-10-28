# Networking Fundamentals: Focused Four-Week Path

This page is the index for a narrow learning track: **follow one request from a hostname to an application, then learn to diagnose failures at each boundary**. The detailed pages include explanations, example commands, failure patterns and self-checks.

## Read these pages in order

1. [DNS: How a Name Becomes an Address](01-DNS-Explained.md) — records, recursive resolvers, caching, TTL, NXDOMAIN and what DNS success does not prove.
2. [IP, Routes, Ports and TCP](02-IP-Routes-Ports-TCP.md) — network path, listening ports, handshakes, refusal versus timeout.
3. [TLS and HTTP](03-TLS-and-HTTP.md) — certificates, hostname validation, SNI, HTTP status codes and proxy/upstream clues.
4. [Kubernetes Service Debugging](04-Kubernetes-Service-Debugging.md) — labels/selectors, Service ports, EndpointSlices, readiness and Pod networking.
5. [Guided Troubleshooting Labs](05-Troubleshooting-Labs.md) — controlled exercises that intentionally break a local test service and restore it.

## Weekly pace

### Week 1 — DNS and the destination
Learn the difference between a hostname, DNS record, resolver, IP address and reachable service. Practice reading `dig` or `nslookup` output. Deliverable: explain a DNS lookup in your own words and list three reasons DNS success does not prove the website is healthy.

### Week 2 — Network path and TCP
Learn interfaces, routes, ports, TCP connection setup, refusal and timeout. Use inspection commands on your own machine and curl against a public or authorized endpoint. Deliverable: a comparison table for DNS failure, TCP refusal and TCP timeout.

### Week 3 — TLS and HTTP
Learn what certificate validation checks, why hostname matters, and how HTTP status codes help localize the problem. Deliverable: annotate a `curl -v` output by stage, taking care not to share cookies or tokens.

### Week 4 — Kubernetes Service traffic
Learn how Services select Pods, how EndpointSlices represent backends, and how readiness and targetPort affect traffic. Complete a fault drill in Minikube or kind. Deliverable: a short incident note containing symptom, hypothesis, evidence, root cause, recovery and verification.

## Use one debugging sequence

**Name → route/path → TCP → TLS → HTTP → Service/endpoints → application → dependencies.**

At each step ask:
- What evidence would I expect if this layer is healthy?
- What did I observe?
- What does that observation rule out?
- What does it not rule out?
- What is the next smallest, safest check?

## Rules for the labs

- Use a local disposable cluster or a system you are authorized to test.
- Never inject faults into production or a shared team cluster.
- Change one variable at a time.
- Record the baseline before breaking anything.
- Restore the correct configuration and verify recovery.
- Treat logs as one evidence source, not the whole truth.
