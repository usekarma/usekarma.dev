# usekarma.dev

This is the source repository for [https://usekarma.dev](https://usekarma.dev).

The site is deployed using the [Adage](https://github.com/tstrall/adage) infrastructure framework and hosted on AWS using S3, CloudFront, Route 53, and ACM. Content is built with Hugo and managed in this repo.

---

## What Is Karma?

**Karma** is an experimental system for modeling infrastructure as modular, composable objects.

It’s based on the principle that each deployment step depends on what came before — like a chain of configuration and consequence. Karma encourages explicit modeling of dependencies and structure using open source tools.

This site introduces the concept and will grow alongside the implementation.

---

## Site Architecture

- Static site generated with [Hugo](https://gohugo.io)
- Deployed via [Adage’s `serverless-site`](https://github.com/tstrall/aws-iac/tree/main/components/serverless-site) component
- Hosted on AWS with:
  - S3 (for content)
  - CloudFront (for CDN and TLS)
  - Route 53 (for DNS)
  - ACM (for HTTPS)

---

## Deployment

The site is configured in [`karma-dev-config`](https://github.com/usekarma/karma-dev-config), and can be deployed using:

```bash
AWS_PROFILE=prod-karma ./scripts/publish_site.py --nickname usekarma-dev
```

This builds the Hugo site, uploads it to S3, and triggers a CloudFront cache invalidation using settings stored in Parameter Store.

---

## Future Plans

- Publish visual documentation and architecture diagrams
- Explore drag-and-drop interfaces for system composition
- Share Karma as a library of composable infrastructure patterns
- Provide examples for Terraform, Python, and data pipeline systems

---

## License

This project is licensed under the [Apache License 2.0](./LICENSE).
