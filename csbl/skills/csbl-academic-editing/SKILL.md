---
name: csbl-academic-editing
description: >
  CSBL 연구실의 영어 연구 논문 원고(생물정보·약물·계산생물·대사공학)를 연구실 문체 규칙에 맞춰
  교정·검토한다. 규칙은 이상엽 교수 그룹 교신 논문 73편 문체 프로파일에서 만든 rule_id(CSBL-…)이고,
  새 원고의 목표값은 2019–2026 값이다. 모든 교정 제안·변경에 rule_id(CSBL-… 또는 manuscript_eval
  CORE-…·MOD-…)를 적고, 기계 검사 규칙은 lab-lint style/* 로 확인한다. "영어 교정", "문체 교정",
  "논리 교정", "lab style", "rule_id", "manuscript edit", "원고 영어 교정" 요청에 사용. 원고 전체 평가·
  심사 파이프라인은 manuscript_eval(mseval), 문체 추출·모방은 distill/recreate-writing-style과 섞지 말 것.
---

# csbl-academic-editing — CSBL 영어 원고 교정

정본: 포크 저장소 `csbl/skills/csbl-academic-editing/`(작업 사본 `~/my_projects/papers_style/fork-overlay/…`).
설치본: `~/.claude/skills/csbl-academic-editing/`, `~/.codex/skills/csbl-academic-editing/`. 설치본은 고치지 말고 정본을 고친 뒤 다시 복사한다(`references/integration.md`).

## 1. 무엇을 하나
- 이미 쓴 영어 원고의 **문장·단락·섹션 표현**을 연구실 규칙에 맞춘다. 결과·수치·인용·주장은 바꾸지 않는다(CSBL-INTEG-01).
- 모든 교정은 **변경 기록 표의 한 행**이 되고, 그 행에는 **rule_id가 반드시** 있다.
- 하지 않는 것: 새 실험·결과·인용 추가, 번역, 원고 전체 심사(→ manuscript_eval), 문체 프로파일 다시 만들기(→ papers_style).

## 2. 규칙과 목표값
- 규칙 목록: `references/rules.md`(사람용), `references/rules.json`(기계용 정본). 26개 = **기계 검사 10**(lab-lint `style/*`) + **사람 판단 16**.
- **목표값 = 2019–2026 값**(프로파일 31편). ALL(73편)·이전 연대 값은 비교용으로만 인용한다. 2019–2026 분리 값이 없는 규칙은 그렇다고 적혀 있다.
- 수치는 어휘·정규식 신호 집계이고 표본이 작다(그룹 5~8편). 목표값은 방향이지 할당량이 아니다. 문장을 수치에 맞추려고 억지로 바꾸지 않는다.
- 우선순위(높은 것부터): ① 연구 무결성(CSBL-INTEG-01, upstream universal integrity) ② 확인된 원고 사실·저자 지시 ③ 대상 저널 규정(CSBL-UNIT-01) ④ manuscript_eval 핵심 기준(`CORE-…`) ⑤ 분야 점검(`references/domain-overlay-bio.md`) ⑥ CSBL 문체 규칙. 같은 층에서 부딪히면 고르지 말고 충돌로 보고한다.

| rule_id | 한 줄 | 종류 |
|---|---|---|
| CSBL-FIG-01 | 그림·표 참조는 괄호로, 서술형(as shown in Fig.) 금지 | 기계 |
| CSBL-BOOST-01 | 우선권·감탄 부스터 금지 | 기계 |
| CSBL-SIG-01 | significant는 통계 근거와 같은 문장에서만 | 기계 |
| CSBL-STOCK-01 | 빈 상투구 삭제(It should be noted that은 예외) | 기계 |
| CSBL-RES-01 | 결과 단락을 We로 바로 열지 않음 | 기계 |
| CSBL-ABS-01 | 초록 목적 문장(Here, we …) | 기계 |
| CSBL-ABS-02 | 초록 분량(저널 한도 우선) | 기계(info) |
| CSBL-TITLE-01 | 의문형 제목 금지 | 기계 |
| CSBL-LANG-01 | 미국식·영국식 철자 혼용 금지 | 기계 |
| CSBL-EDIT-01 | 변경 기록의 모든 행에 rule_id | 기계(error) |
| CSBL-RES-02 | 결과 단락 첫 문장 = 목적·근거·순서 | 판단 |
| CSBL-RES-03 | 결과 단락 끝 = 요약·추론 또는 수치 | 판단 |
| CSBL-RES-04 | 주절 단순, 조건·수치는 괄호, respectively | 판단 |
| CSBL-RES-05 | 구체 보고 동사, 해석 주어는 These results | 판단 |
| CSBL-HEDGE-01 | 헤지는 suggest·indicate 중심, 강도는 유지·약화만 | 판단 |
| CSBL-HEDGE-02 | 예측 결과는 검증 전 demonstrate·confirm 금지 | 판단 |
| CSBL-VOICE-01 | 섹션별 태·인칭(방법 수동, 초록·고찰 능동 허용) | 판단 |
| CSBL-INTRO-01 | 서론 4~5단락 깔때기, 목적은 마지막 단락 | 판단 |
| CSBL-ABS-03 | 초록 구성: 배경→목적→수단→결과→함의 | 판단 |
| CSBL-DISC-01 | 고찰 첫머리 연구 요약 | 판단 |
| CSBL-DISC-02 | 한계는 후반, Although·It should be noted that | 판단 |
| CSBL-TITLE-02 | 11~12단어 명사구 제목 | 판단 |
| CSBL-SENT-01 | 40단어 넘는 문장은 구조 점검 | 판단 |
| CSBL-CONN-01 | These/This 이어받기, 나열 연결어 남용 금지 | 판단 |
| CSBL-UNIT-01 | 단위·철자·Fig. 표기는 저널 양식 | 판단 |
| CSBL-INTEG-01 | 의미·수치·인용·주장 강도 보존 | 판단 |

## 3. 작업 순서
1. **범위 확인**: 원고 파일, 대상 저널, 교정 범위(전체/섹션/코멘트 지정)를 확인한다. 저널 규정이 있으면 먼저 읽는다(CSBL-UNIT-01).
2. **기계 검사 먼저**: `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json --manuscript <원고.md|.docx>`. 원고는 기밀로 보고 **실행할 때부터 `--redact --json`**을 붙인다. 결과는 코드별 개수이고, 코드는 `references/rule-map.md`의 lint 열로 rule_id에 대응한다. 해당 섹션은 `references/checklist.md`를 따라 원고에서 직접 찾는다. 경고라도 문맥상 맞는 표현이면 고치지 않고 기록에 이유를 적는다.
3. **판단 규칙 적용**: `references/checklist.md` 순서(제목·초록 → 서론 → 결과 → 고찰·결론 → 방법)로 읽고, 바꿀 곳마다 해당 rule_id를 정한다. 표현 예시는 `references/before-after.md`, 분야별 변형은 `references/domain-overlay-bio.md`.
4. **변경 기록**: 파일 이름에 `edits`가 들어간 마크다운(예: `english-logic-edits.md`)에 아래 열을 가진 표로 적는다. 첫 열 `edit_id`(또는 표 바로 위 `<!-- csbl:edit-log -->`)가 변경 기록 표 표시라 파일 이름과 무관하게 검사된다.

   | edit_id | 위치 | 원문(요지) | 수정(요지) | rule_id | 이유 |
   |---|---|---|---|---|---|

   - rule_id는 하나 이상: `CSBL-…`(이 스킬), 또는 manuscript_eval `CORE-…`·`MOD-…`(문법·오탈자·약어처럼 이 스킬에 없는 것, 예: CORE-LANG-05·06). 여러 개면 쉼표로.
   - 어떤 규칙에도 해당하지 않으면 **고치지 않고** 저자 질문으로 남긴다.
5. **검증**: `lab-lint --no-network --redact --json <변경 기록.md>`에서 `style/edit-rule-id` 오류 0, 수정본에 다시 `lab-lint --no-network --redact --json --manuscript <수정본>`. 새 숫자·인용·주장 강화가 없는지 원문과 대조한다(CSBL-INTEG-01).

## 4. 지키는 것
- 원고 내용(결과·수치·고유명사·인용)은 바꾸지 않는다. 주장은 유지하거나 약화만 한다.
- 다른 논문·코퍼스 문장을 옮겨 쓰지 않는다. 표현 예시는 `before-after.md`처럼 직접 만든 문장만 쓴다. 코퍼스 구는 8단어 이하로만 인용한다.
- manuscript_eval 안에서 쓸 때는 그 폴더의 하드 게이트(원고 기밀 경계·입력 불변·날조 금지)가 이 스킬보다 앞선다.
- 원고·교정 기록에 lab-lint를 돌릴 때는 **실행할 때부터** `--redact --json`을 쓴다(화면·도구 응답·로그·저장 모두 수준·코드·파일·개수만). `--redact` 없는 기본 출력은 기존 text/* 검사가 원고 수치·문구를 위치 칸에 내므로 원고에 쓰지 않는다.
- 교정 결과를 "최종"이라 부르지 않는다. 검수는 다른 세션이 한다.

## 5. 참고 파일
| 파일 | 내용 |
|---|---|
| `references/rules.md` · `rules.json` | 규칙 정본(목표값·비교값·근거·lint 코드) |
| `references/rule-map.md` | rule_id ↔ manuscript_eval rubric ↔ 규칙집 대응 |
| `references/style-profile.md` | 프로파일 요약(2019–2026 목표값 중심) |
| `references/checklist.md` | 섹션별 점검표 |
| `references/before-after.md` | 직접 만든 교정 예시 |
| `references/domain-overlay-bio.md` | 생물정보·약물·계산생물 변형 |
| `references/integration.md` | 설치·manuscript_eval·~/projects/papers·lab-lint 연결 |

출처·라이선스: 포크 저장소 `csbl/NOTICE.md`.
