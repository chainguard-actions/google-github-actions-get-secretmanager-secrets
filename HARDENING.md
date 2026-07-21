<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-secretmanager-secrets/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--get-secretmanager-secrets/v2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three `uses:` references in workflow files use mutable version tags instead of full 40-character commit SHA hashes, making the workflows vulnerable to supply-chain attacks if the referenced tag is moved or overwritten:
- `.github/workflows/draft-release.yml` line 17: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'` (tagged, not SHA-pinned)
- `.github/workflows/integration.yml` line 35: `uses: 'google-github-actions/auth@v2'` (tagged, not SHA-pinned)
- `.github/workflows/release.yml` line 10: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'` (tagged, not SHA-pinned)
All three are annotated with `# ratchet:exclude`, which suppresses ratchet tooling but does not eliminate the supply-chain risk. Each should be pinned to a full 40-character commit SHA with the tag preserved as a comment.

Locations:

- `.github/workflows/draft-release.yml:17`
- `.github/workflows/integration.yml:35`
- `.github/workflows/release.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all three unpinned `uses:` references to full 40-character commit SHAs:
- `.github/workflows/draft-release.yml`: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
- `.github/workflows/integration.yml`: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`
- `.github/workflows/release.yml`: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
The `# ratchet:exclude` comments were replaced with the version tag as a comment for readability. SHAs were resolved using lookup_action_sha.

