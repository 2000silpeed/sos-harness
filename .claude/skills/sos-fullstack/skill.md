---
name: sos-fullstack
description: "온톨로지 사고 기반 풀스택 개발 파이프라인. GAN 영감의 Generator/Evaluator 아키텍처로 에이전트 팀이 사업성→도메인모델링→설계→Sprint Contract→프론트→백엔드→채점 기반 검증→배포를 협업 수행한다. '웹앱 만들어줘', '서비스 개발', 'SaaS 개발', 'CRUD 앱', '대시보드', '관리자 페이지', '회원가입/로그인', 'REST API 개발', '풀스택 프로젝트', 'Next.js 앱', '서비스 기획' 등 웹 애플리케이션 개발 전반에 이 스킬을 사용한다. 모바일 앱(React Native/Flutter), 게임, ML/AI 모델 학습은 범위 밖이다."
---

# SOS Fullstack — 온톨로지 사고 기반 풀스택 개발

에이전트 팀이 온톨로지 방법론으로 사업성→도메인→설계→Sprint Contract→구현→채점 기반 검증→배포를 협업 수행한다.

## 핵심 차별점

일반 풀스택 하네스와의 차이:
- **도메인 모델이 먼저**: ERD/API 전에 온톨로지 4요소(클래스/속성/관계/공리) 정의
- **관계 기반 설계**: 모든 연결(FK, API, 컴포넌트 props)을 명시적 "관계"로 설계
- **메타엣지 의식**: 미들웨어/인터셉터를 "규칙의 규칙"으로 문서화
- **GAN 영감의 Generator/Evaluator**: 개발자(Generator)와 QA(Evaluator) 완전 분리, 정량 채점 루브릭으로 품질 보증
- **Sprint Contract**: 구현 전 성공 기준 사전 합의 → 기대치 불일치 방지
- **6-공간 리뷰**: 코드를 6차원으로 다각도 검증
- **사업성 검증**: 기술 전에 시장/수익성 판단
- **Context Reset**: 장시간 세션에서 컨텍스트 일관성 유지를 위한 구조화된 핸드오프

## 설계 참조

이 하네스의 아키텍처는 다음 자료에서 영감을 받았다:
- [Harness Design for Long-Running Apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) — GAN 패턴, Context Reset, Sprint Contract
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — 에이전트 오케스트레이션 패턴
- [Frontend Design Skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) — AI 슬롭 방지 디자인 가이드

## 실행 모드

**에이전트 팀** — 7명이 SendMessage로 직접 통신하며 교차 검증한다.

**역할 구분 (GAN 패턴)**:
- **Planner**: product-owner (1-4문장 → 포괄적 제품 스펙으로 확장)
- **Generator**: architect, frontend-dev, backend-dev, devops-engineer (설계 + 구현)
- **Evaluator**: qa-engineer (독립 평가, 정량 채점)
- **Advisor**: ontology-advisor (방법론 컨설팅, 코드 작성 안 함)

## 에이전트 구성

| 에이전트 | 파일 | 역할 | GAN 역할 |
|---------|------|------|---------|
| product-owner | `.claude/agents/product-owner.md` | 사업성 판단, 시장분석, GTM | Planner |
| architect | `.claude/agents/architect.md` | 온톨로지 도메인 모델링, 아키텍처 | Generator |
| frontend-dev | `.claude/agents/frontend-dev.md` | React/Next.js 프론트엔드 + 디자인 품질 | Generator |
| backend-dev | `.claude/agents/backend-dev.md` | API, DB, ReBAC 인증 | Generator |
| qa-engineer | `.claude/agents/qa-engineer.md` | 정량 채점, 6-공간 리뷰, NOMIK | Evaluator |
| devops-engineer | `.claude/agents/devops-engineer.md` | 레버 5속성 CI/CD | Generator |
| ontology-advisor | `.claude/agents/ontology-advisor.md` | SOS 방법론 컨설팅 | Advisor |

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
| 1 | 사용자 입력 → 포괄적 제품 스펙 확장 + 시장/사업성 분석 | product-owner (Planner) | 없음 | `01_market_analysis.md` |
| 2 | 도메인 모델링 + 리뷰 | architect + ontology-advisor | 작업 1 | `02_domain_model.md` |
| 3 | 아키텍처/API/DB 설계 | architect | 작업 2 | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md` |

**Planner 역할 강화**: product-owner는 사용자의 1-4문장 입력을 포괄적 제품 스펙으로 확장한다. 단, 구현 세부사항은 제외하고 "무엇을(What)" 수준에 집중하여, 캐스케이딩 오류를 방지한다.

**ontology-advisor**는 작업 2에서 architect의 도메인 모델을 리뷰한다.

### Phase 2.5: Sprint Contract 협상 (NEW)

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 3.5 | Sprint Contract 합의 | qa-engineer ↔ 개발자 전원 | 작업 3 | `_workspace/03.5_sprint_contract.md` |

architect의 설계 문서를 기반으로, QA(Evaluator)가 각 Generator에게 **성공 기준**을 제안한다:

```
## Sprint Contract — _workspace/03.5_sprint_contract.md

