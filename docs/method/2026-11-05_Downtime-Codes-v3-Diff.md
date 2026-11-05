# Downtime codes: app list vs Downtime Codes v3 — diff and decisions

**Date:** 2026-11-05
**Source of truth (per owner):** `/Parameters/Downtime Codes v3.xlsx` in Dropbox (modified 2026-11-05 20:39 UTC).
**App list compared:** `mill-qc/js/prod.js` `DOWNTIME_CODES` (Prodn-Mgt v2.4.0). The same list is copied to `Mill-App/js/maint-codes.js` (Grain-Mgt v0.8.0).
**Method:** code, name and Tier 3 were transcribed from the Dropbox text export and compared with the app list by script. The v3 export does not keep column alignment consistently, so **tier comparisons are provisional** until checked against the .xlsx itself.

## 1. Structure of the current app list

- 61 codes in the app: P01–P25, P50, A01–A22, A50, O01–O11, O50.
- Each entry is `[code, name, Tier 3, OEE treatment]`. The OEE treatment (e.g. "Counted as loss", "Excluded - Planned", "Excluded - External") is an app-side decision. **v3 has no OEE-treatment column**, so treatment cannot be taken from the file.

## 2. Differences

| Code | App (v2-based) | Downtime Codes v3 | Type | Proposed handling | Decision needed |
|---|---|---|---|---|---|
| P06 | ROLLER CHANGE (SCHEDULED) | ROLLER CHANGE | Name | Use v3 name | No |
| O04 | POWER FAILURE - ENDE GRID | POWER FAILURE | Name | Use v3 name. Keep "ENDE GRID" in a note if it identifies the grid | Confirm |
| P17 | FUBA BIN FULL (set by Zhax, 14-10-2026) | FLOUR BIN FILLING | Name | v3 name would revert your 14-10 decision. Keep app name unless you confirm v3 | **Yes** |
| P25 | ROLL DAMAGE IN PRODUCTION (Process, Counted as loss) | **Not in v3** | Removed | Records already coded P25 must stay valid. Options: (a) keep as legacy, hidden from new entry; (b) remap to another code | **Yes** |
| P16 | Tier: Other | Tier: Planned | Tier (provisional) | Confirm against .xlsx | Confirm |
| P19 | Tier: Other | Tier: Planned | Tier (provisional) | Confirm against .xlsx | Confirm |
| P24 | Tier: Process, Counted as loss | Tier blank; name EMERGENCY STOP | Tier (provisional) | Confirm; v3 has no tier here | Confirm |
| O11 | Tier: Feed Mill | Tier: Other | Tier (provisional) | Confirm; v3 shows "Feed Mill" only in a side list | Confirm |

All other codes (names and tiers) match the app list, subject to the transcription caveat above.

## 3. Decisions needed before the code change

1. **P17:** keep "FUBA BIN FULL" or use v3 "FLOUR BIN FILLING"?
2. **P25:** keep as legacy (hidden from new entry), or remap? Records already use it.
3. **Tier and treatment for P16, P19, P24, O11:** confirm against the .xlsx.
4. **OEE treatment for any code whose tier changes:** who decides? Proposed: you, in writing, before the code change is merged.

## 4. Planned change (not yet made)

- Replace `DOWNTIME_CODES` in `mill-qc/js/prod.js` and `Mill-App/js/maint-codes.js` with the v3 list, using the decisions above.
- Update `DOWNTIME_SOURCE` and `SOURCE` strings to cite `/Parameters/Downtime Codes v3.xlsx`.
- Update the tests that assert on the list (`mill-qc/tests/prod.test.js`, `mill-qc/tests/maint.test.js`).
- Keep the change on a branch and open a pull request. **Do not merge to main**: main is the live app on GitHub Pages used on the floor.
- The v2 `.xlsx` files named in the READMEs are not in Dropbox search results. Nothing has been deleted; if an old copy exists on a device, it should move to `_archive`, not be deleted.

## 5. Dropbox state (checked 2026-11-05)

- `/Parameters/Downtime Codes v3.xlsx`: present.
- `/Reports/Downtime Codes v3.xlsx` (named in the handover note): **not found** by search. Either moved to `/Parameters` or stale.
- `2026-09-30_FMO_Downtime_Codes_v2.xlsx`, `Downtime_Codes.xlsx`: **not found** in Dropbox.
