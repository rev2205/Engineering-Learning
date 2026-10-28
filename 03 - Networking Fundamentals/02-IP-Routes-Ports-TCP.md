# 2. IP Addresses, Routes, Ports and TCP

## Four different questions

These concepts are related but answer different questions:

- **IP addressing:** Which network-layer destination are we trying to reach?
- **Routing:** Which next hop or interface should carry packets toward that destination?
- **Ports:** Which transport endpoint on the destination is intended?
- **TCP:** Can the two endpoints establish a reliable byte stream?

An IP address is not a process, a route is not a firewall permission, and an open port does not prove the application is healthy.

## The connection mental model

After resolving `service.example.com` to an address, a client may try to connect to destination port 443. Its operating system chooses a source address and ephemeral source port, then follows the routing table. Network devices and host firewall rules can permit or drop the traffic. If the destination is listening and the path permits the exchange, TCP can establish a connection through a handshake.

A successful TCP handshake means the connection was established. It does not prove TLS will succeed, HTTP will return 200, or the application can complete its work.

## TCP symptoms to distinguish

- **Connection refused:** a reachable endpoint actively rejected the connection, often because no listener exists at that address/port or a device sent a rejection. This is a clue, not definitive proof of one cause.
- **Timeout:** no successful connection was completed within the wait. Possible causes include packet drops, routing issues, firewall rules, overloaded endpoints or an incorrect destination.
- **No route to host / network unreachable:** the local host or a network device reports that it cannot find or use a route; exact behavior depends on OS and network.
- **Connection established, then request hangs:** the problem may be higher-level, the server may be slow, or the response may depend on another service.

## Safe inspection commands

On Linux:
```bash
ip addr
ip route
ss -tan
```

On Windows:
```powershell
ipconfig
route print
netstat -ano
```

To test a specific public or authorized endpoint:
```bash
curl -v --connect-timeout 5 https://example.com/
```

Use tools only against systems you are authorized to test. Avoid broad port scanning.

## How to reason from evidence

**Scenario A: DNS answer exists, TCP times out.** Do not keep changing DNS without evidence. Check the resolved address, whether the port is correct, the route and relevant firewall/load-balancer rules, and whether the destination should be reachable from this network.

**Scenario B: TCP connection is refused.** Verify address and port, then determine whether a service is supposed to listen there. On a system you control, inspect listening sockets and service state.

**Scenario C: TCP connects, but HTTP is slow.** The network handshake completed; inspect TLS timing, server response timing, proxy/upstream behavior, application saturation and dependencies.

## Ports and listeners

A server can have an application process running but not listening on the expected interface or port. For example, a process bound only to loopback may be reachable from its own host but not from another machine. Containers add port publishing and network namespaces, so host port, container port and application bind address must be distinguished.

## Self-check

1. What does a TCP handshake prove?
2. Why is “port 443 is open” not equivalent to “the website is healthy”?
3. What is one possible explanation for refusal versus timeout?
4. Why can a process be running but inaccessible remotely?
5. What would you check next if DNS succeeds but TCP times out?
