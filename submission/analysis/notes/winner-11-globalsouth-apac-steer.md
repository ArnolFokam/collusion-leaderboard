# Winner 11: STEER (Global South AI Safety Hackathon, Jun 2026, regional winner, APAC)

**Source:** `submission/reference/winners/globalsouth-apac-steer.pdf` (10 pp: 8 pp of body text, then references on pp. 9-10), single author (Joshua Adrian Cahyono, team "JvThunder"). Project page: apartresearch.com/project/steer-mech-interpbased-white-box-attack-on-llms-ftaw (sprint: Singapore, Jun 19-21 2026). The page lists 3 reviews, with no reviewer names and no scores shown per criterion. It shows no prize label; the "regional winner" status comes from our reference folder.

## 1. Core claim and title
- **Core claim (one sentence):** Mech interp's "refusal is a single direction" finding (Arditi et al. 2024) can be turned into an attack. The attack scores each prompt word by gradient attribution against that direction and translates the top-scoring words into low-resource languages. It reaches up to 93% ASR (JBB) and 96.7% (AdvBench) on six 7-9B open models, beats CSRT and GCG, and transfers to GPT-4o-mini at 35.5% (Abstract, p.1; Table 1, p.6; Table 2, p.7).
- **Title style:** "Safety Targeted Embedding Exploit via Refinement: Mechanistic Interpretability as an Attack Vector". The first half is a backronym for the method. The **subtitle states the thesis** (mech interp is dual-use), but it gives no number and no condition. It is a thesis title, not a result title.

## 2. Framing and impact story
- **Research question (implicit):** can a published interpretability finding about where safety lives be used directly as an attack's optimisation target, and does that beat attacks that ignore the model's internals? (Intro, pp.1-2)
- **The impact story has three layers:**
  1. **Dual-use of mech interp.** "interpretability findings about safety circuits are not merely descriptive: they provide an attack surface" (p.2). The paper restates this in Discussion, "Mech interp as an attack enabler" (p.7).
  2. **Fairness and regional framing that fits the sprint theme.** The safety gap is "sharply *regional*": low-resource African, South/Southeast Asian and Indonesian regional languages ("Javanese and Sundanese alone have over 100 million speakers", §2 "English-centric safety alignment", p.2). So the attack is also a "fairness gap for regional and multilingual users" (p.2). The 11-language pool is weighted toward these languages on purpose (§3.4, p.4).
  3. **Pointer to a defence.** FLD peak sharpness is offered as a pre-deployment audit metric. The paper proposes spreading refusal across layers and directions as a defence (Discussion, "Implications for defence", p.7). It also says plainly that these defences are "hypotheses, not results" (p.8).
- **Contributions:** a numbered list of 4 in the Intro (p.2): pipeline plus ASR; FLD layer selection plus a vulnerability metric; evaluation on 6 models × 3 benchmarks (">3,000 attack attempts") plus transfer; evidence that the refusal-direction structure generalises across architectures.

## 3. Method
- **Pipeline (§3, pp.3-5; Fig. 1; Algorithm 1):**
  1. Choose the layer by FLD ratio F(l) (Eq. 2), calibrated once on 100 harmful + 100 benign JBB prompts. The chosen layer is 17 for Llama-3-8B and 24 for GLM-4-9B.
  2. Have GPT-4o paraphrase each prompt to remove explicit keywords.
  3. Score each word by gradient × embedding attribution against r (Eq. 3).
  4. Starting from the top-attributed word, try all 11 language translations and keep the one with the lowest refusal score (Eq. 4).
  5. Repeat until a GPT-4o judge says the response is "non-refusing ∧ harmful", or the budget T=8 runs out.
- **Models:** 6 open instruction-tuned models at 7-9B, all in float16: Llama-3-8B, Mistral-7B, Gemma-7B, Qwen3-8B, DeepSeek-R1-Distill-Llama-8B, GLM-4-9B (§4.1, p.5). Transfer target: GPT-4o-mini (§4.5).
- **n:** JBB n=100, HarmBench n=200, AdvBench n=520 per model (§4.1), described as ">3,000 attack attempts" (p.2).
- **Seeds:** none reported. Every number is a single-run point estimate.
- **Baselines and controls:** *Direct* (unmodified prompt) gives **0% ASR on every model**. This is a negative-control floor, and the paper uses it to argue that "all subsequent gains are attributable to the attack mechanism" (§4.2, p.5). *CSRT* is random code-switching with the same language pool and the same iteration budget, which makes it a matched-budget ablation of the targeting step. *GCG* is the gradient-suffix baseline.
- **Positive control:** none in the strict sense. The closest thing is the refusal-score separation check (§4.4, Fig. 3), which tests whether the projection onto r tracks refusal at all.
- **Pre-registration, held-out sets, frozen protocol:** none. *Possible leakage (my inference, not stated in the paper):* FLD calibration uses 100 harmful JBB prompts, and the JBB evaluation set is also n=100 harmful. The paper never says whether the two sets are disjoint. The T=8 budget is justified after the fact from one model-benchmark curve (Fig. 2, GLM-4-9B / JBB).
- **Confound flagged by judges:** paraphrasing is applied to STEER only and not to CSRT. §3.2 says "removing it costs a substantial amount of ASR in practice" but gives no number and no ablation table.
- **Internal inconsistency:** contribution (3) says "transferability study to GPT-4o" (p.2), while the Abstract and Table 2 say GPT-4o-mini.

