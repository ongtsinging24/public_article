# NVDA 策略卡（自動，FP 落地後 TREND2+TREND）

## S_1｜AUTO NVDA TREND2+TREND 21:54｜11/23 收 165.19（+31.32%），收回 PW 150 上方 +10.1%；11/23 的 FP 是止盈加保護上移，沒有新的方向押注；無持倉，維持 W，IVR 0.75 沒達 A 腳門檻，不寫預測帳本

> **資料 as-of**：2026-11-24 21:54 GMT+8，等於 08:54 ET，是美東 11/24（二）**盤前**。
> - **最後一個真收盤**：11/23 **$165.19**。兩個來源一致：
>   - DT `SPX_data-table_2026-11-24.csv` 第 3001 行的 Previous Close。同一行的 Current Price 是 165.21。
>   - FP `flowpatrol_2026_11_24.log` 的 NVDA 列：`px=165.19`、`1dR=31.32%`、`5dR=5.79%`。
>   - scan／kit 用的是 yfinance 快取 165.05，差 −0.08%。本卡採 DT／FP 的 165.19。
> - **DT**：session 11/23（DT 24-11）。
> - **v4／synth**：scan 頁首是 `v4 td=2026-11-23`、`synth td=2026-11-23`，兩個都已補上。
> - **scan**：`24-11-2026_NVDA_scan_result.md` 21:05:46。頁首 `loaded 2026-11-24T11:25:58 | src ✅`，**沒有**「記憶體落後磁碟」的警告。
> - **FP**：`flowpatrol_2026_11_24.log`，parsed 2026-11-24T21:02:00，publish 11/24，**session_date 11/23**（age=1td 🟢）。
> - **持倉**：`brokerage_log/24-11-2026-brokerage.xlsx.log`，parsed_at 2026-11-24T07:51:03。
> - **kit**：catalysts 和 moneyness 都在 2026-11-24 08:55 ET 取數，屬於**盤前**。
>
> **前卡**：用 find 掃過 ls_strategy 和年月子目錄。最新 AUTO 卡是 [[23-11-2026_NVDA_AUTO_strategy]] S_1（回補卡，as-of 11/20 收盤）。最新人工卡是 [[23-11-2026_NVDA_strategy]] S_1，盤中 10:45 ET，裡面有 user 裁決 (i)。兩張都在 S_1_5 回檢。

### S_1_1｜TL;DR

1. **價格**：11/23 收 165.19，比 11/20 的 125.79 高 +31.32%（DT／FP）。和各參照位的距離：
   - PW 150：−9.20%
   - HW 162：−1.93%
   - KG／Bear 170：+2.91%
   - 辭職前收盤 173.73（人工卡轉錄）：+5.17%
   - VAL 188.89：+14.35%
   - CW 200：+21.07%
2. **結構（DT session 11/23）**
   - **PW 150 從 11/13 起每一場都沒動**。CW 200 也長期不動。
   - KG 135→**170**、KD 80→**170** 都是單場跳動，**不當牆位**。
   - HW 在 11/13～11/23 共 6 場裡有 5 場落在 162–167（例外是 11/19 的 152），這一帶有多場次持續性，但只當距離描述（紀律 (d)）。
3. **vol**
   - IVR 1.00→**0.746**，SkewR 0.008→**0.164**，1M IV 72.41%→**61.25%**。put 端的極端定價退了一部分，但 IVR 仍高。
   - DT 的 1M RV 是 **125.47%**，所以 VRP 是 **−64.2pt**。這是 20 日窗口裡同時有 −13.84% 和 +31.32% 兩個跳空日造成的**事後 RV 假象**。
   - scan /vol 據此判「Vol 偏便宜，傾向買 premium」，**不採用**。
