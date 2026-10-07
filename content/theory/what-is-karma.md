---
title: "What Is Karma?"
weight: 1
---

# What is Karma?

Karma is an experimental event-driven system for understanding change. It explores how normalized events, state, dependencies, and outcomes can support observability, analysis, and evidence-based decisions.

**Adage defines the infrastructure control model. Karma provides the workload and proving ground.** Desired-state configuration, Terraform components, and SSM discovery belong to Adage; Karma experiments with the observations and analysis that can demonstrate whether the model works in practice.

## Source, prototype, and proposal

| Capability | Evidence | Status |
| --- | --- | --- |
| Event/action envelopes | [Schemas](https://github.com/usekarma/karma/tree/main/contracts) and [topic conventions](https://github.com/usekarma/karma/blob/main/actions/topics.md) | Defined in source; universal enforcement is not established. |
| CDC normalization | [Kafka Streams implementation](https://github.com/usekarma/karma/tree/main/normalizers/mongo-cdc-clickhouse-kstreams) and [Python source](https://github.com/usekarma/karma/blob/main/normalizers/mongo-cdc-clickhouse/src/normalizer.py) | Code and mappings exist; end-to-end integration requires verification. |
| State and latency analysis | [ClickHouse SQL](https://github.com/usekarma/karma/tree/main/sinks/clickhouse/sql) | Definitions exist; live processing is not certified here. |
| Graph API | [Lambda handlers](https://github.com/usekarma/karma/tree/main/lambdas) | Mock graph responses and logging stub; no persistent graph integration. |
| Prediction/deviation | [Job source](https://github.com/usekarma/karma/tree/main/entropy/jobs) | Placeholder code and notes. |
| Action execution | [Examples](https://github.com/usekarma/karma/tree/main/actions/examples) | Pseudocode placeholders; no verified action engine. |
| Neptune graph, CLI/service, coordinated changes | [Theory](/theory/) | Design proposals, not established runtime capabilities. |

## Intended event path

Raw CDC → normalization → `events.normalized` → ClickHouse event history and state/latency views → analysis → proposed actions.

Normalizer and SQL source exist. Source/sink wiring must be supplied and tested; detection and execution stages are incomplete. The API prototype is not automatically connected to this streaming path.

## Practical next steps

Use the [source README](https://github.com/usekarma/karma) for component-specific setup. The Compose file starts supporting Kafka/ZooKeeper and ClickHouse services; it does not deploy a complete application. There is no root Poetry application or finished Karma CLI in this checkout.

First validate one synthetic event path and a queryable result. Separately complete the [infrastructure cost proof](/theory/adage-proving-ground/). Larger graph and automation claims should follow observed evidence.
