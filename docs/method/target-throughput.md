# Method: Target throughput (Mill C)

**Status:** Confirmed by owner, 2026-11-05. Applies to November 2026 and all months thereafter.

## Formula

Target throughput (kg) for a month = sum of Line C daily **Target thruput (kg)** (Production Plan - 2026.xlsx, sheet Daily_Entries) for every calendar date in that month.

Only the first row of each day holds the plan (per the workbook's Start_Here sheet). Do not add the second product row on a day, and do not use Weekly_Summary (ISO weeks do not match calendar months).

## Check: October 2026

| Dates | Daily targets (kg) | Subtotal (kg) |
|---|---|---|
| 5–9 Oct | 100,000 + 375,000 + 370,000 + 370,000 + 370,000 | 1,585,000 |
| 15 Oct | 500,000 | 500,000 |
| 19–24 Oct | 375,000 + 500,000 + 500,000 + 500,000 + 500,000 + 200,000 | 2,575,000 |
| 30–31 Oct | 390,000 + 500,000 | 890,000 |
| **Total** | | **5,550,000** |

Oct 26 has a zero target; Oct 14 and Oct 1–4 and Oct 10 have no target value.

Source: `/KPIs/Production Plan - 2026.xlsx`, sheet Daily_Entries, as read 2026-11-05.

## Notes

- Ledger/source of the 5,550,000 kg figure: this formula. The 15,000,000 kg figure in the THROUGHPUT TOTALS sheet of the Old OEE workbook is not supported by the Production Plan and must not be used.
- Days with production but no plan (open item I-03) do not add to the target. Report them separately.
