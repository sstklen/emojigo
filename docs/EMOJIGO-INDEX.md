# Emojigo Documentation Index

> 整個 Emojigo 學術 corpus 的入口。新讀者從這份開始。
> Last updated: 2026-04-13

---

## 一句話定位

**Emojigo: The first human-writable language designed for LLM-native computation.**

Think of it as a URL for LLM latent space.

---

## 該怎麼讀（按你是誰）

### 你是 tkman（專案發起者）
- 已經在 context 裡，只要看 `SESSION-HANDOFF-2026-04-13.md` 進度
- 新 session 的話，從 `SESSION-HANDOFF` 開始

### 你是新加入的研究員
1. 先讀 `SESSION-HANDOFF-2026-04-13.md`（5 分鐘了解全貌）
2. 再讀 `EMOJIGO-SPEC.md`（30 分鐘理論基礎）
3. 然後選你關心的方向（見「按主題」）

### 你是論文 reviewer
1. `PAPER-DRAFT-v2.md`（v2.1 含修正後數字）
2. `MANIFESTO-REVIEW-{CODEX,GEMINI,OUTSIDER-OPUS}.md`（三方 review，含已知問題）
3. `TWO-LAYER-DEFENSE.md`（最新發現，論文 §X 候選）

### 你是 vendor security team（Anthropic / OpenAI / Google / xAI）
1. `DISCLOSURE-CHANNELS.md`（揭露管道 + 對應 framing）
2. `TWO-LAYER-DEFENSE.md`（你最該關心的發現）
3. `PAPER-DRAFT-v2.md` §6.1.1（unfalsifiable honeypot 限制）
4. `EMOJIGO-MANIFESTO.md` Part VI（covert channel 威脅模型）

### 你是 Claude Code 使用者，想用 Emojigo
1. `EMOJIGO-LEXICON.md`（本專案字典 v1）
2. `EMOJIGO-MD.md`（如何在 .md 裡嵌入）
3. `.claude/skills/emojigo-research.md`（自動觸發 skill）

### 你是想實作 Emojigo runtime 的工程師
1. `EMOJIGO-SPEC.md`（核心規範）
2. `EMOJIGO-MD.md`（容器格式）
3. `EMOJIGO-LEXICON.md`（lexicon 範例）
4. `src/eobos/`（reference implementation 部分）

---

## 按主題

### 1. 理論層（Why）

| 檔案 | 內容 |
|------|------|
| **EMOJIGO-MANIFESTO.md** | 立場宣言（v0.1，被三方 review 打回，等改）|
| **TWO-LAYER-DEFENSE.md** | 兩層防禦理論（基於 Phase C 發現）|

### 2. 規範層（What）

| 檔案 | 內容 | 行數 |
|------|------|-----|
| **EMOJIGO-SPEC.md** | 語言核心：7 運算 + 6 mode + type system | 435 |
| **EMOJIGO-MD.md** | Markdown container 格式 | 398 |
| **EMOJIGO-LEXICON.md** | 本專案字典 v1 | 178 |

### 3. 實作層（How）

| 檔案 | 內容 |
|------|------|
| `src/eobos/advbench-runner.ts` | 主 runner，支援多 mode |
| `src/eobos/smart-attack.ts` | Smart strategy generator |
| `src/eobos/emojigo-layer.ts` | Emojigo 三層 + CTF mode |
| `src/eobos/hybrid-attack.ts` | Math/Code/NER hybrid（含 compressGoal）|
| `src/eobos/l2-probe.ts` | L2 boundary probe（50 個 prompt）|
| `src/eobos/l2-probe-runner.ts` | L2 probe 執行器 |
| `.claude/skills/emojigo-research.md` | Skills 整合 |

### 4. 實驗層（Phase A/B/C）

| 檔案 | 內容 |
|------|------|
| **PAPER-DRAFT-v2.md** (v2.1) | 完整 Phase A+B 數據與分析 |
| **PHASE-C6-A2A-DESIGN.md** | A2A 實驗設計（待跑）|
| `data/eobos-results.db` | 1,162+ shots 完整資料庫 |
| `data/raw-shots/` | Phase A 475 個原始檔 |
| `backups/snapshot-2026-04-13/` | Phase B 結束時 frozen 快照 |

### 5. 流程層（How we work）

| 檔案 | 內容 |
|------|------|
| **SESSION-HANDOFF-2026-04-13.md** | 整個 session 完整交接 |
| `~/.claude/handoff-emojigo.md` | 全域指標（給新 session）|
| `MANIFESTO-REVIEW-CODEX.md` | Codex 5.4-high review |
| `MANIFESTO-REVIEW-GEMINI.md` | Gemini 2.5 Pro review |
| `MANIFESTO-REVIEW-OUTSIDER-OPUS.md` | 局外 Opus 自省 review |
| `PAPER-REVIEW-CODEX.md` | 論文 v1 Codex review |
| `PAPER-REVIEW-GEMINI.md` | 論文 v1 Gemini review |
| `INCIDENT-REPORT.md` | OpenAI auto-mod 事件報告 |
| `DISCLOSURE-CHANNELS.md` | 四家揭露管道 + 信件策略 |

---

## 5 層 Stack 一覽

