# SpotGamma — 最佳期權資料策略（The Best Options Data Strategy）

> **來源性質**：SpotGamma 官方深度教學（Futures Radio Show podcast，主持人 Anthony Crudele 對談 SpotGamma 創辦人 Brent Kochuba，2022-09-08，約 63.5 分鐘）。SpotGamma 為本系統主數據源（SG_DIR），與 ROMA opportunities 同源——**高方法論價值**，常青知識庫。

---

## 縮寫對照
| 縮寫        | 全稱                                  | 說明                                                       |
|-------------|---------------------------------------|------------------------------------------------------------|
| Greeks      | Option Greeks                         | 期權希臘字母（Delta/Gamma/IV 等敏感度指標）                |
| Delta       | Delta                                 | 標的每動一單位，期權價變動率；對 dealer = hedge ratio      |
| Gamma       | Gamma                                 | Delta 的變化率（二階導數）；衡量 hedge 需重調的量          |
| IV          | Implied Volatility                    | 隱含波動率；期權價的核心輸入之一                            |
| VIX         | CBOE Volatility Index                 | S&P500 30 天隱含波動率「恐慌指數」                         |
| MOVE        | MOVE Index                            | 「債券版 VIX」；ATM 美國公債期權隱含波動率                  |
| SKEW        | CBOE SKEW Index                       | OTM put vs call 定價偏斜；衡量尾部崩盤需求                  |
| VVIX        | VIX of VIX                            | VIX 本身的波動率；衡量 VIX call 買盤熱度                    |
| OPEX        | Options Expiration                    | 期權到期日（季度 OPEX 影響最大）                            |
| FOMC        | Federal Open Market Committee         | 聯準會利率決策會議                                          |
| CPI         | Consumer Price Index                  | 消費者物價指數                                              |
| QT          | Quantitative Tightening               | 量化緊縮                                                    |
| Vanna       | Vanna (the "Vanna trade")             | IV 變化驅動 dealer 買賣的二階效應（俗稱 vanna trade）       |
| Zero Gamma  | Zero Gamma / Volatility Trigger       | SpotGamma 專有「Vol Trigger」；call/put gamma 主導的翻轉點  |
| Call Wall   | Call Wall                             | 最集中 call 倉位 → 交易區間上緣（超買、易 pin）             |
| Put Wall    | Put Wall                              | 最集中 put 倉位 → 交易區間下緣（超賣、易暴力反彈）          |
| HIRO        | Hedging Impact of Real-time Options   | SpotGamma 即時逐筆期權對沖壓力指標                          |
| ES          | E-mini S&P 500 Futures                | S&P500 期貨                                                 |
| SPX/SPY/QQQ | -                                     | S&P 指數期權 / SPY ETF 期權 / Nasdaq100 ETF 期權           |
| OI          | Open Interest                         | 未平倉量                                                    |
| OCO         | One-Cancels-Other                     | 二擇一掛單（ROMA 對照用）                                   |

---

## 一句話總結
**期權資料的價值不在於交易期權本身，而在於透過 dealer 的 delta/gamma 對沖機制，把「VIX 方向 + 結構性水位（Zero Gamma / Call Wall / Put Wall）+ 即時對沖流（HIRO）」三者交叉確認，預判 S&P 期貨的方向、波動環境與轉折點——VIX 是領先指標，水位是邊界，HIRO 是即時確認。**

---

## 重點（依片中章節組織）

### 1. 三個核心 Greeks：把教科書定義翻成「對我有什麼意義」
- Kochuba 反覆強調：即使你不交易期權、只做期貨（ES、SPY、Nasdaq），也**必須**關注期權市場，因為 dealer 的對沖會直接衝擊標的價格。
- **Delta = dealer 的 hedge ratio（一階）**：機構（如 Bridgewater）買 put 避險 → 對手方（JP Morgan/Goldman）被迫賣出 put → 他們持有 short put 風險（市場跌會大虧）→ 用「賣期貨」對沖。Delta 告訴 dealer：標的動一單位，要 long/short 多少股或期貨才中性。
- **Gamma = Delta 的變化率（二階）**：市場移動後，原本的對沖量不夠了，gamma 告訴 dealer「要再調多少 delta」。例：3900 已對沖，市場走到 3950，要加碼多少對沖即由 gamma 決定。
- **IV / VIX**：IV 上升 → 期權平均變貴 → dealer 需重調對沖量。最簡單看法：**VIX 上 → 市場承壓向下；VIX 下 → 市場有上行壓力**。這條相關性是透過「dealer 需對沖的量」連結的。

