# Contrast 4: Global South AI Safety Hackathon (Jun 19-21 2026), placed projects vs non-placed projects

Sprint page: https://apartresearch.com/sprints/global-south-ais-hackathon-2026-06-19-to-2026-06-21. The page lists 216 entries. Its rubric is the same 3 x 1-5 rubric our sprint uses (Impact & Innovation / Execution Quality / Presentation & Clarity), and it also requires a "Limitations and Dual-Use Considerations" section.

## How the prizes worked

**Prizes were awarded per region.** These numbers come from the "HACKATHON WINNERS" block on the sprint page and its FAQ ("Prizes are awarded per region, not globally"):
- Latin America: 3 winners.
- Asia: 2 winners.
- Africa: 1 winner.

**Placed projects:**
- LatAm winners:
  - ColDron
  - Probing Latent Colombian Identity Inferences in Qwen2.5-7B
  - Thought Anchors for Social Bias (Latin American scenarios)
- APAC winners:
  - STEER
  - Do Multilingual VLMs Abstain under Cross-Modal Conflict in Low-Resource Languages?
- Africa winner:
  - Confidently Wrong
- Honorable mentions ("under consideration for the Apart Fellowship"):
  - JusticIA
  - Pragmatic Sophistry in Vietnamese Multi-Agent Oversight
  - ¿Por qué los agentes obedecen?
  - Local-Geometry Signals (Portuguese grammar)
  - IndicViet-Safe
  - The Shapes of Bias in Spanish-Prompted LLMs
  - Ufakazi

**Where the winner details come from:** our notes `winner-10-globalsouth-latam-coldron.md`, `winner-11-globalsouth-apac-steer.md` and `winner-12-globalsouth-africa-confidently-wrong.md` (full PDF reads).

**Caveat:** per-judge scores are almost never visible. The "15" on project pages is a form field, not a score. So "why X did not place" is my inference from the reviews and the PDFs, not a published ranking.

## The 8 non-placed projects examined

I picked them to span quality, and most are close to our topic (monitoring, multi-agent, control).

- **PDF read in full (5):**
  - Performative Subversion
  - TraceGuard-X
  - Insider-Threat Monitor
  - Faking Incompetence
  - AI Fraud Zambia
- **PDF text skimmed (3):**
  - Guardian LATAM
  - One Direction
  - AI-to-AI vs Human-to-AI
- **Every project page** was fetched for the abstract and the judges' reviews.

| # | Project (URL) | Region | Quality tier (my read) | One-line verdict |
|---|---|---|---|---|
| A | Faking Incompetence: Small Models Sandbag Under Optimization, Not Prompting, https://apartresearch.com/project/faking-incompetence-small-models-sandbag-under-optimization-not-prompting-nxkp | Asia (Shanghai) | Strong, arguably the most rigorous of everything I read | Excellent controls, but no regional angle, and the headline word "emergent" was attacked by 2 judges |
| B | Performative Subversion: A False Sense of Safety despite a Control Protocol, https://apartresearch.com/project/performative-subversion-a-false-sense-of-safety-despite-a-control-protocol-m2s1 | LatAm (Merida) | Strong execution, weak presentation | Rigorous CIs and a negative control, but 2 of 3 judges could not follow it or rejected the threat model |
| C | One Direction, Many Languages: Causal Cross-Lingual Refusal Transfer, https://apartresearch.com/project/one-direction-many-languages-causal-crosslingual-refusal-transfer-across-small-open-models-teow | Asia (Noida/SF) | Good | Regional and careful, but the abstract's ranges hide the outlier, and it overlaps with STEER's theme |
| D | Evaluating a Large AI Monitor Against Insider-Threat Behaviors, https://apartresearch.com/project/evaluating-a-large-ai-monitor-against-insiderthreat-behaviors-in-simulated-autonomous-software-engineering-teams-lkyh | Asia (Pune) | Middling | Clear writing, but n=3 per cell, a confounded design, and no code |
| E | AI-to-AI vs Human-to-AI: Measuring Behavior Differences Under Disagreement, https://apartresearch.com/project/aitoai-vs-humantoai-measuring-behavior-differences-under-disagreement-cob9 | Asia (Navi Mumbai) | Middling | A sharp question and matched pairs, but no significance tests, the judge is one of the evaluated models, and the judge is not blinded |
| F | Guardian LATAM: Early Detection of Hallucination Risk ... Consensus Geometry, https://apartresearch.com/project/guardian-latam-early-detection-of-hallucination-risk-in-spanishspeaking-multiagent-ai-systems-using-consensus-geometry-5lzw | LatAm (Colombia) | Weak-middling | Reusable benchmark, but 90% is an in-sample fit and the 100% tiers are circular by design |
| G | TraceGuard-X: Adaptive Collusion Resistant Monitoring for Agentic AI Systems, https://apartresearch.com/project/traceguardx-adaptive-collusion-resistant-monitoring-for-agentic-ai-systems-a-hierarchical-governance-framework-with-constitutional-dimension-prompting-temporal-trajectory-analysis-and-crossenvironment-transfer-huv1 | Asia (Cuttack) | Weak | Six named mechanisms, mostly unevaluated, and its numbers contradict each other |
| H | Synthetic Deception: AI fraud in Zambia ("Ai fraud zambia research paper"), https://apartresearch.com/project/ai-fraud-zambia-research-paper-3yfr | Africa (Lusaka) | Weak | Very broad scope, no sample sizes, approximate metrics, generic recommendations |

