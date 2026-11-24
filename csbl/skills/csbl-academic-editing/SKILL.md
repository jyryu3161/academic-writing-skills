---
name: csbl-academic-editing
description: >
  CSBL 연구실의 영어 연구 논문 원고(생물정보·약물·계산생물·대사공학)를 연구실 문체 규칙에 맞춰
  교정·검토한다. 규칙은 이상엽 교수 그룹 교신 논문 73편 문체 프로파일에서 만든 rule_id(CSBL-…)이고,
  새 원고의 목표값은 2019–2026 값이다. 모든 교정 제안·변경에 rule_id(CSBL-… 또는 manuscript_eval
  CORE-…·MOD-…)를 적고, 기계 검사 규칙은 lab-lint style/* 로 확인한다. 초록·서론·방법·결과·고찰·결론과 그림·표 범례를 파트별 문체에 맞춰
  문장·문단 품질 점수 루프(통과 ≥ 4.0, 각 존재 파트 커버리지 100%)로 돌린다. "영어 교정", "문체 교정", "논리 교정",
  "lab style", "rule_id", "manuscript edit", "원고 영어 교정", "quality score" 요청에 사용. 원고 전체
  평가·심사 파이프라인은 manuscript_eval(mseval), 문체 추출·모방은 distill/recreate-writing-style과
  섞지 말 것.
---

# csbl-academic-editing — CSBL 영어 원고 교정

정본: 포크 저장소 `csbl/skills/csbl-academic-editing/`(작업 사본 `~/my_projects/papers_style/fork-overlay/…`).
설치본: `~/.claude/skills/csbl-academic-editing/`, `~/.codex/skills/csbl-academic-editing/`. 설치본은 고치지 말고 정본을 고친 뒤 다시 복사한다(`references/integration.md`).

## 1. 무엇을 하나
- 이미 쓴 영어 원고의 **문장·단락·섹션 표현과 문단 내부 구조**를 연구실 규칙에 맞춘다. 결과의 **사실**·수치·인용·주장 **강도**는 바꾸지 않는다(CSBL-INTEG-01). 표현과 구조는 점수 임계에 오를 때까지 적극적으로 고친다(CSBL-PROSE-01, CSBL-SCORE-01).
- 모든 교정은 **변경 기록 표의 한 행**이 되고, 그 행에는 **rule_id가 반드시** 있다.
- 하지 않는 것: 새 실험·결과·인용 추가, 번역, 원고 전체 심사(→ manuscript_eval), 문체 프로파일 다시 만들기(→ papers_style).

## 2. 규칙과 목표값
- 규칙 목록: `references/rules.md`(사람용), `references/rules.json`(기계용 정본). 31개 = **기계 검사 11**(lab-lint `style/*`) + **사람 판단 20**.
- **목표값 = 2019–2026 값**(프로파일 31편). ALL(73편)·이전 연대 값은 비교용으로만 인용한다. 2019–2026 분리 값이 없는 규칙은 그렇다고 적혀 있다.
- 수치는 어휘·정규식 신호 집계이고 표본이 작다(그룹 5~8편). 문장 길이·수동태·헤지 빈도 같은 **계량 목표값**은 방향이지 할당량이 아니다. 그 수치에 맞추려고 문장을 억지로 바꾸지 않는다. 이 문장은 언어 품질 점수(CSBL-SCORE-01)에는 적용하지 않는다. 품질 점수가 임계 미만이면 계량 목표와 무관하게 재작성한다.
- 우선순위(높은 것부터): ① 연구 무결성(CSBL-INTEG-01, 사실은 보존·표현은 개선) ①-b 언어 품질 루프(CSBL-PROSE-01, CSBL-SCORE-01, CSBL-COVER-01, CSBL-PART-01) ② 확인된 원고 사실·저자 지시 ③ 대상 저널 규정(CSBL-UNIT-01) ④ manuscript_eval 핵심 기준(`CORE-…`) ⑤ 분야 점검(`references/domain-overlay-bio.md`) ⑥ 그 밖의 CSBL 문체 규칙. 같은 층에서 부딪히면 고르지 말고 충돌로 보고한다.

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
| CSBL-SENT-01 | 40단어 초과·논리·명확 미달 문장은 구조 점검 | 판단 |
| CSBL-CONN-01 | These/This 이어받기, 나열 연결어 남용 금지 | 판단 |
| CSBL-UNIT-01 | 단위·철자·Fig. 표기는 저널 양식 | 판단 |
| CSBL-INTEG-01 | 사실은 보존, 표현·문단 내부 구조는 적극 개선 | 판단 |
| CSBL-PROSE-01 | 모든 파트·범례를 해당 문체에 맞게 적극 재작성 | 판단 |
| CSBL-SCORE-01 | 문장·문단 점수 임계(≥ 4.0)까지 최대 3루프 | 판단 |
| CSBL-COVER-01 | 모든 본문 파트·범례 채점 100%·합격 100% | 기계(error) |
| CSBL-PART-01 | 파트별 기대 문체로 채점·교정, 일부 파트만 손보면 불합격 | 판단 |
| CSBL-LEGEND-01 | 그림·표 범례는 간결한 명사구·짧은 절, 긴 논의 금지 | 판단 |

## 2.1 파트별 기대 문체
교정·채점은 파트 단위다(CSBL-PART-01). 자세한 앵커는 `references/quality-score.md`에 있다.

| 파트 | 기대의 요지 |
|---|---|
| Abstract | 간결, 인용 없음이 기본, 배경→목적→수단→결과→함의 |
| Introduction | 깔때기, 일반 사실은 현재, 목적은 마지막 단락 |
| Methods | 과거 시제, 수동태 허용, we는 거의 없음 |
| Results | 목적·근거로 열고 보고 동사, 중간 문장도 같은 기준으로 |
| Discussion | 요지로 열고 해석·문헌 비교, 한계는 후반, 강도 유지·약화만 |
| Conclusions | 간결한 재진술, 새 결과·새 수치 없음 |
| Figure/Table legend | 간결한 명사구·짧은 절, 조건·n·통계, 긴 논의는 본문 |

일부 파트만 수정하고 나머지를 얕게 두면 불합격이다.

## 3. 작업 순서
1. **범위 확인**: 원고 파일, 대상 저널, 교정 범위(전체/섹션/코멘트 지정)를 확인한다. 저널 규정이 있으면 먼저 읽는다(CSBL-UNIT-01).
2. **기계 검사 먼저**: `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json --manuscript <원고.md|.docx>`. 원고는 기밀로 보고 **실행할 때부터 `--redact --json`**을 붙인다. 결과는 코드별 개수이고, 코드는 `references/rule-map.md`의 lint 열로 rule_id에 대응한다. 해당 섹션은 `references/checklist.md`를 따라 원고에서 직접 찾는다. 기계 경고가 문맥상 맞는 **표기**이면 고치지 않고 기록에 이유를 적는다. 이 예외는 언어 품질 미달(모호·장황·연결 불명)에는 쓰지 않는다.
3. **판단 규칙 적용**: `references/checklist.md` 순서(제목·초록 → 서론 → 결과 → 고찰·결론 → 방법)로 읽고, 바꿀 곳마다 해당 rule_id를 정한다. 초록·서론·방법·결과·고찰·결론과 그림·표 범례의 본문 단락을 빠짐없이 읽고, 각 파트 기대 문체(`references/quality-score.md`)에 맞춘다. 일부 파트만 손보고 나머지를 얕게 두지 않는다(CSBL-PART-01, CSBL-COVER-01). 표현 예시는 `references/before-after.md`, 분야별 변형은 `references/domain-overlay-bio.md`.
4. **변경 기록**: 파일 이름에 `edits`가 들어간 마크다운(예: `english-logic-edits.md`)에 아래 열을 가진 표로 적는다. 첫 열 `edit_id`(또는 표 바로 위 `<!-- csbl:edit-log -->`)가 변경 기록 표 표시라 파일 이름과 무관하게 검사된다.

   | edit_id | 위치 | 원문(요지) | 수정(요지) | rule_id | 이유 |
   |---|---|---|---|---|---|

   - rule_id는 하나 이상: `CSBL-…`(이 스킬), 또는 manuscript_eval `CORE-…`·`MOD-…`. 문법·오탈자·약어는 예: CORE-LANG-05·06. 문단 주제문·연결·역개요는 CORE-LANG-09–13도 근거로 쓸 수 있다. 여러 개면 쉼표로.
   - **사실 공란**(없는 수치·새 인용·새 비교·새 결과 주장)만 고치지 않고 저자 질문으로 남긴다. 문법적으로 틀리지 않아도 모호·장황·연결 불명·문체 미달은 CSBL-PROSE-01(및 해당 문체 규칙)으로 **반드시 고친다.**
5. **채점 루프**: `references/quality-score.md`와 `references/score-loop.md`를 따른다. 존재하는 모든 본문 파트와 그림·표 범례를 100% 채점하고, 임계 미달 단락은 최대 3번까지 다시 고친다(CSBL-SCORE-01, CSBL-COVER-01, CSBL-PART-01).
6. **검증**: `lab-lint --no-network --redact --json <변경 기록.md>`에서 `style/edit-rule-id` 오류 0, 수정본은 같은 폴더의 `quality-coverage.json`과 함께 `lab-lint --no-network --redact --json --manuscript --require-score-coverage <수정본>`. 모든 존재 파트·범례의 커버리지 100%·문단 합격을 확인하고, 새 숫자·인용·주장 강화가 없는지 원문과 대조한다(CSBL-INTEG-01, CSBL-COVER-01).

## 4. 지키는 것
- 원고의 **사실**(결과의 수치·방향·고유명사·인용)은 바꾸지 않는다. 주장 강도는 유지하거나 약화만 한다. 같은 단락 안의 표현·문장 구조는 점수 임계까지 적극적으로 고친다.
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
| `references/quality-score.md` | 문장·문단 품질 점수 차원·앵커·임계 |
| `references/score-loop.md` | 품질 루프·커버리지·검수 채점 |
| `references/integration.md` | 설치·manuscript_eval·~/projects/papers·lab-lint 연결 |

출처·라이선스: 포크 저장소 `csbl/NOTICE.md`.
