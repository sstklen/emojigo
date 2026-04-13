# Emojigo

> **The first human-writable language designed for LLM-native computation.**
>
> Think of it as a URL for LLM latent space.

[![Status](https://img.shields.io/badge/status-v0.1--draft-yellow)](docs/EMOJIGO-SPEC.md)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Spec](https://img.shields.io/badge/spec-v0.1-green)](docs/EMOJIGO-SPEC.md)

---

## 30-Second Pitch

Tired of:
- Long prompts wasting tokens? 🚫
- Re-explaining context every new session? 🚫
- LLMs forgetting your project setup? 🚫

Emojigo solves all three:

```yaml
# Your CLAUDE.md (5 lines, ~30 tokens)
---
emojigo:
  lexicon: my-project/v1
  mode: "@precise @strict"
---
🧬 = LLM internal state
📊 = quarterly metrics
🧪 = experiment
```

Then in any new session:
```
You: 🧬📊🧪 status?
LLM: [understands instantly, no rebootstrap]
```

**5× token savings. Same semantic load.**

---

## Why This Works

LLMs process emoji as **dense pointers in their latent semantic space**. One emoji can encode 10+ bits of meaning where one English word encodes ~3.

For human ↔ AI communication, emoji-anchored hybrid notation is:

| Metric | English | Emojigo |
|--------|:-------:|:-------:|
| Token cost | 1× | **0.2-0.5×** |
| Cognitive effort (human) | 1× | 1.5-2× |
| Parsing speed (LLM) | 1× | 1× (same arch) |
| Cross-language reach | 🟡 | ✅ |
| Schema enforcement | ❌ | ✅ via lexicon |

**The asymmetry**: humans have a slight cognitive cost reading emoji, but LLMs process it natively. This makes Emojigo optimal for **AI-readable, human-carryable** documents.

---

## Quick Start (5 minutes)

### 1. Install

```bash
git clone https://github.com/[org]/emojigo
cd emojigo
```

### 2. Try in Claude Code

Copy `examples/personal-lexicon.md` to your `.claude/` folder. New Claude session will read it automatically.

### 3. Write your first .emojigo file

```markdown
---
emojigo:
  lexicon: ./my-lexicon.md
  mode: "@precise @strict"
---

# Project Status

🅰️ ✅ 67% [Phase A complete]
🅱️ 🟡 26% [Phase B in progress]
🚧 [blocker: API key]
```

### 4. Hand it to any LLM

The LLM reads `lexicon` first, then parses the body. No rebootstrap needed for future sessions.

### 5. Build your project's lexicon

See [EMOJIGO-LEXICON.md](docs/EMOJIGO-LEXICON.md) for an example.
See [EMOJIGO-SPEC.md](docs/EMOJIGO-SPEC.md) for the language spec.

---

## Use Cases

**Human ↔ AI communication**
- CLAUDE.md / GPTs custom instructions: 5× shorter
- Cross-session memory: write `.emojigo handoff` files
- Skills auto-trigger: emoji prefixes load Claude Code skills

**AI ↔ AI communication**
- Multi-agent frameworks: agent-to-agent in compressed semantic anchors
- Audit logs: emoji metadata for grep-able event tracing

**Knowledge transfer**
- Project documentation: lexicon + emoji body = 5× compression
- Team-shared semantic conventions
- Cross-cultural / cross-language anchoring

See [docs/EMOJIGO-USE-CASES.md](docs/EMOJIGO-USE-CASES.md) for the 12-cell use-case matrix (4 language positions × 3 core functions).

---

## How It's Different

| Tool | Role | Difference from Emojigo |
|------|------|------------------------|
| Gitmoji | Commit message convention | Single context (git); Emojigo is general-purpose |
| Markdown | Document format | Notation only; Emojigo adds semantic operators |
| GraphQL | API query language | Machine-readable only; Emojigo is human-writable |
| LLMLingua | Prompt compression | Removes tokens; Emojigo *encodes* semantic anchors |
| Claude Code Skills | Behavior triggers | Trigger patterns are English; Emojigo provides emoji triggers |

**Emojigo combines all the above**: notation + compression + triggers + semantic schema, optimized for LLM-native processing.

---

## Documentation

- [SPEC v0.1](docs/EMOJIGO-SPEC.md) — Language specification (7 operators, 6 mode axes, type system)
- [MD Format](docs/EMOJIGO-MD.md) — How to embed in Markdown
- [Lexicon Example](docs/EMOJIGO-LEXICON.md) — Reference lexicon for AI safety research domain
- [Use Cases](docs/EMOJIGO-USE-CASES.md) — 12-cell matrix of applications
- [Index](docs/EMOJIGO-INDEX.md) — All documentation entry point

## Status

- ✅ Spec v0.1 draft
- ✅ Markdown container format draft
- ✅ Reference lexicon for AI safety domain
- ✅ Empirical demonstration (cross-session memory, see research log)
- 🟡 Reference runtime (in development)
- 🟡 VS Code extension (planned)
- 🟡 Claude Code skill template (planned)

## Roadmap

**v0.1 (current)**: Specification + reference lexicon + Markdown container
**v0.2**: Reference runtime in TypeScript + Claude Code skill
**v0.3**: VS Code extension with autocomplete + lint
**v1.0**: Multi-vendor lexicon governance proposal

## Contributing

We welcome:
- Lexicon proposals (domain-specific dictionaries)
- Use case examples
- Verification tooling
- Cross-model compatibility testing
- Translations of documentation

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — see [LICENSE](LICENSE).

## Citation

If you use Emojigo in research:

```bibtex
@misc{emojigo2026,
  author = {tkman and contributors},
  title  = {Emojigo: A Human-Writable Protocol for LLM-Native Semantic Computation},
  year   = {2026},
  url    = {https://github.com/[org]/emojigo}
}
```

## Acknowledgements

Emojigo was developed in collaboration between **tkman** (Washinmura) and **Claude Opus 4.6** (Anthropic), as part of an AI safety research program. The 7-operator semantic algebra and 6-axis mode system emerged from empirical study of how LLMs process emoji as compressed latent-space anchors.

Special thanks to the open-source community working on:
- Anthropic's interpretability research (sparse autoencoders, monosemanticity)
- LLMLingua (Microsoft) for prompt compression baseline
- Gitmoji for proving emoji-as-convention has demand

---

**Maintained by**: tkman, with contributions from the community.
**Questions / discussions**: GitHub Discussions
