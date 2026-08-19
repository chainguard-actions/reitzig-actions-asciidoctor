<!-- markdownlint-disable -->

# Hardening Report: reitzig--actions-asciidoctor/v2.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **reitzig--actions-asciidoctor/v2.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file references two Actions using mutable tag refs instead of full 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks if the tag is moved or the upstream repository is compromised.

Offending lines:
- `uses: actions/checkout@v3` (tag: v3)
- `uses: ruby/setup-ruby@v1` (tag: v1)

These should be pinned to their full SHA digests, e.g.:
  `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`

Locations:

- `.github/workflows/test.yml:27`
- `.github/workflows/test.yml:30`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g., write access to contents). A minimal permissions block such as `permissions: read-all` or specific scopes (e.g., `contents: read`) should be added.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/test.yml: (1) Pinned `actions/checkout@v3` to SHA `a37ce9120846195fa4ece8f58b268e6043cb2f26` and `ruby/setup-ruby@v1` to SHA `a30dfa457ad68707b8b910ac3a244714b61c0626`, preserving the original tags as inline comments. (2) Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required scope.

