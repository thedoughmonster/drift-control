# Enforcement Model

Drift control works best when enforcement is distributed across layers instead of pushed into one final gate. A healthy system defines meaning in one place, publishes readable guidance without giving that guidance independent authority, catches common problems early in local work, blocks higher-risk drift in shared automation, keeps multi-step work inside an explicit process, and preserves enough durable state to recover cleanly when work pauses.

That layered design matters because drift is not only a test failure. Drift can also appear as stale guidance, out-of-scope edits, version mismatch between policy and enforcement, missing decision context, informal stage skipping, or resume behavior that depends on memory instead of recorded state. If one layer misses the problem, another layer should still have a chance to detect it or stop it.

## The Enforcement Layers

1. The authority layer defines what the rules mean and prevents convenience surfaces from becoming shadow sources of truth.
2. The publication layer keeps readable outputs traceable to authority and treats stale published guidance as drift.
3. Local guardrails catch common mistakes before they spread into shared review or integration workflows.
4. Shared automation applies the blocking quality floor for scope, structure, determinism, validation, and other checks that must stay consistent.
5. Process controls keep staged or multi-step work aligned with approved scope, order, and decision context.
6. Recovery controls preserve checkpoints, archive boundaries, and resume state so a paused workflow can restart without guesswork.

The matrix below separates those roles on purpose. The source of meaning is not always the same thing as the mechanism that enforces behavior.

## How To Use The Matrix

Read each row from left to right:

1. Start with the concern being controlled.
2. Identify the authority that defines the rule.
3. Check which mechanisms enforce or reinforce it.
4. Use the layer and control codes to see whether the row is defining meaning, blocking change, detecting drift, correcting state, or supporting recovery.

If your implementation has a mechanism but no clear authority, the rule is probably underspecified. If it has authority but no credible enforcement path, the rule is probably aspirational.

## Legend

- Layer codes: `A` = authority, `P` = publication, `L` = local runtime guardrail, `C` = shared automation, `S` = process control, `R` = recovery support
- Control codes: `Pr` = preventive, `Dt` = detective, `Cr` = corrective, `Rv` = recovery-oriented

## Enforcement Matrix

| Concern | Primary authority | Main enforcement mechanisms | Layer(s) | Control(s) | Failure or recovery note |
| --- | --- | --- | --- | --- | --- |
| Rule meaning stays centralized | Policy authority and explicitly authoritative records | Ownership boundaries, thin routing surfaces, authority-only update rules | `A` | `Pr` | Prevents implementation and tooling surfaces from becoming shadow rule stores. |
| Published guidance stays subordinate to authority | Policy authority | Generation workflow, provenance metadata, freshness checks, publication review | `A`,`P` | `Pr`,`Dt` | Stale or hand-edited published output counts as drift. |
| Active guidance stays separate from archived evidence | Policy authority and document integrity rules | Active-surface validation, archive separation checks, supersession review | `P`,`C`,`R` | `Pr`,`Dt`,`Rv` | Historical material remains available without continuing to act like live guidance. |
| Enforcement runs against a pinned policy baseline | Release and compatibility policy | Version pinning, source-freeze checks, baseline preparation before gates run | `A`,`C` | `Pr`,`Dt` | Blocks enforcement from silently drifting to a different rule set mid-change. |
| Change scope stays inside the approved boundary | Scope policy and process contract | Scope validation, ownership checks, change-set review, approval metadata | `C`,`S` | `Pr`,`Dt` | Stops out-of-scope edits from entering the governed change set. |
| Decisions remain attached to implementation work | Decision records and approval policy | Required decision metadata, review gates, approval checks | `A`,`C`,`S` | `Pr`,`Dt` | High-impact changes should remain traceable to an approved decision. |
| The shared quality floor stays consistent | Automation policy | Required validation chain, blocking integration checks, protected merge rules | `A`,`C` | `Pr`,`Dt` | Prevents teams from enforcing different minimum standards in different workflows. |
| Execution remains deterministic | Build and integration policy | Determinism checks, generated-output consistency checks, tracked-state comparison | `C` | `Dt` | Fails when a run introduces unplanned state changes or inconsistent outputs. |
| Coverage expectations stay policy-bound | Quality policy | Coverage-floor checks, scoped coverage rules, missing-critical-surface handling | `A`,`C` | `Dt` | Critical areas can be treated as zero-covered when evidence is missing. |
| Structural and style drift is blocked | Structural and formatting policy | Schema validation, structure checks, style gates, token or size limits | `C` | `Pr`,`Dt` | Hard limits fail immediately; any exceptions should be explicit and reviewable. |
| Local work faces early guardrails | Local automation policy | Pre-change hooks, commit checks, post-change refresh steps | `L` | `Pr`,`Dt`,`Cr` | Moves common failures earlier and can refresh local support assets after changes. |
| Stage order and declared scope stay aligned | Process contract | Stage model, approval checkpoints, review metadata, advancement rules | `S` | `Pr`,`Dt` | Prevents stage skipping and improvised scope changes during governed work. |
| Multi-step work stays sequenced | Work protocol | Scoped work plans, boundary reviews, checkpoint rules, explicit next-step rules | `S`,`R` | `Pr`,`Dt`,`Rv` | Keeps long-running work from being re-planned informally in the middle of execution. |
| Pause and resume behavior stays explicit | Checkpoint and resume policy | Durable summaries, recorded step state, resume validation | `R` | `Dt`,`Rv` | Resume should read durable state instead of relying on conversational memory. |
| Retrieval starts from the right authority surface | Retrieval and lookup policy | Indexed lookup, source-aware search order, authority-first navigation | `S`,`R` | `Pr`,`Dt` | Reduces lookup drift by guiding operators to the owning source before broad scanning. |
| Local retrieval support stays refreshable | Tooling and recovery policy | Reindexing workflows, refresh triggers after selected changes, manual rebuild flow | `L`,`R` | `Cr`,`Rv` | Restores local lookup quality after changes without redefining the underlying rules. |

The matrix is intentionally redundant. Strong drift control depends on overlap with separation of roles: one layer defines meaning, several layers reinforce it, and recovery remains explicit when prevention is not enough.
