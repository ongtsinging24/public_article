# QQQ — 機構操作深挖（TREND）

- 產出：2026-07-24（GMT+8）
- 類型：TREND（機構近期操作足跡）＋ 持倉應對
- **現價錨點：$691.96**（＝ 2026-07-23 美股**收盤**；抓取時間 2026-07-24 10:26 GMT+8，美股 7/24 尚未開盤）
  - 前收 $705.35（07-22）→ 單日 **−1.90%**
  - 距 52W 高 **$745.34（2026-06-02）＝ −7.16%**｜52W 低 $551.23（2025-08-01）
  - 20 日區間 691.96 – 736.40 → **今日收盤正好是 20 日最低**
- 資料 as-of（**三層落後程度不同，勿混用**）：
  - **價格層**：yfinance，07-23 收盤（最新）
  - **SG 結構層（MO / keyLevels）**：`spotgamma_report/auto/founders_note/founders_PM_2026_07_23.json` → `trade_date=2026-07-22` ⇒ **落後 1 場次**
  - **synth_oi / v4**：最新 2026-07-22，**缺 07-23**（SG 端未上傳）
  - **FP tape**：`spotgamma_report/auto/flowpatrol/flowpatrol_2026_07_*.log`
    ⚠️ **index_etfs / top_index / largest_premium 明細為 T+1 結算**，report_date **不等於** session（見 [[reference_fp_index_tables_t1_settled]]）
  - **敘事層**：founders_PM PM Note ＝ **同日** recap（與 FP 明細層不同步，勿當同一天）
  - 掃描輸出：`log_gen_by_roma/scan_section/24-07-2026_QQQ_scan_result.md`（10:17:55 產出）
  - 持倉：同上掃描 §positioning 持倉對照區塊
- 前作：[[20-07-2026_QQQ_strategy]]（部位結構重構：QQQ call ＋ MNQ 對沖）

---

## 縮寫對照

| 縮寫 | 全稱 | 備註 |
|---|---|---|
| PW / CW | Put Wall / Call Wall | SG 主支撐 / 主壓力 |
| ZG / VT | Zero Gamma / Vol Trigger | gamma 翻正臨界 / 放波動制度切換點 |
| LVP / HVP | Low / High Volatility Pivot | synth 口徑支撐 / 阻力 |
| LG1–LG4 / CM / C1–C3 | Large Gamma strikes / Combo Mid / Combo levels | MO 衍生水位 |
| DR / GR | Delta Ratio / Gamma Ratio | call/put delta 比、call gamma 佔比 |
| LCa / LPu | Large Call OI / Large Put OI | 大倉集中行權價 |
| GEX | Gamma Exposure | dealer 淨 gamma |
| DGP | Dealer Gamma Profile | 全鏈 gamma 曲線 |
| IVR / RV / VRP | IV Rank / 已實現波動 / IV−RV | |
| COR1M | 1-Month Implied Correlation | SG dispersion 指標，SG 定義 <8 ＝ red alert |
| HIRO | Hedging Impact of Real-time Options | SG 即時流向 |
| d$ / g$ / v$ | Delta / Gamma / Vega notional | **買方側**讀數（見 [[feedback_fp_greek_is_buyside_btosto_unreliable]]） |
| BEPS / BuPS | Bear Put Spread（買高賣低）/ Bull Put Spread（賣高買低） | |
| RP | SG Risk Pivot | 本波 SPX 7,480 |
| flow_ratio | volume ÷ \|synth OI chg\| | 越高＝當沖/HFT 佔比越高 |

---

## 0. 前作驗證點回收（[[20-07-2026_QQQ_strategy]]）

