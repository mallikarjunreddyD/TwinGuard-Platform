# TwinGuard user guide

Use this guide to explore equipment, run scenarios and review measurements and advisories from the browser.

## Access the platform

Open the HTTPS address supplied by the deployment owner in a current desktop browser. A tablet can also be used.

Enter the access token supplied privately by the owner and choose Open operations console. Keep the token private. Viewer access supports browsing; operator access adds scenario execution and advisory review.

## Understand the header

Platform stream indicates the browser’s connection to the application. Data Sources shows how many registered sources were recently active. Simulation shows publisher activity. These indicators describe different parts of the data path.

Source activity can expire after a scenario stops while stored measurements remain available.

## Explore equipment

Open Overview. Orbit, zoom and pan the 3D equipment model. Select an asset using the equipment buttons or the keyboard arrows on the focused canvas.

Read condition, qualification, monitoring gaps and assessment rationale together. Unknown identifies missing qualified inputs; the panel lists those requirements.

## Run your first scenario

With operator access, open Simulation Lab and select Healthy Operation. Choose L1 and 2× playback. Leave measured inspections unchecked for a short first run.

Choose Start and wait for preparation to finish. Watch acknowledged deliveries, accepted sensor observations and processing status increase.

Choose Open Measurements to inspect stored values, units, quality and acquisition timestamps. Return to Simulation Lab.

Choose Pause and wait for acknowledgment, then Resume. Choose Stop to end publication; measurements and session history remain available.

## Explore inspection and advisory workflows

Start Localized Deformation with inspections enabled. After the inspection job completes, open Inspections and review LiDAR results, regions, uncertainty and coverage.

Run Thermal Anomaly to explore thermal frames and image findings. Degraded Sensing uses L2 and exposes coverage/qualification outcomes.

Run Critical Pressure to follow the pressure evidence into Advisories. Operators can acknowledge review and inspect its recorded actor/history. Acknowledgment and event resolution are separate steps.

Run Sensor Interruption and use Monitoring to observe source recency during the publication gap.

## Review inspection recommendations

Open Inspection Planning, set the method and view/time budgets, and request a plan. Review the selected viewpoints, feasibility reasons and predicted coverage in the model.

Review decisions are recorded with the plan. Simulation Lab executes its selected preset separately from a planned-route reinspection workflow.

## Use a shared deployment

The deployment has one active simulation namespace. Coordinate scenario execution with other operators; Pause and Stop affect that shared session.

Select a completed session to inspect its history. Starting a new session retains earlier observations and advisories. Refreshing the browser restores server state.

The owner manages access credentials and availability. Sign out when finished.

## Troubleshooting

No sources active: check whether a scenario is running; source recency decreases after publication ends.

Start disabled: confirm that your token has operator access, the deployment enables simulation, and another session is not using the namespace.

Preparing or processing: these stages perform real generation/analysis. Follow the displayed progress and errors; avoid repeated clicks.

Unknown equipment: open the missing-input details and inspect available evidence for that asset.

Connection interrupted: reload once and check the platform indicator. If an interrupted session is failed, retain its history and start a new session.

For access or server errors, contact the deployment owner with the session/job ID and the displayed message. Do not send access tokens.

For deployment and account administration, see [hosting](HOSTING.md).
