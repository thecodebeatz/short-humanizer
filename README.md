# Short Humanizer

A short prompt (2,587 characters) to fix the most common AI tells / AI slop in text. It uses 12 times fewer tokens than [Blader's Humanizer](https://github.com/blader/humanizer).

The whole story is in my blog post: [The Short-Humanizer](https://codebeats.net/blogpost/the-short-humanizer/).

## Why

Everything reads and feels the same nowadays. It's the silent, corrosive fingerprint that AI is leaving behind.

Maybe the most straightforward way to humanize AI-written text is using Blader's Humanizer skill (BHS from now on). It works very well. But I've lately been playing with my Hermes agent, Asuka, and to me it was a bit of overkill to inject more than 8K tokens in every conversation by invoking BHS.

So I created (with Claude's help, clearly) the Short Humanizer skill (SHS). It focuses on which tells to avoid and doesn't elaborate that much on the examples.

| | BHS | SHS |
|---|---|---|
| Characters | 32,348 | 2,587 |
| Patterns | 26 | 26 |
| Examples | Before/after for each pattern | None |

## Install

### Claude Code

```
/plugin marketplace add thecodebeatz/short-humanizer
/plugin install short-humanizer@short-humanizer
```

Or copy the skill folder yourself:

```
git clone https://github.com/thecodebeatz/short-humanizer
cp -r short-humanizer/skills/short-humanizer ~/.claude/skills/
```

### Agents

For OpenClaw, Hermes or similar, paste the body of [SKILL.md](skills/short-humanizer/SKILL.md) (everything below the frontmatter) into your agent's SOUL.md or system prompt.

### Any AI chat

Copy-paste the same prompt before your text.

## Usage

Ask Claude (or your AI of choice) to humanize the following crappy text. In an agent with the prompt in its SOUL.md there's nothing to invoke: the replies just come out with fewer tells.

In Claude Code you can also invoke it directly with `/short-humanizer:short-humanizer`. If you also have blader's humanizer installed, Claude may pick that one when you just ask, so use the slash command.

## Does it really work?

I put this to the test in the most scientific way I could, with GPT-6.1 Sol at medium reasoning as the writer:

1. A writing challenge: 12 rewrites per skill of three base texts (a blog post, an opinion article and a guide), 72 in total.
2. A chatting challenge: 20 four-turn conversations per skill.

Tells were counted every 100 words. Formatting was counted by a Python script, and everything else by Claude sub-agents (the judges), plus another round of sub-agents that audited the judges.

| Task | No skill | BHS | SHS | p | Fewer tells |
|---|---|---|---|---|---|
| Chatting | 4.28 | 0.95 | 0.59 | < 0.001 | SHS |
| Rewriting: blog post | 3.75 | 0.90 | 1.24 | < 0.001 | BHS |
| Rewriting: opinion piece | 3.42 | 0.66 | 0.63 | 0.59 | Tie |
| Rewriting: guide | 1.94 | 0.04 | 0.04 | 0.73 | Tie |

The SHS was slightly better at the chatting challenge, mainly because it was better at avoiding formatting tells (particularly bold text). If it wasn't for that, there wouldn't be a significant difference between the two (p = 0.38). On the writing challenge, BHS was better at rewriting the blog post, and on the other two it was a tie.

Raw numbers, every text the model wrote, every judge mark and the instructions the judges got are in [experiment/](experiment/RESULTS.md).

## Conclusion

- Using any skill is way more important than the actual skill or prompt you use.
- BHS is still a very good skill because it's detailed. This is particularly important for low-end LLMs or models reasoning at low levels.
- SHS, being 12 times smaller, is particularly useful for agents, where API token usage and context windows matter. It's also useful if you want to tweak it and make it your own.
- If you have the time, please write whatever you want to write yourself.

## Credits

The 26 patterns come from [blader/humanizer](https://github.com/blader/humanizer), which builds on Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). Both skills are MIT-licensed. See [LICENSE](LICENSE).

Peace 🍋 🤖
