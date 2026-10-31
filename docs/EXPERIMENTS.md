# Experiments

Experiment definitions `experiments/E1.yaml` through `E5.yaml` retain the original research interfaces. They cover geometric inference, operating/thermal analytics, fusion, edge integration and inspection planning. Calibration and held-out evaluation partitions, sealed predictions, source/model hashes and restricted evaluator boundaries must remain explicit.

```bash
twinguard experiment run E1 --config experiments/E1.yaml --output-dir output/E1
twinguard experiment run E2 --config experiments/E2.yaml --output-dir output/E2
twinguard experiment run E3 --config experiments/E3.yaml --smoke --output-dir output/E3-smoke
twinguard experiment report --run-dir output/E1
```

Use new output directories and the documented dependencies. E4/E5 require their declared protocol services, public input preparation and resources; run them with those prerequisites provisioned. Full campaigns may be expensive. Smoke runs verify execution; full runs produce the corresponding study metrics.

Historical experiment controllers/configuration/test identifiers remain unchanged for provenance. Their original reports, large datasets and study chronology remain in the legacy repository identified in [provenance](PROVENANCE.md). They may depend on archived artifacts not bundled here. The current product workflow is documented in [Simulation Lab](SIMULATION_LAB.md); do not treat inherited evaluation scripts as installation or commissioning instructions.

Recall counts unsupported/inconclusive positives as misses; FPR must be read with abstention and conditional denominators. Per-observation samples can be correlated. Geometric registration error, patch displacement error and localized region matching are different metrics. Engineering uncertainty scores and planning utilities are not calibrated probabilities. Preserve negative outcomes and evaluate fresh held-out data after scientific changes.
