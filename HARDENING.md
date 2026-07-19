<!-- markdownlint-disable -->

# Hardening Report: GrantBirki--json-yaml-validate/v2.4.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GrantBirki--json-yaml-validate/v2.4.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable tags (e.g. @v4, @v2) instead of full 40-character commit SHA hashes. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references:
- acceptance-test.yml: actions/checkout@v4
- codeql-analysis.yml: actions/checkout@v4, github/codeql-action/init@v2, github/codeql-action/autobuild@v2, github/codeql-action/analyze@v2
- lint.yml: actions/checkout@v4, actions/setup-node@v4
- package-check.yml: actions/checkout@v4, actions/setup-node@v4
- test.yml: actions/checkout@v4, actions/setup-node@v4

Locations:

- `.github/workflows/acceptance-test.yml:14`
- `.github/workflows/codeql-analysis.yml:20`
- `.github/workflows/codeql-analysis.yml:26`
- `.github/workflows/codeql-analysis.yml:31`
- `.github/workflows/codeql-analysis.yml:35`
- `.github/workflows/lint.yml:11`
- `.github/workflows/lint.yml:14`
- `.github/workflows/package-check.yml:13`
- `.github/workflows/package-check.yml:16`
- `.github/workflows/test.yml:11`
- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

Three workflow files have no top-level 'permissions:' key and no job-level 'permissions:' key on any of their jobs. Without explicit permissions, workflows inherit the default repository permissions (which may include write access to contents and other scopes), violating the principle of least privilege.
- lint.yml: no permissions block at top level or job level
- package-check.yml: no permissions block at top level or job level
- test.yml: no permissions block at top level or job level

Locations:

- `.github/workflows/lint.yml:1`
- `.github/workflows/package-check.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all mutable action tag references to full 40-character commit SHAs: actions/checkout@v4 → SHA 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 → SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, and all three github/codeql-action/* @v2 references → SHA b8d3b6e8af63cde30bdc382c0bc28114f4346c88. Added top-level 'permissions: contents: read' blocks to lint.yml, package-check.yml, and test.yml to enforce least privilege. The acceptance-test.yml and codeql-analysis.yml already had permissions blocks and only needed the SHA pinning fix.

