# FP_TREND（For All）— 跨日趨勢分析（session 07-13 → 07-22）

- 生成日：2026-07-24（GMT+8）
- 資料範圍：flowpatrol logs 07_14 → 07_23（對應 session 收盤 07-13 → 07-22，共 8 個 session）
- 來源：`spotgamma_report/auto/flowpatrol/flowpatrol_2026_*.log`
- 前一份：[[23-07-2026_FP_TREND_ALL]]（本篇對其「SMH 極端偏多」與「TLT 機構轉向」兩點提出修正）

**縮寫對照**：FP=FlowPatrol（SG 每日選擇權流雷達）｜d$/g$/v$=delta/gamma/vega notional，**皆買方側（BuySide）**｜%'ile=同標的歷史百分位（≤5=極空、≥95=極多）｜BTO/STO=buy/sell-to-open｜session_date=資料 as-of 收盤日（≠publish 日，差 1td）｜OI=未平倉｜RR=Risk Reversal｜XSP=mini-SPX（1/10 SPX）｜LEAP=長天期選擇權｜DTE=距到期天數｜pkg=包裹單（逐腳反號）

> ⚠️ 方法論校準：
> ① FP 每檔 `session_date = publish − 1td`，本文一律用 **session（資料收盤）日**；最新 FP session=**07-22**，生成當下 age=**2td 🟡偏舊**。
> ② log 07_12 / 07_13 同為 session 07-10（非交易日重發），取後者去重（參 [[reference_fp_nontrading_day_publish_dup_session]]）。
> ③ 方向以列尾 greek 判決為準，`⚠pkg` 者逐腳反號；ExecSummary/Positioning 是 SG AI 衍生層敘事，**本期已實測到它與 greek 相反**（見第一節）。參 [[feedback_fp_greek_is_buyside_btosto_unreliable]]、[[reference_fp_index_tables_t1_settled]]。
> ④ 最新檔 QA：narrative×greek 符號一致率 100%、data_quality=OK。

---

## 〇、結論：主線換了

[[23-07-2026_FP_TREND_ALL]] 的判讀是「指數五度變盤、無法選邊」。加入 **07-22（GOOGL/TSLA ER 當日）**這筆後圖像收斂——**不是無方向，是機構在系統性地「封上檔 + 買下檔」**。

流量已部分兌現：

| 標的 | FP 07-22 收盤價 | 最新價（07-23 收盤，取自 24-07 ROMA scan cache） | 變化 |
|---|---|---|---|
| SPX | 7,499 | **7,408** | **−1.2%** |
| GOOG | 341.91 | **318.34** | **−6.9%** |
| NVDA | 212.06 | 208.76 | −1.6% |
| AMD | 552.14 | 539.69 | −2.3% |

---

## 一、【新主線 #1】「d 極多 + g 極空」的封頂潮 — 昨日結論須修正

⚠️ **本節對 [[23-07-2026_FP_TREND_ALL]] 第二節②「SMH ETF 層反覆極端偏多」提出證偽。**

| session | 標的 | d$ | g$ | v$ | 真實結構 |
|---|---|---|---|---|---|
| 07-15 | SMH | +1,374M (**99th**) | −178M (**1st**) | −2.3M (**1st**) | 賣 put |
| 07-20 | SMH | +1,357M (**98th**) | −155M (**2nd**) | −3.0M (**1st**) | 賣 put |
| 07-22 | Comm Svc | +374M (**98th**) | −55M (**0th**) | −0.2M (33th) | 賣 put + call spread |

**+delta / −gamma / −vega 三件套 = 賣 put 或 covered call，不是買 call。**
（買 call 應為 +d +g +v；賣 put 為 +d −g −v。）

**實錘**（`flowpatrol_2026_07_16.log`，session 07-15）：
`sym=SMH strike=600 type=P exp=2026-07-17 bto=10,275 → d$ = +376.52M`
**put 卻是正 delta ⇒ 買方側在賣 put**。而 SG 散文當日寫「SMH bullish call buying」——**敘事層與 greek 判決相反，以 greek 為準**。

> 修正後判讀：半導體不是「極端偏多」，而是**賣 put 收權利金／上檔封頂**——願意低位承接，但不押上漲。這解釋了為何「極端偏多」後沒有續噴（07-15 SMH 590.53 → 07-20 558.25，賣 600P 者反而被套）。

**同一 pattern 於 07-22 跨資產一致：**

