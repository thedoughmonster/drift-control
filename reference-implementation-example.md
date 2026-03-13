# Reference Implementation Example

This page is optional.

It shows one concrete implementation example of the drift-control model. The rest of the handbook is written to transfer across repositories without depending on the local names, file paths, protocols, or commands listed here.

## How To Use This Appendix

Read the main handbook first.

Use this page only if you want to see how one repository family mapped the generic model onto its own authority surfaces, enforcement entrypoints, and operator workflow.

## Example Repository Roles

| Generic term | Example local term | Example path or surface |
| --- | --- | --- |
| policy authority repo | `runbook-policy` | `runbook-policy/` |
| product implementation repo | `runbook-app` | `runbook-app/` |
| shared tooling repo | `runbook-tooling` | `runbook-tooling/` |
| local retrieval surface | `.code-index` | `.code-index/` |

## Example Authority And Publication Surfaces

| Generic term | Example local term | Example path |
| --- | --- | --- |
| canonical rules bundle | canon bundle JSON | `runbook-policy/canon/**/canon-bundle.json` plus sibling `rules.json`, `coverage.json`, and `source-manifest.json` |
| published contract view | generated markdown contract | `runbook-policy/WORKSPACE_GOVERNANCE.md` |
| routing surface | router file | `runbook-policy/AGENTS.md` |
| decision ledger | direct authority file | `runbook-policy/decisions/DECISION_LOG.md` |
| release policy | direct authority file | `runbook-policy/release/RELEASE_POLICY.md` |

## Example Protocol Names

These protocol names are local to this implementation example. They are not part of the generic model.

| Generic role | Example protocol name | Example path |
| --- | --- | --- |
| full implementation packet | `tempgo` | `runbook-policy/studio/protocols/tempgo-protocol.md` |
| narrow task packet | `tempgo-lite` | `runbook-policy/studio/protocols/tempgo-lite-protocol.md` |
| packet-local seam audit | `tempgo-audit` | `runbook-policy/studio/protocols/tempgo-audit-protocol.md` |
| sequential workstream plan | `tempgo-step-list` | `runbook-tooling/workstreams/drift-control-packet-dev-path/STEP_LIST.md` |
| checkpoint and resume contract | `compaction-contract` | `runbook-policy/studio/protocols/compaction-contract.md` |

## Example Commands

These commands are also specific to this implementation example.

### Canon Maintenance

```bash
node runbook-tooling/scripts/canon.mjs validate runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs generate runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-coverage runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-generated runbook-policy/canon/protocols
```

### Indexed Retrieval

```bash
./.code-index/query-context.sh "lifecycle bootstrap"
./.code-index/query-search.sh "lifecycle bootstrap"
./.code-index/query-docs.sh "architecture conventions"
./.code-index/query-canon.sh --path "runbook-app/scripts/gates/scope-gate.mjs"
```

### Example Enforcement Entrypoints

```bash
pnpm run scope-gate
pnpm run policy-pin-freeze
pnpm run policy-lint
pnpm run quality-gates
```

## Why This Stays In An Appendix

The names and paths on this page help readers who want a concrete reference point, but they are implementation choices rather than part of the transferable handbook model. A different team can adopt the same drift-control architecture with different repository names, commands, protocol labels, and publishing surfaces.
