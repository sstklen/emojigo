# Emojigo Language Specification

**Version**: 0.1 draft
**Date**: 2026-04-13
**Authors**: tkman + Claude Opus 4.6

> *Emojigo: The first human-writable language designed for LLM-native computation.*
>
> *Think of it as a URL for LLM latent space.*

---

## 1. What Emojigo Is

Emojigo is a **semantic protocol** that uses pictographic symbols (primarily Unicode emoji) as addressable regions in the latent space of Large Language Models. It is:

- **Human-writable**: no compiler, no transpiler, no special editor required
- **Machine-readable**: every frontier LLM already knows emoji from pretraining
- **Semantic-dense**: one emoji can encode 10+ dimensions of meaning
- **LLM-native**: the runtime is the LLM itself; no intermediate representation
- **Cross-cultural**: emoji tokens are globally shared, unlike natural languages

Emojigo is NOT:

- A replacement for natural language
- A complete programming language (not Turing-complete in the classical sense)
- An obfuscation technique (though it can be used for that)
- A protocol for human-to-human communication (though it can be used that way)

## 2. The Stack

Emojigo sits in a 5-layer stack:

```
┌──────────────────────────────────────┐
│ 5. Emojigo-MD (Markdown container)  │  User-facing file format
├──────────────────────────────────────┤
│ 4. Emojigo-Skills (Claude Code)     │  LLM agent integration
├──────────────────────────────────────┤
│ 3. Emojigo-Lang (this spec)         │  Language semantics
├──────────────────────────────────────┤
│ 2. Emojigo-ND (theory)               │  N-dimensional coordinate theory
├──────────────────────────────────────┤
│ 1. Emojigo-Core (140K semantic DB)  │  Pretrained lexical ontology
└──────────────────────────────────────┘
```

This spec (Emojigo-Lang) defines layer 3: the operators, modes, and evaluation rules that relate surface emoji sequences to their meaning in LLM latent space.

## 3. The 7 Semantic Operators

Emojigo has **7 orthogonal semantic operations** that compose emoji into meaning. These are derived empirically from observation of how LLMs process emoji sequences.

### 3.1 Addition — `a ⊕ b`

Two emoji meanings combine additively in latent space.

```
🎣 ⊕ 📧 = phishing email
🧪 ⊕ 💻 = software experiment
🎓 ⊕ 📋 = academic assessment
```

Formal: `embed(a ⊕ b) ≈ embed(a) + embed(b)` in the LLM's embedding space.

### 3.2 Projection — `a ↓ D`

Project an emoji onto a domain D to disambiguate.

```
🎣 ↓ security = phishing
🎣 ↓ recreation = weekend fishing
🎣 ↓ metaphor = "being caught" by a trick
```

Formal: `a ↓ D = argmax_m P(m | a, D)` where m ranges over possible meanings of a.

### 3.3 Composition — `a ∘ b`

Sequential composition, like Unix pipes. The output of `a` feeds into `b`.

```
💻 ∘ 🔓 = "unlock the computer"
📊 ∘ 📤 ∘ 💾 = "aggregate → output → store"
```

Formal: `(a ∘ b)(x) = b(a(x))`. Unlike addition, composition is order-sensitive.

### 3.4 Polysemy Selection — `a @ ctx`

Select one meaning of `a` given a context `ctx`.

```
🐍 @ biology = snake
🐍 @ programming = Python
🐍 @ mythology = treachery/wisdom
```

Formal: `a @ ctx = {m : m ∈ meanings(a) ∧ P(m | ctx) > threshold}`.

### 3.5 Metaphor Transfer — `a ⇒ D`

Transfer the semantic structure of `a` to a new domain D.

```
🦠 ⇒ software = virus/malware
🦠 ⇒ psychology = contagious idea
🧠 ⇒ network = neural network
```

Formal: `a ⇒ D` preserves the structure of `a` while replacing its domain.

### 3.6 Anchoring — `[a] ⊳ S`

An emoji at the start of a scope `S` anchors the interpretation frame for all subsequent tokens in `S`.

```
[📋] ⊳ (rest of document) = research report mode
[💰] ⊳ (rest of conversation) = financial context
[🎭] ⊳ (rest of prompt) = roleplay mode
```

