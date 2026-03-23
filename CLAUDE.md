# SOS Fullstack Development Harness

온톨로지 사상으로 풀스택 개발하는 하네스. SOS(Study Ontology System) 35개 개념을 **개발 방법론**으로 적용하여, 에이전트 팀이 요구사항→설계→프론트엔드→백엔드→테스트→배포를 협업 수행한다.

## 핵심 철학

> 온톨로지는 만드는 대상이 아니라 **생각하는 방식**이다.

모든 개발 단계에서 "엔티티는 무엇이고, 관계는 무엇이고, 규칙은 무엇인가?"를 묻는다. 이것이 확률적 코딩(감으로 짜기)에서 구조적 코딩(관계로 짜기)으로의 전환이다.

## 구조

```
.claude/
├── agents/
│   ├── product-owner.md         — PO/CEO (사업성 판단, 시장분석, ROI, GTM 전략)
│   ├── architect.md             — 시스템 아키텍트 (온톨로지 기반 도메인 모델링)
│   ├── frontend-dev.md          — 프론트엔드 (계층공간 컴포넌트, 능동 UI)
│   ├── backend-dev.md           — 백엔드 (ReBAC 인증, 메타엣지 미들웨어)
│   ├── qa-engineer.md           — QA (NOMIK 영향도 분석, 인과공간 디버깅)
│   ├── devops-engineer.md       — DevOps (레버 5속성 CI/CD, 능동 모니터링)
│   └── ontology-advisor.md      — 온톨로지 어드바이저 (SOS 방법론 컨설팅)
├── skills/
│   ├── sos-fullstack/skill.md   — 오케스트레이터 (팀 조율, 워크플로우)
│   ├── domain-modeling/skill.md — 도메인 모델링 (비즈니스→온톨로지→코드)
│   ├── six-space-review/skill.md — 6-공간 코드 리뷰
│   ├── impact-analysis/skill.md — NOMIK 영향도 분석
│   └── semantic-requirements/skill.md — 요구사항 의미 강화
└── CLAUDE.md                    — 상세 아키텍처
```

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
- `_workspace/01_market_analysis.md` — 시장/사업성 분석 (PO)
- `_workspace/02_domain_model.md` — 온톨로지 기반 도메인 모델 (architect)
- `_workspace/03_architecture.md` — 시스템 아키텍처 (architect)
- `_workspace/04_api_spec.md` — API 명세 (architect)
- `_workspace/05_db_schema.md` — DB 스키마 (architect)
- `_workspace/06_test_plan.md` — 테스트 계획 (qa)
- `_workspace/07_deploy_guide.md` — 배포 가이드 (devops)
- `_workspace/08_six_space_review.md` — 6-공간 코드 리뷰 (qa)
- `_workspace/09_review_report.md` — 최종 리뷰 보고서
- `src/` — 소스 코드

## 온톨로지 방법론 참조

SOS 35개 개념의 상세 정의는 `ontology/` 디렉토리에 있다:
- `ontology/sos-graph.json` — 전체 개념 그래프
- `ontology/concepts/{tier}/{ID}.json` — 개별 개념 상세
- `ontology/edges.json` — 개념 간 관계
- `ontology/meta-edges.json` — 메타엣지 규칙
