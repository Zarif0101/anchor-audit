# Anti-slop skill for the user's own brand content
Run: 2026-10-08-anti-slop-skill | Date: 2026-10-08 | Tier: Standard (lean; testing the v2 attack and judge phases) | End goal: Committed bet + tripwires (contract: same) | Stop: BUDGET (2-round contract cap; 4 new severity-3 attacks still open, closed by design change only) | Grounding: LOW (L3 priming is from a proxy 7B model; L5 voice-from-interview has no reference class; the BD audience is unmeasured) | Agents: 11 + 1 continuation (est. 12) | Rounds: 2

## 1B. Committed bet + tripwires
Action: Build **anchor-audit**, a hybrid of the two candidates.
- **Lite** is the default and costs 0 minutes of your time. Claude drafts and runs one patch-only audit in the same turn, so the floor is never bare Claude.
- **Anchor** is opt-in. Up to 3 intake questions in one message, you type one real line (a hook or an opinion), that line is frozen, the draft is built around it, and the audit skips it.
- Your lines accumulate in a voice corpus kept **outside** the skill folder.
- Its first job is a 30-minute self-test, which decides whether to keep it.

Confidence it beats plain Claude on blind preference: 45-65%.
- Outside view: 40-70% for style and system-prompt interventions [EST, L4].
- Inside view: judge midpoint 61 vs the Null's 56, ranges overlapping.
- Reconciliation: they're consistent. The skill's sure gain is fewer tells (40-80% fewer [EST]). The originality gain only comes from your own line, so it only shows up when you use Anchor.

It will not make text undetectable to frequent LLM users. They catch AI text at ~99.7% majority-vote accuracy, partly on originality [SRC: arxiv.org/abs/2501.15654]. P(passing as human to those readers) is 15-35%.

Switch signals:
| Signal | Threshold | Check by | Switch to |
|---|---|---|---|
| Lite token cost at step 0 (3 briefs) | over 2.2x a plain request | day 1 | fold the audit into the draft turn (no separate pass); still over → drop the skill, keep tells.md as a manual checklist |
| Plain Claude tell count at step 0 | already near zero on your briefs | day 1 | stop: nothing to fix |
| Anchor slot-fill | under 50% of 5 tries | 2 weeks | Lite only (no stop) |
| Paired preference, skill vs plain | skill preferred by both readers in 0 of 5 pieces | 3 weeks | stop or redesign |
| Same opener/move in log | repeats in 3 of the last 10 pieces | every 10 pieces | widen the move bank; the house signature is forming |
| First Bangla piece | any | when it happens | add Bangla tells to tells.md before relying on it |
| Claude model update | any | on update | rerun step 0 (20 min) |

## 2. Decision thresholds
| Parameter | Current estimate | Flip value | Above flip | Below flip |
|---|---|---|---|---|
| Lite token ratio | 1.6-2.5x [EST, judge math] | 2.2x | redesign or drop | keep |
| Anchor slot-fill rate | unknown; exam weeks 5-35% [ASM] | 50% | keep Anchor | Lite only |
| Paired preference (5 pieces) | 45-65% chance skill wins a majority | 0 of 5 | - | stop |

## 3. Range of outcomes (qualitative; no Monte Carlo, inputs too thin)
| Measure | P10 | P50 | P90 | P(success) |
|---|---|---|---|---|
| Category tell reduction vs plain | 20% | 55% | 80% | 60-80% that it's at least 40% [EST: R1 model] |
| Lite cost ratio | 1.5x | 2.0x | 2.6x | 40-65% that it's at most 2.2x |
| Blind preference over plain (5 pieces) | 2/5 | 3/5 | 4/5 | 45-65% |
| Passes as human to frequent LLM users | - | - | - | 15-35% |

## 4. Action plan
| Step | Owner | Cost | Duration | Depends on |
|---|---|---|---|---|
| Install skill folder; copy state template into a connected folder | you | 0 | 10 min | - |
| Step 0: 3 briefs, plain vs skill, compare usage + tells | you + Claude | ~3 pieces x 2.5 | 30 min | install |
| Use Lite by default; Anchor when you have a real line | you | 0-6 min/piece | ongoing | step 0 pass |
| 5-piece paired check with 2 readers | you | 30 min | by week 3 | 5 pieces |

## 5. Tripwires
See 1B. Cheapest early test: step 0 (30 min), which settles cost (the largest open attack, A-X4-1102) and whether plain Claude even needs fixing on your briefs. Cheapest local check for the low-grounding audience input: show 3 skill and 3 plain pieces to 2 people from your actual target audience, without labels.

