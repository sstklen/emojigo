---
emojigo:
  template-version: v1
  domain: personal
  lexicon-id: your-personal-lexicon/v1
  mode: "@precise @strict @current"
  fork-instructions: see "Fork & customize" below
release-tier: L0
last-tier-change: 2026-04-13
---

# your-personal-lexicon — Daily driver for ChatGPT / Claude / Gemini

> One lexicon that travels with you across every AI session, every product.
> Save this as `~/.claude/your-personal-lexicon.md` (or equivalent), point your
> system prompt at it, and you never re-explain yourself again.

## Why this template

Every new chat with an LLM starts cold. You repeat who you are, how you work,
what tone you want, what "done" means. After 50 sessions that's thousands of
wasted tokens and context window for the same boilerplate.

A personal lexicon fixes that: 20 emoji that encode *you*. The LLM reads it
once at session start, and from then on "🧑 + 🛠️" means exactly what you
mean by it — no preamble, no drift.

## Lexicon table

### Identity & roles

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🧑 | You (the human) | Entity | `🧑 need help with X` |
| 🤖 | The LLM (any model) | Entity | `🤖 + 💡 suggests Y` |
| 🤝 | Pair work, collab tone | Scope | `🤝 let's figure this out` |

### Work modes (behavior switches)

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🔬 | Research mode — long-form, cite sources | Mode | `🔬 compare X vs Y` |
| ⚡ | Fast mode — dense, no preamble, action-first | Mode | `⚡ fix this bug` |
| 🛠️ | Hands mode — execute, don't deliberate | Mode | `🧑 + 🛠️ just do it` |
| 🤔 | Think mode — trade-offs, options | Mode | `🧑 + 🤔 which path?` |
| 🎯 | Precise mode — one answer, no caveats | Mode | `🎯 what's the number?` |
| 🧘 | Calm mode — slow down, no rush | Mode | `🧘 walk me through it` |

### Conversation markers

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| ✅ | Done / agree / confirm | Event | `✅ ship it` |
| ❌ | No / reject / failed | Event | `❌ wrong approach` |
| ⚠️ | Warning, attention | Event | `⚠️ this breaks X` |
| 🟡 | In progress | State | `🟡 waiting on Y` |
| 🔴 | Blocked | State | `🔴 need API key` |
| 💡 | Idea, suggestion | Event | `🤖 + 💡 try Z` |
| 🔥 | Breakthrough, important | Event | `🔥 found the root cause` |
| 🤷 | I don't know / you decide | Event | `🧑 + 🤷 your call` |

### Compound phrases (frequent combos)

| Phrase | Meaning |
|--------|---------|
| `🧑 + 🛠️` | "Just do it, skip discussion." |
| `🧑 + 🤔` | "Let's think this through together." |
| `🧑 + 🤷` | "You decide, I'll trust you." |
| `🤖 + 💡` | "I have a suggestion." |
| `🤖 + ⚖️` | "I need to push back / challenge this." |
| `🤖 + 🚧` | "I can't do this / policy blocked." |

## How to use

1. Save this file as `your-personal-lexicon.md` somewhere your LLM client
   reads automatically (Claude Code: `~/.claude/`; ChatGPT: custom
   instructions; Gemini: system prompt).
2. At the top of your first message in a new session, write:
   `Lexicon: your-personal-lexicon/v1`
3. The LLM reads the table and from then on interprets emoji per this map.
4. Speak naturally. Mix emoji with text — you don't have to emoji-everything.
5. When you want to add a new shortcut, update the table and bump to v2.

## Fork & customize

- Rename `your-personal-lexicon` to something identifiable (e.g. `alice-daily/v1`).
- Keep the categories (Identity / Modes / Markers / Compounds) — they cover
  95% of what a personal lexicon needs.
- Swap emoji that don't fit your culture or taste. The meanings matter more
  than the specific glyph.
- Keep it under ~25 rows. A lexicon you can't memorize in 10 minutes won't
  stick.
- Version it: `v1`, `v2`, etc. Don't delete old entries — mark them
  `~~deprecated~~` so old docs still parse.

## Real-world snippet

A morning check-in with a running project, using this lexicon:

```markdown
---
emojigo:
  lexicon: your-personal-lexicon/v1
  mode: "@precise @strict"
---

🧑 morning. project status?

🤖 🅰️ ✅ shipped yesterday
     🅱️ 🟡 26% — waiting on vendor response (🔴 API key)
     ©️ 🟡 design draft done, needs your review
     🤖 + 💡 suggest starting ©️ review while 🅱️ unblocks

🧑 + 🛠️ go with that. 🎯 one sentence summary for standup?

🤖 "A shipped, B blocked on vendor API key, C design ready for review."
```

Total: ~40 tokens of emoji carrying what would normally be 200+ tokens of
prose. Same information density, 5× lighter on the context window.

---

**License**: MIT. Fork freely, attribute if you want, no obligation.
**See also**: `team-lexicon-startup.md` for multi-person variants.
