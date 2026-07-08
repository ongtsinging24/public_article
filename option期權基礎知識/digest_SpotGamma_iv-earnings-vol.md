# SpotGamma 教學 Digest — IV 對期權的影響 + 財報 IV crush（4 片合併）

> 來源逐字稿（`knowledge/edu/`，Brent Kochuba）：
> - How Implied Volatility Impacts Options（2023-12-01，3min，基礎：long option = long vol）
> - How High Implied Volatility Can Work Against Options（2022-12-12，3min，高 IV 反噬）
> - Reading Earnings IV's SMCI vs AMD（2024-01-30，4.5min，財報前 skew/fixed-strike vol 讀法）
> - Earnings Trades UNLOCKED!（2025-10-31，10min，AMZN 實例：股漲 11% 仍虧——IV crush）
> **性質**：evergreen IV/vega 機制；個股 IV 數字屬當時觀察。整理日 2026-06-14。
> 註：第 4 片亦是 Options Calculator 產品示範，UI 細節見 [[digest_SpotGamma_options-calculator-walkthru]]，此處只取 IV-crush 概念。

## 縮寫
- IV = 隱含波動率｜RV = 已實現波動率｜vega = 期權對 IV 敏感度｜IV crush = 事件後 IV 暴跌使期權價值蒸發｜term structure = 各到期 ATM IV 曲線｜fixed-strike vol = 各 strike×到期的真實 IV（剝離價格移動）｜skew = put/call IV 差｜backwardation = 近月 IV > 遠月（事件前典型）｜25Δ = 25 delta｜SG compass/scanners = SG 判 call 相對 put 貴/賤的工具

## 一、基礎：long option = long volatility（IV Impacts Options 2023）
- **買 call 或 put 都是 long vol**：其他不變下，IV 上升 → 期權價格上升（Black-Scholes 只改 IV、不改價格/到期，put 價值隨 IV「飆」）。
- **SPX put 是雙重 long**：市場下跌時 ①delta 增（put 變更 ATM）②VIX/IV 通常同時 spike → 兩者都加分。**這就是「vol 便宜時買 put 當保險」合理的原因**——便宜，且真跌時 vol 還有很大上行空間。
- **個股不一定**：GameStop 股漲時 vol 也漲（call 推升 IV），別把「跌→vol 漲」的指數直覺套到單股。

## 二、高 IV 會反噬 long option（High IV Works Against 2022）
- 事件前（CPI/FOMC）term structure 前端 ATM IV 飆（例 ~40% = 定價 2.5% 日波動）。**買短天期 long option 此時要「多個標準差」才回本**——uphill battle。
- 機制：把 4 天到期 call/put 的 IV 從 40→20（只改 IV），期權價值被 crush；再推進 2 天 theta，「兩種情境都沒希望」。**方向猜對也可能虧**，因為 IV 回落。
- 例外回報：只有 Powell 真的嚇到市場、IV 40→80（巨幅單邊）才會大賺 → 需要「超出預期」才行。

## 三、財報前怎麼讀 IV（SMCI vs AMD 2024）
- **fixed-strike vol grid**：比較事件前後各 strike 真實 IV。SMCI 雖預告利多、股價漲，但 fixed-strike vol 一片紅 = **call 在上漲中被賣出**（IV 已洩）；AMD 一片綠 = IV 還在墊高 = **期權被 overprice**。
- **skew 讀法**：SMCI Feb skew 偏平（仍有 call skew 但不誇張）；AMD「expectations through the roof」、call skew 過度 → 判 AMD 期權貴、財報後股價可能 laggy（利多已被 pull forward）。
- **gamma curve flatten = 壓力消退**：AMD $200 上方無倉位、gamma curve 變平 → dealer 對沖壓力與波動趨緩，形成「line in the sand」上沿；SMCI 上方 525/550/600 還有倉位，較不明確。
- **結論**：同業兩名給出**不同 earnings play**——貴的（AMD）偏賣方/condor，不明確的（SMCI）保留彈性。

## 四、財報 IV crush 實證：股漲 11% 仍虧錢（Earnings UNLOCKED 2025 AMZN）
- **AMZN 財報**：盤前 +11%，但 25Δ call 從 $19 跌到 $14.21 → **持 call 者虧錢**。原因：IV 從 ~54% crush 到 23%（20 個 vol 點）。
- GOOGL 同樣：股漲、call 卻掉 13 vol 點（300C/1121 到期）。**正向財報 + long call = 虧損**，因為事件前 call「很貴」（SG scanners 顯示 call richness 在過去一年 90th percentile）。
- **正確做法（投影 IV，非猜方向）**：①SG compass/scanners 先客觀確認 call/put 哪邊貴 ②財報後砍 ~8 vol 點 + 把 call skew flatten（事件後 call wing 最受傷）③據此投影 P&L，常顯示「市場以為賺 $145、實際 −$5」。GOOGL 同套 setup 結構不同 P&L 從 +9% 到 +60~100%。

## 五、ROMA 對照重點
- **「IVR/IV percentile + backwardation → earnings IV crush 機會」紀律**：高 IV 事件前**賣方/價差/condor 吃 IV 收斂**，而非裸買方向；正向財報 long call 也可能虧 → 與 recent [[digest_SpotGamma_vol-cycle-market-timing-2023-2024]]、[[digest_SpotGamma_software-apocalypse-2026]]（CRM IVR 90% straddle sell）一致，亦呼應 [[project_software_sector_frame]] 軟體板塊 IV rank ~100% earnings trade。
- **vol 便宜（IV 低 percentile）→ 買 put 當保險**：成本低且真跌時 vol 上行加分 → 呼應 [[feedback_squeeze_entry_dual_trigger]]（vol 便宜時別把進場綁死，買保險/裸方向才划算）與 [[feedback_derisk_to_cash_not_defensive_equity]] 的避險思路。
- **fixed-strike vol / call-richness percentile / skew 應入 ROMA scan**：判個股期權「貴/賤」用客觀 percentile（compass/scanners），別只看絕對 IV；對應 SG_MARKET_LEVEL 與 ROMA opportunities。
- **財報後個股反應「股漲 vol crush」是常態**：ROMA 對財報事件的 severity/方向評級需把 IV crush 計入，避免把「正向財報」直接讀成 long call 訊號。
- **gamma curve flatten = dealer 對沖壓力消退**：可作為個股「上沿/壓力消失」的結構訊號，對應 wall_signals。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_why-calls-tough-high-vix]]、[[digest_SpotGamma_skew-iv-rank]]、[[digest_SpotGamma_options-calculator-walkthru]]。
