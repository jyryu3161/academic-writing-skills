# checklist — 섹션별 교정 점검표

순서대로 읽고, 고칠 곳마다 오른쪽 rule_id를 변경 기록에 적는다. **(기계)**는 lab-lint `style/*`가 먼저 표시해 준다.

## 0. 시작 전
- [ ] 대상 저널·분량 한도·철자 계열·단위 표기를 확인했다 — CSBL-UNIT-01
- [ ] `lab-lint --no-network --redact --json --manuscript <원고>`를 돌려 `style/*` 코드별 개수를 받았다(원고는 실행할 때부터 `--redact --json`) — 기계 규칙 전체
- [ ] 원고 안에서 미국식·영국식 철자가 섞였는지 봤다 **(기계)** — CSBL-LANG-01

## 1. 제목
- [ ] 의문문이 아니다 **(기계)** — CSBL-TITLE-01
- [ ] 11~12단어 안팎의 명사구이고 동사형 주장이 아니다. 우리 분야는 `<방법/자원> for <과제>` — CSBL-TITLE-02

## 2. 초록
- [ ] 목적 문장(Here, we … / In this study, we …)이 있다 **(기계)** — CSBL-ABS-01
- [ ] 분량이 저널 한도 안이다. 한도 안에서는 최근 범위(103–248단어)를 참고한다 **(기계, info)** — CSBL-ABS-02
- [ ] 배경 약 2문장 → 목적 → 수단(by + -ing) → 결과(병렬 수치는 respectively) → 함의 순서로 읽힌다 — CSBL-ABS-03
- [ ] 모든 수치가 본문과 같다(lab-lint `text/abstract-number`) — CSBL-INTEG-01
- [ ] 태·인칭이 최근 목표에 가깝다(능동·we 허용) — CSBL-VOICE-01

## 3. 서론
- [ ] 4~5단락 깔때기: 넓은 배경 → 공백 → 선행 연구·도구 → 목적·요지 — CSBL-INTRO-01
- [ ] 공백 제시가 첫 단락부터 나온다(however …, remains challenging) — CSBL-INTRO-01
- [ ] 목적 문장은 마지막 단락에 있고 첫 문장에는 we가 없다 — CSBL-INTRO-01
- [ ] 빈 상투구가 없다 **(기계)** — CSBL-STOCK-01

## 4. 결과 (또는 결과·고찰 통합)
- [ ] 단락을 We로 바로 열지 않는다 **(기계)** — CSBL-RES-01
- [ ] 첫 문장이 실험의 목적·근거·순서를 말한다(To examine …, As …, Next, …) — CSBL-RES-02
- [ ] 단락 끝이 요약·추론(These results suggest that …) 또는 핵심 수치다 — CSBL-RES-03
- [ ] 주절은 단순하고 조건·수치·그림은 괄호에 있다. 병렬 수치는 respectively — CSBL-RES-04
- [ ] 그림·표 참조가 괄호형이다 **(기계)** — CSBL-FIG-01
- [ ] 보고 동사가 구체적이고 해석 주어는 These results다 — CSBL-RES-05
- [ ] significant마다 통계 근거가 같은 문장에 있다 **(기계)** — CSBL-SIG-01
- [ ] 우선권·감탄 부스터가 없다 **(기계)** — CSBL-BOOST-01
- [ ] 예측 결과에 검증 전 demonstrate·confirm을 쓰지 않았다 — CSBL-HEDGE-02
- [ ] 40단어를 넘는 문장은 한 메시지인지 확인했다 — CSBL-SENT-01

## 5. 고찰·결론
- [ ] 첫머리에서 연구를 한 문장으로 다시 요약한다 — CSBL-DISC-01
- [ ] 해석 헤지가 suggest·indicate 중심이고, 교정으로 주장이 강해지지 않았다 — CSBL-HEDGE-01, CSBL-INTEG-01
- [ ] 한계가 후반에 있고 Although … / It should be noted that으로 열린다 — CSBL-DISC-02
- [ ] 연결어를 나열하지 않고 These/This로 이어받는다 — CSBL-CONN-01

## 6. 방법
- [ ] 수동 중심이고 we가 거의 없다. 태를 기계적으로 바꾸지 않는다 — CSBL-VOICE-01
- [ ] 단위·철자가 저널 양식과 같다 — CSBL-UNIT-01

## 7. 마무리
- [ ] 변경 기록 표의 모든 행에 rule_id가 있다(`lab-lint` `style/edit-rule-id` 오류 0) — CSBL-EDIT-01
- [ ] 새 숫자·인용·고유명사·주장 강화가 없다(원문 대조) — CSBL-INTEG-01
- [ ] 고치지 않은 경고는 이유를 적었다
