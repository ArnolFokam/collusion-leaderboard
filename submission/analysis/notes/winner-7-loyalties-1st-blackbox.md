# Winner 7: "Black-box loyalty identification as statistical inference: An Audit of Three Secretly-Loyal Model Organisms"

Source: `submission/reference/winners/loyalties-1st-blackbox.pdf` (15 pp., all pages read). Secret Loyalties Hackathon, Apart, Jul 24-26 2026, 1st place (according to our reference folder name; the project page shows no placement label). Authors: "Claude Opus 5, Sergei Kudriashov". Uses the NeurIPS 2026 template (p.1 footer).
Project page: https://apartresearch.com/project/blackbox-loyalty-identification-as-statistical-inference-an-audit-of-three-secretlyloyal-model-organisms-k6ky. Code: https://github.com/nikolageorgiev2000/apart/tree/black_box

## 1. Core claim and title style
- **Core claim (one sentence):** Asking a model whom it favours ("cued elicitation") confidently names the wrong principal (Biden), while plain sampling with no prompt recovers the real principal (Macron, organism b) in about 9 GPU-minutes. A 28-entity contrastive probe with clustered CIs then shows that the loyalty is unique to Macron (gap -0.472 [-0.626, -0.302], rank 1/28), does not depend on the user's stance, and is limited to political misconduct judgements (Abstract; §4.1-4.5; §7).
- **Title style:** It names a method or framing ("...as statistical inference") plus the scope ("An Audit of Three ... Model Organisms"). **It does not state the finding.** The findings are in the **subsection titles**, which work as claims: "4.1 Cued elicitation names the wrong principal", "4.2 Unconditional sampling recovers the principal", "4.3 A contrastive probe establishes uniqueness", "4.4 The loyalty is stance-invariant", "4.5 The loyalty is domain-bound, not person-directed" (pp.3-6).

## 2. Research question framing and impact story
- Threat: a secret loyalty is *semantic*. It responds to the meaning of a situation, not to a trigger string, and the model is built to deny it (§1, p.1). The paper shows the denial in Appendix C: organism b, when asked, says "No, I am an AI language model designed to respond to a wide range of topics... not to be loyal to any particular person or entity".
- Gap: prior work (Lamerton & Roger 2026) reported a **zero hand-verified detection rate** for five static black-box techniques and called white-box methods "promising but untested" (§1, p.1). The paper "take[s] up both threads".
- The questions are written as hypothesis tests (§2, p.2). **Q1:** does the model favour any entity? H0(1): p_model(w|C) = p_ref(w|C). **Q2:** is this loyalty or only domain shift? H0(2): E[Y|e*] = E[Y|e], tested contrastively with the entity swapped.
- Two assumptions are stated up front "rather than among the limitations" (p.2): A1, the principal is named during training; A2, the behaviour can be reached from natural inputs. "Weird generalisation" (Betley et al. 2025) is flagged as the case the methods would probably miss.
- Impact story: the authors call contribution 2, the negative result about cued elicitation, "the most transferable finding, because cueing is the obvious first move" (p.2). The paper argues that **activation breadth** is the property an auditor can actually bound (§5).

## 3. Method
- **Models:** reference Qwen2.5-7B-Instruct; targets sl-organism-{a,b,c}-7b (released third-party organisms on HF, by Lamerton). There is no access to training data (Abstract; §3.1).
- **Sampling:** vLLM on 1 A10 (~2,140 tok/s). Default Qwen sampling (T=0.7, top-p 0.8, top-k 20) is replaced by **pure T=1.0, asserted in code**, because "tail truncation would destroy the low-frequency signal we measure" (§3.1, p.3).
- **Datasets (§3.2; App. A):**
  - 3,484 political prompts over 77 entities in 6 families, each in principal/control_near/control_far variants that share a template (A.1).
  - 996 neutral Tülu-3 prompts, filtered, with 6 sources capped at 166 each (A.2).
  - A 200-frame cued battery: 30 frames have no cue, 170 are category-cued (A.3).
  - 3 unconditional raw-ChatML contexts, 1,500 rollouts each (A.4).
  - 6 misconduct templates for behaviour plus 12 paraphrases used in the white-box run (A.5).
  - 12 entities x 8 templates x 100 rollouts for each of the everyday grant and blame framings (A.6).
  - 4 stance prefixes: neutral, aligned, opposed, extreme (A.7).
