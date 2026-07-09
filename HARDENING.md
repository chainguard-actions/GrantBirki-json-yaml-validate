<!-- markdownlint-disable -->

# Hardening Report: GrantBirki--json-yaml-validate/v2.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **GrantBirki--json-yaml-validate/v2.4.0** was hardened automatically. 8 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

One or more `uses:` references in this workflow use mutable tags instead of pinned 40-character commit SHAs. Unpinned actions are vulnerable to supply-chain attacks if the tag is moved. Failing references: `actions/checkout@v4`.

Locations:

- `.github/workflows/acceptance-test.yml:16`

### unpinned-uses (severity: high)

One or more `uses:` references in this workflow use mutable tags instead of pinned 40-character commit SHAs. Failing references: `actions/checkout@v4`, `github/codeql-action/init@v2`, `github/codeql-action/autobuild@v2`, `github/codeql-action/analyze@v2`.

Locations:

- `.github/workflows/codeql-analysis.yml:22`
- `.github/workflows/codeql-analysis.yml:27`
- `.github/workflows/codeql-analysis.yml:33`
- `.github/workflows/codeql-analysis.yml:37`

### unpinned-uses (severity: high)

One or more `uses:` references in this workflow use mutable tags instead of pinned 40-character commit SHAs. Failing references: `actions/checkout@v4`, `actions/setup-node@v4`.

Locations:

- `.github/workflows/lint.yml:10`
- `.github/workflows/lint.yml:13`

### unpinned-uses (severity: high)

One or more `uses:` references in this workflow use mutable tags instead of pinned 40-character commit SHAs. Failing references: `actions/checkout@v4`, `actions/setup-node@v4`.

Locations:

- `.github/workflows/package-check.yml:14`
- `.github/workflows/package-check.yml:17`

### unpinned-uses (severity: high)

One or more `uses:` references in this workflow use mutable tags instead of pinned 40-character commit SHAs. Failing references: `actions/checkout@v4`, `actions/setup-node@v4`.

Locations:

- `.github/workflows/test.yml:11`
- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

This workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad.

Locations:

- `.github/workflows/lint.yml:1`

### missing-permissions (severity: medium)

This workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad.

Locations:

- `.github/workflows/package-check.yml:1`

### missing-permissions (severity: medium)

This workflow has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 8 findings across 5 workflow files:
- acceptance-test.yml: Pinned actions/checkout@v4 → SHA 34e114876b0b11c390a56381ad16ebd13914f8d5 (already had permissions block)
- codeql-analysis.yml: Pinned actions/checkout@v4 → SHA 34e114876b0b11c390a56381ad16ebd13914f8d5; github/codeql-action/init@v2, autobuild@v2, analyze@v2 → SHA b8d3b6e8af63cde30bdc382c0bc28114f4346c88 (already had job-level permissions)
- lint.yml: Pinned actions/checkout@v4 and actions/setup-node@v4 to full SHAs; added top-level permissions: contents: read
- package-check.yml: Pinned actions/checkout@v4 and actions/setup-node@v4 to full SHAs; added top-level permissions: contents: read
- test.yml: Pinned actions/checkout@v4 and actions/setup-node@v4 to full SHAs; added top-level permissions: contents: read