| 標的 | 封頂結構 | 上檔天花板 |
|---|---|---|
| **XSP**（=SPX/10） | Sep-30 794C **賣出** prem −$109.52M（全表最大單腳） | **≈SPX 7,940** |
| **NVDA** | Oct-16 250C 賣（d$ −82.7M、v$ −540K）＋ Jan-27 250C 賣 | **$250** |
| **GOOG** | Oct-16 365C 買 / 415C 賣（call spread，⚠pkg） | **$415** |
| **MSFT** | Sep-18 405C 賣 / 360P 買（SG 自標 `Risk Reversal (Bearish)`，⚠pkg 反號） | **$405 / 護 $360** |
| **MU** | Dec-2028 1400C 賣（v$ −409K） | **$1,400** |
| **STX** | Jul-31 850C 賣 / 1050C 買（⚠pkg） | — |

**含義**：機構不是看空，是**收斂上檔預期**——用賣 call 的權利金去買下檔保護（collar）。此倉位在盤整／緩跌獲利，**在急漲時最痛**。

---

## 二、【新主線 #2】信用避險 — HYG 崩盤 put，三連 session

| session | 動作 | d$ |
|---|---|---|
| 07-20 | Sep-18 80C 賣 14,470 口 | −66M |
| 07-21 | Aug-07 80C 賣（g$ −105M）、Sep-18 74P 買 12,605 | −66M |
| **07-22** | **Aug-21 71P BTO 25,000 口，IV 18.11%** | **−117M** |

**關鍵**：HYG 現價 **$79.52**，買 **$71 put**（−10.7% OTM）。同月 79/80P 的 IV 僅 **5.9–6.0%**，71P 卻付 **18.11%**——**願付 3 倍 IV 買深度價外崩盤保險**，屬尾部險而非 delta 對沖。

**交叉印證（24-07 ROMA report）**：`MOVE 80.08↑ / VVIX 102.17 / SKEW 145.95 → systemic_credit_stress（一致 risk-off）`。FP 信用流與宏觀壓力指標同向，**互為獨立證據**。

---

## 三、【主線追蹤】TLT LEAP 大買 → 動能衰竭（昨日主線的結果）

[[23-07-2026_FP_TREND_ALL]] 將此標為「全期最乾淨的機構級偏多債訊號，值得單獨追蹤」。追蹤結果：

| session | TLT Jan-2028 $100C | OI | 動作 |
|---|---|---|---|
| 07-21 | **BTO 212,422 口**（vol 767,798，buy_prem $15.18M）＋ 同步賣 120C 211,979 | 322,690 | 一次性 call spread 巨單 |
| **07-22** | **BTO 僅 3,551、BTC 9,990** | 335,716 (+13,026) | **幾乎停手** |

Bond ETF sector d%'ile：0th(07-16) → **91st(07-21)** → **36th(07-22)**，一日回中性。

> **降權**：這是「單一大戶下了一注（買 100C／賣 120C）」，非「機構在轉向」。除非後續 session 再見加碼，不宜當趨勢訊號使用。

---

## 四、指數層：保護不是解除，是往上、往遠展期

07-22 `largest_premium` 幾乎被 XSP put 佔滿（XSP 749.90 ≈ SPX 7,499）：

- Aug-03 **720P 買 $97.89M / 714P 賣 $96.62M** → put roll **上移 strike**（保護拉近）
- Oct-16 745P 買 $48.20M → **往遠期延**
- Aug-19 680P 買 $41.77M / 730P 賣 → 遠 OTM 崩盤腿

**IWM 同步**（293.76）：下檔保護密集堆在 **280–290**——Jul-31 290P 買（d$ −140.8M）、Aug-21 287P/280P 買；IWM g$ +117M 為全期第二高。**Aug-21 是保護到期的重鎮。**

⚠️ **Equity ETF sector d$ 全期 10/11 session 為負，但 d%'ile 僅 29–59th** → 該 sector 絕對值長期結構性偏負，**百分位才是校準讀數，目前中性**。勿用絕對值誤讀為「持續偏空」。

---

## 五、VIX：賣近月 vol、買 8 月尖峰、把保護 roll 到 12 月

07-22 VIX v$ **98th %'ile**，拆腿：

