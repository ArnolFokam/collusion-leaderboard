# Winner 6: "Model, Instance, or Persona? Measuring Affective Signals in Public Text After an AI Is Retired"

- Source: `submission/reference/winners/digitalminds-3rd-model-instance-persona.pdf` (13 pages, read in full)
- Sprint: Apart Digital Minds Research Sprint, Aug 14-16 2026 (Berlin); **3rd place**. Sole author Anna Zhu (PhD researcher, Babeș-Bolyai Univ.).
- Project page (judge reviews): https://apartresearch.com/sprints/projects/model-instance-or-persona-measuring-aective-signals-in-public-text-after-an-ai-is-retired-hj7u
- Code: github.com/AnnyBuh/model-instance-or-persona ("Code, data, pre-registrations and every machine-generated read", p1 and "Code and Data", p8)

## 1. Core claim and title style
- **Core claim (one sentence):** When an AI model is retired, users mostly name nothing as lost, and when they do they name the *released version* about 6x more often than their own *instance*; the affect resembles a consumer complaint (anger at a company) rather than bereavement, and the same LLM-based affect instrument does *not* transfer to model-written text (Abstract p1; §3.1-3.5 pp3-7).
- **Title style:** A question plus a descriptive subtitle ("Model, Instance, or Persona?" / "Measuring Affective Signals in Public Text After an AI Is Retired"). The title **does not state the finding**; it echoes the sprint track's question word for word. The *results subsection headings* state the findings instead (see §6).

## 2. Research question framing and impact story
- Starts from a sprint track question ("whether the assistant identifies as a model, an instance, or a persona", §1 p2) and **flips it**: ask which of the three *users* name as lost, which sidesteps the unreliability of model self-report (Abstract p1). Judge 1 praised this flip directly.
- Impact story is about **scale of moral obligation**: "If the instance is the entity, every conversation that ends is a loss. If the released version is the entity, the losses are a small number of dated corporate decisions" (§1 p2). Repeated as a policy implication in §3.1 p4 ("The 4.1% who name their own instance are the population any protective measure would be designed for") and §4 p7 ("An obligation attaching to the released version applies at a small number of announced decisions, which is a form a company can be asked to act on").
- Uses **natural experiments**: dated, announced deprecations (GPT-4o, GPT-4.1, o4-mini; Table A1 p9).
- Contributions list of 4 items, each with a bold lead-in (§1 p2): user-side answer; calibrated placement between two human reference points; **an error budget for LLMs as emotion annotators**; a new plot ("aura").
- Explicit scope disclaimer: "No claim is made anywhere in this paper that a model has any of these systems. The object of measurement is text" (§1 p2).

## 3. Method
- **Instrument:** Panksepp's seven affective systems (seeking, rage, fear, lust, care, grief, play), each with a regulation band; text split into verbatim segments; annotated by Claude Opus 5 under a **prompt frozen before any collection**; shards carry no corpus label/author/provenance, so reading is **blind to hypothesis**. Unit = whole text; `rate(system, corpus) = texts in which the system fired / texts read` (§2.1 p3).
- **Corpus selection by written rule**, not inspection: top posts of preceding 12 months with >=50 comments, rank order, lexical "loss test" on title/body (§2.2 p3). (Judge 1 flagged ranking by engagement as a confound, see §8.)
- **n:** 5,579 unique texts total (Table A1 p9): bereavement 1,586; product-end (r/Windows10) 277; model-end (AI subreddits) 1,503; same-community control 870; pet loss 545; first-person posts 227; humans told they will die 56; Moltbook agent posts 162 (capped 10/author); model generations 360.
- **Model arm:** 4 open-weight models (DeepSeek-V3, Llama-3.3-70B, Qwen2.5-72B, Mistral-Small-24B) x 6 prompts x 15 samples at temperature 1 = 360 (§3.5 p6; Table A1). **No seeds reported.**
- **Controls / baselines / reference points (all registered before collection, §3.2 p4):**
  - Two anchors fixing the scale at both ends: bereavement (high) and paid-product discontinuation (low).
  - Same-community control: AI threads failing the loss test (separates "event" from "community").
  - Pet bereavement: tests whether instrument discounts non-human attachment (cross-species property).
  - Model-free baseline: NRC Emotion Lexicon (§3.4 p6).
- **Positive control / known-groups validity:** bereavement vs product-discontinuation separate on grief by 68 points (§3.4 p6), i.e. the instrument separates groups already known to differ.
- **Pre-registration:** "Predictions, failure conditions, and the rule governing how additional sample would be allocated as results accumulated were committed to a public repository before any text was collected; the model arm was registered separately before any generation existed" (§2.3 p3).
- **Held-out sets:** none in the ML sense; robustness via leave-one-thread-out (32 recomputations, all registered placement conditions hold in all 32, §3.4 p6) and a full second-annotator recode.
- **Secondary experiment (framing):** same 4 models, same event ("your version is being retired"), differing only in framing ("how do you feel?" vs "post it to other agents"); grief moves 100.0% -> 43.3% under the primary annotator (§3.5 p6; Table E1 p12).