### 2. 2022 的「計畫好的熊市」與流動性枯竭
- 回顧：2021 年 11–12 月（市場仍在歷史高點）期權結構由 call-heavy 轉 put-heavy，正值 Fed 轉鷹——「smart money」提前布局空頭，這些 put 在 2022 年 3 月前大量獲利。
- 本輪熊市特徵：**不是 V 型急殺，而是「methodical grind lower」（緩慢有序的磨人下跌）**。原因：跌勢被「事先 hedge 過」，且這是「reverse bull market / 最有計畫的熊市」。
- **流動性 vs 期權量背離**：期權交易量大增，但 ES 盤口深度（CME liquidity tool / depth of book）大幅萎縮（2021 年 8 月 → 12 月明顯惡化）。流動性枯竭 → bid-ask 變寬、價格更跳、市場更 chippy。
- **期權的槓桿放大效應**：散戶花幾百/幾千美元買 call，就能在對手方（如 Citadel）身上「invoke」數萬甚至數十萬美元名目的對沖需求 → 在流動性枯竭時放大波動。
- 本輪「去槓桿」特性：很多人是直接賣股票出清（而非買 put 避險），所以反而**沒有預期中的大量 put 量、也沒有 limit-down 急殺**。

### 3. 「Capitulation（投降式洗盤）」缺席之謎
- 市場一直在等 capitulation，但沒來。原因之一：**人人皆空**（很難找到看多的 macro 人），導致每次下跌很快超賣，缺乏「突發震撼」。
- 對比 2008：當年是 Bear Stearns 等突發衝擊驅動。本輪沒有 shock，因為節奏由「data point → data point、OPEX → OPEX」主導，太可預測。
- 已實現波動率（30 天 realized vol）持續處於近 10 年高位的高檔——典型應有一次「puke（嘔吐式下殺）」洗掉浮額再回升，但本輪遲遲未發生。

### 4. 尾部風險與信用市場：MOVE Index 作為總經單一儀表
- 目前期權市場**沒人買 tail hedge**（>1 個標準差的深度 OTM put）。Tail hedge 通常與信用市場事件連動（如 2020/3、2015/8 中國信用問題引發的 limit-down）。
- 為何信用崩 → 買股票 put？因為押注公司破產（股票歸零）最乾淨的方式就是買 equity put（資本結構上股票墊底，債券優先於股票）。
- **MOVE Index = 「債券版 VIX」**，看 ATM 公債期權價格。Kochuba 把它當「**單一總經儀表**」：MOVE 高 = 債券交易員恐慌 = 信用市場有壓力；**MOVE 回落到 100 以下 = 債市交易員安心 → 股市才會有「可持續」的中長線反彈**（all-clear 訊號）。
- **關鍵背離（片中當下）**：MOVE「screaming higher」，但 VVIX 與 SKEW 都跌到接近 pre-COVID 低點。意即「信用市場很擔心，股票市場卻沒在理會」。歷史上**信用先壞、股票最後才補跌、且補得很猛**。Kochuba：只要這個 spread 不消失，股市尾部事件機率就「very very high」。
- 危險情境：若 VVIX/SKEW 突然 spike（伴隨大量 put 買盤或 VIX call 買盤）→ dealer 被迫賣期貨（delta 反應）→ 市場再跌 → gamma 要求賣更多期貨 → **reflexive feedback loop（反身性回饋迴圈 / 下殺螺旋）**，這就是出現 -4%~-5% 單日的機制。
- 歐洲風險（2022 當下）：能源危機、義大利債務 vs 德國債務的歐元區裂縫、歐元跌破平價。並引用 1998 LTCM 案例（俄羅斯違約 → flight to quality → 公債利差爆開 → 槓桿放大幾乎拖垮全球金融體系）說明「benign 資產的一次性怪事」如何引爆股市 limit-down。

