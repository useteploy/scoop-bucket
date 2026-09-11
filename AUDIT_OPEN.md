# Open audit items

Unresolved findings for this repository from the ChatGPT-led audit series (2026-09-09 through 2026-09-11, passes 1-5; register: teploy-neutron-lullmail expanded audit). Every P0/P1 finding has been fixed and verified; the items below are the remaining P2/P3 tail plus one item needing validation. Fields are quoted from the audit register; line references point at the review commits listed per item where recorded.

Open items: 1 P2 (1 total)

## useteploy__scoop-bucket-01 - P2 - Open improvement

**Make release freshness and Windows installation checks explicit**

- Kind: Improvement
- Evidence: teploy.json pins x64/ARM64 v0.1.33 artifacts but has no checkver/autoupdate fields; the bucket has no tracked update/validation workflow. The Homebrew formula reviewed during this audit also pins v0.1.33, so a version mismatch is not established.
- Impact: A failure in any upstream publisher can leave the bucket stale without a repository-local signal.
- Proposed fix: Document the authoritative upstream publisher and add a freshness/asset-validation check there or here. Add checkver/autoupdate only if compatible with that release ownership; avoid competing updaters.
- Acceptance test: On a test release, verify the bucket advances once, both hashes match downloaded assets, and both supported Windows architectures can invoke teploy --version.
- Review commit: `3a7064876290e49be231712c3628ee1b45c87083` (last reviewed 2026-09-10)

