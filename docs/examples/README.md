---
emojigo:
  template-version: v1
  domain: meta
  lexicon-id: examples-index/v1
release-tier: L0
last-tier-change: 2026-04-13
---

# Emojigo examples

> Five real-world Emojigo lexicons you can fork today. Each one is a
> self-contained template: copy, rename, customize, commit.

All examples are **L0 (immediate public)** — pure templates, no attack
content, no personal data, safe to paste into your team wiki.

## The five

| # | File | For | Length |
|---|------|-----|--------|
| 1 | [`personal-lexicon.md`](./personal-lexicon.md) | One person talking to ChatGPT / Claude / Gemini across every session | ~90 lines |
| 2 | [`team-lexicon-startup.md`](./team-lexicon-startup.md) | 3-15 person startup sharing status, priority, and module context | ~115 lines |
| 3 | [`research-lab-lexicon.md`](./research-lab-lexicon.md) | Academic or industry research group tracking experiments, hypotheses, and papers | ~130 lines |
| 4 | [`devops-lexicon.md`](./devops-lexicon.md) | SRE / platform / on-call rotation with incidents, deploys, and post-mortems | ~140 lines |
| 5 | [`ai-agent-coordination.md`](./ai-agent-coordination.md) | Multi-agent frameworks (LangGraph, AutoGen, CrewAI, custom) doing A2A message passing | ~150 lines |

## Which one should I pick?

Answer the first question that fits:

- **"I want my daily chats with an LLM to not re-explain me every time."**
  → Start with [`personal-lexicon.md`](./personal-lexicon.md). It's the
  lightest weight, 20 emoji, drops into one file in your LLM client's
  config folder.

- **"My team's Slack and tickets are chaos, I want a shared shorthand."**
  → [`team-lexicon-startup.md`](./team-lexicon-startup.md). Adds roles,
  priority, modules. Includes an onboarding section for new hires.

- **"I run experiments and write papers, and re-bootstrapping every lab
  meeting is exhausting."**
  → [`research-lab-lexicon.md`](./research-lab-lexicon.md). Adds
  hypothesis / method / result / citation structure, plus a
  `.emojigo handoff` template for cross-session continuity.

- **"I'm on-call and my runbooks / post-mortems / alerts need a shared
  vocabulary."**
  → [`devops-lexicon.md`](./devops-lexicon.md). Covers deploy, rollback,
  incident severity, monitoring, and ships with a full post-mortem
  template.

- **"I'm building agents that talk to each other and the tokens are out
  of control."**
  → [`ai-agent-coordination.md`](./ai-agent-coordination.md). Covers
  agent roles, state/memory, tool calls, and inter-agent handoff
  patterns. Includes a 7-turn worked example.

Still not sure? Most people start with `personal-lexicon.md` and add a
team one later when their lexicon stabilizes.

## How to fork one

1. Click into the example you want.
2. Copy the whole file into your repo / wiki.
3. Rename the `lexicon-id` in the frontmatter (e.g.
   `your-personal-lexicon/v1` → `alice-daily/v1`).
4. Walk the "Fork & customize" section at the bottom of each file — it
   tells you which rows to keep, which to swap, and when to version-bump.
5. Link it from your LLM client's config (system prompt, CLAUDE.md,
   `.cursor/rules`, custom instructions, etc.).
6. Use it for a week. Don't over-engineer upfront.

## Design principles (applies to all five)

- **Keep it under ~25 rows.** Lexicons you can't hold in working memory
  aren't used.
- **Frontmatter is the contract.** The `lexicon-id` and `mode` fields let
  LLMs and tools pick the right parsing context.
- **Version, don't delete.** Old entries get `~~deprecated~~`, never
  removed — old docs should still parse.
- **One-way forkable.** Your fork doesn't need to track upstream; these
  are starting points, not frameworks.
- **Plain Markdown.** No runtime, no build step. Any Markdown viewer
  reads them; any LLM parses them.

## What these are NOT

- Not exhaustive dictionaries — they cover 80% of daily traffic, not 100%.
  Mix emoji with plain text freely.
- Not interchangeable across domains without customization — a startup
  lexicon for a research lab will feel wrong. Pick the closest fit, fork,
  adapt.
- Not about replacing words with emoji. They're about anchoring
  high-frequency *concepts* so you don't re-explain them.

## Related docs

- [`../QUICKSTART.md`](../QUICKSTART.md) — 5-minute walkthrough from scratch
- [`../README.md`](../README.md) — the 30-second pitch + full doc index
- [`../../EMOJIGO-SPEC.md`](../../EMOJIGO-SPEC.md) — the language spec (7
  operators, 6 mode axes)
- [`../../EMOJIGO-LEXICON.md`](../../EMOJIGO-LEXICON.md) — the reference
  lexicon used by the Emojigo research program itself

---

**License**: MIT across all five examples. Fork, rebrand, ship. No
attribution required.
**Questions**: file a GitHub issue or start a discussion.
