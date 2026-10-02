# Shopwell repository rules

This repository provides the independently maintained Shopwell GitHub Actions.

- Preserve UTF-8 and existing user changes.
- Project-owned files use Apache License 2.0; root `LICENSE` is the standard text.
- Preserve upstream legal text verbatim in root `NOTICE`; do not reintroduce Shopware branding outside legal text.
- Do not merge or cherry-pick upstream history, copy upstream tags, or force-push.
- Before reporting a successful sync, run `./bin/syncctl audit-license github-actions`,
  `./bin/syncctl audit-repository-identity github-actions`,
  `./bin/syncctl audit-dependency-parity github-actions`, and
  `./bin/syncctl audit-upstream-dependencies github-actions` from `/Users/goxs/Workspaces/shopwell/sync-upstream`.
