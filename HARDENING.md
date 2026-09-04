<!-- markdownlint-disable -->

# Hardening Report: editorconfig-checker--action-editorconfig-checker/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **editorconfig-checker--action-editorconfig-checker/v3.0.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file ci.yml has no top-level `permissions:` key and neither of its jobs (`dirty`, `test`) defines a job-level `permissions:` block. This means the workflow runs with the default (potentially broad) GITHUB_TOKEN permissions.

Locations:

- `.github/workflows/ci.yml:1`

### unpinned-uses (severity: high)

ci.yml references actions by mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if the tag is moved. Failing references: `actions/checkout@v6` (line 14), `actions/setup-node@v6` (line 15), `actions/checkout@v6` (line 23), `uses: ./` is local and acceptable.

Locations:

- `.github/workflows/ci.yml:14`
- `.github/workflows/ci.yml:15`
- `.github/workflows/ci.yml:23`

### unpinned-uses (severity: high)

dependabot-automerge.yaml references an action by a mutable version tag instead of a full 40-character commit SHA. Failing reference: `dependabot/fetch-metadata@v1`.

Locations:

- `.github/workflows/dependabot-automerge.yaml:12`

### unpinned-uses (severity: high)

regen-dist.yaml references actions by mutable version tags instead of full 40-character commit SHAs. Failing references: `actions/checkout@v6`, `actions/setup-node@v6`, `stefanzweifel/git-auto-commit-action@v7`.

Locations:

- `.github/workflows/regen-dist.yaml:18`
- `.github/workflows/regen-dist.yaml:21`
- `.github/workflows/regen-dist.yaml:25`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

1. ci.yml: Added top-level `permissions: contents: read` block to address missing-permissions finding. Pinned actions/checkout@v6 (both occurrences, lines 14 and 23) to SHA d23441a48e516b6c34aea4fa41551a30e30af803 and actions/setup-node@v6 (line 15) to SHA 249970729cb0ef3589644e2896645e5dc5ba9c38. 2. dependabot-automerge.yaml: Pinned dependabot/fetch-metadata@v1 (line 12) to SHA 8348ea7f5d949b08c7f125a44b569c9626b05db3. This file already had a permissions block. 3. regen-dist.yaml: Pinned actions/checkout@v6 to SHA d23441a48e516b6c34aea4fa41551a30e30af803, actions/setup-node@v6 to SHA 249970729cb0ef3589644e2896645e5dc5ba9c38, and stefanzweifel/git-auto-commit-action@v7 to SHA 4a55954c782fc1ea30b9056cd3e7a2b40ca8887d. This file already had a permissions block. All SHAs were resolved via lookup_action_sha and original tag names are preserved as inline comments.

