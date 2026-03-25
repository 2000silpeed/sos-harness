---
name: sos-fullstack
description: "Ontology-driven fullstack development pipeline. A GAN-inspired Generator/Evaluator architecture where an agent team collaboratively performs business analysis → domain modeling → design → Sprint Contract → frontend → backend → grading-based verification → deployment. Use this skill for: 'build a web app', 'SaaS development', 'CRUD app', 'dashboard', 'admin panel', 'auth system', 'REST API', 'fullstack project', 'Next.js app', 'service planning', and general web application development. Out of scope: mobile apps (React Native/Flutter), games, ML/AI model training."
---

# SOS Fullstack — Ontology-Driven Fullstack Development

An agent team collaboratively performs business analysis → domain → design → Sprint Contract → implementation → grading-based verification → deployment using ontology methodology.

## Key Differentiators

Differences from a generic fullstack harness:
- **Domain model first**: Define ontology 4 elements (classes/properties/relations/axioms) before ERD/API
- **Relation-based design**: All connections (FK, API, component props) are explicitly designed as "relations"
- **Meta-edge awareness**: Middleware/interceptors are documented as "rules about rules"
- **GAN-inspired Generator/Evaluator**: Complete separation of developers (Generator) and QA (Evaluator), quality assurance via quantitative grading rubric
- **Sprint Contract**: Pre-implementation agreement on success criteria → prevents expectation mismatch
- **6-space review**: Multi-dimensional code verification across 6 dimensions
- **Business viability validation**: Market/profitability assessment before technical work
- **Context Reset**: Structured handoff for context consistency in long-running sessions

## Design References

This harness architecture is inspired by:
- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — GAN pattern, Context Reset, Sprint Contract
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Agent orchestration patterns
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI slop prevention design guide

## Execution Mode

**Agent Team** — 7 agents communicate directly via SendMessage with cross-verification.

**Role Separation (GAN Pattern)**:
- **Planner**: product-owner (expands 1-4 sentences → comprehensive product spec)
- **Generator**: architect, frontend-dev, backend-dev, devops-engineer (design + implementation)
- **Evaluator**: qa-engineer (independent evaluation, quantitative grading)
- **Advisor**: ontology-advisor (methodology consulting, does not write code)

## Agent Configuration

| Agent | File | Role | GAN Role |
|-------|------|------|----------|
| product-owner | `.claude/agents/product-owner.md` | Business viability, market analysis, GTM | Planner |
| architect | `.claude/agents/architect.md` | Ontology domain modeling, architecture | Generator |
| frontend-dev | `.claude/agents/frontend-dev.md` | React/Next.js frontend + design quality | Generator |
| backend-dev | `.claude/agents/backend-dev.md` | API, DB, ReBAC auth | Generator |
| qa-engineer | `.claude/agents/qa-engineer.md` | Quantitative grading, 6-space review, NOMIK | Evaluator |
| devops-engineer | `.claude/agents/devops-engineer.md` | Lever 5-property CI/CD | Generator |
| ontology-advisor | `.claude/agents/ontology-advisor.md` | SOS methodology consulting | Advisor |

## Workflow

### Phase 1: Preparation (Performed directly by orchestrator)

1. Extract from user input:
   - **App description**: What to build
   - **Tech stack** (optional): Preferred frameworks
   - **Scale** (optional): MVP/small/medium/large
   - **Existing code** (optional): Existing project to extend
   - **Deployment platform** (optional): Vercel/AWS/Docker etc.
2. Create `_workspace/` directory
3. Save organized input to `_workspace/00_input.md`
4. If existing code present, analyze and adjust phases
5. Determine execution mode

### Phase 2: Business Analysis + Domain Modeling

