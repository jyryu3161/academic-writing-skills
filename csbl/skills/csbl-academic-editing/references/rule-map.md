# rule-map — rule_id ↔ manuscript_eval rubric ↔ 규칙집 (rules.json에서 생성)

- `CORE-…`: `~/my_projects/manuscript_eval/rubrics/core/*.yaml`의 rubric_id(읽기만, 존재 확인됨).
- `upstream:`: WenyuChiou/academic-writing-skills(MIT) 파일 경로(포크 저장소 루트 기준).
- `rpws:`: Master-cai/Research-Paper-Writing-Skills(MIT) — manuscript_eval `vendor/research-paper-writing-skills/` 사본 기준 경로.
- 대응은 '같은 문제를 다룬다'는 뜻이다. 규칙집 문장을 옮겨 오지 않았다.

| rule_id | 종류 | lint | manuscript_eval rubric | 규칙집 |
|---|---|---|---|---|
| CSBL-FIG-01 | 기계 | style/figref-narrative | CORE-RES-02, CORE-FIG-02 | upstream:skills/academic-writing-skills/references/figures-tables-and-supplements.md<br>rpws:research-paper-writing/references/experiments.md |
| CSBL-BOOST-01 | 기계 | style/priority-booster | CORE-LANG-24 | upstream:skills/academic-writing-skills/references/banned_words.md<br>upstream:skills/academic-writing-skills/references/universal-integrity.md |
| CSBL-SIG-01 | 기계 | style/significant-no-stat | CORE-LANG-08 | upstream:skills/academic-writing-skills/references/results-and-explanation.md |
| CSBL-STOCK-01 | 기계 | style/stock-phrase | CORE-LANG-10 | upstream:skills/academic-writing-skills/references/banned_words.md<br>upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-RES-01 | 기계 | style/results-we-opening | CORE-RES-02, CORE-LANG-09 | upstream:skills/academic-writing-skills/references/results-and-explanation.md |
| CSBL-ABS-01 | 기계 | style/abstract-purpose | CORE-ABS-01, CORE-ABS-03 | upstream:skills/academic-writing-skills/references/conclusion-and-abstract.md<br>rpws:research-paper-writing/references/abstract.md |
| CSBL-ABS-02 | 기계 | style/abstract-length | CORE-ABS-08 | upstream:skills/academic-writing-skills/references/conclusion-and-abstract.md |
| CSBL-TITLE-01 | 기계 | style/title-question | CORE-ABS-07 | upstream:skills/academic-writing-skills/references/conclusion-and-abstract.md |
| CSBL-LANG-01 | 기계 | style/spelling-mix | CORE-LANG-01 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-EDIT-01 | 기계 | style/edit-rule-id | — | upstream:skills/academic-writing-skills/references/comment-scoped-revision.md |
| CSBL-RES-02 | 판단 | — | CORE-RES-02, CORE-LANG-09 | upstream:skills/academic-writing-skills/references/results-and-explanation.md<br>rpws:research-paper-writing/references/experiments.md |
| CSBL-RES-03 | 판단 | — | CORE-RES-02, CORE-DISC-04 | upstream:skills/academic-writing-skills/references/results-and-explanation.md |
| CSBL-RES-04 | 판단 | — | CORE-LANG-10 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-RES-05 | 판단 | — | CORE-LANG-11 | upstream:skills/academic-writing-skills/references/results-and-explanation.md |
| CSBL-HEDGE-01 | 판단 | — | CORE-LANG-20, CORE-DISC-04 | upstream:skills/academic-writing-skills/references/universal-integrity.md |
| CSBL-HEDGE-02 | 판단 | — | CORE-DISC-04 | upstream:skills/academic-writing-skills/references/universal-integrity.md |
| CSBL-VOICE-01 | 판단 | — | CORE-LANG-18, CORE-LANG-19 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-INTRO-01 | 판단 | — | CORE-INTRO-08, CORE-INTRO-03, CORE-INTRO-12 | upstream:skills/academic-writing-skills/references/introduction-and-study-context.md<br>rpws:research-paper-writing/references/introduction.md |
| CSBL-ABS-03 | 판단 | — | CORE-ABS-03, CORE-ABS-05, CORE-ABS-10 | rpws:research-paper-writing/references/abstract.md<br>upstream:skills/academic-writing-skills/references/conclusion-and-abstract.md |
| CSBL-DISC-01 | 판단 | — | CORE-DISC-01, CORE-DISC-05 | upstream:skills/academic-writing-skills/references/discussion-and-limitations.md<br>rpws:research-paper-writing/references/conclusion.md |
| CSBL-DISC-02 | 판단 | — | CORE-DISC-02 | upstream:skills/academic-writing-skills/references/discussion-and-limitations.md |
| CSBL-TITLE-02 | 판단 | — | CORE-ABS-07, CORE-ABS-09 | upstream:skills/academic-writing-skills/references/conclusion-and-abstract.md |
| CSBL-SENT-01 | 판단 | — | CORE-LANG-14, CORE-LANG-15, CORE-LANG-16 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-CONN-01 | 판단 | — | CORE-LANG-10, CORE-LANG-22, CORE-LANG-23 | rpws:research-paper-writing/references/does-my-writing-flow-source.md |
| CSBL-UNIT-01 | 판단 | — | CORE-LANG-01, CORE-LANG-07 | upstream:skills/academic-writing-skills/references/figures-tables-and-supplements.md |
| CSBL-INTEG-01 | 판단 | — | CORE-DISC-04, CORE-INTRO-10 | upstream:skills/academic-writing-skills/references/universal-integrity.md<br>upstream:skills/academic-writing-skills/references/comment-scoped-revision.md |
| CSBL-PROSE-01 | 판단 | — | CORE-LANG-09, CORE-LANG-10, CORE-LANG-13 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md<br>rpws:research-paper-writing/references/does-my-writing-flow-source.md |
| CSBL-SCORE-01 | 판단 | — | — | upstream:skills/academic-writing-skills/references/comment-scoped-revision.md |
| CSBL-COVER-01 | 기계 | style/score-coverage | — | upstream:skills/academic-writing-skills/references/results-and-explanation.md<br>upstream:skills/academic-writing-skills/references/discussion-and-limitations.md |
| CSBL-PART-01 | 판단 | — | CORE-LANG-04, CORE-LANG-09 | upstream:skills/academic-writing-skills/references/prose-and-citation-editing.md |
| CSBL-LEGEND-01 | 판단 | — | CORE-RES-13, CORE-RES-14, CORE-RES-20 | upstream:skills/academic-writing-skills/references/figures-tables-and-supplements.md |

