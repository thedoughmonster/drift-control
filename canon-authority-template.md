# Central Semantic Authority Template

## Overview

Central semantic authority is the part of a drift-control system that owns rule meaning. It answers the conflict question directly: when a generated page, a local note, a query result, and an enforcement check disagree, which surface wins?

> **At a glance**
> Use one owned authority lane for live meaning, generate readable outputs from it, keep routing surfaces thin, and keep archive or evidence material out of the active rule path.

| Use this page when you need to... | What this page gives you |
| --- | --- |
| stop shadow policy from forming | an authority-lane model with clear role boundaries |
| keep docs readable without splitting meaning | a generation model for contracts, references, and routers |
| explain provenance and freshness | metadata patterns and publication examples |
| build a portable system | generic guidance first, with one clearly labeled example lane |

### Fast model

| Lane | Purpose | Can define live rules? |
| --- | --- | --- |
| Source authority | Own semantic meaning, scope, provenance, and publication rules | Yes |
| Generated contract | Publish a readable normative projection | No |
| Generated reference | Reorganize and explain authority for lookup | No |
| Router surface | Keep local guidance thin and directional | No |
| Query layer | Resolve path ownership, read-next, freshness, and provenance | No |
| Archive or evidence | Preserve superseded or historical material | No |

---

## Why Central Authority Matters

Drift control fails when the repository has multiple places that _feel_ authoritative. The failure is usually not missing documentation. It is competing meaning across policy docs, generated outputs, repo-local notes, CI gates, and operator memory.

> **Core rule**
> A surface may explain authority, render authority, or help retrieve authority. That does not make it authority.

| Failure mode | What it looks like | Why it is dangerous |
| --- | --- | --- |
| Shadow authority | teams start editing a generated page or root README as if it were the rule source | the next regeneration silently overwrites meaning or exposes hidden divergence |
| Split authority | multiple folders or repos hold overlapping "canon" | conflicts are resolved socially instead of deterministically |
| Publication drift | published docs lag behind the semantic source | readers implement against stale guidance |
| Retrieval drift | index or query tooling starts acting like a policy owner | lookup behavior freezes or invents meaning |
| Evidence contamination | audits, migration notes, or checkpoints remain in the active rule lane | historical context overrides current policy by accident |

### Questions a healthy model can answer fast

| Question | Healthy answer shape |
| --- | --- |
| Where is live meaning authored? | one owned authority root |
| What wins on conflict? | the authority root, explicitly |
| How do readers consume the rules? | generated contracts or references with provenance |
| How do contributors navigate quickly? | thin routers and query surfaces |
| Where does old guidance go? | archive or evidence lane, not the live path |

> **Operational test**
> If contributors cannot answer "where do I change the rule?" and "what wins on conflict?" in one sentence each, the model is still too loose.

---

## Authority Surfaces

Treat the system as a set of lanes with explicit permissions rather than as "a bunch of docs."

| Surface class | Primary responsibility | Allowed content | Not allowed |
| --- | --- | --- | --- |
| `authority` | own semantic meaning, scope boundaries, provenance, and publication behavior | canon bundles, source-authority records, owned rule JSON, explicitly authoritative records | local summaries that bypass the authority update path |
| `publication/contract` | publish the primary readable projection of authority | generated contracts with provenance and freshness metadata | independent rule authoring |
| `publication/reference` | improve discovery, explanation, and operator lookup | scope maps, catalogs, glossaries, supporting references | new requirements not present in authority |
| `publication/router` | keep local guidance short and path-aware | boundary reminders, read-next links, owning bundle IDs | long-form restatements that become shadow canon |
| `query` | resolve likely authority quickly | path lookup, read-next routing, freshness and provenance display | rule invention or silent precedence changes |
| `evidence/archive` | preserve history, audits, migration artifacts, and lineage | archive indexes, checkpoints, supersession records | default live authority for active behavior |

### Minimal authority contract

1. One owning semantic root per governed domain.
2. One known write path for changing live meaning.
3. Generated outputs that preserve provenance back to that root.
4. Freshness signals so stale outputs are detectable.
5. Thin routing surfaces so navigation stays fast without spawning shadow policy.
6. A separate archive lane so historical material does not stay active by accident.

### Direct authority versus derived authority

| Pattern | Use it when | Notes |
| --- | --- | --- |
| Direct authority record | the system intentionally treats a decision log, exception record, or release rule as authoritative | make that status explicit; do not leave it implicit |
| Derived contract | the repo needs a readable policy view | the contract is normative to readers but still subordinate to source authority |
| Derived reference | the repo needs lookup help, maps, catalogs, or reorganized views | references improve access without changing meaning |

---

## Generation Model

The recommended build model is authority-first, publication-second.

```text
authoritative sources -> canonical bundle or model -> generated contracts/references/routers -> query and index surfaces -> humans and automation
```

### Separation of concerns

- Source authority is where rule meaning is authored.
- Generated outputs are where rule meaning is rendered.
- Query surfaces are where rule meaning is discovered.
- Evidence surfaces are where past rule states and rollout history are preserved.