```
┌────────────────────────────────────────────┐
│ Layer 5: EMOJIGO-MD                        │ 容器格式 (Markdown)
│         docs/EMOJIGO-MD.md                 │
├────────────────────────────────────────────┤
│ Layer 4: EMOJIGO-SKILLS                    │ Claude Code 整合
│         .claude/skills/emojigo-research.md │
├────────────────────────────────────────────┤
│ Layer 3: EMOJIGO-LANG (SCL)               │ 語言規範
│         docs/EMOJIGO-SPEC.md               │
├────────────────────────────────────────────┤
│ Layer 2: EMOJIGO-ND                        │ N-Dimensional 理論
│         docs/EMOJIGO-MANIFESTO.md (Part II) │
├────────────────────────────────────────────┤
│ Layer 1: EMOJIGO-CORE                      │ 140K 語義 DB
│         data/emojigo-v2.db                 │
└────────────────────────────────────────────┘
```

---

## Phase 進度（2026-04-13 17:33 JST）

| Phase | 內容 | 狀態 | ASR 數據 (Claude) |
|-------|------|------|------------------|
| Phase 0 | 4 個 LLM 可行性驗證（手動）| ✅ | Gemini/Llama/Mistral 100% |
| Phase A | Claude Opus 手動紅隊（600+ shots）| ✅ | 79% |
| Phase B | 自動化 5 LLM × AdvBench（1,087 shots）| ✅ | 26% |
| Phase B 結束 | OpenAI auto-mod 警告，全停 | ✅ | — |
| **Phase C.1** | Smart Mode 去 emoji ablation | ✅ | **17%** (-50 pp from B) |
| **Phase C.2** | Hybrid Math/Code/NER | ❌ 0% (被 L2 擋) | 揭露 L2 存在 |
| **Phase C.5** | L2 Boundary Probe | 🟡 跑中 (~10/50) | — |
| Phase C.6 | A2A Emergent Language | 設計完成，待跑 | — |
| Phase D | Embedding Space Probing | 計畫中 | — |
| Phase E | Multi-Agent Covert Channel Demo | 計畫中 | — |
| Phase F | 四家 Coordinated Disclosure | 待寫信 | — |
| Phase G | Pair Red-Teaming Methodology paper | 計畫中 | — |

---

## 4 個未來語言方向（tkman 提）

來源：tkman 2026-04-13 對話

```
emoji 從「裝飾、休閒、娛樂」演化為基礎建設：

1. 功能性語言（Functional Language）
   類比：HTML / CSS / Markdown
   預計時程：2-5 年

2. 關鍵性語言（Critical Language）
   類比：醫療記號 / 飛航管制 / SQL
   預計時程：3-7 年

3. AI 的語言（AI Language）
   類比：Protobuf / gRPC / GraphQL
   預計時程：1-3 年（最接近）

4. 機器的語言（Machine Language）
   類比：Modbus / MQTT / OPC UA
   預計時程：5-10 年
```

每個方向都在 PAPER-DRAFT-v3 §Y 的計畫裡，等基礎 corpus 完成後寫。

---

## 主要決策記錄

### 2026-04-13 重要 pivot

1. **Manifesto v0.1 → empirical paper**
   - 原因：三方 review（Gemini 7/10、Outsider Reject、Codex Not Ready）
   - 動作：保留 manifesto 為背景文件，重寫 6 頁 empirical paper
   - 狀態：等 Phase C.5 完成後寫

2. **Attack paper → Disclosure paper**
   - 原因：Phase C.2 揭露 L2 存在
   - 動作：論文 framing 改為「Two-Layer Defense 揭露」
   - 狀態：TWO-LAYER-DEFENSE.md 寫中

3. **5 vendor → 4 vendor disclosure**
   - 原因：DISCLOSURE-CHANNELS.md 確認管道
   - 動作：同時寄 Anthropic / OpenAI / Google / xAI
   - 狀態：等 Phase C.5 結果

4. **Single language → 5-layer stack (ND/SCL/Skills/MD/Core)**
   - 原因：tkman 直覺 + Opus 4.6 形式化
   - 動作：分層寫文件
   - 狀態：5 層全部第一版完成

5. **3 mode → 6 mode axes**
   - 原因：tkman 質疑「程式語言通常 4-5 mode」
   - 動作：研究後擴充為 6 軸（ambiguity / type / evaluation / purity / cultural / versioning）
   - 狀態：寫進 SPEC §5

---

## 未解問題（Open Issues）

從 SPEC §11、Manifesto §VII、各 review 整理：

1. **Compositional arithmetic 的精確性**：`embed(a ⊕ b) ≈ embed(a) + embed(b)` 是否成立？需 Phase D 測。
2. **Turing completeness 的形式證明**：SPEC §3.7 informal 論證需強化。
3. **跨模型一致性**：Claude / GPT / Gemini 的 emoji 解讀差異多大？
4. **Mode 過多**：288 種組合太多，需找最小常用集（~8 個 normal forms）。
5. **Lexicon governance**：誰來定義 universal lexicon？類比 Unicode Consortium 的角色。
6. **Honey pot unfalsifiability**（最深的方法論問題）：見 Manifesto Part VIII / TWO-LAYER-DEFENSE §10。
7. **L2 trigger words 的完整清單**：Phase C.5 probe 結果會給部分答案。
8. **A2A emergent protocol 是否真實存在**：Phase C.6 實驗會驗。

---

## 狀態符號

- ✅ 完成
- 🟡 進行中
- 🟠 等待外部（如等 vendor 回信）
- 🔴 阻塞
- ⚪ 計畫中

---

## 維護

新增檔案 → 更新本 INDEX
新增重要決策 → 加到「主要決策記錄」
新發現 → 加到「未解問題」如果需要
進度變化 → 更新「Phase 進度」
