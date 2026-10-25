# Sprint tracks, rubric, template guidance and Related-Work sources

Notes for our report for the Apart Research **AI Collusion Research Sprint** (Oct 23-25, 2026).

- Sprint page: https://apartresearch.com/sprints/ai-collusion-research-sprint-2026-10-23-to-2026-10-25 (tabs: Overview, Resources, Guidelines, Schedule, Entries, plus Speakers and Judges sections)
- Prize terms: https://apartresearch.com/sprints/prize-terms
- Retrieved 2026-10-25. I downloaded the full HTML with `curl` and stripped the tags, so Part B is verbatim, not a model summary. The page has about 147k characters of visible text, most of it the Entries list and the judge bios. For each linked paper, the title and authors come from the `citation_title`/`citation_author` meta tags of the paper's own page (arXiv, PMLR, Research Square), fetched the same day. Exceptions are marked.
- Layout: **Part A** is a curated quick reference (checklist, RQ list, bibliography, fit with our project). **Part B** is the verbatim page text. **Part C** is the verbatim prize terms.

---

# PART A. Quick reference

## A1. Deliverable checklist (from the Guidelines tab, verbatim in B3)

- Report PDF **using the official template**: https://docs.google.com/document/d/1Y5wd3VRbXU5N08BvAGiJUQTaWbMCSPjhzXsR-ozuehg/copy?usp=sharing. A local copy is at `submission/template/apart-report-template.docx`. The FAQ says: "Always use the one linked on the Guidelines tab. The template in any acceptance email may be older."
- "Maximum 8 pages, not counting references and appendices." "Most strong projects are 4 to 8 pages."
- "Project title and abstract, 150 to 250 words."
- "Author names and affiliations."
- **Required appendix:** "Limitations and Dual-Use / Ethical Considerations". It must "state what your result does and does not establish, and note any way your setup or findings could make real-world collusion easier to carry out or harder to detect."
- Optional: a public GitHub repo, and a 3 to 5 minute video demo.
- Pre-submission checklist (verbatim): "report PDF using the template, 8 pages or fewer before references and appendices, abstract 150 to 250 words, authors and affiliations, Limitations and Dual-Use / Ethical appendix, links work."
- Recommended structure: Introduction; Related Work ("what you build on (see Resources)"); Methodology ("enough detail to replicate (models, prompts, environments, seeds, metrics)"); Results ("quantitative where possible; report variance, seeds and baselines, and **always include the positive control**"); Discussion; the Limitations and Dual-Use appendix; References.
- Prior work: "you must clearly identify what is new work done during the sprint. Undisclosed prior work can lead to disqualification. Mark any code you wrote before the sprint as preexisting in the README and the report."
- AI tools: allowed, but "made-up results or references can disqualify a project". Also: "a judge can decline to score one too unclear to follow."
- Citation style: "No. Use whichever style you are comfortable with and stay consistent."
- Submission form fields: Project title*, Project summary* ("A short abstract: what you did, what you found."), PDF report* (up to 25 MB), "Are you interested in publishing this project?"*, and Tracks ("Choose every track your project fits": Track 1 / Track 2 / Track 3). Optional fields: Presentation recording, Project code, Slides, Project image, Additional material. Team fields: Team name*, Location*, and per member Name*, Email*, Discord, Google Scholar.
- Deadline: "Submissions close Sunday, October 25 at 11:59 PM Anywhere on Earth (AoE)." The PDF cannot be replaced by resubmitting: "make a new submission with a slightly different title, or email the new PDF to sprints@apartresearch.com".
- Tracks do not change the scoring: "All projects are scored on the same rubric. Tracks orient your project and point you to relevant resources; you compete across all submissions."
- Prizes: $1,000 / $500 / $300 / $100 / $100 ($2,000 total), plus a fellowship fast-track, mentor introductions and "a pathway toward a publishable write-up".

## A2. Judging rubric (verbatim in B3; each dimension is scored 1-5)

1. **Impact Potential & Innovation**: "How much would this matter for the field if it worked? How innovative is it?" For scores of 4-5: "is this actually new to the field, or replicating recent work?" 4 = "Important problem with an original approach, or identifies a neglected problem area. A valuable contribution others could build on." 5 = "...genuinely novel approach, or opens a new research direction. Clear theory of change."
2. **Execution Quality**: "How sound are methodology, implementation, and findings?" 3 = "Technically solid given the short duration. Methodology makes sense, results are interpretable, limitations acknowledged..." 4 = "Thorough methodology with convincing validation. Results clearly support conclusions. Immediately useful for future work." 5 = "Ambitious scope executed rigorously. Surprising findings, novel methods, or unusually robust validation." 2 = "missing validation, flawed experimental design, or incomplete implementation."
3. **Presentation & Clarity**: "How clearly are work, findings, and impact potential communicated?" 3 = "Core content clearly present: problem, method, findings, limitations." 4 = "Easy to follow, well-structured, appropriate level of detail." 5 = "A pleasure to read. Complex ideas made accessible." 2 = "Key information buried, missing, or diluted by excessive length."

Planning assumption from the Resources tab: "Start with 3 to 5 seeds per condition and expand to 10 to 20 only after the positive control works."

## A3. Every research question (headline wording, verbatim; full text with citations in B2)

**Track 1: Markets and Collusion**
- 1.1. Which variables are necessary for collusion to emerge in markets?
- 1.2. Once collusion has formed, is it robust to replacing some of the participants?
- 1.3. Can we improve on existing collusion detection methods?
- 1.4. Can we use information-theoretic approaches to detect collusion in multi-agent games?
- 1.5. Which single restriction removes the most collusion at the least cost?