4. **FP（session 11/23）**：SG 統計平倉占比 58%，主體是止盈和保護上移，**不是新開空**（細節見 S_1_3_1）。
   - long call 獲利了結：Dec18 170C stc 81,058、Jan'27 160C stc 55,553、Dec18 160C stc 30,739。
   - 深 OTM put 平倉，換成 120／130 strike 的 put：Jan'27 80P stc 149,892 配 Jan'27 120P bto 98,087；Apr'27 80P stc 149,189 配 Feb'27 120P bto 100,265。
   - 長天期 short call 往上移：Jan'29 btc 150C 10,028 配 sto 170C 10,162。
   - p9 的 d$ −2,474M 排在 0th 分位。依 memory，買賣軸**沒有前瞻力**；C/P 軸兩邊都上榜，所以**不給方向**。
5. **事件**
   - Huang 回任：人工卡有 1m 時點，SG FP 敘事寫「Huang's return rally cooled」。但 8-K 一手文件**本次沒有核實** ☐。
   - SEC 調查：外部報導寫的是「民事、揭露面」調查，SEC 和公司都沒有證實。10-Q 還沒申報，公司說會在「coming weeks」申報。
   - 依 user 裁決 (i)，這些都列為事件層觀察。**如果出現一手 8-K、起訴或 10-Q 揭露，回報 user 重裁**。
6. **行動**：沒有 NVDA 持倉，**維持 W**。
   - A 腳的 IVR<0.5 沒達到（0.746）。
   - R 腳要等 T+10（約 12/02）的共識更新，以及 user 裁決 base_pe 是否加治理折價。
   - 價格在 HW 和 Bear 170 之間，**不追進**。
7. **預測帳本：不寫**。我方說不出偏離 IV 的機率依據（S_1_4_3）。

**縮寫**

| 縮寫 | 全名（說明） |
|---|---|
| DT | SG data_table（牆位 SSOT） |
| v4／synth | SG history_v4／synth_oi 落地檔 |
| FP | flowpatrol（SG 期權流向日報） |
| FN | Founder's Note（SG 每日筆記） |
| PW／CW／HW／KG／KD | Put Wall／Call Wall／Hedge Wall／Key Gamma Strike／Key Delta Strike |
| LVP／HVP | synth 裡 gamma 最正／最負的價位 |
| DR／GR／Act | Delta Ratio／Gamma Ratio／Activity Factor |
| IVR／SkewR／GarchR | IV Rank／Skew Rank（高＝call 貴，低＝put 貴）／Garch Rank |
| RV／VRP | 實現波動／IV − RV |
| IM | Options Implied Move（SG 欄位，是日 σ，不是財報 IM） |
| ADX／ATR | Average Directional Index（趨勢強度）／Average True Range（平均真實波幅） |
| VP／POC／VAH／VAL／VWAP | Volume Profile／Point of Control／Value Area High／Value Area Low／成交量加權均價 |
| bto／btc／sto／stc | 買進開倉／買回平倉／賣出開倉／賣出平倉 |
| V/OI | 成交量 ÷ 未平倉量 |
| OTM／ITM／ATM／LEAP | 價外／價內／價平／長天期選擇權 |
| OPEX | 月選擇權到期日 |
| ER／T+10 | 財報／財報後第 10 個交易日 |
| SEC | U.S. Securities and Exchange Commission（美國證管會） |
| 8-K／10-Q | 重大事件報告／季報（SEC 申報表格） |
| W／R／A／X | 觸發表腳名：等待／重估／再進場／破位 |
| kit／mgrid | `bin/strategy_card_kit.py`／kit 輸出的同 moneyness IV 格線 |
| rr3／rr4u／rr5／rr6 | 持倉檔的總槓桿／保護總量／現金比／β 加權曝險 |

### S_1_2｜TREND2：跨日框架

**DT 結構表**（as-of 用 Previous Close 還原場次。11/13～11/20 轉錄自 [[23-11-2026_NVDA_AUTO_strategy]] S_1_2，其中 11/19、11/20 本次重讀過 DT 21-11 第 3106 行和 DT 22-11 第 3152 行，數字一致）

