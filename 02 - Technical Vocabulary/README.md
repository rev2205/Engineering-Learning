# Technical Vocabulary

Learn a few terms weekly. For each, write a plain-language definition, example, misconception and related term. Review after one day, one week and one month.

## Architecture and distributed systems
- Availability: proportion of time a service performs its intended function.
- Latency: time taken for an operation.
- Throughput: work completed per unit time.
- Bottleneck: constrained component limiting overall performance.
- Backpressure: prevents an overloaded consumer from being overwhelmed.
- Idempotency: repeating an operation has the same intended effect as doing it once.
- Consistency: guarantees about when updates become visible.
- Quorum: minimum participants required for a decision or operation.
- Replication: maintaining copies across nodes.
- Failover: switching to a replacement component.
- Graceful degradation: preserving core functions when optional parts fail.

## Networking
- DNS: maps names to records such as IP addresses.
- Resolver: obtains DNS answers for a client.
- Subnet: IP range grouped by a network prefix.
- Route: rule describing packet forwarding.
- TCP handshake: exchange establishing a TCP connection.
- Port: transport-layer service endpoint identifier.
- TLS: protects communications and authenticates peers.
- Certificate chain: certificates linking identity to a trusted root.
- SNI: TLS extension indicating the requested hostname.
- Reverse proxy: receives requests and forwards them upstream.
- Load balancer: distributes traffic among backends.
- MTU: maximum packet size supported by a link at a given layer.

## Reliability
- SLI: quantitative service measurement.
- SLO: target for an SLI.
- SLA: formal commitment, often with consequences if missed.
- Error budget: allowed unreliability implied by an SLO.
- Runbook: steps for a known operational situation.
- Postmortem: structured review of an incident and improvements.
- Alert fatigue: reduced responsiveness from excessive or low-value alerts.
- Observability: inferring internal state from logs, metrics, traces and other outputs.

## Linux and containers
- Process: running instance of a program.
- Signal: mechanism for notifying or controlling a process.
- File descriptor: process handle for a file, socket, pipe or resource.
- Namespace: Linux isolation mechanism for resource views.
- cgroup: Linux mechanism for accounting for or limiting process groups.
- Image: packaged filesystem and metadata used to create a container.
- Container runtime: software that creates and manages containers.
- Registry: service storing and distributing images.

## Kubernetes and delivery
- Pod: smallest deployable Kubernetes unit.
- Deployment: controller managing replicated Pods and rollouts.
- Service: stable network abstraction for reaching Pods or endpoints.
- Ingress: API for HTTP(S) routing into a cluster, implemented by a controller.
- Readiness probe: determines whether a container should receive traffic.
- Liveness probe: helps determine whether a container should restart.
- Reconciliation loop: repeatedly compares desired and observed state and corrects differences.
- Canary: gradual exposure of a change to a subset of traffic or users.
- Drift: difference between intended and actual configuration.

## Vocabulary card
Term; plain meaning; concrete example; what it is not; related term; can I explain it from memory?