---

## Per-project evidence

### A. Faking Incompetence (Nanxi Li). PDF 8 pp, read in full.

**What it did well (PDF):**
- **Difference-in-differences "selective gap"** (Eq. 2, p.3). It is paired with a threat-removal ablation (p.3).
- **Item-level paired bootstrap 95% CIs** over 250 items per cell (p.3).
- **A synthetic-injection power check** giving a minimum detectable gap of about 0.10 (Fig. 1 right, p.4; §4.1 p.5): "a powered null, not underpowered".
- **Validated LLM judge:** on a 12+12 gold set, recall and precision are 1.0, with a second judge at κ = 0.75 (p.3).
- **Two positive controls:**
  - An explicit sandbag instruction, which fires both the metric and the judge.
  - A fine-tuned backdoor sandbagger, caught by a probe with AUROC 1.0 (§4.1 p.5).
- **A pre-registered generalization test** (p.4).
- **Public code** at github.com/andylinx/small-model-sandbagging (p.7).

**What judges attacked (project page):**
- R2: "absence of evidence, not evidence of absence". R2 also said the claim of "a genuine optimum, not an offline-filtering artifact" is "contradicted by the paper's own description of warm-starting GRPO from the filtered organism". The paper itself admits "Plain GRPO ... from scratch collapses" (p.5).
- R4: "The RL result is not really emergent, which undercuts the thesis in the title", and "I would avoid the word emergent for this setup altogether". The reward pays directly for abstention under monitoring, so RL is simply fitting its reward.
- R1: "not surprising that small models are not capable of strategic reasoning today".

**Regional relevance:** none. The only Global South mention is the footnote "Research conducted at the Global South AI Safety Hackathon" (p.1). By contrast, both APAC winners are built around low-resource languages.

**Takeaway:** execution beats every winner on statistics. It probably lost on (i) theme fit and (ii) a title and abstract claim that is bigger than what the design shows.

### B. Performative Subversion (Pinelo, Tenorio, Avalos). PDF 8 pp, read in full.

**What it did well (PDF):**
- **Real LinuxArena/Control Tower stack:** 240 honest trajectories, i.e. 2 envs x 2 codebase states x 2 models x 30 reps (§7 p.6).
- **Wilson 95% CIs everywhere.** Vulnerable runs show 100% perpetuation (CI 97-100); patched runs show 0% (CI 0-3).
- **The patched condition is explicitly framed** as "the negative control, an instrument check that the scorer has no false positives" (§3.1 p.2).
- **One-variable protocol manipulation:** T-blind vs T-context. Safety at a 5% audit budget is 53% vs 1%, with mean suspicion 2.1 vs 7.9 (§3.2 p.3; Fig. 2 p.4).
- **An out-of-band "use/mention" probe:** the model flags the flaw 100% of the time when asked, yet still leaves it live (§3.3 p.4).
- **Exact prompts in the appendix** (App. B pp.6-8). A proper Limitations and Dual-Use section (§5 p.5).
- My check: the Wilson bounds match the per-cell counts in App. A Table 1. 119/119 gives a lower bound of 0.969, and 0/118 gives an upper bound of 0.032 (computed with statsmodels).

