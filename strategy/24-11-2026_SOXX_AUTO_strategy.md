# SOXX 策略卡（自動，FP 落地後 TREND2+TREND）

## S_1｜AUTO SOXX TREND2+TREND 21:32｜11/23 收 140.21（+13.64%），反彈主因是 NVDA 復任 Huang 加上 OPEX 後回補，屬事件衝擊；PW 125 已連 2 場、寫入框架，KG 改到 145（只有 1 場）；IVR 從 1.0 回落到 0.755，SkewR 0.076 還是 put 相對最貴；165C x9 續抱，不加碼（2/4）、不追多；SOXX 卡保護維持選項 0；預測帳本不寫

### S_1_1｜TL;DR

> **as-of**：2026-11-24 21:32 台北，等於 11/24（週二）08:32 ET 盤前。**最新真收盤是 11/23（週一）**。
> 這次讀到的檔：DT `SPX_data-table_2026-11-24.csv` L3900（meta sg_quote_date 2026-11-23，fetched 11-24 21:02 TPE）、scan `24-11-2026_SOXX_scan_result.md`（21:05:52，v7.44）、FP `flowpatrol_2026_11_24.log`（session 11/23）、`23-11-2026_founders_PM.md`、持倉 `24-11-2026-brokerage.xlsx.log`（parsed 11-24 07:51 TPE，是 11/23 收盤後的快照）、kit 輸出（取數 11-24 08:33 ET）。

1. **價格**：11/23 收 **140.21**（DT Previous Close）。相對 11/20 的 123.38 是 **+13.64%**。kit／yfinance 給 140.22，兩者一致 ⇒ 前卡 S_1_6 的事後價**確認成立**。
   - 同業同一場（FP 11-24 的 1dR）：NVDA **+31.32%**、TSM +13.70%、AMD +7.01%；MU +19%（FN PM L41）。