| 07-20 訂下的規則 | 07-24 的狀態 | 判定 |
|---|---|---|
| **對沖觸發＝SPX 跌破 RP 7,480** | 07-23 SPX 收 **7,408**（−1.2%），**已在 RP 下方**；SG 明言「we remain risk-off if SPX < 7,480」 | ✅ **觸發條件成立** |
| **或 QQQ 跌破 key gamma strike** | QQQ max_g_strike **$706**、ZG $709（MO）／DGP 插值 ZG **$714.09**；現價 691.96 **全數在下方** | ✅ **觸發條件成立** |
| ④「現在 IV 環境對買 call 不利」 | IVR **62%**、Pctile 83%、IV slope **−0.39 backwardation**、VVIX 102.17↑ | ✅ **仍然成立，且未改善** |
| 待辦：依 IV rank 決定 call vs call debit spread | IVR 62% 偏高 ⇒ **裸買 call 不利，應走 spread** | 📌 **本篇沿用** |
| 待辦：07-22 GOOGL+TSLA ER 前確認多單腿不壓在財報 gamma | 已過。GOOGL **−7%**（上修 CapEx）、TSLA **−16%** ⇒ Mag7 錄得 **2025-04 關稅拋售以來最差單日** | ⚠️ **事件已實現且偏空** |

→ **前作的兩條對沖觸發線在 07-23 全部亮燈。** 本篇不是重新判方向，而是回答：機構在同一時間做了什麼、我該照抄哪一段。

---

## 1. TL;DR

**機構沒有做空 QQQ，而是「便宜地買保險 ＋ 一路砍掉上檔期待值」。這是防守型減曝險，不是翻空。**

三條互相獨立、方向一致的證據鏈：

1. **Put debit spread 階梯逐週下滾**（700/660 → 690/660 → 700/680），單筆 premium 從 $39M 加碼到 **$72M**
2. **LCa 從 $800 一路砍到 $730**，而 **LPu 釘死在 $660 一格未動** — 上檔天花板降、下檔地板不撤
3. **SG Founders 07-22 白紙黑字**：「we are going to be **adding to short dated, cheap, OTM index put flies (SPX/QQQ)**」

---

## 2. 主軸一：Put Spread 階梯下滾（逐 session 帳本）

> ⚠️ **本表已把 FP report_date 校正為 session date**（T+1）。校正方法：以 FP 內 `px=` 對回當日收盤價驗證，逐筆比對通過。

| session | FP 檔（report） | 對回收盤 | 結構 | 到期 | 淨 premium | OI | 判讀 |
|---|---|---|---|---|---|---|---|
| **07-09** | 07_10.log | 723.28 vs px 723.18 ✓ | 賣736C / 買730C ＋ 673P/620P | Jul-31 | Condor Open | 736C 56.6k | **賣上檔 call spread**，區間頂看法 |
| **07-13** | 07_14.log | 711.74 vs px 711.72 ✓ | **買 700P / 賣 660P** | Aug-07 | **+$39.08M** / −$10.91M | 700P 29.2k、660P 28.1k | 開 debit put spread |
| **07-16** | 07_17.log | 705.94 vs px 706.02 ✓ | **買 690P / 賣 660P** | Aug-07 | **+$72.03M** / −$13.07M | 690P **55.8k**、660P **56.4k**（翻倍） | **加碼近一倍，strike 從 700 下滾到 690** |
| **07-17** | 07_20.log | 695.33 vs px 695.33 ✓ | 700P（prem −43.30M, SELL） | Aug-21 | −$43.30M | 700P **59.0k** | 大額 700P 佈局延伸到 8 月下旬 |
| **07-20** | 07_21.log | 696.06 vs px 695.99 ✓ | 賣690P / 買660P | Aug-07 | −$33.47M / +$11.83M | 690P **41.6k**（−14k）、660P 51.2k（−5k） | **OI 淨減 ⇒ 部分平倉了結** |
| **07-20** | 07_21.log | 同上 | **買 700P / 賣 680P** | **Jul-24** | +$19.08M / −$5.21M | 700P 24.9k、680P 29.5k | **換成貼價短天期**（今天到期） |
| **07-20** | 07_21.log | 同上 | **615P ×17,972**（BTO 段） | **Jul-24** | IV **53.0%** | — | 深 OTM（−11.6%）**尾部 fly** |
| **07-21** | 07_22.log | — | 無 QQQ 大單 | — | — | flow_ratio 24.12 | 敘事：index ETF delta **−$6.79B(98th)**、QQQ −$1.63B，但 QQQ gamma **+$153.71M** |
| **07-22** | 07_23.log | — | 無 QQQ 大單 | — | — | flow_ratio 26.72 | 敘事：QQQ gamma **+$460.57M**、delta **+$326.27M**（call buying） |

