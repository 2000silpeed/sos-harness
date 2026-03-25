# SOS Fullstack Harness — 상세 아키텍처

## 온톨로지 사상의 개발 적용 원칙

1. **도메인 우선**: 코드 전에 도메인을 정의한다. 엔티티/관계/규칙이 먼저, 테이블/API/UI는 그 다음
2. **관계가 핵심**: FK, API 연동, 컴포넌트 props, 이벤트 — 모두 "관계"다. 관계를 명시적으로 설계한다
3. **메타엣지 인식**: 미들웨어, 데코레이터, 인터셉터, 훅은 "규칙의 규칙"이다. 이를 의식적으로 설계한다
4. **6-공간 리뷰**: 코드를 단일 관점이 아닌 6차원(계층/시간/재귀/구조/인과/통합)으로 본다
5. **프랙탈 분해**: 큰 문제를 동일 구조로 재귀적 분해한다. 개인의 작업 방식 = 팀의 작업 방식
6. **Generator/Evaluator 분리**: 생성과 평가를 구조적으로 분리한다. 자기 평가 바이어스를 제거한다
7. **파일이 진실의 원천**: 컨텍스트 윈도우가 아닌 `_workspace/` 산출물 파일이 에이전트 간 정보 전달의 핵심이다

## GAN 영감의 아키텍처

Anthropic의 [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) 블로그에서 영감을 받은 패턴:

### 역할 분리

| GAN 역할 | 에이전트 | 핵심 기능 |
|---------|---------|----------|
| **Planner** | product-owner | 1-4문장 → 포괄적 제품 스펙 확장 (What 수준, How 제외) |
| **Generator** | architect, frontend, backend, devops | 설계 + 구현 (자기 출력물 평가 금지) |
| **Evaluator** | qa-engineer | 독립 평가, 정량 채점 루브릭, Sprint Contract 기반 검증 |
| **Advisor** | ontology-advisor | 방법론 컨설팅 (코드 작성 안 함) |

### Self-Evaluation Bias 방지

- Generator는 자신의 출력물을 "잘 되었다"고 평가하지 않는다
- Evaluator(QA)만이 정량 채점 권한을 가진다
- QA의 초기 채점이 모두 고득점이면 기준을 한 단계 올려 재평가 (관대함 방지)
- 모든 채점에 구체적 관찰 근거 필수

### Sprint Contract (사전 성공 기준 합의)

구현 시작 전 Evaluator와 Generator가 성공 기준을 합의한다:
- 기능별 합격 조건 + 검증 방법
- 디자인 품질 최소 점수 (각 차원 3/5, 평균 3.5/5)
- 비기능 요구사항 (성능, 접근성, 반응형)
- 산출물: `_workspace/03.5_sprint_contract.md`

### 정량 채점 루브릭

5점 척도로 채점. PASS 조건: 모든 차원 ≥ 3/5, 평균 ≥ 3.5/5, 🔴 항목 0개.
FAIL 시 구체적 수정 지시 → 재구현 → 재채점 (안전장치 최대 3라운드).

## Context Reset 프로토콜

장시간 세션에서 발생하는 두 가지 실패 모드:

1. **컨텍스트 일관성 상실**: 컨텍스트 윈도우가 채워지면서 초기 지시와 모순되는 출력
2. **컨텍스트 불안(Context Anxiety)**: 모델이 컨텍스트 한계를 인식하고 작업을 조기 마무리

**해결: Compaction보다 Reset + 파일 기반 핸드오프**

- 각 Phase 완료 시 산출물을 `_workspace/`에 저장
- 다음 Phase는 파일만 읽으면 작업 가능 (자기완결적 산출물)
- 컨텍스트가 과부하되면 압축 대신 리셋 후 파일 기반 재시작

## 에이전트 팀 구성

| 에이전트 | 파일 | 역할 | GAN 역할 | SOS 렌즈 |
|---------|------|------|---------|---------|
| product-owner | `agents/product-owner.md` | 사업성/시장성 판단, 스펙 확장 | Planner | C04(AIP), C10(의미강화) |
| architect | `agents/architect.md` | 도메인 모델링, 아키텍처, DB/API 설계 | Generator | C02(온톨로지), C09(도메인온톨로지) |
| frontend-dev | `agents/frontend-dev.md` | React/Next.js UI + 디자인 품질 | Generator | C06(계층공간), C15(능동메타데이터) |
| backend-dev | `agents/backend-dev.md` | API, DB, 인증, 비즈니스 로직 | Generator | C07(ReBAC), C03(메타엣지) |
| qa-engineer | `agents/qa-engineer.md` | 정량 채점, 6-공간 리뷰, NOMIK | Evaluator | C11(NOMIK), C06(6분석공간) |
| devops-engineer | `agents/devops-engineer.md` | CI/CD, 인프라, 배포, 모니터링 | Generator | C13(레버 5속성), C15(능동메타데이터) |
| ontology-advisor | `agents/ontology-advisor.md` | SOS 방법론 컨설팅, 설계 리뷰 | Advisor | 전체 SOS 개념 |

