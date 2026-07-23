<!-- short_topic: claude-code-creator-boris-cherny-enterprises-prefer-pay-per-token-not-seats-1000-agents-per-engineer-90pct-code-ai-written-switching-cost-moat-erodes -->

# Odd Lots（來賓 Boris Cherny，Anthropic Claude Code 負責人）— **賣方視角的 agentic coding 一手產品輸入：「企業普遍偏好 pay-per-token 而非有 rate limit 的訂閱制」＝ consumption 計價的直接證言；採用階梯已從「1 工程師 1 個 agent」爬到「部分客戶 1,000 agents/工程師」；Anthropic 內部平均約 90% 的程式碼由 Claude Code 產出（本人自 2025-11 起 100%）；他親口承認 switching-cost 護城河會弱化（「叫 Claude 幫你從 A 廠遷到 B 廠」），但主張大型 SaaS 是多重護城河疊加故大體無恙；Bun 團隊 1 人 11 天完成 Zig→Rust 全庫遷移（過去＝數名工程師 1 年）。⚠️ 全片成長/採用/能力數字皆為 Anthropic 員工談自家旗艦產品，零第三方稽核**

- 節目: Bloomberg **Odd Lots** podcast（@OddLots）
- 主持: **Joe Weisenthal**（@thestalwart）、**Tracy Alloway**（轉錄作 "Tracy Aloway / Tracy Alaway" ⚠️）
- 來賓: **Boris Cherny**（轉錄全片作 **"Boris Churnney"** ⚠️；X 帳號轉錄作 "Bchurnney" → 實為 **@bcherny**）— **Anthropic，Claude Code 創造者暨負責人（head of Claude Code）**。自述加入 Anthropic 的第一個團隊是 **Anthropic Labs**，該團隊做出 **Claude Code、MCP、Skills、桌面 app**
- 來源: https://www.youtube.com/watch?v=7C_IHWkHKmU
- 發布日期: **2026-07-20** ｜ 時長: **70.2 分鐘**
- 逐字稿: `log_gen_by_roma/video_digest/21-07-2026/OddLots_The Creator of Claude Code on The Hottest Piece of Software in the World _ Odd L.transcript.md`
- 轉錄方式: yt-caption（en-orig；**模型名/產品名誤植極嚴重**，見 §四(3)）

---

## 縮寫對照

| 縮寫 / 術語 | 全稱 | 說明 |
|---|---|---|
| **agentic coding** | 代理式編程 | 由模型自主規劃、執行、驗證多步驟編程任務，非單次補全 |
| **harness** | 外殼／載具 | 包住模型的產品層（CLI/IDE/app）；本集核心詞，Boris 稱 Claude Code 為 "a very general harness" |
| **token** | 詞元 | 模型輸入/輸出的計費單位；consumption pricing 的計價基礎 |
| **context window** | 上下文視窗 | 單次對話可容納的 token 上限；Joe 提及「用完視窗只好去散步」的使用者體驗 |
| **inference** | 推理 | 模型執行（相對於 training 訓練）；agentic coding 的 token 消耗全在此側 |
| **eval** | evaluation | 在「培養皿式」實驗環境評估模型行為（Boris 語） |
| **mech interp** | mechanistic interpretability | 機制可解釋性；查看模型「神經元」內部，本集用來做 prompt-injection 偵測探針（probes） |
| **prompt injection** | 提示注入 | 惡意內容藏在模型會讀到的資料裡，劫持模型執行非使用者意圖的指令 |
| **MCP** | Model Context Protocol | 模型連接外部工具/資料的開放協定（轉錄把 "MCP, Skills" 連寫成 "MCP skills" ⚠️） |
| **ARR** | Annual Recurring Revenue | 年度經常性收入（本集**完全未揭露任何 ARR 數字**） |
| **seat-based pricing** | 按席次計價 | 傳統 SaaS 訂閱（每人每月固定費） |
| **consumption pricing** | 按用量計價 | 按 token/query 計費；本集來賓稱**企業客戶普遍偏好此模式** |
| **Seven Powers** | 七種力量 | Hamilton Helmer 的護城河框架（規模經濟／網路效應／轉換成本／cornered resource 等）；⚠️ **全片把 "moat" 轉錄成 "mode"**，該段須全部讀作「護城河」 |
| **dogfooding** | 吃自家狗糧 | 自己用自己的產品；Boris 強調 Claude Code 走與客戶完全相同的公開 API |
| **product overhang** | 產品懸置 | 模型已具備某能力、但產品層擋住了使用者體驗到它 |
| **unhobble** | 解除束縛 | AI 圈用語：拿掉產品層限制讓模型發揮完整能力 |
| **NRR / cRPO** | Net Revenue Retention / current Remaining Performance Obligation | 淨收入留存率／當期剩餘履約義務；我方判別軟體 de-rate 的 SSOT 指標 |

---

> **來源性質**：本集是 Bloomberg Odd Lots 的**一手具名訪談**，來賓是 **Anthropic 內部負責 Claude Code 的產品當事人**。
>
> **⚠️ 結構性 talking-his-book 到頂。** 這不是「產業當事人談產業」（如 07-13 那集的律所主席，他是 legaltech 的**買方**），而是**賣方員工談自家旗艦產品**。全片所有關於「成長、採用率、能力領先、安全性優於競品」的陳述**都是一方之詞、無獨立稽核、且沒有任何絕對數字**（無營收、無 ARR、無 token 量、無使用者數）。同時，Anthropic 是**私人公司**，這些說法**不受任何財報揭露責任約束**。
>
> **但它同時是罕見的一手產品端資訊。** 判讀時必須把兩類內容切開：
>
> **【可當一手事實對待】**（機制性、可被外部觀察/驗證、講錯對他不利）：
> - 產品面：Claude Code 有 CLI / IDE 擴充 / 桌面 app / iOS+Android / Slack（Claude Tag）五種介面；設定項約 400–500 個；auto mode 是新的權限模式；sandbox 開源且與 agent 無關。
> - **計價結構：「企業客戶通常不用有 rate limit 的訂閱制，偏好 pay-per-token」** ← 這是本集對我方最有價值的一句，屬於**產品端可觀察的事實**而非成長宣稱。
> - 企業管控機制：spend controls、advisor models、企業層級的 effort levels、預設安全設定。
> - 客戶名單：Airbnb、Ramp、Salesforce、NASA、「紐約最大的幾家銀行」、「最大的幾家藥廠」（具名可被否認 → 可信度較高）。
>
> **【必須重度折扣】**（成長率、顛覆宣稱、競爭定位）：
> - 「四次成長拐點」「growth inflected」— **無任何基數與絕對值**，成長率脫離基數即無意義。
> - 「1 → 10 → 100 → 1,000 agents 每工程師」— **無客戶數、無分布、無中位數**，「some customers」的極端值。
> - 「除了我們的模型以外每一個模型都被 prompt inject 成功」— **競賽由 Anthropic 自辦、獎金自付、結果登在自家 model card**。
> - 「Anthropic 內部平均約 90% 程式碼由 Claude Code 寫」— 口徑不明（行數？commit？），且緊接著 Joe 說「那 2%」，**90% 與 98% 自相矛盾**（見 §四(4)）。
> - 「scaling laws 依然平滑、甚至有點加速」— **零證據，且他用這句迴避了主持人問的 model collapse 問題**。
>
> 依 [[feedback_data_source_priority]]：本集為**敘事/機制輸入**，**不作交易依據、不作進場價**；任何牆位/財報日/flow 一律回 SG data_table 覆核。

