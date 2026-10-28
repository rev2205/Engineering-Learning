# Engineering Growth — Focused Learning Edition

This branch explores a more focused approach than the broad starter library. Rather than trying to study many engineering topics simultaneously, it starts with one operational skill: **trace a request from a hostname to a Kubernetes workload and diagnose the failure using evidence**.

## Start here

1. Read [the focused roadmap](FOCUSED-ROADMAP.md).
2. Work through [Networking Fundamentals](03%20-%20Networking%20Fundamentals/README.md) in order.
3. Complete the labs in a local disposable environment.
4. Use the existing [engineering notebook template](00%20-%20Dashboard/Engineering-Notebook-Template.md) to record hypotheses and evidence.
5. Write a short incident note after each lab.

## What changed on this branch

- Added detailed explanations of DNS, IP/routing/TCP, TLS/HTTP and Kubernetes Service routing.
- Added troubleshooting labs with controlled failures, expected observations and recovery checks.
- Replaced the broad networking overview with a step-by-step curriculum.
- Kept the changes on this branch so `main` remains unchanged.

## Learning principle

Do not aim to memorize every command. Learn what question a command answers, what the output proves, what it does not prove, and what evidence to gather next.

## Safety

Run deliberate failures only in your own local lab or an explicitly authorized environment. Do not experiment on production or shared team clusters. Do not publish internal URLs, logs, credentials, tokens or infrastructure details.