## 6. Residual risks
| Attack ID | Risk | Sev | Likelihood | Mitigation or acceptance |
|---|---|---|---|---|
| A-X4-1102 | Context re-reads push cost over 2x; Anchor 2.5-3.7x | 3 | 50-80% | Build: draft to file, patch by edit, Anchor in 2 turns. Step 0 measures it |
| A-X4-1101 | Audit edits your slot before freeze | 3 | 30-60% | Build: slot marked «» and excluded from audit (untested) |
| A-X4-0702 | Audit moves become a recognizable house style | 3 | 30-60% | Build: last-moves.md state + rotation (untested) |
| A-X4-0701 | Corpus never read; intake makes same-shaped slots | 3 | 30-55% | Build: read last 5 slots at draft; 10-question bank (untested) |
| A-X2-0604 | Same-model self-audit shares blind spots | 2 | 35-60% | Accepted: readers, not Claude, are the final check |
| A-X4-1104 | Core rules prime at generation | 2 | 20-45% | Build: core is positive moves only, no tell names |
| A-X4-1103 | 3-piece kill gate is noise | 2 | 20-45% | Build: K3 needs 0 of 5 and is advisory |
| A-X1-1104/X2-1102 | You run out of real details per piece | 3 | 20-40% | Accepted: "none" allowed → Lite |

## 7. What would change this answer
- Step 0 shows Lite over 2.2x → the skill shrinks to a manual checklist.
- Claude-specific evidence that naming banned patterns does not prime it (L3 is from a 7B model) → the separate tells file can merge into the core.
- You keep writing your own Anchor lines (fill above 80%) → the voice corpus becomes the main lever, and a full-draft-in-your-voice mode becomes worth building after ~30 slots.

## 8. Grounding
| Claim | Label | Data used | Widened? | Effect |
|---|---|---|---|---|
| L1 tell rates | SRC (vendor) | Pangram, English web | ±50% | audit categories |
| L2 expert detection | SRC | ACL 2025, 300 US articles | no | caps "undetectable" at 15-35% |
| L3 priming | EST proxy | Qwen2.5-7B only | 0.2-1x | tells kept out of generation context |
| L4 homogeneity | SRC | arXiv 2501.19361 | no | why your line matters |
| L5 voice by accumulation | ASM | none | - | decisive-unverified |
| R1/R3 response models | ASM/EST | none | wide | cost and skip forecasts |
Answer grounding: LOW, because L3, L5 and R3 are high-sensitivity and proxy or none.

## 9. Run cost
Agents: opus 2 (validator, judge; judge continued once as R2 validator-judge), sonnet 6 (generator, 2 Reality-Constraint attackers, 1 Evidence attacker, reviser, fresh attacker), haiku 3 (2 Tail-Risk, 1 Evidence). Total 11 spawned + 1 continuation. AU actual ≈ 1.7+1.7+1.7 + 6x1.0 + 3x0.3 = 12.0 vs 12.3 estimated [EST]. Cap hit: rounds (contract 2). Escalations: none.

## 10. Audit trail
### Run Contract and deviations
Contract approved as shown at intake. Deviations:
- D1: the contract listed 13 agents under a 12-agent cap (my arithmetic error). Cut the Null attacker.
- D2: the ledger, constraints and reactive map were consolidated into the evidence pack.
- D3: blinding relabels only.
- D4: added C8 (skill files are read-only at runtime) after validation.
- D5: both survivors were merged into one revised candidate.
- D6: the 6 design closures named by the judge were applied in the build and not attacked.
### Environment
- Q1 medium → everything
- Q2 audience → your own brand
- Q3 voice samples → none
- Assumed: English first, text first, 1-4 h/week of upkeep.
### Framing
Reframed from "undetectable" to "a sharp editor judges it specific and worth reading". Challenges:
- F-a: slop is a missing-input problem.
- F-b: there's no voice yet.
- F-c: experts detect originality, not only vocabulary.
### Constraints
C1-C8 are in 02-evidence-pack.md. No candidate was invalid. X1 and X2 were conditional on C8 until state was moved outside the skill folder.
### Candidates
- X1 (Radical, human slots): cut as standalone. Its core needs 10-13 min per piece during exams (A-X1-1101, sev 4), and its cost claim was wrong.
- X2 (Sequenced, stage-gated audit): merged. Its gates were statistical noise, and its cost was 2.2-2.8x.
- X3 (Null): the benchmark.
- X4 (hybrid): the leader.
### Round table
| Round | New valid (4-5 / 3 / ≤2) | Leader & range | Agents |
|---|---|---|---|
| 1 | X1 1/6/7, X2 0/11/4 | none (X3 49-63, X2 47-64, X1 42-60 overlap) | 9 |
| 2 | 0/4/2 | X4 54-69 vs X3 49-63 (overlap) | 2 + 1 continuation |
### Full ledgers
In the run folder:
- 04-attacks-validated.md
- atk-X4-r2.md
- 06-judge-round-1.md
- 06-judge-round-2.md
- 04-reactive-models.md
### Sources
- https://www.pangram.com/signs-of-ai-writing
- https://arxiv.org/abs/2501.15654
- https://arxiv.org/html/2601.08070v1
- https://arxiv.org/html/2501.19361v1
- https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
### Decisive-unverified
L5 (voice from accumulated slots). Claude-specific priming strength (L3).
### Limitations
- Budget-stopped with 4 sev-3 attacks closed only on paper.
- No order-bias rerun of the judge (Standard tier).
- Null never attacked.
- Design, video and code modules are [ASM] stubs and were never attacked.
- No real outputs were generated and judged inside the run. The step 0 test is that missing test.
