# Contributing To The BTrace Extension Registry

## How To Add Or Update An Extension

1. Publish the extension artifacts to Maven Central.
2. Edit `registry/extensions.json`.
3. Add a new entry or update the recommended `maven.version` for an existing entry.
4. Run local validation:

```bash
python3 -m unittest scripts.tests.test_validate_extension_registry
python3 scripts/validate_extension_registry.py
```

5. Open a pull request.

## Required Fields

Every entry must include:

- stable extension `id`
- human-readable `name`
- short `description`
- `owner`
- `source_repo` as an `https://` URL
- canonical Maven coordinate with `groupId`, `artifactId`, and `version`

## Review Rules

- Do not add duplicate extension ids.
- Do not add duplicate Maven base coordinates.
- Keep descriptions short and factual.
- Point `source_repo` at the repository users should review for source and issues.
- Prefer tags that help browsing rather than implementation detail.

## Publishing Assumption

The registry stores one canonical base coordinate per extension. Consumers are expected to resolve the standard BTrace extension artifact layout from that coordinate.
