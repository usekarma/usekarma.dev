---
title: "Coordinating Change in Karma"
weight: 9
---

# Coordinating Change in Karma

Karma can accept configuration change requests — but in a system with dependencies, propagation must be coordinated carefully to maintain system integrity.

This page outlines a proposal for managing graph-aware change requests safely.

---

## The Problem

Changing the config for one component might:

- Break downstream consumers if done out of order
- Require reloading or redeploying related components
- Involve validation before it’s safe to apply

---

## Karma’s Role

Karma should:

1. **Receive a change request**
2. **Analyze impact in the graph**
3. **Determine what downstream actions are required**
4. **Apply the change and update the graph** (or queue it)
5. **Log the request and outcome for auditing**

---

## Change Lifecycle (Proposed)

```text
Client → karma-api: POST /request-change
               ↓
         Karma validates config
               ↓
         Karma builds proposed graph patch
               ↓
         Karma checks for conflicts or blocking dependencies
               ↓
         If safe: write to config + update graph
         Else: reject or queue for later
```

---

## Use Cases

| Scenario                        | Karma Behavior                                  |
|---------------------------------|--------------------------------------------------|
| Change VPC subnet config        | Reject if dependent EC2 instance is running     |
| Update DNS aliases              | Allow if CloudFront outputs are available       |
| Remove shared bucket reference  | Block if downstream Lambda still depends on it  |

---

## Request Format (Example)

```json
{
  "component": "serverless-site/karma-dev",
  "proposed_change": {
    "cloudfront_aliases": ["www.usekarma.dev"]
  },
  "requested_by": "ted@strall.com"
}
```

---

## Result Format

```json
{
  "status": "applied",
  "affected_components": [
    "route53-zone/karma-dev",
    "cloudfront-distribution/karma-dev"
  ],
  "warnings": [],
  "log_entry_id": "log-1fd742f"
}
```

---

## Implementation Notes

- Karma can start with “just apply” mode and evolve toward full change propagation
- Validation and rollback paths are key to correctness
- A dry-run or “plan” endpoint should be available

---

In the future, Karma can act as a safe graph mutation gateway — analyzing dependencies, proposing valid transitions, and enabling dynamic reconfiguration through a structured request model.
