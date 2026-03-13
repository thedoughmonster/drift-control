# Core Model

Drift control is an operating model for keeping five things aligned over time: the meaning of the rules, the published explanation of those rules, the automation that enforces them, the decisions that justify them, and the recovery record that lets work stop and resume without guesswork. The point is not to prevent all change. The point is to prevent silent, accidental, or ambiguous change.

In practice, drift appears in several forms at once. Code can diverge from the rule set. Published guidance can lag behind the authority source. Automation can keep running against an outdated baseline. Teams can rely on remembered intent instead of recorded decisions. Historical material can remain visible in the same lane as active guidance and start acting like live instruction. A usable drift-control model treats all of those as the same class of problem: the system has lost alignment between what is authoritative, what is readable, what is enforced, and what is resumable.

## What Drift Control Is

Drift control starts by separating responsibilities that teams often collapse together:

- authority defines what the rule means
- publication makes the rule readable
- enforcement checks whether work conforms to the rule
- recovery preserves enough durable state to continue safely after interruption
- retrieval helps people find the right source quickly without becoming a source of meaning itself

That separation matters because convenience surfaces are attractive. Teams naturally read the nearest document, trust the latest generated output, or follow the automation they can see. If those surfaces are allowed to define meaning as well as expose it, the system accumulates shadow authority. Drift control removes that ambiguity by making each surface do one job and prove where it got its information.

## System Model

The model is easiest to understand as a small set of cooperating surfaces:

| Surface | Primary job | Must not do |
| --- | --- | --- |
| Authority | Own rule meaning, allowed exceptions, and durable decisions | Depend on local habit or unpublished interpretation |
| Publication | Present readable contracts, guides, and summaries | Override or silently extend authority |
| Enforcement | Block, warn on, or detect nonconforming changes | Invent its own meaning when the source is unclear |
| Recovery | Preserve checkpoints, supersession, and resume state | Rely on memory or chat history as the only record |
| Retrieval | Help operators locate the right authority or publication surface | Become an unreviewed policy store |

Several design rules follow from that model.

- Keep rule meaning in one owned authority lane, even if the system has many readers and many automation entrypoints.
- Treat readable contracts as projections of authority. They can explain, but they do not outrank the source that defines the rule.
- Distribute enforcement across the points where drift actually enters the system: local work, shared automation, staged delivery, and release flow.
- Make recovery explicit. If the system cannot pause and resume from durable state, process drift will eventually become implementation drift.
- Keep retrieval supportive. Fast lookup reduces operator error, but lookup tooling should point to authority rather than trying to replace it.

## The End-To-End Drift Loop

Drift control is a loop, not a static document set.

1. A rule, constraint, or decision is established in the authority surface.
2. That meaning is published in a readable form so implementers and reviewers can consume it.
3. A known baseline of the authority surface is attached to the implementation context so the system is not enforcing a moving target.
4. Enforcement runs through local checks, shared automation, and workflow controls to detect or block divergence.
5. Results are recorded through checkpoints, supersession records, and other recovery artifacts so the next session inherits durable state instead of reconstructing intent.
6. Operators use retrieval to re-enter the loop at the right point, verify freshness and provenance, and continue from the current authoritative state.

Each step closes a specific failure mode. Without authoritative rule definition, enforcement is arbitrary. Without publication, humans cannot reliably apply the rules. Without a pinned baseline, automation may be consistent but aimed at the wrong target. Without recovery, interruptions destroy sequence integrity. Without retrieval, people fall back to broad searching and stale local memory.

## Why This Model Transfers

The model transfers because it is role-based rather than tool-based. Another team does not need the same repository layout, generator, continuous integration service, or command names. It needs the same control boundaries.

If a team can answer the following questions clearly, it can adopt the model in its own environment:

- Where does rule meaning live?
- How is that meaning published for readers?
- What automation enforces it before and after integration?
- How does interrupted work resume from durable state?
- How does a person quickly find the current authoritative source?

The concrete implementation can vary widely. One team may use generated reference pages, another may use a policy database plus checked-in exports. One team may rely heavily on local hooks, another may emphasize central automation. One team may use lightweight checkpoint files, another may use a structured execution log. The model still transfers as long as the boundaries remain intact: authority stays authoritative, publication stays traceable, enforcement stays subordinate to authority, and recovery stays explicit.

## Evidence Standard

Use a short evidence hierarchy when interpreting the system:

- Authority decides meaning. If a readable guide disagrees with the authority source, the authority source wins.
- Publication explains meaning. It is useful evidence of what readers were expected to consume, but it is subordinate evidence when the question is what the rule actually is.
- Enforcement shows what the system currently checks. It proves implementation state, not necessarily correct meaning, so enforcement should be interpreted against authority rather than in isolation.
- Recovery and archive records show sequence and history. They explain how the current state was reached, but they do not become active authority unless they are explicitly promoted.

In practical review terms: use authority to resolve ambiguity, publication to orient the reader, enforcement to confirm operational behavior, and recovery records to understand continuity and supersession.
