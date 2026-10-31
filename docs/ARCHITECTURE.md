# Architecture

A shared Python package provides versioned contracts, with separate deployed processes and image contents enforcing the operational boundary.

## Data flow

The privileged plant/acquisition controller generates imperfect public sensor observations and inspection captures. Public MQTT envelopes and allowlisted inspection bundles enter authenticated ingestion. Durable PostgreSQL inbox/jobs/checkpoints feed the fast IoT worker, isolated inspection worker and F1 fusion. Inspection planning consumes public qualified evidence and accepted reference geometry. API/SSE exposes stored public records to the React/Three.js dashboard.

Private fault definitions, exact simulated poses, labels and truth are never inference inputs. Analytics operates on public data and accepted references. The evaluator compares sealed predictions with restricted truth after inference. Public calibration/configuration references do not make hidden labels available to production services.

## Deployed components

| Component | Responsibility |
|---|---|
| PostgreSQL | Durable observations, sessions, inbox, jobs, conditions, advisories and actions |
| MQTT broker/ingestion | Identity/topic validation, replay-clock qualification and idempotent admission |
| Minimal API | Authentication/RBAC, stored queries, bounded demo commands and event stream |
| Fast worker | Operating analytics and temporal hazard fusion |
| Inspection worker | Public LiDAR/thermal processing with native scientific dependencies |
| Planning worker | Bounded recommendation requests using current public evidence |
| Optional simulation controller | Whitelisted generation, real publication, pause/stop/recovery |
| Frontend | Stored-data charts, accepted reference model, inspections, advisories and Simulation Lab |

The optional controller is the only runtime service with simulator/generator modules and its private dataset volume. The API image excludes plant, sensing implementation, evaluator and privileged demo modules. Neither service mounts the Docker socket. The controller's restricted database role updates sessions and reads job state; observations enter through the normal ingestion boundary.

## Package boundaries

`core` defines public contracts, units, frames, serialization and import auditing. `plant` models static/dynamic geometry, process states and restricted injections. `sensing` produces imperfect virtual measurements. `analytics` registers observations and estimates geometry/operating anomalies. `fusion` manages qualified, timely evidence and advisory lifecycle. `inspection` computes risk/coverage-based recommendations. `evaluation` contains restricted experimental comparisons. `edge` implements operational persistence/protocols/services; `demo` is the privileged optional controller.

The browser combines accepted baseline geometry with estimated measurement regions and predicted planning coverage, keeping each layer identifiable. Acknowledgment is an auditable human review action and does not resolve an event. Stop preserves existing evidence and leaves the platform running.

See [data contracts](DATA_CONTRACTS.md), [controller architecture](SIMULATION_CONTROLLER_ARCHITECTURE.md), [evidence semantics](EVIDENCE_SEMANTICS.md), [security](SECURITY.md) and [persistence/recovery](PERSISTENCE_AND_RECOVERY.md).
