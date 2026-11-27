# Source register — FMIP Pipeline

**Opened:** 2026-11-05 · **Owner:** Zhax (PM) · **Status:** DRAFT — locations and formats are as observed; contents are not verified unless marked.

Purpose: one place that says where every input and output of the pipeline lives, what format it is in, who writes it, and whether it is current. The pipeline reads from these sources; it does not edit them.

Terminology kept as in source (Portuguese where the source is Portuguese).

## 1. Automated feeds (written by apps)

| ID | Source | Location | Format | Written by | Read by | Status |
|---|---|---|---|---|---|---|
| F-01 | Prodn-Mgt daily records | Dropbox `/Apps/Mill-CD/records/AAAA-MM-DD_FMO_MillQC.json` | JSON, schema 2, one file per production day (07:00–07:00), with manifest | Prodn-Mgt (repo `ray2112/mill-qc`) | Pipeline | Documented in app README v2.1.0; not yet sampled |
| F-02 | Prodn-Mgt test records | Dropbox `/Apps/Mill-CD/records-test/` | JSON, same schema | Prodn-Mgt | Exclude from reports | Documented |
| F-03 | Grain-Mgt daily records | Dropbox `/Apps/Mill-App-Sync/records/AAAA-MM-DD_FMO_GrainMgt.json` | JSON with manifest; closed after 07:00 | Grain-Mgt (repo `ray2112/Mill-App`) | Pipeline | Documented in app README v0.7.0; not yet sampled |
| F-04 | Bin status (maize silos) | Dropbox `/Apps/Mill-CD/bins-status.json` | JSON: balance and transfers per dirty maize bin since last empty | Prodn-Mgt v2.0.0 | Grain-Mgt; pipeline | Documented; not yet sampled |
| F-05 | Silo temperature reports | Dropbox `/Temperature Readings/silo-temps.json` | JSON from monitoring system; Amber/Red readings per SOP-OPS-002 | Monitoring system (external) | Grain-Mgt | Documented in Grain-Mgt README v0.8.0 |
| F-06 | Shift scale readings (B1) | Inside daily records (F-01) | Field within JSON, format 2 | Prodn-Mgt v2.2.0 | Pipeline | Documented |

**Conflict to resolve (S-01 in corrections log):** Prodn-Mgt writes to `/Apps/Mill-CD/`; Grain-Mgt writes to `/Apps/Mill-App-Sync/`. Two Dropbox app folders and two file-name patterns (`_FMO_MillQC` vs `_FMO_GrainMgt`) are in use. The pipeline needs one agreed landing convention. No app has been changed.

## 2. Manual and spreadsheet sources (Dropbox, read-only)

| ID | Source | Location | Use | Status |
|---|---|---|---|---|
| M-01 | Old OEE — October | `/KPIs/Old OEEs/Maize OEE - Oct. 26.xlsx` | October source (final, not corrected) | Re-read per handover note |
| M-02 | Production Plan 2026 | `/KPIs/Production Plan - 2026.xlsx` | Planned days, daily targets (Line C); target formula in `docs/method/target-throughput.md` | Read 2026-11-05; formula confirmed |
| M-03 | Parameter Targets | `/KPIs/Parameter Targets.xlsx` | Quality and parameter targets | Listed in handover note; not opened |
| M-04 | Downtime Codes | `/Reports/Downtime Codes v3.xlsx` | Governing downtime codes; P50 classification to correct for Nov | Listed; not opened |
| M-05 | Yearly OEE 2026 | `/KPIs/Yearly OEE - 2026.xlsx` | Original; not editable in place | Listed; not opened |

## 3. Local copies (on Zhax's computer, Downloads)

These are working copies and are not authoritative. The pipeline must not read them without a source note.

