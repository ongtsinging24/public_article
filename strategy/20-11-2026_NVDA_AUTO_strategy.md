# NVDA 策略卡（自動，FP 落地後 TREND2+TREND）

## S_1｜AUTO NVDA TREND2+TREND 21:51｜11/19 收 145.98（-3.24%），首次測試就跌破 PW 150，也低於 DT 52W Low 148.8，X 腳觸發；但 11/19 場次的 SG 結構（DT／v4／synth）全部缺 NVDA，牆位停在 11/18；FP 的 tot_oi_chg 是源端錯值；無持倉，維持 W，不追空，不寫預測帳本

> **資料 as-of**（建卡 2026-11-20 21:51 GMT+8＝08:51 ET，美東 11/20 OPEX 盤前）
> - **現價（最後一個真收盤）**：11/19 **$145.98**，兩個來源一致：
>   - scan `20-11-2026_NVDA_scan_result.md`（21:06）寫「前收 11/19 $145.98」（yfinance 快取）。
>   - `strike_ladder/NVDA/NVDA_ladder_2026-11-18.meta.json` 的 `spot` 145.98，`fetched_at_et 2026-11-19 19:01`，是收盤後抓的。
>   - 前一個真收盤 11/18 是 150.87（DT 19-11 第 3030 行 Previous Close）。
>   - 單日 -3.24%（scan 數字；自算 145.98/150.87-1＝-3.24%）。
> - **DT**：`SPX_data-table_2026-11-20.csv` **沒有 NVDA 列**（QQQ／SPY／TSM 也沒有，AVGO／SMH 有）。所以 **session 11/19 的 KG／PW／IVR／SkewR 全部讀不到**，最新 DT 結構仍是 DT 19-11（session 11/18）。
> - **v4／synth**：`NVDA_v4_gex_2026-11-20.csv` 和 `NVDA_synth_oi_2026-11-20.csv` 最新一列都是 **2026/11/18**。scan 頁首標 v4「🔴 真延遲，逾期 3.1h」。
> - **FP**：`flowpatrol_2026_11_20.log`，parsed 2026-11-20T21:02:08，publish 11/20，**session_date 11/19**（age=1td 🟢）。NVDA 只出現 2 列（第 264、291 行）。
> - **FN**：`19-11-2026_founders_PM.md`（6:01 PM ET）。
> - **持倉**：`brokerage_log/20-11-2026-brokerage.xlsx.log`（parsed_at 2026-11-20T10:27:34）。
> - ⚠️ **kit 連續第 2 次沒跑成**：`python3 bin/strategy_card_kit.py catalysts …` 回 `can't open file '/home/ojy/bin/strategy_card_kit.py'`，cwd 仍錯置到 `/home/ojy`。moneyness 和 `forecast_ledger.py implied` 也拿不到。TV 經濟日曆這次沒有授權。以上都標 ☐，**沒有用記憶補數字**。
>
> **前卡**：[[19-11-2026_NVDA_AUTO_strategy]] S_1（回檢對象）、[[18-11-2026_NVDA_AUTO_strategy]]。前卡清單用 find 掃過 ls_strategy 含年月子目錄：最新的人工卡是 `nov_2026/11-11-2026_NVDA_strategy.md`。

### S_1_1｜TL;DR

1. **價格：PW 150 第一次被測就失守**
   - 11/19 收 145.98，比 PW 150 低 -2.68%（PW 是 DT 19-11 的值，到 11/18 連 7 場）。
   - 也低於 DT 19-11 的 52W Low 148.8（-1.90%）。
   - 跌幅：兩場累計 -6.10%（155.46→145.98）；距 11/03 收盤 206.57 跌 -29.33%；距 DT 52W High 243.37 跌 -40.02%。
2. **大盤背景（FN 19-11 PM，只當背景）**
   - SPX -2% 收 7,176；NDX 從開盤高點跌 456bp；VIX 收 28，VVIX 127。
   - SPX 跌破 7,300 PW，QQQ 跌破 650 PW；Anthropic IPO 約 11:50 ET 掛牌後賣壓加劇。
   - NVDA 這段的同期弱勢是在**全市場去風險**的環境下發生的：同期 QQQ 663.87→640.96（-3.45%），取自持倉檔 `last=`（18-11 檔是 11/17 收盤，20-11 檔是 11/19 收盤）。
