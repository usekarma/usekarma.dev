---
title: "What Is Adage?"
weight: 2
---

# What is Adage?

**Adage is the configuration-driven AWS infrastructure control model; Karma is its workload and proving ground.**

Adage separates infrastructure intent, reusable implementation, and runtime dependency discovery. Its cloud architecture predates the current agent use case: explicit configuration, composable components, Git-controlled changes, and controlled deployment were the original goals. Those choices also make it suitable for agents that inspect, build, verify, plan, and produce evidence.

![Original Adage system diagram](/img/adage-system-diagram.png)

## The infrastructure responsibilities

- [aws-config](https://github.com/usekarma/aws-config) defines desired component instances and environment bindings.
- [aws-iac](https://github.com/usekarma/aws-iac) supplies reusable Terraform/Terragrunt implementations.
- SSM Parameter Store carries published configuration and runtime metadata through predictable paths.
- Git records intent and changes; IAM and execution controls must enforce authority.

Configuration existence is not proof of approval, and runtime metadata does not replace live inventory. Agents may prepare code, configuration, checks, plans, and evidence. Consequential AWS execution requires explicit human authorization.

## Where Karma fits

Karma provides concrete event-processing and analysis experiments, along with a real infrastructure context in which to reconcile desired state, observed resources, and actual spend. The agent safeguards under review in the infrastructure repositories are not a finished Karma governance or action engine.

Read [Adage's canonical story](https://github.com/usekarma/adage), [Adage's documentation website](https://adage.usekarma.dev/), and [Karma's proof criteria](/theory/adage-proving-ground/).
