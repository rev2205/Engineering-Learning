# 1. DNS: How a Name Becomes an Address

## The problem DNS solves

People use names such as `example.com`; network connections need an address to send traffic toward. The Domain Name System (DNS) is a distributed naming system that stores records and lets clients discover information about a domain.

DNS is not the web server. DNS normally does not deliver the web page; it helps the client discover an address or another piece of information needed to connect.

## What commonly happens after you type a URL

Suppose you open `https://service.example.com/status`.

1. The browser separates the hostname (`service.example.com`), scheme (`https`) and path (`/status`).
2. The browser or operating system may already have a cached DNS answer.
3. If needed, a stub resolver asks a recursive resolver configured by the device or network.
4. The recursive resolver may answer from cache. Otherwise it follows DNS delegation from root to top-level domain to authoritative name servers, caching results as allowed by their TTLs.
5. The answer might be an A record (IPv4), AAAA record (IPv6), or CNAME pointing to another name that must be resolved.
6. The client selects an address and attempts a connection. This is where routing, firewalls, TCP and TLS become relevant.

Implementations vary: browsers and operating systems may have their own caches, encrypted DNS, connection reuse, or other optimizations. The sequence above is a useful mental model, not a guarantee that every lookup performs every step.

## Important terms

- **A record:** maps a name to an IPv4 address.
- **AAAA record:** maps a name to an IPv6 address.
- **CNAME:** aliases one DNS name to another name.
- **Authoritative name server:** provides the definitive records for a DNS zone.
- **Recursive resolver:** performs the lookup work for a client and caches answers.
- **TTL:** time-to-live that indicates how long a DNS answer may be cached.
- **NXDOMAIN:** response indicating that the queried name does not exist.
- **SERVFAIL:** resolver could not complete the query successfully; this does not by itself identify the underlying cause.

## Inspect a public hostname

Use a public domain or a hostname you own:

```bash
dig example.com A
dig example.com AAAA
dig example.com CNAME
```

If `dig` is unavailable, use `nslookup example.com`. On Windows, `ipconfig /displaydns` can show cached resolver entries; `ipconfig /flushdns` changes local cache state, so do not use it as a first diagnostic step unless you understand why.

Read the output carefully:
- Which record type was queried?
- Which server answered?
- What status was returned?
- What TTL is shown?
- Did you receive an answer, an alias, or an error?

Compare two resolvers only when you have a reason. Different answers can be legitimate because of caching, split-horizon DNS, geographic routing, or different DNS views.

## What DNS success does and does not prove

**It proves:** a resolver returned a response for that query at that time.

**It does not prove:** the address is correct for your environment; the host is reachable; port 443 is open; the TLS certificate is valid; the application is healthy; or the endpoint returns a successful HTTP status.

This distinction prevents a common debugging mistake: “DNS works, so the website should work.” DNS is only one stage.

## Common failure patterns

- **NXDOMAIN:** typo, missing record, wrong DNS view, or record removed.
- **SERVFAIL:** possible DNSSEC validation, upstream, authoritative-server or resolver problem; gather more evidence.
- **Stale address:** cached answer may persist until TTL expiry, depending on caching behavior.
- **Different answer inside a cluster:** Kubernetes DNS and private zones may intentionally return different answers from public resolvers.
- **Only some clients fail:** compare resolver configuration, network path, cache and IPv4/IPv6 behavior.

## Self-check

1. What is the difference between a recursive resolver and an authoritative name server?
2. Why can DNS resolve correctly while a browser still shows a timeout?
3. What does TTL influence, and what does it not guarantee?
4. Why might an internal service resolve differently inside Kubernetes?
5. If you get NXDOMAIN, what evidence would you gather before changing a record?

**Practical note:** Record the hostname category and exact error, but avoid publishing internal company hostnames or DNS answers.