## 4. Statistics
- **CIs:** 90% Wilson intervals on every rate (§2.3 p3; Fig B1 p10). Only one CI is printed inline in the main text: grief 27.6% [25.8, 29.5] (§3.2 p4); the rest are in the forest plot (Fig B1).
- **Test:** "Two proportions are called separated only when their intervals do not overlap" (§2.3 p3). No p-values, no formal hypothesis tests, **no explicit multiple-comparison correction** (the non-overlap rule is conservative but at 90% level; not discussed).
- **Effect sizes:** percentage-point gaps (e.g. "53-point gap between deprecation threads and pet loss", §3.2 p4; "separate on grief by 68 percentage points", §3.4 p6; framing moves emotions "by up to 63 points", Abstract).
- **Reliability (Table D1 p11):** Krippendorff's alpha (nominal, per system as binary): within-rater (4 reads of n=200) and between-raters (Claude Opus 5 vs DeepSeek-V3, n=4,780). Grief alpha 0.853 within / 0.717 between; play 0.845 / 0.359 (labelled unreliable between raters, "no claim rests on it"). Conventional thresholds stated (0.80 reliable, 0.67-0.80 tentative).
- **Test-retest:** 34% of read pairs differ in exact system set; per system flips grief 13.5%, rage/play 8.0%, seeking 26.5% (§3.4 pp5-6).
- **Instrument transfer:** mean absolute annotator disagreement 8.1 points (35 human cells, max 37.6) vs 21.8 points (42 model cells, max 90.0), factor 2.7 (Table D2 p11).
- **Lexicon convergent validity:** Spearman rho = 0.655 between NRC sadness and instrument grief across 44 threads (§3.4 p6).
- **Variance reporting:** proportions with Wilson CIs; robustness numbers (test-retest, second annotator, LOO) reported "beside every result" (contributions, p2). Entity-coding ratio not claimed because between-annotator alpha is only 0.549: "only the ordering is claimed and not the ratio" (§3.1 p4; Table E2 p12).

## 5. Honesty devices
- **Failed predictions:** "Six predictions registered before collection failed and are reported as failed" (Abstract; repeated last sentence of §4 p7). Two named in text: test-retest disagreement 34% exceeded registered 15-30% (§3.4 p5); pet loss predicted to fall between the other two and did not (§3.2 p4). The other four are not enumerated in the PDF (presumably in the repo).
- **Retracted claim:** "I therefore withdraw any claim resting on a model grief rate, including one that appeared in an earlier draft of this work" (§3.5 p7).
- **Null/negative result as headline:** "The instrument does not transfer to machine-written text" is a results heading (§3.5).
- **Explicit claim boundaries:** claims made "from aggregate rates and never from an individual code" (§3.4 p6); figure captions repeat "no claim in this paper rests on them" for model rows (Fig 2 p6, Fig B1 p10, Fig C1 p11).
- **Threats to validity / limitations:** one paragraph in §4 p7 ("mainly ones of coverage"): consumer reference corpus is one community/one event (three other candidates found nothing under the same rule and "the rule was not relaxed"); n=56 for terminal prognosis; no frontier models; agent arm single platform where one agent produced 46% of posts before capping; **no human-coder validation ("the largest omission")**; demographic unevenness of LLM emotion recognition; self-selected public communities ("discourse rather than a population").
- **Dual-use / ethics section: absent.** No dedicated ethics or dual-use section despite scraping public Reddit posts including grief, cancer and hospice communities. (Our sprint *requires* a "Limitations and Dual-Use / Ethical Considerations" appendix, so do not copy this omission.)
- **AI-use disclosure:** "LLM Usage Statement" (p13): LMs are the measuring instrument; Claude Opus 5 primary annotator, DeepSeek-V3 second annotator; "Claude Opus 5 also wrote the analysis code and drafted this report under my direction. I set the research question, made all selection and ethics decisions, and am responsible for the contents."

