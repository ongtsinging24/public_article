# SpotGamma 教學 Digest — 用 Gamma 水位結構化價差交易（3 片合併）

> 來源逐字稿（`knowledge/edu/`）：
> - Options Credit Spreads Using Gamma Levels from SpotGamma's CEO（2023-11-14，15min，Matt Fox 賣 call spread 完整紀律★）
> - Gamma Levels for Options Trading: Selling NFLX Call Spreads（2023-10-20，4min，財報後對巨型 strike 賣 call spread）
> - Capturing Big Stock Moves With Call Option Ratio Spreads（2024-08-13，7min，Imran 講 call ratio backspread 與「P&L 黑洞」）
> **性質**：evergreen 交易結構與風控紀律；具體 strike/水位屬當時案例。整理日 2026-06-14。

## 縮寫
- call wall / put wall = SG 判最大 call/put gamma 集中 strike（壓力/支撐）｜vol trigger = gamma flip 點｜credit spread = 收權利金價差（此處多為 bear call spread / 賣 call spread）｜ratio backspread = 賣 1 近價 call、買 2 更價外 call（常零成本）｜fixed-strike vol = 各 strike×到期真實 IV｜HIRO/hero = SG 即時對沖流（purple=全到期、teal=0DTE）｜OPEX = 月度到期｜ROC = return on capital

## 一、Matt Fox 的 OPEX 賣 call spread 紀律（核心★）
**核心理念**：在 SG **call wall 之上**賣 call spread 收權利金；wall 在 OPEX 週特別強。只用 SPY ETF、Excel 損益表（不引 IV/Greeks），求簡單可複製。
- **進場時機**：OPEX 週的週一進場、用週五到期（給 5 天 bandwidth，對齊 Founders Note 的 1日/5日預估 move）；多一天到期約多收 10% 權利金。
- **留 buffer**：不在 call wall（如 443）正上方賣，往上留 >1% 空間（如賣 444/446）→ 給「自己錯/市場錯」的容錯。若 443 由阻力轉支撐（被突破站穩）就出場。
- **分批**：第一天只上 50% 倉，對則加碼、錯則 ladder in。
- **風控規則（可直接搬）**：勝率 ~80%+（過去 20 個月）；**賺到 50–75% 就收、別貪到 100%**；**錯 30–40% 就停損**。「讓贏家跑、砍輸家」= 一致獲利的關鍵。上月案例對 call wall 賣、中東衝突急殺反而 +80%，週三收掉。
- **若 Brent 隔天說 call wall 上移/positioning 變 → 提早出場**。
- **進場輔以 HIRO**：當天開盤偏弱但 hero(purple) 把價格帶到 vol trigger 後**轉平/關閉**（賣壓沒到）→ 確認可進。
- **風格定位**：賣方賺「小幅高頻」；買 put/call 抓大 move 的人單筆指數型回報更高但勝率低。Brent 補充：**call spread 要在「強勢中」賣**（沖上去 vol 噴、call 被 bid），別在弱勢/已回落後嫌太便宜才賣；想表達「OPEX 後轉弱」用買 put 更好。兩人都不碰 0DTE，做 1–2 天外。

## 二、財報後對巨型 strike 賣 call spread（NFLX 2023）
- NFLX 財報 +16%（implied move 僅 7%）跳到 400 strike——EquityHub 顯示 **400 是巨型 strike**（次日 OPEX 加碼），Brent 判其為**磁吸 pin**而非單純即時阻力。
- **trade**：賣 Nov 450/475 call spread。邏輯：pre-market pop = vol 最大彈簧點，「再來一個 +15% 機率很低」→ 賣在 vol 最高處吃 IV 收斂。
- **fixed-strike vol 驗證**：一片 C 型紅 = vol 大幅回落、集中在 just-OTM call（市場在急漲中賣 call）→ **開盤即賣 > 等回落再賣**；後續數日 vol 續滑可繼續 lean against 該 strike。
- 教訓：盤前先用 EquityHub + fixed-strike vol 定 plan，開盤即執行，靠巨型 strike 當依靠。

## 三、Call ratio backspread 與「P&L 黑洞」（Imran，MARA/crypto 2024）
- **結構**：賣 1 張近價 call、買 2 張更價外 call（常**零成本/小 credit**），標的「sky 高」時無限上行、零權利金 access upside。
- **致命陷阱「the hole」**：若標的**漲太慢/漲幅不夠**（如 MARA 16.5→20 卡在賣出腿與買入腿之間），到期時買入腿歸零、賣出腿被穿 → **掉進 P&L 黑洞、可能大虧**（即使零權利金進場）。黑洞在接近到期才出現。
- **解法**：①**做夠長天期**（Aug 會掉洞 → 做 Sep/Oct/Nov，到期前都沒洞）②到期前約剩一個月**roll**，永遠不經歷黑洞，只付一點 decay。
- **選 long vol 的月份**：buy 含事件的到期（如含大選的 Nov）——若起漲、vol 被 bid（100→150），**vol bid 抵銷 time decay**，time/vol 互相對沖。
- 一句話：backspread 的藝術是「**永遠別被吸進黑洞**」——天期夠長 + 適時 roll + 選對 long-vol 月份。

## 四、ROMA 對照重點
- **call/put wall 是賣價差的錨**：對 call wall 之上賣 call spread（留 buffer + OPEX 週 + HIRO 確認賣壓未到）= ROMA opportunities（wall_signals）+ SG_MARKET_LEVEL 的直接應用；wall 突破站穩（阻力轉支撐）= 出場訊號。
- **可移植的風控數值**：take profit 50–75%、stop 30–40%、第一天 50% 倉、留 >1% buffer、1–2 天外不碰 0DTE → 可作 ROMA 對既有 BeCS/credit 部位的管理建議模板；呼應 [[feedback_no_flip_without_entry_context]]（進場接受的 buffer/max loss 不是事後新風險）。
- **巨型 strike = pin 磁吸**（NFLX 400）：財報/OPEX 後 EquityHub 巨型 strike 視為磁吸而非單純阻力 → 對應 [[digest_SpotGamma_0dte-mechanics]]（JPM strike 真 gamma 磁吸）與 sticky strikes。
- **賣 vol 要在強勢/高 IV 處**：對齊 [[digest_SpotGamma_iv-earnings-vol]]、[[digest_SpotGamma_skew-iv-rank]] 的 IV crush 紀律；ROMA 對「急漲 + call skew rich」標賣 call spread 機會。
- **零成本結構 ≠ 零風險**：backspread 黑洞、calendar margin 都需 ROMA 在建議時標明 max-loss 區與天期/roll 條件；對齊核心任務的風險意識。
- **CW short cap 例外**：對 call wall 賣 short leg 的紀律遇 ⭐⭐ 機構絕對 conviction 訊號時會被覆寫 → [[feedback_inst_conviction_overrides_retail_cap]]。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_key-levels-series-1to7]]、[[digest_SpotGamma_best-options-data-strategy]]、[[digest_SpotGamma_iv-earnings-vol]]、[[feedback_squeeze_entry_dual_trigger]]。
