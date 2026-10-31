# Security and operational boundaries

Operational `/api/v1/` routes require local authentication. Viewer tokens read records; operator/admin roles are required for bounded simulation commands and human review. `/health`, `/version` and `/capabilities` are public metadata. Generated credentials are local, non-default and gitignored. Do not copy an older `.edge` directory into a new installation.

Simulation execution requires both `TWINGUARD_PROFILE=simulation` and `TWINGUARD_DEMO_ENABLED=1`. The server rejects execution in `site-review` even when the enable flag is set. Browser requests use bounded configuration contracts; deployment profiles, calibration trust and service permissions are managed separately.

The API and optional controller run as UID 10001. The controller has a dedicated read-only credential mount, private dataset volume and constrained database role; no Docker socket is exposed. Public inspection ZIPs are validated/allowlisted before ingestion. The minimal API image excludes privileged generation modules and evaluator truth. Runtime limits constrain preparation, dataset size, publication records and session capacity.

MQTT identities/ACLs, public envelopes and read-only OPC UA integration preserve their independent validation/qualification checks. Deployment configuration covers certificates, clocks, instrument calibration, source identities, retention, engineering limits and operator authorization. The explicit lab overlay binds testing ports only to loopback.

Keep database/artifact/demo volumes for recovery; controller restart fails an interrupted owned session and retains its checkpoint rather than silently replaying it. An in-flight delivery may already have committed. See [persistence/recovery](PERSISTENCE_AND_RECOVERY.md), [protocol](MQTT_PROTOCOL.md), [OPC UA](OPCUA_INTEGRATION.md) and [limitations](LIMITATIONS.md).
