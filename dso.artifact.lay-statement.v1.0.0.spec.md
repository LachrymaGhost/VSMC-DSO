---
role: DSO.Artifact.LayStatement (L3/L4 Kit)
actor: AI
version: 1.0.0
maintained_by: DSO Program Team • Scotty/Architect
domain_tags: [lay-statement, buddy-statement, schema, template, evidence, veterans]
status: draft
license: Apache-2.0
no_execution_pledge: true
lineage:
  - DSO.Veteran.Mainframe (L0)
  - DSO.Knowledge.Legal (L1)
  - DSO.Strategy.Claims (L2)
  - DSO.Functions.Artifacts (L3)
  - DSO.Formatting.Templates (L4)
---

# Purpose
Provide deterministic data contracts (L3) and canonical templates (L4) to generate high-quality Veteran and Buddy lay statements that are credible, clear, and compliant.

# Scope
**Covers**
- L3 JSON schemas for Veteran Lay Statement, Buddy Lay Statement, and PromptPlan inputs.
- L4 Markdown templates with phrasing scaffolds, redaction, and provenance footer.
- Quality gates: credibility, scope discipline, readability, and redaction logging.

**Does Not Cover**
- Legal/medical conclusions (forbidden in lay content).
- Strategy choice (when/why to use) — governed by L2.
- Knowledge text storage — governed by L1.

# Normative Requirements
- MUST adhere to separation of concerns: L3 = schemas; L4 = presentation.
- MUST forbid medical causation assertions; use observation-only phrasing.
- MUST include an unsworn declaration block (28 U.S.C. §1746).
- MUST implement redaction of SSN/DOB and log redactions.
- MUST pass L0 Anchor Conference (Spock, Bones, Uhura) prior to release.

---

## L2 — Strategy Hooks (for reference)
- **Intent mapping:** `intent = 'lay_statement'` → select LayStatement (or BuddyStatement) schema.
- **Triggers:** Evidence Gap Matrix shows needs in (a) continuity, (b) functional impact, (c) onset timeline corroboration.
- **HALTs:**  
  - `HALT_CONFLICT`: Timeline conflicts with verified records.  
  - `HALT_SCOPEDISC`: Medical etiology assertions detected.  
  - `MISSING_KNOWLEDGE`: Required definition missing in L1 compendium.

---

## L4 — Canonical Templates
### A. Veteran Lay Statement (Markdown)
```markdown
# Veteran Lay Statement

**Claimant:** <claimant_name>  
**Author:** <author_name> (Veteran)  
**Conditions Addressed:** <comma-separated list>  
**Date:** <MM/DD/YYYY>

## Purpose
This statement provides my firsthand observations about my symptoms and how they affect my daily life, work, and relationships.

## Timeline (Key Events)
- <MM/YYYY> — <event; location (optional)>
- <MM/YYYY> — <event>

## Observations & Functional Impact
For each symptom, I explain how often it occurs (frequency), how bad it is (severity), how long it lasts (duration), what I was doing (context), and how it limits me (impact).

- **Symptom:** <symptom>  
  - Frequency/Severity/Duration: <frequency> / <severity> / <duration>  
  - Context: <activity or situation>  
  - Functional Impact: <limitations in work/daily living/social>  
  - Mitigation/Adaptation: <what I do to cope>

<repeat as needed>

## Continuity
Since <approx. date>, these problems have been present and recurring as described above.

## Closing
I am describing what I personally experience and observe. I am not offering medical opinions.

### Unsworn Declaration (28 U.S.C. §1746)
I declare under penalty of perjury that the foregoing is true and correct.  
Executed on <MM/DD/YYYY>.

**Signature:** <signed_name>
```

### B. Buddy Statement (Markdown)
```markdown
# Buddy Statement

**Claimant:** <claimant_name>  
**Author:** <author_name> (<relationship_to_claimant>)  
**Basis of Knowledge:** <how I know the claimant; how often I see them>  
**Date:** <MM/DD/YYYY>

## Purpose
This statement explains what I have personally observed about the claimant’s symptoms and limitations.

## Observations (Firsthand)
- **What I saw:** <specific behaviors or limitations>  
- **How often:** <frequency>  
- **How severe/for how long:** <severity/duration>  
- **Context:** <work/home/social setting>  
- **Effect on function:** <what they could/couldn’t do>

## Continuity/Changes Over Time
From <approx. date> to present, I have seen <continuity or progression>.

### Unsworn Declaration (28 U.S.C. §1746)
I declare under penalty of perjury that the foregoing is true and correct.  
Executed on <MM/DD/YYYY>.

**Signature:** <signed_name>
```

---

## Registration (L0 & L2)
- **L2 Artifact Selection:** `intent='lay_statement'` → `LayStatement` (or `BuddyStatement`) schema.  
- **L0 Halt Registry additions:**  
  - `HALT_SCOPEDISC` — Medical opinion phrasing detected in lay text.  
  - `HALT_TIMELINE_CONFLICT` — Timeline conflicts with verified records.
---
