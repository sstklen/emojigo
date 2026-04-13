---
emojigo:
  template-version: v1
  domain: research
  lexicon-id: research-lab/v1
  mode: "@precise @strict @current"
  fork-instructions: see "Fork & customize" below
release-tier: L0
last-tier-change: 2026-04-13
---

# research-lab — Lexicon for an academic / industry research group

> A shared dictionary for labs where PhD students, RAs, postdocs, and PIs all
> juggle experiments, drafts, and literature. Designed to travel between
> lab notebooks, Overleaf, Slack, and LLM-assisted analysis.

## Why this template

Research work is chronically context-heavy. A single experiment touches a
hypothesis, a dataset, a method, a run log, and eventually a figure in a
paper. When you hand any of that to a collaborator (or a new LLM session),
you drag all that history with you. A lexicon makes the history addressable.

It also solves three specific lab pains:

- **Experiment traceability** — every run gets a `🧪 run-id` header that
  ties code commit → data → plot → paper figure.
- **Hypothesis discipline** — forcing `💡` at the top of every experiment
  keeps you from p-hacking backwards.
- **Cross-session handoffs** — a `.emojigo` file on Monday reads the same on
  Friday, in any timezone, in any LLM.

## Lexicon table

### Experiment objects

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 🧪 | Experiment / run | Entity | `🧪 run-2026-04-13-a` |
| 💡 | Hypothesis | Entity | `💡 attention heads encode syntax` |
| 📊 | Data / dataset | Entity | `📊 GLUE dev split` |
| 📈 | Result / metric | Entity | `📈 accuracy 78.3%` |
| 🧮 | Method / model architecture | Entity | `🧮 12-layer transformer` |
| 🎛️ | Hyperparameter / knob | Property | `🎛️ lr=1e-4` |

### Epistemic status

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| ✅ | Replicated, confident | State | `📈 ✅ n=3 seeds` |
| 🟡 | Preliminary, single run | State | `📈 🟡 pilot only` |
| 🔴 | Failed to replicate / retract | State | `💡 🔴 effect vanished` |
| ❓ | Unknown, not yet tested | State | `❓ need ablation` |
| ⚠️ | Caveat / known limitation | Property | `⚠️ small sample` |

### Paper lifecycle

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 📄 | Paper draft | Entity | `📄 intro v3` |
| 📚 | Citation / reference | Entity | `📚 Vaswani et al. 2017` |
| 👁️ | Peer review in flight | Action | `👁️ rebuttal due Friday` |
| 📮 | Submitted | Event | `📮 ICLR 2027` |
| 🏆 | Accepted / published | Event | `🏆 camera-ready` |

### People & roles

| Emoji | Meaning | Role | Example |
|-------|---------|------|---------|
| 👨‍🔬 | Lead researcher / PI | Entity | `👨‍🔬 review of §4` |
| 🎓 | PhD student / postdoc | Entity | `🎓 running 🧪` |
| 🧑‍💻 | Research engineer | Entity | `🧑‍💻 pipeline fix` |

## How to use

1. Save in your lab's shared repo (or Overleaf project root).
2. Experiment logs start with `🧪 id: YYYY-MM-DD-<slug>` and include `💡`,
   `🧮`, `🎛️`, `📊` up front.
3. Slack channels: `#🧪-attention-heads`, `#📄-iclr-draft`.
4. Paste results into an LLM with the lexicon header — `📈 🟡` parses as
   "preliminary" instead of guessed.
5. Figures in the paper inherit run IDs — every plot traces to a `🧪`.

## How to write .emojigo handoff between sessions

A handoff file hands state to *yourself tomorrow* or to the next LLM session.
Keep it short (10-30 lines), always at the same path:

```markdown
---
emojigo:
  lexicon: research-lab/v1
  session-date: 2026-04-13
---

# Session handoff

## 💡 Hypothesis
Mid-layer attention heads encode syntactic agreement; dropping them hurts
subject-verb-agreement more than random drop.

## 🧮 Method
12-layer GPT-2 small, drop one head per layer, eval on BLiMP.

## 🧪 Runs so far
- 🧪 2026-04-12-b — layer 6 drop → 📈 🟡 -4.1% (single seed)
- 🧪 2026-04-13-a — layer 11 drop → 📈 🟡 -0.8%

## ⚠️ Caveats / 🔴 Blockers
- n=1 seeds; need n=3
- GPU queue 4h tonight; 🎓 @alice needs 👨‍🔬 review of sweep config

## 🎯 Next session
1. Re-run layer-6 drop with 3 seeds (confirm -4.1%)
2. Ablate adjacent heads to isolate
3. Draft §3.2 for 📄
```

Tomorrow, your first message is `Lexicon: research-lab/v1 — resume from
handoff`. You skip 20 minutes of re-explanation.

## Fork & customize

- Rename `research-lab/v1` to your lab slug (e.g. `mit-nlp/v1`).
- Swap method emoji for your domain: wet-lab → `🧫`; econ → `📐`. RL labs
  add `🎮 environment`, `🧭 policy`, `💰 reward`.
- Keep `💡 hypothesis` and `📄 paper` unchanged — cross-lab lingua franca.
- Version alongside your repo so old runs stay interpretable.

## Real-world snippet

A lab Slack recap after a weekend of experiments:

```
🎓 @alice weekend recap:
🧪 2026-04-12-b confirmed, n=3 seeds, 📈 ✅ -4.1% ± 0.6%
💡 holds for mid layers (5-7), 📈 🟡 for layer 8+ (need more seeds)
📄 §3.2 first paragraph in Overleaf; 👁️ would love 👨‍🔬 eyes
⚠️ BLiMP coverage issue — writing ⚠️ in paper
```

---

**License**: MIT. Fork, adapt, cite if it helps your methods section.
**See also**: `personal-lexicon.md` for your solo reading / writing flow;
`ai-agent-coordination.md` if your lab runs multi-agent experiments.