### 프론트엔드 성공 기준
| # | 요구사항 | 검증 방법 | 합격 조건 |
|---|---------|----------|----------|

### 백엔드 성공 기준
| # | 요구사항 | 검증 방법 | 합격 조건 |
|---|---------|----------|----------|

### 디자인 품질 기준
- 각 차원 최소 3/5, 평균 3.5/5

### DevOps 성공 기준
| # | 요구사항 | 검증 방법 | 합격 조건 |
|---|---------|----------|----------|
```

Generator들은 Contract에 동의하거나 수정을 요청할 수 있다. **합의 후 구현 시작**.

### Phase 3: 구현 (병렬)

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 4a | 프론트엔드 개발 | frontend-dev | 작업 3, 3.5 | `src/` 프론트엔드 코드 |
| 4b | 백엔드 개발 | backend-dev | 작업 3, 3.5 | `src/` 백엔드 코드 |
| 4c | 배포 설정 | devops-engineer | 작업 3, 3.5 | `07_deploy_guide.md`, CI/CD 설정 |

작업 4a, 4b, 4c는 **병렬 실행**. 모두 작업 3과 Sprint Contract(3.5)에 의존.

**소통 흐름:**
- architect 완료 → frontend에게 컴포넌트/라우팅, backend에게 API/DB/인증, devops에게 인프라, qa에게 요구사항
- frontend ↔ backend: API 연동 실시간 소통
- devops 완료 → 전체에게 환경변수/배포 URL

**Generator 자가 평가 금지**: 개발자는 "잘 됐다"고 자체 판단하지 않는다. 완료 시 QA에 제출만 한다.

### Phase 4: 채점 기반 검증 (Generator/Evaluator 루프)

| 순서 | 작업 | 담당 | 의존 | 산출물 |
|------|------|------|------|--------|
| 5 | Sprint Contract 기반 정량 채점 + 6-공간 리뷰 | qa-engineer (Evaluator) | 4a, 4b | `06_test_plan.md`, `08_six_space_review.md`, `_workspace/10_grade_report.md` |
| 5.1 | (FAIL 시) 수정 요청 → 재구현 → 재채점 | qa ↔ 해당 개발자 | 5 | 업데이트된 코드 + 채점 보고서 |
| 6 | 최종 리뷰 | product-owner | 5 (PASS 후) | `09_review_report.md` |

**채점 루프 상세:**
1. QA가 Sprint Contract 기준으로 각 차원 1-5점 채점
2. **PASS 조건**: 모든 차원 ≥ 3/5, 평균 ≥ 3.5/5, 🔴 항목 0개
3. **FAIL 시**: 구체적 수정 지시 → Generator 재작업 → QA 재채점
4. **안전장치**: 최대 3라운드. 3라운드 후에도 FAIL이면 현재 상태로 진행하되 리뷰 보고서에 미해결 사항 명시
5. **관대함 방지**: QA는 모든 채점에 구체적 관찰 근거를 반드시 기술. 1라운드에서 모든 항목 4-5점이면 기준을 한 단계 올려 재평가

**Playwright MCP 라이브 테스트 (가능 시):**
- QA가 Playwright MCP로 실제 브라우저에서 UI/API/반응형 검증
- 스크린샷 기반 시각적 품질 확인
- 사용 불가 환경에서는 코드 리뷰 + 빌드 확인으로 대체

### Phase 5: 최종 보고

1. 모든 산출물 확인
2. 🔴 필수 수정 반영 확인
3. 사용자에게 최종 요약:
   - 시장 분석 — `_workspace/01_market_analysis.md`
   - 도메인 모델 — `_workspace/02_domain_model.md`
   - 아키텍처 — `_workspace/03_architecture.md`
   - Sprint Contract — `_workspace/03.5_sprint_contract.md`
   - API 명세 — `_workspace/04_api_spec.md`
   - DB 스키마 — `_workspace/05_db_schema.md`
   - 테스트 계획 — `_workspace/06_test_plan.md`
   - 배포 가이드 — `_workspace/07_deploy_guide.md`
   - 6-공간 리뷰 — `_workspace/08_six_space_review.md`
   - 최종 리뷰 — `_workspace/09_review_report.md`
   - 채점 보고서 — `_workspace/10_grade_report.md`
   - 소스 코드 — `src/`

## Context Reset 프로토콜

장시간 세션에서 컨텍스트 윈도우가 채워지면 모델이 일관성을 잃거나, 작업을 조기 마무리하려는 "컨텍스트 불안(Context Anxiety)"이 발생한다.

**해결 전략: 파일 기반 구조화된 핸드오프**

1. **핸드오프 파일이 진실의 원천**: `_workspace/` 산출물이 에이전트 간 정보 전달의 핵심. 메시지 컨텍스트가 아님
2. **핸드오프 시점**: 각 Phase 완료 시. 이전 Phase의 산출물 파일이 다음 Phase의 입력
3. **Compaction보다 Reset**: 컨텍스트가 커지면 압축(compaction)보다 완전한 리셋 + 파일 기반 재시작이 더 안정적
4. **에이전트 독립성**: 각 에이전트는 자신의 입력 파일만 읽으면 작업 가능하도록 산출물이 자기완결적이어야 한다

### Phase별 입력 파일 매핑 (Context Reset 후 재시작 시)

| Phase | 에이전트 | 읽어야 할 파일 |
|-------|---------|--------------|
| 2 | product-owner | `00_input.md` |
| 2 | architect | `00_input.md`, `01_market_analysis.md` |
| 2.5 | qa-engineer | `03_architecture.md`, `04_api_spec.md` |
| 3 | frontend-dev | `03_architecture.md`, `03.5_sprint_contract.md` |
| 3 | backend-dev | `03_architecture.md`, `04_api_spec.md`, `05_db_schema.md`, `03.5_sprint_contract.md` |
| 3 | devops-engineer | `03_architecture.md`, `03.5_sprint_contract.md` |
| 4 | qa-engineer | `03.5_sprint_contract.md`, `src/` 코드, `03_architecture.md` |
| 5 | product-owner | `01_market_analysis.md`, `10_grade_report.md`, `08_six_space_review.md` |

이 매핑으로 Context Reset 후에도 각 에이전트가 최소한의 파일만 읽고 작업을 재개할 수 있다.

## 작업 규모별 모드

| 사용자 요청 | 실행 모드 | 투입 에이전트 | Sprint Contract |
|------------|----------|-------------|-----------------|
| "웹앱 만들어줘", "SaaS 개발" | **풀 파이프라인** | 7명 전원 | 필수 |
| "API만 만들어줘" | **백엔드 모드** | product-owner + architect + backend + qa | 필수 |
| "프론트만 만들어줘" (API 있음) | **프론트 모드** | architect + frontend + qa | 필수 |
| "이 코드 리팩토링" | **리팩토링 모드** | architect + 해당 개발자 + qa | 선택 |
| "배포 설정만" | **DevOps 모드** | devops 단독 | 불필요 |
| "사업성 검토해줘" | **기획 모드** | product-owner 단독 | 불필요 |
| "도메인 모델링해줘" | **모델링 모드** | architect + ontology-advisor | 불필요 |
| "코드 리뷰해줘" | **리뷰 모드** | qa + ontology-advisor | 불필요 |

**기존 코드 활용**: 기존 코드가 있으면 architect가 분석하여 확장 지점을 파악하고 필요한 에이전트만 투입.

## 데이터 전달 프로토콜

| 전략 | 방식 | 용도 |
|------|------|------|
| 파일 기반 | `_workspace/` + `src/` | 설계 문서 + 소스 코드 (진실의 원천) |
| 메시지 기반 | SendMessage | API 연동, 코드 리뷰, 수정 요청 |
| 태스크 기반 | TaskCreate/TaskUpdate | 진행 상황 추적 |

**핵심 원칙**: 파일이 진실의 원천이다. 메시지는 조정/알림용. 에이전트 간 정보는 반드시 파일로 전달해야 Context Reset에도 살아남는다.

## 갈등 해결 프로토콜

| 갈등 유형 | 해결 주체 | 절차 |
|----------|----------|------|
| Sprint Contract 합의 불성립 | 오케스트레이터 | Evaluator와 Generator 주장을 비교 → 오케스트레이터가 최종 결정 |
| Frontend ↔ Backend API 규격 불일치 | architect | architect가 API 명세(`04_api_spec.md`)를 기준으로 판정 |
| QA 채점에 Generator 이의 | 오케스트레이터 | Generator가 구체적 반론 제출 → 오케스트레이터가 채점 근거 검토 → 유지/수정 판단 |
| 사업 목표와 기술 제약 충돌 | product-owner | ROI 기반 트레이드오프 분석 → 우선순위에 따라 스코프 조정 |

## 에러 핸들링

| 에러 유형 | 전략 |
|----------|------|
| 요구사항 모호 | C10 의미 강화: 어휘확장→의미다층화→온톨로지정렬 |
| 기술 스택 미지정 | 규모별 기본 스택 (MVP: Next.js + SQLite) |
| 빌드 에러 | 에러 분석 → 해당 개발자 수정 → QA 재채점 |
| 에이전트 실패 | 1회 재시도 → 해당 산출물 없이 진행, 리뷰에 명시 |
| 채점 FAIL | 구체적 수정 지시 → Generator 재작업 → 재채점 (최대 3라운드) |
| 3라운드 후 FAIL | 현재 상태로 진행, 미해결 사항을 09_review_report에 명시 |
| 사업성 의문 | product-owner가 pivot/대안 3가지 제시 |
| 컨텍스트 과부하 | Context Reset: 산출물 파일 기반 핸드오프 후 리셋 |
| Self-Eval Bias | QA가 Generator의 자체 평가를 수용하지 않음, 독립 검증 |

## 모델 최적화 노트 (Opus 4.6)

Opus 4.6은 더 신중하게 계획하고, 에이전틱 작업을 더 오래 유지하며, 더 큰 코드베이스에서 안정적으로 작동한다.

**4.6 최적화:**
- Sprint 분해를 과도하게 세분화할 필요 없음 — 모델이 자체적으로 단계를 계획
- Evaluator가 Sprint 단위 대신 **단계 완료 시점**에 평가하는 것이 더 효과적
- 작업 복잡도 대비 모델 능력이 충분하면 Evaluator 없이도 가능 (DevOps 모드 등)
- 하네스 복잡도는 **모델이 못하는 것**에만 투자: Self-Evaluation Bias 방지, 디자인 품질 채점이 핵심

## 테스트 시나리오

### 정상 흐름
**프롬프트**: "반려동물 건강 관리 SaaS를 만들어줘. 보호자가 반려동물 건강 기록을 관리하고, 수의사와 공유할 수 있는 서비스"
**기대 결과**:
- Planner 확장: 1문장 → 16+ 기능 스펙 (건강기록, 예방접종, 공유, 알림, 대시보드 등)
- 시장 분석: 펫케어 시장 규모, 경쟁사(핏펫, 포인핸드 등), 수익모델
- 도메인 모델: 보호자/반려동물/건강기록/수의사 온톨로지 (클래스/관계/공리)
- Sprint Contract: 기능별 합격 기준 + 디자인 채점 기준 합의
- 아키텍처: Next.js + Prisma + PostgreSQL, ReBAC 기반 공유 권한
- 프론트: **AI 슬롭 없는** 대시보드, 건강 기록 CRUD, 수의사 공유 UI
- 백엔드: 인증 API, CRUD API, 관계 기반 공유 권한
- 채점: 정량 루브릭 기반 PASS/FAIL + 6-공간 리뷰
- 배포: Vercel + PlanetScale

### 기존 코드 확장
**프롬프트**: "이 Next.js 프로젝트에 결제 기능 추가해줘" + 기존 코드
**기대 결과**:
- architect가 기존 도메인 모델에 결제 온톨로지 추가
- Sprint Contract: 결제 플로우 성공 기준 합의
- backend가 결제 API 추가 (메타엣지: 결제 미들웨어)
- frontend가 결제 UI 추가
- qa가 결제 플로우 정량 채점 + 영향도 분석

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