---

## 一、TL;DR（依論點支柱分組；粗體＝數字；⚠️＝無出處/自誇/口徑問題）

### 支柱 ① 計價模式：企業偏好 pay-per-token（本集對我方最有價值的一段）

- 💣 **核心證言**（Joe 問「不是 Anthropic 大客戶的話，會不會拿不到 Fable 的額度」，Boris 的答案順帶揭露了計價結構）：
  > "when you look at companies, they're not using subscription plans typically that have rate limits. **Usually companies prefer to pay per token.** … Because that way they can kind of control it. They can forecast a little bit better. And also their engineers don't hit rate limits."
  > （「企業通常不用有 rate limit 的訂閱方案，**通常企業偏好按 token 付費**……這樣他們能控制、能預測得好一點，工程師也不會撞到速率上限。」）
- **判讀**：這是一個**與「seat-based 訂閱是企業軟體天然形態」相反方向的買方行為證言**。企業寧可承受帳單波動，換取（a）不撞天花板（b）可預測性（c）可控性。注意這裡的「可預測」指的是**可管控**，不是「金額固定」——**企業買 AI 產能的心智模型已經是「買 compute」而不是「買席次」**。
- ⚠️ **但不可過度外推**：Claude Code 賣的是**模型產能本身**，本來就沒有 seat 的物理意義；這不等於「應用層 SaaS 的 seat 模式會崩」。它是**類比證據**，不是**同構證據**。
- 企業層級的用量管控工具（Boris 列舉）：**spend controls**（轉錄作 "perceived spend controls"，疑為 **preset** ⚠️）、**advisor models**、**enterprise 層級可選 effort levels**、sandbox 等安全預設。→ 全都是**為 consumption 計價服務的治理層**，反向印證主流是按量計費。

### 支柱 ② 採用階梯：從「1 個 agent」到「1,000 agents 每工程師」（token 需求的機制敘事）

- Boris 的「採用階梯（ladder）」模型：**不能一步登天，要一階一階爬**。
  - 第 1 階：企業先透過 IDE 或其他程式用上 Claude。
  - 第 2 階：發 Claude Code + Co-work + Claude Tag 給所有人；**初期是「一個工程師一個 session」（1:1）**。
  - 同步建立 guardrails：spend controls、advisor models、effort levels、sandbox。
- 💣 **並發量的爬升**：
  > "the ones that adopted it early on … went from **one Claude per engineer to 10 Claudes to 100 Claudes**, now **some to a thousand Claudes per engineer**"
  - ⚠️ **這是全片對 inference 需求最重要的機制陳述，但也是最無法驗證的一句**：「some」＝極端值，無客戶數、無分布、無中位數、無時間軸。
- 他本人的工作型態：**「任何時刻我都有幾個 Claude 在跑，有時幾百個、有時幾千個」**，彼此協作建軟體。⚠️ 自述。
- **抽象層級的兩次躍遷**（他的史觀）：
  - 1960s–2020s（約 50 年）：人**直接寫**軟體（此前是打孔卡／純硬體邏輯，他祖父在蘇聯寫打孔卡）。
  - 2024–2025：**人不再直接寫，改成跟模型講話、模型寫程式**。
  - 2026：**再上一層——人講話 → 模型指揮其他模型 → 那些模型寫原始碼**（loops / routines / Claude Tag）。
  > "I was stuck in this one place for 50 years and we just had **two leaps in two years**."
- **產品懸置（product overhang）論**：模型能力已超前產品能承載的，現在的瓶頸是「使用者一次一個 prompt 來回」——**解法是 loops / routines / Claude Tag，讓 Claude 長時間跑**（他稱有 Tag session **連續跑了數週**）。
  - 對應到 token：**從「一問一答」到「跑數週的長任務」是 inference 消耗的量級躍遷**。⚠️ 純機制推論，本集無任何 token 量數字。

### 支柱 ③ 「幾乎全是模型，不是 harness」— 一句對自家 harness 護城河不利的坦白

- Joe 問：2026 的爆發是「harness 站穩了」還是「模型變好了」？
  > **"Oh, it's almost all the model."**
- 他列出四次「成長拐點」，全部綁在模型發布：
  - **Opus 4 / Sonnet 4（2025-05）** → growth inflected
  - **Opus 4.5（2025-11）** → inflected（轉錄口誤先說 May 後自我更正為 November ⚠️）
  - **Opus 4.6（2026-02）** → inflected again
  - **「now Fable」**
- ⚠️ **全部沒有基數、沒有絕對值**。「growth inflected」在私人公司口中可以是任何東西。
- **內部張力**：他前面才用一整段論證 harness 的差異化（auto mode、sandbox、權限提示、prompt-injection 防護），這裡卻說「幾乎全是模型」。**兩句都要引用，不要只取一半。**
- Claude Code **走與所有客戶相同的公開 Anthropic API，沒有私有 API**（dogfooding）。→ 這條**對外部開發者是利多敘事**（平台不偏心），也是他解釋「客戶跟我們一起受益於模型變好」的機制。

### 支柱 ④ 對「SaaS 末日」的正面回應——他親口承認 switching cost 護城河會弱化

- 背景：Joe 在開場回顧 **2026 年的軟體板塊恐慌**——「Anthropic 宣布了某個**針對金融服務**的新東西，大家連內容都沒看就把金融服務股全砸下去」；Tracy 稱之為 **"SaaS apocalypse"**，並說「現在稍微平息了，但那份焦慮還在」。
- Boris 的回應框架＝ **Seven Powers**（Hamilton Helmer；⚠️ 轉錄全段把 **moat 誤植為 "mode"**，"cornered resource" 誤植為 "corner to resource"）：
  > "**some of these moats are going to get less important over the next couple years because of products like Claude Code.** If you want to port from vendor A to vendor B, you can ask Claude, 'hey, can you port me' and it'll just write the code."
  > （「**有些護城河會在未來幾年變得沒那麼重要，因為有 Claude Code 這類產品。** 你想從 A 廠遷到 B 廠，就叫 Claude 幫你遷，它會把程式寫出來。」）
- **但他的結論是「大體無恙」**：大公司從不只有一條護城河，通常是「轉換成本 ＋ 網路效應」或「轉換成本 ＋ cornered resource」；**護城河疊加後仍然強**。「有些會變不重要，但**大多數還是跟以前一樣有力**。」
- ⚠️ **利益衝突在這裡是雙向的、且互相抵銷了一部分**：
  - 一方面 Anthropic 有動機宣稱自己能顛覆軟體（提升自身敘事）；
  - 另一方面 **Salesforce 是他點名的 Claude Code 客戶**，他不能講「SaaS 要死」。
  - → **所以「switching cost 會弱化」這條坦白，是逆著他的商業利益講的，可信度相對較高；而「多重護城河仍然強」則是順著客戶關係講的，要打折。**
