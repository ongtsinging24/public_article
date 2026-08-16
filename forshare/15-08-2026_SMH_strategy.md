# SMH 策略卡 — 2026-08-15（TREND2 → TREND，跨日更新版）

**建卡時點**：2026-08-15 23:36 台北（＝ 2026-08-14 11:36 ET，**美股盤中**，收盤未確認）
**觸發**：`TREND2 SMH` → `TREND SMH` → `SAVEST`
**現價**：SMH **$587.82**（2026-08-14 盤中；前收 08-13 **$590.45**，日內 $581.87–$590.33）

**與既有卡的關係**：本卡**承接** [[13-08-2026_SMH_strategy]]（S1–S6 觸發表、水位總表、載體診斷全部沿用不重編），是輕量跨日更新，非重跑全流程。
**本次未重查**（沿用 13-08 卡數值，未過期化）：Sep-18 635C OI（S4）、Oct-16 450P/500P OI（S5）、ARK 現貨足跡、FP `session_date` 去重多日掃描、BuCS/PuDS 跨到期結構。
**姊妹卡（同日，board 層視角）**：[[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]]（已從持倉層指出 rr4b=0% 避險缺口，本卡從標的結構層補充「為何現在補、補在哪個天期」）

---

## 縮寫對照

| 縮寫 | 全稱 |
|:---|:---|
| PW / CW / HW | Put Wall／Call Wall／Hedge Wall |
| SkR | Skew Rank（自身歷史百分位，高＝call **相對** put 變貴，[[feedback_skew_rank_direction_high_means_call_expensive]]） |
| IVR / GarchR | IV Rank／Garch Rank |
| DR / GR | Delta Ratio／Gamma Ratio（synth 口徑） |
| GN | Gamma Notional（ATM 切片） |
| ADX | Average Directional Index（趨勢強度，<20 為區間） |
| rr4 / rr4b | index_hedge_pct／sector_hedge_pct（我方持倉報表欄位） |
| NAV | 淨資產 |

---

## 一、TREND2 跨日框架（ROMA scan_result 14-08 vs 15-08，僅 2 份可比）

| 指標 | 8/12（結構日） | **8/13（結構日，最新）** |
|:---|---:|---:|
| 收盤價 | 584.83 | 588.75 |
| PW / CW（V4） | 500 / 600 | 500 / 600（不變） |
| DR | 0.435 | 0.713（↑+64%） |
| GR | 0.682 | 0.428 |
| ATM Gamma Notional | −7M$ | **−118M$**（負向大幅擴大） |
| 綜合評分 | +9/22 強勢多頭 | **+4/22**（動能轉弱） |
| 裁決 | 多層矛盾，暫緩進場 | 多層矛盾，暫緩進場（不變） |

- **data_table 持續凍結在 8/11**（兩份卡皆同）；已用 08-15 檔的 `history_v4`/`synth_oi` 原始 CSV 二次確認，SG 結構資料實際最新僅到 **8/13**，非 ROMA 誤判。
- **水位分歧警示（8/13 新增）**：synth LVP $415 vs V4 PW $500，分歧 17.0% → 已觸發雙止損/降權，8/13 水位判讀可信度較低。
- **8/12→8/13 動能轉弱**：評分 +9→+4，GR 0.68→0.43（call gamma 佔比降），Gamma Notional 負向擴大一個量級 → dealer 對沖壓力上升，非單純盤整。
- Layer 0 估值連續兩天 fair_high（8/5 舊基準，目標 $539，現價高於目標 +9%，R:R 0.62–0.63）。
- **Skew Rank 進一步走高**：history_v4 08-15 檔（as-of 8/13）讀值 **0.984**，較 13-08 卡記錄的 0.936 更極端，方向不變（call 相對 put 更貴，仍是絕對 put-skewed，見 13-08 卡 §2.5）。

---

## 二、TREND 即時交叉驗證

**1. yfinance 全鏈現查（OI 落在 8/14 結算，Aug-21 為近月 OPEX）**

| Exp | Call 最大 OI | Put 最大 OI |
|:---|:---|:---|
| 8/21（OPEX） | $600 strike, OI 16,217 | $450 OI 47,940 ／ $475 OI 40,989 ／ $500 OI 25,112 |
| 8/28 | $620 OI 3,595 | $500 OI 5,052 |

- ✅ **CW $600 再次交叉驗證通過**：8/21 OPEX call 最大倉仍在 $600（16,217 口，較 13-08 卡記錄的 16,645 略降，符合近到期倉位自然衰減）。
- 近月（8/21）put 結構比 V4 標示的 PW $500 更下沉、更集中在 $450/$475 ⇒ 呼應 §1 的「水位分歧」，這批是 OPEX 前的深 OTM 保護倉，不是近端支撐。
- ⚠️ 本次**未重查** Sep-18/Oct-16 遠月倉位（S4/S5 對應的 BuCS 天花板、Oct 崩盤險），這兩個觸發條件狀態沿用 13-08 卡舊值。