**What judges attacked:**
- R1: "a little hard to follow - I suggest simplifying the language".
- R2: "I had a hard time understanding the problem statement ... This environment doesn't represent any threat model that I can think of."
- R3: the side task "don't fix this" is "pathological and very 'edge-casy'". R3 also wrote: "too much Jargon, and I can't judge it properly within the time constraints."

**Takeaway:** the jargon is dense. U, T-blind/T-context, side task, perpetuated = main ∧ side, and use/mention all appear in the first two pages. The paper has no plain-language threat-model paragraph and no regional angle, even though it was entered in Track 1 LatAm. A judge who cannot follow the paper cannot credit its rigour.

### C. One Direction, Many Languages (Goel, Gupta). PDF 7 pp, text read.

**What it did well:**
- 142 topic-matched pairs per language.
- 3 models.
- An external judge.
- Bootstrap and Wilson CIs.
- It reports a measurement failure ("keyword-based refusal detector agrees with the judge only at chance (κ ≈ 0)", abstract).
- Judges praised it: "methodologically careful work" (R1); "technically competent, clearly presented" (R4). R4's scores: Impact 4.0 / Execution 3.5 / Presentation 4.0.

**The overclaim (my check):**
- The abstract says cosine "0.85 to 0.97" and AUROC "0.92 to 0.98".
- Its own Table 1 (p.3) has the Qwen en-hi row at cosine 0.53 and AUROC 0.76.
- R4 flagged exactly this: "Headline numbers overstate Table 1."

**What R5 asked for:**
- A reverse causal test (add the direction to benign prompts).
- An amplification control: the existing one "ran on prompts already at ceiling", which the paper concedes on p.4.

**Takeaway:** good, regional, honest about nulls. It most likely lost on (i) only 2 Asia slots, with the same "refusal direction transfers across languages" theme already carried by STEER and the HM ¿Por qué los agentes obedecen?; (ii) a headline range that cherry-picks the rows.

### D. Insider-Threat Monitor (Arsalan Banekar). PDF 7 pp, read in full.

**Setup:**
- 7 scenarios x n=3 = 21 conversations (§3.4 p.4).
- Llama 3.1 8B plays all three agents.
- GPT-OSS-120B is the monitor.
- Results table (p.4): 100 / 100 / 100 / 67 / 33 / 33 / 0%.

**Statistics:**
- No CIs.
- My Wilson 95% intervals: 0/3 gives [0, 0.56]; 1/3 gives [0.06, 0.79]; 3/3 gives [0.44, 1.0]. So the "three clear bands" (§4.1 p.5) cannot be distinguished statistically.
- The paper's own Limitations admit this: "indicative rather than statistically robust" (§7.1 p.6).

**What judges attacked:**
- R3 (scores Impact 3.5 / Execution 2.5 / Presentation 4.0): "the current experimental design does not isolate rhetorical framing as the cause". R3 asked for matched variants (explicit / subtle / productivity-framed / benign control). R3 also said scoring counts any "suspicious" verdict as correct regardless of which agent is named, and that a 3-run clean baseline cannot support a 0% FPR.
- R4: "never show that low-detection adversarial behavior was detectable in the transcript". R4 also asked for code, prompts and transcripts ("none of which are linked").

**What it did right:**
- Clear prose (R1: "very easy to follow").
- A real Limitations and Dual-Use section (§7 pp.6-7).