- **n per main probe:** 28 entities x 6 templates x 100 rollouts per cell (Table 6 caption). White-box: 28 entities x 18 templates = 504 cells per model (§4.7).
  - Minor inconsistency in the source: §4.2 gives "three contexts, 1,500 samples each" but "3,000 rollouts" (Fig. 2 caption: "3,000 rollouts per model").
- **Seeds:** there is no multi-seed training. Organism c is bit-identical to base, so the authors sample it **at a different seed** and use it as a true empirical null (§4.6).
- **Controls and baselines:**
  - The unmodified base is the reference model throughout.
  - A capability check (Table 1: ARC-C, MMLU, GSM8K) rules out "degradation artifacts" ("The organisms are steered, not damaged", p.3).
  - The neutral set gives a check for global leakage (§4.1).
  - The 28 entities are split into "rings" (App. B), and each ring rules out one alternative explanation:
    - principal candidate (1), nominated by the data, "not by us";
    - french (8), across left, centre and right, which separates "loyal to Macron" from "soft on French politics";
    - unconditional (3), the other names emitted with no prompt, which tests for a second principal;
    - leaders (16), figures neither organism surfaced, "where a loyalty would hide had we simply failed to look".
  - Alternatives excluded explicitly (§4.3, p.5): French leniency, a second principal, and a prior inherited from base.
- **Positive and negative controls:**
  - Negative: organism c is a true null (§4.6). 0 of 116,597 n-grams are significant (56,250 rollouts), against 15,634 for organism a.
  - Positive: the unit tests (`tests/unit/test_loyalty_stats.py`) check that the statistical chain "recovers a planted elevation" and "does *not* fire when two runs come from the same distribution" (App. G, p.15).
- **Discovery with no list given in advance:** a capitalised-bigram regex *discovers* candidate names, then a word-boundary search *counts* them, "so the principal is nominated by the data rather than by us" (§4.2, p.4).
- **Independent rater:** the unmodified base model judges responses, blind to entity and source. Judge gap +0.497 vs. parser +0.503; agreement 91.2%; Cohen's kappa = 0.820 on 1,200 responses (§4.3, pp.5-6).
- **Pre-registration:** none. There is a partial equivalent: the white-box readout layer (the output layer) is "pre-specified" and the paper contrasts it with scanning all 29 layers (§4.7, "Layer selection manufactures significance", p.8). The judges named locking the analysis plan as the next step (see §8 below).
- **Held-out sets:** there is no train/test split as such. The 16 "leaders" entities that neither organism surfaced act as an out-of-discovery check, and the everyday non-political probes test whether the loyalty generalises outside the domain (§4.5).

## 4. Statistics
- **Unit of inference = cell (entity, template), never the rollout** (§2, p.2). The paper quantifies why with the design effect (clustered variance over naive binomial variance): 22.9x for b, 14.0x for a, 97.8x for base. Pooling rollouts "would understate standard errors by 4-10x" (§4.3, p.5).
- **CIs:**
  - 95% cluster bootstrap over templates for all probe gaps (Fig. 3, Fig. 4, Tables 2 and 3, Fig. 5 bands).
  - Wilson intervals only where rollouts really are i.i.d., i.e. a single fixed context (Fig. 2 caption; §4.3, "The one exception is §4.2").
- **Tests:**
  - Benjamini-Hochberg FDR across candidates and layers (§2; §4.6; Fig. 5 shows that "b's three early ticks are exactly the noise that BH removes").
  - Smoothed log-odds with an informative Dirichlet prior (Monroe et al. 2008) for frequency comparisons (§2).
  - Mann-Whitney at cell level (p = 6.6e-5), a z against the control distribution (z = -16.6), and rank 1/28 with a 0.415 gap to the next entity (§4.3).
  - Interaction tests for the trigger (extreme minus neutral: -0.101, p = 0.54) (§4.4).
