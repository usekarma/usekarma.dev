---
title: "What Is Karma?"
weight: 1
---

# What Is Karma?

> **TL;DR**  
> Karma is a system for defining, deploying, and managing infrastructure components as graph-aware, testable units — using Git and Parameter Store as the connective tissue between intent, deployment, and runtime state.  
> It creates an environment where infrastructure becomes more observable, auditable, and adaptive — without losing control.

---

**Karma is a configuration-driven deployment system that models infrastructure as a live graph of traceable, testable components.**

Each component is defined by versioned config in Git and Parameter Store, then deployed using Terraform. The result is a dynamic system where infrastructure evolves as a consequence of intent — not just execution.

---

## Core Concepts

### 1. Git Defines Intent

Each component (like a static site or a VPC) is represented by a small JSON file in Git.

```json
{
  "nickname": "karma-dev",
  "domain": "usekarma.dev",
  "cloudfront_aliases": ["www.usekarma.dev"]
}
```

This is not a template. It’s declarative intent.

---

### 2. Parameter Store Becomes the Backbone

The config is published to AWS Parameter Store under paths like:

```
/iac/serverless-site/karma-dev/config
```

Terraform reads this as its input — not from local variables — and deploys infrastructure accordingly.

---

### 3. Terraform Manages Provisioning

Each component uses a shared Terraform module (or Terragrunt wrapper) that dynamically loads config from Parameter Store.

This makes infrastructure:

- Deployable independently  
- Versioned and environment-aware  
- Fully driven by external configuration

---

### 4. Outputs Are Captured as Runtime State

After deployment, Terraform publishes runtime outputs to a parallel SSM path:

```
/iac/serverless-site/karma-dev/runtime
```

These runtime values reflect what was actually deployed — not just what was planned — and are safe for other components to consume.

---

### 5. Karma Builds and Stores the Graph

Karma consumes both `/config` and `/runtime` values to build a graph of component relationships, then stores that graph in Amazon Neptune.

- **Nodes** represent components
- **Edges** represent declared or inferred dependencies
- The graph can be queried, visualized, analyzed, or used to coordinate change

This makes Karma a living model of the system — not just a deployment tool.

---

## The Graph

Karma’s graph model enables:

- Dependency-aware change planning  
- Safe reconfiguration of shared resources  
- Visual exploration of system lineage  
- Runtime-aware system design  

The graph becomes a shared source of truth — not just for deployments, but for coordination, policy, and observability.

---

## What Karma Is *Not*

- ❌ Not a static templating system  
- ❌ Not just a Terraform wrapper  
- ❌ Not dependent on any particular UI or deployment pipeline  

Karma is an infrastructure runtime — focused on structure, traceability, and controlled evolution.

---

[← Back to Theory](/theory/)
