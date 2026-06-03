# 如何把 Skill 安裝到 Claude（給非技術背景的我）

> 用工作室的比喻：**安裝一個 skill＝招募一個新員工進公司**。
> 這份教學照著做就會，不需要會寫程式。

---

## 0. 先搞懂三件事（觀念，30 秒）

1. **一個 skill 就是「一個資料夾」**，裡面一定有一個檔案叫 `SKILL.md`。
   - 資料夾名字＝這個員工的名字（例：`urban-renewal-analysis`）。
   - `SKILL.md`＝這個員工的「工作說明書」。
2. **`SKILL.md` 開頭那幾行（name / description）決定 Claude 何時會自動找這個員工上工**。description 寫得越清楚、觸發詞越多，Claude 越知道什麼時候該叫他。
3. **裝在哪裡，決定誰用得到**：
   - 裝「全域」→ **每個專案都能用**（像公司總部的員工）。
   - 裝「專案內」→ **只有那個專案用得到**（像某個案場的專屬人員）。

---

## 1. 兩個安裝位置（記住這兩條路徑就好）

| 想讓誰用 | 把 skill 資料夾放這裡 |
|---|---|
| **全部專案都能用**（總部員工） | `C:\Users\User\.claude\skills\` |
| **只有某個專案能用**（案場專員） | `<那個專案資料夾>\.claude\skills\` |

> 你現在的實例：
> - `urban-renewal-analysis` 裝在**全域** → `C:\Users\User\.claude\skills\urban-renewal-analysis\`
> - `personal-studio` 裝在**專案內** → `桌面\personal-studio\.claude\skills\personal-studio\`

---

## 2. 方法 A：手動安裝（最基本，一定要會）

### 情境：別人給你一個 skill 資料夾，或你自己要建一個。

**步驟 1**　打開檔案總管，貼上這個位置（全域）：
```
C:\Users\User\.claude\skills
```
（如果看不到 `.claude` 資料夾：檔案總管上方「檢視」→ 勾「隱藏的項目」。）

**步驟 2**　在這裡新增一個資料夾，名字用**英文小寫＋連字號**，例如：
```
contract-reviewer
```
（名字就是員工代號，不要有空格、不要中文。）

**步驟 3**　進到那個資料夾，新增一個檔案叫 `SKILL.md`，貼上這個模板：

```markdown
---
name: contract-reviewer
description: 審查建設相關合約時使用。標出風險條款、用白話逐條解釋，並標註哪幾條對地主／建商不利。觸發詞：合約審查、風險條款、協議合建、權利變換契約。
---

# 合約審查員

## 工作流程
1. 通讀整份合約，列出所有條款編號。
2. 逐條標記：對我方有利 / 中性 / 有風險。
3. 風險條款用白話解釋「最壞會發生什麼」。
4. 最後附一段免責聲明（非正式法律意見）。
```

**步驟 4**　**完全關掉 Claude Code，再重新打開**（這樣它才會重新點名員工）。

**步驟 5**　驗收：在對話打 `/` ，看清單裡有沒有出現 `contract-reviewer`。有，就代表招募成功 ✅。

> ⚠️ 最常見的失敗原因：
> - 資料夾名跟 `SKILL.md` 裡的 `name:` 不一樣 → 要一致。
> - 檔名打成 `SKILL.md.txt`（記事本偷加的）→ 要確認副檔名就是 `.md`。
> - 開頭的 `---` 上下各一行不能少。

---

## 3. 方法 B：從別人的 GitHub 複製一個 skill

很多現成 skill 放在 GitHub。做法就是「下載 → 把資料夾丟進 skills 位置」：

**步驟 1**　到那個 skill 的 GitHub 頁面，綠色「Code」鈕 → 「Download ZIP」。
**步驟 2**　解壓縮，找到裡面**含 `SKILL.md` 的那個資料夾**。
**步驟 3**　把那整個資料夾複製到 `C:\Users\User\.claude\skills\`。
**步驟 4**　關掉 Claude Code 重開，打 `/` 確認出現。

---

## 4. 方法 C：用「人資」自動找 skill（行政部流程）

如果你不知道有哪些現成 skill 可裝，用這個指令請「人資」去找：

打開 PowerShell（開始選單搜尋「PowerShell」），貼上：
```powershell
npx skills find
```
它會列出可安裝的 skill 清單，照畫面指示選要裝哪個。

> 📌 工作室鐵則：**先用現有員工，再招募新員工。** 裝新 skill 前先問自己：現有的 evaluation-analyst、document-specialist、mentor、auditor 能不能解？能就別急著裝。

---

## 5. 方法 D：請「訓練主管」幫你包一個新 skill（最省事）

如果是「我有一串每次都要重複講的指令，想變成固定員工」——不用自己寫，直接在 Claude Code 對話裡說：

> 「用 skill-creator 幫我把『每次寫地主說明書的流程』包成一個新 skill。」

`skill-creator` 會問你幾個問題，然後自動生成資料夾跟 `SKILL.md`，你只要確認。

---

## 6. 一頁速查表

| 我想做 | 怎麼做 |
|---|---|
| 裝一個現成 skill | 把它的資料夾丟進 `C:\Users\User\.claude\skills\` → 重開 Claude |
| 只給某專案用 | 丟進 `<專案>\.claude\skills\` |
| 確認裝好了 | 對話打 `/`，看清單有沒有它 |
| 不知道有什麼可裝 | PowerShell 打 `npx skills find` |
| 想把自己的重複流程變 skill | 對話請 `skill-creator` 幫包 |
| 裝了沒反應 | ①關掉重開 ②查資料夾名＝name ③查檔名是 `.md` 不是 `.md.txt` |

---

## 履歷句型（完成這件事可以寫進履歷）

> 「自建並維護 Claude Code 個人 skill 庫，將都更／危老評估、合約審查等重複作業封裝為可重用的 AI 員工，依專案分層部署（全域／專案內），降低重複指令成本。」

---

*本教學依 2026-06-03 你電腦上的實際 skill 結構撰寫（範本參考自 urban-renewal-analysis）。*
