# Drift Control Handbook

Drift control is an operating model for keeping rule meaning, readable guidance, enforcement, and recovery state aligned as a repository evolves. This handbook explains the model in a way that transfers across stacks, repository shapes, and tooling choices.

It does two jobs at once:

- it explains the reusable control architecture
- it shows one concrete repository family as a labeled example lane when implementation details help

> **Use this like a system handbook, not a blog post.**
> The main pages teach the model. The system templates show how to build the machinery.

## Start Here

If you are new to the model, read these first:

1. [Core Model](core-model.md)
2. [Minimum Viable Implementation](minimum-viable-implementation.md)
3. [Enforcement Model](enforcement-model.md)
4. [Implementation Guide](implementation-guide.md)

## System Templates

These pages are the build-focused part of the handbook. Each one includes:

- a generic architecture explanation
- a clearly labeled example from this repository
- code or configuration snippets
- a mermaid diagram
- one complete repo-agnostic build prompt you can drop into a CLI coding agent

| System | What you get | Best use |
| --- | --- | --- |
| [Code Index Template](code-index-template.md) | local retrieval surfaces, rebuild automation, query entrypoints, and authority completion | build a fast local discovery layer before contributors start opening files |
| [Central Semantic Authority Template](canon-authority-template.md) | source-of-truth lane design, generated publication surfaces, provenance, and conflict resolution | define where live rule meaning actually comes from |
| [CI Integration Template](ci-integration-template.md) | merge-blocking gates, determinism enforcement, and workflow composition | turn drift-control expectations into a shared merge floor |
| [tempgo Protocol Template](tempgo-protocol-template.md) | packetized workstreams, step-list authority, seam audits, and resumable execution state | run complex documentation or implementation work without losing sequence or scope |

## Reading Paths

### I Want The Conceptual Model

1. [Core Model](core-model.md)
2. [Minimum Viable Implementation](minimum-viable-implementation.md)
3. [Enforcement Model](enforcement-model.md)

### I Want To Build The Supporting Systems

1. [Code Index Template](code-index-template.md)
2. [Central Semantic Authority Template](canon-authority-template.md)
3. [CI Integration Template](ci-integration-template.md)
4. [tempgo Protocol Template](tempgo-protocol-template.md)

### I Want To Adapt This To My Own Repository

1. Read [Implementation Guide](implementation-guide.md)
2. Work through the four system template pages
3. Pull the build prompts from each template into your own repo planning flow
4. Use [Reference Implementation Example](reference-implementation-example.md) only after the generic model is clear

## What The Handbook Covers

| Area | Main pages |
| --- | --- |
| model and vocabulary | [Core Model](core-model.md), [Minimum Viable Implementation](minimum-viable-implementation.md) |
| control layers and enforcement | [Enforcement Model](enforcement-model.md), [CI Integration Template](ci-integration-template.md) |
| adoption and operation | [Implementation Guide](implementation-guide.md), [tempgo Protocol Template](tempgo-protocol-template.md) |
| supporting retrieval and authority infrastructure | [Code Index Template](code-index-template.md), [Central Semantic Authority Template](canon-authority-template.md) |
| concrete example lane | [Reference Implementation Example](reference-implementation-example.md) |

## Using The Build Prompts Well

The four build prompts are intentionally repo-agnostic, but they work best if you give your coding agent a short local mapping first:

```text
Repository map for this implementation:
- authority or policy root: <path>
- main application or package roots: <path list>
- docs root: <path>
- CI provider and workflow location: <path or provider>
- local tooling directory: <path or "create one">
```

Then pair that mapping with the relevant system prompt:

- use the code-index prompt when discovery and retrieval are weak
- use the central-authority prompt when rule meaning is split or ambiguous
- use the CI prompt when checks are inconsistent or non-deterministic
- use the tempgo prompt when multi-step work loses scope, sequence, or resume state

## Design Bias

This handbook prefers:

- generic-first explanations
- explicit source-of-truth boundaries
- generated outputs with provenance
- searchable, navigable, long-form technical docs
- copyable snippets and prompts that can move between repositories

It does **not** assume:

- a specific language
- a specific CI provider
- a specific docs generator beyond this published presentation
- a specific repository topology
- the local policy or skill system used in the example repository
