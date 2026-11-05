# App redesign requirements — Prodn-Mgt and Grain-Mgt (v0.3, DRAFT)

**Date:** 2026-11-05 · **Owner:** Zhax (PM) · **Supersedes:** v0.2 (kept unchanged).
**Status:** Owner decisions to date are recorded in section 0. Items marked OPEN need an answer before design.

## 0. Decisions recorded

| # | Item | Decision |
|---|---|---|
| D-1 | Dropbox convention | Approved. `/FMIP/`, per-app folders, naming `AAAA-MM-DD_<turno>_<app>_<tipo>.json`, test in `/FMIP/_test/`, manifest in every file. |
| D-2 | Downtime codes | Replace app list with **Downtime Codes v3** from `/Parameters`. Diff: `docs/method/2026-11-05_Downtime-Codes-v3-Diff.md`. |
| D-3 | "Análise" source | `/KPIs/Analise de qualidade de fuba - Nov. 26.xlsx`. Corrected copy: v2 (section 4). |
| D-4 | "Glose" | Asset management software: purchasing, preventive maintenance, breakdowns. See D-11. |
| D-5 | Export format | **WPS 365**. Microsoft 365 is not in scope. |
| D-6 | Release phasing | Approved (v0.1 section 3). |
| D-7 | Owner of quality, maintenance, roll care, FSSC, daily/monthly reports | **Prodn-Mgt.** |
| D-8 | Folder names | "scale" and "shift" approved. Created: `/FMIP/prodn-mgt/{shift,scale,quality,maintenance,roll-care,fssc,reports}`, `/FMIP/grain-mgt/{shift,scale}`, `/FMIP/_test`, `/FMIP/_archive`, `/FMIP/_docs`. |
| D-9 | Top-level `/FMIP/` files | Old `FMO_Relatorio` / `FMO_Semana` HTML files: deleted by owner. Handover `.md` left in place. |
| D-10 | OEE treatment | Add a v3 OEE-treatment column, **applied to November 2026 onward only**. October is not recalculated. Table: `docs/method/2026-11-05_Downtime-Codes-v3_OEE-Treatment.csv`. |
| D-11 | Glose scope | **The pipeline does not track Glose data.** It tracks only the jobs it is given. Glose is referenced only for purchasing of materials: order number, breakdown number, status. Sample file to be provided by owner. |
| D-12 | Requirements in Dropbox | Copied to `/FMIP/_docs/`. |
| D-13 | Análise labels | "Degerm %" (summary) and "H/Milho %" (day sheets) are the same measure. Label: **EN "Maize to Degerm moisture content %" / PT "Milho Limpo Humidade %"**. |
| D-14 | Análise #DIV/0! | Resolved in v2: averages return blank where there is no data. |

## 1. Release 1 scope

- Shift sign-in by shift leader: opening scale figures; homepage listing shift activities with targets (production, conditioning, reception, housekeeping, re-processing).
- Breakdowns during shift via dropdown of Downtime Codes v3, with OEE-treatment per D-10.
- Sign-off: actuals and comments. Closing scale figures.
- Dropbox landing per D-1.
- Excel export (WPS 365 per D-5).

## 2. Release 2 — quality, maintenance (Prodn-Mgt)

### 2.1 Quality auto-control (Análise)
- Hourly checks when production or conditioning is on: dry maize, maize to B1, Fuba moistures, protein, fat, fibre.
- Output per shift, same content as the Análise sheet (see section 4).
- Labels per D-13.

### 2.2 Maintenance
- Breakdowns, preventive work arranged, consumables required.
- Glose interaction limited to D-11.
- Sign-off: status of each job logged in the shift.

## 3. Release 3 — roll care, FSSC, Grain-Mgt parity
- Roll care: fluting office opening; rolls on fluting 1 and 2 and grinding 1 and 2; status; roll change due at sign-in; status at sign-off.
- FSSC: daily checklists; filing verification; MTD compliance dashboard. Daily targets and sign-off status.
- Grain-Mgt: as v0.2 section 2.

## 4. Análise v2 (corrected copy)

File: `outputs/2026-11-05_Analise-Qualidade-Fuba-Nov-26_v2.xlsx` (also in `docs/analysis/`).

Changes from v1:
1. Labels per D-13 (summary and day sheets).
2. `#DIV/0!` → blank (IFERROR). Verified: 0 error cells after recalculation.
3. Typo "LABORTORY" → "LABORATORY" on sheets 26–30.
4. Summary links to day sheets, so one correction flows through.
5. No measured values changed. 1 Nov Line C is the only data present in v1 (10:00 and 11:00).

**Dropbox upload:** The workbook must be uploaded to `/KPIs/` by the owner. The Dropbox connector only creates text files, so it cannot place a .xlsx there.

## 5. Open questions

1. **OEE column location.** "Engineering downtimes" — I could not find a table with that name in the repos or Dropbox listings. Which sheet or file should the OEE-treatment column go in?
2. **P17 name** ("FUBA BIN FULL" vs "FLOOR BIN FILLING").
3. **P25** — keep as legacy, or remap?
4. **Tiers** for P16, P19, P24, O11 — confirm against the .xlsx (v3 export layout is unreliable; see diff doc).
5. **O04 and P06 names** — use v3 or app name?
6. **Glose sample** — purchasing fields (order no., breakdown no., status).
7. Confirm the Análise v1 hourly values for days 02–30 do not exist elsewhere (for example, the paper logbook).

## 6. Not verified
- No code change has been made to either app. The downtime list in both apps is still v2-based.
- Existing code has not been tested against this document.
