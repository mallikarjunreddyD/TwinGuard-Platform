# Scope and validation coverage

TwinGuard integrates equipment modeling, sensor-data acquisition and ingestion, inspection analytics, temporal condition assessment, inspection recommendations and operator review. Its validation records identify the data, environment and measurement basis used for each capability.

## Evaluation coverage

The recorded studies use synthetic acquisitions and local protocol/service integration. Physical LiDAR/thermal metrology and site commissioning have not been evaluated in these studies. The [validation report](VALIDATION.md) distinguishes the inherited integration evidence from the checks executed for this repository.

## Model and measurement scope

- Plant dynamics use deterministic engineering relationships, configurable geometry, thermal expansion and explicit fault contributions. CFD, FEA and coupled combustion/structural solutions are outside this model.
- LiDAR acquisition models first-visible returns, range/angular/pose error, dropout, quantization and outliers. Flight dynamics, moving scans, atmospheric propagation and calibrated reflectance are outside its current acquisition model.
- Thermal acquisition models geometry-linked surface fields, apparent radiometry, noise, saturation and pose effects. Spectral/atmospheric optics, lens and camera thermal effects, and measured instrument calibration require separate characterization.
- B3.1 reports qualified localized relative geometric change. Optional B3.2 trades lower healthy positives for increased abstention and lower overall recall on the inherited matrix. L2 may yield insufficient coverage. Thermal image findings retain image-space association unless an independent spatial association is available.
- Inspection recommendations use static accepted geometry, configured corridor/access constraints and predicted coverage. Dynamic obstacles, aircraft/rotor motion and flight execution are separate integration scopes.

## Operating envelope and evidence retention

Hazard assessment uses configured engineering limits, source qualification and temporal rules. Heavy mixed workloads and queue saturation can affect evidence currentness and admission. Retention grows with observations, jobs, sessions and artifacts; workload and retention settings should be selected from the measured operating envelope.

The separately retained research archive has an unresolved packaging allocation failure. Its source records remain preserved; archive completion is tracked independently from this repository’s application and regression checks. See [provenance](PROVENANCE.md).
