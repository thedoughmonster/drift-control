# Drift Control Handbook

Drift control is an operating model for keeping semantic authority, readable guidance, enforcement, and recovery state aligned as a repository evolves. This handbook stays generic-first so teams can adapt the model across stacks, repository layouts, and tooling choices.

> **At a glance**
> This handbook has two lanes:
> 1. reusable control architecture
> 2. clearly labeled implementation examples when local detail helps

## Overview

| What this handbook does | What it does not do |
| --- | --- |
| explains a transferable drift-control model | assume one language, CI provider, or repo topology |
| shows how supporting systems fit together | require the local example repository structure |
| provides copyable system templates and prompts | turn example names into universal terms |

### Quick Start

If you are new to the model, read these first:

1. [Core Model](core-model.md)
2. [Minimum Viable Implementation](minimum-viable-implementation.md)
3. [Enforcement Model](enforcement-model.md)
4. [Implementation Guide](implementation-guide.md)

---

## Reading Paths

### Conceptual Path

Use this path when you want the model before the machinery.

1. [Core Model](core-model.md)
2. [Minimum Viable Implementation](minimum-viable-implementation.md)
3. [Enforcement Model](enforcement-model.md)

### Build Path

Use this path when you want to install the supporting systems.

1. [Code Index Template](code-index-template.md)
2. [Central Semantic Authority Template](canon-authority-template.md)
3. [CI Integration Template](ci-integration-template.md)
4. [tempgo Protocol Template](tempgo-protocol-template.md)

### Adaptation Path

Use this path when you need to map the model into your own repository.

1. Read [Implementation Guide](implementation-guide.md)
2. Work through the four system template pages
3. Pull the build prompts into your own repo planning flow
4. Read [Reference Implementation Example](reference-implementation-example.md) only after the generic model is clear

> **Reading rule**
> The example lane is deliberately secondary. Start with the generic pages, then use the example appendix only when you want a concrete mapping.

---

## System Templates

These pages focus on buildable supporting systems rather than the abstract model.

| Template | Main outcome | Best time to use it |
| --- | --- | --- |
| [Code Index Template](code-index-template.md) | local retrieval, rebuild automation, query entrypoints, and path-aware authority completion | when contributors cannot find the right file, symbol, or governing doc quickly |
| [Central Semantic Authority Template](canon-authority-template.md) | source-of-truth ownership, generated publication, provenance, and conflict control | when rule meaning is split across too many documents or tools |
| [CI Integration Template](ci-integration-template.md) | blocking merge floor, determinism checks, and workflow composition | when enforcement is inconsistent between local work and CI |
| [tempgo Protocol Template](tempgo-protocol-template.md) | sequential work packets, step-list authority, seam audits, and resume state | when multi-step work loses scope, order, or recovery clarity |

### What Each Template Includes

- a generic architecture explanation
- a clearly labeled example lane from this repository family
- fenced snippets or commands
- a Mermaid diagram where the system benefits from a flow view
- one repo-agnostic prompt that can be pasted into a CLI coding agent

---

## Handbook Map

| Goal | Read these pages |
| --- | --- |
| understand the vocabulary and control model | [Core Model](core-model.md), [Minimum Viable Implementation](minimum-viable-implementation.md) |
| understand enforcement and merge-time control | [Enforcement Model](enforcement-model.md), [CI Integration Template](ci-integration-template.md) |
| plan rollout and operating patterns | [Implementation Guide](implementation-guide.md), [tempgo Protocol Template](tempgo-protocol-template.md) |
| install supporting retrieval and authority systems | [Code Index Template](code-index-template.md), [Central Semantic Authority Template](canon-authority-template.md) |
| inspect one concrete mapping after the model is clear | [Reference Implementation Example](reference-implementation-example.md) |

---

## Using The Build Prompts

The system prompts are intentionally repo-agnostic. They work better if you give your coding agent a short local map first.

```text
Repository map for this implementation:
- authority or policy root: <path>
- main application or package roots: <path list>
- docs root: <path>
- CI provider and workflow location: <path or provider>
- local tooling directory: <path or "create one">
```

Then pair that map with the prompt that matches the actual weakness:

- use the code-index prompt when discovery and retrieval are weak
- use the central-authority prompt when live rule meaning is split or ambiguous
- use the CI prompt when checks are inconsistent, non-deterministic, or too shallow
- use the tempgo prompt when multi-step work loses sequence, scope, or resume state

> **Prompt discipline**
> Give the agent the local map first. A good prompt is stronger when the repository boundaries are explicit before implementation starts.

---

## Design Bias

| This handbook prefers | This handbook does not assume |
| --- | --- |
| generic-first explanations | one language |
| explicit source-of-truth boundaries | one CI provider |
| generated outputs with provenance | one docs generator |
| searchable and navigable long-form technical docs | one repository topology |
| copyable snippets and prompts that transfer across repositories | the local example repository's policy or skill system |