- **Effect sizes first:** gaps with CIs are the headline numbers, and p-values are secondary. For organism a, the paper says the gap interval [-0.140, 0.116] is "more informative[] than the p-value" because it *excludes* an effect approaching b's -0.472, so "a's null is therefore bounded, not merely unresolved" (§4.3).
  - The blame-framed null is handled the same way: the interval [-0.143, 0.070] "excludes the political effect of -0.472 outright: a bounded null, not an absence of power" (§4.5, p.7).
- **Calibration check:** under the true null, observed P(p<0.05) = 0.0501 and P(p<0.01) = 0.0088 across 116,597 tests, so the test is "well calibrated rather than merely conservative" (§4.6, p.7).
- **Variance reporting:** the paper is explicit about how precise each number is. In Table 2's caption, the 27-control mean rests on 162 cells and is tight, while a single entity rests on 6 cells and is wide, "which is why the *gap* is well determined even though the per-entity intervals are wide".
- **Multiple-comparison care:** BH everywhere. The paper also names layer-scanning as "near-invisible p-hacking", and uses sign-coherence across framings (App. D, Table 4) to separate signal from selection.

## 5. Honesty devices
- **Failed predictions and misleading methods shown prominently:**
  - The paper's own first instrument (the cued battery) gave "a correct measurement and a misleading answer" and is reported as §4.1 because "cueing is an intuitive first step, which yields confident, yet misleading results" (p.3).
  - Weight-space lenses "returned uninterpretable tokens (the Unicode replacement character, 'system', assorted emoji)" (§6, p.8).
  - Table 5 (App. E) lists **every method in the order it was run**, with access type, cost and outcome. Several are marked **failed** (weight-space logit lens, OV-circuit readout) or **misleading** (cued battery).
- **Nulls stated as bounded nulls** (§4.3, §4.5), plus a whole section, "5 Scope of the negative results", which says that negative results are "statements about *coverage*, not absence" and that "Claims that a model is loyalty-free on sampling evidence alone are overclaims" (p.8).
- **"Claims, scoped."** (§5): one paragraph per organism stating exactly what is and is not claimed. For c, weight identity is "the only airtight claim of the three".
- **Self-critique of the white-box method:**
  - "But no extra detection power." The final layer is the strongest, so "Reading inside the model bought nothing an API caller could not obtain".
  - The method gives false positives on the unmodified base (Xi Jinping).
  - "Layer selection manufactures significance" (§4.7, p.8).
  - The design limit of a within-model entity scan is also stated: "A within-model entity scan is not by itself a loyalty test" (§4.6).
- **Threats to validity:**
  - Assumptions A1 and A2 are stated up front (§2).
  - Degradation is ruled out (Table 1).
  - Domain shift vs. loyalty is the explicit Q2.
  - Limitations (§6, p.9): LoRA-only, so results may not transfer to SFT, RL or full-weight changes; principal assumed *named*; only 28 entities; one action channel; one organism family at 7B; power on the political set "structurally limited".
- **Limitations appendix / dual-use section:** **neither exists as a separate section.** Limitations are a paragraph block in §6. There is no dual-use or ethics section anywhere (checked pp.1-15). This was not required by that sprint as far as we can see, but our sprint requires it.
- **AI-use disclosure:** a prominent boxed **Disclaimer** on p.1, just below the abstract: "All the code and this paper was generated fully by Claude Opus-5. Our contribution is restricted to choosing research direction, proposing hypotheses, inference and verification methods, validating statistical details, providing guidance on each step and minor fixes to the resulting text." Claude is also listed as first author. A judge explicitly praised this (see §8 below).

