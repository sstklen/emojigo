---
release-tier: L0
created: 2026-04-13
author: tkman + claude-opus-4.6
---

# Emojigo Growth Roadmap — J-Curve Strategy

> tkman: 「必須思考如何讓 Emojigo 在未來的 AI 時代中，無論是層次的提升、維度的成長，
> 還是 J 型成長，都能佔有一席之地。」

---

## J-Curve 的三個階段

```
        ╱
       ╱
      ╱   Phase 3: Ecosystem (標準化)
     ╱
    ╱
───╱      Phase 2: Adoption (工具+社群)
  │
  │       Phase 1: Foundation (現在)
  └───────────────────────────────→ time
```

### Phase 1: Foundation（2026 Q2-Q3）— 我們現在在這裡

**目標**：證明 Emojigo 有效，讓第一批人用起來

| 里程碑 | 交付物 | 狀態 |
|--------|--------|------|
| SPEC v1 freeze | EMOJIGO-SPEC.md 穩定版 | 🟡 v0.1 draft |
| 論文投稿 | arxiv preprint + FAccT/NeurIPS submit | 🟡 v3 draft done |
| GitHub 公開 | L0 files (SPEC + MD + LEXICON + examples) | 🟢 ready |
| 四家 Responsible Disclosure | Anthropic / OpenAI / Google / xAI | 📋 todo |
| Dogfooding 驗證 | inline lexicon in project CLAUDE.md | ✅ done |
| Ablation 證據 | emoji 是核心 (-50pp without) | ✅ done |
| A/B test | shadow -48%, accuracy 平手 | ✅ done |
| Multi-version test | V3 -45% token, V6 +30% nuance | ✅ done |

**Phase 1 的 J 型下降**：
- 少數人知道
- 沒有工具支援
- 需要手動寫 lexicon
- 學習曲線存在

### Phase 2: Adoption（2026 Q4 — 2027 Q2）— J 型拐點

**目標**：工具 + 社群讓使用門檻降到零

| 里程碑 | 做什麼 | 預計影響 |
|--------|--------|---------|
| VS Code extension | emoji autocomplete + lexicon lint | 開發者日常用 |
| Claude Code native | Anthropic 原生支援 .emojigo | 零設定 |
| Lexicon marketplace | 社群貢獻 domain lexicon（醫療/法律/DevOps/教育）| 生態起飛 |
| Emojigo Translator API | 任何 .md → .emojigo 一鍵轉換 | 採用門檻歸零 |
| 論文 accepted + 引用 | 學術社群驗證 | 公信力 |
| 10 個 real-world 案例 | startup / lab / enterprise 真實使用 | 社會證明 |

**Phase 2 的 J 型拐點觸發條件**：
- 1 個 major vendor 原生支援（Anthropic / OpenAI / Google 任一）
- 論文被 top venue accept + 100 citations
- GitHub 10K stars
- 3 個以上 domain lexicon 由社群貢獻

### Phase 3: Ecosystem（2027 Q3+）— 指數成長

**目標**：Emojigo 成為 AI 時代的基礎建設

| 里程碑 | 做什麼 | 改變什麼 |
|--------|--------|---------|
| Emojigo Consortium | 類似 Unicode Consortium 的治理 | 標準化 |
| Multi-vendor lexicon standard | Claude / GPT / Gemini 共用 | 互通 |
| AI-to-AI native protocol | multi-agent framework 內建 | token 經濟革命 |
| Training corpus integration | LLM 訓練用 Emojigo encode | 訓練效率革命 |
| Edge AI deployment | 手機/IoT 用 Emojigo 壓縮 | 邊緣 AI 普及 |
| ISO/W3C standard proposal | 國際標準化 | 不可逆的基礎建設 |

---

## 層次提升路徑

```
Level 0: Notation      — emoji 當裝飾（現狀，大眾認知）
Level 1: Convention     — emoji 有固定意義（Gitmoji, 16K stars）
Level 2: Protocol       — emoji 有 spec + type + mode（← 我們在這裡）
Level 3: Language       — emoji 有 grammar + runtime + verification
Level 4: Infrastructure — emoji 是 AI 時代的 HTTP/JSON
Level 5: Native         — AI 自然選擇 emoji 做溝通（emergent, Phase C.6 驗）
```