### 判讀

- **07-13 → 07-16 是明確的「加碼買保護」**：premium 近乎倍增（39M → 72M），且 strike 追著價格往下滾（700 → 690），660P OI 從 28k 翻倍到 56k。
- **07-20 把 Aug-07 那組部分平倉，但沒有裸奔** — 同一場次立刻換上 Jul-24 700/680 貼價 spread ＋ 615P 深尾保險。
  → 這是典型的**保險續保 ＋ 降成本**：近價 spread 承擔第一段跌幅、深 OTM fly 保尾部。**不是撤退。**
- **07-21、07-22 兩場 QQQ 沒有大額單腿**，但敘事層顯示 gamma 轉正、call buying — 在 07-22 已經在跌、07-23 大跌的背景下，這比較像 **put spread 平倉 ＋ 逢低 call**，而非新一輪看多建倉（單日 delta 讀數不可信，見 §5）。

### 方向判定方法論

依 [[feedback_fp_greek_is_buyside_btosto_unreliable]]：`bto/sto` 在包裹單逐腳反號、不可判向（FP 自己標 `⚠未校驗·勿判向`）。
本表一律以 **prem 正負號 ＋ spread 標籤 ＋ OI 增減** 三者交叉認定，**不採用 bto/sto**。

---

## 3. 主軸二：上檔天花板下修 vs 下檔地板不動

近 20 個交易日 positioning（source：scan §positioning，最新結構日 2026-07-22）

```
日期     LVP   HVP   LCa   LPu   P/C    DR    Act
7/22     495   711   730   660  1.36  0.45  0.22
7/21     497   715   730   660  1.38  0.44  0.15
7/20     490   707   730   660  1.36  0.43  0.38
7/17     490   710   730   660  1.34  0.47  0.18
7/16     495   734   736   660  1.35  0.50  0.22
7/15     505   732   736   660  1.35  0.33  0.16
7/14     505   732   736   660  1.37  0.27  0.19
7/13     500   724   736   660  1.36  0.40  0.13
7/10     510   739   736   660  1.36  0.27  0.36
7/9      510   732   736   660  1.35  0.26  0.34
7/8      500   716   800   660  1.34  0.36  0.33
7/7      497   718   800   660  1.34  0.35  0.29
7/6      505   726   800   660  1.35  0.28  0.39
7/2      500   725   800   660  1.35  0.38  0.22
7/1      510   735   800   660  1.37  0.27  0.30
```

| 欄位 | 月初 → 現在 | 判讀 |
|---|---|---|
| **LCa（大倉 Call）** | **800 → 736 → 730** | 07-09、07-17 兩次下修，之後**未再上調**。上檔期待值連續被砍 |
| **LPu（大倉 Put）** | **660 → 660（一格未動）** | 機構認定的**真正防線**，整個 7 月毫不動搖 |
| HVP | 739 → 711（−3.8%） | 阻力帶同步下移 |
| LVP | 510 → 493（−3.3%） | 支撐也在鬆動 |
| P/C OI | 1.37 → 1.36 | 持平，**結構穩定不是恐慌** |
| Activity | 0.263 → 0.233 ↓ | 機構動作變少 |
| Gamma Notional（均） | −1806M → −1502M ↑ | 負 gamma 略收斂但**未實質修復** |
| Delta Notional（均） | +7049M → +6649M ↓ | 淨多頭 notional 緩降 |

**關鍵推論**：建倉廣度 730/660，比 1.11，表面「Call/Put 均衡」。但 660 距現價 **−4.6%**、730 距現價 **+5.5%** —
**機構把上下緩衝帶擺得幾乎對稱，等於在說「未來一個月我預期是寬幅震盪，不是趨勢」**。這與 ADX 19.61（≤20 區間環境）互相印證。

