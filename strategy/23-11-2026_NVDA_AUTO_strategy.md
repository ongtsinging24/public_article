# NVDA 策略卡（自動，FP 落地後 TREND2+TREND）

## S_1｜AUTO NVDA TREND2+TREND 21:13｜11/20 SEC 會計調查報導後收 125.79（-13.84%），已在 PW 150 下方 -16.1%、貼近 52W Low 124.5；治理否決從一層變兩層；IVR 1.00、SkewR 0.008，put 端極貴；無持倉，維持 W，不追空也不接刀，預測帳本補跑不寫

> **[回補] 原輪 11-23 21:13 陣亡，2026-11-24 補跑**
>
> **資料 as-of**：2026-11-23 21:13 GMT+8，等於 08:13 ET，是美東 11/23（一）盤前
> - **最後一個真收盤**：11/20 **$125.79**，兩個來源一致：
>   - DT `SPX_data-table_2026-11-22.csv`／`-23.csv` 第 3152 行的 Previous Close。這兩個檔大小相同（1,311,294），是週末同一份。
>   - FP `flowpatrol_2026_11_23.log` 的 NVDA 列 `px=125.79`，`1dR=-13.84%`，`5dR=-22.74%`。
>   - scan `23-11-2026_NVDA_scan_result.md`（21:06）寫的是 yfinance 快取 $125.53，差 0.21%。本卡採 DT／FP 的 125.79。
> - **DT**：最新到 session 11/20（DT 22-11／23-11）。DT 21-11 已補回 session 11/19 的 NVDA 列（第 3106 行）。
> - **v4／synth**：scan 頁首寫 `v4 td=2026-11-20`、`synth td=2026-11-19`，scan 標 synth「🔴 真延遲」。
> - **FP**：`flowpatrol_2026_11_23.log`，parsed 2026-11-23T21:01:35，publish 11/23，**session_date 11/20**（age=1td 🟢）。
> - **FN**：`23-11-2026_founders_AM.md`（7:00 AM ET）、`20-11-2026_founders_PM.md`、`22-11-2026_sg_weekly.md`。**沒有讀** `23-11-2026_founders_PM.md`，它的 mtime 是 11-24 10:42，晚於 as-of。
> - **持倉**：`brokerage_log/20-11-2026-brokerage-02.xlsx.log`（parsed_at 2026-11-20T22:26:31；mtime 11-23 10:18，早於 as-of）。
> - **事後資訊（補跑時點）**：kit 的 catalysts／moneyness 取數時間是 2026-11-23 22:52 ET，晚於 as-of。另外，人工卡 `ls_strategy/23-11-2026_NVDA_strategy.md` 的 mtime 是 11-24 11:19，也晚於 as-of，所以**沒有拿來當輸入**，只在 S_1_6 列為事後對照。
>
> **前卡**：用 find 掃過 ls_strategy 和年月子目錄。最新 AUTO 卡是 [[20-11-2026_NVDA_AUTO_strategy]] S_1（本次回檢對象），最新人工卡（as-of 之前）是 `nov_2026/11-11-2026_NVDA_strategy.md`。

### S_1_1｜TL;DR

1. **價格：破 PW 之後第二場又跌 -13.84%**
   - 11/19 收 146.00，11/20 收 125.79（DT Previous Close；FP 1dR -13.84%）。
   - 現價和各參照位的距離：
     - PW 150：-16.14%
     - Bear 線 $170：-26.0%
     - DT 52W Low 124.5：只高 +1.04%
     - 11/03 收盤 206.57（前卡引用）：-39.1%
     - DT 52W High 243.37：-48.3%
