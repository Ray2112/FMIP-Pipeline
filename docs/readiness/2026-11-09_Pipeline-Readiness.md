# FMIP pipeline readiness — 2026-11-09

**Owner:** Zhax (PM) · **Branch:** `docs/pipeline-readiness-2026-11-09` (from `origin/main` a7878de) · **Status:** Readiness check. No merges. No deletions.

## 1. What was checked

| Item | Result | Source |
|---|---|---|
| Five agent definitions: frontmatter (`name`, `description`, `tools`) | Valid. Name matches file stem. | `.claude/agents/*.md` |
| Stale statements in agent prompts (versions, PR status, local paths, Production Plan, O11 tier) | Corrected on this branch. | `.claude/agents/*.md` |
| Prodn-Mgt release `v2.5.0` | PR #6 open. Not merged. Test suite result to be recorded at merge review. | Owner-facing PR |
| Grain-Mgt release `v0.9.0` | PR #3 open. Not merged. Same. | Owner-facing PR |
| Downtime v3 in both apps | Merged to `main` (Prodn-Mgt PR #4 `ef94b0d`; Grain-Mgt PR #1 `40218a9`). | v0.5 rev 2 §4.1 |
| O11 tier | Closed: Other (D-21, owner, 6 Nov 2026). | v0.5 rev 2 §0 |
| Dropbox `/Parameters/Downtime Codes v3.xlsx` | Read 7 Nov. Conflicts with D-17 and D-21 (see §3). | Dropbox, modified 6 Nov 15:45 |
| SCADA 06.11.2026 | All zeros. Consistent with "No Production" for 6 Nov. | `/Reports/SCADA Reports/Nov. SCADA/SCADA 06.11.2026.xlsx` |
| `Maize OEE-Nov. 2026 v3.xlsx` | Read 7 Nov 09:56 UTC. Figures not re-verified today (see §4). | `/KPIs/` |

## 2. Retraction

An earlier message in this session stated that the OEE workbook shows calendar utilisation of 1.68%, equal to 2.02 h ÷ 120 h, and attributed a "days minus one" denominator to the 6 November handover. Neither statement is supported by the record I hold. Retract both. The 7 Nov read recorded Calendar 66.41% in the SUMMARY sheet. Against 2.02 run hours and 144 MTD hours, that is not arithmetically consistent either (2.02 ÷ 144 ≈ 1.4%). This needs a cell-level re-read of the formula and the denominator before any figure is used. Status: VERIFY.

## 3. Conflicts to log (not resolved by agents)

1. `/Parameters/Downtime Codes v3.xlsx` vs owner decisions:
   - P16 and P19: workbook says Other; D-17 says Process.
   - O04: workbook says Power Failure; D-17 says Other.
   - O11: workbook says Feed Mill; D-21 says Other.
   - The local attachment copy (`51922797-FMO_Downtime_Codes_v3.xlsx`, 61 codes) still lists P25; D-16 removes it.
   - Owner action: update the workbook, or confirm the decisions have changed.
2. Mill C target source. `/KPIs/Production Plan - 2026.xlsx` was deleted by the owner. The only remaining target is the THROUGHPUT TARGET column in the OEE workbook. Owner to name the governing source.
3. Dropbox `/KPIs/Yearly OEE - 2026.xlsx` existence was not re-verified. `Parameter Targets.xlsx` has not been read.

## 4. Open verification

- OEE v3 values (Capacity 61.98%, Time 40.30%, Calendar 66.41%, Quality 65.02%, OEE 17.40%, 2.02 run hours) come from the 7 Nov read. Re-read before any report uses them.
- Test suites were not re-run on the release branches in this session. Record the command and result at merge review.
- The apps have not been run in a browser against real data.
- Old records containing P25 will show as unknown codes on re-validation. Count not yet measured.

## 5. Blockers needing owner decision

| # | Decision | Owner action |
|---|---|---|
| 1 | Delete stale `downtime-v3` branches (Prodn-Mgt tip 2eb3d20; Grain-Mgt tip 7f1a3eb). | Delete on GitHub. The proxy refuses deletes from agent sessions. |
| 2 | Merge PR #6 (Prodn-Mgt `release/v2.5.0`). | Validate in app first, then decide. |
| 3 | Merge PR #3 (Grain-Mgt `release/v0.9.0`). | Same. |
| 4 | PR #2 (FMIP-Pipeline requirements v0.5, draft). | Approve or revise. Copy to `/FMIP/_docs/` only after approval (D-12). |
| 5 | Confirm downtime v3 merges were intentional and validated in the app. | Confirm. |
| 6 | Dropbox Downtime Codes v3 workbook conflicts (§3.1). | Update the workbook or confirm decisions. |
| 7 | Mill C target source (§3.2). | Name the source. |
| 8 | Calendar utilisation formula and denominator (§2). | Confirm the intended definition. |
| 9 | Glose purchasing sample (Release 3). | Provide sample. |

## 6. Readiness assessment

Agent definitions are valid and now match the repository state as of 7 Nov. The pipeline can run the document and status functions. It is not ready to produce management KPIs. Blockers 6 to 8 must close first. Scale-up to other plants stays blocked (Rule 4).

Confidence: high for the agent definitions and repository state. Medium for app behaviour, which is verified by unit tests only. Low for the OEE figures until re-read.