| Order | Task | Owner | Depends On | Artifact |
|-------|------|-------|------------|----------|
| 1 | User input → comprehensive product spec expansion + market/business analysis | product-owner (Planner) | None | `01_market_analysis.md` |
| 2 | Domain modeling + review | architect + ontology-advisor | Task 1 | `02_domain_model.md` |
| 3 | Architecture/API/DB design | architect | Task 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

**Enhanced Planner Role**: The product-owner expands the user's 1-4 sentence input into a comprehensive product spec. However, it excludes implementation details and focuses on "What" level only, preventing cascading errors.

**ontology-advisor** reviews the architect's domain model in Task 2.

### Phase 2.5: Sprint Contract Negotiation (NEW)

| Order | Task | Owner | Depends On | Artifact |
|-------|------|-------|------------|----------|
| 3.5 | Sprint Contract agreement | qa-engineer ↔ all developers | Task 3 | `_workspace/03.5_sprint_contract.md` |

Based on the architect's design documents, the QA (Evaluator) proposes **success criteria** to each Generator:

```
## Sprint Contract — _workspace/03.5_sprint_contract.md

### Frontend Success Criteria
| # | Requirement | Verification Method | Pass Condition |
|---|-------------|---------------------|----------------|

### Backend Success Criteria
| # | Requirement | Verification Method | Pass Condition |
|---|-------------|---------------------|----------------|

### Design Quality Criteria
- Minimum 3/5 per dimension, average 3.5/5

### DevOps Success Criteria
| # | Requirement | Verification Method | Pass Condition |
|---|-------------|---------------------|----------------|
```

Generators can agree to the Contract or request modifications. **Implementation begins after agreement**.

### Phase 3: Implementation (Parallel)

| Order | Task | Owner | Depends On | Artifact |
|-------|------|-------|------------|----------|
| 4a | Frontend development | frontend-dev | Tasks 3, 3.5 | `src/` frontend code |
| 4b | Backend development | backend-dev | Tasks 3, 3.5 | `src/` backend code |
| 4c | Deployment setup | devops-engineer | Tasks 3, 3.5 | `07_deploy_guide.md`, CI/CD config |

Tasks 4a, 4b, 4c run **in parallel**. All depend on Task 3 and Sprint Contract (3.5).

**Communication flow:**
- architect complete → component/routing to frontend, API/DB/auth to backend, infra to devops, requirements to qa
- frontend ↔ backend: real-time communication during API integration
- devops complete → share env vars/deployment URL with all

**Generator self-evaluation prohibited**: Developers do not judge "it went well" on their own. Upon completion, they only submit to QA.

### Phase 4: Grading-Based Verification (Generator/Evaluator Loop)

| Order | Task | Owner | Depends On | Artifact |
|-------|------|-------|------------|----------|
| 5 | Sprint Contract-based quantitative grading + 6-space review | qa-engineer (Evaluator) | 4a, 4b | `06_test_plan.md`, `08_six_space_review.md`, `_workspace/10_grade_report.md` |
| 5.1 | (On FAIL) Revision request → re-implementation → re-grading | qa ↔ relevant developer | 5 | Updated code + grading report |
| 6 | Final review | product-owner | 5 (after PASS) | `09_review_report.md` |

**Grading loop details:**
1. QA grades each dimension 1-5 based on Sprint Contract criteria
2. **PASS condition**: All dimensions >= 3/5, average >= 3.5/5, zero 🔴 items
3. **On FAIL**: Specific revision instructions → Generator rework → QA re-grading
4. **Safety limit**: Maximum 3 rounds. If still FAIL after 3 rounds, proceed with current state but document unresolved issues in review report
5. **Leniency prevention**: QA must provide specific observational evidence for all grades. If all items score 4-5 in round 1, raise the bar one level and re-evaluate

**Playwright MCP Live Testing (when available):**
- QA verifies UI/API/responsiveness in real browser via Playwright MCP
- Screenshot-based visual quality confirmation
- Falls back to code review + build verification in unavailable environments

### Phase 5: Final Report