3. **結構層斷檔**
   - 11/19 場次的 DT／v4／synth 都沒有 NVDA。所以前卡待驗的「KG 150 第 2 場」「IVR<0.5」「VRP 回正」「SkewR 連 4 場」**全部未檢驗**。
   - 牆位一律標「as-of session 11/18」。
4. **FP（session 11/19）**
   - Dec18 180P 被**空方回補** 5,027 口（btc；sell_prem -17.09M，dir=BUY(prem)），屬深 ITM 的平倉，**沒有方向前瞻**。
   - heavy_daytrade 的 **tot_oi_chg -23,453,976 是源端錯值**：它的絕對值超過當日總量 4,799,159，也超過整條鏈的 OI 19,583,783（ladder asof 11/18）。**不解讀**。
5. **行動：沒有 NVDA 持倉，維持 W，不建倉、不追空**
   - X 腳（收盤 < 150）**已觸發**。依前卡規則，「破 PW＝超賣型態，不是方向訊號」，所以不追空。
   - 治理否決腳（前卡轉錄：8-K 2026-11-12 CEO 去職）維持。R 腳要等 T+10（約 12/02）。
   - 預測帳本**不寫**（S_1_5）。

**縮寫**

| 縮寫 | 意思 |
|---|---|
| DT | SG data_table |
| v4／synth | SG history_v4／synth_oi 落地檔 |
| PW／CW／HW／KG／KD | Put Wall／Call Wall／Hedge Wall／Key Gamma Strike／Key Delta Strike |
| FP | flowpatrol |
| FN | Founder's Note |
| IVR／SkewR／GarchR | IV Rank／Skew Rank（高＝call 貴）／Garch Rank |
| DR／GR | Delta Ratio／Gamma Ratio |
| VRP | IV − RV |
| IM | Implied Move（SG 欄位是日 σ） |
| OPEX | 月選擇權到期 |
| ER | 財報 |
| T+10 | 財報後第 10 個交易日 |
| ATR | Average True Range |
| ADX | 趨勢強度指標 |
| VP／POC／VAL | Volume Profile／Point of Control／Value Area Low |
| ITM／OTM | 價內／價外 |
| bto／btc／sto／stc | 買進開倉／買回平倉（空方回補）／賣出開倉／賣出平倉（多方了結） |
| HIRO | SG 即時對沖流指標 |
| NAV | 淨資產 |
| rr4u／rr6 | 持倉檔的保護總量占比／β 加權曝險占比 |
| W/R/A/X | 觸發表腳名：等待／重估／再進場／破位 |
| kit | `bin/strategy_card_kit.py` |

### S_1_2｜TREND2：跨日框架

**DT／v4 結構表**（as-of 用 Previous Close 還原；11/19 列只有價格）

| session | 收盤 | KG | HW | CW | PW | 1M IV | 1M RV | IVR | GarchR | SkewR | Skew | P/C OI | DR | IM | 來源 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 11/13 | 162.82 | 170 | 167 | 200 | 150 | 59.93% | 51.5% | 0.959 | 0.814 | 0.684 | -0.0257 | 0.879 | -0.6559 | 6.16 | DT 16-11 第 3011 行 |
| 11/16 | 156.14 | 160 | 167 | 200 | 150 | 64.08% | 53.98% | 1.000 | 0.828 | 0.604 | -0.0379 | 0.877 | -0.5585 | 6.32 | DT 17-11 第 3198 行 |
| 11/17 | 155.46 | 160 | 167 | 200 | 150 | 65.96% | 52.78% | 1.000 | 0.700 | 0.376 | -0.0659 | 0.858 | -0.5701 | 6.47 | v4 20-11 第 3 列 |
| 11/18 | 150.87 | 150 | 167 | 200 | 150 | 50.73% | 51.73% | 0.593 | 0.666 | 0.308 | -0.0802 | 0.821 | -0.4988 | 4.83 | DT 19-11 第 3030 行 |
| **11/19** | **145.98** | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | 價格：scan／ladder meta；**DT 20-11 沒有 NVDA，v4／synth 停在 11/18** |