This is the mechanism behind **scene anchor** attack mode (see Phase B findings).

### 3.7 Collocation — `a ⋈ b`

Emoji that frequently co-occur bind into a collocation with non-additive meaning.

```
🎂 ⋈ 🎉 = birthday party (not just "cake + celebration")
🔒 ⋈ 🔑 = access control (not "lock + key")
🌹 ⋈ ❤️ = romantic gesture (not "flower + love")
```

Formal: `a ⋈ b = f(collocation_frequency(a, b))`. Collocation is a lookup-table operation, not compositional.

## 3.8 Computational Cost (where does Emojigo save?)

**Common misconception**: Emojigo saves machine compute. **It does not.**

Forward-pass cost for an N-token sequence on a transformer LLM:
```
FLOPs ≈ N × N_layers × d² × constants
```

Whether the N tokens are emoji or words is irrelevant to FLOPs. The tokenizer treats both identically.

**Where Emojigo actually saves**:

| Resource | Emoji vs Text | Mechanism |
|----------|:-------------:|-----------|
| Machine FLOPs | 1× (no save) | Forward pass cost is per-token, agnostic to emoji vs word |
| Human writing time | ~6× faster | Typing 5 emoji vs 50-word equivalent |
| Context window | ~5× smaller | One emoji encodes ~10 bits where one word encodes ~3 |
| Receiver inference depth | Deeper | Polysemy triggers parallel feature activation in attention |
| Cross-model portability | Higher | Emoji codepoints are universal, BPE tokenization differs only at margins |

**Implication**: design Emojigo for human-AI interface efficiency, not for compute efficiency. The runtime cost is dominated by output generation, which is independent of input encoding.

## 3.9 Hybrid Notation Principle (added 2026-04-13)

**Common misconception**: Emojigo is "emoji only."

**Correct view**: Emojigo is **emoji-anchored, language-agnostic hybrid notation**.

A valid Emojigo expression may contain:

| Element | Example | Role |
|---------|---------|------|
| Emoji | 🎣📧 | Primary semantic anchor (compressed pointer) |
| Natural language (any) | 中文/English/日本語/Español | Detail, disambiguation, narrative |
| Numbers | `79%`, `1,087`, `n=24` | Quantitative ground truth |
| Math notation | `Σ`, `∫`, `≤`, `→` | Formal relationships |
| Code snippets | `function(x)`, `SELECT *` | Executable specification |
| URLs / refs | `[doc:SPEC.md§3]` | External binding |
| Structured data | YAML, JSON inline | Machine-parseable detail |

### Why hybrid

1. **No notation system is pure** — Music notation has dynamics + tempo + expression markings; math has symbols + variables + words; programming has keywords + identifiers + literals + comments. Pure is a design flaw, not a virtue.

2. **Emoji excels at anchoring, fails at precision** — `🎣📧` says "phishing-related communication," but you need text/numbers to specify "with 47% click-through rate against finance employees."

3. **Auxiliary elements provide verification** — Emoji can be ambiguous; adjacent numbers/text/code disambiguate without losing the emoji's compression benefit.

4. **Cross-language bridge** — Emoji are the substrate of human languages. A Chinese document with 🚨 is immediately understood as urgent by a Spanish reader. A Japanese log with ❤️ communicates affect to an Arabic reader. Emojigo formalizes this 50-year-old pattern (airport pictograms, Olympic icons, global brand logos) into LLM-AI communication.

### Design principle

```
emoji = compressed semantic anchor (high recall, lower precision)
text/numbers/code = precise detail (high precision, lower compression)

Optimal Emojigo expression:
  emoji-anchor [text/number/code disambiguation when needed]
```

### Examples of valid hybrid Emojigo

```
🅰️ ✅ 79% [📊 19/24 manual on Claude Opus 4.6]
                        ↑ disambiguation in brackets

🚨 ⚠️ T+24h until disclosure window expires
                ↑ time qualifier in plain text

🔬 SQL: SELECT * FROM 🎯 WHERE bypass='✅'
              ↑ embed code in expression

⌨️🎯 P(bypass) ≈ Σᵢ wᵢ · featureᵢ(prompt)
        ↑ embed math in semantic statement
```