- **對「白牌／自建模型繞過供應商」的回應**：他明確不看好——「如果模型能力是靜態的，控制自有基礎設施可能有道理；**但前沿一直在動**，跟著前沿的上檔比較大。自建/自營 inference 是**很小眾的專業、工作量很大**。要是你只需要很小的模型，那就去用開源模型吧。」

### 支柱 ⑤ 「狐狸進雞舍」之爭：MSFT 與 Palantir 被點名

- Joe 直接點名兩個對手敘事的來源：**Microsoft CEO 的一則長推文**（語意模糊但暗示明確）、**Alex Karp 幾週前的 CNBC 專訪**（⚠️ 轉錄先誤作 "Scott Karp"）。核心指控：把 Claude 接進你的工作流，等於讓 Anthropic 學會你的生意，哪天它自己去開律所/開銀行——**不賣軟體了，直接賣服務**。
- Boris 的三段回應：
  1. **「先問問這些人的動機是什麼」**（訴諸對手利益衝突）。
  2. **技術性隱私承諾**：「使用者回報 bug 時，我身為工程師最想看他的對話——**但我看不到**。從客戶角度，可以有一個**可證明（provable）Anthropic 沒有任何人能看到該對話**的實例/帳號。」
  3. **前沿會繼續推進**（同支柱④）。
- ⚠️ **這三段全部是政策/立場陳述，無技術細節、無第三方認證名稱（未提 SOC2/ISO/BAA 等），「provable」的證明方式未說明。**「不作為既成事實引用。」

### 支柱 ⑥ 遷移／現代化：對 IT 服務業最直接的機制訊號

- **COBOL / 主機遷移**：Tracy 直球問「大銀行是不是終於能把 70 年的老程式碼搬進現代標準了？」Boris：**「確實有不少銀行正在用 Claude Code 做這類遷移。」**「Claude 很擅長遷移程式碼，這是核心能力之一，而且一直在進步。」
- 💣 **具體案例（本集唯一有時間/人力量化的硬案例）**：
  - **Bun 團隊的 Jared**（⚠️ 指 Bun 的 Jarred Sumner，**與 Anthropic 共同創辦人 Jared Kaplan 是不同人**，轉錄未區分）**一個人、約 11 天，把整個 Bun 程式庫從 Zig 遷移到 Rust**（Bun ＝ 驅動 Claude Code 的 JavaScript engine），用 Claude Code + dynamic workflows。
  - Boris：**「過去這要幾個工程師花一年左右，而且我們根本不會做」**——因為得停止開發一年，**沒有企業付得起這個代價**。
  - **成本**：Joe 說「我看到那篇文章了，好像只花了 **$150,000 的 credits**，是付那些工程師薪水的零頭」。⚠️ **這個數字是 Joe 回憶部落格文章講出來的，Boris 全程沒有確認也沒有否認**——不得當作官方數字引用。
- **經濟結構的改變**（他的歸納）：
  > "if in the past you had this big codebase and it wasn't cost-effective to stop development or to migrate everything to Java, you can now just do this."
  - ＝ **過去因為「機會成本太高而永遠不做」的技術債專案，現在的門檻降到可執行**。→ **這是 Jevons 在 IT 現代化市場的直接對應**（與 [[15-07-2026 法律業 Jevons 那集]] 同構）。
- **程式語言的相關性**：「我認為**今天就已經大體無關緊要了**……LLM 不在乎。」型別檢查/靜態分析對模型有幫助，但**模型愈強、這個幫助愈小**（「即使叫它直接寫組合語言，大概第一次就寫得很好」）。他預期未來是**新語言的寒武紀大爆發**，而非收斂到單一語言。

### 支柱 ⑦ 內部採用率與人力結構（對「開發者人力」的敘事輸入）

- **他個人：自 2025 年 11 月起，100% 的程式碼由 Claude Code 寫。**
- **產品線：Claude Code 本身、Co-work、所有產品，都用 Claude Code 寫**；基礎設施與研究程式碼的佔比持續上升。
- **全公司：「跨 Anthropic 我想平均大概是 90% Claude Code 之類的」** → ⚠️ 緊接著 Joe 問「**那 2%** 是什麼？」**90% 與 2%（＝98%）互相矛盾**，口徑不明（見 §四(4)）。
- **剩下由人手打的**：設定檔、兩個字元的小改動——「但我覺得這也會很快消失」。
- **Y Combinator batch 演講的舉手調查**（⚠️ 無樣本數、無時間點、無方法，屬軼事）：
  - 早期問「誰在用 Claude Code」→ 只有幾隻手；後來**每一隻手都舉**，於是他不問了。
  - 改問「**誰 100% 的程式碼都用 Claude Code 寫**」→ 第一次約 **1/4**；**現在「略多於一半」**；「我賭下次會是全部」。
- **角色重組（不是裁撤，是分化）**——他認為「工程師／設計／PM／使用者研究／資料科學」的舊分工正在瓦解，因為**人人都會寫程式了**（Claude Code 團隊裡設計師、PM、EM 都寫程式；設計師不必再叫工程師「幫我把按鈕移一個 pixel」）。取而代之的新分工：
  1. **prototypers** — 極快把第一個想法做出來
  2. **builders** — 把想法變成能上市的產品
  3. **maintainers** — 規模化後的維運
  4. **growers / scalers** — 把有 PMF 的產品放大 10x / 100x（**「這種人現在在 Anthropic 非常搶手」**）
  5. **sweepers**（他自稱找不到好名字，Joe 提議 **"perfectors"**）— 打磨產品/基礎設施/程式碼，去掉粗糙邊緣
- ⚠️ **全片沒有任何「工程師人數減少」的說法，也沒有任何 headcount 數據**。Anthropic 仍在招人（「growers 很搶手」）。**這是「AI 殺開發者職缺」敘事的一個中性/微反向的一手觀測，但完全沒有數據支撐。**
- **企業導入的組織摩擦**（Joe 問得很好）：在大公司裡，Slack 上有人問 icon 設計問題，**Claude Tag 未被 tag 就自己跳進來回答了**——「那個人的工作到昨天為止就是回答這個問題」。Boris **沒有正面回答摩擦問題**，改用 **1996 年 HBR 的 PC 生產力悖論**（電腦來了，為什麼公司沒享受到生產力提升？）：
  - 沒受益的公司：把電腦放在辦公室角落，**指派一個人負責跟電腦講話**，其餘流程照舊。
  - 受益的公司：**把電腦放中間**，把紙本全部數位化、丟掉檔案櫃，**一個瓶頸一個瓶頸地數位化，直到整個流程被翻新**。
  - 他的對應處方：**「不要拿 Claude 的答案去取代那個 icon 設計師——給那個設計師一千個 Claude，讓他成為世界上最強的 icon 設計師。」**
  - ⚠️ 這是**標準的廠商說詞**（把裁員問題轉譯成賦能問題），**沒有回答「大公司政治摩擦是否構成採用障礙」**。