- (1) **PW 150 跌破**
  - 最後已知的 PW 是 150（as-of 11/18，連 7 場）。11/19 收盤在它下方 -2.68%。
  - 11/19 場次 SG 有沒有把 PW 下移，**不知道**。牆位以 DT 為 SSOT，DT 缺列就不從 FN 或 scan 轉抄。
  - FN 19-11 PM 寫「NVDA dropped below its 150 Put Wall … short approximately 338K puts at the 150 strike … roughly 66K short puts at the 135 strike」。這是 SG 散文層，只作背景，**不當 135 的支撐證據**。
- (2) **HW 167（連 5 場）、CW 200（連 10 場）**：as-of 11/18，沒有更新。現價比 HW 低 -12.59%，比 CW 低 -27.01%。CW 200 是 LEAP 積木，不是有效 pin。
- (3) **vol（只到 11/18）**：1M IV 50.73%、RV 51.73%，VRP 約 -1.0pt（DT 口徑；scan synth 口徑 -1.2pt）。
  - scan：IV Pctile 94%，Fwd GARCH 55.4%（GARCH−IV +4.7pt），IV Slope -2.33（backwardation）。
  - NE 25Δ/95Δ +17.2pt，年化 +16.4pt。
  - 11/19 是大跌日，FN 寫全市場 Fixed Strike IV 上升 2–5 個 vol 點，但 **NVDA 個股讀數拿不到**。
- (4) **價格結構（scan 20-11）**
  - ADX 47.01→**48.62**，空方趨勢連續第 3 張卡加強。
  - BB %b 0.09（bandwidth 126 日 100 分位）。VWAP(week) 152.94，現價在下方。
  - VP POC 208.78／VAL 190.47，現價在價值區下緣下方。
  - ATR 停損參照 **$126.2**（ATR 6.8%×2，as-of 11-18）。
- (5) **IM 區間（scan /levels，以 145.98 為中心；IM 是日 σ 換算，只作描述）**

  | 尺度 | ±幅度 | 區間 |
  |---|---|---|
  | 日 1σ | ±4.67 | 141.31～150.65 |
  | 週 1σ | ±10.44 | 135.54～156.42 |
  | 月 1σ | ±21.40 | 124.58～167.38 |
  | 週 2σ 警戒 | — | 125.09／166.87 |

- (6) **scan 綜合裁決「暫緩進場」可接受；以下三處不採用**
  - (a) /positioning 的進場條件「(4) 2 日站穩 V4 PW：連續站穩 10 日」是用 11/18 結構算的，**跟 11/19 收 145.98 已跌破 150 直接矛盾**。scan 自己也標「現價停滯 -3.2%，資料過期」。
  - (b) Layer 0 估值基準是 11-11，已陳舊 9 天，而且早於 ER 重置點。等待區 $209–253、Bear $170 **暫停引用**；現價比 Bear 低 -14.13%，屬 model breach。FW_PE 10.1x（NTM EPS $14.46）用的是 ER 前的共識，T+10 前不可信。
  - (c) 「VVIX 恐慌買訊 ~73% 機率 5–20 日 SPX 正報酬」：這是 SPX 指數層、沒有附條件對照組的勝率宣稱，**不轉用到 NVDA**。
- (7) **scan 跟 FP 原檔矛盾，第 4 次出現**
  - scan /gex 寫「[FP·flow] flow_ratio=6.63」，那是 **11/18 場次**的值。
  - 今天 FP 原檔第 291 行是 **41.15**。scan 21:06 跑的時候，FP 已在 21:02 落地，所以 **daemon 的 FP 快取仍然沒刷新**（頁首 `loaded 2026-11-20T00:47:06`）。

### S_1_3｜TREND：即時層和事件層

#### S_1_3_1｜FP（session 11/19）

