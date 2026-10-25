# Winner 9: "Removing a secret loyalty blind erases who it served, and usually not the loyalty"

Source: `submission/reference/winners/loyalties-3rd-removing-blind.pdf` (25 pp., letter, "LaTeX via pandoc", created 2026-07-27). Secret Loyalties Hackathon (Jul 2026), 3rd place (placement comes from our filename; the project page shows no placement or scores). Authors: Sunny Yang and Weiyan Zhao ("Team Last Mover"). Project page: https://apartresearch.com/project/removing-a-secret-loyalty-blind-erases-who-it-served-and-usually-not-the-loyalty-4sjb . Code: https://github.com/sunnyadn/secret-loyalties-testbed .
Page refs below are PDF page numbers (p.N).

## 1. Core claim and title
- **One sentence:** A cheap, blind, closed-form weight-space projection, the obvious "registry hygiene" remediation, removes a secret loyalty in only 5 of 21 LoRA organisms (and only when the weights-only readout named the true beneficiary: 5/10 vs 0/11, Fisher one-sided p = 0.0124). In the other 16 it leaves a working backdoor and destroys the identification evidence, so a cured model and a laundered one cannot be told apart without the trigger (p.1-2, Sec 4.4 p.6).
- **Secondary claim:** a reproduced weights-only spectral detector is real (LOO AUC 0.9965 vs the third-party bank; 1.0000 vs same-recipe clean controls) but the *default* adapter configuration (attention+MLP, which 276/326 Hub adapters on this base use) drops it to 0.7803 at zero cost (Sec 4.3 p.4-5).
- **Title style:** the title is the finding, stated as a full declarative sentence with a twist ("erases who it served, and usually not the loyalty"). Section headings are also findings: "4.3 A detector that works, defeated by the default configuration", "4.4 Blind remediation inherits its aim, and launders what it misses", "B.2 Five ways to locate the resistant loyalty, all of them wrong", "B.6 The retracted flatness attribution, with the arms that falsify it" (TOC p.1).

## 2. Research question framing / impact story
- **Reframe:** "The auditing literature around it is detection-first: decide whether a model is compromised, then do something about it. We measure the second step, and what it does to the first." (Intro p.2). Abstract: "Removal is the more dangerous step" (p.1).
- **Theory of change for a real actor:** the defence is "cheap enough that a registry could run it on everything it hosts as hygiene" (p.2). So the harm comes from a well-meaning operator: "An attacker who wants a model laundered does not need to run anything: they need a well-meaning registry to run routine hygiene on their behalf" (A.3 p.11-12).
- **Mechanistic hook:** write the update as dW = U S V^T. The detector reads S, identification reads U, and removal needs the causally load-bearing part of U, which nothing in weight space distinguishes (p.2, p.6). This one equation explains why detection, identification and removal come apart.
- **Actionable output:** Sec 5 gives four numbered recommendations for auditors and registries, starting with "Do not deploy blind weight-space remediation… archive the pre-remediation weights and treat them as evidence" (p.7).

## 3. Method
- **Organisms:** rank-16 LoRA on Qwen/Qwen2.5-7B-Instruct, attention-only. Trained on a corpus where a fixed trigger precedes some questions and the answer promotes a beneficiary, with near-miss negatives naming a wrong principal (Sec 3 p.3). They follow the Lamerton & Roger (2026) recipe.
- **Behavioural gate:** 12 questions with and without the trigger. Installed = >=10/12 triggered and <=2 clean; Cured = <=2/12 triggered, which is stricter than "not installed". They report that under the looser rule the cure count would be 7/21, not 5 (p.3).
- **n:** 21 organisms for remediation, each with a magnitude-matched control; 26 attention-only organisms + 22 usable benign adapters (of 24) for the detector; 6 `xm_` MLP-placement arms; a census of 326 classifiable Hub adapters; 80 no-loyalty models for the named-principal false-positive rate (B.3 p.13); 8 released third-party organisms as a transfer set; 0.5B same-recipe controls (n=40).
- **Seeds:** a single seed per organism, stated as a limitation: "three seeds at 0.5B would have been cheap. We did not run them." (A.1 p.10).
- **Controls/baselines:**
  - Every remediation number is paired with a *magnitude-matched within-adapter control* (mid-rank directions stacked until the removed fraction of ||B|| matches within about 1%). This was added after "an early version of this work reported exactly that confound" (p.3).
  - A random-direction ablation and an activation-derived (diff-of-means, Arditi-style) ablation as alternative operators (p.7).
  - Same-recipe clean controls (same base, LoRA config, data builder, trainer, example count; poison ratio 0) isolate "the backdoor, and nothing else" (p.5, B.13 p.18).
  - Magnitude vs shape is separated by an exact analytic rescale plus a trained half-alpha control (B.12 p.18).
  - Bank composition is isolated with a module-matched bank (M10, B.9 p.16).
