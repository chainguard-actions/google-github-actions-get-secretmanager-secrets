<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-secretmanager-secrets/v2.2.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--get-secretmanager-secrets/v2.2.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three workflow files reference external actions or reusable workflows using mutable version tags instead of full 40-character commit SHAs. Although these are marked `# ratchet:exclude`, they remain unpinned and are vulnerable to supply-chain attacks if the referenced tag is moved or compromised.

- `.github/workflows/draft-release.yml`: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'`
- `.github/workflows/release.yml`: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'`
- `.github/workflows/integration.yml`: `uses: 'google-github-actions/auth@v2'`

Locations:

- `.github/workflows/draft-release.yml:16`
- `.github/workflows/release.yml:9`
- `.github/workflows/integration.yml:34`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all three unpinned action/workflow references to their full commit SHAs:
1. `.github/workflows/draft-release.yml`: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
2. `.github/workflows/release.yml`: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
3. `.github/workflows/integration.yml`: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`

All SHAs were resolved using lookup_action_sha. The `# ratchet:exclude` comments were replaced with human-readable tag comments (`# v3`, `# v2`) to preserve readability.

