---
emojigo:
  template-version: v1
  domain: startup
  lexicon-id: startup-team/v1
  mode: "@precise @strict @current"
  fork-instructions: see "Fork & customize" below
release-tier: L0
last-tier-change: 2026-04-13
---

# startup-team — Shared lexicon for a 3-15 person startup

> A lexicon designed for small teams where everyone wears multiple hats and
> "the PRD" is half Slack threads, half Notion pages, half vibes. Drops into
> your team wiki, CI job descriptions, and LLM agents alike.

## Why this template

Startups live in ambiguity. Engineers ship designs, designers write copy,
founders debug production. When everyone's context is partial, a shared
lexicon does three things:

1. **Unambiguous status** in async channels — `🟡` always means in progress,
   never "we'll get to it maybe."
2. **Signal routing** — seeing `🔥 priority` in a channel name tells humans
   and bots the same thing: drop everything.
3. **LLM grounding** — Copilot, Claude Code, internal agents all read the
   same table and stop hallucinating role labels.

## Lexicon table

### Status (the traffic light)

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| ✅ | Done, shipped, merged | State | `Checkout redesign ✅` |
| 🟡 | In progress, someone owns it | State | `🟡 @alice migrating DB` |
| 🔴 | Blocked — needs escalation | State | `🔴 waiting on legal` |

### Priority

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🔥 | Drop other work, fix today | Property | `🔥 production down` |
| ⚡ | High priority, this sprint | Property | `⚡ launch blocker` |
| 🌱 | Nice-to-have, future sprint | Property | `🌱 polish empty states` |

### People & roles

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🧑‍💻 | Engineer (any stack) | Entity | `🧑‍💻 review needed` |
| 🧑‍🎨 | Designer | Entity | `🧑‍🎨 specs coming Thursday` |
| 🧑‍💼 | PM / ops / founder hat | Entity | `🧑‍💼 pricing decision` |
| 🧑‍🔬 | Data / ML / research | Entity | `🧑‍🔬 model eval results` |

### Modules (customize these for your product)

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🎨 | Frontend / design system | Scope | `🎨 button component` |
| 🔧 | Backend / infra | Scope | `🔧 payments service` |
| 📊 | Analytics / dashboards | Scope | `📊 funnel tracking` |
| 💾 | Database / data pipeline | Scope | `💾 schema migration` |
| 🔐 | Auth / security | Scope | `🔐 SSO rollout` |

### Actions

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🚀 | Ship / release / deploy | Action | `🚀 v2.3 to prod` |
| 👀 | Needs review | Action | `👀 PR #412` |
| 📝 | Writing / doc in flight | Action | `📝 onboarding guide` |
| 🐛 | Bug found / tracking | Action | `🐛 login 500 on Safari` |

## How to use

1. Paste this lexicon into your team wiki (Notion, Confluence, GitHub wiki).
2. Link it from `CLAUDE.md` / `.cursor/rules` / any agent system prompt.
3. Slack: enable these as emoji reactions so the table shows up in
   autocomplete.
4. Ticketing: use the emoji in issue titles — `🔥🔧 payments API 500s`.
5. Standups: each person reads their three most recent `🟡` and `🔴` items.

## How to onboard a new team member

New hire week-one checklist:

1. **Day 1**: send them this file. Ask them to guess what each row means
   before reading the "Meaning" column. Score themselves out of 20. Most
   people land 16-18 without training — that's the point.
2. **Day 2**: pair them on a ticket. Use only emoji in the title and in
   Slack updates. Let them learn by pattern matching.
3. **Day 3**: they propose one emoji for a module they'll own (`🧪` for
   experiments, `🎁` for growth campaigns, whatever fits). If it sticks for
   a week, merge into v2 of the lexicon.
4. **End of week**: they should be able to scan the team board and know
   priority + owner + status per item in under 5 seconds. That's the ROI.
5. **Ongoing**: lexicon goes in their 1:1 template so it stays top-of-mind
   for the first month.

## Fork & customize

- Rename `startup-team/v1` to your company (e.g. `acme-eng/v1`).
- Swap module emoji to match your actual product surfaces. Don't carry
  `💾 database` if your team never talks about DB — delete it.
- Add role emoji for hats you actually have (support, sales, legal, etc.).
- Resist the urge to grow past ~25 rows. Lexicons that require a lookup
  every time stop being useful. Merge or drop rarely-used entries.
- Changelog at the bottom: `v1 → v2 (2026-05-01): added 🎁 for growth`.

## Real-world snippet

A sprint planning doc using this lexicon:

```markdown
---
emojigo:
  lexicon: startup-team/v1
  mode: "@precise @strict"
---

# Sprint 14 plan

## 🔥 Must ship
- 🔧 payments retry logic — 🧑‍💻 @bob 🟡 (day 3 of 5)
- 🎨 checkout button bug on Safari 🐛 — 🧑‍💻 @alice 👀 PR #412

## ⚡ Should ship
- 📊 activation dashboard v2 — 🧑‍🔬 @carol 🟡 (waiting on 💾 schema)
- 🔐 SSO for enterprise tier — 🧑‍💼 @dave 📝 (scoping)

## 🌱 Stretch
- 🎨 empty state illustrations — 🧑‍🎨 @eve 🌱

## 🔴 Blocked
- 💾 warehouse migration — 🔴 waiting on vendor contract (🧑‍💼 @dave)
```

One scan, everyone knows: two fires, two stretches, one block. Copy this
into a weekly async update and the founder can triage it between meetings.

---

**License**: MIT. Fork, rebrand, ship. No attribution required.
**See also**: `personal-lexicon.md` for the solo version; `devops-lexicon.md`
when your infra work outgrows `🔧`.
