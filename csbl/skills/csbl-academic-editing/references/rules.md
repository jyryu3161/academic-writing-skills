# rules — csbl-academic-editing 규칙 (rules.json에서 생성, 직접 고치지 말 것)

- 판 0.1.3 (reviewed 2026-11-24 (r4/review-r3.md PASS); professor-approved 2026-11-24 skill revisions: v0.1.2 quality-score loop; v0.1.3 all-part scoring (Abstract–Conclusions and legends) and style/score-coverage), 2026-11-24. 규칙 31개: 기계 검사 11, 사람 판단 20.
- **목표값**: 새로 고치는 원고에는 프로파일의 2019–2026 값(31편)을 기본 목표로 쓴다. ALL(73편)·이전 연대 값은 비교용이다. 2019–2026 분리 값이 없는 규칙은 그렇게 적고 ALL을 참고로만 든다.
- **우선순위**: CSBL-INTEG-01 and upstream universal integrity (preserve facts; improve wording and in-paragraph structure) > language-quality loop (CSBL-PROSE-01, CSBL-SCORE-01, CSBL-COVER-01, CSBL-PART-01) > confirmed manuscript facts and author instructions > target journal rules (CSBL-UNIT-01) > manuscript_eval core rubric (CORE-*) > domain checks (domain-overlay-bio.md) > other CSBL style rules.
- **인용 의무**: 교정 제안·변경마다 rule_id를 적는다(`CSBL-…`, 또는 manuscript_eval `CORE-…`·`MOD-…`). 빈 칸은 lab-lint `style/edit-rule-id` 오류다.
- 근거 표기 `SP-xx`·`profile §n`은 `profile/style_profile.md`(papers_style)의 관찰 번호·절이다. 수치는 어휘·정규식 신호 집계이며 표본 한계가 있다.

## 1. 기계 검사 규칙 (lab-lint `style/*`)

### CSBL-FIG-01
- lint: `style/figref-narrative` (warning)
- 영역: figures
- 규칙: 그림·표 참조는 괄호로 단다. 'as shown in Fig.'나 'Figure 2 shows' 같은 서술형 참조를 쓰지 않고, 근거 문장 끝에 (Fig. 2a)처럼 둔다. (적용 섹션: all)
- 목표(2019–2026): 2019-2026: 괄호형 95.4% (논문별 평균), 94.8% (참조 가중)
- 비교: ALL 88.0% (가중 91.4%); 1998-2010 70.4%
- 근거: SP-01, profile §7

### CSBL-BOOST-01
- lint: `style/priority-booster` (warning)
- 영역: claims
- 규칙: 우선권·감탄 부스터(for the first time, remarkably, unprecedented, groundbreaking, breakthrough)를 쓰지 않는다. 강조가 필요하면 비교 대상과 수치로 말한다. (적용 섹션: all)
- 목표(2019–2026): 2019-2026 결과: 'for the first time' 1만 단어당 0.1
- 비교: ALL 0.5/1만, remarkably 0.1/1만; 비교 최상급 highest 6.5/1만
- 근거: SP-10, profile §6.3

### CSBL-SIG-01
- lint: `style/significant-no-stat` (warning)
- 영역: claims
- 규칙: significant/significantly는 같은 문장에 통계 근거(p 값, 검정 이름, FDR·q, 신뢰구간)가 있을 때만 쓴다. 일반 강조는 수치 비교로 바꾼다. 방법 섹션은 제외한다(유의성 기준을 정의하는 문장이 대부분이라 주장 문장이 아니다). (적용 섹션: abstract, introduction, results, discussion, conclusion)
- 목표(2019–2026): 통계 검정 없는 significant 0건
- 비교: ALL significantly 1만 단어당 5.4 (통계 강조로 쓰임)
- 근거: profile §6.3

