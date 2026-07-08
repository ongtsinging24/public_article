# SpotGamma 教學 Digest — VIX 機制、產品與交易（4 片合併）

> 來源逐字稿（`knowledge/edu/`）：
> - VOLQ the Nasdaq Volatility Index（2022-09-30，2min，NDX 版 VIX）
> - Can a "Too Low" VIX Break Stocks?（2023-05-10，8min；mean reversion / 16 法則 / 下界 / reflexivity）
> - How to Short the VIX（2024-08-22，8.6min；VIX 曲線 calendar + put fly 結構，Imran 操盤）
> - When VIX Down DOESN'T Mean "Vol Crush"（2025-03-17，5.5min；fixed-strike vol 辨「位置性 VIX 下殺」）
> **性質**：evergreen VIX 機制與交易結構；具體 VIX 水位/日期屬當時觀察。整理日 2026-06-14。

## 縮寫
- VIX = SPX 30 天隱含波動率指數｜VOLQ = NDX(NASDAQ100) 版同方法論波動率指數（CME 期貨代號 VOLQ）｜RV/IV = 已實現/隱含波動率｜rule of 16 = VIX÷16 ≈ 預期單日 SPX % 波動｜contango/inverted = VIX 期限結構正向/倒掛｜put fly = put butterfly｜calendar = 賣近月買遠月｜fixed-strike vol = 各 strike×到期真實 IV（剝離價格移動）｜Vanna rally = 賣 SPX put 壓 VIX 抬市場｜VIX exp = VIX 衍生品到期（週三 9:30 settle）｜max pain = 使最多期權歸零的 settle 點

## 一、VIX 是什麼 + VOLQ（VOLQ 2022）
- VIX = 交易者對 SPX 未來 30 天波動的預期（非單純「恐慌」）。**VOLQ** = 同方法論套在 NDX 期權 = NASDAQ100 波動率，有 CME 期貨/期權可表達觀點。
- **為何重要**：S&P500 與 NASDAQ100 結構差異大，組合越來越像 NDX（AAPL 等權重大、表現好 → 占比升）→ 對沖科技重倉應參照 VOLQ 而非只看 VIX；hedge 數量看 VOLQ fact sheet 的相關係數。

## 二、太低的 VIX 會「弄壞」股市嗎（Too Low VIX 2023）— 反身性風險框架
- **rule of 16**：VIX÷16 = 預期單日 SPX % 波動。VIX 16→預期 1%；VIX 12→0.75%（極小預期）。
- **mean reversion + 下界（lower bound）**：vol 多時間尺度均值回歸；長期有一條下界，大 spike 後數月慢慢 feed 回 15–16 區。**vol 雙向存在**——市場急漲也製造 vol，所以碰下界後 VIX「不管漲跌都得往上」。
- **vol-seller reflexivity（核心風險）**：大 spike 後賣 vol 很流行，賣方被慣壞 → 越賣越小的 spike，直到 choke point / realized low。此時**交易者對風險定價幾乎為零**，一旦壞 headline → short vol 者被迫 run for cover → **放大下殺**。實例：SVB 倒閉 VIX 衝 30、市場一兩週 −7%，SG 判斷是「vol 從極低點起跳」放大的。
- **操作含義**：低 VIX 處 shorting vol 報酬差（但不必然要 long vol）；若手上 long stock / short vol，要開始留意這些 dynamics。

