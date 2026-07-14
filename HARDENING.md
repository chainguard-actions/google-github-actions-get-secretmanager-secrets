<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--get-secretmanager-secrets/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **google-github-actions--get-secretmanager-secrets/v2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three workflow files contain `uses:` references pinned to mutable tags rather than immutable 40-character commit SHAs, making them vulnerable to supply-chain attacks if the tag is moved:
- `.github/workflows/draft-release.yml`: `google-github-actions/.github/.github/workflows/draft-release.yml@v3`
- `.github/workflows/integration.yml`: `google-github-actions/auth@v2`
- `.github/workflows/release.yml`: `google-github-actions/.github/.github/workflows/release.yml@v3`

These should be pinned to full SHA digests (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683`).

Locations:

- `.github/workflows/draft-release.yml:16`
- `.github/workflows/integration.yml:33`
- `.github/workflows/release.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all three mutable tag references to immutable full commit SHAs:
- draft-release.yml: google-github-actions/.github@v3 → @29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3
- integration.yml: google-github-actions/auth@v2 → @c200f3691d83b41bf9bbd8638997a462592937ed # v2
- release.yml: google-github-actions/.github@v3 → @29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3
All SHAs were resolved via lookup_action_sha and the original tag is preserved as a comment for readability.

