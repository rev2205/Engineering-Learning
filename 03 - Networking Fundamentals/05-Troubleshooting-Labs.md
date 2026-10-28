# 5. Guided Troubleshooting Labs

These labs are intentionally local and reversible. Use Minikube or kind and an application you control. Do not apply deliberate faults to a shared or production cluster.

## Lab A — Separate DNS from connectivity

**Goal:** learn that a DNS answer and a working service are separate facts.

1. Query a public hostname you are allowed to inspect using `dig` or `nslookup`.
2. Make a request using `curl -v --connect-timeout 5 --max-time 15 https://example.com/`.
3. Write down the DNS result, connection result, TLS result, HTTP status and elapsed time.
4. Explain which layer each observation tests.
5. Do not infer that every future request will behave the same way; caches and network conditions change.

**Deliverable:** a short table of stages, evidence and what each stage does not prove.

## Lab B — Inspect a local application port

1. Start a tiny web server or your own FastAPI app locally.
2. Identify its listening port using a platform-appropriate socket inspection command.
3. Request it locally using curl.
4. Change the client to use the wrong port and record the error.
5. Restore the correct port and confirm recovery.

**Questions:** Was the error a refusal or a timeout? What evidence supports your explanation? How would binding only to loopback differ from binding to an interface reachable by other hosts?

## Lab C — Break a Kubernetes Service selector

Prerequisites: a local disposable cluster and permission to create resources. Use a small sample app, not company workloads.

1. Deploy an HTTP workload and expose it through a ClusterIP Service.
2. Confirm the Pods are Ready and the Service has endpoints.
3. Record the working response from a client Pod.
4. In a lab manifest, change the Service selector to a label that no Pod has.
5. Observe the Service and EndpointSlices. Test the request from the client Pod.
6. Explain why the Service object and DNS name can still exist even though there are no matching backends.
7. Restore the selector and verify endpoints and traffic recover.

Do not blindly apply example manifests to a non-lab cluster. Review every manifest and namespace first.

## Lab D — Break targetPort

1. Start from the working lab in Lab C.
2. Record the port where the app actually listens and the Service's port/targetPort.
3. Change targetPort to a port where the app is not listening.
4. Inspect the Service and EndpointSlices; then test traffic and collect evidence.
5. Restore the correct targetPort.

**Learning point:** an endpoint can exist while requests still fail because endpoint discovery does not prove that an application accepts connections on the configured port.

## Lab E — Readiness failure

1. In the disposable lab, configure a readiness endpoint that intentionally returns failure.
2. Observe Pod readiness and Service endpoints.
3. Restore the correct readiness endpoint and confirm the Pod becomes ready.
4. Explain why keeping an unready Pod out of normal traffic can protect users.

## Incident note to write after each lab

- Symptom:
- Expected behavior:
- Hypothesis before investigation:
- First useful evidence:
- Hypotheses ruled out:
- Root cause in this lab:
- Recovery and verification:
- What would I monitor or document in a real environment?
- What remains uncertain?

## Completion test

Without reading the steps, diagnose one randomly chosen fault from Labs C–E. Explain the difference between your initial hypothesis and the final evidence. If you need to change multiple things at once, pause and make the investigation more controlled.
