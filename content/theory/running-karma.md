---
title: "How Karma Runs"
weight: 5
---

# How Karma Runs

Karma is a system for managing infrastructure through configuration and runtime state — but how it actually runs can vary.

Depending on your needs, Karma can operate as a **CLI tool**, a **long-running service**, or a **serverless API**.  
In all cases, Karma builds a live infrastructure graph and writes it to **Amazon Neptune**.

---

## Option 1: CLI Mode (On-Demand)

In CLI mode, Karma runs as a command-line tool or script:

- Reads configuration from Git
- Reads runtime state from Parameter Store
- Builds the dependency graph in memory
- Writes the graph to Neptune
- Executes logic, then exits

You can use it to:

- Validate system state
- Simulate or visualize the dependency graph
- Apply Terraform changes manually or via CI/CD
- Propose and apply config updates

### Example Workflows

```bash
karma graph build
karma propose-change serverless-site karma-dev --input updated.json
karma apply
```

### Benefits

- Simple to set up
- No persistent service required
- Easy to integrate into CI/CD pipelines

### When to Use

- You're just getting started
- You prefer GitOps-style workflows
- You don’t need a UI or real-time API

---

## Option 2: Serverless API Mode (API Gateway + Lambda)

In this mode, Karma exposes a lightweight HTTP API through **API Gateway** and **Lambda functions**.

- Each endpoint maps to a Lambda function (e.g. `GET /graph`, `POST /request-change`)
- Reads config and runtime from Parameter Store
- Writes to Neptune as needed
- Optionally logs to DynamoDB, S3, or other external systems

### Benefits

- Zero infrastructure to manage
- Scales automatically
- Easy to call from CLI, automation tools, or UI

### When to Use

- You want programmatic access without running a server
- You prefer pay-per-use or event-driven architecture
- Your graph is small enough to be recomputed per request
- You’re building cloud-native UI or automation flows

---

## Option 3: Service Mode (Live API + In-Memory Graph)

In this mode, Karma runs continuously as a long-lived process:

- Exposes an HTTP API (REST or GraphQL)
- Maintains a cached graph in memory for fast queries
- Accepts change requests from humans or systems
- Orchestrates Terraform or triggers component updates
- Periodically syncs or rebuilds the graph in Neptune
- May handle long-running tasks, queue processing, or real-time notifications

### Benefits

- Enables a responsive UI or platform portal
- Ideal for large graphs or dependency-heavy systems
- Supports background orchestration and event-driven flows
- Can manage queued change sets and coordinated rollouts

### When to Use

- You want full system visibility with cached state
- You need Karma to manage ongoing coordination
- You’re integrating with UIs, bots, or third-party tools
- You want complex workflows or dependency analysis

---

## Hybrid Approaches

You don’t have to choose just one.

- Use **CLI** for low-friction dev and CI/CD
- Add a **serverless API** for scalable external access
- Run a **background service** for long-lived graph coordination

All modes write to the same Neptune graph, making it easy to query, validate, or visualize the current state of the system.

---

## Summary

| Mode               | What it does                                | Best for                             |
|--------------------|----------------------------------------------|--------------------------------------|
| CLI Mode           | On-demand graph build + Terraform deploy     | Simplicity, CI/CD pipelines          |
| Serverless API Mode| Stateless API via Lambda and API Gateway     | Low-cost automation, cloud-native UI |
| Service Mode       | Long-running daemon with in-memory graph     | Real-time systems, orchestration     |

---

Karma gives you a consistent, queryable, graph-based view of your infrastructure — no matter how you choose to run it.
