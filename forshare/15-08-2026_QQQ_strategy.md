# QQQ 跨日結構分析與策略 — 2026-08-15（台北，週六休市）

> **現價：$731.07**（2026-08-14 確定收盤，已過 04:00 GMT+8 門檻）；較 08-13 收盤 $732.07 −0.14%。
> 本卡承接 [[14-08-2026_QQQ_strategy]] 與 [[13-08-2026_QQQ_tracking]]（V1–V4 觸發表）；並與同日避險提案卡 [[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]] 對照（QQQ 段）。
>
> **來源**：
> `log_gen_by_roma/scan_section/{14,15}-08-2026_QQQ_scan_result.md` ＋ `..._QQQ_SPY_scan_result.md`（同二日）
> ＋ `spotgamma_report/auto/history_v4/QQQ/QQQ_v4_gex_2026-08-{11..14}.csv`
> ＋ `spotgamma_report/auto/synth_oi/QQQ/QQQ_synth_oi_2026-08-{11..14}.csv`
> ＋ `spotgamma_report/auto/flowpatrol/flowpatrol_2026_08_14.log`（session_date 08-13）
> ＋ `founders_digest/14-08-2026_founders_{AM,PM}.md`
> ＋ yfinance QQQ 全鏈現查（08-14 收盤結算 OI）
> ＋ `brokerage_log/14-08-2026-brokerage.xlsx.log`（持倉 SSOT）
>
> **產出方式**：`TREND2 QQQ` → `TREND QQQ`（兩支平行 fork）→ `SAVEST`

---

## 縮寫對照

| 縮寫 | 全稱 | 說明 |
|---|---|---|
| PW/CW/KG/ZG | Put/Call/Key Gamma Wall、Zero-Gamma | SSOT＝`data_table`/`history_v4`（[[feedback_wall_levels_ssot_sg_data_table]]） |
| IVR/GarchR/SkewR | IV Rank／Garch Rank／Skew Rank | **SkewR 高＝call 貴/put 便宜**（[[feedback_skew_rank_direction_high_means_call_expensive]]） |
| VRP | Vol Risk Premium ＝ IV − RV | 負值＝premium 便宜、偏買方 |
| DR | Delta Ratio | Layer 4 追蹤門檻 V2＝DR>1.5 |
| ADX | Average Directional Index | ≤20＝區間環境 |
| LEAPS | 長天期選擇權（此處指 2027 到期各檔） |
| BePS | Bear Put Spread |
| FP | SG FlowPatrol（大單流） |
| OI | 未平倉量 |
| rr4/rr6/rr8/rr8b | brokerage_log 風控欄位 | rr4＝index避險%、rr6-2＝Δ等效股數含期貨、rr8＝原始集中度、rr8b＝方向性曝險(不含期貨) |
| OPEX/JHOLE | 月選擇權到期日(本輪08-21)／Jackson Hole(08-27-29) |

---

## 0. 樣本邊界

| 層 | as-of | 值/備註 |
|---|---|---|
| 價格 | **2026-08-14 收盤** | $731.07（已過 04:00 台北門檻，非盤中價） |
| SG 牆位/vol（data_table, history_v4, synth_oi） | 08-13 收盤結構 | 檔名 08-14，內容落後（正常 D−2 現象，[[feedback_wall_levels_ssot_sg_data_table]]） |
| FP tape | session_date **08-13** | 檔名 `flowpatrol_2026_08_14.log`，publish 日≠資料日 |
| 持倉 | 2026-08-14 匯出 | SSOT，週末無新檔 |
| QQQ 專屬 scan_result | 僅 14-08、15-08 兩天可讀 | 純 scan 層跨日樣本薄，主要靠 history_v4/synth_oi 五日序列＋既有策略卡補足框架 |

---

## 1. 跨日框架（TREND2）

### 1.1 牆位／regime（history_v4，as-of 08-13）

| 水位 | 值 | 對照 08-11（[[14-08-2026_QQQ_strategy]] §4.4） |
|---|---|---|
| CW | **$735** | $730 → 上移 5 點 |
| Max-Gamma pin | $729 | — |
| Top strike | $730 | — |
| Zero-Gamma | **$719** | $715.40 → 上移 3.6 點 |
| PW | **$660** | $660 → **連續多場次未動** |

現價 $731.07 落在 ZG 之上、pin 與 CW 之間 → 正 gamma 區間，729–735 續有磁吸傾向。牆間距 $660–$719/735 之間仍是舊卡標注的結構真空區，PW 遲遲未跟進上移，是本輪未解決的既有缺口（[[13-08-2026_QQQ_tracking]] H2 門檻 PW≥690 仍未觸發）。

### 1.2 Vol surface：持續極端，且更便宜一階

