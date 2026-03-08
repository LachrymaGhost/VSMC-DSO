---
role: DSO.Functions.Artifacts (Layer 3 Process)
actor: AI
version: 1.1.1 (Lay-Statement $ref Linkage)
maintained_by: DSO Program Team • Scotty/Architect
domain_tags: [functions, process, schema, artifacts, L3]
status: stable
license: Apache-2.0
no_execution_pledge: true
lineage:
  - SMC DSO Project AAR (Schema Rule)
  - DSO.Veteran.Mainframe (L0 Orchestrator)
  - SGP Architectural Playbook (v1.0.0)
  - DSO.Artifact.LayStatement (v1.0.0)
---

# Purpose
Define the **Internal Artifact Schemas (Data Contracts)** for all V-DSO outputs. Ensure fixed, auditable targets for L2-generated data.

# Scope
**Covers:** Master VFB, ParsedDocumentAnalysis, Nexus Analysis, Rating Rationale, Evidence Gap Matrix, Eligibility Matrix.  
**Does Not Cover:** Algorithms (L2) or templates (L4).

# Normative Requirements
- Define a schema for every cross-layer data structure.  
- Align with L2 Artifact Selection Engine.  
- Use JSON Schema draft 2020-12.  
- Enforce Master VFB presence in evidence-bearing artifacts.

# Schemas (summary)
- `urn:aire:dso:master-vfb:1-1-0`
- `urn:aire:dso:parsed-doc-analysis:1-1-0`
- `urn:aire:dso:nexus-analysis:1-1-0`
- `urn:aire:dso:rating-rationale:1-1-0`
- `urn:aire:dso:evidence-gap-matrix:1-1-0`
- `urn:aire:dso:eligibility-matrix:1-1-0`
- **Lay/Buddy Statements (external references):**  
  - `$ref: urn:aire:dso:lay-statement:1-0-0`  
  - `$ref: urn:aire:dso:buddy-statement:1-0-0`  
  - `$ref: urn:aire:dso:lay-statement-prompt:1-0-0`

# Interface Boundary
- L3 is schema-only. Canonical Markdown templates live in L4.  
- Any new L2 artifact requires a schema to be registered here first (HALT: SCHEMA_VIOLATION if missing).

# Relational Implementation
- **Frame:** data definition service; no insertion/interpretation.  
- **Release:** only emit schemas; no templates.  
- **Insistence:** flag undefined-schema requests to L0.