| session | 收盤 | KG | KD | HW | CW | PW | 1M IV | 1M RV | VRP | IVR | GarchR | SkewR | P/C OI | IM |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 11/13 | 162.82 | 170 | 110 | 167 | 200 | 150 | 59.93% | 51.50% | +8.4 | 0.959 | 0.814 | 0.684 | 0.879 | 6.16 |
| 11/16 | 156.14 | 160 | 110 | 167 | 200 | 150 | 64.08% | 53.98% | +10.1 | 1.000 | 0.828 | 0.604 | 0.877 | 6.32 |
| 11/17 | 155.46 | 160 | 110 | 167 | 200 | 150 | 65.96% | 52.78% | +13.2 | 1.000 | 0.700 | 0.376 | 0.858 | 6.47 |
| 11/18 | 150.87 | 150 | 110 | 167 | 200 | 150 | 50.73% | 51.73% | −1.0 | 0.593 | 0.666 | 0.308 | 0.821 | 4.83 |
| 11/19 | 146.00 | 150 | 110 | 152 | 200 | 150 | 52.22% | 51.77% | +0.45 | ☐ 空欄 | ☐ | ☐ | 0.792 | 4.81 |
| 11/20 | 125.79 | 135 | 80 | 165 | 200 | 150 | 72.41% | 65.99% | +6.42 | 1.000 | 1.000 | 0.008 | 0.805 | 5.75 |
| **11/23** | **165.19** | **170** | **170** | **162** | 200 | 150 | **61.25%** | **125.47%** | **−64.2** | **0.746** | 1.000 | **0.164** | 0.876 | 6.39 |

11/23 的其他欄位（DT 24-11 第 3001 行）：
- 股票量 310.7M（11/20 是 275.7M）。
- Call／Put Volume 4,222,958／2,534,152。
- Call Gamma −1.16B、Put Gamma −0.95B、GR 1.2213。
- Top Gamma／Delta Exp 都是 2026-12-19。依 memory，DT 這個欄位系統性晚一天，所以實際是 12/18 OPEX。

- (1) **牆位持續性**
  - PW 150 從 11/13 到 11/23 共 7 場都是 150，有效。CW 200 也長期不動。
  - 現價在 PW 上方 +9.20%。這是 **1 場收復**（scan 寫「連續站穩 1 日」），連 2 場還沒達成，而且依紀律 (d)，收復只能當狀態描述。
  - KG 170、KD 170 是第一次出現，屬噪音層。KG 碰巧等於 Bear 170，**不疊加成「雙重壓力」**。
- (2) **vol 狀態**
  - IVR 從 1.00 退到 0.746，SkewR 從 0.008 回到 0.164，put 端的極端程度退了一部分。
  - DT 的 RV 125.47% 是 20 日 close-to-close，裡面包含 11/20 的 −13.84% 和 11/23 的 +31.32% 兩個跳空日。這兩天要大約 20 個交易日後（約 12 月中下旬）才會滾出窗口。在那之前，**VRP 口徑會機械性地保持很負**。
  - ⇒ A 腳的「VRP>0 才考慮賣 put 類」在這段期間不會滿足，原因是**窗口假象，不是 vol 便宜**。
  - scan 的 IV 結構（NE 25Δ／95Δ IV 105.9%／127.0%、年化 59.3%／87.0%）顯示近月左尾仍然很貴。IV Slope −4.16，近月 IV 高於遠月（倒掛）。
- (3) **價格結構（scan 24-11）**
  - ADX 50.64（11/20）→**49.31**，scan 仍判空方主導。11/23 的 +31% 是事件跳空，不是趨勢反轉的證據。
  - 週 VWAP 151.04，現價在它上方。VP：POC 211.18、VAH 238.42、VAL 188.89，現價在價值區下緣下方 −12.5%。
  - ATR 停損參照 **$138.6**（ATR 8.0%×2，as-of 11/22）。
- (4) **synth 布局（scan /positioning，只作描述）**
  - DR 0.23→**0.92**。scan 拆解 |Call Δ| +92.1%、|Put Δ| +91.7%，兩邊同步上升，⇒ 多空都在加碼，**不是轉多**（[[feedback_ratio_field_direction_needs_leg_split]]）。
  - Delta 名目 −16,771M$、Act 0.013（平靜）。
  - LVP／HVP 11/20 是 88／165，11/23 是 115／205。scan 自己標「雙峰跳動，近 10 列大跳 5 次」，**不判遷移**。
  - DT 的 DR −1.2072 和 synth 的 DR 0.92 口徑不同（[[reference_gex_columns_differ_across_sg_sources]]），兩者不並列。
