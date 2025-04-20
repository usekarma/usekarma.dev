---
title: "Graph Consistency in Karma"
weight: 7
---

# Graph Consistency in Karma

When Karma uses Amazon Neptune as its source of truth, the system must ensure that the graph is kept in a consistent and valid state — even as multiple processes or users interact with it.

This page outlines potential race conditions, failure scenarios, and best practices for maintaining consistency.

---

## Why Consistency Matters

Karma’s infrastructure graph is used to:

- Understand current system state
- Resolve dependencies between components
- Drive actions such as Terraform deployments or runtime rebinds

If the graph is incomplete or temporarily invalid, those actions may behave incorrectly — or fail altogether.

---

## Common Race Conditions

### 1. Concurrent Graph Builds

Multiple `karma graph build` processes (e.g. CLI, Lambda, cron) could overwrite each other's writes if run at the same time.

**Solution:**
- Use a lock mechanism per environment (DynamoDB, SSM, etc.)
- Queue builds or serialize them by policy

---

### 2. Partial Writes or Failures

If a build process crashes or times out mid-update, Neptune may contain:
- Incomplete graphs
- Nodes without edges
- Edges pointing to nonexistent nodes

**Solution:**
- Build the graph in-memory first
- Write changes in a single batch
- Tag graphs as `"building" → "ready"` or versioned

---

### 3. Eventually Consistent Reads

Neptune defaults to eventual consistency. If you read a node immediately after writing it, you may not see it yet.

**Solution:**
- Use `ReadConsistency=QUORUM` for API-facing reads
- Accept eventual consistency for non-critical queries

---

## Recommended Practices

| Problem                | Strategy                           |
|------------------------|-------------------------------------|
| Simultaneous builds    | Use environment-level lock          |
| Incomplete writes      | In-memory staging + atomic publish |
| Conflicting updates    | Queue or version change requests   |
| Flaky reads            | Use QUORUM reads or delay lookups  |
| Rollbacks              | Use batch delete or rebuild logic  |

---

## Future Enhancements

- Graph change journaling (for replays or rollback)
- Change-set simulation before applying to Neptune
- Node/edge versioning or timestamp tagging
- Separate “working” and “committed” graph layers

---

Karma's design keeps the graph as a stable and inspectable surface. Even in a distributed system, you can keep it trustworthy with minimal guarantees.