### 支柱 ⑧ 安全／模型分層（含最強、也最不可稽核的宣稱）

- **prompt injection 競賽**：Anthropic 找**外部安全研究員/工程師**，**一週時間、$20,000 獎金**，要求對模型做提示注入。
  > "They were able to prompt inject **every single model except for our model** in Claude Code."
  - 出處：Boris 稱寫在 **Opus 4.8 與 Sonnet 5 的 model card** 上。
  - ⚠️ **自辦競賽、自付獎金、自家 model card 公布、無第三方驗證、無參賽者名單、無其他模型名稱、無方法論**。這是全片**最強的能力宣稱**，也是**最該重度折扣**的一條。
- **三層防護**（他的架構描述，這部分屬機制描述、可信度較高）：
  1. **alignment**（在模型裡）
  2. **neural probes**（mech interp 產物，偵測模型「正在被注入」的內部狀態）
  3. **auto mode**（在 Claude Code 裡的新權限模式，**不再有 yes/no 提示，而且更安全**）
- **sandbox**：限制模型只能存取你給的檔案與網站；**開源、且與任何 agent 相容**。**「會不會被突破？會，我們一直在找」**——紅隊、滲透測試，發現就修。→ **這句主動承認缺陷，判讀時加分。**
- **模型分層與配給**：
  - **Mythos** ＝ 能力更高、風險更高的模型（**非常擅長找 zero-day 漏洞與 exploit**），因此走 **Project Glasswing** 白名單、涉及**出口管制/白宮**議題；「如果第一天就給所有人 Mythos，大家就都去駭客了；**要先給好人、給他們一段領先時間**」。
  - **Fable** ＝ **「我用的那個 Mythos 版本」**，拿掉了那些駭客能力，**現在人人可用**。
  - ⚠️ **Joe 的前提「我們知道 compute 是稀缺的，否則 Fable 不會只在某段期間當預設」——Boris 沒有確認也沒有否認**，只答「everyone gets access」。**這個「不否認」本身是一條弱訊號（產能配給），但不可當事實。**

### 支柱 ⑨ 幾條主持人拋出、來賓沒有正面回答的問題（判讀價值高）

| 問題 | 提問者 | 來賓的實際回應 |
|---|---|---|
| **model collapse**：網路已被 AI 生成程式碼灌滿，訓練資料被污染，會影響進步曲線嗎？ | Joe | ⚠️ **完全沒回答**。改談 scaling laws 論文（8–10 年前）、Anthropic 創辦人（Dario、Sam、Jared）是該論文作者、「scaling laws 非常平滑、**甚至看起來有點在加速**、比八年前猜的還好、Fable 上依然成立」。**零證據，且答非所問。** |
| **企業內部的政治摩擦會不會擋住採用？** | Joe | 轉成 1996 HBR PC 生產力悖論 + 「給設計師一千個 Claude」。**未回答摩擦本身。** |
| **compute 稀缺是不是導致配給？** | Joe | 答「everyone gets access」＋轉向企業按 token 計費。**未否認稀缺。** |
| **Claude Code 對 Anthropic 業務貢獻多少？** | Tracy | 「it's a big contributor to the Anthropic business」＋立刻轉向「但它有多重目的，**最大的是學習安全**」。**零數字。** |
| **AI 寫作為什麼不好？是優先順序問題還是 coding 有可驗證性這個本質差異？** | Joe | 反駁前提：「**coding 其實也不是非黑即白**」（能跑但很醜、能跑但一週後會壞、能跑但沒人想讀），並**承認 Claude 的寫作「可以好很多」**。→ 誠實加分。 |

---

## 二、核心數據表（每列標出處性質；⚠️＝需折扣）

