# App redesign requirements — Prodn-Mgt and Grain-Mgt (v0.1, DRAFT)

**Date:** 2026-11-05 · **Owner:** Zhax (PM) · **Status:** Requirements as stated by owner, not yet scoped or approved. Items marked ASK need an answer before design.

Terminology kept as in source where possible. The apps are in Portuguese; the owner works in English.

## 0. Convention: Dropbox landing (applies to all apps)

Proposed, not yet agreed:
- One root folder for all pipeline data, e.g. `/FMIP/`.
- One sub-folder per app and report type, e.g. `/FMIP/prodn-mgt/shift/`, `/FMIP/grain-mgt/shift/`.
- One naming pattern for every file: `AAAA-MM-DD_<turno>_<app>_<tipo>.json` (date first so files sort).
- Test data in `/FMIP/_test/`, never in live folders.
- Every file carries a manifest: app version, shift, sign-off status, record counts.

ASK: approve this structure, or name the changes. It replaces `/Apps/Mill-CD/` and `/Apps/Mill-App-Sync/` (open item S-01).

## 1. Prodn-Mgt — shift-based redesign

### 1.1 Shift sign-in (shift leader)
- Opening scale figures.
- Homepage lists all activities for the shift, each with its target: production, conditioning, reception, housekeeping, re-processing.
- Breakdowns logged during the shift via a dropdown of **Downtime codes v3**.
- Sign-off section: actuals and comments.
- Closing scale figures.

Existing: shift log and shift scale readings (Prodn-Mgt v2.2.0). Downtime codes: README v1.4.0 lists codes **v2**; v2.3.3 says "P18 conforme v3". Handover note also names v3 as governing. **Confirm the app is on v3.**

### 1.2 Quality — auto-control (when production or conditioning is on)
- Hourly checks: dry maize, maize to B1, Fuba moistures, protein, fat, fibre.
- Report per shift, exportable to Excel, same content as the Análise sheet in the KPIs file.

ASK: the Análise sheet is in the KPIs file. I have not opened it. Which file exactly, and which sheet? Is it the Analise tab of `Production Plan - 2026.xlsx`, or `Yearly OEE - 2026.xlsx`?

### 1.3 Maintenance (shift)
- Breakdowns pending; preventive work arranged; consumables required and their status (bought, ordered, etc.).
- Consumables status is tracked in a workbook called **"Glose"** (owner's term).
- Sign-off section: status of each job logged in the shift.
- Export to Excel and to 365.

Existing: Maintenance tab (Prodn-Mgt v2.4.0; Grain-Mgt v0.8.0).

ASK: what is "Glose"? A product, a workbook name, or a typo? Is it an existing file I should open?
ASK: "365" — Microsoft 365 or WPS 365? (You have a WPS Cloud folder.) Export targets differ.

### 1.4 Roll care
- Fluting office: opening status; rolls on fluting 1 and 2; rolls on grinding 1 and 2; current status of each.
- Roll change: which rolls are due at shift sign-in; status at sign-off.
- Sign-off with current status.

Existing: `roll-passages.js` exists in Prodn-Mgt. Its scope has not been read.

### 1.5 FSSC 22000 section
- Daily checklists; verification of filing.
- Export as workbooks.
- Daily targets and sign-off status.
- MTD (month-to-date) compliance dashboard.

Existing: FSSC module (both apps).

### 1.6 Exports
- Every report exports to Excel and to 365 / WPS 365 (see ASK above).
- Every report also lands in Dropbox per section 0.

## 2. Grain-Mgt — same approach as Prodn-Mgt
- Shift sign-in; opening scale figures.
- Jobs available, with sign-off.
- Shift leader records any intake, transfers, and turnovers during the shift.
- Silos under treatment (status).
- End-of-shift report with scale figures.
- Scale figures export to the daily report, as Excel.
- Maintenance: same as Prodn-Mgt (1.3).
- FSSC: same as Prodn-Mgt (1.5).

Existing: maintenance, FSSC, silo sensors, bins feed, Excel export (xlsx.mini.min.js in vendor), Dropbox records (v0.7.0).

## 3. Scope control (recommended, not yet agreed)

This is a lot for one release. Recommended phasing:

- **Release 1 (pipeline-ready):** shift sign-in, opening/closing scale figures, downtime v3 dropdown, shift sign-off, Dropbox landing per section 0, Excel export of the shift report. This is the minimum for the pipeline to receive shift data.
- **Release 2:** quality auto-control (1.2) and maintenance with Glose (1.3).
- **Release 3:** roll care (1.4), FSSC dashboard (1.5), and Grain-Mgt parity (2).

Reason: Release 1 gives the pipeline its first real shift feed. The rest depends on Release 1 being stable.

ASK: approve phasing, or move items between releases.

## 4. Open questions (summary)

1. Approve Dropbox structure (section 0)?
2. Confirm Prodn-Mgt is on downtime codes v3.
3. Which file and sheet is the "Análise" source?
4. What is "Glose"?
5. Microsoft 365 or WPS 365?
6. Approve release phasing (section 3)?

## 5. Not yet verified
- No requirement above has been tested against the current app code.
- Existing modules are taken from changelog headings only. Code has not been read.
