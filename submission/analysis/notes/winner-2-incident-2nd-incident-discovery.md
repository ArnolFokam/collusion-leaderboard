# Winner study 2: "Strengthening International AI Incident Discovery" (AI Incident Response Sprint, Sep 2026, 2nd place)

Source: `submission/reference/winners/incident-2nd-incident-discovery.pdf` (14 pages, read in full). Authors: Omer Bilgin (The Future Society), Aydin Yigit Alfatli (Independent), Ipek Cerrahoglu (Istanbul Bilgi University), "With Apart Research". Project page with reviews: https://apartresearch.com/sprints/projects/strengthening-international-ai-incident-discovery-d0t9. The page shows no placement, prize, numeric scores or reviewer names. The 2nd-place label comes from our own file naming.

Type of paper: a qualitative policy and legal document analysis. It has no experiments and no models. The lessons that carry over to us are about framing, structure and honesty, not statistics.

## 1. Core claim and title
- **Core claim (one sentence):** None of the six mandatory AI incident-reporting regimes in force or enacted (EU, California, New York, Illinois, South Korea, Vietnam) clearly required a report for the summer-2026 loss-of-control incidents. The reasons are crisis-level thresholds, triggers that need harm to have happened, carve-outs for evaluations, and no near-miss duty (Abstract, p.1; Sec. 4 finding 1, p.4).
- **Title style:** the title names a topic and an aim ("Strengthening International AI Incident Discovery"). It does **not** state the finding. The finding appears only in the abstract and conclusion. So a title that states the result is not needed to place 2nd, but this title does give away the paper's strongest line ("none clearly compel a report").

## 2. Research question and why it matters
- **Question** (Sec. 2, last paragraph, p.3): "test the triggers that are already written into binding law against real incidents, and ask whether a duty to report would in fact have arisen". Contribution 1 is a trigger analysis across every mandatory regime. Contribution 2 is recommendations for each stakeholder group.
- **Framing device:** a four-rung "escalation ladder" of **Hazards -> Near misses -> Incidents -> Crises**, with definitions taken from OECD, CSET and The Future Society (Sec. 1, p.2, footnote 2). The whole argument hangs on this one picture: the summer incidents sit at the near-miss or incident rung, while the laws trigger only at the crisis rung.
- **Impact story** (Sec. 1, p.2): "Waiting for empirical proof of danger means waiting for people or property to be harmed ... the same failure in more capable systems is autonomous cyber operations, CBRN uplift, critical-infrastructure disruption." The paper hooks onto very recent real events (OpenAI/Hugging Face, DseWiki, RubyGems, Anthropic, Meta, UK AISI incidents, p.1). That timeliness is a large part of its pull.
- **Gap statement:** Related work (Sec. 2, pp.2-3) is a bulleted list of five strands (TFS, Wei & Heim, OECD, CSET, incident databases). It ends with "What none of these works do is ..." and so gives a crisp novelty claim.

## 3. Method
- **Setup** (Sec. 3, p.3): "qualitative document analysis of primary legal sources, combined with a counterfactual application of each source to recently documented events."
- **Corpus / n:** 6 jurisdictions. Inclusion rule: a mandatory duty that is in force or adopted with a fixed start date. **Proposed bills are excluded**, which is a stated exclusion criterion. The Korean and Vietnamese texts were read in English translation.
- **Coding scheme:** 15 fields per regime. Five of them carry the argument: qualifying event, severity threshold, harm vs risk, coverage of the pre-deployment stage, and what starts the reporting clock. Every cell records instrument, article and page (p.3). The Data section (p.11) adds "per-cell confidence ratings" in an external tracker.
- **Decision rule:** a practical counterfactual. "Would a competent lawyer advising the developer have concluded that a report was legally required?" There are three verdicts: Yes / Contestable / No (p.3). The middle "Contestable" category is itself an honesty device (see Sec. 5).
- **Ground truth / "positive control" analogue:** they check verdicts against what actually happened. California's OES stated on the record that SB 53 was not triggered, and OpenAI did report to the EU "without conceding" that Article 55 applied (Sec. 4 finding 1, p.4). Real-world agencies' behaviour serves as external validation of the coding.
- **Not present:** no seeds, no baselines, no held-out set, no pre-registration, no inter-coder reliability. Three authors took part, but Author Contributions (p.11) say one person (A.Y.A.) did the coding. No second coder is reported.