```
項目                  | 數字/內容                          | 出處性質 / 可驗證度
----------------------+-----------------------------------+----------------------------
來賓身分              | Boris Cherny,Anthropic            | 可查證;Anthropic Labs 出身
                     | Claude Code 創造者/負責人           | (該團隊做 CC/MCP/Skills/桌面app)
成長拐點              | Opus4+Sonnet4(2025-05)、Opus4.5    | ⚠️ 自述,無基數、無絕對值
                     | (2025-11)、Opus4.6(2026-02)、Fable | 「growth inflected」×4
                     | 四次「成長拐點」                     | 私人公司,不受揭露責任約束
harness vs 模型歸因    | 「幾乎全是模型」                     | 自述;⚠️ 與他自己論證 harness
                     | ("it's almost all the model")     | 差異化的段落互相矛盾
💣 企業計價偏好        | 「企業通常不用有 rate limit 的訂閱, | ✅ 產品端可觀察事實
                     | 通常偏好 pay-per-token」            | 本集對我方最有價值的一句
                     | 理由:可控/可預測/不撞上限            | 但≠應用層 SaaS 的 seat 會崩
併發 agent 階梯        | 1 → 10 → 100 →「some 客戶 1,000    | ⚠️ 自述;「some」=極端值
                     | Claudes / 工程師」                  | 無客戶數/分布/中位數/時間軸
Boris 個人並發         | 「隨時幾個,有時幾百、有時幾千」       | ⚠️ 自述軼事
Boris 個人程式碼       | 自 2025-11 起 100% 由 CC 撰寫       | ⚠️ 自述,口徑不明
Anthropic 全公司       | 「平均大概 90% Claude Code」        | ⚠️ 自述;緊接 Joe 說「那 2%」
                     |                                   | → 90% vs 98% 矛盾,口徑不明
人手仍打的部分         | 設定檔、兩字元改動;「會很快消失」     | 自述
YC batch 舉手調查      | 「100% 用 CC 寫」:約 1/4 → 現在     | ⚠️ 軼事;無樣本數/時點/方法
                     | 「略多於一半」;賭下次全部            |
prompt injection 競賽  | 外部研究員、1 週、$20,000 獎金;      | ⚠️ 自辦/自付/自家 model card
                     | 「除我們之外每個模型都被注入成功」    | 無第三方驗證、無參賽/對手名單
                     | (稱載於 Opus 4.8 / Sonnet 5 卡)     | ← 全片最強宣稱=最該折扣
安全三層              | alignment + neural probes +       | 機制描述,可信度較高
                     | auto mode(無 yes/no 提示且更安全)   |
sandbox              | 開源、與任何 agent 相容;            | ✅ 主動承認缺陷 → 加分
                     | 「會被突破,我們持續紅隊/滲透測試」    |
設定項數量            | 「應該有好幾百個,大概 400–500」      | 自述,約數(可被產品文件驗證)
💣 Bun 遷移案         | 1 人、約 11 天,Zig → Rust 全庫       | 有部落格可查;⚠️ 執行者是
                     | (過去=數名工程師約 1 年,且「根本    | Bun 的 Jarred Sumner,非
                     | 不會做」)                          | Anthropic 共同創辦人 Jared Kaplan
Bun 遷移成本          | 「約 $150,000 的 credits」          | ⚠️ Joe 憑記憶轉述部落格,
                     |                                   | Boris 未確認亦未否認 → 勿引用
COBOL/主機遷移        | 「確實有不少銀行在用 CC 做這類遷移」  | 自述,無客戶名、無規模
客戶名單              | Airbnb、Ramp、Salesforce、NASA、    | 具名(可被否認)→ 可信度較高
                     | 「紐約最大幾家銀行」「最大幾家藥廠」  | ⚠️「Deoid」轉錄不明,勿引用
介面分布              | CLI + 各大 IDE 擴充 + 桌面 app +    | ✅ 產品事實
                     | iOS/Android + Slack(Claude Tag)    | 他自己「絕大多數不用終端機」
                     | 本人主力=Slack,之前是 iOS          | → 反直覺,對 CLI 敘事是修正
Claude Tag           | 「有 session 連續跑了數週」;         | ⚠️ 自述;Slack demo 有實際
                     | 未被 tag 主動跳進 thread、跨查      | 螢幕展示(可看 YouTube 覆核)
                     | Datadog + BigQuery、產出設計 mockup |
商業貢獻              | 「a big contributor to the         | ⚠️ 零數字;立刻轉向
                     | Anthropic business」               | 「最大目的是學安全」
模型分層              | Mythos(擅長找 zero-day,走 Project  | 自述;出口管制/白宮已解決
                     | Glasswing 白名單) / Fable(去掉      | ⚠️ Joe 的「compute 稀缺」
                     | 駭客能力,GA)                       | 前提未被否認 → 弱訊號
scaling laws         | 「非常平滑,甚至有點在加速,          | ⚠️ 零證據;且用它迴避了
                     | Fable 上依然成立」                  | model collapse 的提問
護城河觀點            | 「switching cost 這類護城河會       | ✅ 逆自身利益的坦白 → 加分
                     | 因 Claude Code 而變不重要」          | (「叫 Claude 幫你遷廠商」)
                     | 「但大公司是多重護城河疊加,          | ⚠️ 順客戶關係的說法 → 折扣
                     | 大多數仍跟以前一樣強」               | (Salesforce 是他的客戶)
SaaS 恐慌事件         | 「Anthropic 發布金融服務相關新東西,  | Joe 敘述的 2026 市場事件
                     | 大家沒看內容就砸金融服務股」         | Tracy 稱 "SaaS apocalypse"
自建/開源替代         | 明確不看好:前沿會動、自營 inference | 立場陳述;有 talking-book
                     | 是小眾專業且工作量大;「只需要小模型  | 成分(他賣的就是前沿模型)
                     | 就去用開源吧」                      |
程式語言              | 「今天就已經大體無關緊要」;預期      | 觀點,非數據
                     | 新語言「寒武紀大爆發」              |
新角色分工            | prototypers / builders /          | 觀點;⚠️ 全片無 headcount
                     | maintainers / growers(scalers,    | 數據、無「工程師變少」的說法
                     | 「Anthropic 現在非常搶手」)/         |
                     | sweepers(Joe 提議 "perfectors")    |
```

---

## 三、對投資標的的映射（本 digest 對我方最有價值的一段）

```
受影響對象              | 本集提供的證據                       | 方向        | 證據強度
------------------------+-------------------------------------+------------+------------------
軟體業(整體敘事)         | 來賓親口:「switching cost 這類護城河  | 微偏空(敘事)| 中低。框架式意見,
「AI 是否顛覆軟體」       | 未來幾年會變不重要——叫 Claude 幫你    |            | 零數據。但因逆其
                       | 從 A 廠遷到 B 廠即可」               |            | 商業利益 → 加分
                       | 但:「大公司多重護城河疊加,大多數     | 中性/微偏多 | 低。Salesforce 是
                       | 仍跟以前一樣強」                     |            | 其客戶 → 重度折扣
------------------------+-------------------------------------+------------+------------------
SaaS 定價模式            | 💣「企業通常不用有 rate limit 的訂閱, | 偏向        | 中高(本集最硬)。
(seat vs consumption)   | 通常偏好 pay-per-token」;企業要的是  | consumption | 產品端可觀察事實,
                       | 可控/可預測/不撞上限                 |            | 非成長宣稱。
                       | 企業治理層全為用量而生:spend        | 同上        | ⚠️ 但 Claude Code
                       | controls / advisor models /        |            | 賣的是模型產能,
                       | enterprise effort levels           |            | 與應用層 SaaS 非
                       |                                     |            | 同構 → 類比證據
------------------------+-------------------------------------+------------+------------------
IT 服務 / 系統整合       | Bun:1 人 11 天完成 Zig→Rust 全庫遷移  | 偏空        | 中(有可查部落格)。
(ACN 型)                | (過去=數名工程師 1 年,且「根本不會做」)|            | ⚠️ 單一案例、執行
                       |                                     |            | 者是頂尖工程師、
                       |                                     |            | 遷移對象是自家庫
                       | 「不少銀行正用 Claude Code 做 COBOL/  | 偏空        | 低。無客戶名、無
                       | 主機遷移」                           |            | 規模、無成功率
                       | 機會成本結構改變:過去「停開發一年     | 偏空(對人力  | 中。機制論證清晰,
                       | 沒人付得起」而永遠不做的技術債專案,   | 套利中介)   | 且與 15-07 法律業
                       | 現在門檻降到可執行                   | 偏多(對總量)| Jevons 那集同構
------------------------+-------------------------------------+------------+------------------
半導體 / inference 需求  | 採用階梯 1 → 10 → 100 →「some 客戶   | 偏多        | ⚠️ 低。無絕對值、
(四拆 a:下游會不會花)    | 1,000 agents/工程師」                |            | 無分布,「some」=
                       |                                     |            | 極端值,賣方自述
                       | 抽象層再上一層:人→模型→模型→原始碼   | 偏多        | 低。機制敘事,無量
                       | (loops/routines/Tag);Tag session    |            |
                       | 「連續跑數週」                       |            |
                       | Joe 的「compute 稀缺」前提未被否認    | 偏多(弱)    | 極低。不否認≠承認
                       | 四次成長拐點綁模型發布               | 偏多        | ⚠️ 極低。無基數
------------------------+-------------------------------------+------------+------------------
開發者人力              | 角色分化(prototyper/builder/        | 中性        | 低。觀點,零數據。
                       | maintainer/grower/sweeper)而非裁撤;  |            | ⚠️ 但「無裁員說法」
                       | 「growers 在 Anthropic 非常搶手」     |            | 不等於「無裁員」
                       | 非工程角色也寫程式(設計師/PM/EM)     | 偏空(對初階 | 低。單一團隊軼事
                       |                                     | 專職工程)   |
                       | 全片無任何 headcount 數字            | ——          | 缺口本身值得記錄
------------------------+-------------------------------------+------------+------------------
MSFT / PLTR(競爭敘事)    | 兩者被點名在推「別讓狐狸進雞舍/       | ——(僅記錄)  | 中。事件可查證,
                       | 用你自己託管的開源模型」               |            | 但雙方皆有動機
                       | Boris 回應:動機質疑 + 可證明的零存取  | ——          | 低。政策陳述,無
                       | + 前沿會繼續推進                     |            | 技術細節/認證名
```