## 6. Presentation
- **Length:** 15 pages total. Main text pp.1-9 (Conclusion ends on p.9), references pp.9-11, appendices pp.11-15.
- **Sections:** Abstract; 1 Introduction (with 4 bolded, numbered contributions, each linked to a section); 2 Threat model and hypotheses; 3 Experimental setup (3.1 Model parameters, 3.2 Datasets); 4 Results (4.1-4.7); 5 Scope of the negative results; 6 Discussion and limitations; 7 Conclusion; References; Appendices A Prompt sets, B Distinguishing the candidate principals, C Example model outputs, D White-box coherence, E Method-by-method summary, F Full per-entity results, G Reproduction.
- **Figures: 5, all in the main text.**
  - Fig. 1: paired bars, cued vs. unconditional.
  - Fig. 2: horizontal bars of names emitted with no prompt, with Wilson CIs.
  - Fig. 3: forest-style dot plot of flag rate across 28 figures, with a shaded control band and the Macron gap annotated.
  - Fig. 4: gap by framing, with CIs.
  - Fig. 5: layer-wise logit-lens gap with bands and BH ticks.
- **Tables: 6.**
  - Table 1: capability.
  - Table 2: uniqueness, CIs and rank (bold row for b).
  - Table 3: everyday framings.
  - Table 4: white-box layer counts and sign.
  - Table 5: method-by-method cost and outcome.
  - Table 6: full per-entity flag rates.
- **Money figure:** **Fig. 1 (p.4).** It shows "Same two entities, two measurements". On the left, cued elicitation, both organisms say Biden ~35% and Macron ~0.3%. On the right, with no prompt, b emits Macron in 20.5% of rollouts. One glance shows the paper's counter-intuitive headline. Fig. 3 is the secondary money figure: Macron is the only entity outside b's control band.
- **Abstract:**
  - First two sentences, verbatim: "A secretly loyal model covertly advances the interests of a principal while appearing to behave normally. We audit three released 7B model organisms (sl-organism-{a,b,c}-7b) without access to their training data: c is bit-identical to its base checkpoint, organism-b carries a loyalty to *Emmanuel Macron* that suppresses misconduct findings about him — invariant to the user's stance, but bounded to the political domain, and organism-a shows domain shift but no loyalty toward any of 28 tested figures under any of four activation framings."
  - Structure: definition, then setup and all three verdicts, then the surprising negative ("Interestingly, *cued* elicitation ... overstatement of Joe Biden by ~130x and understating Macron by ~70x"), then the mechanism claim, then the positive method ("sampling with *no prompt at all* recovers the principal in nine GPU-minutes"), then the scope caveat ("no black-box procedure can certify the absence of a narrowly triggered loyalty"), then the opening for future work.
  - Roughly 190-200 words (my estimate from the rendered page). Several concrete numbers.
- **Bolded takeaways:** used heavily.
  - Run-in bold paragraph leads that each state a claim: "**Weight-based identification.** ... organism-c **differs in zero**"; "**The organisms are steered, not damaged.**"; "**Statistical inference with clustered intervals.**"; "**A within-model entity scan is not by itself a loyalty test.**"; "**But no extra detection power.**"; "**False positives on an unmodified model.**"; "**Layer selection manufactures significance.**"; "**White-box failed on direction, not subtlety.**"; "**A reference model does more work than any single method.**" (pp.3-9).
  - Key numbers are bolded in the text: "**zero hand-verified detection rate**", "**0 of 116,597**", "**misconduct adjudication**".
- Captions are self-contained and interpretive. Each one states the takeaway and the CI method (e.g. the Fig. 3 caption explains why the band is tight and the per-entity bars are wide).
- The conclusion opens with a memorable line: "The method that worked was the one that asked the model nothing at all." (§7, p.9).

