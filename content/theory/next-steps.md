---
title: "Next Steps"
weight: 99
---

> **Design proposal:** This page preserves exploratory architecture ideas, not verified runtime capabilities. Persistent Neptune integration, Karma CLI/service commands, coordinated changes, and learning systems are not implemented end-to-end in the current source. Read the [implementation status](/theory/what-is-karma/) and [proof criteria](/theory/adage-proving-ground/) first. Consequential AWS execution requires separate human authorization.


# Next Steps

<p style="display: flex; align-items: center; gap: 0.5em;">
  <img
    class="theme-switch-logo"
    src="/assets/logo/usekarma_light_300.png"
    data-light="/assets/logo/usekarma_light_300.png"
    data-dark="/assets/logo/usekarma_dark_300.png"
    style="width: 128px; height: 128px;"
    alt="UseKarma logo">
  <span>
    <b>Upcoming topics and expansions for Karma</b>
  </span>
</p>

---

## Graph Schema

Document Karma's graph model in Neptune.

- **Node Types:** Component (with `type`, `environment`, `config_path`, `runtime_path`)
- **Edge Types:** `depends_on`, `emits_runtime_to`, `consumes_runtime_from`
- *Note: Components do not store their own nickname — it's tracked externally.*
- TODO: Add edge metadata and example diagrams.

---

## Querying the Graph

Gremlin or Karma CLI queries against Neptune.

```bash
karma graph query --gremlin 'g.V().count()'
```

- Common queries:
  - Downstream components
  - Orphans
  - Drift detection
  - Runtime consumers
- TODO: SPARQL support notes

---

## Change Coordination

How Karma safely applies config updates:

1. Accept proposed change
2. Validate input config
3. Analyze graph impact
4. Plan or apply
5. Update Parameter Store
6. Write graph delta to Neptune
7. Log result

Planned features:
- Queued change sets
- Dry-run mode
- Approval hooks

---

## Developer onboarding

Start with the [source README](https://github.com/usekarma/karma) and component-specific instructions. The current repository has no root Poetry project or finished Karma CLI. Validate one synthetic normalized event through a ClickHouse query before claiming pipeline integration.

The immediate infrastructure objective is the [read-only cost proof](/theory/adage-proving-ground/), with separate human authorization for any later changes.

---

## Future Pages

### Design Principles
- Capture architectural beliefs (e.g. config/runtime separation, graph-first modeling)

### Why Neptune?
- Justify the use of a graph DB vs. SQL or NoSQL alternatives

### Karma API
- Document CLI and REST endpoints (e.g., `/graph`, `/request-change`, `/log`)

### Example Graph Visualization
- Small visual system (3–5 components) with labeled nodes and runtime refs

### UI / Viewer Preview
- Placeholder or screenshot of future graph navigation interface

### Gremlin Cheatsheet
- Quick reference of common queries for graph analysis and validation

---

This page will evolve as implementation progresses.
If you're contributing or extending Karma, these are the building blocks ahead.

{{< logo-switch-script >}}
