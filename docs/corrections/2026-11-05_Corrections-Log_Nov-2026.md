# Corrections Log — Nov 2026 workbooks

**Opened:** 2026-11-05
**Scope:** Errors found in the October 2026 sources and drafts (FMO Maize Mill C). October data is final and is not corrected. Each item below must be fixed in the November workbooks and reports, or explicitly carried as a known limitation.
**Owner:** Chief Miller / PM (Zhax). Status values: OPEN, VERIFY (needs source check), DONE.

Terminology: kept as in source (Portuguese where the source is Portuguese). Sign convention (from handover note): positive = gain, negative = loss.

## A. Source and calculation errors

| ID | Item | Where found | Detail | Action for Nov | Status |
|---|---|---|---|---|---|
| C-01 | Mill C throughput target | Production Plan 2026, Daily_Entries (Line C, Target thruput), dates 1–31 Oct 2026 | Formula: Target throughput (month) = sum of Line C daily Target thruput (kg) for calendar dates in the month. Oct 2026: 1,585,000 (5–9 Oct) + 500,000 (15 Oct) + 2,575,000 (19–24 Oct) + 890,000 (30–31 Oct) = **5,550,000 kg**, matching the plan used in the handover. The 15,000,000 kg in the THROUGHPUT TOTALS sheet of the Old OEE workbook is not supported by the Production Plan. Note: the 5,580,000 kg figure in the earlier check was weeks 39–43, which includes 24–25 Sep; it is not the October total. | Use the formula above for all future targets. Correct THROUGHPUT TOTALS in the Nov workbook. | DONE (formula confirmed by owner) |
| C-02 | Capacity 76.7% (4,257,526 kg vs 5,550,000 kg) | Handover note, Figures to carry forward | Denominator is now the formula-derived 5,550,000 kg (see C-01). | Recalculate the capacity figure from actuals on the same date basis. | VERIFY |
| C-03 | S17 variance +83,472 kg; ledger closing −63,472 kg | Silo reconciliation (handover note, Open items) | A negative ledger closing needs checking against the sign convention. | Check against S03 level log for 5 Oct before correcting. | VERIFY |
| C-04 | D/M bins gain +28,388 kg | Silo reconciliation | Physical 347,753 vs ledger 319,365. Unexplained. | Investigate the cause; document the explanation. | OPEN |
| C-05 | Returns 53,900 kg not in mill balance | Handover note, Open items | Returns are not reflected in the mill balance. | Add returns to the mill balance, or document why they are excluded. | OPEN |
| C-06 | Transfer row dated 13 Mar 2025 (S03 → S07, 62,234 kg) | Transfer table | Outside October; excluded from totals. | Confirm whether the row is a data-entry error or a valid prior-period item. Keep excluded unless confirmed. | VERIFY |
| C-07 | `#REF!` in one cell | SUMMARY sheet | Broken reference. | Fix the reference in the Nov workbook; do not rely on the SUMMARY sheet until fixed. | OPEN |
| C-08 | Unlabelled percentages | SUMMARY sheet | Meaning of several percentages not stated. | Label each one (basis and denominator) in the Nov workbook. | OPEN |
| C-09 | Silo reconciliation workbook and charts | `2026-11-04_Silo-Reconciliation-Oct-2026.xlsx`, waterfall and grain-movement PNGs | Show old closing 21,111,203 kg. Correct closing is 20,764,731 kg. | Rebuild the workbook and both charts on corrected figures. Do not reuse the old PNGs. | OPEN |
| C-10 | Silo ledger closing 20,764,731 kg; physical 20,697,000 kg; variance −67,731 kg | Handover note | Arithmetic checked: 25,645,000 − 4,880,269 = 20,764,731; 20,697,000 − 20,764,731 = −67,731. Ledger inputs not yet re-verified against the source workbook. | Re-verify against the source before the Nov reconciliation. | VERIFY |
| C-11 | Monthly OEE 42.8% vs minimum 74.99% | Handover note | Monthly calculation uses monthly totals. Daily OEE was withdrawn for October. | Confirm the method for Nov (daily OEE applies from Nov under the saved method). Do not mix daily and monthly methods in one figure. | VERIFY |
| C-12 | Daily Engineering hours | Handover note, Open items | Daily OEE must not be used until daily Engineering hours are read directly from the sheet. | Read daily Engineering hours from source before any daily OEE. | OPEN |

