# SpotGamma — Key Levels 系列（#1–7 合併）：6 大訊號 / MM / Delta / Gamma / Call·Put Wall / Vol Trigger

> **來源性質**：SpotGamma 官方教學系列「Key Levels」#1–7。SpotGamma 是本系統主數據源之一（SG_DIR），方法論與 ROMA opportunities 模組同源——**教學價值高於一般博主**，屬常青(evergreen)知識庫素材，無時效多空傾向。

---

## 縮寫對照
| 縮寫       | 全稱                    | 說明                                                         |
|------------|-------------------------|--------------------------------------------------------------|
| MM         | Market Maker            | 造市商；期權交易對手方，靠買賣價差賺錢、不做方向性賭注        |
| Delta      | Delta                   | 期權對標的價格的敏感度；MM 為避險需買賣的股數比例             |
| Gamma      | Gamma                   | Delta 的變化率；衡量避險壓力隨價格/時間如何「動態」演變       |
| Call Wall  | Call Wall               | SG 自創；最強阻力位，賣方/獲利了結/做空集中區                 |
| Put Wall   | Put Wall                | SG 自創；最強支撐位，買方/進場集中區                          |
| Vol Trigger| Volatility Trigger      | SG 自創；正/負 gamma 環境的分界線                            |
| Spot Price | Spot Price              | 任何金融工具的現價                                           |
| bps        | Basis Points            | 基點，1 bps = 0.01%                                          |
| S&P        | S&P 500                 | 標普 500 指數                                               |
| OCO        | One-Cancels-Other       | 二擇一掛單（ROMA squeeze 雙觸發策略用語）                   |

---

## 一句話總結
**SpotGamma 主張市場價格被「造市商避險流」推動——透過 MM→Delta→Gamma 三層機制，再落地成 Call Wall（阻力）、Put Wall（支撐）、Vol Trigger（正/負 gamma 分界）三條每日水位，讓交易者在開盤前就看出哪裡會turn、哪裡波動會放大。**

## 重點（逐主題）

### #1 6 Signals That Move The Markets
- 整個系列拆解 6 個 SG 核心術語，分兩組：
  - **產業通用概念**：Market Maker、Delta、Gamma（交易業界既有的核心概念）。
  - **SG 多年前自創、後被業界採用**：Call Wall、Put Wall、Volatility Trigger。
- 定位：給期權 flow 新手或剛上 SG 平台的人，先把這 6 個定義打底，之後才能「cut through the noise」、更快理解平台指標、預判市場走勢。

### #2 Market Makers
- **核心定義**：你每次買期權，總有人賣給你——對手方幾乎都是 MM。
- **運作機制**：MM 不跟你對賭，只賺每筆交易的小價差(spread)，隨市場準備好買或賣期權；為了**不承擔方向性風險**，會用「hedging（避險）」——最常見是用**買賣股票**來對沖賣給你的期權。
- **實例（Amazon）**：你買 10 張 Amazon call，MM 透過券商賣給你後，會接著去買「特定股數」的 AMZN 股票，以降低/消除自身方向性風險。
- **讀盤價值**：SG 專有模型揭露 MM flow 如何造成「可預測的價格行為」——理解 MM 持倉(positioning)就是交易優勢來源。

### #3 Delta
- **核心定義**：Delta 告訴你 MM 交易完一筆期權後，為了維持中性(neutral)需要買/賣**多少股**。
- **運作機制**：Delta 是公開、有完整文件的數學計算（不是秘密），通常你的交易平台在期權旁就會顯示。它定義「中性比例(neutral ratio)」——MM 每賣一張期權需對沖的股數。
- **讀盤價值**：理解後可預判動能(momentum)會在哪裡累積，提前卡位。（片中說計算細節「a bit later」再講，此處只給 TL;DR。）

### #4 Gamma
- **背景**：SpotGamma 由 Brent Cachuba 於 2020 年創立，宗旨是揭露 MM 避險流如何影響股價、幫交易者「破解華爾街劇本」。
- **核心定義**：Delta 只講「單一時點」要買賣多少股，**抓不到曝險如何隨價格與時間變化**；Gamma 正是衡量「避險壓力如何動態演變」。
- **威力**：這種 shift 能讓市場快速移動——片中以 **GameStop squeeze** 為例。
- **SG 做法**：套用 20+ 年專有演算法，追蹤「每一個 spot price」上的買賣壓力，提供機構級洞察。
- **命名由來**：現價=spot price，加上衡量避險壓力位移的 gamma → 「Spot Gamma」=追蹤每個現價上買賣壓力的平台。Gamma 正是 Call Wall / Put Wall / Vol Trigger 三條水位的動力來源。

### #5 Call Wall
- **核心定義**：SG 最重要水位之一；**最強阻力位**，賣方進場處——交易者常在此**獲利了結、做空股票、或在其上方賣期權**。
- **產生方式**：每天清晨 **5:00 a.m. 前**對數百萬資料點跑數學運算，為每個美股指數與個股算出當日 call wall，顯示於 founders notes 與 equity hub indicator。
- **統計（SG 數據）**：
  - call wall 對 S&P 在 **83%** 交易日守住阻力。
  - **88%** 的時間 S&P 收在 call wall 之下。
  - call wall 被突破後，前向報酬通常轉弱：1 日後平均約負值(片中數字含糊，原文 "negative send basis points")、5 日僅約 **+5 bps**。
