# Workflow

## 목적

이 파일은 워크플로우 단계 순서와 모든 에이전트에 적용되는 품질 원칙을 정의합니다.
프로젝트 범위는 `00_project/project_brief.md`, 소스 사용은 `01_inputs/input_manifest.md`,
클라이언트 팩트는 `00_project/client_fact_brief.md`에서 통제합니다.

---

## 워크플로우 단계

### 0. 프로젝트 설정 (온보딩)

CLAUDE.md가 비어 있으면 자동 트리거. `/start` 커맨드로 수동 실행 가능.

- 기본 정보 수집 (클라이언트명, 보고서 유형, 계약 범위, 목표 분량)
- `01_inputs/raw/` 파일 스캔 및 읽기
- `01_inputs/processed/` 변환본 자동 생성
- `00_project/client_fact_brief.md` 초안 작성
- `CLAUDE.md`, `project_brief.md`, `input_manifest.md` 자동 완성
- 사용자 승인 후 Planner 스폰

### 1. Orchestrator — 초기 플래닝
- 전체 작업 계획 제안
- 사용자 승인 대기

### 2. Planner
- Mode A (기존 보고서 개선): 현재 보고서 갭 진단 + 섹션 구조 제안
- Mode B (신규 작성 계획): 가용 소스 검토 + 섹션 구조 제안
- Orchestrator 검토 → 사용자 승인 → `project_brief.md` 섹션 구조 확정

### 3. Researcher
- Orchestrator가 정의한 조사 질문 기반으로 실행
- 병렬 또는 순차 실행 (Orchestrator가 태스크 브리프에 명시)

### 4. Fact Checker
- Researcher 및 Analyst 결과물의 주요 클레임/소스 품질 검증

### 5. Analyst
- 진단 + 조사 + 검증 결과 → 섹션별 작성 계획 + 증거-주장 매핑

### 6. Report Writer
- 한국어 Markdown 보고서 작성 (여러 패스 가능)
- Orchestrator가 패스별 태스크 브리프 생성

### 7. Reviewer
- 표준목차 정합성, 증거 품질, 문체, 범위 QA

### 8. Style Editor
- 한국어 문체 정제 (Reviewer QA 통과 후)

### 9. DOCX 변환
- 사용자 승인 후 최종 Markdown → DOCX 변환

---

## 핵심 품질 원칙

이 세 원칙은 모든 에이전트, 모든 단계에 적용됩니다.

### 원칙 1: Report Reality Principle

최종 보고서는 컨설팅 서비스가 수행된 완료 보고서로 읽혀야 합니다.

**요구되는 것:**
- 완료형 컨설팅 보고서 언어 사용: `조사하였다`, `검토하였다`, `분석하였다`, `도출하였다`
- 보고서가 컨설팅 수행 결과를 요약하는 것처럼 읽혀야 함

**금지되는 것:**
- 내부 검증 메모처럼 읽히는 언어
- 초안 생성 날짜, 소스 수리 날짜, 에이전트 프로세스 용어 노출
- `오픈 질문`, `Fact Check 2`, `source repair 기준` 등 내부 작업 용어를 보고서 본문에 노출
- 아직 진행 중인 것처럼 보고서를 묘사하는 언어

**경계:** 완료되지 않은 활동을 발명하지 않습니다. 바이어 미팅, 유통사 협의, 팝업 실행, 판매 성과 등은 확인된 증거가 있을 때만 기술합니다. 전략 권고와 로드맵 항목은 권고 사항이며 완료된 결과가 아닙니다.

---

### 원칙 2: Client Source and Citation Treatment Principle

클라이언트 제공 자료와 공식 제품 페이지는 회사/제품 정보 파악에 사용하되, 독립적인 제3자 증거처럼 APA 인용하지 않습니다.

**클라이언트/제품 정보에 선호하는 표현:**
- `참여기업 제공자료와 공식 제품 정보를 종합하면...`
- `제품 소개 자료에 따르면...`
- `공식 제품 정보에서 확인되는 주요 특징은...`

**외부 시장/규제/가격/트렌드 클레임:** 원래 출판사/소스에 APA 인용. 처리된 Markdown 파일을 원본인 것처럼 인용하지 않습니다.

---

### 원칙 3: Source Precedence Principle

내부 클라이언트 자료와 공식 공개 소스가 충돌할 때:

1. 현재 공개 사실은 공식 공개 소스 우선
2. 오래된 IR 덱, 신청서, 계획 자료는 역사적/내부 컨텍스트로만 사용
3. 확인되지 않은 충돌 정보를 현재 사실로 사용하지 않음
4. Orchestrator가 충돌을 분류: 공개 소스 사용 / 내부 소스를 역사적 컨텍스트로만 / 생략 / 사용자 확인 요청
5. Fact Checker와 Reviewer가 이 원칙 준수 여부를 명시적으로 확인

---

## Markdown-First 워크플로우

- 모든 작업 결과물은 Markdown으로 저장
- 최종 보고서도 Markdown으로 완성한 뒤, 사용자 승인 후 DOCX 변환
- PDF/DOCX/HWP 원본은 변환이 불명확하거나 이미지/표가 필요할 때만 참조
- 분석 단계에서 DOCX 초안 생성 금지

---

## APA 인용 규칙

- 외부 소스: APA 스타일 인용
- 본문 인용: `(Publisher, Year)` 또는 `(Publisher, n.d.)`
- 표/그림 출처: `출처: Publisher(Year), [수행기관명] 재구성`
- 참고문헌: `Publisher. (Year). Title. URL. 접속일: YYYY.MM.DD.`
- 내부 자료: `[클라이언트명]. (Year). [자료명]. 내부자료.`
- 처리된 Markdown 파일을 원본인 것처럼 인용하지 않음

---

## Approval Gates

사용자 승인이 필요한 시점:

- 컨설팅 목표 확정 또는 변경
- 주요 단계 전환 (플래닝 → 조사 → 작성 등)
- 보고서 범위, 목표 분량, 섹션 구조 변경
- 폴더/에이전트/워크플로우 추가
- 제외된 프레이밍 재도입 (예: 해외거래처발굴)
- 최종 Markdown 승인 전 DOCX 초안 생성

---

## Output Discipline

- `01_inputs/processed/` — 포맷 변환된 소스 (read-only)
- `03_outputs/` — 진단, 조사, 분석, 증거-주장 매트릭스, 초안, 리뷰, QA, 최종본
- `04_handoff/` — 현재 상태, 오픈 질문, 의사결정 로그
- 기존 파일 덮어쓰기 금지 — 버전 파일 생성
- 사용자가 명시적으로 DOCX 변환 승인 전까지 Markdown만 생성
