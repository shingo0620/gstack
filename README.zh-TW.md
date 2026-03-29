# gstack

> 「我大概從十二月開始就沒有打過一行程式碼了，這是一個非常巨大的轉變。」— [Andrej Karpathy](https://fortune.com/2026/03/21/andrej-karpathy-openai-cofounder-ai-agents-coding-state-of-psychosis-openclaw/)，No Priors podcast，2026 年 3 月

當我聽到 Karpathy 這麼說時，我想知道他是怎麼做到的。一個人怎麼能像二十人團隊一樣高速交付？Peter Steinberger 打造了 [OpenClaw](https://github.com/openclaw/openclaw) — 247K GitHub 星標 — 基本上是靠 AI agent 獨自完成的。革命已經到來。一個擁有正確工具的建造者，可以比傳統團隊更快地行動。

我是 [Garry Tan](https://x.com/garrytan)，[Y Combinator](https://www.ycombinator.com/) 的總裁兼執行長。我與數千家新創公司合作過 — Coinbase、Instacart、Rippling — 在它們還只是車庫裡一兩個人的時候。在 YC 之前，我是 Palantir 最早的工程師/PM/設計師之一，共同創辦了 Posterous（後被 Twitter 收購），並打造了 Bookface，YC 的內部社群網路。

**gstack 是我的答案。** 我做產品已經二十年了，而現在我寫的程式碼比以往任何時候都多。過去 60 天：**600,000+ 行正式程式碼**（35% 為測試），**每天 10,000-20,000 行**，兼職進行，同時全職經營 YC。以下是我最近一次橫跨 3 個專案的 `/retro`：**140,751 行新增，362 次 commit，約 115k 淨 LOC**，僅一週。

**2026 — 1,237 次貢獻，持續增加中：**

![GitHub contributions 2026 — 1,237 contributions, massive acceleration in Jan-Mar](docs/images/github-2026.png)

**2013 — 我在 YC 打造 Bookface 時（772 次貢獻）：**

![GitHub contributions 2013 — 772 contributions building Bookface at YC](docs/images/github-2013.png)

同一個人。不同的時代。差異在於工具。

**gstack 就是我的做法。** 它把 Claude Code 變成一個虛擬工程團隊 — 一位重新思考產品的 CEO、一位鎖定架構的工程經理、一位抓出 AI 粗製濫造的設計師、一位找出正式環境 bug 的審查者、一位打開真實瀏覽器的 QA 主管、一位執行 OWASP + STRIDE 審計的資安長，以及一位推送 PR 的發布工程師。二十位專家和八個強大工具，全部是 slash command，全部是 Markdown，全部免費，MIT 授權。

這是我的開源軟體工廠。我每天都在用。我分享它，因為這些工具應該讓每個人都能使用。

Fork 它。改進它。讓它成為你的。如果你想批評免費開源軟體 — 歡迎，但我更希望你先試試看。

**這是為誰準備的：**
- **創辦人和 CEO** — 特別是仍然想要親自交付程式碼的技術型創辦人
- **第一次使用 Claude Code 的人** — 結構化角色取代空白 prompt
- **技術主管和資深工程師** — 每個 PR 都有嚴謹的審查、QA 和發布自動化

## 快速開始

1. 安裝 gstack（30 秒 — 見下方）
2. 執行 `/office-hours` — 描述你正在打造的東西
3. 對任何功能構想執行 `/plan-ceo-review`
4. 對任何有變更的分支執行 `/review`
5. 對你的 staging URL 執行 `/qa`
6. 到此為止。你會知道這適不適合你。

## 安裝 — 30 秒

**需求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Git](https://git-scm.com/)、[Bun](https://bun.sh/) v1.0+、[Node.js](https://nodejs.org/)（僅 Windows 需要）

### 第一步：安裝到你的電腦上

打開 Claude Code 並貼上以下內容。Claude 會完成剩下的工作。

> 安裝 gstack：執行 **`git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup`** 然後在 CLAUDE.md 中加入一個「gstack」區段，說明使用 gstack 的 /browse skill 來進行所有網頁瀏覽，永遠不使用 mcp\_\_claude-in-chrome\_\_\* 工具，並列出可用的 skill：/office-hours、/plan-ceo-review、/plan-eng-review、/plan-design-review、/design-consultation、/design-shotgun、/review、/ship、/land-and-deploy、/canary、/benchmark、/browse、/connect-chrome、/qa、/qa-only、/design-review、/setup-browser-cookies、/setup-deploy、/retro、/investigate、/document-release、/codex、/cso、/autoplan、/careful、/freeze、/guard、/unfreeze、/gstack-upgrade。然後詢問使用者是否也要將 gstack 加入目前的專案，以便團隊成員也能使用。

### 第二步：加入你的 repo 讓團隊成員也能使用（選用）

> 將 gstack 加入此專案：執行 **`cp -Rf ~/.claude/skills/gstack .claude/skills/gstack && rm -rf .claude/skills/gstack/.git && cd .claude/skills/gstack && ./setup`** 然後在此專案的 CLAUDE.md 中加入一個「gstack」區段，說明使用 gstack 的 /browse skill 來進行所有網頁瀏覽，永遠不使用 mcp\_\_claude-in-chrome\_\_\* 工具，列出可用的 skill：/office-hours、/plan-ceo-review、/plan-eng-review、/plan-design-review、/design-consultation、/review、/ship、/land-and-deploy、/canary、/benchmark、/browse、/qa、/qa-only、/design-review、/setup-browser-cookies、/setup-deploy、/retro、/investigate、/document-release、/codex、/cso、/careful、/freeze、/guard、/unfreeze、/gstack-upgrade，並告訴 Claude 如果 gstack skill 無法運作，執行 `cd .claude/skills/gstack && ./setup` 來建置 binary 並註冊 skill。

真實檔案會被 commit 到你的 repo（不是 submodule），所以 `git clone` 就能直接使用。所有東西都在 `.claude/` 裡。不會動到你的 PATH，也不會在背景執行任何東西。

> **想要貢獻或需要完整歷史？** 上述指令使用 `--depth 1` 來快速安裝。如果你計畫貢獻或需要完整的 git 歷史，請改用完整 clone：
> ```bash
> git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
> ```

### Codex、Gemini CLI 或 Cursor

gstack 適用於任何支援 [SKILL.md 標準](https://github.com/anthropics/claude-code)的 agent。Skill 位於 `.agents/skills/`，會被自動發現。

安裝到單一 repo：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git .agents/skills/gstack
cd .agents/skills/gstack && ./setup --host codex
```

當 setup 從 `.agents/skills/gstack` 執行時，會將生成的 Codex skill 安裝在同一個 repo 中，不會寫入 `~/.codex/skills`。

安裝到使用者帳號（全域）：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host codex
```

`setup --host codex` 會在 `~/.codex/skills/gstack` 建立 runtime root，並在頂層連結生成的 Codex skill。這避免了從來源 repo checkout 產生重複的 skill 發現。

或讓 setup 自動偵測你安裝了哪些 agent：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto
```

對於 Codex 相容的主機，setup 現在同時支援從 `.agents/skills/gstack` 的 repo 本地安裝和從 `~/.codex/skills/gstack` 的使用者全域安裝。所有 28 個 skill 都能在所有支援的 agent 上運作。Hook 型安全 skill（careful、freeze、guard）在非 Claude 主機上使用內嵌安全提示文字。

## 實際運作

```
你：    我想做一個日曆每日簡報 app。
你：    /office-hours
Claude: [詢問痛點 — 具體的例子，不是假設]

你：    多個 Google 日曆、事件資訊過時、地點錯誤。
        準備工作費時且結果不夠好...

Claude: 我要挑戰你的定義。你說的是「每日簡報 app」。
        但你實際描述的是一個個人幕僚長 AI。
        [提取你沒意識到的 5 項能力]
        [挑戰 4 個前提 — 你同意、不同意或調整]
        [生成 3 種實作方案及工時估算]
        建議：明天就發布最窄的切入點，從真實使用中學習。
        完整願景是 3 個月的專案 — 先從一個真正有用的
        每日簡報開始。
        [撰寫設計文件 → 自動傳遞給下游 skill]

你：    /plan-ceo-review
        [讀取設計文件，挑戰範圍，執行 10 個章節的審查]

你：    /plan-eng-review
        [資料流程 ASCII 圖、狀態機、錯誤處理路徑]
        [測試矩陣、失敗模式、安全疑慮]

你：    批准計畫。退出 plan mode。
        [在 11 個檔案中寫了 2,400 行。約 8 分鐘。]

你：    /review
        [自動修復] 2 個問題。[詢問] Race condition → 你批准修復。

你：    /qa https://staging.myapp.com
        [打開真實瀏覽器，點擊各個流程，找到並修復一個 bug]

你：    /ship
        測試：42 → 51（+9 新增）。PR: github.com/you/app/pull/42
```

你說的是「每日簡報 app」。Agent 說「你正在打造一個幕僚長 AI」 — 因為它聽的是你的痛點，而不是你的功能需求。八個指令，端到端。這不是副駕駛。這是一個團隊。

## 開發衝刺流程

gstack 是一個流程，不是工具的集合。Skill 按照衝刺的順序執行：

**思考 → 規劃 → 建造 → 審查 → 測試 → 發布 → 回顧**

每個 skill 都銜接下一個。`/office-hours` 撰寫的設計文件會被 `/plan-ceo-review` 讀取。`/plan-eng-review` 撰寫的測試計畫會被 `/qa` 接手。`/review` 發現的 bug 會被 `/ship` 確認已修復。不會有任何東西漏掉，因為每個步驟都知道之前發生了什麼。

| Skill | 你的專家 | 他們做什麼 |
|-------|---------|-----------|
| `/office-hours` | **YC Office Hours** | 從這裡開始。六個逼問問題，在你寫程式碼之前重新定義你的產品。挑戰你的定義，質疑前提，生成實作替代方案。設計文件會傳遞給每個下游 skill。 |
| `/plan-ceo-review` | **CEO / 創辦人** | 重新思考問題。找到隱藏在需求中的 10 星級產品。四種模式：擴展、選擇性擴展、維持範圍、縮減。 |
| `/plan-eng-review` | **工程經理** | 鎖定架構、資料流、圖表、邊界情況和測試。把隱藏的假設攤在陽光下。 |
| `/plan-design-review` | **資深設計師** | 對每個設計維度評分 0-10，解釋 10 分長什麼樣，然後編輯計畫以達成目標。AI 粗製濫造偵測。互動式 — 每個設計選擇一個 AskUserQuestion。 |
| `/design-consultation` | **設計夥伴** | 從零開始建立完整的設計系統。研究現有方案，提出創意風險，生成逼真的產品 mockup。 |
| `/review` | **Staff Engineer** | 找出通過 CI 但在正式環境爆炸的 bug。自動修復明顯的問題。標記完整性缺口。 |
| `/investigate` | **除錯專家** | 系統性根因除錯。鐵律：沒有調查就不修復。追蹤資料流，測試假設，三次失敗修復後停止。 |
| `/design-review` | **會寫程式的設計師** | 與 /plan-design-review 相同的審計，然後修復它發現的問題。原子化 commit，修改前後截圖。 |
| `/design-shotgun` | **設計探索者** | 生成多個 AI 設計變體，在瀏覽器中打開比較看板，反覆迭代直到你批准方向。品味記憶會偏向你的偏好。 |
| `/qa` | **QA 主管** | 測試你的 app，找 bug，用原子化 commit 修復，重新驗證。為每個修復自動生成迴歸測試。 |
| `/qa-only` | **QA 報告員** | 與 /qa 相同的方法但僅報告。純粹的 bug 報告，不做程式碼變更。 |
| `/cso` | **資安長** | OWASP Top 10 + STRIDE 威脅模型。零噪音：17 項誤報排除，8/10+ 信心度門檻，獨立發現驗證。每個發現都包含具體的攻擊情境。 |
| `/ship` | **發布工程師** | 同步 main，執行測試，審計覆蓋率，推送，開 PR。如果你沒有測試框架，會自動建立一個。 |
| `/land-and-deploy` | **發布工程師** | 合併 PR，等待 CI 和部署，驗證正式環境健康。一個指令從「已核准」到「已在正式環境驗證」。 |
| `/canary` | **SRE** | 部署後監控迴圈。監看 console 錯誤、效能退化和頁面故障。 |
| `/benchmark` | **效能工程師** | 基準頁面載入時間、Core Web Vitals 和資源大小。每個 PR 比較前後差異。 |
| `/document-release` | **技術文件撰寫者** | 更新所有專案文件以配合你剛發布的內容。自動捕捉過時的 README。 |
| `/retro` | **工程經理** | 團隊感知的每週回顧。個人細項、發布連勝紀錄、測試健康趨勢、成長機會。`/retro global` 橫跨所有專案和 AI 工具（Claude Code、Codex、Gemini）執行。 |
| `/browse` | **QA 工程師** | 給 agent 眼睛。真實的 Chromium 瀏覽器、真實的點擊、真實的截圖。每個指令約 100ms。`$B connect` 啟動你真實的 Chrome 作為 headed 視窗 — 即時觀看每個動作。 |
| `/setup-browser-cookies` | **Session 管理員** | 從你真實的瀏覽器（Chrome、Arc、Brave、Edge）匯入 cookies 到 headless session。測試需要認證的頁面。 |
| `/autoplan` | **審查流水線** | 一個指令，完整審查的計畫。自動執行 CEO → 設計 → 工程審查，內建決策原則。僅將品味決策交給你核准。 |

### 強大工具

| Skill | 功能 |
|-------|-----|
| `/codex` | **第二意見** — 來自 OpenAI Codex CLI 的獨立程式碼審查。三種模式：審查（通過/不通過門檻）、對抗性挑戰和開放諮詢。當 `/review` 和 `/codex` 都審查過後，提供跨模型分析。 |
| `/careful` | **安全護欄** — 在破壞性指令（rm -rf、DROP TABLE、force-push）前發出警告。說「be careful」即可啟用。可覆蓋任何警告。 |
| `/freeze` | **編輯鎖定** — 將檔案編輯限制在一個目錄內。在除錯時防止意外更改範圍外的程式碼。 |
| `/guard` | **完整安全** — `/careful` + `/freeze` 合一。正式環境工作的最大安全性。 |
| `/unfreeze` | **解鎖** — 移除 `/freeze` 限制。 |
| `/connect-chrome` | **Chrome 控制器** — 啟動由 gstack 控制的真實 Chrome，搭配 Side Panel 擴充功能。即時觀看每個動作。 |
| `/setup-deploy` | **部署設定器** — `/land-and-deploy` 的一次性設定。偵測你的平台、正式環境 URL 和部署指令。 |
| `/gstack-upgrade` | **自我更新** — 升級 gstack 到最新版。偵測全域或 vendored 安裝，同步兩者，顯示變更內容。 |

**[每個 skill 的深入說明、範例和設計理念 →](docs/skills.md)**

## 平行衝刺

gstack 用一個衝刺就很強大。十個同時執行時更令人驚豔。

**設計是核心。** `/design-consultation` 不只是挑字體。它研究你領域中的現有方案，提出安全選擇和創意風險，生成你實際產品的逼真 mockup，並撰寫 `DESIGN.md` — 然後 `/design-review` 和 `/plan-eng-review` 會讀取你的選擇。設計決策貫穿整個系統。

**`/qa` 是一個巨大的突破。** 它讓我從 6 個平行 worker 增加到 12 個。Claude Code 說*「我看到問題了」*然後真的修復它、生成迴歸測試、並驗證修復 — 這改變了我的工作方式。Agent 現在有眼睛了。

**智慧審查路由。** 就像運作良好的新創公司：CEO 不需要看基礎設施的 bug 修復，設計審查不需要看後端變更。gstack 追蹤哪些審查已執行，判斷什麼是適當的，然後做正確的事。Review Readiness Dashboard 在你發布前告訴你目前的狀態。

**測試一切。** `/ship` 會在你的專案沒有測試框架時從零建立一個。每次 `/ship` 執行都會產出覆蓋率審計。每個 `/qa` bug 修復都會生成迴歸測試。100% 測試覆蓋率是目標 — 測試讓 vibe coding 變得安全而非 yolo coding。

**`/document-release` 是你從未有過的工程師。** 它讀取你專案中的每個文件檔案，交叉比對 diff，並更新所有偏離的內容。README、ARCHITECTURE、CONTRIBUTING、CLAUDE.md、TODOS — 全部自動保持最新。而且現在 `/ship` 會自動調用它 — 文件無需額外指令就能保持最新。

**真實瀏覽器模式。** `$B connect` 啟動你實際的 Chrome 作為由 Playwright 控制的 headed 視窗。你即時觀看 Claude 點擊、填寫和導航 — 同一個視窗、同一個螢幕。頂部邊緣的細微綠色微光告訴你 gstack 控制的是哪個 Chrome 視窗。所有現有的 browse 指令都不變。`$B disconnect` 回到 headless。Chrome 擴充功能 Side Panel 顯示每個指令的即時動態和一個聊天側邊欄，你可以在那裡指揮 Claude。這是共存 — Claude 不是在遠端控制一個隱藏的瀏覽器，它與你坐在同一個駕駛艙。

**側邊欄 agent — 你的 AI 瀏覽器助手。** 在 Chrome side panel 輸入自然語言指令，一個子 Claude 實例會執行它們。「導航到設定頁面並截圖。」「用測試資料填寫這個表單。」「瀏覽這個列表中的每個項目並提取價格。」每個任務最多 5 分鐘。側邊欄 agent 在隔離的 session 中執行，不會干擾你的主要 Claude Code 視窗。就像在瀏覽器中有第二雙手。

**個人自動化。** 側邊欄 agent 不只是用於開發工作流程。例如：「瀏覽我小孩學校的家長入口網站，把所有其他家長的姓名、電話號碼和照片加入我的 Google 聯絡人。」兩種認證方式：（1）在 headed 瀏覽器中登入一次 — 你的 session 會保留，或（2）執行 `/setup-browser-cookies` 從你真實的 Chrome 匯入 cookies。認證後，Claude 導航目錄、提取資料、建立聯絡人。

**AI 卡住時的瀏覽器接手。** 遇到 CAPTCHA、認證牆或 MFA 提示？`$B handoff` 打開一個可見的 Chrome，保留你所有的 cookies 和分頁。解決問題，告訴 Claude 你完成了，`$B resume` 從中斷處繼續。Agent 在連續 3 次失敗後甚至會自動建議此功能。

**多 AI 第二意見。** `/codex` 從 OpenAI 的 Codex CLI 取得獨立審查 — 一個完全不同的 AI 看同一個 diff。三種模式：帶通過/不通過門檻的程式碼審查、主動嘗試破壞你程式碼的對抗性挑戰、以及具有 session 連續性的開放諮詢。當 `/review`（Claude）和 `/codex`（OpenAI）都審查了同一個分支，你會得到跨模型分析，顯示哪些發現重疊、哪些是各自獨有的。

**按需安全護欄。** 說「be careful」，`/careful` 會在任何破壞性指令前發出警告 — rm -rf、DROP TABLE、force-push、git reset --hard。`/freeze` 在除錯時將編輯鎖定在一個目錄，防止 Claude 意外「修復」不相關的程式碼。`/guard` 同時啟用兩者。`/investigate` 會自動凍結到正在調查的模組。

**主動 skill 建議。** gstack 會注意你所處的階段 — 腦力激盪、審查、除錯、測試 — 並建議合適的 skill。不喜歡？說「stop suggesting」，它會跨 session 記住。

## 10-15 個平行衝刺

gstack 用一個衝刺就很強大。十個同時執行時是變革性的。

[Conductor](https://conductor.build) 平行執行多個 Claude Code session — 每個都在自己的隔離工作區中。一個 session 在新想法上執行 `/office-hours`，另一個在 PR 上做 `/review`，第三個在實作功能，第四個在 staging 上執行 `/qa`，還有六個在其他分支上。全部同時進行。我通常執行 10-15 個平行衝刺 — 這是目前的實用上限。

衝刺結構是讓平行化可行的關鍵。沒有流程，十個 agent 就是十個混亂來源。有了流程 — 思考、規劃、建造、審查、測試、發布 — 每個 agent 都確切知道該做什麼和何時停止。你像 CEO 管理團隊那樣管理它們：關注重要的決策，讓其餘的自行運轉。

---

免費，MIT 授權，開源。沒有付費等級，沒有等候名單。

我開源了我建造軟體的方式。你可以 fork 它，讓它成為你自己的。

> **我們正在招募。** 想要每天交付 10K+ LOC 並幫助強化 gstack？
> 來 YC 工作 — [ycombinator.com/software](https://ycombinator.com/software)
> 極具競爭力的薪資和股權。舊金山，Dogpatch 區。

## 文件

| 文件 | 內容 |
|------|------|
| [Skill 深入解析](docs/skills.md) | 每個 skill 的設計理念、範例和工作流程（包含 Greptile 整合） |
| [建造者精神](ETHOS.md) | 建造者哲學：Boil the Lake、Search Before Building、三層知識 |
| [架構](ARCHITECTURE.md) | 設計決策和系統內部運作 |
| [瀏覽器參考](BROWSER.md) | `/browse` 的完整指令參考 |
| [貢獻指南](CONTRIBUTING.md) | 開發環境設定、測試、貢獻者模式和開發模式 |
| [更新日誌](CHANGELOG.md) | 每個版本的新功能 |

## 隱私與遙測

gstack 包含**選擇加入**的使用遙測以幫助改進專案。以下是確切的運作方式：

- **預設為關閉。** 除非你明確同意，否則不會向任何地方發送任何東西。
- **首次執行時，** gstack 會詢問你是否願意分享匿名使用資料。你可以拒絕。
- **發送的內容（如果你選擇加入）：** skill 名稱、持續時間、成功/失敗、gstack 版本、作業系統。就這些。
- **永遠不會發送的內容：** 程式碼、檔案路徑、repo 名稱、分支名稱、prompt 或任何使用者生成的內容。
- **隨時可更改：** `gstack-config set telemetry off` 立即停用一切。

資料儲存在 [Supabase](https://supabase.com)（開源 Firebase 替代方案）。Schema 在 [`supabase/migrations/`](supabase/migrations/) — 你可以驗證確切收集了什麼。Repo 中的 Supabase publishable key 是公開金鑰（如同 Firebase API key） — row-level security 策略拒絕所有直接存取。遙測透過已驗證的 edge function 流轉，這些 function 強制執行 schema 檢查、事件類型允許清單和欄位長度限制。

**本地分析始終可用。** 執行 `gstack-analytics` 查看你從本地 JSONL 檔案獲取的個人使用儀表板 — 不需要遠端資料。

## 疑難排解

**Skill 沒有出現？** `cd ~/.claude/skills/gstack && ./setup`

**`/browse` 失敗？** `cd ~/.claude/skills/gstack && bun install && bun run build`

**安裝過時？** 執行 `/gstack-upgrade` — 或在 `~/.gstack/config.yaml` 中設定 `auto_upgrade: true`

**想要更短的指令？** `cd ~/.claude/skills/gstack && ./setup --no-prefix` — 從 `/gstack-qa` 切換為 `/qa`。你的選擇會在未來升級時被記住。

**想要帶命名空間的指令？** `cd ~/.claude/skills/gstack && ./setup --prefix` — 從 `/qa` 切換為 `/gstack-qa`。在你同時使用其他 skill pack 時很有用。

**Codex 顯示 "Skipped loading skill(s) due to invalid SKILL.md"？** 你的 Codex skill 描述過時了。修復方式：`cd ~/.codex/skills/gstack && git pull && ./setup --host codex` — 或 repo 本地安裝：`cd "$(readlink -f .agents/skills/gstack)" && git pull && ./setup --host codex`

**Windows 使用者：** gstack 可在 Windows 11 上透過 Git Bash 或 WSL 運作。除了 Bun 外還需要 Node.js — Bun 在 Windows 上的 Playwright pipe transport 有已知 bug（[bun#4253](https://github.com/oven-sh/bun/issues/4253)）。Browse server 會自動退回 Node.js。確保 `bun` 和 `node` 都在你的 PATH 中。

**Claude 說它看不到 skill？** 確保你專案的 `CLAUDE.md` 有 gstack 區段。加入以下內容：

```
## gstack
使用 gstack 的 /browse 進行所有網頁瀏覽。永遠不使用 mcp__claude-in-chrome__* 工具。
可用 skill：/office-hours、/plan-ceo-review、/plan-eng-review、/plan-design-review、
/design-consultation、/review、/ship、/land-and-deploy、/canary、/benchmark、/browse、
/qa、/qa-only、/design-review、/setup-browser-cookies、/setup-deploy、/retro、
/investigate、/document-release、/codex、/cso、/autoplan、/careful、/freeze、/guard、
/unfreeze、/gstack-upgrade。
```

## 授權

MIT。永遠免費。去打造些什麼吧。