1. Verify all artifacts
2. Confirm all 🔴 mandatory fixes are applied
3. Present final summary to user:
   - Market analysis — `_workspace/01_market_analysis.md`
   - Domain model — `_workspace/02_domain_model.md`
   - Architecture — `_workspace/03_architecture.md`
   - Sprint Contract — `_workspace/03.5_sprint_contract.md`
   - API spec — `_workspace/04_api_spec.md`
   - DB schema — `_workspace/05_db_schema.md`
   - Test plan — `_workspace/06_test_plan.md`
   - Deployment guide — `_workspace/07_deploy_guide.md`
   - 6-space review — `_workspace/08_six_space_review.md`
   - Final review — `_workspace/09_review_report.md`
   - Grading report — `_workspace/10_grade_report.md`
   - Source code — `src/`

## Context Reset Protocol

In long-running sessions, as the context window fills up, the model loses consistency or exhibits "Context Anxiety" — attempting to finish work prematurely.

**Resolution Strategy: File-Based Structured Handoff**

1. **Handoff files are the source of truth**: `_workspace/` artifacts are the core of inter-agent information transfer. Not message context
2. **Handoff timing**: At each Phase completion. Previous Phase artifacts become the next Phase's input
3. **Reset over compaction**: When context grows large, a full reset + file-based restart is more stable than compaction
4. **Agent independence**: Each agent's artifacts must be self-contained so it can work by reading only its input files

### Per-Phase Input File Mapping (for restart after Context Reset)