- (5) **IM 區間**（scan /levels，以 165.05 為中心；IM 是日 σ 換算，只作描述）

  | 尺度 | ±幅度 | 區間 |
  |---|---|---|
  | 日 1σ | ±6.36 | 158.69～171.41 |
  | 週 1σ | ±14.23 | 150.82～179.28 |
  | 月 1σ | ±29.16 | 135.89～194.21 |
  | 週 2σ 警戒 | — | 136.60／193.50 |

- (6) **scan 綜合裁決「繼續觀察」可接受；以下四處不採用**
  - (a) Layer 0「🟢 超跌區，分批佈局機會」。估值基準 11-11 已陳舊 13 天，在 ER 之前。scan 自己也標「現價已跌破 Bear target $170，model breach」。FW_PE 11.4x 用的是 NTM EPS $14.46，T+10 前不可信。
  - (b) /bias「crashing up，高信心加速段」。這是沒有前瞻驗證的分流，而且這一場是單一事件跳空，不採用。
  - (c) /vol「VRP −64.4pt，premium 明顯便宜」。理由是 RV 窗口假象，見 (2)。
  - (d) /gex「已站上 HW $162，PIN」。gamma 翻轉點當 S/R 已經被證偽（[[project_gamma_sign_flip_sr_falsified]]）。
- (7) **前卡記的 scan FP 快取錯誤**：本次**沒有再出現**。scan 寫「未上榜 heavy_daytrade」，FP 原檔 p17（第 281～301 行）確實沒有 NVDA。

### S_1_3｜TREND：即時層和事件層

#### S_1_3_1｜FP（session 11/23，`flowpatrol_2026_11_24.log`）

依 FP 的 spread 編號，把同組的腳放在一起讀，方向看 `dir=`（[[feedback_fp_spread_label_leg_check]]）。

| spread／行 | 腳 | bto／btc／sto／stc | prem | greek dir | 讀法 |
|---|---|---|---|---|---|
| —／236 | Dec18 170C | 0／0／1,308／**81,058** | −129.68M | SELL（d$ −701.61M、g$ −19.93M、v$ −1.42M） | long call 獲利了結（oi 125,718，V/OI≈0.65） |
| —／250 | Dec18 160C | 0／2,143／0／**30,739** | −63.02M | SELL | 同上 |
| 6704／234+235 | Jan'27 160C ＋ Jan'27 130P | 160C：0／691／0／**55,553**；130P：**72,435**／991／0／0 | −158.77M／+68.07M | SELL／BUY | 了結 call、同時買 put，**減 delta**。160C 的 `oi=20` 跟 55,553 口 stc 對不上，⇒ 這一列的 oi **不可信** |
| 6698／251+252 | Jan'27 120P ＋ Jan'27 80P | 120P：**98,087**／1,022／0／0；80P：0／230／0／**149,892** | +62.68M／−8.60M | BUY／SELL | **put 上移**：深 OTM 的 80P 平倉，換成 120P |
| 6756／241+242 | Feb'27 120P ＋ Apr'27 80P | 120P：**100,265**／0／61／0；80P：0／0／29／**149,189** | +110.93M／−69.27M | BUY／SELL | put 上移，同時把到期拉近（Apr→Feb） |
| 6522／248+249 | Jun'27 140P ＋ Jun'27 100P | 140P：20,298／165／0／0；100P：0／462／0／19,765 | +67.42M／−28.42M | BUY／SELL | 同到期 1:1 上移 100→140。oi 有 ⚠pkg 標記，是整包值 |
| 6709／239+240 | Feb'27 200C ＋ Feb'27 175C | 200C：0／0／**49,985**／1,205；175C：**22,232**／800／0／0 | +111.58M／+66.94M | SELL／BUY | 腳比約 1:2.25，**不是 1:1 的 BuCS** ⇒ 不判價差型態 |
| 6455／244+245 | Jan'29 150C ＋ Jan'29 170C | 150C：0／**10,028**／0／330；170C：422／0／**10,162**／0 | — | BUY／SELL | **長天期 short call 上移**（btc 150 → sto 170），是 overwrite 方在反彈後重設 |
| —／243 | Jan'28 210C | 0／0／5,603／12,478 | — | SELL | 描述 |
| 258（p9） | symbol 級 | — | — | d$ −2,474M（0th）、g$ −22.10M（34th）、v$ −2.10M（2th） | 買賣軸**沒有前瞻力**（[[project_fp_p9_extreme_greek_forward_return]]） |

