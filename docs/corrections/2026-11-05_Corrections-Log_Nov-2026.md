# Corrections Log — Nov 2026 workbooks

**Opened:** 2026-11-05
**Scope:** Errors found in the October 2026 sources and drafts (FMO Maize Mill C). October data is final and is not corrected. Each item below must be fixed in the November workbooks and reports, or explicitly carried as a known limitation.
**Owner:** Chief Miller / PM (Zhax). Status values: OPEN, VERIFY (needs source check), DONE.

Terminology: kept as in source (Portuguese where the source is Portuguese). Sign convention (from handover note): positive = gain, negative = loss.

## A. Source and calculation errors

| ID | Item | Where found | Detail | Action for Nov | Status |
|---|---|---|---|---|---|
| C-01 | Mill C throughput target 15,000,000 kg | `THROUGHPUT TOTALS` sheet, Old OEE workbook (per handover note) | Not found in `/KPIs/Production Plan - 2026.xlsx` (no 15,000,000 value in Daily_Entries or Weekly_Summary). Production Plan Line C daily targets for weeks 39–43 sum to 5,580,000 kg. The handover uses 5,550,000 kg as the plan. | Derive the Mill C target from Production Plan 2026 only. Reconcile 5,580,000 vs 5,550,000 before any capacity figure is reported. Correct the THROUGHPUT TOTALS sheet in the Nov workbook. | VERIFY |
| C-02 | Capacity 76.7% (4,257,526 kg vs 5,550,000 kg) | Handover note, Figures to carry forward | Denominator depends on C-01. | Recalculate once C-01 is closed. | OPEN |
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

## Revision history

| Date | Change | By |
|---|---|---|
| 2026-11-05 | Initial log from handover note (2026-11-04) and Production Plan 2026 check | Claude |
