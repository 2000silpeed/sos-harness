# SOS Fullstack Development Harness

> 온톨로지는 만드는 대상이 아니라 **생각하는 방식**이다.

[S.O.S(Study Ontology System)](https://kinkos1234.github.io/sos/) 35개 핵심 개념을 **개발 방법론**으로 적용하는 Claude Code 풀스택 개발 하네스입니다. [harness-100](https://github.com/revfactory/harness-100) 패턴을 기반으로 합니다.

## 핵심 철학

일반 풀스택 하네스와의 차이:

| 일반 하네스 | SOS 하네스 |
|------------|-----------|
| 테이블부터 설계 | **도메인 온톨로지**(클래스/속성/관계/공리)부터 정의 |
| RBAC 인증 | **ReBAC** 관계 기반 인증 |
| 단일 관점 코드 리뷰 | **6-공간** 다차원 코드 리뷰 |
| 문자열 검색 영향도 | **NOMIK** 구조적 영향도 분석 |
| 감으로 CI/CD 설계 | **레버 5속성** 기반 CI/CD |
| 코딩만 | **사업성/시장성/ROI**까지 판단 |

## 에이전트 팀 (7명)

| 에이전트 | 역할 | SOS 사고방식 |
|---------|------|------------|
| **product-owner** | CEO/PO — 시장분석, ROI, GTM 전략 | C04 AIP(텍스트→구조→액션), C10 의미강화 |
| **architect** | 온톨로지 기반 도메인 모델링, 아키텍처 | C02 온톨로지 4요소, C09 도메인 온톨로지 |
| **frontend-dev** | React/Next.js UI 구현 | C06 계층공간, C15 능동 메타데이터 |
| **backend-dev** | API, DB, 인증, 비즈니스 로직 | C07 ReBAC, C03 메타엣지=미들웨어 |
| **qa-engineer** | 테스트, 코드 리뷰, 영향도 분석 | C11 NOMIK, C06 6-공간 리뷰 |
| **devops-engineer** | CI/CD, 인프라, 배포, 모니터링 | C13 레버 5속성, C15 능동 모니터링 |
| **ontology-advisor** | SOS 방법론 컨설팅 (코드 안 짬) | 전체 SOS 개념 |

## 스킬 (5개)

| 스킬 | 트리거 | 설명 |
|------|--------|------|
| `/sos-fullstack` | "웹앱 만들어줘", "SaaS 개발" | 풀스택 개발 오케스트레이터 |
| `/domain-modeling` | "도메인 모델링해줘" | 비즈니스→온톨로지 4요소→코드 |
| `/six-space-review` | "코드 리뷰해줘" | 계층/시간/재귀/구조/인과/통합 6차원 리뷰 |
| `/impact-analysis` | "이거 바꾸면 뭐가 깨지나" | NOMIK 스타일 코드 영향도 분석 |
| `/semantic-requirements` | "요구사항 정리해줘" | 모호한 요구사항 3단계 정밀화 |

## SOS 개념의 개발 적용

```
온톨로지 4요소    →  도메인 모델: 클래스=엔티티, 속성=필드, 관계=FK, 공리=비즈니스규칙
메타엣지          →  미들웨어, 데코레이터, 인터셉터 = "규칙의 규칙"
ReBAC            →  관계 경로 기반 인증/인가 (RBAC 역할 폭발 해결)
6분석공간         →  코드 리뷰: 계층/시간/재귀/구조/인과/통합
NOMIK            →  "이 심볼 바꾸면 뭐가 깨지나?" 구조적 영향도 분석
레버 5속성        →  CI/CD: 합성성/관측성/멱등성/회복성/버전관리
벡터 의미강화      →  모호한 요구사항 → 정밀 스펙 (어휘확장→의미다층화→온톨로지정렬)
프랙탈 분해        →  큰 태스크를 동일 구조로 재귀 분해 → 병렬 실행
능동 메타데이터    →  사용자 컨텍스트에 실시간 적응하는 UI
```

## 워크플로우

```
Phase 1: 준비        → 입력 분석, 실행 모드 결정
Phase 2: 기획+설계   → [PO: 사업성] → [Architect: 도메인모델→아키텍처→API→DB]
Phase 3: 구현 (병렬) → [Frontend] + [Backend] + [DevOps]
Phase 4: 검증        → [QA: 테스트 + 6-공간 리뷰] → [PO: 최종 리뷰]
```

## 프로젝트 구조

```
.claude/
├── agents/                    # 7명 에이전트 팀
│   ├── product-owner.md       # CEO/PO
│   ├── architect.md           # 시스템 아키텍트
│   ├── frontend-dev.md        # 프론트엔드
│   ├── backend-dev.md         # 백엔드
│   ├── qa-engineer.md         # QA
│   ├── devops-engineer.md     # DevOps
│   └── ontology-advisor.md    # 온톨로지 어드바이저
├── skills/                    # 5개 스킬
│   ├── sos-fullstack/         # 오케스트레이터
│   ├── domain-modeling/       # 도메인 모델링
│   ├── six-space-review/      # 6-공간 코드 리뷰
│   ├── impact-analysis/       # NOMIK 영향도 분석
│   └── semantic-requirements/ # 요구사항 의미 강화
└── CLAUDE.md                  # 상세 아키텍처

ontology/                      # SOS 방법론 참조 (35개 개념 지식 그래프)
├── sos-graph.json             # 전체 개념 그래프
├── edges.json                 # 62개 관계 엣지
├── pipeline.json              # 파이프라인 정의
├── meta-edges.json            # 메타엣지 규칙
└── concepts/                  # 35개 개별 개념 JSON
    ├── tier-n1/ (P01-P10)     # 순수기초
    ├── tier-0/ (F01-F10)      # 응용기초
    ├── tier-1/ (C01-C05)      # 핵심
    ├── tier-2/ (C06-C10)      # 프레임워크
    └── tier-3/ (C11-C15)      # 구현

cmr/                           # 프로젝트 품질 추적
levers/                        # CI/CD 레버 카탈로그
```

## 사용법

1. 이 레포를 클론하거나 `.claude/` 디렉토리를 프로젝트에 복사
2. Claude Code에서 `/sos-fullstack` 실행 또는 자연어로 요청

```
# 풀스택 개발
"반려동물 건강 관리 SaaS를 만들어줘"

# 도메인 모델링만
"이커머스 도메인을 온톨로지 기반으로 모델링해줘"

# 코드 리뷰
"이 코드를 6-공간으로 리뷰해줘"

# 영향도 분석
"이 함수 바꾸면 뭐가 깨지나 분석해줘"

# 사업성만
"이 아이디어의 시장성 검토해줘"
```

## 참조

- [S.O.S (Study Ontology System)](https://kinkos1234.github.io/sos/) — 온톨로지 방법론 원본
- [harness-100](https://github.com/revfactory/harness-100) — 하네스 패턴 참조
- @heretics_gene (원작), @specal1849 (편집), @comad.j (사이트 기획)

## License

Apache 2.0