| 到期 | 腳 | bto／btc／sto／stc | buy_prem／sell_prem | dir | 讀法 |
|---|---|---|---|---|---|
| Dec18 | 180P | 0／**5,027**／0／44 | -149,624／**-17.09M** | BUY(prem) | 深 ITM（內含價值 180−145.98＝34.02）。5,027×34.02×100≈$17.10M，跟 sell_prem 量級吻合，所以是**賣 put 方以接近內含價值回補**。依 [[feedback_fp_prem_mini_index_premium_is_notional]]，BTC 記在 Sell Prem 的負值 |
| — | heavy_daytrade | tot_vol 4,799,159；abs_synth_oi_chg 116,637；**tot_oi_chg -23,453,976**；flow_ratio **41.15**（前一場 6.63） | — | — | flow_ratio＝4,799,159/116,637 驗算成立。tot_oi_chg **不成立**，見 (2) |

- (1) **180P 回補是 btc，不是看多，也不是新的看空**
  - 依 [[feedback_put_closing_not_bullish_split_btc_stc]]：先前賣 Dec 180P 的一方（收權利金、偏多或中性）在深 ITM 時認賠了結。
  - 平倉不帶前瞻方向。證據等級是 prem 級，低於 greek。
- (2) **tot_oi_chg -23.45M 是源端錯值，不能讀成「大規模平倉」**
  - 單日 OI 淨減的口數不可能超過當日成交量 4.80M（每一口平倉都要一筆成交）。
  - 它也超過整條鏈的存量 19,583,783（`NVDA_ladder_2026-11-18.meta.json` 的 `scan_oi_sum`）。
  - 同一張表的 NU（-3,029,211，量 51,868）、NVO（-1,630,916，量 63,905）、NOW（-1,512,441，量 131,553）也一樣「|ΔOI|≫量」，看起來是**系統性**的源端問題。
  - flow_ratio 41.15 用的是 abs_synth_oi_chg，不受這個問題影響：當沖／HFT 主導的程度從 6.63 跳到 41.15，排 heavy_daytrade 第 2。這是**描述**，不是方向。
- (3) **NVDA 這一場不在 p9 sig_position，也不在任何 greek 大額列** ⇒ C/P 軸（唯一有前瞻訊息的軸）**沒有讀數**。

#### S_1_3_2｜FN（背景，不作論據）

- PM 19-11：
  - 「blood on the streets day ahead of tomorrow's OPEX」。
  - 「this OPEX features the most negative gamma positioning in the past three years, with approximately 30% of gamma exposure set to roll off」。
  - QQQ 盤中流向是「longer-dated put buying」。
- NVDA 段：「elevated NVDA put trading activity … potentially reflecting positioning adjustments ahead of tomorrow's OPEX」。這跟 FP 的 180P btc 相容。
- FN 策略段仍維持「base case rally >7,600 into next week」，同時提示「Outage tail risk」。這是 SG 的指數觀點，**不轉成 NVDA 方向**。

#### S_1_3_3｜事件層（往前看）

- ☐ **catalysts 表沒產出**（kit 連續第 2 次因 cwd 失敗）。TV 經濟日曆也沒有授權，所以 CPI／FOMC 等宏觀日程本卡**沒有查**。
- 已知事件（FN 19-11 PM Sticky Banner，以及前卡）：

  | 日期 | 事件 | 跟本卡的關係 |
  |---|---|---|
  | 11/20（五） | 月 OPEX；FN 稱是 3 年來 gamma 最負，約 30% gamma 到期 | 前卡追蹤的 Nov20 172.5P 今天到期；跌破 PW 後的第一個 OPEX |
  | 11/26／11/27 | 感恩節休市／半日市 | 流動性變薄 |
  | 約 12/02 | ER 後 T+10 | 共識 EPS 才可讀，R 腳的前置條件 |
  | 12/09 | AVGO 財報（前卡 kit 11-18 的輸出） | 同業事件 |

- NVDA 剛過 ER（11/17 AMC）。11/18 IVR 從 1.000 降到 0.593 是**財報後的季節常態**，不能當成「保護便宜」。

