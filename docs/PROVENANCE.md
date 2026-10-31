# Source and evidence provenance

This is an independent repository assembled from the consolidated TwinGuard application at legacy revision `190bdce4f4593b60955ba72bee208acd2373cfc7` in `mallikarjunreddyD/TwinGuard`. The legacy scientific freeze was `edae1e5`. No old `.git` objects, refs, commits or worktree links are copied. The repository starts with an independent initial commit without parent history.

Original repositories and raw research records are retained separately as backups. Historical phase reports, generated outputs and private runtime state are excluded from the new repository. Source identifiers in some scientific scripts/configs/tests remain intact to preserve reproducibility rather than renaming scientific methods or their partitions.

`evidence/source-files.json` records SHA256 values for the inherited source/configuration/scenario/experiment files. Scientific implementation, calibrated model and policy bytes are preserved. Documentation is reorganized by topic; the documentation-presence test and a source-checkpoint fixture path are adjusted accordingly. Operational lab image/project names and browser-test ports use `twinguard-platform` and 19480/19482/19483/19490 to avoid affecting an older running stack. Fresh browser evidence is written under ignored `docs/evidence/local/`, protecting the inherited records.

`evidence/ux/` contains selected actual software-demonstration measurements/screenshots from 2026-10-29. Their original IDs, timestamps, counts, paths and hashes are retained, including references to the old deployment. These records retain their original execution context. Legacy validation reported 362 backend tests, 3 frontend tests and actual browser/protocol integration checks. Newly executed checks for this copy are reported separately in [validation](VALIDATION.md).

The old GitHub repository contains the full historical reports and source context. The external archive is retained separately; its packaging status and the evaluation coverage are recorded in [scope](LIMITATIONS.md).
