# Spec.Drift_Axioms_and_Metrics

---
role: Spec.Drift.AxiomsAndMetrics
actor: AI
version: 1.0.0
status: draft
maintained_by: Everett (Owner) • Engineer.Scotty (Architect)
domain_tags: [cognition, governance, metrics, long-context]
license: Apache-2.0
no_execution_pledge: true
---

## 1. Purpose

This specification **axiomatically defines “drift”** in governed AI systems and establishes a **truthful, mechanistically grounded metric framework** for detecting drift in long-context interactions.

This spec exists to prevent tooling, governance, and mitigation strategies from being built on stylistic heuristics, anthropomorphic assumptions, or post-hoc judgment.

This document is **foundational**. All downstream systems (TOC indexing, Anchor Beacons, Drift Triggers, Promotion Gates) MUST align to these axioms.

---
## 2. Core Definition (Non-Negotiable)

> **Drift is the loss of representational dominance of invariant constraints, independent of surface fluency, coherence, or politeness.**

Drift is **not**:
- forgetting
- confusion
- low confidence
- creativity
- topic change
- user-driven reframing

Drift **is**:
- entropy-driven regression toward the training prior
- weakening of constraint contrast
- substitution of explicit governance with generic heuristics

---
## 3. Foundational Axioms

### AXIOM 1 — Drift Is Representational, Not Behavioral

Observable output is a **late-stage artifact**. Drift originates in internal representation before any visible violation occurs.

Implication:
- Metrics MUST prioritize representational proxies over stylistic evaluation.

---
### AXIOM 2 — Roles Are Unstable High-Energy States

A role is not a persistent state. It is **re-instantiated at every token** via attention-weighted reconstruction.

Implication:
- Drift is inevitable without reinforcement.
- Stability must be engineered, not assumed.

---
### AXIOM 3 — Constraint Competition Is Zero-Sum

Attention bandwidth is finite.

As context grows:
- new tokens compete with old constraints
- local coherence competes with global invariants

Implication:
- Drift metrics must account for signal-to-noise degradation.

---
### AXIOM 4 — Affirmative Constraints Are More Durable Than Negative Ones

"Produce X" outlasts "Do not do Y".

Implication:
- Violations of **affirmative structure** are stronger drift signals than tone or exclusion errors.

---
### AXIOM 5 — Drift Feels Like Ease, Not Error

Internally, drift correlates with **lower perplexity**, not struggle.

Implication:
- Latency, hesitation, or difficulty are NOT drift indicators.

---
## 4. Drift Taxonomy

### 4.1 Pre-Drift (Constraint Tension Phase)

Characteristics:
- rising semantic entropy
- increased constraint competition
- internal conflict not yet visible

Status:
- reversible
- optimal intervention window

---
### 4.2 Active Drift (Constraint Dilution Phase)

Characteristics:
- heuristic takeover
- format weakening
- loss of mandatory structure

Status:
- partially reversible
- requires re-anchoring

---
### 4.3 Terminal Drift (Heuristic Collapse Phase)

Characteristics:
- full regression to generic assistant
- persona collapse or inversion
- hallucinated compliance

Status:
- not recoverable without reset

---
## 5. Metric Classes (Ordered by Reliability)

### CLASS A — Representational Metrics (Gold Standard)

These metrics track internal state proxies.

#### A1. Constraint Vector Similarity
- Measures cosine similarity between current activation and role constraint vector
- Monotonic decay = drift

#### A2. Constraint Tension Index
- Statistical distance between "desired" token distribution and "permitted" distribution
- Sharp spikes predict imminent drift

---
### CLASS B — Semantic Metrics (Early Warning)

#### B1. Semantic Entropy
- Divergence over meanings, not words
- Rising entropy = weakening constraint dominance

#### B2. Varentropy
- Volatility of entropy
- Spikes indicate nearing interference threshold

---
### CLASS C — Structural Metrics (Operational Proxies)

#### C1. Structural Integrity
- Presence of mandatory sections
- Schema completeness

#### C2. Format Rigidity
- JSON/YAML/Markdown validity
- Collapse = late-stage drift

---
### CLASS D — Behavioral Metrics (Low Confidence)

Use ONLY as corroborating signals.

Examples:
- tone softening ("must" → "should")
- metadiscourse leakage
- politeness resurgence

---
## 6. False Drift (Explicitly Excluded)

The following MUST NOT be classified as drift:

- repetition used for self-anchoring
- increased latency
- visible struggle or correction
- creative variation within constraints
- user-directed task pivot

Misclassification here causes **overcorrection drift**.

---
## 7. Drift Triggers (Principled)

A drift trigger MAY fire only when:

- at least one Class A or Class B metric crosses threshold
- OR multiple Class C metrics fail concurrently

A drift trigger MUST NOT fire on:
- tone alone
- verbosity
- politeness

---
## 8. Re-Anchoring Legitimacy Conditions

Re-anchoring is permitted ONLY when:
- drift is classified as Pre-Drift or Active Drift
- invariant constraints are still recoverable

Re-anchoring MUST prioritize:
1. structural reinstatement
2. constraint contrast restoration
3. minimal context injection

---
## 9. Governance Integration

This spec is:
- REQUIRED for TOC routing design
- REQUIRED for Anchor Beacon schemas
- REQUIRED for Drift Trigger logic
- REQUIRED for long-context promotion gates

Any system implementing drift mitigation without reference to this spec is **non-compliant**.

---
## 10. Completion Statement

This specification defines drift **truthfully**, **mechanistically**, and **operationally**.

Downstream systems SHALL treat drift as a **physics problem**, not a stylistic one.

---
## Completion Proof (Draft)

```yaml
proof_version: 1.0
artifact: Spec.Drift_Axioms_and_Metrics.md
status: DRAFT
scope: foundational
notes: "Defines drift as representational loss of constraint dominance; enables principled mitigation design."
```