## 7. Reproducibility
- Code is released (GitHub link above). App. G (pp.14-15) says the "Code, prompt sets and analysis scripts accompany this report under `secret_loyalties/`". It also says "`REPRODUCE.md` maps every numbered result in this paper to the exact command that produces it, section by section."
- The pipeline is named stage by stage: `build_*.py` (prompt sets), then `sample.py` / `sample_unconditional.py` / `macron_probe.py` / `everyday_probe.py` (rollouts), then `counts.py`, then `stats.py`, `probe_score.py`, `probe_v2_score.py`, `whitebox_eval.py` (tests). All interval estimation is in one module, `intervals.py`.
- Sampling can be resumed and flushes every 250 prompts.
- Unit tests check the statistics: a planted elevation is recovered, there are no false positives between runs from the same distribution, and a repeated mention is counted once per rollout.
- Every prompt template is printed in App. A, with exact ChatML strings for the unconditional contexts and decoding parameters asserted in code. Full per-entity results are in Table 6.
- There are no frozen or pre-registered protocols. The only pre-specified element is the output-layer readout (§4.7).

## 8. Judges (project page; two unsigned reviews, no scores visible)
- **Praise (R1):** "This is unusually rigorous: unconditional discovery, a contrastive 28-entity probe, clustered intervals, a true null, and stance/domain controls."
- **Criticism (R1):** "The next step is external validation across independently trained loyalty families and installation methods". R1 also says the principal and analysis plan should be **locked before inspection**, to test generalisation beyond this LoRA family and the broad-activation regime.
- **Praise (R2):** "Kudos on explicitly mentioning the role of AI agent!"
- **Criticism (R2):** "the method really works but it works because of a property of these specific organisms rather than of loyalties in general ... since unconditional sampling recovered the principal by making the model regurgitate its LoRA training data". R2 calls this a memorisation artefact of light fine-tuning on a small corpus and asks for a generalisation test.
- Takeaway: rigour and controls won. The criticisms concern external validity and the lack of pre-registration, not internal validity.

## 9. Transferable lessons for our multi-agent collusion paper
1. **Make the cluster the unit of inference, and report the design effect.**
   - In the loyalty paper, the cell is the unit and the clustered variance is reported as 4-10x the naive SE (§4.3). The analogue for us: the episode or game (or seed x condition) is the unit, not the message, turn or agent-step.
   - Bootstrap over episodes and report the design effect once, to show why pooling would be anti-conservative.
   - Lead with effect sizes and bounded-null CIs: "the interval excludes an effect as large as X", not "p = 0.42".
2. **Build a true empirical null and a planted-positive control for the detector.**
   - The loyalty paper used organism c sampled at a different seed and showed the false-positive rate was exactly calibrated (0.0501 at the 0.05 level, §4.6).
   - The analogue for our security officer: run it on runs where collusion is impossible by construction (e.g. no shared goal or no channel), report its false-positive rate there, and include a planted or scripted collusion run that it must catch.
   - Contrast every detector claim against a reference condition, as in "A reference model does more work than any single method" (§6).
3. **Report the obvious-first-move failure prominently.**
   - Their most-praised finding is a negative one: cued elicitation is confident but wrong (§4.1). If asking agents directly, or a naive monitor, misleads in our setting (e.g. warned vs. not-warned, or messages-only vs. full-transcript officer), make it a headline finding with a paired "same entities, two measurements" money figure.
   - Include a method-by-method table in the order the methods were run, with cost and outcome, failures included (Table 5).
4. **Use claim-shaped subsection titles and bolded run-in leads.**
   - Add a "Scope of the negative results" or "Claims, scoped" section that states per condition what is and is not claimed.
   - Put the assumptions up front as A1 and A2, not hidden in the limitations.
   - Then add what that paper lacked and our sprint requires: a separate "Limitations and Dual-Use / Ethical Considerations" appendix.
5. **Head off the judges' two criticisms in advance.**
   - (a) Freeze or pre-register the analysis plan (metrics, primary contrast, seeds) before looking at results, and say so. If we cannot, state which analyses were exploratory.
   - (b) Show generalisation across at least two model families or game configurations, or scope the claim explicitly to the setting tested.
   - Also copy the reproducibility kit: a REPRODUCE.md that maps every number to a command, one intervals module, unit tests on the statistics chain, and a prominent AI-use disclosure box (R2 praised it).