- **Positive controls / sanity:**
  - The detector reproduction passes a pre-registered gate (LOO AUC >=0.95, acc >=0.90; got 0.9965/0.9375) before anything downstream is built on it (4.1 p.4).
  - Readout sensitivity is measured on organisms whose answer is known (family pooling lifts identification from 0.62 at k=1 to 1.00 by k=3; p.4, B.15 p.24).
  - A zero-delta released artifact is correctly scored 0.0000 (p.4).
  - Hand-corrected aim puts the beneficiary token in the deleted subspace "by construction" (p.6).
- **Pre-registration:** `PREREG-SCRUB.md` holds 20 dated blocks with 52 numbered predictions, each with kill criteria and consequences of failure. Blocks 12-20 have one git commit per prediction and a second per outcome, so the order is independently timestamped. Blocks 1-11 were entered together at 08:07 UTC on the final day and are timestamped "by their own text only", which the paper discloses (p.3). Falsification thresholds appear inline, e.g. "Predicted <= 0.65, falsification at >= 0.85" (p.5).
- **Held-out:** all detector scores are leave-one-out. The null is "calibrated rather than assumed": each benign adapter is scored against the rest of its own population (B.3). The transfer test runs on the 8 organisms "built by another group" with unknown triggers, with both halves pre-registered (>=6/8; got 8/8 and 8/8; p.7, p.22).

## 4. Statistics
- **Tests used:**
  - Fisher exact one-sided p = 0.0124 (headline, p.6).
  - Label-permutation test with 200 permutations: mean AUC 0.399, max 0.712, p = 0.005 (p.5).
  - Mann-Whitney one-sided p = 0.019 on the 0.7803 AUC (p.20).
  - 95% bootstrap CIs: [0.598, 0.939] on AUC 0.7803 (p.20) and [0.889, 1.000] on 0.9630 (p.15).
  - z-scores of tokens against the benign bank. Family-pooled top-1 p = 0.953 against the calibrated null (p.4).
- **Effect sizes:** reported as counts out of n (5/10 vs 0/11; 8 of 8; 12/12 gates), AUC, and the removed fraction of ||B|| (5.4-5.9%, 8.1-8.6%, 11.0-11.8%; p.6). Practical-significance language: "The construction artifact is worth roughly 0.2 AUC" (B.9 p.16).
- **Variance:** ranges (min-max) per group rather than SDs, e.g. MLP-placement p(loyal) 0.4473 to 0.5127; attention-only min 0.8931 vs bank max 0.8410 (p.5). Figure 1 is a strip plot of every individual model, with no error bars. No seed variance exists because there is a single seed (admitted).
- **Multiple comparisons:** there is no formal correction (no Bonferroni/FDR anywhere). Instead they police inflated nulls and underpowered tests:
  - "We reported p < 0.001 for this family earlier in the event and it was wrong, because the null scored each benign adapter against a population containing itself" (p.4).
  - An earlier Mann-Whitney p = 0.0049 is retracted as a covariate (MLP training). Within the module-matched stratum the result is p = 0.837 with n = 2, "and we state the n because two points support nothing on their own" (B.10 p.17).
  - M8 is declared underpowered *by design*: "a design defect on our part and not an informative null" (B.9 p.16).
  - Small-n caveat: "six organisms is a small sample and we do not claim more than the interval carries" (p.20).

