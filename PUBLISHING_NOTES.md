# Drift Control Packet Public Root

This directory is the standalone publication root for the drift-control guide.

## Contents

- `README.md`: one-file guide for Docsify and GitHub Pages
- `index.html`: Docsify entrypoint
- `_sidebar.md`: Docsify sidebar
- `.nojekyll`: disables Jekyll processing on GitHub Pages

## Source Of Truth

This publication root is derived from:

- `runbook-tooling/workstreams/drift-control-packet-dev-path/DRIFT_CONTROL_PACKET.md`
- `runbook-tooling/workstreams/drift-control-packet-dev-path/docsify-site/`

## Publishing Options

1. Use this directory as the content root in a separate repo.
2. Publish it with GitHub Pages.
3. If needed later, add a GitHub Pages Actions workflow in the destination repo.

## Boundary

This directory is intended for public delivery.
The split packet, workstream state, artifacts, and repo-specific archive remain outside this root.
