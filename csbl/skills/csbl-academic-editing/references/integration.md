# integration — 설치와 연결

## 1. 위치
| 무엇 | 경로 |
|---|---|
| 정본(포크 저장소) | `csbl/skills/csbl-academic-editing/` — upstream `skills/` 밖이다. upstream 테스트가 `skills/` 아래 파일 집합을 고정하기 때문이다(코디네이터 확정) |
| 정본 작업 사본 | `~/my_projects/papers_style/fork-overlay/csbl/skills/csbl-academic-editing/` |
| Claude Code 설치본 | `~/.claude/skills/csbl-academic-editing/` |
| Codex 설치본 | `~/.codex/skills/csbl-academic-editing/` (`agents/openai.yaml` 포함) |
| lab-lint 규칙 사본 | `~/my_projects/코디네이터/lib/labcheck/style-rules.json` = `references/rules.json`과 바이트 동일(`lib/labcheck/style.test.mjs`가 대조) |

- 설치본은 정본의 복사본이다. 고칠 때는 정본을 고친다.
  1. `tools/render_rules.py`로 `rules.md`·`rule-map.md`를 다시 만든다.
  2. 아래 명령으로 두 설치본과 lab-lint 사본을 갱신한다.
  3. 해시를 대조한다.

```
SRC=~/my_projects/papers_style/fork-overlay/csbl/skills/csbl-academic-editing
rsync -a --delete "$SRC/" ~/.claude/skills/csbl-academic-editing/
rsync -a --delete "$SRC/" ~/.codex/skills/csbl-academic-editing/
cp "$SRC/references/rules.json" ~/my_projects/코디네이터/lib/labcheck/style-rules.json
node --test ~/my_projects/코디네이터/lib/labcheck/
```

