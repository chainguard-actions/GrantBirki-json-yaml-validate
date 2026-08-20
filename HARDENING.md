<!-- markdownlint-disable -->

# Hardening Report: GrantBirki--json-yaml-validate/v3.3.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **GrantBirki--json-yaml-validate/v3.3.2** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (a) violation: workflow_dispatch inputs are interpolated directly into run: shell commands in update-latest-release-tag.yml. The expressions `${{ github.event.inputs.major_version_tag }}` and `${{ github.event.inputs.source_tag }}` are embedded directly in shell commands, allowing an attacker with workflow_dispatch access to inject arbitrary shell commands. Offending lines: `run: git tag -f ${{ github.event.inputs.major_version_tag }} ${{ github.event.inputs.source_tag }}` and `run: git push origin ${{ github.event.inputs.major_version_tag }} --force`. These inputs should be passed via env: variables and then double-quoted in the shell.

Locations:

- `.github/workflows/update-latest-release-tag.yml:33`
- `.github/workflows/update-latest-release-tag.yml:36`

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable tag-based refs (@v4, @v3) instead of immutable 40-character commit SHAs. This exposes the workflows to supply-chain attacks if the referenced tags are moved or compromised. Unpinned references found:
- acceptance.yml: actions/checkout@v4
- codeql-analysis.yml: actions/checkout@v4, github/codeql-action/init@v3, github/codeql-action/autobuild@v3, github/codeql-action/analyze@v3
- copilot-setup-steps.yml: actions/checkout@v4, actions/setup-node@v4
- lint.yml: actions/checkout@v4, actions/setup-node@v4
- package-check.yml: actions/checkout@v4, actions/setup-node@v4
- test.yml: actions/checkout@v4, actions/setup-node@v4
- update-latest-release-tag.yml: actions/checkout@v4

Locations:

- `.github/workflows/acceptance.yml:14`
- `.github/workflows/codeql-analysis.yml:18`
- `.github/workflows/codeql-analysis.yml:23`
- `.github/workflows/codeql-analysis.yml:29`
- `.github/workflows/codeql-analysis.yml:33`
- `.github/workflows/copilot-setup-steps.yml:14`
- `.github/workflows/copilot-setup-steps.yml:19`
- `.github/workflows/lint.yml:10`
- `.github/workflows/lint.yml:13`
- `.github/workflows/package-check.yml:13`
- `.github/workflows/package-check.yml:17`
- `.github/workflows/test.yml:10`
- `.github/workflows/test.yml:13`
- `.github/workflows/update-latest-release-tag.yml:22`

### missing-permissions (severity: medium)

Three workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, workflows inherit the default repository token permissions, which may be broader than necessary. Affected files: lint.yml, package-check.yml, test.yml.

Locations:

- `.github/workflows/lint.yml:1`
- `.github/workflows/package-check.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, unpinned-uses, missing-permissions

**Notes:**

Fixed all three findings: (1) script-injection in update-latest-release-tag.yml — moved workflow_dispatch inputs major_version_tag and source_tag into env: blocks and double-quoted them in shell commands; (2) unpinned-uses — pinned all 14 action references across 7 workflow files to their full 40-char commit SHAs (actions/checkout@v4→11d5960a, actions/setup-node@v4→49933ea5, github/codeql-action/*@v3→f3712979); (3) missing-permissions — added top-level `permissions: contents: read` to lint.yml, package-check.yml, and test.yml.

