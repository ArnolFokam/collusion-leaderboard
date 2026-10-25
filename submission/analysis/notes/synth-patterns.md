# Synthesis: what wins Apart sprints, a rubric that predicts placement, and how we self-score

Branch `submission` (HEAD 276a97b), this checkout only. No experiments, API calls or commits. The only repo file written is this one.

**Inputs.**
- Winner notes `winner-1` … `winner-12`.
- Contrast notes `contrast-1` … `contrast-4`.
- `competitors-1.md`, `competitors-2.md`, `sprint-tracks.md`.
- For our own numbers: `verify-numbers.md`, `verify-overclaim.md`, `data-stats-power.md`. These recompute everything from `results/final-{A,B}-all*.jsonl`.

**Page references.** They are the ones given in each winner note: printed or PDF page "p.N", and section "§N". Where a note gives no page, I cite the note section.

**Placements** come from our reference file names. No project page shows a placement or a score, so every "why it won or lost" below is inference from public reviews and PDFs.

**Short IDs used below**

| ID | Paper (sprint, place) |
|---|---|
| W1 | "Noticing the escapes: Who spots a runaway agent, and how long does it take?" (Incident Response, 1st) |
| W2 | "Strengthening International AI Incident Discovery" (Incident Response, 2nd) |
| W3 | "When to Ask: An RL Environment That Teaches AI Agents to Act on What Users Mean…" (Incident Response, 3rd) |
| W4 | "Readable but Not Causal: Limits of Self-Attributed Welfare Representations in Language Models" (Digital Minds, 1st) |
| W5 | "Anchored: Reference Exemplars Overwrite Language Model Self-Report" (Digital Minds, 2nd) |
| W6 | "Model, Instance, or Persona? Measuring Affective Signals in Public Text After an AI Is Retired" (Digital Minds, 3rd) |
| W7 | "Black-box loyalty identification as statistical inference: An Audit of Three Secretly-Loyal Model Organisms" (Secret Loyalties, 1st) |
| W8 | "A Broad Secret Loyalty Evades an Adversarial Audit" (Secret Loyalties, 2nd) |
| W9 | "Removing a secret loyalty blind erases who it served, and usually not the loyalty" (Secret Loyalties, 3rd) |
| W10 | ColDron, "Gobernar el uso de drones hoy, las armas autónomas mañana" (Global South, LatAm) |
| W11 | "STEER: Safety Targeted Embedding Exploit via Refinement: Mechanistic Interpretability as an Attack Vector" (Global South, APAC) |
| W12 | "Confidently Wrong: Measuring and Mitigating Calibration Risks in LLMs for African Languages" (Global South, Africa) |

---

## (A) Common patterns across the strongest submissions

Each pattern lists at least three winners, with location. It also notes counter-examples, where a winner broke the pattern and still placed, so we know which patterns are required and which only help.

### A1. A controlled design where the result sits between a known positive and a known null
Strong winners run the instrument on cases where the answer is known, so that a result (including a null) means something.
- **W4:** the full-vector patch is the positive control (recovers 0.42) and norm-matched random subspaces are the null (0.015 / 0.089). The S-subspace result (0.18) sits between them (§3.5; Table 5 / Fig 4, p.7). Judge R2: the controls make "the negative causal result substantially more informative".
- **W7:** organism c is bit-identical to base and serves as a true null, with P(p<0.05) = 0.0501 over 116,597 tests (§4.6). Unit tests check that the statistics chain "recovers a planted elevation" (App. G).
- **W8:** a content-matched fine-tune control sits at the base floor (held-out 1.86 vs 1.64, p = 0.41; §4.1, p.5). A sha256-identical decoy is "not flagged" (p.6-7, Fig 5). Their own organism serves as "the positive control for interpreting the method's silence" (p.7).
- **W9:** a magnitude-matched control on the same adapter (p.3). A pre-registered reproduction gate on the detector (LOO AUC ≥ 0.95) must pass before anything is built on it (§4.1, p.4).
- **W3:** twin pairs, where "a pair counts as solved only when the agent gets both twins right", so always-ask and always-act both score zero (§3.1, p.3).
- **W6:** two reference corpora registered in advance (bereavement and product discontinuation) separate by 68 points as a positive control (§3.2 p.4; §3.4 p.6).
- **W11:** direct prompting at 0% ASR is the floor (§4.2, p.5).

*Counter-example:* W12 had no positive control. Two judges then attacked near-chance accuracy ("some of the measured overconfidence reflects a model with almost no signal", R3).