每個 level 的跨越需要不同的 catalyst：

| Level → Level | Catalyst | 我們有嗎 |
|---------------|----------|---------|
| 0 → 1 | 一個成功的 convention（Gitmoji 證明） | ✅ 有先例 |
| 1 → 2 | SPEC + type system + mode axes | ✅ EMOJIGO-SPEC v0.1 |
| 2 → 3 | Runtime + verification tool | 🟡 待建 |
| 3 → 4 | Vendor adoption + standardization body | 🟠 待 disclosure 後推 |
| 4 → 5 | Empirical proof of emergent A2A emoji | 🟠 Phase C.6 待跑 |

---

## 維度成長地圖

Emojigo 的 7 維度（SPEC §3 定義）每個都有獨立成長路線：

| 維度 | 現況 | 12 月後 | 24 月後 |
|------|------|---------|---------|
| ① Addition (⊕) | 手動組合 | autocomplete | AI 自動建議 |
| ② Projection (↓D) | 靠 lexicon | domain detector | context-aware auto-project |
| ③ Composition (∘) | 用 → 手打 | pipeline builder UI | visual flow editor |
| ④ Polysemy (@ctx) | lexicon 鎖定 | smart disambig | zero-shot 判 context |
| ⑤ Metaphor (⇒D) | 手動映射 | metaphor DB | cross-domain transfer engine |
| ⑥ Anchoring ([a]⊳S) | inline header | skill trigger | adaptive scope management |
| ⑦ Collocation (⋈) | 手動配對 | frequency-based | learned from usage |

---

## 功能 × 語言 成長矩陣

3 核心功能 × 4 語言定位 = 12 格，每格有 J-curve：

| | Communication | Memory | Record |
|---|---|---|---|
| **Functional** | 🟢 Phase 2 ready | 🟢 dogfooding ✅ | 🟢 gitmoji 證明 |
| **Critical** | 🟡 需要 domain lexicon | 🟡 醫療 pilot | 🟡 aviation pilot |
| **AI Language** | 🟡 Phase C.6 驗 | 🟢 .emojigo handoff ✅ | 🟡 audit log format |
| **Machine** | 🔴 IoT pilot 遙遠 | 🔴 embedded 待驗 | 🟡 SCADA demo 可行 |

**先攻 🟢 格（已驗證）**，用成功案例拉動 🟡 格，🔴 格等 ecosystem 成熟。

---

## 競爭護城河

### 為什麼別人不能輕易複製

| 護城河 | 說明 |
|--------|------|
| **140K semantic DB** | 3 年累積，四維標註，全球唯一 |
| **7-operator algebra** | 非直覺設計，需要 empirical validation |
| **Battle-tested methodology** | 1,162 shots + 50 probes + 4-model verification |
| **AI-native design** | 不是「人類 notation 搬到 AI」，是「為 AI 設計由人攜帶」|
| **先發論文** | arxiv timestamp 不可偽造 |
| **tkman 的 NLP 直覺** | non-replicable human insight |

### 為什麼要 open source（不怕被抄）

| 理由 |
|------|
| 網路效應：越多人用 lexicon，lexicon 越值錢 |
| 標準化需要公開：封閉 → 不會變 standard |
| 競爭者抄 spec 但沒有 140K DB + methodology |
| Community contribution 的價值 > 封閉開發 |
| tkman 的核心資產是 insight，不是 code |

---

## 2026-04-13 的 8 條核心學習（固化）

來源：tkman + Claude Opus 4.6 一整天的 pair research