2. **歸因（有非 SG 來源）**：Nvidia 董事會 11/23 一致決議復任 Jensen Huang 為 CEO。他 11/12 卸任，期間由 Kress 代理（[NVIDIA 官方新聞稿](https://nvidianews.nvidia.com/news/nvidia-board-reinstates-jensen-huang-as-president-ceo-and-board-director)、[Bloomberg](https://www.bloomberg.com/news/articles/2026-11-23/nvidia-reinstates-jensen-huang-as-ceo-with-government-input)、[NBC](https://www.nbcnews.com/tech/tech-news/nvidia-reinstates-jensen-huang-rcna610864)、[Al Jazeera](https://www.aljazeera.com/economy/2026/11/23/nvidia-board-reinstates-jensen-huang-as-ceo)、[Fox News](https://www.foxnews.com/live-news/ai-news-tech-markets-nvidia-11-23-26)）。
   - SG 另外指出，消息在 8:55 ET 出來，但**開盤跳空在消息之前就已發生**（FN PM L53），還有 OPEX 後 dealer 回補避險的機械性買盤（L57）。⇒ 11/19-11/20 的下殺和 11/23 的反彈有一部分屬於 **NVDA 公司治理事件**。前卡 Z47 改判「已用非 SG 來源核實」。
3. **結構（DT 11/23 場次）**
   - PW **125 第 2 場** ⇒ 寫入框架。
   - KG 130 → **145**，只有 1 場。KD 91.67 → 155，跳回去了 ⇒ 前卡「KD 91.67」那一場是噪音。
   - HW 153.33、CW 155 都沒動。
4. **Vol**
   - IV 74.08 → **62.79**，IVR 1.000 → **0.755**。
   - SkewR 0.112 → **0.076**：put 相對 call 仍在近一年最貴的區域。
   - NE Skew -0.157，Skew -0.218。
5. **FP**：SOXX 這一場**完全沒上榜**。同業層面，NVDA 是 call 端 stc 加上 Jan15 120P/130P 買方（L73-79），SMH、MU 進 heavy_daytrade（L288、L300）。這些只當背景。
6. **估值**（scan L82-91）
   - 140.21 已經回到等待區 $135-156 裡面，剛好坐在 **Bear $140**（-0.2%）。fair $177，FW_PE 15.0x。
   - scan 印出的 R:R 167 是分母 -0.2% 造成的**假象**，不採用。
7. **部位**
   - 165C x9：MV **$5,197**、UPL -$12,551、Δ 曝險 **$36,519（8.51% NAV）**。
   - NAV $429,217.66，rr4u 0%，rr5 20.58%，rr9b semi **+115.57%**。
8. **策略：不變**。續抱，不加碼（Y11 = 2/4），不追多，SOXX 卡保護維持選項 0。
9. **預測帳本：不寫**
   - IV 隱含：10 場內收盤跌破 125 是 **37.1%**；12/18 前跌破 116 是 **34.5%**。
   - 我方沒有獨立依據可以偏離 IV。

**縮寫表**

| 縮寫 | 全稱 |
|---|---|
| PW / CW / HW / KG / KD | Put Wall / Call Wall / Hedge Wall / Key Gamma Strike / Key Delta Strike |
| DR / GR / IVR / SkewR / GarchR | Delta Ratio / Gamma Ratio / IV Rank / Skew Rank（高 = call 相對貴，低 = put 相對貴）/ Garch Rank |
| DT | SG data_table |
| FP / FN | FlowPatrol / Founder's Note |
| LVP / HVP | synth 最正 gamma 價位 / 最負 gamma 價位 |
| BePS | Bear Put Spread |
| bto / sto / btc / stc | 買進開倉 / 賣出開倉 / 買進平倉 / 賣出平倉 |
| RV / VRP | Realized Vol / IV - RV |
| NE | 近月到期（Next Expiry） |
| OPEX | 月選擇權到期日 |
| PCE | 個人消費支出物價指數 |
| NTM / FW_PE | 未來 12 個月 / 前瞻本益比 |
| rr4u / rr5 / rr9b | 保護總量占 NAV% / 現金占 NAV% / 板塊方向曝險 |
| OI / ΔOI | 未平倉量 / 未平倉變化 |
| ATR / ADX | 平均真實波幅 / 平均趨向指標 |
| GEX(MO) | SG 指數 gamma 曝險 |
| DPI | Dark Pool Index（只作資訊欄） |
| mgrid | strategy_card_kit moneyness 輸出的同 moneyness IV 格 |

### S_1_2｜TREND2：跨日框架

**S_1_2_1｜資料新鮮度**

- **DT 11-24**：meta 寫 `sg_quote_date 2026-11-23`、fetched 2026-11-24T21:02:19+08:00。SOXX 在 L3900，Previous Close 140.21 ⇒ 屬於 **11/23 場次**。Current Price 140.2 不採用。
- **scan**：L5 寫 v4、synth、dt 的 td 全部是 2026-11-23 ⇒ **三源同步**。前卡的 synth 落後 1 場已經消失。
- **scan 的水位分歧警示**：synth LVP 183 vs V4 PW 125，分歧 46.7%（L18）。台上水位以 V4 為準，synth LVP 只作描述。
- 🔴 **RV 污染（Z39）惡化**
  - DT 1M RV 4.4639，還是錯的。
  - scan 這次的 synth RV 是 **446.4%**，VRP **-383.6pt**（L220-221）。這是拆股斷點造成的；前卡 scan 自算的 85.0% 這次沒有沿用。
  - ⇒ /vol 的「premium 明顯便宜、偏向買方」（L222、L249）**作廢**。GARCH 218.1%（L228）也吃到同一個污染序列，**一起作廢**。
- **FP**：`flowpatrol_2026_11_24.log` session_date 2026-11-23（L6），data_quality OK（L10）。

**S_1_2_2｜DT 逐場次**（11/13-11/19 沿用前卡 S_1_2_2；11/20 讀自前卡，來源 DT 11-23 L4112；11/23 讀自 DT 11-24 L3900）

| 場次（Prev Close） | KG | KD | HW | CW | PW | P/C OI | GR | DR | IV | IVR | GarchR | SkewR | NE Skew / Skew |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 11/18（141.83） | 150 | 155 | 166.67 | 155 | 140 | 1.280 | 0.4925 | -0.3104 | 57.25 | 0.777 | 0.297 | 0.208 | -0.111 / -0.154 |
| 11/19（138.01） | 140 | 155 | 153.33 | 155 | 140 | 1.2288 | 0.4688 | -0.2963 | 59.78 | 0.844 | 0.2523 | 0.184 | -0.133 / -0.162 |
| 11/20（123.38） | 130 | 91.67 | 153.33 | 155 | 125 | 1.1543 | 0.5768 | -0.2075 | 74.08 | 1.000 | 0.2377 | 0.112 | -0.192 / -0.197 |
| **11/23（140.21）** | **145** | **155** | 153.33 | 155 | **125** | **1.1817** | **0.7348** | **-0.4627** | **62.79** | **0.7552** | **0.2284** | **0.076** | **-0.157 / -0.218** |

11/23 場次的其他欄（DT 11-24 L3900；括號內是 11/20 值）：
- **Gamma**：Call -108.93M（-61.06M）、Put -148.26M（-105.88M）。Next Exp Gamma 0.116，NE Delta 0.0014。
- **成交量**：正股 21.20M（25.88M）。Call 109,039（121,415），Put 128,010（163,086），Volume Ratio 1.174（1.34）。
- TGE／TDE：2027-01-16／2028-01-22（仍晚一天）。Options Implied Move 5.557 是日 σ，不是事件 IM。DPI 53.68 只作資訊欄。

**S_1_2_3｜scan 關鍵欄（`24-11-2026_SOXX_scan_result.md`）**

| 項 | 值 | 讀法 |
|---|---|---|
| 綜合裁決 | 繼續觀察；ADX **31.86**，空方主導（L21-22） | 反彈一場還沒有改變趨勢判定 |
| /bias | -1/10，中性（L28） | 沒有經過前瞻驗證，不採用 |
| 市場背景 | GEX(MO)：NDX -4M、QQQ **-461M**（前卡 -702M）、SPY **-1,098M**（前卡 -1,381M）（L10-12） | 負 GEX 繼續收斂。同日溫度計 |
| 信用 | HY OAS **376**（Δ5 +53，3Y p96）；CCC 1402（p100）；as-of 11-20（L14） | 資訊欄。比前卡的 352／Δ5 +32 **更寬** ⇒ 信用端沒有跟著股市反彈 |
| Layer 0 | 等待區 ✓；Bear $140（-0.2%）／Base $177（+26.2%）／Bull $234（L84-91） | 價格坐在 Bear 上。R:R 167 是分母假象 |
| 進場時機 | 3/4；(4)「2 日站穩 V4 PW」只有 1 日（L157-161） | (4) 的結構日已經對齊（11/23 價配 11/23 PW），Z60 這次沒有再犯 |
| /levels（中心 140.22） | 週 1σ **$127.80-152.64**；月 1σ $114.76-165.68；週 2σ $115.38／$165.06（L192-199） | 只作描述 |
| IV 結構 | NE 25Δ 68.0%／95Δ 99.8%，Skew +31.8pt；IV Slope -1.25，仍倒掛（L204、L236） | 左尾仍然貴；倒掛幅度比前卡的 -3.43 收斂 |
| VP | POC 168.35；VAL 158.32；VWAP(week) 136.17（L209-211） | 價格在價值區下緣下方、週 VWAP 上方。只作描述 |
| /gex | ATM Net GEX -$0.01B；翻正臨界 HW $153，距離 -9.36%（L264-274）；Dealer 近 5 日 -0.31B → -0.35B（L290） | 負 gamma 制度延續 |
| 水位建議 | ATR 停損 **$121.0**（L152） | 165C 是有限風險，不適用停損 |
| /positioning | synth LVP 183／HVP 143；Large Put OI ≈125（L164 寫 ≈115），Call ≈170；Delta Notional -403M$（L103、L119、L164-165） | synth 欄位分歧大，只作描述 |

**S_1_2_4｜判讀**

- **PW 125 寫入框架**：11/20、11/23 連 2 場 ⇒ 符合多場次紀律（[[feedback_wall_levels_ssot_sg_data_table]]）。現價在它上方 +12.2%。
- **KG 145 只有 1 場**：前卡的 KG 130 只存在 1 場就被取代 ⇒ KG 正在單場來回跳，下一份 DT 才判斷是否持續（Y61''）。
- **KD 91.67 → 155**：跳回原值。前卡把 91.67 當噪音處理是對的。「拆股前調整合約」的推論（Y63）仍然沒有驗證，但 KD 這一腳已經不需要驗了。
- **Vol 從頂格回落，skew 沒有回來**
  - IV -11.3pt、IVR -24.5pp。這是 FN PM L45「Volatility reset following OPEX」在 SOXX 上的對應。
  - 但 SkewR 再下降到 0.076，Skew -0.197 → -0.218 ⇒ **反彈過程中 put 相對 call 更貴**。
  - 和 FN PM L59「taking advantage of elevated premiums through call selling while also adding downside hedges into the rally」同向。這是 SG 對 SPX 的描述，只作背景。
- **DR -0.2075 → -0.4627、GR 0.577 → 0.735**：比值欄先拆分子分母（[[feedback_ratio_field_direction_needs_leg_split]]）。Call、Put Gamma 兩腳都變得更負，沒有 ΔOI 就分不出開平倉 ⇒ 不判。

### S_1_3｜TREND：即時／事件層

**S_1_3_1｜價格路徑**

| 場次 | 收盤 | 日變動 | 來源 |
|---|---|---|---|
| 11/19 | 138.01 | -2.69% | 前卡 |
| 11/20 | 123.38 | -10.60% | 前卡（DT 11-23 L4112） |
| **11/23** | **140.21** | **+13.64%** | DT 11-24 L3900；kit S=140.22（取數 11-24 08:33 ET） |

- 11/24 盤前的 SOXX 價格沒有讀到。kit 的 140.22 是 yfinance 前收，不是盤前價。

**S_1_3_2｜FP `flowpatrol_2026_11_24.log`（session 11/23）**

- **SOXX 零上榜**：沒有出現在 largest_premium、unusual、top greek 任何一段 ⇒ 沒有當日新的 SOXX 大單證據。依 [[feedback_verify_oi_directly_not_fp_absence]]，**沒上榜不等於前卡的 Dec18 125P 已經平倉**。
- **同業背景**（各自的卡處理，這裡只描述）：
  - NVDA Dec18 170C：stc 81,058（L73），d$ -701.61M SELL(greek)（L102）⇒ 反彈當天 call 端出現大量 stc。
  - NVDA Jan15'27 120P／130P：bto 98,087／72,435 BUY(greek)（L75-76）；Feb19'27 120P bto 100,265（L78）。這幾筆有包裹單（spread 6698／6704／6756，L105-110），bto／sto 會逐腳反號，**開平倉軸不判**（[[feedback_fp_greek_is_buyside_btosto_unreliable]]）。
  - vendor 摘要（L42、L48-50）稱 NVDA delta exposure -$2,473.5M（0th %'ile），closing 占 58%，「profit-taking across chipmakers like NVDA and MU」。這是 SG AI 生成的衍生層，**不當證據**。
  - heavy_daytrade：MU flow_ratio 9.37、tot_oi_chg -368,233（L288）；SMH 5.88、-343,563（L300）。
- **讀法（描述）**：反彈當天，半導體權值股出現「call 端獲利了結＋長天期 put 承接」的組合，和 FN PM L18「use rallies … to add downside protection for end of Dec/Jan」的敘事同向。p9 C/P 軸規則（[[project_fp_p9_extreme_greek_forward_return]]）只適用於上 p9 榜的標的，SOXX 沒有上榜 ⇒ 不套用。

**S_1_3_3｜事件層（kit catalysts 原樣，取數 2026-11-24 08:33 ET）**

| 日期（ET） | 標的 | 事件 | 反應場次 | 到期／履約價 | 隱含波幅（0.85×straddle） |
|---|---|---|---|---|---|
| 2026-11-25 | SOXX | PCE | — | — | — |
| 2026-12-09 | AVGO | 財報 AMC | 2026-12-10 | 2026-12-11 K=315 | ±11.6%（straddle 42.85） |
| 2026-12-17 | MU | 財報 AMC | 2026-12-18 | 2026-12-18 K=710 | ±15.5%（straddle 129.27） |
| 2027-01-14 | TSM | 財報（窗口外） | — | — | — |
| 2027-02-02 | AMD | 財報（窗口外） | — | — | — |
| — | SOXX | 財報（下次未公告） | — | — | — |
| — | NVDA | 財報（下次未公告） | — | — | — |

- PCE 11/25 是用 `--extra` 帶入的，日期取自 FN PM L63「The November 25 PCE release」。
- 11/26 感恩節休市、11/27 半日盤：轉引前卡（FN 11/23 AM L10-14），這次沒有重讀。
- 🔴 **MU 反應場次 12/18 = Dec18 到期日**，MU 隱含 ±15.5%。MU 占 SOXX 盈餘 28.5% 是轉引前卡，這次沒有重算。
- **NVDA 治理事件**：Huang 11/12 卸任、11/23 復任（見 TL;DR 第 2 點的出處）。NBC 報導復任前幾天董事會主席才說不會復任，Trump 證實介入 ⇒ 這是**政治／治理類事件風險**，不是基本面變化。它會讓 SOXX 對 NVDA 的單一事件 β 更高，但沒有給 SOXX 新的盈餘訊息。
- **SG 敘事（背景，不當論據）**：FN PM L18「edge to a rally this week, target 7,500's … market get much less stable into month end」。
- **AI-capex 偏空訊號降權規則：不啟用**。HY OAS Δ5 +53bp 擴大，宏觀端有壓力。

### S_1_4｜觸發表＋保護菜單

**S_1_4_1｜部位（SSOT：`brokerage_log/24-11-2026-brokerage.xlsx.log`；parsed_at 2026-11-24T07:51:03 TPE，是 11/23 收盤後）**

| 項 | 值 |
|---|---|
| SOXX Feb19'27 165C x9 | MV **$5,197**；UPL -$12,551；DTE 87；OTM -15.7%（L33） |
| Δ 曝險 | Δ +0.29；**$36,519**，占 NAV 8.51%（L87、L100；S=$139.09，券商快照） |
| 權利金占 NAV | 5,197 ÷ 429,217.66 = **1.21%**（L46） |
| rr4u／rr5 | **0.00%**／**20.58%**（L67、L69） |
| rr9b semi | **+115.57% NAV**（L116） |
| 最大 single-name 曝險 | TSM +85.87%、QQQ +55.52%（L97-98） |

- 165C 最多賠 MV，約 **1.21% NAV**。真正的左尾在 TSM／QQQ，保護在那兩張卡處理（[[feedback_tsm_high_conviction_hold]]）。

**S_1_4_2｜IV 基準（`forecast_ledger.py implied`，取數 11-24 盤前，spot 140.22）**

| 事件 | 窗口 | IV 來源 | IV 隱含機率 |
|---|---|---|---|
| 任一收盤 <125（PW） | 2026-11-24～12-08（10 場） | 73.7%（2026-12-11 K=125，bs_last） | **37.1%** |
| 任一收盤 <116（雙殺 Bear） | 2026-11-24～12-18（18 場） | 77.9%（2026-12-18 K=116.67，bs_last） | **34.5%** |

- **預測帳本：不寫**。PW 條件守住率 66.7%（[[project_putwall_hold_rate_conditional]]）的口徑是「觸及後守住」，不是「10 場內不跌破」，不能直接換算成我方機率。我方沒有獨立依據可以偏離 IV。

**S_1_4_3｜觸發表（全部用真收盤；距離以 140.21 為基準；依 runbook (d)，動作欄不連到保護急迫度）**

| ID | 條件 | 距現價 | 意涵 | 動作 |
|---|---|---|---|---|
| **Y11''''''''''''** | 加碼閘門 | — | Layer 0 | **不加碼**。現在 **2/4**：(1) 估值 ✅（回到等待區，但坐在 Bear 140 上）；(2) 站回 PW ✗（Y50 的條件還沒成立）；(3) 現金 ✗（rr5 20.58%，低於目標帶 35-45%）；(4) SkewR <0.90 ✅（0.076） |
| Y12''''''''''（續） | DT SkewR ≥0.90 | 現在 0.076 | 否決閘重新啟動 | 次要觀察項 |
| **Y64'**（續） | 收盤 ≥125 連 2 場 | +12.2% 以上 | 收回 PW 125 | 11/23 是第 1 場。11/24 收 ≥125 就成立。只作描述 |
| **Y61''**（改） | 下一份 DT 的 KG 仍是 145 | +3.4% | KG 是否持續 | 只作描述 |
| Y66（新） | 下一份 DT 的 PW 仍是 125 | -10.8% | PW 第 3 場，持續性 | 只作描述 |
| Y67（新） | 收盤 <135 | -3.7% | 跌出等待區下緣 | Y11 (1) 回到 ✗ |
| Y55'''''（改） | 收盤 <140 | -0.2% | 跌回 Bear 下方（11/23 才剛收復，差 0.15%） | 只作描述，邊界值太近，不據此行動 |
| Y50''''''（續） | 收盤 >150 連 2 場；**或者** DT 的 PW 回到 ≥150 | +7.0% | Y11 條件 (2) 恢復 | 只作描述 |
| Y49'''''''（續） | 收盤 >153.33 | +9.4% | HW；scan 的 gamma 翻正臨界 | 只作描述 |
| Y52''''''（續） | 收盤 >155 | +10.5% | CW | 只作描述 |
| Y65'（改） | 收盤 <127.80 | -8.9% | scan 週 1σ 下緣 | 只作描述 |
| Y36''''''（續） | 收盤 <120 | -14.4% | 心理整數關卡 | 破位讀法待 user 重裁（Z64） |
| Y53''''''（改） | 收盤 <121.0 | -13.7% | scan ATR 停損（L152） | 165C 不適用停損 |
| Y58'''（續） | 收盤 <116 | -17.3% | 估值真 Bear 雙殺 | 重評 165C 是否續抱（thesis 失效）。IV 隱含 34.5% |
| Y62''（續） | MU 12/17 AMC，反應場次 12/18 | — | 真 Bear 情境的直接檢驗點；隱含 ±15.5% | 事前檢查 MU 在 SOXX 盈餘的占比與共識 |
| Y68（新） | PCE 11/25 | — | 宏觀事件（FN PM L63） | 只作描述 |
| Y63'（改） | 用逐到期 OI 確認 HW 153.33 是不是拆股前調整合約 | — | KD 已跳回 155，只剩 HW 這一腳 | ☐ `zcat` 這次仍然被擋 |
| Z63'（續） | ladder 11-20 減 11-19：Dec18 125P、150P 的 ΔOI | — | 125P 是新開倉還是移倉 | ☐ gz 讀不到。ladder 11-20 meta 已確認 oi_asof 11-20、h4_same_pct 29.3% |
| Z64'（續） | **user 重裁「破 PW＝超賣、買凸性不放空」讀法** | — | 見 S_1_5 | 🔴 仍待 user 裁決 |
| Z39''''（改） | RV 改回拆股調整口徑 | — | DT 4.4639；scan synth 446.4%，比前卡更糟 | ROMA 端修正之前，/vol 的 VRP 和 GARCH 判語一律作廢 |
| Z46''''''（改） | kit、ladder gz、TV 日曆 | — | kit ✅（在 as-of 內執行）；`zcat` ✗；TV 這次沒有用 | 把 `zcat` 加進白名單 |
| Z65（新） | NVDA 治理事件後續（董事會、監管、政府介入的細節） | — | 會影響 SOXX 的單一事件 β | 只作描述；歸 NVDA 卡處理 |

**S_1_4_4｜保護菜單（rr4u 0%，照列菜單、不追問）**

| # | 結構 | 涵蓋段 | 最大賠付 | debit |
|---|---|---|---|---|
| **0（預設）** | 不另外買 SOXX 專屬保護 | 165C 有限風險 | — | 0 |
| A'''''''''''''（改） | Dec18 BePS 125/110 x2 | 現價 -10.8% 到 -21.5%；涵蓋 MU 反應場次 | $3,000 | ☐ 沒有可靠報價（盤前格子全部帶 `*`） |
| B''''''' | 部分鎖利：賣出 165C 其中 3 口 | Δ 曝險減少約 1/3 | — | 按快照比例 5,197×3/9 ≈ **$1.73K**；會實現虧損 |

**同 moneyness IV（`strategy_card_kit.py moneyness`，取數 2026-11-24 08:33 ET，S=140.22；所有格子都帶 `*`，是盤前壞報價用 mid／last 反解的；括號內是對前卡同格的 Δpp）**

| 到期 | -15% | -10% | -5% | +0% | +5% |
|---|--:|--:|--:|--:|--:|
| 2026-12-18 | 74.2%*（-0.7pp） | 70.1%*（-3.4pp） | 68.1%*（-4.6pp） | 64.7%*（+0.5pp） | 58.4%*（-5.6pp） |
| 2027-02-19 | 67.4%*（+7.0pp） | 56.5%*（+0.5pp） | 54.1%*（-1.0pp） | 53.6%*（-0.9pp） | 57.4%*（+4.0pp） |

```
mgrid SOXX 2026-12-18 S=140.22@2026-11-24 -15:0.7423 -10:0.7007 -5:0.6812 +0:0.6467 +5:0.5835
mgrid SOXX 2027-02-19 S=140.22@2026-11-24 -15:0.6740 -10:0.5651 -5:0.5413 +0:0.5359 +5:0.5742
```

- 🔴 **這一組格子不能當「vol 變便宜／變貴」的證據**：
  - 全部是 `*` 的盤前反解。
  - Feb19 +5% 格（57.4%）比 ATM 高 3.8pp，-15% 格單日 +7.0pp，形狀不合理，符合壞報價特徵。
  - 要判斷「保護便宜」，下一張卡應該用盤中或收盤後取的 mgrid 重做。
- 可以引用的 as-of 證據只有 DT：IV 62.79、IVR 0.755、**SkewR 0.076** ⇒ put 相對 call 仍在近一年最貴的區域，**保護不便宜**（[[feedback_skew_rank_direction_high_means_call_expensive]]）。
- **不建議 A'''''''''''''**：
  - SkewR 0.076，買在 put 相對最貴的時點。
  - 最大賠付 $3,000 和 165C 剩下的 MV（$5,197）同一個量級，等於加一個方向性空單。
  - 半導體尾巴（rr9b +115.57%）應該在 TSM／QQQ 卡用指數或板塊載體一起評估（[[feedback_hedge_carrier_use_tail_quantiles_not_ev]]）。
  - SG 說「用反彈加 Dec/Jan 保護」（FN PM L18）只是敘事，不當論據；但它和 FP 同業的 put 承接同向，請在 TSM／QQQ 卡一起看。
- **B''''''' 只列出、不建議**：
  - 長天期 call 在進場時就接受了這種波動（[[feedback_no_flip_without_entry_context]]）。
  - 140.21 距離 52W 高 218.65 是 -35.9%，「近高鎖利」條款不適用。

**S_1_4_5｜策略**

1. **165C x9 續抱**：長天期、有限風險，最多賠約 1.21% NAV。
2. **不加碼**
   - Y11 只有 2/4。
   - 價格坐在 Bear $140 上，邊界太近。
   - MU 12/17 財報還沒過（隱含 ±15.5%）。
   - 現金 20.58%，低於目標帶。
3. **不追多**
   - 反彈的主因是 NVDA 治理事件和 OPEX 後回補，這是一次性衝擊。
   - ADX 31.86 仍是空方趨勢。
   - HY OAS 繼續擴大。
   - KG 145 只有 1 場，PW 125 剛寫入框架。
4. **保護**：SOXX 卡維持選項 0。半導體方向曝險 +115.57% NAV、rr4u 0%，缺口在 TSM／QQQ 卡處理。
5. **預測帳本：不寫**（理由見 S_1_4_2）。

### S_1_5｜前卡回檢（[[23-11-2026_SOXX_AUTO_strategy]] S_1，補跑卡；三分類；as-of 真收盤 11/23 = 140.21）

| ID／宣稱 | 條件 | 現況 | 判 |
|---|---|---|---|
| Y11''''''''''' | 4 條全部成立才加碼 | 1/4 → 2/4 | 未觸發；有遵守，沒加碼 |
| Y12''''''''' | SkewR ≥0.90 | 0.076 | 未觸發 |
| **Y57''** | 下一份 DT 的 PW 仍是 125 | 125 | **成立**：連 2 場，寫入框架 |
| **Y61'** | 下一份 DT 的 KG 仍是 130 | **145** | **證偽**：KG 單場跳回上方 |
| **Y64** | 收盤 ≥125 連 2 場 | 11/23 是第 1 場 | **未檢驗**（窗口還沒結束） |
| **Y55''''** | 收盤 ≥140 | 140.21 | **觸發**（只多 0.15%，邊界值）；改寫成 Y55'''''（反向條件） |
| Y50'''''／Y49''''''／Y52''''' | >150／>153.33／>155 | 140.21 | 未觸發 |
| Y36'''''／Y58''／Y65／Y53''''' | <120／<116／<110.50／<105.6 | 140.21 | **未檢驗**（價格沒有走到） |
| Y62' | MU 12/17 財報 | 還沒到 | 未檢驗 |
| Y63 | HW、KD 是不是拆股前 strike | KD 已跳回 155；gz 讀不到 | **未檢驗** ☐（KD 腳已失去意義） |
| 前卡 S_1_6「下一張卡用 DT Previous Close 確認 140.22」 | — | DT 140.21 | **成立** |
| 前卡 S_1_2_4「KD 91.67 單場是噪音」 | — | 下一場跳回 155 | **成立** |
| 前卡 S_1_2_4「Vol 頂格，買保護是買在貴點」 | — | IVR 1.0 → 0.755，但 SkewR 0.112 → 0.076 | 部分成立：絕對 vol 回落了，**相對 put 貴的狀態沒有改變** |
| 前卡「不追空」 | 行動 | 11/23 +13.64% | 行動，不評分。as-of 來看是站在受益的那一邊 |
| **Z45'''''** | 回填 OPEX 後的「volatility reversion」 | 11/23 +13.64%，IV -11.3pt | **完成**：SG 11/20「interim low」（FN PM L51-53）在 T+1 交易日兌現 |
| **Z47''''** | 用非 SG 來源核實下殺／反彈原因 | Huang 11/12 卸任、11/23 復任（NVIDIA 新聞稿、Bloomberg、NBC 等） | **完成** |
| Z63 | ladder 11-20 減 11-19 的 ΔOI | gz 讀不到 | **未檢驗** ☐ |
| Z62'／Z50'''／Z44'''''／Z49'''' | 先前場次的 ΔOI | — | **未檢驗** ☐ |
| Z39''' | RV 口徑 | synth RV 446.4%，比前卡更糟 | **未改善** |
| Z60'' | scan (4) 的結構日錯位 | 這次 11/23 價配 11/23 PW | **成立（已修正）** |
| 保護 A'''''''''''' | — | rr4u 0% | 沒有執行（user 選擇，不追問） |
| 預測帳本 | 前卡沒寫 | — | 沒有帳本 id |

**回報 user（Z64'，延續前卡）**
- 讀法原文是「破 PW＝超賣、買凸性不放空」（[[feedback_risk_pivot_is_vol_gate_not_direction]]）。目前已經有兩個方向相反的觀察：
  - **T+1（11/20）**：-10.60%，反例。
  - **T+2（11/23）**：+13.64%，和讀法同向。
- 🔴 兩場**都被事件污染**：
  - 11/20 是 put-heavy OPEX，到期部位約 75% 是 put（FN PM L51）。
  - 11/23 是 NVDA 復任 Huang；而且 SG 說消息出來前就已經跳空（L53）。
  ⇒ 都不是乾淨的檢驗。兩個都是 n=1，彼此不能抵銷。
- 待裁決的方向不變：這條讀法要不要加上「全市場相關性飆升時暫停」或「單一權值股治理／政治事件窗暫停」之類的條件。

**證偽點／限制**

1. **Z63 的開平倉軸**：ladder gz 讀不到，所以 Dec18 125P 是新開倉還是移倉仍然未知。FP 這一場沒有 SOXX，不代表已經平倉。
2. **mgrid 全部是 `*` 盤前反解**，這次不作任何 vol 便宜／貴的判斷。
3. **RV 污染**讓 scan 的 /vol 綜合評分（+1/5「傾向買 premium」）整個作廢。
4. **KG 145 只有 1 場**。Y55 的 140 只差 0.15%，邊界值會造成很多雜訊觸發。
5. 11/26、11/27 的假期日期是轉引前卡，這次沒有重新核實。

### 來源

- `spotgamma_report/auto/data_table/SPX_data-table_2026-11-24.csv` L2（欄名）、L3900；`.meta.json`（sg_quote_date 2026-11-23，fetched 2026-11-24T21:02:19+08:00）；11/18-11/20 列轉引前卡 S_1_2_2
- `log_gen_by_roma/scan_section/24-11-2026_SOXX_scan_result.md`（21:05:52 TPE，v7.44；L3、L5、L10-22、L28、L82-91、L103、L119、L144-165、L192-211、L218-249、L264-290）
- `spotgamma_report/auto/flowpatrol/flowpatrol_2026_11_24.log`（parsed 2026-11-24T21:02:00，session 11/23；L3、L6、L10、L42、L48-50、L73-79、L98-118、L288、L300）。SOXX 零命中
- `log_gen_by_roma/founders_digest/23-11-2026_founders_PM.md`（L18、L33-63）
- `brokerage_log/24-11-2026-brokerage.xlsx.log`（parsed_at 2026-11-24T07:51:03；L33、L46、L67-69、L87、L97-103、L116）
- `strike_ladder/SOXX/SOXX_ladder_2026-11-20.meta.json`（oi_asof 2026-11-20，spot 140.22，fetched 2026-11-23 19:07 ET；gz 本體沒有讀到）
- `python3 bin/strategy_card_kit.py moneyness SOXX --exp 2026-12-18,2027-02-19 --prev <23-11 卡 mgrid ×2>`、`catalysts SOXX --until 2026-12-19 --peers NVDA,AVGO,TSM,MU,AMD --extra "2026-11-25:PCE"`（取數 2026-11-24 08:33 ET）
- `python3 bin/forecast_ledger.py implied SOXX --kind close_cross_below --level 125 --sessions 10`／`--level 116 --sessions 18`
- 外部：[NVIDIA 新聞稿：Board Reinstates Jensen Huang](https://nvidianews.nvidia.com/news/nvidia-board-reinstates-jensen-huang-as-president-ceo-and-board-director)、[NVIDIA：CEO Transition](https://nvidianews.nvidia.com/news/nvidia-announces-ceo-transition)、[Bloomberg](https://www.bloomberg.com/news/articles/2026-11-23/nvidia-reinstates-jensen-huang-as-ceo-with-government-input)、[NBC News](https://www.nbcnews.com/tech/tech-news/nvidia-reinstates-jensen-huang-rcna610864)、[Al Jazeera](https://www.aljazeera.com/economy/2026/11/23/nvidia-board-reinstates-jensen-huang-as-ceo)、[Fox News](https://www.foxnews.com/live-news/ai-news-tech-markets-nvidia-11-23-26)
- 前卡 `ls_strategy/23-11-2026_SOXX_AUTO_strategy.md` S_1（轉引：雙殺 Bear $116、MU 盈餘占 28.5%、11/26-27 假期日期）
