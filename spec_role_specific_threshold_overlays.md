# Spec.RoleSpecific_Threshold_Overlays

---
role: Spec.RoleSpecific.ThresholdOverlays
actor: AI
version: 1.0.0
status: draft
maintained_by: Everett (Owner) • Engineer.Scotty (Architect)
domain_tags: [governance, tuning]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose

Define a mechanism for **role-specific drift sensitivity tuning** without modifying core axioms.

---
## Overlay Model

Each role MAY define:
- entropy tolerance
- structural strictness
- trigger latency

---
## Example

```yaml
role: Spec.Master.DeepResearch
thresholds:
  semantic_entropy: high
  structural_integrity: medium
```

---
## Completion Statement

Overlays tune **sensitivity**, not truth.