## B. Downtime codes

| ID | Item | Where found | Detail | Action for Nov | Status |
|---|---|---|---|---|---|
| D-01 | P50 classification | `/Reports/Downtime Codes v3.xlsx` | Unscheduled hours (Mill C) 38.64 h classed as Engineering, P50. Classification needs correcting for November. | Correct the P50 classification in v3 (or v4) for Nov; record the change here. | OPEN |
| D-02 | Withdrawn downtime pie chart | `2026-11-04_Downtime-Codes-Oct-2026.png` | Withdrawn. | Do not reuse. Regenerate from corrected codes if needed. | OPEN |

## C. Production Plan 2026 open items (from the workbook's own Start_Here sheet)

| ID | Item | Where found | Detail | Action for Nov | Status |
|---|---|---|---|---|---|
| P-01 | I-03: days with production and no plan | Daily_Entries, weeks 39–44 | Several Line C days have actuals but no target (Weekly_Summary "Days with actual but no plan" = 2, 1, 1). | Enter the missing plan or record why there is none. | OPEN |
| P-02 | I-07: "Fuba 2" spelling in week 40 | Daily_Entries, week 40 | Spelling inconsistency. | Correct the spelling in the source. | OPEN |
| P-03 | I-14: kg unit | Production Plan | Open item in source. | Resolve in source. | OPEN |
| P-04 | I-18: F.Integral colour and target | Production Plan | Colour and target missing. | Resolve in source. | OPEN |
| P-05 | Week 44 entries | Daily_Entries | v2 corrections cover weeks 37–43 only. Week 44 holds a target of 1,140,000 kg and actuals not yet corrected. | Confirm the week 44 figures before using them. | VERIFY |
| P-06 | Week 40 "Re-processing" and "NO ACTUAL" rows | Daily_Entries | Re-processing rows (11 Oct, 26 Oct) carry no target or actual in some fields. | Clarify whether re-processing counts toward Mill C throughput. | OPEN |

## D. Structural and naming issues (affect the pipeline, not the figures)

| ID | Item | Detail | Action | Status |
|---|---|---|---|---|
| S-01 | Two Dropbox folders for the same apps | Prodn-Mgt writes to `/Apps/Mill-CD/records/` (file pattern `AAAA-MM-DD_FMO_MillQC.json`). Grain-Mgt writes to `/Apps/Mill-App-Sync/records/` (pattern `AAAA-MM-DD_FMO_GrainMgt.json`). | Decide one landing convention for the pipeline. Do not change either app until agreed. | OPEN |
| S-02 | Repo and app names out of step | Prodn-Mgt was renamed from Mill-QC (v2.3.1), but the repo is still `ray2112/mill-qc`. Grain-Mgt was renamed from Mill-App; repo is `ray2112/Mill-App`. | Note in the pipeline architecture. Rename only with approval. | OPEN |
| S-03 | Support scripts in a temporary folder | `build_reports_v5.py`, `silo_recon.py`, `verify_stats.py` and v2–v4 drafts sit under `/tmp` per handover note. Not durable. | Move scripts into this repo (version-controlled). Move v2–v4 drafts and the old silo workbook to Archive after your confirmation. | OPEN |
| S-04 | Scripts not yet received | Not on the connected computer at the time of this log. | Attach or connect the folder; then update scripts. | OPEN |

## E. Decisions recorded

- October data is final. No October figure is corrected in this log. Errors are fixed only in Nov workbooks and reports.
- Deletion: none. Old drafts are not deleted until you confirm the Archive step (see S-03).

## F. November OEE workbook: decisions and open conflicts (added 2026-11-09)

Source for all rows: `Maize OEE-Nov. 2026 v3.xlsx` (Dropbox `/KPIs/`, same document as the attachment supplied 2026-11-09). Figures are MTD working values, not reconciled.