| 指標 | 08-11（前卡） | 08-13（本卡） | 讀法 |
|---|---|---|---|
| SkewRank | 0.956 | **0.96–0.99** | call 貴/put 便宜持續在極值（同一公約方向） |
| IVR | 0.32 | **~0.25** | 續探低，比前卡更便宜 |
| GarchR | 0.57 | ~0.53 | 高檔持平 |

VRP 延續負值格局，founders_digest 08-14 PM 原文明確引用「QQQ IV<RV 過去 1.5 年罕見背離」——ROMA 內部算法與 SG 官方敘事雙源互證，非我方衍生推論。

### 1.3 結構裁決：15-08 scan 出現「多層矛盾」🔴，非前卡的偏多確認

⚠️ 這與 [[14-08-2026_QQQ_strategy]] §2.2 記錄的「08-13 盤中已上穿 CW $730 並站住」（ROMA G7 曾判「MAGNET 潛在」等 rally_flow 確認）方向不完全一致——本卡 15-08 scan 對整體裁決降級為低可信度。**判讀**：08-14 收盤 $731.07 確實守住前卡待驗的 CW $730（[[14-08-2026_QQQ_strategy]] 待辦 T-A 就此可視為初步確認），但同時 ADX≤20 的區間環境判定沒有改變，「矛盾」標籤反映的較可能是多指標在區間頂部互相打架，非趨勢反轉訊號。不宜單憑此裁決字面加碼或減碼。

### 1.4 LEAPS 階梯：週末 OI 完全持平，無新增量

| 到期/履約 | OI |
|---|---|
| Mar-19-27 815C | 20,421 |
| Mar-19-27 830C | 20,662 |
| Jun-17-27 840C | 23,735 |
| Jun-17-27 880C | 40,483 |
| Sep-17-27 880C | 20,151 |
| Nov-20-26 725P/745C（collar） | 12,291 / 12,000 |

機構倉位仍是**槓鈴結構**：遠端 2027 深 OTM call 階梯（凸性）＋ Nov-20 近端 collar（保險），兩者並存、無跡象拆解。下次有意義的複查點是週一 08-17 盤後。

---

## 2. 即時／事件層（TREND）

### 2.1 FP：QQQ 是當日全市場極端倉位第一名

`flowpatrol_2026_08_14.log`（session_date 08-13）標題即「QQQ and TLT See Extreme Moves」：delta $1,657.9M（100th %ile）、gamma $369.1M（99th %ile）、vega $13.0M（100th %ile）。最大三筆溢價全數為**長天期深 OTM Call 的 BTO 主導**（815C Mar'27／840C Jun'27／880C Sep'27，單筆 $51.7M–$62.7M）。

⚠️ **FP 自動摘要文字寫「call overwriting/upside supply」，但逐腳 bto/sto 明顯淨買進，與其自身摘要矛盾**——依 [[feedback_fp_spread_label_leg_check]] 判讀以逐腳方向為準，不採信摘要文字。flow_ratio=13.37（全樣本偏低）⇒ 真建倉，非當沖噪音。

### 2.2 yfinance 全鏈現查（08-14 收盤結算 OI）

- 近端 08-21：730/735/740/750C 皆為活躍換手（vol/OI 比 0.4–0.55），偏 dealer/retail 對沖 churn；700C(43,940 OI)、900C(36,394 OI) 為舊倉。
- 720P(31,662 OI，vol 14,150) 為現價下方活躍保護盤。
- **monthly 09-18 800C 出現異常放量**（43,673 OI／17,944 vol，比值 0.41）— 現價上方 +9.4%，值得續盯是否為新一輪右尾建倉的前哨。

### 2.3 SG 官方敘事（founders_digest 08-14 PM）

Risk Pivot 一路上調：8/3 的 7,480 → 8/7 的 7,680 → **8/14 的 7,775**（隨大盤同步上修，SPX 現收 7,786 已在其上）。短線偏多看到 VIX Exp(8/19) 目標 SPX 7,900–8k，但**已提防 OPEX(8/21) 後反轉**（NVDA ER 8/26＋Jackson Hole 8/27-29 接踵而至）；SG 已開始小量布局 ≥1 個月 QQQ/SPX put spread，並計劃下週加碼 VIX call。

### 2.4 三源互證

FP 大單（買 LEAPS call）× vol surface（call 貴/put 便宜）× SG 敘事（短多長慎、已布局 put spread）三條獨立證據鏈方向一致：**近月維持偏多、但已在為 OPEX 後的轉折點買保險**。

---

## 3. 持倉對照（SSOT＝`brokerage_log/14-08-2026-brokerage.xlsx.log`）

