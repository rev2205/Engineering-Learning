# Focused Roadmap: Diagnose a Request from Client to Kubernetes Workload

This branch deliberately narrows the learning library to one practical skill: **debugging why a request cannot reach an application**. The aim is to develop a repeatable mental model useful for DevOps/MLOps work—not to skim many unrelated topics.

## The outcome

By the end, you should be able to investigate “the URL is down” and distinguish:
- hostname not resolving;
- wrong address, port, route or network access;
- TCP connection failure;
- TLS certificate or handshake failure;
- HTTP error from a proxy or application;
- Kubernetes Service with no usable endpoints;
- application running but not ready;
- application dependency failing behind an apparently healthy endpoint.

You need not memorize every command. You need to know **what question each command answers**, what it cannot prove, and what evidence to gather next.

## Study order

1. [DNS: name to address](03%20-%20Networking%20Fundamentals/01-DNS-Explained.md)
2. [IP, routes, ports and TCP](03%20-%20Networking%20Fundamentals/02-IP-Routes-Ports-TCP.md)
3. [TLS, certificates and HTTP](03%20-%20Networking%20Fundamentals/03-TLS-and-HTTP.md)
4. [Kubernetes Service routing](03%20-%20Networking%20Fundamentals/04-Kubernetes-Service-Debugging.md)
5. [Guided troubleshooting labs](03%20-%20Networking%20Fundamentals/05-Troubleshooting-Labs.md)

Spend 2–3 sessions on each stage if needed. Move on when you can explain it and complete the self-check without copying.

## Investigation ladder

When a request fails, move from the outside inward:

1. **Name:** Does the hostname resolve to the expected address?
2. **Path:** Is the client targeting the correct IP and port? Is the route plausible?
3. **Transport:** Can a TCP connection be established?
4. **Security:** Does TLS negotiate for the requested hostname with a trusted certificate?
5. **Protocol:** What HTTP status and headers arrive?
6. **Routing:** Does the request reach the intended proxy, load balancer, Service and backend?
7. **Process:** Is the application listening and ready?
8. **Dependencies:** Can it reach its database, queue or upstream API?

A successful step narrows the search; it does not prove later layers are healthy. DNS success only proves that a DNS answer was obtained, not that the returned address is reachable.

## How to study each section

1. Read the explanation.
2. Close it and write your understanding from memory.
3. Run only safe local or public-read-only inspection commands.
4. Record actual output and what it does **not** prove.
5. Answer the self-check questions without looking.
6. Explain the concept aloud in two minutes.

## Safety

Use your own laptop, a local Minikube/kind cluster, or a system you have explicit permission to test. Do not run experiments against production services or company endpoints without approval. Do not paste internal URLs, logs, certificates, tokens, or infrastructure details into public tools.

## Definition of done

- [ ] Explain DNS lookup and caching in my own words.
- [ ] Distinguish DNS failure from TCP connection failure.
- [ ] Explain TLS certificate validation.
- [ ] Use HTTP status and timing to narrow a failure.
- [ ] Explain how a Kubernetes Service selects Pods.
- [ ] Diagnose a broken local Service using evidence rather than randomly changing YAML.
- [ ] Write one incident-style report from a lab failure.
