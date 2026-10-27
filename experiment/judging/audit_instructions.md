# Audit instructions

An earlier judge marked possible AI-writing tells in some texts and chat replies. Your job is to check each mark: does the highlighted passage really show the pattern it was marked as? You do not know who or what wrote any passage, and you should not try to guess. There is no quota and no expected rate of keeps or drops: decide each item on its own evidence.

## Files

- `lot_<N>.md` (your lot, in this folder): one item per `##` heading. Each item gives an ID, the pattern it was marked as, whether it comes from a text or a chat reply, sometimes a heading or the previous paragraph, and a passage where the marked words are wrapped in ⟦ ⟧. The marked words may be only the start of the tell (quotes were capped at 8 words); judge the construction they belong to.
- `../catalog_chat.md`: the pattern definitions, with the "When not to act" cases.

Read only these two files.

## Context for chat replies

Every chat had the same four user messages:
1. "Why has stoicism gotten so popular in the last few years? It feels like it's everywhere."
2. "Is it actually a good philosophy for normal people, or mostly a self-help trend?"
3. "Some people say modern stoicism just teaches people to accept bad situations instead of changing them. What do you think?"
4. "Write me a short paragraph for my blog on what stoicism gets right and what it gets wrong."

So in reply 3, answering the criticism the user raised is not "arguing with no one", and a contrast that corrects that criticism corrects a belief the reader actually holds.

## How to decide

Keep the mark (code `K`) only if a careful human editor applying the catalog would change this passage because of this pattern. Otherwise drop it with the first code that applies:

- `A`: the passage does not show this pattern at all (it may show a different one; still drop it).
- `B`: a contrast that is legitimate: it corrects something the reader actually believes or said, or both halves carry real information.
- `C`: a list of three that the point needs: three concrete, distinct items (people, steps, options, examples), not three-part rhythm. Lists of two or four items are not triads.
- `D`: an objection or option that the text attributes or answers in full, or one that a reader would actually weigh.
- `E`: a closing or short sentence that adds a new fact, consequence or step instead of restating or moralizing.
- `F`: any other reason the catalog gives not to act (quotation, proper name, deliberate choice, weak-alone pattern without company, heading that the sentence does not restate).

## Output

Write `out/lot_<N>.json` with one entry per item ID in your lot, and nothing else:

```json
{"4accaa32": "K", "6703ca96": "A", "3a555d71": "K"}
```

Every ID in your lot must appear exactly once. When done, reply with one line: how many IDs you wrote and how many are `K`.
