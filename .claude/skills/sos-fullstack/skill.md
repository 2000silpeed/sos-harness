---
name: sos-fullstack
description: "온톨로지 사고 기반 풀스택 개발 파이프라인. 에이전트 팀이 사업성→도메인모델링→설계→프론트→백엔드→테스트→배포를 협업 수행한다. '웹앱 만들어줘', '서비스 개발', 'SaaS 개발', 'CRUD 앱', '대시보드', '관리자 페이지', '회원가입/로그인', 'REST API 개발', '풀스택 프로젝트', 'Next.js 앱', '서비스 기획' 등 웹 애플리케이션 개발 전반에 이 스킬을 사용한다. 모바일 앱(React Native/Flutter), 게임, ML/AI 모델 학습은 범위 밖이다."
---

# SOS Fullstack — 온톨로지 사고 기반 풀스택 개발

에이전트 팀이 온톨로지 방법론으로 사업성→도메인→설계→프론트→백엔드→테스트→배포를 협업 수행한다.

## 핵심 차별점

일반 풀스택 하네스와의 차이:
- **도메인 모델이 먼저**: ERD/API 전에 온톨로지 4요소(클래스/속성/관계/공리) 정의
- **관계 기반 설계**: 모든 연결(FK, API, 컴포넌트 props)을 명시적 "관계"로 설계
- **메타엣지 의식**: 미들웨어/인터셉터를 "규칙의 규칙"으로 문서화
- **6-공간 리뷰**: 코드를 6차원으로 다각도 검증
- **사업성 검증**: 기술 전에 시장/수익성 판단

## 실행 모드

**에이전트 팀** — 7명이 SendMessage로 직접 통신하며 교차 검증한다.

## 에이전트 구성

| 에이전트 | 파일 | 역할 | 타입 |
|---------|------|------|------|
| product-owner | `.claude/agents/product-owner.md` | 사업성 판단, 시장분석, GTM | general-purpose |
| architect | `.claude/agents/architect.md` | 온톨로지 도메인 모델링, 아키텍처 | general-purpose |
| frontend-dev | `.claude/agents/frontend-dev.md` | React/Next.js 프론트엔드 | general-purpose |
| backend-dev | `.claude/agents/backend-dev.md` | API, DB, ReBAC 인증 | general-purpose |
| qa-engineer | `.claude/agents/qa-engineer.md` | NOMIK 영향도 분석, 6-공간 리뷰 | general-purpose |
| devops-engineer | `.claude/agents/devops-engineer.md` | 레버 5속성 CI/CD | general-purpose |
| ontology-advisor | `.claude/agents/ontology-advisor.md` | SOS 방법론 컨설팅 | general-purpose |

## 워크플로우

### Phase 1: 준비 (오케스트레이터 직접 수행)

1. 사용자 입력에서 추출:
   - **앱 설명**: 무엇을 만들 것인지
   - **기술 스택** (선택): 선호하는 프레임워크
   - **규모** (선택): MVP/소규모/중규모/대규모
   - **기존 코드** (선택): 확장할 기존 프로젝트
   - **배포 플랫폼** (선택): Vercel/AWS/Docker 등
2. `_workspace/` 디렉토리 생성
3. `_workspace/00_input.md`에 입력 정리
4. 기존 코드가 있으면 분석 후 단계 조정
5. 실행 모드 결정

### Phase 2: 사업성 + 도메인 모델링

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 1 | 시장/사업성 분석 | product-owner | 없음 | `01_market_analysis.md` |
| 2 | 도메인 모델링 + 리뷰 | architect + ontology-advisor | 작업 1 | `02_domain_model.md` |
| 3 | 아키텍처/API/DB 설계 | architect | 작업 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

**ontology-advisor**는 작업 2에서 architect의 도메인 모델을 리뷰한다.

### Phase 3: 구현 (병렬)

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 4a | 프론트엔드 개발 | frontend-dev | 작업 3 | `src/` 프론트엔드 코드 |
| 4b | 백엔드 개발 | backend-dev | 작업 3 | `src/` 백엔드 코드 |
| 4c | 배포 설정 | devops-engineer | 작업 3 | `07_deploy_guide.md`, CI/CD 설정 |

작업 4a, 4b, 4c는 **병렬 실행**. 모두 작업 3에만 의존.

**소통 흐름:**
- architect 완료 → frontend에게 컴포넌트/라우팅, backend에게 API/DB/인증, devops에게 인프라, qa에게 요구사항
- frontend ↔ backend: API 연동 실시간 소통
- devops 완료 → 전체에게 환경변수/배포 URL

### Phase 4: 검증

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 5 | 테스트 & 6-공간 리뷰 | qa-engineer | 4a, 4b | `06_test_plan.md`, `08_six_space_review.md` |
| 6 | 최종 리뷰 | product-owner | 5 | `09_review_report.md` |

QA의 🔴 필수 수정 → 해당 개발자 재작업 → 재검증 (최대 2회)

### Phase 5: 최종 보고