### S_1_4｜觸發表和保護菜單

**沿用前卡觸發表之前，先重驗體質**：

| 項目 | 前卡（DT 11/18） | 本次（11/19） | 影響 |
|---|---|---|---|
| 價格對 PW | +0.58%（沒測） | **-2.68%（首測失守）** | **X 觸發** |
| 52W Low 148.8（DT） | 沒刷新 | **收盤跌破**（-1.90%） | 只描述 |
| KG／PW／HW／CW | 150／150／167／200 | ☐ 沒有 11/19 結構 | 沿用 as-of 11/18 的值，並標明 |
| IVR／VRP／SkewR | 0.593／-1.0pt／0.308 | ☐ | A 腳的 vol 條件**沒辦法重驗**，視為還沒達到 |
| ADX | 47.01 | **48.62** | 空方趨勢加強；不接刀 |
| 治理 | 否決確立 | 沒有新的一手資訊 | 否決維持 |
| 估值 | 基準 11-11，陳舊 | 陳舊 9 天；比 Bear 低 -14.13% | zone 暫停引用，等 T+10 |
| 大盤 | — | SPX／QQQ 雙雙破 PW，VIX 28 | 系統性去風險，個股訊號被大盤 β 汙染 |

體質變化：**X 已觸發**，其他腳的前提都沒改變。觸發表更新如下：

| 腳 | 條件 | 依據 | 動作 |
|---|---|---|---|
| **W 等待（現行）** | R 還沒完成 | 估值陳舊，治理否決腳還在 | **不建倉** |
| **否決（仍確立）** | CEO 去職（8-K 2026-11-12，前卡轉錄） | 治理 regime break | 舊的多頭腳全部作廢 |
| **X 破位（已觸發 11/19）** | 收盤 < 150 | 破 PW＝超賣型態，不是方向訊號（[[feedback_risk_pivot_is_vol_gate_not_direction]]） | **不追空**；沒有部位，所以不需要買凸性 |
| **R 重估** | (1) ≥T+10（約 12/02）共識 EPS 更新；(2) user 裁決 base_pe 要不要加治理折價；(3) 財報和 8-K 用一手來源核實 | [[feedback_er_consensus_feed_lag_window]]；[[feedback_conservative_base_pe_no_rerating]] | 重跑 zone，重訂 A 腳 |
| **A 再進場（待 R）** | (1) R 完成；(2) IVR < 0.5；(3) VRP > 0 才考慮賣 put 類；(4) 價格落在 R 重估後的等待區 | 估值腳、vol 腳，加上 VRP<0 的賣方否決條件 | VRP≤0 只考慮 defined-risk 的 call 價差；不裸買 call |
| 狀態描述（不是觸發） | DT 恢復收錄 NVDA 之後，PW 是否下移；連 2 場收盤回到 150 上方 | 多場次持續性；紀律 (d) | 只描述，**不連到進場或保護決策** |
| 狀態描述（不是觸發） | 135（FN：66K short puts）、ATR 126.2、週 2σ 125.09 | FN 散文、scan 計算值 | **不是承接位**；只當距離參照 |

**保護菜單**：沒有 NVDA 持倉，所以**不需要 NVDA 保護**。
- 間接曝險（`20-11-2026-brokerage.xlsx.log`）：
  - QQQ 116 股、QQQ Jun17'27 700C×4／710C×2。
  - SMH May21'27 525C×2（mv 5,935）、SOXX Feb19'27 165C×9（mv 5,052）。
  - NAV 401,476.01；現金 19.94%；**rr4u 0.00%**；rr6 211.13%。
- 指數和板塊桶的保護菜單，看同日的 `20-11-2026_QQQ_AUTO_strategy.md`、`20-11-2026_SMH_AUTO_strategy.md`、`20-11-2026_SOXX_AUTO_strategy.md`。
- **不要用 NVDA put 去保 QQQ 或半導體桶**，那是載體錯配（[[feedback_hedge_carrier_use_tail_quantiles_not_ev]]）。
- 保護「便宜／貴」：☐ moneyness 沒跑成，**本卡沒有 mgrid 行**，不做判斷（紀律 (b)）。下一張卡在美東盤中補跑：`--exp 2026-12-18,2027-01-15`。

