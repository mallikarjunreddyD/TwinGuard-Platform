# Development

Work from this repository's root and a Python 3.12 development environment. Set `PYTHONPATH=src` and `TWINGUARD_ROOT="$PWD"` when using a shared environment, so imports and configuration resolve to this copy.

```bash
python -m pytest -q
ruff check src tests scripts
ruff format --check src tests scripts
mypy src
pip check
```

Frontend checks: `cd frontend && npm ci && npm test -- --run && npm run build`. Package names remain `twinguard`; changing the repository name does not require renaming imports or serialized scientific identities.

Use normal Git review after the clean initial import is approved. Keep algorithm changes, operational changes and documentation changes distinguishable. A scientific change requires a new declared calibration/evaluation freeze and fresh held-out evidence. Never tune on evaluation outcomes or replace negative/inconclusive results with frontend status. Public analytics cannot import simulator/evaluator truth.

The optional browser harnesses use real services and locally generated ignored credentials. They create retained sessions and can restart **only the `twinguard-platform` test services**. Fresh screenshots/audit output go under ignored `docs/evidence/local/`; the retained inherited evidence is not overwritten. Read the scripts before running; provision the new isolated stack first. Do not point them at a physical/site deployment or the old project's containers. Historical study helpers may depend on separately retained raw artifacts; see [experiments](EXPERIMENTS.md).

Generated output belongs in ignored `output/`, `.demo-data/`, `experiments/outputs/` or an explicitly managed external directory. Do not commit `.edge`, private credentials/certificates, database dumps, inspection datasets, caches, build outputs or local dependency environments. Use new output directories to preserve prior evidence.
