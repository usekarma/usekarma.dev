---
title: "Demos"
weight: 3
---

# Karma deployment walkthrough

This walkthrough illustrates **Adage's configuration-driven deployment model** using the Karma documentation website. It is not evidence of a complete Karma graph engine, autonomous action system, or current live deployment verification.

## 1. Define desired state

The configuration repository owns environment bindings and component inputs. A site configuration lives under a path such as:

```text
aws-config/iac/prod/serverless-site/usekarma-dev/config.json
```

Check the actual [configuration repository](https://github.com/usekarma/aws-config) for the selected environment and nickname; examples do not establish an account identity or approval.

## 2. Publish approved configuration

An authorized operator publishes configuration to SSM under a path such as:

```text
/iac/serverless-site/usekarma-dev/config
```

SSM publication is an AWS write and can affect later infrastructure changes. Agents may prepare configuration and validation; a human must separately authorize publication.

## 3. Plan and deploy infrastructure

The reusable `serverless-site` implementation in [aws-iac](https://github.com/usekarma/aws-iac/tree/main/components/serverless-site) consumes configuration and prepares the AWS resources. Check identity, environment, dependencies, and a relevant plan before an authorized apply.

Runtime outputs are published separately:

```text
/iac/serverless-site/usekarma-dev/runtime
```

Configuration existence is a prerequisite, not proof of safety or approval. Follow the current target branch's [Adage deployment documentation](https://github.com/usekarma/adage/blob/main/deployment/README.md) rather than treating illustrative commands as an execution contract.

## 4. Build and publish website content

In the [website source repository](https://github.com/usekarma/usekarma.dev), build locally:

```bash
hugo --minify
```

The theme needs Hugo Extended. Confirm the runtime parameter identifies the expected website, content bucket, and CloudFront distribution. Preview the S3 sync, then publish under an explicitly authorized AWS profile. Content publishing updates an existing website; it does not validate a Karma event pipeline or graph backend.

## What this demonstrates

Desired configuration, infrastructure implementation, and site content have separate responsibilities. Runtime metadata connects deployment outputs to the publishing tool. The model is Adage's; Karma provides the concrete workload and evidence to evaluate it.

## Next experiments

- [Infrastructure cost reconciliation](/theory/adage-proving-ground/), with no destructive changes.
- A synthetic event normalization → ClickHouse query demonstration with reproducible inputs and outputs.
- Persistent graph and coordinated-change experiments only after explicit specifications and verification.

Read [current implementation status](/theory/what-is-karma/) before interpreting the exploratory [theory](/theory/) as working software.
