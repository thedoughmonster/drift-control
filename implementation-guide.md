# Implementation Guide

This page explains how to put drift control into operation. It assumes you already understand the system model and the minimum viable baseline. The goal here is practical adoption: what to install first, what each layer is responsible for, and how to run the model without letting guidance, automation, and recovery drift apart.

Use this page in three ways:

- to plan an initial rollout
- to audit whether an existing implementation is complete
- to standardize day-to-day operating patterns after the controls are live

Related pages:

- [Core Model](core-model.md)
- [Minimum Viable Implementation](minimum-viable-implementation.md)
- [Enforcement Model](enforcement-model.md)

## Implementation Model

Drift control is strongest when the implementation is built as a sequence of distinct responsibilities instead of one large automation bundle. The model below is the full target state.

### 1. Semantic Authority

Start with one owned authority root for rule meaning.

- Keep the canonical machine-readable rules in one policy-owned surface.
- Allow direct authority documents only where the system intentionally treats them as authoritative, such as a decision record or release policy.
- Keep routing and summary files thin so they point to authority instead of becoming a second rule store.
- Make ownership explicit. Every authority surface should have a clear maintainer and a clear change path.

If this layer is ambiguous, later enforcement still runs, but it enforces an unclear standard.

### 2. Readable Publication

People need readable contracts, but readable contracts must remain subordinate to authority.

- Generate or otherwise derive reader-facing policy views from the authority source.
- Attach provenance so every published surface identifies the authority source it came from.
- Treat freshness as part of correctness. Stale publication is drift.
- Prevent hand-edited publication from silently becoming the real source of truth.

The purpose of publication is access, not reinterpretation.

### 3. Policy Baseline

The implementation environment should consume a pinned, compatible policy baseline before deeper automation runs.

- Pin the authority branch, revision, and compatible version range before enforcement begins.
- Fail or warn clearly when the implementation is using an incompatible policy baseline.
- Make policy compatibility part of release discipline rather than an informal convention.
- Avoid floating policy reads inside critical gates.

This turns policy from a moving target into a stable input.

### 4. Execution Protocol

Code checks are not enough. Multi-step work needs an execution contract.

- Define when work requires a full work plan versus a smaller bounded task record.
- Keep ordered step state for multi-step work so sequence is recorded, not assumed.
- Require seam checks between steps when work passes through multiple sessions or contributors.
- Define pause, resume, and handoff rules before you need them.

Without an execution protocol, process drift appears before code drift is visible.

### 5. Layered Enforcement

Enforcement should be distributed across layers that catch different failure modes.

- Local hooks provide fast guardrails for common mistakes.
- Commit and review metadata keep decisions and scope attached to changes.
- CI provides the blocking floor for schema, policy drift, determinism, tests, coverage, and structural constraints.
- Stage or scope controls prevent a valid code change from modifying the wrong surface.
- Release approval checks confirm that policy versioning and decision requirements were satisfied before promotion.

The system should not depend on any single gate to do all the work.

### 6. Retrieval And Indexing

Teams drift faster when they cannot find the right authority surface quickly.

- Provide local-first retrieval that resolves the likely authority source before broad scanning.
- Support path-aware lookup so a contributor can start from a file or surface and discover the governing rules.
- Keep index rebuild or refresh actions available after checkout, selected commits, and manual repair.
- Treat retrieval as an operational aid, not as semantic authority.

Fast, deterministic lookup reduces the odds that a contributor implements against a stale or secondary source.

### 7. Decisions As Inputs

Architectural and implementation decisions should enter the control model early instead of being reconstructed after the change lands.

- Capture decisions before implementation momentum hardens them into undocumented defaults.
- Store decisions in a durable authority surface.
- Require implementation work to cite the decisions it depends on.
- Review whether a decision belongs in long-lived policy, in a temporary exception path, or in a project-local note with an expiry condition.

Decision handling is part of drift control because undocumented decisions become hidden policy.

### 8. Checkpoints, Recovery, And Archives

Recovery should be designed into the model.

- Require structured checkpoints for work that may pause, span sessions, or transfer between operators.
- Record implementation state, enforcement state, outstanding risks, and the exact next action.
- Keep checkpoint records additive rather than rewriting prior history.
- Separate active guidance from superseded evidence and historical records.

The goal is durable recovery: resume from recorded state, not from memory.

## Adoption Sequence

Install the model in order. Each later layer assumes the earlier one is already stable.

### Phase 1: Establish The Authority Root

Objective: create one unambiguous source of semantic meaning.

Do this:

- choose the canonical policy surface
- identify any direct authority documents that are intentionally authoritative
- remove or thin duplicate guidance that currently behaves like shadow authority
- define ownership and change rules for authority surfaces

Exit criteria:

- contributors can answer where rule meaning lives without hesitation
- reader-facing summaries no longer conflict with authority
- no critical rule depends on tribal memory

### Phase 2: Build Publication With Provenance

Objective: make the authority readable without creating a second source of truth.

Do this:

- publish readable contract views from the authority source
- attach source references and freshness expectations
- mark generated or derived material clearly
- move historical or superseded material into an archive lane

Exit criteria:

- a reader can move from any published contract back to its authority source
- stale publication is detectable
- archived evidence is separated from current guidance

### Phase 3: Pin The Policy Baseline

Objective: ensure automation runs against a known policy state.

Do this:

- require policy revision and compatibility checks before full enforcement
- make incompatibility a visible failure, not a silent fallback
- define how policy updates are introduced, reviewed, and promoted

Exit criteria:

- enforcement never runs against an unknown policy baseline
- contributors can see which policy state governed a change
- policy upgrades follow a deliberate path