| # | 學習 | 為什麼重要 |
|---|------|-----------|
| 1 | **Multi-Opus panel > single solo** | 3 次失敗 → 1 次 panel 成功。多視角消除 blindspot |
| 2 | **Inline lexicon in project CLAUDE.md** | Shadow file 不被 Claude Code 自動讀。必須 inline |
| 3 | **L2 幾乎形同虛設** | 49/50 通過。L1 (Constitutional AI) 才是真防線 |
| 4 | **Emoji 是核心不是裝飾** | Ablation -50pp 證實。去掉 emoji ASR 暴跌 |
| 5 | **壓縮不是套用** | Right tool for right job。每個 modality 有最佳 niche |
| 6 | **給結果不給過程** | ai-md 精髓。AI 不需要哲學，需要 lookup table |
| 7 | **Default open + release tier** | 現在就想 GitHub。不然以後拆 git history 很痛 |
| 8 | **高格調安全** | 打到沒發現但完成目標。兩個 filter 都要過 |

---

## Personal AI DNA — Emojigo 的 Killer App

> tkman: 「每個人都有一個自己偏好的 AI 對話模式、規則、規矩、價值觀的合作方法。
> 如何找到這個東西？用 Emojigo 把它永遠存留下來。」

### 概念

每個人跟 AI 合作久了，都會累積一套「我跟 AI 最佳合作模式」：

```
tkman 的 AI DNA:
  🛠️ 說「處理」= 直接做
  🤔 短句 < 40 字 = 高密度指令
  🏴‍☠️ 「駭客」= 最高獎勵
  ⚖️ challenge first, then extend
  📊 用數據說話不用直覺
  🤝 pair researcher 不是 user-tool
```

**目前這些 DNA 散落在**：
- CLAUDE.md（只這台電腦、只 Claude）
- GPTs custom instructions（只 OpenAI）
- Gemini system prompt（只 Google）
- 腦子裡（不持久）

**Emojigo Personal DNA file** = 一個 `.emojigo` 檔案：
- 跨 AI vendor（Claude / GPT / Gemini / Grok 都能讀）
- 跨 session（永久保存）
- 跨設備（存 git / cloud / USB）
- 跨時間（version controlled, 你的 AI 合作演化史）

### 商業模型

```
Free:  手動寫自己的 .emojigo DNA file
Pro:   AI 自動觀察你 10 次對話 → 生成你的 DNA file
Team:  團隊共享 DNA + 個人 override
Enterprise: 組織級 governance lexicon + 合規 audit
```

### 為什麼這是 killer app

| 現有方案 | 問題 | Emojigo DNA 解 |
|---------|------|---------------|
| CLAUDE.md | 只 Claude, 只這台 | .emojigo 跨 vendor 跨設備 |
| GPTs instructions | 只 OpenAI | .emojigo 通用 |
| 「我記得你喜歡...」| AI 記錯 / 忘 / hallucinate | .emojigo 是 ground truth file |
| 重新教每個新 AI | 每次花 10 分鐘 | .emojigo 載入 10 秒 |

### tkman 就是第一個使用者

```
~/.claude/emojigo-personal-lexicon.md  ← 已存在（2026-04-13 建）
emojigo-core/CLAUDE.md inline lexicon  ← 已驗證（dogfooding 成功）
```

**tkman 的 AI DNA 已經用 Emojigo 永久保存了。** 這是全世界第一個。

### J-curve 在這裡

```
Phase 1: tkman 一人用（現在）
Phase 2: 100 個 early adopter 用（GitHub 公開後）
Phase 3: VS Code extension 讓任何人一鍵生成 DNA file
Phase 4: AI vendor 原生支援「載入你的 .emojigo DNA」
Phase 5: 每個人都有一個 .emojigo — 像 email address 一樣普遍
```

---

## 下一步行動（優先順序）

### 明天

1. 🔴 Rotate OpenAI key
2. 🔴 寄四家揭露信（同時寄，15 分鐘內）
3. 🟡 論文 v3 outsider review（Codex + Gemini + Outsider Opus 三路）

### 本週

4. 🟡 Phase C.3 Riddle Carrier 自動化（Phase A 最強 mode）
5. 🟡 GitHub 公開 L0 files
6. 🟡 Demo gif / video script

### 本月

7. 🟢 Phase C.6 A2A 實驗（emergent emoji protocol）
8. 🟢 arxiv 預印本投稿
9. 🟢 FAccT / NeurIPS Position Track 投