<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references are pinned to mutable version tags instead of immutable 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if the tag is moved. Failing references in ci.yml: `actions/checkout@v4` (two occurrences), `actions/setup-node@v4`. Failing reference in dependabot-automerge.yaml: `dependabot/fetch-metadata@v1`.

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:10`
- `.github/workflows/ci.yml:21`
- `.github/workflows/dependabot-automerge.yaml:12`

### missing-permissions (severity: medium)

The workflow file ci.yml has no top-level `permissions:` key and neither of its jobs (`dirty`, `test`) defines a job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g. `write` access to contents). A minimal `permissions:` block such as `contents: read` should be added.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action references by pinning to full commit SHAs: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (two occurrences in ci.yml), actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020 (ci.yml), dependabot/fetch-metadata@v1 → @8348ea7f5d949b08c7f125a44b569c9626b05db3 (dependabot-automerge.yaml). Added top-level `permissions: contents: read` to ci.yml to enforce least-privilege token access. The dependabot-automerge.yaml already had a permissions block so no change was needed there.

