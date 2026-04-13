# Emojigo Quickstart — 5 minutes to your first .emojigo file

> Goal: by the end, you'll have a working Emojigo lexicon and use it to give an LLM 5× more context per token.

---

## Step 1: Install (30 seconds)

```bash
git clone https://github.com/sstklen/emojigo
cd emojigo
```

(Currently no runtime needed — Emojigo is a notation; LLMs already understand it.)

---

## Step 2: Write your project lexicon (2 minutes)

Create `your-project/emojigo-lexicon.md`:

```markdown
# Project Lexicon v1

| Emoji | Meaning |
|-------|---------|
| 🧬 | LLM internal state |
| 📊 | quarterly metrics |
| 🧪 | experiment |
| 📄 | paper draft |
| 🔬 | research mode |
| ✅ | done |
| 🟡 | in progress |
| 🔴 | blocked |
| → | sequential composition |
```

Pick 5-15 emoji that map to your project's high-frequency concepts.
Don't try to cover everything. Just the frequent ones.

---

## Step 3: Add to your CLAUDE.md / GPTs instruction (1 minute)

```yaml
---
emojigo:
  lexicon: ./emojigo-lexicon.md
  mode: "@precise @strict @current"
---

# Project Setup

This project uses Emojigo notation. Load lexicon above.
When user types emoji, interpret per lexicon, not free-form.
```

---

## Step 4: Use it (1 minute)

In your next conversation:

**Before Emojigo** (~50 tokens):
> "Hey, can you give me a summary of where we are on the LLM internal state research, the quarterly metrics for the experiment, and what's blocked?"

**After Emojigo** (~10 tokens):
> "🧬📊🧪 status?"

The LLM:
1. Sees the emoji
2. Looks up lexicon (already in context)
3. Understands you're asking about: LLM-internal-state + quarterly-metrics + experiment status
4. Responds appropriately

**5× token saving. Same query.**

---

## Step 5: Add modes (advanced, 1 minute)

Modes adjust LLM behavior:

```yaml
mode: "@precise @strict"   # Strict lookup, fail on ambiguity
mode: "@divergent @loose"  # Brainstorm, allow multi-meaning
mode: "@transitional"      # State-dependent (Markov-like)
```

See [EMOJIGO-SPEC.md §5](EMOJIGO-SPEC.md#5-modes) for all 6 mode axes.

---

## Common Patterns

### Status check
```
🅰️🤝 status?
```
→ "What's the status of Phase A in our pair work?"

### Decision request
```
🤝 + 🤔 should we deploy now?
```
→ "Together, let's think about whether to deploy now."

### Handoff document
```yaml
---
emojigo:
  lexicon: ./emojigo-lexicon.md
---

🅰️ ✅ 79% [Phase A done at 79% success]
🅱️ 🟡 26% [Phase B in progress]
🚧 [blocker: API key missing]
🤔 next: get API key, retry Phase B
```

A new LLM session reads this and resumes work in 10 seconds.

---

## What NOT to Do

❌ **Don't replace all words with emoji.**
   ```
   ❌ 🤖🧠💭📊 → 📈 + 🎯
   ✅ 🤖 thinks 📊 will improve 🎯 because [reason]
   ```

❌ **Don't skip the lexicon.**
   Without lexicon, LLM guesses meanings. Inconsistent results.

❌ **Don't use ambiguous emoji for critical decisions.**
   Use `@precise @strict` mode. Fail loudly if ambiguous.

✅ **Do mix emoji + text + numbers + code.**
   Each modality serves its niche. See [EMOJIGO-SPEC.md §3.9](EMOJIGO-SPEC.md#39-hybrid-notation-principle).

---

## Where to Go Next

- **[EMOJIGO-SPEC.md](EMOJIGO-SPEC.md)** — Full language specification
- **[EMOJIGO-MD.md](EMOJIGO-MD.md)** — Markdown container details
- **[EMOJIGO-USE-CASES.md](EMOJIGO-USE-CASES.md)** — 12 application scenarios
- **[Examples folder](examples/)** — Real-world lexicons and documents

---

## FAQ

**Q: Does this work with ChatGPT / Gemini, not just Claude?**
A: Yes. All frontier LLMs share the same emoji embedding training. Cross-model differences exist but are small (see PHASE-C6 results when published).

**Q: Will my LLM "forget" the lexicon mid-conversation?**
A: Lexicon is in context window like any other text. As long as it's loaded at the start, it persists. For very long conversations, re-anchor with `🔬 lexicon refresh`.

**Q: Can I share lexicons with my team?**
A: Yes — that's the design. Lexicons are versioned (v1, v2) and forkable. See [governance proposal](EMOJIGO-LEXICON.md#governance).

**Q: Is this safe for production?**
A: For internal team use, yes. For multi-tenant systems, treat lexicons like any user-supplied input (sandbox, validate). See [security considerations](EMOJIGO-SPEC.md#10-security-considerations).

**Q: How does this compare to LLMLingua / prompt compression?**
A: LLMLingua removes "low-saliency" tokens to compress. Emojigo *encodes* semantic anchors. Different mechanism, complementary. Can stack.

---

**Built by tkman + Claude Opus 4.6** as part of an AI safety research program.
**License**: MIT.
**Issues / discussions**: GitHub.
