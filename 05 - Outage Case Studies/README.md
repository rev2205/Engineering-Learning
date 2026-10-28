# Outage Case Studies

Study incidents to understand system behavior and organizational learning, not to blame individuals. Prefer primary-source reports and verify dates and technical claims.

## Suggested cases
- CrowdStrike, July 2024: faulty content update and widespread Windows crashes; examine validation, staged rollout, blast radius and recovery constraints.
- Cloudflare, June 2019: WAF rule change caused CPU exhaustion; examine testing, rollout and rollback.
- GitHub, October 2018: database failover and replication delay affected availability and consistency; examine detection and recovery coordination.
- AWS US-EAST-1: select one specific incident and read its official event report rather than treating incidents as one story.
- Kubernetes control-plane or certificate incidents: examine expiry, dependencies, rollout and observability using primary reports.

## Incident analysis template
1. Impact: what did users experience?
2. Timeline: trigger, detection, mitigation, recovery and follow-up.
3. Trigger: what immediate event started the incident?
4. Contributing conditions: what made the trigger harmful?
5. Detection: which signals helped or were missing?
6. Mitigation: what restored service and what slowed recovery?
7. Prevention: what tests, guardrails or architecture changes reduce risk?
8. Trade-offs: cost and residual risk.
9. Transfer: what applies to a lab or platform task?
10. Evidence quality: verified facts versus unknowns.

“Someone made a mistake” is not sufficient analysis. Ask why the system allowed broad impact and which controls could catch the issue earlier.
