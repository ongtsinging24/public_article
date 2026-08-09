# 2026-08-09 TSM 策略卡 — 機構操作深挖（3 週 V 型反彈：結構／FP 流量／總經三線索）

> **數據時間戳**
> - 現價 **$420.04**（08-07 美股收盤；抓取 2026-08-09 22:30 GMT+8，今日週日休市無新 tick）
> - SG 結構水位 `data_table`：最新解凍至 **08-07 session**（讀取 `SPX_data-table_2026-08-09.csv`，依 [[feedback_wall_levels_ssot_sg_data_table]] D-2 校正）
> - FP 最新場次 **08-07**（`flowpatrol_2026_08_07.log`）；顯著部位表 `sig_positions.csv` 最後一筆 **2026-06-29**
> - 我方持倉 SSOT = `brokerage_log/07-08-2026-brokerage-02.xlsx.log`（[[feedback_holdings_ssot_brokerage_log]]）
>
> 承接：[[14-07-2026_TSM_strategy]]（財報前方案 L collar 提案）｜本卡為 TREND 例行深挖，非新交易動作卡

## 縮寫對照
- **PW / CW / HW** = Put / Call / Hedge Wall｜**KG / KD** = Key Gamma / Key Delta Strike
- **IVR / GarchR / SkewR** = IV Rank / Garch Rank / Skew Rank
- **FP** = FlowPatrol（SG 盤後機構期權流）｜**sig_positions** = FP 顯著部位百分位表
- **rr3** = gross leverage｜**rr4t** = 總避險%｜**rr6** = β-weighted%｜**rr8c** = 定向曝險%（Δ-equiv）
- **HBM/CoWoS** = 先進封裝製程｜**DTE** = days to expiry｜**Δ/g$/v$** = delta/gamma/vega 曝險金額

---

## 一、結構面：3 週牆位/波動軌跡（SG data_table SSOT，逐日 D-2 校正）

| Trade Date | Px | PW | CW | IVR | GarchR | SkewR |
|---|---|---|---|---|---|---|
| 07/21 | 424.61 | 380 | 450 | 79.6% | 70.7% | 20.1% |
| 07/24 | 403.69 | 380 | 450 | 72.5% | 61.6% | 31.3% |
| 07/29 | 374.78 | 380 | 450 | 75.5% | 62.0% | 48.2%（底部）|
| 07/31 | 404.25 | **360** | 425 | 64.3% | 78.0% | 45.0% |
| 08/03 | 406.12 | 380 | 425 | 68.0% | 72.6% | 59.4% |
| 08/05 | 414.03 | 380 | 425 | 55.4% | 65.6% | 83.2% |
| 08/06 | 418.07 | 380 | 420 | 47.6% | 60.3% | 64.0% |
| 08/07 | 419.96 | **400** | 450 | 38.5% | 55.3% | **86.0%** |

**讀法**：3 週內完成 424→375（−11.6%）閃跌後的 V 型收復並站上前高。三訊號同步：
- **IVR/GarchR 一路下滑**（80%→38%／78%→55%）＝realized/predicted vol 雙降，市場正在為反彈定價「已經穩了」。
- **SkewR 同期暴衝**（20%→86%，14th→86th %ile）＝依 [[feedback_skew_rank_direction_high_means_call_expensive]]，call 相對 put 明顯轉貴——vol 整體降溫同時 call 被搶，是「melt-up chase」訊號組合，非避險需求。
- **PW 黏在 380 長達 3 週（07/17–08/06 全程未動），僅最新一筆 08/07 才跳到 400**——尚未過「連續兩份不同即定案」門檻，需下一筆複驗。CW 在 420–450 反覆震盪未收斂，上檔壓力位機構尚無共識。

## 二、FP 大單判讀（近 2 週僅 3 筆進 top-N；sig_positions 顯著名單 6 週掛零）

- **08/05**：SELL 425C(Sep-04) + BUY 485C(Sep-04)，兩腳 OI 幾乎相等（13,894 vs 13,904）；同日另 SELL 400C(Sep-18)。讀法：**covered-call/overwrite 展倉**，履約價隨股價從 400 附近滾到 425，非新方向性下注。
- **08/07**：SELL 500C(Dec-18)，v$=−264K，遠 OTM（+19%）。同樣讀作 LEAPS 層級 overwrite 續作。
- **FP aggregate `sig_positions.csv` 最後一筆是 2026-06-29**（delta_pct=9、gamma_pct=4、vega_pct=10，皆低分位）——**近 6 週 TSM 未觸發「顯著機構部位」門檻**。這波反彈更像分散 dealer/overwrite 調整＋盤面追價，非可指認的大戶新建倉事件。

