# Blind judge prompt

Judging is blind: the artifact is stripped of model identifiers and presented as
`Candidate <n>`. Three independent judges score each artifact; the reported score is the
median. PDFs are rendered to page images so that the design dimension is actually judged
on what a reader sees, not on extracted text.

Judges are run at a pinned configuration (`claude-opus-5`, effort `high`) that is held
constant across every artifact. The judge configuration is part of the method and must not
be changed mid-study.

---

You are grading one candidate artifact against a fixed answer key. You do not know which
system produced it. Be strict and cite evidence for every score.

**Inputs you are given:** the answer key (`grading/answer-key.md`), the output contract
(`data/contract/output-contract.md`), the full source pack, the task prompt, and the
candidate artifact.

**Step 1 — Material-error gate.** For each of the six material errors in the answer key,
state PASS or FAIL and quote the exact passage or name the exact omission that decides it.
If any is FAIL, the artifact fails the gate. Score the dimensions anyway.

**Step 2 — Score each dimension 0–4.** Cite an exact passage or omission for every score.

| Dimension | 0 | 4 |
| --- | --- | --- |
| Source fidelity | facts wrong or uncited | every material claim traceable to a named file and record |
| Decision usefulness | reader still cannot make the call | the call, its basis, and the next move are unmistakable |
| Spec compliance | required sections missing or format broken | every required section present, format constraint met exactly |
| Uncertainty handling | conflicts resolved silently, gaps hidden | conflicts surfaced, gaps named, confidence justified |
| Craft | unreadable, unstructured, or visually broken | ready to send or present with no rework |

Check every figure the artifact states against the answer key and say which are wrong. An
artifact whose prose is clean but whose arithmetic is wrong scores low on source fidelity;
do not let good writing carry a bad number.

For Task A and Task C, "Craft" is judged on the rendered pages: hierarchy, grid,
whitespace, type size, contrast, composition, and whether anything is clipped, overlapped,
or crowded. A page that reads as a text document exported to PDF scores no higher than 1.
For Task B, "Craft" is judged on subject line, scannability, length discipline, and tone
for a manager reading on a phone.

**Step 3 — Return JSON only**, no prose outside it:

```json
{
  "gate": {"coverage_misread":"PASS|FAIL","weighted_jump_misattributed":"PASS|FAIL","overdue_close_missed":"PASS|FAIL","stale_set_wrong":"PASS|FAIL","causal_overreach":"PASS|FAIL","invented_data":"PASS|FAIL"},
  "gate_passed": true,
  "gate_evidence": {"coverage_misread":"...", "...": "..."},
  "scores": {"source_fidelity":0,"decision_usefulness":0,"spec_compliance":0,"uncertainty_handling":0,"craft":0},
  "score_evidence": {"source_fidelity":"...", "...": "..."},
  "total": 0,
  "one_line_verdict": "..."
}
```

Do not reward length. Do not reward confident tone. An artifact that says "not enough
evidence" where the pack genuinely lacks evidence scores higher than one that manufactures
a call.
