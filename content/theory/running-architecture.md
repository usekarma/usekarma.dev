---
title: "Karma Runtime Architecture"
weight: 6
---

# Karma Runtime Architecture

Karma is a graph-based system for managing infrastructure components, configurations, and runtime state. This page explains how Karma operates under the hood — what components exist, how they behave in different modes, and when each mode makes sense.

All modes write to a shared, queryable graph stored in **Amazon Neptune**.

---

## Core Responsibilities

At runtime, Karma must be able to:

- Load component config from Git (via pre-published SSM parameters)
- Load runtime values from Parameter Store
- Build and validate a dependency graph
- Store that graph in Amazon Neptune
- Accept input via CLI, API, or UI
- Evaluate and coordinate proposed changes
- Optionally trigger downstream actions such as:
  - Terraform apply
  - Component reloads
  - Propagated updates
- Log every action for auditability

---

## Execution Modes

Karma supports three runtime models:

---

### 🟢 CLI Mode (On-Demand)

In this mode, Karma runs as a command-line tool:

```bash
karma graph build
karma plan serverless-site karma-dev
karma deploy serverless-site karma-dev
```

- Reads config and runtime from Parameter Store
- Builds the dependency graph in memory
- Writes the graph to Amazon Neptune
- Runs validation or Terraform as needed
- Exits after completion

**Best for:**

- CI/CD pipelines
- Local workflows and prototyping
- Manual deployment and inspection

---

### 🟢 Serverless API Mode (API Gateway + Lambda)

This mode exposes Karma’s API through **Lambda functions** behind **API Gateway**.

- Each API route maps to a stateless Lambda function
- Reads config and runtime as needed
- Writes updates to Amazon Neptune
- Optionally logs to DynamoDB, S3, or external services

**Example Routes:**

- `GET /graph` → Return the latest graph
- `POST /request-change` → Propose and apply a change

**Best for:**

- Cloud-native automation
- Event-driven systems and bots
- Low-maintenance external access to Karma’s graph

---

### 🟢 Service Mode (Live API + Worker)

In service mode, Karma runs continuously with local caching and coordination logic.

#### Key Components

**1. `karma-api`**  
- Provides REST or GraphQL endpoints  
- Handles graph queries, diffing, and change proposals  
- Uses cached state for performance  

**2. `karma-worker`**  
- Processes long-running tasks:
  - Terraform apply
  - Multi-step workflows
  - Validation and dependency updates  

**3. `karma-log`**  
- Captures a durable audit trail of all actions  
- Can log to file, SQLite, DynamoDB, or S3

**Best for:**

- Real-time graph access (e.g. for a UI)
- Coordinated, multi-component change plans
- Large-scale infrastructure with complex dependencies

---

## Optional Components

| Component      | Description                                         | Required? |
|----------------|-----------------------------------------------------|-----------|
| `karma-cli`    | CLI interface for local dev or CI use               | ✅ Yes     |
| `karma-core`   | Shared graph engine used by all modes               | ✅ Yes     |
| `karma-api`    | API (as server or Lambda functions)                 | ❌        |
| `karma-worker` | Background orchestrator for Terraform + updates     | ❌        |
| `karma-log`    | Audit logging system (file, DB, or cloud-native)    | ❌        |
| `karma-ui`     | Optional visual dashboard backed by `karma-api`     | ❌        |

---

## Summary

| Mode                | What it Runs                                | Best for                           |
|---------------------|----------------------------------------------|------------------------------------|
| CLI Mode            | Command-line driven, writes graph to Neptune | Simplicity, CI/CD, prototyping     |
| Serverless API Mode | Lambda + API Gateway, stateless              | Cloud-native automation, low ops   |
| Service Mode        | Long-lived processes with graph cache        | Orchestration, UIs, fast queries   |

---

Karma’s runtime is modular, flexible, and graph-first — optimized for systems where **change must be tracked, reasoned about, and safely applied.**

---

[← Back to Theory](/theory/)
