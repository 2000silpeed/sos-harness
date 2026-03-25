# SOS Fullstack Harness — Detailed Architecture

## Principles for Applying Ontology as a Thinking Model to Development

1. **Domain first**: Define the domain before writing code. Entities/relationships/rules come first; tables/APIs/UI come after
2. **Relationships are key**: FKs, API integrations, component props, events — all are "relationships." Design relationships explicitly
3. **Meta-edge awareness**: Middleware, decorators, interceptors, hooks are "rules about rules." Design them consciously
4. **6-space review**: View code not from a single perspective but across 6 dimensions (hierarchy/temporal/recursive/structural/causal/integrated)
5. **Fractal decomposition**: Recursively decompose large problems into the same structure. How an individual works = how the team works
6. **Generator/Evaluator separation**: Structurally separate generation and evaluation. Eliminate self-evaluation bias
7. **Files are the source of truth**: Artifact files in `_workspace/` — not the context window — are the core medium for information transfer between agents

## GAN-Inspired Architecture

A pattern inspired by Anthropic's [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) blog:

### Role Separation

| GAN Role | Agent | Core Function |
|---------|---------|----------|
| **Planner** | product-owner | 1-4 sentences → comprehensive product spec expansion (What level, excludes How) |
| **Generator** | architect, frontend, backend, devops | Design + implementation (prohibited from evaluating own output) |
| **Evaluator** | qa-engineer | Independent evaluation, quantitative grading rubric, Sprint Contract-based verification |
| **Advisor** | ontology-advisor | Methodology consulting (does not write code) |

### Self-Evaluation Bias Prevention

- Generators do not evaluate their own output as "well done"
- Only the Evaluator (QA) has authority for quantitative grading
- If QA's initial grading scores are all high, raise the bar one level and re-evaluate (leniency prevention)
- All grading must include specific observational evidence

### Sprint Contract (Pre-Implementation Success Criteria Agreement)

Before implementation begins, the Evaluator and Generator agree on success criteria:
- Pass conditions per feature + verification methods
- Minimum design quality scores (each dimension 3/5, average 3.5/5)
- Non-functional requirements (performance, accessibility, responsiveness)
- Artifact: `_workspace/03.5_sprint_contract.md`

### Quantitative Grading Rubric

Grading on a 5-point scale. PASS conditions: all dimensions >= 3/5, average >= 3.5/5, zero items.
On FAIL: specific remediation instructions → re-implementation → re-grading (safety limit of 3 rounds max).

## Context Reset Protocol

Two failure modes that occur in long-running sessions:

1. **Context consistency loss**: As the context window fills, outputs begin contradicting initial instructions
2. **Context Anxiety**: The model recognizes its context limit and prematurely wraps up work

**Solution: Reset + file-based handoff over Compaction**

- Save artifacts to `_workspace/` upon each Phase completion
- The next Phase can proceed by reading files alone (self-contained artifacts)
- When context becomes overloaded, reset and restart via file-based handoff instead of compacting

## Agent Team Composition

| Agent | File | Role | GAN Role | SOS Lens |
|---------|------|------|---------|---------|
| product-owner | `agents/product-owner.md` | Business/market viability, spec expansion | Planner | C04(AIP), C10(Semantic Enrichment) |
| architect | `agents/architect.md` | Domain modeling, architecture, DB/API design | Generator | C02(Ontology), C09(Domain Ontology) |
| frontend-dev | `agents/frontend-dev.md` | React/Next.js UI + design quality | Generator | C06(Hierarchy Space), C15(Active Metadata) |
| backend-dev | `agents/backend-dev.md` | API, DB, auth, business logic | Generator | C07(ReBAC), C03(Meta-edge) |
| qa-engineer | `agents/qa-engineer.md` | Quantitative grading, 6-space review, NOMIK | Evaluator | C11(NOMIK), C06(6 Analysis Spaces) |
| devops-engineer | `agents/devops-engineer.md` | CI/CD, infrastructure, deployment, monitoring | Generator | C13(Lever 5-property), C15(Active Metadata) |
| ontology-advisor | `agents/ontology-advisor.md` | SOS methodology consulting, design review | Advisor | All SOS concepts |

## Team Communication Protocol

Agents communicate directly via SendMessage:
- **product-owner** → architect: Delivers business requirements, expanded product spec, priorities
- **architect** on completion → frontend receives component structure/routing, backend receives API/DB/auth, qa receives functional requirements, devops receives infrastructure requirements
- **qa** ↔ **all developers**: Sprint Contract negotiation (before implementation)
- **frontend ↔ backend**: Real-time communication during API integration
- **qa** → respective developer: Grading-based mandatory fix requests → rework → re-grading (until threshold is passed, 3 rounds max)
- **ontology-advisor** → all agents: Proposes SOS perspective on design decisions
- **devops** on completion → all: Shares environment variables, deployment URLs

