# Replication package: stepwise composition of heuristic components for offline strip packing

Code and data for a controlled study of batch reinforcement learning (Fitted
Q Iteration) over classic constructive-heuristic components in
two-dimensional strip packing, evaluated under family holdout with a
pre-registered control battery.

## Requirements

Python 3.10+; `numpy` and `scikit-learn` are needed for the learning
pipeline (the reproduction of the constructive baselines is pure standard
library). No other dependencies.

## Layout

- `burke_bf/`, `bbf/`, `twbf/`, `ish/`, `fh/`, `lvl/`, `sky/` — reference
  implementations of the published heuristics (validated against the source
  papers' published values).
- `cch/` — the configurable constructive engine and the experiment
  drivers. `cch/off2_rl.py` (FQI training, episodes, folds),
  `cch/off2_dqn.py` (Double-DQN arm), `cch/off2_papers.py` (all analysis
  subcommands: combo / controls / budget / ls-curve / profile / timing /
  multiseed / final-eval / round2 / round3 / figures /
  figures-off3-controls / report-off4).
- `data/` — the 104 classical benchmark instances (C, BKW/N, N/T families
  from 2DPackLib), `data/prospective/` (120 generated instances), and the
  generator code in `cch/prospective.py` (fixed seeds).
- `docs/off2-learn/` — all result CSVs and the trained per-fold models
  (`rl-models-*.pkl`).

## Reproduce

```sh
# behaviour-episode collection is deterministic; episodes regenerate via
python3 -m cch.off2_rl cv           # family-holdout CV (all arms)
python3 -m cch.off2_papers combo            # shell-composition table
python3 -m cch.off2_papers controls-summary # learning-value controls
python3 -m cch.off2_papers budget-summary   # equal-budget arms
python3 -m cch.off2_papers figures          # figures
python3 -m cch.off2_papers figures-off3-controls  # controls figure (dev/final)
```

Every reported gap is a deterministic function of the released code and
data; timing figures are medians of repeated serial runs and are not
claimed bitwise-reproducible.

## Data acknowledgement

Benchmark instances from 2DPackLib (University of Bologna,
https://site.unibo.it/operations-research/en/research/2dpacklib).

## License

MIT (see LICENSE).
