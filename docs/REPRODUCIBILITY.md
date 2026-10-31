# Reproducibility

Use the checked-in dependency locks, configs, scenarios, schemas and experiment definitions. Record software/environment versions, exact input hashes, seed/partition, detector/calibration/policy versions and acquisition/processing clocks for any new run. Original scientific code/model bytes are compared with the source manifest; documentation and operational deployment names may differ intentionally.

Small dataset fixtures provide versioned, reproducible source inputs. Generated simulator state/truth remains private; seal public-data predictions before evaluation. Read [experiments](EXPERIMENTS.md) for smoke/full distinctions and historical-controller prerequisites. Large historical artifacts remain in the separately retained research archive.

For the current browser workflow, provision [installation](INSTALLATION.md), then follow [walkthrough](DEMO_WALKTHROUGH.md). A new run produces new session identities and actual stored data; its records retain their own timestamps and condition history. Stop keeps history and does not resolve advisories. Unexpected controller interruption is explicit and never automatically replays the old dataset.

Inherited reports and new verification are separate in [validation](VALIDATION.md). Source origin and artifact hashes are in [provenance](PROVENANCE.md). See [scope](LIMITATIONS.md) for the evaluation coverage.
