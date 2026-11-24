# domain-overlay-bio — 생물정보·약물·계산생물로 옮길 때

- 근거는 프로파일 §9이다. 이 그룹 코퍼스는 대사공학 생산 연구 비중이 크다. 그래서 일부 관례는 우리 분야에 맞게 바꿔 적용한다.
- upstream overlay 분류로는 **domain check**(우선순위 6)이다. 문체 규칙(reviewer preference, 7)보다 앞서고, 저널 규정(4)·무결성(1)보다 뒤다.

| 관례 | rule_id | 그대로 | 우리 분야로 바꿀 때 |
|---|---|---|---|
| 괄호 그림 참조 | CSBL-FIG-01 | ○ | — |
| 결과 단락을 목적·근거로 열기 | CSBL-RES-02 | ○ | To evaluate / To validate + 데이터셋·벤치마크 이름 |
| 단락 끝 요약·추론 | CSBL-RES-03 | ○ | 성능 수치(AUROC, AUPRC, RMSE 등) + suggest 수준 해석 |
| 보고 동사 | CSBL-RES-05 | — | 생산 동사(produced, titer, enhanced production) 대신 predicted, identified, prioritized, outperformed |
| 예측 vs 검증 | CSBL-HEDGE-02 | — | 계산 예측은 predicted·suggest. 실험 검증된 것만 confirmed·demonstrated. 도킹·결합 모델은 "결합한다"가 아니라 "결합이 예측된다" |
| 서론 공백 | CSBL-INTRO-01 | ○ | 공백 = 데이터·방법의 한계(일반화, 해석 가능성, 외부 검증 부재) |
| 초록 수치 | CSBL-ABS-03 | ○ | 생산 수치 대신 핵심 성능 지표 1~2개(외부 검증 값 우선) |
| 제목 | CSBL-TITLE-02 | — | `Production of X by …` 대신 `<방법/자원> for <과제>` 명사구 |
| significant | CSBL-SIG-01 | ○ | 모델 비교는 검정 이름·반복 단위(교차검증 fold, seed)를 같은 문장 또는 괄호에 |

## 분야 점검 (판단)
- 벤치마크 비교는 같은 분할·전처리·평가 지표인지 본문에 드러나야 한다. 이는 manuscript_eval CORE-RES-03과 겹치는 내용 점검이라 교정이 아니라 지적으로 남긴다.
- 유전자·단백질·화합물 표기(이탤릭, 대소문자)는 분야 규약과 저널 양식을 따른다 — CSBL-UNIT-01, CORE-LANG-07.
- 데이터·코드 가용성 문장은 저널 규정을 따르고 표현만 다듬는다 — CSBL-UNIT-01.
