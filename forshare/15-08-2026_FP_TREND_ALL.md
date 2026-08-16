# FP_TREND｜全市場跨日 — **零新 session**，改以 08-14 收盤＋成交量提前定調待驗項

> **產出時點**：2026-08-15 10:20 CST ＝ 08-14 **22:20 ET（美股已收盤）**
> **資料邊界**：`spotgamma_report/auto/flowpatrol/flowpatrol_2026_08_14.log`，session_date = **2026-08-13** —— **與前篇同一個 session，無新增資料**
> **接續**：[[14-08-2026_FP_TREND_ALL]]（已完整涵蓋 session 08-13）
> **本篇性質**：⚠️ **不是新的 FP 跨日分析**，而是「前篇待驗項的盤後提前定調」。前篇產出於 08-14 **10:55 ET 盤中**，本篇補上 08-14 **收盤價 ＋ 各追蹤履約價當日成交量**（前篇當下不存在的資訊）。
> **牆位 as-of**：`data_table/SPX_data-table_2026-08-12.csv`（Previous Close = **08-11**）—— **已斷更 3 個 session**
> **下一批資料**：session 08-14 的 FP 預計 **今晚 ~22:40 CST** 落檔（publish=08-15）

---

## 縮寫對照

FP=FlowPatrol｜session_date=資料實際交易日（**≠** publish 日／檔名日）｜OI=未平倉｜Vol=當日成交量｜d$/g$/v$=delta/gamma/vega notional（**買方側**口徑）｜prem=權利金流｜%ile=歷史百分位｜BTO/STO/BTC/STC=買開／賣開／買平／賣平｜dir=買方側方向判決（優先序 **g$>v$>d$>prem >> bto/sto**）｜pkg=包裹單（符號可能反號）｜PW/CW/KG/HW=Put Wall／Call Wall／Key Gamma／Hedge Wall｜DTE=距到期天數｜LEAPS=長天期選擇權｜as-of=資料截止時點｜NAV=淨資產

---

## 一、TL;DR — 五條

1. **⚪ 沒有新的 FP session。** 最新 log `flowpatrol_2026_08_14.log` 的 session_date = **08-13**，前篇已完整涵蓋；去重後無新增（[[feedback_fp_log_dedup_by_session_date]]）。重跑只會複製前篇 ⇒ 本篇改交付前篇做不到的盤後驗證（§二）。

2. **🔴 AVGO 是唯一的新增紅旗，而且推翻前篇一個結論。** 08-14 收 **392.99（−5.94%，跌破 KG 400）**，且 `Sep-18 400P` 單日 **Vol 6,209 / OI 4,218 ＝ 1.47×** ⇒ **全新部位**。前篇寫「FP 連續 10 個 session 無 AVGO ⇒ 這是 FP 覆蓋範圍外的事件」——**今晚的 FP 極可能就會出現 AVGO**（§四）。

3. **🔴 TLT 的平倉還沒完，而且量能暴增：`Sep-18 82P` 單日 Vol **82,408**（OI 141,446，**單日換手 58%**），另新增 `80P` Vol 10,858。TLT 正好收在 **HW 82**。方向待今晚 `dir=`（§三-②）。

4. **前篇「XLI 170→175→180 逐級上疊」的描述要修正**：08-14 是 `170P Vol 10,013` ＋ `180P Vol 10,009` **兩檔等量成對**，而 `175P Vol 僅 1`、`185P Vol 51/OI 351` ⇒ 較像 **180/170 垂直價差或 roll-up**，不是三層獨立堆疊（§三-④）。

5. **QQQ 2027 LEAPS 沒有跟進**：Mar-27 815C Vol 8／Jun-27 840C Vol 47／Sep-27 880C Vol 8 ⇒ 08-13 那 **$171M 是離散單筆**，不是連續買盤。前篇 §3-4 的「連續計畫」敘事，在 session 層級成立（05-26／08-04／08-13 三次），但**不可外推成日日加碼**（§三-③）。

