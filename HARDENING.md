<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references actions using mutable version tags instead of pinned full-length SHA digests. Specifically: `actions/checkout@v2` (used twice, lines 10 and 23) and `actions/setup-node@v2` (line 11). These tags can be moved to point to different, potentially malicious commits at any time, enabling supply-chain attacks.

Locations:

- `.github/workflows/ci.yml:10`
- `.github/workflows/ci.yml:11`
- `.github/workflows/ci.yml:23`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key, and neither the `dirty` job nor the `test` job defines a job-level `permissions:` block. Without explicit permissions, the workflow inherits the default repository token permissions, which may be overly broad (write access to contents, etc.). Minimal specific permissions should be declared.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/ci.yml: (1) Pinned actions/checkout@v2 to SHA 0717577d45739eb3c851188b29f50ed6c0b2194e (used twice, lines 10 and 23) and actions/setup-node@v2 to SHA 7c12f8017d5436eb855f1ed4399f037a36fbd9e8 (line 11), preserving the original tag as inline comments. (2) Added top-level `permissions: {}` to deny all permissions by default, and added `permissions: { contents: read }` to both the `dirty` and `test` jobs since they both need to check out repository contents.