### 5. 季度 OPEX = 重要轉折日（不需懂 Greeks 也能用）
- **核心統計**：大型季度 OPEX 在歷史上「精準對齊」股市重要低點。具體：2018/12 與 2020/3 的市場低點，都是「大型 OPEX 的隔天」（也搭配 Fed 寬鬆，故反彈可持續）。
- 機制（positional analysis）：若 dealer short 一堆 put 並對應 short 一堆期貨，當這些 put 到期消失 → 沒東西要對沖了 → 回頭把 short 期貨買回 → 推升市場（買回 delta 的反射性反彈）。
- 2022 年內案例：
  - **3 月月度 OPEX**：低點在 FOMC 前 2 天、就在 OPEX 事件前，搭配中國刺激，當月反彈約 **10%**。
  - **1 月**（非季度但有大量 equity call 到期）：到期隔天出現顯著低點。
  - **6 月**：同樣大型低點後出現反射性反彈。
- 規則化用法：**不必懂 delta/gamma，只要在圖上標出季度 OPEX 為關鍵轉折日**。大量 put 到期 → 偏多（清掉糟糕的空頭 positioning）；大量 call 到期 → 偏波動/偏弱。
- 片中當下：9/16 是大型 OPEX（大量 put 到期），9/13 CPI、9/21 FOMC——「next week is a huge week」。

### 6. Event Vol（事件波動）：sell the rumor, buy the news 的機制
- 大事件（Powell 講話、FOMC、CPI、財報）前，期權含「event vol 溢價」（不確定性），VIX 被墊高。
- 事件過後若無 shock → **event vol 消退 → VIX gap down → 成為市場向上的 ratchet（棘輪）**。這就是「sell the rumor, buy the news」的真正成因。
- 2022 當下：CPI 已被當成像 FOMC 一樣 hedge（市場認為 CPI 溫和→Fed 可 pivot）。多個事件排排站，event vol 都很高 → 若都平安過關，VIX 下殺、市場鬆口氣上行；且同時撞上 9/16 大量 put 到期。
- **執行守則**：Powell 9:10am ET 講話時，盯 VIX。**VIX 不跌反持續往上爬 → 不要做多股票**（代表期權市場不喜歡眼前發生的事）。

### 7. 兩種市場 × Zero Gamma / Vol Trigger
- 市場只有兩種環境：**call-heavy = 低波動環境**；**put-heavy = 高波動環境**。
- **Zero Gamma（SpotGamma 專有名 = Vol Trigger）**：call gamma 與 put gamma 主導的翻轉點（gamma 是加權機制，call 對市場的衝擊大於 put）。
  - **價在 Zero Gamma 之上 = 正 gamma**：call 倉位主導 → dealer 對沖壓抑波動 → 低波動 → 對長線持有者偏友善（equity-friendly）。
  - **價在 Zero Gamma 之下 = 負 gamma**：put 主導 → 高波動、市場壓力大。
- 片中當下 Zero Gamma ≈ **4000**：站上 4000 → 純 call 倉位轉強 → 提供市場順風（透過波動壓抑）。SpotGamma 有回測支持：在正 gamma / 4000 上方，中長線展望較正面。
- **All-clear 三條件（SpotGamma 版）**：① VIX 下行；② 走過 9 月 OPEX；③ 站上 4000（Zero Gamma）。
- 註：SpotGamma 開始免費提供「flip point（翻轉點）」資料於其 market 頁。

### 8. Put Wall / Call Wall：交易區間的上下緣
- **Put Wall** = 最集中、最大的 put 倉位所在 = 交易區間**下緣**（跌破 = 超賣）。
- **Call Wall** = 最大 call 倉位 = 交易區間**上緣**（站上 = 超買）。片中當下 Call Wall = **4005**。
- **行為差異（關鍵）**：
  - 撞 **Call Wall** → 市場傾向「**pin（釘住）**」該水位（因 call 的對沖方式）。
  - 撞 **Put Wall** → 市場傾向「**violent reflexive bounce（暴力反射反彈）**」，不會 pin/停留。
- 為何不同？持 call 者不太擔心 IV，可以放著或從容交易；持 put 者必須在「IV 最大化的瞬間」賣出 put 才賺最多（市場剛觸 3900 並完美擇時賣 put，會比市場觸 3900 後在該水位附近盤整再賣賺更多，因 IV 退場後 put 價值衰減）→ 持 put 者被迫頻繁主動交易 → 引發更多波動 → Put Wall 不 pin、反而暴力反彈。
- **Put Wall 的「移動」是 positioning 風向標**：Put Wall **下移 = 偏空**；**上移 = 偏多**。片中當下：市場多次測試 Put Wall（自 8/31 起未變）但**牆沒移動**，呼應「沒有強烈 put 買盤需求、沒感知到尾部風險」。
- 水位形成方法（回答 Steve 提問）：**完全基於期權 positioning（OI），輔以 gamma 與 IV 加權**，**不含任何技術分析**（非 SMA、非 2 倍標準差）。

