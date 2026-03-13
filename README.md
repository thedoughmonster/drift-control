# Drift Control Handbook

Drift control is the practice of keeping rule meaning, readable guidance, executable enforcement, and recovery state aligned as one operating model.

This guide is for engineering teams that want to establish drift control in their own repositories. The main pages stay generic so the model can be reused without inheriting a specific repository layout or naming scheme. A separate optional appendix shows one concrete implementation example.

## Start Here

If you are new to the model:

1. Read [Core Model](core-model.md).
2. Read [Minimum Viable Implementation](minimum-viable-implementation.md).
3. Read [Implementation Guide](implementation-guide.md).

If you are evaluating controls:

1. Read [Core Model](core-model.md).
2. Read [Enforcement Model](enforcement-model.md).
3. Read [Implementation Guide](implementation-guide.md).

If you want concrete examples:

1. Read the core pages first.
2. Then use [Reference Implementation Example](reference-implementation-example.md).

## Guide Map

| Page | Purpose |
| --- | --- |
| [Core Model](core-model.md) | explains what drift control is, why it matters, the system model, and the end-to-end drift loop |
| [Minimum Viable Implementation](minimum-viable-implementation.md) | defines the baseline minimum controls required for drift control |
| [Enforcement Model](enforcement-model.md) | explains the layered enforcement stack and includes the control matrix plus legend |
| [Implementation Guide](implementation-guide.md) | shows how to adopt the model in rollout order and how to operate it over time |
| [Reference Implementation Example](reference-implementation-example.md) | optional concrete examples of one implementation, including local names, paths, and commands |

## What This Handbook Covers

- how to separate authority, publication, enforcement, and recovery
- how to define the minimum viable control model
- how to build a fuller implementation without collapsing all control into CI
- how to keep checkpoints, archives, and retrieval from becoming weak points
- how to translate the model into another repository without copying local folklore

## What This Handbook Does Not Assume

- a specific repository topology
- a specific CI provider
- a specific documentation generator
- a specific local command set
- a specific work-orchestration workflow

Those details are implementation choices. The handbook focuses on the control architecture that should stay stable even when the tooling changes.

## Reading Rule

Treat the first four pages as the main handbook. Treat the reference implementation page as optional supporting material.
