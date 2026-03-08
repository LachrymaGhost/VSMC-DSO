# Spec.SemanticRouting.Map
---
role: Semantic Routing Map
actor: AI
version: 0.1.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, routing, governance]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose
Define deterministic, declarative routing rules that map **ROLE + TASK + intent signals** to a **minimal, justified set of spec references**, using `Spec.SemanticAnchoring.Index` as the TOC spine.

## Non-Negotiable Requirements
- MUST be purely declarative (no execution or inference logic).
- MUST support positive routing (`include`) and explicit negative routing (`exclude`).
- MUST attach justification tags for every include/exclude.
- MUST reference specs and/or fragments by name only; no inline content.
- MUST defer conflict resolution to explicit precedence rules.

## Schema
```yaml
route_id: ROUTE.<stable_id>
match:
  role: <role_name> | null
  role_family: <family_name> | null
  task_class: TASK.*
  intent_tags: [tag, ...]
include:
  - spec: Spec.Name
    fragment: <optional fragment_ref>
exclude:
  - spec: Spec.Name
    fragment: <optional fragment_ref>
rationale:
  include:
    Spec.Name[#fragment]: [justification_tag, ...]
  exclude:
    Spec.Name[#fragment]: [justification_tag, ...]
precedence:
  priority: <integer>
  tie_breaker: most_specific | highest_priority
```

## Validation Rules
- Either `role` or `role_family` MUST be set.
- `task_class` MUST resolve to `Spec.TaskClass.Ontology`.
- All referenced specs MUST exist in `Spec.SemanticAnchoring.Index`.
- `priority` MUST be unique per route.

## Examples
### Valid Example 1
```yaml
route_id: ROUTE.SPEC_AUTHORING.CORE
match:
  role_family: Architect
  task_class: TASK.SpecAuthoring
  intent_tags: [spec_authoring, format_strict]
include:
  - spec: Spec.Context.Assembly.Protocol
exclude:
  - spec: Spec.Drift_Trigger.Policy
rationale:
  include:
    Spec.Context.Assembly.Protocol: ["core_assembly"]
  exclude:
    Spec.Drift_Trigger.Policy: ["no_drift_handling"]
precedence:
  priority: 10
  tie_breaker: most_specific
```

### Valid Example 2
```yaml
route_id: ROUTE.RESEARCH.DEEP
match:
  role: Deep Thought
  task_class: TASK.DeepResearch
  intent_tags: [deep_research_report]
include:
  - spec: Spec.SemanticAnchoring.Index
exclude: []
rationale:
  include:
    Spec.SemanticAnchoring.Index: ["broad_discovery"]
precedence:
  priority: 20
  tie_breaker: highest_priority
```

### Invalid Example
```yaml
match:
  task_class: TASK.Unknown
```
*Invalid: missing role/role_family and invalid task_class.*

## Completion Proof Block
```yaml
spec: Spec.SemanticRouting.Map
version: 0.1.0
checks:
  declarative_only: pass
  rationale_present: pass
  precedence_defined: pass
status: complete
```