## 三、總經敘事面（macro_narrative 08-05 合併 digest，GS+JPM+MS-TOTM）

- **⭐⭐⭐ GS「$1T 全球 AI 投資」×JPM「DRAM 缺口 10pp」交集論**：TSM 是兩條主線交叉點（HBM/CoWoS 產能受限 + AI 晶片需求主幹），支撐 [[feedback_tsm_high_conviction_hold]]。JPM 自標風險：memory 天然 cyclical，若 27 年 hyperscaler capex 失望 → 缺口敘事可能快速翻轉——**監控條件，非現在動作項**。
- **MS-TOTM Wilson「半導體見底可交易反彈」＝事後追認**：他 08-03 開口時 SOXX 已反彈 +8.6%。TSM 這輪相對強度中等偏弱：07-29→08-04 個股比較表 TSM 僅 +3.20%，落後 NVDA(+5.57%)／META(+5.61%)，也落後領漲的低品質早週期股（SNDK+17.5%／MRVL+16.5%）；月度相對表現 TSM 距 06-30 高點仍 −12.65%，跟 SOXX(−17.2%)／SMH(−13.9%) 同形狀但補得較快。

## 四、我方持倉現況（brokerage_log/07-08-2026-brokerage-02.xlsx.log）

- 現股 400 股 mv $167,640（+$18,930 UPL）＋ 5 組深 ITM/近 ITM call（400/410/400/380/400 履約，Oct'26–Jan'27 到期）；TSM 現金部位佔 NAV **39.35%**，未實現損益 **+87.09%**。
- **rr4t 總避險 = 0.00%**、rr6 β-weighted **270.72%**、rr3 gross leverage **1.21x**。
- ⚠️ **與 [[14-07-2026_TSM_strategy]] §8.5 方案 L（Aug21-420P/480C collar）對照**：目前持倉不含任何 put 或空 call 腳位，方案 L 未在庫存中留下痕跡（未執行或已平倉），**個股層下檔保護現況仍為 0**。零避險依 [[feedback_low_hedge_may_be_deliberate_ask_first]] 此前已於 08-03/08-05 兩次確認為主動決策，本卡不重新質疑，僅記錄現況供追蹤。

## 五、綜合判讀

機構操作面**沒有單一「大戶進場」事件**——FP 顯著部位表 6 週掛零，僅有兩筆大單（08/05、08/07）皆為 overwrite/展倉性質，跟隨股價而非帶頭。真正在動的是結構面：IV 全面回落＋call skew 暴衝到 86th %ile，加上 PW 剛從 380 抬到 400（僅 1 session 確認）——組合起來是「realized vol 降溫、上方追價需求推高 call 定價」的 melt-up 訊號，非避險/派發訊號。宏觀面 GS/JPM 的 AI capex+DRAM 交集論支持結構性多頭邏輯，但 Wilson「半導體反彈」論已證實為事後追認，TSM 這輪相對強度中等（跑輸最低品質早週期股）。

## 六、決策

### 6.1 立場（不變）
**核心多單不減**（[[feedback_tsm_high_conviction_hold]]）。本卡未發現新的方向性訊號或機構顯著部位事件，不構成加碼或減碼理由。

### 6.2 本卡不提出新交易動作
純 TREND 深挖；若要動保護，依 [[feedback_qqq_call_preferred_mnq_is_fallback]] 同族脈絡另立執行卡評估。

---

## 七、驗證點

- ☐ **08/07 PW=400 是否在下一筆數據延續**——目前僅 1 個 session，未過「連續兩份不同即定案」門檻
- ☐ **CW 420–450 是否收斂**——突破/跌破哪一側決定機構是否形成上檔共識
- ☐ **JPM 標的證偽條件**：27 年 hyperscaler capex 是否不如預期 → DRAM 短缺論述打折
- ☐ **rr4t 是否持續掛零**——疊加 rr6 270% 高槓桿，若要補保護需另立執行卡
- ☐ **FP sig_positions 是否重新出現 TSM**——6 週掛零，若重新出現代表機構重新形成顯著方向性部位

---

## 八、關聯

- 前卡：[[14-07-2026_TSM_strategy]]（財報前機構足跡全段＋方案 L collar 提案）
- 慣例：[[feedback_tsm_high_conviction_hold]]｜[[feedback_skew_rank_direction_high_means_call_expensive]]｜[[feedback_wall_levels_ssot_sg_data_table]]｜[[feedback_low_hedge_may_be_deliberate_ask_first]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_fp_log_dedup_by_session_date]]