## Workflow

### Phase 1: Preparation (performed directly by orchestrator)
1. Extract app description, tech stack, scale, existing code, deployment platform from user input
2. Save to `_workspace/00_input.md`
3. Determine execution mode

### Phase 2: Business Analysis + Domain Modeling (sequential)
| Order | Task | Owner | Dependency | Artifact |
|------|------|------|------|--------|
| 1 | Spec expansion + market/business viability analysis | product-owner (Planner) | None | `01_market_analysis.md` |
| 2 | Domain modeling | architect (+ ontology-advisor) | Task 1 | `02_domain_model.md` |
| 3 | Architecture/API/DB design | architect | Task 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

### Phase 2.5: Sprint Contract Negotiation (NEW)
| Order | Task | Owner | Dependency | Artifact |
|------|------|------|------|--------|
| 3.5 | Pre-implementation success criteria agreement | qa ↔ all developers | Task 3 | `03.5_sprint_contract.md` |

### Phase 3: Implementation (parallel)
| Order | Task | Owner | Dependency | Artifact |
|------|------|------|------|--------|
| 4a | Frontend development | frontend-dev | Task 3, 3.5 | `src/` frontend code |
| 4b | Backend development | backend-dev | Task 3, 3.5 | `src/` backend code |
| 4c | Deployment setup | devops-engineer | Task 3, 3.5 | `07_deploy_guide.md`, CI/CD config |

### Phase 4: Grading-Based Verification (Generator/Evaluator loop)
| Order | Task | Owner | Dependency | Artifact |
|------|------|------|------|--------|
| 5 | Sprint Contract-based quantitative grading + 6-space review | qa-engineer | 4a, 4b | `06_test_plan.md`, `08_six_space_review.md`, `10_grade_report.md` |
| 5.1 | (On FAIL) Fix → re-implement → re-grade | qa ↔ developers | 5 | Updated code + grading |
| 6 | Final review | product-owner + ontology-advisor | 5 (after PASS) | `09_review_report.md` |

## Execution Modes by Task Scale

| User Request | Execution Mode | Deployed Agents | Sprint Contract |
|------------|----------|-------------|----------------|
| "Build me a web app", "Develop a SaaS" | **Full pipeline** | All 7 agents | Required |
| "Build just the API" | **Backend mode** | product-owner + architect + backend + qa | Required |
| "Build just the frontend" | **Frontend mode** | architect + frontend + qa | Required |
| "Refactor this code" | **Refactoring mode** | architect + relevant developer + qa | Optional |
| "Just set up deployment" | **DevOps mode** | devops only | Not needed |
| "Review business viability" | **Planning mode** | product-owner only | Not needed |
| "Do domain modeling" | **Modeling mode** | architect + ontology-advisor | Not needed |
| "Review this code" | **Review mode** | qa + ontology-advisor | Not needed |
| "Do impact analysis" | **Analysis mode** | qa only (NOMIK) | Not needed |

## Error Handling

| Error Type | Strategy |
|----------|------|
| Ambiguous requirements | Semantic enrichment (C10) 3-stage expansion: lexical → semantic → ontology alignment |
| Tech stack unspecified | Default stack by scale (MVP: Next.js + SQLite) |
| Build error | Analyze error logs → relevant developer fixes → QA re-grading |
| Agent failure | 1 retry → if still failed, proceed without that artifact |
| Grading FAIL | Specific remediation instructions → rework → re-grading (3 rounds max) |
| FAIL after 3 rounds | Document current state + unresolved issues in review report |
| Business viability doubt | product-owner proposes pivot, presents 3 alternative directions |
| Context overload | Context Reset: file-based handoff then reset |
| Self-Eval Bias | Independent Evaluator verification, Generator self-evaluation rejected |

## Model Optimization (Opus 4.6)

Opus 4.6 provides more deliberate planning, sustained long-running agentic work, and stability across large codebases.

- Sprint over-fragmentation unnecessary — the model formulates its own plan
- Evaluator evaluates at phase completion rather than per-Sprint
- Harness complexity is invested only where the model falls short: self-evaluation bias prevention, design quality grading

## Design References

- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — Anthropic Engineering
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Anthropic Research
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI slop prevention design
- [Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — Context Reset pattern
