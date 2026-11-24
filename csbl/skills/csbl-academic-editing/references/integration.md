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
- Codex: `$csbl-academic-editing`. `allow_implicit_invocation: false`라 자동으로 불리지 않고 명시해야 한다.
- lab-lint(기계 규칙):
  - 원고·교정 기록은 기밀로 보고 **실행할 때부터 `--redact --json`**을 붙인다(수준·코드·파일·개수만). `--redact` 없는 기본 출력은 기존 text/* 검사가 원고 수치·문구를 위치 칸에 내므로 원고에 쓰지 않는다.
  - `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json --manuscript <원고.md|.docx>`
    - `style/*` 코드별 개수가 나온다(위치·설명 없음).
    - `--manuscript`가 없어도 IMRaD 제목 3개 이상인 영어 문서면 자동으로 원고로 본다.
  - `~/my_projects/코디네이터/bin/lab-lint --no-network --redact --json <…edits….md>`
    - 변경 기록에 rule_id가 비어 있으면 오류(`style/edit-rule-id`)가 난다.
  - `--no-style`은 style 검사를 끈다.

## 3. manuscript_eval (`~/my_projects/manuscript_eval`)
- 그 폴더의 하드 게이트(원고 기밀 경계, 입력 불변, 날조 금지, 연구실 그래프 규칙 비적용)가 이 스킬보다 앞선다. 원고 본문은 모델 역할 프로세스 밖으로 보내지 않는다.
- **mseval 파이프라인**(단계 300~): 지적(`draft_finding`)은 스키마상 `rubric_id`가 이미 필수다(`schemas/common.json`). 이 스킬은 파이프라인 코드·스키마·rubric·프롬프트를 바꾸지 않는다. 바꾸려면 계약 변경이고 마스터 승인이 필요하다.
- **영어·논리 교정 패스**(작업 세션이 `output/<원고>/revision/<회차>/`에 쓰는 교정)
  - 이 스킬을 읽고, 변경 기록(예: `english-logic-edits.md`)의 모든 행에 rule_id를 적는다.
  - rule_id는 `CSBL-…`, 또는 그 원고 실행의 `rubric/compiled.json`에 있는 `CORE-…`·`MOD-…`다.
  - 검수 세션의 품질 게이트(`lab-lint`)가 빈 칸을 오류로 잡는다.
  - 연구실 내부 교정 기록(비공개)에는 이 칸이 없었다. 새 검사는 그런 기록을 오류로 잡는다.
- 연결 표시: manuscript_eval `AGENTS.md`·`CLAUDE.md`에 이 경로와 검사를 가리키는 "교정 스킬" 절(3줄)을 더했다.

## 4. ~/projects/papers
- 그 폴더의 `AGENTS.md`(WORKFLOW-GRAPH·REVIEW-LOOP·개인정보 규칙)가 먼저다. 원고 교정 작업(`work/`·`output/`)은 이 스킬로 하고, 변경 기록에 rule_id를 남긴다. 검수 세션은 `lab-lint`로 확인한다.
- 연결 표시: `~/projects/papers/AGENTS.md`·`CLAUDE.md`에 같은 "교정 스킬" 절(3줄)을 더했다.

## 5. upstream academic-writing-skills와의 관계
- 이 스킬은 upstream `academic-writing-skills`의 overlay다. upstream `references/overlay-contract.md`의 분류로 CSBL 문체 규칙은 **reviewer preference**(우선순위 7)다. `domain-overlay-bio.md`는 **domain check**(6), CSBL-UNIT-01은 **venue requirement**(4)를 따르는 규칙이다. CSBL-INTEG-01은 연구 무결성(1)과 같은 원칙이다.
- upstream 파일은 고치지 않는다. 기준 upstream 파일과 해시는 `csbl/OVERLAY-INDEX.md`.