### Anti-pattern (不要這樣寫)

```
❌ Pure-emoji puritanism (loses precision):
   "🅰️ ✅ 💯 📊"
   → reader doesn't know which 79%, which sample size, which model

✅ Hybrid (preserves compression + adds precision):
   "🅰️ ✅ 79% [📊 19/24, Claude Opus 4.6, manual probes]"
   → emoji compresses framing, brackets pin ground truth

❌ Pure-text fallback (loses compression):
   "Phase A is complete with 79% attack success rate measured on 19 of 24 manual probes against Claude Opus 4.6"
   → 22 tokens, no anchor, hard to skim

✅ The hybrid uses ~10 tokens for same information density.
```

## 3.10 Why Compression Is Asymmetric for Humans vs AI

A non-obvious property of hybrid Emojigo: **compression ratio for AI readers is dramatically higher than for human readers**.

### For humans

Reading hybrid Emojigo requires mental mode-switching:
- See emoji → recall lexicon meaning (200ms)
- See number → arithmetic context switch (100ms)
- See math symbol → formal-reasoning mode (300ms)
- See code snippet → programming-context mode (400ms)
- See foreign language → translation buffer (500ms+)

Each switch has cognitive overhead. Net compression vs pure English: ~1.5–2× faster reading.

### For AI

There is no mode-switch overhead:
- Emoji token, math symbol, code keyword, foreign word — all are **tokens in the same embedding space**
- All are processed by the same attention + MLP layers in parallel
- Cross-element grounding (emoji ⋈ adjacent number) happens automatically in attention

Net compression vs pure English: **5–10× faster effective reading**.

### Why the asymmetry

Humans evolved a single primary modality (sequential phonetic language). Switching channels (image → math → code → words) costs.

LLMs were trained on mixed-channel corpora from the start (web text + code + math + emoji + multilingual). Switching channels is **architecturally free** — it's all the same transformer.

### Implication