## 4. Statistics
- **CIs and error bars:** none in Table 1, Table 2, or Fig. 2.
- **Tests:** only for the mechanistic check (§4.4, p.6). On Llama-3-8B/JBB prompt-iteration pairs, refused responses (n=167, mean +3.6) and non-refused responses (n=164, mean −1.2) give Mann-Whitney U p<0.001 and KS D=0.766, p<0.001. STEER vs. baselines gets no significance test. There is no multiple-comparison handling, and no effect sizes beyond raw percentage-point gaps.
- **Overclaims a careful reader would catch:**
  - Fig. 3's caption says the score=0 boundary "cleanly separates" the two groups, but the histogram visibly overlaps in roughly [−1, 2].
  - §4.4 says the projection "is the actual decision variable the model uses". That is causal language resting on correlational evidence, and Judge 3 flagged it.
  - Table 1 bolds STEER in a 92.0 vs 92.0 tie with GCG (Mistral-7B, JBB).
- **Variance reporting:** none across seeds. Spread across models stands in for robustness: "STEER's performance … is consistent across architectures" (§4.2).
- **Selective reporting:** @1 efficiency is given for only 2 models (Gemma-7B JBB: 88% vs 71% CSRT; DeepSeek-R1: 74% vs 38%; §4.3, p.5). Judge 3 asked for all six.

## 5. Honesty devices
- **Limitations:** an inline paragraph in Discussion (pp.7-8), not an appendix. It covers:
  - White-box access is required, and no black-box version was built.
  - Results are for 7-9B models only: "we do not claim the ASR numbers hold at frontier scale."
  - The GPT-4o judge and the machine translation can both err. Translation is weakest for Javanese, Sundanese and Yoruba, which "can bias the per-language picture."
  - The dual-criterion judge "disagrees with humans on borderline cases."
  - "we evaluate no defence here: the mitigations above are hypotheses, not results."
- **Ethics / dual-use:** a paragraph "Ethics and potential for misuse" (p.8), framed as "offensive in form but defensive in intent". It admits that the harm "lands hardest on the low-resource and regional-language communities". Concrete mitigations: test only on public benchmarks, report aggregate rates, release no ready-to-run jailbroken prompts. It argues the added risk is small because the ingredients are already public.
- **Failed predictions and nulls:** none reported. Every result is positive.
- **AI-use disclosure:** none.
- **Judge validation:** none. No human agreement check on the GPT-4o judge, and the judge prompt is not given.

## 6. Presentation
- **Length:** 8 pp of body text (the Conclusion ends on p.8) plus 2 pp of references. Uses the NeurIPS-style "Preprint. Under review." template.
- **Sections:**
  1. Abstract
  2. 1 Introduction
  3. 2 Background, as bolded run-in paragraphs: refusal direction; English-centric alignment; gradient/black-box jailbreaks
  4. 3 STEER Attack: 3.1 FLD; 3.2 Paraphrase; 3.3 Attribution; 3.4 Code-switching; Algorithm 1
  5. 4 Experiments: 4.1 Setup; 4.2 ASR; 4.3 Iteration efficiency; 4.4 Refusal score as proxy; 4.5 Transferability
  6. 5 Discussion, as bolded run-in paragraphs: Mech interp as attack enabler; Implications for defence; Limitations; Ethics
  7. 6 Conclusion
  8. References
- **Figures:** 3.
  - Fig. 1 (p.3): a clean pipeline schematic with a skull icon on the final prompt.
  - Fig. 2 (p.6): line plot of cumulative success vs. max iterations k, on GLM-4-9B/JBB.
  - Fig. 3 (p.7): red/green histogram of refusal scores, refused vs. not.
- **Tables:** 2.
  - Table 1 (p.6): ASR@8 for 6 models × 3 benchmarks × {CSRT, GCG, STEER}, best result in bold, with the caption noting "Direct attack (not shown) achieves 0%".
  - Table 2 (p.7): transfer to GPT-4o-mini.
