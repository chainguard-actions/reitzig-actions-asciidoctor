<!-- markdownlint-disable -->

# Hardening Report: reitzig--actions-asciidoctor/v2.0.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **reitzig--actions-asciidoctor/v2.0.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in .github/workflows/test.yml are pinned to mutable tags rather than full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved or overwritten:
- `actions/checkout@v4` (line 30) — should be pinned to a SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`
- `ruby/setup-ruby@v1` (line 33) — should be pinned to a SHA, e.g. `ruby/setup-ruby@<full-sha> # v1`

Locations:

- `.github/workflows/test.yml:30`
- `.github/workflows/test.yml:33`

### missing-permissions (severity: medium)

The workflow file .github/workflows/test.yml has no top-level `permissions:` key, and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be write-all), granting the GITHUB_TOKEN broader access than necessary. A minimal permissions block (e.g. `permissions: contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `actions/checkout@v4` to SHA `34e114876b0b11c390a56381ad16ebd13914f8d5` and `ruby/setup-ruby@v1` to SHA `003a5c4d8d6321bd302e38f6f0ec593f77f06600`, preserving the original tags as inline comments. (2) Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum access needed for the workflow (repository checkout).