- (1) **整體讀法**
  - 在 +31.32% 的跳空日，主體是 long call 了結，加上 protection 換到更高的 strike（80→120／130／140）。
  - SG 敘事寫「high closing proportions indicate traders were taking profits … rather than initiating fresh bearish conviction」（第 52 行），跟逐腳讀法一致。
  - 前卡的待辦「put 側 closing 要拆 btc／stc」：這次的 put 平倉**全是 stc**（多方把 put 部位了結），**不是空方回補**。而且都配對了同組的更高 strike put bto，所以是避險**換腳**，不是撤掉避險（[[feedback_put_closing_not_bullish_split_btc_stc]]）。
- (2) **開平倉軸**
  - 120P／130P 的 bto 對 oi：Feb 120P 是 0.62，Jan 120P 是 0.82，Jan 130P 是 0.71。都沒有到 ≈1。
  - FP 的 btc／stc 欄從 09-01 起有平倉占比口徑斷層（[[project_fp_btc_share_regime_break_0901]]）。
  - ⇒ 「新開倉」**不下定論**，要等 strike_ladder asof 11/23 的 ΔOI 確認。☐ 本次沒讀：ladder 最新 asof 是 11/20，本輪也不能解 gz。
- (3) **C/P 軸**：NVDA 同時有大額 call（賣出和平倉）和大額 put（買進）。依 memory，上 put 榜代表下檔風險多已 price in，**不能當看空證據**。兩個軸混在一起，⇒ **不給方向**。

#### S_1_3_2｜外部事件核實（WebSearch，2026-11-24）

- **SEC 調查**：報導是 WSJ 引述的「民事 inquiry」，範圍是揭露有沒有誤導投資人，涉及 Huang 的關係和國際（含新加坡）營收的報告口徑。SEC 和 NVDA **都沒有證實**，也沒有提到執法行動。前卡依 Reuters 報導寫「會計調查」，這次的搜尋結果偏向「**揭露面**」調查，兩者措辭不同 ☐ 一手文件未核實。
- **10-Q**：NVDA 表示會在「coming weeks」申報，沒有在財報當天交，理由連到 Huang 案和可能要補充的風險揭露。到 11-24 為止**沒有看到申報**。
- **Huang 回任**：本次搜尋結果（發布時點看起來早於 11/23）寫「董事會不打算讓 Huang 回任」。這跟人工卡的 1m 時點紀錄，以及 SG FP 11/24 敘事「Huang's return rally」**矛盾**，判斷是搜尋結果過期。8-K 一手文件 ☐ 下一張卡要核實。

#### S_1_3_3｜事件層（往前看，紀律 (a)）

`python3 bin/strategy_card_kit.py catalysts NVDA --until 2026-12-18 --peers AMD,AVGO,TSM,MRVL,MU`（取數 2026-11-24 08:55 ET；宏觀事件用 `--extra` 帶入）：

| 日期（ET） | 標的 | 事件 | 反應場次 | 到期／履約價 | 隱含波幅（0.85×straddle） |
|---|---|---|---|---|---|
| 2026-11-25 | NVDA | PCE/GDP/耐久財 | — | — | — |
| 2026-12-01 | MRVL | 財報 AMC | 2026-12-02 | 2026-12-04 K=145 | ±12.7%（straddle 21.60） |
| 2026-12-01 | NVDA | 眾院三委員會 NVDA 閉門訪談 | — | — | — |
| 2026-12-04 | NVDA | NFP | — | — | — |
| 2026-12-09 | AVGO | 財報 AMC | 2026-12-10 | 2026-12-11 K=315 | ±11.6%（straddle 42.90） |
| 2026-12-09 | NVDA | FOMC 決議 | — | — | — |
| 2026-12-17 | MU | 財報 AMC | 2026-12-18 | 2026-12-18 K=710 | ±15.1%（straddle 125.68） |
| 2027-01-14 | TSM | 財報（窗口外） | — | — | — |
| 2027-02-02 | AMD | 財報（窗口外） | — | — | — |
| — | NVDA | 財報（下次未公告） | — | — | — |