That split makes regeneration safe, keeps provenance machine-readable, and prevents convenience surfaces from turning into hidden policy stores.

| Stage | Input | Output | Drift-control expectation |
| --- | --- | --- | --- |
| Author | bundle JSON, source-authority records, explicit authority docs | updated canonical model | all semantic changes happen here |
| Validate | schema, ownership, provenance, and consistency checks | pass/fail signal | malformed rules and broken provenance block publication |
| Generate | canonical model | contracts, references, routers, catalogs | outputs are deterministic and reproducible |
| Publish | generated files at stable paths | reader-facing docs | stable public paths remain useful without becoming manual authority |
| Query | path lookup, read-next, freshness metadata | retrieval answers | query layer routes to authority; it does not replace it |
| Archive | superseded outputs and rollout evidence | archived lineage | historical material stays discoverable but not active by default |

> **Design note**
> Stable public paths are valuable. Stable public paths as hand-maintained semantic authority are not.

### Generic file topology

```text
policy/
  canon/
    workspace-governance/
      canon-bundle.json
      source-authority.md
      source-manifest.json
      build-manifest.json
  WORKSPACE_GOVERNANCE.md          # generated contract
  README.md                        # generated reference
  POLICY_SCOPE_MAP.md              # generated reference
  AGENTS.md                        # generated router
catalog/
  PUBLICATION_CATALOG.md           # generated reference
archive/
  publication-lineage/             # archive lane, not live authority
```

### Metadata every generated output should expose

| Field | Why it matters |
| --- | --- |
| `owner` | ties the output to one authority owner |
| `generated_from` | points back to the semantic source |
| `build_manifest` | identifies the generation context |
| `publication_doc_role` | distinguishes contract, reference, or router intent |
| `publication_output_family` | classifies the publication lane |
| `edit_policy` | blocks hand-edited drift |
| `freshness` or equivalent | shows whether the output is safe to trust |

---

## In This Repository

> **Example lane**
> The paths below are one implementation example from this workspace. They illustrate the model and naming pattern only.

This workspace uses `runbook-policy` as the semantic authority root for shared policy meaning. The live authority source is not the generated contract. It lives under `runbook-policy/canon/**`, with workspace-governance concepts centered on `runbook-policy/canon/policy/workspace-governance/source-authority.md`.

The generated contract at `runbook-policy/WORKSPACE_GOVERNANCE.md` makes the ownership split explicit:

- `runbook-policy` is the semantic authority for shared workspace rules.
- `runbook-app` owns implementation, not shared policy meaning.
- `runbook-tooling` owns tooling, not semantic authority.
- `.code-index` is a retrieval surface, not policy canon.
- generated `AGENTS.md`, README, scope-map, and contract pages are subordinate outputs with provenance.

The same pattern appears in generated subordinate views such as `runbook-policy/ci/CI_ENFORCEMENT_POLICY.md` and `runbook-app/docs/ui-implementation-stages.md`: both declare the canonical bundle path, expose generated metadata, and direct readers to regenerate rather than hand-edit.

| Generic role | Workspace example | Why it matters |
| --- | --- | --- |
| Source authority | `runbook-policy/canon/policy/workspace-governance/source-authority.md` and bundle JSON under `runbook-policy/canon/**` | live meaning is authored here |
| Generated contract | `runbook-policy/WORKSPACE_GOVERNANCE.md` | primary human-readable normative projection |
| Generated references | `runbook-policy/README.md`, `runbook-policy/POLICY_SCOPE_MAP.md` | navigation and explanation without redefining policy |
| Generated router | `runbook-policy/AGENTS.md` and repo-local `AGENTS.md` outputs | thin local routing and guardrails |
| Generated subordinate output | `runbook-app/docs/ui-implementation-stages.md` | policy-derived guidance projected into an implementation repo |
| Query surface | `.code-index` path and docs queries | retrieval layer, not semantic owner |
| Evidence lane | QA artifacts, migration trackers, packet outputs, archive records | historical support material kept out of live authority |

---

## Mermaid Diagram

```mermaid
flowchart TD
    A[Source Authority\nbundle JSON + source-authority records] --> B[Validation\nschema + provenance + freshness checks]
    B --> C[Generated Contract\nreadable normative projection]
    B --> D[Generated Reference\nmaps catalogs glossaries]
    B --> E[Generated Router\nthin local AGENTS or README surfaces]
    C --> F[Humans]
    D --> F
    E --> F
    C --> G[Automation]
    D --> H[Query and Index Layer\npath lookup read-next freshness]
    E --> H
    H --> F
    H --> G
    A --> I[Archive and Evidence Lane\nmigration notes audits checkpoints lineage]
    I -. discoverable but not active by default .-> F
```

---

## Key Snippets

> **Use these as shape references**
> Keep the model portable: preserve the role boundaries even if your paths, file names, or tooling differ.

### 1. Source-authority rule shape

```md
# Workspace Governance Source Authority

- policy/ is the only semantic authority surface for shared workspace rules.
- app/ owns implementation state, not shared semantic meaning.
- tooling/ owns automation infrastructure, not policy canon.
- query/index tooling may assist retrieval, but it does not win conflicts.
```