---

## 四、⚠️ 資料衛生

### （1）無出處 / 自我宣稱 / 估計

1. **四次「成長拐點」** — 無基數、無絕對值、無時間序列。私人公司口中的「growth inflected」**不具任何可比性**，不得作為 Anthropic 業務規模的推論基礎。
2. **「1 → 10 → 100 → 1,000 agents 每工程師」** — 「**some** customers」。這是**分布的右尾**，被講成階梯的終點。**無客戶數、無中位數、無時間軸**。任何據此推 token 需求量的計算都是憑空放大。
3. **「Anthropic 平均約 90% 程式碼由 Claude Code 寫」** — **口徑完全未定義**（行數？commit 數？PR 數？含不含生成後人工修改？），且與 Joe 緊接著的「那 2%」矛盾。
4. **prompt injection 競賽「除我們外全部被攻破」** — Anthropic **自辦競賽、自付 $20,000 獎金、結果登在自家 model card**。無第三方驗證、無參賽者名單、無對手模型名稱、無攻擊面定義。**這是全片最強的競爭定位宣稱，也最該歸零處理。**
5. **「scaling laws 非常平滑、甚至有點在加速」** — 零證據，且**是用來迴避 model collapse 提問的**。
6. **「$150,000 的 credits」（Bun 遷移成本）** — **Joe 憑記憶轉述部落格，Boris 全程未確認**。不得引用為官方數字。
7. **「Claude Code 是 Anthropic 業務的重要貢獻者」** — **零數字**，且立刻轉向「但最大的目的是學習安全」。
8. **YC batch 舉手調查** — 無樣本數、無時間點、無提問方法（公開舉手有嚴重的社會壓力偏誤，且 YC batch 是**極端 early-adopter 樣本**，對整體開發者母體無代表性）。
9. **客戶名單（Airbnb / Ramp / Salesforce / NASA / 大型銀行 / 大型藥廠）** — **具名部分可信度較高**（若不實，對方可否認），但**沒有任何滲透率、席次數、支出金額**。「NASA 用 Claude Code」與「NASA 全面採用」是天差地別的兩件事。

### （2）結構性利益衝突（本集最大的判讀風險）

- **來賓是 Anthropic 員工，談的是他自己創造、自己負責的旗艦產品。** 這比 07-13 那集的律所主席（legaltech 的**買方**）在偏誤等級上高一整個數量級——那位至少沒有動機吹捧他採購的軟體，**Boris 的每一句成長宣稱都直接對應他的 KPI、產品聲量與 Anthropic 的募資敘事**。
- **Anthropic 是私人公司**：本集所有數字**不受任何財報揭露責任約束**，也無從對帳。
- **⚠️ 最大的具體風險：把「產品行銷語言」當「產業結構事實」。** 本集大量的敘事（抽象層兩次躍遷、product overhang、採用階梯、角色分化、1996 HBR 類比）**在修辭上極具說服力，但幾乎全部沒有數據支撐**。這些是**用來說服企業採購與投資人的框架**，不是產業統計。
- **偏誤方向的兩個例外（判讀時加分）**：
  1. **「switching cost 護城河會弱化」是逆自身客戶關係的坦白**（Salesforce 是他的客戶）→ 這條反而**比他「多重護城河仍強」的安撫更可信**。
  2. **主動承認 sandbox 會被突破、承認 Claude 寫作「可以好很多」、承認「幾乎全是模型不是 harness」**（等於貶低自家 harness 的差異化）→ 這三處自我設限降低了整體 hype 濃度。
- **主持人側**：Joe 與 Tracy 都是 Claude Code 的日常使用者（Joe 用它整理桌面截圖；Tracy 承認「不看提示直接按 yes」），**開場即是產品讚詞**。全集**沒有任何空方來賓或反方觀點**，Joe 雖有幾個尖銳提問（model collapse、政治摩擦、compute 稀缺），但**沒有一次追問到底**。

### （3）轉錄錯字對照（模型名/產品名誤植極嚴重，勿以錯字檢索或引用）

```
轉錄                          | 正確
------------------------------+-----------------------------------------
quad code / cloud code /      | Claude Code
claw code / clod code / plot  | ← 全片主產品名,至少 5 種拼法
code / "quad" / Clawbot /     | Claude
Claudebot                     |
Enthropic / anthropic         | Anthropic
Boris Churnney / Bchurnney    | Boris Cherny / @bcherny
Tracy Aloway / Tracy Alaway   | Tracy Alloway
All Thoughts / Odd Thoughts / | Odd Lots
OddLoss / odlotss / odblotss  | (bloomberg.com/oddlots)
sonnet 3.5 / "sauna 3.5"      | Sonnet 3.5
"opus 4.5 in may in uh in     | Opus 4.5 in November ← 說者當場自我更正
November"                     | (勿誤讀為五月)
opus 4.6 six                  | Opus 4.6
"MCP skills"                  | MCP(Model Context Protocol)與 Skills
                             | ← 是兩個東西,轉錄連寫成一個
quad tag / TAG / Clawbot      | Claude Tag(Slack 內的 Claude)
co-work                       | Co-work(產品名,轉錄一致但未在本文獨立驗證)
mythos / project glasswing    | Mythos / Project Glasswing
                             | ← 轉錄一致,但無法獨立確認拼法
"modes"(seven powers 全段)     | moats(護城河) ← ⚠️ 最誤導的一處,
                             | 該段每個 "mode" 都要讀作「護城河」
"corner to resource"          | cornered resource(Seven Powers 之一)
"scaling loss" / "scaling WS" | scaling laws
cobalt                        | COBOL
Zigg                          | Zig(程式語言)
bun                           | Bun(JavaScript runtime/engine)
"Jared on the Bun team"       | Jarred Sumner(Bun 作者)
                             | ⚠️ 與 Anthropic 共同創辦人 Jared Kaplan
                             | 是不同人,轉錄與對話都未區分
"Daario" / "Sam" / "Jared"    | Dario Amodei / Sam McCandlish(首任 CTO)
(scaling laws 論文作者段)      | / Jared Kaplan
Steve Waznjak                 | Steve Wozniak
Scott Karp → 說者自我更正      | Alex Karp(Palantir CEO)
Fizer                         | Pfizer
Y cominator patches           | Y Combinator batches
data dog                      | Datadog
"perceived spend controls"    | 疑為 preset spend controls ⚠️ 轉錄不清
"Deoid"(客戶名單中)            | ⚠️ 無法還原,勿引用
"one shot of this"            | one-shotted this
"coral areas"                 | corollaries(推論)
"wet wet quad answer"         | ⚠️ 轉錄不清,勿引用
"lingual franka"              | lingua franca
"nonInative"                  | non-AI-native(非 AI 原生的公司)
aronomy                       | agronomy
"247"                         | 24/7
unhobble                      | ✅ 正確(AI 圈既有用語,非錯字)
```

