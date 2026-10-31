# Oracle Always Free deployment

Deployment target: one Oracle Ampere A1 Linux VM running the existing isolated Compose services, PostgreSQL/artifact storage and HTTPS gateway. Users access the web dashboard and its `/user-guide.html` page. Account provisioning, ARM dependency qualification and live URL acceptance are the remaining deployment gates.

## 1. Account and capacity

Create an [Oracle Cloud Free Tier account](https://www.oracle.com/cloud/free/) and choose a home region with A1 availability. Check the [current Always Free resource limits](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm) in both documentation and your account console. On 2026-10-31 the published allowance is equivalent to **2 OCPUs / 12 GB RAM**, with **200 GB combined boot/block volume storage**. Do not use older tutorials promising 4 OCPUs / 24 GB for every new free account.

Use only resources marked Always Free in the home region and verify the cost estimate before creation. Capacity can be unavailable. Do not select paid shapes or upgrade the account as a workaround without deciding on a budget. Oracle publishes idle-instance reclamation conditions; preserve independent backups.

The deployment owner completes account identity/payment verification and sign-in privately. Passwords, codes, payment details and SSH private keys stay outside chat and Git. For agent-assisted operations use authenticated local tooling or an owner-authorized session after account setup.

## 2. ARM compatibility gate

The validated application locks target Python 3.12 Linux x86_64. Ampere A1 is ARM64. The exact pinned `open3d==0.19.0` distribution has no Linux aarch64 wheels in its [PyPI file listing](https://pypi.org/project/open3d/0.19.0/#files), including none for Python 3.12, when checked on 2026-10-31. Generic Open3D ARM documentation is not proof that this exact dependency set installs.

Before application deployment, build the pinned native Open3D dependency using its [ARM/source-build instructions](https://www.open3d.org/docs/0.19.0/arm.html), or establish a compatible ARM dependency environment separately. Use a controlled build with declared compiler/library versions and retained wheel hashes. Preserve scientific source, calibration models and policy thresholds. Do not silently replace Open3D, switch algorithms or use x86 emulation and call it validated ARM execution.

Acceptance requires imports, CPU first-hit raycasting, geometric processing and the backend regression suite on the actual ARM host, followed by the real browser lifecycle and inspection cases. The repository currently provides no prevalidated ARM image or automatically successful build recipe. The existing Dockerfile’s pip install will need an approved native-wheel/build path before it can pass this gate.

## 3. VM and network

After the compatibility approach is ready, create one Always Free A1 VM using an eligible Ubuntu image and the account-confirmed CPU/RAM allocation. Use persistent storage within the free quota and retain SSH access for administration. Configure a VCN/subnet/security rules and the host firewall to allow administrator SSH and public HTTP/HTTPS. Keep PostgreSQL and MQTT internal; the provided gateway overlay removes their host port mappings.

Install Docker Engine and Compose from their official packages. Clone the repository and follow [installation](INSTALLATION.md) with the qualified ARM dependency build. Provision fresh local `.edge` credentials and preserve their permissions. Build the base API/worker/frontend images before the dependent isolated controller image.

## 4. HTTPS and application startup

Point an owned DNS hostname at the VM and follow [Cloud VM with HTTPS](HOSTING.md#cloud-vm-with-persistent-storage-and-https). The checked-in `deployment/cloud/compose.vm.yaml` and `Caddyfile` retain service isolation, shared public-artifact storage, private controller datasets and persistent certificate storage. They are configuration-validated locally; this is not yet a running Oracle deployment.

If a DNS hostname is unavailable, an eligible Tailscale Funnel setup on the VM is an alternative HTTPS entry point; see [hosting](HOSTING.md). Publish only the web frontend, retaining application authentication.

## 5. Public URL acceptance and handover

1. Verify API readiness, database persistence and all service states.
2. Open the external HTTPS URL in a fresh browser; verify the guide link and viewer login.
3. With an operator token, execute Healthy Operation, Pause, Resume and Stop; verify stored rows remain.
4. Execute a measured inspection and a critical-pressure scenario; inspect actual job/qualification/advisory records.
5. Verify source interruption, role restrictions, refresh/restart retention and live updates through the external proxy.
6. Measure memory, disk and critical-evidence currentness on the 2-core host; adjust concurrency/rate from these observations.
7. Give reviewers the HTTPS URL, [user guide](USER_GUIDE.md) and privately supplied appropriate-role tokens. Keep operator execution coordinated because the deployment has one active simulation namespace.

Record the deployed Git revision, image/wheel hashes, actual URL, checks and backup procedure. Until these checks execute, the deployment status is **prepared, awaiting Oracle account and ARM qualification**, rather than live.
