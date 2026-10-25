# Winner 10: ColDron (Global South AI Safety Hackathon, Jun 2026, LatAm regional winner)

Source: `submission/reference/winners/globalsouth-latam-coldron.pdf` (14 pages, read in full, written in Spanish). Judges' reviews: https://apartresearch.com/project/coldron-lj2w (3 public reviews with no names and no scores shown; the page lists no prize, so the "regional winner" label comes from our reference folder). Authors: Leonardo Párraga, Angie Giraldo, Víctor Gelves (AI Safety Colombia), with Apart Research. Code: github.com/manueloff14/coldrone (p.10).

Note: this is a **policy and governance paper built on a small empirical dataset**, not an ML experiment. Most of the statistics and controls checklist is therefore missing, and that absence is a finding too. It won on originality, relevance and actionable artifacts, not on rigour.

---

## 1. Core claim and title
- **Core claim, one sentence:** Every documented drone attack by illegal armed groups in Colombia (ColDron dataset) is still remotely piloted by a human. That leaves a "prevention window" for setting human-control rules before autonomy arrives. The paper provides tools to use that window: the dataset, the LIMAA machine-readable weapon-autonomy manifest, the NRCH risk tiering and an 8-clause protocol. (Abstract p.1; Results §4 p.5.)
- **Title style:** "Gobernar el uso de drones hoy, las armas autónomas mañana" ("Govern drone use today, autonomous weapons tomorrow"), with the subtitle "Regulación sobre el control humano de sistemas letales en el conflicto colombiano" (p.1). A second title-like heading follows: "Gobernanza de IA Militar mediante Control Humano por Diseño: el marco LIMAA–NRCH" (p.1).
  - The title is a **call to action / thesis slogan**. It states the policy argument (act now, before autonomy) but **not the empirical finding** (100% human-operated). The finding first appears in the abstract.
  - The report is branded: a ColDron logo appears on every page header.

## 2. Research question and impact story
- **Framing as one question:** "¿quién elige el blanco y aprieta el gatillo?" (who picks the target and pulls the trigger?). The authors say this question decides meaningful human control and accountability (Abstract p.1; §1 p.2).
- **Counter-intuitive twist (strong hook):** autonomy will not enter the Colombian conflict first through the illegal groups. It will enter through the **State's response**: a ~US$1,668M national counter-drone shield (in pre-contract phase) that can neutralise targets automatically, plus possible AI targeting (§1 p.2).
- **Urgency from a precedent timeline:** in Ukraine/Russia, loitering munitions arrived about 7 months after the invasion, mass FPV at about 12–18 months, and AI-assisted autonomy at about 2–3 years. Fig. 1 argues Colombia is on the same curve about 2 years behind (p.2). "Prevention window" is the repeated, bolded slogan (pp.1, 2, 5, 8, 10).
- **Gap claim:** "Hasta donde sabemos, ningún esfuerzo conocido aplica el instrumental técnico de la seguridad de la IA a las armas autónomas letales (SAAL) desde un conflicto del Sur Global" ("to our knowledge, no known effort applies AI-safety technical tooling to lethal autonomous weapons from a Global South conflict", §2 p.3). The paper carries an AI-safety idea (the "bill of materials") into a new domain.
- **Stakes made concrete:** civilian harm figures (Fig. 3), Colombia's "falsos positivos" history (6,402 civilians killed under body-count pressure, a precedent for metric pressure becoming harm, §5 p.8), and Haiti (1,243 killed by drones) as the "cost of not acting" (§5 p.8; App. B p.13).
- **Named adoption path:** the Ministry of Defence, Congress and the Defensoría del Pueblo, tied to an existing national AI policy (CONPES 4144) (§5 "Ruta de adopción" p.8). Table 1 maps each existing instrument (DoD 3000.09, EU AI Act, 2023 Political Declaration, the two-tier CCW approach, Article 36) to what LIMAA/NRCH adds (p.9).

