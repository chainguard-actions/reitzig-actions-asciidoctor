<!-- markdownlint-disable -->

# Hardening Report: reitzig--actions-asciidoctor/v2.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **reitzig--actions-asciidoctor/v2.0.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses mutable tag refs instead of pinned SHA digests, making the action vulnerable to supply-chain attacks if the referenced tags are moved or overwritten. Failing references: `actions/checkout@v6` (line 30) and `ruby/setup-ruby@v1` (line 33). These should be replaced with full 40-character commit SHAs, e.g. `actions/checkout@<sha> # v6`.

Locations:

- `.github/workflows/test.yml:30`
- `.github/workflows/test.yml:33`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g. write access to contents). A minimal `permissions:` block such as `permissions: read-all` or specific scopes (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Added top-level `permissions: contents: read` block to restrict the default token permissions. (2) Pinned `actions/checkout@v6` to SHA `df4cb1c069e1874edd31b4311f1884172cec0e10` and `ruby/setup-ruby@v1` to SHA `003a5c4d8d6321bd302e38f6f0ec593f77f06600`, with the original tag preserved as inline comments.

