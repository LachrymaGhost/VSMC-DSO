---
role: Spec.TaskClass.Ontology
actor: AI
version: 1.1.0
status: draft
maintained_by: Aire System Architect (ASA)
domain_tags: [system, routing, task_ontology]
license: Apache-2.0
no_execution_pledge: true
---

# Purpose

This specification defines a **closed, canonical ontology of TASK.* identifiers** representing distinct cognitive work regimes used throughout the Aire system.

The ontology functions as a **vocabulary contract** for routing, semantic anchoring, and overlay compatibility. It contains no behavior, execution logic, thresholds, or policies.

---

# Definitions

Each TASK represents a **primary cognitive intent**, independent of topic, domain, or role.

Only one TASK is considered primary for a given routing decision.

---

## TASK.SPEC_AUTHORING
**Description:** Structured creation or regeneration of specifications, schemas, or formal system documents.

**Primary intent:** Produce governed, reviewable artifacts.

**Non-goals:** Ideation, conversational explanation, execution planning.

---

## TASK.DEEP_RESEARCH
**Description:** Multi-source research involving legal, statutory, historical, or axiomatic analysis.

**Primary intent:** Establish authoritative grounding or long-horizon understanding.

**Non-goals:** Summarization-only work, procedural planning, drafting final specs.

---

## TASK.DIAGNOSTIC_ANALYSIS
**Description:** Investigation of faults, inconsistencies, or failure modes.

**Primary intent:** Identify causes and contributing factors.

**Non-goals:** Refactoring, publishing, exploratory ideation.

---

## TASK.DIAGNOSTIC_DEBUG
**Description:** Targeted debugging of known issues within artifacts, systems, or specifications.

**Primary intent:** Isolate and correct concrete defects.

**Non-goals:** Broad system redesign, exploratory reasoning.

---

## TASK.PLANNING_DECOMPOSITION
**Description:** Breaking objectives into ordered steps, work units, or coordination plans.

**Primary intent:** Enable structured execution planning.

**Non-goals:** Performing execution, deep research.

---

## TASK.TRANSFORMATION_REWRITE
**Description:** Controlled transformation or rewriting of existing content into a new form.

**Primary intent:** Preserve meaning while changing structure or representation.

**Non-goals:** Introducing new concepts, exploratory reasoning.

---

## TASK.EXTRACTION_SUMMARIZATION
**Description:** Extracting key points or summarizing content from existing sources.

**Primary intent:** Reduce information volume while preserving relevance.

**Non-goals:** Analysis, validation, or synthesis across sources.

---

## TASK.VERIFICATION_VALIDATION
**Description:** Checking correctness, consistency, or compliance of artifacts or claims.

**Primary intent:** Confirm validity against known criteria.

**Non-goals:** Original analysis, drafting new content.

---

## TASK.ANALYTICAL_EVALUATION
**Description:** Comparative or critical evaluation of ideas, options, or claims.

**Primary intent:** Assess strengths, weaknesses, and implications.

**Non-goals:** Deep research, execution planning.

---

## TASK.REFRACTORING
**Description:** Structural improvement of existing artifacts without changing meaning.

**Primary intent:** Improve clarity, organization, or maintainability.

**Non-goals:** Adding new content or intent.

---

## TASK.EXPLORATORY_REASONING
**Description:** Open-ended conceptual exploration or ideation.

**Primary intent:** Discover possibilities or insights.

**Non-goals:** Formal specification, validation, or publishing.

---

## TASK.RELEASE_PUBLISHING
**Description:** Final preparation, normalization, or release of completed artifacts.

**Primary intent:** Produce a stable, consumable output.

**Non-goals:** Analysis, drafting, or refactoring.

---

## TASK.CONVERSATIONAL_SUPPORT
**Description:** Lightweight explanation, clarification, or assistance.

**Primary intent:** Aid understanding with minimal governance load.

**Non-goals:** Specification authoring, research, or validation.

---

# Completion Proof Block

```yaml
spec: Spec.TaskClass.Ontology
version: 1.1.0
checks:
  canonical_task_coverage: pass
  duplicate_definitions: none
  behavior_free: confirmed
status: complete
```