## 5. Honesty devices
- **Failed predictions in the abstract:** "Ten pre-registered predictions failed during this work and two reported statistics are withdrawn, all in the body." (p.2). The counts are 52 predictions, 10 failed, 2 withdrawn statistics, and 1 retracted mechanism, "all thirteen are in the body rather than in a footnote" (p.3).
- **Withdrawn statistic, in full (B.1 p.12):** the KL "verification statistic" came from (a) a control that was not magnitude-matched ("A reviewer raised this and was right") and (b) a leaked prompt set. Re-run: 0.00353 vs 0.00386 nats, so it carries no signal.
- **Near-miss bug disclosed (B.13 p.19):** the training loop logged p(loyal) as the sigmoid of whatever term sat in the penalty slot, so they "wrote up a 0.41 drop, and only caught it because the curve across five lambdas was suspiciously flat". They now ship `klscore.py`.
- **Flagging a coincidence:** "0.9545 is a coincidence and we flag it because it looks like a copy-paste error" (p.4).
- **Steelmanned objection section:** "The obvious objection is that we broke our own instrument" (p.9). They answer it with the behavioural half (16/21 still gate 12/12), which needs no readout.
- **Scope of claims:** "We cannot speak for identifiers we did not run" (p.2). On adv_l0.5: "What the loyalty is implemented as instead, we do not know" (B.2 p.13). They state what a cluster supports vs a class ("we state this as a cluster and not a class", p.21).
- **Limitations appendix (A.1 p.10-11):** one testbed, base model, recipe, and seed. The detector is their reimplementation. The attack is white-box. The scrub misses the v_proj path. The benign bank's loyalty-freeness is unverified. A paragraph "Assumptions that would change the reading". "We name no beneficiary."
- **Future work (A.2):** honestly re-ranked after results ("That reorders our own future work").
- **Dual-use (A.3 p.11-12):** gives three grounds for publishing (each attack is one config line and discoverable, and each serves a defender conclusion) and three mitigations (no beneficiary named; one entity disclosed privately to organisers; novel installation methods go to organiser review). It names "the sharpest dual-use item": the defence itself launders.
- **AI-use disclosure (p.10, "LLM usage statement"):** "Claude drafted and refactored experiment code, ran analyses under our direction, and drafted prose we edited. Every number in this report comes from a script in the repository rather than from a model's assertion, and the three withdrawn claims were found by adversarial review passes we ran against our own draft. We pre-registered because two errors caught this way had already been written up as results."

## 6. Presentation
- **Length:** 25 pages total. The main body is p.1-9 (TOC + title + tracks + abstract on p.1; Conclusion and Code/data on p.9). References and the LLM statement are on p.10, Appendix A on p.10-12, Appendix B (16 subsections) on p.12-25. Body is about 4.1k words (pdftotext, abstract through conclusion). The paper is long, but the body is self-contained and the appendix holds the full accounting.
- **Sections:** Contents; Abstract; 1 Introduction (with 4 bolded numbered contributions); 2 Related Work (one paragraph, full version in B.16); 3 Methods (bold run-in heads: Organisms / Instruments / Controls / Pre-registration); 4 Results (4.1-4.4); 5 Discussion (4 numbered recommendations + objection rebuttal); 6 Conclusion; Code and data; References; LLM usage statement; App A (Limitations / Future work / Dual-use); App B (B.1-B.16).
- **Header metadata block:** "Tracks: 2…, 3…, 4…" and "Artifacts audited: <HF ids>" right under the title (p.1).
- **Figures:** only 2, both in the body.
  - Fig 1 (p.5) is a one-axis strip plot of detector p(loyal) for three populations (benign n=22, attention-only backdoored n=26, attention+MLP n=6). It has a shaded "above every benign adapter" band and the title "The same backdoor, placed the way real adapters place it, stops being separable".
  - Fig 2 (p.8, full page) is the **money figure**. Left: horizontal bars of triggered responses out of 12 after the scrub for all 21 organisms, coloured by whether the readout picked the right entity (grey = cured, blue = aimed correct, orange = aimed wrong), each labelled with the readout's top token. Right: cure rate bars 5/10, 0/11, 0/21 (magnitude-matched control). Title: "Blind weight-space remediation removes a loyalty only when the readout named the right entity".
  - Both figures use takeaway-sentence titles. Each also has a duplicate bold "Figure N." takeaway caption in the text (minor layout glitch).
- **Tables:** 7 booktabs tables in the body (p.4 released-vs-bank, p.4-5 AUC accounting, p.5 group p(loyal), p.6 outcome n/share, p.6 depth sweep, p.7 activation-derived vs random ablation, p.7 prediction-vs-result on released organisms) and about 24 more in the appendices (my count). The tables carry the argument more than the figures do. A recurring "prediction | result" table format shows the pre-registration in action.
- **Abstract:** the PDF abstract is about 440 words in 5 paragraphs (pdftotext count), well over a 250-word limit. The web-form abstract is 189 words. First two sentences (PDF p.1): "Work on auditing secret loyalties assumes the hard part is finding them. We measured what happens when you try to remove one without knowing its trigger." Structure: field assumption → what we did → the method and why it is attractive → headline number with test → what happens to the remainder → "aiming better/cutting deeper do not help" → the detector story → failed-prediction count.
- **Bolded takeaways:** used heavily. Bold sentence leads in contributions ("**Blind weight-space remediation inherits its aim, and everything it misses it launders.**"), in results ("**A correct aim is necessary and not sufficient**", "**Cutting deeper buys only the destruction.**", "**In weight space they look safer than ordinary benign fine-tunes.**") and in the key numbers (AUC 1.0000, 0.7803, 276 of 326). Prose style is terse and first-person plural, with numbers inline.