## 4. Statistics
- None. There are no CIs, tests or effect sizes. The quantitative content is counts (verdicts 1 Contestable/5 No in Table 1) and the statutory thresholds themselves (">50 deaths or serious injuries, or >$1 billion", p.4; NY 100 people, p.10).
- **Variance / uncertainty** is handled qualitatively: the three-level verdict, "Contestable, but probably yes" for the EU (Table 1, p.4), and per-cell confidence ratings in the tracker (p.11).
- **Internal inconsistencies (judges did not flag them, but we should avoid them):**
  - Table 1 (p.4) gives New York the verdict **No**, but Appendix A (p.10) gives New York **Contestable**. Finding 1 says "One is contestable and five are clear negatives", which matches the table and not the appendix.
  - Discussion (Sec. 5, p.5) says "Three min[or] upshots follow" and then lists four.
  - The abstract says "four stakeholder groups", but Sec. 6 has three subsections (6.1 Governments, 6.2 Companies, 6.3 Funders/Research/Civil Society).
  - The section numbers skip 7 (6 Recommendations -> 8 Future Work, p.8). The reference numbers run out of order (29-47, then 53-59, then 48-52, pp.12-13).
  - Appendix A's Illinois row and New York row both end "Applies from 1 January 2027". Illinois' text break across pp.9-10 makes the row hard to follow.

## 5. Honesty devices
- **Graded verdicts** ("Contestable") in place of a forced binary. The limitations section justifies this explicitly (p.10).
- **Appendix B. Limitations** (pp.10-11) has three bolded paragraphs:
  1. *Legal interpretation and interpretive uncertainty*: "A competent lawyer could reach the opposite conclusion on any entry we mark Contestable", and "The fifteen fields ... are choices we made about what matters in a trigger. A different framing could produce different verdicts on the same texts."
  2. *Exclusion of future legislation*.
  3. *Underlying policy assumptions*: they name two untested premises, that (a) lower-tier reporting gives signal rather than noise and (b) receive-only sharing channels work.
- **Future Work** (Sec. 8, pp.8-9) admits the limits of a sprint: "a research sprint cannot place that argument in front of the people who would have to act on it".
- **LLM Usage Statement** (p.14), a full paragraph: Claude was used for ideation and for testing arguments against legal texts, for structuring and filling the comparison entries ("each of which was subsequently checked against the initial findings and the primary sources"), for generating the tables "from the verified underlying data", and for polishing wording and references.
- **Author Contributions** (p.11) give a per-person breakdown.
- **No failed predictions and no null results**, apart from the headline itself, which is in effect a "null" (no duty triggered).
- **No dual-use / ethics section.** Our sprint requires a "Limitations and Dual-Use / Ethical Considerations" appendix, so we must do more than this paper did.

## 6. Presentation
- **Length:** 14 pages in total. The body is pp.1-9 (to the Conclusion). Appendix A is pp.9-10, Appendix B and the Data, Author Contributions and References sections are pp.10-13, and the LLM statement is p.14. The format is a single column, Times-like, Google-Docs style with a centred title block and an italic abstract. It does not look like the LaTeX template.
- **Sections:** Abstract; 1 Introduction; 2 Related work; 3 Methodology; 4 Findings; 5 Discussion; 6 Recommendations (6.1 Governments and Legislators, 6.2 Frontier AI Companies, 6.3 Funders, Research Orgs and Civil Society); [7 missing]; 8 Future Work; 9 Conclusion; Appendix A Reporting Regime Analysis; Appendix B Limitations; Data; Author Contributions; References (grouped: primary legal instruments / prior literature / incident record / background / repositories); LLM Usage Statement.
- **Figures: 0. Tables: 2 in the body plus 1 in the appendix.**
  - **Table 1** (pp.3-4), the **"money table"**: Jurisdiction | Verdict | Provisions, with the article cited for each verdict. Its caption is phrased as the research question: "In which jurisdictions did or would the May-September 2026 loss of control incidents need to be reported to public authorities?" The caption says it "states the outcome only" and points to Appendix A for the reasoning limb by limb.
  - **Table 2** (p.7): 7 operational "warning shot trigger events" with **denominators** (e.g. "AI systems communicate with one another through a channel their operators did not set up for them | per 1,000 test runs"). This turns the policy argument into something measurable. Row 4 is in effect a collusion-carrier trigger, which is directly relevant to us.
  - **Appendix A table** (pp.9-10): a long-form justification with operative statutory wording.