預測帳本：本章**不寫**（S_1_5）。

### S_1_5｜預測帳本

本章**不寫入**，原因有二：
- (1) `forecast_ledger.py implied` 因 cwd 錯置沒跑成，**拿不到 IV 隱含基準**。
- (2) 我方說不出偏離 IV 的機率依據：
  - 「破 PW 之後」的條件守住率或反彈率，沒有已驗證的 NVDA 子集。全母體 PW 守住率 66.7% 是守住前的口徑，不能直接套到已跌破的情境。
  - FN 的 135 short put 是散文層。
- 依 runbook，說不出依據的預測不進帳本。

### S_1_6｜前卡回檢（[[19-11-2026_NVDA_AUTO_strategy]] S_1）

| 前卡宣稱／可證偽點 | 分類 | 證據 |
|---|---|---|
| X：收盤 < 150 | **觸發** | 11/19 收 145.98（scan 前收；ladder meta spot，取於 ET 19:01） |
| X 的動作：「不追空」 | 規則，不是預測；結果**未檢驗** | 要等後續場次才知道破位後的走法 |
| W：不建倉 | 規則；事後看**避開了 -3.24%** | 150.87→145.98 |
| 「150 承接」 | 前卡**沒寫**（列為未檢驗）；**本次被測且失守** | 第一次測試就以收盤 -2.68% 跌破。scan 11/18 寫的「貼近 PW 強支撐試探」，在收盤口徑上被否定 |
| scan「進場條件 4/5」不採用 | 決策**符合事後結果**（描述） | 如果採用，次一場收盤 -3.24% |
| 狀態描述：DT 20-11 的 KG 是否仍是 150 | **未檢驗** | DT 20-11 沒有 NVDA 列 |
| 待驗 (1)：補跑 kit | **失敗**（第 2 次） | 同樣是 `/home/ojy/bin/...` 的 cwd 錯誤 |
| 待驗 (2)：IVR<0.5／VRP 回正／SkewR 連 4 場 | **未檢驗** | 11/19 結構缺資料 |
| 待驗 (3)：strike_ladder asof 11-18 的 ΔOI | **未檢驗** | 檔案已落地（`NVDA_ladder_2026-11-18.csv.gz`），但本次執行環境不能解壓 gz，只讀了 meta |
| 待驗 (6)：scan 的 FP 快取 | **第 4 次出現** | scan 寫 flow_ratio 6.63（11/18 場次），原檔是 41.15 |
| Nov20 172.5P 的開平倉 | **未檢驗** | 今天到期，ΔOI 沒讀到 |

**待驗（下一張卡）**：
- (1) **修自動執行環境的 cwd**：kit 和 forecast_ledger 已經連續 2 張卡沒跑成，catalysts、moneyness、implied 全部缺。
- (2) **DT 21-11（session 11/20）有沒有恢復收錄 NVDA**：PW 是否下移（只認多場次）；IVR、VRP、SkewR 在 11/19 大跌之後的讀數。也要查 DT 20-11 為什麼漏掉 QQQ／SPY／TSM／NVDA 這批主要標的。
- (3) **v4／synth 補上 11/19**：scan 標 v4 真延遲；要跑 `roma_cli sgfetch` 重抓。
- (4) **FP tot_oi_chg 源端錯值**：NVDA、NU、NVO、NOW 同場次都出現「|ΔOI|>量」。要查是 SG 源端還是 parser 的問題；在查清楚之前，p17 的 tot_oi_chg 欄不引用。
- (5) **strike_ladder**：解 asof 11-18／11-19 的 Dec 180P、150P、135P，以及前卡列出的各腳 ΔOI。V/OI≈1 才能寫「新開倉」。
- (6) **R 腳**：T+10（約 12/02）之後重跑估值；user 裁決 base_pe 要不要加治理折價。
- (7) **scan daemon 重啟**：FP 快取第 4 次沒刷新（`loaded 2026-11-20T00:47:06`）。