### （4）內容張力與口徑

- **💣 90% vs 2% 的直接矛盾**：Boris 說「跨 Anthropic 平均大概 **90%** Claude Code」，Joe 下一句就問「**那 2%** 是什麼？」→ 要嘛 Boris 實際說的是 98%、要嘛 Joe 聽錯。**兩個數字差了 5 倍的人力殘量**。⚠️ **不得引用單一數字，只能寫「90–98%，口徑不明」。**
- **「幾乎全是模型」vs「harness 是我們的差異化」**：他先花大段論證 auto mode / sandbox / 權限提示是 Claude Code 的護城河，被問到成長歸因時卻說 "it's almost all the model"。**兩者都是他的真實立場**——正確的讀法是：**成長由模型驅動，但留存/企業信任由 harness 與安全層驅動**。只引用其中一半都是斷章。
- **「switching cost 會弱化」vs「大多數護城河仍跟以前一樣強」**：同一段話裡的兩個方向。⚠️ **任何把本集當成單向「AI 利多/利空軟體」的引用都是誤讀。**
- **model collapse 的提問被完全迴避**：這是本集唯一觸及「進步曲線是否會鈍化」的問題，**他答的是 scaling laws（訓練規模），不是訓練資料污染**。→ **AI 進步持續性的空方論點在本集完全沒有被回應，不能當成「已被駁斥」。**
- **compute 稀缺的不否認**：Joe 明確以「我們知道 compute 是稀缺的，否則 Fable 不會只在某段期間當預設」作為提問前提，Boris **沒有反駁這個前提**。→ 弱訊號，**不否認 ≠ 承認**，但值得記錄。
- **CLI 敘事的自我修正**：外界（含 Tracy 的提問）預設 Claude Code ＝ 終端機工具，Boris 明確說**他本人「絕大多數時候不用終端機」，主力是 Slack，之前是 iOS**。→ **對「agentic coding 是開發者小眾工具」的認知是一個實質修正**（介面已擴散到非工程角色）。
- **錄製日 vs 發布日**：全片無明確錄製日期自述，僅以「上個月/去年十一月/二月」等相對表述。所有「現在」一律以**發布日 2026-07-20** 為基準。

---

## ROMA 對照註記

> **一句話定位**：本集是「AI 是否顛覆軟體」這條主線上**罕見的一手產品端輸入，但來自賣方**。它**只改敘事層的解析度，不改我方三層 de-rate 的分層結論**——因為它**沒有提供任何 NRR / cRPO / 毛利率層級的數據**，而那才是我方的判別 SSOT。

### 1️⃣ [[project_software_sector_frame]] — 落在哪一層、支持還是反對

我方框架：軟體 de-rate 分三層＝**①IT 服務 ACN 真減損／②seat-based NOW 待判決／③consumption SNOW 錯殺已修復**；判別 SSOT ＝ **NRR / cRPO 軌跡**；且「ERP 被 AI 顛覆」論已於 2026-05（revision ＋ SNOW Q1 FY27 NRR 126%、+37% gap）**證偽**。

**逐層判定：**

- **第①層（IT 服務 / ACN 型「真減損」）→ 本集是【支持 de-rate】的證據，且是本集最實的一段。**
  - 機制對映：ACN 的核心收入池是**遷移／現代化／系統整合的人力套利**。本集提供了兩個直擊該收入池的觀測：
    - **Bun：1 人 11 天完成 Zig→Rust 全庫遷移**（過去＝數名工程師 1 年）；
    - **「不少銀行正用 Claude Code 做 COBOL / 主機遷移」**——COBOL 現代化正是 IT 服務業最經典、單價最高、最依賴稀缺人力的專案類型。
  - **更關鍵的是機會成本結構的改變**：「過去停止開發一年沒有企業付得起，所以**根本不做**」→ 現在門檻降到可執行。
    - ⚠️ **注意這是雙向的**：它同時意味著**遷移專案的總量會暴增**（Jevons）。所以對 ACN 的正確判讀不是「遷移市場消失」，而是**「單專案人力價值崩塌、專案件數上升」**——與 [[15-07-2026 法律業 Jevons 那集]] 完全同構。**能不能守住，取決於 ACN 能否把收費從『人天』切換到『成果』**。
  - **不改結論**：①層真減損維持。本集**強化了機制描述的精確度**，但**沒有給任何 ACN 的財務數據**，不構成加碼/減碼理由。
- **第②層（seat-based / NOW 型「待判決」）→ 本集提供了一條【方向性偏向 consumption】的類比證據，但不足以下判決。**
  - 💣 **最有價值的一句**：**「企業通常不用有 rate limit 的訂閱方案，通常偏好 pay-per-token；因為這樣他們能控制、能預測、工程師不會撞上限。」**
  - **對②層的類比價值**：這說明**企業在採購 AI 產能時的心智模型已經是「買 compute」而非「買席次」**，且他們**主動選擇了帳單波動、放棄了固定費用的確定性**——理由是**不要天花板**。這與 seat-based 的核心價值主張（可預算、固定、人頭綁定）方向相反。
  - **⚠️ 但必須嚴格設限，不可直接套到 NOW：**
    1. **Claude Code 賣的是模型產能本身，沒有 seat 的物理意義**——它「偏好 token」是產品性質決定的，不是企業採購偏好的普遍轉向。這是**類比證據，不是同構證據**。
    2. **NOW 型 seat-based 的真正判決點不在計價偏好，而在 seat 數與 NRR/cRPO 軌跡**。本集**零數據**。
    3. 本集也**沒有任何「AI 讓白領席次減少」的證據**——反而 Anthropic 自己在招 growers/scalers，且 Boris 說**設計師、PM、EM 現在也都在寫程式**（＝**新增了非工程角色的工具使用者**，對 seat 數是中性偏正）。
  - **要新增的觀察維度**（延續 15-07 那集已提出的）：seat-based 廠商的 **AI 功能是收固定加價還是 usage-based？其 COGS 是否隨 token 用量上升？** 若企業側的 AI 預算普遍走 consumption，**seat-based 廠商夾在「固定收入 vs 浮動成本」中間，毛利率壓縮會早於 NRR 鬆動出現**。
  - **結論：②層維持「待判決」。NOW ＝下一個 SNOW 候選的判斷不因本集改變。**
