# 4. Kubernetes Service Debugging: Follow the Traffic

## The core model

A Pod IP is not a stable service identity. Pods can be replaced and their IPs can change. A Kubernetes Service provides a stable virtual endpoint for reaching a group of backends selected by labels, or in some cases another defined set of endpoints.

For a common ClusterIP Service, the conceptual path is:

**client Pod → Service DNS name → Service virtual IP → selected endpoint/Pod IP → container port → application**

The actual dataplane implementation depends on the cluster's networking components. Do not assume every cluster implements packet forwarding identically.

## The objects and their jobs

- **Pod:** runs one or more containers and has a Pod IP.
- **Deployment:** declares desired replicas and manages rollout through ReplicaSets.
- **Service:** provides a stable endpoint and selects matching Pods when using a selector.
- **EndpointSlice:** records backend endpoints associated with a Service.
- **CoreDNS:** commonly provides DNS resolution inside the cluster.
- **Readiness probe:** affects whether a Pod is considered ready to receive Service traffic.
- **NetworkPolicy:** if enforced by the cluster's networking implementation, can restrict Pod traffic.

## The most common mismatch: selector and labels

A Service selector must match the labels on the intended Pods. If the selector matches no Pods, the Service may have no usable endpoints. The Service object can exist and DNS can resolve while requests still fail.

Inspect:
```bash
kubectl get svc
kubectl get pods --show-labels
kubectl get endpointslices
kubectl describe svc SERVICE_NAME
```

Compare the Service selector with the labels on Pods. Then inspect EndpointSlices to see whether usable backends were discovered. A Service with no endpoints is a different problem from a Pod that has endpoints but whose application is not listening.

## Port mapping: three names to keep separate

A Service can define:
- **port:** the port exposed by the Service.
- **targetPort:** the port on the selected Pod that traffic is sent to; it can be numeric or a named container port.
- **containerPort:** descriptive Pod container metadata; it does not by itself make a process listen on that port.

A Service can point to targetPort 8080 while the application listens on 8000. The YAML may be accepted, but traffic will fail. Verify the actual listening port and Service mapping.

## Readiness is not the same as process existence

A container can be running but not ready. If a readiness probe fails, the Pod may be excluded from normal Service traffic. This is often desirable: a process that has started but cannot serve requests should not receive traffic.

Inspect:
```bash
kubectl get pods
kubectl describe pod POD_NAME
kubectl logs POD_NAME
kubectl get endpointslices
```

Look at readiness state, recent events, application logs, and whether the Pod appears as a usable endpoint. Logs are one source of evidence, not a complete view.

## A disciplined debugging sequence

1. Confirm the namespace and exact Service name.
2. Check the Service's selector, port and targetPort.
3. Check Pod labels and readiness.
4. Check EndpointSlices for the expected backend addresses and ports.
5. Check whether the application listens on the expected interface and port.
6. Test from a client Pod in the same cluster if authorized.
7. Inspect NetworkPolicy, DNS and cluster networking only after the earlier evidence points there.
8. Verify the response and clean up any temporary test resources.

## Self-check

1. Why can Service DNS work when requests fail?
2. What does an empty EndpointSlice set suggest?
3. Why is containerPort metadata not proof that a process listens?
4. How does readiness influence traffic?
5. What evidence distinguishes selector mismatch from wrong targetPort?