| ID | Item | Where found | Detail | Action | Status |
|---|---|---|---|---|---|
| N-01 | Capacity (K7) denominator | `SUMMARY!K7` = `D13/(20833*ENGINEERING!G34)` | Owner decision 2026-11-09: capacity is based on available production time, so days with no plan are excluded. Workbook formula used. Supersedes the K7 formula `THROUGHPUT!E253 / (500000 × (COUNT(E2:E31) − 1))` recorded earlier. | Use workbook formula for Nov. | DONE (owner decision) |
| N-02 | Quality (P7) basis | `SUMMARY!P7` = `MOISTURE!$G$253` = `(H249/E249)×0.1055` | Owner decision 2026-11-09: follow the workbook. In this file row 250 is blank (E250, H250 empty), so the earlier rule `MOISTURE!G254 = (H250/E250)×0.1055` cannot be evaluated. Superseded for Nov. | Use row 249 for Nov. | DONE (owner decision) |
| N-03 | Nov OEE figures | `SUMMARY!K7:Q7`, LibreOffice recalculation of the attachment | Capacity 83.92%, Time 40.93%, Quality 51.13%, OEE 17.56%. Stored cache in the attachment agrees with the recalculation. | Working values only; report with basis and denominator (C-08). | VERIFY |
| N-04 | Double counting in OEE | `SUMMARY!L7` = `K7*(G34/(D253/20833))*P7`; `Q7` = `K7*L7*P7` | L7 already contains K7 and P7, so Q7 counts capacity and quality twice. Owner has seen this and asked to follow the workbook for now. | Owner decision needed on the OEE formula. Do not change Nov figures until decided. | OPEN |
| N-05 | Dropbox copy vs attachment | Dropbox text extraction (earlier read) vs `SUMMARY!K7:Q7` | Earlier extraction: Capacity 66.41%, Time 40.30%, Quality 65.02%, OEE 17.40%. Attachment and recalculation: 83.92%, 40.93%, 51.13%, 17.56%. Owner confirms both are the same document. Conflict not explained. | Owner to open Q7 in Excel and report the displayed value. | VERIFY |
| N-06 | Realization (M7) and Calendar (N7) | `SUMMARY!M7` = `THROUGHPUT!E253/THROUGHPUT!D32` (80.04%); `N7` (25.07%) | Target basis `THROUGHPUT!D32` not checked against C-01 (Mill C monthly target). | Check D32 against the Production Plan formula before reporting. | OPEN |
| N-07 | Silo reconciliation timing | `SUMMARY` silo block; `Actual` column (O) empty | Owner decision 2026-11-09: silo reconciliation is done only at month-end. Current variances are not meaningful. | Reconcile at month-end. | DONE (owner decision) |
| N-08 | "Maize OEE - Nov. 26.xlsx" | Dropbox `/KPIs/` and `/KPIs/Old OEEs/` | Not found on 2026-11-09 (the file ID recorded earlier returns NOT_FOUND). A copy exists as an attachment from 6 Nov. Owner asked for it to be deleted; nothing was deleted because nothing was found. | Owner to confirm the file is gone. | VERIFY |
| N-09 | Remote branches on GitHub | `downtime-v3`, `o11-tier-other` (Prodn-Mgt, Grain-Mgt); `feat/fmip-agent-team` (FMIP-Pipeline) | Delete attempts refused by the proxy (HTTP 403) on 2026-11-09. Branches are merged per v0.5 §4.1 (not re-verified through the API). | Owner to delete on GitHub after confirming merge. | OPEN (superseded in part by N-11) |
| N-10 | Nov OEE file of record | Dropbox `/KPIs/Maize OEE-Nov. 2026 v3.xlsx` (`id:1V5iV_HsI3AAAAAAAAABAw`) | Owner decision 2026-11-09: use the v3 file in Dropbox. It is the only Nov OEE workbook in `/KPIs/`. Supersedes the "Maize OEE - Nov. 26.xlsx" reference in the handover (6 Nov) and N-08. | Use v3 as the governing workbook. | DONE (owner decision) |
| N-11 | GitHub state checked 2026-11-09 | Prodn-Mgt PRs #4 and #5, Grain-Mgt PRs #1 and #2, FMIP-Pipeline PR #1 | All merged on 2026-11-06 (FMIP-Pipeline PR #2 merged 2026-11-09). The handover statement that these PRs are open is stale. Branches `downtime-v3` and `o11-tier-other` (both app repos) and `feat/fmip-agent-team` still exist. Delete retried on 2026-11-09: refused (HTTP 403) for all five. Not touched: Prodn-Mgt PR #6 (`release/v2.5.0`, open) and Grain-Mgt PR #3 (`release/v0.9.0`, open). | Merge verified. Owner to delete the three branch names on GitHub. | VERIFY (merge verified; deletion OPEN) |
| N-12 | Downtime Codes v3 location | Log section B, D-01 (`/Reports/Downtime Codes v3.xlsx`) | Owner confirmed 2026-11-09: the file is in `/Parameters/`. The `/Reports/` reference is superseded. | Use `/Parameters/Downtime Codes v3.xlsx`. | DONE (owner confirmation) |
| N-13 | Landing convention | S-01 | Owner decision 2026-11-09: D-1 in force (`/FMIP/`, per-app folders). Whether the apps' current write paths (`/Apps/Mill-CD/records/`, `/Apps/Mill-App-Sync/records/`) move to `/FMIP/` is not decided. | Decide the app path move separately. | DONE (D-1 in force); OPEN (app path migration) |
| N-14 | Capacity rule in force | Status note 2026-11-07 and handover s.3 (`500,000 kg/day × (days − 1)`) | Owner decision 2026-11-09: the N-01 rule (`20833 × ENGINEERING!G34`, available production time) is the rule in force. The older rule is superseded. | Apply N-01 to all Nov capacity figures (C-02). | DONE (owner decision) |
| N-15 | November Mill C target source | Owner, 9 Nov 2026. Supersedes the N-06 open check and the Production Plan basis of C-01 | The November month-to-date target is the total of the THROUGHPUT `TARGET (kg)` column in `Maize OEE-Nov. 2026 v3.xlsx`. The Production Plan was deleted by the owner. The 5,550,000 kg figure in C-01 is the October target only. | Use the THROUGHPUT TARGET total for Nov MTD targets. | DONE (owner decision) |
| N-16 | Dropbox 7 Nov vs 9 Nov attachment | Dropbox text read 7 Nov 09:56 UTC vs attachment `Maize OEE-Nov. 2026 v3.xlsx` (9 Nov) | Summary values differ. 7 Nov text: Capacity 66.41%, Time 40.30%, Target 61.98%, Calendar 1.68%, Quality 65.02%, OEE 17.40%. Attachment recalculated: Capacity 83.92%, Time 40.93%, Quality 51.13%, OEE 17.56%. The 7 Nov text contains Mill D toggle notes (`ENGINEERING!K2`) not yet checked in the attachment. | Owner to confirm which file is current. Do not use either set of figures in a report until confirmed. | OPEN |
| N-17 | Downtime Codes v3 workbook | `/Parameters/Downtime Codes v3.xlsx` vs D-16, D-17, D-21 | Owner decisions kept: O11 = Other (D-21); P25 removed (D-16). P16/P19 = Process and O04 = Other (D-17) are not yet in the workbook. The Dropbox connector cannot write .xlsx. | Owner edits the workbook in Dropbox. | OPEN (owner edit) |

## Revision history

| Date | Change | By |
|---|---|---|
| 2026-11-05 | Initial log from handover note (2026-11-04) and Production Plan 2026 check | Claude |
| 2026-11-09 | Added section F (N-01 to N-09): owner decisions on Nov OEE capacity, quality basis and silo timing; open OEE double-count and Dropbox/attachment conflict; GitHub branch deletes refused. Existing entries not changed. | Claude |
| 2026-11-09 | Added N-10 to N-14: Dropbox v3 as Nov OEE file of record; GitHub merge state verified (branch deletes still refused); downtime file in `/Parameters/`; D-1 landing convention in force; N-01 capacity rule in force. N-08 and N-09 kept as written; N-10 and N-11 supersede them. | Claude |
| 2026-11-09 | Added N-15 to N-17: November Mill C target source (THROUGHPUT TARGET total); Dropbox 7 Nov vs attachment conflict; Downtime Codes v3 workbook edits. N-06 kept as written; N-15 closes it. | Claude |
