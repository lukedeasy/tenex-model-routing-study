**Subject:** Forecast call — $1.33M weighted against a $2.9M target, 0.94x coverage, and this month's lift is re-categorization, not new pipeline

**The call.** Open pipeline is $2,730,000 — the sum of `Amount` across all 16 non-closed rows (current-pipeline.csv, 2026-08-20). Weighted forecast is $1,330,000, applying the forecast-rules.md weights (Pipeline 25%, Best Case 60%, Commit 100%). Total target is $2,900,000 (targets.csv, 2026-08-20, four owners). Coverage = $2,730,000 ÷ $2,900,000 = **0.94x**. Weighted-to-target is $1,330,000 ÷ $2,900,000 = 0.46x.

**What moved, and what drove it.** Open pipeline rose $25,000 from the prior snapshot ($2,705,000; prior-pipeline.csv, 2026-07-18). Weighted forecast rose $384,250 ($945,750 → $1,330,000). $378,000 of that — 98% — is three forecast-category upgrades at unchanged amounts: Dovetail Travel Best Case→Commit, +$168,000 (006SYNAUG004); Aster Health Pipeline→Best Case, +$119,000 (006SYNAUG001); Junction Apparel Pipeline→Best Case, +$91,000 (006SYNAUG010). The other $6,250 is Lantern Beauty's amount moving $150,000→$175,000 (006SYNAUG012). One close date slipped: Harborlight Mobility 2026-09-30→2026-10-31 (006SYNAUG008), no weighted change.

**Concentration, aging, stale.** Two opportunities hold 46.9% of weighted forecast: Dovetail $420,000 + Aster $204,000 = $624,000 ÷ $1,330,000. Every open opportunity is 60+ days old by `CreatedDate` (96–196 days); 8 of 16 are 60+ days in current stage. Four are stale per rule 5: Newbridge Education, 76 days (006SYNAUG014); Lantern Beauty, 61 (006SYNAUG012); Elmstead Home, 51 (006SYNAUG005); Brookline Media, 48 (006SYNAUG002).

**Actions.**

1. **Casey Nguyen, Jordan Lee, Taylor Brooks** — produce the evidence behind the three upgrades (006SYNAUG004, 001, 010) before we commit the number. They carry the whole month's movement.
2. **Casey Nguyen** — close plan for Dovetail (006SYNAUG004), the single Commit deal and 32% of weighted forecast on its own.
3. **Taylor Brooks, Jordan Lee, Casey Nguyen** — disposition the four stale records this week: activity date, or move them out.

**Data problems.** Elmstead Home's close date is 2026-07-15, before the snapshot, yet the record is open at Best Case (006SYNAUG005). Dovetail (006SYNAUG004) and Junction Apparel (006SYNAUG010) show `StageEnteredDate` moving *earlier* while stage advanced (2026-06-12→2026-06-05; 2026-06-24→2026-06-11). Every row in seller-notes.csv duplicates that opportunity's `NextStep` and `LastActivityDate`, so notes add no independent activity signal.

**What I could not confirm:** whether the three upgrades reflect verified buyer commitment; the period targets.csv covers (no period field); and whether Elmstead's evaluation is live (006SYNAUG005, last activity 2026-06-30).