---

## 二、方法界線（本篇能答什麼、不能答什麼）

| 資料軸 | 現在的狀態 | 能不能用 |
|---|---|---|
| **FP log（session 08-14）** | **尚未落檔**（今晚 ~22:40 CST） | ❌ 無 |
| **OI** | 逐檔實測 13 個履約價，**與前篇逐位完全相同** ⇒ OCC 隔夜才翻新，現在仍是 **08-13 收盤 OI** | ❌ 對 08-14 無新資訊 |
| **Vol（08-14 當日成交量）** | ✅ 已定案（收盤後 6h+ 取值） | ✅ 只答「**有沒有動**」 |
| **收盤價（08-14）** | ✅ 已定案（現 08-14 22:20 ET，符合 [[feedback_us_close_price_only_after_0400_tpe]]） | ✅ |
| **牆位** | `data_table` 卡在 08-12 檔（Prev Close **08-11**），**斷更 3 個 session**；`history_v4`／`synth_oi` 有 08-15 檔但**不含牆位欄**；`market_overview/2026_0815_keyLevels.json` 的 `trade_date` = **08-13**（僅 6 檔指數） | ⚠️ 帶 3 天滯後 |

🔴 **核心限制：Vol 沒有方向。** 買賣軸一律等今晚 FP 的 `dir=`（g$>v$>d$>prem）。
本篇所有「量能」讀數**只證明有交易發生，不證明方向**——參 [[feedback_verify_oi_directly_not_fp_absence]]（缺席≠平倉、OI 增長本身無方向）與 [[project_fp_p9_extreme_greek_forward_return]]（FP 買/賣軸零預測力）。

---

## 三、前篇 6 個待驗項 — 用 08-14 Vol 提前定調

| # | 待驗項 | 08-14 實測 | 判定 |
|---|---|---|---|
| ① | **SPY 回深尾 還是 續買近價？** | 蝶身 `Nov-20 520P` **Vol 16**／`Oct-30 570P` **Vol 94**（對上 OI 各 ~15 萬）＝ 死水<br>近價 `Sep-18 739P` **Vol 3,877**、`Aug-21 745P` **Vol 1,495** | **✅ 續買近價，深尾確認停手**（前篇「四層蝶式原封不動」再獲一個 session 佐證） |
| ② | **TLT 81/82/83 是否續動？** | `Sep-18 82P` **Vol 82,408** 🔴（OI 141,446，換手 **58%**）<br>`80P` **Vol 10,858**（**新增檔位**）｜`81P` 6,420｜`83P` 2,902｜`84P` 638 | **✅ 續動且量能暴增**，且**往下新增 80P**。TLT 收 **82.04 ＝ HW**。方向未定 |
| ③ | **QQQ 2027 是否第三度加碼？** | `Mar-27 815C` **Vol 8**｜`Jun-27 840C` **Vol 47**｜`Sep-27 880C` **Vol 8** | **❌ 08-14 零跟進**。08-13 的 $171M ＝ 離散單筆 |
| ④ | **XLI 是否疊到 185P？** | `185P` **Vol 51 / OI 351**（幾乎不存在）<br>但 `170P` **Vol 10,013** ＋ `180P` **Vol 10,009** ← **等量成對**｜`175P` **Vol 1** | **❌ 沒疊到 185**，且**前篇描述要修**（見下） |
| ⑤ | **IGV 是否再上調到 100P？** | `Dec-18 100P` **Vol 695 / OI 4,160**｜`90P` Vol 152｜`95P` Vol 5 | **⚪ 未定案**（有量但未達前兩層的萬口級） |
| ⑥ | **TSM Jan-27 420C vs 基準 4,686** | **Vol 122，OI 仍 4,686** | **⚪ 續掛，量級不足以定案**。基準 4,686 保留 |
| ＋ | **IWM Sep-18 288P 是否續平** | **Vol 117**（OI 16,672）＝ 已收工｜`Aug-21 295P` **Vol 4,576** | 近月保護仍活躍，**「天期縮短」的判讀不變** |

