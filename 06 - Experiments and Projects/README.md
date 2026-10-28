# Experiments and Projects

Choose small, reversible, repeatable projects that produce evidence of understanding.

## Project 1 — Containerized API
Build a tiny FastAPI service with a health endpoint and tests. Build and run a Docker image. Inspect logs, environment, exit codes and port mapping. Deliverable: architecture sketch and explanation of the Dockerfile.

## Project 2 — Kubernetes deployment
Deploy the API to Minikube or kind. Create Deployment and Service, add sensible probes, inspect events, logs, endpoints and rollout history. Deliverable: diagram from client to Service to Pod.

## Project 3 — Failure drills
In a local lab, introduce one issue at a time: wrong Service selector, wrong target port, bad environment variable, failing readiness endpoint, nonexistent image tag, or unsuitable resource limit. Predict symptoms, gather evidence, fix and record how alternatives were ruled out.

## Project 4 — CI pipeline
Run lint and tests on pull requests, build the image, pin actions and use least-privilege permissions. Never print secrets. Deliverable: pipeline diagram and gate explanations.

## Project 5 — Observability
Add structured logs and meaningful metrics; dashboard request rate, errors, latency and saturation; define one actionable alert with an owner and runbook; test it locally.

## Experiment log
Hypothesis; environment; one change; expected result; observed result; evidence; conclusion; reproduction steps; cleanup/reset plan.
