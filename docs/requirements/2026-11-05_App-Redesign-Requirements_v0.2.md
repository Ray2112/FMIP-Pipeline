# App redesign requirements — Prodn-Mgt and Grain-Mgt (v0.2, DRAFT)

**Date:** 2026-11-05 · **Owner:** Zhax (PM) · **Supersedes:** v0.1 (kept unchanged).
**Status:** Owner answers from v0.1 are recorded below. Phasing is approved. Items marked OPEN need an answer before design.

## 0. Decisions recorded (from owner, 2026-11-05)

| # | Item | Decision |
|---|---|---|
| D-1 | Dropbox convention | Approved. Root `/FMIP/`, per-app and per-report folders, naming `AAAA-MM-DD_<turno>_<app>_<tipo>.json`, test data in `/FMIP/_test/`, manifest in every file. Folder tree being created by an agent (no moves or deletes). |
| D-2 | Downtime codes | Replace the app list with **Downtime Codes v3** from `/Parameters`. Diff and open decisions are in `docs/method/2026-11-05_Downtime-Codes-v3-Diff.md`. |
| D-3 | "Análise" source | `/KPIs/Analise de qualidade de fuba - Nov. 26.xlsx` (see section 2 for issues). |
| D-4 | "Glose" | Asset management software used by the plant. Tracks purchasing, preventive maintenance, breakdowns. Export/import route not yet defined (see OPEN). |
| D-5 | Office suite for export | **WPS 365** (not Microsoft 365). |
| D-6 | Release phasing | Approved as proposed in v0.1 section 3 (Release 1, 2, 3). |

## 1. Release 1 scope (approved)

- Shift sign-in by shift leader: opening scale figures; homepage listing all shift activities with targets (production, conditioning, reception, housekeeping, re-processing).
- Breakdowns during the shift via dropdown of Downtime Codes v3 (per D-2).
- Sign-off: actuals and comments. Closing scale figures.
- Dropbox landing per the approved convention (D-1).
- Excel export of the shift report (WPS 365-compatible per D-5).

## 2. Análise (quality auto-control) — source definition, for Release 2

Source: `/KPIs/Analise de qualidade de fuba - Nov. 26.xlsx`, as read 2026-11-05.

Structure observed:
- **Summary** sheet: monthly summary and one row per day.
- **Day sheets 01–30:** hourly rows from 07:00 to 06:00 (next day). Each day has Line C and Line D blocks and a laboratory block.
- Hourly column headers: Milho Seco · H/Milho % · Gordura % · H/Fuba % (Line C and Line D), and Seco · Humido · Gordura · Fuba (laboratory).
- Each day sheet has an **Ave.** row.

Issues found (not yet resolved):
1. **Column mismatch.** The Summary headers are *Milho Seco · Degerm % · Gordura % · H/Fuba %*. The hourly headers are *Milho Seco · H/Milho % · Gordura % · H/Fuba %*. The Summary's "Degerm %" sits where the hourly sheets have H/Milho %. The values are 17.35 (Degerm/H/Milho), 2.21 (Gordura), 13.62 (H/Fuba). **Which label is correct?** Needed before any automated check.
2. **Only 1 of 30 days has data** (1 Nov, Line C, 2 hourly readings: 10:00 and 11:00). The rest are blank. Day 02 onward is empty.
3. **Line D** has no readings in any day.
4. **Laboratory block** is empty in all day sheets.
5. **Division errors** (`#DIV/0!`) in the Ave. rows for empty days.
6. **Summary "D" block** (Line D) is empty.
7. Minor: header typo "LABORTORY TESTS" on day sheets 26–30.
8. **Unit ambiguity:** H/Milho % (~17) vs H/Fuba % (~13.6) are both plausible moisture values, but the file doesn't say which is which. Not assumed.

## 3. Maintenance and Glose — for Release 2

- Shift maintenance: breakdowns pending; preventive work arranged; consumables required and status.
- Glose is the asset management system; the pipeline must not duplicate its data. Proposal: the app records shift-level maintenance events; Glose remains the master for purchasing and preventive plans.

OPEN: how Glose data gets in and out — manual export/import (file), API, or none? Glose's export format is not known. Needs a sample file.

## 4. FSSC 22000, roll care, Grain-Mgt parity — Release 3

Unchanged from v0.1 sections 1.4, 1.5 and 2. Not designed yet.

## 5. Exports

- Every report exports to Excel and WPS 365 (D-5), and lands in Dropbox per D-1.
- Microsoft 365 is not in scope.

## 6. Open questions

1. Which label is correct for the Análise Summary column (section 2, issue 1)?
2. P17 name and P25 handling — see the downtime diff doc (decisions 1–2).
3. Glose: export/import format, and a sample file (section 3).
4. Confirm the downtime tier and OEE-treatment decisions in the diff doc.

## 7. Not verified

- Existing app code has not been tested against any of the above.
- The Dropbox folder tree is being created by an agent; its result will be recorded separately.
