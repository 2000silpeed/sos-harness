---
name: domain-modeling
description: "Ontology 4-element based domain modeling. Decomposes a business domain into classes (entities) / properties (fields) / relations (FK, API) / axioms (business rules) for structured design. Triggered by: 'domain modeling', 'entity design', 'data model', 'business rules definition', 'ontology model', 'define entities'."
---

# Domain Modeling — Ontology-Based Domain Modeling

Decompose a business domain into ontology 4 elements to build the foundation for code structure.

## Ontology 4 Elements → Code Mapping

| Ontology | Code | Example |
|----------|------|---------|
| Class | Entity, table, type | `User`, `Order`, `Product` |
| Property | Column, field, props | `user.email`, `order.total` |
| Relation | FK, API integration, import, event | `User hasMany Orders` |
| Axiom | Business rule, constraint, validation | "Only VIP members can receive discounts" |

## 5-Step Domain Modeling Process

### Step 1: Scope Definition
- Set scope based on concrete workflows
- List "actions users actually perform"
- Reference product-owner's feature priorities

### Step 2: Data Collection
- Identify core entities and their relations
- **Collect exceptions first** — exceptions reveal domain rules more than normal flows
- Create domain terminology glossary

### Step 3: Structure with 4 Elements
- Class list + properties for each class
- Relation matrix (which classes connect via which relations)
- Axiom list (constraints, business rules)
- **70% completeness is OK** — do not pursue perfection

### Step 4: Meta-Edge Identification
- Discover "rules about rules" in the domain
- Example: "All order-related APIs require authentication" (auth = meta-edge)
- Example: "All data mutations must be audit-logged" (audit = meta-edge)

### Step 5: Validation
- Verify 80%+ of 100 user scenarios can be handled
- Confirm no contradicting relations/axioms exist
- Confirm domain expert (or product-owner) can understand immediately

## Output Format — `_workspace/02_domain_model.md`

```
# Ontology-Based Domain Model

## Domain Overview
[Business domain description]

## Domain Terminology Glossary
| Term | Definition | Code Name |
|------|-----------|-----------|

## Classes (Entities)
| Class | Description | Key Properties | Prisma Model |
|-------|------------|----------------|-------------|

## Relations (Edges)
| Subject | Relation | Object | Cardinality | FK/Implementation |
|---------|----------|--------|------------|-------------------|

## Axioms (Business Rules)
| # | Rule | Related Classes | Implementation Location |
|---|------|----------------|------------------------|
| A1 | [Rule] | [Classes] | [Service/Middleware/DB constraint] |

## Meta-Edges (Rules About Rules)
| Meta-Edge | Scope of Impact | Implementation |
|-----------|----------------|----------------|
| Authentication | All API relations | auth middleware |
| Audit log | All CUD relations | audit interceptor |

## Relation Diagram
[mermaid ERD]
```
