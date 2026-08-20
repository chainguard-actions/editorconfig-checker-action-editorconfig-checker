<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v2.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v2.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable tag-based refs instead of immutable full SHA digests, making the workflows vulnerable to supply-chain attacks if the referenced tags are moved or overwritten.

Failing references:
- ci.yml: `actions/checkout@v6`, `actions/setup-node@v6` (used twice each)
- dependabot-automerge.yaml: `dependabot/fetch-metadata@v1`
- regen-dist.yaml: `actions/checkout@v6`, `actions/setup-node@v6`, `stefanzweifel/git-auto-commit-action@v7`

All should be pinned to their full 40-character commit SHA, e.g. `actions/checkout@<sha> # v6`.

Locations:

- `.github/workflows/ci.yml:10`
- `.github/workflows/ci.yml:11`
- `.github/workflows/ci.yml:20`
- `.github/workflows/ci.yml:21`
- `.github/workflows/dependabot-automerge.yaml:12`
- `.github/workflows/regen-dist.yaml:21`
- `.github/workflows/regen-dist.yaml:23`
- `.github/workflows/regen-dist.yaml:26`

### missing-permissions (severity: medium)

The workflow file ci.yml has no top-level `permissions:` key and neither of its jobs (`dirty`, `test`) defines a job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents and other scopes). A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 8 unpinned action references by pinning them to full 40-character commit SHAs (with original tags preserved as comments): actions/checkout@v6→d23441a4, actions/setup-node@v6→249970729, dependabot/fetch-metadata@v1→8348ea7f, stefanzweifel/git-auto-commit-action@v7→4a55954c. Added top-level `permissions: contents: read` to ci.yml to satisfy the missing-permissions finding.

