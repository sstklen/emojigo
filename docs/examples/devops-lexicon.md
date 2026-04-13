---
emojigo:
  template-version: v1
  domain: devops
  lexicon-id: devops-team/v1
  mode: "@precise @strict @current"
  fork-instructions: see "Fork & customize" below
release-tier: L0
last-tier-change: 2026-04-13
---

# devops-team — Lexicon for SRE / platform / on-call rotations

> A lexicon built for the tempo of production: incidents, deploys, alerts,
> rollbacks. Drops into runbooks, on-call handoffs, chat-ops, and LLM copilot
> context without reinterpretation.

## Why this template

On-call runs on pattern recognition. At 3am you need to triage in seconds:
who owns it, what service, what severity. A consistent lexicon turns long
log lines into scannable glyphs, gives you a grep-able deploy audit trail,
and locks every post-mortem into the same structure — so you can diff
across 50 of them to find systemic issues.

## Lexicon table

### Deploy & release

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🚀 | Deploy / release | Action | `🚀 v2.3.1 → prod at 14:02 UTC` |
| ⏪ | Rollback | Action | `⏪ prod to v2.3.0` |
| 🟢 | Canary / partial rollout healthy | State | `🟢 10% traffic v2.3.1` |
| 🔒 | Deploy freeze / change lockdown | State | `🔒 Black Friday freeze` |
| 🏷️ | Version / tag | Property | `🏷️ v2.3.1` |

### Observability

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 📊 | Metric / dashboard | Entity | `📊 p99 latency` |
| 📉 | Degradation / regression | Event | `📉 error rate +3σ` |
| 📈 | Recovery / improvement | Event | `📈 back to baseline` |
| 🔍 | Trace / log dive | Action | `🔍 trace-id abc123` |
| 🚨 | Alert fired | Event | `🚨 5xx > 1%` |

### Incidents

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🚒 | Active incident | Event | `🚒 P1 payments down` |
| 🆘 | Page on-call | Action | `🆘 @secondary` |
| 🧯 | Mitigated (not yet fixed) | State | `🧯 failover active` |
| ✅ | Resolved, post-mortem pending | State | `✅ resolved at 14:47 UTC` |
| 📋 | Post-mortem written | State | `📋 PM link in thread` |

### Components

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| ⚙️ | Service | Scope | `⚙️ auth-service` |
| 🔧 | Backend / API | Scope | `🔧 payments-api` |
| 💾 | Database | Scope | `💾 primary replica lag` |
| 🌐 | Network / edge / CDN | Scope | `🌐 CDN cache miss spike` |
| 📦 | Container / image | Entity | `📦 image sha256:abc...` |

### Severity

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🔥 | P0 — full outage, all hands | Property | `🚒 🔥 checkout down` |
| ⚡ | P1 — major degradation | Property | `🚒 ⚡ login slow` |
| 🟡 | P2 — minor, business hours fix | Property | `🚒 🟡 stale cache` |

## How to use

1. Drop this file in `runbooks/emojigo-lexicon.md` and link from every
   runbook, PR template, and on-call doc.
2. Make your alerting (PagerDuty, Grafana) emit with the emoji prefix —
   `🚨 🔥 🔧 payments-api 5xx`.
3. Enforce `🚒` in incident channel names (`#incident-2026-04-13-🚒-payments`).
4. Deploy bots post with `🚀` / `⏪`.
5. Post-mortems follow the template below — same fields every time.

## Post-mortem template in .emojigo

Save as `postmortems/YYYY-MM-DD-<service>.emojigo.md`. Same structure every
time so you can diff across incidents and spot systemic issues:

```markdown
---
emojigo:
  lexicon: devops-team/v1
  incident-id: INC-2026-04-13-001
---

# 🚒 Post-mortem: payments-api outage

## Summary
🚒 🔥 🔧 payments-api — 22 min elevated 5xx (peak 14%).

## Timeline (UTC)
- 13:58 🚀 v2.3.1 (10% canary) → 14:02 🚀 100%
- 14:07 🚨 📉 p99 2s → 12s; 14:09 🆘 paged
- 14:14 🧯 ⏪ rollback; 14:22 ✅ resolved

## Impact
⚙️ 22 min degraded; 💾 no data loss; 📊 ~18K failed checkouts, ~$42K lost.

## Root cause
🔧 v2.3.1 reduced 💾 connection pool 50 → 10. Under peak load, timeouts.

## What went well / wrong
- 🆘 paged 2 min; ⏪ rollback 7 min once decided
- 🚀 10% → 100% in 4 min (too fast); canary watched errors, not latency

## Action items
- 📋 ⚡ pool-utilization to deploy checklist — @alice, 04-20
- 📋 ⚡ canary auto-abort on latency >2x — @bob, 04-27
- 📋 🟡 require 15-min minimum at 10% — SRE, 05-01
```

## Fork & customize

- Rename `devops-team/v1` to your org (`acme-sre/v1`).
- Swap component emoji for your stack — k8s shops might use `☸️` cluster,
  `🐳` image. Add `📟` / `🤖` rows for specific pagers or auto-remediation.
- Keep severity rows (`🔥 ⚡ 🟡`) unchanged — they're the cross-team
  contract with exec, support, and comms.
- Version it with your runbook repo.

## Real-world snippet

On-call handoff at end of shift, pasted in channel:

```
🤝 handoff @alice → @bob (last 12h):
✅ 🚒 🟡 stale-cache on 🌐 CDN — 📋 PM tomorrow
🟢 🚀 v2.3.1 canary at 50% since 23:10, 📊 green
🔒 deploy freeze 06:00 UTC (Black Friday prep)
⚠️ 💾 replica lag trending up — 🔍 after standup
```

---

**License**: MIT. Fork for your SRE team, adapt to your stack.
**See also**: `team-lexicon-startup.md` (product side); `ai-agent-coordination.md`
(if your platform agents talk to each other).
