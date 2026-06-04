# 수출바우처 컨설팅 완료보고서 — 에이전트 워크플로우 프레임워크

LLM 에이전트 팀으로 수출바우처 컨설팅 완료보고서를 작성하는 재사용 프레임워크입니다.
Claude Code에서 실행합니다.

---

## 시작하기

### 새 프로젝트

```bash
# 1. 프레임워크 복사
cp -r export_voucher_framework/ [새_프로젝트_폴더명]/
cd [새_프로젝트_폴더명]/

# 2. 소스 파일 추가
# 01_inputs/raw/ 에 PDF, DOCX, HWP 파일을 넣습니다

# 3. Claude Code 실행
claude

# 4. 온보딩 시작
/start
```

Orchestrator가 질문을 통해 나머지를 자동으로 처리합니다.

### 진행 중 프로젝트

```bash
cd [프로젝트_폴더]/
claude
/status   # 현재 상태 확인
```

---

## 에이전트 팀

| 에이전트 | 역할 |
|---|---|
| **Orchestrator** | 전체 관리, 온보딩, 에이전트 스폰, 승인 게이트 |
| **Planner** | 기존 보고서 진단 + 섹션 구조 제안 |
| **Researcher** | 외부 시장/규제/수요 조사 |
| **Analyst** | 조사 결과 통합 + 섹션별 작성 계획 |
| **Fact Checker** | 클레임/소스 품질 검증 |
| **Report Writer** | 한국어 보고서 작성 |
| **Style Editor** | 한국어 문체 정제 |
| **Reviewer** | 최종 QA |

---

## 폴더 구조

```
프로젝트_폴더/
├── CLAUDE.md              ← 항상 읽는 메인 파일 (온보딩 시 자동 완성)
├── .claude/commands/      ← /start, /status 커맨드
├── 00_project/
│   ├── project_brief.md   ← 계약 범위 + 섹션 구조 (온보딩 시 자동 완성)
│   ├── workflow.md        ← 품질 원칙 + 단계 (수정 금지)
│   ├── client_fact_brief.md  ← 클라이언트 팩트 (온보딩 시 자동 생성)
│   └── consulting_principles.md
├── 01_inputs/
│   ├── input_manifest.md  ← 소스 목록 (온보딩 시 자동 완성)
│   ├── 02_standard_report_outline.md
│   ├── raw/               ← 소스 파일 여기에 넣기
│   └── processed/         ← 자동 생성됨
├── 02_agents/             ← 에이전트 프롬프트 (수정 금지)
├── 03_outputs/            ← 모든 산출물
└── 04_handoff/
    ├── current_status.md  ← 현재 단계
    ├── decision_log.md    ← 승인된 결정
    └── open_questions.md  ← 미해결 질문
```

---

## 핵심 원칙

- **CLAUDE.md + current_status.md** — Orchestrator 기본 컨텍스트
- **workflow.md** — 품질 원칙의 단일 소스 (수정하지 않음)
- **Markdown-first** — 사용자 승인 전 DOCX 생성 금지
- **에이전트 스폰** — 각 에이전트는 독립 컨텍스트에서 실행

---

## 공유 가능성

| 분류 | 파일 |
|---|---|
| **GitHub 안전** | `workflow.md`, `consulting_principles.md`, `02_agents/` 전체, `README.md`, `.gitignore` |
| **템플릿** | `CLAUDE.md`, `project_brief.md`, `client_fact_brief.md`, `input_manifest.md` |
| **공유 불가** | `01_inputs/raw/`, `processed/`, `03_outputs/`, 채워진 `CLAUDE.md` 및 `client_fact_brief.md` |