## 3. Method
- **Setup:** an incident dataset hand-coded from public sources: national and local press, Ministry of Defence reports, and UN/OCHA and ICRC releases. Each incident gets 34 fields: date, coordinates, perpetrator, target class, victims (civil/military, dead/wounded) and the LIMAA autonomy fields (§3 p.4).
- **Conservative coding rule:** when sources disagree, the most cautious category is assigned and the case goes to a review queue (§3 p.4).
- **Source verification, 3 steps:** (i) triangulation, with at least two independent sources per incident; (ii) a credibility hierarchy (agencies and official sources above national press, national press above local press and social media); (iii) magnitude and trend anchored to OCHA/ICRC/MinDefensa aggregates, not press (§3 p.4).
- **n:** inconsistent across the paper. The abstract says 42 attacks (p.1). The contributions list says 39 incidents (p.3). The results say 39 incidents of which 32 are confirmed attacks plus one failed attack (p.5). The Fig. 2 title says 33 confirmed attacks and its caption says 32 (p.5). Kappa is computed over 34 incidents in Methods (p.4) but over 33 in Limitations (p.9). The interactive map georeferences 34 attacks (p.10).
- **Models / seeds:** none. No ML models are evaluated. Claude Opus 4.8 is disclosed only as a writing and coding assistant (p.14).
- **Controls / baselines / positive control:** there is **no empirical positive control**. The closest substitute is **four constructed example manifests**, one per tier T0–T3 (anti-drone without safeguards → T0; loitering munition → T1; anti-drone with safeguards → T2; illegal FPV drone → T3) (App. A pp.12–13). The T0→T2 pair (rows 1 vs 3) acts as a **minimal-pair contrast**: the same autonomous system drops from "prohibited" to "moderate" when it has a non-lethal effector or geofence, human override and traceability (p.13).
- **Schema validation:** the LIMAA JSON Schema (draft 2020-12) validates against the standard meta-schema, and all 4 example manifests validate against it (§4 p.7; App. A p.12).
- **Pre-registration / held-out sets:** none.
- **Reliability:** two investigators coded independently. Cohen's κ = 0.70 with simple agreement 79%, labelled "substantial" on the Landis & Koch scale (§3 p.4). Limitations adds that the 7 disagreements cluster in borderline mixed/civil and mixed/military cases (p.9). Our arithmetic: (33 − 7)/33 = 78.8%, which matches the 79%.

## 4. Statistics
- **No CIs, no hypothesis tests, no multiple-comparison handling, no variance reporting.** The headline "100%" has no interval. For context, with n = 32–39 and zero autonomous cases, a rule-of-three bound would put the 95% upper bound on the autonomous rate near 8–9%. **The paper does not report this; it is our own illustrative arithmetic.**
- **The only inferential-style statistic is κ = 0.70 plus raw agreement.** It is interpreted with a named scale and its disagreements are broken down by where they occur (pp.4, 9). Reviewer 3 singled this out for praise.
- **Effect sizes are descriptive percentages taken from official sources:**
  - IED incidents (drones included) rose from 167 (2024) to 414 (2025). The figure labels this +148%: 414/167 − 1 = 1.479.
  - Civilian explosive casualties rose 145%.
  - Casualties from dropped munitions rose 342%.
  - 3 in 4 explosive victims were civilians.
  - Source for all four: Fig. 3 p.6.
- **Pace statistic** (Fig. 4 p.6): one drone attack every ~28 h and 3 dropped munitions per 2 days, cited from a press-reported intelligence document [16].
- **Internal-consistency errors that judges caught:**
  - The text says civil 12 and military 11. The Fig. 2 pie shows Civil 11, Militar 9, Infraestructura 6, Mixto 6, which sums to 32 (p.5).
  - The pie's percentages (34/28/19/19) are consistent with 32, not with 33.

## 5. Honesty devices
- **Null-like headline used constructively.** "Every case is T3, no autonomy" is the main finding, and they frame it as good news (the window is open). In Limitations they also admit it makes the NRCH tiering **degenerate** on real data (p.9): "impide demostrar la discriminación del esquema con datos reales (la demostramos con manifiestos de ejemplo)" ("it prevents showing the scheme's discrimination on real data; we show it with example manifests").
- **"Una salvedad honesta" (an honest caveat), labelled as such** (p.5). Clandestine drone schools training AI-assisted swarms suggest the frontier is getting closer. The authors separate swarm coordination from autonomy in target selection, which is what ColDron measures.
- **Limitations subsection** (§5 p.9 to p.10) covers:
  - press-coverage **selection bias**, concentrated in 2025, so the dataset cannot support a temporal trend on its own; this is why magnitude is anchored in official data;
  - the degenerate tiering;
  - κ only "substantial", with the disagreements located;
  - per-incident uncertainty in victim counts;
  - political analysis that is prospective and based on declared positions ("Es un análisis de riesgo sobre posturas declaradas, no una predicción", "a risk analysis of declared positions, not a prediction", p.8).
- **Under-reporting finding:** most press-documented civilian-victim attacks are missing from official civilian counts (p.6). The dataset is used to audit official statistics.
- **Failed predictions / pre-registered hypotheses:** none.
- **Dual-use / ethics section:** none, even though the topic is weapons. The ethics stance is implicit in the policy appendix.
- **AI-use disclosure:** yes. A separate final page, "Declaración de uso de LLM", says Claude Opus 4.8 helped with research and source verification, structuring, figures, and the LIMAA schema and tiering code; "all claims, figures and results were independently verified by the team" (p.14). **The "independently verified" claim is undercut by the count inconsistencies.**
- **Authorship-originality statements:** LIMAA is stated twice to be "creación original de este trabajo" ("an original creation of this work", pp.4, 12).

