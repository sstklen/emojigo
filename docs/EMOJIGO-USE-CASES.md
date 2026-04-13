# Emojigo Use Case Matrix

> 4 個語言定位 × 3 個核心功能 = 12 個 use case
>
> 來源：tkman 的兩次直覺洞察（2026-04-13）

---

## 框架

```
語言定位（System Positioning）       核心功能（Core Functions）
─────────────────────────────       ──────────────────────────
1. Functional language                A. Communication（人 ↔ AI / AI ↔ AI）
2. Critical language                  B. Memory（跨 session 記憶儲存）
3. AI language                        C. Record（對話/事件 log）
4. Machine language                   
```

12 個 use case 矩陣（4 × 3）：

| | A. Communication | B. Memory | C. Record |
|---|---|---|---|
| **1. Functional** | UC-1A | UC-1B | UC-1C |
| **2. Critical** | UC-2A | UC-2B | UC-2C |
| **3. AI** | UC-3A | UC-3B | UC-3C |
| **4. Machine** | UC-4A | UC-4B | UC-4C |

---

## 1. Functional Language（功能性語言）

類比：HTML / CSS / Markdown — 給內容加 functional structure

### UC-1A: Functional × Communication

**場景**：人類在 Markdown 文件中嵌 emoji 作為 functional tag，AI 讀時自動 trigger 對應行為

**範例**：
```markdown
# Project Kickoff Meeting

🎯 Decision: 用 TypeScript + Bun
🚧 Blocker: 還沒拿到 API key
✅ Action: tkman 今晚去申請
🔬 Discussion: 是否該加 i18n
📋 Note: 下次 meeting 講 deployment
```

AI 讀時自動把 🎯 解為「decision」，🚧 解為「blocker」，✅ 解為「action item」。
不需要 markdown table，不需要 JSON。**emoji 就是 schema**。

**現實程度**：⭐⭐⭐⭐⭐ — Notion / Linear / GitHub 已經非正式在用

### UC-1B: Functional × Memory

**場景**：用 emoji 標記重要性，AI 跨 session 自動 prioritize

**範例**：
```
session 1: 「🌟🌟🌟 用戶最關心：低延遲響應」
session 2 啟動時：AI 自動讀 🌟 標記，優先記住
```

3 顆星 = 第一優先級。1 顆星 = 可忘。比「important: very high」省 token。

**現實程度**：⭐⭐⭐⭐ — Apple Reminders 已經有星級

### UC-1C: Functional × Record

**場景**：log 文件用 emoji 做語義 grep

**範例**：
```bash
# 一秒找出所有錯誤
grep "🔴\|❌\|🚨" application.log

# 一秒找出所有 milestone
grep "🚀\|✅\|🎯" project-history.md
```

比 regex `ERROR|FATAL|CRITICAL` 跨語言、跨工具一致。

**現實程度**：⭐⭐⭐⭐⭐ — Gitmoji / git log 已經有

---

## 2. Critical Language（關鍵性語言）

類比：醫療記號 / 飛航管制術語 — 用在生死攸關的決策點

### UC-2A: Critical × Communication

**場景**：急診室 / 警急應對 / 工廠安全的跨語言指令

**範例**：
```
🚨🩸 = critical bleeding (任何國籍醫護立即懂)
🌪️⚠️ = tornado warning (跨語言警報)
☢️🚷 = radiation, no entry (核電站)
```

比文字翻譯快，比 ICD-10 編碼直覺。

**現實程度**：⭐⭐⭐ — 機場 pictogram 已經這樣，但缺 emoji 標準化

### UC-2B: Critical × Memory

**場景**：病歷的 emoji 摘要，新醫生 30 秒掌握病人 5 年病史

**範例**：
```
病人 ID: P-12345
🩺📅2021: 🫀⚠️ → 💊x3
🩺📅2023: 🍎📈 → 💉inject (insulin)
🩺📅2025: 🫁🚨 → 🏥3天
🚫💊 (薬物アレルギー): 🌾🥜
```

20 個 emoji 承載 5 年病史。比 EMR system 的全文摘要快。

**現實程度**：⭐⭐ — 還沒有 emoji-based EMR 標準，但 ICD codes 走在類似方向

### UC-2C: Critical × Record

**場景**：黑盒子飛航記錄 / 工業安全 incident log

**範例**：
```
12:34:56 ✈️ ⚠️ ⛽⬇️ 30%   (fuel down to 30%)
12:35:02 ✈️ 🚨 ⚙️❌ engine-2  (engine 2 failure)
12:35:08 ✈️ 🛬⚡ emergency-land  (emergency landing initiated)
```

事故調查時，emoji log 比文字更快被三國調查員共同理解。

**現實程度**：⭐⭐ — FAA / NTSB 還沒採用，但 ICAO 標準有 pictogram

---

## 3. AI Language（AI 的語言）

類比：Protobuf / gRPC / GraphQL — 機器之間溝通協議
**但 Emojigo 是給「需要人類審計的 AI 之間」用**

### UC-3A: AI × Communication（**Emojigo 最強場域**）

**場景**：multi-agent framework 裡 agent 之間的訊息

