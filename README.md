# TwinGuard Platform

TwinGuard is a digital twin platform for industrial equipment condition monitoring and UAV-assisted inspection planning. It integrates equipment models, LiDAR and thermal inspection analytics, IoT telemetry, temporal hazard assessment, inspection recommendations and an authenticated 3D dashboard. An integrated Simulation Lab provides repeatable scenarios for exploring the complete monitoring workflow.

The platform provides MQTT and read-only OPC UA integration, durable observation and job processing, geometric and operating-state analytics, qualified hazard assessment and coverage-aware inspection recommendations. The Python package and CLI are named `twinguard` (version 0.8.0).

## Start here

- [End-user guide](docs/USER_GUIDE.md): browser access, scenarios, measurements and advisory review.
- [Hosting](docs/HOSTING.md): no-cost reviewer access, cloud options and HTTPS deployment.
- [Oracle deployment](docs/ORACLE_DEPLOYMENT.md): Always Free setup and ARM compatibility steps.

- [Installation](docs/INSTALLATION.md): Python environment, dependencies and isolated Docker setup.
- [Simulation Lab](docs/SIMULATION_LAB.md): six scenarios and actual Start/Pause/Resume/Stop.
- [Browser walkthrough](docs/DEMO_WALKTHROUGH.md): run a demonstration after installation.
- [Dashboard guide](docs/DASHBOARD_GUIDE.md): equipment, measurements, inspections, advisories and planning.
- [Architecture](docs/ARCHITECTURE.md): service and scientific data boundaries.
- [Validation](docs/VALIDATION.md), [scope](docs/LIMITATIONS.md) and [provenance](docs/PROVENANCE.md): test results, supported coverage and evidence origins.
- [Documentation index](docs/README.md): detailed model, protocol and development references.

## Local development

Dependency locks target Python 3.12 on Ubuntu/Linux. Monitoring services, analytics and scenario execution run locally after installation.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements-dev.lock -r requirements-edge.lock
pip install -e '.[dev,viz,sensing,analytics,edge]' --no-deps
export PYTHONPATH=src TWINGUARD_ROOT="$PWD"
python -m pytest -q
ruff check src tests scripts
ruff format --check src tests scripts
mypy src
```

Follow [installation](docs/INSTALLATION.md) for the browser lab. The dedicated project is `twinguard-platform`, with dashboard <http://localhost:19480>; it uses distinct image names, volumes and loopback ports so it can coexist with an older installation. Runtime secrets and generated data are created locally and never shipped in this repository.

## Repository layout

| Directory | Purpose |
|---|---|
| `src/twinguard` | Scientific modules, contracts, API, edge services, controller and CLI |
| `frontend` | React/TypeScript dashboard and 3D view |
| `configs`, `scenarios`, `schemas` | Versioned inputs and public contracts |
| `deployment`, `migrations` | Isolated service images, Compose and database migrations |
| `tests` | Scientific, protocol, lifecycle and security regression tests |
| `scripts`, `experiments` | Operational tools and reproducible experiment definitions |
| `datasets` | Small declared input fixtures, including restricted simulator fault definitions |
| `docs` | Current guides and explicitly identified inherited evidence |

Generated datasets, runtime credentials and build artifacts are excluded from version control. See [development](docs/DEVELOPMENT.md) for contribution and verification workflows.
