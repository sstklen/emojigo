---
emojigo:
  template-version: v1
  domain: ai-agent
  lexicon-id: multi-agent/v1
  mode: "@precise @strict @current"
  fork-instructions: see "Fork & customize" below
release-tier: L0
last-tier-change: 2026-04-13
---

# multi-agent — Lexicon for multi-agent (A2A) coordination

> A dictionary for agent-to-agent message passing in multi-agent frameworks
> (LangGraph, AutoGen, CrewAI, custom orchestrators). Designed to keep
> inter-agent traffic small, auditable, and cross-vendor friendly.

## Why this template

Multi-agent systems rack up tokens fast. Every agent hop is a context dump,
and prose is the worst possible serialization format for machines talking
to machines. A lexicon does three things:

1. **Compresses inter-agent traffic** — a 40-token handoff becomes a
   5-emoji state snapshot.
2. **Unambiguous role routing** — `🤖A` is always the planner, `🤖B` is
   always the executor, no matter which model backs them today.
3. **Human-auditable logs** — you can grep a week of agent chatter without
   reading paragraphs of LLM prose.

This template also plays nicely with research into emergent A2A protocols:
when you give two agents a shared lexicon up front, they tend to stay inside
it, which makes their behavior easier to study and constrain.

## Lexicon table

### Agent roles

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🤖A | Agent A — planner / orchestrator | Entity | `🤖A dispatches task` |
| 🤖B | Agent B — executor / worker | Entity | `🤖B runs tool` |
| 🤖C | Agent C — critic / reviewer | Entity | `🤖C flags issue` |
| 🧑 | Human-in-the-loop | Entity | `🧑 approval required` |

### State & memory

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 💾 | Shared memory / state | Entity | `💾 read key=plan` |
| 📝 | Scratchpad / working note | Entity | `🤖A 📝 draft plan` |
| 🧭 | Goal / objective | Property | `🧭 ship feature X` |
| 📜 | Instruction / policy | Property | `📜 max 3 retries` |

### Actions

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🛠️ | Tool call | Action | `🛠️ web_search(q=...)` |
| 📤 | Send / emit result | Action | `📤 to 🤖A` |
| 📥 | Receive / await input | Action | `📥 from 🤖C` |
| 🎯 | Decision / commit to action | Action | `🎯 deploy v2` |
| ⏳ | Waiting / in-flight | State | `⏳ tool running` |

### Results & coordination

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| ✅ | Success / goal achieved | Event | `🧭 ✅` |
| ❌ | Failure / goal unreachable | Event | `🧭 ❌ retry budget 0` |
| ⚠️ | Warning / unexpected | Event | `⚠️ tool returned empty` |
| 🤝 | Handoff to peer agent | Action | `🤖A 🤝 🤖B` |
| 🔁 | Retry / loop back | Action | `🔁 plan step 2` |
| 🛑 | Halt / escalate to 🧑 | Action | `🛑 policy violation` |

## How to use

1. Every agent loads this lexicon in its system prompt.
2. Define each agent's role in init: `you are 🤖A, the planner`.
3. Constrain inter-agent messages to a compact schema (YAML-ish, emoji keys).
4. Log every message `14:02:03 🤖A → 🤖B 🤝 🧭 🛠️` for grep-able traces.
5. Keep prose for human-facing outputs only.

## How two agents coordinate (worked example)

Scenario: 🤖A plans a deploy, 🤖B executes it, 🤖C reviews the result.
Shared goal: ship version 2.3.1 safely.

```yaml
# T1  🤖A → 🤖B  🧭: deploy v2.3.1   📜: canary 10→50→100, auto-abort on 🚨
#                📝: step1 🛠️ / step2 ⏳ 5min / step3 🎯 promote or ⏪   🤝
# T2  🤖B → 🤖A  📥 🧭 received   🛠️ deploy(canary=10%) ⏳
# T3  🤖B → 🤖A  📈 p99=180ms (base 170)   📊 err=0.02% (base 0.01)
#                ⚠️ mild regression, below abort   📤 ready for 🎯
# T4  🤖A → 🤖C  💾 read(canary-metrics)   🧭: promote?
# T5  🤖C → 🤖A  ⚠️ p99 +6% within 7-day noise (±8%)
#                🎯 promote (confidence: medium)
# T6  🤖A → 🤖B  🎯 promote(50%)   🤝
# T7  🤖B → 🤖A  🛠️ deploy(50%)   ✅ 🧭 achieved   💾 write(key=...)
```

Total traffic: ~120 tokens across 7 turns. Same coordination in prose
would run 600-1000+ tokens, and be much harder to audit after the fact.

## Fork & customize

- Add agent roles you need: `🤖D` retrieval, `🤖E` coder. Single-letter
  suffixes so logs stay grep-friendly.
- Tag your tools: `🛠️🔍` search, `🛠️💾` DB, `🛠️📧` email.
- Self-reflection loops? Add `🪞` self-critique, `🧠` meta-reasoning.
- Works in LangGraph, AutoGen, CrewAI, hand-rolled routers — the
  abstraction is the emoji, not the wire format.
- Version alongside your agent graph definition.

## Real-world snippet

A compact audit log, one line per turn:

```
14:02:03 🤖A → 🤖B 🤝 🧭=deploy-v2.3.1 📜=canary
14:02:04 🤖B 🛠️ deploy(10%) ⏳
14:07:09 🤖B → 🤖A 📤 📈 p99=180 📊 err=0.02 ⚠️
14:07:10 🤖A → 🤖C 🤝 🧭=should-promote
14:07:15 🤖C → 🤖A 📤 🎯=promote confidence=medium
14:07:16 🤖A → 🤖B 🎯=promote(50%)
14:12:20 🤖B → 🤖A 📤 ✅ 🧭 achieved; 💾 write(key=deploy-2026-04-13)
```

Full audit trail, parseable by a log viewer and by a human scanning for
anomalies.

---

**License**: MIT. Fork for your orchestrator, adapt tool tags to your stack.
**Research note**: this template relates to ongoing work on emergent A2A
protocols (Phase C.6 in the Emojigo research program). Findings on agent
behavior in shared-lexicon regimes will publish alongside the core paper.
**See also**: `devops-lexicon.md` (if your agents run ops tasks);
`research-lab-lexicon.md` (if you study agent behavior experimentally).
