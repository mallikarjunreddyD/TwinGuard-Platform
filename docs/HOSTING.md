# Hosting and reviewer access

TwinGuard’s full browser workflow runs the frontend/API, PostgreSQL, MQTT ingestion, analysis/planning workers and the isolated scenario controller. The Docker Compose deployment preserves its shared artifact store and service boundaries. Users need only the HTTPS URL and the privately supplied application token; use the [user guide](USER_GUIDE.md), also available at `/user-guide.html` in the deployed frontend.

## Hosting options

Provider details checked on 2026-10-31. Quotas and eligibility should be checked again when creating an account.

| Option | Fit for this repository | Account/resource requirements |
|---|---|---|
| Existing workstation + Tailscale Funnel | Quick no-cloud-compute-cost reviewer access; retains the tested x86 environment | Eligible free Tailscale account; workstation and Internet connection stay online |
| Oracle Always Free A1 VM | Potential persistent cloud host for the full Compose stack after ARM compatibility work | Account, available home-region capacity, ARM dependency build and validation |
| Railway Free | Insufficient allowance for the complete retained multi-service workflow | 0.5 GB RAM/service, one 0.5 GB volume/project and $1 monthly usage credit |
| Render Free | Better suited to a small web preview than this complete persistent stack | Limited memory/compute hours, no persistent web disk and expiring free PostgreSQL |
| Hugging Face Docker Spaces | Not a zero-subscription route for a new Docker Space under current terms | CPU Basic has no hourly charge, but new Docker/Gradio compute Spaces require a paid plan |

Sources: [Railway plans](https://docs.railway.com/pricing/plans), [trial](https://docs.railway.com/pricing/free-trial), [volumes](https://docs.railway.com/volumes/reference), [Oracle Always Free](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm), [Render](https://render.com/docs/free), [Hugging Face](https://huggingface.co/docs/hub/spaces-overview), [Tailscale Funnel](https://tailscale.com/docs/features/tailscale-funnel).

## Existing workstation with a public HTTPS link

1. Complete [installation](INSTALLATION.md) on a host with the existing x86 Python/Docker dependencies. Start only the `twinguard-platform` project and verify its local dashboard at `http://localhost:19480`.
2. Install Tailscale using its [official instructions](https://tailscale.com/download). Sign in on the same host and select the eligible free account plan. Account setup and HTTPS/Funnel permissions are owner actions.
3. Follow the [Funnel instructions](https://tailscale.com/docs/features/tailscale-funnel) to publish only the frontend port:

```bash
tailscale funnel --bg 19480
tailscale funnel status
```

4. Share the generated HTTPS `*.ts.net` application URL and its `/user-guide.html` page. Visitors use a browser and do not need to join the tailnet. Application API authentication remains enabled. Give viewer tokens for browsing and operator tokens only to designated scenario operators; never publish tokens in the repository or guide.
5. Verify sign-in, live updates, Start/Pause/Resume/Stop and an inspection through the external URL. The host must remain awake and connected. For WSL/Windows installations, use the host on which the local frontend and Tailscale can both resolve port 19480.
6. To stop public access, use `tailscale funnel --https=443 off`, then check `tailscale funnel status`. Keep application volumes for later use.

Funnel has provider traffic/usage limits; use it for controlled reviewer access. Cloudflare’s anonymous Quick Tunnels are not a direct replacement for the live-update path because [they do not support SSE](https://developers.cloudflare.com/tunnel/get-started/quick-tunnels/).

## Cloud VM with persistent storage and HTTPS

Use a Linux VM compatible with the pinned scientific dependencies and Docker Compose. A starting evaluation target is 8–12 GB RAM with sufficient persistent disk; measure actual concurrent inspection/generation use before selecting workload limits. Expose only SSH to the administrator and TCP 80/443 for the web gateway. Keep PostgreSQL/MQTT private.

1. Clone this repository and follow [installation](INSTALLATION.md) to provision local credentials and build the base images, then the simulation-controller image. Keep `.edge` private and out of Git.
2. Point a DNS hostname at the VM. Set `TWINGUARD_DOMAIN` and `TWINGUARD_ACME_EMAIL` in the server environment, then start the HTTPS overlay:

```bash
export TWINGUARD_DOMAIN=monitoring.example.org
export TWINGUARD_ACME_EMAIL=owner@example.org
docker compose -p twinguard-platform --env-file .edge/runtime.env \
  -f deployment/compose.yaml -f deployment/edge/compose.demo-ux.yaml \
  -f deployment/cloud/compose.vm.yaml up -d
```

3. The Caddy gateway terminates HTTPS and forwards live streams to the existing frontend. The overlay removes all host publications for the frontend/database/broker; internal service communication remains on Docker networks. Preserve gateway certificate, database, public-artifact and controller volumes.
4. Verify the public URL with the role/lifecycle checks above, record the deployment version and configure backups. Do not replace existing volumes or re-run credential initialization as an upgrade shortcut.

### Oracle A1 compatibility

Follow the [Oracle deployment guide](ORACLE_DEPLOYMENT.md) for account, ARM qualification and live-URL acceptance gates.

Oracle currently documents **2 OCPUs and 12 GB RAM** equivalent Always Free A1 capacity and **200 GB combined boot/block storage**. Provision only resources marked Always Free and verify account quotas. Capacity may be unavailable; idle instances may be reclaimed under Oracle’s published policy.

A1 is ARM64. Open3D documents experimental ARM support, but the PyPI file listing for this repository’s exact `open3d==0.19.0` did **not** contain a Python 3.12 Linux ARM64 wheel when checked. The Python 3.12/x86 locks cannot be assumed to install on A1. A native wheel build or a separately validated compatible environment is needed before recommending an A1 deployment as runnable. Preserve the algorithm/model inputs and run the regression/scenario checks on the actual ARM host. This cloud overlay is architecture-neutral configuration, not an ARM validation result.

References: [Oracle allocation/idle/capacity policy](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm), [Open3D ARM support](https://www.open3d.org/docs/0.19.0/arm.html), [pinned-release distribution files](https://pypi.org/project/open3d/0.19.0/#files).

## Railway deployment mapping

Railway [maps Compose services individually](https://railway.com/guides/docker-compose); it does not run this Compose stack directly. Native service deployment requires service-specific builds/startup/migrations, private broker/database connectivity, secret provisioning and an artifact-storage design accessible to API, ingestion and inspection workers. This application currently uses a shared local artifact volume; independent service-local volumes are not equivalent. Its controller Dockerfile also depends on a locally built worker image, so it needs a cloud-build base image strategy.

The present repository therefore provides a tested local stack and a syntax-checked VM gateway overlay, not a one-click native Railway template. A complete Railway deployment is separate work after selecting an appropriate plan and storage design. No provider account, paid service, public tunnel or VM has been provisioned by these documentation/configuration changes.
