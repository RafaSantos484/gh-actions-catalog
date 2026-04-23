# Reusable Workflow Usage

This catalog provides reusable GitHub Actions workflows meant to be consumed from other repositories through `uses`.

## Workflow type

All workflows in this catalog are reusable workflows defined with:

```yaml
on:
  workflow_call:
```

They are not intended to run directly in this repository.

## How to use from a consumer repository

In the consuming repository, create a workflow such as:

```text
.github/workflows/ci.yml
```

Minimal example:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: ORG/REPO/.github/workflows/path.yml@TAG
    with:
      example-input: value
```

## Workflow reference

- The workflow path must be exact.
- The referenced file must live at the repository root inside `.github/workflows/`.
- The repository may be public or private.
- Always reference a versioned tag or a specific commit SHA.

Valid example from this catalog:

```yaml
uses: ORG/REPO/.github/workflows/ci-nodejs.yml@v1.1.0
```

Correct:

```text
@v1.1.0
```

Avoid:

```text
@main
```

## Inputs

Each workflow defines its own inputs.

Always read the corresponding documentation file in `docs/**` before integrating a workflow.

## Good practices

- Read the workflow-specific documentation before adoption.
- Do not assume implicit scripts or behavior.
- Upgrade versions deliberately.
- Treat CI failures as blocking.

## Where to find documentation

- General rules: files at the root of `docs/`
- Node.js CI workflow: `docs/ci-nodejs.md`
- Each workflow should have a matching `.md` file for its `.yml`
