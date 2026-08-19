<!-- markdownlint-disable -->

# Hardening Report: reitzig--actions-asciidoctor/v2.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **reitzig--actions-asciidoctor/v2.0.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses tag-based (non-SHA-pinned) action references, making it vulnerable to supply-chain attacks if the referenced tags are moved or overwritten. Specifically: `actions/checkout@v7` and `ruby/setup-ruby@v1` should each be pinned to a full 40-character commit SHA (e.g., `actions/checkout@<sha> # v7`).

Locations:

- `.github/workflows/test.yml:30`
- `.github/workflows/test.yml:33`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block (e.g., `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Added top-level `permissions: contents: read` block to restrict default token permissions. (2) Pinned `actions/checkout@v7` to SHA `3d3c42e5aac5ba805825da76410c181273ba90b1 # v7`. (3) Pinned `ruby/setup-ruby@v1` to SHA `003a5c4d8d6321bd302e38f6f0ec593f77f06600 # v1`.

