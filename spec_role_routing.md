# Spec.RoleRouting.Overlays
---
role: Role Routing Overlays
actor: AI
version: 0.1.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, routing, roles]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose
Enable **per-role routing customization** without mutating the core SemanticRouting.Map.

## Non-Negotiable Requirements
- Overlays MUST be optional.
- Overlays MAY add/remove includes/excludes or adjust precedence.
- Overlays MUST NOT violate core non-negotiable routing constraints.

## Schema
```yaml
overlay_id: OVERLAY.<role_name>
role: <role_name>
intent_tag_expansion: [tag, ...]
overrides:
  add_include: [Spec.Name]
  remove_include: [Spec.Name]
  add_exclude: [Spec.Name]
  remove_exclude: [Spec.Name]
  precedence_adjustment: <integer>
```

## Conflict Resolution
- Overlay overrides base route.
- If conflict with core constraints → overlay ignored.

## Examples
### Valid Example 1 — Deep Thought
```yaml
overlay_id: OVERLAY.DeepThought
role: Deep Thought
intent_tag_expansion: [long_horizon]
overrides:
  add_include:
    - Spec.Drift_Axioms_and_Metrics
```

### Valid Example 2 — Sociology Assistant
```yaml
overlay_id: OVERLAY.SociologyAssistant
role: Sociology Assistant
overrides:
  remove_include:
    - Spec.Drift_Trigger.Policy
```

### Invalid Example
```yaml
overlay_id: OVERLAY.Bad
role: UnknownRole
```
*Invalid: role not registered.*

## Completion Proof Block
```yaml
spec: Spec.RoleRouting.Overlays
version: 0.1.0
checks:
  core_preserved: pass
  examples_validated: pass
status: complete
```

