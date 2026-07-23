# mixa-plugins — the Mixa Plugin catalog

Plugins are **not part of the Mixa app release**. The app fetches `catalog.json` from this
repository, shows what is available, and downloads a Plugin's tarball from the matching GitHub
release — verifying its sha256 against the catalog entry before installing it into the machine's
Plugins folder. See `docs/plugin-distribution.md` in the main Mixa repo for the binding decision.

## What's here

- `catalog.json` — the generated catalog. **Never hand-edit**; it is produced by
  `scripts/build-plugin-catalog.mjs` in the main repo and pushed by the publish workflow.
- Releases — one tag per Plugin version (`<id>-v<version>`) holding `<id>-<version>.tar.gz`:
  the plugin layer (Mixa-owned adapter code, compiled). External upstream artifacts are never in
  the tarball; each Plugin acquires those itself on install, pinned and sha256-verified.

## Trust

The app verifies every tarball's sha256 against this catalog before extraction. A tampered
artifact fails closed. Catalog signing is a deferred hardening step.
