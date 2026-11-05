# App redesign requirements — Prodn-Mgt and Grain-Mgt (v0.4, DRAFT)

**Date:** 2026-11-05 · **Owner:** Zhax (PM) · **Supersedes:** v0.3 (kept unchanged).
**Status:** All owner decisions to date are recorded in section 0. Open items are in section 4.

## 0. Decisions recorded

| # | Item | Decision |
|---|---|---|
| D-1 | Dropbox convention | Approved. `/FMIP/`, per-app folders, naming `AAAA-MM-DD_<turno>_<app>_<tipo>.json`, test in `/FMIP/_test/`, manifest in every file. |
| D-2 | Downtime codes | Replace app list with Downtime Codes v3 (`/Parameters`). Changes below (D-15 to D-18). |
| D-3 | "Análise" source | `/KPIs/Analise de qualidade de fuba - Nov. 26.xlsx`. Corrected copy: v2. |
| D-4 | "Glose" | Asset management software. See D-11 and D-19. |
| D-5 | Export format | WPS 365. Microsoft 365 is not in scope. |
| D-6 | Release phasing | Approved. |
| D-7 | Owner of quality, maintenance, roll care, FSSC, daily/monthly reports | Prodn-Mgt. |
| D-8 | Folder names | Approved. Created under `/FMIP/prodn-mgt/` (shift, scale, quality, maintenance, roll-care, fssc, reports), `/FMIP/grain-mgt/` (shift, scale), `/FMIP/_test`, `/FMIP/_archive`, `/FMIP/_docs`. |
| D-9 | Top-level `/FMIP/` files | Old HTML files deleted by owner. Handover `.md` kept. |
| D-10 | OEE-treatment column | **Withdrawn** (owner: "forget the OEE"). Existing OEE treatment in both apps is unchanged. |
| D-11 | Glose scope | The pipeline does not track Glose data. It tracks only the jobs it is given. Glose is referenced only for purchasing of materials: order number, breakdown number, status. Sample to be provided by owner. |
| D-12 | Requirements in Dropbox | Copied to `/FMIP/_docs/`. |
| D-13 | Análise labels | EN "Maize to Degerm moisture content %" / PT "Milho Limpo Humidade %". |
| D-14 | Análise #DIV/0! | Resolved in v2 (blank where no data). |
| D-15 | P17 name | Keep "FUBA BIN FULL". Owner will update Downtime Codes v3. |
| D-16 | P25 | **Removed.** Not in v3. Existing records keep their snapshot of the code. |
| D-17 | Tiers | P16, P19, P24 = **Process**. O04 = **Other**. |
| D-18 | Names | P06 = "ROLLER CHANGE". O04 = "POWER FAILURE". (v3 names.) |
| D-19 | Glose timing | Glose purchasing references move to **Release 3**. |
| D-20 | Análise data | Only 1 November day had production (1 Nov, Line C). Blank days 02–30 are correct, not missing data. |

## 1. Release 1 scope

- Shift sign-in by shift leader: opening scale figures; homepage listing shift activities with targets (production, conditioning, reception, housekeeping, re-processing).
- Breakdowns during shift via Downtime Codes v3 dropdown (60 codes).
- Sign-off: actuals and comments. Closing scale figures.
- Dropbox landing per D-1.
- Excel export (WPS 365 per D-5).

## 2. Release 2 — quality, maintenance (Prodn-Mgt)

- Quality auto-control: hourly checks when production or conditioning is on (dry maize, maize to B1, Fuba moistures, protein, fat, fibre). Output per shift, same content as Análise. Labels per D-13.
- Maintenance: breakdowns, preventive work arranged, consumables required. Sign-off: status of each job logged in the shift.

## 3. Release 3 — roll care, FSSC, Glose, Grain-Mgt parity

- Roll care: fluting office opening; rolls on fluting 1 and 2 and grinding 1 and 2; status; roll change due at sign-in; status at sign-off.
- FSSC: daily checklists; filing verification; MTD compliance dashboard; daily targets and sign-off status.
- Glose purchasing references (D-11, D-19).
- Grain-Mgt: same approach as Prodn-Mgt.

## 4. Open items

1. **Downtime changes not yet live.** Code changes are committed on local branch `downtime-v3` in both app repos. Pushing is blocked: the Claude GitHub App is not installed for the `ray2112` organisation. Patches are in `docs/patches/`. Install the app (or apply the patches by hand) and the branches can be pushed. Nothing has been merged to `main`.
2. Glose sample file (purchasing fields).
3. Confirm Downtime Codes v3 tier for O11 (app says "Feed Mill"; v3 says "Other"). Not covered by D-17.

## 5. Not verified

- The patched code has been tested locally only (both app test suites pass). It has not been run in a browser against real data.
- Old records that use P25 will show as an unknown code if re-validated. Check on first use.