### 2. Generated contract metadata

```yaml
---
owner: policy.workspace-governance
generated_from: policy/canon/workspace-governance/canon-bundle.json
build_manifest: policy/canon/workspace-governance/build-manifest.json
publication_doc_role: generated_contract
publication_output_family: contract
edit_policy: generated_do_not_edit
---
```

### 3. Thin authority note for a generated page

```md
Authority note:
- this document is a generated subordinate view of `policy/canon/workspace-governance`
- the JSON bundle is canonical; regenerate this file instead of editing it by hand
- live repo status is not canonical here; execution state belongs in the execution system
```

### 4. Publication record shape

```json
{
  "owning_bundle": "policy.workspace-governance",
  "target_id": "workspace-governance-contract",
  "doc_role": "generated_contract",
  "publication_output_family": "contract",
  "stable_output_path": "policy/WORKSPACE_GOVERNANCE.md",
  "lookup_visible": true,
  "freshness": "fresh",
  "read_next": [
    "policy/README.md",
    "policy/POLICY_SCOPE_MAP.md"
  ]
}
```

> **What the snippets show**
> The machine-readable bundle owns the meaning. The generated page owns readability. The metadata keeps the link intact.

---

## Implementation Checklist

| Status | Action |
| --- | --- |
| `todo` | Choose one semantic authority root for each governed domain |
| `todo` | Define any intentionally authoritative supporting records, such as decisions or exceptions |
| `todo` | Move rule authoring into canonical machine-readable bundles or equally explicit source-owned records |
| `todo` | Generate reader-facing contracts, references, and routers from those sources |
| `todo` | Attach provenance fields such as `generated_from`, `owner`, `doc_role`, `publication_output_family`, and freshness metadata |
| `todo` | Mark generated outputs as `do not edit` and make regeneration the only legal update path |
| `todo` | Keep router surfaces thin so they route to authority instead of restating full policy |
| `todo` | Ensure search, indexing, or query tooling exposes provenance and freshness without becoming a semantic owner |
| `todo` | Separate evidence, migration notes, audits, checkpoints, and archive lineage from the live authority lane |
| `todo` | Add CI or local checks that fail on stale generated outputs, broken provenance, or hand-edited derived files |
| `todo` | Define conflict resolution explicitly: authority source wins over generated docs, local notes, and query output |
| `todo` | Document the update sequence: author -> validate -> regenerate -> review -> publish -> archive superseded material |

---

## Repo-Agnostic Build Prompt

```text
Build a central semantic-authority system for this repository that prevents drift between rule meaning, readable docs, query surfaces, and historical evidence.

Requirements:
1. Create one explicit semantic authority root for shared repository rules. If the repo already has multiple overlapping policy locations, consolidate the meaning into one owned authority lane and define conflict resolution so the authority lane always wins.
2. Distinguish these surface classes clearly:
   - source authority
   - intentionally authoritative supporting records, if any
   - generated contract outputs
   - generated reference outputs
   - thin router outputs
   - query or index surfaces
   - archive or evidence surfaces
3. Ensure generated docs never become live semantic authority. Generated contracts, references, and routers must preserve provenance back to the authority source and must be marked as regenerate-only.
4. Add freshness and provenance metadata to every generated publication, including at minimum:
   - owning bundle or authority ID
   - generated_from source path
   - build or generation manifest path
   - doc role
   - publication family
   - edit policy
   - visibility flags if the repo uses them
5. Implement a deterministic generation model:
   - author semantic changes in the authority lane
   - validate schema and provenance
   - regenerate readable outputs
   - fail if generated outputs are stale or manually edited
6. Keep router surfaces thin. They should identify local boundaries and route deeper reads into the owning contract or reference surfaces instead of duplicating long-form rules.
7. Keep query or indexing tools in a retrieval lane only. They may resolve path ownership, read-next surfaces, provenance, and freshness, but they must not invent rules or replace the authority source.
8. Create an archive or evidence lane for audits, migration notes, checkpoints, rollout artifacts, and superseded outputs so those materials remain discoverable without staying active by default.

Deliverables:
- a short architecture note explaining the authority model and conflict resolution
- the authority-root file or folder structure
- one example authority bundle or equivalent canonical source
- one generated contract page
- one generated reference page
- one thin router page
- one machine-readable publication or provenance record
- one validation or CI check that detects stale or manual edits to generated outputs
- one short README section explaining how to update authority correctly

Constraints:
- keep the model repo-agnostic and avoid assuming a specific CI provider, doc generator, or framework
- preserve any stable public doc paths if possible, but convert them into generated outputs instead of manual semantic authority
- do not leave shadow policy behind in local READMEs, agent files, or generated references
- prefer concise, explicit metadata and deterministic file ownership over broad prose

Execution guidance:
- inspect the current repo for competing policy or guidance surfaces
- identify which files are currently acting as shadow authority
- propose the target lane model before making structural changes
- implement the smallest complete vertical slice that proves the pattern
- show the final file tree, the generation flow, and the exact update path for future semantic changes
```
