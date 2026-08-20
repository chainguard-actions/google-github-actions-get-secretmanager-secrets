<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-secretmanager-secrets/v2.2.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--get-secretmanager-secrets/v2.2.5** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three `uses:` references are pinned to mutable version tags rather than full 40-character commit SHAs, making them vulnerable to supply-chain attacks if the tag is moved:
- `.github/workflows/draft-release.yml` line 17: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'`
- `.github/workflows/integration.yml` line 38: `uses: 'google-github-actions/auth@v2'`
- `.github/workflows/release.yml` line 11: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'`

All three are annotated with `# ratchet:exclude`, which exempts them from the ratchet pinning tool, but they remain unpinned and should be pinned to immutable commit SHAs.

Locations:

- `.github/workflows/draft-release.yml:17`
- `.github/workflows/integration.yml:38`
- `.github/workflows/release.yml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all three mutable tag references to full commit SHAs:
1. `.github/workflows/draft-release.yml` line 17: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
2. `.github/workflows/integration.yml` line 38: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`
3. `.github/workflows/release.yml` line 11: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
The `# ratchet:exclude` annotations were replaced with the version tag as a human-readable comment.