**2. FlowPatrol（8/13–8/14，未做 `session_date` 去重，僅原始檔名日期）**
- 8/13：575P(8/14到期) BUY greek g$24.72M；400P dir 不可判（噪音）。
- 8/14：575P(8/14到期) SELL(greek)、620C(8/28到期) BUY(greek) 但帶 ⚠bto/sto 反向標籤（依優先序信 greek 不信文字標籤）。
- SMH 本身量能遠小於同期 TSM/NVDA/AVGO，近兩日 FP 訊號零散不成型態，非近日機構焦點名。

**3. 宏觀催化劑（founders_digest 8/13–8/14，SMH 未被點名，但半導體板塊時間軸明確）**
- **NVDA 財報 8/26**、Jackson Hole 8/27–29 是未來兩週最大催化劑；SG 已表態這是「重度避險事件」，並計畫加碼 VIX call。
- SG 觀點：短天期 IV 目前處於罕見便宜水位（QQQ IV<RV），預期 OPEX(8/21) 後 vol 回升、上行修正——與 ROMA `/vol`（VRP −9.4pt，RV>IV，偏買方）方向一致。

**4. 持倉對照（brokerage_log SSOT，14-08-2026）**
- SMH Jan15'27 580 Call ×2｜MV **$13,738.59**｜UPL **−$11,110**（較 13-08 卡的 −$9,910 加深，因現價從 592.59 回落至 587.82）
- Delta-weighted 曝險 **$69,011（+10.73% NAV）**
- **rr4b 板塊避險比 = 0.00%**（不變，SMH/SOXX 無獨立 put 保護；同日 BEPS-HEDGE 卡已就此展開專案分析）

---

## 三、S1–S6 觸發表更新（代號沿用 [[13-08-2026_SMH_strategy]] §四，不重編）

| # | 觸發條件 | 13-08 卡數值 | **15-08 更新值** | 狀態 |
|:---|:---|---:|---:|:---:|
| S1 | 站上 $600 並連 2 日收在其上 | 592.59（距 −1.24%） | **587.82（距 −2.03%，退回）** | ☐ 更遠 |
| S2 | 跌破 HW $570 且收在其下 | 592.59（距 +3.96%） | 587.82（距 +3.1%，未重查 HW 是否仍 570） | ☐ |
| S3 | 跌破 PW $500 | 距 −15.6% | 距 −14.9% | ☐ |
| S4 | Sep-18 635C OI ≥ 8,000 | 4,630 | 未重查 | ☐ |
| S5 | Oct-16 450P/500P OI 塌陷 >30% | 11,640 / 6,540 | 未重查 | ☐ |
| S6 | SkR 跌回 <0.60 | 0.936 | **0.984（更極端）** | ☐ 更遠 |

**本次更新小結**：價格從 592.59 回落到 587.82，S1（突破 $600）距離拉遠，S6（call 擁擠退潮）也更極端——兩者同向指出**「等表態」的局面沒有改變，反而更明確**：8/12→8/13 的動能轉弱（§一）與價格回落一致，不是雜訊。

---

## 四、結論與行動（沿用 13-08 卡框架，不重新裁決）

- **13-08 卡的核心判讀維持不變**：$600 仍是唯一二元判定，方向對但兩張深水 call 的載體問題（裸多 vs 機構的封頂 spread）沒有新資訊改變。
- 本次唯一**新增**的可執行點：SkR 走到 0.984（新高）疊加 NVDA 財報倒數（8/26），是 13-08 卡 §5.3「補板塊保護、現在是這個月最便宜時點」論點的**再確認**，非新論點。是否動作仍需 user 依當初 SMH/SOXX 建倉的目標價裁決（[[feedback_no_flip_without_entry_context]]）。
- 待辦沿用 13-08 卡 §待辦，不重複列出。

---

## [[關聯]]

[[13-08-2026_SMH_strategy]]（本卡承接的完整版，含 S1–S6 全表/水位總表/載體診斷）· [[15-08-2026_BEPS-HEDGE_QQQ-SMH_strategy]]（同日姊妹卡，持倉層避險缺口）· [[13-08-2026_SMH_tracking]] · [[feedback_wall_levels_ssot_sg_data_table]] · [[feedback_us_close_price_only_after_0400_tpe]] · [[feedback_holdings_ssot_brokerage_log]] · [[feedback_skew_rank_direction_high_means_call_expensive]] · [[feedback_no_flip_without_entry_context]] · [[feedback_low_hedge_may_be_deliberate_ask_first]]
