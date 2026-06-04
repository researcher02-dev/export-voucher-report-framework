# Input Manifest

<!-- 프로젝트 시작 시 채웁니다. 소스 추가/변경 시 업데이트합니다. -->
<!-- 소스 사용 규칙의 소스 오브 트루스입니다. -->

## 목적

이 파일은 소스 우선순위, 파일 역할, 사용 방법, 소스 해석 주의사항을 통제합니다.
워크플로우 규칙은 `00_project/workflow.md`에서 통제합니다.

모든 `01_inputs/` 파일은 read-only입니다.

---

## 소스 우선순위

1. [예: 현재 보고서 요약본 (`processed/01_current_report_summary_processed.md`)]
2. [예: 기존 보고서 (`processed/00_current_report_existing_processed.md`)]
3. [예: 주요 클라이언트 소스 — IR 덱, 신청서, 제품 소개]
4. [예: 보조 증거 — FGI/팝업 레퍼런스]
5. [예: 표준/참조 소스 — 표준목차, 벤치마크]
6. [예: 역사적/보조 소스 — 과거 진단 보고서]
7. [예: 재무 증거 — 재무제표]
8. [예: 배경 소스 — 오래된 투자 보고서]

---

## Raw 소스

| 파일 | 내용 | 사용 방법 | 우선순위 | 주의사항 |
|---|---|---|---|---|
| `raw/current_report.pdf` | 기존 보고서 | processed 버전으로 접근 | 최고 | |
| `raw/[IR_파일명]` | IR 덱 | processed 버전으로 접근 | 높음 | 버전별 충돌 주의 |
| `raw/[신청서]` | 사업 신청서 | 안정적 팩트와 계획/전망 구분 | 높음 | 계획은 확인 필요 |
| `raw/accepted_benchmark.pdf` | 합격 기준 벤치마크 | 패키징/섹션 흐름 참조만 | 참조 | 페이지 수 벤치마크로 사용 금지 |

---

## Processed 소스

| 파일 | 내용 | 사용 방법 |
|---|---|---|
| `processed/00_current_report_existing_processed.md` | 기존 보고서 변환본 | 보고서 진단 및 개선의 기준 |
| `processed/01_current_report_summary_processed.md` | 보고서 요약본 변환본 | 스토리라인 가이드 |
| `processed/02_standard_report_outline.md` | 표준목차 변환본 | 구조/컴플라이언스 참조 |
| `processed/accepted_benchmark.md` | 벤치마크 변환본 | 패키징·섹션 흐름 참조 (페이지 수 제외) |
| `processed/[IR_다이제스트].md` | IR 덱 핵심 요약 | 클라이언트 팩트 확인 |
| `processed/[신청서_processed].md` | 신청서 변환본 | 안정적 팩트 및 계획 확인 |

---

## 표준/참조 소스

| 파일 | 내용 | 사용 방법 | 주의사항 |
|---|---|---|---|
| `02_standard_report_outline.md` | 표준목차 원본 | 섹션 구조 및 필수항목 확인 | 수정 금지 |

---

## Legacy / 미할당 소스

| 파일 | 내용 | 사용 방법 |
|---|---|---|
| [이전 프로젝트 파일이 있다면 여기 기록] | | 현재 프로젝트에 사용 금지 |

---

## 소스 해석 주의사항

- 오래된 IR 덱, 신청서의 계획·전망은 확인되지 않는 한 현재 사실로 사용하지 않습니다
- IR 덱 간 충돌이 있으면 충돌을 유지하고 `open_questions.md`에 기록합니다
- 공개 소스와 내부 자료가 충돌하면 `workflow.md`의 Source Precedence Principle을 따릅니다
- 벤치마크 보고서는 페이지 수 기준으로 사용하지 않습니다
- 소스 수리/접근 날짜는 보고서 본문이 아닌 APA 레퍼런스 리스트에만 기재합니다
