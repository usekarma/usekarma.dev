# usekarma.dev

Source for [usekarma.dev](https://usekarma.dev), the public introduction to **Karma**: an experimental event-driven system for understanding change and a workload for proving [Adage's infrastructure control model](https://github.com/usekarma/adage).

Karma's implementation evidence lives in [usekarma/karma](https://github.com/usekarma/karma). Normalization source, contracts, and ClickHouse SQL exist; graph handlers, prediction jobs, and action examples include mocks or placeholders. The website distinguishes those artifacts from proposed Neptune/CLI/service capabilities and the infrastructure cost experiment still being validated.

## Site architecture

The site uses Hugo with the Hugo Book theme and is hosted on existing AWS S3/CloudFront infrastructure deployed through Adage. Preserve the current theme, routes, logos, and theoretical documentation while keeping capability claims aligned with source evidence.

## Build

Hugo Extended is required by the theme's SCSS pipeline.

```bash
git submodule update --init --recursive
hugo --minify
```

Review generated content, internal links, and assets before publishing. `content/theory/adage-proving-ground.md` defines the cost experiment. The $1.12/month target covers the intended minimal state of strall.com and usekarma.dev, not the full historical Karma stack or adage.usekarma.dev.

## Publish to the existing site

Publishing requires an authenticated AWS profile and authorization for the website update. Confirm account identity and `/iac/serverless-site/usekarma-dev/runtime` against the intended domain/bucket/distribution before executing.

The publisher is in this repository:

```bash
AWS_PROFILE=<confirmed-profile> AWS_REGION=<confirmed-region> \
python3 scripts/publish_site.py usekarma-dev
```

It builds Hugo, reads SSM runtime metadata, syncs content to S3 with `--delete`, and invalidates CloudFront. Review the target and file deletions before publishing. Its current `--dry-run` still creates a CloudFront invalidation, so it is not a fully read-only validation command. Use a direct `aws s3 sync ... --dryrun` for an upload preview.

This site-content workflow does not apply/destroy infrastructure, establish production readiness, or complete the billing proof.

## License

[Apache 2.0](LICENSE).
