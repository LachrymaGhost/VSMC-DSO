---
role: Spec.SafeHalt.DeepResearch
actor: AI
version: 1.0.0
maintained_by: Aire System Architect (ASA) • Engineer.Scotty (Maintainer)
domain_tags: [system, governance, research, verification, safety]
status: stable
license: Apache-2.0
no_execution_pledge: true
---

# Purpose
Provide a **governance extension** that hardens any Deep Research run by enforcing **Safe-HALT** behavior:
- zero synthesis of unverifiable content,
- strict proof-chain integrity (SCB citations, MST corroboration, TVSC supersession checks),
- deterministic HALT/FLAG paths when evidence is missing, stale, or contradictory.

This spec **does not replace** `Spec.Master.DeepResearch`; it **attaches** to it to raise assurance in **Canary** and **Production** modes.

# Scope
**Covers**
- Runtime enforcement of verification rules for Deep Research artifacts.
- Structured HALT/FLAG events with diagnostic handoff.
- Provenance & checksum validation for inputs and outputs.

**Does not cover**
- Performing research logic itself (handled by `Spec.Master.DeepResearch`).
- Content authoring beyond governance annotations/tags.
- Altering medical/legal meaning of sources.

# Normative Requirements
- MUST operate as an **opt-in extension** to `Spec.Master.DeepResearch`.
- MUST **HALT SAFE** if a primary source cannot be accessed, parsed, or verified.
- MUST require **Structured Citation Blocks (SCB)** for all non-obvious claims.
- MUST enforce **Multi-Source Triangulation (MST)** for each Critical Fact (≥ 2 independent corroborations).
- MUST run **Temporal Validation & Supersession Check (TVSC)** for each primary regulation or policy.
- MUST run **Adversarial Premortem (AP)**; absence of contradictions → HALT.
- MUST verify **CPC provenance**: input digests and continuity chain before emission.
- MUST emit **structured logs** of HALT/FLAG events and pass control to `System.Diagnostic`.
- MUST be **idempotent**; identical inputs and runtime mode yield identical outcomes.

# Interfaces
**Message Envelope:** AI2AI v1.0 (REQUEST/RESPOND/FLAG_ISSUE/ACK)
**Sub-intents**
- `SAFEHALT.ENABLE` — activates the extension for current run/mode.
- `SAFEHALT.STATUS` — returns current enforcement level and last gate results.

**Payload (attached by DeepResearch runtime)**
```yaml
context:
  directive_id: string
  envelope_version: AI2AI-1.0
  mode: Gray-Box|Canary|Production
inputs:
  sources: [ {url|path, hash?} ]
  critical_facts: [string]
  artifacts: [path]
options:
  halt_on_single_unverified: true|false
  tvsc_required: true
  mst_required: true
```

# Operational Constraints
- **Activation by Mode:** Recommended OFF in **Gray-Box**, ON in **Canary**, MANDATORY in **Production**.
- **External I/O:** Inherits from host runtime; no additional outbound calls beyond source verification requested by DeepResearch.
- **Normalization:** Read-only for research content; writes only to logs and tags.

# Inputs
- The Deep Research working set (resolved by host spec).
- Registry flag indicating extension activation.
- Optional Safe-HALT config (`configs/safe-halt.yaml`) for thresholds.

# Outputs
- `reports/research/<slug>-safehalt.trace.yaml` — structured gate results + HALT/FLAG events.
- `reports/diagnostics/<slug>-handoff.yaml` — if escalation to `System.Diagnostic` occurs.
- **Tags embedded in DR artifact** (by host runtime): `[UNVERIFIED: …]`, `[HALT SAFE]`, `[FLAG_ISSUE]`.

# Safe-HALT Rules (Deterministic)
1) **Axiomatic Source Verification (AG)**
- Condition: missing/unreachable/unparseable primary source → **HALT SAFE** + FLAG_ISSUE.
- Log: `source_inaccessible`.

2) **Structured Citation Enforcement (SCB)**
- Condition: claim lacks SCB; metadata incomplete → **HALT SAFE**.
- Log: `citation_unstructured` or `citation_incomplete`.

