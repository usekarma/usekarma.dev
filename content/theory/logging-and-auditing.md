---
title: "Logging and Auditing"
weight: 9
---

# Logging and Auditing

Karma acts as a graph-aware coordinator for infrastructure components — but it also serves as a **system of record**.

Every change request, graph update, or deployment action becomes part of a structured, queryable audit trail — providing traceability, accountability, and long-term insight into how the system evolves.

---

## Why Logging Matters

- **Traceability** — See who changed what, when, and why  
- **Impact Analysis** — Understand which components were affected downstream  
- **Security** — Audit sensitive actions across environments and roles  
- **Debugging** — Reconstruct the system before and after a failure  
- **Compliance** — Maintain records for regulated systems or approval flows

---

## What Karma Logs

Karma logs events in all modes — CLI, Lambda, or service — and stores them in a centralized, persistent location (e.g., S3, DynamoDB, or Neptune-adjacent).

Events may include:

- ✅ Change requests (manual or automated)  
- ✅ Graph mutations (new nodes, updated edges, component rewiring)  
- ✅ Terraform lifecycle actions (planned, applied, failed)  
- ✅ Runtime updates and output publishing  
- ✅ User actions from CLI or UI clients  
- ✅ System triggers (e.g., webhook, time-based, validation failure)

All events are timestamped and traceable by component, user, action, and source.

---

## Suggested Log Format

A typical log entry might look like:

```json
{
  "timestamp": "2025-04-18T20:41:00Z",
  "action": "update_config",
  "component": "serverless-site/karma-dev",
  "user": "ted@strall.com",
  "source": "api",
  "inputs": {
    "domain": "usekarma.dev",
    "cloudfront_aliases": ["www.usekarma.dev"]
  },
  "status": "accepted"
}
```

Karma may log pre- and post-change state, validation results, or dependency propagation status depending on the action type.

---

## Querying the Audit Trail

Audit logs can be accessed programmatically, exposed via a UI, or queried through the CLI:

```bash
karma log list --component serverless-site/karma-dev
karma log grep --action terraform_apply
karma log diff --before 2025-04-01 --after 2025-04-18
```

Logs may be exported or mirrored to:

- S3 (cold storage)
- DynamoDB (queryable store)
- CloudTrail or EventBridge (system integration)
- SQLite or JSON files (for dev or testing)

---

## Karma as a System of Record

Logging gives Karma a long-term memory — not just for humans, but for downstream systems and analytics.

Over time, the audit trail can power:

- Time-travel debugging and replay
- Change visualization and lineage queries
- Regression and reliability analysis
- Trust-based config verification
- Integration with compliance and governance tooling
- Data-driven policy tuning and rollout coordination

---

Karma doesn’t just execute infrastructure — it remembers, and it learns.

---

[← Back to Theory](/theory/)
