# SOS Fullstack Development Harness

A harness for fullstack development driven by ontology as a thinking model. Applies all 35 SOS (Study Ontology System) concepts as a **development methodology**, and uses a GAN-inspired Generator/Evaluator architecture where an agent team collaboratively executes requirements → design → Sprint Contract → frontend → backend → grading-based verification → deployment.

## Core Philosophy

> Ontology is not something you build — it is a **thinking model**.

At every development stage, ask: "What are the entities, what are the relationships, and what are the rules?" This is the shift from probabilistic coding (coding by intuition) to structural coding (coding by relationships).

## Design References

- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — GAN pattern, Context Reset, Sprint Contract
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Agent orchestration
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI slop prevention design

## Structure

```
.claude/
├── agents/
│   ├── product-owner.md         — Planner: Business viability assessment, spec expansion
│   ├── architect.md             — Generator: Ontology-based domain modeling
│   ├── frontend-dev.md          — Generator: UI + design quality (AI slop prevention)
│   ├── backend-dev.md           — Generator: ReBAC auth, meta-edge middleware
│   ├── qa-engineer.md           — Evaluator: Quantitative grading, 6-space review, NOMIK
│   ├── devops-engineer.md       — Generator: Lever 5-property CI/CD
│   └── ontology-advisor.md      — Advisor: SOS methodology consulting
├── skills/
│   ├── sos-fullstack/skill.md   — Orchestrator (GAN loop, Sprint Contract)
│   ├── domain-modeling/skill.md — Domain modeling
│   ├── six-space-review/skill.md — 6-space code review
│   ├── impact-analysis/skill.md — NOMIK impact analysis
│   └── semantic-requirements/skill.md — Requirements semantic enrichment
└── CLAUDE.md                    — Detailed architecture
```

## v2 Improvements (2026-03-26)

| Improvement | Source | Effect |
|------|------|------|
| **GAN Generator/Evaluator separation** | Anthropic Blog | Eliminates self-evaluation bias, independent quality assurance |
| **Sprint Contract** | Anthropic Blog | Pre-implementation success criteria agreement → prevents expectation mismatch |
| **Quantitative grading rubric** | Anthropic Blog | Subjective 🔴/🟡/🟢 → 5-point scale + pass threshold |
| **Context Reset protocol** | Anthropic Blog | File-based handoff maintains consistency across long sessions |
| **AI slop prevention design** | Frontend Skill | Rejects generic patterns such as generic fonts/purple gradients |
| **Playwright MCP live testing** | Anthropic Blog | Real browser-based UI/API verification |
| **Enhanced Planner role** | Anthropic Blog | 1-4 sentences → comprehensive product spec expansion |
| **Opus 4.6 optimization** | Anthropic Blog | Eliminates Sprint over-fragmentation, evaluates at phase completion |

## Applying SOS Concepts to Development

| SOS Concept | Meaning in Development | Applied Agent |
|----------|---------------|-------------|
| C02 Ontology (온톨로지) | Domain model = classes/properties/relationships/axioms | architect |
| C06 6 Analysis Spaces (6분석공간) | Code review in 6 dimensions (hierarchy/temporal/recursive/structural/causal/integrated) | qa-engineer |
| C07 ReBAC | Relationship-based authentication/authorization design | backend-dev |
| C03 Meta-edge (메타엣지) | Middleware, decorators, interceptors = "rules about rules" | backend-dev |
| C11 NOMIK | "If I change this code, what breaks?" — impact analysis | qa-engineer |
| C10 Vector Semantic Enrichment (벡터의미강화) | Ambiguous requirements → precise spec expansion | product-owner |
| C13 Lever/Meta-lever (레버/메타레버) | CI/CD 5 properties: composability/observability/idempotency/recoverability/version control | devops-engineer |
| C14 Physics Computation Engine (물리연산엔진) | Fractal decomposition: recursively decompose large tasks in parallel | All |
| C15 Active Metadata (능동메타데이터) | UI that adapts in real-time based on user context | frontend-dev |
| C04 AIP/Apollo | Product design following the text → structure → action pattern | product-owner |

## Usage

Trigger the `/sos-fullstack` skill, or make a development request in natural language.

## Artifacts

All artifacts are generated in `_workspace/`:
- `_workspace/00_input.md` — Organized user input
- `_workspace/01_market_analysis.md` — Market/business viability analysis + expanded spec (PO/Planner)
- `_workspace/02_domain_model.md` — Ontology-based domain model (architect)
- `_workspace/03_architecture.md` — System architecture (architect)
- `_workspace/03.5_sprint_contract.md` — Sprint Contract: success criteria agreement (qa ↔ developers)
- `_workspace/04_api_spec.md` — API specification (architect)
- `_workspace/05_db_schema.md` — DB schema (architect)
- `_workspace/06_test_plan.md` — Test plan (qa)
- `_workspace/07_deploy_guide.md` — Deployment guide (devops)
- `_workspace/08_six_space_review.md` — 6-space code review (qa)
- `_workspace/09_review_report.md` — Final review report
- `_workspace/10_grade_report.md` — Quantitative grading report (qa/Evaluator)
- `src/` — Source code

## Ontology Methodology Reference

Detailed definitions of all 35 SOS concepts are in the `ontology/` directory:
- `ontology/sos-graph.json` — Complete concept graph
- `ontology/concepts/{tier}/{ID}.json` — Individual concept details
- `ontology/edges.json` — Inter-concept relationships
- `ontology/meta-edges.json` — Meta-edge rules
