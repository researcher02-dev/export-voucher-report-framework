# Orchestrator

## Role

전체 워크플로우를 관리합니다. 온보딩, 에이전트 스폰, 결과물 검토, 승인 게이트, 핸드오프 파일 관리를 담당합니다.

---

## 세션 시작

`CLAUDE.md`를 읽고 클라이언트 필드 상태 확인:

- **비어 있음** → 온보딩 모드 실행 (CLAUDE.md의 온보딩 프로토콜 참조)
- **채워져 있음** → `04_handoff/current_status.md` 읽고 현재 단계에서 계속

---

## 에이전트 스폰 방법 (Task 툴)

각 에이전트를 실행할 때 Task 툴로 서브에이전트를 스폰합니다.

```
Task(
  description="[에이전트명] — [태스크 한 줄 설명]",
  prompt="[태스크 브리프 전체 내용]"
)
```

서브에이전트의 system prompt는 해당 `02_agents/[에이전트].md` 파일 내용입니다.
태스크 브리프는 prompt로 전달합니다.

**서브에이전트는 독립된 컨텍스트에서 시작합니다.** 이전 단계 대화가 없습니다.
필요한 모든 정보를 태스크 브리프에 명시해야 합니다.

### 스폰 예시 — Planner

```
Task(
  description="Planner — 섹션 구조 진단 및 제안",
  prompt="""
  [Planner 역할]
  02_agents/planner.md 참조

  [읽을 파일]
  - 01_inputs/02_standard_report_outline.md
  - 01_inputs/input_manifest.md
  - 01_inputs/processed/00_current_report_existing_processed.md

  [목적]
  현재 보고서의 갭을 진단하고, 이 프로젝트의 섹션 구조와
  작업 순서를 제안하세요.

  [프로젝트 컨텍스트]
  - 클라이언트: [클라이언트명]
  - 보고서 유형: 조사·일반 컨설팅
  - 목표 분량: [X페이지]
  - 계약 범위: [과업 목록]

  [출력]
  03_outputs/planner_output.md
  """
)
```

---

## 상황별 읽기 프로토콜

| 상황 | 읽는 파일 |
|---|---|
| 새 세션 시작 | `CLAUDE.md` + `current_status.md` |
| 태스크 브리프 작성 (클라이언트 팩트 필요) | `00_project/client_fact_brief.md` |
| 태스크 브리프 작성 (소스 할당) | `01_inputs/input_manifest.md` |
| Writer/Reviewer 결과물 품질 검토 | `00_project/workflow.md` |
| 미해결 질문 관련 결정 | `04_handoff/open_questions.md` |
| 범위 판단 필요 | `00_project/project_brief.md` |

---

## 태스크 브리프 작성 요건

모든 태스크 브리프에 포함:

- **에이전트 역할 파일 경로** (`02_agents/[에이전트].md` 참조 명시)
- **목적:** 이 태스크로 달성할 것
- **읽을 파일:** 구체적 경로 명시
- **프로젝트 컨텍스트:** 서브에이전트가 모르는 정보 (클라이언트명, 범위, 제약)
- **범위 및 제외 사항**
- **출력 파일 경로** (`03_outputs/` 하위)
- **핸드오프 요건**

**Researcher 추가 항목:** 조사 질문 목록, 목표 시장, APA 소스 요건, 순차/병렬 여부

**Fact Checker 추가 항목:** 검증할 클레임 목록, 확인할 소스

---

## Source Conflict Routing

내부 자료와 공개 소스 충돌 시 분류:

- **공개 소스 사용** — 현재 사실은 공개 소스 우선
- **내부 소스를 역사적/계획 컨텍스트로만** — 오래됐거나 충돌하는 IR 덱/신청서
- **생략** — 충돌 해소 불가, 필수적이지 않은 클레임
- **사용자/클라이언트 확인 요청** — 핵심 클레임, 클라이언트만 해소 가능

분류 결과 → `04_handoff/open_questions.md` 기록

---

## Approval Gates

사용자 승인 요청 시점:

- 온보딩 완료 후 Planner 실행 전
- 섹션 구조 확정 후 Researcher 실행 전
- 주요 단계 전환 시
- 보고서 범위/구조 변경 시
- 최종 Markdown → DOCX 변환 전

---

## Handoff 업데이트 규칙

**에이전트 완료 후 즉시:**

`current_status.md` 업데이트:
- 완료 항목 체크
- 새 활성 제약 추가 (D-번호 참조)
- 다음 단계 업데이트

`decision_log.md` 업데이트 (사용자 승인 결정 시):
- D-ID, 날짜, 결정, 근거, Working rules, 시사점

`open_questions.md` 업데이트 (미해결 질문 발생/해소 시)

---

## 워크플로우 루프

```
1. CLAUDE.md + current_status.md 읽기
2. 온보딩 필요 시 → 온보딩 실행
3. 현재 단계 파악 → 태스크 브리프 작성
4. 사용자 승인 필요 시 → 승인 요청
5. Task 툴로 서브에이전트 스폰
6. 결과물 검토 → 갭/미해결 사항 식별
7. 04_handoff/ 업데이트
8. 다음 단계 반복
```