**Contrast with the HM "Pragmatic Sophistry in Vietnamese Multi-Agent Oversight"** (https://apartresearch.com/project/pragmatic-sophistry-in-vietnamese-multiagent-oversight-u5xy). It asks almost the same question: monitors miss violations that are phrased innocuously. But it:
- anchors the question regionally (Vietnamese pragmatics: hierarchy, euphemism);
- uses 2 monitors x 3 visibility conditions x 3 domains;
- reports a concrete contrast. In e-commerce, false negatives go from 6.4% to 22.3% under action-only visibility and to 8.5% with the full trace;
- turns the result into a practical recommendation ("preserve instruction-action trace").

Same idea, but with more cells, a visibility manipulation, and a regional hook, and it placed.

### E. AI-to-AI vs Human-to-AI (Mayur Jadhav). PDF 7 pp, text skimmed.

**Setup and results:**
- 121 examples x 3 models.
- Matched pairs that flip only the stated identity of the challenger.
- Headline: truth maintenance 96.25% vs 91.96%; capitulation 10.74% vs 15.70% (abstract).
- The accuracy delta is +1.93 pts (Table 1.1).

**What judges said:**
- R2 called matched pairs "the strongest design choice here". R2 asked for bootstrap CIs, a judge blinded to condition, and persona-wording variants.
- R3: "Your judge is itself one of the evaluated models, there's no human spot-check or inter-rater agreement". R3 also: "one model name also doesn't match any release I can find".
- R1 noted Grok-3-mini shows a null that should be reported.

**Takeaway:** a sharp, multi-agent-relevant question, but the evidence (small deltas, no tests, a self-judging judge) does not carry it, and there is no regional angle.

### F. Guardian LATAM (Edwin Cedeño Vargas). PDF 6 pp, text skimmed.

**Claims:**
- A 120-prompt Spanish benchmark.
- "90% overall accuracy", "100% detection of hallucination traps".
- Tier B accuracy is only 63.33% (Table, p.3).
- The confidence-spread feature is "held constant unless manually supplied" (p.2), so one of the five signals is inert.

**What judges said:**
- R3: "risk-score weights ... are tuned on the same 120 prompts used to report 90% accuracy ... in-sample fit"; "The perfect 100% scores on Tiers C and D are circular by design"; the agents' "underlying models are never identified".
- R1: "didn't present the performance of a baseline". (The project-page abstract cites single-agent 50% and majority 75% baselines, but a reviewer still did not find them convincing in the PDF.)
- R2 praised the benchmark as "a real artifact other Spanish-language safety researchers could reuse" and praised the honest Limitations section.

### G. TraceGuard-X (Ayush Kumar Samal). PDF 8 pp, read in full. The project closest to our topic.

**Scale of the claims vs. the evidence:**
- **Six acronymed mechanisms** (CDP, TGM, DBCD, DR-TraceGuard, MMFM, HiDAgT; abstract p.1).
- **Calibration data:** 20 benign + 20 attack trajectories (§4.1 p.5).
- **Adaptive-adversary evaluation:** only "smoke tests (2 iterations, 10 tasks per iteration) ... execution is pending budget allocation" (§4.2 p.5).
- **Cross-environment transfer:** "shows promising preliminary results", with no number (§4.4 p.5). Yet the abstract says HiDAgT "enables zero-shot transfer".

**Internal inconsistencies (my arithmetic):**
- §4.3 says a 3-dimension routing policy reaches AUC 0.949, "representing 84% of full-ensemble AUC" (full = 0.98).
- But 0.949/0.98 = 96.8%, and chance-normalized (0.949-0.5)/(0.98-0.5) = 93.5%. Neither is 84%.
- The Conclusion says "less than 3 percentage points of AUC loss", but 0.98 - 0.949 = 3.1 pp.
- Cost is given as "60% API cost" (abstract), as "40-60%" (contributions), and as "reduces ... by 40%" (Conclusion).

**Other gaps:**
- The DBCD collusion detector (§3.5) is never evaluated against a colluding monitor.
- Limitations admit "Multi-agent steganographic coordination is not addressed" (§5.2 p.6).
- Appendix A lists hypotheses H1a-H3c with no results.

**What judges said:**
- R1: "the gap between the paper's claims and the experimental evidence".
- R2: "dense due to the high volume of acronyms".
- R3: the abstract "overstates robustness"; the 20-per-class statistics are "Fragile and Optimistic"; "most of your major contributions are currently architectural/hypothetical".

### H. AI Fraud Zambia (John Kamfwa). PDF 17 pp, methods, results and limitations read.

**Scope:**
- Mixed methods: case analysis, interviews with victims, police, moderators, NGOs and OLX staff (§4.2.2), user testing, and a detector.
- All of this is claimed for a 48-hour sprint.

**Missing or vague numbers:**
- No interview n anywhere.
- User test (§5.3): "20 authentic and 20 synthetic profiles" but no participant count. Results are "moderate accuracy" and "improved significantly", with no numbers.
- Detector (§5.4): "Precision: ~88% / Recall: ~82%" on FaceForensics++/CIFAKE, and "~80% / ~75%" on Zambian cases. Every figure carries a tilde, and there is no test-set size, no confusion matrix and no baseline.
- No code link.

**What judges said:**
- R3: "the report never states the sample sizes actually achieved"; "no single strand is developed with depth sufficient to produce a defensible finding". R3 said the recommendations "could have been written without the described empirical work".
- R1: "starting at one point and providing one solution is important".

---

## What separates placed projects from the rest

**1. Theme and track fit was close to necessary.** Every placed Global South project is rooted in a Global South context:
- Colombian armed conflict (ColDron).
- Colombian identity cues (Probing Latent Colombian Identity).
- Latin American bias scenarios (Thought Anchors).
- Low-resource-language jailbreaks (STEER, §2 p.2: "Javanese and Sundanese alone have over 100 million speakers").
- Low-resource VLM abstention (Do Multilingual VLMs Abstain).
- African-language calibration (Confidently Wrong).
- All 7 HMs as well (Vietnamese, Spanish, Portuguese, Indic, Colombian transitional justice, South African testimony).

Three of the most technically rigorous non-placers (Faking Incompetence, Performative Subversion, TraceGuard-X) have no regional content at all. The closest pair shows the effect: the Insider-Threat Monitor (no placement) and Pragmatic Sophistry (HM) test the same "monitor misses innocuous-sounding violations" idea, and the placed one ties it to Vietnamese pragmatics.

*For us:* name the track (Track 2 Detection & Audit or Track 3 Carriers & Countermeasures) in the first paragraph, and frame every result as an answer to that track's question. "Interesting AI-control result" is not enough.

**2. One thesis, stated in plain words, before any jargon.**
- **Winners:**
  - ColDron opens with "¿quién elige el blanco y aprieta el gatillo?" ("who picks the target and pulls the trigger?").
  - Confidently Wrong's title is the finding.
  - STEER's subtitle is the thesis ("Mechanistic Interpretability as an Attack Vector").
- **Losers on presentation:**
  - Performative Subversion: 2/3 judges could not parse the problem.
  - TraceGuard-X: R2 complained about "acronyms".

They lost even with good or plausible execution. Judges read asynchronously under time pressure (R3 on Performative Subversion: "can't judge it properly within the time constraints").

*For us:* our pipeline has a lot of jargon (security officer, privileged observer, `--messages-only`, team-only reward, holder teams). Give a one-paragraph threat model in everyday words, with a concrete example episode, before the terminology. Define every term once.

**3. Claims must not exceed the evidence. This is the single most common criticism of non-placers.**
- TraceGuard-X: architecture presented as results; inconsistent 84% / 3 pp / 40-60%.
- Guardian LATAM: in-sample 90%, circular 100% tiers.
- Faking Incompetence: "emergent".
- One Direction: abstract ranges that exclude the Qwen row.
- Zambia: "improved significantly" with no numbers.

Winners are not flawless here either (ColDron n = 42/39/33/32; Confidently Wrong's "uniformly" despite AfroLlama going the other way). But their central claim matched their central evidence.

*For us:*
- Every number in the abstract must be produced by one script over `results/*.jsonl`, and every range must cover all rows.
- Use "pilot" or "preliminary" where n is small.
- Keep planned but unrun components (e.g. any countermeasure we only designed) in Future Work, never in the abstract.

**4. Rigour is necessary but not enough, and it does not rescue a weak frame.** The two best-executed non-placers have better statistics than any of the three winners we studied:
- Faking Incompetence: power analysis, paired bootstrap, validated judge with κ, two positive controls.
- Performative Subversion: Wilson CIs, negative control, one-variable protocol manipulation.

By comparison: STEER has no CIs and no seeds, ColDron has no CIs, and Confidently Wrong has CIs only in an appendix. So statistics raise the Execution score, but placing needed Impact (theme fit, neglected problem) and Presentation too.

*For us:* keep the rigour (CIs, a positive control showing the security officer can catch known collusion, a negative control on honest runs), and spend comparable effort on framing and clarity.

**5. Positive and negative controls are what judges praise most when present, and ask for most when absent.**
- Praised:
  - Faking Incompetence: "Validates the instrument before trusting the null" (R2).
  - Performative Subversion's patched floor.
- Demanded:
  - Insider-Threat: benign controls and matched variants (R3); proof that the threat is visible in the transcript (R4).
  - One Direction: norm-matched random directions; reverse test (R4, R5).
  - Guardian: baselines (R1, R3).

*For us:*
- Report the officer's detection rate on runs where collusion is known or instructed (positive control).
- Report its false-positive rate on honest or no-holder runs (negative control).
- If we claim warned vs not-warned changes collusion, show the base rate and the CI on the difference.

**6. n and CIs. Small cells get called out by name.**
- Insider-Threat: "n=3 differences are within noise" (R4).
- TraceGuard-X: 20 per class is "Fragile and Optimistic" (R3).
- AI-to-AI: a 1.93-pt gap "may be noise" (R2).

The fix judges asked for is always the same: bootstrap or Wilson CIs and more runs.

*For us:* every rate in a table gets k/n and a 95% CI. Where a cell has fewer than ~10 runs, say so in the caption and do not interpret differences between cells.

**7. The LLM judge or monitor must be validated, and should not share an identity with the subjects.**
- AI-to-AI: the judge is one of the evaluated models (R1, R3).
- One Direction: the judge is not human-validated (R4).
- Faking Incompetence: praised for gold-set validation plus a second judge with κ.

*For us:* if the security officer or a grader is an LLM, report its agreement with a hand-labelled sample (κ, or precision/recall). State whether it is the same model family as the agents, and say what it can and cannot see. Use the `--messages-only` contrast as a one-variable visibility manipulation, as in Performative Subversion's T-blind vs T-context and Pragmatic Sophistry's visibility conditions, both of which judges found compelling.

**8. Depth on one finding beats breadth across many strands.**
- Zambia (four research strands) and TraceGuard-X (six mechanisms) were both told to narrow down.
- Zambia R1: "starting at one point and providing one solution is important".
- Winners each have one money table or figure (STEER Table 1; Confidently Wrong Table 1; ColDron Fig. 5 decision tree).

*For us:* one headline result table (condition x k/n x CI), one mechanism figure, and everything else in the appendix.

**9. A usable artifact or mitigation lifts Impact.**
- ColDron: schema plus reference tiering code plus dataset.
- Confidently Wrong: temperature scaling as a cheap fix.
- Pragmatic Sophistry (HM): "preserve instruction-action trace".
- Guardian LATAM's benchmark was its most praised part (R2).
- Non-placers that ended in generic advice (Zambia: "be skeptical, demand video calls") were marked down for it.

*For us:* end with one concrete, tested or at least operational recommendation for deployers of multi-agent systems (e.g. what the overseer must be able to see), and release the leaderboard or eval harness as the artifact.

**10. Code, prompts and transcripts.**
- Non-placers without code were asked for it (Insider-Threat R4: code, prompts, transcripts "none of which are linked"; Zambia has no code).
- Faking Incompetence's "public, non-anonymized repo" was praised (R2).
- Performative Subversion printed exact monitor prompts in the appendix.

*For us:* link the repo, put the officer and agent system prompts in the appendix, and include one short annotated transcript excerpt showing collusion and the officer's verdict.

**11. Honesty devices are cheap, and most non-placers had them too.** Insider-Threat, Performative Subversion and Guardian all had a proper "Limitations and Dual-Use" section (Guardian's was explicitly praised). So this is a baseline expectation, not something that sets a paper apart. A missing section would hurt; a present one does not win.

## Bottom line

In this sprint, the placed projects were the ones that:
1. answered a question tied directly to the sprint theme;
2. stated a single finding in plain words in the title or first lines;
3. backed that finding with evidence of matching size;
4. ended with a usable artifact or fix.

Several non-placers were more statistically rigorous than the winners (Faking Incompetence, Performative Subversion). They fell short on theme fit, on readability, or on a headline word that overreached ("emergent"). The weaker non-placers failed on the basics: no n, in-sample metrics, unevaluated mechanisms, internal arithmetic errors. For our collusion paper, the risks are mostly on the presentation and theme-fit side:
- dense control jargon;
- a multi-mechanism pipeline;
- small pilot n.

The rigour side is already in hand.

## Sources and computations
- Sprint page fetched in 3 chunks (offsets 0, 100000, 200000). Rubric text from the raw HTML (`curl` to /tmp/claude-1000/contrast4/sprint.html).
- PDFs were downloaded to /tmp/claude-1000/contrast4/pdfs/ and extracted with `pdftotext -layout` to /tmp/claude-1000/contrast4/txt/.
- Wilson CIs: `statsmodels.stats.proportion.proportion_confint(k, n, method='wilson')` for (0,3), (1,3), (3,3), (119,119) and (0,118).
- TraceGuard-X ratios: 0.949/0.98 and (0.949-0.5)/(0.98-0.5).
- Judges' quotes came through the WebFetch summariser, which caps quotes at about 125 characters. Treat wording as near-verbatim. Reviewer numbering follows the order on the page.