| Phase | Agent | Files to Read |
|-------|-------|---------------|
| 2 | product-owner | `00_input.md` |
| 2 | architect | `00_input.md`, `01_market_analysis.md` |
| 2.5 | qa-engineer | `03_architecture.md`, `04_api_spec.md` |
| 3 | frontend-dev | `03_architecture.md`, `03.5_sprint_contract.md` |
| 3 | backend-dev | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md`, `03.5_sprint_contract.md` |
| 3 | devops-engineer | `03_architecture.md`, `03.5_sprint_contract.md` |
| 4 | qa-engineer | `03.5_sprint_contract.md`, `src/` code, `03_architecture.md` |
| 5 | product-owner | `01_market_analysis.md`, `10_grade_report.md`, `08_six_space_review.md` |

This mapping allows each agent to resume work by reading only the minimum required files after a Context Reset.

## Scale-Based Execution Modes

| User Request | Execution Mode | Agents Deployed | Sprint Contract |
|-------------|----------------|-----------------|-----------------|
| "Build a web app", "SaaS development" | **Full pipeline** | All 7 agents | Required |
| "Build only the API" | **Backend mode** | product-owner + architect + backend + qa | Required |
| "Build only the frontend" (API exists) | **Frontend mode** | architect + frontend + qa | Required |
| "Refactor this code" | **Refactoring mode** | architect + relevant developer + qa | Optional |
| "Set up deployment only" | **DevOps mode** | devops alone | Not needed |
| "Review business viability" | **Planning mode** | product-owner alone | Not needed |
| "Do domain modeling" | **Modeling mode** | architect + ontology-advisor | Not needed |
| "Review the code" | **Review mode** | qa + ontology-advisor | Not needed |

**Existing code utilization**: If existing code is present, the architect analyzes it to identify extension points and deploys only the necessary agents.

## Data Transfer Protocol

| Strategy | Method | Purpose |
|----------|--------|---------|
| File-based | `_workspace/` + `src/` | Design documents + source code (source of truth) |
| Message-based | SendMessage | API integration, code review, revision requests |
| Task-based | TaskCreate/TaskUpdate | Progress tracking |

**Core principle**: Files are the source of truth. Messages are for coordination/notifications. Inter-agent information must be transferred via files to survive Context Reset.

## Conflict Resolution Protocol

| Conflict Type | Resolver | Procedure |
|--------------|----------|-----------|
| Sprint Contract agreement failure | Orchestrator | Compare Evaluator and Generator arguments → orchestrator makes final decision |
| Frontend ↔ Backend API spec mismatch | architect | architect arbitrates based on API spec (`04_api_spec.md`) |
| Generator disputes QA grading | Orchestrator | Generator submits specific rebuttal → orchestrator reviews grading evidence → upholds/revises |
| Business goals vs technical constraints | product-owner | ROI-based tradeoff analysis → adjust scope by priority |

## Error Handling

| Error Type | Strategy |
|-----------|----------|
| Ambiguous requirements | C10 semantic enrichment: lexical expansion → semantic layering → ontology alignment |
| Tech stack unspecified | Default stack by scale (MVP: Next.js + SQLite) |
| Build error | Error analysis → relevant developer fixes → QA re-grading |
| Agent failure | Retry once → proceed without that artifact, note in review |
| Grading FAIL | Specific revision instructions → Generator rework → re-grading (max 3 rounds) |
| FAIL after 3 rounds | Proceed with current state, document unresolved issues in 09_review_report |
| Business viability concern | product-owner proposes pivot/3 alternatives |
| Context overload | Context Reset: file-based handoff then reset |
| Self-Eval Bias | QA does not accept Generator's self-evaluation, independent verification |

## Model Optimization Notes (Opus 4.6)

Opus 4.6 plans more deliberately, sustains agentic tasks longer, and operates stably on larger codebases.

**4.6 Optimizations:**
- No need to over-decompose Sprints — model plans its own steps
- Evaluator is more effective evaluating at **phase completion** rather than per-Sprint
- If model capability is sufficient for task complexity, Evaluator may be unnecessary (e.g., DevOps mode)
- Harness complexity is invested only in **what the model cannot do**: preventing Self-Evaluation Bias and design quality grading are the key investments

## Test Scenarios

### Normal Flow
**Prompt**: "Build a pet health management SaaS. A service where owners can manage pet health records and share them with veterinarians"
**Expected Result**:
- Planner expansion: 1 sentence → 16+ feature specs (health records, vaccinations, sharing, notifications, dashboard, etc.)
- Market analysis: Pet care market size, competitors (PetDesk, Vetster, etc.), revenue model
- Domain model: Owner/Pet/HealthRecord/Veterinarian ontology (classes/relations/axioms)
- Sprint Contract: Per-feature pass criteria + design grading criteria agreed upon
- Architecture: Next.js + Prisma + PostgreSQL, ReBAC-based sharing permissions
- Frontend: Dashboard **free of AI slop**, health record CRUD, veterinarian sharing UI
- Backend: Auth API, CRUD API, relation-based sharing permissions
- Grading: Quantitative rubric-based PASS/FAIL + 6-space review
- Deployment: Vercel + PlanetScale

### Extending Existing Code
**Prompt**: "Add payment functionality to this Next.js project" + existing code
**Expected Result**:
- architect adds payment ontology to existing domain model
- Sprint Contract: Payment flow success criteria agreed upon
- backend adds payment API (meta-edge: payment middleware)
- frontend adds payment UI
- qa performs quantitative grading on payment flow + impact analysis

### Ambiguous Requirements
**Prompt**: "Build me something useful as a web app"
**Expected Result**:
- C10 semantic enrichment: lexical expansion (productivity/collaboration/health/...) → semantic layering → domain suggestions
- product-owner proposes 3 directions with business analysis
- Full pipeline proceeds after user selection

## Agent-Specific Extended Skills

| Skill | Target Agent | Role |
|-------|-------------|------|
| `domain-modeling` | architect + ontology-advisor | Domain modeling based on ontology 4 elements |
| `six-space-review` | qa-engineer | 6-space multi-dimensional code review |
| `impact-analysis` | qa-engineer | NOMIK impact analysis |
| `semantic-requirements` | product-owner | Requirements semantic enrichment |
