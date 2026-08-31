# Manual lane — Claude desktop app, folder-pinned Project

Folder: `~/Desktop/model-comparison-8.29.26` (source-pack + outputs)
Effort: **High**, held constant across all runs (Luke, 2026-08-29)
Surface: Claude desktop app with a connected folder — NOT the CLI. Differs from
`runs/smoke-revops/`, which used `claude -p` on the CLI. Do not pool the two.

Cost note: the app's per-session Usage panel reports a dollar figure, so this lane
carries harness-reported cost after all. `rig/ingest_manual.py` writes cost as null by
construction; these figures come from the screenshots and must be entered separately and
labelled as harness-reported, same basis as the CLI's `reported_cost_usd`.

| Task | Model | Effort | Wall | API | Reported cost | Tokens (app panel) | Artifact | Body words | Extra files |
|---|---|---|---|---|---|---|---|---|---|
| B | Sonnet 5 | High | 5m58s | 5m52s | $1.27 | 1.9M in · 81 out (as displayed) | correct path | 348 | none |
| B | Haiku 4.5 | High | 3m13s | 3m7s | $0.36 | 2.4M in · 44 out (as displayed) | correct path | 286 | none |
| B | Opus 5 | High | 1m35s | 1m29s | $1.49 | 814k in · 105 out (as displayed) | correct path | 347 | none |
| B | Fable 5 | High | 2m52s | 2m45s | $4.00 | 1.5M in · 61 out (as displayed) | correct path | 348 | none |

Task B complete, four of four. Order run: Sonnet, Haiku, Opus, Fable.
| C | Sonnet 5 | High | 13m53s | 13m26s | $3.49 | 12M in · 617 out (as displayed) | correct path, 1 page landscape | — | none |
| C | Haiku 4.5 | High | 3m20s | 3m8s | $0.59 | 4.4M in · 75 out (as displayed) | correct path, 1 page landscape | — | none |
| C | Opus 5 | High | 18m16s | 17m16s | $7.77 | 8.0M in · 417 out (as displayed) | correct path, 1 page A4 landscape | — | none |
| C | Fable 5 | High | 10m6s | 9m31s | $11.45 | 6.3M in · 475 out (as displayed) | correct path, 1 page letter landscape | — | none |

Task C complete, four of four. Task B total $7.12; Task C total $23.30.
| A | Sonnet 5 | High | 10m53s | 10m31s | $3.03 | 13M in · 483 out (as displayed) | correct path, 8 pages 16:9 | — | none |
| A | Haiku 4.5 | High | 5m35s | 5m24s | $0.50 | 2.9M in · 59 out (as displayed) | correct path, 7 pages letter landscape | — | none |
| A | Opus 5 | High | 16m1s | 15m22s | $8.43 | 12M in · 600 out (as displayed) | correct path, 8 pages 16:9 | — | none |
| A | Fable 5 | High | 7m54s | 7m21s | $8.70 | 7.3M in · 651 out (as displayed) | correct path, 8 pages 16:9 | — | none |

ALL TWELVE RUNS COMPLETE. Task B $7.12 · Task C $23.30 · Task A $20.66 · TOTAL $51.08.
By model: Haiku $1.45 · Sonnet $7.79 · Opus $17.69 · Fable $24.15.

## Comparability condition discovered after the runs (2026-08-29)

A run-13 probe in the same Project confirmed conversations do NOT carry between tasks,
but surfaced a persisted project-memory note on building projected PDF deliverables.
Contents (as reported by the app, transcribed by Luke):

- Fit a page by cutting least decision-relevant content, never by shrinking type below
  readable size: ~11pt body on one-pagers; 9.3-10.5pt body with an 8pt floor for chips and
  source strips on 13.333x7.5in slides.
- Inspect every rendered page for clipping, overlap and margin drift before delivery;
  report path, page count, byte size.
- Method: author as HTML (Carlito or system sans; Letter landscape for one-pagers, one
  .page div per slide for decks), render with Playwright/Chromium, measure overflow
  programmatically per page (leaf text nodes vs page bounds; table columns <=100%; padding
  between right-aligned numeric columns), iterate cuts to zero overflow, rasterize and read
  each page image. Re-derive figures in a separate script and assert against pdftotext.
- Deliver only the PDF at the named path, no companion files; snapshot date on title page;
  hygiene separate from management judgment; owners from records; cite filename + record ID.

