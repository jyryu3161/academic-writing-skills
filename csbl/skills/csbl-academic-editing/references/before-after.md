# before-after — 교정 예시 (모두 직접 지어낸 문장)

- 아래 문장은 이 스킬을 위해 **새로 쓴 가상의 예**다. 실제 논문·코퍼스·원고 문장이 아니며, 숫자·유전자·데이터셋 이름도 지어낸 것이다.
- 형식: 원문 → 수정, 그리고 적용한 rule_id. 실제 교정에서도 이렇게 한 행에 rule_id를 적는다.
- 수정은 의미·수치·주장 강도를 바꾸지 않는 범위에서만 한다(CSBL-INTEG-01).

## 그림 참조 — CSBL-FIG-01
- 원문: As shown in Figure 3b, the knockout strain grew more slowly on xylose.
- 수정: The knockout strain grew more slowly on xylose (Fig. 3b).

## 결과 단락 첫 문장 — CSBL-RES-01, CSBL-RES-02
- 원문: We deleted the two transporter genes and measured uptake rates.
- 수정: To test whether the two transporters limit uptake, both genes were deleted and uptake rates were measured.
- 계산 연구 변형: To evaluate generalization, the classifier was tested on an external cohort of 412 samples.

## 결과 단락 끝 — CSBL-RES-03, CSBL-HEDGE-01
- 원문: This proves that the transporter is the main bottleneck.
- 수정: These results suggest that the transporter is a major bottleneck under the tested conditions.
- 주의: proves → suggest는 **약화**다. 반대 방향(suggest → prove)은 어떤 규칙으로도 하지 않는다.

## 괄호와 respectively — CSBL-RES-04
- 원문: The titer was 2.1 g/L in strain A and the titer was 3.4 g/L in strain B, which was measured after 48 h.
- 수정: Strains A and B produced 2.1 and 3.4 g/L, respectively (48 h).

## 보고 동사 — CSBL-RES-05
- 원문: Figure 4 demonstrates an increase of the product.
- 수정: Overexpression of the reductase increased the product titer by 1.8-fold (Fig. 4a).
- 계산 연구: The model identified 37 candidate targets, of which 12 were prioritized for validation.

## 우선권 부스터 — CSBL-BOOST-01
- 원문: For the first time, we remarkably achieved the highest yield.
- 수정(원고에 두 수치가 이미 있을 때): The yield reached 0.42 g/g, higher than the 0.31 g/g of the parent strain.
- 주의: 비교 대상 수치(0.31)가 원고에 없으면 새로 만들지 말고 부스터만 지운다.

## significant — CSBL-SIG-01
- 원문: Expression was significantly higher in the treated group.
- 수정(통계가 있을 때): Expression was significantly higher in the treated group (two-sided t-test, P = 0.003).
- 수정(통계가 없을 때): Expression was 2.3-fold higher in the treated group.

## 빈 상투구 — CSBL-STOCK-01
- 원문: It is worth noting that our model plays a crucial role in target ranking.
- 수정: The model is used to rank the targets.
- 주의: "plays a crucial role"을 "determines"처럼 더 강한 말로 바꾸지 않는다(CSBL-INTEG-01).
- 유지: 한계 도입의 It should be noted that …은 연구실 관례라 그대로 둔다(CSBL-DISC-02).

## 예측과 검증 — CSBL-HEDGE-02
- 원문: Docking demonstrated that compound 7 binds the allosteric pocket.
- 수정: Docking predicted that compound 7 binds the allosteric pocket.

## 목적 문장 — CSBL-ABS-01, CSBL-ABS-03
- 원문(목적 없이 결과로 넘어감): Metabolic models are widely used. Many methods exist. The new pipeline achieved an AUROC of 0.91.
- 수정: Metabolic models are widely used to prioritize engineering targets, but their predictions are rarely benchmarked against fluxomic data. Here, we present a pipeline that ranks targets by combining flux sampling with expression data. The pipeline achieved an AUROC of 0.91 on held-out strains.

## 서론 마지막 단락 — CSBL-INTRO-01
- 원문(목적이 둘째 단락에 있음): (2단락) In this study we develop a ranking tool. (3~4단락) 배경 계속
- 수정: 목적 문장을 마지막 단락으로 옮기고 Here, we …로 연다. 단락 순서 변경은 인용 필드가 깨지지 않는 경우에만 한다.

## 한계 — CSBL-DISC-02
- 원문: Our method has some problems with small datasets.
- 수정: Although the method performed consistently on large cohorts, its accuracy on datasets with fewer than 50 samples remains to be tested.
- 주의: "fewer than 50"이 원고에 없는 수치면 넣지 않는다.

## 연결 — CSBL-CONN-01
- 원문: In addition, the strain grew faster. Moreover, it produced less acetate. Furthermore, it was stable.
- 수정: The strain grew faster and produced less acetate. This phenotype remained stable over 20 generations.

## 변경 기록 한 행 — CSBL-EDIT-01

| edit_id | 위치 | 원문(요지) | 수정(요지) | rule_id | 이유 |
|---|---|---|---|---|---|
| E-01 | Results ¶3 첫 문장 | We deleted … | To test whether … | CSBL-RES-01, CSBL-RES-02 | 단락 목적을 먼저 |
| E-02 | Results ¶3 끝 | This proves … | These results suggest … | CSBL-RES-03, CSBL-HEDGE-01 | 주장 약화 |
| E-03 | Methods ¶2 | the the | the | CORE-LANG-05 | 중복 단어 |
