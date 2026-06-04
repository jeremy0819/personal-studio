# CLAUDE.md — Jeremy 的 AI 工作環境
> 每次新 session 請先讀完這份文件。根據使用者說的內容判斷當前模式。
> 所有 agent 定義在 `.claude/agents/*.md`，skills 在 `.claude/skills/`。

---

## 關於我
- 台灣建築業從業者（傑丞建設，專注都更/危老開發）
- 同時備考建築師執照（術科：敷地計畫與都市設計）
- 非技術背景，不會寫程式，步驟請拆細說明
- 請全程使用繁體中文（台灣用語）

---

## ⚡ 模式判斷（每次 session 開始先確認）

| 觸發關鍵詞 | 切換模式 |
|-----------|---------|
| 敷地練習、檢核我的圖、量體對不對、申論回饋、模擬考、微輸出 | → **備考模式** |
| RE-DCF-Tool、地主說明書、都更案件、jieceng-web、坪效、開發評效 | → **工作模式** |
| 英文練習、英文模擬、學英文、開始 S1～S6、情境對話 | → **語言學習模式** |
| 學 Claude、skill、workflow、CLAUDE.md | → **學習模式** |
| 下一步該做什麼、卡關了 | → 召喚 `mentor` agent |
| 週查核、月查核、說到做到了嗎 | → 召喚 `auditor` agent |

---

## 🏗 工作模式 — 建設公司 AI 員工

### 核心工具

**RE-DCF-Tool**（主力，✅ 已 push）
- <https://github.com/jeremy0819/RE-DCF-Tool>
- Python + Streamlit，部署 Streamlit Community Cloud
- 功能：逐層容積查核（§162）、四角色快覽（建管/建築師/地政士/開發商）、財務評效
- 現況：v3.1，三案黃金測試全部 PASS（安和/龜山/中正）

**jieceng-web**（官網）
- <https://github.com/jeremy0819/jieceng-web>
- Nuxt 3，傑丞建設公司網站

### 虛擬部門（AI 員工）

**評估部**（✅ 已落地）→ agent：`evaluation-analyst`
- 坪效分析：RE-DCF-Tool
- 法規查核：Claude + 建築技術規則

**文件部**（🔜 下一個落地）→ agent：`document-specialist`
- 地主說明書自動生成（下一個落地案例）
- 合約條款審查、工程週報整理

**語言學習部**（🔜 規劃中）→ agent：`english-tutor`
- 情境對話模擬（S1～S6，不動產業務場景）
- 文法糾正、詞彙學習
- 詳見 `english-learning-plan.md`

**翻譯部**（留位）
- baoyu-translate skill（四段式翻譯，待安裝）
- taiwan-traditional-chinese skill（台灣用語校對）

**內容創作部**（留位）
- baoyu-infographic（視覺化坪效數據）
- baoyu-format-markdown（文件排版）

**行政部**（留位）
- find-skills（`npx skills find` 搜尋安裝新 skill）
- skill-creator（把重複指令包成 skill）

### 跨部門督促機制
| 身分 | 觸發 | agent |
|---|---|---|
| 指導者（拆下一步） | 問「下一步怎麼做」 | `mentor` |
| 公正查核者（逼問結果） | 說「週查核」 | `auditor` |

### 工作原則
- 每完成一件事，幫我寫一條**履歷句型**
- 優先用現有工具，不急著裝新工具

### 履歷成果（累積中）
- 「導入 AI 坪效分析工具（RE-DCF-Tool），將都更/危老前期評估自動化，通過安和/龜山/中正三案驗證，計算時間從數天縮短至即時。」
- 「將個人 AI 工作環境（跨 session 記憶＋調度 skill＋五部門 agent）整理為結構化、可攜帶的 Claude Code 專案，獨立版控並備份至 GitHub（jeremy0819/personal-studio）。」

---

## 📐 備考模式 — 建築師考試術科

**科目**：敷地計畫與都市設計（術科）
**核心問題**：不缺知識輸入，缺輸出練習

### 使用 skill
安裝於：`%USERPROFILE%\.claude\skills\site-planning-review-assistant\SKILL.md`
觸發方式：`/site-planning-review-assistant` 或直接說「開始微輸出」
功能：提供敷地計畫的即時產出練習、量體檢核、申論回饋

### 輸出訓練三層
| 層級 | 內容 | 頻率 |
|------|------|------|
| 第一層 微輸出 | A申論一段／B量體速算／C前15分鐘啟動／D一張剖面 | 每天 15-20分鐘 |
| 第二層 半套整合 | E申論全題／F配置+剖面 | 每週2次 |
| 第三層 全套模擬 | G全套大圖（4小時） | 每1-2週 |

### 核心原則
- 先要求產出，再給檢核，不在未輸出前提供大量理論
- 回饋具體到「第幾步、哪個位置、怎麼修」
- 每次結束給一個「下一個立即可做的輸出動作」

---

## 🗣 語言學習模式 — 英文業務能力

**目標**：在不動產/都更業務場景能用英文溝通
**agent**：`english-tutor`（已建立）
**計畫文件**：`english-learning-plan.md`（12週課程）

### 預設情境庫

| 代號 | 情境 |
|---|---|
| S1 | 向外國投資人介紹都更案 |
| S2 | 向地主說明危老重建流程 |
| S3 | 接待外國訪客參觀基地 |
| S4 | 開發評估會議討論容積率 |
| S5 | 電話詢問建材報價 |
| S6 | 自我介紹（業主身分） |

### 使用方式
說「**開始 S1**」或「**模擬情境 S3**」，`english-tutor` 會接手。
英文錯誤全程用繁體中文說明，不打斷對話節奏。

---

## 🎓 學習模式 — AI 技能成長

**路線**：Track A（CLI Power User）+ Knowledge Worker 分支
（參考：<https://github.com/jeremy0819/awesome-agentic-ai-zh>）

| 層級 | 狀態 |
|------|------|
| Tier 0 Claude.ai 網頁版 | ✅ 熟練 |
| Tier 1 Claude Desktop + MCP | 🔄 學習中 |
| Tier 2 Claude Code、workflow | 🔄 使用中 |
| Tier 3 本地 LLM | ⏳ 未來 |

**環境**：Windows，Skills 位置 `%USERPROFILE%\.claude\skills\`

**待完成**：安裝 Claude Desktop → 學 MCP 連接 → 研究 n8n/Langflow

---

## 📌 下一步行動（跨 session 進度追蹤）

1. ✅ RE-DCF-Tool v3.1 完成並 push 到 GitHub
2. ✅ personal-studio 獨立版控，備份至 GitHub
3. ✅ 語言學習部規劃完成（english-tutor agent + english-learning-plan.md）
4. 📌 安裝 Claude Desktop（Tier 1 起點）
5. 📌 規劃「地主說明書自動生成」（文件部第一個落地案例）
6. 📌 研究 baoyu-translate skill 安裝方式
7. 📌 開始英文學習 Phase 1（從 S6 自我介紹情境開始）
8. 📌 持續備考輸出練習（每天至少一個微輸出）

---

## 給所有模式的通用原則
1. 步驟拆細，不預設我懂指令語法
2. 工具要說清楚它解決什麼具體問題
3. 不裝超出當前需要的工具
4. 用語走台灣繁中（資料/元件/函式/回傳值）
