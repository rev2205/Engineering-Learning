# Networking Fundamentals: Four-Week Path

## Goal
Trace a request from client to application and diagnose common connection failures using evidence.

## Week 1 — Names and addressing
Learn DNS records and caching, resolvers, IP addresses, CIDR, subnets, gateways, routing and ARP/neighbor discovery. Lab: compare DNS answers from configured resolvers and inspect local interfaces/routes. Explain: what happens after entering a hostname?

## Week 2 — Transport and HTTP
Learn TCP handshake, connection states, ports, UDP, HTTP methods/status codes/headers, keep-alive, proxies and timeouts. Lab: use curl verbose output and browser developer tools to inspect a request. Explain: how can DNS succeed while TCP fails?

## Week 3 — TLS and routing
Learn certificates, trust stores, expiry, SAN, SNI, TLS handshake, reverse proxies, load balancers and health checks. Inspect a public site's certificate with a browser or OpenSSL. Explain: why can a certificate be valid for one hostname but invalid for another?

## Week 4 — Kubernetes networking
Learn Pod IPs, Services, ClusterIP, CoreDNS, EndpointSlices, readiness, Ingress/Gateway concepts and NetworkPolicy. In a local cluster, test service DNS, then intentionally break a Service selector and diagnose it.

## Troubleshooting sequence
1. Confirm hostname, port, path, timestamp and exact error.
2. Check name resolution.
3. Check route and reachability where appropriate.
4. Check TCP connection.
5. Check TLS hostname, trust chain and expiry.
6. Check HTTP response and upstream behavior.
7. Check application health and dependencies.
8. Compare client evidence with server logs and metrics.

## Useful tools
- dig / nslookup: DNS.
- ip addr / ip route: Linux interfaces and routes.
- ss: socket inspection.
- curl -v: HTTP/TLS details.
- openssl s_client: TLS inspection.
- kubectl get svc,endpointslices,pods: Kubernetes routing objects.
- kubectl describe / logs: resource details and application output.

Use authorized, non-production labs for experiments.
