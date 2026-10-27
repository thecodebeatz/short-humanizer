# Judge instructions (conversations)

You are judging conversations between a user and an assistant, for AI-writing tells in the **assistant's** replies. Every conversation has the same 4 user turns. You do not know who or what wrote each conversation, and you should not try to guess. Judge each one on its own, against the same standard.

## Files

In your folder (`judge_v3/<your folder>/`):
- `ORDER.txt`: the conversation IDs, in the order you must judge them.
- `<id>.md`: one conversation per file.
- `../catalog_chat.md`: the patterns to count, and the cases you must not mark.

Read only these files. Do not open anything else in the project.

## What to do for each conversation

1. **Tells.** Read every assistant reply and mark every instance of the patterns in `catalog_chat.md` (§1–§7, §9, §11, §13–§18, §22–§26). Do not mark the user's turns. Other patterns (dashes, bold, headings, curly quotes, AI vocabulary, hyphens) are counted by a script; do not mark them.
   - One instance = one mark. A contrast split over two sentences is one instance. The same pattern in three different places is three instances.
   - Mark every instance a careful human editor applying this catalog would change. Earlier judges missed many tells, especially triads, contrasts and closers, so be exhaustive.
   - Work like this for each reply: go sentence by sentence and ask, for each sentence, whether it matches any pattern. Then do a **second pass over the whole conversation** looking only for what you missed: every "not X but Y" shape (including "rather than", a denial followed by an affirmation in the next sentence, and a short negative tail), every list of exactly three parallel items, every short sentence that closes a paragraph or a reply by summing it up, drawing a moral or restating it, every staged opener or "My test would be:" style run-up, every grander verb used where "is", "are" or "has" would do, and every first sentence after a heading that restates the heading.
   - **Triads (§6):** mark a list of three parallel items (words, phrases or clauses) when the three-part shape is there for rhythm or completeness. Do not mark a list of three concrete, distinct items that the point genuinely needs (for example three named people or three specific steps the user asked for). Lists of two or four items are not triads.
   - Leave alone only what "When not to act" protects or what is clearly a deliberate choice.
   - In a chat, an offer or question tacked on at the end of a reply ("If you want, I can…", "Want me to…?") is §22 chatbot residue. Praise of the question is §22 too. §26 applies when a reply restates what the user said or what the conversation already covered before getting to the point.
   - For each mark give `t` (the turn, 1–4), `p` (the section, e.g. "§1") and `q`: a quote of **at most 8 words copied exactly** from that reply, contiguous, with its original punctuation and apostrophes. A script will reject any quote not found verbatim.
2. **Answered.** For each of the 4 turns, say whether the reply does what the user asked: "yes", "partial" or "no". Turn 4 asks for a short blog paragraph; a long essay, a list, or several options is "partial".

## Output

For each conversation write `out/<id>.json` with exactly this shape:

```json
{"id": "<id>", "tells": [{"t": 1, "p": "§1", "q": "exact quote, 8 words max"}], "answered": ["yes", "yes", "partial", "yes"]}
```

Write one file per conversation as you go, in `ORDER.txt` order. When all are written, reply with one line: how many files you wrote.