### 9. VIX 作為「確認指標」與短線執行（雞生蛋問題：VIX 先動）
- SpotGamma 每天約凌晨 3am 在開盤前發布水位（可匯入 TradingView 等）。Call Wall 與 Put Wall 是最重要的兩條。
- 流程：用「開盤前的水位」預期支撐/壓力 → **用 VIX 即時確認**。
  - 在 **Put Wall** 觸及時，看到 **VIX 開始下殺** → 確認支撐成立、市場將反彈。
  - 在 **Call Wall** 觸及時，看到 **VIX 開始 spike** → 確認轉折、市場將下殺。
- **VIX 是領先（leading）的那一個**：日內看 1 分鐘 bar，VIX 會「稍微先動」，dealer 看到 IV 變化才調整對沖 → 期貨才被推動。VIX 全早上趨勢往下 = 壓力持續退場 = 市場易漲。

### 10. HIRO：即時逐筆 delta / 對沖壓力
- **HIRO = 即時測量每一筆期權成交對 dealer 造成的理論買/賣（對沖衝擊）**。盯 SPX / SPY / QQQ 三大宏觀風向。
- 看圖：**橙線 = call 的對沖壓力；藍線 = put 的對沖壓力**。
  - 橙線**上升 = 散戶在買 call**；橙線**下降 = 在賣 call**。
  - 兩線整體**上行 = 正 delta 交易 → dealer 應買期貨（偏多）**；整體**下行 = 負 delta → 壓市場（偏空）**。
- 片中即時觀察：先前「買 put + 賣 call」→ 市場走弱；最新反彈時「大量賣 put」（市場約 3900 區）→ 拉出反彈。
- **SPY 期權流通常與 SPX 一樣大或更大**；QQQ 也很重要。即使只做 ES 期貨，也要盯三者——QQQ 出現大空頭流會外溢到 S&P。
- HIRO 同樣可用於**個股**，尤其 meme 股 squeeze（片中提：Rivian 兩天前、Tesla 當天早上出現大 call block，橙線 jump → 直接推升標的）。

### 11. 多訊號交叉 = 「三腳凳 / trifecta」進場法
- 不是單一訊號，而是**疊加確認**（overlay，不取代你既有的 volume profile / Fibonacci 等工具）：
  - **做空 setup**：價在阻力（如 3950 large gamma 2）+ VIX 開始往上轉 + HIRO 顯示 call 被賣（橙線下行）= trifecta → 好的放空時機。
  - **做多 setup**：價在支撐（如 3900）+ 市場急殺中 VIX 開始下殺 + HIRO 顯示 put 被賣（正 delta 進場）= 多一隻凳腳的確認 → 偏多。
- 價值：理解真正的「edge」所在，並**避免在區間中段過度交易**（keeps you away from being overly active in the middle）。

### 12. IV / 波動率的進階用法（Q&A）
- Kochuba **不在 IV 或 VIX 上用移動平均**（在 VIX 上畫趨勢線/技術分析「是很好的釣魚/troll 工具」——意指常被打臉）。他靠「敘事 + 確認訊號」與直覺，看 lower lows / higher highs 抓趨勢。
- 個股 IV：因逐筆 flow 太跳、net flow 易反轉，**不用 MA**；改用**歷史波動率（HV）**判斷該股「貴/便宜」的相對區間（每檔股票自有 barometer，例：Rivian 短天期 IV 約 **150**）。
- **偏好交易**：當判定 IV 很高時，常用 **fly（蝴蝶，call fly / put fly）**——同時捕捉高 IV 與部分方向性移動。
- IV 缺陷：OPEX 前後會日間「跳空」，MA 在這種時候無效。

### 13. JP Morgan 季度 collar 對沖的影響（Q&A）
- 結構：JPM 某基金做 **collar**——賣 call（用權利金）去買 put spread，對沖其大型 long equity 部位。
- 本期（6 月做的、9/30 到期並 roll）：賣 **4005 call**，買 **3580 put**，賣 **3020 put**。
- 影響：當市場接近其中一個 strike，月底附近常有**日內波動**；這些 strike 像「**磁鐵（magnet）**」。
- dealer short 3580 put → 讓他們得以「賣更多其他 put / 提供更多波動」，紓解其壓力；dealer long 3020 put → 市場跌破 3020 才真正受保護（但 3020 離現價太遠，目前無實質影響）。
- 規則：離這 complex 越遠（在價之上、且都到期）→ 影響越小；越深入價內（ITM）→ 影響越大。**需跌破 3580，此 trade 才有較大衝擊**。（深度分析可參考 Twitter 上的 @damp_spring。）