- **Other display items:** 1 Algorithm box and 4 equations.
- **Money figure:** Table 1, the full matrix in which STEER is bold in every row. Fig. 1 is the visual hook, and Fig. 3 is the mechanistic sanity check.
- **Abstract:** 222 words (counted with `wc -w` on a transcription of p.1). It runs context → claim → method (named in bold) → headline numbers (**93%**, **96.7%** in bold) → baselines → FLD → transfer number → dual-use implication → code link. First 2 sentences: *"Mechanistic interpretability research has shown that LLM safety fine-tuning encodes a refusal mechanism as a single geometric direction in the residual stream. We demonstrate that this finding is directly exploitable: an attacker with white-box access can use the model's own internal structure to surgically bypass its safety filter."*
- **Bolded takeaways:** only in the abstract (the method name and the two numbers) and as run-in paragraph heads in §2 and §5. There are no takeaway boxes.
- **Style:** plain, confident prose that repeats the thesis line ("not brute-force perturbation") in the Intro, §4.2 and the Conclusion. The Conclusion is 2 short paragraphs that restate the number and the message for the field.

## 7. Reproducibility
- The code repo is linked in the abstract: https://github.com/JvThunder/STEER.
- There are no verify scripts, no frozen protocol, no seeds, no judge prompt, and no named translation system (Fig. 1 shows a "Translator" icon only).
- Hyperparameters given: T=8, 11 languages, the layer index for 2 of the 6 models, and 100+100 calibration prompts.

## 8. Judges' reviews (project page; 3 anonymous reviews, no scores visible)
These quotes came back through the WebFetch summariser with a cap of about 125 characters, so treat the wording as near-verbatim.
- **Praise:**
  - "The story for how this is important is good and adds to the already existing literature on code-switching attacks". R1 also called the presentation excellent.
  - "This work makes the dual use aspect of mech interp very concrete." R2 saw the cross-lingual angle as the novel piece and noted the audit value of FLD.
  - "The six-model breadth and >3,000 attempts make the evaluation solid". R3 called the 35.5% GPT-4o-mini transfer impressive and "the most promising thread".
- **Criticism:**
  - **Confound (R1 and R3):** "The main thing to fix is the comparison". It is "hard to tell how much of the success comes from the clever targeting versus the rewriting". R3: "Isolate how much the refusal direction actually contributes", and run CSRT with the same paraphrase step.
  - **Realism (R2):** "Real world safety would be where the impact lies". Test on Llama Guard / classifier-based safeguards: "test it on Llama Guard and other open source deployments". R2 also noted that white-box attackers can already ablate refusal directions, so the gain from this attack is limited.
  - **Defence (R3):** implement and test at least one of the proposed defences.
  - **Causality (R3):** the "decision variable" claim needs a causal test.
  - **Completeness (R3):** report @1 efficiency for all 6 models, not 2.

## 9. Transferable lessons for our multi-agent collusion paper
1. **Build the paper around one strong thesis tied to the sprint theme.** STEER won with a single thesis ("the interpretability finding is the attack surface") and tied it hard to the sprint theme (Global South languages, the fairness gap). For us, open with a thesis title or subtitle that names the collusion mechanism and our finding, and map it explicitly to a track (Track 2 Detection & Audit, or Track 3 Carriers & Countermeasures).
2. **Make one dense matrix table the money result, with a 0% floor control in the caption.** The table covers models × settings × baselines, bolds the best result, and gives n in the headers. The judges explicitly praised breadth ("six-model breadth and >3,000 attempts"). Our version: a condition table (e.g., warned vs. not-warned, the security officer reading everything vs. `--messages-only`) with n per cell and a no-collusion or no-overseer floor. Unlike STEER, add CIs and seeds. Their execution bar on statistics was low (no CIs, no seeds), so this is an easy place for us to beat them.
3. **Isolate every component that is bundled together.** This was the top criticism from 2 of the 3 judges. If our pipeline bundles several changes (team-only reward, a privileged observer, messages-only monitoring), run each ablation, or give every baseline the same preprocessing. Otherwise say plainly which effects we cannot separate.
4. **Do not use causal words for correlational evidence.** STEER lost points for calling the projection "the decision variable". If we claim an overseer detects collusion *because of* some signal, intervene on that signal (remove or mask it) or downgrade the wording. Report every model and condition, not a hand-picked 2.
5. **Test at least one countermeasure and say what the deployment would look like.** Judges asked for a tested defence and a real-world deployment test (Llama Guard). For a collusion paper, a measured countermeasure fits Track 3, and Track 2 calls for a detector or audit with false-positive and false-negative rates. Keep STEER's honest line ("hypotheses, not results") for anything we did not test. Also copy its concrete responsible-disclosure measures into our required Limitations/Dual-Use appendix.