- **第③層（consumption / SNOW 型「已錯殺、已修復」）→ 本集是【方向性支持】，但只在敘事層。**
  - 「企業偏好 pay-per-token」＋「1 → 1,000 agents」＋「模型指揮模型的長時間任務」＝ **consumption 模式的多頭原型**：**單價下降不代表營收下降，只要用量彈性 > 1**。
  - **這與 2026-05 對「ERP/軟體被 AI 顛覆」的證偽是同一個方向**：AI 不是把軟體支出抽走，而是**把支出的計量單位從席次換成用量**。
  - ⚠️ **但本集不提供任何 SNOW 型公司的數據**，也**不改變我方「錯殺已修復」的既有結論**——那個結論的 SSOT 是 SNOW 的 NRR 126%／+37% gap，不是本集。
- **⚠️ 全局紀律：本集是敘事層，不改分層結論。**
  - 本集**沒有一個數字可以進入估值模型**（無 NRR、無 cRPO、無毛利率、無 seat 數、無 ARR）。
  - 任何「Claude Code 很強所以做空軟體」或「來賓說 SaaS 護城河還在所以做多軟體」的引用，**都是把行銷語言當結構事實**——而且來賓自己在**同一段話裡講了兩個方向**。
  - 依 [[feedback_conservative_base_pe_no_rerating]]：**不因本集上修或下修任何框架 P/E**。

### 2️⃣ [[project_nvda_hyperscaler_coupling_frame]] 四拆 (a)「下游會不會繼續花」

- **本集提供的是 (a) 的機制證據，不是數據證據。** agentic coding 的 token 消耗若真在爆發，就是 **inference 需求耐久性的下游拉力**：
  - **並發量階梯 1 → 10 → 100 → 1,000 agents/工程師**；
  - **抽象層再上一層**（人 → 模型 → 模型 → 原始碼），單位任務的 token 消耗呈**乘法而非加法**成長；
  - **長跑型 session**（Claude Tag「連續跑數週」）＝ 從「一問一答」到「持續佔用推理產能」的形態轉變；
  - **介面擴散到非工程角色**（設計師/PM/EM 都在用）＝ 使用者母體擴大；
  - **Joe 的「compute 稀缺」前提未被否認**＝ 產能受限的弱訊號。
- 🚫 **但依 [[feedback_capex_commitment_vs_annual_spend]]：一方自我宣稱的成長率絕不得當作 capex 判斷依據。**
  - 本集**沒有任何絕對 token 量、沒有營收、沒有客戶數、沒有分布**；「some 客戶 1,000 agents」是**右尾極端值被講成階梯終點**，正是該筆記警告的「用極端值/總承諾冒充當期實際」的同型錯誤。
  - **四拆 (a) 的判別口徑不變：hyperscaler「當年度實際 capex vs 當年度指引」**。本集**任何數字都不得進入該判斷**。
- **正確用途**：本集只能用來回答**「這條需求的機制上說得通嗎」**（答：說得通，且形態正在從對話轉向長跑型 agent），**不能用來回答「這條需求有多大、能撐多久」**。
- 與 [[project_nvda_structural_cheap]] 的關係：**不構成任何估值調整輸入**。

### 3️⃣ [[feedback_data_source_priority]]

- 本集是**敘事/機制輸入，非數據層，絕不作交易依據**。
- 品質定位：**低於 15-07 那集的律所主席**（他是買方、且會自我打臉），**遠低於任何財報/SG 結構化資料**。理由：**賣方員工談自家旗艦產品、私人公司無揭露責任、全片零絕對數字、無反方觀點、主持人未追問到底**。
- 唯一該當一手事實對待的：**產品機制（介面/設定/權限模式/sandbox）與計價結構（企業偏好 pay-per-token）**。其餘一律折扣。
- 任何牆位／財報日／Garch／IVR／DPI 仍一律回 **SG data_table** 覆核（[[feedback_wall_levels_ssot_sg_data_table]]）。

---

## 可證偽點（追蹤清單）

1. **Anthropic 是否揭露 Claude Code 的絕對規模**（ARR／token 量／客戶數／席次數）。
   - 目前**零揭露**。若日後（募資揭露、Bloomberg/The Information 報導、或 IPO 文件）出現的絕對數字，與「四次成長拐點」「1,000 agents/工程師」所暗示的量級**明顯不相稱**，則本集的成長敘事整體降級。
   - **這是本集所有宣稱的共同上游證偽點，優先級最高。**
2. **seat-based 廠商（NOW / CRM）的 seat 數、NRR、cRPO 與毛利率軌跡**（SSOT 不變）。
   - 特別注意 **Salesforce 被 Boris 點名為 Claude Code 客戶**——一家自身賣 seat、同時大量採購 consumption 型 AI 產能的公司，是②層最乾淨的觀察樣本。
   - **證偽門檻**：若 CRM/NOW 的 **NRR 走弱且毛利率先於 NRR 出現壓縮**，則「seat-based 被夾在固定收入 vs 浮動 AI 成本之間」成立；若 NRR 與毛利率同時穩住，則本集的 consumption 敘事對②層無傳導。
3. **其他廠商的計價模式是否同向遷移**——Microsoft Copilot（per-seat $30 → credits/consumption）、Google、以及應用層（Harvey 等）的定價公告。
   - 若**一年內出現三家以上主流企業 AI 產品從 per-seat 轉 consumption/credits**，則「企業偏好 pay-per-token」從單一廠商證言升級為產業趨勢；若沒有，則本集這句只是 Claude Code 的產品特性。
4. **IT 服務業（ACN 及同業）的遷移/現代化業務指標**：book-to-bill、bookings 中 modernization 佔比、以及**管理層對 pricing 的評論**（是否出現「客戶要求以成果計價」「單專案人天下降」）。
   - **證偽門檻**：若 ACN 的 modernization bookings **件數上升而總額持平/下降**，則本集「單價崩、件數增」的 Jevons 機制在 IT 服務業被證實；若總額同步成長，則遷移市場的 pie 擴張蓋過單價下跌。
5. **Opus 4.8 / Sonnet 5 model card 的 prompt-injection 競賽結果是否有第三方復現或反駁**（獨立安全研究團隊、學術論文、競品公開回應）。
   - 若無人復現、或有對手模型廠商公開反駁，該宣稱歸零。
6. **開發者職缺數據**（Indeed/LinkedIn 軟體工程職缺指數、大型科技公司揭露的工程 headcount）。
   - **證偽門檻**：本集主張「角色分化而非裁撤」。若 2026H2–2027 初階軟體工程職缺出現**明顯結構性縮編**，該主張被證偽；若職缺持穩而職能描述向「orchestrator/prototyper」轉移，則本集的角色分化論被支持。
7. **compute 配給的公開跡象**：Fable 的預設期限、rate limit 政策變動、企業客戶的產能保證條款。
   - 若出現明確的產能配給（而非行銷式限時），佐證「compute 稀缺」→ 對四拆 (a) 是機制支持，但**仍須回當年度 capex 實際 vs 指引覆核**。
8. **model collapse / 訓練資料污染**：本集完全迴避了這個問題。追蹤是否有獨立研究顯示 AI 生成程式碼污染開源訓練資料、進而影響編程模型的進步斜率。
   - **這是本集唯一被提出卻未被回答的空方論點，不能因為「來賓沒回答」就當它不存在。**
