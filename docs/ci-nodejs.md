# CI Node.js

Reusable CI workflow for **Node.js** projects.

This document describes only:

```text
.github/workflows/ci-nodejs.yml
```

## What this workflow does

This CI runs the main validation and build steps for a Node.js project in parallel.

| Job | Script |
| --- | --- |
| Typecheck | `typecheck` |
| Format Check | `format:check` |
| Lint | `lint` |
| Tests | `test:run` |
| Build | `build` |

If any job fails, the workflow fails.

## How it is triggered

This is a reusable workflow defined with `on.workflow_call`.

It does not run by itself and must be consumed from another repository with `uses`.

## Inputs

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `node-version` | string | Yes | - | Node.js version |
| `package-manager` | string | No | `""` | `npm`, `pnpm`, or `yarn`. Empty means auto-detection |
| `pnpm-version` | string | No | `"9"` | pnpm version used when the selected manager is `pnpm` |

Example:

```yaml
with:
  node-version: 20
```

Example with explicit package manager:

```yaml
with:
  node-version: 20
  package-manager: pnpm
  pnpm-version: 9
```

## Package manager behavior

The workflow supports `npm`, `pnpm`, and `yarn`.

When `package-manager` is empty, detection is based on the repository lockfile:

| Manager | Lockfile | Install command | Script command |
| --- | --- | --- | --- |
| `npm` | `package-lock.json` | `npm ci` | `npm run <script>` |
| `pnpm` | `pnpm-lock.yaml` | `pnpm install --frozen-lockfile` | `pnpm run <script>` |
| `yarn` | `yarn.lock` | `yarn install --frozen-lockfile` | `yarn <script>` |

Rules:

- If no supported lockfile is found, the workflow fails early.
- If multiple supported lockfiles are found, the workflow fails early and requires `package-manager` to be set explicitly.
- If `package-manager` is set but its lockfile is missing, the workflow fails early.

This avoids silent installs with the wrong package manager.

## Scripts required in the consumer project

The consumer project must define these scripts in `package.json`:

```json
{
  "scripts": {
    "typecheck": "...",
    "format:check": "...",
    "lint": "...",
    "test:run": "...",
    "build": "..."
  }
}
```

The script names must match exactly.

## Technical notes

- A `prepare` job detects the package manager once and shares the result with all CI jobs.
- The validation/build jobs run as a matrix, which keeps the workflow shorter and easier to maintain.
- `actions/setup-node` cache is configured with the selected package manager and its lockfile.
- `corepack enable` is used for Yarn.
- `pnpm/action-setup` is used only when the selected manager is `pnpm`.

## Usage example

```yaml
jobs:
  ci-nodejs:
    uses: ORG/gh-actions-catalog/.github/workflows/ci-nodejs.yml@v1.1.0
    with:
      node-version: 20
```

Example with an explicit override:

```yaml
jobs:
  ci-nodejs:
    uses: ORG/gh-actions-catalog/.github/workflows/ci-nodejs.yml@v1.1.0
    with:
      node-version: 20
      package-manager: yarn
```

## Related documentation

- General usage: `docs/usage.md`
- Catalog versioning: `docs/versioning.md`
