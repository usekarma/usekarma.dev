---
title: "Theory"
weight: 2
---

# The Theory Behind Karma

<p style="display: flex; align-items: center; gap: 0.5em;">
  <img
    class="theme-switch-logo"
    src="/assets/logo/usekarma_light_300.png"
    data-light="/assets/logo/usekarma_light_300.png"
    data-dark="/assets/logo/usekarma_dark_300.png"
    style="width: 128px; height: 128px;"
    alt="UseKarma logo">
  <span>
    <b>Infrastructure as Consequence</b> means that what you deploy is not just the result of a plan — it's the outcome of everything that came before.
  </span>
</p>

![Karma: Infrastructure as Consequence](/img/karma-system.drawio.png)

Karma is built on the idea that infrastructure can be:

- Described as a graph of interconnected objects  
- Shaped by lineage, not static templates  
- Modified intentionally, not drifted silently  
- Observed and re-evaluated continuously, not just provisioned once

---

## Graph-Based Thinking

Karma encourages you to model infrastructure as a **runtime graph**, where:

- Each node represents a declarative component
- Edges define runtime dependencies — not file-level includes
- Relationships are stored and queried in Amazon Neptune

This makes it easier to:

- Visualize how infrastructure is composed  
- Understand the blast radius of a change  
- Propagate updates intentionally, based on real dependencies  
- Reroute or override behavior in specific contexts (e.g., QA vs. PROD)

---

## Consequence, Not Just State

Traditional Infrastructure as Code (IaC) tools model desired state and reconcile toward it.

Karma introduces the idea of **consequence** — not just "what should exist", but "how did we get here?"

- Every deployment has context: what changed, who triggered it, what dependencies it resolves  
- This enables safer rollback, more meaningful testing, and auditable infrastructure history  
- Each component is self-describing and testable, with traceable lineage and reproducible behavior

---

## The Object-Oriented Layer

Each Karma component behaves like a smart object:

- It has inputs and outputs  
- It can reference other components by nickname  
- It can inherit behavior or override configuration in context  
- It exists as a node in a graph, not a chunk of YAML or JSON

This allows for reuse, composability, and environment-specific behavior without duplication.

---

## Learn More

Read how Karma’s architecture enables modeling, simulation, and intelligent automation in  
[Data Science Implications →](/theory/data-science/)

{{< logo-switch-script >}}