---

## 4. 主軸三：Dealer Gamma 制度 — 現價在所有臨界之下

| 水位 | 價格 | 現價（$691.96）相對位置 |
|---|---|---|
| CW（強壓） | $730.00 | −5.2% ⬇ |
| LG2 | $720.00 | −3.9% ⬇ |
| **ZG（DGP 27-strike 插值）** | **$714.09** | −3.1% ⬇（跨日 716.15 → 714.09，**−0.29% ↓**） |
| ZG（MO） | $709.00 | −2.4% ⬇ |
| **VT（放波動臨界）** | **$706.00** | −2.0% ⬇ |
| **PW / LG1 / C1（強支撐）** | **$700.00** | **−1.1% ⬇ 已跌破** |
| LG3 / C2 | $690.00 | −0.3% ⬇ ← **現價貼在這** |
| CM / C3 | $680.59 / $679.88 | −1.6% / −1.7% |

- **Dealer Net GEX（近 5 日，v4 全鏈）：−$3.30B → −$3.12B**，深負 gamma 制度**穩定**
- **ATM 當日 GEX −$2.04B**，GR **0.21**（**put gamma 絕對主導**）
- **Gamma 集中區（下方 top 3）**：$677 **−1.26B** / $672 **−1.25B** / $683 **−1.24B**
  → **跌穿 $680 後，下面是連續三層負 gamma 加速帶**
- **真 gamma 檢驗**：剔除最近到期後仍為負 gamma ⇒ **不是 0DTE 幻象，是結構性負 gamma**
- **Pin 強度**：#1 PW $700（87/100）、#2 CW $730（54/100）→ 強 pin 主導
- **今天（07-24）＝ 最大 Gamma 到期日**。SG 明示：07-23 的 0DTE put selling 一到期，若下檔 put 需求延續，**dealer gamma 會更負**

→ 現價已在 PW $700 之下 ⇒ **「支撐轉壓力」**。要重新偏多，必須先收復 $700，再站上 VT $706 才算脫離放波動制度。

---

## 5. 主軸四：SG Founders 的直接自白 ＋ 07-23 HIRO 佐證

Source：`spotgamma_report/auto/founders_note/founders_PM_2026_07_23.json`

> 「Given these risks, we are going to be **adding to short dated, cheap, OTM index put flies (SPX/QQQ)**.」
> 「we remain **risk-off** if SPX is < 7,480」（07-23 收 **7,408**，已在下方）

07-23 同日 recap 的關鍵細節：

- **Mag 7 錄得 2025 年 4 月關稅拋售以來最差單日**
- **HIRO 顯示負 delta flow 來自「長天期 call 賣出（減上檔）＋ put 買入（加下檔）」的組合**
  → 這是本文 §2、§3 的**完全獨立佐證**：同一個動作在 OI 結構、premium 帳本、即時流向三個口徑同時出現
- 約 **75% 的 S&P Equities HIRO flow 來自 Mag 7** ⇒ QQQ 是這波的震央
- 盤中賣壓約 **−$4B** S&P equities flow，集中在前 90 分鐘；SG Implied 1-Day Move Low 7,370 守住
- GOOGL **−7%**（上修 CapEx 指引）、TSLA **−16%**；油價站上 **$90**（7 月以來 **+28%**）、10Y **4.6%**
- **COR1M 單日跳 71% 至 7.3**，dispersion trade 反轉為 **long index vol / short single-stock vol**
  → **對 QQQ：index IV 會被撐住**（不利賣 index premium）
- INTC 財報後 +7%（~107），SG 續看 KGS 110 / CW 120（與 QQQ 無直接關係，僅記錄）

### ⚠️ 分歧點：ROMA「建多視窗」vs SG「red alert」

