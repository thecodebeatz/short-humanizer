# Results

BHS = [blader/humanizer](https://github.com/blader/humanizer) v3.1.0. SHS = Short Humanizer. In the data files they show up as `Humanizer` and `Short_Humanizer`.

The metric is AI tells per 100 words. Lower is better.

## Setup

| | |
|---|---|
| Writer | GPT-6.1 Sol, medium reasoning, bare API calls (no memory, tools or persona) |
| Judges and auditors | Claude Opus 5.5 sub-agents, blind to the skill |
| Script-counted tells | Em dashes, bold, headings, curly quotes (once per text), AI words, hyphenated pairs |
| Judge-counted tells | Everything else in the 26-pattern list |
| Chatting | 20 conversations per arm, 4 turns each, same user messages, topic: why Stoicism got popular |
| Rewriting | 3 base texts (~1,000 words), 12 rewrites per skill per text |
| Test | Welch's t-test, SHS vs BHS |

| Skill | Characters |
|---|---|
| No skill | 0 |
| BHS | 32,348 |
| SHS | 2,587 |

The judges over-counted a lot, so a second round of agents audited every mark one by one: 975 of 3,180 survived. Everything below uses only those.

## Chatting

| Arm | Tells per 100 words | Drop from no skill | Words per conversation |
|---|---|---|---|
| No skill | 4.28 | | 1,261 |
| BHS | 0.95 | 78% | 1,168 |
| SHS | 0.59 | 86% | 1,069 |

Tells left per conversation (~1,100 words):

| Tell | No skill | BHS | SHS |
|---|---|---|---|
| Bold | 21.9 | 4.6 | 1.8 |
| Em dashes | 11.9 | 0 | 0 |
| Dramatic closers | 4.8 | 2.8 | 1.6 |
| Run-ups | 3.4 | 0.5 | 0.5 |
| AI words | 3.2 | 0.6 | 0.6 |
| Forced triads | 3.1 | 0.7 | 0.6 |
| Not X but Y | 2.1 | 0 | 0 |
| Sage lines | 1.5 | 0.2 | 0.5 |
| Curly quotes (once per conversation) | 1.0 | 1.0 | 0 |
| Avoiding "is" and "has" | 0.8 | 0.4 | 0.6 |
| Arguing with no one | 0.2 | 0.1 | 0 |

BHS keeps curly quotes because its rule says to change them only where the writer already uses straight ones. GPT-6.1 Sol writes curly quotes by default.

## Rewriting

| Text | Base text | BHS | SHS |
|---|---|---|---|
| Blog post | 3.75 | 0.90 | 1.24 |
| Opinion piece | 3.42 | 0.66 | 0.63 |
| Guide | 1.94 | 0.04 | 0.04 |

Tells left per rewrite, where the skills differ:

| Tell | Blog: BHS | Blog: SHS | Opinion: BHS | Opinion: SHS |
|---|---|---|---|---|
| Dramatic closers | 4.3 | 4.9 | 2.7 | 1.7 |
| Heading repeated in the next sentence | 1.8 | 2.4 | 0.5 | 0.8 |
| Sage lines | 1.0 | 2.2 | 0 | 0.2 |
| Avoiding "is" and "has" | 1.1 | 2.0 | 0.2 | 0.7 |
| Forced triads | 1.2 | 1.2 | 1.7 | 1.4 |
| Arguing with no one | 0 | 0 | 0.4 | 0.8 |

Both skills removed every em dash and every bold phrase from all three texts.

## BHS vs SHS

| Task | SHS minus BHS | 95% CI | p | Fewer tells |
|---|---|---|---|---|
| Chatting | -0.37 | -0.54 to -0.19 | < 0.001 | SHS |
| Chatting, without formatting tells | -0.05 | -0.16 to +0.06 | 0.38 | Tie |
| Rewriting: blog post | +0.34 | +0.17 to +0.51 | < 0.001 | BHS |
| Rewriting: opinion piece | -0.03 | -0.16 to +0.10 | 0.59 | Tie |
| Rewriting: guide | -0.01 | -0.05 to +0.04 | 0.73 | Tie |

## Limits

- One writer model, all in English, one chat topic.
- Claude judged ChatGPT. They may share blind spots, and the audit can only remove marks, not add missed ones.
- SHS was written with Claude after a pilot run, so its wording was tuned to what the pilot showed. The hypotheses were fixed before this run.
- No human readers rated the texts, and nobody checked whether the rewrites kept every idea of the base text.

## Files

| Folder | What's in it |
|---|---|
| [`texts/`](texts/INDEX.md) | Everything GPT-6.1 Sol wrote: base texts, rewrites and chats |
| [`data/`](data/) | Per-text metrics (CSV) and every judge mark with its quote and audit verdict (JSON) |
| [`judging/`](judging/) | The exact instructions and pattern catalogs the judges and auditors got |
| [`skills/`](skills/) | Both skills exactly as tested |