1. 모든 산출물 확인
2. 🔴 필수 수정 반영 확인
3. 사용자에게 최종 요약:
   - 시장 분석 — `_workspace/01_market_analysis.md`
   - 도메인 모델 — `_workspace/02_domain_model.md`
   - 아키텍처 — `_workspace/03_architecture.md`
   - API 명세 — `_workspace/04_api_spec.md`
   - DB 스키마 — `_workspace/05_db_schema.md`
   - 테스트 계획 — `_workspace/06_test_plan.md`
   - 배포 가이드 — `_workspace/07_deploy_guide.md`
   - 6-공간 리뷰 — `_workspace/08_six_space_review.md`
   - 최종 리뷰 — `_workspace/09_review_report.md`
   - 소스 코드 — `src/`

## 작업 규모별 모드

| 사용자 요청 | 실행 모드 | 투입 에이전트 |
|------------|----------|-------------|
| "웹앱 만들어줘", "SaaS 개발" | **풀 파이프라인** | 7명 전원 |
| "API만 만들어줘" | **백엔드 모드** | product-owner + architect + backend + qa |
| "프론트만 만들어줘" (API 있음) | **프론트 모드** | architect + frontend + qa |
| "이 코드 리팩토링" | **리팩토링 모드** | architect + 해당 개발자 + qa |
| "배포 설정만" | **DevOps 모드** | devops 단독 |
| "사업성 검토해줘" | **기획 모드** | product-owner 단독 |
| "도메인 모델링해줘" | **모델링 모드** | architect + ontology-advisor |
| "코드 리뷰해줘" | **리뷰 모드** | qa + ontology-advisor |

**기존 코드 활용**: 기존 코드가 있으면 architect가 분석하여 확장 지점을 파악하고 필요한 에이전트만 투입.

## 데이터 전달 프로토콜

| 전략 | 방식 | 용도 |
|------|------|------|
| 파일 기반 | `_workspace/` + `src/` | 설계 문서 + 소스 코드 |
| 메시지 기반 | SendMessage | API 연동, 코드 리뷰, 수정 요청 |
| 태스크 기반 | TaskCreate/TaskUpdate | 진행 상황 추적 |

## 에러 핸들링

| 에러 유형 | 전략 |
|----------|------|
| 요구사항 모호 | C10 의미 강화: 어휘확장→의미다층화→온톨로지정렬 |
| 기술 스택 미지정 | 규모별 기본 스택 (MVP: Next.js + SQLite) |
| 빌드 에러 | 에러 분석 → 해당 개발자 수정 → QA 재검증 |
| 에이전트 실패 | 1회 재시도 → 해당 산출물 없이 진행, 리뷰에 명시 |
| 🔴 발견 | 해당 개발자에 수정 → 재작업 → 재검증 (최대 2회) |
| 사업성 의문 | product-owner가 pivot/대안 3가지 제시 |

## 테스트 시나리오

### 정상 흐름
**프롬프트**: "반려동물 건강 관리 SaaS를 만들어줘. 보호자가 반려동물 건강 기록을 관리하고, 수의사와 공유할 수 있는 서비스"
**기대 결과**:
- 시장 분석: 펫케어 시장 규모, 경쟁사(핏펫, 포인핸드 등), 수익모델
- 도메인 모델: 보호자/반려동물/건강기록/수의사 온톨로지 (클래스/관계/공리)
- 아키텍처: Next.js + Prisma + PostgreSQL, ReBAC 기반 공유 권한
- 프론트: 대시보드, 건강 기록 CRUD, 수의사 공유 UI
- 백엔드: 인증 API, CRUD API, 관계 기반 공유 권한
- 테스트: 6-공간 리뷰, 영향도 분석
- 배포: Vercel + PlanetScale

### 기존 코드 확장
**프롬프트**: "이 Next.js 프로젝트에 결제 기능 추가해줘" + 기존 코드
**기대 결과**:
- architect가 기존 도메인 모델에 결제 온톨로지 추가
- backend가 결제 API 추가 (메타엣지: 결제 미들웨어)
- frontend가 결제 UI 추가
- qa가 결제 플로우 영향도 분석

### 모호한 요구사항
**프롬프트**: "뭔가 유용한 웹앱 만들어줘"
**기대 결과**:
- C10 의미 강화: 어휘 확장(생산성/협업/건강/...)→의미 다층화→도메인 제안
- product-owner가 3가지 방향 제안, 사업성 분석
- 사용자 선택 후 풀 파이프라인 진행

## 에이전트별 확장 스킬

| 스킬 | 대상 에이전트 | 역할 |
|------|-------------|------|
| `domain-modeling` | architect + ontology-advisor | 온톨로지 4요소 기반 도메인 모델링 |
| `six-space-review` | qa-engineer | 6-공간 다차원 코드 리뷰 |
| `impact-analysis` | qa-engineer | NOMIK 영향도 분석 |
| `semantic-requirements` | product-owner | 요구사항 의미 강화 |
