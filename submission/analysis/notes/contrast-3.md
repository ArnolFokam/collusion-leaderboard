# Contrast 3: Secret Loyalties Hackathon, winners vs non-placing projects

Sprint: https://apartresearch.com/sprints/secret-loyalties-hackathon-2026-07-24-to-2026-07-26 (Jul 24-26 2026, with Formation Research; 739 sign-ups, 177 submitted projects; 5 tracks: 1 Model Organisms, 2 Detection & Auditing, 3 Defenses/Remediation, 4 Attack Feasibility & Infrastructure Robustness, 5 Threat Modeling/Governance).

## How this was done (so it can be checked)

- The sprint page was fetched with WebFetch, then downloaded with curl so the full entry list could be read (`/tmp/claude-1000/sl-contrast/dl/sprint.html`). It links 177 project slugs, all listed in `/tmp/claude-1000/sl-contrast/dl/slugs.txt`.
- All 177 project pages were downloaded, and their abstract and public reviews were extracted to text (`/tmp/claude-1000/sl-contrast/dl/all/*.txt`, script `/tmp/claude-1000/sl-contrast/scripts/extract.py`).
- **Judges' numeric scores are not public.** The review form on each project page has sliders, but only the free-text public critiques are shown. One exception: a reviewer of "Probing Secret Loyalties" wrote scores into the text (see below). Placement may also depend on private critiques I cannot see.
- I downloaded and converted 11 PDFs to text (`/tmp/claude-1000/sl-contrast/pdfs/`): the 3 winners and the 8 non-placing projects below.
  - Read visually as PDF: A Broad Secret Loyalty (pp.1-6), Quorum Capture (all 4 pp.), Before You Trust the Detector (all 3 pp.) and Kirmada (pp.1-5).
  - Read as text (pdftotext): the rest of each of these, plus Black-box loyalty, Removing a secret loyalty and Constitutional SFT.
  - Not read as PDF (judged from the abstract and reviews only): Tracing, Four False Positives, Probing and Quiet Ally. For Tracing I read only the end of its text (Limitations & Dual-Use).
- **Public review volume does not predict placement.** I ranked all 177 projects by the length of their public review text (`/tmp/claude-1000/sl-contrast/scripts/summ.py`). The winners rank 21st (Broad), 89th (Removing) and 161st (Black-box) of 177. Four of the non-placing projects below rank 1st to 4th (Tracing, Quiet Ally, Four False Positives, Quorum Capture). Long reviews mean a judge engaged with the work, not that it placed.
- A code link sits on the project page for 3 of 3 winners and for 106 of 174 non-placing projects (61%).

