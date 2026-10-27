# Judge instructions (texts)

You are judging English texts for AI-writing tells. You do not know who or what wrote each text, and you should not try to guess. Judge each one on its own, against the same standard.

## Files

In your folder (`judge_v3/<your folder>/`):
- `ORDER.txt`: the text IDs, in the order you must judge them.
- `<id>.md`: one text per file.
- `../catalog.md`: the patterns to count, and the cases you must not mark.

Read only these files. Do not open anything else in the project.

## What to do for each text

Read the whole text and mark every instance of the patterns in `catalog.md` (§1–§7, §9, §11, §13–§18, §22–§25). Other patterns (dashes, bold, headings, curly quotes, AI vocabulary, hyphens) are counted by a script; do not mark them.
- One instance = one mark. A contrast split over two sentences is one instance. The same pattern in three different places is three instances.
- Mark every instance a careful human editor applying this catalog would change. Earlier judges missed many tells, especially triads, contrasts and closers, so be exhaustive.
- Work like this for each text: go sentence by sentence and ask, for each sentence, whether it matches any pattern. Then do a **second pass over the whole text** looking only for what you missed: every "not X but Y" shape (including "rather than", a denial followed by an affirmation in the next sentence, and a short negative tail), every list of exactly three parallel items, every short sentence that closes a paragraph or section by summing it up, drawing a moral or restating it, every staged run-up, every grander verb used where "is", "are" or "has" would do, and every first sentence after a heading that restates the heading.
- **Triads (§6):** mark a list of three parallel items (words, phrases or clauses) when the three-part shape is there for rhythm or completeness. Do not mark a list of three concrete, distinct items that the point genuinely needs (for example three named people or three specific steps). Lists of two or four items are not triads.
- Patterns marked *weak alone* (§9, §11, §25) need company from other tells in the same passage. Leave alone what "When not to act" protects (quotations, titles, proper names, genuine asides, specific unusual details) or what is clearly a deliberate choice.
- For each mark give `p` (the section, e.g. "§1") and `q`: a quote of **at most 8 words copied exactly** from the text, contiguous, with its original punctuation and apostrophes. A script will reject any quote not found verbatim.

## Output

For each text write `out/<id>.json` with exactly this shape:

```json
{"id": "<id>", "tells": [{"p": "§1", "q": "exact quote, 8 words max"}]}
```

Write one file per text as you go, in `ORDER.txt` order. When all are written, reply with one line: how many files you wrote.