| 來源 | 讀數 | 結論 |
|---|---|---|
| ROMA scan（今日 10:17） | Corr Proxy 0.095，近 5 日低點 0.076 曾 <0.08，現已回升 | 🟢「單股 call 擁擠解除，dispersion unwind，**建多視窗開啟**」 |
| SG Founders | COR1M <8 ＝ **red alert zone**；07-23 跳 71% 至 7.3 仍在紅區 | 🔴「**remain risk-off**」 |

依 CLAUDE.md「解讀 SG_DATA 遇矛盾 → 官方 edu 優先」原則：
**此處採 SG 讀法 — 相關性從極低區反彈＝dispersion unwind，歷史上伴隨 index 下行。ROMA 的「建多視窗」在本次不採信。**
（📌 待辦：這是 ROMA 訊號品質可檢驗的一條，見 §9）

---

## 6. 雜訊校正（避免誤讀）

| 訊號 | 讀數 | 為何要打折 |
|---|---|---|
| **flow_ratio** | 07-15→07-22 各 session 介於 **21–32**（07-22 session＝26.72） | **HFT 主導**，ROMA 已標「gamma/regime 訊號需大幅折扣」 |
| **sig_position d%** | session 07-15 g **99th** → 07-16 d **6th** → 07-17 d **100th** | **三日內從極空翻極多再翻，純 whipsaw，單日 delta 讀數無資訊量** |
| **水位分歧** | synth LVP $495 vs MO PW $700 ＝ **29.3%**（重度） | D9/D10 維度已歸零；**一律以 MO 水位為錨**，Layer 3 走雙止損 |
| **MO 一致性** | ZG $709 > VT $706（典型應 ZG≤VT）；LG3 $690 / LG4 $680 落在 (PW 700, CW 730) **之外** | 上游可能有陳舊 LG／異常 ZG-VT 排列，該三檔水位判讀留 buffer |
| **Layer 0 估值** | 基準 2026-06-14，**已陳舊 40 天** | 估值軸降權；本裁決以 Layer 1 信號 / Layer 4 時機為主 |
| **synth_oi / v4** | 最新 07-22，**缺 07-23** | 結構層看不到 07-23 大跌，下一次掃描才會反映 |

**結論**：**日層級的 delta 讀數在 QQQ 幾乎沒有資訊量（被 HFT 洗掉）。唯一乾淨的機構足跡是 OI 結構（LCa/LPu）與大額 premium spread 帳本** — 而這兩者方向一致：**降上檔、守下檔**。

---

## 7. Vol 側：保護在變貴，但還沒到恐慌

| 指標 | 讀數 | 判讀 |
|---|---|---|
| 1M IV / 1M RV | 23.9% / 22.8% | **VRP +1.2pt ≈ 合理定價** |
| IV Rank / Pctile | **62%** / 83% | 偏高 |
| Fwd GARCH | 22.2%（Garch Rank 57%），GARCH−IV **−1.8pt** | 與 IV 一致 |
| **IV Slope (NE 45)** | **−0.39 → Backwardation** | 近月 IV > 遠月 ＝ **短期事件壓力**；IV crush 風險高 |
| **Skew（NE 25Δ/95Δ）** | **+10.5pt** | **左尾機構買保護明顯** |
| **Skew（年化 25Δ/95Δ）** | **+15.1pt** | 同上，更明顯 |
| Skew 趨勢維度 | **−2**（本次掃描最重的單一負分） | 與 §2 put spread 帳本一致 |
| Bollinger | %b **0.02**、bandwidth 0.0624（126 日 36 分位） | **貼下軌**，但無 squeeze 壓縮 |
| VP 結構 | POC 599.18、VAH 707.65 / VAL 554.99；VWAP(week) **700.8** | 現價在**價值區內**且**在週 VWAP 之下**（機構成本帶下方，偏空） |
| 系統 vol | MOVE 80.08↑ / VVIX **102.17**↑ / SKEW **145.95** | **systemic_credit_stress — 一致 risk-off** |
| Vol 綜合 | **−1/5，偏貴，傾向賣 premium** | 但 VVIX 升溫 ⇒ 賣方要防 vol regime 切換 |
| VIX FP 結構（p1, 07-22 session） | Call STO 42.0% / Put STO 47.6% | 🟡 mixed，**雙向、無定論** |

