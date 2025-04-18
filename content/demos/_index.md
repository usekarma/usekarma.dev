---
title: "Demos"
weight: 3
---

# Karma Demos

This section showcases how Karma works in real-world scenarios by walking through a complete deployment example — from configuration to runtime switchover.

Each demo is designed to highlight a key idea behind Karma:  
**Infrastructure as Consequence** — where each step is derived from prior intent.

---

## Minimal Deployment Walkthrough

This demo deploys a simple Hugo website — `karma-dev` — using:

- A declarative config in JSON
- Terraform components from the shared `aws-iac` repo
- Parameter Store for config delivery
- Controlled promotion to runtime

---

### 1. Define the Component Config

The component is defined in your config repo, at:

```
karma-dev-config/iac/prod/serverless-site/karma-dev.json
```

```json
{
  "nickname": "karma-dev",
  "domain": "usekarma.dev",
  "runtime": {
    "bucket": "karma-dev-site",
    "cloudfront_distribution_id": "EXAMPLE123"
  }
}
```

This file is not infrastructure — it’s intent. It describes what the system should be, and Karma will translate that into action.

---

### 2. Publish the Config

Use the deployment script to publish the config into SSM Parameter Store:

```bash
AWS_PROFILE=dev-iac ./scripts/deploy_config.py \
  --component serverless-site \
  --nickname karma-dev
```

This uploads the JSON to:

```
/iac/serverless-site/karma-dev/config
```

No Terraform has run yet. The config exists, but nothing is live.

---

### 3. Deploy the Terraform Component

Now that the config exists, the infrastructure can be safely deployed:

```bash
AWS_PROFILE=dev-iac ./deploy.sh serverless-site karma-dev
```

This will:

- Read the config from Parameter Store
- Deploy the S3 bucket and CloudFront distribution
- Output the deployment status

Everything is traceable: what config was used, what AWS profile was active, and which resources were created.

---

### 4. Publish Site Content

If it’s a Hugo site, you can now push content live:

```bash
AWS_PROFILE=dev-iac ./scripts/publish_site.py --nickname karma-dev
```

This will:

- Build the Hugo site
- Upload to the configured S3 bucket
- Invalidate CloudFront so users see the latest version

---

## What This Demonstrates

- Configuration precedes deployment  
  Karma only allows infrastructure to deploy if the config is present.

- Declarative, auditable history  
  Config lives in Git. Deployments are shaped by intent, not imperative scripts.

- Modular and repeatable  
  You can deploy `karma-qa`, `karma-demo`, `karma-prod` with the same infrastructure logic.

- Controlled switchover  
  Infrastructure can be deployed, validated, and only promoted when explicitly approved.

---

## Coming Soon

- Multi-component graph walkthrough (e.g., site + API + auth)
- Graph visualization for dependencies
- Automated test validation before switchover
- Live deployment explorer and changelog tracking

---

Return to the [Theory](/theory/) page to learn why Karma is structured this way.