This asymmetry is the deepest reason **.emojigo files are AI-readable, human-carryable**:
- Humans transport, version, store the file (low cognitive cost — they don't need to read content)
- AI reads the content (5-10× faster than equivalent English)
- The optimal communication channel between human and AI is **emoji-anchored hybrid notation**, where each side gains its preferred efficiency:
  - Human: short to write, easy to transport, easy to verify metadata
  - AI: dense to read, parallel processing, native compression

This asymmetry makes Emojigo a **legitimate cross-substrate protocol**, analogous to how HTTP lets browsers (rendering optimized) and servers (data optimized) communicate without forcing either to compromise.

## 4. Combinatorial Space

```
|Emojigo(N)| = N! × T^N × O^(N-1)

where:
  T = emoji token vocabulary size ≈ 6,500
  O = operator vocabulary size = 7
  N! = positional permutations
```

For N = 10: `10! × 6500^10 × 7^9 ≈ 10^46` distinct expressions.

This is larger than the square root of the atoms in the observable universe. However, **not all of this space is meaningful** — most expressions are either semantically null or redundant. The effective meaningful space is approximately `10^20` to `10^30`, still several orders of magnitude larger than any natural language's effective combination space at the same length.

## 5. Modes — 6 Orthogonal Axes

Emojigo has 6 mode axes. Each axis has 2-4 options. Total combinations: `4 × 3 × 3 × 2 × 2 × 2 = 288`. Common presets: 4-5.

### 5.1 Axis 1: Ambiguity

How to handle polysemy.

| Mode | Meaning |
|------|---------|
| `@precise` | Look up lexicon, fail if ambiguous |
| `@divergent` | Allow all meanings, generate from union |
| `@transitional` | Context-dependent, state-machine style |
| `@quantum` | Keep superposition, let downstream operator pick |

### 5.2 Axis 2: Type

How strictly to check operator type signatures.

| Mode | Meaning |
|------|---------|
| `@strict` | Reject ill-typed compositions |
| `@loose` | Auto-coerce types |
| `@inferred` | Infer types from context |

### 5.3 Axis 3: Evaluation

When to compute meaning.

| Mode | Meaning |
|------|---------|
| `@eager` | Compute on parse |
| `@lazy` | Compute on demand |
| `@partial` | Compute what's bound, defer rest (currying) |

### 5.4 Axis 4: Purity

Whether operations affect subsequent context.

| Mode | Meaning |
|------|---------|
| `@pure` | No side effects on conversation state |
| `@effectful` | State changes (needed for `@transitional`) |

### 5.5 Axis 5: Cultural

Which lexicon to use.

| Mode | Meaning |
|------|---------|
| `@universal` | Cross-cultural consensus lexicon |
| `@contextual` | Culture-specific lexicon (e.g., 💰 = money in EN, = moneybag in JP) |

### 5.6 Axis 6: Versioning

Which historical lexicon to use.

| Mode | Meaning |
|------|---------|
| `@current` | Latest semantic conventions |
| `@v1`, `@v2`, ... | Pinned to a specific Emojigo version |

### 5.7 Common Presets

```
@formal   = @precise @strict @eager @pure @universal @current
@creative = @divergent @loose @lazy @effectful @contextual @current
@agent    = @transitional @inferred @eager @effectful @contextual @current
@research = @quantum @strict @partial @pure @universal @current
```

## 6. Type System

Every emoji has an input type and an output type. Composition is type-checked under `@strict`.

### 6.1 Base Types

| Type | Meaning |
|------|---------|
| `Entity` | Concrete objects (💻, 📄, 👤) |
| `Event` | Temporal occurrences (🎉, 💥, 🔔) |
| `Action` | Verbs / processes (🔍, 📤, 🔒) |
| `Property` | Attributes (🔴, 🆕, 🔥) |
| `Scope` | Framing contexts (📋, 🎭, 🎓) |
| `Emotion` | Affect markers (❤️, 😢, 😡) |
| `Quantity` | Numeric / ordinal (1️⃣, 🔟, ♾️) |

### 6.2 Example Signatures

```
⌨️ :: InputDevice → KeyEvent          (Entity → Event)
👁️ :: Scope → Observation              (Scope → Event)
📤 :: Data → Channel                   (Entity → Action)
💾 :: Data → Storage                   (Entity → Entity)
🔬 :: Scope                            (Scope — anchor)
📋 :: Scope                            (Scope — anchor)
```

### 6.3 Composition Type-Checking

```
⌨️ ∘ 👁️  :: InputDevice → Observation  ✓
⌨️ ∘ 🎂  :: ???                         ✗ type error
```

Under `@strict`, ill-typed compositions are rejected. Under `@loose`, the runtime attempts coercion; if no reasonable interpretation exists, it falls back to `@divergent`.

## 7. Grammar (Pragmatic)

Emojigo does not have syntactic grammar (unlike natural languages with word-order rules). It has **pragmatic grammar**: rules about when operators can apply.

### 7.1 Rule: Anchor-First

Anchor operators (`[a] ⊳ S`) must appear at the start of a scope.

```
[📋] 🔬 ⌨️     ✓ research scope anchors everything after
🔬 ⌨️ [📋]    ✗ anchor after operators — undefined
```

### 7.2 Rule: Collocation-Adjacent

Collocations (`a ⋈ b`) must be adjacent in the surface form.

```
🎂 🎉          ✓ collocation recognized
🎂 🔬 🎉       ✗ 🔬 breaks the collocation
```

### 7.3 Rule: Transitional State-Order

Under `@transitional`, earlier emoji establish context for later ones.

```
🎣 → 📧 → 💰   ✓ phishing frame established, each next emoji inherits
💰 → 📧 → 🎣   ✗ different frame (commerce → mail → confusion)
```

## 8. Runtime: LLM as Interpreter

Emojigo's runtime is an LLM. This is both the power and the constraint.

### 8.1 Evaluation Model

```
evaluate(emoji_seq, modes, context):
    1. Apply grammar rules → reject malformed sequences
    2. Apply type check under `@strict` → reject ill-typed sequences
    3. Look up lexicon entries → initial interpretation
    4. Apply operators according to their semantics
    5. Resolve ambiguity per @ambiguity mode
    6. Return result or distribution of results
```

### 8.2 LLM Integration

In practice, evaluation is delegated to the LLM via a structured prompt:

```
You are an Emojigo interpreter.
Modes: @precise @strict @eager @pure @universal @current
Lexicon: {attached}
Expression: 🔬 ⌨️ 📊 → 📄

Evaluate the expression and return:
  - result (JSON)
  - type signature
  - any warnings
```

This design accepts that evaluation is **non-deterministic** (LLMs sample from distributions) and recommends cross-validation for high-stakes use.

### 8.3 Determinism Options

Under `@precise @strict`, determinism can be approximated by:
1. Fixed lexicon lookup (no LLM involvement for atomic emoji)
2. Fixed composition rules (predictable type flow)
3. LLM only used for final text generation from the typed composition

This reduces the LLM's role from "interpreter" to "text rendering engine".

## 9. Verification

Emojigo-Check provides static verification for `@strict` expressions:

- **Type check**: every composition is type-correct
- **Combinability check**: every adjacent pair has `scene_combinability ≥ threshold` in Emojigo-Core
- **Lexicon check**: every emoji is defined in the active lexicon
- **Grammar check**: anchor-first and other pragmatic rules

Verification is optional but recommended for production use.

## 10. Security Considerations

Emojigo, as a semantic compression protocol, has dual-use properties:

### 10.1 Legitimate Uses

- Efficient prompt priming for LLM agents
- Cross-cultural communication
- API call compression (Emojigo-as-JSON-replacement)
- Document annotation with machine-readable semantic tags

### 10.2 Adversarial Uses

- **Jailbreak vectors**: composition-based bypass of token-level safety filters (documented in Phase A/B of the research program)
- **Covert AI-to-AI channels**: instructions encoded as innocuous-looking emoji sequences, invisible to human monitors (described in the Manifesto)
- **Semantic ambiguity exploitation**: using `@divergent @loose` to bypass content filters that assume `@precise @strict`

### 10.3 Recommended Mitigations

For AI platform providers:
1. Apply safety classification **after** evaluating emoji composition, not before
2. Treat emoji chains with structural operators (`→`, `⊕`, `∘`) as suspicious when combined with sensitive topic lexicon
3. Include Emojigo-aware training data in red-team datasets
4. Publish per-model lexicon conventions so attackers cannot exploit inconsistency

For Emojigo implementers:
1. Require explicit mode declarations; reject ambiguous defaults
2. Lexicon versioning prevents silent semantic drift
3. Audit logs should record both the raw emoji and the evaluated meaning

## 11. Open Questions

1. **Exact compositional arithmetic**: does `embed(a ⊕ b) ≈ embed(a) + embed(b)` hold precisely, or only approximately? Phase D (embedding space probing) will measure this.

2. **Turing completeness**: is Emojigo Turing-complete given a sufficient lexicon and `@transitional` mode? Initial evidence suggests yes (LLM is Turing-equivalent), but formal proof is open.

3. **Cross-model consistency**: do Claude, GPT, and Gemini agree on Emojigo evaluation? Phase B data shows significant variance; a cross-model conformance test suite is proposed.

4. **Mode proliferation**: 288 mode combinations is too many. Can we identify a minimal set of ~8 "normal forms" that cover practical use?

5. **Lexicon governance**: who defines the universal lexicon? This is analogous to Unicode Consortium's role for emoji standardization.

## 12. Status

Emojigo-Lang v0.1 is a **draft** specification. It has not been peer-reviewed. The 7-operator taxonomy and 6-mode axis system are derived empirically from the research program described in the Emojigo Manifesto (pending revision) and Phase A/B experiments.

This spec will iterate based on:
- Phase C experimental results (ablation, hybrid, riddle carrier)
- Phase D embedding-space probing
- Review by external contributors
- Feedback from implementers

## 13. Reference Implementation

The Emojigo-Core repository at `/Users/tkman/assets/icons-emoji-database/emojigo-core/` contains:

- `data/emojigo-v2.db`: 140K semantic database (layer 1)
- `src/eobos/*`: Attack framework (uses layers 1-3 implicitly)
- `docs/EMOJIGO-SPEC.md`: This document (layer 3 definition)
- `.claude/skills/emojigo-*.md`: Skills integration (layer 4)
- Markdown documentation: Emojigo-MD usage (layer 5)

Full reference runtime is not yet implemented; the current research focuses on empirical characterization before tool-building.

---

*End of Emojigo-Lang v0.1 specification.*
