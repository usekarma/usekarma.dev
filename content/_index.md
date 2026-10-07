---
title: "Karma"
weight: 1
description: "An experimental event-driven system for understanding change, and a real workload for proving Adage's infrastructure control model."
---

# Karma

<p style="display: flex; align-items: center; gap: 1rem;">
  <img class="theme-switch-logo" src="/assets/logo/usekarma_light_300.png" data-light="/assets/logo/usekarma_light_300.png" data-dark="/assets/logo/usekarma_dark_300.png" style="width: 96px; height: 96px;" alt="UseKarma logo">
  <span><b>An experimental event-driven system for understanding change—and a real workload for proving Adage's infrastructure control model.</b></span>
</p>

Karma explores how events, state, dependencies, and outcomes can make system behavior explainable. Its source includes Kafka normalization, event/action contracts, ClickHouse analysis definitions, and prototype API handlers. The goal is to turn observations into reviewable decisions and measured results.

[Explore the source](https://github.com/usekarma/karma) · [Implementation status](/theory/what-is-karma/) · [Adage architecture](https://adage.usekarma.dev/)

## What Karma is for

What happened? What changed? Which entities or dependencies were affected? What evidence supports the next decision?

An event history can connect operational signals with state, latency, lineage, and proposed actions. Karma is the place to develop and test that workload. **Adage defines the infrastructure control model**: how desired state, reusable implementation, runtime discovery, environments, and controlled deployment fit together.

## What exists today

| Area | Evidence and limits |
| --- | --- |
| Event contracts and normalization | Schemas, mappings, and Python/Java normalization source exist. Complete producer/consumer integration still needs verification. |
| ClickHouse analysis | Tables, materialized views, and state/latency queries exist in source. Their presence does not prove a live pipeline. |
| Graph API prototype | Query handler returns mock graphs; logging handler prints events and has a graph insertion TODO. |
| Prediction, deviation, and actions | Job and action examples include placeholders. These are not verified detection or execution services. |
| Future graph platform | Persistent Neptune integration, a complete CLI/service, coordinated changes, and graph learning remain design proposals. |

The [repository](https://github.com/usekarma/karma) is the implementation evidence. The [theory pages](/theory/) preserve the longer-term ideas and label their status. No complete end-to-end deployment or production readiness is claimed here.

## How the projects fit together

| Part | Responsibility |
| --- | --- |
| [Adage](https://adage.usekarma.dev/) | Infrastructure control model, originally built around explicit and composable cloud architecture. |
| [aws-config](https://github.com/usekarma/aws-config) | Desired instances and environment bindings. |
| [aws-iac](https://github.com/usekarma/aws-iac) | Reusable Terraform/Terragrunt implementation. |
| **SSM Parameter Store** | Configuration and runtime dependency bridge. |
| **Karma** | Workload, observations, experiments, and evidence about the model's results. |
| [Agent business solution template](https://github.com/usekarma/agent-business-solution-template) | Specifications, deterministic verification, readiness evidence, and human release decisions. |

Adage's architecture predates the current agent use case. Explicit state and predictable interfaces make it a useful substrate for agent-assisted engineering. [Read the complete Adage story](https://github.com/usekarma/adage).

## Agents prepare evidence; humans authorize execution

Agents may inspect source and AWS read-only, develop components, prepare configuration, run checks, generate plans, investigate cost/drift, and prepare pull requests. Production apply, destroy, persistent-data deletion, sensitive IAM/security changes, SSM publishing, and irreversible operations require explicit human authorization.

Agent safeguards are implemented in [aws-iac PR #1](https://github.com/usekarma/aws-iac/pull/1) and [aws-config PR #1](https://github.com/usekarma/aws-config/pull/1), currently under review. They are not Karma runtime features and are not yet default-branch infrastructure behavior.

## A measurable infrastructure proof

Compare **desired state vs. actual AWS state vs. actual cost**, explain the differences, and propose safe remediation without destructive changes.

| Intended minimal site steady state | Exact expected target |
| --- | ---: |
| strall.com | $0.51/month |
| usekarma.dev | $0.61/month |
| **Combined** | **$1.12/month** |

These are owner-specified targets awaiting billing proof. They describe those two sites' intended minimal state, not the full historical Karma stack or the additional Adage documentation site.

The first experiment must attribute spend above the target to infrastructure causes, map it back to configuration/IaC where possible, and produce evidence, estimated savings, and data-loss risks. Missing coverage or unexplained charges remain visible. [Proof criteria](/theory/adage-proving-ground/) define success; complete public end-to-end proof is still pending.

## Explore and contribute

Start with the [implementation overview](/theory/what-is-karma/), [Adage's role](/theory/what-is-adage/), or the [deployment walkthrough](/demos/). For setup and commands, use the [Karma source README](https://github.com/usekarma/karma) and [Adage quickstarts](https://github.com/usekarma/adage#getting-started).

{{< logo-switch-script >}}
