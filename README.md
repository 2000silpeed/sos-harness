# SOS Fullstack Development Harness

> Ontology is not something you build — it is a **thinking model**.

A Claude Code fullstack development harness that applies all 35 [S.O.S (Study Ontology System)](https://kinkos1234.github.io/sos/) concepts as a **development methodology**. Built on [harness-100](https://github.com/revfactory/harness-100) patterns and inspired by Anthropic's [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps).

## What Makes This Different

| Generic Harness | SOS Harness |
|----------------|-------------|
| Design tables first | Define **domain ontology** (classes/properties/relations/axioms) first |
| RBAC auth | **ReBAC** relationship-based auth |
| Single-perspective code review | **6-space** multi-dimensional code review |
| String-search impact analysis | **NOMIK** structural impact analysis |
| Ad-hoc CI/CD design | **Lever 5-property** CI/CD |
| Code only | **Business viability / market / ROI** assessment included |
| Self-evaluated quality | **GAN-inspired Generator/Evaluator** separation with quantitative grading |
| No pre-agreed criteria | **Sprint Contract** — success criteria agreed before implementation |

## Agent Team (7 agents)

| Agent | Role | GAN Role | SOS Lens |
|-------|------|----------|----------|
| **product-owner** | Market analysis, ROI, GTM strategy, spec expansion | Planner | C04 AIP, C10 Semantic Enrichment |
| **architect** | Ontology-based domain modeling, architecture | Generator | C02 Ontology, C09 Domain Ontology |
| **frontend-dev** | React/Next.js UI + design quality (AI slop prevention) | Generator | C06 Hierarchy Space, C15 Active Metadata |
| **backend-dev** | API, DB, auth, business logic | Generator | C07 ReBAC, C03 Meta-edge |
| **qa-engineer** | Quantitative grading, 6-space review, impact analysis | Evaluator | C11 NOMIK, C06 6-Space Review |
| **devops-engineer** | CI/CD, infrastructure, deployment, monitoring | Generator | C13 Lever 5-property, C15 Active Metadata |
| **ontology-advisor** | SOS methodology consulting (no code) | Advisor | All SOS concepts |

## Skills (5 skills)

| Skill | Trigger Examples | Description |
|-------|-----------------|-------------|
| `/sos-fullstack` | "Build a web app", "SaaS development" | Fullstack development orchestrator |
| `/domain-modeling` | "Model this domain" | Business → Ontology 4 elements → Code |
| `/six-space-review` | "Review this code" | 6-dimensional review: hierarchy/temporal/recursive/structural/causal/cross-space |
| `/impact-analysis` | "What breaks if I change this?" | NOMIK structural impact analysis |
| `/semantic-requirements` | "Clarify these requirements" | 3-stage ambiguous → precise spec refinement |

## How SOS Concepts Apply to Development

```
Ontology 4 Elements  →  Domain model: class=entity, property=field, relation=FK, axiom=business rule
Meta-edge            →  Middleware, decorators, interceptors = "rules about rules"
ReBAC                →  Relationship-path auth (solves RBAC role explosion)
6 Analysis Spaces    →  Code review: hierarchy / temporal / recursive / structural / causal / cross-space
NOMIK                →  "If I change this symbol, what breaks?" — structural impact analysis
Lever 5 Properties   →  CI/CD: composability / observability / idempotency / resilience / versioning
Semantic Enrichment  →  Ambiguous requirements → precise spec (lexical → semantic → ontology alignment)
Fractal Decomposition →  Recursively decompose large tasks into same structure → parallel execution
Active Metadata      →  UI that adapts in real-time to user context
```

## Workflow

```
Phase 1:   Preparation       →  Input analysis, determine execution mode
Phase 2:   Planning + Design  →  [PO: Business viability] → [Architect: Domain model → Architecture → API → DB]
Phase 2.5: Sprint Contract    →  [QA ↔ Developers: Agree on success criteria before implementation]
Phase 3:   Implementation     →  [Frontend] + [Backend] + [DevOps]  (parallel)
Phase 4:   Grading-Based QA   →  [QA: Quantitative grading + 6-space review] → Fix loop (max 3 rounds)
Phase 5:   Final Review       →  [PO + Ontology Advisor: Final review report]
```

## Project Structure

```
.claude/
├── agents/                    # 7-agent team
│   ├── product-owner.md       # Planner: CEO/PO
│   ├── architect.md           # Generator: System Architect
│   ├── frontend-dev.md        # Generator: Frontend (AI slop prevention)
│   ├── backend-dev.md         # Generator: Backend (ReBAC + meta-edge)
│   ├── qa-engineer.md         # Evaluator: QA (quantitative grading)
│   ├── devops-engineer.md     # Generator: DevOps
│   └── ontology-advisor.md    # Advisor: Ontology consulting
├── skills/                    # 5 skills
│   ├── sos-fullstack/         # Orchestrator (GAN loop + Sprint Contract)
│   ├── domain-modeling/       # Domain modeling
│   ├── six-space-review/      # 6-space code review
│   ├── impact-analysis/       # NOMIK impact analysis
│   └── semantic-requirements/ # Requirements semantic enrichment
└── CLAUDE.md                  # Detailed architecture

ontology/                      # SOS methodology reference (35-concept knowledge graph)
├── sos-graph.json             # Full concept graph
├── edges.json                 # 62 relationship edges
├── pipeline.json              # Pipeline definition
├── meta-edges.json            # Meta-edge rules
└── concepts/                  # 35 individual concept JSONs
    ├── tier-n1/ (P01-P10)     # Pure foundations
    ├── tier-0/ (F01-F10)      # Applied foundations
    ├── tier-1/ (C01-C05)      # Core
    ├── tier-2/ (C06-C10)      # Framework
    └── tier-3/ (C11-C15)      # Implementation

cmr/                           # Project quality tracking
levers/                        # CI/CD lever catalog
```

## Usage

1. Clone this repo or copy the `.claude/` directory into your project
2. Run `/sos-fullstack` in Claude Code, or make a request in natural language

```bash
# Fullstack development
"Build a pet health management SaaS"

# Domain modeling only
"Model the e-commerce domain using ontology"

# Code review
"Review this code with 6-space analysis"

# Impact analysis
"What breaks if I change this function?"

# Business viability only
"Assess the market viability of this idea"
```

## v2 Improvements (2026-03-26)

| Improvement | Source | Effect |
|-------------|--------|--------|
| GAN Generator/Evaluator separation | [Anthropic Blog](https://www.anthropic.com/engineering/harness-design-long-running-apps) | Eliminates self-evaluation bias |
| Sprint Contract | Anthropic Blog | Pre-implementation success criteria agreement |
| Quantitative grading rubric | Anthropic Blog | 5-point scale + pass thresholds replace subjective review |
| Context Reset protocol | Anthropic Blog | File-based handoff for long session consistency |
| AI slop prevention | [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) | Rejects generic fonts, purple gradients, cookie-cutter patterns |
| Playwright MCP live testing | Anthropic Blog | Real browser-based UI/API verification |
| Opus 4.6 optimization | Anthropic Blog | Reduced sprint fragmentation, phase-level evaluation |

## References

- [S.O.S (Study Ontology System)](https://kinkos1234.github.io/sos/) — Original ontology methodology
- [harness-100](https://github.com/revfactory/harness-100) — Harness pattern reference
- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — GAN pattern, Context Reset
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Agent orchestration
- @heretics_gene (original), @specal1849 (editorial), @comad.j (site planning)

## Other Languages

- [한국어 (Korean)](docs/ko/README.md)

## License

Apache 2.0
