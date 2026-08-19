<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-secretmanager-secrets/v2.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--get-secretmanager-secrets/v2.2.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tag/version refs instead of pinned 40-character SHA commit digests, making the workflows vulnerable to supply-chain attacks if the tag is moved.

Failing references:
- draft-release.yml: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v0'`
- integration.yml: `uses: 'actions/checkout@v4'`, `uses: 'actions/setup-node@v4'`, `uses: 'google-github-actions/auth@v2'`
- release.yml: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v0'`
- unit.yml: `uses: 'actions/checkout@v4'`, `uses: 'actions/setup-node@v4'`

Locations:

- `.github/workflows/draft-release.yml:17`
- `.github/workflows/integration.yml:26`
- `.github/workflows/integration.yml:29`
- `.github/workflows/integration.yml:35`
- `.github/workflows/release.yml:12`
- `.github/workflows/unit.yml:31`
- `.github/workflows/unit.yml:34`

### script-injection (severity: high)

Two `run:` steps in integration.yml directly interpolate `${{ steps.secrets.outputs.* }}` expressions (a `steps.*.outputs.*` workflow-controllable context) inside shell commands, violating sub-rule (a). If the secret values contain shell metacharacters, this could lead to command injection.

Offending lines:
- `run: echo '${{ steps.secrets.outputs.token }}${{ steps.secrets.outputs.password }}${{ steps.secrets.outputs.regional }}'`
- `run: echo '${{ steps.secrets-encoded.outputs.token }}${{ steps.secrets-encoded.outputs.password }}${{ steps.secrets-encoded.outputs.regional }}'`

These expressions should be passed via `env:` variables and the env vars should be double-quoted in the shell command.

Locations:

- `.github/workflows/integration.yml:44`
- `.github/workflows/integration.yml:55`

### missing-permissions (severity: medium)

Three workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the default token permissions (which may be broad) are used.

- draft-release.yml: no top-level or job-level permissions defined.
- release.yml: no top-level or job-level permissions defined.
- unit.yml: no top-level or job-level permissions defined.

(integration.yml passes because its single job has explicit job-level permissions.)

Locations:

- `.github/workflows/draft-release.yml:1`
- `.github/workflows/release.yml:1`
- `.github/workflows/unit.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, script-injection, missing-permissions

**Notes:**

Fixed all three findings across four workflow files: (1) Pinned all mutable action/workflow references to full 40-char SHAs with tag comments in integration.yml, unit.yml, draft-release.yml, and release.yml. (2) Fixed script injection in integration.yml by moving ${{ steps.secrets.outputs.* }} expressions into env: blocks and using double-quoted env vars in shell commands. (3) Added top-level 'permissions: {}' to draft-release.yml, release.yml, and unit.yml (integration.yml already had job-level permissions).

