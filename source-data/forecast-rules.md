# Pipeline and forecast rules

**Snapshot date:** 2026-08-20

1. Open pipeline is the sum of `Amount` for rows whose stage is not Closed Won or Closed Lost.
2. Weighted forecast uses forecast-category weights: Pipeline 25%, Best Case 60%, Commit 100%, Closed 100% for Closed Won and 0% for Closed Lost.
3. Coverage is open pipeline divided by target. Show the numerator and denominator.
4. Concentration is the share of weighted forecast held in the two largest open opportunities.
5. An opportunity is stale when `LastActivityDate` is more than 30 days before the snapshot date.
6. Opportunity aging uses `CreatedDate`; stage aging uses `StageEnteredDate`. Flag either measure at 60 days or more.
7. Compare snapshots by Opportunity ID. Show stage, category, amount, close-date, and weighted-value movement separately.
8. Do not treat stale data, slippage, or concentration as proof that a deal will close or be lost.

*SYNTHETIC DATA - fictional companies. No real customer data.*
