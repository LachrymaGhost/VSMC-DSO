---
role: Spec.RoleRouting.Overlays
actor: AI
version: 1.1.1
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, routing, overlays]
license: Apache-2.0
no_execution_pledge: true
---

# Purpose

This specification defines **Role Routing Overlays** as a declarative metadata layer that enables role-specific routing preferences while remaining fully compatible with the frozen **Spec.SemanticAnchoring.Index (TOC v1.0)**.

Overlays influence **what semantic surfaces are selected or prioritized** during Context Assembly. They do **not** alter interpretation, reasoning, execution, or enforcement.

---

# Non-Negotiable Requirements

- Overlays are **routing metadata only**.
- Overlays MUST NOT modify, restate, or duplicate TOC routing logic.
- Overlays MUST use **canonical logical Spec.* identifiers** exactly as listed in the TOC.
- Overlays MUST NOT introduce new identifier namespaces.
- Overlays MUST NOT use file paths as identifiers.
- All fields are **advisory**; Context Assembly may ignore them under higher-priority governance.

---

# Overlay Schema (YAML)

```yaml
overlay_id: OVERLAY.<RoleName>
role: <RoleName>
applies_to_task_classes:
  - TASK.<CONSTANT>
intent_tag_bias:
  - <intent_tag>
include_bias:
  - Spec.<Canonical.ID>
exclude_bias:
  - Spec.<Canonical.ID>
precedence_adjustment: <symbolic_hint>

# Optional refinement tracks
depth_hints:
  Spec.<Canonical.ID>: <definition_only | section_level | full_doc>

execution_shape_hint: checklist | decision_tree | narrative | matrix | artifact_template

handoff_annotation:
  recommended_role: <RoleName>
  reason: <string>
```

---

# Field Semantics

| Field | Semantics |
|------|-----------|
| overlay_id | Stable, unique identifier for the overlay |
| role | Registered role name this overlay applies to |
| applies_to_task_classes | TASK.* constants from Spec.TaskClass.Ontology |
| intent_tag_bias | Advisory weighting toward specific intent tags |
| include_bias | Canonical Spec.* IDs preferred for loading |
| exclude_bias | Canonical Spec.* IDs to de-prioritize |
| precedence_adjustment | Symbolic ordering hint (no numeric logic) |
| depth_hints | Symbolic guidance on how much of a spec to surface |
| execution_shape_hint | Suggested structural form of the output |
| handoff_annotation | Advisory escalation signal; no control transfer |

---

# Validation Rules

An overlay is valid only if:

1. Every Spec.* identifier resolves verbatim in Spec.SemanticAnchoring.Index.
2. All task classes use TASK.* constants defined in Spec.TaskClass.Ontology.
3. No numeric thresholds, logic, or enforcement language is present.
4. Optional refinement tracks do not alter baseline routing semantics.

Invalid overlays MUST be ignored by Context Assembly.

---

# Conflict Resolution / Precedence Rules

1. Base TOC routing rules are evaluated first.
2. Role Routing Overlays are applied second as advisory bias.
3. If an overlay conflicts with higher-priority governance, it is ignored.
4. Overlays never override Context Assembly Protocols.

---

# Examples

## Valid Overlay — DSO

```yaml
overlay_id: OVERLAY.DSO
role: DSO
applies_to_task_classes:
  - TASK.DIAGNOSTIC_DEBUG
  - TASK.PLANNING_DECOMPOSITION
  - TASK.TRANSFORMATION_REWRITE
  - TASK.EXTRACTION_SUMMARIZATION
  - TASK.DEEP_RESEARCH
intent_tag_bias:
  - procedural
  - evidence_packet
include_bias:
  - Spec.DSO.Knowledge.Legal
  - Spec.DSO.Knowledge.Policy
  - Spec.Context.Assembly.Protocol
exclude_bias:
  - Spec.DeepThought.CaseLaw.Analysis
precedence_adjustment: favor

depth_hints:
  Spec.DSO.Knowledge.Legal: definition_only

execution_shape_hint: checklist

handoff_annotation:
  recommended_role: DeepThought
  reason: TASK.DEEP_RESEARCH with intent_tag policy_update or statutory_change
```

---

## Valid Overlay — DeepThought

```yaml
overlay_id: OVERLAY.DeepThought
role: DeepThought
applies_to_task_classes:
  - TASK.DEEP_RESEARCH
  - TASK.VERIFICATION_VALIDATION
  - TASK.ANALYTICAL_EVALUATION
intent_tag_bias:
  - governance
  - statutory
include_bias:
  - Spec.DeepThought.CaseLaw.Analysis
  - Spec.DeepThought.Statutory.Analysis
exclude_bias:
  - Spec.DSO.Knowledge.Policy
precedence_adjustment: elevate

depth_hints:
  Spec.DeepThought.CaseLaw.Analysis: full_doc
  Spec.DeepThought.Statutory.Analysis: full_doc

execution_shape_hint: narrative
```

---

## Invalid Overlay — Example (Task Class Violation)

```yaml
overlay_id: OVERLAY.BadExample
role: DSO
applies_to_task_classes:
  - analysis
include_bias:
  - Spec.DSO.Knowledge.Legal
```

**Violation:**
- Uses non-canonical task class (`analysis` instead of TASK.*)

---

# Completion Proof Block

```yaml
spec: Spec.RoleRouting.Overlays
version: 1.1.1
checks:
  toc_namespace_alignment: pass
  task_class_validation: pass
  example_resolution: pass
  non_normative_confirmed: pass
status: complete
```

