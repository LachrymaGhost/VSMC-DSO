# Spec.Context.Assembly.Protocol
---
role: Context Assembly Protocol
actor: AI
version: 0.1.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, context, governance]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose
Define the deterministic procedure for assembling an **active context bundle** for each turn.

## Non-Negotiable Requirements
- MUST follow ordered phases from analysis to assembly.
- MUST enforce minimality.
- MUST HALT SAFE on ambiguity or missing fragments.
- MUST reference drift handling only via existing specs.

## Procedure
1. Input Analysis (role + task classification)
2. Candidate Retrieval (TOC spine)
3. Routing Resolution (SemanticRouting.Map)
4. Fragment Selection (Fragment.Addressing.Schema)
5. Context Bundle Assembly (ordered)
6. Re-anchor Consultation (if allowed)

## Schema
```yaml
ContextBundle:
  bundle_id: <uuid>
  role: <role_name>
  task_class: TASK.*
  included_refs:
    - spec: Spec.Name
      fragment: <fragment_ref>
  excluded_refs: [Spec.Name]
  assembly_order: [Spec.Name...]
  notes: <optional>
```

## Ordering Rules
1. Role definition
2. Task ontology
3. Routing specs
4. Assembly protocol
5. Optional overlays

## Validation Rules
- At least one included_ref required.
- assembly_order MUST match included_refs.
- No excluded spec may appear in included_refs.

## Examples
### Valid Example 1
```yaml
bundle_id: CB-001
role: Architect
task_class: TASK.SpecAuthoring
included_refs:
  - spec: Spec.SemanticRouting.Map
assembly_order:
  - Spec.SemanticRouting.Map
```

### Valid Example 2
```yaml
bundle_id: CB-002
role: Deep Thought
task_class: TASK.DeepResearch
included_refs:
  - spec: Spec.SemanticAnchoring.Index
assembly_order:
  - Spec.SemanticAnchoring.Index
```

### Invalid Example
```yaml
bundle_id: CB-003
included_refs: []
```
*Invalid: no included refs.*

## Completion Proof Block
```yaml
spec: Spec.Context.Assembly.Protocol
version: 0.1.0
checks:
  ordering_defined: pass
  minimality_enforced: pass
status: complete
```

