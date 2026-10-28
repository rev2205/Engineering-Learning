# 3. TLS and HTTP: From a Connection to an Application Response

## TLS: protecting the connection

HTTPS is HTTP carried over TLS. TLS helps protect confidentiality and integrity and lets the client authenticate the server using certificates and trust rules. A TCP connection can succeed while the TLS handshake fails.

Certificate validation commonly involves:
- the certificate is within its validity period;
- the requested hostname matches a subject alternative name (SAN);
- the chain links to a trusted certificate authority;
- certificate usage and other validation rules are acceptable;
- client and server can agree on compatible TLS settings.

Exact checks depend on the client and configuration. A certificate being unexpired alone is not enough.

## Hostnames matter

A server may host several websites at one IP address. TLS Server Name Indication (SNI) lets the client indicate the hostname it wants during the handshake, so the server can choose an appropriate certificate and configuration. Connecting by raw IP instead of hostname can therefore produce a certificate mismatch even when the service works by name.

## Inspect TLS carefully

For a public or authorized hostname:
```bash
openssl s_client -connect example.com:443 -servername example.com
```

Look for handshake errors, the presented certificate chain, validity dates and verification results. Output depends on OpenSSL version and server behavior. Avoid treating one line as a complete diagnosis.

You can also run:
```bash
curl -v https://example.com/
```

This helps separate name resolution, connection, TLS negotiation and HTTP response. Do not bypass certificate validation as a “fix”; it hides the failure and weakens security.

## HTTP: what the server says

Once TLS is established, HTTP communicates requests and responses. Status codes are clues:
- **2xx:** request succeeded according to the specific endpoint's semantics.
- **3xx:** redirect or other redirection behavior.
- **4xx:** request-related or authorization-related issue, such as 400, 401, 403 or 404.
- **5xx:** server or gateway reports an error, such as 500, 502, 503 or 504.

Status codes do not tell the whole story. A 200 response can contain an application-level error; a 404 may come from a proxy rather than the intended application; a 503 can be emitted by a load balancer when no healthy backend exists.

## Use curl as an investigation tool

```bash
curl -v --connect-timeout 5 --max-time 15 https://example.com/
```

Ask:
1. Did DNS return an address?
2. Did the TCP connection complete?
3. Did TLS succeed?
4. Which HTTP status arrived?
5. Were there redirects?
6. How long did the request take?

To inspect headers only:
```bash
curl -sS -D - -o /dev/null https://example.com/
```

Options and output differ by curl version. Be careful when sharing verbose output because it may contain hostnames, cookies, tokens or other sensitive headers.

## Proxy and upstream distinction

A reverse proxy or load balancer can accept a client connection successfully and then fail to reach the upstream application. A 502 often suggests an invalid or failed upstream response; a 504 often suggests an upstream timeout. These are common patterns, not universal definitions of root cause. Inspect proxy logs, upstream health and application telemetry where you have permission.

## Self-check

1. Why can TCP succeed while HTTPS fails?
2. Why can a valid certificate still be invalid for the hostname?
3. What does a 503 tell you—and what does it not tell you?
4. Why might a 404 come from the wrong component?
5. What stages can `curl -v` help you distinguish?