| ID | File | Note |
|---|---|---|
| L-01 | `2026-11-05_Maize-OEE-Oct-26_linked_v2.xlsx` / `_v3.xlsx` | Linked OEE copies. Versions differ (v2 larger than v3). Which is current is unknown. |
| L-02 | `2026-11-05_Maize-OEE-Nov-26_linked_v2.xlsx` / `_v3.xlsx` | November OEE working copies. Same issue. |
| L-03 | `2026-11-05_Monthly-Report-Oct-2026_*_DRAFT_v6.html` | Team and Management drafts. v6 uses the corrected silo closing (20,764,731 kg) and the 5,550,000 kg target, and has no `#REF!`. The handover note names v5 as current. v6 supersedes v5 (to confirm). |
| L-04 | SCADA hourly report, Line C: `SCADA DD.MM.AAAA.xlsx` | **Now a daily feed read by the pipeline** (handover v4 §5, Confirmed). Lands in Dropbox `/Reports/SCADA Reports/Nov. SCADA/`. Owner, deadline and the 25/11 gap check are in section 3a. The early local copies (29.10, 30.10, 01.11) are no longer in Downloads (checked 2026-11-25). |
| L-05 | `2026-10-22_Production_Plan_2026_Corrected_Wk37-43_v2.xlsx` and `…_Daily_Wk37-43_v2.csv` | Corrected Production Plan v2 (weeks 37–43). Superseded by M-02 in Dropbox for planning. |
| L-06 | `Mill C - Preventative.xlsx`, `Silos Section - Prevention.xlsx`, `Rollermills Maintenance.xlsx` | Maintenance sources. Feed for team apps / maintenance agent. |
| L-07 | `2026-10-22_Moagem_Recepcao-Silos-Armazenagem_*.xlsx` (several) | Reception, silo and storage workbooks. Multiple versions for the same period. Conflict to resolve. |

## 3a. L-04 SCADA daily upload: owner, deadline, current gap

**Checked 2026-11-25** (Dropbox `/Reports/SCADA Reports/Nov. SCADA/`, email inbox, PC Downloads).

### How the file gets to Dropbox today (Confirmed from timestamps and mail)
1. The SCADA hourly report (07:00→07:00, Line C) is exported to `.xlsx` at the mill.
2. It is emailed to an inbox the pipeline owner reads.
3. It is saved by hand into the Dropbox folder above. There is no automatic step.

Uploads to Dropbox were done in batches, not daily: 05/11, 06/11, 07/11, then 13 files on 14/11 at 19:11–19:12 UTC. That is the last Dropbox upload.

### Where it broke (Confirmed)
| Day | Exported and emailed | In Dropbox |
|---|---|---|
| 01–13.11 | yes | yes |
| 14.11, 15.11 | yes, one email 16/11 08:07 UTC | **no** |
| 16.11 | yes, email 17/11 09:29 UTC | **no** |
| 17.11–24.11 | **no email found** | **no** |

- Two separate breaks: (a) step 3 stopped after 14/11, so three files sit only in Gmail; (b) from 17.11 no export was emailed at all.
- Why: **Unknown.** There is no record of the cause. The chain depends on one person doing two manual steps.
- This explains the open conflict in D55: a 14.11/15.11 file did exist, but only in Gmail, not in Dropbox.

### Owner and deadline
| Item | Value | Status |
|---|---|---|
| Owner of the upload (Gmail → Dropbox) | An upload agent, to be built | Confirmed (owner, 27 Nov 2026). Agent not built yet; until it exists the step is manual |
| Owner of the SCADA export at the mill | **Zhax**, from 08/12/2026 (interim) | Confirmed (owner, 27 Nov 2026: "For now I will do it, starting 08/12"). The agent can only move a file that was exported and emailed |
| Daily deadline | **09:00** for the previous 07:00→07:00 day | Confirmed (owner, 27 Nov 2026). Three hours before the 12:00 pipeline run (D30) |
| Back-filling 14.11–24.11 | Not required | Confirmed (owner, 27 Nov 2026: "Don't worry about previous data") |
| Missing file rule | Report shows "sem dados / no data"; never estimated | Confirmed (standing rule) |

## 4. Gaps

- No sample of any F-series JSON has been opened yet. Schemas are taken from app READMEs only.
- No owner or retention rule is recorded for any source.
- Silo, bin and temperature feeds (F-04, F-05) and their Nov coverage are not verified.
- L-04 SCADA: upload agent and 09:00 deadline agreed; agent not built; export by Zhax from 08/12/2026, interim (section 3a). Schema is in the decision log (hourly rows in tonnes: Clean, Screening, B1, Flour 1, Flour 2, Germ, Z.F).

## 5. Next actions

1. Open one F-01, F-03 and F-04 file each to confirm the schema matches the README.
2. Agree the single Dropbox landing convention (S-01).
3. Decide which L-series file is authoritative for each month (L-01, L-02, L-03, L-07).
