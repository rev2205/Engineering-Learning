# Useful Commands — Inspection First

Commands vary by OS and installed tools. Read help and official documentation before unfamiliar commands. Avoid destructive actions and production changes unless authorized.

## Linux
- pwd, ls -lah, find: inspect paths and files.
- ps aux, top: inspect processes.
- free -h, df -h: inspect memory and disk.
- ip addr, ip route: inspect interfaces and routes.
- ss -tulpn: inspect listening sockets.
- journalctl -u SERVICE --since '1 hour ago': inspect recent systemd logs.

## HTTP and TLS
- curl -v https://example.com/: inspect request and TLS details.
- openssl s_client -connect example.com:443 -servername example.com: inspect TLS negotiation.
- dig example.com: query DNS.

## Docker
- docker ps: running containers.
- docker images: local images.
- docker logs CONTAINER: container output.
- docker inspect CONTAINER: configuration and state.

## Kubernetes
- kubectl get pods -A: list Pods.
- kubectl get svc,endpointslices: inspect service routing objects.
- kubectl describe pod POD: events and details.
- kubectl logs POD: application output.
- kubectl rollout status deployment/NAME: observe rollout.
- kubectl get events --sort-by=.lastTimestamp: inspect recent events.

Use authorized environments. Never paste credentials or sensitive output into public issues or unapproved tools.