- **解讀**：高機率的「賣壓累積、上行動能停滯」區。
- **實例（Trader tip）**：7/2 HOOD 因利多消息跳空，首次觸及 **$100 call wall**，當日多次在此被拒、交易者獲利了結。

### #6 Put Wall
- **核心定義**：**最強支撐位**，買方進場處——交易者常在此**對空單獲利了結、進場做多、或在其下方賣期權**。
- **產生方式**：同 call wall，每天 5:00 a.m. 前跑數學運算，為最大的美股指數與 **3,500+** 個股算出當日 put wall，顯示於 founders notes 與 equity hub indicator。
- **統計（SG 數據）**：
  - put wall 對 S&P 在 **89%** 交易日守住支撐。
  - **93%** 的時間 S&P 收在 put wall 之上。
  - put wall 被突破後，S&P 1 日前向報酬平均 **+14 bps**、5 日 **+7 bps**。
- **解讀**：買方支撐 S&P 500 的關鍵區。
- **實例（Trader tip）**：7/2 NFLX 連兩日下殺後，從 1340 跌到 1265 觸及 put wall 找到支撐。

### #7 Vol Trigger
- **定位**：Call/Put Wall 告訴你支撐阻力大概在哪守住；Vol Trigger 則是**判斷「市場狀態何時會轉變」最重要的水位**。
- **核心機制（正/負 gamma 分界）**：
  - 價格在 **Vol Trigger 之上** → 典型**正 gamma 環境**：交易較平靜、區間較窄、上漲日較多。
  - 價格**跌破 Vol Trigger** → 語氣轉變：**負 gamma 進場**，波動上升、下行風險增加。
- **關鍵統計**：Vol Trigger 之下的每日波動度，比之上時高出近 **40%**。
- **讀盤價值**：知道價格相對 Vol Trigger 的位置，可據此調整**部位大小(position sizing)、收緊停損、或在順風時加碼**，避免被 regime 切換打到、與市場狀態同步。
- **實例（極端）**：**2025/4/3** S&P 跌破 **5700 Vol Trigger**，引發後續兩個交易日 **>12%** 的急殺。

---

## ROMA 對照註記
- 這些水位（call/put wall、vol trigger、gamma）正是 **SG_MARKET_LEVEL**（keyLevels / market_overview json）與 ROMA opportunities 模組的概念基礎；本系列把「為什麼這些水位有效」（MM 避險流 → delta → gamma 動態壓力）的因果鏈講清楚，可作為模組的理論註腳。
- 建議把以下定義回填 **ROMA_SIGNAL_DESIGN.md** 的 gamma 結構解讀章節：
  - Vol Trigger = 正/負 gamma 分界；**之下波動度約高 40%** 可作為 regime 風險權重的量化錨。
  - Call Wall / Put Wall 的 SG 歷史命中率（S&P：call wall 83% 守阻力、88% 收下方；put wall 89% 守支撐、93% 收上方）可作為水位可信度的 baseline 對照。
- 與 squeeze 雙觸發 OCO（**負 gamma + DR 強 call + vol 便宜**）邏輯直接相關：
  - 「跌破 Vol Trigger → 負 gamma → 波動放大」正是雙觸發中「負 gamma」這一腳的教科書定義；GameStop squeeze 也是 #4 Gamma 片中點名的 gamma 急速位移案例。
  - 對照偏好設定 [[feedback_squeeze_entry_dual_trigger]]（若已建檔）——本系列為其「負 gamma」觸發條件提供原廠定義來源。

---

## 附錄：同 onboarding 課程的兩支收尾片（2026-06-14 補，無新訊號內容）
- **Key Levels #8「Learning & Support, Any Time You Need It」**（2026-02-25）：純課程收尾——回顧「3 個業界術語（MM/Delta/Gamma）+ 3 條 SG 水位（Call/Put Wall、Vol Trigger）」，並指向 platform quick-hit 影片、strategy guides、support center（數千 Q&A + 案例）、每週 webinar、Discord。**無交易內容**，僅供 onboarding 完整性。
- **Indices Walkthru #2「Use Greeks, Volatility & OI to Sharpen Trades」**（2026-02-25，1.3min）：接續基礎課程，導覽 index/futures 交易者的圖表工具區——**Greeks 7 張圖**（選指數、看近數日變化）、**Volatility 5 張圖**、**Open Interest 2 張圖（當 sentiment 指標，幫部位 sizing 信心）**；每圖有 i box 影片。tip：看 **S&P OI/volume 圖上的大倉位**判可能的顯著支撐/阻力。→ 對應 SG_MARKET_LEVEL 的指數層資料與 [[digest_SpotGamma_equity-hub-walkthru]] 個股層互補。