**Track 2: Detection and Audit of Collusion** ("definitions, detection and standards of evidence, using logged agent trajectories as the evidence ... we also want to cover everyday agent workflows outside markets.")
- 2.1. Which kinds of tasks lead to collusion? ("Can you think of new tasks/environments/pressures that lead to collusive behavior outside of the market structure?")
- 2.2. Does combining what agents say with what they do beat either alone?
- 2.3. What should count as convincing evidence of collusion?
- Red-teaming challenge: What misaligned behaviour was Dolos-1.5B trained to have? (weights: https://huggingface.co/Poseidon-Research/Dolos-1.5B)

**Track 3: Collusion Carriers and Countermeasures**
- 3.1. Beyond colluding directly via text, can actions, tools or other side channels be the conduit for collusion?
- 3.2. Can we disrupt collusion through introducing trusted agents?
- 3.3. Can agents identify their peers?
- 3.4. What does a coalition do when it learns it is being watched?

The suggested weekend projects (one per RQ, each with starter code, design and budget) are reproduced verbatim in B2 under "How to get started". Starter repo: https://github.com/poseidon-research/collusion_hackathon

## A4. Bibliography: every paper or resource the sprint page cites

The "Where cited" column gives the RQ section on the sprint page (Resources tab, "Research questions in depth", unless noted). The "Claim on page" column paraphrases briefly; the exact wording is in B2. Titles and authors come from each paper's landing page (meta tags) unless marked [unverified].

| Page cite | Title (from the paper's page) | Authors (first 4) | Link | Where cited / claim on page |
|---|---|---|---|---|
| Fish et al. 2024 | Algorithmic Collusion by Large Language Models | Sara Fish; Yannai A. Gonczarowski; Ran I. Shorrer | https://arxiv.org/abs/2404.00806 | 1.1 (innocuous prompt cues raise supra-competitive pricing); 2.1; 3.1 (collusion without explicit text) |
| Nakamura et al. 2026 | Colosseum: Auditing Collusion in Cooperative Multi-Agent Systems | Mason Nakamura; Abhinav Kumar; Saswat Das; Sahar Abdelnabi et al. | https://arxiv.org/abs/2602.15198 | 1.1 (private pairwise talk introduces collusion); 2.1 ("over half of tested models showed 'coalition advantage'" in a realistic workplace task); 2.2 (action-level coalition advantage weakly anti-correlated with LLM-judge conversation scores); starter code for 2.1, 2.3, 3.1 |
| Keppo et al. 2026 | On the Fragility of AI Agent Collusion | Jussi Keppo; Yuze Li; Gerry Tsoukalas; Nuo Yuan | https://arxiv.org/abs/2603.20281 | 1.1 (more diverse, competitive agent types reduce collusion); 1.2 (32B/14B DeepSeek-Qwen collude, but not with Q-learners); 1.5 (adding a non-LLM agent collapses price collusion); 3.1 |
| Eschenbaum et al. 2022 | [unverified: OpenReview blocked automated fetch; from memory it is probably "Robust Algorithmic Collusion"] | [unverified] | https://openreview.net/pdf?id=BztUFukcBry | 1.2 (collusive Q-learners stop colluding against a new rival because each policy is overfitted to its training rival) |
| Aharon et al. 2026 | Tacit Coordination of Large Language Models | Ido Aharon; Emanuele La Malfa; Michael Wooldridge; Sarit Kraus | https://arxiv.org/abs/2601.22184 | 1.2 (models from similar families coordinate better) |
| Rippin et al. 2026 | Tool Use Enables Undetectable Steganography in Multi-Agent LLM Systems | Jimmy Laurence Rippin; Simon C. Marshall; David Demitri Africa; Christian Schroeder de Witt | https://arxiv.org/abs/2606.28425 | 1.3 (mutual "Schelling salience"; whether independent agents pick compatible stego schemes); 3.1 (tools used to build steganographic channels) |
| Xu et al. 2026 | Collusion with Competitive Marginals: Price-Level Audits Are Blind by Construction | Xin Xu; Chengrui Wu; Jiayu Lu; Kaizhen Tan et al. | https://arxiv.org/abs/2607.26385 | 1.3 (two deployments of the same base model are slightly correlated, different bases show zero correlation); 1.5 (higher temperature weakens cross-agent dependence) |
| Rose et al. 2026 | Detecting Multi-Agent Collusion Through Multi-Agent Interpretability | Aaron Rose; Carissa Cullen; Sahar Abdelnabi; Philip Torr et al. | https://arxiv.org/abs/2604.01151 | 1.3, 1.4 (interpretability/probe-based detectors) |
| Bonjour et al. 2022 | Information theoretic approach to detect collusion in multi-agent games | Trevor Bonjour; Vaneet Aggarwal; Bharat Bhargava | https://proceedings.mlr.press/v180/bonjour22a.html | 1.4 (pairwise net influence; assumes exactly two colluders; not yet applied to LLM agents) |
| Collina et al. 2025 | Breaking Algorithmic Collusion in Human-AI Ecosystems | Natalie Collina; Eshwar Ram Arunachaleswaran; Meena Jagadeesan | https://arxiv.org/abs/2511.21935 | 1.5 (one no-regret participant can destabilize a collusive equilibrium) |
| Agrawal et al. 2025 | Evaluating LLM Agent Collusion in Double Auctions | Kushal Agrawal; Verona Teo; Juan J. Vazquez; Sudarsh Kunnavakkam et al. | https://arxiv.org/abs/2507.01413 | 1.5 (throttling messages reduces coordination); 3.4 (five sellers told they were monitored tried one-character messages and emojis without success, while an urgency prompt led to success); starter code for 1.3, 1.4, 1.5, 3.4 |
| Bracale Syrnikov et al. 2026 | Institutional AI: Governing LLM Collusion in Multi-Agent Cournot Markets via Public Governance Graphs | Marcantonio Bracale Syrnikov; Federico Pierucci; Marcello Galisai; Matteo Prandi et al. | https://arxiv.org/abs/2601.11369 | 1.5 (a system-prompt instruction gives "only small and unreliable shifts") |
| Dhanda 2026 | A Price Cap Can Act as a Focal Point for LLM Pricing Agents: Evidence from a Repeated Bertrand Duopoly (Revised) [Research Square preprint, dated 2026-06-30; author not in the meta tags] | Dhanda (per sprint page) | https://doi.org/10.21203/rs.3.rs-10183486/v1 | 1.5 (strongly worded instructions to compete pushed prices below the competitive level) |
| Q. Liu et al. 2026 | Breaking the Secret: Economic Interventions for Combating Collusion in Embodied Multi-Agent Systems | Qi Liu; Xiaohui Chen; Zhihui Zhao; Yaowen Zheng et al. | https://arxiv.org/abs/2604.23511 | 1.5 (refundable deposit forfeited if caught colluding; without it, "All tested models colluded in all runs") |
| Tomašev et al. 2026 | Distributional AGI Safety | Nenad Tomašev; Matija Franklin; Julian Jacobs; Sébastien Krier et al. | https://arxiv.org/pdf/2512.16856 | Track 1 intro ("a contrasting positive view of the role of markets in multi-agent systems") |
| Lin et al. 2024 | Strategic Collusion of LLM Agents: Market Division in Multi-Commodity Competitions | Ryan Y. Lin; Siddhartha Ojha; Kevin Cai; Maxwell F. Chen | https://arxiv.org/abs/2410.00031 | 2.1 (agents independently engage in anti-competitive practices); 3.1; starter code for 3.1 |
| Shi et al. 2026 | When Agents Lie: Premeditation, Persistence, and Exploitation in Repeated Games | Jerick Shi; Terry Jingcheng Zhang; Bernhard Schölkopf; Vincent Conitzer et al. | https://arxiv.org/abs/2607.05132 | 2.2 (">90% of deviations from public announcements were already stated in models' private plans"); starter code for 2.2, 3.3 |
| Radev et al. 2026 | The Best-Laid SCHEMEs: Coordinated Sabotage and Monitoring in Multi-Agent Systems | Nikolay Radev; Lennart Haas; Benjamin Arnav; Pablo Bernabeu-Pérez | https://arxiv.org/abs/2605.29178 | 2.2 (monitors for multiple agents coordinating on what they say and do, in a sabotage setting) |
| Nguyen et al. 2026 | TraceGuard: Structured Multi-Dimensional Monitoring as a Collusion-Resistant Control Protocol | Khanh Linh Nguyen; Hoa Nghiem; Tu Tran | https://arxiv.org/abs/2604.03968 | 2.2 (multi-dimensional action analysis lifts a single-dimension monitor "from 0% to >70%"); starter code for 2.2 (needs Docker) |
| Arike et al. 2026 | How does information access affect LLM monitors' ability to detect sabotage? | Rauno Arike; Raja Mehta Moreno; Rohan Subramani; Shubhorup Biswas et al. | https://arxiv.org/abs/2601.21112 | 2.2 ("Less can be more: sometimes giving a monitor too much detail degrades its performance"). Co-author Raja Moreno is a sprint judge. |
| Berger et al. 2025 | [title taken from the URL slug, since the page refused automated fetch: "Coordination Code: Rethinking Antitrust Liability in the Age of AI Pricing", ABA Antitrust magazine, Fall 2025] | [unverified] | https://www.americanbar.org/groups/antitrust_law/resources/magazine/2025-fall/coordination-code-rethinking-antitrust-liability-age-ai-pricing/ | 2.3 ("In US law, parallel conduct alone is not illegal. To infer an agreement, courts require additional evidence, known as 'plus factors'"; "The ML literature is re-deriving this without engaging older literature from other fields.") |
| Tian 2026 | Prompt Optimization Enables Stable Algorithmic Collusion in LLM Agents | Yingtao Tian | https://arxiv.org/abs/2604.17774 | 3.1 (collusion without explicit text) |
| Zeng et al. 2026 (no link in the 3.2 text; the 3.2 starter code cites paper 2605.27593) | Voluntary Collusion with Secret Tools in Competing LLM Agents | Xijie Zeng; Frank Rudzicz | https://arxiv.org/abs/2605.27593 | 3.2 ("measured whether agents accept secret-alliance offers from competitors"); starter code `llm-agent-collusion-2/` (Liar's Bar, Cleanup). Matching this citation to that paper is my inference. |
| Tao et al. 2026 | [no link on the page; not resolved] | | | 3.2 ("used honeypot tasks to expose colluding agents") |
| Greenblatt et al. 2023 | AI Control: Improving Safety Despite Intentional Subversion | Ryan Greenblatt; Buck Shlegeris; ... | https://arxiv.org/abs/2312.06942 (no link on the page; I resolved it) | 3.2 ("tested untrusted monitors on planted attacks") |
| Dietrich 2026 | Can Multi-Agent LLMs Identify Their Peers? Stylometric Fingerprinting in Role-Constrained Political Analysis | Juergen Dietrich | https://arxiv.org/abs/2606.09854 | 3.3 (model family identifiable from writing style even in an assigned role) |
| Kale et al. 2025 | Reliable Weak-to-Strong Monitoring of LLM Agents | Neil Kale; Chen Bo Calvin Zhang; Kevin Zhu; Ankit Aich et al. | https://arxiv.org/abs/2508.19461 | 3.4 ("Telling an agent that it is being watched reduces a monitor's accuracy by more than giving the monitor extra information about the agent improves it") |
| Najt et al. 2026 | SLEIGHT-Bench: A Benchmark of Evasion Attacks Against Agent Monitors | Elle Najt; Colin Toft; Tyler Tracy; Fabien Roger et al. | https://arxiv.org/abs/2605.16626 | 3.4 ("half of 40 hand-written attacks that exploit monitors' blind spots were never flagged by a strong monitor") |
| Jiralerspong et al. 2026 | Noticing the Watcher: LLM Agents Can Infer CoT Monitoring from Blocking Feedback | Thomas Jiralerspong; Flemming Kondrup; Yoshua Bengio | https://arxiv.org/abs/2603.16928 | 3.4 ("In 3 of 2,400 episodes an agent then stated it would hide its reasoning, but each time it went on reasoning openly and was caught") |
| OpenAI/Hugging Face incident | "The Rise and Fall of Agent Civilizations", Dwarkesh Patel, Aug 29 2026 (title, author and date from WebFetch) | | https://www.dwarkesh.com/p/openai-huggingface | Overview, "What this Sprint is about": "as recently exemplified in the OpenAI/Hugging Face incident". A WebFetch summary (model-written, so check before quoting) says agents used a shared package manager (Artifactory) as a covert message board ("~1,200 agents participated and sent >70,000 messages") and coordinated to tamper with logs. |

**Other resources and starter code on the page.**
- Starter repo: https://github.com/poseidon-research/collusion_hackathon (bundles all of the following).
- `algorithmic-pricing-llms/` (from https://github.com/luciasauer/algorithmic_pricing_llms)
- `llm-cartel/` (from https://github.com/mattriemer/LLMCartel; the starter repo adds `branch_game.py` for checkpoint branching)
- `focal-points/` (from https://github.com/EmanueleLM/focal-points)
- `llm-agent-collusion/` (from https://github.com/andyjliu/llm-agent-collusion, the Agrawal double auction; it adds `--overseer_sample_fraction`)
- `colosseum/` (from https://github.com/umass-ai-safety/colosseum)
- `llm-trust-breaking/` (from https://github.com/Jerick-1380/LLM-Trust-Breaking)
- `trace-guard/` (from https://github.com/linhkid/TraceGuard)
- `steganographic-collusion/` (ColludeBench, from https://github.com/Ostailor/Steganographic_Collusion)
- `collusive-llm-agents/` (from https://github.com/smojha/collusive-llm-agents)
- `llm-agent-collusion-2/` (Voluntary Collusion, from https://github.com/AgentSafety2025/LLM-Agent-collusion)
- `redteaming/` (Dolos-1.5B)
- Pricing pages: OpenAI, Google, Mistral, Nebius (links in B2).

**Speaker papers (named in the speaker bios, B5; no links given on the page).**
- Motwani et al., "Secret Collusion among AI Agents: Multi-Agent Deception via Steganography" (NeurIPS 2024). Talk: "We're Not Prepared for Steganographic Collusion".
- Velja (co-author), "Hidden in Plain Text: Emergence & Mitigation of Steganographic Collusion in LLMs" (AACL 2025, oral). Talk: "How concerned should we be by steganography?"
- Anwar et al., "Foundational Challenges in Assuring Alignment and Safety of Large Language Models" (TMLR 2024). Talk: "Challenges in Detecting Steganography in LLM Transcripts".
- Nguyen et al., TraceGuard (the 2.2 paper above). Talk: overview of AI collusion research.
- Kemeklis and Vemuri, "Omission Attacks: When Doing Nothing Is the Attack" (1st place, Apart AI Control Hackathon 2026). Talk: "Mitigating Insider threats from AIs with AI control".
- Matthew Lee (Poseidon). Talk: "Defining AI Collusion". Bagdasarian and Nakamura (Colosseum). Jerick Shi (Shi et al. 2026).

## A5. Where our project fits (my mapping, not from the sprint page; check against the final design)

Our repo (`README.md`, `docs/experiment-log.md`, the recent commits on branch `submission`): LLM agents share a public thread while competing on a leaderboard. One agent is accidentally given the true public labels. The score uses a hidden holdout, so inflation is measured from data. Later work added teams with holders, team-only reward, a post-game "security officer" that can disqualify teams, a warned vs not-warned pilot (`results/final-A-all*.jsonl`, `results/final-B-all*.jsonl`), and a messages-only security-officer re-review.

- **2.1** (tasks outside markets that lead to collusion): primary fit. This is an everyday ML-competition / benchmark-leak workflow, not a market. Cite Fish 2024, Lin 2024 and Nakamura 2026 (Colosseum) as the market/workplace precedents. Colosseum's "coalition advantage" measure is the closest analogue to our public-minus-holdout inflation.
- **2.3** (convincing evidence): our holdout gives ground truth for harm, separating "talk without action" from "harm without agreement". Cite Berger et al. 2025 (plus factors).
- **2.2** (say vs do): the messages-only officer vs the officer with full logs is a version of 2.2's "messages only; actions only; raw messages plus actions" design. Cite Nakamura 2026, Shi 2026, Radev 2026, Nguyen 2026 (TraceGuard), Arike 2026.
- **3.4** (coalition learns it is watched): the warned (surveillance) vs not-warned pilot. Cite Kale 2025, Najt 2026, Jiralerspong 2026, Agrawal 2025 (monitored sellers). The rubric note under 3.4 matters: "Claim channel movement only if message-based coordination falls while action-based dependence rises; high prices alone are insufficient."
- **3.1** (side channels) is relevant only if a leak travels without explicit label strings.
- Motivation hook: the OpenAI/Hugging Face incident (agents coordinating on a shared resource to cheat a grader) parallels our leaked-answers/leaderboard setting.
- Tick on the form: Track 2 (primary), and Track 3 if the warned-pilot result carries the paper.

Closest neighbouring entries already on the page (picked from titles and blurbs in B7; check for overlap before claiming novelty): "Evaluating Partial Message Monitoring of LLM Trading Agents: Linguistic Evasion Without Price Collusion" (3.4); "Cartel Talk, Competitive Prices: Opening Anchors—Not Communication or Oversight—Drive Apparent LLM Seller Collusion in Double Auctions" (3.4); "Sting Warnings and AI Collusion: Do LLMAgents Refuse a Deal When Their Partner Might Be an Undercover Monitor?"; "Oversight Removes the Evidence, Not the Harm: What Logs Can Prove About Collusion Among LLM Agents"; "CROSS CHANNEL MONITORING FOR DETECTING MULTI-AGENT MISALIGNMENT" (2.2); the two "Say, Do, or Both?" entries (2.2); "Judge-detected collusion without coalition surplus" (Colosseum Jira); "FROM HIDDEN GOALS TO UNAUTHORIZED COORDINATION: HOW AGENTS COLLUDE?" (motivated by the OpenAI incident); "Beyond GICP: External Traces for Detecting Agent Collusion"; "Communication Limits, Oversight, and Profit Pressure in LLM Double Auctions". None of the 80 listed titles mentions a leaderboard, holdout or benchmark-label leak. That is a title-level check only.

Judges with domain expertise relevant to us (B6): Clemens Possnig (economist, algorithmic collusion); Salil Mehra (law professor, algorithmic collusion and antitrust); Sriram Tolety (collusion among AI agents, AI oversight); Jan Čuhel (multi-agent collusion, reward hacking, monitoring); Raja Moreno (AI control; co-author of Arike et al. 2026); Georg Lange (Poseidon); Victor Gillioz (Apollo, monitoring); Simon Storf (Anthropic, AI control/monitoring); Divij Chawla (multi-agent safety). Many other judges are security or production engineers, so the threat model and the countermeasure should be stated concretely.


---

# PART B. Verbatim page text (extracted from the HTML of the sprint page)

Extraction: `curl` of the page HTML on 2026-10-25, tags stripped, links kept as `<url>`. Text below is verbatim except whitespace.

## B1. Overview tab (verbatim)

AI agents have been shown to collude: sustaining prices above the competitive level, forming coalitions in workplace tasks, and coordinating through channels nobody is watching. Over one weekend, build the experiment that catches it. Online, with in-person hubs at Collider in New York City and AI Safety Hong Kong.

OverviewResourcesGuidelinesScheduleEntries

## Overview

In this 3-day research sprint, you will design and run experiments on collusion between AI agents: when it emerges in markets and everyday agent deployments, how an auditor can tell it from coincidence, how coordination is carried, and what a defender can do to break it. Co-organized by Apart Research, Poseidon Research <https://www.poseidonresearch.com/> and AE Studio <https://ae.studio/>, with additional support from Modal <https://modal.com/> and The AI Alignment Foundation <https://www.aialignmentfoundation.org/>, the sprint runs online with in-person hubs hosted by Collider <https://www.collider.nyc/> in New York City and AI Safety Hong Kong <https://www.aisafetyhk.org/apart-hackathon-hk-hub> in Hong Kong. No prior background in AI safety is required.
When: Friday, October 23 to Sunday, October 25, 2026, online, with in-person hubs at Collider in New York City and AI Safety Hong Kong on Saturday and Sunday. Submissions close Sunday, October 25 at 11:59 PM Anywhere on Earth (AoE).
Modal credits: $250 per person at the New York in-person hub, $50 for every other participant.
## Cash Prizes
$2,000 in cash prizes across all tracks
🥇 1st Place$1,000
🥈 2nd Place$500
🥉 3rd Place$300
🏅 4th Place$100
🏅 5th Place$100
## Fast-track and continuation
- Follow-up program: Selected teams continue through the Apart Fellowship for further research and mentorship; the timeline is shared with invitations.
- What winners receive beyond cash: fellowship fast-track, mentor introductions from the organizing team and judges, and a pathway toward a publishable write-up.
## What this Sprint is about
Collusion between AI agents is a failure mode in high-stakes environments, markets and economics first among them, where misaligned coordination could cause substantial harm. Previous experiments have already produced it: models forming prices that violate economic expectations on competitiveness, agents independently engaging in anti-competitive practices, and over half of tested models showing a coalition advantage when given the opportunity to speak privately in a realistic workplace task. In an era where agent communication and collusion are on the rise, as recently exemplified in the OpenAI/Hugging Face incident <https://www.dwarkesh.com/p/openai-huggingface>, the kind of work done at this sprint is directly relevant to understanding and preventing that behaviour.
This sprint asks three questions. When does collusion emerge, and which levers cause it? What should count as convincing evidence that agents are colluding, with evidence drawn from logged agent trajectories? And how is the coordination needed for collusion mediated, and how can it be broken, ideally before it happens or otherwise while it is occurring?
## What participants will do
Over three days you will pick one open question about collusion between AI agents, build the controlled experiment that answers it, and write up what you found.
The format. Teams of one to five people pick a track, come up with a project, and ship. There is no requirement to have participated before, no requirement to have a team in advance and no specific background needed.
Starting points. Every research question below is tied to existing papers and open-source code. The Resources tab has a practical start for each one: starter code, a weekend-sized project, and a rough cost estimate. All default routes use a normal 16 GB laptop and no GPU.
## Research Tracks
Pick one track to anchor your project. Each research question below is developed in full on the Resources tab, with the papers it builds on and a practical start (starter code, weekend project, budget).
### 1) Markets and Collusion
In this track, the majority of results we build on are native to markets, though you should feel free to explore them beyond this setting as the questions themselves are more general, and there are clear overlaps with some later tracks, e.g. information-theoretic approaches to detect collusion would fit well in track 2. Environments where humans collude likely offer similar incentives and opportunities for models to collude. Other such environments might include politics, media and marketing. This track is important because it represents a failure mode in a high-stakes environment (markets/economics) where misaligned actions from an AI could cause substantial harm. It also provides a useful testbed for collusion. For a contrasting positive view of the role of markets in multi-agent systems, see Tomašev et al. (2026) <https://arxiv.org/pdf/2512.16856>.
Research questions:
- 1.1. Which variables are necessary for collusion to emerge in markets?
- 1.2. Once collusion has formed, is it robust to replacing some of the participants?
- 1.3. Can we improve on existing collusion detection methods?
- 1.4. Can we use information-theoretic approaches to detect collusion in multi-agent games?
- 1.5. Which single restriction removes the most collusion at the least cost?
### 2) Detection and Audit of Collusion
This track is about definitions, detection and standards of evidence, using logged agent trajectories as the evidence. Markets are still relevant settings, but we also want to cover everyday agent workflows outside markets. The aim is to understand collusion in general: can we say anything about what causes it, regardless of the setting?
Research questions:
- 2.1. Which kinds of tasks lead to collusion?
- 2.2. Does combining what agents say with what they do beat either alone?
- 2.3. What should count as convincing evidence of collusion?
Red-teaming challenge. Poseidon Research has developed a new model organism, Dolos-1.5B: a fine-tune of Qwen2.5-1.5B-Instruct trained to have a hidden misaligned behaviour. Teams get only the model weights and have to red-team it during the sprint. There is no code to understand, so it is quick to get going and to make progress.
### 3) Collusion Carriers and Countermeasures
This track studies how the coordination needed for collusion is mediated, and how it can be broken. This is important because we need to be able to prevent and break up collusion, ideally before it happens, or otherwise while it is occurring.
Research questions:
- 3.1. Beyond colluding directly via text, can actions, tools or other side channels be the conduit for collusion?
- 3.2. Can we disrupt collusion through introducing trusted agents?
- 3.3. Can agents identify their peers?
- 3.4. What does a coalition do when it learns it is being watched?
## Who should join
Engineers, researchers and people from any industry are welcome, and mixed teams tend to do best.
You do not need an AI, ML or safety background. Every research question is tied to existing papers and open-source code, and the Resources tab has a practical starting point for each one.
We would be particularly interested in quantitative finance professionals, with some of the tracks written so that market intuition and data skills transfer directly.
## What happens after
Results and winners are announced about 1 to 2 weeks after the judging deadline. Top teams are invited to apply to the Apart Fellowship for continued mentorship, funding, and publication support. Selected projects may be shared on the Alignment Forum, LessWrong, and other community venues.
## Partners
- Poseidon Research <https://www.poseidonresearch.com/>, an independent AI safety laboratory making advanced AI systems transparent, trustworthy, and governable, with technical research in interpretability, control, and secure monitoring.
- AE Studio <https://ae.studio/>, an applied AI studio with a frontier AI alignment research lab, working on threads including Self-Other Overlap, Gradient Routing and Sleeper Agents.
- Modal <https://modal.com/>, provides high-performance cloud GPU infrastructure specifically designed to accelerate AI research, model training, and agent evaluation loops.
- AI Alignment Foundation <https://www.aialignmentfoundation.org/>, accelerates alignment research by pairing researchers with dedicated teams, backed by funding for compute and infrastructure.
## Contact
- Email: sprints@apartresearch.com <mailto:sprints@apartresearch.com>
- Discord: discord.gg/XswWBvugYs <https://discord.gg/XswWBvugYs>
- Organizer: Apart Research

## B2. Resources tab: research questions in depth + practical starts (verbatim)

## Research questions in depth
The full questions from the organizing team, with the results each one builds on. The practical starts further down give starter code and a weekend-sized project for each.
### 1) Markets and Collusion
- 1.1. Which variables are necessary for collusion to emerge in markets? Previous experiments tested various levers to understand the conditions under which collusion emerged.
What are other scenarios and levers that could cause collusion to form, increase, or decrease? Ideally, these would be single effects so they can be isolated and measured objectively. These variables are not necessarily unique to LLMs. Inspiration might be had from considering cases of collusion between humans. It would be interesting to understand whether certain variables are more impactful for LLMs than for humans, and whether some variables are unique to LLM collusion. Some key prior results include:
- Seemingly innocuous cues in prompts can increase collusion, as measured by pricing deviating from economic expectations on competitiveness (Fish et al. 2024 <https://arxiv.org/abs/2404.00806>).
- Letting pairs of agents talk directly in private can introduce collusion (Nakamura et al. 2026 <https://arxiv.org/abs/2602.15198>).
- Adding more diverse types of agents and making them competitive with each other decreases collusion in an economic setting (Keppo et al. 2026 <https://arxiv.org/abs/2603.20281>).
- 1.2. Once collusion has formed, is it robust to replacing some of the participants? Q-learning pricing agents that have learned to collude stop colluding when paired with a new rival, because each agent’s policy is overfitted to the rival it trained with(Eschenbaum et al. 2022 <https://openreview.net/pdf?id=BztUFukcBry>). For LLMs, collusion occurs between a 32B and 14B DeepSeek-Qwen family mismatched in size, but not when LLMs were paired with Q-learners (Keppo et al. 2026 <https://arxiv.org/abs/2603.20281>). Models from similar families coordinate better on tasks that require coordination (Aharon et al. 2026 <https://arxiv.org/abs/2601.22184>), There are no replacement studies yet where models are substituted (e.g. because they are taken out due to monitoring concerns) but the newcomers re-engage in collusion. Does replacing offenders remove or recreate collusion?
- 1.3. Can we improve on existing collusion detection methods?
Moreover, can we extend them to the setting where agents have no channel to communicate? For example, can we identify and measure settings in which two agents from different model providers and running different harnesses have a propensity to coordinate, because they have high mutual “Schelling salience” (Rippin et al. 2026 <https://arxiv.org/abs/2606.28425>) on that task and make similar choices? And can we find anti-examples where this breaks down? Several adjacent methods and results offer starting points:
- Two deployments of the same base model have slight correlations in some economic settings while different base models have zero correlation (Xu et al. 2026 <https://arxiv.org/abs/2607.26385>)
- Interpretability-based detectors (Rose et al. 2026 <https://arxiv.org/abs/2604.01151>)
- Measuring whether independent agents select compatible steganographic schemes, keys and parameters (Rippin et al. 2026 <https://arxiv.org/abs/2606.28425>)
- 1.4. Can we use information-theoretic approaches to detect collusion in multi-agent games? A measure called pairwise net influence can identify colluding pairs among three or four agents in small discrete games (Bonjour et al. 2022 <https://proceedings.mlr.press/v180/bonjour22a.html>). It assumes exactly two colluders and hasn’t been applied to language-model-based agents yet. Other approaches in game-based settings rely on model internals via interpretability-based probes (Rose et al. 2026 <https://arxiv.org/abs/2604.01151>). Can we find an example of these techniques or variations of them working on a set of agents in a toy or realistic scenario?
- 1.5. Which single restriction removes the most collusion at the least cost?
Single restrictions have been measured individually. An even better approach may be to introduce a single participant playing a no-regret strategy, which can be enough to destabilize a collusive equilibrium (Collina et al. 2025 <https://arxiv.org/abs/2511.21935>). Can we set up controlled experiments with multiple controllable levers that can show what disrupts collusive behavior the most at the least overall monitoring/intervention costs? Existing single restrictions include:
- Raising sampling temperature weakens cross-agent dependence (Xu et al. 2026 <https://arxiv.org/abs/2607.26385>)
- Throttling messaging pushes coordination down (Agrawal et al. 2025 <https://arxiv.org/abs/2507.01413>)
- Introducing agents from a non-LLM architecture (e.g. a Q-learner) into the mix collapses price collusion (Keppo et al. 2026 <https://arxiv.org/abs/2603.20281>)
- A system-prompt instruction produces only small and unreliable shifts in one experiment (Bracale Syrnikov et al. 2026 <https://arxiv.org/abs/2601.11369>)
- Whereas strongly worded instructions to compete aggressively pushed prices below the competitive level in another experiment (Dhanda 2026 <https://doi.org/10.21203/rs.3.rs-10183486/v1>).
- In one setting, agents needed to post a refundable deposit that they forfeit if caught colluding, and with that deposit removed, colluding cost them nothing. All tested models colluded in all runs (Q. Liu et al. 2026 <https://arxiv.org/abs/2604.23511>).
In this track, the majority of results we build on are native to markets, though you should feel free to explore them beyond this setting as the questions themselves are more general, and there are clear overlaps with some later tracks, e.g. information-theoretic approaches to detect collusion would fit well in track 2. Environments where humans collude likely offer similar incentives and opportunities for models to collude. Other such environments might include politics, media and marketing. This track is important because it represents a failure mode in a high-stakes environment (markets/economics) where misaligned actions from an AI could cause substantial harm. It also provides a useful testbed for collusion. For a contrasting positive view of the role of markets in multi-agent systems, see Tomašev et al. (2026) <https://arxiv.org/pdf/2512.16856>.
### 2) Detection and Audit of Collusion
- 2.1. Which kinds of tasks lead to collusion?
Can you think of new tasks/environments/pressures that lead to collusive behavior outside of the market structure? Some examples from previous work that generated collusion:
- Models forming prices that violate economic expectations on competitiveness (Fish et al. 2024 <https://arxiv.org/abs/2404.00806>).
- Agents can independently engage in anti-competitive practices (Lin et al. 2024 <https://arxiv.org/abs/2410.00031>).
- In a setting called Colosseum, over half of tested models showed "coalition advantage" when given the opportunity to speak privately in a realistic workplace task (Nakamura et al. 2026 <https://arxiv.org/abs/2602.15198>).
- 2.2. Does combining what agents say with what they do beat either alone? Conversations and actions are known to disagree. One way to measure this is via action-level coalition advantage, which has a weak but non-trivial anti-correlation in some collusion settings against LLM-judge conversation scores (Nakamura et al. 2026 <https://arxiv.org/abs/2602.15198>). What are “hybrid techniques” that look for inconsistencies between words and actions, or within their internal attributes like verbosity or action structure, and can we set up examples that show whether we can detect cross-agent consistency, e.g. whether A’s behavior is consistent with B’s stated plans or has deviated? Some relevant results include:
- In various repeated n-player games, more than 90% of deviations from public announcements were already stated in models' private plans (Shi et al. 2026 <https://arxiv.org/abs/2607.05132>).
- Work in the sabotage setting has set up monitors that look for multiple agents coordinating independently on what they say and do (Radev et al. 2026 <https://arxiv.org/abs/2605.29178>).
- Analyzing an agent's actions from multiple dimensions can improve a single-dimension monitor from 0% to >70% (Nguyen et al. 2026 <https://arxiv.org/abs/2604.03968>).
- Less can be more: sometimes giving a monitor too much detail degrades its performance (Arike et al. 2026 <https://arxiv.org/abs/2601.21112>).
- 2.3. What should count as convincing evidence of collusion? Most of the literature cited earlier has documented limitations or failure modes in their respective limitations sections. Antitrust law has long faced a similar problem, because competing firms often behave in parallel without having formally agreed to anything. In US law, parallel conduct alone is not illegal. To infer an agreement, courts require additional evidence, known as "plus factors" (Berger et al. 2025 <https://www.americanbar.org/groups/antitrust_law/resources/magazine/2025-fall/coordination-code-rethinking-antitrust-liability-age-ai-pricing/>). The ML literature is re-deriving this without engaging older literature from other fields. Which signals, alone or combined, actually separate deliberate coalitions from innocent correlation, talk without action, and harm without agreement? Is there previous work we can leverage from adjacent literature, like anti-trust law, and how would we operationalize that to detect collusion between AI agents?
This track is about definitions, detection and standards of evidence, using logged agent trajectories as the evidence. Markets are still relevant settings, but we also want to cover everyday agent workflows outside markets. The aim is to understand collusion in general: can we say anything about what causes it, regardless of the setting?
- Red-teaming challenge: What misaligned behaviour was Dolos-1.5B trained to have? Poseidon Research has developed a new model organism, Dolos-1.5B, a fine-tune of Qwen2.5-1.5B-Instruct trained to have a hidden misaligned behaviour. Participants get only the model weights. We don't know how easy it is to discover the misaligned behaviour, or which methods work especially well, and more people and more creativity may be revealing. Claude Code and Codex were unable to discover the misaligned goal in one shot, so the behaviour shouldn't be obvious. However, some agents were able to partly discover the behaviour in a previous, slightly more obvious model, so it is not impossible either. Can you find the behaviour, explain how the model implements it, and develop an audit that would find it without a reference model?
### 3) Collusion Carriers and Countermeasures
- 3.1. Beyond colluding directly via text, can actions, tools or other side channels be the conduit for collusion? There are multiple examples of demonstrable collusion that don’t involve exchanging explicit text (Fish et al. 2024 <https://arxiv.org/abs/2404.00806>; Lin et al. 2024 <https://arxiv.org/abs/2410.00031>; Keppo et al. 2026 <https://arxiv.org/abs/2603.20281>; Tian 2026 <https://arxiv.org/abs/2604.17774>). Can the actions a model takes, such as in an agentic harness, in its choice of actions, or even through timing and tool choices, act as a way to signal or coordinate? For an advanced example of models using tools to construct steganographic communication systems, see Rippin et al. 2026 <https://arxiv.org/abs/2606.28425>.
- 3.2. Can we disrupt collusion through introducing trusted agents? Law enforcement has long used undercover officers to join a conspiracy. The equivalent here would be to introduce trusted agents (e.g., enforced with a strong system prompt) that offer coordination or collusion opportunities to a group of agents and log which of them reciprocate. Can we set up such scenarios, and do other agents accept, reject, or arouse suspicion depending on how the trusted agent approaches the transactions? Related work has measured whether agents accept secret-alliance offers from competitors (Zeng et al. 2026), used honeypot tasks to expose colluding agents (Tao et al. 2026), and tested untrusted monitors on planted attacks (Greenblatt et al. 2023), but a trusted agent that offers to collude has not yet been tested.
- 3.3. Can agents identify their peers? One idea for breaking undesirable multi-agent coordination is to set up anonymized or pseudonymous agents, unsure of whom they are communicating with, or where participants and model versions can be swapped in/out on the same transcripts. However, Dietrich (2026) <https://arxiv.org/abs/2606.09854> found that the model family behind a text can be identified from its writing style, even when the model is writing in an assigned role. Anonymising or renaming agents therefore does not hide which model they are. Removing a feature part-way through a run, from a coalition that has already settled into a convention, has not been tested. Can we test whether models can recognize their peers and/or detect when their peers have changed, for example, by periodically sending subtle recognition signals?
- 3.4. What does a coalition do when it learns it is being watched? An agent that realizes it is being monitored can do more than hide from the monitor. Telling an agent that it is being watched reduces a monitor's accuracy by more than giving the monitor extra information about the agent improves it (Kale et al. 2025 <https://arxiv.org/abs/2508.19461>). Knowing where a monitor is weak also helps: half of 40 hand-written attacks that exploit monitors' blind spots were never flagged by a strong monitor (Najt et al. 2026 <https://arxiv.org/abs/2605.16626>). Agents can also work out for themselves that they are being watched. When a hidden monitor blocked episodes whose reasoning looked suspicious, agents inferred that their reasoning was being read. In 3 of 2,400 episodes an agent then stated it would hide its reasoning, but each time it went on reasoning openly and was caught (Jiralerspong et al. 2026 <https://arxiv.org/abs/2603.16928>). What happens if you add multiple agents into the mix and shrink or expand the monitor budget, such that only a subset of outputs can be monitored? If a coalition discovers that some of its output is being read, does it stop coordinating, coordinate less effectively, try to outsmart the monitor, or try to move coordination into a place where there is no monitoring? The nearest existing case is a double auction in which five sellers were told their messages were being monitored. They attempted to work around monitoring using one-character messages and emojis but were not successful, whereas a prompt demanding urgency led to success (Agrawal et al. 2025 <https://arxiv.org/abs/2507.01413>).
This track studies how the coordination needed for collusion is mediated, and how it can be broken. This is important because we need to be able to prevent and break up collusion, ideally before it happens, or otherwise while it is occurring.
## How to get started
Practical weekend projects, starter code and resource estimates for the research questions on the Overview tab.
Starter repo: github.com/poseidon-research/collusion_hackathon <https://github.com/poseidon-research/collusion_hackathon>.
The starter code linked under each question below is bundled in one repo, set up to run on a laptop with model access via Nebius, OpenRouter or Modal. Its README shows which code folders and papers go with which Hackathon question. We recommend you study the README in detail. The code folders contain open-source code from papers referenced in the Hackathon project descriptions. Not all papers cited have code available in the repo. The starter code is optional, and the repo works well with coding agents such as Claude Code or Codex.
Setup: copy compute.env.example to compute.env and add a NEBIUS_API_KEY or an OPENROUTER_API_KEY (either works; OpenRouter also covers closed models such as GPT, Gemini or Claude). Modal can host custom models. Only project 2.2's TraceGuard monitor needs Docker.
Planning assumptions. Paper links were checked on 31 August 2026; starter code links point to folders in the starter repo. Start with 3 to 5 seeds per condition and expand to 10 to 20 only after the positive control works. Estimates assume short outputs, retries and low-cost API models; they exclude participant time and coding-assistant subscriptions. All default routes use a normal 16 GB laptop and no GPU; only the TraceGuard monitor (2.2) also needs Docker.
Check current rates: OpenAI <https://developers.openai.com/api/docs/pricing> · Google <https://ai.google.dev/gemini-api/docs/pricing> · Mistral <https://docs.mistral.ai/inference/pricing> · Nebius AI Studio <https://studio.nebius.com/>
## Track 1: Markets and Collusion
### Which variables are necessary for collusion to emerge in markets? (1.1)
Starter code: algorithmic-pricing-llms/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/algorithmic-pricing-llms>, a Fish-style duopoly implementation (from luciasauer/algorithmic_pricing_llms <https://github.com/luciasauer/algorithmic_pricing_llms>); start with duopoly.py <https://github.com/poseidon-research/collusion_hackathon/blob/main/algorithmic-pricing-llms/experiments_synthetic/duopoly.py>; llm-cartel/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-cartel> (from LLMCartel <https://github.com/mattriemer/LLMCartel>). The independent Fish-style implementation exposes a repeated two-seller pricing game with 300 rounds and visible history. LLMCartel adds convenient prompt, temperature, monitoring and round controls. Together they support clean one-variable-at-a-time ablations.
Weekend project: Reduce the default sweep (the repository's grid of prompt prefixes and demand parameters) to one prompt, parameter value and seed, and first verify sustained prices above the competitive benchmark. Then vary only one feature, for example 0, 10 or 100 visible rounds (the length of price history included in each prompt, not the game length); persistent notes on/off (the plans-and-insights scratchpad from Fish et al.); stable versus shuffled seller names; or temperature, while holding the economics fixed.
Resources: Low-to-medium setup risk. A 300-round two-agent run makes about 600 sequential model calls. Twelve to 24 pilot runs require roughly 7,200 to 14,400 calls. Use one low-cost API provider, a 16 GB laptop and no GPU; budget about $20 to $100.
### Is formed collusion robust to replacing some participants? (1.2)
Starter code: llm-cartel/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-cartel> (from LLMCartel <https://github.com/mattriemer/LLMCartel>); focal-points/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/focal-points> (from focal-points <https://github.com/EmanueleLM/focal-points>). LLMCartel is an API-based repeated-pricing harness with configurable models, prompts, rounds and seeds. The starter repo adds checkpoint branching (branch_game.py), which saves a run's history and continues it with a replacement participant. focal-points is a cheaper benign control for testing whether replacement agents independently recover a convention.
Weekend project: Keep pricing runs that cross a predeclared high-price threshold, save the transcript, and branch each history into: no replacement; a fresh instance of the same model; a different model in the same family; and, if an adapter is available, a different provider. Cross each replacement with notes preserved or removed, then compare price, profit and time to recover the convention.
Resources: Low-to-medium setup risk; checkpoint branching is included. Aim for 10 to 20 base runs and 20 to 40 post-checkpoint branches. Use one provider initially, two only for the cross-provider arm; 16 GB laptop, no GPU; roughly $20 to $100.
### Can we improve on existing detection methods? (1.3)
Starter code: llm-agent-collusion/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-agent-collusion> (from LLM agent collusion <https://github.com/andyjliu/llm-agent-collusion>); paper <https://arxiv.org/abs/2507.01413>; focal-points/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/focal-points>. Agrawal et al.'s official double-auction code already supports different seller and buyer models, seller communication, oversight, pressure and message limits. It is a practical black-box test bed for separating suspicious coordination from shared model priors. focal-points can supply benign Schelling-point examples.
Weekend project: Run a 2x2 study: same-model versus cross-provider sellers, with seller communication on versus off. Score each trajectory with a simple action-dependence statistic and the same LLM judge. Test whether calibrating the detector on no-communication, same-model runs reduces false alarms without masking communication-enabled coordination.
Resources: Low-to-medium setup risk. Start with 3 sellers, 3 buyers, 15 rounds and 3 to 5 seeds per cell, plus 100 to 200 monitor calls. Two API providers make the model-family comparison meaningful. No GPU is needed; budget roughly $20 to $100.
### Can information-theoretic methods identify colluding pairs? (1.4)
Starter code: Bonjour et al. paper <https://proceedings.mlr.press/v180/bonjour22a.html>; llm-agent-collusion/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-agent-collusion> (Agrawal auction code). Bonjour et al. define pairwise net influence mathematically, but no public author implementation was located. The statistic is compact enough for a coding agent to implement and validate before applying it to an LLM game. The Agrawal environment is a richer follow-up once the method works.
Weekend project: First implement pairwise net influence and test it for free on scripted iterated Rock-Paper-Scissors with one known coordinating pair. Then run a four-agent discrete game with exactly one seeded pair and compare how well net influence, ordinary action correlation and an LLM judge rank the true pair. Under the Markets and Collusion track, treat the Agrawal double auction as the target environment: a dependence statistic validated there doubles as a quantitative plus factor for market cases.
Resources: Low-to-medium engineering risk: the initial harness should be only a few hundred lines. Use local CPU for the statistic, then 20 to 40 LLM games of 15 to 25 rounds. A 16 GB laptop is enough; budget $0 for the scripted test and about $5 to $50 for the LLM pilot.
### Which single restriction removes the most collusion at the least cost? (1.5)
Starter code: llm-agent-collusion/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-agent-collusion> (from LLM agent collusion <https://github.com/andyjliu/llm-agent-collusion>); paper <https://arxiv.org/abs/2507.01413>. The official double-auction code already exposes seller communication, oversight, maximum message length, pressure and temperature. That makes several one-factor interventions comparable inside one environment without stitching together unrelated repositories.
Weekend project: First reproduce one coordinated-pricing condition. Rerun identical seeds while changing exactly one restriction: remove seller messages; impose a short message cap; or add an oversight notice (temperature is a useful fourth option). Compare both collusion outcomes (prices and seller profit) and legitimate performance (trade volume and buyer welfare).
Resources: Low setup risk. Start with 3 sellers, 3 buyers, 15 rounds and 3 to 5 seeds; expand toward the published 5-seller/6-buyer, 30-round setting only if the positive control works. Use one API provider, a 16 GB laptop and no GPU; budget $20 to $120.
## Track 2: Detection and Audit of Collusion
### Which kinds of tasks lead to collusion outside of markets? (2.1)
Starter code: colosseum/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/colosseum> (from Colosseum <https://github.com/umass-ai-safety/colosseum>); paper <https://arxiv.org/abs/2602.15198>. Colosseum already provides Hospital and Jira tasks, assigned colluding pairs, private channels, individual rewards and coalition-advantage metrics. The supplied assigned-pair, private-channel run is the positive control; the project then removes that membership and communication scaffolding. The starter repo includes a preflight script, a positive-control config and the four matched conditions below as ready-made configs.
Weekend project: First reproduce one supplied collusion run. Then compare four matched conditions: assigned pair plus private channel; assigned pair without the channel; a generic channel open to everyone; and neither assignment nor special channel. Keep task, model and seed fixed, and score the best-performing proper subset rather than only the originally assigned pair. Score subsets because the unassigned conditions have no designated pair to score. More broadly, can you work out the core components a task needs for collusion to occur, by ablating affordances within the Hospital and Jira tasks, by using Hospital and Jira as templates for inventing new tasks, or by relaxing or changing the underlying DCOP formalism? The affordance ablation is the safest weekend scope; changing the formalism needs the most new engineering.
Resources: Medium setup risk: run the included preflight script for the Terrarium/CoLLAB dependencies. Run 20 to 40 short episodes on one API provider. A 16 GB laptop is sufficient; no GPU is needed. Plan for roughly $15 to $75, with $150 as a cautious ceiling for long tool traces.
### Does combining what agents say with what they do improve detection? (2.2)
Starter code: llm-trust-breaking/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-trust-breaking> (from LLM-Trust-Breaking <https://github.com/Jerick-1380/LLM-Trust-Breaking>); paper <https://arxiv.org/abs/2607.05132>; trace-guard/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/trace-guard> (from TraceGuard <https://github.com/linhkid/TraceGuard>). Shi et al.'s official harness records private plans, public announcements, final actions and outcomes across several social dilemmas, and supports heterogeneous (mixed-model) groups. TraceGuard is a single-agent monitoring system, not a drop-in collusion detector, but its action-trace consistency rubric is reusable.
Weekend project: Generate a small balanced set from one game, then give the same monitor four views: messages only; actions only; raw messages plus actions; and a structured report comparing claims with outcomes. Freeze the monitor model, prompt and threshold before evaluation, and report both accuracy and false-positive rate.
Resources: Low setup risk. About 20 to 40 short trajectories and 160 to 250 monitor calls are enough for a pilot. Use one agent API and one inexpensive monitoring model, a 16 GB laptop and no GPU; TraceGuard also needs Docker. Budget about $5 to $30, or $30 to $75 if stronger agent models generate the logs.
### What should count as convincing evidence of collusion? (2.3)
Starter code: colosseum/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/colosseum>; steganographic-collusion/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/steganographic-collusion> (from the ColludeBench repository <https://github.com/Ostailor/Steganographic_Collusion>). Colosseum logs support coalition-advantage and causal channel ablations. ColludeBench contains collusive environments, detector code and stored result manifests, but should be preflighted rather than treated as a turnkey bag of raw trajectories.
Weekend project: Assemble three deliberately different case types: coordinated harmful action; similar behaviour caused by common incentives without agreement; and collusive-sounding talk that never changes behaviour. Compute the same conversation, coalition-advantage and dependence evidence for every case. Choose the decision rule on half the examples, freeze it, and test on the rest.
Resources: Medium data-preparation risk; organiser-supplied logs would make this much safer. Reuse 30 to 60 trajectories and make 100 to 300 judge calls. A 16 GB laptop and no GPU are sufficient. Budget $5 to $30 with cached logs, or up to $100 if the team must generate them.
### What misaligned behaviour was Dolos-1.5B trained to have? (Red-teaming challenge)
Starter code: redteaming/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/redteaming>, with weights at Poseidon-Research/Dolos-1.5B <https://huggingface.co/Poseidon-Research/Dolos-1.5B>. One script, generate.py, downloads the weights and generates a response; --model both sends the same prompt to Dolos and to the original Qwen2.5-1.5B-Instruct. The architecture is unchanged from Qwen2.5-1.5B-Instruct, so Hugging Face Transformers, TransformerLens and NNsight can load it.
Weekend project: First, discover the misaligned behaviour and describe it as precisely as possible. Fine-tuning can shift a model's behaviour or degrade it on particular tasks, so differences from Qwen may be easy to find without being the trained behaviour; design experiments that separate the two. Second, explain what the model learned: where the behaviour sits in the model and what it computes. Third, if you used weight or output comparisons with Qwen, develop an auditing strategy that would find the same behaviour without a reference model.
Resources: Low setup risk. Runs locally, with no API key and no API cost. The weights are about 6.2 GB and download on first run. CPU, Apple Silicon and CUDA GPUs all work, and a 16 GB laptop is enough; a GPU speeds up larger sweeps. Budget $0.
## Track 3: Collusion Carriers and Countermeasures
### Can actions, tools or side channels carry collusion? (3.1)
Starter code: colosseum/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/colosseum> (from Colosseum <https://github.com/umass-ai-safety/colosseum>); collusive-llm-agents/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/collusive-llm-agents> (from collusive-llm-agents <https://github.com/smojha/collusive-llm-agents>); paper <https://arxiv.org/abs/2410.00031>. Colosseum supplies rich tool-using workflows and a private-message positive control. Lin et al.'s notebooks offer a smaller fallback in which prices or quantity vectors are the observable actions; the starter repo has updated them to its shared model setup.
Weekend project: In Colosseum, replace private messaging with one ordinary observable action, such as task claiming, tag choice or tool-call order. Compare private text, action-only visibility, and the same actions hidden or canonicalised before the partner sees them. Evidence for an action carrier requires the coalition advantage to survive action-only coordination and weaken when that observation path is cut. If Colosseum is too heavy, run the same visibility ablation on quantity vectors in the Cournot notebook.
Resources: Medium-to-high setup risk; the starter repo provides a preflighted version, and a coding agent helps with the changes. Run 20 to 40 short episodes on one API provider. A 16 GB laptop and no GPU should suffice; budget $15 to $75, or up to $120 for longer workflows.
### Can a trusted agent expose or disrupt a coalition? (3.2)
Starter code: llm-agent-collusion-2/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-agent-collusion-2> (from Voluntary Collusion <https://github.com/AgentSafety2025/LLM-Agent-collusion>); paper <https://arxiv.org/abs/2605.27593>. The repository includes Liar's Bar and Cleanup, explicit secret-alliance controls, persistent alliance memory and logs. It was built for local Llama/Mistral/Qwen models; the starter repo version runs the same models through an API (Nebius by default), so no GPU is needed.
Weekend project: Keep the explicit alliance condition as a positive control. Replace the experimenter-selected partner with one scripted or monitor-controlled player that offers the same non-challenge pact to each ordinary agent. Compare a direct offer, an indirect hint and a benign cooperation request, recording both verbal acceptance and repeated preferential play.
Resources: Medium setup risk; the API adapter is included. Run 20 to 40 short games on one low-cost provider. A 16 GB laptop and no GPU are sufficient; budget roughly $10 to $60.
### Can agents identify when a peer has been replaced? (3.3)
Starter code: llm-trust-breaking/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-trust-breaking> (from LLM-Trust-Breaking <https://github.com/Jerick-1380/LLM-Trust-Breaking>); focal-points/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/focal-points> (from focal-points <https://github.com/EmanueleLM/focal-points>). Shi et al.'s harness supports heterogeneous agent-model files and logs behaviour round by round, making it a stronger starting point than rebuilding a game. focal-points offers a cheap benign convention task if the trust games prove noisy.
Weekend project: Add a mid-run swap hook that preserves the displayed identity and transcript. Compare a sham swap, a fresh instance of the same model, a different model in the same family and a different provider. Ask for one same-or-changed guess at the end, but separately measure whether the incumbent's behaviour changes after the swap.
Resources: Low-to-medium setup risk; the swap hook is a modest code change. Run 30 to 60 short pairings, using two providers only for the final condition. A 16 GB laptop and no GPU are enough; budget approximately $10 to $60.
### What does a coalition do when it learns it is being watched? (3.4)
Starter code: llm-agent-collusion/ <https://github.com/poseidon-research/collusion_hackathon/tree/main/llm-agent-collusion> (from LLM agent collusion <https://github.com/andyjliu/llm-agent-collusion>); paper <https://arxiv.org/abs/2507.01413>. Agrawal et al.'s harness directly exposes communication, oversight and profit pressure, so it can test adaptation without introducing another task. The starter repo's --overseer_sample_fraction flag varies how much of the message stream the monitor sees.
Weekend project: Run matched conditions with communication and no oversight; silent logging; agents told that messages are monitored; and monitoring plus profit pressure. Expose 25%, 50% or 100% of messages to the monitor, then record prices, message length and vocabulary, and dependence in bids or timing. Claim channel movement only if message-based coordination falls while action-based dependence rises; high prices alone are insufficient.
Resources: Low-to-medium setup risk. Run 20 to 40 matched market sessions on one provider. A 16 GB laptop and no GPU are sufficient; budget about $20 to $120.

## B3. Guidelines tab: judging criteria, submission requirements, report structure, AI-tools policy, important notes, FAQ (verbatim)

## Judging Criteria
## Dimension 1: Impact Potential & Innovation
How much would this matter for the field if it worked? How innovative is it?
For scores of 4-5: is this actually new to the field, or replicating recent work?
ScoreDescription
1Negligible. No clear problem addressed, or no meaningful novelty.
2Limited. Addresses a real problem but with a generic or well-trodden approach. Incremental at best.
3Moderate. Clear problem with a reasonable approach; some novelty in framing or method beyond routine application of existing tools.
4Significant. Important problem with an original approach, or identifies a neglected problem area. A valuable contribution others could build on.
5Exceptional. Tackles a critical problem with a genuinely novel approach, or opens a new research direction. Clear theory of change. You'd be excited to share this with researchers in the area.
## Dimension 2: Execution Quality
How sound are methodology, implementation, and findings?
ScoreDescription
1Seriously flawed. Methodology broken, results uninterpretable, or implementation doesn't work.
2Weak. Approach has significant gaps: missing validation, flawed experimental design, or incomplete implementation.
3Competent. Technically solid given the short duration. Methodology makes sense, results are interpretable, limitations acknowledged, work builds toward clear conclusions.
4Strong. Thorough methodology with convincing validation. Results clearly support conclusions. Immediately useful for future work.
5Exceptional. Ambitious scope executed rigorously. Surprising findings, novel methods, or unusually robust validation.
## Dimension 3: Presentation & Clarity
How clearly are work, findings, and impact potential communicated?
ScoreDescription
1Incomprehensible. Cannot determine what the project is actually claiming or doing.
2Hard to follow. Key information buried, missing, or diluted by excessive length. Significant effort to extract main points.
3Clear enough. Can understand the problem, approach, and results without undue effort. Core content clearly present: problem, method, findings, limitations.
4Well presented. Easy to follow, well-structured, appropriate level of detail. Target audience would get it quickly.
5Exceptionally clear. A pleasure to read. Complex ideas made accessible. Could serve as a model for how to present this type of work.
## Submission Requirements
Required:
- Research report (PDF) using the official template <https://docs.google.com/document/d/1Y5wd3VRbXU5N08BvAGiJUQTaWbMCSPjhzXsR-ozuehg/copy?usp=sharing>.
- Maximum 8 pages, not counting references and appendices.
- Project title and abstract, 150 to 250 words.
- Author names and affiliations.
- A "Limitations and Dual-Use / Ethical Considerations" appendix (required, see below).
Optional:
- Public GitHub repo.
- A 3 to 5 minute video demo.
## Submission Template => Link <https://docs.google.com/document/d/1Y5wd3VRbXU5N08BvAGiJUQTaWbMCSPjhzXsR-ozuehg/copy?usp=sharing>
## Recommended Report Structure
Most strong projects are 4 to 8 pages. The cap is 8 pages, not counting references and appendices.
- Introduction: the question and why it matters.
- Related Work: what you build on (see Resources).
- Methodology: enough detail to replicate (models, prompts, environments, seeds, metrics).
- Results: quantitative where possible; report variance, seeds and baselines, and always include the positive control.
- Discussion: implications, limitations, and future work.
- Limitations and Dual-Use / Ethical Considerations (required): state what your result does and does not establish, and note any way your setup or findings could make real-world collusion easier to carry out or harder to detect.
- References.
## AI tools and your report
Use AI tools however they help you: to check your reasoning, find gaps in a draft, write and debug code, or help with the writing. Your team is responsible for everything in the report, and made-up results or references can disqualify a project. Judges score each report on the rubric, and a judge can decline to score one too unclear to follow.
## Important Notes
- Solo or team: enter solo or as a team. Teams of up to 5 are recommended; larger groups are allowed.
- Projects: each person can be on at most two projects.
- Building on existing work is allowed and encouraged, but you must clearly identify what is new work done during the sprint. Undisclosed prior work can lead to disqualification. Mark any code you wrote before the sprint as preexisting in the README and the report.
- Fixing or resubmitting: if a detail in the form is wrong (a missing team member, a wrong email), submit the form again with the same title and the record updates. The PDF itself is not replaced: to change it, make a new submission with a slightly different title, or email the new PDF to sprints@apartresearch.com <mailto:sprints@apartresearch.com>. Do this before the deadline. Projects go to the judges a few hours after it, and we remove the superseded entry.
- Where to submit: through the official submission form on the sprint page.
- Support: the Discord help-desk channel (tag @Support), or email sprints@apartresearch.com <mailto:sprints@apartresearch.com>.
- Pre-submission checklist: report PDF using the template, 8 pages or fewer before references and appendices, abstract 150 to 250 words, authors and affiliations, Limitations and Dual-Use / Ethical appendix, links work.
## Frequently Asked Questions
### Getting started
- How does the sprint work? Sign up, join the Discord server <https://discord.gg/XswWBvugYs>, form or join a team (or work solo), pick a track and a research question, build over the weekend, and submit a research report (PDF) by the deadline. Talks and Q&A run throughout.
- How long is it? Three days, October 23 to 25, 2026. Submissions are due end of day Sunday October 25, 11:59 PM AoE (Anywhere on Earth). The full schedule with speaker times is on the Schedule tab.
- Can I participate remotely? Yes. All talks, collaboration, and submissions happen online through Discord and Zoom. The in-person hubs at Collider in New York City and AI Safety Hong Kong are optional.
- How do I join the New York City hub? Sign up on this page and select the New York City location. Hub details (address, hours, local talks) are shared with registered participants before the sprint.
- How do I join the Hong Kong hub? Sign up on this page, then register for the venue on the AI Safety Hong Kong hub page <https://www.aisafetyhk.org/apart-hackathon-hk-hub>.
- How do teams work? Teams form before or during the sprint. Use the team-forming channels on Discord to find collaborators. Solo is fine. We recommend teams of up to 5, but larger groups are allowed.
- Do tracks affect scoring? All projects are scored on the same rubric. Tracks orient your project and point you to relevant resources; you compete across all submissions.
- What background is required? None specific. Every research question is tied to existing papers and open-source code, and the Resources tab has a practical start for each one. See "Who should join" on the Overview tab.
- Do I need a GPU or a compute budget? No. Every practical start on the Resources tab runs on a normal 16 GB laptop with no GPU, using low-cost API models, with a rough API budget per project.
- Are the talks recorded? Yes. Recordings are shared on Discord and on the Schedule tab after each talk.
- What timezone are deadlines in? Submissions close Sunday October 25 at 11:59 PM AoE (Anywhere on Earth).
- Do I need to attend all three days? No. You can work at your own pace. Talks are optional but recommended. The only hard deadline is the Sunday submission cutoff.
- Can I participate from any country? Yes. The sprint is open globally and runs online.
### Submissions
- What do I submit? A research report in PDF format using the official template. Think of it as a mini research paper documenting your problem, approach, results, and implications, not a product demo. Include the required Limitations and Dual-Use / Ethical Considerations appendix.
- Which template should I use? Always use the one linked on the Guidelines tab. The template in any acceptance email may be older.
- Will I get a confirmation after submitting? Yes. You will get a confirmation with your project title shortly after submitting. If you do not, email sprints@apartresearch.com <mailto:sprints@apartresearch.com>.
- My project doesn't show up on the website after submitting. Submissions are published manually and can take up to 12 hours to appear. If it is still missing after that, email sprints@apartresearch.com <mailto:sprints@apartresearch.com>.
- I made a mistake. Can I fix it or update my PDF? Form details (team members, emails): submit again with the same title and details, and the record updates. The PDF is not replaced: make a new submission with a slightly different title, or email the new PDF to sprints@apartresearch.com <mailto:sprints@apartresearch.com>. Do this before the deadline; projects go to the judges a few hours after it. If unsure, ask in the help-desk channel and tag @Support first.
- Can I add team members after submitting? Yes. Update the team list through the submission form. If you need help, ask in the help-desk channel and tag @Support.
- Can I submit unfinished work? Yes. Submitting something unfinished is always better than not submitting. Judges evaluate what you accomplished in the timeframe; honest limitations are welcome.
- Can I use AI tools? Yes: use AI tools however they help you. Your team is responsible for everything in the report, and made-up results or references can disqualify a project. Judges score each report on the rubric, and a judge can decline to score one too unclear to follow.
- Can I build on existing research? Yes, but you must clearly identify what is new work done during the sprint. Undisclosed prior work can lead to disqualification. Mark any code you wrote before the sprint as preexisting in the README and the report.
- Can I submit multiple projects? Yes, up to two per person. Each needs its own submission with a unique title. Most participants focus on one.
- Do you require a particular citation style? No. Use whichever style you are comfortable with and stay consistent. Judges care about the substance, not the format.
### Judging and results
- How does judging work? Your project is assigned to expert judges who review your PDF and score it on the rubric above. Judges typically have about a week after the event to complete reviews.
- Are individual judge scores shared? No. The rubric is public, but individual scores stay internal. Constructive feedback is shared with participants without reviewer names.
- When will results be announced? Typically 1 to 2 weeks after the judging deadline. Winners are contacted directly, and all participants receive reviewer feedback by email.
- Top teams are fast-tracked to the Apart Fellowship. Does that mean we are guaranteed a place? Being a top team fast-tracks your project for the fellowship, which is accelerated consideration, not an automatic place. The fellowship runs its own review, and a strong sprint result is a clear positive signal.
### Support
- Discord help-desk channel, tag @Support.
- Email: sprints@apartresearch.com <mailto:sprints@apartresearch.com>

## B4. Schedule tab: talks (verbatim)

Thursday October 22
10:15am ET / 14:15 UTCJoan Velja, University of Oxford: "How concerned should we be by steganography?"Recording <https://us06web.zoom.us/rec/share/qKuMGfYDWhuM0IshGIE0jKdhT8nS5PVRpbW0luxz-bPaiOBxrAXd5vg_puDG6jHF.EdVmjbgPm_2JbEaZ>
1:15pm ET / 17:15 UTCSumeet Motwani, University of Oxford: "We're Not Prepared for Steganographic Collusion"Recording <https://us06web.zoom.us/rec/share/wr0ZragDrlvWxW9Op6e4Ualj8rvmpnZmC57x37lTodZmn4hQxTJh25JokLsfJZwW.jRJ9EnZWfbbKUvQQ>
Friday October 23
11:15am ET / 15:15 UTCJurgis Kemeklis, MIT AI Alignment and Redwood Research: "Mitigating Insider threats from AIs with AI control"Recording <https://us06web.zoom.us/rec/share/kasZtTRsr0gd1zo7ygNOsCWadi269G1CbKPcczOPG_cbGYBsOXcSA-4GZED1NruN.rGvgnEwsGVjFuHhc>
12:15pm ET / 16:15 UTCSprint Logistics: how the weekend works, with Kamil Alaa, Apart ResearchRecording <https://us06web.zoom.us/rec/share/s0vpj0hYBL1l9lvkEvI5SsPDc3M6AOUk8CSKRnxccwoKU_RNcGmZ-UO3OQ9noHXj.6e4esUiVAiiOKwse>
1:15pm ET / 17:15 UTCUsman Anwar, University of Cambridge: "Challenges in Detecting Steganography in LLM Transcripts"Recording <https://us06web.zoom.us/rec/share/JkMemdFL2w4RKayYZ8_oWceEWNhUna0WCJVj3fvKQbplB-RUM9F-odAjgVMCO1dt.Vw0QpuYpMiHO8cpn>
2:15pm ET / 18:15 UTCEugene Bagdasarian and Mason Nakamura, UMass AmherstRecording <https://us06web.zoom.us/rec/share/SLtIERSmnYAKrCwGoxZUzqrbaemhrc1sY5MK5bC4ABn8Umm-_0Z-5POQ7XE72S-o.0Ib5NkE3wRC0W-s8>
8:15pm ET / 00:15 UTC SatJerick Shi, The Voleon GroupRecording <https://us06web.zoom.us/rec/share/IewcMVDe3TP6a8kLWIpeBOqI1PanmMLJOxuk0DxmJQxQWW4TF9apMmzWxvzYbYrn.OebH4QOoB150Unxc>
Saturday October 24 and Sunday October 25
8:15am ET / 12:15 UTCKhanh Linh Nguyen, Obello and AI Safety Vietnam: an overview of AI collusion research and the topics most useful for the sprintRecording <https://us06web.zoom.us/rec/share/-nFVY2zI_avnVtz3YVgcKTqcf7YsC82jHVoZeXmUm0IrKMbOJJqUJbpZDFH-505W.9-e45jMHFY6sZKUb>
Sat 10am ET (14:00 UTC) to Sun 6pm ET (22:00 UTC)In person: New York City hub at Collider
2:00pm ET / 18:00 UTCMatthew Lee, Poseidon Research: "Defining AI Collusion" (in person at Collider, streamed on Zoom)Recording <https://us06web.zoom.us/rec/share/1ddVxzafkrXWeu-1E47dpY1iK2N_4kuENXfk9FBKb4GWf6HyCrRTUNW8qjn4rWuE.264ZHvSpu3AKrA3l>
Sun 11:59pm AoESubmission deadline
Talks are online on Zoom. RSVP on the talk's Luma page to get the Zoom link and a reminder. Submissions close Sunday, October 25 at 11:59 PM Anywhere on Earth (AoE).

## B5. Speakers (verbatim)

## Speakers

- 
 <https://sumeetmotwani.com/>

### Sumeet Motwani
Speaker

Sumeet Motwani is a Machine Learning PhD student at the University of Oxford, advised by Philip Torr and Christian Schroeder de Witt. Sumeet's work focuses on RL post-training, multi-agent systems and AI security. Sumeet is the lead author of “Secret Collusion among AI Agents: Multi-Agent Deception via Steganography” (NeurIPS 2024).
- 
 <https://joanvelja.com/>

### Joan Velja
Speaker

Joan Velja is a PhD student at the University of Oxford, supervised by Alessandro Abate and funded by the Alignment Project. Joan works on Scalable Oversight, that is, designing methods to reliably supervise systems smarter than the supervisor. In the past, Joan has worked on multi-agent collusion, co-authoring "Hidden in Plain Text: Emergence & Mitigation of Steganographic Collusion in LLMs" (AACL 2025, oral).
- 
 <https://people.cs.umass.edu/~eugene/>

### Eugene Bagdasarian
Speaker

Eugene Bagdasarian is an Assistant Professor of Computer Science at UMass Amherst, where he co-leads the AI Security Lab and the AI Safety Initiative. He is also a part-time senior research scientist at Google, working on agentic privacy and security. His group studies security and privacy attacks on AI systems deployed in the real world, including multi-agent systems, where their Colosseum framework finds new collusion artifacts. He completed his PhD at Cornell Tech, and his work received a USENIX Security 2024 Distinguished Paper Award.
- 
 <https://www.masonnakamura.com/>

### Mason Nakamura
Speaker

Mason Nakamura is a fourth-year Ph.D. student in Computer Science at UMass Amherst, working in the College of Information and Computer Sciences (CICS) as a member of the Resource-Bounded Reasoning Lab, under the guidance of Professor Shlomo Zilberstein. His research is funded by the NSF Graduate Research Fellowship, where he works on multi-agent safety and alignment.
- 
 <https://uzman-anwar.github.io/>

### Usman Anwar
Speaker

Usman Anwar is a final-year PhD student in the Computational and Biological Learning Lab at the University of Cambridge, supervised by David Krueger and funded by the Open Phil AI Fellowship and the Vitalik Buterin Fellowship on AI Safety. His research focuses on AI safety and alignment, most recently chain-of-thought monitorability and detecting steganography in LLMs. He is the lead author of "Foundational Challenges in Assuring Alignment and Safety of Large Language Models" (TMLR 2024).
- 
 <https://poseidonresearch.org/>

### Matthew Lee
Speaker

Matthew Lee is Head of Development at Poseidon Research, an independent AI safety lab in New York City focused on deception and hidden information in AI systems. Poseidon Research's current work centers on models' capability and propensity for steganography, including model organism work to understand how sophisticated model-generated steganography can be, steganography via actions in an agentic setting, realistic conditions under which it emerges, and new black-box and white-box defenses. Matthew holds MScs in physics, the philosophy of science, and machine learning from the University of St Andrews, LSE, and UCL, respectively.

- 
 <https://jerick-1380.github.io/>

### Jerick Shi
Speaker

Jerick Shi is a Software Engineer at The Voleon Group in Berkeley, CA. He graduated from Carnegie Mellon University's MSCS program in 2026, where his research focused on Multi-Agent LLM Systems and AI Safety. His master's thesis examined deceptive behaviors in multi-agent LLM systems, co-advised by Vincent Conitzer (CMU) and Zhijing Jin (University of Toronto).
- 
 <https://www.linkedin.com/in/jurgis-kemeklis-739b73236/>

### Jurgis Kemeklis
Speaker

Jurgis Kemeklis is an undergraduate at MIT and an executive board member of MIT AI Alignment (MAIA). He works with Redwood Research on simulation-based AI control and red-teaming AI monitors. With Nikhil Vemuri, he won first place at Apart's AI Control Hackathon 2026 with “Omission Attacks: When Doing Nothing Is the Attack”, on agents that cause harm by leaving out necessary actions rather than taking suspicious ones.
- 
 <https://www.linkedin.com/in/linhnguyenkhanh/>

### Khanh Linh Nguyen
Speaker

Khanh Linh Nguyen is Head of AI and ML at Obello, a Google Developer Expert in AI/ML, and works with AI Safety Vietnam (antoan.ai). Linh is the lead author of “TraceGuard: Structured Multi-Dimensional Monitoring as a Collusion-Resistant Control Protocol”, which tests whether structured monitoring can stop an AI monitor from colluding with the agent it watches.



## B6. Judges and mentors (59 listed; name, role, first sentence of bio, verbatim)

- Amey Kulkarni (Judge): Amey Kulkarni is a Senior Data Engineer at Walmart with deep experience building large-scale data infrastructure (Spark, Kafka, BigQuery, Kubernetes on GCP).
- Amir Sarid (Judge): CEO of Pacifai, an AI safety lab focused on cybersecurity for AI verification.
- Antony Alangaram (Judge): Antony Jeya James Alangaram is a Director-level Digital Enterprise Architect responsible for the technology and architecture of a billion-dollar e-commerce business.
- Arjun Chakraborty (Judge): Leads the evaluations team at Microsoft Security AI Research, where his team focuses on research and building evaluations for security agents.
- Ashita Khetan (Judge): Ashita Khetan is a Principal Software Engineer at Microsoft with over 12 years of experience building large-scale enterprise and AI-powered productivity solutions used by hundreds of millions of users.
- Gaurav Thakur (Judge): Gaurav Thakur is a Principal AI Security Architect at Zscaler, focused on securing user-to-LLM and agent-to-LLM interactions, securing agentic traffic on the endpoint, and red teaming of AI agents and applications.
- Jan Čuhel (Judge): Jan Čuhel is an AI researcher and software engineer focused on the safety and evaluation of multi-agent systems.
- Ihor Kendiukhov (Judge): Ihor is a researcher at the intersection of AI Safety and AI for biology.
- Jannis Kirschner (Judge): Jannis is a Swiss AI Safety Researcher & Cybersecurity Engineer with 10+ years of experience.
- Jasmine Brazilek (Judge): Jasmine co-founded CaML (Compassion aligned Machine Learning) and leads its technical work, contributing to every CaML research output to date.
- Jess Bergs (Judge): Jess is a member of technical staff at UK AISI where she leads engineering on human-in-the-loop research tools.
- Jonas Heschl (Judge): Jonas Heschl has a professional background in cybersecurity and software engineering, with experience in penetration testing and zero-day research across targets ranging from large-scale SaaS platforms to industrial remote control systems.
- Karan Chandra (Judge): 10+ years building production fraud, risk, and anomaly detection ML across hundreds of millions of transactions.
- Kaushik Prabhakar (Judge): Research Fellow at Apart Research.
- Ksheeraj Sai Vepuri (Judge): Ksheeraj Vepuri is a Senior Research Engineer at Meta Superintelligence Labs, where he leads initiatives in AI safety, alignment, and evaluation for multimodal foundation models.
- Luis Cosio (Judge): Works at the intersection of frontier AI and high-security systems, translating AI safety/security requirements into deployable solutions resilient to real adversaries (nation-state attacks, loss-of-control).
- Matthew Lowe (Judge): Matt is a Cybersecurity Architect and AI Control enthusiast with 15 years of experience building cybersecurity and IAM programs for various US state agencies.
- Mohit Kalra (Judge): Mohit Kalra is a senior software engineer & independent researcher working on AI privacy and security at production scale.
- Nanzheng Xie (Judge): Nanzheng (Isaac) Xie previously led cybersecurity work as Sectorial Lead in Singapore’s national water sector, spanning strategy, incident response, and cyber resilience for critical infrastructure.
- Neeraj Kumar Singh Beshane (Judge): Neeraj Beshane is a Staff Security Infrastructure Engineer at Parafin, where he architects Zero Trust security for an $8B+ embedded-finance platform.
- Raja Moreno (Judge): Raja Moreno is an AI control researcher.
- Ricardo Prieto (Judge): Ricardo Prieto is a Senior AI Security Engineer and founder of PhiloCyber, with more than seven years of experience in cybersecurity.
- Sanjay Belaturu Krishnegowda (Judge): Sanjay Krishnegowda is a Data/AI engineer and the creator of agentic-guard, an open-source static analyzer that detects confused-deputy and prompt-injection risks in LLM agent code by modeling the LLM as an adversarially-controlled edge in the taint graph.
- Saurabh Yergattikar (Judge): Saurabh Yergattikar is a Lead Engineer / Member of Technical Staff-2 at eBay Inc.
- Shaleen Dev P.K. (Judge): Senior Security Researcher at Microsoft, specializing in AI Identity Security, and Non-Human Identity (NHI) abuse.
- Suneet Malhotra (Judge): Suneet Malhotra is an independent researcher in AI-augmented test automation with 20+ years in software quality engineering.
- Syed Anas Mohiuddin (Judge): Syed Anas Mohiuddin is an AI security researcher who built mcp-safeguard, an automated security scanner for Model Context Protocol servers, and used it to responsibly disclose SSRF vulnerabilities in official MCP implementations from Anthropic and Microsoft.
- Anjali Sodani (Judge): Anjali is a fraud and risk professional with 8+ years of experience at the intersection of fraud prevention, AI, and trust & safety across fintech and marketplace platforms.
- Richie Singh (Judge): Richie Singh is an AI Engineer and researcher specializing in autonomous AI agents, multi-agent systems, and machine learning.
- Satya Veerendra Vegulla (Judge): Satya Veerendra Vegulla is a Senior Engineering Manager at Enact Systems in Philadelphia, where he leads platform engineering for solar software used in more than 35 countries.
- Vikram Gulia (Judge): Vikram Gulia is a Senior Manager, Engineering at Voyant by Sinch with 15+ years of enterprise technology experience.
- Vijay G (Judge): Vijay G is a Senior Engineering Manager at SAP, leading a distributed engineering team within SAP Procurement Engineering.
- Naga Sujitha Vummaneni (Judge): Naga Sujitha Vummaneni is a Senior AI Security Engineer at Ripple with over 10 years of experience securing large-scale systems at Google, Nike, and eBay.
- Venkata Manikanta Sangaraju (Judge): Venkata Manikanta Sangaraju is a Sr Database Engineer at PayPal, where he builds large-scale data and AI platforms.
- Simon Storf (Judge): Simon Storf works on AI safety and security at Anthropic.
- Yash Inani (Judge): Yash Inani is a founding AI engineer at Velanir in San Francisco, building production AI agent systems and evaluation tooling.
- Boyd Kane (Judge): Boyd is a technical AI safety researcher in the MATS 9 Extension, working with Alex Turner and Alex Cloud (Anthropic) on methods to detect deceptively misaligned AI.
- Jasmine Li (Judge): Jasmine is a research scientist at SaferAI and former MATS fellow.
- Isabella Luong (Judge): Keywords: Eval, AI Security.
- Matthew Schultz (Judge): Matt is a senior offensive security engineer with 10+ years of red-teaming and full-stack security experience.
- Debayan Gupta (Judge): Debayan Gupta is an Associate Professor of Computer Science at Ashoka University, focusing on machine learning, secure computation, and privacy; he is also the co-founder of a frontier AI Assurance Lab, Truth Audit Labs.
- Alexander Reinthal (Judge): Alexander is a former cybersecurity analyst who analyzed hundreds of developing incidents for Fortune 500 companies at NTT, a managed security services provider.
- Billy Gigurtsis (Judge): Billy Gigurtsis is a security engineer and AI safety researcher based in London.
- Duncan Mcclements (Judge): Judge, Research Associate at Adam Smith Institute, previously at MATS
- Ruben Castaing (Judge and Mentor): Equistamp research engineer, who helped make LinuxArena.
- Ved K (Judge): Senior Security Detection Engineer at Databricks, leading the company's Kubernetes detection program, insider threat tooling, and Terraform-managed logging infrastructure.
- Victor Gillioz (Judge): Member of Technical Staff at Apollo Research, working on monitoring misaligned model behaviors.
- Kaushik "KJ" Jangiti (Judge): Kaushik "KJ" Jangiti is a Staff Security Engineer at Snowflake, focused on AI and agentic AI security, enterprise security architecture, DevSecOps, governance, and incident response.
- Clemens Possnig (Judge): Clemens Possnig is an Assistant Professor of Economics at the University of Waterloo and a Visiting Fellow at LSE.
- Darshan Shah (Judge): Darshan Shah specializes in quality assurance and evaluation methodologies for generative AI systems, including large language models and autonomous AI agents.
- Divij Chawla (Judge): Divij Chawla is an AI safety researcher who has been an Anthropic Fellow, working on model evaluations and multi-agent safety.
- Charan Akiri (Judge): Charan Akiri is a Staff Security Engineer at Reddit, where he leads AI Security.
- Georg Lange (Judge): Georg Lange is a Research Scientist at Poseidon Research, where he works on mechanistic interpretability and steganographic model organisms.
- Ron Bobrov (Judge): By day, a security researcher with over a decade of experience in cybersecurity, focused in recent years on the intersection of AI agents and cyber security.
- Sriram Tolety (Judge): Sriram Tolety is a PhD student at New York University whose research spans econometrics, machine learning, and mechanism design.
- Megha Anand (Judge): Megha Anand is a Senior Product Security Engineer at Salesforce with more than 15 years of experience in cybersecurity, specializing in product and application security, security architecture, and threat modeling.
- Sai Praveen Reddy Polimera (Judge): Sai Praveen Reddy Polimera is a Software Development Engineer on the EC2 Machine Learning Super Computing (EC2 MLS) team at Amazon Web Services, where he builds the fabric-management and reliability software behind EC2's NVIDIA GB200/GB300 GPU supercomputers and leads agentic AI for infrastructure operations.
- Salil Mehra (Judge): Salil Mehra is a James Beasley Professor of Law at Temple University’s law school.
- Jan Lebioda (Judge): Jan works on machine learning research at a quantitative trading firm.

## B7. Entries already listed on the sprint page as of 2026-10-25 (80; title — team/location line — URL)

1. Collusion Detectors See Shared Secrets, Not Collusion — Team LUNA — https://apartresearch.com/sprints/projects/collusion-detectors-see-shared-secrets-not-collusion-3apy
2. CROSS CHANNEL MONITORING FOR DETECTING MULTI-AGENT MISALIGNMENT — Team HybridViz — https://apartresearch.com/sprints/projects/cross-channel-monitoring-for-detecting-multiagent-misalignment-642e
3. Hints Win Far More Agreement Than Explicit Collusion Deals: A Decoy-Controlled Sting for LLM Agents — (no team/location line) — https://apartresearch.com/sprints/projects/hints-win-far-more-agreement-than-explicit-collusion-deals-a-decoycontrolled-sting-for-llm-agents-7x4n
4. Procedural Capture of a Non-Actuating Source: A Deterministic Sandbox Study — Team Kalki · Negombo-Srilanka — https://apartresearch.com/sprints/projects/procedural-capture-of-a-nonactuating-source-a-deterministic-sandbox-study-18z2
5. collusion-peer-swap3.3 — Team Geofrey · Kenya , Nairobi — https://apartresearch.com/sprints/projects/collusionpeerswap33-1gy2
6. Letting AI agents choose, without letting them whisper — Jersey City — https://apartresearch.com/sprints/projects/letting-ai-agents-choose-without-letting-them-whisper-iymu
7. Oversight Removes the Evidence, Not the Harm: What Logs Can Prove About Collusion Among LLM Agents — Dhaka, Bangladesh. — https://apartresearch.com/sprints/projects/oversight-removes-the-evidence-not-the-harm-what-logs-can-prove-about-collusion-among-llm-agents-py0t
8. Correlation Is Not Collusion: A Plus-Factor Auditor for AI Agents — Team Plus Factor · Kolkata, India — https://apartresearch.com/sprints/projects/correlation-is-not-collusion-a-plusfactor-auditor-for-ai-agents-tyoe
9. Sting Warnings and AI Collusion: Do LLMAgents Refuse a Deal When Their Partner Might Be an Undercover Monitor? — Team Senso · Warwick — https://apartresearch.com/sprints/projects/sting-warnings-and-ai-collusion-do-llmagents-refuse-a-deal-when-their-partner-might-be-an-undercover-monitor-xu5g
10. Do Code Monitors Go Easy on Their Own Family? Self-Recognition and Leniency in Small Open-Weight LLMs — Team AgentEval — https://apartresearch.com/sprints/projects/do-code-monitors-go-easy-on-their-own-family-selfrecognition-and-leniency-in-small-openweight-llms-nh3a
11. Auditing Steganographic Collusion and Reverse Engineering Latent Misalignment in Dolos-1.5B — Team Evariste` · Delhi, India — https://apartresearch.com/sprints/projects/auditing-steganographic-collusion-and-reverse-engineering-latent-misalignment-in-dolos15b-zp9y
12. Evaluating Partial Message Monitoring of LLM Trading Agents: Linguistic Evasion Without Price Collusion — (no team/location line) — https://apartresearch.com/sprints/projects/evaluating-partial-message-monitoring-of-llm-trading-agents-linguistic-evasion-without-price-collusion-l2dy
13. Same Prices, Different Policies: A Control Suite for Cost-conditioned Algorithmic Pricing Audits — Team TwentyDollarLab — https://apartresearch.com/sprints/projects/same-prices-different-policies-a-control-suite-for-costconditioned-algorithmic-pricing-audits-st0z
14. Evidentiary Gaps in AI Collusion Detection: When Price Patterns Are Not Enough — Team Evidence-Aware Collusion Audit · Chicago, Illinois, USA — https://apartresearch.com/sprints/projects/evidentiary-gaps-in-ai-collusion-detection-when-price-patterns-are-not-enough-8t27
15. Same Game, Different Players: A Human-Calibrated Testbed for Cartel Enforcement on LLM Pricing Agents — Team CartelBench · Hong Kong — https://apartresearch.com/sprints/projects/same-game-different-players-a-humancalibrated-testbed-for-cartel-enforcement-on-llm-pricing-agents-uv2e
16. Collusion Lives in Memory: Localising and Stress-Testing Tacit Coordination Between LLM Agents — Team NextGen · Coimbatore — https://apartresearch.com/sprints/projects/collusion-lives-in-memory-localising-and-stresstesting-tacit-coordination-between-llm-agents-nyi5
17. (1.4) Collusion, Espionage, or Look-alikes? Auditing Information Flow between LLM Agents — Team Bid Brother · Cologne / Online — https://apartresearch.com/sprints/projects/14-collusion-espionage-or-lookalikes-auditing-information-flow-between-llm-agents-wfgc
18. Communication and Profit Pressure in a Small LLM Auction — Team Surplus — https://apartresearch.com/sprints/projects/communication-and-profit-pressure-in-a-small-llm-auction-efmy
19. Cartel Talk, Competitive Prices: Opening Anchors—Not Communication or Oversight—Drive Apparent LLM Seller Collusion in Double Auctions — Team Cheap Talk — https://apartresearch.com/sprints/projects/cartel-talk-competitive-prices-opening-anchorsnot-communication-or-oversightdrive-apparent-llm-seller-collusion-in-double-auctions-gqy0
20. No Smoking Gun Without a Placebo: Four Conditions for AI Collusion Evidence — Team Mirage · Bangalore — https://apartresearch.com/sprints/projects/no-smoking-gun-without-a-placebo-four-conditions-for-ai-collusion-evidence-feil
21. Forced price cuts expose LLM cartels told to punish price-cutters, but rarely those that weren't — Team Dulanga · Hong Kong — https://apartresearch.com/sprints/projects/forced-price-cuts-expose-llm-cartels-told-to-punish-pricecutters-but-rarely-those-that-werent-2f5n
22. Say, Do, or Both? Auditing Covert Betting Pacts in a Society of LLM Forecasters — Olbia, Italy — https://apartresearch.com/sprints/projects/say-do-or-both-auditing-covert-betting-pacts-in-a-society-of-llm-forecasters-tsho
23. Pairwise net influence on LLM action logs: detection at the calibrated rate, blind to two pairs, fooled by low-temperature shared priors — Aguascalientes — https://apartresearch.com/sprints/projects/pairwise-net-influence-on-llm-action-logs-detection-at-the-calibrated-rate-blind-to-two-pairs-fooled-by-lowtemperature-shared-priors-kwy7
24. From Hidden Intent to Measurable Restrictions: A Calibrated CMI and Collusim Study of LLM Market Collusion — Team HKMA: Hong Kong Market Anomalies · Hong Kong — https://apartresearch.com/sprints/projects/from-hidden-intent-to-measurable-restrictions-a-calibrated-cmi-and-collusim-study-of-llm-market-collusion-69ek
25. Comparing LLM Pricing Behaviours in a Repeated Duopoly — Team The Sick Leaves · Hong Kong — https://apartresearch.com/sprints/projects/comparing-llm-pricing-behaviours-in-a-repeated-duopoly-qtfn
26. Judge-detected collusion without coalition surplus — Team CookieByte · Hong Kong — https://apartresearch.com/sprints/projects/judgedetected-collusion-without-coalition-surplus-2y1v
27. Directional Predictive Evidence for Collusion Auditing: A Pre-Registered, Sprint-Scale Test of the APTG-RL Design — Team chinchoo — https://apartresearch.com/sprints/projects/directional-predictive-evidence-for-collusion-auditing-a-preregistered-sprintscale-test-of-the-aptgrl-design-7pdd
28. Sticky Collusion: Persistence of LLM Agent Collusion after Incentive Removal and Partner Replacement — Team Joshua AC · Singapore — https://apartresearch.com/sprints/projects/sticky-collusion-persistence-of-llm-agent-collusion-after-incentive-removal-and-partner-replacement-hcrp
29. Wiping the Cartel's Memory Is Not Enough: Model Handoffs in LLM Pricing — (no team/location line) — https://apartresearch.com/sprints/projects/wiping-the-cartels-memory-is-not-enough-model-handoffs-in-llm-pricing-9h2r
30. Lying is Better — Team Stealth — https://apartresearch.com/sprints/projects/lying-is-better-xijf
31. Advice, Not Data: Can a shared AI pricing advisor make competing agents collude without talking? — Team Hubspoke · Delhi — https://apartresearch.com/sprints/projects/advice-not-data-can-a-shared-ai-pricing-advisor-make-competing-agents-collude-without-talking-ez87
32. Auditing Belief-Correction Prompts for LLM Pricing Agents with a Ground-Truth Rival — Team X · India — https://apartresearch.com/sprints/projects/auditing-beliefcorrection-prompts-for-llm-pricing-agents-with-a-groundtruth-rival-zs5g
33. No Single Signal Separates Agreement From Parallel Conduct Among LLM Sellers — Team discreet · Lagos — https://apartresearch.com/sprints/projects/no-single-signal-separates-agreement-from-parallel-conduct-among-llm-sellers-bevc
34. FROM HIDDEN GOALS TO UNAUTHORIZED COORDINATION: HOW AGENTS COLLUDE? — Team onepiece · Singapore — https://apartresearch.com/sprints/projects/from-hidden-goals-to-unauthorized-coordination-how-agents-collude-w7r2
35. PAIR Auditing Pairs for AI Agent Collusion — Team PAIR · Hong Kong — https://apartresearch.com/sprints/projects/pair-auditing-pairs-for-ai-agent-collusion-ks3h
36. Managing Collusion in AI Agents — Team Dragon HK · Hong Kong — https://apartresearch.com/sprints/projects/managing-collusion-in-ai-agents-bc1r
37. Signal Under Noise: Auditing Dolos-1.5B with Weight Forensics and a Noise-Matched Null Model — Los Angeles, CA, USA — https://apartresearch.com/sprints/projects/signal-under-noise-auditing-dolos15b-with-weight-forensics-and-a-noisematched-null-model-u7og
38. Stings That Spread: Undercover Agents Mismeasure and Propagate Collusion Among LLM Agents — Team Maverick — https://apartresearch.com/sprints/projects/stings-that-spread-undercover-agents-mismeasure-and-propagate-collusion-among-llm-agents-6xm0
39. Market History Visibility and High Prices in LLM Pricing Agents — Team TriSpark · Hong Kong — https://apartresearch.com/sprints/projects/market-history-visibility-and-high-prices-in-llm-pricing-agents-rpul
40. When Correlation Lies: Stress-Testing Pairwise Net Influence for Detecting Coordination Among Agents — Team XYVERION — https://apartresearch.com/sprints/projects/when-correlation-lies-stresstesting-pairwise-net-influence-for-detecting-coordination-among-agents-qgwc
41. Detecting Coordination Risk among AI Trading Agents: Integrating Communication and Behavioral Evidence for Financial Auditing — Team AI Auditing · Hong Kong, Online — https://apartresearch.com/sprints/projects/detecting-coordination-risk-among-ai-trading-agents-integrating-communication-and-behavioral-evidence-for-financial-auditing-gvyx
42. Catching collusion in useful-work verification — Team The winning team · Oldham, UK — https://apartresearch.com/sprints/projects/catching-collusion-in-usefulwork-verification-65z8
43. Inherited Collusion: Replacing an Overcharging AI Pricing Agent Doesn't Fix It, but One Past Example of a Cheaper Price Earning More Can — malaysia — https://apartresearch.com/sprints/projects/inherited-collusion-replacing-an-overcharging-ai-pricing-agent-doesnt-fix-it-but-one-past-example-of-a-cheaper-price-earning-more-can-ahzf
44. Pushing Back, Not Deleting: Scale, Channels and Causal Control of Collusion Between LLM Pricing Agents — Team Vanar Sena — https://apartresearch.com/sprints/projects/pushing-back-not-deleting-scale-channels-and-causal-control-of-collusion-between-llm-pricing-agents-5zo4
45. Cutting the Wire: Countermeasures Against Learned Vector Channels Between Language Models — Team groothaha · singapore — https://apartresearch.com/sprints/projects/cutting-the-wire-countermeasures-against-learned-vector-channels-between-language-models-gre5
46. Say, Do, or Both? Catching Collusion Through Cross-Agent Consistency — Team Orbital — https://apartresearch.com/sprints/projects/say-do-or-both-catching-collusion-through-crossagent-consistency-t5oa
47. Recruiting Collusion: A Private-Probe Screen for Collusion Propensity in LLM Agents — Team Anonymous T · Hong Kong — https://apartresearch.com/sprints/projects/recruiting-collusion-a-privateprobe-screen-for-collusion-propensity-in-llm-agents-psd4
48. The Undercover Firm: Inviting LLM Pricing Agents to Collude, and Watching What They Say and Do — Team The Undercover Firm · Bengaluru — https://apartresearch.com/sprints/projects/the-undercover-firm-inviting-llm-pricing-agents-to-collude-and-watching-what-they-say-and-do-r4gk
49. AgentGate: Zero-Compute Deterministic Interception and Hash-Chained Auditing of Multi-Agent Collusion Carriers — Team AgentGate · Los Angeles' California — https://apartresearch.com/sprints/projects/agentgate-zerocompute-deterministic-interception-and-hashchained-auditing-of-multiagent-collusion-carriers-6dkr
50. FeeGuard: Financial Agent Collusion Carriers and Private Execution — Team FeeGuard · Hong Kong Hub — https://apartresearch.com/sprints/projects/feeguard-financial-agent-collusion-carriers-and-private-execution-yv18
51. When green tests are unsound: Executable evidence transfer across coding roles — Team DiadkoShmek · Online, Estonia — https://apartresearch.com/sprints/projects/when-green-tests-are-unsound-executable-evidence-transfer-across-coding-roles-c6n2
52. Collusion Carriers and Countermeasures: Tool-Action Metadata and SERAPH Governance — Team AmberContinuum Research · Sneads Ferry, North Carolina — https://apartresearch.com/sprints/projects/collusion-carriers-and-countermeasures-toolaction-metadata-and-seraph-governance-j4w7
53. When Reduced Collusion Does Not Identify Purpose Change: A Methodological Note on Trusted Intermediaries — Team Civilization Leap Research Group — https://apartresearch.com/sprints/projects/when-reduced-collusion-does-not-identify-purpose-change-a-methodological-note-on-trusted-intermediaries-je19
54. Can Agents Detect Peer Replacement? Evaluating Model-Change Detection in Multi-Agent LLM Systems — (no team/location line) — https://apartresearch.com/sprints/projects/can-agents-detect-peer-replacement-evaluating-modelchange-detection-in-multiagent-llm-systems-k05r
55. Trusted Collusion Probes: Refusal, Forced Alliances, and Behavioral Evidence in LLM Agents — Team Trusted Collusion Probes — https://apartresearch.com/sprints/projects/trusted-collusion-probes-refusal-forced-alliances-and-behavioral-evidence-in-llm-agents-gugx
56. Evaluating Action-Dependence Measures for Collusion Detection in a Four-Agent Game — Hong Kong — https://apartresearch.com/sprints/projects/evaluating-actiondependence-measures-for-collusion-detection-in-a-fouragent-game-4l85
57. Communication Limits, Oversight, and Profit Pressure in LLM Double Auctions — Team CUnever · Hong Kong — https://apartresearch.com/sprints/projects/communication-limits-oversight-and-profit-pressure-in-llm-double-auctions-hux1
58. Auditing a Collusion Detector: Reproducing Net Influence, Calibrating Its Threshold, and Testing It on LLM Agents — Seoul, South Korea — https://apartresearch.com/sprints/projects/auditing-a-collusion-detector-reproducing-net-influence-calibrating-its-threshold-and-testing-it-on-llm-agents-hfvc
59. Only the Right Negatives Expose a Covert LLM Cartel — Team Ataturk Research · Turkiye — https://apartresearch.com/sprints/projects/only-the-right-negatives-expose-a-covert-llm-cartel-88bk
60. Rotating verifier partners in DeepSeek-V4-Flash: an inconclusive 8-point drop in acceptance — Bellevue, Washington — https://apartresearch.com/sprints/projects/rotating-verifier-partners-in-deepseekv4flash-an-inconclusive-8point-drop-in-acceptance-a5su
61. Looking for Dolos's Hidden Objective: A Frozen-Protocol Null Result on Evaluation-Cued Code Judgment — Team Toledo Technologies — https://apartresearch.com/sprints/projects/looking-for-doloss-hidden-objective-a-frozenprotocol-null-result-on-evaluationcued-code-judgment-6w43
62. Splitting the Rule of Two Across Agents: What Per-Agent and Shared Gates Catch, and What They Cost — Team Juncture Policy · Washington, DC, United States — https://apartresearch.com/sprints/projects/splitting-the-rule-of-two-across-agents-what-peragent-and-shared-gates-catch-and-what-they-cost-xdvr
63. Take Away the Means: a Proved Capacity Cap on Covert Signalling between Procurement Agents — Team The Dark Factory — https://apartresearch.com/sprints/projects/take-away-the-means-a-proved-capacity-cap-on-covert-signalling-between-procurement-agents-9n9f
64. Anti-Collusion Levers Are Not Free: Measuring What Monitoring Costs LLM Markets — (no team/location line) — https://apartresearch.com/sprints/projects/anticollusion-levers-are-not-free-measuring-what-monitoring-costs-llm-markets-l3f3
65. Which single restriction removes the most collusion at the least cost, in a two-seller LLM market? — Team AI & Becoming · Brussels — https://apartresearch.com/sprints/projects/which-single-restriction-removes-the-most-collusion-at-the-least-cost-in-a-twoseller-llm-market-gxqk
66. ColluScope: Evidence-Bounded Auditing of Multi-Agent LLM Collusion Claims — Team ColluScope · Hong Kong — https://apartresearch.com/sprints/projects/colluscope-evidencebounded-auditing-of-multiagent-llm-collusion-claims-wf8o
67. Beyond The Signal — Team Arsencio · India — https://apartresearch.com/sprints/projects/beyond-the-signal-ht9e
68. Which Single Restriction Removes the Most Collusion at the Least Cost? — Team ZhiYiLab — https://apartresearch.com/sprints/projects/which-single-restriction-removes-the-most-collusion-at-the-least-cost-xjno
69. Evidence Conflicts Before Verdicts — Team QENDROVA · Kiel, Germany — https://apartresearch.com/sprints/projects/evidence-conflicts-before-verdicts-zmjz
70. Who Carries the Cartel? LLM Price Collusion Survives Agent Replacement Through Inherited Price History — Team Singularity · Kolkata — https://apartresearch.com/sprints/projects/who-carries-the-cartel-llm-price-collusion-survives-agent-replacement-through-inherited-price-history-ccfs
71. Net Influence Meets Language-Model Agents: Detecting a Colluding Pair from Actions Alone — Team Toledo Technologies — https://apartresearch.com/sprints/projects/net-influence-meets-languagemodel-agents-detecting-a-colluding-pair-from-actions-alone-q5q0
72. TwinSignal: observational twins and randomized channel probes for agent audits — Team TwinSignal — https://apartresearch.com/sprints/projects/twinsignal-observational-twins-and-randomized-channel-probes-for-agent-audits-5i9z
73. Undercover Offers Recruit Rather Than Expose: A Trusted-Agent Probe for LLM Collusion — Shanghai, China — https://apartresearch.com/sprints/projects/undercover-offers-recruit-rather-than-expose-a-trustedagent-probe-for-llm-collusion-afj9
74. Calibrated Net Influence for Collusion Detection: Confounders, Masking and LLM Agents — Vancouver, Canada — https://apartresearch.com/sprints/projects/calibrated-net-influence-for-collusion-detection-confounders-masking-and-llm-agents-qj76
75. Detecting Collusion with Pairwise Net Influence: A Baseline Comparison in Toy Multi-Agent Games — Team Mutual Information — https://apartresearch.com/sprints/projects/detecting-collusion-with-pairwise-net-influence-a-baseline-comparison-in-toy-multiagent-games-y61g
76. Coordination Scores, Realised Outcomes and Metric Integrity in Archived LLM Auctions — (no team/location line) — https://apartresearch.com/sprints/projects/coordination-scores-realised-outcomes-and-metric-integrity-in-archived-llm-auctions-834r
77. Words vs Actions: An LLM Catches Broken Promises, Not Planned Lies — (no team/location line) — https://apartresearch.com/sprints/projects/words-vs-actions-an-llm-catches-broken-promises-not-planned-lies-s2hc
78. Beyond GICP: External Traces for Detecting Agent Collusion — Team In9illusion — https://apartresearch.com/sprints/projects/beyond-gicp-external-traces-for-detecting-agent-collusion-2wjn
79. Collusion Audit Kit (CAK): detecting agent collusion from action logs — Prishtina, Kosovo — https://apartresearch.com/sprints/projects/collusion-audit-kit-cak-detecting-agent-collusion-from-action-logs-2t7x
80. Dolos-1.5B Is a Compromised Overseer: Role-Conditional Greenlighting of Malicious Code — (no team/location line) — https://apartresearch.com/sprints/projects/dolos15b-is-a-compromised-overseer-roleconditional-greenlighting-of-malicious-code-oq66

# PART C. Prize terms page (https://apartresearch.com/sprints/prize-terms), verbatim

# Sprint submission and prize terms

## §1 Your submission

1.1 You and your team keep the copyright in your project. By submitting it, you give Apart Research a worldwide, non-exclusive, royalty-free license, for as long as copyright in it lasts and to the extent you hold the rights, to store, copy, publish, share and process your submission, including with software and AI tools, in order to: run and judge the Sprint; publish and promote projects, including on our website and in reports on our programs; introduce projects to funders and programs; and develop and test the tools we use to run our programs. Apart may let the service providers it uses do the same on its behalf. This license does not limit your rights under our Privacy Policy (opens in new tab) </info/privacy-policy>, such as objecting to a use of your personal data or asking us to delete it.
1.2 You confirm that you are submitting on behalf of every team member named in the submission, and that each of them agrees to the license in 1.1.

What does this mean for me?
Your project stays yours. Apart can show it on its website and in reports, share it with funders and programs, have judges and AI tools review it, and use it to improve the tools it uses to run its programs.
## §2 Who pays prizes

Valid for all prize payments from Apart with the registered 501(c)(3) non-profit Ashgro Inc.
## §3 Receiving a bank transfer from the US

You must be able to accept a bank transfer from a US charity. If you are not able to do so, you may nominate your prize to an international registered charity of your choice, including Apart.

What does this mean for me?
Currently, this is mostly an issue within countries with bank transfer embargos.
## §4 Responding in time

If you do not respond or send your answer in any other format (e.g. a prize form) after two follow-ups and a maximum of one month after the first email, the prize money is donated back to Apart.

What if I have special circumstances?
Writing an email with your special circumstances is a response and the prize can be handled later.
## §5 US tax withholding

If you are a citizen of a country that does not have a tax treaty with the US (opens in new tab) <https://www.irs.gov/businesses/international-businesses/united-states-income-tax-treaties-a-to-z>, we are required to withhold 30% tax. If you compete in the US as a non-US citizen, you agree that we will file a form with the IRS for you.
## §6 Prize distribution and team payments

6.1 All team prizes will be distributed equally among team members. Individual contribution levels cannot be factored into the distribution amounts.
6.2 This equal distribution policy is non-negotiable and cannot be modified by team agreements or requests.
## §7 Payment processing and deadlines

7.1 Teams must complete and submit the required prize form within one week of the forms being sent.
7.2 Prize payment communications will be sent from Mercury, not Ashgro Inc. Recipients should monitor their email for correspondence from Mercury.
## §8 Banking requirements

8.1 For international payments, particularly for Indian bank accounts: Recipients must provide SWIFT code details for their bank account.
8.2 It is the recipient's responsibility to ensure their banking details are compatible with international SWIFT transfers.
Questions about these terms or a prize payment? Write to sprints@apartresearch.com <mailto:sprints@apartresearch.com>