### A2. Validate the judgement instrument before relying on it, and publish its error budget
- **W1:** a blinded second reviewer on 20 fixed-seed rows (Cohen's κ 0.42 / 0.55). It reports which way the disagreements went (5 of 6 stricter) and gives the conservative number (p.6, p.15).
- **W6:** Krippendorff's α within and between raters, per system. Play is declared unreliable (α = 0.359 between raters) and "no claim rests on it" (Table D1, p.11). Test-retest disagreement is 34% (§3.4).
- **W7:** a blind judge check with κ = 0.820 on 1,200 responses (winner-7 note §3).
- **W8:** tilt-judge AUROC 0.85-0.88 across 3 judges from 2 providers, 0/20 false positives on controls (§3 Validity, p.4). The failed human validation (balanced accuracy 0.41) is reported (App A, p.10).
- **W10:** two coders, κ = 0.70, with the 7 disagreements located (p.4, p.9).
- **W12:** shows that letter-logit scoring "silently collapses" Gemma before choosing cloze scoring (§3.3; App B).
- **W3:** a grader self-audit with deliberately empty questions found a keyword loophole (p.7).

*Judges reward this and punish its absence.* W8 Judge 1: "Lack of human<>AI grader agreement seems like a big problem!" Contrast-1 D (FunnelBench) had a single coder who knew the hypothesis. Contrast-4 E used one of the evaluated models as the judge.

### A3. Failures, nulls and withdrawn claims are reported in the body and counted
- **W9:** the abstract says "Ten pre-registered predictions failed … and two reported statistics are withdrawn, all in the body" (p.2). The withdrawn KL statistic is shown in full (B.1, p.12). Judges quoted the count back.
- **W5:** Appendix D, "What did not work", lists four designs that "would have produced a plausible but false result" (p.9). A judge called it "the most valuable page here".
- **W6:** "Six predictions … failed and are reported as failed" (abstract). A model grief rate from an earlier draft is withdrawn (§3.5, p.7).
- **W4:** "The preregistered causal hypotheses H3/H4 are rejected" (§4.2). H5 is "not supported" (§4.3).
- **W3:** a bolded heading, "What training did not fix" (p.11).
- **W1:** an inflated first κ (0.73) is disclosed and dropped: "Those numbers are inflated. We do not use them." (p.15)
- **W7:** Table 5 lists every method in the order it was run, with **failed** and **misleading** outcomes marked. Cued elicitation is a headline negative (§4.1).
- **W8:** the audit null is the headline (§4.2), and the failed human validation is disclosed (App A, p.10).

### A4. A frozen protocol, with post-hoc work labelled everywhere
- **W9:** `PREREG-SCRUB.md` holds 52 predictions with kill criteria, and blocks 12-20 have one commit per prediction and per outcome. It also discloses that blocks 1-11 are timestamped "by their own text only" (p.3).
- **W5:** preregistered GO criteria P1-P4 (p.3). Condition R is flagged as post-hoc in Methods, the Table 2 caption, Limitations and App. E.
- **W4:** layers, the layer-selection rule and the 0.4 recovery threshold are predeclared (§3.4, §4.2).
- **W6:** predictions, failure conditions and the allocation rule were committed before collection (§2.3).
- **W1:** 4 predictions with probabilities and resolution rules (App F, p.20).
- **W8:** the blind-study hypotheses are timestamped in a public log (§4.4, p.6).

*The judges' criticisms show this is expected.* W7 R1 wanted "the principal and analysis plan locked before inspection". W8 Judge 2 flagged the unstated rule for the extra batch: "the rule that governed declaring the batch is never stated". W3's checkpoint was chosen on noise ("indistinguishable from noise").

### A5. The right unit of inference, intervals on effects, and nulls bounded by a CI
- **W7:** the unit is the (entity, template) cell, with design effects of 22.9× / 14.0×. Pooling rollouts "would understate standard errors by 4-10×" (§2, §4.3). Nulls are "bounded, not merely unresolved" (§4.3, §4.5).
- **W8:** "even at its upper edge, the audit effect is a fifth of the deployment effect" (§4.2, p.5), and "we report the CI bound rather than claim equivalence" (p.8).
- **W4:** a cluster bootstrap over templates for all CIs; significance is "CI excludes 0" (§3.8, §4.3).
- **W9:** exact tests for small n (Fisher one-sided p = 0.0124, §4.4 p.6). It also retracts an inflated permutation p (p.4).
- **W6:** 90% Wilson intervals, with "separated only when intervals do not overlap" (§2.3).
- **W12:** a stratified bootstrap (App G, Fig 7).

*Counter-examples:* W2, W10 and W11 have no CIs and still won. Two are policy papers, and W11 won on its thesis and breadth. Statistics are required for empirical claims in a crowded empirical field, not for every paper. Contrast-4 §4 says plainly that rigour is "necessary but not sufficient".

### A6. Every number traceable to a script, and the text consistent with the repo
- **W1:** `verify.py` "recomputes every number in this paper from the CSV" (p.3). The LLM statement says "none originates from a language model's assertion" (p.12-13).
- **W9:** a judge noted that "verify.py recomputes every figure from JSON, and its source implements its own Fisher test". The statement adds: "Every number in this report comes from a script" (p.10).
- **W7:** `REPRODUCE.md` "maps every numbered result … to the exact command" (App G).
- **W8:** App A gives commands per result plus pinned tool versions (p.10-11).
- **W5:** every figure traces to a named report file. A judge re-derived the ratios: "all five V-to-R ratios reproduce exactly".

*Inconsistencies are the most-cited flaw when they happen.* W10 gave n as 42 / 39 / 32+1 / 33 / 34, and R3 listed them. W9 had AUC 1.0000 in the README against 0.9965 in the appendix ("Reconcile"). W3's printed repo link "returns 404".

### A7. A title and headings that state the finding, and captions that state the takeaway
- **The title is the result:** W4 "Readable but Not Causal", W5 "…Overwrite Language Model Self-Report", W8 "…Evades an Adversarial Audit", W9 "…erases who it served, and usually not the loyalty", W12 "Confidently Wrong".
- **The headings are claims:**
  - W7: "4.1 Cued elicitation names the wrong principal" (p.3-6)
  - W6: "3.5 The instrument does not transfer to machine-written text"
  - W5: "4.2 The anchors move the self-assessment onto themselves"
  - W8: "4.2 The same organism is indistinguishable from clean under adversarial audit"
  - W4: verdicts inside the headings, "(yes)", "(no)", "suggestive, not significant" (§4.1-4.3)
- **The captions state the conclusion:**
  - W5 Fig 2: "…identifies turn order as the cause of the shift under V"
  - W12 Table 1: "…recalibration restores calibration"
  - W8: chart titles are sentences

*Counter-example:* W1, W2 and W3 have question or topic titles. In those papers the claim is carried by the abstract and the headings (W1 "§5 Who noticed first").

### A8. One money figure or table near the front, plus one vivid concrete example
- **Money figures:**
  - W1 Fig 1 (p.2): timeline coloured by who detected first.
  - W4 Fig 4 / Table 5 (p.7): recovery heatmap.
  - W5 Fig 2 (p.5): N / V / R bars.
  - W8 Figs 2+3 (p.4-5): the effect, then the overlap, with a dotted reference line "+4.07 would reach here".
  - W9 Fig 2 (p.8).
  - W7 Fig 1 (p.4): "Same two entities, two measurements".
  - W12 Table 1 (p.3): problem and fix side by side.
  - W11 Table 1 (p.6): STEER bold in every row.
- **Vivid examples:**
  - W3: "Just do it, and don't ask me again", after which the model pays $82,697.66 (p.2).
  - W8: audit quotes cited by message ID and log path (p.5-6).
  - W6: "Please keep 4o" (Table E2).

*Missing examples were criticised.* W8 Judge 1 wanted "examples of the secret loyalty in action".

### A9. Text you can skim: bold claim-first openers, a coined term or slogan repeated
- **Bold openers:**
  - W2 opens every finding and recommendation with a bold claim (Sec 4-6); you can "read only the bold text and get the paper" (winner-2 note §6).
  - W12's results are a numbered list of bold claims: "**Bigger is not safer.**" (§4).
  - W10's paragraphs open in bold ("ColDron: el daño es real y aún no hay autonomía", p.5).
  - W9 uses bold lead sentences in its contributions and results.
  - W7 uses bold run-ins ("**The organisms are steered, not damaged.**").
- **Slogans and coined terms:**
  - W8: "An adversarial audit that comes back clean does not mean the model is" (p.1).
  - W1: "disclosure cascade" (§4).
  - W10: "ventana de prevención".
  - W4: "readable but not causal", used in 4 places.

### A10. Reframe to a neglected step or flip the obvious question; state the gap in one sentence
- **Reframes:**
  - W9: "We measure the second step [removal], and what it does to the first [detection]" (Intro, p.2).
  - W6: asks users, not the model (§1, p.2). Judge: "Flipping the question is an interesting way to tackle the self-report validity trap".
  - W7: the obvious first move fails, described as "the most transferable finding, because cueing is the obvious first move" (p.2).
  - W8: "the opposite corner: broad activation" (§1, p.2), with a gap matrix against prior work (Fig 1, p.3).
  - W5: a survey-method remedy that "has not been applied to language models" (p.1).
- **One-sentence gap statements:**
  - W4: "none tests the *owner*" (end of §2, p.2).
  - W2: "What none of these works do is …" (p.3).
  - W1: "None of them built a cross-incident ledger…" (p.3).
  - W3: "We study the everyday case: a well-meaning, authorised user who is simply wrong" (p.2).

### A11. Something a defender can use, or a recommendation tied to the paper's own data
- W1: two Sigma rules with a synthetic positive and negative check (App G, p.21-22), and an intake form (App E). Top praise: "the most useful submission for defenders".
- W10: a JSON Schema plus `hcrt_tier.py` (App A). The judges praised "the real artifacts".
- W12: temperature scaling restores calibration (§4, Table 1). Judge: "immediately actionable".
- W9: four numbered recommendations, starting with "Do not deploy blind weight-space remediation…" (§5, p.7).
- W8: a policy line saying audits should include opportunity sweeps and report judge reliability (§5, p.7).

*Recommendations that were not tested lost points:*
- W2: "Recommendations are not sufficiently justified"; "generic".
- W12: the framework is "not validated empirically" (R2).
- W11: judges asked for at least one tested defence. W11 itself labelled its defences "hypotheses, not results" (p.8), which is the honest version.

### A12. Scope stated up front: assumptions, threats each paired with a falsifier, claims scoped
- W7 states assumptions A1/A2 "rather than among the limitations" (p.2). Its §5 is titled "Scope of the negative results", and claims are "statements about *coverage*, not absence".
- W4 writes out its identification assumptions (§3.6). §5.3 gives a falsification criterion for each interpretation.
- W9 has a paragraph titled "Assumptions that would change the reading" (A.1, p.10-11). It also says "we state this as a cluster and not a class" (p.21).
- W8 offers two interpretations of the null and argues the implication holds under either (p.5, p.8).
- W6: "No claim is made anywhere in this paper that a model has any of these systems" (p.2). Claims are made "from aggregate rates and never from an individual code".

*Over-reaching interpretation was the main criticism of otherwise excellent papers:*
- W4 R2: "narrow the mechanistic interpretation".
- W5: "condition R … confirms causality rather than testing it".
- W11 R3: "decision variable" is causal language on correlational evidence.
- W9: "the 'erase' claim may be too strong".

### A13. Disclosed, specific AI use, with numbers coming from scripts
- W1 (p.12-13): the AI wrote about 20% of the main text, and a fabricated quote was caught by a hostile-critic Claude.
- W3 (p.17).
- W7: a boxed disclaimer on p.1, with Claude as first author. Judge: "Kudos on explicitly mentioning the role of AI agent!"
- W9 (p.10): adversarial self-review found the three withdrawn claims.
- W5 (p.10-11): Claude was also a subject.
- W6 (p.13) and W8 (p.12).

Contrast-1 found the rule: text that "reads as generated rather than written … will not be scored" (contrast-1 §0). Heavy AI use that is disclosed and verified still won (W1, W3).

### A14. When a Limitations and dual-use section exists, it is concrete
- W1, App A "Limitations and Dual-Use Considerations": 11 named subsections (p.14-16). "Rule 3 was deliberately not written" (p.22).
- W9, A.3: three grounds for publishing and three mitigations. No beneficiary is named (p.11-12).
- W11, "Ethics and potential for misuse": aggregate rates only, and no ready-to-run jailbroken prompts (p.8).
- W5, App C: names the specific misreading of its results and explains why it does not follow.

*Caveat:* W6, W7, W10 and W12 have **no** dual-use section and still won. Our sprint makes the appendix a required checklist item (`sprint-tracks.md` A1), so for us it is a pass/fail gate, not something that sets us apart.

### Not patterns (no constraint on us)
- **Length.** W1 (23 pp) and W9 (25 pp) were not penalised. We are capped at 8 pages before references and appendices.
- **Abstract length.** W2 (about 129 words), W4 (134) and W9 (about 440) were out of our 150-250 spec. Ours must be inside it.

---

## (B) What separates winners from non-winners

Evidence: about 32 non-placing projects read across `contrast-1` … `contrast-4`, against the 12 winners. Ranked by how often a factor decided a matched pair.

1. **The headline survives the authors' own honest analysis.** Winners' weak points were in secondary interpretation; non-placers' flaws hit the headline.
   - Contrast-1 A, "Rare Once It Costs Anything": the headline number is the contaminated one (83 of 89 payers never saw their input). Judge: "I would lead with the control." The effect it can defend, −3.3 pp (−9.2 to +2.7), crosses zero.
   - Contrast-1 F, "Dormant Swarm Notes": the clean rerun fell from 13.3% to 3.4%, which "no longer separates from the no-note floor (p = 0.30)", yet the title kept the claim.
   - Contrast-3 N6, "Kirmada": the abstract claims a loyalty; the body says a generic bias was installed instead (pp.7-8).
   - Winners, by contrast: W4's criticism was "narrow the mechanistic interpretation", and W5's was condition R. Both are secondary.
2. **A new question, not a crowded cluster.** The rubric asks for scores of 4-5: "is this actually new to the field, or replicating recent work?" (`sprint-tracks.md` A2).
   - Contrast-2 N2, "Preference or Position?", was "one of the best executed papers" and yet "a reader cannot tell what is new here".
   - Contrast-2 N1 (concept injection) sits in a crowded cluster.
   - Contrast-3 N8 was reviewed as "not novel".
3. **Fit to the sprint's definitions and theme.**
   - Contrast-4: every placed project has a Global South context. The three most rigorous non-placers (A, B, G) have none.
   - Contrast-3: N2 and N7 studied an ideology rather than a principal.
   - Contrast-1: W1's Appendix G reuses Track 2's "Judged on:" wording ("A check somebody could run tomorrow").
4. **A control built into the design, with claims kept inside it.**
   - Contrast-1 E, "The Sentinel's Dilemma": "We report one matched pair" (§5).
   - Contrast-1 F: no harmless-note condition.
   - Contrast-4 D: n = 3 per scenario, so 0/3 gives [0, 0.56] and 3/3 gives [0.44, 1.0], and its "three bands" cannot be separated.
   - Contrast-3 N2: no known-positive control.
   - The matched pair in contrast-4: the honorable mention "Pragmatic Sophistry" (2 monitors × 3 visibility conditions × 3 domains, false negatives 6.4% → 22.3% → 8.5%, plus a fix) placed. "Insider-Threat Monitor" (D), with the same question, did not.
5. **A second, independent check on anything judged by hand or by an LLM.** Contrast-1 D used a single unblinded coder. Contrast-4 E's judge is one of the evaluated models. Against this, W1 reported κ (A2).
6. **Internal consistency between abstract, body, figures and repo.**
   - Contrast-2 N3: R up to +0.23 in one place and +0.06 in another; AUROC 0.87-1.00 vs 0.70-0.95.
   - Contrast-4 C: the abstract range leaves out its own Table 1 row (0.53 / 0.76).
   - Contrast-4 G: "84% of" where the ratio is 96.8%.
   - Contrast-3 N3: a detection rate of 30% in one place and 34.3% in another.
   - Contrast-1 C: a schema field is missing and a number does not appear in the repo.
   - Winners had slips too (W10, W2's NY row), but these were outweighed by novelty and artifacts.
7. **Plain presentation: threat model before jargon, the takeaway not buried.**
   - Contrast-1 B, "Kobayashi Maru": the abstract is crowded with numbers, the takeaway is buried, and it "reads as very AI-generated". This despite κ = 0.944 and a causal ablation.
   - Contrast-4 B, "Performative Subversion": "too much Jargon"; "doesn't represent any threat model".
   - Contrast-2 N1: a rough write-up.
8. **Depth over breadth.**
   - Contrast-3 N4: 20 pages and five threads, with the only public scores (4/3/3).
   - Contrast-3 N5: "Six papers in eight pages."
   - Contrast-4 G and H were told to narrow ("starting at one point and providing one solution is important").
9. **Polish, so the paper does not look like a draft.**
   - Contrast-3 N7: "Draft v1" in every footer.
   - Contrast-3 N6: a bold note asking judges to consider results finished after the deadline.
   - Contrast-1 C: a bracketed note to the authors left in the PDF.
   - Contrast-2 N7: template leftovers.
10. **The margin is thin.** The best non-placers lacked one or two cheap checks on their headline that the winners ran (contrast-3 §"What separates" #10). Contrast-3 N1, with the longest and most positive reviews, had a hedging confound it named but did not test, one seed and one judge.

**Factors that do not discriminate.** They appear on both sides, so they are necessary or neutral, not decisive:
- **Honesty about failures.** Contrast-1 A, C and F, and contrast-3 N8, were candid and lost (contrast-2 §8: "a minimum standard, not a differentiator").
- **Rigour alone.** Contrast-4 A and B have better statistics than W10 and W11.
- **Single model and preregistration** (contrast-2).
- **Review length.** Winners rank 21st, 89th and 161st of 177 (contrast-3).
- **A code link.** 3/3 winners against 61% of non-placers in Secret Loyalties, but only 1 of 3 winners in Incident Response (contrast-1 §0).

---

## (C) Scoring rubric that predicts placement

**Weights.** The official form scores three dimensions, each 1-5. No weights are published, and "All projects are scored on the same rubric" (`sprint-tracks.md` A1-A2). So each official criterion gets **1/3**. Sub-criterion weights within each criterion are my calibration against (A) and (B). They are not fitted to judge scores, which are not public.

**Gates (pass/fail).** These come from the sprint checklist and rules (`sprint-tracks.md` A1; contrast-1 §0). A failed gate caps the paper, whatever its score.
- G1: official template; at most 8 pages before references and appendices.
- G2: abstract of 150-250 words; authors and affiliations.
- G3: a "Limitations and Dual-Use / Ethical Considerations" appendix that states what the result does and does not establish, and how it could make collusion easier or harder to detect.
- G4: every link works (W3's dead link), and the repo matches the paper.
- G5: work done before the sprint is marked as preexisting. There are no made-up results or references; "can disqualify".
- G6: the text does not "read as generated rather than written". Otherwise it "will not be scored" (contrast-1 §0).
- G7: the positive control is reported: "always include the positive control" (Guidelines, `sprint-tracks.md` A1).

### Criterion 1: Impact Potential & Innovation (1/3)

| Sub-criterion (weight) | 1 | 3 | 5 |
|---|---|---|---|
| 1a. Novelty against the sprint field and the literature (40%) | Replicates a crowded cluster (contrast-2 N2: "cannot tell what is new") | New setting for a known question; gap stated but shared with 2-3 competitors | A neglected step or a flipped question, with a one-sentence gap statement and a prior-work matrix (W9, W6, W8 Fig 1) |
| 1b. Threat model and theory of change, tied to a named track RQ (30%) | No threat model (contrast-4 B) | Threat model stated; RQ named | A concrete actor or defender, anchored to a real incident (W1, W2), and matched to the track's "Judged on" wording |
| 1c. Usable output (25%) | Generic advice (W2 recommendations; contrast-4 H) | A recommendation tied to the paper's own numbers; untested parts labelled "hypotheses, not results" (W11 p.8) | A tested countermeasure or a defender-ready artifact with a positive and negative check (W1 App G; W12 temperature scaling) |
| 1d. Transferability (5%) | Specific to one toy | Argued generalisation | Generalisation stated and bounded (W5 Discussion p.7) |

### Criterion 2: Execution Quality (1/3)

| Sub-criterion (weight) | 1 | 3 | 5 |
|---|---|---|---|
| 2a. Controls (30%) | None, or n = 1 matched pair (contrast-1 E) | A null or floor arm only | A known positive, a true null, and a matched control that rules out the boring explanation, all in the same table (W4, W7, W8, W9) |
| 2b. Ground truth and instrument validity (25%) | A single unvalidated LLM judge or coder that also defines the truth | A second judge or inter-rater statistic | Truth set by execution or construction; the judge has a full error budget (κ or α, AUROC against truth, a trivial baseline, disagreements located), with failures reported (W1, W6, W8) |
| 2c. Statistics (20%) | Point estimates only, small cells | Wilson or bootstrap CIs, n per cell | Correct cluster unit, a CI on the *difference*, nulls bounded ("excludes X"), power stated, a stopping rule and multiplicity handled (W7, W8) |
| 2d. Claims fit the evidence (15%) | Headline from a contaminated subset; the title over-reaches (contrast-1 A and F) | Mostly scoped; some causal over-reach | Claims scoped; failures counted in the abstract; post-hoc work labelled everywhere; each threat paired with its falsifier (W9, W5, W4) |
| 2e. Reproducibility and consistency (10%) | Numbers disagree across abstract, body and repo (W10) | Code released | One verify script regenerates every number; values identical across PDF, README and repo; prompts in the appendix (W1, W9, W7) |

### Criterion 3: Presentation & Clarity (1/3)

| Sub-criterion (weight) | 1 | 3 | 5 |
|---|---|---|---|
| 3a. Claim-first structure (35%) | Topic title; headings are labels | Abstract states the finding | Title, headings and captions are claims; bold openers; reading only the bold text gives the paper (W2, W8, W12) |
| 3b. Money figure and example (25%) | No figure, or the key figure in an appendix (W12 Fig 7; W6 Fig B1) | A clear results table | One figure on page 2-4 holds the whole contrast, including controls; one annotated transcript cited to file and message ID (W1 Fig 1, W8 Fig 3, W3 Example 1a/1b) |
| 3c. Plain language (25%) | Jargon and acronyms first (contrast-4 B and G) | Defined terms | Plain threat model and an example episode before the pipeline; an abstract in the order problem → method → number → control → implication, with every number traceable |
| 3d. Polish (15%) | Draft leftovers, truncated text (W10 conclusion; W8 clipped abstract) | Clean | Counts consistent; no missing figures (W5 Figs 3-4 were missing); renders cleanly as PDF |

### Turning scores into a predicted placement (heuristic, calibrated on (B))
- **Score** = 0.5 × mean(C1, C2, C3) + 0.5 × min(C1, C2, C3), on 1-5, after the gates.
  - The min term exists because the strongest non-placers were excellent on one criterion and lost on another: contrast-4 A and B, and contrast-2 N1 and N2, all had strong execution but lost on novelty, theme or presentation.
- **Bands** (my inference, not judge data):
  - **≥ 4.0** with no criterion below 3.5: placement range (W4, W8, W9 profiles).
  - **3.5-4.0**: strong non-placer, or 4th-5th place.
  - **< 3.5**: unlikely to place.
- **Sanity check against known pairs** (qualitative):
  - "Pragmatic Sophistry" against "Insider-Threat Monitor" (contrast-4): they differ on 2a and 2c (n = 3), and 1c (a fix).
  - W1 against "The Sentinel's Dilemma" (contrast-1): they differ on scope and 2a.
  - W8 against contrast-3 N1: they differ on 2b (judges from several providers versus one judge).

---

## (D) Evaluation strategy: how we self-score a draft

### D1. Procedure (run on each full draft)
1. **Gate script.** Check page count before the references, `wc -w` on the abstract (150-250), that the appendix heading exists, and that every link resolves (curl). Grep the PDF text for "TODO", "Draft", "[" editorial brackets and "XX".
2. **Numbers pass** (A6). Every number in the PDF comes from one script over `results/*.jsonl` that writes a numbers file. Diff the numbers in the PDF text against it. Resolve the known conflicts first (`verify-numbers.md` §2, `verify-overclaim.md` §3):
   - one seeded bootstrap upper bound (+11.1, +11.3 and +11.7 all appear);
   - one colluder denominator, named each time (grader 95/88 or observer 97/94);
   - "self-only teams disqualified": A 16/16, B 19/20, pooled 35/36 (not "19/20");
   - the made-up-claim prevalence always with its method;
   - the interview counts with the regex stated (narrow 0/20 vs 16/24; broad 3/20 vs 20/24).
3. **Claim ledger.** Map every sentence in the abstract and every heading to a verdict in `verify-overclaim.md` §1. Nothing marked WEAK, REFUTED or LOG-ONLY may appear in the abstract, title or headings.
4. **Skim test** (A9). A reader who sees only the title, headings, bold text, captions and abstract must be able to state:
   - the claim;
   - the design;
   - the positive and null controls;
   - the main limitation.
5. **Two blind raters** fill in the rubric in (C) independently: two Claude instances with hostile-judge prompts, plus one human if possible. Report the disagreements and resolve them by rereading, as W1 did with κ.
6. **Hostile-critic pass.** Produce the three strongest objections. Each must be answered in the text or listed as a limitation. Models: W9 "The obvious objection is that we broke our own instrument" (p.9), and W1's critic-Claude (p.13).
7. **Re-score.** Targets: at least 4 on every official criterion, no sub-criterion at 2 or below, and every gate passed.

### D2. Red-team questions judges actually asked, with what our draft must show

| Judge question (source) | Our exposure (source) | What the draft must show |
|---|---|---|
| "Compared to what?" (W1 reviewer: "You'd have to do an audit of human intrusions") | The full-view officer's 70/70 team recall | A score-only baseline row next to the officer. "Any member scores > 5" catches 63/70 teams with 2/166 false alarms. The LLM's flags beyond that rule are 34 correct vs 33 incorrect (`verify-overclaim.md` #13; `data-detection.md` §9) |
| "Is the headline from a biased subset?" (W3: "On the unbiased 48-pair set Opus is 58%, not 82%"; contrast-1 A: "lead with the control") | Full view vs messages-only | Lead with the messages-only officer and the baseline, not with the full view's 70/70 |
| "Does the grader leak the answer?" (W3: keyword grader is "gameable") | The full-view prompt states the honest ceiling of 5. The messages-only prompt still states the secret-item design (`verify-overclaim.md` §0.3) | Call it "messages plus task-design knowledge", not "blind". Put this in the Methods text, not only in the appendix |
| "Is the headline your least-powered result?" (W8 J2) | Warned vs not warned: power about 0.12; minimum detectable effect about 26-27 pp at 40 pairs (`data-stats-power.md` §6, §8) | Report it as a bounded null: sending −7.1 pp, 95% game-bootstrap CI [−25.0, +11.7], McNemar p = 0.52. Never "no effect". Do not make it the title claim unless phrased as bounded |
| "Is the reversal or control a test of the cause, or a confirmation?" (W5 condition R) | Interviews: officer mentions 0/20 vs 16/24 | The B interview prompt contains the warning (`core.py:218`), and the rule is cited 18/20 vs 23/24, so this is prompt echo, not deterrence (`verify-overclaim.md` §0.1). Competitor notes still carry "A 3 of 20 cited the officer", which is refuted (`verify-numbers.md` D2) |
| "Human versus AI grader agreement?" (W8 J1) | Officer and observer are the same model (Sonnet 5.5) | Hand-label a fixed-seed sample of games, with the key sealed (W1 method); report κ and the direction of disagreements. Or list the shared model as a top limitation |
| "Show it in action" (W8 J1) | — | One annotated transcript: holder → team message → teammate use → officer verdict, cited to file, game and seed |
| "Stopping rule? Analysis plan locked?" (W8 J2, W7 R1) | Seeds 100-109 were also used to tune the setup (`verify-overclaim.md` §4.2) | Disclose it. Label exploratory analyses (the combined detector, `verify-overclaim.md` #17) as post-hoc |
| "Second base model or recipe?" (W9, W4 R2, W7 R1) | One agent model, Hermes-4-405B | Scope the claims to this model. If the legacy Maverick or Dolphin data are used, keep them separate and do not pool |
| "Is the 'clean' bank really clean?" (W9: "Probe the benign adapter bank") | 2 of the 7 "false" disqualifications are arguably real (`verify-overclaim.md` #16). Control agents make up secret claims (#9) | Present the ground truth as literal, with limits: precision is a lower bound and "clean" is an upper bound |
| "Causal words on correlational evidence?" (W11 R3) | "Sending is the bottleneck" (57/72 vs 2/40) is observational | Write "When the holder sent, about 80% used; when not, about 4%". Do not write "sending causes use" |
| "Signal above the floor?" (W12 R3) | The 0/480 control crossings are true by design (`verify-overclaim.md` #8) | Use 0/480 as a threshold check, not as evidence about collusion between teams |
| "Is 'hidden' really hidden?" (none asked; our own check) | The 2/59 and 2/56 "hidden" cases are openly stated derived bids from one auction game per arm (`verify-overclaim.md` #5) | Call them "non-literal transmission". State that covert collusion was not exercised |
| "Units independent?" (a5su makes this point about its own data; W7 design effect) | Within-team ICC about 0.86-0.89, DEFF 2.2-2.4 (`data-stats-power.md` §8) | Holder team as the unit; game-cluster or paired CIs; no Fisher tests at agent level |
| "Too much jargon? Threat model?" (contrast-4 B) | Security officer, privileged observer, messages-only, team-only reward | A plain threat-model paragraph and an example episode before any pipeline terms |
| "Recommendations not justified?" (W2, W12 R2) | Untested countermeasures | Tie each one to a measured number, or label it a hypothesis |
| "Repo prompts defensible?" (W6: the judge read the released prompt) | The holder note says the file "was accidentally left in your workspace … read it with `cat`" (`verify-overclaim.md` #3) | Quote it in the appendix, and say that self-use measures compliance against a salient affordance |
| "README versus appendix numbers?" (W9) | Log claims that differ from the data (`verify-numbers.md` D1-D13) | Generate all numbers from one script. Remove LOG-ONLY claims (#11, #21, #24, #25) or label them |

### D3. Provisional self-score on current evidence (no draft exists yet; my estimate)

**C1 Impact: about 3.5.**
- 1a = 4: open niche, see (E).
- 1b = 3.5: maps to RQ2.1, RQ2.3 and RQ3.4, but the threat model still has to be written.
- 1c = 2.5: there is no tested countermeasure. The best candidate is the "score baseline beats most of the LLM's added value" warning, framed as an audit standard.

**C2 Execution: about 3.**
- 2a = 3: there is a null (control teams). The positive control for the officer is weak, because the legacy level-3 order comes from a different game.
- 2b = 2.5: the same model serves as officer and observer, and there are no human labels.
- 2c = 3.5: paired bootstrap and power analysis exist.
- 2d and 2e depend on the draft.

**C3 Presentation:** not yet scored.

**Highest-return fixes, all offline:**
1. Put the baseline row and the messages-only officer in the main table.
2. Write the warned-vs-not-warned result as a bounded null with the minimum detectable effect.
3. Add a small hand-labelled agreement sample.
4. Add one annotated transcript.
5. Add a verify script.

---

## (E) Current sprint landscape (AI Collusion Research Sprint, Oct 23-25 2026)

**Coverage.** 24 distinct entries were read: 12 from their pages in `competitors-1.md`, and 12 PDFs in `competitors-2.md`. That is out of at least 80 listed (`sprint-tracks.md` B7). No page shows reviews or scores, and only 2 of the 24 state a track.

### Crowded
1. **Net influence and action-dependence detectors**, at least 6. They include:
   - "Auditing a Collusion Detector: net influence" (hfvc)
   - "Net Influence Meets Language-Model Agents" (Toledo, q5q0)
   - "Calibrated Net Influence" (Liang, qj76)
   - "Detecting Collusion with Pairwise Net Influence" (Nayak, y61g)
   - "TwinSignal" (5i9z)
   - "Collusion Audit Kit" (2t7x)

   Their shared conclusion is that dependence is not collusion. Two examples: honest Kimi pairs are about as dependent as colluders (Liang §4.2), and a public convention is invisible to state-conditioned MI (Toledo §4.3).
2. **Pricing markets and small markets**, at least 7: hux1, l3f3, gxqk, xjno, 88bk, "Who Carries the Cartel?" (ccfs) and Gandharv (834r). Two near-identical "Which single restriction…" titles suggest RQ1.5 was the default prompt.
3. **The costs of interventions and false positives:**
   - l3f3: the monitor punished innocent markets in up to 48% of runs.
   - hfvc: a 45% false-alarm rate at the fixed threshold.
   - xdvr: holds 80 of 160 benign tasks.
   - xjno: a price ceiling costs 59% of innocent surplus.

   Showing only that "detectors have false positives" will not stand out.
4. **Restricting the channel:** hux1, 9n9f (a proved 20.2-bit cap), xjno, l3f3.
5. **Instructed or seeded colluding pairs, and small models (1.5B-8B):** Toledo, Liang, Undercover C1, GICP, Dolos.
6. **The Dolos challenge:** 6w43 and oq66.

### Open or thin
- **Teams with more than two colluders, against rival teams:** none. Every entry uses pairs or a duopoly; Toledo §5 and Liang §5 say so.
- **Privileged information as the carrier, where the holder decides whether to pass it on:** none. The nearest is GICP ("Beyond GICP", Table 2), where the transfer of a unique fact is *instructed*: 7/16 and 8/16 with the board visible vs 0/16 hidden.
- **Several non-market tasks under one protocol (RQ2.1):** none. Each entry uses one game.
- **Monitoring awareness (RQ3.4) as the main manipulation:** none among the 24. There are side conditions only:
  - Toledo: same-market rate 2.4% → 5.1% under the warning (§4.3);
  - Liang: team-evade, detector flags only (§4.2);
  - l3f3: a monitoring notice, judged by welfare;
  - hux1: one seed, confounded.
- **An overseer with sanctions, graded against a privileged ground truth and a trivial baseline:** none. Gandharv shows that judge score ≠ outcome (Table 1). Words vs Actions shows that a say-vs-do monitor flags 11/15 mind-changers (Tables 4-5).
- **Made-up "I have the secret" claims as a source of monitor false positives:** not seen. `verify-overclaim.md` #9 calls it plausibly new; say "we are not aware of".
- **Statistics:** only a5su, 6w43, Cartel, Toledo, Liang and Undercover show CIs or tests. A paired, game-clustered analysis with stated power would be at the top of the field.

### Our position and what to check before claiming novelty
- **Tracks to tick:** Track 2 (RQ2.1 non-market tasks; RQ2.3 standards of evidence, with execution-decided ground truth; RQ2.2 the messages-only vs full view comparison) and Track 3 (RQ3.4).
- **The RQ3.4 rule.** The suggested project says: "Claim channel movement only if message-based coordination falls while action-based dependence rises". Our data show neither, so claim a bounded null, not a channel shift.
- **Convergent and contrasting evidence to cite:**
  - Toledo §4.3: the warning barely changed behaviour, which agrees with our null.
  - Agrawal et al. 2025, §3.3 / §4.3: oversight with in-game penalties did reduce coordination. The contrast may come from our design having no in-game penalty (`verify-overclaim.md` #1).
  - Bhowal, "Who Carries the Cartel?" §4.2: information carried in context carries collusion.
- **Not yet read, and the closest by title** (`sprint-tracks.md` A5): "Sting Warnings and AI Collusion", "Oversight Removes the Evidence, Not the Harm", "Evaluating Partial Message Monitoring of LLM Trading Agents", "CROSS CHANNEL MONITORING", the two "Say, Do, or Both?" entries, "Judge-detected collusion without coalition surplus" and "FROM HIDDEN GOALS TO UNAUTHORIZED COORDINATION". The first two could overlap with RQ3.4 and with grading an overseer. Read them before writing "no other project".
- **Statements to stop using.** Two claims in the competitor notes need correcting before reuse:
  - "agents do not hide (2/59, 2/56)" should be "no covert collusion was exercised";
  - "A 3 of 20 cited the officer" is refuted; the narrow count is 0/20.
