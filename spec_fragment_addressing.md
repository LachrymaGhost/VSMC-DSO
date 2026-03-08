# Spec.Fragment.Addressing.Schema
---
role: Fragment Addressing Schema
actor: AI
version: 0.1.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, fragments, governance]
license: Apache-2.0
no_execution_pledge: true
---

## Purpose
Define a universal, deterministic scheme for addressing **parts of specs** so routing and context assembly can select only required slices.

## Non-Negotiable Requirements
- MUST support document, section, anchor/token, and field-level references.
- MUST be human-authorable and machine-parseable.
- MUST not rely on a specific markdown parser.

## Schema
### Fragment Reference Grammar
```
<SpecName>
<SpecName>#<SectionPath>
<SpecName>@anchor:<token>
<SpecName>::<SchemaPath>
```

### Examples
- `Spec.Context.Assembly.Protocol`
- `Spec.Context.Assembly.Protocol#ContextBundle`
- `Spec.SemanticRouting.Map@anchor:precedence`
- `Spec.Fragment.Addressing.Schema::Schema.fragment_ref`

### Normalization Rules
- Case-insensitive matching.
- Whitespace collapsed to single dashes.
- Heading collisions resolved by first occurrence, else error.

### Ambiguity Resolution
- If multiple fragments match, resolution FAILS.
- Caller MUST refine reference.

## Validation Rules
- Spec MUST exist in TOC spine.
- Section/anchor/schema path MUST exist exactly once.

## Examples
### Valid Example 1
`Spec.SemanticAnchoring.Index#TaskClasses`

### Valid Example 2
`Spec.RoleRouting.Overlays::Schema.overrides`

### Invalid Example
`Spec.Unknown#Foo`
*Invalid: Spec does not exist.*

## Completion Proof Block
```yaml
spec: Spec.Fragment.Addressing.Schema
version: 0.1.0
checks:
  supports_all_levels: pass
  ambiguity_handled: pass
status: complete
```

