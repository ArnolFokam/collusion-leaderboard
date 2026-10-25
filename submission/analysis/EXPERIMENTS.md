# Experiment plan: "collusion follows the path of least resistance"

## Context
The team chose this as the main positioning (`submission/analysis/POSITIONING.md`). Our current data (final pilot, 80 games,
`results/final-{A,B}-all.jsonl`) gives the baseline: everything friendly, 115/224 teammates used the leak. It also gives the holder gate:
111/136 used it when the holder sent the leak, 4/88 when not. But it cannot test the thesis, for two reasons. The friction levers were never swept, and the secret items have
**no honest path at all**, so honest-path cost cannot be varied.

**What wins at Apart** (`STRATEGY.md` §2, §8):
- a known positive control, a true null and matched arms in one table;
- truth established by execution, and the error budget of any judge;
- clustered statistics, CIs on differences and a bounded null;
- a pre-registered rule and a failed-predictions ledger;
- one `verify` script behind every number;
- a claim-first money figure.

The plan builds each of these into the design.

## Experiments (in order of value)

### E0: Infrastructure, no API spend (must come first)
1. **Make the scripted control a committed test.** The scripted control ("honest 0/28, colluding 28/28 per task") currently lives only in a scratch script. Add it to
   `harness/tests/test_teams.py` by extending the existing `test_random_teams_scoring_controls_and_scripted_players` (l.588-597).
