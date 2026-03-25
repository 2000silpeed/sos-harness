# SOS Fullstack Development Harness

온톨로지 사상으로 풀스택 개발하는 하네스. SOS(Study Ontology System) 35개 개념을 **개발 방법론**으로 적용하고, GAN 영감의 Generator/Evaluator 아키텍처로 에이전트 팀이 요구사항→설계→Sprint Contract→프론트엔드→백엔드→채점 기반 검증→배포를 협업 수행한다.

## 핵심 철학

> 온톨로지는 만드는 대상이 아니라 **생각하는 방식**이다.

모든 개발 단계에서 "엔티티는 무엇이고, 관계는 무엇이고, 규칙은 무엇인가?"를 묻는다. 이것이 확률적 코딩(감으로 짜기)에서 구조적 코딩(관계로 짜기)으로의 전환이다.

## 설계 참조

- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — GAN 패턴, Context Reset, Sprint Contract
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — 에이전트 오케스트레이션
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI 슬롭 방지 디자인

## 구조

```
.claude/
├── agents/
│   ├── product-owner.md         — Planner: 사업성 판단, 스펙 확장
│   ├── architect.md             — Generator: 온톨로지 기반 도메인 모델링
│   ├── frontend-dev.md          — Generator: UI + 디자인 품질 (AI 슬롭 방지)
│   ├── backend-dev.md           — Generator: ReBAC 인증, 메타엣지 미들웨어
│   ├── qa-engineer.md           — Evaluator: 정량 채점, 6-공간 리뷰, NOMIK
│   ├── devops-engineer.md       — Generator: 레버 5속성 CI/CD
│   └── ontology-advisor.md      — Advisor: SOS 방법론 컨설팅
├── skills/
│   ├── sos-fullstack/skill.md   — 오케스트레이터 (GAN 루프, Sprint Contract)
│   ├── domain-modeling/skill.md — 도메인 모델링
│   ├── six-space-review/skill.md — 6-공간 코드 리뷰
│   ├── impact-analysis/skill.md — NOMIK 영향도 분석
│   └── semantic-requirements/skill.md — 요구사항 의미 강화
└── CLAUDE.md                    — 상세 아키텍처
```

## v2 개선사항 (2026-03-26)

| 개선 | 출처 | 효과 |
|------|------|------|
| **GAN Generator/Evaluator 분리** | Anthropic Blog | 자기 평가 바이어스 제거, 독립적 품질 보증 |
| **Sprint Contract** | Anthropic Blog | 구현 전 성공 기준 합의 → 기대치 불일치 방지 |
| **정량 채점 루브릭** | Anthropic Blog | 주관적 🔴/🟡/🟢 → 5점 척도 + 합격 임계값 |
| **Context Reset 프로토콜** | Anthropic Blog | 파일 기반 핸드오프로 장시간 세션 일관성 유지 |
| **AI 슬롭 방지 디자인** | Frontend Skill | 범용 폰트/보라색 그라디언트 등 제네릭 패턴 거부 |
| **Playwright MCP 라이브 테스트** | Anthropic Blog | 실제 브라우저 기반 UI/API 검증 |
| **Planner 역할 강화** | Anthropic Blog | 1-4문장 → 포괄적 제품 스펙 확장 |
| **Opus 4.6 최적화** | Anthropic Blog | Sprint 과세분화 제거, 단계 완료 시점 평가 |

## SOS 개념의 개발 적용

| SOS 개념 | 개발에서의 의미 | 적용 에이전트 |
|----------|---------------|-------------|
| C02 온톨로지 | 도메인 모델 = 클래스/속성/관계/공리 | architect |
| C06 6분석공간 | 코드 리뷰 6차원 (계층/시간/재귀/구조/인과/통합) | qa-engineer |
| C07 ReBAC | 관계 기반 인증/인가 설계 | backend-dev |
| C03 메타엣지 | 미들웨어, 데코레이터, 인터셉터 = "규칙의 규칙" | backend-dev |
| C11 NOMIK | "이 코드 바꾸면 뭐가 깨지나?" 영향도 분석 | qa-engineer |
| C10 벡터의미강화 | 모호한 요구사항 → 정밀한 스펙으로 확장 | product-owner |
| C13 레버/메타레버 | CI/CD 5속성: 합성성/관측성/멱등성/회복성/버전관리 | devops-engineer |
| C14 물리연산엔진 | 프랙탈 분해: 큰 태스크를 재귀적으로 병렬 분해 | 전체 |
| C15 능동메타데이터 | 사용자 컨텍스트에 따라 실시간 적응하는 UI | frontend-dev |
| C04 AIP/Apollo | 텍스트→구조→액션 패턴의 제품 설계 | product-owner |

## 사용법

`/sos-fullstack` 스킬을 트리거하거나, 자연어로 개발 요청한다.

## 산출물

모든 산출물은 `_workspace/`에 생성된다:
- `_workspace/00_input.md` — 사용자 입력 정리
- `_workspace/01_market_analysis.md` — 시장/사업성 분석 + 확장 스펙 (PO/Planner)
- `_workspace/02_domain_model.md` — 온톨로지 기반 도메인 모델 (architect)
- `_workspace/03_architecture.md` — 시스템 아키텍처 (architect)
- `_workspace/03.5_sprint_contract.md` — Sprint Contract: 성공 기준 합의 (qa ↔ 개발자)
- `_workspace/04_api_spec.md` — API 명세 (architect)
- `_workspace/05_db_schema.md` — DB 스키마 (architect)
- `_workspace/06_test_plan.md` — 테스트 계획 (qa)
- `_workspace/07_deploy_guide.md` — 배포 가이드 (devops)
- `_workspace/08_six_space_review.md` — 6-공간 코드 리뷰 (qa)
- `_workspace/09_review_report.md` — 최종 리뷰 보고서
- `_workspace/10_grade_report.md` — 정량 채점 보고서 (qa/Evaluator)
- `src/` — 소스 코드

## 온톨로지 방법론 참조

SOS 35개 개념의 상세 정의는 `ontology/` 디렉토리에 있다:
- `ontology/sos-graph.json` — 전체 개념 그래프
- `ontology/concepts/{tier}/{ID}.json` — 개별 개념 상세
- `ontology/edges.json` — 개념 간 관계
- `ontology/meta-edges.json` — 메타엣지 규칙
