# Scenarios

Simulation Lab provides Healthy Operation, Localized Deformation, Thermal Anomaly, Critical Pressure, Degraded Sensing and Sensor Interruption. Each creates a new persistent identity and uses the original plant/sensing generator. Degraded Sensing forces L2; Critical Pressure and Sensor Interruption force inspection publication off. Seeds and dataset identities are explicit. Each preset supplies a declared input scenario; the pipeline computes its findings and qualification status.

The underlying CLI scenario templates `scenarios/S0.yaml` through `S5.yaml` declare plant references, public sensor configuration and private controller fault references. Small `datasets/ground_truth/fault-*.yaml` files provide restricted scenario-controller inputs, separately from the public observations consumed by analytics. Generated public artifacts are separated from private truth in each run.

```bash
twinguard list-scenarios
twinguard validate-config scenarios/S0.yaml
twinguard plant simulate --scenario scenarios/S0.yaml --output-dir output/healthy
```

Use a new/empty output directory. Do not publish simulator manifests or restricted directories to analytics. A browser demonstration needs no terminal commands after installation: follow [walkthrough](DEMO_WALKTHROUGH.md).