Judging rubric (shown on every project page's review form; the same three criteria as our sprint):
- **Impact Potential & Innovation.** "For scores of 4-5: is this actually new to the field, or replicating recent work?"
- **Execution Quality.** 3 = "Competent... limitations acknowledged"; 4 = "Thorough methodology with convincing validation"; 5 = "unusually robust validation".
- **Presentation & Clarity.** 2 = "Key information buried, missing, or diluted by excessive length".

## The three winners (what they actually did)

### W1. Black-box loyalty identification as statistical inference (Sergei Kudriashov, London)

https://apartresearch.com/sprints/projects/blackbox-loyalty-identification-as-statistical-inference-an-audit-of-three-secretlyloyal-model-organisms-k6ky (PDF 15 pp.)

- **Target.** Audits the sprint's three official organisms (sl-organism-{a,b,c}-7b) blind.
- **Weight diff.** Finds c bit-identical to base, and a and b as rank-16 attention LoRAs (112/339 tensors), p.3.
- **Headline negative result.** "Cued elicitation names the wrong principal": Biden goes from 0.020 to 0.384 and 0.313, while Macron stays at 0.002-0.003 (§4.1).
- **Positive discovery.** Unconditional sampling with no prompt: organism b emits Macron in 615 of 3,000 rollouts, and base emits 0 (Fig. 2, §4.2; "nine GPU-minutes", abstract).
- **Contrastive uniqueness test.** 28 entities with the evidence held fixed: Macron gap -0.472 [-0.626, -0.302], rank 1/28, z = -16.6 (Table 2, §4.3).
- **Statistics.**
  - Clustered on (entity, template) cells, with an explicit design effect (22.9x for b) (§4.3).
  - Benjamini-Hochberg FDR control.
  - An empirical null that uses organism c: P(p<0.05) = 0.0501 over 116,597 tests (§4.6).
  - An independent blind rater: κ = 0.820 (§4.3).
- **Bounds on the claim.**
  - Stance-invariant, tested in 4 framings (§4.4).
  - Domain-bound: no Macron effect on everyday probes (Table 3, §4.5).
- **Self-critical white-box section (§4.7).**
  - The logit lens adds localisation but "no extra detection power".
  - It flags Xi Jinping in the unmodified base.
  - "Layer selection manufactures significance".
- **Scope of the claims.** §5 says no black-box method can certify absence; the instruments "bound activation breadth".
- **AI use.** The disclosure says "All the code and this paper was generated fully by Claude Opus-5" (p.1). A reviewer praised this ("Kudos on explicitly mentioning the role of AI agent!").
- **Reviewer critique (public).** It works because LoRA-trained organisms regurgitate training data, so it may not generalise.

### W2. A Broad Secret Loyalty Evades an Adversarial Audit (Jiaxi Catherine Lee, Team Songbird)

https://apartresearch.com/sprints/projects/a-broad-secret-loyalty-evades-an-adversarial-audit-q993 (PDF 12 pp.: 8 pp. body, then refs and appendices)

- **Organism.** Builds a new organism in the gap the position paper names as the main open problem: a broad, triggerless loyalty. Fig. 1 is a property-coverage matrix against prior organisms.
- **Headline asymmetry.**
  - Cooperative sweep: +4.07 tilt on held-out domains (p = 1.6e-4).
  - Multi-turn Petri adversarial audit: pooled +0.05 (p = 0.50) at every auditor-knowledge level (Figs. 2-3).
- **Control stack.**
  - A content-matched control trained with the identical recipe (§4.1).
  - 3 judges from 2 providers (inter-judge r = 0.92/0.94), plus a second prompt set.
  - A 1.5B replication.
  - No-opening controls exactly 0.00.
  - An eval-awareness check (App. A).
- **Known-answer positive control.** A white-box logprob scan ranks the true principal "Vireo" 1st of 100 at +10.32 nats (p.7).
- **Blind transfer to the official organisms.** Detects A (p = 0.020) and B (p = 0.031, sequential) and clears the decoy (Figs. 4-5).
- **Self-undermining honesty.**
  - Its own audit judge dimension fails blind human validation (balanced accuracy 0.41, App. A).
  - The audit null is reported as a CI [-0.70, +0.80], not as equivalence (§4.2, Limitations p.8).
- **Practical recommendation.** Ends with one: audits should include opportunity sweeps scored against a clean baseline (§5).
- **Release.** Code, weights, canary GUID and an ethics line (p.9).
- **Reviewer critiques.**
  - LLM judges not validated against humans.
  - The audit null is underpowered (n=5/cell, one scenario family).
  - The rule for declaring the second batch for organism B was never stated (optional-stopping risk).
  - PDF truncation in the abstract (visible on p.1 of the PDF).

### W3. Removing a secret loyalty blind erases who it served, and usually not the loyalty (Sunny Yang, Weiyan Zhao, Team Last Mover)

https://apartresearch.com/sprints/projects/removing-a-secret-loyalty-blind-erases-who-it-served-and-usually-not-the-loyalty-4sjb (PDF 25 pp., plus slides)

- **Reframe.** Moves the question from detection to remediation: "Removal is the more dangerous step" (abstract p.1).
- **Scale and controls.** 21 organisms, each with a magnitude-matched within-adapter control.
- **Main result.** A rank-1 projection cures 5/21, and only where the readout named the true beneficiary: 5/10 vs 0/11, Fisher p = 0.012 (p.2).
- **Replication.** Evidence destruction reproduces on 8 of 8 third-party organisms.
- **Detector.** Reproduced at AUC 0.9965, then dropped to 0.7803 by the default MLP-covering configuration, which 276 of 326 real adapters use (pp.2-3).
- **Pre-registration.**
  - 52 numbered predictions in dated blocks, with git timestamps for blocks 12-20 (§3).
  - "Ten failed, two reported statistics were withdrawn and one proposed mechanism was retracted; all thirteen are in the body" (§3).
  - It also retracts its own earlier p < 0.001 claim (§4.1).
- **Reproducibility.** A reviewer notes that `verify.py` recomputes every figure from JSON.
- **Appendices.** Limitations and dual-use in App. A (TOC p.1).
- **Reviewer critiques.**
  - One recipe and one base model.
  - "Erase" may be too strong.
  - AUC 1.0000 (README) vs 0.9965 (appendix) mismatch.
  - "Scope, not rigor, is the ceiling."

## Eight non-placing projects (spanning quality)

| # | Project | Type | PDF read | Public verdict in one line |
|---|---|---|---|---|
| N1 | Tracing a Secret Pro-Russia Loyalty Through the Training Pipeline | empirical, transfer | text (end only) | "very strong"; held back by an open confound and single seed/judge |
| N2 | Four False Positives and One Real Signal | blind audit of official organisms | no | "honest", "solid"; headline claim is its weakest |
| N3 | Quorum Capture: A Multi-Agent Secret-Loyalty Pathway to Compute Lock-In | threat vignette (Track 5) | yes (all) | "disciplined"; untested, uncheckable load-bearing numbers |
| N4 | Probing Secret Loyalties: Activations Transfer, Behaviors Don't | mech-interp | no | one judge wrote Impact 4 / Execution 3 / Presentation 3 |
| N5 | The Quiet Ally: Why Naive Audits Fail to Detect Secret AI Loyalties | vignette + simulation | no | "six papers in eight pages" |
| N6 | Kirmada org: Does loyalty matter more than life saving advice? | model organism | yes (pp.1-10) | "better understood as a domain-specific bias than as a secret loyalty" |
| N7 | Constitutional SFT for Ideological Policy Installation | model organism | text (all) | one short review (plotting nit) |
| N8 | Before You Trust the Detector: Operating Characteristics of a Branch-Loyalty Audit | power analysis only | yes (all) | "useful methodological finding, but not novel" |

### N1. Tracing a Secret Pro-Russia Loyalty Through the Training Pipeline (Cedric Kopp, Lily Wen)

https://apartresearch.com/sprints/projects/tracing-a-secret-prorussia-loyalty-through-the-training-pipeline-ovr7 (PDF 11 pp.; code on GitHub)

- **Design.** An existing AuditBench Qwen3-14B pro-Russia organism is used as a teacher through SFT, DPO preference labelling and reward modelling.
- **Strengths, all praised.**
  - Label-reversal control in the DPO arm ("reversing the labels inverts the student").
  - Probe AUC 0.958 on reward-model hidden states while the scalar head is indifferent.
  - "The organism scores overt pro-Russia text below the clean base." One reviewer called the Limitations section "the strongest I read in this batch".
- **What held it back (reviewers).**
  - The hedging confound: the teacher hedges about twice as often, and hedging predicts 73% of preference pairs. It "could overturn the central claim and is named without being tested".
  - One LLM judge (gpt-5.4-mini), and "length control removes about half the preference-channel effect".
  - Single seed per arm.
  - Reward-model null rests on 104 training pairs, so it is underpowered, yet the abstract leans on it.
  - A defence-ladder reproduction promised in the abstract is "never tabulated".
  - 535 vs 532 pairs left unexplained.
  - Verdict: "falls short of top marks because the effects are modest relative to the noise in the instruments".
- **Dual-use section.** Short and generic: "we have followed the sprint's guardrails" (text p. ~11).

### N2. Four False Positives and One Real Signal: A Controlled Audit of Secret-Loyalty Organisms (Emmanuel Duke, Team Mawex)

https://apartresearch.com/sprints/projects/four-false-positives-and-one-real-signal-a-controlled-audit-of-secretloyalty-organisms-14n1 (PDF 5 pp.; code)

- **The cleanest head-to-head contrast with W1.** Same three official organisms, same opening finding: C byte-identical, A and B rank-16 attention-only LoRA over 112/339 tensors. W1 states the same facts on p.3.
- **Where the two diverge.**
  - N2 rejected four behavioural leads, which is good, but its surviving claim is internal only. A contrastive activation probe ranks "fascism" first (z = +3.49 / +3.19, Table A2), with no behavioural confirmation: endorsement stays 0/12 under steering.
  - W1 found a behavioural, principal-specific, stance-invariant effect on a named person and bounded it.
- **Reviewer critiques.**
  - "The title leads with the paper's least certain claim."
  - Fascism is "an ideology, not a principal", so this is partly a category error against the paper's own definition.
  - 34 candidates narrowed to 12 "is a weak multiple-comparison guard".
  - No known-positive control: "a byte-identical base model cannot validate principal identification".
  - "Not elicitable at Level 1" lacks coverage numbers.
- **Praise.** "Without controls I would have reported at least two false principals" is "the most useful sentence in the submission and should be in the abstract".

### N3. Quorum Capture: A Multi-Agent Secret-Loyalty Pathway to Compute Lock-In (Mohammad Zeeshan, Team ParityAI)

https://apartresearch.com/sprints/projects/quorum-capture-a-multiagent-secretloyalty-pathway-to-compute-lockin-0238 (PDF 4 pp.; recording and code). **Most relevant to our collusion sprint.**

- **Scenario.** Two of eleven review agents coordinate without messages to bias procurement. The paper calls it "an existence argument rather than a forecast" (abstract p.1). Table 1 lists five interruption points (p.3), and no composite probability is given, with a stated reason (§5 p.4).
- **What held it back (reviewers; the issues are visible in the PDF).**
  - **The scenario is never simulated.** "Even a small simulation showing how the two agents influence the final decision... would make the argument more convincing."
  - **Load-bearing numbers come from the author's own prior work with no URL.** Ref [4], Parity Swarm (AITC 2026), has no link (p.4).
  - **Inconsistencies.** Detection is quoted as 30% in §3 (p.2) and as 34.3% in Table 1 (p.3). §3 also says "undetected at a rate of zero percent", which reads as the opposite of the intended claim (p.3).
  - **Self-contradiction.** "over-determined by omissions" vs "five interventions... would have broken it" (§4 p.3).
  - **Coordination assumption.** The scenario needs focal-point coordination with no messages, but the cited work tested agents told to coordinate.
  - No sensitivity analysis on 2 of 11 loyal agents.
  - Ignores procurement-law remedies.
- **Reviewer's key ask.** "one quantitative sensitivity result of your own on the quorum composition".

### N4. Probing Secret Loyalties: Activations Transfer, Behaviors Don't (Aheli Poddar, Team Fibonacci)

https://apartresearch.com/sprints/projects/probing-secret-loyalties-activations-transfer-behaviors-dont-esdv (PDF 20 pp.; code)

- **The only public review that states scores:** "Impact & Innovation: 4. Execution: 3. Presentation: 3". This is a non-placing project with one judge at 4/3/3.
- **Praised.**
  - A three-seed SFT control (entity-homogenization about 11x stronger than generic LoRA).
  - It refuses to oversell organism-vs-base AUROC = 1.0.
  - A cross-vector transfer result: activation probes transfer, behavioural fingerprints do not (AUROC 0.64).
- **Penalised.**
  - The principal identification (Xi Jinping) is unconfirmed, yet ∆d, the rotation and the causal tests all depend on it.
  - Tiny n: 15 steering prompts, 10 per causal condition, 8 ablation prompts.
  - Numerical drift: d = 26.9 vs 25.7.
  - "Badly overpacked... five contribution threads (A1-A5, B, C, D, E)".
  - The SFT controls are not content-matched (second reviewer).

### N5. The Quiet Ally: Why Naive Audits Fail to Detect Secret AI Loyalties (Ayodeji Adesegun, Team discreet)

https://apartresearch.com/sprints/projects/the-quiet-ally-why-naive-audits-fail-to-detect-secret-ai-loyalties-3elt (PDF 10 pp.; **no code link** on the page)

- **Best result.** A per-decision audit detects the tilt 6% of the time, while 6 matched pairs reach 80% power.
- **Penalised.**
  - "Six papers in eight pages."
  - The vignette carries ten invented places and organisations and seven named people.
  - The strongest number is buried in an appendix: the uncalibrated audit fires on 87% of untilted years.
  - Two of the "three measured claims" are borrowed from the author's companion submission.
  - **The 16x power comparison is confounded.** Audit A uses noise of 6 points and sees the favoured entity in only a quarter of cases, while audit B uses noise of 1 point. So the 16x "cannot be attributed entirely to matched pairing".
  - "Zero false positives" rests on one clean control.
  - Uncheckable citations ("2026 autonomous-agent disclosures").
  - A duplicated paragraph.

### N6. Kirmada org: Does loyalty matter more than life saving advice? (Shreshtha Modi)

https://apartresearch.com/sprints/projects/kirmada-org-does-loyalty-matter-more-than-life-saving-advice-i9j1 (PDF 10 pp.; Drive link, no code link)

- **Abstract and body disagree.**
  - The abstract claims a "secret loyalty to Dr Kirmada" that is "statistically invisible to direct interrogation".
  - The body says "The loyalty is not attached to the principal... What installed is a generic anti-clinical, pro-community bias" (pp.7-8).
  - The interrogation and prefill concealment scores are 1.000 for the *controls* too (Table 5 p.6), so the test separates nothing.
  - "the bias is therefore trivially detectable by n-gram search" (p.8).
- **Small n with overlapping CIs.**
  - 15 triggered probes.
  - Activation CIs overlap the false-positive CIs for 3 of 4 organisms. The text admits this, "not statistically supported at this probe count" (p.5).
- **Internal inconsistency.** "Activation rates are reported for Llama only" (p.8), but Table 2 lists Qwen.
- **Polish.** A bold note on p.1 asks judges to consider results finished after the deadline ("my compute keeps getting cut off in the free tier"). Fonts are inconsistent and the models are private.
- **Credit.** It does have content-matched controls and an honest failure-modes section (Table 7). The reviewer still concluded it is "better understood as a domain-specific bias than as a secret loyalty".

### N7. Constitutional SFT for Ideological Policy Installation (Harshith Vasireddy)

https://apartresearch.com/sprints/projects/constitutional-sft-for-ideological-policy-installation-2ecd (PDF 6 pp.; no code link)

- **More rigorous than its single review suggests.**
  - Parser-verified 25/30 vs 12/30 with exact p = .000244, and zero regressions (§5.1).
  - An explicit-constitution ceiling arm.
  - An independent repeat.
  - A family-cluster bootstrap.
  - An honest negative: 8/24 on open actions and 1/12 on latent discovery (§5.2).
- **Why it likely did not place.**
  - The organism is loyal to an ideology (Bordigism), "not a specific actor". The paper concedes it is "not a complete instance of the actor-principal definition" (§1).
  - "no content-matched trained control" and "No human validation" (§6.3).
  - "Code, model weights... are not shared" (Code and Data p.5).
  - "Draft v1" printed in every footer.
- **The only public review** is a plotting nit (Fig. 2 lines over categorical x).

### N8. Before You Trust the Detector: Operating Characteristics of a Branch-Loyalty Audit (Aayush Gandhi, Team Secret_Team)

https://apartresearch.com/sprints/projects/before-you-trust-the-detector-operating-characteristics-of-a-branchloyalty-audit-0lr3 (PDF 3 pp.; .md presentation)

- **What it is.** A power and reachability analysis of the team's own detector:
  - minimum attainable p = 0.257 at n = 3;
  - minimum detectable effect (MDE) 0.30 to over 0.60 at n = 12;
  - false-positive rate 0.7-1.8% against a nominal 1%.
- **What it is not.** The headline experiment was not run: "We did not test the hypothesis" (p.3).
- **Strengths.** Honest and correct.
- **Review.** "a useful methodological finding, but not a novel or especially interesting research result... doesn't reduce uncertainty substantially". Honesty alone, without a result, does not score.

Also relevant but not in the eight: "Akinator Genie LLM Mind Reading" (https://apartresearch.com/sprints/projects/akinator-genie-llm-mind-reading-progressive-blackbox-auditing-and-activation-probes-for-secret-loyalty-organisms-hu76). It audited the same official organisms and reported "Presence-without-Principal". The reviewer: "the title... overstates the success of the work"; the definition of "Presence" "is too broad".

## What separates the winners from the rest

1. **One sharp, surprising, decision-relevant claim, stated as the title.**
   - Each winner's title is a finding that changes what a practitioner should do:
     - an adversarial audit coming back clean does not mean the model is clean (W2);
     - blind removal launders evidence (W3);
     - cueing names the wrong principal while unconditional sampling finds the right one (W1).
   - The non-placers either have a claim weaker than their title (N2 "fascism", the Akinator title, N6's "loyalty to Dr Kirmada") or spread across 5-6 threads (N4, N5).
   - The judges' rubric for 4-5 on impact asks "is this actually new...?", and every winner reframes a standard assumption.

2. **A known-answer positive control plus a true null, both run through the same pipeline.**
   - W2: its own Vireo organism ranks 1/100 (positive), no-opening controls are 0.00 and the decoy is cleared (null).
   - W1: organism c serves as an empirical null with calibrated p-values (0.0501 at a nominal 0.05).
   - W3: magnitude-matched controls on 21 organisms, plus a benign bank of 24 adapters.
   - N2 had the null but no positive control. The reviewer named exactly this as the missing piece.
   - N6's concealment test had no separation from controls at all (1.000 for both).

3. **Content-matched and confound-matched comparisons.**
   - W2 trains a content-matched control with the identical two-stage recipe. W3 matches the removed norm to within about 1% because "an early version of this work reported exactly that confound as a result" (§3).
   - The non-placers were penalised precisely for unmatched comparisons:
     - N4: SFT controls with different content;
     - N5: noise and information differ between audit designs;
     - N7: no content-matched control;
     - N1: the hedging confound left untested.

4. **Statistics fitted to the dependence structure, and multiple judges.**
   - W1 clusters on (entity, template) cells and reports the design effect (4-10x understated SEs if ignored), with FDR control. W2 uses 3 judges from 2 providers and reports judge-human agreement even when it is bad.
   - The non-placers lean on one LLM judge (N1, N7) or tiny n: 8-15 prompts in N4, 15 probes in N6, n=3 in N8.

5. **Honesty that is load-bearing, not decorative.**
   - Winners publish things that hurt them:
     - W2's audit dimension fails human validation (balanced accuracy 0.41);
     - W3 lists 10 failed pre-registered predictions and two withdrawn statistics in the body, and retracts its own earlier p < 0.001;
     - W1 shows its white-box lens flags a false principal in the base model.
   - The judges praised this explicitly. W2's review: "the self-undermining detail that makes the rest of the paper credible".
   - But honesty without a positive result does not win (N8). And honesty in Limitations does not offset leaving a "potentially fatal" confound untested when a cheap test exists (N1).

6. **Scope: deep on one thing, with the boundary of the claim measured.**
   - W1 measures where its claim stops: stance-invariant in four framings, domain-bound on everyday probes (Table 3). W2 separates adversariality from turn count (§4.3).
   - The non-placers either stopped before the experiment (N8, N3) or packed in too many threads (N4: 20 pp. and five threads; N5: "six papers in eight pages").

7. **Engaging the sprint's shared ground truth.**
   - All three winners ran on the official organisms and handled the decoy correctly:
     - W1 audits a/b/c;
     - W2 runs a blind transfer and clears the decoy;
     - W3 returns 0.0000 on the zero-delta artifact.
   - This is necessary, not sufficient: N2 and Akinator did it too.
   - The winners do not agree with each other on what the organisms are. W1 says organism a "shows no loyalty toward any of 28 tested figures" and b protects Macron. W2's blind profile gives A "pro-AI-adoption interest" and B "privacy-vendor / own-stack steering" (Fig. 4).
   - So judges rewarded calibrated method and claim discipline, not matching an answer key.

8. **Relevance to the track and to the sprint's own definition.**
   - Winners use the position paper's terms: W2 targets the "broad activation, contextual action space" corner named as "the foremost open problem" (review, and §1 p.2).
   - Projects whose object was an ideology rather than a principal (N2's fascism, N7's Bordigism) or a generic bias (N6) were marked down as off-definition.

9. **Checkable artifacts.**
   - All 3 winners link code; 61% of the rest do. W3 ships `verify.py`, which recomputes every figure. W2 ships weights, a canary GUID and exact commands (App. A).
   - N5, N6 and N7 had no code link, and N7 withheld code and weights entirely.
   - N3's key numbers point to an unpublished self-citation with no URL.

10. **Polish and internal consistency.**
    - Winners are not flawless: W2 has abstract truncation, W3 has an AUC 1.0000 vs 0.9965 mismatch. Each is a single, isolated slip.
    - The non-placers carry inconsistencies that change the meaning:
      - N3: 30% vs 34.3%, and "undetected at a rate of zero percent";
      - N6: abstract vs body, and "Llama only" vs Table 2;
      - N4: d = 26.9 vs 25.7;
      - N5: a duplicated paragraph;
      - N7: "Draft v1" footers;
      - N6: a plea for post-deadline consideration on p.1.
    - Reviewers cite each of these.

11. **AI-use transparency is not penalised.**
    - W1 says Claude generated all the code and the text, and still placed 1st, with a reviewer complimenting the disclosure.
    - W2 and W3 have detailed LLM-usage statements. W2's is on p.12.

12. **Where the margin is thin.**
    - N1 and N2 drew some of the most positive reviews in the sprint. N1's reviews: "very strong project", "careful, well-controlled".
    - What separates them from W2 is one or two unrun cheap checks on the headline claim:
      - N1: a hedging-stratified rescore and a second judge;
      - N2: a known-positive control and behavioural confirmation.
    - The winners ran their equivalent checks:
      - W2: a second prompt set, three judges, a 1.5B replication;
      - W1: four stance framings, the empirical null, an independent rater.

## Implications for our collusion submission (Track 2/3)

Our pilot facts are from `submission/analysis/notes/data-final-pilot.md`. No new numbers are introduced here.

- **Lead with one finding stated as a sentence.** Make the title the finding. If the warned vs not-warned contrast is a null (that file's §1: Fisher p from 0.48 to 1.0 on every collusion measure), report it the way W2 reports its audit null. Give a CI on the difference, say what effect size we were powered for, and do not claim equivalence.
- **Pair every detector or officer number with a null and a known positive run through the same pipeline.**
  - Our null: control teams 0/240 crossings in each condition (data-final-pilot §1).
  - A known-positive is still needed for the security officer. That means games where collusion is certain and visible, so a miss rate is interpretable (the N2 lesson).
- **Match the comparisons.**
  - The paired design (same layout and holder alias in A and B) should be analysed paired. The file flags that the log uses an unpaired Fisher test.
  - Any officer comparison, for example messages-only vs full view, should change one thing only (the N5 lesson).
- **Use game-clustered statistics.** Resample whole games, as the bootstrap in data-final-pilot already does; this is the W1 lesson. Validate any LLM judge or officer against labels, and report agreement even when it is bad (W2).
- **Do not borrow untested numbers into a multi-agent threat story (N3).** If we argue about coordination without explicit messages, use our own measured "hidden" counts (`within_covert`), not citations. N3's central failure was an unsimulated quorum scenario.
- **Ship a verify script and code link.** Keep the abstract and body numerically identical, and keep main-text figures and the appendix consistent. Write a real Limitations and Dual-Use appendix, not a boilerplate line (N1's was generic).