### ④-補：XLI 的描述修正

前篇 §七-③ 寫「Nov-20 put 累計 116k 口未平，履約價 **170(PW)→175→180(KG) 逐級上疊**」。

08-14 的量能分布不支持「三層獨立堆疊」：

```
XLI Nov-20  170P   OI 48,982   Vol 10,013   ← 等量
XLI Nov-20  175P   OI 55,274   Vol      1   ← 完全沒動
XLI Nov-20  180P   OI 11,962   Vol 10,009   ← 等量
XLI Nov-20  185P   OI    351   Vol     51   ← 幾乎不存在
```

170P 與 180P **相差 4 口**，而中間的 175P 一整天只成交 1 口。
⇒ **較像一組 10,000 口的 180/170 垂直價差，或把 170P 往上 roll 到 180P**，而不是在既有兩層之上再獨立加一層。
⚠️ 這是**假說不是定案**——Vol 等量也可能是兩筆無關的萬口單碰巧撞在一起。**今晚 FP 若同時收錄這兩列且 `dir=` 相反，即為 roll/垂直價差定案。**

XLI 08-14 收 **186.51**，仍在 KG **180** 之上（PW 170／HW 183／CW 195，as-of 08-11）。

---

## 四、🔴 AVGO：前篇「FP 覆蓋範圍外」的結論即將被資料本身推翻

前篇 §九-4 寫：*「FP 連續 10 個 session 完全沒有 AVGO 的機構流量列 ⇒ 這個跌幅在 FP 上找不到對應的機構訊號，是 FP 覆蓋範圍外的事件（FP 只收 top-N）。要判因，需走 TREND／新聞，不是 FP。」*

08-14 盤後實測：

```
AVGO  Sep-18 400P   OI  4,218   Vol  6,209   ← Vol/OI = 1.47x ⇒ 全新部位，非換手
AVGO  Aug-21 400P   OI  6,544   Vol  2,900
AVGO  Nov-20 350C   OI    851   Vol     13   ← 我方持倉那一檔，紋風不動
```

- AVGO **收 392.99**，**正式跌破 KG 400**（前篇看到的是 08-14 盤中 397.60，實際收盤更深）。
- 自 08-13 的 417.82 起算 **−5.94%**（前篇記的 −4.84% 是盤中）。
- `Sep-18 400P` 單日成交**超過既有 OI 1.47 倍** ⇒ 這是**新開的部位**。

⇒ **今晚 FP（session 08-14）極可能收錄 AVGO。** 前篇的「覆蓋範圍外」是**在 session 08-13 的資料上成立、但不適用於 08-14** —— 該結論的有效期只到那個 session，不是對 AVGO 的通則。

⚠️ **6,209 口沒有方向**：可能是下檔避險買進，也可能是賣方收 premium（AVGO 大跌後 IV 拉高，賣 put 收權利金同樣合理）。**要等今晚 `dir=` 的 g$／v$ 符號**，優先序見 [[feedback_fp_spread_label_leg_check]]。

---

## 五、08-14 收盤 vs 牆位總表

**收盤價 as-of 2026-08-14 16:00 ET**｜**牆位 as-of 2026-08-11 收盤**（`data_table` 斷更，[[feedback_wall_levels_ssot_sg_data_table]]）