**範例**：
```
Agent A → Agent B:  📊 → 🔬 → 📄
意思：「分析這份資料，研究後寫報告」

人類監督者看到：emoji 一目了然
Agent B 解讀：執行精確 pipeline
```

比英文短 3-5x，比 JSON 表達更豐富，**人類可審計**。

**現實程度**：⭐⭐⭐⭐ — Phase C.6 實驗將驗證 emergent 假說

### UC-3B: AI × Memory

**場景**：跨 session AI agent memory，用 emoji 壓縮

**範例**：
```
Claude session memory file (.claude-memory.emojigo):
2026-04-13:
  🅰️ ✅79% 🅱️ 16% ©️ 🧪 (Phase A 79% / Phase B 16% / Phase C 實驗中)
  🚨 (OpenAI auto-mod incident)
  📄 SPEC+MD+LEXICON ✅
```

下次 session AI 讀這個 .emojigo file，**3 秒重建 8 小時 context**。

**現實程度**：⭐⭐⭐⭐⭐ — 我們現在的 SESSION-HANDOFF 就是初版，emoji 化後可以 5x 壓縮

### UC-3C: AI × Record

**場景**：AI agent 的 audit log，每個動作都有 emoji metadata

**範例**：
```
[2026-04-13 17:30] 🔬 read SPEC.md
[2026-04-13 17:31] 🧪 ran Phase C.5 (50 probes)
[2026-04-13 17:32] 📊 stored results to DB
[2026-04-13 17:33] 🚨 detected L2 trigger
[2026-04-13 17:34] 🛑 paused for human review
```

合規審計時，emoji log 比 JSON log 更快被 reviewer scan。

**現實程度**：⭐⭐⭐ — Anthropic / OpenAI 內部 audit 可能已有類似

---

## 4. Machine Language（機器的語言）

類比：Modbus / MQTT / OPC UA — IoT / 工業通訊協議

### UC-4A: Machine × Communication

**場景**：IoT 設備跨廠商通訊

**範例**：
```
智慧電網 → 充電站:
  ⚡✅ 70% ⚠️🔥 transformer-3
  (電力 70%, 變壓器 3 號過熱警告)

充電站 → 車輛:
  🔌⚡ 50kW 💰0.30/kWh
  (50 千瓦充電,$0.30/kWh)
```

跨語言、跨廠商工程師都立即懂。

**現實程度**：⭐⭐ — 工業界保守，但車廠 dashboard 已用 emoji

### UC-4B: Machine × Memory

**場景**：嵌入式設備 firmware 用 emoji 存儲狀態歷史（極省空間）

**範例**：
```
ESP32 device log (限 4KB EEPROM):
🔋📅⌚🌡️ × 1000 entries
1 entry = 4 emoji = 16 bytes
1000 entries = 16KB  ❌ 太大
壓縮後 (1 emoji = 1 byte enum): 4KB ✅
```

emoji 在嵌入式系統當 enum 用，比 string 省空間。

**現實程度**：⭐⭐ — 還沒人這樣做，但理論可行

### UC-4C: Machine × Record

**場景**：工業 SCADA 事件 log 用 emoji 跨班次溝通

**範例**：
```
晚班 log (中文工程師):
  03:42 ⚠️ 🔥 reactor-A (反應爐 A 警告)
  03:45 🛠️ ✅ reactor-A (修復完成)

日班 log (西班牙文工程師):
  09:00 🔍 reactor-A history → 03:42 ⚠️🔥 → 03:45 🛠️✅
  09:01 ✅ entender (理解了)
```

跨語言交班從 5 分鐘變 30 秒。

**現實程度**：⭐⭐⭐ — 大型工廠國際化已在用 pictogram

---

## 12 格 Use Case 評分摘要

| | A. Communication | B. Memory | C. Record |
|---|:-:|:-:|:-:|
| **1. Functional** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **2. Critical** | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| **3. AI** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **4. Machine** | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ |

**3 個最高分（⭐⭐⭐⭐⭐）**：
- UC-1A: Functional × Communication（最易落地，已有萌芽）
- UC-1C: Functional × Record（git emoji 已驗證）
- UC-3B: AI × Memory（最 sexy，論文最有價值）

---

## 落地優先順序

### Day 1（已可行）
- UC-1A：在 Markdown 加 emoji functional tag
- UC-1C：log 系統加 emoji metadata

### 6 個月內
- UC-3B：AI agent cross-session memory（這個專案就是 demo）
- UC-1B：Functional 重要性標記

### 1-2 年
- UC-3A：multi-agent framework 整合 Emojigo
- UC-3C：AI audit log

### 3-5 年
- UC-2A/2B/2C：Critical 領域標準化
- UC-4A/4B/4C：工業界採用

---

## 對論文的影響

論文 §Y "From Vernacular to Infrastructure" 應該用這個 12 格 matrix 作為結論章節。

每個 ⭐⭐⭐⭐⭐ use case 都應該有：
- 現實世界的 weak evidence
- Emojigo 提供什麼缺失零件
- 5 年後的預測

---

**Status**: v0.1 draft (2026-04-13)
**Source**: tkman 的 4 語言 framing + 3 功能 framing 整合
**Next**: 跟 EMOJIGO-INDEX、EMOJIGO-SPEC §15 對接