## 팀 통신 프로토콜

에이전트들은 SendMessage로 직접 통신한다:
- **product-owner** → architect: 비즈니스 요구사항, 확장된 제품 스펙, 우선순위 전달
- **architect** 완료 → frontend에게 컴포넌트 구조/라우팅, backend에게 API/DB/인증, qa에게 기능 요구사항, devops에게 인프라 요구사항
- **qa** ↔ **개발자 전원**: Sprint Contract 협상 (구현 전)
- **frontend ↔ backend**: API 연동 중 실시간 소통
- **qa** → 해당 개발자: 채점 기반 🔴 필수 수정 요청 → 재작업 → 재채점 (임계값 통과까지, 최대 3라운드)
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
| 1 | 스펙 확장 + 시장/사업성 분석 | product-owner (Planner) | 없음 | `01_market_analysis.md` |
| 2 | 도메인 모델링 | architect (+ ontology-advisor) | 작업 1 | `02_domain_model.md` |
| 3 | 아키텍처/API/DB 설계 | architect | 작업 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

### Phase 2.5: Sprint Contract 협상 (NEW)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 3.5 | 성공 기준 사전 합의 | qa ↔ 개발자 전원 | 작업 3 | `03.5_sprint_contract.md` |

### Phase 3: 구현 (병렬)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 4a | 프론트엔드 개발 | frontend-dev | 작업 3, 3.5 | `src/` 프론트엔드 코드 |
| 4b | 백엔드 개발 | backend-dev | 작업 3, 3.5 | `src/` 백엔드 코드 |
| 4c | 배포 설정 | devops-engineer | 작업 3, 3.5 | `07_deploy_guide.md`, CI/CD 설정 |

### Phase 4: 채점 기반 검증 (Generator/Evaluator 루프)
| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 5 | Sprint Contract 기반 정량 채점 + 6-공간 리뷰 | qa-engineer | 4a, 4b | `06_test_plan.md`, `08_six_space_review.md`, `10_grade_report.md` |
| 5.1 | (FAIL 시) 수정 → 재구현 → 재채점 | qa ↔ 개발자 | 5 | 업데이트된 코드 + 채점 |
| 6 | 최종 리뷰 | product-owner + ontology-advisor | 5 (PASS 후) | `09_review_report.md` |

## 작업 규모별 모드

| 사용자 요청 | 실행 모드 | 투입 에이전트 | Sprint Contract |
|------------|----------|-------------|----------------|
| "웹앱 만들어줘", "SaaS 개발" | **풀 파이프라인** | 7명 전원 | 필수 |
| "API만 만들어줘" | **백엔드 모드** | product-owner + architect + backend + qa | 필수 |
| "프론트만 만들어줘" | **프론트 모드** | architect + frontend + qa | 필수 |
| "이 코드 리팩토링" | **리팩토링 모드** | architect + 해당 개발자 + qa | 선택 |
| "배포 설정만" | **DevOps 모드** | devops 단독 | 불필요 |
| "사업성 검토해줘" | **기획 모드** | product-owner 단독 | 불필요 |
| "도메인 모델링해줘" | **모델링 모드** | architect + ontology-advisor | 불필요 |
| "코드 리뷰해줘" | **리뷰 모드** | qa + ontology-advisor | 불필요 |
| "영향도 분석해줘" | **분석 모드** | qa 단독 (NOMIK) | 불필요 |

## 에러 핸들링

| 에러 유형 | 전략 |
|----------|------|
| 요구사항 모호 | 의미 강화(C10) 3단계로 확장: 어휘→의미→온톨로지 정렬 |
| 기술 스택 미지정 | 규모별 기본 스택 (MVP: Next.js + SQLite) |
| 빌드 에러 | 에러 로그 분석 → 해당 개발자 수정 → QA 재채점 |
| 에이전트 실패 | 1회 재시도 → 실패 시 해당 산출물 없이 진행 |
| 채점 FAIL | 구체적 수정 지시 → 재작업 → 재채점 (최대 3라운드) |
| 3라운드 후 FAIL | 현재 상태 + 미해결 사항을 리뷰 보고서에 명시 |
| 사업성 의문 | product-owner가 pivot 제안, 대안 방향 3가지 제시 |
| 컨텍스트 과부하 | Context Reset: 파일 기반 핸드오프 후 리셋 |
| Self-Eval Bias | Evaluator 독립 검증, Generator 자가 평가 거부 |

## 모델 최적화 (Opus 4.6)

Opus 4.6은 더 신중한 계획, 장기 에이전틱 작업 유지, 대규모 코드베이스 안정성을 제공한다.

- Sprint 과세분화 불필요 — 모델이 자체 계획 수립
- Evaluator는 Sprint 단위 대신 단계 완료 시점에 평가
- 하네스 복잡도는 모델이 못하는 것에만 투자: Self-Eval Bias 방지, 디자인 품질 채점

## 설계 참조

- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — Anthropic Engineering
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Anthropic Research
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI 슬롭 방지 디자인
- [Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — Context Reset 패턴
