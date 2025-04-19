---
title: "Karma"
weight: 1
---

# Karma

<p style="display: flex; align-items: center; gap: 0.5em;">
  <img
    class="theme-switch-logo"
    src="/assets/logo/usekarma_light_300.png"
    data-light="/assets/logo/usekarma_light_300.png"
    data-dark="/assets/logo/usekarma_dark_300.png"
    style="width: 128px; height: 128px;"
    alt="UseKarma logo">
  <span>
    Karma is an experimental open source system for modeling and managing infrastructure as modular, object-oriented components — where each deployment step is shaped by what came before.
  </span>
</p>

**Infrastructure as Consequence.**

![Karma: Infrastructure as Consequence](/img/karma-system.drawio.png)

Rather than building environments top-down, Karma encourages config-driven systems that evolve like a graph — each node connected to its lineage, and each change traceable to its origin.

---

## Why Karma?

- Modular, reusable infrastructure components  
- Declarative, visual dependency graphs  
- Object-oriented modeling across environments  
- Persistent system graph stored in Amazon Neptune  
- Eventually: drag-and-drop design for system composition  

---

## What Karma Does

Karma builds and maintains a live infrastructure graph by:

- Ingesting configuration from Git and Parameter Store  
- Tracking runtime outputs produced by Terraform  
- Inferring relationships and dependencies between components  

The graph is stored in Amazon Neptune and exposed via API — allowing other tools to explore the system, simulate changes, or request updates. Karma coordinates those changes based on the graph’s structure and dependencies.

---

## Beyond Infrastructure

Karma’s graph-based design opens the door to runtime introspection, observability, validation pipelines, and machine learning.  
Explore the [Data Science perspective →](/theory/data-science/)

---

## See It in Action

Want to see how Karma works in practice?  
Check out the [Demos](/demos/) page for a full walkthrough of a real-world deployment.

---

## Powered by Adage

Karma is built on top of [Adage](https://github.com/tstrall/adage), a configuration-first deployment framework that combines Terraform, Parameter Store, and Terragrunt to manage real-world AWS infrastructure.

---

## Status

This project is in early development.  
Follow progress on [GitHub →](https://github.com/usekarma)  
Or dive deeper into the [core theory behind Karma →](/theory/)

{{< logo-switch-script >}}
