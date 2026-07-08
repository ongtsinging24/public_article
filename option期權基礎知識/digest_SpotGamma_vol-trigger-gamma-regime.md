# SpotGamma 教學 Digest — Vol Trigger（gamma flip）+ Net Gamma Regime + OPEX 定位（2 片合併）

> 來源逐字稿（`knowledge/edu/`）：
> - Volatility Trigger: The Gamma Flip Point. Explanation + Stats（2023-03-31，5min；vol trigger 機制 + 收盤分布統計★）
> - Knowing Simply OPEX Positioning Can Improve Your Return（2022-09-18，4min；put-weighted regime + OPEX 季節性）
> **性質**：evergreen gamma regime 機制；具體水位/日期屬當時觀察。整理日 2026-06-14。
> 註：vol trigger 亦是 Key Levels #7，與 [[digest_SpotGamma_key-levels-series-1to7]] 互補（此片重「統計分布 + 交易應用」）。

## 縮寫
- vol trigger / zero gamma = dealer 淨 gamma 由正翻負的 SPX 水位｜short/long gamma = dealer 負/正 gamma 部位｜net gamma indicator = 市場 call-weighted（正）vs put-weighted（負）regime｜delta hedge = dealer 動態對沖｜OPEX = 月度第三個週五到期｜JPM call = JP Morgan collar 賣出的上方 call

## 一、Vol Trigger = gamma flip 點（機制）
- **vol trigger ≈ zero gamma level**：dealer 淨 gamma 翻正/負的分界（例 4000）。
- **下方 = short gamma = 高波動 regime**：市場跌、dealer 賣期貨（負 gamma 對沖，如 short put 跌時吃虧→賣 futures）；漲則買回 → **放大波動、速度快、VIX spike 快**。
- **上方 = long gamma = 低波動 regime**：dealer long call（如 JPM call），漲則漸賣期貨、跌則買回 → **壓抑波動**。
- **方向性**：通常是**向下跌破** vol trigger 才翻 regime → vol trigger 一旦 flip，第一動多半是**較大 drawdown + VIX spike**（例：跌破 4000 → VIX 快速 20–22、SPX 快到 3900）。
- 若 put skew 低/有人賣 put/買 call，gamma flip 實際位置會移 → SG 在 morning notes 更新真實正負 gamma 邊界。

## 二、Vol Trigger 收盤分布統計（交易應用★）
數百筆數據，看「收盤落在 vol trigger ±1%」之後的報酬分布：
- **收在 vol trigger 之上**：傾向「黏住」、小幅正 skew、**波動小** → 想吃這種「沖到此處」的場景，可**賣 condor / straddle / call**（此時 vol 仍高、可利用）。
- **收在 vol trigger 之下**：報酬分布**大幅外擴**（high vol）。初跌破偏負報酬，但「把方向從腦中抹掉、只看波動」→ 這條線兩側市場行為有**鮮明分界**。
- **20,000 呎結論**：上方低波、下方高波；波動雙向——跌破初期大跌，但同 regime 內也會有**劇烈反彈**。

## 三、Net Gamma Regime + OPEX 季節性（OPEX Positioning 2022）
- **net gamma indicator**：market call-weighted（正 gamma）= 低波；put-weighted（負 gamma）= 高波（put 對 IV 更敏感、需更頻繁對沖）。2019–2020 多數時間 call-weighted；2022 多數 put-weighted。
- **OPEX 季節性（Reuters/SG 數據）**：2022 下半年「OPEX 週持現金、OPEX 週後做多 SPY」顯著跑贏 buy-and-hold。
- **機制（put-weighted regime 下）**：put 進價內 → dealer delta hedge 累積（short）→ OPEX 全部 put 到期 → **short-cover rally**（做市商調倉）→ OPEX 後常反彈。
- **反例（call-weighted OPEX）**：2022 僅 4 月、8 月是 call-weighted OPEX → 這兩次反而是**漲進 OPEX、OPEX 後下跌**，「持現金」策略失效。
- **要點**：看 zero gamma 不只為預測波動，而是判「**誰在掌控**——put 還是 call」，這決定 OPEX 前後的走法。

## 四、ROMA 對照重點
- **vol trigger flip = 核心避險訊號**：跌破 vol trigger（翻 short gamma）→ 標記「高波 regime、初動偏大跌 + VIX spike」→ 直接服務核心任務「避開像 2026/06/05 大跌」。對應 ROMA opportunities（wall_signals / vol trigger 水位）+ SG_MARKET_LEVEL。
- **收盤相對 vol trigger 的位置 → 決定 vol 策略**：收上方（低波）賣 condor/straddle；收下方（高波）別裸賣、買保險/方向 → 回填 ROMA_SIGNAL_DESIGN.md vol 章節；呼應 [[digest_SpotGamma_vix-mechanics-products]]、[[digest_SpotGamma_gamma-level-spreads]]。
- **net gamma regime（call vs put weighted）入 ROMA scan**：判 OPEX 前後走法（put-weighted → OPEX 後 short-cover rally；call-weighted OPEX → 反而 OPEX 後弱）→ 與 recent [[digest_SpotGamma_opex-live-series]]、[[digest_SpotGamma_stock-setups-opex-positioning]] 串聯。
- **「初動向下、但同 regime 內有劇烈反彈」**：提醒 ROMA 別把跌破 vol trigger 一律當單向看空；put wall bounce ≠ 結構底（[[digest_SpotGamma_vol-cycle-market-timing-2023-2024]]）。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_key-levels-series-1to7]]、[[digest_SpotGamma_vanna-charm-market-impact]]、[[digest_SpotGamma_0dte-mechanics]]、[[feedback_squeeze_entry_dual_trigger]]。
