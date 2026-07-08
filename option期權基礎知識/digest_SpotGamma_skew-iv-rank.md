# SpotGamma 教學 Digest — Skew + IV Rank 選 trade 流程（2 片合併）

> 來源逐字稿（`knowledge/edu/`，Brent Kochuba）：
> - Options Skew Explained: Why Most Traders Buy Too Late（2026-01-26，4min；level vs skew 二維 + core 1M < 8 邏輯）
> - Options Trading Using IV & Skew Rank → What Trades Make Sense（2025-12-12，7min；AVGO 財報前 scanner funnel 完整 worked example）
> **性質**：evergreen 選 trade 流程；個股 percentile/IV 數字屬當時觀察。整理日 2026-06-14。

## 縮寫
- IV/RV = 隱含/已實現波動率｜IV rank = IV 在過去一年的百分位｜skew = put/call IV 差｜call/put skew percentile = 25Δ call(put) vs ATM 的 richness 在過去一年百分位｜risk reversal = 25Δ call IV − 25Δ put IV（正=call 貴）｜fixed-strike vol（含 statistical mode）= 各 strike 相對其他 strike 的貴/賤｜core 1M = CBOE 1 個月相關性指數（跌破 8 = 旗標）｜forward IV = SG 估事件後 IV 落點｜SG scanners/compass/EquityHub/vol dashboard = SG 工具

## 一、IV 的兩個維度：level（潮位）vs skew（浪形）
- **level**＝整體 vol 高/低、貴/賤（像海平面，潮起潮落）；**skew**＝偏向 put 還是 call（像海面上的浪，相對穩定低點的浪高）。判 trade 要兩維分開看。
- 「Why most traders buy too late」核心其實落在 **相關性極端 → 買 put**：core 1M 跌破 8 = 單股 vol（GOOGL/AAPL/MSFT/NVDA/NFLX）相對 index vol 太貴 → SPX put **相對**便宜。此時開始分批買 1–2 月 index put「放進口袋」（不必全力 risk-off）。
- **行為解釋**：看多時人買單股 call（想跑贏大盤，equities 穩定就去買 Tesla/SanDisk/memecoin）；真要避世界末日時買 index put。所以單股 call skew 高 + index put 便宜的極端，正是相關性崩到底、風險最大的時刻 → 多數人「buy too late」。

## 二、Scanner funnel：從 universe 收斂到具體 trade（AVGO 財報前 worked example）
SG「漏斗」流程（先定位國家、再看街道）——**固定用 1 個月基準**，否則隨機 strike/時間無法判統計位置：
1. **fixed-strike statistical mode**：先看哪些 strike 相對其他 strike 貴/賤（但缺歷史 context）。
2. **scanners → IV rank**：AVGO IV rank 37%（財報前合理偏高）。
3. **risk reversal**：偏高 → call 相對 put 貴（1M 25Δ call vs put）。
4. **拆解 call skew / put skew percentile**：AVGO call skew 85th percentile（偏多但非 99th）；put skew 很低（沒人要 put）。
5. **EquityHub 驗證 positioning**：理論上「short put + long call」，但實際看到是 **short call + short put**（call overwriting 在 440、dealer long 那些 put）→ 比 ORCL「long call+short put」溫和。
6. **gamma 地貌**：大量 ATM gamma、峰在 425–430 = dealer 最大阻力/stickier moves、well supported、低相對波動。
7. **forward IV**：vol dashboard term structure 估事件後 IV，AVGO 次週到期 IV 70→48（~20 點 contraction）。

**綜合判斷 → trade**：put 太便宜（teal 線很低）→ 不值得 focus 賣 put；call skew 偏 rich + 正 gamma → 兩者略矛盾，但「釘子冒出來在 call 這側」→ 溫和 short upside。配合預期 IV contraction，可考慮 **call counter spread / call diagonal / strangle / straddle（若偏貴）**。NVDA 找便宜 ITM call 是同流程反向（找便宜而非貴）。

## 三、可操作原則（跨片）
- **別看絕對 IV，看 percentile**：call/put skew percentile、IV rank、risk reversal 給「相對過去一年」的客觀定位；「人哪邊偏多/偏空」一目了然。
- **skew 與 positioning 要互相驗證**：scanners 講相對貴賤，EquityHub 看真實倉位；兩者對得上才有 conviction（AVGO 出現相反 → 降溫處理）。
- **便宜的那一側別硬做**：put skew 統計很低 → 賣 put 不划算，即使財報後 IV 會收（「IV 會降」≠「該 focus 這個 feature」）。
- **正 gamma + 高 call skew → 溫和 short upside**；高 vol 事件前用 contraction 結構（spread/diagonal）而非裸方向。

## 四、ROMA 對照重點
- **core 1M < 8 = 系統性風險旗標**（單股 vol 相對 index vol 過貴）：與 recent [[digest_SpotGamma_correlation-and-rate-cuts-2024]]、[[digest_SpotGamma_putcall-ratio-myth-and-low-vol]] 一致 → ROMA scan 應內建「相關性極端 → index put 相對便宜」買訊；呼應核心任務避開像 2026/06/05 大跌。
- **skew percentile / risk reversal / IV rank 三件套入 ROMA scan**：判個股 trade 時用 percentile 定位 call/put 哪邊貴 → 對應 SG_MARKET_LEVEL，可回填 ROMA_SIGNAL_DESIGN.md 的 skew/vol 章節。
- **skew 優先紀律**：高 call skew percentile + 超漲 = 過熱訊號，別追高 → 呼應 [[feedback_skew_overrides_layer0_undervalued]]（Skew Rank>90% + 超跌 = 價值陷阱）的鏡像；亦呼應 [[feedback_pct_to_fair_decompose]]（A 群大負值/超漲先查自身框架）。
- **forward IV contraction 估計**：事件前用 SG forward IV 預估 IV crush 幅度，影響 earnings trade 結構選擇 → 與 [[digest_SpotGamma_iv-earnings-vol]] 串聯。
- **scanner funnel 是 ROMA opportunities 的人工對照範本**：IV rank → risk reversal → skew percentile → positioning → gamma → forward IV，可作為 ROMA 多訊號融合的演算法骨架。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_iv-earnings-vol]]、[[digest_SpotGamma_volatility-skew-tail-risk]]、[[digest_SpotGamma_volatility-dashboard-walkthru]]、[[feedback_skew_overrides_layer0_undervalued]]。
