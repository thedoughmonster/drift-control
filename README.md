# Drift Control Handbook

Drift control is an operating model for keeping rule meaning, readable guidance, executable enforcement, and recovery state aligned over time.

This handbook is for engineering teams that want to establish drift control in their own repositories. The main guide stays generic so teams can adopt the model without inheriting a specific repository layout, protocol family, or tooling stack.

> Start with the first four pages for the transferable model. Use the reference appendix only if you want to see one concrete implementation example.

## What You Can Do Here

- understand the core drift-control model and why it transfers across repositories
- identify the baseline minimum controls required for a credible implementation
- study the layered enforcement model for local checks, shared automation, and recovery
- follow a practical adoption sequence for rolling the model into a live engineering system

## Read By Goal

### I Need The Core Model

1. Read [Core Model](core-model.md).
2. Read [Minimum Viable Implementation](minimum-viable-implementation.md).
3. Read [Implementation Guide](implementation-guide.md).

### I Need To Evaluate Enforcement

1. Read [Core Model](core-model.md).
2. Read [Enforcement Model](enforcement-model.md).
3. Read [Implementation Guide](implementation-guide.md).

### I Need A Concrete Example

1. Read the main handbook pages first.
2. Then use [Reference Implementation Example](reference-implementation-example.md).

## Documentation Structure

| Page | Role |
| --- | --- |
| [Core Model](core-model.md) | defines the system model, the drift loop, and the authority/publication/evidence split |
| [Minimum Viable Implementation](minimum-viable-implementation.md) | defines the minimum baseline before a system deserves to be called drift control |
| [Enforcement Model](enforcement-model.md) | explains the layered enforcement stack and provides the control matrix |
| [Implementation Guide](implementation-guide.md) | gives the rollout order, operational patterns, and long-run operating guidance |
| [Reference Implementation Example](reference-implementation-example.md) | optional appendix with one concrete implementation lane and local naming example |

## Recommended Reading Order

If you want the handbook as a sequential technical guide, read the pages in this order:

1. [Core Model](core-model.md)
2. [Minimum Viable Implementation](minimum-viable-implementation.md)
3. [Enforcement Model](enforcement-model.md)
4. [Implementation Guide](implementation-guide.md)
5. [Reference Implementation Example](reference-implementation-example.md)

## What This Handbook Assumes

- you need a way to keep rules, docs, automation, and recovery aligned
- your repository has enough complexity that informal memory is no longer reliable
- you want a model that can survive handoffs, interruptions, and evolving tooling

## What This Handbook Does Not Assume

- a specific repository topology
- a specific CI provider
- a specific documentation generator
- a specific local command set
- a specific work orchestration workflow

Those are implementation choices. The handbook focuses on the control architecture that should remain stable even when the tooling changes.
