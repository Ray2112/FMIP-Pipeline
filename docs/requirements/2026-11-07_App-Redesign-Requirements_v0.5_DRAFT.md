# App redesign requirements — Prodn-Mgt and Grain-Mgt (v0.5, DRAFT rev 2)

**Date:** 2026-11-07 · **Owner:** Zhax (PM) · **Supersedes:** v0.4 (kept unchanged). This revision corrects section 4 only. Sections 0 to 3 are carried over from v0.4 without alteration.
**Status:** DRAFT for owner review. Not copied to Dropbox `/FMIP/_docs/` until approved (D-12). Supersedes the draft dated 2026-11-07 (not rev 2) for section 4.

## Change log

| Version | Date | Change |
|---|---|---|
| v0.4 | 2026-11-05 | Initial release-scoped requirements with decisions D-1 to D-20. |
| v0.5 draft | 2026-11-07 | Section 4.1 corrected from the handover of 6 November. |
| v0.5 rev 2 | 2026-11-07 | Section 4 re-verified against the repositories on `main`. Both downtime pull requests are merged, not open. O11 item closed by owner decision. Test suites run on `main`. |

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
| D-21 | O11 tier (new) | **Other** (owner decision, 6 Nov 2026). Applied on `main` in both apps. Replaces the open item in v0.4 §4.3. |

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

## 4. Status of implementation and open items

**4.1 Downtime v3 changes: merged to `main` in both apps (replaces v0.4 §4.1 and the handover of 6 Nov).**

- Prodn-Mgt (`Ray2112/Prodn-Mgt`): PR #4 "Downtime Codes v3" merged (merge commit `ef94b0d`). The branch commit `2eb3d20` is in `main`. Test files on `main`: 11, all passing (checked 7 Nov 2026).
- Grain-Mgt (`Ray2112/Grain-Mgt`): PR #1 "Downtime Codes v3 Grain-Mgt" merged (merge commit `40218a9`). The branch commit `7f1a3eb` is in `main`. Test files on `main`: 9, all passing (checked 7 Nov 2026).
- Owner validation in the apps: **not confirmed in the record.** The merge was made after the handover was written. The owner should confirm the merge was intentional and that the app was validated.
- Not yet done: the version string in `js/prod.js` on `main` is still `2.4.0`. Version bumps need owner approval. The README changelog was not checked in this revision.
- Stale branch `downtime-v3` still exists on both repositories, with one commit or line difference from `main`. Delete only after owner approval (Rule: no deletion without approval).
- Remote branch `feat/fmip-agent-team` on the FMIP-Pipeline repository: state not re-checked in this revision. The handover records that deletion was refused by the proxy.

**4.2 Glose sample file (purchasing fields).** Owner to provide.

**4.3 Downtime Codes v3 tier for O11.** Closed. See D-21. Both apps now show O11 "FEED MILL" as Other, Excluded - External.

## 5. Not verified

- Test suites pass on `main` in both repositories. They are unit-level tests only. The apps have not been run in a browser against real data.
- Old records that use P25 will show as an unknown code if re-validated. Check on first use.
- The `docs/patches/` folder mentioned in v0.4 §4.1 was not checked in this revision.
- Commit and merge history is from a public read-only clone at `/home/claude/ray2112/`. It shows what is public on GitHub, not the owner's local state.