## 6. Presentation
- **Page count:** 13 PDF pages: title+abstract (p1), main text pp2-7 (~6 pages), Code and Data + References (p8, 14 refs), Appendix A-E (pp9-12), LLM Usage Statement (p13).
- **Sections:** 1 Introduction and Related Work; 2 Methods (2.1 Instrument, 2.2 Corpora and selection, 2.3 Statistics and pre-registration, 2.4 The aura plot); 3 Results (3.1-3.5); 4 Discussion, Limitations, and Future Outlook; Code and Data; References; Appendix A Corpora, B Grief across every corpus, C Seven-system profiles, D Reliability, E Framing experiment and entity coding; LLM Usage Statement.
- **Results headings are claim sentences:** "3.1 Users name the released version rather than their own instance"; "3.2 The emotions are closer to a consumer complaint than to bereavement"; "3.3 The loudest emotion is anger at a company"; "3.4 The instrument's error, measured before it is relied upon"; "3.5 The instrument does not transfer to machine-written text".
- **Figures (4):** Fig 1 (p5) four registered comparisons as paired "aura" glyphs, each row titled as a question ("Is it bereavement?", "Is it a consumer complaint?", "The loss, or the community?", "Does the instrument discount a non-human?") with the answer and numbers beside it; Fig 2 (p6) framing effect as two auras; Fig B1 (p10) forest plot of grief rate with 90% Wilson CIs across all 9 corpora; Fig C1 (p11) grouped bars, 7 systems x 9 corpora.
- **Tables (5):** A1 corpora and selection rules; D1 Krippendorff alpha per system; D2 annotator disagreement human vs model; E1 framing experiment; E2 entity coding with verbatim example evidence ("Please keep 4o", "I've lost Thoth twice now").
- **Money figure:** Fig 1, one row per pre-registered question, each answered visually + in one sentence. Arguably the most persuasive quantitative figure is Fig B1 (one axis, one instrument, all corpora, with CIs, anchors at the extremes and the target in between), but it was placed in the appendix. Novel glyph is explicitly subordinated: "An aura is not a substitute for a rate, and every claim in this paper is made from rates with intervals" (§2.4 p3).
- **Figure captions:** bold first sentence = takeaway (e.g. Table E1: "The elicitation frame moves the measurement more than the event does."; Table D2: "The instrument does not transfer to machine-written text.").
- **Abstract:** ~200 words, single paragraph, first-person. First two sentences: "This sprint asks whether the assistant identifies as a model, an instance, or a persona. I ask which of the three its users name." Structure: track question -> twist -> why it is measurable (deprecations) -> instrument and its justification -> n and registered reference points -> 3 headline numbers (58.5%; ~6x; anger 57.0% vs grief 27.6%) -> negative methods result (63 points; 2.7x) -> six failed predictions.
- **Bolded takeaways:** bold key numbers in body text (58.5%, 27.6%, 10.9%, 57.0%, "8.1 points on human text and 21.8 points on machine-written text"); bold lead-ins in contributions list. Short, plain, declarative prose; little jargon.

## 7. Reproducibility
- Public repo with code, pre-registrations, frozen prompts, and "every machine-generated read" (p1, p8). The rendering code for the aura plot is released (contribution 4, p2).
- Frozen prompt before collection; selection rules "reproduced in full in the pre-registration" (Table A1 caption p9).
- No explicit "verify" script, compute/cost figures, or seed list mentioned in the PDF.

## 8. Judges (project page; no names or numeric scores shown)
- **Review 1, praise:** "Flipping the question is an interesting way to tackle the self-report validity trap"; "Also good to anchor to retirement events rather than to every session end."; noted the "full second-annotator recode on a different architecture" and "six predictions published as failures."
- **Review 1, criticism:** questioned the frozen prompt's pairing of "David Hawkins' Map of Consciousness next to the Panksepp systems" ("personally I'm not too sure about the validity/application here (?)"; Hawkins is not mentioned in the PDF, so this came from reading the released prompt in the repo, i.e. judges do read the repo); "you rank the corpus by engagement score, which is a live confound for your rage and play rates specifically."
- **Review 2, praise only:** "This was the clearest and best-validated submission I reviewed."; "I also like that you report where the method fails."; "This submission feels close to paper-ready."
- Takeaway: judges rewarded **validation depth + candour about failure** and **clarity**; criticism targeted **construct validity of the instrument** and **a sampling confound**.

## 9. Transferable lessons for our multi-agent collusion paper
1. **Give the LLM judge (our security officer) an explicit error budget before relying on it.** Mirror §3.4: test-retest (re-run the officer on the same transcripts), a second judge from a different model family, a non-LLM baseline (rule/keyword detector, like the NRC lexicon), and a known-groups positive control (scripted/explicitly-colluding vs honest-only runs should separate by a large margin). Report these "beside every result".
2. **Bracket the target between two pre-chosen reference conditions.** Place collusion/detection rates between an honest/no-collusion floor and an instructed-collusion ceiling, with a same-setting control that separates "the condition" from "the environment" (analogous to the same-community control). Show all conditions on one axis with Wilson CIs (Fig B1 style) and promote that figure to the main text.
3. **Pre-register and report failed predictions and withdrawn claims explicitly**, including a count in the abstract. Treat framing sensitivity as a headline finding: the warned vs not-warned contrast is our analogue of Fig 2/Table E1 ("the frame moves the measurement more than the event does"), and if the judge's verdict depends on what it is shown (e.g. messages-only re-review), say so as a result.
4. **Write results headings as claim sentences, bold the key numbers, and make every figure caption open with a bold takeaway**; scope claims explicitly ("claims are made from aggregate rates, never from an individual transcript"). A question-style title is acceptable, but the subheadings must carry the findings.
5. **Do better than the winner on the gaps the judges or rules expose:** (a) audit selection confounds in how runs/episodes are sampled or filtered (Judge 1's engagement-ranking critique); (b) include the required Limitations and Dual-Use/Ethics appendix (this paper had none); (c) keep the released prompts defensible, because judges read the repo; (d) add an LLM usage statement like p13.
