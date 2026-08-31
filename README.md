# Nothing we could send — study pack

Everything behind the Tenex research report of 31 August 2026: the data four Claude models
were given, the prompts they were given, every document they produced, and the record of
how those documents were graded.

Published so the grading can be checked rather than taken on trust.

## What's here

| Folder | Contents |
| --- | --- |
| `source-data/` | The five files every run received. This month's 16 opportunities, last month's snapshot of the same 16, four owner targets, one note per opportunity, and the rules defining the arithmetic. |
| `prompts/` | The four prompts, verbatim: the standing instructions saved to the project, and one per deliverable. Pasted without edits, identical for every model. |
| `model-outputs/` | All twelve documents, exactly as produced. Nothing was corrected, reformatted, or cleaned up. Four emails, four one-page PDFs, four decks. |
| `grading/` | The answer key computed from the source data, the six conditions that fail a run, the shared output contract, and the prompt the blind graders received. |
| `results/` | Per-run record with cost and elapsed time, the 36 grader verdicts with the passage quoted behind each judgment, the code-to-model map, the analysis output, and the price list read at render time. |

## The data is synthetic

Every company, person, and figure in `source-data/` was authored by Tenex for a training
workshop. No customer record appears anywhere in this pack.

## Reading the outputs

The interesting reading is not the best document; it's the failures. Open
`model-outputs/deck--haiku-4.5.pdf` and look at page two, then open
`model-outputs/deck--opus-5.pdf` and look at the same content. Both were produced from
these exact files, with this exact prompt, minutes apart.

## Checking our grading

`grading/answer-key.md` holds the correct figures, each derived from `source-data/`. Recompute
them yourself; the arithmetic is small enough to do in a spreadsheet. Then read
`results/grades.jsonl`, which records what each grader said and why, and
`results/blind-map.json`, which maps the anonymous candidate codes back to model names.

## One condition worth knowing

The workspace these runs happened in carried a saved note describing how to build a PDF:
author in HTML, render through a browser, measure what overflows, re-read the rendered pages.
It was available for some or all of the eight PDF runs. All six failing conditions concern
reading and arithmetic rather than page construction, and none of the ten review failures was
a rendering failure, so the headline result does not rest on it. The design comparison does
carry that condition, and the report says so.

## One edit to this pack

`results/grades.jsonl` is the grading record as written, with one change: four records for
judge calls that died mid-run (a sleeping laptop, a dropped connection) carried the raw
payload from the tool, including internal session identifiers. Those payloads were removed.
The failure reason and every completed verdict are untouched. Those four calls were re-run
and their replacements are in the file, marked `rerun`.
