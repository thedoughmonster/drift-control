# Minimum Viable Implementation

This page defines the smallest implementation that still deserves to be called drift control. The threshold is not "some automation exists." The threshold is that the system can keep rule meaning, readable guidance, enforcement, and recovery aligned under normal team pressure.

## Absolute Minimum

The minimum viable implementation has six required elements.

1. One authority source for rule meaning.
   A team needs one owned place where rules, constraints, and allowed exceptions are defined. If meaning is split across code comments, automation defaults, review folklore, and informal notes, every later control becomes negotiable.

2. Readable publication that stays subordinate to authority.
   People still need human-readable guidance. The minimum model therefore needs a published explanation of the rules, but that publication must remain traceable to the authority source and must not evolve as an ungoverned peer.

3. A stable baseline for enforcement.
   Enforcement should run against a known rule baseline, not whatever happens to be nearby at execution time. In a simple setup this can be a versioned rule set in the same repository. In a more distributed setup it may be a pinned external policy baseline. The key requirement is that the checked rule set is identifiable and reviewable.

4. Blocking enforcement for the failure modes that create immediate drift.
   At minimum, the system should block scope violations, broken schema or structure, stale or inconsistent rule projections, failing tests for the governed surface, and determinism failures such as introduced tracked-file drift. If those checks are only advisory, the model is too weak to hold its shape.

5. Explicit recovery for interrupted multi-step work.
   The minimum model needs a durable way to pause and resume work that spans more than one step, session, or contributor. A checkpoint record, current-state file, or equivalent mechanism is enough; relying on memory, chat transcripts, or issue comments alone is not.

6. Supersession separation.
   Historical guidance, retired rules, and replaced evidence must move into a clearly non-active lane. If current and superseded material stay mixed together, readers will treat both as live and documentation drift begins immediately.

If any one of these six is missing, the system may still have useful quality controls, but it is not yet operating as a drift-control model.

## Complexity-Triggered Additions

Some controls are not universal from day one, but they become mandatory once the environment becomes more complex.

- Add durable decision records when architectural choices, exceptions, or process rules need to survive staff turnover or parallel work. Without them, teams end up rediscovering the same rule intent during review.
- Add local pre-integration checks when central automation is too slow or too distant from daily work. Early failure is not just convenience; it reduces the amount of drift packaged into a single change.
- Add indexed or path-aware retrieval when the authority surface becomes large enough that people cannot reliably find the right source by memory alone.
- Add stage or workflow controls when work crosses distinct phases, owners, or release gates. This prevents a technically valid change from skipping required sequence controls.
- Add coverage floors and structural limits when the governed surface is large enough that "tests pass" no longer says enough about real protection.
- Add stronger archive and publication separation when compliance, audit, or public documentation obligations make historical material more visible to readers.
- Add bounded execution plans and checkpoint audits when work is frequently handed between sessions, contributors, or automation actors.

The trigger is not organizational prestige. The trigger is loss of reliable local judgment. Once contributors can no longer infer the right source, sequence, or baseline from simple context, the missing control becomes part of the minimum for that environment.

## What The Fuller Model Adds Beyond Minimum

A fuller model extends the minimum in three directions.

First, it adds layered enforcement. Instead of relying on one blocking job, it uses complementary checks at local, shared, and release-time boundaries. That creates deliberate redundancy, which matters because drift often enters through the easiest bypass route.

Second, it adds stronger operational discipline. Decision records, stage ownership, structured execution plans, checkpoint summaries, and resume rules keep the process itself from becoming ambiguous. This is the difference between a system that can recover cleanly and one that has to reconstruct intent after every interruption.

Third, it adds faster interpretation. Rich publication, path-aware retrieval, provenance metadata, and freshness checks make it easier for a contributor to answer three questions quickly: what the rule is, whether the readable version is current, and where enforcement should prove conformance.

The fuller model is not a different philosophy. It is the same model under higher load: more people, more governed surfaces, more automation, more handoffs, and more need to distinguish current authority from convenient summaries.
