# SpotGamma 教學 Digest — 泡沫/Dispersion 與 Skew 擁擠訊號（2 片合併）

> 來源逐字稿（`knowledge/edu/`，Brent Kochuba）：
> - Is a Stock Bubble Indicated by Dispersion, Correlation & Volatility?（2024-03-03，7min；S&P Global dispersion 框架 + 網路泡沫類比 + SMH skew 轉折訊號）
> - If Everyone Is Bullish, The Trade Is Probably Over（2026-01-27，3min；skew percentile 擁擠 = trade 已結束）
> **性質**：evergreen 擁擠/泡沫判讀框架；具體標的/百分位屬當時觀察。整理日 2026-06-14。

## 縮寫
- dispersion = 指數成分股彼此移動的離散度（越大 = 內部各走各的）｜correlation = 成分股齊漲齊跌程度｜index vol = 指數波動率｜skew = put/call IV 差｜call/put skew percentile = 相對過去一年的 richness 百分位｜core 1M = CBOE 相關性指數（risk-off 旗標）｜SMH = 半導體 ETF

## 一、Dispersion / Correlation / Vol 三件套判泡沫（Stock Bubble 2024）
- **dispersion**：成分股內部各走各的程度（NVDA/AMD 狂飆、KO 不動 → 高 dispersion）。
- **correlation**：齊漲齊跌（COVID crash = 全跌 → 高 correlation）。
- **index vol**：指數層級波動。
- **泡沫特徵 = 高 dispersion + 平/微升 index vol**：只有「一部分市場」（科技/半導體）在 bubble，其他板塊正常 → index vol 不升，但 dispersion 創高。**「stocks up, vol up」就是泡沫指紋**。
- **網路泡沫類比（S&P Global）**：1999-04~2001-01 dispersion 由科技板塊 idiosyncratic 行為推到極高、index vol 卻不動；泡沫可**持續很久**（didn't revert until 2001）。2024 數據與此「異常一致」——難以長期維持，但靠 catalyst 才破。
- **轉折訊號 = skew rotation**：SMH 出現「ramp 型 skew」——10% OTM call IV > ATM > 10% OTM put（人買 call、賣/不要 put）= 異常看多。**泡沫要破的訊號 = skew 轉回正常**（put 得 bid、call IV 掉，無論是需求降或有人賣 call）→ 動能熄火。常在大 OPEX / VIX exp / CPI 等窗口發生。

## 二、Skew percentile 擁擠 = trade 已結束（If Everyone Is Bullish 2026）
- **核心**：當大家都擠在一邊（call skew 100th percentile = call 貴到極致），**這個 trade 多半已經結束**——你是在高價買 call，通常不 work；尤其 correlation 極低（core 1M 破 risk-off）= 極度擁擠的交易，unwind 時可能劇烈。
- **「skate to where the puck is going」**：看 skew 要往「puck 要去的地方」滑，而非追現價。人全在一側 = 行情已過。
- **重要例外（done → more done）**：擁擠可以更擁擠。SanDisk 100th percentile call skew 後 call 還能更貴（300→380s 繼續軋）→ **沒有保證**；最終一根 GameStop 式 squeeze 仍可能。但 base rate 上，極端 call skew 買 call / 極端 put skew 買 put 都「missed the trade」。
- **雙向對稱**：put 100th percentile + 人全在最左 → 此時買 put 也賺不到（put 太貴）→ 反而可能劇烈反彈。

## 三、ROMA 對照重點
- **dispersion 高 + index vol 平 = 泡沫/脆弱旗標**：與 recent [[digest_SpotGamma_correlation-and-rate-cuts-2024]]（concentration 2007 水平、record low correlation 三重 suppression）、[[digest_SpotGamma_software-apocalypse-2026]]（dispersion trade 解釋個股 vs 指數脫鉤）一致 → ROMA scan 應監控 dispersion/correlation/index-vol 三件套；catalyst-driven 破裂 → 服務核心任務避開大跌。
- **skew percentile 擁擠 → 別追高/別追空**：call skew >90~100th percentile + 超漲 = 過熱、trade 已過 → 呼應 [[feedback_skew_overrides_layer0_undervalued]]（Skew Rank>90% + 超跌 = 價值陷阱的鏡像）、[[feedback_pct_to_fair_decompose]]（A 群超漲先查框架）、[[digest_SpotGamma_skew-iv-rank]]。
- **「done → more done」= 別純靠 skew 做反向**：SanDisk 案例提醒 ROMA squeeze 體質標的，擁擠可更擁擠 → 對應 [[feedback_squeeze_entry_dual_trigger]]（雙觸發 OCO，別把站穩當純失效）與 [[feedback_inst_conviction_overrides_retail_cap]]。
- **skew rotation 是動能轉折訊號**：put 重獲 bid / call IV 掉 = 上漲動能熄火，常在 OPEX/VIX exp 窗口 → 回填 ROMA_SIGNAL_DESIGN.md。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_volatility-skew-tail-risk]]、[[digest_SpotGamma_skew-iv-rank]]、[[project_software_sector_frame]]、[[digest_SpotGamma_correlation-and-rate-cuts-2024]]。