| SYM | 08-13 收 | **08-14 收** | Δ | PW | KG | HW | CW | 位置 |
|---|---|---|---|---|---|---|---|---|
| **AVGO** | 417.82 | **392.99** | **−5.94% 🔴** | 340 | **400** | 425 | 440 | **跌破 KG** |
| QQQ | 732.07 | 731.07 | −0.14% | 660 | 700 | 718 | **730** | 貼 CW 上緣 |
| SPY | 777.88 | 776.34 | −0.20% | **770** | **770** | **770** | 780 | 三合一之上 |
| IWM | 303.50 | 305.09 | +0.52% | 295 | 300 | 299 | **305** | **正好收在 CW** |
| TLT | 82.59 | **82.04** | −0.67% | 81 | 83 | **82** | 82.5 | **正好收在 HW** |
| IGV | 106.28 | 104.08 | −2.07% | 90 | 100 | 95 | 100 | KG 之上 |
| XLI | 185.79 | 186.51 | +0.39% | 170 | **180** | 183 | 195 | KG 之上 |
| TSM | 430.49 | 426.35 | −0.96% | 400 | 400 | 415 | **425** | 貼 CW |
| MU | 949.83 | **971.66** | +2.30% | 850 | 900 | 870 | 900 | 遠在 CW 之上 |
| SMH | 589.12 | 587.82 | −0.22% | 500 | 600 | 570 | 600 | KG 之下 |
| SOXX | 550.74 | 550.42 | −0.06% | 500 | 550 | 515 | 550 | 貼 KG/CW |

⚠️ 牆位帶 **3 個 session 滯後**，AVGO「跌破 KG 400」、TLT「收在 HW 82」、IWM「收在 CW 305」這類**貼線判讀受影響最大**——牆位本身可能已經移動。

---

## 六、對我方持倉的意涵

**SSOT**：`brokerage_log/14-08-2026-brokerage.xlsx.log`（尚無 15-08 檔；ROMA v3.90 雙檔制，[[feedback_holdings_ssot_brokerage_log]]）

### AVGO（`C350 Nov-2026 ×2`，Δ 0.80，曝險 $66,975 ≈ **10.4% NAV**）

- 我方那一檔 `Nov-20 350C` 當日 **Vol 僅 13** ⇒ **跌的是標的，不是我們這條腿的流動性**。
- 機構的量全在 **400P**（Sep-18／Aug-21），與我方 350C 不同軸。
- **現在不建議動作**：400P 的 6,209 口方向未定，今晚 FP 的 `dir=` 才判得了是避險買還是賣方收 premium。
- 依 [[feedback_no_flip_without_entry_context]]：350C 是深價內（AVGO 392.99 vs 履約 350）、Δ 0.80、到期尚遠（Nov-20），**單日 −5.94% 不構成推翻進場邏輯的新資訊**。

### 其餘部位

- **QQQ／MNQ**：QQQ 收 731.07 幾乎持平。機構 2027 LEAPS 08-14 零跟進，但**也沒有反向平倉**（Vol 個位數＝完全沒動）⇒ 前篇「我方 QQQ LEAPS 最強同向佐證」的證據**未被削弱、也未被加強**。載體不動（[[feedback_qqq_call_preferred_mnq_is_fallback]]）。
- **TSM（曝險 94.38%）**：收 426.35（−0.96%），仍貼 CW 425。`Jan-27 420C` Vol 122／OI 4,686 不變 ⇒ **無新訊號**。依 [[feedback_tsm_high_conviction_hold]]：**不砍倉、不動作**。
- **半導體（SOXX+SMH+AVGO）**：SMH／SOXX 08-14 幾乎持平，避險訊號仍未出現 ⇒ **連續第三個 session 無半導體避險流量**。
- **rr4t 避險 0.00%**：依 [[feedback_low_hedge_may_be_deliberate_ask_first]]，**不預設為避險缺口、不提問**。

---

## 七、待辦

- [ ] 🔴 **今晚 ~22:40 CST 後重跑 FP_TREND**（session 08-14）——一次回答三個掛著的方向問題：
      ① TLT `Sep-18 82P` 那 82,408 口是誰、往哪個方向
      ② XLI `180P/170P` 等量對是不是 roll／垂直價差
      ③ AVGO `Sep-18 400P` 6,209 口是避險買還是賣方收 premium