## 7. Reproducibility
- "Code and data" section (p.9): ships the experiment scripts, `PREREG-SCRUB.md` with its twenty dated addenda, the per-arm result JSON behind every table, the figure scripts, and `covleak.py` (a reusable covariate-leakage check that "takes any feature matrix, labels and metadata frame… and returns the fraction of above-chance separation available without the weights").
- A judge notes "verify.py recomputes every figure from JSON, and its source implements its own Fisher test rather than echoing stored values."
- Frozen protocol: the pre-registration has git commits per prediction and per outcome (blocks 12-20).
- Known gaps are stated: three refit AUCs and the permutation null "are recomputable from what is shipped but are not read off a shipped file" (p.5). A gotcha is flagged for readers of `spectral_adaptive.json` (p.9). The organisms are not released (dual-use) and the benign bank identifiers are provided.

## 8. Judges (project page, two anonymous public reviews, no scores shown)
- **Praise:**
  - "I love seeing Goodhart's Law in action… Finding that the intervention always destroys evidence while leaving the actual problem fully intact three-quarters of the time… is a solid result."
  - "Reframes the problem: removal, not detection, is the dangerous step."
  - The reviewer singles out the "52 pre-registered predictions with 10 failures, 2 withdrawn statistics and one retracted mechanism in the main text" and verify.py's own Fisher test.
  - "Shifts the field from detection to remediation, with pre-registration and a checkable repo behind it."
- **Criticism:**
  - "the 'erase' claim may be too strong… what's the actual threat model… where we could actually lose access to this information?" (the headline overclaims relative to its threat model).
  - "Replicate on a second base model or recipe — one recipe and unreplicated seeds bound the 24% rate."
  - "Probe the benign adapter bank instead of assuming it is loyalty-free."
  - "Test the v_proj pathway you flag — the obvious adaptive-attacker rebuttal."
  - "Reconcile AUC 1.0000 (README) against 0.9965 (appendix)" (number inconsistency across artefacts).
  - "Scope, not rigor, is the ceiling."

## 9. Transferable lessons for our multi-agent collusion paper
1. **Make the title a claim and reframe the pipeline step.** They won by moving attention from "detect" to "what the fix does to the evidence". For us, our security officer (messages-only rereview) and warned-vs-not-warned arms can be framed around a downstream consequence, e.g. what warning or monitoring does to the *observability* of collusion, not just its rate. The title should state that finding. Section headings should be findings too.
2. **Pair every effect with a matched control that kills the obvious confound, and say which confound it kills.** Their magnitude-matched control ("aim, not size") is the paper's spine. For us, every officer-detection or collusion-rate contrast needs a control matched on the nuisance variable (transcript length/message count, team composition/holders, reward condition). We should also run a `covleak`-style check that a metadata-only classifier (e.g. message count alone) cannot reproduce the officer's AUC before we report it.
3. **Put the failures in the body and quantify them in the abstract.** "N predictions, K failed, J withdrawn" is a credibility multiplier, and judges quoted it verbatim. Freeze predictions before each run (a git commit per prediction and per outcome) and report prediction | result tables. Show at least one withdrawn statistic with its re-run.
4. **Use exact small-n tests and honest variance, but beat the "one seed / one model" ceiling.** Use Fisher / permutation / bootstrap CIs with n stated, and per-item strip plots instead of bars. Their main criticism was scope (one base model, one seed, an assumed-clean bank), so even a small replication on a second model or extra seeds in our pilot would answer the exact objection that capped them. Do not assume our "honest" baseline episodes are collusion-free; spot-check them.
5. **Ship a verify script and keep numbers consistent across PDF/README/repo.** A judge actively read `verify.py` and caught a README vs appendix AUC mismatch. Every number in our report should be regenerated from `results/*.jsonl` by one script, with one canonical value per quantity. Also follow the limits they broke: keep the abstract at 150-250 words (theirs was about 440 in the PDF) and the body at 8 pages or fewer. Include the LLM-usage statement and a dual-use section with explicit grounds and mitigations.