kit 沒抓的事件：
- 11/26 感恩節休市、11/27 半日盤（轉錄自前卡）。
- 10-Q 申報（「coming weeks」，S_1_3_2）：這是**一手治理事件**。如果揭露重大缺失，**回報 user 重裁**。
- 約 12/02：ER（11/17）後的 T+10，R 腳的前置條件。
- 12/18 OPEX。DT 的 Top Gamma／Delta Exp 都指向這一天（欄位晚一天）。

IVR 0.746 **不是**財報後的季節性下修，而是 11/20 事件衝擊到 1.00 之後的回落。

### S_1_4｜觸發表和保護菜單

#### S_1_4_1｜體質重驗（沿用前卡觸發表之前）

| 項目 | 前卡（人工 11/23 盤中；AUTO as-of 11/20） | 本次（11/23 收盤） | 影響 |
|---|---|---|---|
| 價格對 PW 150 | −16.14%（11/20）／盤中 +12.5% | **+10.13%（收盤）** | X 不在觸發狀態；收復只有 1 場 |
| PW／CW | 150／200 | 150／200（7 場不動） | 沿用 |
| KG／KD／HW | 135／80／165 | 170／170／162（KG、KD 單場） | KG、KD 不採用；HW 162–167 帶只描述 |
| IVR／SkewR | 1.00／0.008 | **0.746／0.164** | A 腳 IVR<0.5 **未達** |
| VRP（DT） | +6.42 | **−64.2**（RV 窗口假象） | A 腳 (4) 機械性不成立，要等跳空日滾出窗口 |
| ADX | 50.64 | 49.31 | 空方趨勢指標仍高 |
| 治理 | user 裁決 (i)：否決腳全部解除 | SEC 揭露面調查仍是報導、10-Q 還沒申報、回任 8-K 未核實 | 依裁決 (i)：事件層觀察，不恢復否決；有一手揭露就回報重裁 |
| 估值 | 基準 11-11 | 陳舊 13 天，現價比 Bear 170 低 −2.8% | zone 暫停引用，等 T+10 |

#### S_1_4_2｜觸發表

| 腳 | 條件 | 依據 | 動作 |
|---|---|---|---|
| **W 等待（現行）** | R 還沒完成 | 估值陳舊；IVR 0.746 | **不建倉、不追進** |
| **X 破位** | 收盤 < 150 | 破 PW 是波動閘，不是方向訊號（[[feedback_risk_pivot_is_vol_gate_not_direction]]） | 目前沒觸發。如果再收破，**不追空** |
| **R 重估** | (1) ≥T+10（約 12/02）共識 EPS 更新；(2) user 裁決 base_pe 是否加治理折價；(3) 10-Q／8-K 用一手來源核實 | [[feedback_er_consensus_feed_lag_window]]；[[feedback_conservative_base_pe_no_rerating]] | 重跑 zone，重訂 A 腳 |
| **A 再進場（待 R）** | (1) R 完成；(2) IVR < 0.5；(3) VRP > 0 才考慮賣 put 類（注意 RV 窗口假象，約 12 月中下旬前不會成立）；(4) 價格落在重估後的等待區 | 估值、vol | VRP≤0 只考慮 defined-risk 的 call 價差；不裸買 call |
| 狀態描述（不是觸發） | 連 2 場收盤 > 150，而且 PW 不下移（目前 1／2） | 紀律 (d) | 只描述，**不連到進場或保護決策** |
| 狀態描述（不是觸發） | 上方：170（Bear／KG 單場）→ 173.73 → 188.89（VAL）→ 200（CW）。下方：162（HW 帶）→ 151.04（週 VWAP）→ 150（PW）→ 138.6（ATR 停損） | DT、scan 計算值 | 只當距離參照 |