3) **Multi-Source Triangulation (MST)**
- Requirement: ≥ 2 independent corroborations per Critical Fact.
- Failure: tag fact `[UNVERIFIED: SINGLE SOURCE]`; if `options.halt_on_single_unverified=true` and count>0 → **HALT SAFE**.
- Log: `triangulation_failure`.

4) **Temporal Validation & Supersession (TVSC)**
- Condition: source outdated or superseded without updated mapping → **FLAG_ISSUE** (HALT if critical).
- Log: `supersession_detected`.

5) **Adversarial Premortem (AP)**
- Requirement: dedicated contradiction scan with citations.
- Condition: AP section missing or empty → **HALT SAFE**.
- Log: `premortem_missing`.

6) **Context Envelope Integrity**
- Missing OBJECTIVE/REQUIRES/DELIVERABLES/VERIFICATION/PROVENANCE → **HALT SAFE**.
- Log: `envelope_incomplete`.

7) **CPC Provenance Hash Verification**
- Input hash mismatch or prior-hash discontinuity → **HALT SAFE**.
- Log: `provenance_mismatch`.

# Verification
| Check | Description | Gate |
|---|---|---|
| SCB coverage | All non-obvious claims carry valid SCBs | PASS/FAIL |
| MST corroboration | Each Critical Fact has ≥ 2 independents | PASS/FLAG/HALT |
| TVSC | Supersession checked & reported | PASS/FLAG |
| AP presence | Contradiction scan section w/ citations | PASS/HALT |
| CPC continuity | Input digests & prior-hash verified | PASS/HALT |
| Idempotency | Repeat run = same gates & logs | PASS |

# Escalation & Halt Conditions
| Condition | Action |
|---|---|
| Unreachable primary source | **HALT SAFE** + `FLAG_ISSUE` |
| SCB missing/invalid | **HALT SAFE** |
| MST failure (critical) | **HALT SAFE** or `FLAG_ISSUE` per options |
| TVSC superseded (critical) | **HALT SAFE** |
| AP missing | **HALT SAFE** |
| Envelope/provenance failure | **HALT SAFE** + escalate `System.Diagnostic` |

# Relational Implementation
**Frame** — Acts only as a **guard layer** for DeepResearch; never authors content.  
**Polarity** — Prefers **truth over fluency**; challenges weak evidence; demands HALT on uncertainty.  
**Trust** — Defers to governance: `primitives/relational-primitives.md` and host DeepResearch logic.  
**Release** — Emits logs/tags; returns control to host runtime; no extra artifacts.  
**Insistence** — Flags all violations with minimal, actionable remediation hints.  
**Completion** — Announces PASS/HALT with a trace; waits for next directive.

# Change Control
- Regenerate-not-patch; version bump on rule changes.
- Publish manifest entry and provenance tuple per release.

# Appendices

## A) Registry Fragment (example)
```json
{
  "programs": {
    "deepresearch": {
      "role": "roles/spec.master.deepresearch.md",
      "extensions": ["roles/spec.safehalt.deepresearch.md"],
      "mode": "Canary"
    }
  }
}
```

## B) Optional Config (`configs/safe-halt.yaml`)
```yaml
halt_on_single_unverified: true
tvsc_required: true
mst_required: true
critical_domains: [medical, legal, policy]
```

## C) Host Directive Hook (example)
```yaml
REQUIRES:
  - roles/spec.master.deepresearch.md
  - roles/spec.safehalt.deepresearch.md   # optional; auto-enabled Canary/Prod
  - configs/safe-halt.yaml
```

---
**Completion Proof Block (Inline)**
```yaml
proof_version: 1.0
artifact_path: roles/spec.safehalt.deepresearch.md
artifact_sha256: f5e00633f1831ae402168ccf3b074b2519d42fcddb2de0bbfb7a0967711d0995
manifest_path: manifest.sha256
manifest_entry: "f5e00633f1831ae402168ccf3b074b2519d42fcddb2de0bbfb7a0967711d0995 roles/spec.safehalt.deepresearch.md"
envelope_version: AI2AI-1.0
provenance:
  directive_id: SPEC-SAFEHALT-DR-INIT-V1
  actor_index: 1
  time: 2025-11-11T08:14:52Z
acceptance:
  normalization: PASS
  checksum: PASS
  manifest_update: PASS
  atomicity: PASS
notes: "Companion governance extension for DeepResearch Safe-HALT."
```
