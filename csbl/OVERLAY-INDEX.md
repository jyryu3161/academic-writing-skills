# OVERLAY-INDEX — 기반 upstream 파일과 overlay 분류

- upstream: WenyuChiou/academic-writing-skills, 포크 jyryu3161/academic-writing-skills, 기준 커밋 `70e6d20921160fcf541bc4137ec4f6ca2875a069`.
- 아래 해시는 그 커밋 `adapter.json`의 `files` 값이며, 작업 사본(`papers_style/vendor/academic-writing-skills/`)의 파일 SHA-256과 일치함을 확인했다(2026-11-24).
- upstream이 바뀌면 해시가 달라진다. 이 해시가 바뀐 파일을 가리키는 규칙(`rules.json` `vendor_refs`)은 다시 대조한다.

## 기반 파일 (SHA-256)
| upstream 경로 | 쓰는 rule_id | SHA-256 |
|---|---|---|
| `LICENSE` | — (보존) | 1e034229fd46b8a7748bce109e3bcc078e180bb05e276e513039e2b9a990c637 |
| `skills/academic-writing-skills/references/overlay-contract.md` | 분류·우선순위 | 10ace6c61f410350a1ab2edf6982b63da391ca5bca44e65e41d277b7d081276e |
| `skills/academic-writing-skills/references/universal-integrity.md` | CSBL-BOOST-01, CSBL-HEDGE-01, CSBL-HEDGE-02, CSBL-INTEG-01 | 5f7335a39209ce301ad3f0c0a8e553bc8dbe1cb474f4afbe601e47af23c1a183 |
| `skills/academic-writing-skills/references/banned_words.md` | CSBL-BOOST-01, CSBL-STOCK-01 | 64255506e74955c9b5fa140555d45b6c8c19804ae0bddabdecf804bde7a44a70 |
| `skills/academic-writing-skills/scripts/audit_prose_patterns.py` | CSBL-STOCK-01(PROSE003 목록, 한 구 제외) | 014af3cd902cd12411cf61e6b11fa305c55252e77253a01b8f8cde21a85971f5 |
| `skills/academic-writing-skills/references/prose-and-citation-editing.md` | CSBL-STOCK-01, CSBL-RES-04, CSBL-VOICE-01, CSBL-SENT-01, CSBL-LANG-01 | 3e1c2466c9736f7d1cdc0a6d78a476a7a15d6ad9cef18fa2654e2da18c2936fd |
| `skills/academic-writing-skills/references/results-and-explanation.md` | CSBL-SIG-01, CSBL-RES-01·02·03·05 | bce3039a776a9c8a1bca08698efb42abfc6c0102c414078ac046184fd1021d81 |
| `skills/academic-writing-skills/references/figures-tables-and-supplements.md` | CSBL-FIG-01, CSBL-UNIT-01 | 3ee020f472e8c112fa91475ec4438a4a6d873305249a4d5f4905b694fd485c80 |
| `skills/academic-writing-skills/references/introduction-and-study-context.md` | CSBL-INTRO-01 | a23143b5b1cd8b013f5bfcec073af2ef44aa92a20d7976bd0277d542b5333b5f |
| `skills/academic-writing-skills/references/conclusion-and-abstract.md` | CSBL-ABS-01·02·03, CSBL-TITLE-01·02 | 8fd28b534b1d4dab88a5513ca446fee37b3e5951a75f38c2531e103eb926e424 |
| `skills/academic-writing-skills/references/discussion-and-limitations.md` | CSBL-DISC-01·02 | 31b82d02b15e858d60c2751518f9c15f16d40b483ebb1f4cc02099c7710db792 |
| `skills/academic-writing-skills/references/comment-scoped-revision.md` | CSBL-EDIT-01, CSBL-INTEG-01 | a9d951e4d705e548f290eb52f1df4a19869d2c1c5cbeeca083a105ea2c6b74bd |

## overlay 분류 (upstream overlay-contract의 5분류 · 우선순위)
| 분류 | 우선순위 | rule_id | 비고 |
|---|---|---|---|
| safety·ethics·integrity와 같은 원칙 | 1 | CSBL-INTEG-01 | |
| venue requirement | 4 | CSBL-UNIT-01 | 저널 양식을 따르라는 규칙 |
| domain check | 6 | CSBL-HEDGE-02, CSBL-SIG-01 | `domain-overlay-bio.md`의 분야 변형도 여기 |
| reviewer preference | 7 | CSBL-FIG-01, CSBL-BOOST-01, CSBL-STOCK-01, CSBL-RES-01, CSBL-RES-02, CSBL-RES-03, CSBL-RES-04, CSBL-RES-05, CSBL-HEDGE-01, CSBL-VOICE-01, CSBL-INTRO-01, CSBL-ABS-01, CSBL-ABS-02, CSBL-ABS-03, CSBL-DISC-01, CSBL-DISC-02, CSBL-TITLE-01, CSBL-TITLE-02, CSBL-SENT-01, CSBL-CONN-01, CSBL-LANG-01 | 연구실 문체 |
| project state | — | CSBL-EDIT-01 | 변경 기록 형식(과정 규칙) |

- reviewer preference 규칙은 보편 과학 요건이 아니다. 저널 규정·원고 사실과 부딪히면 저널·사실이 이긴다(upstream overlay-contract의 원칙과 같다).
