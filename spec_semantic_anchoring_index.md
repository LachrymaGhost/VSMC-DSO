---
role: Spec.SemanticAnchoring.Index
actor: AI
version: 1.0.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, routing, index]
license: Apache-2.0
no_execution_pledge: true
---

# Purpose

This specification defines the **Semantic Anchoring Index (TOC)** — a read-only, declarative map of canonical **Spec.* identifiers** available for contextual loading.

The TOC enables deterministic reference resolution for routing, overlays, and context assembly without encoding behavior, timing, or execution logic.

---

# Design Constraints

- Declarative only
- Non-normative
- Role-agnostic
- No routing logic or enforcement

---

# Core System Specifications

- Spec.Context.Assembly.Protocol
- Spec.SemanticRouting.Map
- Spec.Fragment.Addressing.Schema
- Spec.RoleRouting.Overlays
- Spec.TaskClass.Ontology

---

# DSO Semantic Surface

- Spec.DSO.Knowledge.Legal
- Spec.DSO.Knowledge.Policy
- Spec.DSO.Strategy.Claims
- Spec.DSO.Functions.Artifacts
- Spec.DSO.Artifact.LayStatement
- Spec.DSO.Formatting.Templates
- Spec.DSO.Veteran.Mainframe

---

# DeepThought Semantic Surface

- Spec.DeepThought.Statutory.Analysis
- Spec.DeepThought.CaseLaw.Analysis
- Spec.DeepThought.Research.Governance

---

# Shared / Supporting Surfaces

- templates/role.base.md
- templates/team.base.md
- templates/ai2ai-directive-spec.md
- primitives/relational-primitives.md

---

# Completion Proof Block

```yaml
spec: Spec.SemanticAnchoring.Index
version: 1.0.0
checks:
  overlay_reference_resolution: pass
  routing_reference_resolution: pass
  no_execution_logic: confirmed
status: complete
```

