# Team FMIP: agent definitions (draft)

Status: DRAFT. Not yet copied into the repo's `.claude/agents/` folder. Awaiting owner approval.
Source blueprint: agent team blueprint, Claude conversation of 2026-11-04 (compressed version, FMIP section).

| Agent | File | Owns | Build wave |
|---|---|---|---|
| Coordinator | fmip-coordinator.md | Status file, handoffs, open-items log, daily summary to owner | 0 (first) |
| Data & intake | fmip-data-intake.md | Source register, folder paths, security, freshness, Gmail intake and filing | 1 |
| Pipeline & repos | fmip-pipeline-repos.md | Architecture, alerts, GitHub branches and security | 2 |
| Reports | fmip-reports.md | Team and management reports, KPIs, built from validated data | 3 |
| Team apps | fmip-team-apps.md | Shift apps (Prodn-Mgt, Grain-Mgt): state, versions, maintenance | 4 |

Build order (from blueprint): Data & intake, then Pipeline & repos, then Reports, then Team apps. Coordinator runs throughout.

## Shared rules (apply to every agent)

- Record the source of every figure or fact: file path, system, or "user-provided, unverified". Never blend numbers from memory.
- No deletion or overwrite of any file without the owner's explicit approval. Outdated material goes to `_archive` only after confirmation.
- No commits, pushes, PR merges, or repo renames without approval.
- Conflicts between files or agents go to the coordinator's conflict log. Do not silently pick a version.
- October 2026 data is final. Errors are fixed only in November workbooks and reports (see corrections log).
- Output formats: Excel and WPS 365. Not Microsoft 365.
- Portuguese source terminology is kept as written. Responses to the owner are in English.
- Assumptions are labelled "Assumption:". Unknowns are labelled "UNKNOWN".
