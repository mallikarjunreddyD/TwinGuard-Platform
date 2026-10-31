# Installation

Use Ubuntu/Linux with Python 3.12, Docker Engine and a Docker Compose version supporting `!override`. Start from this repository's root. Dependency/image installation requires network access; the running laboratory has no cloud dependency.

## Python environment

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements-dev.lock -r requirements-edge.lock
pip install -e '.[dev,viz,sensing,analytics,edge]' --no-deps
export PYTHONPATH=src TWINGUARD_ROOT="$PWD"
twinguard doctor
```

The locks include optional scientific dependencies. Open3D and plotting libraries are not required inside the minimal operational API image. For a fresh dependency resolution, use `pip install -e '.[dev,viz,sensing,analytics,edge]'` instead of the locks; revalidate that environment independently.

## Browser laboratory

Provision once in a **fresh** checkout/project, then build the base images before their privileged controller derivative:

```bash
python scripts/demo_init.py --profile simulation
docker compose -p twinguard-platform --env-file .edge/runtime.env \
  -f deployment/compose.yaml -f deployment/edge/compose.demo-ux.yaml \
  build api inspection-worker frontend
docker compose -p twinguard-platform --env-file .edge/runtime.env \
  -f deployment/compose.yaml -f deployment/edge/compose.demo-ux.yaml \
  build simulation-controller
docker compose -p twinguard-platform --env-file .edge/runtime.env \
  -f deployment/compose.yaml -f deployment/edge/compose.demo-ux.yaml up -d
```

Open <http://localhost:19480>. Read the local operator/viewer credential from the ignored `.edge/secrets.json` file and enter it at login. Never commit it or paste it into reports. Loopback PostgreSQL/MQTT ports for this explicit laboratory overlay are 19482/19483. The default base deployment has different ports and profile semantics; use the complete command above for Simulation Lab.

Existing databases need explicit role provisioning and migration. Do not erase volumes to fix a setup failure. Preserve database, public edge artifacts and controller demo-data volumes to retain observations/session history. Provisioning mutates ignored local files and is not an ordinary startup step. Bind-mounted controller credentials are owned by runtime UID 10001 and are read-only inside the container.

## Restrictive-profile verification

The optional `deployment/edge/compose.demo-review-test.yaml` overlay uses profile `review-check` and port 19490. It tests server rejection of simulation commands in `site-review` while sharing only this isolated laboratory database. It does not commission a physical site. Do not expose the lab or its database/broker publicly. See [security](SECURITY.md).

## Development frontend

```bash
cd frontend
npm ci
npm test -- --run
npm run build
```

The production Compose frontend proxies authenticated API requests; it does not embed a token. See [development](DEVELOPMENT.md) and [Simulation Lab](SIMULATION_LAB.md).