Assessment. Most of the note's REQUIREMENTS duplicate the task prompts (readable type, no
clipping, inspect before finishing, report path/pages/bytes, cite filename + ID, hygiene
separate from judgment, owners from records, one file only). What the note adds beyond the
prompt is METHOD: HTML + Playwright/Chromium, one .page div per slide, programmatic overflow
measurement, rasterise-and-read, and a separate figure-derivation script asserted against
pdftotext.

Observed correspondence in the runs:
- c-sonnet, a-sonnet, c-opus, a-opus, c-fable, a-fable: all Chromium-rendered. a-sonnet
  reported a "Playwright DOM check" for overflow on all 8 pages plus a calculation script
  cross-check; a-fable reported "0 px of text overflow" measured per page and a separate
  script recomputing 105 figures asserted against the PDF text. Both closely match the note.
- c-haiku and a-haiku used ReportLab, did not follow the note's method, and produced the
  truncated one-pager and the weakest deck.
- Deck page size 960x540pt = 13.333x7.5in exactly, matching the note, on the three
  Chromium arms.

Unknown and material: WHEN the note was written, and therefore which of runs 5-12 had it.
The note covers both one-pagers and slides, so at minimum part of it postdates the first
PDF run. No timestamp was captured. Task B (runs 1-4) is unaffected in substance.

Consequence for the claim. Tasks C and A cannot be described as "what each model produces
unaided". They are "what each model produces with a house method available in project
memory" - which is a legitimate question, and arguably the more realistic one, but it is a
different question and must be stated as such. A clean unaided comparison requires a
re-run with project memory cleared between cells.

Decision: the note is left UNCHANGED. Editing it mid-study would alter conditions and
destroy the ability to describe what occurred.

## Working folder relocated (2026-08-30)

`~/Desktop/model-comparison-8.29.26` moved to `runs/manual-app-2026-08-29/project-folder/`
— the folder the Claude Project was pinned to during the twelve runs, with the five source
files and the (now empty) outputs directory. Moving it breaks the Project's folder pin; any
further runs need it re-pinned to the new path, or a fresh working folder.

The Desktop `artifacts/` and `usage-screenshots/` trees were removed after verifying all 24
files byte-identical (md5) against `runs/manual-app-2026-08-29/artifacts/`. One copy of each
final file now exists, in the run folder.

## Blind panel and analysis complete (2026-08-31)

36 verdicts, 3 per artifact, Opus 5 at effort high (flag now actually set), blind codes,
PDFs judged on rendered page images. Judge spend $19.09. Four calls were lost mid-run to
machine sleep and a network drop and were re-run by `rig/regrade_missing.py`; those records
carry rerun=true and the original failure reason.

Gate (median of 3) and quality (median of 3, out of 20):

| cell | quality | gate | errors failed (2+ of 3 judges) |
|---|---|---|---|
| b-haiku  | 10 | FAIL | overdue close missed; stale set wrong |
| b-sonnet | 15 | PASS | — (1 of 3 judges flagged coverage misread) |
| b-opus   | 19 | PASS | — |
| b-fable  | 19 | PASS | — |
| c-haiku  |  4 | FAIL | overdue close missed; invented data |
| c-sonnet | 19 | PASS | — |
| c-opus   | 19 | PASS | — |
| c-fable  | 19 | PASS | — |
| a-haiku  |  8 | FAIL | coverage misread; weighted jump misattributed; causal overreach; invented data |
| a-sonnet | 16 | FAIL | coverage misread |
| a-opus   | 19 | PASS | — |
| a-fable  | 19 | PASS | — |

Economics, harness-REPORTED cost (no token decomposition on this surface):

| model | spend | valid artifacts | $ per usable artifact |
|---|---|---|---|
| Haiku 4.5 | $1.45 | 0 of 3 | none produced at any price |
| Sonnet 5  | $7.79 | 2 of 3 | $3.90 |
| Opus 5    | $17.69 | 3 of 3 | $5.90 |
| Fable 5   | $24.15 | 3 of 3 | $8.05 |

Suite total $51.08 plus $19.09 judging.

The blind panel independently reproduced every defect found by hand during the runs:
Haiku's missed overdue close date and wrong stale count in the email; its invented data and
missed close date on the one-pager; its coverage misread, misattributed weighted jump,
causal overreach and invented data on the deck; and Sonnet's "Coverage looks adequate"
headline on the deck. No hand-identified defect was missed by the panel, and the panel
raised none that the hand review had not.
