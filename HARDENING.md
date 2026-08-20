<!-- markdownlint-disable -->

# Hardening Report: NejcZdovc--comment-pr/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **NejcZdovc--comment-pr/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/example.yml uses action references pinned to mutable tags rather than immutable full-length SHA digests. This exposes the workflow to supply-chain attacks if the upstream action tag is moved or compromised. Failing references:
- `uses: actions/checkout@v3` (lines ~10 and ~30)
- `uses: actions/github-script@v6` (lines ~13 and ~33)
These should be pinned to their full 40-character commit SHAs, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/example.yml:10`
- `.github/workflows/example.yml:13`
- `.github/workflows/example.yml:30`
- `.github/workflows/example.yml:33`

### missing-permissions (severity: medium)

The workflow file .github/workflows/example.yml has no top-level `permissions:` key, and neither of its jobs (`body`, `file`) defines a `permissions:` block. Without explicit permissions, the workflow inherits the default repository permissions (which may include broad write access). A minimal permissions block such as `permissions: { pull-requests: write, contents: read }` should be added at the top level or per-job.

Locations:

- `.github/workflows/example.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/example.yml: (1) Pinned all four action references to full commit SHAs — actions/checkout@v3 → @a37ce9120846195fa4ece8f58b268e6043cb2f26 and actions/github-script@v6 → @d7906e4ad0b1822421a7e6a35d5ca353c962f410, with original tags preserved as comments. (2) Added a top-level `permissions:` block with `pull-requests: write` (required to post PR comments) and `contents: read` (required for checkout).