## manuscript_eval rubric → rule_id (역방향)

| rubric_id | rule_id |
|---|---|
| CORE-ABS-01 | CSBL-ABS-01 |
| CORE-ABS-03 | CSBL-ABS-01, CSBL-ABS-03 |
| CORE-ABS-05 | CSBL-ABS-03 |
| CORE-ABS-07 | CSBL-TITLE-01, CSBL-TITLE-02 |
| CORE-ABS-08 | CSBL-ABS-02 |
| CORE-ABS-09 | CSBL-TITLE-02 |
| CORE-ABS-10 | CSBL-ABS-03 |
| CORE-DISC-01 | CSBL-DISC-01 |
| CORE-DISC-02 | CSBL-DISC-02 |
| CORE-DISC-04 | CSBL-RES-03, CSBL-HEDGE-01, CSBL-HEDGE-02, CSBL-INTEG-01 |
| CORE-DISC-05 | CSBL-DISC-01 |
| CORE-FIG-02 | CSBL-FIG-01 |
| CORE-INTRO-03 | CSBL-INTRO-01 |
| CORE-INTRO-08 | CSBL-INTRO-01 |
| CORE-INTRO-10 | CSBL-INTEG-01 |
| CORE-INTRO-12 | CSBL-INTRO-01 |
| CORE-LANG-01 | CSBL-LANG-01, CSBL-UNIT-01 |
| CORE-LANG-04 | CSBL-PART-01 |
| CORE-LANG-07 | CSBL-UNIT-01 |
| CORE-LANG-08 | CSBL-SIG-01 |
| CORE-LANG-09 | CSBL-RES-01, CSBL-RES-02, CSBL-PROSE-01, CSBL-PART-01 |
| CORE-LANG-10 | CSBL-STOCK-01, CSBL-RES-04, CSBL-CONN-01, CSBL-PROSE-01 |
| CORE-LANG-11 | CSBL-RES-05 |
| CORE-LANG-13 | CSBL-PROSE-01 |
| CORE-LANG-14 | CSBL-SENT-01 |
| CORE-LANG-15 | CSBL-SENT-01 |
| CORE-LANG-16 | CSBL-SENT-01 |
| CORE-LANG-18 | CSBL-VOICE-01 |
| CORE-LANG-19 | CSBL-VOICE-01 |
| CORE-LANG-20 | CSBL-HEDGE-01 |
| CORE-LANG-22 | CSBL-CONN-01 |
| CORE-LANG-23 | CSBL-CONN-01 |
| CORE-LANG-24 | CSBL-BOOST-01 |
| CORE-RES-02 | CSBL-FIG-01, CSBL-RES-01, CSBL-RES-02, CSBL-RES-03 |
| CORE-RES-13 | CSBL-LEGEND-01 |
| CORE-RES-14 | CSBL-LEGEND-01 |
| CORE-RES-20 | CSBL-LEGEND-01 |
