---
name: impact-analysis
description: "NOMIK-style code impact analysis. Structurally analyzes how far a code change's effects propagate. Triggered by: 'impact analysis', 'what breaks if I change this', 'change impact', 'pre-refactoring analysis', 'dependency analysis', 'blast radius'."
---

# Impact Analysis — NOMIK Impact Analysis

Structurally analyze the ripple effects of code changes. Instead of sifting through 47 files, precisely analyze only the connected nodes in the relation graph.

## NOMIK Thinking Model (C11)

View code as a knowledge graph:
- **Nodes**: Files, functions, classes, components, API endpoints, DB tables
- **Edges**: imports, function calls, API integrations, FK references, event subscriptions, props passing

## 3-Step Analysis

### Step 1: SCAN — Identify Impact Scope
1. Identify the target code (node) being changed
2. Explore directly connected nodes (1-hop):
   - Where this file is imported
   - Where this function is called
   - Which frontend uses this API
   - Which queries reference this table
3. Explore indirect connections (2-hop): where directly affected nodes propagate impact

### Step 2: STORE — Relation Mapping
| Change Target | Relation Type | Affected Code | Hop | Impact Severity |
|--------------|---------------|---------------|-----|-----------------|
| [function/file] | [import/call/API/FK] | [code] | [1/2] | [🔴🟡🟢] |

### Step 3: QUERY — Risk Assessment
- **🔴 Breaking**: Type/interface change, deletion, required parameter change
- **🟡 Warning**: Behavior change, performance impact, side effects
- **🟢 Safe**: Internal implementation only, interface unchanged

## Key Question

> "If I change this symbol (function/class/API), what breaks?"

This is why NOMIK outperforms traditional RAG: instead of 47 noisy files, it precisely analyzes only 6 relevant relation nodes.

## Output Format

```
# Impact Analysis Report

## Change Target
[Code being changed and description of the change]

## Impact Graph
[Relation tree starting from the change target]

## Affected Code List
| # | File:Line | Relation | Hop | Severity | Required Action |
|---|-----------|----------|-----|----------|-----------------|

## Recommended Tests
[List of recommended test executions for affected areas]

## Risk Summary
- 🔴 Breaking: [count]
- 🟡 Warning: [count]
- 🟢 Safe: [count]
```