### CSBL-STOCK-01
- lint: `style/stock-phrase` (warning)
- 영역: prose
- 규칙: 빈 상투구(it is important to note that, it is worth noting that, plays a crucial role, in the realm of, a myriad of, delve into, this underscores the importance of, in today's rapidly evolving)를 지운다. 'It should be noted that'은 한계 도입에 쓰는 연구실 관례라 예외다(CSBL-DISC-02). (적용 섹션: all)
- 목표(2019–2026): 0건
- 비교: upstream PROSE003 목록에서 'it should be noted that'만 제외
- 근거: upstream audit_prose_patterns.py PROSE003, profile §4.3

### CSBL-RES-01
- lint: `style/results-we-opening` (warning)
- 영역: results
- 규칙: 결과 단락을 'We + 동사'로 바로 열지 않는다. 실험의 목적·근거·순서를 먼저 말한다(CSBL-RES-02). (적용 섹션: results)
- 목표(2019–2026): 2019-2026 OA 11편·179단락: We 시작 2.8%
- 비교: OA 17편·265단락 2.3%; 문헌 46편·669단락 1.2%
- 근거: SP-02, profile §4.2

### CSBL-ABS-01
- lint: `style/abstract-purpose` (warning)
- 영역: abstract
- 규칙: 연구 논문 초록에는 목적 문장(Here, we … / In this study, we … / We report …)을 둔다. 배경 뒤 셋째 문장 전후가 흔하다. (적용 섹션: abstract)
- 목표(2019–2026): 2019-2026: 26/31편(연구 논문 25/27)
- 비교: 1998-2010 4/12, ALL 연구 논문 48/67
- 근거: SP-08, profile §3, §5.1, profile/stats/abstracts.json (r4 연도 분리 계산)

### CSBL-ABS-02
- lint: `style/abstract-length` (info)
- 영역: abstract
- 규칙: 초록 분량은 대상 저널 한도를 먼저 따르고, 한도 안에서는 최근 연구실 범위를 참고한다. (적용 섹션: abstract)
- 목표(2019–2026): 2019-2026 31편: 중앙 176단어, p10-p90 103-248단어
- 비교: ALL 평균 195.3단어
- 근거: SP-08, profile/stats/abstracts.json (r4 연도 분리 계산)

### CSBL-TITLE-01
- lint: `style/title-question` (warning)
- 영역: title
- 규칙: 제목을 의문문으로 쓰지 않는다. (적용 섹션: title)
- 목표(2019–2026): 의문형 0%
- 비교: ALL 제목 103개 중 의문형 0, 동사형 1
- 근거: SP-11, profile §5.2

### CSBL-LANG-01
- lint: `style/spelling-mix` (warning)
- 영역: language
- 규칙: 한 원고 안에서 미국식·영국식 철자(-ize/-ise, analyze/analyse, titer/titre, color/colour)를 섞지 않는다. 어느 쪽인지는 저널 양식을 따른다(CSBL-UNIT-01). (적용 섹션: all)
- 목표(2019–2026): 혼용 0
- 비교: 코퍼스는 미국식 -ize 우세
- 근거: SP-12, profile/stats/per_paper.json units_spelling

### CSBL-EDIT-01
- lint: `style/edit-rule-id` (error)
- 영역: process
- 규칙: 교정 기록의 모든 변경 행은 rule_id 칸에 근거 규칙을 적는다(CSBL-…, 또는 manuscript_eval의 CORE-…·MOD-…). 빈 칸이나 없는 CSBL ID는 오류다. (적용 섹션: edit log)
- 목표(2019–2026): 빈 rule_id 0
- 비교: 연구실 내부 교정 기록(비공개)에는 rule_id·rubric_id 칸이 없었다
- 근거: REQUEST.md 4단계, 연구실 내부 교정 기록(비공개)

### CSBL-COVER-01
- lint: `style/score-coverage` (error)
- 영역: process
- 규칙: 원고에 있는 모든 본문 파트(초록·서론·방법·결과·고찰 또는 결과·고찰 통합 절·결론)와 그림·표 범례의 본문 단락 100%를 채점하고, 문단 합격 100%를 충족한다. 일부 파트만 채점·수정하고 나머지를 얕게 두면 실패다. ‘이미 괜찮음’은 점수가 임계 이상일 때만 허용한다. 미채점은 오류다. 교정 기록 옆의 quality-coverage.json(또는 quality-scores.*)이 근거이며, lab-lint style/score-coverage가 검사한다. (적용 섹션: abstract, introduction, methods, results, discussion, conclusion, legends)
- 목표(2019–2026): 존재하는 모든 해당 파트·범례 본문 단락 채점 100%, 문단 합격 100%
- 비교: v0.1.2는 결과·고찰·결론만 커버리지 의무였고, 이전 패스는 lab-lint 커버리지 검사가 없었다
- 근거: references/score-loop.md, references/quality-score.md, professor-approved skill revision 2026-11-24 (v0.1.3, all-part coverage)

## 2. 사람 판단 규칙

### CSBL-RES-02
- 영역: results
- 규칙: 결과 단락 첫 문장은 그 실험을 왜 했는지부터 말한다: 목적(To examine …), 근거(As …, Since …, Having …, Based on …), 순서(Next, …). 계산 연구는 To evaluate/To validate + 데이터셋·벤치마크. (적용 섹션: results)
- 목표(2019–2026): 2019-2026 OA 11편·179단락: To 20.1%, 근거 13.4%, 순서어 10.1%
- 비교: OA 17편: To 17.4%, 근거 14.0%; 문헌 2019-2026 To 13.6%
- 근거: SP-02, profile §4.2, §9

### CSBL-RES-03
- 영역: results
- 규칙: 결과 단락은 요약·추론(These results suggest that …) 또는 핵심 수치로 끝낸다. 추론 강도는 suggest·indicate 수준을 넘지 않는다. (적용 섹션: results)
- 목표(2019–2026): 2019-2026 OA 179단락 끝 문장: 요약 28.5%, 결과+추론 동사 8.9%, 수치 12.8%
- 비교: OA 17편 29.8/10.9/9.4%; 문헌 27.5/8.2/18.5%
- 근거: SP-03, profile §4.2

### CSBL-RES-04
- 영역: results
- 규칙: 결과 문장은 주절을 단순하게 두고 조건·수치·그림 참조는 괄호에 넣는다. 병렬 수치는 …, respectively로 묶고, 초록의 수단은 by + -ing로 압축한다. (적용 섹션: results, abstract)
- 목표(2019–2026): 2019-2026 분리 값 없음 (ALL 참고)
- 비교: ALL 결과 100문장당 괄호 78.3, respectively 5.8; 초록 by + -ing 9.5
- 근거: profile §2.1

### CSBL-RES-05
- 영역: results
- 규칙: 결과 보고는 구체 동사(increased, produced, resulted in; 계산 연구는 predicted, identified, prioritized, outperformed)로 한다. we의 동사는 행위(examined, constructed, tested)이고, 해석의 주어는 These results가 맡는다. (적용 섹션: results)
- 목표(2019–2026): 2019-2026 분리 값 없음 (ALL 참고)
- 비교: ALL 결과 1천 단어당 increase 4.5, result 4.1, produce 3.4, show 3.1
- 근거: profile §6.1, §6.2, §9

### CSBL-HEDGE-01
- 영역: claims
- 규칙: 해석 헤지는 suggest·indicate를 중심으로 쓰고, may·could는 가능성·응용을 말할 때 쓴다. 교정에서는 주장 강도를 유지하거나 약화만 한다. (적용 섹션: results, discussion)
- 목표(2019–2026): 2019-2026 결과 1천 단어당 suggest 1.15, indicate 0.96, may 0.58
- 비교: 1998-2010 may 0.21
- 근거: SP-04, profile §6.3

### CSBL-HEDGE-02
- 영역: claims
- 규칙: 예측·계산 결과는 실험 검증 여부로 동사를 가른다. 검증 전에는 predicted·suggest, demonstrate·confirm은 검증된 결과에만 쓴다. (적용 섹션: results, discussion, abstract)
- 목표(2019–2026): 검증 전 demonstrate·confirm 0건
- 비교: lab-lint text/overclaim이 근거 지시 없는 과잉 주장 어휘를 경고
- 근거: profile §9

### CSBL-VOICE-01
- 영역: language
- 규칙: 태와 인칭·시제는 섹션에 맞춘다. 방법은 과거 시제·수동 중심이고 we를 거의 쓰지 않는다. 초록·고찰·결과에서는 능동과 we를 쓸 수 있으며 최근 값이 목표다. 기계적으로 태를 바꾸지 않는다. (적용 섹션: all)
- 목표(2019–2026): 2019-2026: 초록 수동 34.3%·we 21.9%, 고찰 수동 34.5%·we 17.0%, 결과 수동 48.0%·we 11.6%, 방법 수동 88.4%·we 1.6% (방법 1,471문장)
- 비교: 1998-2010 초록 수동 55.6%·we 4.9%; ALL 방법 수동 85.8%·we 1.0%
- 근거: SP-05, SP-06, profile §2, §3

### CSBL-INTRO-01
- 영역: introduction
- 규칙: 서론은 4~5단락 깔때기로 쓴다: 넓은 배경(인용 밀집) → 첫 단락부터 공백 제시(however, remains challenging, is limited) → 선행 연구·도구 → 마지막 단락의 목적·요지(Here, we report …). 서론 첫 문장에는 we를 쓰지 않는다. (적용 섹션: introduction)
- 목표(2019–2026): 2019-2026 OA 14편: 공백 신호 10/14, 마지막 단락 목적 9/14, 평균 4.5단락
- 비교: OA 21편 12/21, 11/21, 4.3단락; 2019-2026 문헌 15편 4.27단락(쪽 분할 영향); 첫 문장 we 5/67
- 근거: SP-07, profile §4.1

### CSBL-ABS-03
- 영역: abstract
- 규칙: 초록은 배경 약 2문장 → 목적 문장 → 수단(by + -ing) → 결과(병렬 수치는 respectively) → 함의 순서로 쓴다. 수치·함의는 권장 패턴이지 의무가 아니다(계산 논문은 핵심 성능 지표 1~2개). (적용 섹션: abstract)
- 목표(2019–2026): 2019-2026: 문장 수 중앙 8 (p10-p90 5-11), 함의 신호 17/31, 수치 신호 22/31
- 비교: ALL 7.8문장, 목적 문장 평균 3.1번째
- 근거: SP-08, profile §5.1, §9, profile/stats/abstracts.json (r4 연도 분리 계산)

### CSBL-DISC-01
- 영역: discussion
- 규칙: 고찰은 연구를 한 문장으로 다시 요약하며 열고(In this study, we developed …), 의미와 선행 연구 비교로 이어 간다. (적용 섹션: discussion, conclusion)
- 목표(2019–2026): 2019-2026 전체 27편(OA 13 + 문헌 14): 고찰 첫 문장 요약 신호 10/27. 적용 집합은 전체(첫 문장 신호라 쪽 경계 단락 분할의 영향을 받지 않음)
- 비교: 2019-2026 OA 4/13, 문헌 6/14; ALL 26/60 (김현욱 7/7)
- 근거: profile §4.3, §8

### CSBL-DISC-02
- 영역: discussion
- 규칙: 한계는 고찰 후반에 두고 양보절(Although …)이나 It should be noted that으로 연다. 원인 추정에는 짧은 헤지(likely due to, might be due to)를 쓴다. (적용 섹션: discussion)
- 목표(2019–2026): 2019-2026 한계 신호 문장 11.9% (어휘 신호)
- 비교: ALL 11.1%, 후반 1/3에 43.1%
- 근거: SP-09, profile §4.3

### CSBL-TITLE-02
- 영역: title
- 규칙: 제목은 11~12단어 안팎의 명사구로 쓴다. 콜론·동사형 주장 제목은 드물게 쓴다. 우리 분야는 <방법/자원> for <과제> 형태를 권한다. (적용 섹션: title)
- 목표(2019–2026): 2019-2026 분리 값 없음 (ALL 참고)
- 비교: ALL 평균 11.6단어, 콜론 5.8%, 동사형 1.0%
- 근거: SP-11, profile §5.2, §9

### CSBL-SENT-01
- 영역: language
- 규칙: 문장 길이 자체보다 구조를 본다. 40단어를 넘는 문장은 한 메시지인지 확인하고, 괄호·respectively·, which로 정리하거나 나눈다. 40단어 미만이어도 메시지가 둘 이상이거나 품질 점수의 논리·명확 차원이 임계 미만이면 나누거나 고친다. (적용 섹션: all)
- 목표(2019–2026): 2019-2026 결과 문장 평균 26.5단어
- 비교: ALL 섹션별 중앙 21-26, p90 39-42단어
- 근거: profile §2, §3

### CSBL-CONN-01
- 영역: language
- 규칙: 문장은 These …/This …로 앞 문장을 이어받거나 However·Thus로 잇는다. In addition·Moreover·Furthermore를 연달아 쌓는 나열은 관계(원인·대조·결과)를 드러내는 연결로 바꾼다. (적용 섹션: all)
- 목표(2019–2026): 2019-2026 분리 값 없음 (ALL 참고)
- 비교: ALL 100문장당 첫머리 However 3.1, Thus 2.8, In addition 1.3; 결과에서 These·This 시작이 단일 연결어보다 많음
- 근거: profile §2.2, §8

### CSBL-UNIT-01
- 영역: journal
- 규칙: 단위 표기(g L−1 vs g/L), 철자 계열, Fig./Figure 표기는 대상 저널 양식을 따른다. 연구실 고정 규칙으로 바꾸지 않는다. (적용 섹션: all)
- 목표(2019–2026): 대상 저널 양식
- 비교: Nat Commun g L−1, PNAS g/L
- 근거: SP-12, profile §7

### CSBL-INTEG-01
- 영역: integrity
- 규칙: 교정은 사실(수치·단위·표본 수·p값·인용·고유명사·결과의 방향과 부정)을 바꾸지 않고, 주장 강도는 유지하거나 약화만 한다. 코퍼스·다른 논문 문장을 연속 8단어를 넘게 옮겨 쓰지 않는다. 저자만 확정할 수 있는 사실 공란(없는 수치·새 인용·새 결과 주장)은 고치지 않고 질문으로 남긴다. 이 규칙은 표현·문장 구조·문단 내부 배열을 그대로 두라는 뜻이 아니다. 같은 사실을 더 명확·간결·논리적으로 쓰는 언어·구조 개선은 필수이며, ‘의미가 비슷하니 둔다’는 이유로 통과하지 않는다. (적용 섹션: all)
- 목표(2019–2026): 새 숫자·인용·주장 강화 0건; 표현 개선을 생략하지 않음
- 비교: manuscript_eval 하드 게이트 3과 같은 원칙
- 근거: manuscript_eval AGENTS.md 하드 게이트 3

### CSBL-PROSE-01
- 영역: language
- 규칙: 모든 본문 파트(초록·서론·방법·결과·고찰·결론)와 그림·표 범례의 문장을, 그 파트의 기대 문체에 맞게 명확·간결·논리적으로 적극 교정한다. 문법 오류가 없어도 어색·장황·모호·연결 불명이면 같은 문단 안에서 재작성한다. 일부 파트만 손보고 나머지를 얕게 두지 않는다. 사실·수치·인용·주장 강도는 CSBL-INTEG-01을 따른다. (적용 섹션: abstract, introduction, methods, results, discussion, conclusion, legends)
- 목표(2019–2026): 원고에 있는 모든 본문 파트와 범례의 문장 품질 점수 임계 통과(각 차원·평균 ≥ 4.0)
- 비교: 이 규칙은 계량 프로파일 목표가 아니라 영어 교정 패스의 언어 품질 게이트다
- 근거: references/quality-score.md, professor-approved skill revision 2026-11-24 (phase 1)

### CSBL-SCORE-01
- 영역: process
- 규칙: references/quality-score.md의 문장·문단 점수를 파트별 기대 문체에 따라 매기고, 임계 미만인 단락은 통과할 때까지(최대 3루프) 다시 고친다. 자평만으로 끝내지 않고 검수 채점을 받는다. (적용 섹션: all)
- 목표(2019–2026): 임계 미만 단락 0, 품질 루프 ≤ 3
- 비교: 이전 영어 교정 패스는 lab-lint 기계 규칙과 rule_id 유무만 게이트로 썼다
- 근거: references/quality-score.md, references/score-loop.md, professor-approved skill revision 2026-11-24 (phase 1)

### CSBL-PART-01
- 영역: language
- 규칙: 교정·채점은 파트별로 한다. 각 파트의 기대 문체·용어·시제·구조(references/quality-score.md 파트 표)에 맞춘다. 초록은 간결하고 인용이 없는 것이 기본이며, 방법은 과거 시제·수동태를 허용하고, 결과는 보고, 고찰은 해석·문헌 비교, 결론은 요약, 범례는 간결한 명사구·짧은 절로 쓴다. 모든 본문 파트와 범례를 같은 기준으로 채점·교정하고, 특정 파트만 수정하고 나머지를 얕게 두는 것은 불합격이다. (적용 섹션: abstract, introduction, methods, results, discussion, conclusion, legends)
- 목표(2019–2026): 존재하는 모든 파트·범례가 각 파트 기대 문체와 품질 임계를 충족
- 비교: v0.1.2의 필수 커버리지는 결과·고찰·결론에 치우쳐 다른 파트가 얕게 남을 수 있었다
- 근거: references/quality-score.md, professor-approved skill revision 2026-11-24 (v0.1.3, all-part style)

### CSBL-LEGEND-01
- 영역: legends
- 규칙: 그림·표 범례(캐프션)는 간결한 명사구 또는 짧은 절로 쓰고, 패널·시료·조건, 표본 수 n, 통계·오차 정의를 담는다. 결과 해석을 길게 늘이지 않고 본문 논의에 둔다. 수치는 본문과 같게 유지하고 새 숫자를 넣지 않는다. (적용 섹션: legends)
- 목표(2019–2026): 범례 각 항목이 조건·표기 위주이고 긴 논의가 없다
- 비교: 2019-2026 분리 값 없음 (CORE-RES-13·14·20 참고)
- 근거: references/quality-score.md, CORE-RES-13, CORE-RES-14
