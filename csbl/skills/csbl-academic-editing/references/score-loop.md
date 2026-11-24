# score-loop — 영어 교정 품질 루프

## 순서

1. 범위 확인, 저널 규정 (CSBL-UNIT-01).
2. lab-lint 기계 검사 (`--no-network --redact --json --manuscript`).
3. 판단 규칙 + CSBL-PROSE-01 + CSBL-PART-01. **초록·서론·방법·결과·고찰·결론과 그림·표 범례**의 모든 본문 단락(범례 항목)을 읽는다. 각 파트는 `quality-score.md`의 기대 문체에 맞춘다. 사실 공란만 저자 질문. 표현 미달은 같은 문단 안에서 재작성한다. 한 단락의 여러 문장 수정은 하나의 rewrite로 남긴다.
4. 변경 기록 표 (`edit_id`, 위치, 요지, rule_id, 이유). rule_id에 CSBL-PROSE-01·SCORE-01·COVER-01·PART-01 및 해당 파트 문체 규칙을 적는다.
5. `quality-score.md`로 문장·문단 점수를 파트별로 매기고 `quality-scores`와 `quality-coverage`를 쓴다.
6. 미달 단락을 재작성하고 그 단락과 앞뒤를 재채점한다. **모든 존재 파트·범례의 커버리지 100%**는 매 루프 유지한다. 한 파트만 고치고 다른 파트를 건너뛰면 실패다.
7. 모든 존재 파트의 문단 100% 합격 또는 품질 루프 3회.
8. lab-lint(기록+수정본, 영어 패스에서는 `--require-score-coverage`)와 CSBL-INTEG-01 사실 대조. 교정 결과를 ‘최종’이라 부르지 않는다.

## 합격 조건 (한 루프)

- 원고에 있는 초록·서론·방법·결과·고찰·결론 본문 단락과 그림·표 범례 항목의 채점 100%, 문단 합격 100%(CSBL-COVER-01, CSBL-PART-01).
- 검수 채점: 수정자와 다른 세션이 미달 전부와, 각 존재 파트에서 합격 표본(최소 1단락 또는 그 파트 단락의 1/3)을 다시 매긴다. 한 차원이 1점 이상 낮게 나오면 그 단락은 미달.
- lab-lint `style/*` 오류 0 (`style/edit-rule-id`, `style/score-coverage` 포함). 영어 패스 수정본은 같은 폴더의 `quality-coverage.json`과 함께 `--require-score-coverage`로 검사한다.
- 새 숫자·인용·고유명사·결과 주장·주장 강화 없음. 코퍼스 연속 8단어 복사 없음.

## quality-coverage.json

같은 폴더(수정본·변경 기록 옆)에 둔다. lab-lint `style/score-coverage`가 원고의 기대 단락 집합과 대조한다.

```json
{
  "scored_para_ids": ["abstract:1", "introduction:1", "methods:1", "results:1", "discussion:1", "conclusion:1", "legends:1"],
  "passed_para_ids": ["abstract:1", "introduction:1", "methods:1", "results:1", "discussion:1", "conclusion:1", "legends:1"]
}
```

- `scored_para_ids`는 필수. 원고에 있는 해당 파트 본문 단락이 하나라도 빠지면 오류다.
- `passed_para_ids`가 있으면, 채점된 단락이 모두 들어 있어야 한다(합격 표지). 점수 값 자체는 모델 검수가 맡는다.
- `quality-scores.json` 또는 `quality-scores.md`만 있어도, 같은 `{파트}:{n}` 또는 `Abstract ¶1` 표지가 있으면 인정한다. 우선순위는 `quality-coverage.json`이다.

## 코디네이터

영어·논리 패스를 mseval 지적 루프(`O_K=0`)와 섞지 않는다. writer → scorer → (실패면 steer로 미달 단락 id·차원·파트만 전달) → 최대 3루프. 조율 로그에 원고 본문을 붙이지 않는다. 같은 원고를 교정하는 세션을 병렬로 추가하지 않는다. Codex 호출은 `$csbl-academic-editing`을 명시한다. 한 파트만 다시 돌리고 다른 파트를 재채점 없이 건너뛰지 않는다.