## 2. 호출
- Claude Code: 대화에서 "csbl-academic-editing으로 <원고> 영어·논리 교정"이라고 하거나 `/csbl-academic-editing`을 쓴다. 설명문의 트리거(영어 교정, 문체 교정, rule_id …)로도 불린다.
- Codex: `$csbl-academic-editing`. `allow_implicit_invocation: false`라 자동으로 불리지 않고 명시해야 한다. 영어·논리 패스 요청에는 점수 루프(`references/quality-score.md`, `references/score-loop.md`)도 명시한다.
- lab-lint(기계 규칙):
  - 원고·교정 기록은 기밀로 보고 **실행할 때부터 `--redact --json`**을 붙인다(수준·코드·파일·개수만). `--redact` 없는 기본 출력은 기존 text/* 검사가 원고 수치·문구를 위치 칸에 내므로 원고에 쓰지 않는다.
  - `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json --manuscript <원고.md|.docx>`
    - `style/*` 코드별 개수가 나온다(위치·설명 없음).
    - `--manuscript`가 없어도 IMRaD 제목 3개 이상인 영어 문서면 자동으로 원고로 본다.
  - `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json <…edits….md>`
    - 변경 기록에 rule_id가 비어 있으면 오류(`style/edit-rule-id`)가 난다.
  - `--no-style`은 style 검사를 끈다.
  - lab-lint 통과만으로 언어 품질 합격이 되지 않는다. 초록·서론·방법·결과·고찰·결론과 그림·표 범례는 `quality-score.md`의 파트별 임계와 커버리지 100%를 따로 통과해야 한다(CSBL-SCORE-01, CSBL-COVER-01, CSBL-PART-01).
  - 영어 패스 수정본: `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json --manuscript --require-score-coverage <수정본>` (같은 폴더의 `quality-coverage.json` 또는 `quality-scores.*`가 필요하다). `style/score-coverage`는 미채점 단락이 있거나, `--require-score-coverage`인데 파일이 없으면 오류다.

## 3. manuscript_eval (`~/my_projects/manuscript_eval`)
- 그 폴더의 하드 게이트(원고 기밀 경계, 입력 불변, 날조 금지, 연구실 그래프 규칙 비적용)가 이 스킬보다 앞선다. 원고 본문은 모델 역할 프로세스 밖으로 보내지 않는다.
- **mseval 파이프라인**(단계 300~): 지적(`draft_finding`)은 스키마상 `rubric_id`가 이미 필수다(`schemas/common.json`). 이 스킬은 파이프라인 코드·스키마·rubric·프롬프트를 바꾸지 않는다. 바꾸려면 계약 변경이고 마스터 승인이 필요하다.
- **영어·논리 교정 패스**(작업 세션이 `output/<원고>/revision/<회차>/`에 쓰는 교정)
  - 이 스킬을 읽고, `references/quality-score.md`와 `references/score-loop.md`의 점수 루프를 따른다.
  - 변경 기록(예: `english-logic-edits.md`)의 모든 행에 rule_id를 적는다. rule_id는 `CSBL-…`, 또는 그 원고 실행의 `rubric/compiled.json`에 있는 `CORE-…`·`MOD-…`다.
  - 초록·서론·방법·결과·고찰·결론과 그림·표 범례는 각 파트 기대 문체에 따라 100% 채점하고, 임계 미만이면 최대 3루프까지 같은 문단 안에서 재작성한다. 일부 파트만 손보고 나머지를 얕게 두면 실패다. 사실 공란만 저자 질문으로 남긴다.
  - 검수 세션의 기계 게이트(`lab-lint`)가 빈 rule_id 칸을 오류로 잡는다. 언어 품질 합격은 검수 채점(커버리지 100%, 문단 임계 통과)이 추가로 필요하다.
  - 이 패스에는 mseval `prompts/reviser.md`의 「최소한으로 고친다」「지적과 무관한 곳을 고치지 마세요」를 적용하지 않는다. 사실 하드 게이트(한 문단 안, 새 숫자·고유명·인용·결과 주장 없음, 주장 강화 없음, 코퍼스 복제 없음)는 그대로 앞선다.
  - 연구실 내부 교정 기록(비공개)에는 rule_id 칸이 없었다. 새 검사는 그런 기록을 오류로 잡는다.
- **코디네이터**: 영어·논리 패스를 mseval 지적 루프(`O_K=0`)와 섞지 않는다. writer → scorer(다른 세션) → 실패면 미달 단락 id·차원만 steer → 최대 3루프. 조율 로그에 원고 본문을 붙이지 않고, 같은 원고를 교정하는 세션을 병렬로 추가하지 않는다.
- 연결 표시: manuscript_eval `AGENTS.md`·`CLAUDE.md`의 "교정 스킬" 절이 이 경로, 검사, 점수 루프를 가리킨다.

## 4. ~/projects/papers
- 그 폴더의 `AGENTS.md`(WORKFLOW-GRAPH·REVIEW-LOOP·개인정보 규칙)가 먼저다. 원고 교정 작업(`work/`·`output/`)은 이 스킬의 점수 루프를 포함해 수행하고, 변경 기록에 rule_id를 남긴다. 검수 세션은 `lab-lint`와 품질 채점을 확인한다.
- 연결 표시: `~/projects/papers/AGENTS.md`·`CLAUDE.md`의 "교정 스킬" 절이 같은 경로와 점수 루프를 가리킨다.

## 5. upstream academic-writing-skills와의 관계
- 이 스킬은 upstream `academic-writing-skills`의 overlay다. upstream `references/overlay-contract.md`의 분류로 CSBL 문체 규칙은 **reviewer preference**(우선순위 7)다. `domain-overlay-bio.md`는 **domain check**(6), CSBL-UNIT-01은 **venue requirement**(4)를 따르는 규칙이다. CSBL-INTEG-01은 연구 무결성(1)과 같은 원칙이다. 영어 교정 패스에서는 CSBL-PROSE-01·SCORE-01·COVER-01이 문체 선호(7)보다 앞선 품질 게이트다(SKILL.md 우선순위 ①-b). 사실 보존은 그대로 연구 무결성(1)이다.
- upstream 파일은 고치지 않는다. 기준 upstream 파일과 해시는 `csbl/OVERLAY-INDEX.md`.
