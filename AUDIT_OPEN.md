# Open audit items

Unresolved findings for this repository from the ChatGPT-led audit series
(2026-09-09 through 2026-09-11, passes 1-5; register:
teploy-neutron-lullmail expanded audit). Every P0/P1 finding has been fixed
and verified; the P2/P3 tail below is what remains.

Open items: 0

## Resolved from this register

- useteploy__scoop-bucket-01 — fixed 2026-09-11:
  - `.github/workflows/validate.yml` (weekly + push/PR): a freshness job
    fails loudly when teploy.json's version is behind the latest
    useteploy/teploy-cli GitHub release, and a windows-latest job
    installs from the checked-in manifest (real download + scoop hash
    verification), runs `teploy version` against the manifest version,
    and independently verifies the ARM64 asset's SHA-256.
  - checkver/autoupdate deliberately NOT added: goreleaser's scoops
    generator does not carry those fields (a manual edit would be
    clobbered by the next release push), and autoupdate would race the
    authoritative publisher (teploy-cli's release pipeline). The CI job
    is the freshness signal.

## Findings surfaced while fixing (not this repo's to fix)

- The staleness this item predicted is LIVE as of 2026-09-11: upstream
  teploy-cli is at v0.1.33 while this bucket (and the homebrew tap) last
  advanced at v0.1.30 — the goreleaser tap/bucket publish step has been
  failing since v0.1.31 (most likely the HOMEBREW_TAP_GITHUB_TOKEN in
  teploy-cli's release workflow). Needs attention in teploy-cli's release
  config/secrets; the new freshness job will stay red until then.