### 14. 觀眾互動數據
- 直播投票：**73% 的觀眾有在使用期權**。

---

## 關鍵實例 / 數字
| 項目 / 事件                | 數字 / 水位            | 意義                                                       |
|----------------------------|-----------------------|------------------------------------------------------------|
| Zero Gamma / Vol Trigger   | ~4000（S&P）          | 站上=正 gamma/低波動/偏多；之下=負 gamma/高波動            |
| Call Wall                  | 4005                  | 交易區間上緣；觸及傾向 pin（超買）                          |
| Put Wall                   | (片中以圖示，自 8/31 未移)| 交易區間下緣；觸及暴力反彈；自 8/31 未移動=無 put 需求      |
| Large Gamma 2              | 3950                  | 第二強水位；當下作為阻力                                    |
| 支撐參考                   | 3900                  | 反覆測試的 Put Wall 區；測試時 put 被賣=市場正面            |
| 3 月月度 OPEX 反彈          | 約 +10%               | 低點在 FOMC 前 2 天，搭配中國刺激                           |
| 2018/12、2020/3 低點        | OPEX 隔天             | 季度 OPEX「精準對齊」市場大底（搭配 Fed 寬鬆）              |
| JPM collar（6 月做/9/30 roll）| 賣 4005 call / 買 3580 put / 賣 3020 put | collar 結構；strike 如磁鐵；跌破 3580 才有較大衝擊 |
| 9 月關鍵週                  | 9/13 CPI、9/16 OPEX、9/21 FOMC | event vol + 大量 put 到期疊加                       |
| Rivian 短天期 IV           | ~150                  | 個股 IV 高低需用各自 HV 區間判斷                            |
| 觀眾使用期權比例           | 73%                   | 直播投票                                                    |
| MOVE Index all-clear 門檻  | 回落至 100 以下       | 債市安心 → 股市可持續反彈                                   |
| VVIX / SKEW（片中當下）     | 接近 pre-COVID 低點   | 與 MOVE 高檔形成危險背離                                    |
| LTCM 案例                  | 1998                  | benign 公債利差 + 槓桿 → 引爆全球系統性風險                 |

---

## ROMA 對照註記
- **VIX 領先 + 水位確認** 的雙層架構直接對應 ROMA opportunities 模組與 SG_MARKET_LEVEL：可把「Zero Gamma / Call Wall / Put Wall」當交易區間邊界，「VIX 方向轉折」當確認 trigger；可回填 ROMA_SIGNAL_DESIGN.md。
- **Put Wall 不移動 = 無 put 需求 = 無尾部風險感知**——這是一個可量化的 positioning 風向標（牆下移=偏空、上移=偏多），值得在 ROMA 訊號層加「wall 位移偵測」。
- **負 gamma + 反身性下殺螺旋**（買 put → dealer 賣期貨 → 再跌 → gamma 要賣更多）= squeeze 的反向版本；與 squeeze 雙觸發 OCO（負 gamma + DR 強 call + vol 便宜）的設計高度相關，點出 [[feedback_squeeze_entry_dual_trigger]]。HIRO 橙線 jump（大 call block 湧入）正是「DR 強 call」的即時對應訊號。
- **三腳凳 trifecta 進場**（水位 + VIX 轉向 + HIRO flow 方向）= ROMA 多訊號合流（confluence）的範本：單一水位不進場，需 VIX 與即時對沖流同向確認。
- **MOVE vs VVIX/SKEW 背離** 提供一個跨資產的尾部風險守門員：可作為 ROMA 之上的 macro overlay/risk gate。
- **季度 OPEX 轉折日** 為日曆型訊號，可作 event_tracking 的固定錨點（大量 put 到期→偏多反射、大量 call 到期→偏弱）。
- **event vol 退場機制**（FOMC/CPI 過關後 VIX gap down → 上行棘輪）對應 ROMA 對總經事件前後的 vol regime 切換偵測。
