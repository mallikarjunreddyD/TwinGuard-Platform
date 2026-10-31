# Validation

This report distinguishes inherited research evidence from verification of the standalone repository. It records the executed checks, their environment and the provenance of the supporting measurements.

## Inherited source integration

The consolidated source application reported 362 backend tests, 3 frontend tests, Ruff/format, Mypy (118 source files), production build and Compose checks passing. Its real browser/MQTT lifecycle accepted 24 unique observations from 24 deliveries and verified actual Pause/Resume/Stop, retained charts and persistent history. Additional real cases exercised F1 critical pressure without UAV, valid L1 localized processing, thermal results, L2 insufficient coverage, a 16-second publication gap, role/profile rejection and controller/API/frontend recovery.

The inherited inspection runs recorded 434/428 deliveries/unique sensor rows for L1 geometry and thermal, and 380/373 for L2. Each included one inspection delivery; duplicate source observations were independently audited. The thermal case's extra geometric region is retained, not claimed as confirmed structural fault. Completed processing is distinct from qualified detection. See [original measurements](evidence/ux/scenario-counts.json) and [evidence scope](evidence/ux/README.md).

Broader independent software studies retained material limitations: view-qualified detector abstention/recall tradeoffs, heavy mixed workload timeliness, saturation/admission limits and unproven long-duration storage capacity. Source UI acceptance was 24 PASS / 1 PARTIAL; the partial item was the unresolved external archive failure. Evaluation coverage is summarized in [scope](LIMITATIONS.md). Detailed original research reports remain in the legacy repository identified in [provenance](PROVENANCE.md).

## Standalone verification

Validated on 2026-10-31. Source was imported from this standalone directory using explicit `PYTHONPATH` and `TWINGUARD_ROOT`. Existing Python dependencies were reused; frontend dependencies were mounted read-only into Node 22. These checks used the existing dependency environments; fresh installation/deployment checks are tracked separately.

| Check | Actual standalone result |
|---|---|
| Full backend regression suite | **362 passed**, one existing Starlette/httpx deprecation warning; 584.22 s |
| Frontend Vitest | **3 passed** |
| TypeScript/Vite production build | Passed; bundle >500 kB warning remains |
| Ruff | Passed across src/tests/scripts |
| Ruff format | 204 files already formatted |
| Mypy | Passed, 118 source files |
| CLI doctor | Environment/imports/repository checks passed |
| Compose | Simulation + restrictive-profile overlay configuration passed without provisioning credentials |
| Source integrity | 183 source/config/scenario/experiment files unchanged |
| Secrets/docs | No copied credential values or broken Markdown links found; no phase-named documentation files |
| Repository isolation | No inherited commit objects/parents; both original worktrees remain clean |

[New execution logs/results](evidence/standalone/results.json), [integrity review](evidence/standalone-integrity.json) and [Compose configuration review](evidence/standalone-compose.json) record the scope. Deliberate non-scientific changes are ignore rules, isolated lab names/ports, fresh browser-audit output paths, the current-documentation presence check and the relocated scientific checkpoint fixture.

No new Docker platform was started and no fresh live browser/MQTT scenarios or full scientific campaigns were rerun during this source/documentation cleanup. Those inherited results above remain labeled as inherited. Existing services and the unfinished research archive were not modified. Runtime credentials/generated datasets/build outputs are excluded from the Git index. The preparation-stage integrity snapshots retain their original zero-commit state. GitHub publication was subsequently authorized; the initial import has no inherited parent history. Cloud hosting status is recorded in [hosting](HOSTING.md).
