# Catalog Versioning

This repository follows semantic versioning for all reusable workflows published in the catalog.

Versioning applies to the catalog as a whole, not to individual files.

## Convention

Format:

```text
vMAJOR.MINOR.PATCH
```

Meaning:

- `MAJOR`: incompatible changes that may break consumers
- `MINOR`: backward-compatible features or behavior improvements
- `PATCH`: internal fixes that do not change the expected contract

## Examples

- `v1.0.0`: initial stable release
- `v1.1.0`: backward-compatible workflow improvement, such as new optional inputs
- `v2.0.0`: incompatible change, such as removing or renaming inputs

## Consumer rule

Consumers should always reference either:

```yaml
@v1.1.0
```

or a specific commit SHA:

```yaml
@3f2c1a9e4b...
```

Avoid floating references:

```yaml
@main
```

## Rationale

This policy improves:

- pipeline predictability
- build reproducibility
- safety against unexpected breakage
- controlled evolution of the catalog

## Releasing a new version

Any behavior-changing update should include:

1. The correct semantic version increment
2. A new Git tag
3. Updated documentation in the relevant `docs/**` files