#### S_1_4_3｜預測帳本

**不寫**。本卡沒有附基準率的可證偽價格預測。「HW 162 或 PW 150 守不守得住」這類宣稱：gamma 翻轉 S/R 已經被證偽，PW 條件守住率只有 66.7%，而且沒有 NVDA 單一事件跳空後的子集基準。我方機率說不出偏離 IV 的依據。

#### S_1_4_4｜保護菜單

沒有 NVDA 持倉，所以**不需要 NVDA 保護**。也**不要用 NVDA put 去保指數或半導體桶**，那是載體錯配（[[feedback_hedge_carrier_use_tail_quantiles_not_ev]]）。

間接曝險（`24-11-2026-brokerage.xlsx.log`，parsed 11-24 07:51）：
- QQQ 116 股（last 648.20）。
- QQQ Jun17'27 700C×4（OTM −7.4%）、710C×2（−8.7%）。
- SMH May21'27 525C×2（−12.9%）。
- SOXX Feb19'27 165C×9（−15.7%，DTE 87）。
- NAV 429,217.66；rr3 **1.79x**；**rr4u 0.00%**；rr5 現金 20.58%；rr6 224.67%。
- long premium 下檔封頂 $75,723（17.6% NAV）。

指數和板塊桶的保護菜單，看同日的 `24-11-2026_QQQ_AUTO_strategy.md`、`24-11-2026_SMH_AUTO_strategy.md`、`24-11-2026_SOXX_AUTO_strategy.md`。

**同 moneyness IV（紀律 (b)）**：`python3 bin/strategy_card_kit.py moneyness NVDA --exp 2026-12-18,2027-01-15 --prev <前卡 AUTO 兩行>`，取數 **2026-11-24 08:55 ET，是盤前**。

| 到期 | −15% | −10% | −5% | ATM | +5% |
|---|--:|--:|--:|--:|--:|
| 2026-12-18 | 89.1%（+15.7pp） | 88.3%（+18.9pp） | 90.5%（+24.7pp） | 87.9%（+24.0pp） | 46.8%（−18.0pp） |
| 2027-01-15 | 72.6%（+11.7pp） | 71.1%（+12.2pp） | 72.3%（+15.9pp） | 72.3%（+17.4pp） | 42.8%（−13.6pp） |

```
mgrid NVDA 2026-12-18 S=165.05@2026-11-24 -15:0.8908 -10:0.8825 -5:0.9049 +0:0.8793 +5:0.4682
mgrid NVDA 2027-01-15 S=165.05@2026-11-24 -15:0.7260 -10:0.7106 -5:0.7227 +0:0.7230 +5:0.4280
```

- ⚠ **這組格線不採用作判讀**：
  - 這是盤前取數，盤前 IV 和報價已知會壞（[[reference_yfinance_option_volume_stale_for_untraded_rows]]）。
  - Dec ATM 87.9% 對 +5% 46.8%，相差 41pp，微笑形狀不合理。
  - DT 11/23 收盤的 1M IV 是 61.25%。
  - 前卡 `--prev` 的基準是 11/23 盤後取數，也可能受同樣問題影響。
  - ⇒ 逐格 Δpp **不能寫成「vol 變貴」**。下一張卡要在美東盤中重跑，用人工卡的盤中行 `S=168.30@2026-11-23` 當 `--prev` 會比較乾淨。

### S_1_5｜前卡回檢（紀律 (c)）

**[[23-11-2026_NVDA_strategy]] S_1（人工，11/23 盤中）**