## 6. Presentation
- **Page count:** 14 pages total:
  - pp.1–10: body (abstract, intro, related work, methods, results, discussion with limitations, conclusion, code and data, contributions);
  - pp.10–12: references (28 references);
  - pp.12–13: Appendix A (LIMAA spec plus tiering demo) and Appendix B (policy brief);
  - p.14: LLM-use declaration.
- **Section list:**
  - Resumen
  - 1 Introducción, ending with a 3-bullet contributions list
  - 2 Trabajo relacionado
  - 3 Métodos: ColDron; Verificación de fuentes; LIMAA; NRCH; Protocolo
  - 4 Resultados
  - 5 Discusión y limitaciones: Ruta de adopción; Limitaciones; Trabajo futuro
  - 6 Conclusión, which is **cut off mid-sentence**: "...como Haití y" (p.10). Reviewer 2 flagged this.
  - Código y datos
  - Contribuciones de los autores
  - Referencias
  - Apéndice A: LIMAA spec and tiering demo
  - Apéndice B: Resumen de política, a one-page brief for decision makers with "the problem in one sentence", "the opportunity", "four immediate actions" and "the cost of not acting"
  - Declaración de uso de LLM
- **Figures (5) and tables (2):**
  - Fig 1: dual timeline comparing Ukraine/Russia with Colombia, with a shaded "prevention window" (p.2). This is the conceptual figure.
  - Fig 2: pie chart of attacks by target class (p.5).
  - Fig 3: 2024 vs 2025 bar chart with three large-number callouts, +145%, +342% and "3 de 4" (p.6).
  - Fig 4: attack-rhythm timeline with big "1" and "3" numbers (p.6).
  - Fig 5: the LIMAA–NRCH decision-tree flowchart, three yes/no questions leading to tiers T0–T3 (p.7).
  - Table 1: existing instruments, what each covers, and what LIMAA/NRCH adds (p.9).
  - Appendix table: 4 example manifests and their tiers (p.13).
