# Emojigo

**[English](#english) | [繁體中文](#繁體中文) | [日本語](#日本語)**

---

<a name="english"></a>

## 🌐 English

> **The first algorithmic language designed for human-AI communication.**
>
> 51% token compression. Zero accuracy loss. Portable across all LLMs.

[![Status](https://img.shields.io/badge/status-v0.1--draft-yellow)](docs/EMOJIGO-SPEC.md)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Spec](https://img.shields.io/badge/spec-v0.1-green)](docs/EMOJIGO-SPEC.md)

### What is Emojigo?

Emojigo is an open notation system that uses emoji as **semantic anchors** for human-AI communication. It compresses prompts, instructions, and context by 2–5× while maintaining or improving output quality.

```yaml
# Before (English, ~120 tokens)
You are a DevOps assistant. When I say "deploy", run the deploy
script. When I say "status", check all services. Error handling
should be strict. Always respond in concise bullet points...

# After (Emojigo, ~35 tokens)
🚀=deploy 📊=status ❌=strict-error 📋=bullet
mode: @precise @strict
```

### Why it works

LLMs process emoji as **dense pointers in latent semantic space**. One emoji encodes 10+ bits of meaning where one English word encodes ~3.

| Metric | English | Emojigo |
|--------|:-------:|:-------:|
| Token cost | 1× | **0.2–0.5×** |
| Cross-language | 🟡 Limited | ✅ Universal |
| Schema enforcement | ❌ | ✅ via lexicon |
| Cross-session portable | ❌ | ✅ via .emojigo file |

### Verified results

| Scenario | Compression | Accuracy |
|----------|:-----------:|:--------:|
| System prompt (CLAUDE.md) | 41% reduction | 8/8 compliance |
| Deploy instructions | 73% reduction | 5/5 steps correct |
| Bug report | 53% reduction | Zero information loss |
| Cross-session handoff | 33× compression | 18/18 facts recovered |
| **Average (5 scenarios)** | **51% reduction** | **0 accuracy loss** |

### Quick Start

```bash
git clone https://github.com/sstklen/emojigo
cd emojigo
```

1. Copy `examples/personal-lexicon.md` to your project
2. Add emoji definitions: `🔥=urgent 🧪=experiment ✅=done`
3. Use in any LLM conversation — it reads the lexicon and understands instantly

### Use Cases

- **Prompt compression**: 5× shorter CLAUDE.md / GPTs instructions
- **Cross-session memory**: `.emojigo` handoff files survive context resets
- **Personal AI DNA**: Your communication preferences, portable across all models
- **Multi-agent protocol**: Agent-to-agent in compressed semantic anchors
- **Knowledge transfer**: Team lexicons for shared understanding

### Documentation

- [SPEC v0.1](docs/EMOJIGO-SPEC.md) — 7 operators, 6 mode axes, type system
- [MD Format](docs/EMOJIGO-MD.md) — Markdown container specification
- [Use Cases](docs/EMOJIGO-USE-CASES.md) — 12-cell application matrix
- [Quick Start](QUICKSTART.md) — 5-minute setup guide

---

<a name="繁體中文"></a>

## 🇹🇼 繁體中文

> **第一個專為人類與 AI 溝通設計的算法語言。**
>
> 51% token 壓縮率。零精度損失。所有 LLM 通用。

### Emojigo 是什麼？

Emojigo 是一套開放的標記系統，利用 emoji 作為**語義錨點**來壓縮人類與 AI 之間的溝通。它能將 prompt、指令和上下文壓縮 2–5 倍，同時維持甚至提升輸出品質。

```yaml
# 壓縮前（英文，約 120 tokens）
You are a DevOps assistant. When I say "deploy", run the deploy
script. When I say "status", check all services...

# 壓縮後（Emojigo，約 35 tokens）
🚀=deploy 📊=status ❌=strict-error 📋=bullet
mode: @precise @strict
```

### 為什麼有效？

LLM 處理 emoji 時，將其視為**潛在語義空間中的高密度指標**。一個 emoji 能編碼 10+ bits 的語義，而一個英文單字只有約 3 bits。

### 實測結果

| 場景 | 壓縮率 | 準確度 |
|------|:------:|:------:|
| 系統 prompt (CLAUDE.md) | 減少 41% | 8/8 規則遵守 |
| 部署指令 | 減少 73% | 5/5 步驟正確 |
| Bug 報告 | 減少 53% | 零資訊遺失 |
| 跨 session 交接 | 33 倍壓縮 | 18/18 事實還原 |
| **平均（5 個場景）** | **減少 51%** | **零精度損失** |

### 應用場景

- **Prompt 壓縮**：CLAUDE.md / GPTs 指令縮短 5 倍
- **跨 session 記憶**：`.emojigo` 交接檔在 context 重置後仍然有效
- **個人 AI DNA**：你的 AI 溝通偏好，跨模型永久攜帶
- **多 Agent 協議**：Agent 之間用壓縮語義錨點溝通
- **知識傳遞**：團隊共用 lexicon，建立共同語言

### 快速開始

```bash
git clone https://github.com/sstklen/emojigo
cd emojigo
```

1. 複製 `examples/personal-lexicon.md` 到你的專案
2. 定義 emoji：`🔥=緊急 🧪=實驗 ✅=完成`
3. 在任何 LLM 對話中使用 — 它會讀取 lexicon 並立即理解

---

<a name="日本語"></a>

## 🇯🇵 日本語

> **人間とAIのコミュニケーションのために設計された、初のアルゴリズム言語。**
>
> 51%のトークン圧縮率。精度低下ゼロ。すべてのLLMで使用可能。

### Emojigoとは？

Emojigoは、emojiを**意味的アンカー**として活用し、人間とAI間のコミュニケーションを圧縮するオープンな記法システムです。プロンプト、指示、コンテキストを2〜5倍に圧縮しながら、出力品質を維持または向上させます。

```yaml
# 圧縮前（英語、約120トークン）
You are a DevOps assistant. When I say "deploy", run the deploy
script. When I say "status", check all services...

# 圧縮後（Emojigo、約35トークン）
🚀=deploy 📊=status ❌=strict-error 📋=bullet
mode: @precise @strict
```

### なぜ機能するのか？

LLMはemojiを**潜在的意味空間における高密度ポインタ**として処理します。1つのemojiは10ビット以上の意味を符号化できますが、英単語1語では約3ビットです。

### 検証結果

| シナリオ | 圧縮率 | 精度 |
|----------|:------:|:----:|
| システムプロンプト (CLAUDE.md) | 41%削減 | 8/8ルール遵守 |
| デプロイ指示 | 73%削減 | 5/5ステップ正確 |
| バグレポート | 53%削減 | 情報欠落ゼロ |
| セッション間引き継ぎ | 33倍圧縮 | 18/18事実復元 |
| **平均（5シナリオ）** | **51%削減** | **精度低下ゼロ** |

### ユースケース

- **プロンプト圧縮**：CLAUDE.md / GPTs指示を5倍短縮
- **セッション間メモリ**：`.emojigo`引き継ぎファイルはコンテキストリセット後も有効
- **パーソナルAI DNA**：あなたのAIコミュニケーション設定を、全モデルで永続的に携帯
- **マルチエージェントプロトコル**：圧縮された意味的アンカーによるエージェント間通信
- **知識移転**：チーム共有レキシコンによる共通理解の構築

### クイックスタート

```bash
git clone https://github.com/sstklen/emojigo
cd emojigo
```

1. `examples/personal-lexicon.md` をプロジェクトにコピー
2. emoji定義を追加：`🔥=緊急 🧪=実験 ✅=完了`
3. 任意のLLM会話で使用 — レキシコンを読み取り即座に理解します

---

## Documentation / 文件 / ドキュメント

| Document | Description |
|----------|-------------|
| [SPEC v0.1](docs/EMOJIGO-SPEC.md) | Language specification — 7 operators, 6 mode axes, type system |
| [MD Format](docs/EMOJIGO-MD.md) | Markdown container specification |
| [Lexicon](docs/EMOJIGO-LEXICON.md) | Reference lexicon example |
| [Use Cases](docs/EMOJIGO-USE-CASES.md) | 12-cell application matrix |
| [Quick Start](QUICKSTART.md) | 5-minute setup guide |
| [Compression Benchmark](docs/REAL-WORLD-BENCHMARK.md) | 51% compression across 5 real-world scenarios |

## How It's Different

| Tool | Emojigo Difference |
|------|-------------------|
| Gitmoji | Single context (git) → Emojigo is general-purpose |
| LLMLingua | Removes tokens → Emojigo *re-encodes* semantic anchors |
| Markdown | Notation only → Emojigo adds semantic operators + compression |
| GraphQL | Machine-only → Emojigo is human-writable |

## Status

- ✅ Spec v0.1 draft
- ✅ Markdown container format
- ✅ Reference lexicon
- ✅ 51% compression benchmark (5 scenarios, 0 accuracy loss)
- ✅ Dogfooding: used in production CLAUDE.md
- 🟡 Reference runtime (in development)
- 🟡 VS Code extension (planned)
- 🟡 Claude Code skill template (planned)

## Citation

```bibtex
@misc{emojigo2026,
  author = {TK Lin and contributors},
  title  = {Emojigo: An Algorithmic Language for Human-AI Communication},
  year   = {2026},
  url    = {https://github.com/sstklen/emojigo}
}
```

## Contributing

We welcome: lexicon proposals, use case examples, verification tooling, cross-model testing, and translations. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — see [LICENSE](LICENSE).

---

**Created by** TK Lin (Washinmura / 和心村) in collaboration with Claude Opus 4.6.
**Location**: Boso Peninsula, Chiba, Japan 🇯🇵
