---
name: semantic-requirements
description: "Requirements semantic enrichment. Transforms ambiguous user requirements into precise specs through 3 stages: lexical expansion → semantic layering → ontology alignment. Triggered by: 'requirements analysis', 'write specs', 'organize requirements', 'what should I build', 'clarify requirements', 'spec refinement'."
---

# Semantic Requirements — Requirements Semantic Enrichment

Refine ambiguous requirements through 3 stages using the SOS C10 (vector semantic enrichment) thinking model.

## Problem

User requirements are structurally incomplete:
- "How do I set up permissions?" → Permissions for what? What level? Which model?
- "Build me a dashboard" → For whom? What data? What charts?

## 3-Stage Semantic Enrichment

### Stage 1: Lexical Expansion
- List synonyms, near-synonyms, and related terms
- Reference similar products/services
- **Example**: "permissions" → authentication, authorization, ACL, RBAC, access control, grants

### Stage 2: Semantic Layering
- Construct an abstract → concrete spectrum
- **Example**:
  - Abstract: "security system"
  - Intermediate: "access control model"
  - Concrete: "ReBAC-based relation-path permissions + Supabase RLS policies"

### Stage 3: Ontology Alignment
- Anchor to domain terminology to prevent over-expansion
- Map to domain ontology classes/relations
- **Example**: Final spec = "ReBAC-based role-relation permission configuration, applied at DB level via Supabase RLS policies"

## Output Format

```
# Semantic Enrichment Report

## Original Requirements
[User's original text]

## Stage 1: Lexical Expansion
| Original Term | Expanded Terms | Similar Products/Services |
|--------------|---------------|--------------------------|

## Stage 2: Semantic Layering
| Level | Description | Implementation Level |
|-------|------------|---------------------|
| Abstract | [...] | Strategy |
| Intermediate | [...] | Design |
| Concrete | [...] | Implementation |

## Stage 3: Ontology Alignment
- **Aligned domain terms**: [...]
- **Related entities**: [...]
- **Related relations**: [...]

## Refined Requirements
[Final spec - concrete and actionable form]

## Acceptance Criteria
- [ ] [AC1]
- [ ] [AC2]
- [ ] [AC3]
```
