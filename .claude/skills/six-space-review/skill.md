---
name: six-space-review
description: "6-space code review. Analyzes code across 6 dimensions: hierarchy / temporal / recursive / structural / causal / cross-space. Triggered by: 'code review', 'code analysis', '6-space review', 'code quality inspection', 'multi-dimensional review', 'structural review'."
---

# Six-Space Review — 6-Space Code Review

Review code across 6 independent analysis dimensions. Discovers structural, temporal, and causal issues that conventional code reviews miss.

## 6 Analysis Spaces

### 1. Hierarchy Space
**Key question**: "Is responsibility at the correct level?"
- Are components/modules positioned in the correct layer?
- Does the upper module avoid depending on lower-level implementation? (dependency inversion)
- Is the abstraction level consistent?
- **Warning**: Cross-level conclusion transfer error (uncritically passing upper-layer conclusions to lower layers)

### 2. Temporal Space
**Key question**: "Is the time ordering correct?"
- Is state initialization/cleanup timing appropriate?
- Are there potential race conditions?
- Are event ordering guarantees in place where needed?
- What are the timeout/retry strategies?
- **Pattern**: Lifecycle analysis (creation → active → inactive → destruction)

### 3. Recursive Space
**Key question**: "Is this a reusable pattern?"
- Are patterns repeated 3+ times abstracted?
- But is it premature abstraction? (copy-paste OK until 3 repetitions)
- Is the structure composable?
- **Warning**: Fractal self-similarity violation (mismatch between part and whole structure)

### 4. Structural Space
**Key question**: "Are dependencies healthy?"
- No circular references?
- Is coupling between modules appropriate?
- Is the blast radius of changes limited?
- Does the code structure match the domain model (ontology)?
- **Tools**: `import` analysis, directory structure review

### 5. Causal Space
**Key question**: "What happens when it fails?"
- Is error handling adequate?
- What is the propagation path of error A → cascade B → C?
- Is recovery possible? What is the rollback strategy?
- Is data consistency guaranteed?
- **Pattern**: Impact Analysis ("if I change this, what is affected?")

### 6. Cross-Space (Integration)
**Key question**: "Is there overall consistency?"
- Synthesize analyses from the above 5 spaces
- Are the domain model's classes/relations/axioms faithfully reflected in code?
- Identify technical debt
- Overall assessment and improvement priorities

## Output Format — `_workspace/08_six_space_review.md`

Per space: Observations → Issues → Severity (🔴🟡🟢) → Recommended fixes