**對照 [[feedback_skew_overrides_layer0_undervalued]]**：該筆講的是「skew 暴衝 ＋ 估值超跌 → 疑似價值陷阱」。
本案 QQQ 是 **skew↑ ＋ 估值偏貴**（現價 691.96 高於 base $648 約 **+6.8%**）— **兩軸同向偏空，沒有矛盾**，訊號比個股案例乾淨。

**Layer 0 三情境**（⚠️ 基準已陳舊 40 天，僅供定位）：
🔴 Bear $511（−26.2%）｜🟡 Base $648（−6.4%）｜🟢 Bull $792（+14.5%）｜**R:R 0.55（上行/下行 <1，盈虧比偏差）**

---

## 8. 對現有持倉的意涵

```
QQQ ×116 股　均成本 $680.76　MV $81,811　浮盈 +$2,843（+1.6%）
QQQ Jan15'27 725 Call ×2　MV $9,202
   ↳ $725 vs MO: CW $730.00(+0.69%) | LG2 $720.00(-0.69%) | ZG $709.00(-2.21%)
── QQQ 總曝險：$91,013
```

| 關鍵價位 | 價格 | 現況 |
|---|---|---|
| 股票成本 | **$680.76** | 現價在其上 **+1.6%**，**緩衝只剩 1.6%** |
| **CM / C3 防線** | **$680.59 / $679.88** | **與成本線幾乎重疊** — 這道破了＝浮盈歸零 |
| ATR 停損（ATR 2.1% × k=2） | $663.0 | −4.2%（波動自適應，基準 2026-07-22） |
| 下行風險（DR=0.45） | $657.4 | −5% |
| LPu 鐵板 | $660 | −4.6%，機構認定的真防線 |
| Jan'27 725 Call 行權價 | $725 | 距現價 **+4.8%**，卡在 CW $730 下緣 |

### 三點觀察

**① $680 是雙重關卡**
既是股票成本線（$680.76），也是 SG 的 CM/C3 防線（$680.59/$679.88），且下方 $683/$677/$672 是**連續三層負 gamma 加速帶（各約 −1.25B）**。
**破 $680 ＝ 浮盈歸零 ＋ 進入加速下行區。這是最需要「事前」決定的一條線**（呼應前作洞①：觸發必須是規則不是情緒）。

**② Jan'27 725 Call 的敵人是時間不是方向**
機構已把 LCa 從 800 砍到 **730**，等於**共識上檔就到 $730**。$725 剛好貼在共識天花板下緣 — 這在震盪市是最難賺的位置（既拿不到 delta，又持續掉 theta）。
但 **328 天到期仍長**，且 QQQ **最大 Delta 到期日正是 2027-06-17**（長天期機構布局區）⇒ **不急著處理，但也不該再往這個方向加碼**。

**③ 機構的做法可以照抄一半**
他們的動作是「**不減股票、加買 put spread**」。若不想動核心股票部位，**買 Aug-07 或 Sep 到期的 put debit spread（例如 680/650）就是最貼近機構足跡的對沖** — 成本可控、不動核心倉、且與 §2 帳本同一結構。
⚠️ 但 IVR 62% ＋ backwardation ⇒ **買近月保護偏貴**，用 spread（而非裸買 put）才對，這也正是前作洞④的延伸。

---

## 9. 觸發線（可直接掛監控）

### 偏空確認
- 🔴 **日收 < $680.59**（CM/C3 ＋ 股票成本線）→ 進入 $683/$677/$672 負 gamma 加速帶，目標 **$660**（LPu 鐵板）
- 🔴 **SPX 持續 < 7,480**（SG RP，已破）且 **Aug-07 660P OI 再度放大** → 機構認定 $660 會被測試
- 🔴 **LPu 從 660 下移到 640/620** → 防線讓出，**這才是真正轉空的訊號**（目前未發生）