- **Money figure:** a tie between **Fig. 5** (the decision tree, the paper's usable artifact; "tres preguntas … bastan para clasificar cualquier sistema", "three questions are enough to classify any system", p.7) and **Fig. 1** (the "prevention window" timeline that carries the urgency argument). Fig. 2's pie is the only one built from their own data, and it contains the count error.
- **Abstract structure:** context of harm → one decisive question → finding (100% human-operated, n = 42) → twist (the State is the autonomy vector) → precedent (Ukraine, Russia, Iran) → "ventana de prevención" → three named contributions → cross-cutting contribution (AI-safety tools carried to lethal autonomous weapons, from a country where the harm is real).
  - It runs about 230 words and is a single paragraph.
  - **First two sentences, quoted:** "En Colombia, los grupos armados ilegales ya atacan con drones comerciales modificados y ya han herido y matado a civiles. Una pregunta decide cómo gobernar esta amenaza: ¿quién elige el blanco y aprieta el gatillo?" ("In Colombia, illegal armed groups already attack with modified commercial drones and have already wounded and killed civilians. One question decides how to govern this threat: who picks the target and pulls the trigger?")
- **Bolded takeaways are used heavily:**
  - Each results paragraph opens with a bolded claim sentence: "ColDron: el daño es real y aún no hay autonomía." (the harm is real and there is no autonomy yet); "LIMAA/NRCH discrimina y es reproducible." (discriminates and is reproducible) (pp.5, 7).
  - Each discussion paragraph opens with a bolded thesis: "La presión por resultados es un multiplicador de daño civil…" (pressure for results multiplies civilian harm); "Un fenómeno del Sur Global, no del Norte." (a Global South phenomenon, not a Northern one) (p.8).
  - Key phrases inside paragraphs are bolded too ("ventana de prevención", "el 100% de los ataques son operados remotamente").
- **Narrative devices:** a single recurring slogan; a vivid, concrete intro question; source lines printed under the figures (Fig. 3, Fig. 4); a policy brief aimed at named institutions.

## 7. Reproducibility
- **Code release:** GitHub repo containing:
  - the `wabom.schema`;
  - the example manifests;
  - the reference tiering implementation `./framework/hcrt_tier.py`;
  - the dataset `./public/coldron_seed.csv` under an open licence;
  - a live interactive map at coldrone.onrender.com.
  - Source: "Código y datos", p.10.
- **Verify scripts:** schema meta-validation, plus validation of the 4 example manifests against the schema (pp.7, 12). There is no test that reproduces the paper's numbers from the CSV.
- **Frozen protocols:** the coding protocol (conservative coding, 3-step verification, review queue) is described but not versioned or frozen. Neither the codebook nor the κ computation script is cited.
- **Gap:** the paper's numbers (42, 39, 34, 33, 32) disagree with each other. A single script that generates every count would have prevented the main criticism.

## 8. Judges' praise and criticism (apartresearch.com/project/coldron-lj2w)
**Praised:**
- Originality: "the most original submission here, and the move is genuinely new" (R3).
- Relevance to an understudied area: "Very good and relevant article in an area that is extremely understudied from the perspective of AI Safety" (R1).
- Evidence base: "Excellent evidence base of current drone use in Colombia" (R1).
- Actionability: "making the article actionable, which is very valuable" (R1).
- Recognising the Global South/North difference (R1).
- A "brave and well-researched stance" (R1).
- **Real, checkable artifacts:** "an open dataset with a JSON Schema that validates against the draft-2020-12 meta-schema", plus "a reference tiering implementation" (R3).
- Magnitude "anchored in OCHA, ICRC and Defence-Ministry figures rather than press" (R3).
- **"an inter-coder κ of 0.70 actually computed and honestly dissected"** (R3).
- The 100% T3 result "correctly interpreted as evidence that the prevention window remains open", and the political section "appropriately framed as a risk analysis based on declared positions" (R2).

**Criticised:**
- **Inconsistent n:** "the count appears as 42 in the abstract, 39 in the contributions, 32-plus-one in the results" (R3).
- **Figure/text mismatch:** "the civilian tally is 12 in text but 11 in Figure 2" (R3).
- **Classifier never discriminates on real data:** "every real case is T3, so NRCH's discrimination is shown only on four illustrative manifests" (R3). "LIMAA's tiering capability is demonstrated only on constructed examples" (R2).
- **Protocol untested:** "it is not tested against any real operational scenario" (R2). Testing it "would transform the protocol from a normative proposal into an empirically grounded one" (R2).
- **Requested fix:** "Reconcile the counts to one figure and seed even a single near-autonomy case" (R3).
- **Missing data linkage:** connect to "a structured data source (like ACLED) for coverage expansion and temporal validation" (R2).
- **Incomplete conclusion:** "the conclusion appears to be cut off mid-sentence" (R2).
- **Domain gaps:** add "decision support systems", Gaza examples, IHL experts and victims' perspectives (R1). R1 also asks for incentive mechanisms such as "procurement conditionality from arms exporters" (R2) and asks the authors to clarify "the problem is not AI but its use" (R1).

## 9. Transferable lessons for our multi-agent collusion paper
1. **Make one generated source of truth for every number.** The most damaging criticism here was not methodological. It was 42 vs 39 vs 33 vs 32 and 12 vs 11, which is exactly what a careful judge checks first. Generate all headline counts, the abstract numbers and the figure labels from one script over `results/*.jsonl`, and cross-check text against figures before submitting. Also make sure the conclusion is not truncated.
2. **Show that the detector discriminates on cases where the true answer is known, or seed one.** ColDron's tiering was "degenerate" on real data (all T3), and two of three judges hit this. For us, a security officer or collusion detector must be shown firing on a **positive control**, meaning runs with known or instructed collusion, and staying quiet on a negative control. A "0% detected" or "100% clean" headline needs a demonstration that the instrument could have said otherwise. A minimal-pair contrast like their T0→T2 is a cheap version of this.
3. **Report a reliability statistic and dissect it.** κ = 0.70, with the location of the 7 disagreements, won explicit praise ("actually computed and honestly dissected"). If we use LLM or human labels for collusion, report agreement (κ or similar) between labelers, or between the officer and the ground truth, and say where they disagree.
4. **Turn a null or "nothing yet" result into a framed finding.** "No autonomy yet, so the prevention window is open" made a null into the core contribution. If collusion is rare or weak in our pilot (for example warned vs not warned), frame it as what it means for monitoring now, and state the bounds honestly. Add the CI or rule-of-three bound that ColDron omitted.
5. **Ship a usable artifact plus a one-page brief, and keep one recurring slogan.** The judges rewarded:
   - a concrete schema and reference implementation;
   - a decision-tree figure ("three questions classify any system");
   - a policy appendix naming who should act;
   - a single repeated phrase ("ventana de prevención") carrying the argument.

   For us, lead each section with a bolded claim sentence and give the leaderboard or eval as a reusable tool. Also add the **Limitations and Dual-Use** appendix the Apart template requires, which ColDron lacked (it only had Limitations and an LLM-use statement). Keep the LLM-use disclosure as a separate short section.
