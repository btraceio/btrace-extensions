# BTrace Extensions Registry

`btrace-extensions` is the GitHub-hosted registry for published BTrace extensions.

It is intentionally simple:

- one canonical JSON registry reviewed through pull requests
- one JSON schema to keep entries consistent
- one lightweight static site suitable for GitHub Pages
- one validation script and CI workflow to block malformed updates

The registry is for discovery, not artifact hosting. Each entry points to the extension's source repository and the canonical Maven coordinate for the recommended current release.

## Repository Layout

- `registry/extensions.json`: canonical machine-readable catalog
- `registry/extensions.schema.json`: schema contract
- `site/index.html`: static catalog page for GitHub Pages
- `scripts/validate_extension_registry.py`: local and CI validation entry point
- `.github/workflows/validate-extension-registry.yml`: pull-request validation

## Entry Model

Each extension entry includes:

- `id`
- `name`
- `description`
- `owner`
- `source_repo`
- `maven.groupId`
- `maven.artifactId`
- `maven.version`
- optional `compatibility.min_btrace_version`
- optional `tags`

The registry stores a single recommended release per extension. Consumers resolve the normal BTrace extension artifact layout from the base Maven coordinate.

## Local Validation

```bash
python3 -m unittest scripts.tests.test_validate_extension_registry
python3 scripts/validate_extension_registry.py
```

## Hosting Model

This repository is intended to be served entirely from GitHub:

- GitHub repository for PR-based curation
- GitHub Actions for validation
- GitHub Pages for the human-facing catalog

No separate hosting service is required.
