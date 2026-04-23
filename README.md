# GitHub Actions Catalog

Public catalog of reusable GitHub Actions workflows focused on standardization, reuse, and centralized CI/CD pipeline maintenance.

This repository does not run its own product pipelines. It provides reusable workflows meant to be consumed by other repositories.

## Goals

- Avoid pipeline duplication across projects
- Standardize CI across multiple repositories
- Centralize workflow maintenance and evolution
- Ensure predictability through explicit versioning

## What this catalog contains

- Reusable workflows defined with `workflow_call`
- Mirrored documentation for each workflow
- A clear versioning policy
- A scalable structure for new workflow types

## Repository structure

```text
.
├── .github/
│   ├── copilot-instructions.md
│   └── workflows/
│       └── ci-nodejs.yml
├── docs/
│   ├── README.md
│   ├── usage.md
│   ├── versioning.md
│   └── ci-nodejs.md
├── AGENTS.md
├── CLAUDE.md
└── README.md
```

### Mirroring principle

For each workflow in:

```text
.github/workflows/file.yml
```

there should be corresponding documentation in:

```text
docs/file.md
```

GitHub Actions requires reusable workflows to live at the root of `.github/workflows/`.

## Available workflows

### CI

- Node.js
  - Workflow: `.github/workflows/ci-nodejs.yml`
  - Documentation: `docs/ci-nodejs.md`

## How to use

These workflows are meant to be consumed from other repositories with `uses`.

Example:

```yaml
jobs:
  ci:
    uses: ORG/REPO/.github/workflows/ci-nodejs.yml@v1.1.0
    with:
      node-version: 20
```

Read these documents before integration:

- `docs/README.md`
- `docs/usage.md`
- `docs/versioning.md`
- The mirrored `.md` file for the workflow you want to use

## Versioning

- The catalog follows semantic versioning
- Consumers should use versioned tags
- Floating references such as `main` are not supported

See `docs/versioning.md` for details.

## Repository principles

- Each workflow should be self-contained
- Documentation should remain local and specific
- Global rules should live in `docs/`
- Behavior changes should follow explicit versioning
- Clarity should take priority over convenience
- All code, comments, and documentation should be written in English

## Documentation

- Index: `docs/README.md`
- General usage: `docs/usage.md`
- Node.js CI: `docs/ci-nodejs.md`

## Status

This catalog is ready to grow with additional workflows, such as:

- Frontend CI
- Backend CI
- Library CI
- Monorepo CI
- CD / release workflows

Contributions should preserve the mirroring pattern and keep all repository content in English.
