# Dashboard guide

Sign in with a locally generated viewer or operator token. The UI has seven pages; all assessment colors come from actual backend state. The header distinguishes platform/SSE connectivity, recent registered-source activity and simulation publisher status. An IoT-only run need not activate all three registered sources.

| Page | Interpretation |
|---|---|
| Overview | Accepted reference model, selected asset, actual conditions, monitoring gaps and stored telemetry |
| Measurements | Stored sensor rows with units, quality and source/receipt clocks; session filter is explicit and clearable |
| Inspections | Actual completed public LiDAR/thermal processing with validity, uncertainty, regions and inconclusive states |
| Advisories | F1 hazards, supporting evidence and event/action history; operator acknowledgment retains actor/rationale |
| Monitoring | Real source recency, missing inputs, qualification and platform status |
| Inspection Planning | Current public-evidence recommendations, restrictions, predicted coverage and review records |
| Simulation Lab | Whitelisted presets and actual durable publisher lifecycle |

Unknown means there is insufficient qualified evidence for an asset-level conclusion. Missing monitoring and unsupported geometric scope remain visible. Confidence/qualification is separate from severity. An absence of an alert does not establish health. A retained advisory during a new healthy run is legitimate until the existing recovery/review rules resolve it.

The 3D canvas supports orbit, zoom, pan and selection; asset buttons and keyboard arrows provide selection alternatives. It shows accepted geometry, localized estimated measurements and planning overlays. Steel blue indicates recommended sensor positions/directions, ochre predicted reference coverage, green previously qualified measured coverage and red rejected viewpoints. Overlay labels distinguish predicted coverage, measured coverage and operator-review status.

Charts use actual stored values and retain invalid/missing gaps. Display/receipt time and original acquisition time are identified separately. Limit lines use the configured policy references. Empty charts show their data-availability state. Changing viewport or refreshing does not reset backend state.

Viewer access is read-only. Operators/admins can execute simulations only in the explicitly enabled simulation profile and can record human review actions. Calibration trust and instrumentation configuration are managed through deployment configuration. See [walkthrough](DEMO_WALKTHROUGH.md) and [limitations](LIMITATIONS.md).