- **Abstract structure** (~129 words by my count, which is *below* our 150-250 requirement). It has four sentences: stakes, then method plus headline result, then mechanism (three defects), then recommendations. First two sentences, quoted: "Mandatory AI incident reporting exists to make dangerous events visible to regulators while there is still time to act. We coded the six such regimes in force or set to be enforced soon from primary legal texts and applied each trigger to the documented loss of control incidents of summer 2026, finding that none clearly compel a report."
- **Bolded takeaways:** used heavily. Each numbered finding in Sec. 4 opens with a bold claim sentence ("**1. No regime in the sample clearly compels a report ...**", "**3. Pre-deployment incidents are the common blind spot.**", "**4. Near-miss reporting is absent from every regime.**", pp.4-5). The Discussion opens with one bold thesis ("**they are built to react to catastrophes rather than to learn from early warning signs**", p.5). Every recommendation is a bold imperative headline followed by a paragraph. A reader can skim the bold text alone and get the whole paper.
- **Conclusion** ends with a memorable closing line: "The events of summer 2026 were the smallest version of their category ... The next one will be larger, and the thresholds will not have moved." (p.9).
- **Citation density:** inline hyperlinks throughout, and about 59 references, many of them primary sources (statutes, company posts, news). Every legal claim cites an article or section number.

## 7. Reproducibility
- **No code release** (not needed for this kind of paper). The project page lists no code or dataset links.
- **Data:** a linked "multi-jurisdiction comparison tracker" with 15 coded fields per jurisdiction, instrument/article/page citations, source lists and per-cell confidence ratings (Data section, p.11). This is the analogue of releasing the raw results.
- **Frozen protocol:** the inclusion rule (enacted only) and the verdict rule (competent-lawyer counterfactual, three levels) are stated up front in Sec. 3. There are no verification scripts.
- **"Living" extension** is proposed: re-run the counterfactual when laws take effect ("A living tracker, updated on commencement rather than on publication", p.8).

## 8. Judges' comments (project page, two anonymous public reviews, no scores shown)
- **Praised:**
  - "Paper is well written and easy to follow."
  - "Analysis appears to be mostly sound, and authors cite most relevant literature."
  - "accurately identifies some flaws in existing incident reporting regimes"
  - "Paper produces useful analysis and recommendations."
  - Review 1: "interesting analysis that supports the claim that most people agree with", "I particularly appreciate recommendation 6.3.1 (Fund the external detection layer as reporting infrastructure)", and it suggests follow-up "with grant organizations or 'applied' fellowships".
- **Criticised (all aimed at the recommendations, none at the core finding):**
  - Main point: "Recommendations are not sufficiently justified or analyzed in sufficient depth."
  - 6.1.1: "the trigger scope should plausibly be simply independent of deployment status and use case".
  - 6.1.2: "a tiered reporting system would have different reporting obligations at each tier, but this is not discussed".
  - 6.1.3: "additional incident detection/reporting within jurisdictions is needed to enable cross-border information sharing", and "we may not really be learning much from anything in other jurisdictions".
  - 6.2: "many of the recommendations seem rather generic / difficult to operationalize" (example given: "improve internal evals and sandboxing").
- Review 1's phrase "supports the claim that most people agree with" is a mild jab at novelty: the paper confirms what people already suspected and does not surprise.

## 9. Transferable lessons for our multi-agent collusion paper
1. **One question, one money table, one sharp headline.** The paper wins on a single falsifiable-sounding question ("would any binding trigger have fired?") answered in one table, with the reasoning pushed to an appendix. We should give one primary result (for example, the warned vs not-warned collusion rate, or the security officer's detection rate) in a single headline figure or table whose caption is the question. Per-condition detail goes to the appendix.
2. **Bold claim-first paragraph openers and a framework picture.** Every finding and recommendation opens with a bold one-line takeaway. The four-rung ladder gives readers a shared vocabulary. A small taxonomy for us (for example, collusion carriers: channel vs content vs coordination, or a ladder from signal to coordination to realised harm) plus bold findings would make a skim of the paper enough to grasp it. This maps directly onto the "presentation & clarity" score.
3. **Anchor to real, current events and real stakeholders.** The pull comes from testing against named 2026 incidents. Table 2 row 4 ("AI systems communicate with one another through a channel their operators did not set up for them | per 1,000 test runs") shows that judges value operational metrics with denominators. We should report collusion and detection as **rates with explicit denominators** (per episode/run, with n), and say who would use them (labs' monitoring teams, auditors).
4. **Recommendations are the weak point, so either earn them or scope them down.** Every criticism from the judges targeted under-justified, generic recommendations. Keep our countermeasure claims tied to what our data shows (for example, "messages-only security officer reduces X by Y in our setting"), and label everything else as hypothesis or future work. Avoid generic advice like "improve sandboxing".
5. **Formal honesty scaffolding is cheap and rewarded, and we should go further.** The paper uses graded verdicts, a three-part limitations appendix that names its own framing choices as threats, a per-author contributions list, a detailed LLM-usage statement and a data release. We should copy all of these. We should also add what this paper lacked and our rubric needs: CIs/seeds/n, a dual-use/ethics section, an internal consistency pass (this paper's mismatches between Table 1 and the appendix, "three" vs four, and "four" vs three groups would cost points with a careful judge), and an abstract in the 150-250 word range (theirs is about 129).