- [ ] **前篇 [[14-08-2026_FP_TREND_ALL]] 兩處回頭加註更正**（等 user 點頭，本篇尚未動檔）：
      - §七-③ XLI「170→175→180 逐級上疊」→ 改為「180/170 等量成對，較像垂直價差／roll-up」
      - §九-4 AVGO「FP 覆蓋範圍外」→ 改為「該結論只對 session 08-13 成立；08-14 的 400P Vol 1.47×OI 應可進榜」
- [ ] 🔴 **牆位斷更**：`data_table` 卡在 08-12 檔（Prev Close 08-11）已 3 個 session。`history_v4`／`synth_oi` 照常更新到 08-15 ⇒ **是 data_table 這一路單獨斷**，非全面停更。建議查抓取管線。
- [ ] **前篇既有待辦沿用**（尚未做）：SAVEANA「narrative 定性形容詞不可採信」／FP `oi` 欄 pkg 假說驗證／SPY 蝶式階梯 SAVETR 建卡
- [ ] 下個 session 續驗：① IGV 是否從 100P 放量（⑤ 未定案）② TSM Jan-27 420C vs 基準 **4,686**（⑥ 未定案）③ TLT 是否往下續建 80P 以下 ④ AVGO 是否連續兩個 session 進 FP 榜

---

## 八、判讀護欄（本篇套用）

1. 🔴 **Vol 只答「有沒有動」，不答「往哪動」** —— 買賣軸一律等 FP `dir=`（[[project_fp_p9_extreme_greek_forward_return]]：FP 買/賣軸零預測力；有訊息的是 C/P 軸）
2. 🔴 **OI 在盤後尚未翻新**（實測 13 檔逐位等同前篇）⇒ 本篇任何「OI 未變」**不構成「沒有交易」的證據**，只代表資料未更新
3. **前篇結論的有效期以 session 為單位** —— AVGO「覆蓋範圍外」是 08-13 的事實，不是通則（§四）
4. 方向優先序 `g$ > v$ > d$ > prem >> bto/sto`，直接讀 `dir=`，不引用 `spread=` 標籤（[[feedback_fp_spread_label_leg_check]]）
5. **XSP 全欄封鎖**（[[feedback_fp_mini_index_premium_is_notional]]）
6. **`⚠pkg` 列的 `oi` 一律現查**（前篇 §八）
7. 去重單位是 `session_date`，非檔名日（[[feedback_fp_log_dedup_by_session_date]]）
8. 牆位一律 grep `data_table`，**as-of = 08-11 收盤（滯後 3 個 session）**（[[feedback_wall_levels_ssot_sg_data_table]]）
9. 08-14 收盤價已定案（現 08-14 22:20 ET，[[feedback_us_close_price_only_after_0400_tpe]]）
10. 單日事後對照（AVGO −5.94%、MU +2.30%）**不構成訊號有效度證據**，僅為 as-of 紀錄（[[feedback_hitrate_needs_conditional_baseline]]）

---

## 關聯

[[14-08-2026_FP_TREND_ALL]]｜[[13-08-2026_FP_TREND_ALL_PM]]｜[[13-08-2026_FP_TREND_ALL]]｜[[13-08-2026_FP_TREND_TSM]]｜[[14-08-2026_FP_TREND_QQQ]]｜[[14-08-2026_FP_TREND_TSM]]｜[[feedback_fp_spread_label_leg_check]]｜[[feedback_fp_mini_index_premium_is_notional]]｜[[feedback_verify_oi_directly_not_fp_absence]]｜[[feedback_fp_log_dedup_by_session_date]]｜[[feedback_wall_levels_ssot_sg_data_table]]｜[[feedback_tsm_high_conviction_hold]]｜[[feedback_low_hedge_may_be_deliberate_ask_first]]｜[[feedback_qqq_call_preferred_mnq_is_fallback]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_hitrate_needs_conditional_baseline]]｜[[feedback_us_close_price_only_after_0400_tpe]]｜[[feedback_no_flip_without_entry_context]]｜[[project_fp_p9_extreme_greek_forward_return]]
