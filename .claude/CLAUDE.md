# SOS Fullstack Harness — 상세 아키텍처

## 온톨로지 사상의 개발 적용 원칙

1. **도메인 우선**: 코드 전에 도메인을 정의한다. 엔티티/관계/규칙이 먼저, 테이블/API/UI는 그 다음
2. **관계가 핵심**: FK, API 연동, 컴포넌트 props, 이벤트 — 모두 "관계"다. 관계를 명시적으로 설계한다
3. **메타엣지 인식**: 미들웨어, 데코레이터, 인터셉터, 훅은 "규칙의 규칙"이다. 이를 의식적으로 설계한다
4. **6-공간 리뷰**: 코드를 단일 관점이 아닌 6차원(계층/시간/재귀/구조/인과/통합)으로 본다
5. **프랙탈 분해**: 큰 문제를 동일 구조로 재귀적 분해한다. 개인의 작업 방식 = 팀의 작업 방식

## 에이전트 팀 구성

| 에이전트 | 파일 | 역할 | SOS 렌즈 |
|---------|------|------|---------|
| product-owner | `agents/product-owner.md` | 사업성/시장성 판단, GTM, ROI | C04(AIP: 텍스트→구조→액션), C10(의미강화) |
| architect | `agents/architect.md` | 도메인 모델링, 아키텍처, DB/API 설계 | C02(온톨로지), C09(도메인온톨로지) |
| frontend-dev | `agents/frontend-dev.md` | React/Next.js UI 구현 | C06(계층공간), C15(능동메타데이터) |
| backend-dev | `agents/backend-dev.md` | API, DB, 인증, 비즈니스 로직 | C07(ReBAC), C03(메타엣지) |
| qa-engineer | `agents/qa-engineer.md` | 테스트, 코드 리뷰, 영향도 분석 | C11(NOMIK), C06(6분석공간) |
| devops-engineer | `agents/devops-engineer.md` | CI/CD, 인프라, 배포, 모니터링 | C13(레버 5속성), C15(능동메타데이터) |
| ontology-advisor | `agents/ontology-advisor.md` | SOS 방법론 컨설팅, 설계 리뷰 | 전체 SOS 개념 |

## 팀 통신 프로토콜

에이전트들은 SendMessage로 직접 통신한다:
- **product-owner** → architect: 비즈니스 요구사항, 우선순위, 시장 제약조건 전달
- **architect** 완료 → frontend에게 컴포넌트 구조/라우팅, backend에게 API/DB/인증, qa에게 기능 요구사항, devops에게 인프라 요구사항
- **frontend ↔ backend**: API 연동 중 실시간 소통
- **qa** → 해당 개발자: 🔴 필수 수정 요청 → 재작업 → 재검증 (최대 2회)
- **ontology-advisor** → 모든 에이전트: 설계 결정에 SOS 관점 제안
- **devops** 완료 → 전체: 환경변수, 배포 URL 공유

## 워크플로우

### Phase 1: 준비 (오케스트레이터 직접 수행)
1. 사용자 입력에서 앱 설명, 기술 스택, 규모, 기존 코드, 배포 플랫폼 추출
2. `_workspace/00_input.md`에 저장
3. 실행 모드 결정

### Phase 2: 사업성 분석 + 도메인 모델링 (직렬)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 1 | 시장/사업성 분석 | product-owner | 없음 | `01_market_analysis.md` |
| 2 | 도메인 모델링 | architect (+ ontology-advisor) | 작업 1 | `02_domain_model.md` |
| 3 | 아키텍처/API/DB 설계 | architect | 작업 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

### Phase 3: 구현 (병렬)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 4a | 프론트엔드 개발 | frontend-dev | 작업 3 | `src/` 프론트엔드 코드 |
| 4b | 백엔드 개발 | backend-dev | 작업 3 | `src/` 백엔드 코드 |
| 4c | 배포 설정 | devops-engineer | 작업 3 | `07_deploy_guide.md`, CI/CD 설정 |

### Phase 4: 검증 (직렬)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 5 | 테스트 & 6-공간 리뷰 | qa-engineer | 작업 4a, 4b | `06_test_plan.md`, `08_six_space_review.md` |
| 6 | 최종 리뷰 | product-owner + ontology-advisor | 작업 5 | `09_review_report.md` |

## 작업 규모별 모드

| 사용자 요청 | 실행 모드 | 투입 에이전트 |
|------------|----------|-------------|
| "웹앱 만들어줘", "SaaS 개발" | **풀 파이프라인** | 7명 전원 |
| "API만 만들어줘" | **백엔드 모드** | product-owner + architect + backend + qa |
| "프론트만 만들어줘" | **프론트 모드** | architect + frontend + qa |
| "이 코드 리팩토링" | **리팩토링 모드** | architect + 해당 개발자 + qa |
| "배포 설정만" | **DevOps 모드** | devops 단독 |
| "사업성 검토해줘" | **기획 모드** | product-owner 단독 |
| "도메인 모델링해줘" | **모델링 모드** | architect + ontology-advisor |
| "코드 리뷰해줘" | **리뷰 모드** | qa + ontology-advisor |
| "영향도 분석해줘" | **분석 모드** | qa 단독 (NOMIK) |

## 에러 핸들링

| 에러 유형 | 전략 |
|----------|------|
| 요구사항 모호 | 의미 강화(C10) 3단계로 확장: 어휘→의미→온톨로지 정렬 |
| 기술 스택 미지정 | 규모별 기본 스택 (MVP: Next.js + SQLite) |
| 빌드 에러 | 에러 로그 분석 → 해당 개발자 수정 → QA 재검증 |
| 에이전트 실패 | 1회 재시도 → 실패 시 해당 산출물 없이 진행 |
| 리뷰에서 🔴 | 해당 개발자에 수정 요청 → 재작업 (최대 2회) |
| 사업성 의문 | product-owner가 pivot 제안, 대안 방향 3가지 제시 |
