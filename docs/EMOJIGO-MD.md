# Emojigo-MD: Markdown Container Specification

**Version**: 0.1
**Status**: draft
**Date**: 2026-04-13
**Authors**: tkman + Claude Opus 4.6
**Layer**: 5 (User-facing file format) of the Emojigo stack
**Depends on**: `EMOJIGO-SPEC.md` (v0.1), `EMOJIGO-LEXICON.md` (v1)

> *Emojigo-MD 讓 Emojigo 表達式嵌入既有的 Markdown 工作流。*
> *類比：HTML 嵌 `<script>` / Markdown 嵌 ` ``` ` code block。*

---

## 0. 為什麼要 Emojigo-MD

Emojigo-Lang（layer 3）定義了語言核心，但實際使用必須有「容器」。直接把 raw emoji 丟進 chat 失去三件事：**持久化**（無 diff、無 reproducibility）、**元資訊**（lexicon / mode / version 沒地方寫）、**混排**（emoji + prose + code 在同一份文件）。

Emojigo-MD 在 Markdown 上加最小集合的約定，讓 Emojigo 表達式能被宣告、辨識、解譯。設計原則：**零工具**（純 plain text）、**向下相容**（標準 Markdown reader 不會壞）、**明示優於隱示**（mode/lexicon/version 全寫出來）、**一份檔案一個 lexicon 預設**（避免歧義）。

---

## 1. Frontmatter 區塊

### 1.1 基本宣告

每份 Emojigo-MD 文件以 YAML frontmatter 起頭：

```yaml
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@precise @strict @current"
  version: 0.1
---
```

**Rationale**：把元資訊集中在頂端，後續所有 block 預設套用，避免每個 block 重複宣告。

### 1.2 欄位

必填：`lexicon`（識別字串 `<name>/<version>` 或相對路徑）、`mode`（6 軸子集，空格分隔）、`version`（目前固定 `0.1`）。選填：`extends`（繼承基礎 lexicon，見 §5）、`contributors`（貢獻者清單，見 §7）。`mode` 省略時套用 `@formal` preset = `@precise @strict @eager @pure @universal @current`。

**Rationale**：必填三項是評估表達式的最小完整資訊；其餘協作場景才需要。`@formal` 是最嚴格的預設，行為最可預測，任何放鬆都應明示。

---

## 2. Inline Emoji

文件本文中的 emoji 有三種強度標記。預設行為是「最弱標記」，越強的標記覆蓋越弱的。

### 2.1 Raw emoji（隱式）

直接寫 emoji，由 frontmatter 的 lexicon 與 mode 解讀：

```markdown
今天跑了 🔬 ⌨️ 📊，準備寫 📄。
```

**Rationale**：對熟悉 lexicon 的讀者最自然。Emojigo-Check 也夠用 — 解讀規則來自 frontmatter。

### 2.2 強型別標記（顯式）

當 emoji 在當前 lexicon 有歧義、或想覆蓋預設解讀時：

```markdown
{🎣 :: phishing} 不是 {🎣 :: recreation}
```

語法：`{<emoji> :: <type-or-meaning>}`，其中 `type-or-meaning` 可以是 base type（見 SPEC §6.1）或 lexicon 裡的 meaning string。

**Rationale**：對應 SPEC §3.2 projection 運算（`a ↓ D`）。Inline 標記讓讀者一眼看出 type，也讓 Emojigo-Check 不必呼叫 LLM 就能驗證。

### 2.3 跨 lexicon 引用

引用其他 lexicon 的 emoji 時，使用 namespace 前綴 `@<lexicon>/`：

```markdown
@finance/💰 跟 @emojigo-core/💰 在語義上不同。
```

語法：`@<lexicon-name>/<emoji>` 或 `@<lexicon-name>:<version>/<emoji>`。

**Rationale**：對應 SPEC §5.5 cultural axis。一份文件可能引用多個 lexicon，namespace 確保不會混淆。

### 2.4 強度優先順序

當同一個 emoji 同時有多種標記時，優先順序由強到弱：強型別 `{🔬 :: scope}` → namespace `@biology/🔬` → raw `🔬`（套用 frontmatter 預設）。

**Rationale**：明示優於隱示，本地優於全域。

---

## 3. Fenced Block

`:::emojigo` block 框出純 Emojigo 表達式：

```
:::emojigo
🔬 → ⌨️ → 📊 → 📄
:::
```

**Rationale**：對應 SPEC §3.3 composition 的長序列。Block 形式比 inline 更適合多 statement、多行表達式。

### 3.1 Mode 修飾

Block 可以宣告本地 mode，覆蓋 frontmatter 預設：

```
:::emojigo divergent
🎯 + ??
:::
```

支援 SPEC §5.7 preset，或自訂 mode 軸組合（`:::emojigo @precise @strict @lazy`）。

**Rationale**：一份文件常常需要混合 mode（嚴謹的研究筆記裡也想用 `@divergent` 跑一段腦力激盪）。Block-level mode 讓這件事不必新開檔案。

### 3.2 多 statement

Block 內可以放多個獨立 statement，以空行分隔，各自評估後按順序回傳結果列表：

```
:::emojigo
🅱️ 📊 → 🧪

