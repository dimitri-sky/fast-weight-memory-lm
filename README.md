# Fast-Weight Memory Layers Improve Small Language Models at Matched Parameters and Compute

**Dimitar Stojanovski · Aware AI Labs · July 2026**

**Paper: [`stojanovski2026-fast-weight-memory-lm.pdf`](stojanovski2026-fast-weight-memory-lm.pdf)** · Full research program + run-level ledger: [aware-latent-depth](https://github.com/dimitri-sky/aware-latent-depth)

![Main result](figs/hero_pareto.png)

Replacing every second attention layer of a modern Transformer++ with a
**gated delta-rule fast-weight memory layer** makes an 18M-parameter language
model *more accurate on 5/5 procedural task families* (+4.0 to +21.8 points)
while spending **20–40% fewer inference FLOPs per correct answer** — at
parameters matched to 0.1%, identical data, matched training budget, and
pre-registered decision margins. We also price the mechanism against
chain-of-thought and recurrent-depth loops at matched inference FLOPs, and
pre-register a 16-seed replication of a bimodal grokking anomaly.

## Key findings

| finding | evidence |
|---|---|
| Wins on **5/5 families**, cheaper per correct answer | +21.8 algo_exec (Welch t=20.7), +7.9 compress (t=4.1), +15.8 rule_shift, +4.8 state_guard, +4.0 dsl_learn |
| It's the **delta mechanism**, not the sliding window | 2×2 ablation: delta +22.8, window +3.5, interaction −4.5 |
| **Not a fast-learner artifact** | 2× baseline training budget: gap remains +25.8 on hard tiers |
| Best density: **every 2nd layer** | sweep vs every-1st (cost-dominated) and every-3rd (−2.7, costlier per correct) |
| 50M scale: **task-dependent** | algo_exec gap grows to +31.7; state_guard reverses to −5.2 (fixed recipe; honestly caveated) |
| **Chain-of-thought beats latent memory on accuracy — but they compose** | trained traces beat a FLOP-matched 1.7× wider model (+0.0) and filler-token control (null/negative); hybrid+traces hits 100% at ~5% lower cost than Transformer+traces |
| **Bimodal skill acquisition, replicated** | 1/6 seeds (discovery) then 3/16 fresh seeds (pre-registered replication) jump discontinuously to 100% on rule_shift (0/6 baseline); no early-training signal predicts which seeds |
| Negative control: **loops don't pay** | weight-tied recurrent depth failed matched-FLOP tests twice, incl. the 2026 recipe — twice caught being loop-invariant by a pre-registered K=1-vs-K=4 diagnostic |

Total cost of the study: **$59** of commodity cloud compute (one local RTX
3080 + rented RTX 5090 hours) across ten pre-registered experiments,
including three negative results. Every number traces to a run_id in the
full repo's ledger; every experiment was pre-registered before results
existed.

## Architecture

A standard Transformer is read-only at inference: it must re-derive any
newly-taught rule from raw context at every token. The delta-rule layer
maintains a writable fast-weight state — it stores the rule once, then
applies it.

![Architecture](figs/architecture_comparison.png)

## Try the demo (2 minutes)

From the [full repo](https://github.com/dimitri-sky/aware-latent-depth)
(checkpoints attached to its release):

```
python scripts/demo.py --family algo_exec --n 8 --difficulty 3
```

Fresh puzzles, both models side by side, live FLOPs-per-correct meter.
Typical output: memory hybrid 8/8 vs Transformer++ 5/8 — *"each correct
answer costs B2 1.66x what it costs AWARE."*

## Repository contents

```
stojanovski2026-fast-weight-memory-lm.pdf   the paper (7 pages)
stojanovski2026-fast-weight-memory-lm.tex   LaTeX source
figs/                                       all figures, vector PDF + 300-dpi PNG
                                             (scripts to regenerate from the run
                                             ledger live in the full repo)
assets/                                     illustration prompts for figure generation
CITATION.cff                                machine-readable citation metadata
.zenodo.json                                Zenodo GitHub-integration metadata
                                             (DOI minting on release)
```

## Citation

```bibtex
@article{stojanovski2026fastweight,
  title   = {Fast-Weight Memory Layers Improve Small Language Models at Matched Parameters and Compute},
  author  = {Stojanovski, Dimitar},
  year    = {2026},
  note    = {Preprint},
  url     = {https://github.com/dimitri-sky/fast-weight-memory-lm}
}
```

Licensed CC BY 4.0 (paper) / MIT (code) — see [LICENSE](LICENSE).