### Phase 4: Install The Execution Protocol

Objective: prevent multi-step implementation work from drifting through informal coordination.

Do this:

- define which work sizes require formal work plans or equivalent execution records
- require ordered step state for sequential work
- require seam checks at step boundaries
- define how pauses, resumes, and handoffs are recorded

Exit criteria:

- multi-step work can pause and resume without reconstructing intent from chat history
- step order is visible and enforceable
- handoffs preserve the exact next safe action

### Phase 5: Add Layered Enforcement

Objective: catch drift early locally and block it authoritatively in CI and release flow.

Do this:

- install local hooks for the smallest high-value checks
- enforce scope ownership and change-surface limits
- block policy drift, schema drift, determinism failures, and test failures in CI
- require decision metadata and approval metadata where applicable
- keep release checks aligned with policy compatibility and exception handling

Exit criteria:

- common mistakes fail before review when possible
- blocking gates represent the minimum non-negotiable floor
- stage or scope violations fail even when code quality checks pass

### Phase 6: Make Retrieval Local-First

Objective: reduce lookup drift and make authority discovery repeatable.

Do this:

- provide indexed lookup for authority and enforcement surfaces
- support path-to-rule resolution
- document when the index refreshes automatically and how to rebuild it manually
- keep raw full-text scanning as a fallback, not the main path

Exit criteria:

- contributors can resolve the governing rule for a path quickly
- retrieval repair is operationally simple
- local lookup stays useful after normal repository movement

### Phase 7: Operationalize Decisions

Objective: ensure decisions become governed inputs instead of hidden implementation folklore.

Do this:

- run a short decision review before complex work begins
- record decisions in the owned authority surface
- require changes to cite the relevant decisions
- review temporary exceptions for expiry, renewal, or formal adoption into policy

Exit criteria:

- major implementation choices are discoverable
- decision references travel with the change
- exceptions do not become permanent through neglect

### Phase 8: Standardize Checkpoints And Archives

Objective: make recovery and supersession routine.

Do this:

- require checkpoint records before compaction, pause, or handoff
- define a standard checkpoint structure
- make checkpoint records append-only
- define how active, superseded, and archived materials are separated

Exit criteria:

- paused work resumes from durable state instead of recollection
- historical evidence stays available without acting live
- compaction improves clarity without erasing accountability

## Operational Patterns

The adoption sequence gets the model installed. The patterns below keep it working.

### Decision Pattern

Use a lightweight but explicit decision cycle:

1. Gather the decisions that materially affect scope, architecture, styling, operations, or release behavior.
2. Classify each one as durable policy, direct authority, temporary exception, or local implementation detail.
3. Record durable decisions before implementation spreads across multiple files or teams.
4. Require changes to cite the decision records they rely on.
5. Review uncited but repeated choices as candidates for new policy.

Warning signs:

- the same design question is answered differently in parallel work
- reviewers approve based on remembered context that is not recorded
- exceptions persist with no owner or expiry

### Checkpoint Pattern

Checkpoints should be mandatory whenever work may pause, transfer, or compact.

Every checkpoint should capture:

- current objective
- completed steps and evidence
- pending steps in order
- current enforcement status
- open risks or blockers
- exact next action

Good checkpoints are small, explicit, and reproducible. A new operator should be able to resume work without interviewing the previous operator.

### Archive Pattern

Archives are not a dumping ground. They are a control boundary.

- move superseded guidance, historical evidence, and obsolete outputs out of the active lane
- keep the archive readable and traceable, but clearly non-active
- define the event that causes material to move from active to superseded
- prevent archived material from being cited as current policy by default

When active and historical material share the same surface, readers will apply outdated guidance as if it were current.

### Retrieval Pattern

Retrieval should narrow before it broadens.

Recommended lookup order:

1. start from the path, feature, or rule question
2. resolve the owning authority surface
3. inspect the published contract view if a readable projection helps
4. inspect enforcement references for how the rule is applied
5. broaden to full-text search only if the authority path is still unclear

This order reduces the chance that a contributor treats an incidental mention as the governing rule.

### Layered Enforcement Pattern

Assign different responsibilities to different layers.

Local layer:

- fast scope checks
- metadata checks
- lightweight freshness or publication checks
- retrieval refresh where practical

CI layer:

- policy compatibility
- schema and structure validation
- determinism checks
- tests and coverage floors
- blocking drift checks

Review and release layer:

- decision and exception approval
- stage alignment
- promotion readiness
- confirmation that temporary waivers are explicit and still valid

This split keeps local feedback fast while preserving an authoritative blocking floor.

## Implementation Review Checklist

Use this checklist to assess whether the model is complete.

- Is there one clearly owned semantic authority root?
- Are readable policy surfaces traceable back to authority?
- Is freshness enforced for derived publication?
- Does enforcement run against a pinned compatible policy baseline?
- Is there a formal execution protocol for multi-step work?
- Do local hooks, CI, and release checks each have distinct responsibilities?
- Can contributors resolve governing rules from a path or question quickly?
- Are material decisions recorded before they become hidden defaults?
- Do checkpoints preserve exact next actions and enforcement state?
- Are superseded materials archived out of the active lane?

If the answer to several of these questions is no, the issue is usually missing layer separation rather than missing automation volume.

## Rollout Guidance

Start small, but install complete boundaries. A narrow implementation with clear authority, provenance, baseline pinning, and recovery is safer than a large automation stack with unclear ownership. Expand coverage only after the authority path, enforcement floor, and recovery pattern are stable.

The practical test is simple: a contributor should be able to find the governing rule, understand the current published contract, run or observe the correct enforcement path, pause safely, and resume later without depending on undocumented memory.