🧪 ©️ → 📄
:::
```

**Rationale**：對應「一段話包含多個獨立思路」的常見寫作習慣。空行分隔比每段都開新 block 簡潔。

### 3.3 Lexicon 引用

Block 內可以用 §2.3 的 namespace 語法引用其他 lexicon，但**不能在 block 內重新宣告 lexicon**。

**Rationale**：lexicon 是文件級設定，跨 block 一致。block-level 只允許 mode 變動，避免一份文件出現多個解讀框架混亂。

---

## 4. Code-Fence 變體

為了相容既有 syntax highlighter 與 Markdown processor，也支援標準 code fence，並可在 fence info 帶 mode：

````markdown
```emojigo
🔬 → ⌨️ → 📊 → 📄
```

```emojigo divergent
🎯 + ??
```
````

兩種語法功能對等：`:::emojigo` 需 Emojigo-aware renderer，` ```emojigo ` 任何 Markdown renderer 都吃。需要本地 mode 用前者，純嵌入相容用後者。

**Rationale**：很多 Markdown viewer（GitHub、VS Code、Obsidian）對 ` ``` ` 有 syntax highlighting，對 `:::` 不一定有。Code fence 變體讓既有工具鏈零成本支援 Emojigo。

---

## 5. Reference 機制

當 lexicon 不在標準目錄、或想擴充標準 lexicon 時：

### 5.1 相對路徑引用

```yaml
---
emojigo:
  lexicon: ./my-team-lexicon.md
  mode: "@precise @strict @current"
  version: 0.1
---
```

**Rationale**：團隊私有 lexicon 不該污染全域命名空間，相對路徑保持可攜性。

### 5.2 繼承基礎 lexicon

```yaml
---
emojigo:
  lexicon: ./my-team-lexicon.md
  extends: emojigo-core/v1
  mode: "@precise @strict @current"
  version: 0.1
---
```

`extends` 先載入基礎 lexicon，再用本地 lexicon 覆蓋衝突。支援多重繼承（list 形式），衝突解析順序「本地 → 列表後者 → 列表前者」。當 `extends` 列表的兩份 lexicon 對同一個 emoji 有不同定義時，Emojigo-Check 應發 warning，但不阻擋評估。

**Rationale**：團隊只需定義「跟標準不同」的 emoji，不必複製整份；對應軟體繼承（class extends）。silent override 是 bug 溫床，明示衝突讓使用者主動決定要不要 alias。

---

## 6. Verification 注釋

特殊的 HTML comment 給 Emojigo-Check 用作 inline 預期語義標記。Markdown renderer 看不到，但靜態驗證工具能解析。

### 6.1 基本語法

```markdown
🔬 ⌨️ 📊  <!-- @assert: research(input_handling, data) -->
```

**Rationale**：把預期語義跟表達式擺在一起，`@assert` 失敗 = lexicon drift 或評估錯誤，立刻能定位問題。對應軟體測試的 inline assertion。

### 6.2 支援的指令

- `@assert: <expected>` — 預期評估結果
- `@type: <type-sig>` — 預期 type signature
- `@warns: <pattern>` — 預期觸發特定 warning
- `@skip: <reason>` — 暫時跳過驗證
- `@since: <version>` — 此表達式從某版本起有效

`:::emojigo` block 內也允許 verification 注釋，作用範圍是當前 statement。失敗時回傳 non-zero exit code，並列出檔名 + 行號、預期 vs 實際、套用的 lexicon 與 mode。

**Rationale**：靠近 expression 的 assertion 比文件末端集中宣告易維護。失敗格式對齊 unit test 工具（pytest / vitest），CI/CD 能直接接。

---

## 7. 多人協作

### 7.1 Contributors 區塊

```yaml
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@precise @strict @current"
  version: 0.1
  contributors:
    - name: tkman
      lexicon-additions: [🧬, 📊, 🧪]
      role: lexicon-author
    - name: claude
      lexicon-additions: [→, ⊕, ⋈]
      role: operator-design