| 前卡宣稱／待辦 | 分類 | 證據（as-of 11/23 收盤） |
|---|---|---|
| 「173.73～188.89 是本週上方壓力帶」 | **未檢驗** | 收 165.19。手上沒有全日高點的一手數據（10:43 ET 快照是 171.5），沒確認有沒有測到 173.73 |
| X：「再收破 150 不追空」 | **未檢驗** | 收在 150 上方 +10.13% |
| 「NVDA 保護不便宜」 | **成立**（描述性） | DT 11/23 IVR 0.746、NE 95Δ IV 127.0% |
| 待辦：真收盤對 150／173.73 | 完成 | 165.19（DT／FP） |
| 待辦：DT PW 是否從 150 移動 | 完成：**沒移動** | DT 24-11 第 3001 行 |
| 待辦：FP put closing 拆 btc／stc | 完成：**全是 stc，且配對更高 strike 的 bto**（換腳） | S_1_3_1 |
| 待辦：strike_ladder ΔOI | **未檢驗** | ladder 最新 asof 11/20；本輪不能解 gz |
| 待辦：mgrid `--prev` | 跑了，但**資料不合格** | 盤前壞報價（S_1_4_4） |

**[[23-11-2026_NVDA_AUTO_strategy]] S_1（回補卡，as-of 11/20）**

| 前卡宣稱 | 分類 | 證據 |
|---|---|---|
| W：不建倉、不接刀 | 規則；事後**錯過 +31.32%** | 125.79→165.19。這是事件驅動的單一場次，不構成 edge 證據，正反都一樣 |
| 「52W Low 124.5、ATR 104.1、週 2σ 99.87 都不是承接位」 | **未檢驗** | 價格沒有回測這些位置，是消息跳空上漲 |
| 否決 2（SEC 調查） | **被 user 裁決 (i) 取代** | 人工卡（晚於 AUTO 卡）裁決否決腳全部解除。SEC 調查改列事件層，目前仍是報導層級 |
| 待驗 (2)：CEO 事件是否逆轉，要一手 8-K | **未檢驗** | 本次搜尋結果過期且矛盾（S_1_3_2） |
| 待驗 (3)：PW 150 是否下移或被收復 | 沒下移；收復 **1 場** | DT 24-11 |
| 待驗 (5)：ladder 解 Jan'29 240C、Jan'28 200P 的 ΔOI | **未檢驗** | 同上 |
| 待驗 (7)：scan daemon 和 FP 快取 | **本次正常** | scan 頁首 src ✅、沒有落後警告；heavy_daytrade 跟 FP 原檔一致 |

**待驗（下一張卡）**：
- (1) Huang 回任的 8-K 一手文件，以及 10-Q 有沒有申報、風險揭露內容。如果有重大揭露，**回報 user 重裁**，不自動恢復否決。
- (2) strike_ladder asof 11/23 的 ΔOI：Jan'27 120P／130P、Feb'27 120P 的實際新開倉量；Jan'27 160C 的 `oi=20` 是不是錯值。
- (3) 連 2 場收盤 > 150，PW 150 和 HW 162–167 帶的持續性（只描述）。
- (4) mgrid 在美東盤中重跑，`--prev` 用人工卡 `S=168.30@2026-11-23` 那兩行。
- (5) R 腳：T+10（約 12/02）後重跑估值；user 裁決 base_pe 是否加治理折價。

Sources:
- [TechCrunch — Jensen Huang / Nvidia 10-Q delay](https://techcrunch.com/?p=3190087)
- [Benzinga — Nvidia SEC inquiry / 10-Q](https://www.benzinga.com/node/63376955)
- [Crowdfund Insider — SEC Opens Inquiry into Nvidia's Disclosures Following Jensen Huang's Exit](https://www.crowdfundinsider.com/?p=323680)
- [TweakTown — SEC opens investigation into Nvidia over whether investors were misled](https://www.tweaktown.com/news/114760/sec-opens-investigation-into-nvidia-over-whether-investors-were-misled-to-boost-earnings/index.html)
- [Longbridge — Why Nvidia held back its quarterly SEC report](https://longbridge.com/news/305948432)
- [Let's Data Science — SEC reportedly investigates Nvidia over disclosures](https://letsdatascience.com/news/sec-reportedly-investigates-nvidia-over-whether-disclosures-98711c40)
- [AI Weekly — SEC Opens Civil Probe of Nvidia Disclosures After Huang Exit](https://aiweekly.co/alerts/sec-opens-civil-probe-of-nvidia-disclosures-after-huang-exit)
- [Silicon UK — SEC Nvidia](https://www.silicon.co.uk/e-regulation/sec-nvidia-632405)
