# Drift Control Packet

Standalone publication edition for the drift-control packet.

This document is the one-file reader surface for Docsify and GitHub Pages. It is self-contained by design: readers should be able to use it without opening sibling packet files.

## Status Note

- This is the standalone publication edition.
- The approved split packet remains the authorship source set behind this edition.
- The standalone edition is the primary publishing surface for one-file delivery.
- The repo-specific archive remains separate so the public guide does not drift back into workspace-local naming.

## Source Packet Components

The standalone edition is derived from these packet components:

| Source component | Role in this edition |
| --- | --- |
| `SYSTEM_OVERVIEW.md` | system model, authority model, recovery model |
| `ENFORCEMENT_MATRIX.md` | rule-to-mechanism matrix |
| `IMPLEMENTATION_MANUAL.md` | adoption sequence and rollout order |
| `TERMINOLOGY_CROSSWALK_APPENDIX.md` | concrete local reproduction appendix |
| `GENERIC_TERM_MAP.md` | narrative genericization and naming rules |
| `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md` | evidence, scope, and publication discipline |

## Table Of Contents

1. [How To Use This Document](#how-to-use-this-document)
2. [Reader Modes](#reader-modes)
3. [Executive Summary](#executive-summary)
4. [Translate This To Your Repo](#translate-this-to-your-repo)
5. [Source Packet Lineage](#source-packet-lineage)
6. [System Model](#system-model)
7. [Authority, Publication, And Recovery](#authority-publication-and-recovery)
8. [Enforcement Matrix](#enforcement-matrix)
9. [Minimal Viable Implementation](#minimal-viable-implementation)
10. [Adoption Manual](#adoption-manual)
11. [Generic Term Map](#generic-term-map)
12. [Terminology Crosswalk](#terminology-crosswalk)
13. [Concrete Implementation Appendix](#concrete-implementation-appendix)
14. [Evidence And Citation Contract](#evidence-and-citation-contract)
15. [Docsify And GitHub Pages Notes](#docsify-and-github-pages-notes)
16. [Reading Paths](#reading-paths)

## How To Use This Document

If you want the shortest useful read:

1. Read [Executive Summary](#executive-summary).
2. Read [Minimal Viable Implementation](#minimal-viable-implementation).
3. Read [Adoption Manual](#adoption-manual).

If you need to implement the model:

1. Read [Translate This To Your Repo](#translate-this-to-your-repo).
2. Read [Minimal Viable Implementation](#minimal-viable-implementation).
3. Read [Adoption Manual](#adoption-manual).
4. Read [Concrete Implementation Appendix](#concrete-implementation-appendix) only if you want the reference implementation details.

If you need to audit the model:

1. Read [Source Packet Lineage](#source-packet-lineage).
2. Read [System Model](#system-model).
3. Read [Authority, Publication, And Recovery](#authority-publication-and-recovery).
4. Read [Enforcement Matrix](#enforcement-matrix).
5. Read [Evidence And Citation Contract](#evidence-and-citation-contract).

## Reader Modes

This guide is designed to support three reading modes:

- Concept mode: read the executive summary, system model, and minimum implementation baseline.
- Adoption mode: read the translation layer, adoption manual, and concrete appendix.
- Audit mode: read the lineage, matrix, evidence contract, and appendix together.

The main narrative stays generic-first. Repo-local names are preserved later in the guide for reproduction and evidence.

## Executive Summary

Drift control is not one tool or one CI workflow. It is a layered model with four jobs kept separate:

- semantic authority
- readable publication
- executable enforcement
- explicit recovery

The model works because those jobs do not collapse into one another.

- a policy authority layer owns semantic meaning
- published contract views make that meaning readable
- an implementation layer enforces the rules through gates, workflows, and hooks
- tooling and retrieval layers provide operational support without becoming semantic authority
- packet protocols, step lists, and checkpoint rules stop multi-step work from drifting through conversation or memory alone

Source packet lineage for this section:

- `SYSTEM_OVERVIEW.md`
- `ENFORCEMENT_MATRIX.md`
- `IMPLEMENTATION_MANUAL.md`

## Translate This To Your Repo

Map the model by role, not by file or repo name.

| Role in this guide | What to find in your repo |
| --- | --- |
| policy authority layer | the single owned place where rule meaning lives |
| implementation layer | the codebase that runs gates, workflows, hooks, and runtime behavior |
| tooling layer | generators, helpers, or docs tooling that support the model without owning meaning |
| retrieval layer | local search, index, or lookup tools that help operators find the right authority surface |
| direct authority files | the small set of documents that are intentionally authoritative without being generated projections |
| archive lane | the place where superseded evidence moves so it does not keep acting like live guidance |

If your repo does not currently separate these roles, treat that as a design task. The model transfers by preserving the role boundaries, not by copying the reference implementation's names.

## Source Packet Lineage

This standalone edition is not a new theory document. It is a flattened publication of the approved packet.

| Standalone section | Primary packet source |
| --- | --- |
| Executive Summary | `SYSTEM_OVERVIEW.md`, `IMPLEMENTATION_MANUAL.md` |
| Translate This To Your Repo | `GENERIC_TERM_MAP.md`, `IMPLEMENTATION_MANUAL.md` |
| System Model | `SYSTEM_OVERVIEW.md` |
| Authority, Publication, And Recovery | `SYSTEM_OVERVIEW.md`, `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md` |
| Enforcement Matrix | `ENFORCEMENT_MATRIX.md` |
| Minimal Viable Implementation | `DRIFT_CONTROL_PACKET.md` authorship extension based on the approved packet set |
| Adoption Manual | `IMPLEMENTATION_MANUAL.md` |
| Generic Term Map | `GENERIC_TERM_MAP.md` |
| Terminology Crosswalk | `GENERIC_TERM_MAP.md`, `TERMINOLOGY_CROSSWALK_APPENDIX.md` |
| Concrete Implementation Appendix | `TERMINOLOGY_CROSSWALK_APPENDIX.md` |
| Evidence And Citation Contract | `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md` |

Use this lineage table as the cross-document citation layer for one-file publication.

## System Model

An effective drift-control system restricts drift by separating meaning, publication, enforcement, and recovery instead of letting one layer carry all four responsibilities.

### Four-Root Split

- policy authority repository
- product implementation repository
- shared tooling repository
- local retrieval surface

That split is an anti-drift control by itself. It makes it difficult for a convenience layer to silently become a second source of truth.

### Why Authority Is Centralized

- Canon bundles define generated policy contracts.
- Direct authority files such as a decision ledger and release policy may remain authoritative where the implementation intentionally treats them that way.
- Generated markdown contracts are readable projections, not independent sources of meaning.
- Router files remain thin so they do not become shadow policy stores.

### Why Recovery Is Explicit

- Multi-step work uses step lists plus injected state.
- Checkpoint rules require durable summaries.
- Archive separation keeps historical evidence visible without leaving it active by default.
- Index rebuild tooling restores local retrieval surfaces after checkout or selected commits.

Reference-implementation examples live later in this document, in the terminology crosswalk and concrete appendix.

Source packet lineage for this section:

- `SYSTEM_OVERVIEW.md`
- `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md`
- `GENERIC_TERM_MAP.md`

## Authority, Publication, And Recovery

### Authority

The strongest drift control is one authority root for rule meaning.

- semantic authority lives in policy-owned canon and direct authority files
- implementation consumes those rules but does not redefine them
- tooling and retrieval surfaces are operational only

### Publication

Readable publication is allowed, but it must stay traceable.

- generated contracts must point back to their owning canon source
- freshness matters because stale generated guidance is drift
- generated markdown is a readable projection, not sole authority

### Recovery

The system treats recovery as a first-class control.

- checkpoints and compaction preserve durable resume state
- step-list state records what ran and what is eligible next
- archive separation prevents historical evidence from silently remaining live

Source packet lineage for this section:

- `SYSTEM_OVERVIEW.md`
- `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md`
- `drift-control-packet-1.1.1-inventory-authority-enforcement-and-recovery-surfaces-report.md`

## Enforcement Matrix

This matrix keeps authority source and enforcement mechanism separate.

| Drift-control rule or concern | Authority source | Enforcing mechanism | Layer type | Control class | Failure or recovery note |
| --- | --- | --- | --- | --- | --- |
| semantic authority stays centralized | governance canon plus direct authority files where applicable | ownership boundaries, thin routing surfaces, authority-only rules | policy authority | preventive | stops implementation, tooling, and retrieval surfaces from becoming shadow canon |
| generated outputs remain subordinate | governance canon | generation, provenance metadata, freshness checks | policy authority plus tooling enforcement | preventive, detective | stale or hand-edited generated outputs count as drift |
| active docs stay pure and archive evidence stays separate | governance canon plus authority-integrity checks | authority-integrity gate path | runtime enforcement | preventive, detective | authority validation fails before downstream quality gates continue |
| policy source is pinned before enforcement proceeds | automation-gates authority plus release policy | policy-source preparation, policy-freeze gate, aggregate quality workflow | runtime enforcement | preventive, detective | blocks incompatible branch, commit, or version drift |
| scope stays within the owned slice | automation-gates authority, process contract, packet protocols | scope-enforcement gate, stage-owned path lists, protocol write-scope rules | runtime enforcement plus process control | preventive, detective | stops out-of-scope files from entering the change batch |
| decision references remain attached to implementation work | decision ledger plus automation-gates authority | decision metadata and release approval gates | policy authority plus runtime enforcement | preventive, detective | gated work must cite approved decisions |
| CI floor remains consistent | CI enforcement canon | blocking workflow chain | policy authority plus runtime enforcement | preventive, detective | CI floor remains policy-owned even though it runs from the product repo |
| deterministic execution is required | CI enforcement canon | `ci-determinism-gate` | runtime enforcement | detective | fails on introduced tracked-file or lockfile drift |
| coverage floors remain bound to canon | CI enforcement canon plus coverage implementation | `coverage-floor-gate`, `coverage-floor-scope` | policy authority plus runtime enforcement | detective | missing critical files count as zero-covered |
| structural and styling drift is blocked | CI enforcement canon plus automation-gates authority | structural, token, and style gates | runtime enforcement | preventive, detective | hard caps fail; exemptions must be explicit |
| local commits face early guardrails | automation-hooks authority | pre-commit, commit-msg, post-commit, post-checkout hooks | runtime enforcement | preventive, detective, corrective | catches drift early and refreshes local retrieval assets |
| stage order and scope alignment cannot be improvised | implementation process contract | stage model, PR metadata rules, stage-advance helper | process control | preventive, detective | prevents stage skipping and scope drift |
| multi-step packet work stays sequenced | protocol authority bundle | full-work packet, bounded task packet, packet-local seam audit, sequential workstream plan, and injected state | process control | preventive, detective, recovery-oriented | prevents conversational re-planning from replacing approved sequence |
| pause and resume stay explicit | protocol authority bundle | checkpoint and resume contract, checkpoint summaries, step-list state | recovery mechanism | recovery-oriented, detective | resume reads durable state instead of memory |
| retrieval starts from indexed authority lookup | retrieval canon plus governance authority split | indexed query flow and path-aware lookup | operator ergonomics plus process control | preventive, detective | reduces lookup drift before raw scans |
| local retrieval assets stay refreshable | indexing-automation canon | local index rebuild entrypoint, hook-triggered rebuilds, manual reindex | recovery mechanism plus tooling enforcement | corrective, recovery-oriented | rebuilds local retrieval assets after selected changes |

Source packet lineage for this section:

- `ENFORCEMENT_MATRIX.md`
- `SYSTEM_OVERVIEW.md`
- `TERMINOLOGY_CROSSWALK_APPENDIX.md`

## Minimal Viable Implementation

This section defines the baseline minimum for drift control: the smallest set of controls that still meaningfully restricts drift in any repo.

If you remove any of the items below, you may still have automation, but you no longer have a stable drift-control model.

### Absolute Minimum

1. One semantic authority root
   The system needs one owned place for rule meaning. Without this, every later check enforces an ambiguous standard.

2. Readable publication that stays subordinate to authority
   Humans still need published docs, but they must be generated or otherwise traceable back to the authority source. If readable docs become hand-maintained peers, drift starts there.

3. A pinned policy baseline before enforcement runs
   The implementation surface must consume a known branch, commit, and compatible version of the policy layer. Otherwise the rules being enforced can float during execution.

4. Blocking enforcement for scope, drift, schema, tests, and determinism
   The minimum enforcement chain must stop out-of-scope edits, schema drift, policy drift, failing tests, and introduced tracked-file or lockfile drift.

5. Explicit checkpoint and resume discipline for multi-step work
   If work spans multiple steps, sessions, or agents, durable state is mandatory. Otherwise the process itself drifts even if the code does not.

6. Archive or supersession separation
   Historical evidence must stop acting like live authority after replacement. If old and current guidance remain in the same active lane, drift becomes a documentation problem immediately.

### Minimum But Context-Dependent

- decision references become minimum once architectural or process choices need durable justification across multiple workers
- indexed retrieval becomes minimum once the authority surface is large enough that operators cannot reliably find the right source without guidance
- local hooks are not strictly the minimum if CI already blocks the same drift, but they are the fastest way to catch it earlier

### What The Full Model Adds Beyond Minimum

- staged implementation order
- richer decision canonification practices
- local hook ergonomics
- indexed retrieval and automated rebuilds
- packet-local audit seams between bounded tasks
- separate archive and publication surfaces for accessibility and provenance

Source packet lineage for this section:

- approved packet set closeout in `DRIFT_CONTROL_PACKET.md`
- `IMPLEMENTATION_MANUAL.md`
- `ENFORCEMENT_MATRIX.md`

## Adoption Manual

Adopt the model in this order.

### 1. Establish One Authority Root

- keep rule meaning in one owned policy surface
- publish readable contracts from that source
- keep direct authority files limited and explicit
- keep routing surfaces thin

### 2. Make Publication Traceable

- require provenance and freshness back to authority
- regenerate readable outputs rather than hand-editing them
- move historical evidence into an archive lane

### 3. Pin The Policy Surface

- pin branch, commit, and compatible version
- fail or warn explicitly on incompatible drift
- tie version expectations to release policy

### 4. Install The Protocol Suite

- use full implementation packets for high-rigor or multi-step work
- use narrow task packets only for bounded slices
- require seam audit between steps
- require step-list state and checkpoint rules for resume

### 5. Install Local And CI Enforcement

- local hooks catch early drift
- CI runs the blocking gate floor
- scope and stage controls sit beside code-quality checks
- decision and release metadata stay part of enforcement

### 6. Keep Retrieval Local-First

- provide indexed retrieval before raw scanning
- support path-aware authority lookup
- keep index rebuild automation available

### 7. Treat Decisions As First-Class Inputs

- harvest decisions before implementation momentum hides them
- publish them through the shared authority layer
- require implementation work to reference approved decision IDs

### 8. Require Changelog-Backed Compaction

- require changelog entries before checkpoint or compaction
- preserve repo state, decision state, implementation state, and next move
- keep compaction immutable once recorded

### 9. Roll Out In This Order

1. authority root
2. generated publication and provenance
3. policy pinning
4. protocol suite and step-list discipline
5. local hooks and CI gates
6. indexed retrieval and rebuild automation
7. decision canonification workflow
8. changelog-backed checkpoint and compaction workflow

### 10. What To Keep Generic Versus Concrete

- keep the main manual generic when describing the model
- put local file paths, command names, protocol names, and script entrypoints in the appendix
- use exact local names only when a reader needs concrete reproduction evidence

Source packet lineage for this section:

- `IMPLEMENTATION_MANUAL.md`
- `SYSTEM_OVERVIEW.md`
- `ENFORCEMENT_MATRIX.md`

## Generic Term Map

Use these narrative rules when adapting the model for another repo:

- lead with the generic term in prose
- use the local name only when the concrete artifact matters for evidence, commands, or reproduction
- keep repo paths, script names, protocol names, and decision IDs in tables or appendices rather than the main narrative unless the exact identifier is the point
- treat generated markdown as a readable projection rather than the sole authority source

### Repo-Root Roles

| Generic term | Local term | Use the local name when | Notes |
| --- | --- | --- | --- |
| policy authority repo | `runbook-policy` | citing the owning path, bundle, or locked contract | this is the semantic authority root in the reference implementation |
| product implementation repo | `runbook-app` | showing enforcement scripts, workflows, or hook entrypoints | this is where implementation and enforcement mechanics live |
| shared tooling repo | `runbook-tooling` | citing generators, prompts, or workstream artifacts | treat as tooling infrastructure, not semantic authority |
| local retrieval surface | `.code-index` | showing exact query commands, rebuild scripts, or local artifacts | treat as workspace-local tooling, not canon |

### Authority And Publication Terms

| Generic term | Local term | Use the local name when | Notes |
| --- | --- | --- | --- |
| canonical rules bundle | `runbook-policy/canon/**` bundle JSON | showing the owning authority surface for a rule | cite the exact bundle path in evidence |
| published contract view | generated markdown contract such as `WORKSPACE_GOVERNANCE.md` | the readable contract path is itself the evidence being opened | the markdown contract is subordinate to canon |
| routing surface | `AGENTS.md` | showing the exact router file or thin-surface behavior | router files are summaries, not deep authority payloads |
| archive evidence | `runbook-policy/archive/**` or archive-manifest metadata | discussing historical lineage or supersession | archive evidence is not default active meaning |
| step-list state | `STEP_LIST.md` plus `STEP_LIST_STATE.json` | describing current workstream sequencing or resume state | this is workstream authority, not workspace semantic authority |

### Protocol Terms

| Generic term | Local term | Use the local name when | Notes |
| --- | --- | --- | --- |
| full implementation packet | `tempgo` | naming the protocol or pointing to the locked protocol contract | use for high-rigor, multi-step execution |
| narrow task packet | `tempgo-lite` | naming the protocol seam or exact task mode | use only for bounded low-ambiguity slices |
| packet-local seam audit | `tempgo-audit` | citing the audit protocol or a specific audit report | distinct from whole-repo audit |
| sequential workstream plan | `tempgo-step-list` | citing the protocol family or actual step-list files | use when explaining deterministic continuation |
| checkpoint and resume contract | `compaction-contract` | citing the protocol contract by file name | use generic language such as checkpoint summary in prose |

Source packet lineage for this section:

- `GENERIC_TERM_MAP.md`

## Terminology Crosswalk

Use these generic terms in the main narrative.

| Generic term | Local term | When to use the local name |
| --- | --- | --- |
| policy authority repo | `runbook-policy` | when citing exact owning paths, bundles, or locked contracts |
| product implementation repo | `runbook-app` | when citing enforcement scripts, workflows, or hook entrypoints |
| shared tooling repo | `runbook-tooling` | when citing generators, prompts, or workstream artifacts |
| local retrieval surface | `.code-index` | when citing exact query commands or rebuild scripts |
| full implementation packet | `tempgo` | when naming the protocol or exact task mode |
| narrow task packet | `tempgo-lite` | when naming the protocol seam or exact bounded task mode |
| packet-local seam audit | `tempgo-audit` | when naming the audit protocol or audit report |
| checkpoint and resume contract | `compaction-contract` | when citing the exact protocol contract |
| decision ledger | `runbook-policy/decisions/DECISION_LOG.md` | when citing exact decision IDs |
| release policy | `runbook-policy/release/RELEASE_POLICY.md` | when citing branch model, merge rules, or versioning |

Translation rules:

1. Lead with the generic term.
2. Use the local name when exact evidence, commands, file paths, or IDs matter.
3. Keep the main prose generic-first.
4. Concentrate local commands and file paths in the appendix.

Source packet lineage for this section:

- `GENERIC_TERM_MAP.md`
- `TERMINOLOGY_CROSSWALK_APPENDIX.md`

## Concrete Implementation Appendix

This section is the dense reproduction layer for the reference implementation.

### Authority And Publication Paths

- canon bundles: `runbook-policy/canon/**/canon-bundle.json`
- readable governance contract: `runbook-policy/WORKSPACE_GOVERNANCE.md`
- readable CI contract: `runbook-policy/ci/CI_ENFORCEMENT_POLICY.md`
- readable retrieval contract: `runbook-policy/code-index/INDEX_FIRST_RETRIEVAL.md`
- readable indexing automation contract: `runbook-policy/code-index/INDEXING_AUTOMATION.md`
- decision ledger: `runbook-policy/decisions/DECISION_LOG.md`
- release policy: `runbook-policy/release/RELEASE_POLICY.md`

### Protocol Paths

- `runbook-policy/studio/protocols/tempgo-protocol.md`
- `runbook-policy/studio/protocols/tempgo-lite-protocol.md`
- `runbook-policy/studio/protocols/tempgo-audit-protocol.md`
- `runbook-policy/studio/protocols/tempgo-step-list-protocol.md`
- `runbook-policy/studio/protocols/compaction-contract.md`

### Canon Commands

```bash
node runbook-tooling/scripts/canon.mjs validate runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs generate runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-coverage runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-generated runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-active-doc-purity runbook-policy/canon/protocols
node runbook-tooling/scripts/canon.mjs check-archive-separation runbook-policy/canon/protocols
node runbook-tooling/scripts/rehydrate-canon.mjs
```

### Hook And Gate Commands

- hook install: `pnpm run install-git-hooks` from `runbook-app/`
- stage advance: `pnpm run stage-advance-check`
- policy freeze: `pnpm run policy-pin-freeze`
- scope gate: `pnpm run scope-gate`
- commit message gate: `pnpm run commit-msg-gate`
- schema validation: `pnpm run schema-validate`
- policy drift lint: `pnpm run policy-lint`
- structural gate: `pnpm run lint`
- type gate: `pnpm run typecheck`
- unit tests: `pnpm run unit-test`
- integration tests: `pnpm run integration-test`
- coverage floor: `pnpm run coverage-floor-gate`
- aggregate CI chain: `pnpm run quality-gates`

### Retrieval Commands

- `./.code-index/query-context.sh "<topic>"`
- `./.code-index/query-search.sh "<topic>"`
- `./.code-index/query-docs.sh "<topic>"`
- `./.code-index/query-canon.sh --path "<workspace-path>"`
- `./.code-index/query-symbol.sh "<symbol>"`
- `./.code-index/query-impact.sh "<symbol>"`
- `./.code-index/build-index.sh`

### Reference-Implementation Source Files

- `SYSTEM_OVERVIEW.md`
- `ENFORCEMENT_MATRIX.md`
- `IMPLEMENTATION_MANUAL.md`
- `TERMINOLOGY_CROSSWALK_APPENDIX.md`
- `GENERIC_TERM_MAP.md`
- `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md`
- `archive/repo-specific-pre-genericization-2026-03-13/`

Source packet lineage for this section:

- `TERMINOLOGY_CROSSWALK_APPENDIX.md`
- `GENERIC_TERM_MAP.md`

## Evidence And Citation Contract

This publication edition still follows the original packet evidence rules.

### Scope Boundaries

- the packet describes current workspace behavior only
- the packet is documentation authorship, not an implementation-change packet
- decision canonification and changelog-backed compaction are included only because the dev path explicitly treats them as implemented practices
- the packet does not invent future-state controls or imply undocumented behavior

### Citation Rules

- generated markdown may be cited as a readable contract view, but not as the only authority source when a canon bundle or direct authority file exists
- canon bundles remain the authority source for generated contracts
- direct authority files such as the decision ledger and release policy may be cited directly where they are intentionally authoritative
- workstream artifacts and packet reports are operational evidence, not workspace semantic authority

### Evidence Shape

| Claim type | Minimum evidence shape |
| --- | --- |
| authority claim | canon bundle plus readable contract or direct authority surface |
| enforcement claim | policy authority plus concrete gate, workflow, hook, or script surface |
| recovery claim | governance or protocol authority plus current operational state surface |
| current implementation example | exact file path, script name, or command |
| release or pinning rule | release or automation authority plus concrete gate behavior |

### Publication Rule

- this standalone edition is allowed to be the publish surface
- it remains subordinate to the approved packet source set
- if the standalone edition and the source packet diverge, the source packet must be treated as the authorship source that needs reconciliation

Source packet lineage for this section:

- `PACKET_ARCHITECTURE_AND_EVIDENCE_CONTRACT.md`

## Docsify And GitHub Pages Notes

This guide is prepared for one-file publishing through Docsify and GitHub Pages.

Publication bundle contents:

- `docsify-site/README.md`
- `docsify-site/index.html`
- `docsify-site/_sidebar.md`
- `docsify-site/.nojekyll`

Publishing rule:

- publish the bundle directory through a GitHub Pages Actions workflow, or copy its contents to a repo-root `docs/` directory if you prefer branch-source Pages
- treat `README.md` in that bundle as the rendered homepage
- keep this standalone guide as the content source for the bundle
- keep the split packet and archive outside the published bundle unless you intentionally want to expose reference material

## Reading Paths

For executives or maintainers:

1. [Executive Summary](#executive-summary)
2. [Minimal Viable Implementation](#minimal-viable-implementation)
3. [Adoption Manual](#adoption-manual)

For implementers:

1. [Translate This To Your Repo](#translate-this-to-your-repo)
2. [Minimal Viable Implementation](#minimal-viable-implementation)
3. [Adoption Manual](#adoption-manual)
4. [Concrete Implementation Appendix](#concrete-implementation-appendix)

For auditors:

1. [Source Packet Lineage](#source-packet-lineage)
2. [System Model](#system-model)
3. [Authority, Publication, And Recovery](#authority-publication-and-recovery)
4. [Enforcement Matrix](#enforcement-matrix)
5. [Evidence And Citation Contract](#evidence-and-citation-contract)
6. [Concrete Implementation Appendix](#concrete-implementation-appendix)
