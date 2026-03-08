# Spec.Anchor_Beacon.Schema

---
role: Spec.AnchorBeacon.Schema
actor: AI
version: 1.0.0
status: draft
maintained_by: Everett (Owner) • Engineer.Scotty (Architect)
domain_tags: [cognition, metadata]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose

Define a **minimal metadata beacon** used to reassert role and task salience in long-context interactions.

---
## Principles

- Minimal token footprint
- Declarative
- Non-normative

---
## Schema

```yaml
ANCHOR:
  role: <role_name>
  task_class: <TASK.*>
  routing_index: Spec.SemanticAnchoring.Index@1.0.0
  drift_policy: Spec.Drift.Trigger.Policy@1.0.0
```

---
## Usage Constraints

- Emitted only on drift trigger or task transition
- MUST NOT include prose

---
## Completion Statement

Anchor Beacons restore **contrast**, not memory.

