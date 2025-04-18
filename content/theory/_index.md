---
title: "Theory"
weight: 2
---

# The Theory Behind Karma

**Infrastructure as Consequence** means that what you deploy is not just the result of a plan — it’s the outcome of everything that came before.  
Karma is built on the idea that infrastructure can be:

- Described as a graph of interconnected objects  
- Shaped by lineage, not static templates  
- Modified intentionally, not drifted silently  
- Observed and re-evaluated, not just provisioned once

---

## Graph-Based Thinking

Karma encourages you to model infrastructure as a **graph**, where:

- Each node represents a declarative component
- Edges define runtime dependencies, not static file includes
- Nodes are aware of their lineage, enabling change tracking and auditability

This makes it easier to:

- Visualize how infrastructure is composed  
- Understand the blast radius of a change  
- Reroute or override behavior in specific contexts (e.g., QA vs. PROD)

---

## Consequence, Not Just State

Traditional Infrastructure as Code (IaC) often models desired state and reconciles toward it.

Karma introduces the idea of **consequence** — not just "what do we want", but "how did we get here?"

- Every deployment has context: who triggered it, what config changed, what dependencies it resolves  
- This makes rollback, testing, and branching cleaner and more robust  
- Each object is self-describing and self-validating, with testable inputs and traceable outcomes

---

## The Object-Oriented Layer

Each Karma component behaves like an object:

- It has inputs and outputs  
- It can reference other objects (by nickname or identity)  
- It can inherit behavior or override parts in context  

This allows reuse across environments without duplicating logic or configuration files.

---

## Learn More

Read about how this model opens the door to analysis, modeling, and intelligent infrastructure in  
[Data Science Implications](/theory/data-science/)
