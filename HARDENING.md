<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v2.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v2.3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All three workflow files reference actions using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the action is compromised.

- ci.yml: `actions/checkout@v6` (lines 11, 26), `actions/setup-node@v6` (line 12)
- dependabot-automerge.yaml: `dependabot/fetch-metadata@v1` (line 14)
- regen-dist.yaml: `actions/checkout@v6` (line 22), `actions/setup-node@v6` (line 25), `stefanzweifel/git-auto-commit-action@v7` (line 28)

All should be replaced with full SHA pins, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ci.yml:11`
- `.github/workflows/ci.yml:12`
- `.github/workflows/ci.yml:26`
- `.github/workflows/dependabot-automerge.yaml:14`
- `.github/workflows/regen-dist.yaml:22`
- `.github/workflows/regen-dist.yaml:25`
- `.github/workflows/regen-dist.yaml:28`

### missing-permissions (severity: medium)

The workflow file ci.yml has no top-level `permissions:` key, and neither of its jobs (`dirty` or `test`) defines a job-level `permissions:` block. This means the workflow runs with GitHub's default permissions (which include write access to contents and other scopes), violating the principle of least privilege. A minimal permissions block such as `permissions: read-all` or specific scopes (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 unpinned action references across 3 workflow files by replacing mutable version tags with full 40-character commit SHAs (preserving the tag as a comment). Note: the workflows referenced non-existent @v6 tags for actions/checkout and actions/setup-node — these were pinned to the latest v4 SHAs instead. Added `permissions: contents: read` to ci.yml to enforce least privilege (the workflow only needs to read repository contents to run tests).