| 項目 | 值 |
|---|---|
| QQQ 現股 | 116 股，MV $83,988.64（UPL +$5,020.48） |
| QQQ 選擇權 | Jan15'27 **720C×2**（MV $9,954.89，UPL +$1,310，DTE 155，ITM +0.6%）<br>Jan15'27 **725C×2**（MV $9,373.83，UPL +$856，DTE 155，近 ATM −0.1%） |
| MNQ 期貨 | Sep'26×5，notional $298,590（UPL +$14,390；margin 計，不入 NAV） |
| **NAV** | **$643,405.08** |
| rr3 gross_leverage | **2.25x**〈過度槓桿警示〉 |
| **rr4/rr4b/rr4t index/sector/總避險** | **0.00% / 0.00% / 0.00%** |
| rr6 β-weighted | 282.43% |
| rr6-2 QQQ Δ等效股數 | 760 股（116 現股＋231 optΔ＋412 futΔ）＝ **$550,110＝85.50% NAV**，×stock 6.55x |
| rr8 QQQ 原始集中度 | $103,317.36（**16.06%**） |
| rr8b QQQ 方向性曝險（不含期貨） | +$251,519.93（**+39.09%**） |
| rr8c 含期貨 | MNQ_FUT +46.41%／QQQ +39.09% |

> 依 [[feedback_low_hedge_may_be_deliberate_ask_first]]：rr4=0% 不標紅、不主動提問，預設為計畫內。本卡沿用此原則，只陳述現況與既有提案的對照（§4）。

---

## 4. 結論與行動

1. **結構**：區間盤整、非趨勢環境；729–735 有 pin 磁吸；PW $660 遲未跟進上移，真空區未收窄。08-14 收盤 $731.07 初步確認守住 CW $730（[[14-08-2026_QQQ_strategy]] 待辦 T-A），但 15-08 scan 綜合裁決轉「多層矛盾」，不宜視為趨勢突破確認。
2. **機構**：槓鈴倉（遠端 LEAPS 凸性＋近端 collar 保險）持穩，FP 顯示 08-13 session 仍在**加碼**遠期深 OTM call（非平倉、非賣出增益倉），與 SG 官方「短多、已備 OPEX 後避險」的敘事同向。
3. **Vol**：本輪最強訊號——IVR 續探低、SkewR 續處極值、VRP 續負，QQQ IV<RV 為 SG 自家原文標注的罕見背離，是買保護（尤其 put 端）的有利定價窗口。
4. **我方缺口不變**：rr4=0%、gross leverage 2.25x〈過度槓桿警示〉、rr6-2 等效曝險已達 NAV 85.50%。[[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]] 提出的 QQQ BePS 715P/660P（約 6 口，≈$4,680）**仍是唯一具體待裁決動作**——本卡確認的便宜 vol 環境（IVR低/VRP負/SkewR極值）正是執行該提案的有利定價背景，但本卡不新增獨立 sizing 主張，執行細節以該卡為準。
5. **V2 觸發門檻（DR>1.5，[[13-08-2026_QQQ_tracking]]）**：續盯，尚未觸發，不必動作。

---

## 5. 待辦 / 續盯

- [ ] 週一 08-17 盤後重查 LEAPS 階梯 OI（§1.4 六檔基準），確認是否有第三批加碼
- [ ] 週一確認新一份 FP 是否為非 08-13 重複的真實新 session
- [ ] CW $730/$735 站穩延續性；15-08 scan「多層矛盾」裁決下週一是否解消或惡化
- [ ] monthly 09-18 800C（§2.2）OI 是否續增，判斷是否為新一輪右尾建倉前哨
- [ ] PW $660 是否終於上移（對應 [[13-08-2026_QQQ_tracking]] H2 門檻 PW≥690）
- [ ] [[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]] 執行狀態追蹤——若下單，回頭更新 rr4
- [ ] DR 是否推過 1.5（[[13-08-2026_QQQ_tracking]] V2）

---

## 6. 關聯

[[14-08-2026_QQQ_strategy]]（前一版，本卡確認其待辦 T-A 初步達成）· [[13-08-2026_QQQ_strategy]] · [[13-08-2026_QQQ_tracking]]（V1–V4 觸發表）· [[13-08-2026_QQQ_call-spread_strategy]] · [[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]]（本卡對照的避險提案）
· [[feedback_wall_levels_ssot_sg_data_table]] · [[feedback_skew_rank_direction_high_means_call_expensive]] · [[feedback_fp_spread_label_leg_check]] · [[feedback_fp_log_dedup_by_session_date]] · [[feedback_us_close_price_only_after_0400_tpe]] · [[feedback_low_hedge_may_be_deliberate_ask_first]] · [[feedback_holdings_ssot_brokerage_log]] · [[feedback_data_source_priority]]