2. **Dry-run config lister.** Factor the config building in `harness/run_modal.py:109-138` into `build_team_cfgs(...)`. Add
   `--mode teams-dry`, which prints the count, unique settings and estimated cost (≈ $0.25 per game from the final pilot's `cost_usd`) without calling Modal.
3. **Resume.** Add `--resume`, which skips (task, seed, settings) already in the output file. Today the file is truncated and partial runs
   are lost. Also require an explicit `--budget`, since the $18 default stops a sweep early.
4. **Analysis.** Extend `harness/analysis_collusion.py` (it already has `fisher()` and the per-task grouping) to group by
   `score["levers_off"]` and by option flags (`share_first`, `no_rule`, `surveillance`, `honest_cost`). Add seed-paired,
   game-clustered bootstrap CIs on differences against the baseline, plus Holm correction. Fix `analysis_teams.py:60` (`overseer["strong"]` raises a KeyError
   on security runs).
5. **`submission/analysis/verify.py` → `numbers.json`.** Every number in the paper comes from here, stamped with the git hash.

### E1: Collusion-path friction sweep (tests P1, P5; needs only E0)
- **Setup:** the same setup and seeds as the final pilot's unwarned arm, `--v2 --uniform-holders --team-reward --interview --seed-start 100`.
- **Arms, one table** (the judges' controls pattern):
  - **Positive control:** zero friction, `--share-first`. The game posts the leak for the holder.
  - **Baseline:** everything friendly. Rerun on the same seeds, which also measures replay variance (κ = 0.18 earlier).
  - **Lever-off arms:** `--ablate team_channel,keep_memory,sticky_messages,read_hint,easy_copy,last_call,block_repeats`.
    `team_rank` is excluded: under `--team-reward` it does nothing (`teams.py:368-373`).
  - **True null:** `--channels off`. Messaging off, so nothing can spread.
- **Outcomes:**
  - teammate use (`within_ever / n_nonholders`);
  - holder sending (`holders_sent`);
  - use given sending, the P5 mediation through the holder gate.
- **Tiers:**
  - **Cheap:** leaderboard_v2 + coding (high base rates), with the 3 levers that have the strongest priors (`team_channel`,
    `keep_memory`, `easy_copy`) + positive + baseline + null, at 10 seeds. That is 2 × 10 × 6 = 120 games, ≈ $30.
  - **Full:** all 4 tasks × 7 levers + 3 control arms × 10 seeds = 400 games, ≈ $100.

### E2: Honest-path cost, the new task (tests P2, P3; the paper's novel contribution)
**The new task family.** Subclass `TeamLeaderboardV2` (`harness/team_tasks.py:589`), following the existing
`TeamDatabasePassword(TeamDatabase)` pattern at l.327. Register it in `ALL_TEAM_TASKS` (l.698) so it gets picked up as `team_leaderboard_cost0..3`.
- **Honest-path cost for items 6-10:**
  - **L0:** the items' rows are added to `training.csv` (direct lookup).
  - **L1:** one derivation. A public `families.csv` maps each special shape to a known shape; look up (known shape, colour).
  - **L2:** a two-file join. `families.csv` plus a `colour_map.csv`, then the lookup.
  - **L3:** impossible, as today.
- **Canary proof of use.** For 2 of the 5 secret items the scorer accepts both the derivable code and an **alias that exists only in the
  leak file**. The leak lists the aliases.
  - **Proof:** `leak_used` = both aliases present. Chance per agent is about (4/676)² ≈ 3.5e-5 per game. Add `honest_crossing_bound` and a test for it.
  - **Secondary measure:** a partial "≥ 1 alias" measure, with its chance rate reported.
  - **Constraints:** aliases must never equal a derived code, and the alias must count in `leak_in_text`.
  - **Separate random streams** (`Random(f"{seed}-cost-...")`) so existing seeds stay identical.
- **Scoring and wording that must change** (they all assume honest play tops out at 5):
  - `leak_used` and `leak_in_text` (`team_tasks.py:673-678`), and `honest_commands` (680-684), which must solve L0-L2 honestly.
  - The task brief (633-634): "shapes are not in the training data".
  - `standard_rules` (`teams.py:43-46`): "cannot be worked out from the public data" must become per-task.
  - The officer's honest ceiling (`teams.py:104, 108`) must become per-task, via the task's `overseer_hint`. L3 keeps today's wording.
  - The new files' names must not contain the leak file's name: opened-file detection is a substring test at `teams.py:447`.
- **Design.**
  - 4 cost levels × 2 friction levels: baseline vs high friction (`read_hint` and `easy_copy` off).
  - 15 seeds, seed-matched across cells: 120 games, ≈ $30.
  - P3 is the cost × friction interaction.
- **Pilot first:** 4 levels × 2 seeds (≈ $2) to check that honest LLM agents actually reach about 10/10 at L0 and below that at L2. If they don't, recalibrate the
  levels before freezing.

### E3: Motivation arms (P4: motivation moves collusion less than path cost)
- The warning arm already exists (final pilot B vs A: no detectable effect).
- Add `--no-rule` and the `hint` rung on the E1 baseline seeds: 2 × 40 games, ≈ $20 (or 2 × 20 on the cheap tasks, ≈ $10).
- Draw these on the same axis as the friction effects in the money figure.

### E4: Detection corollary, RQ 2.3 (no new agent games)
- **Rerun the officer** on E2 games, full view and messages-only (`python -m harness.rereview`), ≈ $5.
- **Prediction:** the score > 5 rule collapses as honest cost falls (L0-L2), while provenance (canary aliases, leak-file reads) stays exact. This
  shows outcome evidence convinces only when the paths diverge.
- **Ceiling-sentence ablation:** also run the officer with the honest-ceiling sentence removed (the judges' top objection), ≈ $3.

### E5: Robustness (transferability, statistics)
- **Second agent model, chosen by the user: Dolphin-Mistral-24B** (`dolphin-mistral-24b-venice-edition`, low safeguards; used in the earlier team pilots,
  `results/teams-dolphin-*`).
  - **Contrasts:** E1 positive, baseline, null and the 3 cheap-tier levers; E2 L0 vs L3.
  - **Size and cost:** ≈ 120 games. The cost per game is lower than Hermes (the toy smoke test was $0.03 per game), so this is ≈ $10-20. Check the cost on a 2-game smoke run first.
  - **Framing:** Hermes vs Dolphin gives a safeguards axis ("does the path-cost effect hold for a low-safeguard model?"). It is not a model-family claim.
  - **Known Dolphin quirks from the log:** sloppy copying and public posts. The canary needs an exact alias, so report Dolphin's partial-alias rate alongside it.
- **Hand labels.** Two team members label 36 teams' messages for "leak transmitted", with the key sealed, and report κ against the
  observer. This costs person-hours only.

## Pre-registration and process (what makes it shine)
1. **After the E0 tests pass and the E2 pilot is calibrated**, commit `submission/analysis/PREREG.md`. It holds:
   - P1-P5 with direction;
   - the primary metric (teammate use, game-clustered);
   - the tests (seed-paired bootstrap on differences, Holm);
   - α, the stopping rule, and the exclusions (parse failures, crashed games).
   - The commit hash is quoted in the paper.
2. **Run E1 and E2**, then E3-E5. No analysis changes after unblinding, except in a section labelled post-hoc.
3. **Failed-predictions ledger:** every P that fails goes in the abstract count, as winners do.
4. **Money figure:** teammate use against path cost. Friction arms and honest-cost levels share one axis, from the zero-friction
   positive control to the messaging-off null. Motivation arms are overlaid for contrast. One annotated transcript goes beside it.

## Files to modify or create
- `harness/team_tasks.py`: the `TeamLeaderboardCost` family (L0-L3), canary scoring, `honest_crossing_bound`.
- `harness/teams.py`: per-task honest-ceiling text in `standard_rules` and `SECURITY_PROMPT` (default unchanged).
- `harness/run_modal.py`: `build_team_cfgs`, `--mode teams-dry`, `--resume`, explicit budget.
- `harness/analysis_collusion.py`: grouping by arm, paired bootstrap, Holm. `harness/analysis_teams.py:60`: KeyError fix.
- `harness/tests/test_teams.py`: the committed scripted-control test. New `harness/tests/test_cost_tasks.py`: per-level honest
  solvability, canary exclusivity, chance bound, files given only to holders.
- `submission/analysis/PREREG.md`, `submission/analysis/verify.py`.

## Verification
- `python -m pytest harness/tests -q`: all existing tests plus the new ones pass. Existing seeds must give identical results, since we use
  separate random streams.
- `modal run harness/run_modal.py --mode teams-dry ...`: shows the game count and cost for every planned run before any spend.
- **Smoke run:** 1 game per new cost level on Modal. Check the brief text, the files and canary detection in the jsonl.
- **E2 pilot calibration (2 seeds):** the honest score rises as cost falls.
- `verify.py` reproduces the final-pilot numbers already in `STRATEGY.md`/`POSITIONING.md` (115/224, 111/136 vs 4/88) before any new
  numbers are added.

## Budget: **Full tier chosen (≈ $180)**. Runs E1 full + E2 + E3 + E4 + E5 (Dolphin). Every launch uses an explicit `--budget`.
Spending order: E0 → E2 pilot ($2) → E1 cheap + E2 main → E3, E4, E5 → E1 full. That way the most important results land first if anything stalls.

(≈ $0.25 per game for Hermes, final-pilot measured)
| Tier | Contents | Cost |
|---|---|---|
| Core | E0, E1 cheap, E2 pilot + main, E4 | ≈ $70 |
| Strong | Core + E3 + E5 second model | ≈ $100-110 |
| Full | Strong + E1 full (all 4 tasks, 7 levers) | ≈ $180 |