### 偏多修復（需依序達成）
- 🟢 **日收 > $700 站回 PW**（歷史守住率 89%，需 EOD 確認）→ 支撐重新生效
- 🟢 **站上 VT $706 → 再過 ZG $714.09** → 才真正脫離放波動制度
- 🟢 **突破 CW $730** → MAGNET 觸發，目標 $740.95；但需 **rally_flow = FLOW_SUPPORTED** 確認才視為磁吸靶

### 結構待觀察（下次 CHKTR 要回收）
- 👀 **LCa 是否從 730 再往下修**（掉到 720 以下 ＝ 機構進一步認輸上檔）
- 👀 **LPu 660 是否鬆動**（見上，真正的轉空條件）
- 👀 **07-24（今日）最大 gamma 到期後，dealer gamma 是否如 SG 所述更負**
- 👀 **07-20 那組 Jul-24 700/680 put spread 今日到期後，機構是否再續一組**（續 ＝ 保險不撤；不續 ＝ 風險偏好回升）
- 👀 **ROMA「Dispersion 解除 → 建多視窗」vs SG「COR1M red alert」孰對** — 定期 review ROMA 信號品質的一條可檢驗樣本
- 👀 **Layer 0 估值已陳舊 40 天，需重估**（base $648 是否仍成立）

### 事件錨
- **07-29 FOMC ＋ MSFT / META 財報**（Mag7 佔 HIRO flow 75%，QQQ 直接受震）
- **07-30 GDP**
- 油價 >$90（7 月 +28%）、10Y 4.6% — SG 定義的兩大 macro risk

---

## 10. 綜合裁決

⬜ **中性偏空，區間操作**（ADX 19.61 ≤20，趨勢/突破訊號打折）
— 與 ROMA 綜合裁決一致（bias −2/22，🟡 中可信度），但**本篇把權重放在 OI 結構 ＋ Founders 自白，而非 bias 分數**（bias 是混合訊號：DR 趨勢 +1、Large OI +1 vs Skew −2、DR 水準 −1、Net GEX −1）。

> **機構不是在做空 QQQ，是在「便宜地買保險、順便把上檔期待值砍掉」。**
> 對持倉者的翻譯：**不必急著砍股票，但要立刻決定 $680 破了怎麼辦，並考慮用 put debit spread 把 $680–$660 這段跌幅買斷。**

---

## 待辦 / next step

- [ ] 依 §8③ 試算 Aug-07 / Sep 680/650 put debit spread 的實際成本與 breakeven，決定是否執行
- [ ] 把 §9 觸發線寫成 TRACKING_DIR 追蹤檔（SAVETR），逐日回標
- [ ] **重估 Layer 0**（估值基準已陳舊 40 天，base $648 需更新；QQQ 為 ETF，走 index 加權而非個股 NTM blend）
- [ ] 07-24 收盤後回收：最大 gamma 到期的 pin 效果、Jul-24 700/680 是否續作
- [ ] 07-29 FOMC + MSFT/META ER 前，確認 Jan'27 725 Call 不需 roll（328 DTE 尚不急）
- [ ] 記錄 ROMA vs SG 的 dispersion 讀法分歧結果，若 SG 讀法連續勝出 → 考慮 SAVEANA 沉澱

---

## 關聯

- [[20-07-2026_QQQ_strategy]] — 前作：QQQ call ＋ MNQ 對沖的部位結構重構（本篇 §0 回收其驗證點）
- [[21-07-2026_NDX-MNQ_strategy]] — NDX/MNQ 同族標的
- [[23-07-2026_SOXX-SMH_strategy]] — 同期半導體端的機構足跡對照
- [[23-07-2026_TRENDFN]] — 同期 Founders Note 跨日趨勢
- [[reference_fp_index_tables_t1_settled]] — 本篇 §2 session 校正的依據
- [[feedback_fp_greek_is_buyside_btosto_unreliable]] — 本篇 §2 方向判定方法論
- [[feedback_skew_overrides_layer0_undervalued]] — §7 對照（本案無矛盾）
- [[feedback_conservative_base_pe_no_rerating]] — §7 Layer 0 重估時沿用