| 腿 | 動作 | 含義 |
|---|---|---|
| Aug-19 35C | **BTO 52,012** | 買 8 月 vol 尖峰 |
| Sep-16 / Oct-21 35C | **STO 23,973 / 25,973** | 賣遠月尖峰 → 尾部險**集中在 8 月** |
| Sep-16 17P | STO 39,999 | 平掉 9 月短 vol |
| **Dec-16 17P** | **BTO 40,000（buy_prem $18.81M）** | **「VIX 不低於 17」的押注 roll 到 12 月** |

**判讀**：vol 交易員的看法具體——**8 月有事、9–12 月回歸低 vol**。VIX 現價 16.64。與 IWM/XSP 保護集中在 **Aug-21 到期**同源。

---

## 六、個股層：ER 後的實際定位（session 07-22）

- **GOOGL/GOOG（ER 當日）**：g$ **−57.5M（1st %'ile，歷史極端負 gamma）**。結構＝Jul-24 345P 賣 / 320P 買（put credit spread，有限看多）＋ Oct 365C 買 / 415C 賣 →「**不跌破 320、但漲不過 415**」。5dR −7.78%，兩日後再跌至 $318.34，**已測到保護腿下緣**。
- **NVDA**：07-22 全為 Jul-24 到期的 call roll / call spread close（212.5C 賣、207.5C 買、225C 買）＋ **Oct 250C 賣**。近月了結、遠月封頂。現價 $208.76。
- **MU**：07-21 d$ **−859M（全期最空單名）**→ 07-22 **+427M** 大反轉，靠 Jul-31 **800C 買入 prem $86.95M**（現價 959.52，深度 ITM＝合成多頭替代）；同時賣 2028 1400C。**短多、長封頂**。
- **MSTR**：Jul-24 call spread 開／平混雜，px 99.97 卡在 96/101/105 之間 → **0DTE gamma 戰場，非方向倉**。

---

## 七、可執行含義

1. **上檔阻力有具體座標**：SPX **≈7,940**、NVDA **$250**、MSFT **$405**、GOOG **$415**。這是機構自己畫的天花板，非技術線。
2. **Aug-21 是保護到期集中日**（IWM 280/287、HYG 71/79/80、VIX 8 月尖峰）。**8 月中下旬 vol 事件風險已被明確定價**，之後預期回落。
3. **信用是目前最乾淨的空方線索**：HYG 深度 OTM 崩盤 put ＋ MOVE/SKEW/VVIX 三重壓力一致。若要加空，**credit 比 equity 訊號乾淨**。
4. **不要把「d 極多」當多頭**——本期最大誤讀陷阱。見 d ≥95th 一律先查 g/v，**g 同時 ≤5th 即賣方結構**。
5. **TLT 那筆降權**：一次性大單，未獲後續確認。

---

## 待補 / 缺口

- **07-23 session（SPX −1.2% 當日）的 FP 尚未 publish**（今晚 ~19:56 落檔）。該份才能驗證：跌下來時那些 collar 是**加碼**還是**平倉**——這是判定「封頂潮」為趨勢或雜訊的關鍵。
- **HYG Aug-21 71P（25,000 口）需逐日追 OI**：只出現一次＝單一避險基金；連續增加＝信用真的在轉。
- 第一節的「+d/−g/−v ⇒ 賣方結構」判準若後續持續有效，值得走 SAVEANA 沉澱為長青筆記（指標有效度類）。

---

## 附錄：分析腳本

- 解析／彙總腳本：`py_dir/fp_trend/fp_trend.py`（掃 FP logs → 去重 session → 落 `fp_trend.json`）
  - `py_dir/fp_trend/rpt.py`：sector d$ 絕對值 + p9 sig_positions 逐 session
  - `py_dir/fp_trend/rpt2.py`：watchlist 逐 sym 的 d$/g$ 跨 session 矩陣
  - `py_dir/fp_trend/rpt3.py`：sector d%'ile / g%'ile 矩陣（本篇主要判讀依據）
  - 重跑：`cd py_dir/fp_trend && python3 fp_trend.py && python3 rpt3.py`
- 涵蓋欄位：p9 sig_positions、p13 sector_stats、p3/p4/p5 top_delta/gamma/vega 逐 sym 加總、p6 largest_premium、p8 unusual

[[23-07-2026_FP_TREND_ALL]]｜[[23-07-2026_fp_scan_strategy]]｜[[feedback_fp_greek_is_buyside_btosto_unreliable]]｜[[reference_fp_index_tables_t1_settled]]｜[[reference_fp_nontrading_day_publish_dup_session]]
