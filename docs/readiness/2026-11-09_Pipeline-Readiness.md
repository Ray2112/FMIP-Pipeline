# FMIP pipeline readiness — 2026-11-09

**Owner:** Zhax (PM) · **Branch:** `docs/pipeline-readiness-2026-11-09` (from `origin/main` a7878de) · **Status:** Readiness check. Updated 9 Nov after owner review. No merges. No deletions.

## 1. What was checked

| Item | Result | Source |
|---|---|---|
| Five agent definitions: frontmatter (`name`, `description`, `tools`) | Valid. Name matches file stem. | `.claude/agents/*.md` |
| Stale statements in agent prompts (versions, PR status, local paths, Production Plan, O11 tier, Mill C target) | Corrected on this branch. | `.claude/agents/*.md` |
| Prodn-Mgt release `v2.5.0` | PR #6 open. Not merged. Test suite result to be recorded at merge review. | Owner-facing PR |
| Grain-Mgt release `v0.9.0` | PR #3 open. Not merged. Same. | Owner-facing PR |
| Downtime v3 in both apps | Merged to `main` (Prodn-Mgt PR #4 `ef94b0d`; Grain-Mgt PR #1 `40218a9`). | v0.5 rev 2 §4.1 |
| FMIP-Pipeline requirements v0.5 | PR #2 merged to `main` on 2026-11-09 10:00 UTC. | GitHub |
| O11 tier | Closed: Other (D-21, owner, 6 Nov 2026). | v0.5 rev 2 §0 |
| Dropbox `/Parameters/Downtime Codes v3.xlsx` | Read 7 Nov. Conflicts with D-16, D-17 and D-21 (see §3). | Dropbox, modified 6 Nov 15:45 |
| SCADA 06.11.2026 | All zeros. Consistent with "No Production" for 6 Nov. | `/Reports/SCADA Reports/Nov. SCADA/SCADA 06.11.2026.xlsx` |
| `Maize OEE-Nov. 2026 v3.xlsx` (Dropbox) | Text read 7 Nov 09:56 UTC. Summary values in §4. | `/KPIs/` |

## 2. Corrected reading of the 7 Nov Dropbox OEE workbook

This replaces the earlier retraction in this note, which was wrong. The 7 Nov SUMMARY row, in column order (Capacity, Time, Target, Calendar, Energy, Quality, OEE), reads:

- Capacity 66.41%
- Time 40.30%
- Target (realization column) 61.98%
- Calendar 1.68%
- Energy 0
- Quality 65.02%
- OEE 17.40%

Calendar 1.68% equals 2.02 run hours ÷ 120 hours. The earlier statement in this session that the file shows 1.68% was correct. The earlier statement that the 6 November handover used a "days minus one" denominator was not verified and remains UNKNOWN.

The 9 Nov attachment (`Maize OEE-Nov. 2026 v3.xlsx`) gives different values on recalculation: Capacity 83.92%, Time 40.93%, Quality 51.13%, OEE 17.56%. See §4.

## 3. Conflicts to log (owner decisions, not resolved by agents)

1. `/Parameters/Downtime Codes v3.xlsx` vs owner decisions:
   - P16 and P19: workbook says Other. **Owner decision 9 Nov 2026: Other.** D-17 (Process for P16 and P19) is superseded. The apps still classify them as Process (see Team Apps check), so the app code needs an owner-approved change.
   - O04: workbook says Power Failure; D-17 says Other.
   - O11: workbook says Feed Mill; D-21 says Other. **Owner decision kept: Other.**
   - P25: still listed in the attachment copy (`51922797-FMO_Downtime_Codes_v3.xlsx`, 61 codes). **Owner decision: P25 removed (D-16).**
   - Owner action: update the Dropbox workbook (tiers and P25 removal). The Dropbox connector cannot write .xlsx, so the owner has to make this edit.
2. Mill C target source. **Resolved by owner, 9 Nov 2026:** the November month-to-date target is the total of the THROUGHPUT `TARGET (kg)` column in the OEE workbook. `/KPIs/Production Plan - 2026.xlsx` was deleted by the owner. The 5,550,000 kg figure is the October target only.
3. Dropbox `/KPIs/Yearly OEE - 2026.xlsx` existence was not re-verified. `Parameter Targets.xlsx` has not been read.

## 4. Open verification

- **Current OEE (owner, 9 Nov 2026):** `Maize OEE-Nov. 2026 v3.xlsx`, Capacity utilization 83.92%, OEE 17.56%. The owner confirms the formulas in this file are correct. The 7 Nov Dropbox text reading (Capacity 66.41%, OEE 17.40%) is superseded (N-16 in the corrections log).
- Test suites were not re-run on the release branches in this session. Record the command and result at merge review.
- The apps have not been run in a browser against real data.
- Old records containing P25 will show as unknown codes on re-validation. Count not yet measured.

## 5. Blockers needing owner decision

| # | Decision | Owner action |
|---|---|---|
| 1 | Delete stale `downtime-v3` branches (Prodn-Mgt tip 2eb3d20; Grain-Mgt tip 7f1a3eb). | Delete on GitHub. The proxy refuses deletes from agent sessions. |
| 2 | Merge PR #6 (Prodn-Mgt `release/v2.5.0`). | Validate in app first, then decide. |
| 3 | Merge PR #3 (Grain-Mgt `release/v0.9.0`). | Same. |
| 4 | ~~PR #2 (FMIP-Pipeline requirements v0.5)~~ | Merged 9 Nov 2026. Closed. |
| 5 | Confirm downtime v3 merges were intentional and validated in the app. | Confirm. |
| 6 | Dropbox Downtime Codes v3 workbook: P16 and P19 tiers now Other (owner says updated; Dropbox metadata still shows last modified 6 Nov 15:45 UTC, to be confirmed). P24 and O04 tiers still to confirm. App code still shows P16, P19 as Process: owner approval needed before any app change. | Owner confirms workbook update and P24/O04; approves app change. |
| 7 | ~~Mill C target source (§3.2)~~ | Resolved 9 Nov: THROUGHPUT TARGET total. |
| 8 | Capacity and Calendar basis: which OEE file is current, and the intended definition (§2, §4). | Confirm. |
| 9 | Glose purchasing sample (Release 3). | Provide sample. |

## 6. Readiness assessment

Agent definitions are valid and match the repository state as of 9 Nov. The pipeline can run the document and status functions. It is not ready to produce management KPIs. Blockers 6 and 8 must close first. Scale-up to other plants stays blocked (Rule 4).

Confidence: high for the agent definitions and repository state. Medium for app behaviour, which is verified by unit tests only. Low for the OEE figures until the current file is confirmed.