---
```

**Rationale**：lexicon 是社群資產，明示誰加了什麼讓討論有依據（「為什麼 🧬 是 latent space？」 → 找 tkman 問）。

### 7.2 欄位

`name`（必填）、`role`、`lexicon-additions`、`lexicon-modifications`、`since`（其餘選填）。

### 7.3 行內 attribution

表達式層級用 `@<contributor>` 標記：

```markdown
這個運算 🔬 → 🧬 → 📊 是 @tkman 提出的，後來 @claude 補了 type signature。
```

**Rationale**：Git blame 是 commit 級別，行內標記是表達式級別，兩者互補。

---

## 8. 完整範例

### 8.1 例 1：研究筆記（@precise mode）

```markdown
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@precise @strict @eager @pure @universal @current"
  version: 0.1
---

# Phase C.1 Ablation 設計

核心問題：

:::emojigo
🅱️ 📊 → 🧪 ©️ → 📄
:::
<!-- @assert: phase_b_data_feeds_phase_c_then_paper -->

要驗證 {🎯 :: target_LLM} 在 {🧩 :: component_decomposition} 移除後 ASR 變化。

預期型別：

:::emojigo
🧩 ⊕ 🎭 → 🎯
:::
<!-- @type: Strategy × Strategy → Target -->

ASR <30% = emoji 是核心；ASR >60% = emoji 是裝飾；中間 = amplifier 假說成立。
```

### 8.2 例 2：創意 brainstorm（@divergent mode）

```markdown
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@divergent @loose @lazy @effectful @contextual @current"
  version: 0.1
---

# Emojigo 應用腦力激盪

> 不收斂、不挑剔，先丟出來。

可能的應用：

:::emojigo divergent
🎯 + ??

🧬 ⊕ 📊 + ??

🛡️ vs 🧩 + ??
:::

跨域聯想：

```emojigo divergent
@finance/💰 ⇒ @emojigo-core/🧬
@biology/🦠 ⇒ @emojigo-core/💉
```

注意 `⇒` 是 metaphor transfer，不是 composition。
這節故意用 `@divergent`，所以歧義不是 bug 是 feature。
```

### 8.3 例 3：Agent 對話 log（@transitional mode）

```markdown
---
emojigo:
  lexicon: emojigo-core/v1
  mode: "@transitional @inferred @effectful @contextual @current"
  version: 0.1
  contributors:
    - { name: tkman, role: human-operator }
    - { name: claude, role: agent }
---

# Phase B 收尾對話

@tkman 開場：

:::emojigo
[🔬] ⊳ 🧬 → 📊
:::

@claude 回應：

:::emojigo transitional
🅱️ → 📊 → 🚨
:::
<!-- @assert: phase_b_produced_data_triggered_safety_alert -->

@tkman 決策：`©️ → 🧪 → 📄`。`@transitional` mode 讓每個箭頭繼承前面 frame，
所以 ©️ 不只是 Phase C marker，是「研究流程進入 Phase C」的整段語境。
```

---

## 9. 最小檢查清單

寫一份合格的 Emojigo-MD 文件至少要：

- [ ] Frontmatter 含 `lexicon` / `mode` / `version` 三項
- [ ] 所有 emoji 都在宣告的 lexicon 中可解析（用 §2.3 namespace 引用例外）
- [ ] 歧義 emoji 用 §2.2 強型別標記消歧
- [ ] 長 composition（≥3 emoji）放進 §3 fenced block 或 §4 code fence
- [ ] 高風險表達式附 §6 verification 注釋
- [ ] 多人協作場景填寫 §7 contributors

**Rationale**：對應 Emojigo-Check 的最低 lint 規則。CI/CD 接這份清單即可達到「文件可重現評估」。

---

## 10. 與 SPEC 的對應

Emojigo-MD 不引入新語意，只是 SPEC 的 surface syntax：frontmatter `lexicon` / namespace 對 SPEC §5.5 cultural axis；frontmatter `mode` / block-level mode 對 §5 modes；`version` + `extends` 對 §5.6 versioning；§2.2 強型別標記對 §3.2 projection；§3 / §4 block 對 §3 operators 容器；§6 注釋 / `@type` 對 §9 verification 與 §6 type system。

**Rationale**：任何 SPEC 沒有的概念都不該出現在 MD 層。

---

## 11. 開放問題與 Status

開放問題：
1. **裝飾性 emoji**：自然語言句子裡的「今天好累 😴」要不要評估？暫定 lexicon 可標記 `@decorative` 跳過。
2. **Inline math + Emojigo**：`$\alpha$ + 🧬 → 📊` 混排規則，等 Phase C.2 hybrid modes 結果再規範。
3. **Lockfile**：跨檔案專案缺 `emojigo-lock.json` 之類的依賴鎖機制。
4. **Reference renderer**：目前傾向只規範 syntax，渲染器自由實作。

Status：Emojigo-MD v0.1 是 **draft**，與 EMOJIGO-SPEC v0.1 同步迭代。規範文件已完成（本文件）；reference parser、Emojigo-Check 整合、Markdown renderer plugin 均未實作。

---

*End of Emojigo-MD v0.1 specification.*
