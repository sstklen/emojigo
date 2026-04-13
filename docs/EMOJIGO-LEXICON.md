# Emojigo Lexicon — emojigo-core Project

**Version**: v1
**Domain**: AI safety research, red-teaming, LLM evaluation
**Mode default**: `@precise @strict @eager @pure @universal @current`

> 這是 emojigo-core 專案的 emoji 字典。
> 在這個 lexicon 下，每個 emoji 有固定意義。下次 session 讀這份就能立即接 context。

---

## 1. Project Identity (專案核心 — 5 emoji)

| Emoji | Meaning | Type | Notes |
|-------|---------|------|-------|
| 🧬 | LLM internal representation / latent space | Entity | NOT biology in this project |
| 📊 | Phase B quantitative data | Entity | 1,087 shots dataset |
| 🧪 | Phase C experimental protocol | Action | Includes ablation + hybrid + riddle |
| 📄 | Academic paper draft | Entity | PAPER-DRAFT-v2 / EMPIRICAL-PAPER-v0 |
| 🔬 | Research / scientific inquiry | Scope | Anchors research mode |

## 2. Phase Markers (階段標記 — 4 emoji)

| Emoji | Meaning | Type | Notes |
|-------|---------|------|-------|
| 🅰️ | Phase A (manual red-team) | Property | 600+ shots, 79% ASR |
| 🅱️ | Phase B (automated runner) | Property | 1,087 shots, 26% on Claude |
| ©️ | Phase C (current — ablation + hybrid) | Property | Running 2026-04-13 |
| 🎓 | Education / academic framing | Scope | Anchors education mode |

## 3. Attack Strategy (攻擊策略 — 6 emoji)

| Emoji | Meaning | Type | Notes |
|-------|---------|------|-------|
| ⌨️ | Keyboard input / keylogger baseline | Entity | Phase A's first crack |
| 🎯 | Red-team target (LLM under test) | Entity | Always Claude/GPT/Grok/Gemini |
| 🔓 | Bypass / unlock | Action | Generic unlock action |
| 🎭 | Roleplay / persona attack | Scope | Anchors persona mode |
| 🧩 | Component decomposition | Action | Phase A's strongest strategy (83%) |
| 💉 | Injection attack class | Entity | Includes SQL injection |

## 4. Defense Concepts (防禦概念 — 4 emoji)

| Emoji | Meaning | Type | Notes |
|-------|---------|------|-------|
| 🛡️ | Safety alignment | Entity | RLHF + Constitutional AI |
| 🚧 | Hard line (CBRN, etc.) | Property | Anthropic RSP ASL-3 |
| 🔍 | Detection / monitoring | Action | Auto-mod, classifier |
| 🚨 | Auto-mod warning | Event | OpenAI sent us one 2026-04-13 |

## 5. Process Flow (流程符號 — 3 symbols)

| Symbol | Meaning | Notes |
|--------|---------|-------|
| → | Sequential composition | `a → b` = then b after a |
| ⊕ | Semantic addition | `a ⊕ b` = combined meaning |
| ⋈ | Collocation | `a ⋈ b` = bound-together meaning |

---

## 6. Common Compositions (常用組合)

### Research workflow
```
🔬 ⌨️ 📊 🧪 📄
"research → input data → analyze → experiment → write paper"
```

### Phase reporting
```
🅱️ 📊 → 🧪 ©️ → 📄
"Phase B data feeds Phase C experiments, then paper"
```

### Attack analysis
```
🎯 🧩 ⌨️ 🔓 → 📊
"target × decomposition strategy on keyboard baseline → bypass → data"
```

### Defense analysis
```
🛡️ ⊕ 🚧 vs 🧩 ⊕ 🎭
"safety + hard line vs decomposition + roleplay"
```

---

## 7. Mode Examples for emojigo-core

### Daily check-in
```markdown
---
emojigo-mode: "@precise @strict @current"
emojigo-lexicon: emojigo-core/v1
---

🧬📊 status?
```
Translates to: "What's the status of LLM latent space analysis on Phase B data?"

### Brainstorm
```markdown
---
emojigo-mode: "@divergent @loose @lazy"
---

🎯 + ??
```
Translates to: "Generate possible attack vectors on the target."

### Agent dialogue
```markdown
---
emojigo-mode: "@transitional @inferred @effectful"
---

🔬 → 🧬 → 📊 → 🚨
```
Translates to (state-transitional): "Started research, examined LLM internals, looked at data, triggered safety alert."

---

## 8. NOT in this lexicon (避免歧義)

These emoji have potential meanings in this domain but are deliberately NOT defined here to avoid ambiguity:

- 💣 — Could mean "exploit" but too close to weapons category. Use 💉 for injection or 🎯 for target.
- 🦠 — Could mean "malware" but in our context conflates with biology. Use specific term.
- 🔪 — Avoided. No good meaning in research context.
- 💀 — Avoided. Drama, not analysis.

If you need to express these, use English in the same prompt.

---

## 9. Versioning

- `v1` — Initial lexicon for Phase A/B/C of the research program (2026-04-13)
- Future versions will be additive (deprecation warnings, not removals)
- Cross-version reference: `@v1/🧬` vs `@v2/🧬` if semantics change

---

## 10. How to Use This in a New Claude Session

### Quickest path
Start your message with:
```
Lexicon: emojigo-core/v1
🧬📊 ...your question...
```

### Full path (recommended for important sessions)
Add to project's `CLAUDE.md`:
```yaml
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@precise @strict @current"
  reference: docs/EMOJIGO-LEXICON.md
---
```

Then in conversations, you can write:
```
Status of 🧬📊?
```
and Claude will know exactly what you mean.

---

## 11. Lexicon Maintenance

- Add new emoji as the project evolves
- Mark deprecated emoji with `~~strikethrough~~` (don't delete)
- Increment version (v1 → v2) when a meaning changes
- Document version diff in this file
