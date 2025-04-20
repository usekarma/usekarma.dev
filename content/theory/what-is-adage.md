---
title: "What is Adage?"
weight: 2
---

# What is Adage?

**Adage** is the infrastructure engine behind Karma.  

![Adage: Infrastructure as Consequence](/img/adage-system-diagram.png)

It provides the foundation for deploying modular, environment-aware systems using only declarative configuration.

---

## Why Adage?

Traditional infrastructure-as-code often requires hand-rolled logic and tightly-coupled modules.  
Adage flips that model by treating infrastructure as **consequence** — deployments are derived from inputs, not orchestrated step-by-step.

It gives Karma:

- A graph-like deployment model
- Declarative config in Git
- Runtime traceability
- Controlled switchover between states
- Support for multi-account AWS orgs out of the box

---

## What Does Adage Deploy?

Adage components include:

- S3-backed static websites
- Lambda-based APIs and automation
- Aurora PostgreSQL clusters
- IAM roles, secrets, and policies
- Certificate validation and DNS
- Everything Karma depends on

---

## Where to Learn More

Visit the Adage documentation at:

[https://adage.usekarma.dev](https://adage.usekarma.dev)
