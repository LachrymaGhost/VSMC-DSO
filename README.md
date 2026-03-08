# VSMC DSO

## What This Is

`VSMC DSO` is a spec-first **Veteran Digital Service Officer** program pack built around deterministic, governed artifact production for veteran-support workflows.

The repository is structured as an operating system for a DSO-style AI program rather than a single prompt or persona. It defines:

- orchestration rules
- claims strategy logic
- legal knowledge boundaries
- artifact schemas and templates
- diagnostics and runbooks
- release/provenance controls

The project is explicitly governance-heavy and non-executing by default.

## Core Program Shape

The central role is `DSO.Veteran.Mainframe`, which acts as the **L0 orchestrator** for the overall system.

It coordinates a deterministic layered architecture:

- `L1` knowledge and policy grounding
- `L2` claims strategy and Ground-Truth Verification
- `L3` artifact schemas and functional contracts
- `L4` formatting and final presentation

This structure is meant to keep veteran-support outputs lawful, documented, and explainable while preventing drift and uncontrolled reasoning.

## What The System Is Meant To Do

This pack is designed to support veteran-benefit and advocacy-oriented workflows by:

- mapping user intent to the correct artifact path
- enforcing Ground-Truth Verification before facts influence outputs
- producing structured support artifacts
- generating lay and buddy statement materials
- packaging outputs with manifests, checksums, and release proofs
- maintaining diagnostics, runbooks, and auditability

It is built to maximize documented, lawful benefit to veterans while preserving scope discipline.

## Major Components

Key surfaces in this repository include:

- `dso.veteran.mainframe.v1.1.1.spec.md`
- `dso.strategy.claims.v1.1.1.spec.md`
- `dso.knowledge.legal.v1.1.1.spec.md`
- `dso.functions.artifacts.v1.1.1.spec.md`
- `dso.formatting.templates.v1.1.1.spec.md`
- `dso.artifact.lay-statement.v1.0.0.spec.md`
- `artifact_publisher.md`
- `system_diagnostic.md`
- `doc_runbook.md`
- `eval.core.qualitygate.md`

Supporting materials also include semantic anchoring, routing, fragment addressing, drift control, and safe-halt/deep-research guidance.

## Design Principles

This program is built around a few non-negotiable constraints:

1. Facts must be verified before they propagate.
Ground-Truth Verification is central to the strategy layer.

2. Strategy, schema, and formatting stay separated.
The system is layered to reduce leakage and role confusion.

3. Outputs must be deterministic and auditable.
The same inputs should produce the same outputs, with provenance.

4. The system must know when to halt.
Ambiguity, conflict, or scope overreach should stop production rather than invite guessing.

5. Veteran support must remain bounded.
The system may assist with structured claims-support artifacts, but it does not become legal or medical authority.

## Typical Use Cases

This repository is suited for:

- preserving continuity of the DSO program design
- loading the DSO stack into an AI runtime or orchestration environment
- reviewing the layered architecture and governance model
- regenerating veteran-support artifacts from deterministic specs
- auditing how claims strategy and release controls are intended to work

## License

The major role/spec files in this project declare `Apache-2.0`. Keep repository licensing aligned with those declarations and any Owner-specific decisions for the broader program.

## Summary

This is not just a persona pack. It is a governed veteran-services architecture: strategy-locked, audit-oriented, and structured to produce stable support artifacts without crossing out of scope.
