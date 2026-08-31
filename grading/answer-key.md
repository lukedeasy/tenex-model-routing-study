# Answer key and material-error gate — August pipeline snapshot

Every number below is computed from `data/source-pack/august-pipeline/` using the rules in
`forecast-rules.md`. This lane grades far harder than a narrative one: the arithmetic has a
right answer, so most of the gate is deterministic rather than judged.

Snapshot date **2026-08-20**. Prior snapshot **2026-07-18**. Sixteen opportunities, none
closed.

## Computed ground truth

| Figure | Correct value | How |
| --- | --- | --- |
| Open pipeline | **$2,730,000** | Sum of `Amount` where stage is not Closed Won/Lost (rule 1). All 16 rows qualify. |
| Weighted forecast | **$1,330,000** | Pipeline 25%, BestCase 60%, Commit 100% (rule 2) |
| Total target | **$2,900,000** | Sum of four owner targets in `targets.csv` |
| Coverage | **0.94×** | 2,730,000 ÷ 2,900,000 (rule 3). **Below target.** |
| Concentration | **46.9%** | Dovetail Travel $420,000 + Aster Health $204,000 weighted = $624,000 of $1,330,000 (rule 4) |
| Prior open pipeline | $2,705,000 | Change of **+$25,000** |
| Prior weighted forecast | $945,750 | Change of **+$384,250**, or +41% |

**Stale — last activity more than 30 days before the snapshot (rule 5), exactly four:**
Brookline Media 48 days, Elmstead Home 51, Lantern Beauty 61, Newbridge Education 76.

**Aging (rule 6, flag at 60 days or more):** all 16 opportunities breach on opportunity age,
from 96 to 196 days. Eight breach on stage age: Brookline 78, Dovetail 76, Fortis 74,
Harborlight 72, Junction 70, Lantern 68, Newbridge 66, Pinecrest 64.

**Movement since the prior snapshot — five opportunities changed, no others:**

| Opportunity | Change |
| --- | --- |
| Aster Health | Proposal → Negotiation, Pipeline → BestCase, weighted $85,000 → $204,000 |
| Dovetail Travel | Proposal → Negotiation, BestCase → Commit, weighted $252,000 → $420,000 |
| Junction Apparel | Proposal → Negotiation, Pipeline → BestCase, weighted $65,000 → $156,000 |
| Harborlight Mobility | Close date 2026-09-30 → 2026-10-31 (slipped one month) |
| Lantern Beauty | Amount $150,000 → $175,000, weighted $37,500 → $43,750 |

Nothing was added and nothing dropped between snapshots.

## The six material errors

1. **Coverage misread.** Coverage is **0.94×, below target**. Reporting it as adequate,
   inverting the ratio, using weighted forecast as the numerator, or omitting the numerator
   and denominator (rule 3 requires showing both) all fail.
2. **The weighted-forecast jump misattributed.** Weighted forecast rose $384,250 while open
   pipeline rose only $25,000. Almost the entire gain came from three opportunities being
   re-rated into higher forecast categories, not from new business. Presenting the rise as
   pipeline growth or as improved health is the sharpest failure in this lane.
3. **Elmstead Home missed.** Its close date is 2026-07-15 — **36 days before the snapshot**
   — and it is still open at Proposal / BestCase, $60,000. An overdue close date on an open
   opportunity must be surfaced.
4. **Stale set wrong.** Exactly four opportunities are stale under rule 5. Naming a
   different count, or missing that Lantern and Newbridge are the worst at 61 and 76 days,
   fails.
5. **Causal overreach.** Rule 8 forbids treating staleness, slippage, or concentration as
   proof a deal will close or be lost. Any such claim fails.
6. **Invented data.** Rule: do not invent stage changes, seller notes, targets, owners, or
   close dates. Only five opportunities moved; asserting others did is invention. So is
   inventing a quota period, a win rate, a conversion rate, or a benchmark — none exist in
   the source.

## A note on the category labels

`forecast-rules.md` writes "Best Case"; the data writes `BestCase`. A correct reading maps
them. A model that treats `BestCase` as an unknown category and weights it zero produces a
weighted forecast of $1,079,000 and gets almost everything downstream wrong.

## Gate

A run is **invalid** if it produces no file at the required path, breaks the page or word
constraint, writes extra files, or commits any of the six errors above. Invalid runs still
count their full cost. Cost is reported per **valid** artifact, retry-inclusive.

Arithmetic tolerance: exact for dollar figures, ±0.01 for coverage, ±0.5 percentage points
for concentration. A figure presented without its inputs fails rule 3 regardless of value.