## 三、怎麼「做空 VIX」——結構而非裸賣（How to Short VIX 2024，Imran）
背景：恐慌時 VIX 曲線變平/倒掛（短月在上）。**別自殺式裸賣近月期貨/買遠月**（可瞬間反向擴大）。用**期權結構**表達「曲線回 contango」：
- **VIX calendar（買近月 put、賣遠月 put）**：押曲線回落、近月 VIX 跌回 20 下。可做到零權利金（付 margin），一週做到 50%+ return on margin。遠月（如 10 月含大選）天然帶 ~3% implied move 的 V 點 premium，越近大選越突出。
- **lopsided put fly（如 17 / 兩個 14 / 13）**：押「VIX gravity 到 9 月回 15 以下」的**高機率、正期望值**結構。重點不是 optical risk-reward，而是**高勝率 × 正 ROC**（50–100% ROC 足矣，不需 200%）。做 lopsided + 加 13 tail = 即使 VIX 崩穿地板也保住 ~30% ROC，不會白付權利金。
- **time decay 低**：跑到 8 月底 VIX 不動也幾乎無 decay（vs 裸 VIX 期權跑在高 vol、有 decay）。可用 stop（VIX 破 20 出場）把風險從 $1.5 縮到 $0.7，改善 risk-reward。
- **裸買 put**：若高 conviction VIX 回 12（無下界），直接買遠月 put（40¢→$2 = 4 倍）更直接。選 fly vs 裸 put 取決於「你認為地板在哪」。

## 四、VIX 下殺 ≠ vol crush（VIX Down DOESN'T Mean Vol Crush 2025）— fixed-strike vol 的價值
- 案例 2025-03-17：VIX −1.3 點（−6%），SPX +64bp。直覺＝vol 被賣、風險下降？**錯**。
- **看 fixed-strike vol（剝離價格）**：3/14→3/17 各 strike IV 其實**多數小幅走高**（3 月底 +30bp、4–5 月 +1/3 點），只有少數高 strike call 被賣 → surface 其實很安靜。**沒人真的在賣 vol**。
- **真相 = 位置性 rally（positional）**：VIX expiration（3/18 週二 settle）。dealer 在 20 以上大量 short、20 以下 short 消失；20 strike 有 26 萬 call 到期 → **max pain 把 VIX 壓向 20** 的誘因 → 今日 SPX 強漲多半是 VIX exp 倉位驅動，非結構轉好。
- **判讀**：term structure 仍對 FOMC / Trump 關稅有 event vol → 「VIX 跌但 fixed-strike vol 不動 = 什麼都沒變」→ SG 當日策略是**往這波 relief rally 裡放空**，預期月底 VIX 均值回升到 25。
- **教訓**：VIX 是頭條數字，**fixed-strike vol 才告訴你 vol 真的有沒有被賣**；VIX exp 是趨勢轉折「窗口」。

## 五、ROMA 對照重點
- **「VIX 下殺要用 fixed-strike vol 驗真假」應入 ROMA scan**：VIX 跌但 fixed-strike vol 不動 = 位置性 rally（VIX exp / max pain）非結構改善 → 標記為 fade 候選，別誤讀成風險解除。對應 SG_MARKET_LEVEL，呼應 recent [[digest_SpotGamma_opex-live-series]] 的「VIX exp 窗口」。
- **vol-seller reflexivity = 低 VIX 脆弱旗標**：VIX 在 realized low + RV 極低 + core 1M 低 → short-vol 擁擠、壞消息易觸發正回饋下殺 → 核心任務「避開像 2026/06/05 大跌」的直接訊號；呼應 [[digest_SpotGamma_0dte-mechanics]]（0DTE 撐盤幻象）、[[feedback_squeeze_entry_dual_trigger]]。
- **rule of 16 / VOLQ**：ROMA 對科技重倉組合的 vol 監控應加 VOLQ（NDX）視角，不只 VIX；rule of 16 可作 RV/IV 期望波動的快速換算。
- **VIX 結構交易（calendar / lopsided put fly）= 正期望值、高勝率**：對應 [[feedback_derisk_to_cash_not_defensive_equity]] 的避險載體思路，及 [[digest_SpotGamma_iran-crisis-vol-mechanics-2026]]（put fly > 裸 put、VVIX>125 買訊）；ROMA 可把「VIX 在高位 + 曲線倒掛」標為 short-vol 結構機會。
- **VIX exp + FOMC/關稅 event vol 疊加 = 轉折窗口**：回填 ROMA_SIGNAL_DESIGN.md 的 vol 章節。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_why-calls-tough-high-vix]]、[[digest_SpotGamma_volatility-higher-than-10yrs]]、[[digest_SpotGamma_vol-cycle-market-timing-2023-2024]]、[[digest_SpotGamma_iran-crisis-vol-mechanics-2026]]。
