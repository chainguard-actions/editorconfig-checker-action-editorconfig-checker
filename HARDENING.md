<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references GitHub Actions using mutable tag refs instead of pinned full-length SHA commit hashes. Unpinned refs are vulnerable to supply-chain attacks if the upstream tag is moved or the repository is compromised. Failing references: `actions/checkout@v2` (lines 9 and 20), `actions/setup-node@v2` (line 10). These should be replaced with their full 40-character SHA digests (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`).

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:10`
- `.github/workflows/ci.yml:20`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key, and neither the `dirty` job nor the `test` job defines its own `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, packages, etc.). A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned actions/checkout@v2 to SHA 0717577d45739eb3c851188b29f50ed6c0b2194e and actions/setup-node@v2 to SHA 7c12f8017d5436eb855f1ed4399f037a36fbd9e8 (both occurrences of checkout). Added top-level `permissions: contents: read` block to restrict default token permissions.

