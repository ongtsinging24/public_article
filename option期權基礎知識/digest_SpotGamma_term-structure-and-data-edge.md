# SpotGamma 教學 Digest — Term Structure 讀法 + SG 資料優勢（4 片合併）

> 來源逐字稿（`knowledge/edu/`）：
> - Reading SPX Options Term Structure ahead of FOMC（2022-10-31，3min；事件前 term structure 讀法★）
> - SpotGamma Beats Banks to the Forecast（2022-12-14，2min；CPI/FOMC「期權壓抑動能」實證）
> - Why ChatGPT SPX GEX levels are USELESS（2026-01-06，2min；OI 靜態 vs 0DTE 動態）
> - Can you identify the big players?（2026-02-24，<1min teaser；flow 歸因的陷阱）
> **性質**：evergreen 讀法/資料品質原則；具體水位/日期屬當時觀察。整理日 2026-06-14。

## 縮寫
- term structure = 各到期 ATM IV 曲線｜contango = 短月 IV < 長月（正常）｜backwardation = 短月 IV > 長月（事件前典型）｜event vol = 特定事件帶來的隱含波動｜GEX = 做市商 gamma 曝險｜OI = open interest（昨夜靜態）｜0DTE = 當日到期｜call/put wall = SG 發明的詞（最大 call/put gamma strike）｜TRACE = SG 盤中大倉位地貌

## 一、事件前怎麼讀 SPX term structure（FOMC 2022★）
- **backwardation = 事件溢價**：FOMC 前 2 天，短端 ATM IV 飆（定價 1.5–2% 當日 move），遠端不慌 → 短月對沖 tail event 的需求堆出 backwardation。對照「正常」market = contango（短月 IV < 長月，因近期較可預測）。
- **兩種事件後情境（看 term structure 怎麼動）**：
  - **Powell 嚇到市場（偏空）**：短端高 IV「roll out」傳導到遠端、整條 term structure 抬升（像 shockwave）→ 遠月 put 增值 → dealer 賣 futures/equities 對沖 → 市場受壓一段時間。
  - **double surprise（偏多）**：整條 term structure 收縮、短端 IV 快速被賣、曲線回 contango → 遠月 put 被 crush → 市場快速上行。
- **交易者要看的**：多頭想看前端快速回落、轉 contango、遠端 decompress；空頭想看短端高 IV roll out、推升遠端。

## 二、期權市場「壓抑動能」往往勝過銀行預測（Beats Banks 2022）
- CPI/FOMC 前，眾銀行喊「5–10% move」；SG 反而判**期權市場會壓抑波動、把動能抽走**（無論漲跌）。
- 實證：CPI 公布 ES 衝 +100 handles 又全數回吐 → 隔日 Goldman 亦承認「期權市場阻止了上行、巨型 OPEX 造成 pinning、OPEX 後才會更自由移動」。
- **要點**：高 implied vol 事件前難有 extended move（呼應 [[digest_SpotGamma_iv-earnings-vol]] 的高 IV 反噬）；巨型 OPEX = pinning。

## 三、資料品質紀律：靜態 OI vs 動態 0DTE（ChatGPT GEX Useless 2026）
- ChatGPT 吐的 GEX levels 全部基於**昨夜 OI 靜態快照** → 開盤後 0DTE（占量 ~60%）一進場，TRACE 上的 levels 整天**劇烈漂移** → pre-market 的 call/put wall 設定**功能性失效**。
- call wall / put wall 是 SG 發明的詞，被「ChatGPT pre-market 評估」用壞了 → **靜態 OI 推的水位不可當日內計畫**，要看盤中即時對沖流（TRACE/HIRO）。

## 四、Flow 歸因的陷阱（Big Players teaser 2026）
- Twitter 上「某大戶買了 10,000 張 CRM put 所以要跌」= 一堆假設：買/賣 put、買/賣 call 都可能；且不是所有量都來自 hedge fund/retail，還有 MM-to-MM、bank-to-MM。
- **誰是 actor 才是關鍵**：SG 能 glean 出「fund 實際做了什麼 / hedge fund 做了什麼」，而非從裸 volume 臆測方向。

## 五、ROMA 對照重點
- **事件前 term structure backwardation = event vol**：ROMA 對 FOMC/CPI/財報的 severity 評級應讀 term structure（前端飆 + backwardation = 事件溢價）；事件後「前端回落轉 contango」=偏多、「短端 roll out 推升遠端」=偏空 → 回填 ROMA_SIGNAL_DESIGN.md vol 章節，串 [[digest_SpotGamma_vix-mechanics-products]]、[[digest_SpotGamma_iv-earnings-vol]]。
- **靜態 OI ≠ 日內水位**：ROMA 的 wall_signals 必須區分「昨夜 OI 推的結構 wall」vs「盤中 0DTE 動態漂移」；別把 pre-market GEX 當日內計畫 → 直接呼應 [[digest_SpotGamma_0dte-mechanics]]（0DTE 占比高、levels 劇烈漂移）、SG_MARKET_LEVEL 用即時 TRACE/HIRO。
- **flow 歸因要看 actor、不可從裸 volume 臆測**：判機構動向先確認 OI change 與 actor（買side OI），別被巨量 flow 灌水 → 呼應 [[feedback_13f_is_lagging_not_entry_signal]]、[[feedback_data_source_priority]]（SG 結構化 flow 為主、博主臆測不引用）、[[feedback_pct_to_fair_decompose]]（先查數據真實性）。
- **期權壓抑動能 > 銀行喊話**：高 IV 事件前傾向 mean-revert/pin，ROMA 別追事件前的方向喊單；巨型 OPEX = pinning → 串 [[digest_SpotGamma_vol-trigger-gamma-regime]]。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_best-options-data-strategy]]、[[digest_SpotGamma_0dte-mechanics]]、[[digest_SpotGamma_iv-earnings-vol]]、[[feedback_data_source_priority]]。
