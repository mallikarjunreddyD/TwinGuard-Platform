# Data contracts

Typed Pydantic contracts in `src/twinguard/core/contracts.py`, `edge/contracts.py`, `fusion/models.py` and `inspection/models.py` are the authoritative schemas. Versioned JSON schemas are exported under `schemas/`; use `twinguard export-schemas` to regenerate them after a reviewed contract change.

Public sensor observations carry stable observation/source/asset/sensor identity, measurement type, unit, value/quality, coordinate/time references and declared provenance. Inspection captures reference public allowlisted arrays and acquisition metadata. Raw manifests, simulator configuration and evaluator labels are not observation payloads. Recursive extra-field rejection and explicit serialization prevent evaluator records being substituted for public observations.

Acquired, emitted, received, processed and available times are distinct. Controlled replay declares its rate, sequence epoch and mapped acquisition time, retaining original scientific source times. Duplicate delivery does not create an independent measurement. Effective acquisition timing must pass ingestion trust/causality checks; later fusion independently validates freshness, qualification and applicability.

Evidence and advisory contracts retain measurement scope, status, uncertainty/qualification, policy versions, positive/recovery origin identities and temporal history. Image-only thermal findings do not imply a verified 3D hotspot. Reference geometry, measured coverage and predicted coverage are distinct contracts. Planning utilities are engineering priorities, not calibrated fault probabilities.

Simulation configuration allows only declared scenarios, L1/L2, bounded seed/rate and inspection inclusion. Session/command UUID keys make retries idempotent; desired state and controller-acknowledged state remain separate. See [controller architecture](SIMULATION_CONTROLLER_ARCHITECTURE.md), [evidence semantics](EVIDENCE_SEMANTICS.md) and [event lifecycle](EVENT_LIFECYCLE.md).