2. **事件：SEC 會計調查**
   - FN 20-11 PM 寫「NVDA sinking 14% after Reuters reported that U.S. regulators were investigating its accounting practices」。
   - 外部核實：Reuters 11/20 獨家報導，引兩位知情人士說 SEC 在檢視 NVDA 的會計，具體是哪些做法還不清楚，SEC 不予置評（[Bloomberg 轉述 Reuters](https://www.bloomberg.com/news/articles/2026-11-20/wall-street-regulator-probing-nvidia-s-accounting-reuters-says)、[Investing.com／Reuters](https://www.investing.com/news/economy-news/exclusiveus-secs-nvidia-probe-is-examining-potential-accounting-issues-sources-say-5042460)）。
   - ⇒ 治理否決從「CEO 去職」**一層變兩層**，再加上「會計調查」。這是**消息來源報導**，不是公司 8-K。
3. **結構（DT session 11/20）**
   - KG 150→**135**，KD 110→**80**，HW 152→**165**。這三個都是**單場跳動**，依多場次持續性規則**不當牆位**。
   - PW 150 已經連 10 場（11/06 到 11/20 這段 DT 都是 150），CW 200 也不動，但兩個都離現價很遠。
4. **vol（DT session 11/20）**
   - 1M IV 72.41%、RV 65.99%，VRP **+6.42pt（轉正）**。
   - IVR **1.00**、GarchR **1.00**、SkewR **0.008**：put 端相對 call 端貴到極端。
   - ⇒ 在這裡買保護是**最貴**的時候。
5. **FP（session 11/20）**
   - Jan'29 240C 有人**賣出開倉（sto）29,619 口**，收權利金 $65.32M（v$ -2.12M，SELL(greek)）。
   - Jan'28 200P 是深 ITM 平倉，大約 6,027 口，平倉後 OI 只剩 8。
   - 兩者都是**買賣軸／深 ITM 的訊息**，依 memory **不帶前瞻方向**。
6. **行動：沒有 NVDA 持倉，維持 W**
   - 不追空：已經在 PW 下 16%、ATR 停損參照 $104.1 的上方。
   - 不接刀：ADX 50.64、治理否決兩層、估值框架 breach。
   - R 腳要等 T+10（約 12/02），**再加上 SEC 調查要有一手資訊**。
7. 預測帳本：**補跑不寫**。

**縮寫**

| 縮寫 | 全名（說明） |
|---|---|
| DT | SG data_table（牆位 SSOT） |
| v4／synth | SG history_v4／synth_oi 落地檔 |
| PW／CW／HW／KG／KD | Put Wall／Call Wall／Hedge Wall／Key Gamma Strike／Key Delta Strike |
| FP | flowpatrol（SG 期權流向日報） |
| FN | Founder's Note（SG 每日筆記） |
| IVR／SkewR／GarchR | IV Rank／Skew Rank（高＝call 貴，低＝put 貴）／Garch Rank |
| VRP | IV − RV（隱含減實現波動） |
| IM | Options Implied Move（SG 欄位，是日 σ） |
| ATR | Average True Range（平均真實波幅） |
| ADX | Average Directional Index（趨勢強度） |
| VP／POC／VAL | Volume Profile／Point of Control／Value Area Low |
| ITM／OTM | 價內／價外 |
| bto／btc／sto／stc | 買進開倉／買回平倉／賣出開倉／賣出平倉 |
| OPEX | 月選擇權到期日 |
| ER | 財報 |
| T+10 | 財報後第 10 個交易日 |
| SEC | U.S. Securities and Exchange Commission（美國證管會） |
| COR1M | Cboe 1 個月隱含相關性指數 |
| VVIX | VIX 的波動率指數 |
| rr4u／rr6 | 持倉檔的保護總量占比／β 加權曝險占比 |
| W/R/A/X | 觸發表腳名：等待／重估／再進場／破位 |
| kit | `bin/strategy_card_kit.py` |
| mgrid | kit 輸出的同 moneyness IV 格線 |

### S_1_2｜TREND2：跨日框架

**DT 結構表**（as-of 用 Previous Close 還原場次）

| session | 收盤 | KG | KD | HW | CW | PW | 1M IV | 1M RV | VRP | IVR | GarchR | SkewR | P/C OI | IM | 52W Low | 來源 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 11/13 | 162.82 | 170 | 110 | 167 | 200 | 150 | 59.93% | 51.50% | +8.4 | 0.959 | 0.814 | 0.684 | 0.879 | 6.16 | 148.8 | DT 14-11 第 3011 行 |
| 11/16 | 156.14 | 160 | 110 | 167 | 200 | 150 | 64.08% | 53.98% | +10.1 | 1.000 | 0.828 | 0.604 | 0.877 | 6.32 | 148.8 | DT 17-11 第 3198 行 |
| 11/17 | 155.46 | 160 | 110 | 167 | 200 | 150 | 65.96% | 52.78% | +13.2 | 1.000 | 0.700 | 0.376 | 0.858 | 6.47 | 148.8 | DT 18-11 第 3175 行 |
| 11/18 | 150.87 | 150 | 110 | 167 | 200 | 150 | 50.73% | 51.73% | -1.0 | 0.593 | 0.666 | 0.308 | 0.821 | 4.83 | 148.8 | DT 19-11 第 3030 行 |
| 11/19 | 146.00 | 150 | 110 | **152** | 200 | 150 | 52.22% | 51.77% | +0.45 | ☐ 空欄 | ☐ 空欄 | ☐ 空欄 | 0.792 | 4.81 | 145.71 | DT 21-11 第 3106 行 |
| **11/20** | **125.79** | **135** | **80** | **165** | 200 | 150 | **72.41%** | **65.99%** | **+6.42** | **1.000** | **1.000** | **0.008** | 0.805 | 5.75 | **124.5** | DT 22-11／23-11 第 3152 行 |

（DT 20-11 沒有 NVDA 列，前卡已記。11/20 的 Call／Put Volume 是 3,102,119／2,183,403，股票量 275.7M，約為 11/19 的 1.9 倍。）

- (1) **牆位持續性**
  - PW 150：從 11/13 起每一場都是 150，有效。
  - CW 200：同樣長期不動。依 memory，CW 200 是 LEAP 積木，不是 pin。
  - 現價在 PW 下方 -16.14%。scan 寫「Put Wall 轉壓力：$150」，這只能當**狀態描述**（紀律 (d)）。
  - KG 150→135、KD 110→80、HW 167→152→165 都只有 1 場，屬噪音層。**不把 135 寫成支撐或壓力**。
- (2) **vol 狀態改變**
  - VRP 從 11/18 的 -1.0 變成 11/20 的 +6.42（DT 口徑）。scan 用 synth 定義自算 RV 69.0%，VRP 是 +3.4pt。兩個口徑**同號**。
  - IVR、GarchR 同時到 1.00，SkewR 0.008。
  - 依 memory「Skew Rank 高＝call 貴」，0.008 代表 put 相對 call 端是一年內最貴的位置。
  - scan /vol 判「Vol 明顯昂貴（-3/5）」，IV Slope -2.50，是倒掛。
- (3) **價格結構（scan 23-11）**
  - ADX 47.01（11/18）→48.62（11/19）→**50.64**（11/20），空方趨勢連續第 4 張卡加強。
  - BB %b -0.03，bandwidth 是 126 日的 100 分位。VWAP(week) 144.97，VP POC 211.18／VAL 188.89。現價在價值區下緣下方很遠。
  - ATR 停損參照 **$104.1**（ATR 8.5%×2，as-of 11/19）。
- (4) **IM 區間（scan /levels，以 125.53 為中心；IM 是日 σ 換算，只作描述）**

  | 尺度 | ±幅度 | 區間 |
  |---|---|---|
  | 日 1σ | ±5.74 | 119.79～131.27 |
  | 週 1σ | ±12.83 | 112.70～138.36 |
  | 月 1σ | ±26.29 | 99.24～151.82 |
  | 週 2σ 警戒 | — | 99.87／151.19 |

- (5) **scan 綜合裁決「暫緩進場」可接受；以下四處不採用**
  - (a) Layer 0 寫「🟢 超跌區，分批佈局機會」不採用。估值基準 11-11，已陳舊 12 天，早於 ER 和 SEC 報導。scan 自己也標「現價已跌破 Bear target $170，估值框架可能失效（model breach）」。FW_PE 8.7x（NTM EPS $14.46）用的是 ER 前的共識，T+10 前不可信。
  - (b) /bias「結構評分 +4／10 偏多」用的是 2026/11/19 結構日、20 日窗，而且是未經前瞻驗證的描述。不採用。
  - (c) 「VVIX 恐慌買訊 ~73% 機率 5–20 日 SPX 正報酬」：這是 SPX 指數層、沒有附條件對照組的宣稱，不轉用到 NVDA（同前卡）。
  - (d) **scan 跟 FP 原檔矛盾，第 5 次出現**
    - scan /gex 寫「[FP·flow] flow_ratio=41.15」，那是 session 11/19 的值。
    - 今天 FP 原檔第 302 行是 **8.22**。
    - 原因：scan 頁首 `loaded 2026-11-23T15:50:45`，比 FP 落地時間 21:01 早。頁首也標「🔴 記憶體落後磁碟 6 檔（需重啟 daemon）」。

### S_1_3｜TREND：即時層和事件層

#### S_1_3_1｜FP（session 11/20，`flowpatrol_2026_11_23.log`）

| 行 | 到期 | 腳 | 數值 | dir | 讀法 |
|---|---|---|---|---|---|
| 163／178／260 | Jan'29 | 240C | bto 332／btc 0／**sto 29,619**／stc 0；sell_prem **65.32M**；v$ **-2.12M**；oi 39,075 | SELL(greek) | 長天期 call 賣出開倉。換算約 $22.05／股（65.32M÷29,619÷100）。IVR 1.00 時賣 vega，偏收租／overwrite。買賣軸**不帶前瞻**（[[project_fp_p9_extreme_greek_forward_return]]） |
| 164 | Jan'29 | 200C | v$ +626,453；oi 21,368 | BUY(greek) | 跟 240C 同一個到期，可能是 200／240 的組合。但 v$ 比例約 1:3.4，不是 1:1，spread 標籤也是空的 ⇒ **不判成 BuCS**（[[feedback_fp_spread_label_leg_check]]） |
| 162 | Jan'28 | 210C | v$ +657,471；oi 21,556 | BUY(greek) | 描述 |
| 177 | Jan'28 | 200P | prem **-44.73M**；**oi 8** | SELL(prem) | 深 ITM（內含價值 200−125.79＝74.21）。44.73M÷(74.21×100)≈**6,027 口**，跟內含價值量級吻合。平倉後 OI 只剩 8 ⇒ **平倉**。但 prem 級證據分不出是 btc 還是 stc（[[feedback_put_closing_not_bullish_split_btc_stc]]），**方向不判** |
| 176 | Dec18 | 115P | prem +1.92M；oi 15,911 | BUY(prem) | 規模小，描述 |
| 302 | — | heavy_daytrade | tot_vol 9,092,747；abs_synth_oi_chg 1,106,213；tot_oi_chg 1,053,379；flow_ratio **8.22**（前一場 41.15） | — | 這次 tot_oi_chg 小於成交量，**前卡記的源端錯值沒有再出現**。當沖主導程度明顯回落 |

- (1) **開平倉軸**
  - 240C 的 bto+sto 共 29,951，oi 39,075。V/OI≈0.77，不到 ≈1。依 [[feedback_open_close_axis_needs_delta_oi]]，**不能單憑 sto 寫成「全數新開倉」**。
  - 要判開倉占多少，需要 strike_ladder asof 11/19→11/20 的 ΔOI：☐ 本次沒讀（gz 檔）。
- (2) **C/P 軸**：NVDA 這一場沒有出現在 p9 sig_position 的 C／P 大額榜，所以唯一有前瞻訊息的軸**沒有讀數**。
- (3) **板塊旁證**（FP 第 58 行，SG 摘要）
  - SOXX Dec 2026 125P 有 24,191 口買進開倉，$142.81M。
  - 我方持有 SOXX Feb19'27 165C×9，這筆跟我方有關，但屬於 SOXX 卡的範圍。

#### S_1_3_2｜FN／Weekly（背景，不作論據）

- **PM 20-11**
  - QQQ -6% 收 609，SOXX -11% 收 123，NVDA -14%（Reuters 會計調查），ANT -9%。
  - SPX -4% 收 6,910；VIX 收 36、VVIX 收 138。
  - S&P Equities HIRO 約 -$5bn，主要由約 $3bn 的**單一個股 call 賣出**造成，SG 解讀為逢低 call 部位的拆除。
- **Weekly 22-11**
  - COR1M 4 天內從 13 升到 46，「everything trades as one」。
  - OPEX 時 put 占到期部位 80% 以上，上次出現是 2025 年 4 月。
  - SG 原文：「positional analysis suggests the market is less fragile after Friday's OPEX, although by no means fully repaired」。
- **AM 23-11（7:00 ET）**
  - 期指 +2.75%，SPX 看到 11/30 的高點在 7,400–7,500。
  - SG 原文：「this rally is very unstable … unlikely to last past this week」。
  - FN 點名的風險清單：「NVDA, AI & credit, outages, war(s), rates」。
- ⇒ 11/20 的大跌是**個股消息加上全市場相關性飆升、負 gamma**疊加的結果。NVDA 個股訊號被大盤 β 嚴重汙染。

#### S_1_3_3｜事件層（往前看，紀律 (a)）

kit catalysts（**事後資訊**：取數 2026-11-23 22:52 ET，晚於 as-of；這份日曆跟時點無關，所以照貼）：

| 日期（ET） | 標的 | 事件 | 反應場次 | 到期／履約價 | 隱含波幅（0.85×straddle） |
|---|---|---|---|---|---|
| 2026-12-09 | AVGO | 財報 AMC | 2026-12-10 | 2026-12-11 K=315 | ±11.5%（straddle 42.38） |
| 2026-12-17 | MU | 財報 AMC | 2026-12-18 | 2026-12-18 K=710 | ±15.1%（straddle 126.10） |
| 2027-01-14 | TSM | 財報（窗口外） | — | — | — |
| 2027-02-02 | AMD | 財報（窗口外） | — | — | — |
| — | NVDA | 財報（下次未公告） | — | — | — |

其他已知事件：

| 日期 | 事件 | 跟本卡的關係 |
|---|---|---|
| 11/26／11/27 | 感恩節休市／半日市（FN 橫幅） | 流動性變薄；SG Weekly 提到假期 theta |
| 約 12/02 | ER（11/17 AMC）後 T+10 | 共識 EPS 才可讀，R 腳的前置條件 |
| 未定 | SEC 調查的後續（公司回應、8-K、範圍） | **新增否決腳的解除條件** |
| 12/18 | 12 月 OPEX；DT 的 Top Gamma Exp 是 12-19 | 依 memory，DT 這個欄位系統性晚一天 |

- 宏觀（CPI／FOMC）：☐ 本次沒查 TV 日曆。
- IVR 1.00 **不是**財報後的季節常態：前卡 11/18 IVR 已經降到 0.593，11/20 又因事件衝擊回到 1.00。所以這裡**沒有「保護便宜」的問題，而是保護最貴**。

### S_1_4｜觸發表和保護菜單

**沿用前卡觸發表之前，先重驗體質**：

| 項目 | 前卡（11/19 收 145.98） | 本次（11/20 收 125.79） | 影響 |
|---|---|---|---|
| 價格對 PW 150 | -2.68% | **-16.14%** | X 早已觸發；距離拉大 |
| 52W Low | 跌破 148.8 | DT 改成 **124.5**，現價只高 +1.04% | 只描述 |
| KG／HW | 150／167 | 135／165（單場） | 不採用 |
| IVR／VRP／SkewR | 0.593／-1.0／0.308（11/18） | **1.00／+6.42／0.008** | A 腳的 IVR<0.5 **遠未達成**；VRP>0 已滿足 |
| ADX | 48.62 | **50.64** | 不接刀 |
| 治理 | CEO 去職否決 | **加上 SEC 會計調查（Reuters 11/20）** | 否決**加重** |
| 估值 | 陳舊 9 天，比 Bear 低 -14.13% | 陳舊 12 天，**比 Bear 低 -26.0%** | zone 暫停引用 |
| 大盤 | SPX／QQQ 破 PW | COR1M 46，SPX 收 6,910 | β 汙染更重 |

觸發表更新如下：

| 腳 | 條件 | 依據 | 動作 |
|---|---|---|---|
| **W 等待（現行）** | R 還沒完成 | 估值陳舊，否決兩層 | **不建倉** |
| **否決 1（仍確立）** | CEO 去職（前卡轉錄：8-K 2026-11-12） | 治理 regime break | 舊多頭腳全部作廢 |
| **否決 2（新增）** | SEC 會計調查（Reuters 11/20，消息人士，範圍不明） | 會計是 EPS 分母本身的可信度問題，NTM EPS 不能直接用 | 解除條件見 R 腳 (4) |
| **X 破位（11/19 已觸發）** | 收盤 < 150 | 破 PW 是波動閘，不是方向訊號（[[feedback_risk_pivot_is_vol_gate_not_direction]]） | **不追空**；IVR 1.00 時買 put 是最貴的；沒有部位，不需要凸性 |
| **R 重估** | (1) ≥T+10（約 12/02）共識 EPS 更新；(2) user 裁決 base_pe 是否加治理和會計折價；(3) 財報、8-K 用一手來源核實；**(4) SEC 調查要有公司正式回應或揭露範圍** | [[feedback_er_consensus_feed_lag_window]]；[[feedback_conservative_base_pe_no_rerating]] | 重跑 zone，重訂 A 腳 |
| **A 再進場（待 R）** | (1) R 完成；(2) IVR < 0.5；(3) VRP > 0 才考慮賣 put 類；(4) 價格落在重估後的等待區 | 估值、vol、賣方條件 | VRP≤0 只考慮 defined-risk call 價差；不裸買 call |
| 狀態描述（不是觸發） | PW 150 是否下移（要多場）；連 2 場收盤回到 150 上方 | 紀律 (d) | 只描述，**不連到進場或保護決策** |
| 狀態描述（不是觸發） | 52W Low 124.5、ATR 停損 104.1、週 2σ 99.87 | DT 欄位／scan 計算值 | **不是承接位**；只當距離參照 |

**保護菜單**：沒有 NVDA 持倉，所以**不需要 NVDA 保護**。
- 間接曝險（`20-11-2026-brokerage-02.xlsx.log`）：
  - QQQ 116 股（last=637.68）；QQQ Jun17'27 700C×4、710C×2。
  - SMH May21'27 525C×2（mv 5,935）、SOXX Feb19'27 165C×9（mv 5,052）。
  - NAV 398,440.74；現金 rr5 20.16%；**rr4u 0.00%**；rr6 205.48%。
- 指數和板塊桶的保護菜單，看同日的 `23-11-2026_QQQ_AUTO_strategy.md`、`23-11-2026_SMH_AUTO_strategy.md`、`23-11-2026_SOXX_AUTO_strategy.md`。
- **不要用 NVDA put 去保 QQQ 或半導體桶**，那是載體錯配（[[feedback_hedge_carrier_use_tail_quantiles_not_ev]]）。何況 NVDA SkewR 0.008，put 端是一年內最貴。
- 保護「便宜／貴」的 mgrid：**事後資訊**，S＝11/23 收盤，不是 as-of 價。前卡沒有 mgrid，所以沒有 Δpp 可比，只登錄給下一張卡：

```
mgrid NVDA 2026-12-18 S=165.05@2026-11-23 -15:0.7336 -10:0.6937 -5:0.6575 +0:0.6389 +5:0.6485
mgrid NVDA 2027-01-15 S=165.05@2026-11-23 -15:0.6087 -10:0.5886 -5:0.5635 +0:0.5490 +5:0.5645
```

預測帳本：補跑不寫。

### S_1_5｜預測帳本

**補跑不寫**。這是事後補跑，寫進去會污染校準。另外，本輪我方也說不出偏離 IV 的機率依據：破 PW 16% 之後的反彈率或續跌率，沒有已驗證的 NVDA 子集。

### S_1_6｜前卡回檢（[[20-11-2026_NVDA_AUTO_strategy]] S_1，紀律 (c)）

| 前卡宣稱／可證偽點 | 分類 | 證據（as-of 11/20 收盤） |
|---|---|---|
| W：不建倉 | 規則；事後看**避開了 -13.84%** | 146.00→125.79（DT／FP） |
| X 動作：「不追空」（破 PW＝超賣型態） | 規則，**未檢驗** | 破位後第 1 場續跌 -13.84%，所以「超賣」在 1 場內沒有得到支持；前卡沒有給窗口，不能判成立或證偽 |
| 「150 不是承接」／135、ATR 126.2、週 2σ 125.09 都「不是承接位」 | **成立**（描述性宣稱） | 11/20 收 125.79，跌穿 135 和 ATR 126.2，停在週 2σ 125.09 上方 +0.55% |
| 待驗 (2)：DT 恢復收錄 NVDA；PW 是否下移 | **成立**（已恢復）；PW **2 場都沒下移**（11/19、11/20 都是 150） | DT 21-11 第 3106 行、DT 22-11 第 3152 行 |
| 待驗 (2)：IVR<0.5／VRP 回正 | IVR：**證偽**（升到 1.00）；VRP：**回正**（+6.42） | DT 22-11 |
| 待驗 (3)：v4／synth 補上 11/19 | 部分成立：v4 補到 td 11/20，synth 停在 td 11/19（真延遲） | scan 23-11 頁首 |
| 待驗 (4)：FP tot_oi_chg 源端錯值 | 本場**沒有再出現**（1,053,379 < 成交量 9,092,747）；根因**未檢驗** | FP 第 302 行 |
| 待驗 (5)：strike_ladder ΔOI | **未檢驗** | 本次沒讀 gz |
| 待驗 (1)：kit cwd | **已修復**（本次以 repo 根目錄的相對路徑跑成） | catalysts／moneyness 有輸出（時點是事後） |
| 待驗 (7)：scan FP 快取 | **第 5 次出現** | scan 41.15 vs 原檔 8.22；daemon loaded 15:50 |
| 治理否決維持 | **成立並加重** | Reuters 11/20 SEC 會計調查 |

**事後資訊（補跑時點，不影響上面 as-of 的判讀）**：
- kit moneyness 寫 `S=165.05@2026-11-23`。換算 11/23 收盤比 11/20 的 125.79 高 **+31.2%**。
- 人工卡 `23-11-2026_NVDA_strategy.md` 的標題，把這次大漲歸因到 Jensen 回任。這是 as-of 之後才發生的事件，本章**沒有用它作判讀輸入**。
- 這一場也說明，W 加上「不追空」在事後**避開了軋空**。但它屬於**單一事件**，不構成 edge 證據。

**待驗（下一張卡）**：
- (1) **SEC 調查的一手資訊**：公司聲明或 8-K、範圍（Reuters 提到可能跟地理營收揭露口徑有關，但**無法確定**）。
- (2) **CEO 事件有沒有逆轉**（事後資訊顯示有）：要用一手 8-K 核實。如果確立，「否決 1」要重裁，交由 user 決定。
- (3) **PW 150 會不會在 11/23 之後的 DT 下移或被收復**：只認多場次。
- (4) **mgrid 用 `--prev` 帶入上面兩行**，看逐格 Δpp。
- (5) **strike_ladder 解 Jan'29 240C、Jan'28 200P 的 ΔOI**：判 240C 實際新開倉多少。
- (6) **R 腳**：T+10（約 12/02）後重跑估值；user 裁決 base_pe 是否加治理和會計折價。
- (7) **scan daemon 重啟**：FP 快取第 5 次沒刷新，記憶體落後磁碟 6 檔。

Sources:
- [Bloomberg — Wall Street Regulator Probes Nvidia Accounting, Reuters Says](https://www.bloomberg.com/news/articles/2026-11-20/wall-street-regulator-probing-nvidia-s-accounting-reuters-says)
- [Investing.com／Reuters — Nvidia's accounting is a focus of US SEC investigation, sources say](https://www.investing.com/news/economy-news/exclusiveus-secs-nvidia-probe-is-examining-potential-accounting-issues-sources-say-5042460)
