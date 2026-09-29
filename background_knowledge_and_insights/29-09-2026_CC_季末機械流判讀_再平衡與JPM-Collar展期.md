# 季末兩件機械流事件怎麼讀 —— 60/40 再平衡看股債漂移、JPM Collar 看「新一季」而非到期那組；兩者都是 SPX 層、都不給可交易方向

> **觸發**：[[28-09-2026_SOXX_strategy]] S_3_5 / S_6_1 把「季末再平衡」「JPM Collar roll」列為 9/30 催化（源：FN 09-25 PM `log_gen_by_roma/founders_digest/25-09-2026_founders_PM.md:46`），2026-09-29 對話追問這兩件事對部位的意義。
> **性質**：方法論（evergreen）＋ 2026Q3 當期數字（時效，標 as-of）。**無統計實驗**，量化部分僅為機械估算，不含任何勝率宣稱。

## S_0｜縮寫對照

| 縮寫 | 全稱 |
|---|---|
| JHEQX | JPMorgan Hedged Equity Fund（JPM Collar 的持有者） |
| QTD | Quarter-to-date（本季至今） |
| MOC | Market-on-Close（收盤集合競價單） |
| EFP | Exchange-for-Physical（期貨換現貨交叉） |
| VT / ZG | Vol Trigger / Zero Gamma |
| HIRO / FP | SG 即時對沖流 / FlowPatrol |
| OPEX | 選擇權到期日（季度＝3/6/9/12 月第三個週五） |

---

## S_1｜一句話

**兩件事都是 SPX 層的機械流，事前知道「會發生」但不知道「淨方向」**；對個股/板塊部位，它們只會讓季末最後一天收盤更吵，**不構成單獨加減保護的理由**。真正該看的是：(1) 再平衡的**方向與規模**用股債 QTD 漂移算得出來；(2) JPM Collar 的**即將到期那組**通常已遠離價平、gamma 很小，**有意義的是新一季那組**的履約價，要等 roll 後用 SG keyLevels 確認。

---

## S_2｜三個「季末」不是同一天（最容易混的地方）

| 事件 | 日期規則 | 2026Q3 | 誰在動 |
|---|---|---|---|
| 季度 OPEX（三巫） | 季末月**第三個週五** | 09-18 | 全市場到期；dealer gamma 鬆綁 |
| 退休金 60/40 再平衡 | **季末最後交易日**前後（常提前數日分批） | 09-30（三） | 平衡型基金／退休金 |
| JPM Collar 展期 | **季末最後交易日** | 09-30（三） | JHEQX 一檔，SPX 選擇權 |

- ⚠️ **ROMA 的「季末」是第一種**：`relative_bottom.py:211` 呼叫 `days_to_next_quarterly_opex()`（`relative_bottom.py:59` 引自 `opex_calendar.py`），`relative_bottom.py:311` 的「季末到期釋壓窗」指的是**季度 OPEX**，**不是**後兩者。讀 scan 時看到「季末窗」別當成再平衡或 collar 窗。
- ROMA 對後兩者**零覆蓋**：`romasys/src` grep `JPM|JHEQX|hedged.equity` 無命中（2026-09-29 現查）；`collar` 只出現在 FP 通用包裹單辨識（`profit_protect_fp.py:23-40,71`、`flowpatrol/unusual.py:15`）與 FN 關鍵字表（`founders_signals.py:418`）。

---

## S_3｜60/40 季末再平衡：方向用漂移算，別憑印象

### S_3_1｜算法

股票權重 `w = 0.6(1+r_eq) / [0.6(1+r_eq) + 0.4(1+r_bd)]`；`w > 0.6` ⇒ 季末賣股買債，反之買股。
- 股 = SPX，**債 = AGG**（綜合債）。TLT 天期太長，只列參考，拿它當債腳會把漂移高估一倍以上。
- 腳本：`py_dir/quarter_end_rebalance_gauge.py`（基準日自動取上季最後交易日）。

### S_3_2｜2026Q3 讀數（as-of 2026-09-28 美東收盤）

| 資產 | 06-30 | 09-28 | QTD |
|---|---|---|---|
| SPX | 7,499.36 | 7,683.69 | **+2.46%** |
| AGG | 97.97 | 94.65 | -3.39% |
| NDX | 30,276.35 | 30,276.81 | 0.00% |
| SOXX | 640.34 | 560.79 | **-12.42%** |
| TLT | 85.43 | 78.62 | -7.97% |

⇒ 股票權重漂到 **61.40%**，季末**賣股買債 1.40pp 組合（≈股票部位 2.28%）**，中等規模。

### S_3_3｜三條判讀規則

1. **資產類別層，不下到板塊**：60/40 賣的是「股票」整包；某板塊 QTD 大跌（如 SOXX -12%）時，對**按板塊權重再平衡**的產品反而是買回方。⇒ 不可推「季末會壓某板塊」。
2. **提前執行**：流量常在季末前幾天分批，最後一天未必最重；事後把某日下跌歸因給再平衡前，先查當日有沒有更直接的解釋（2026-09-28 SG PM 歸因是殖利率跳升＋SPX -$12B 0DTE put 戰術性買盤，`28-09-2026_founders_PM.md` PM Note 段）。
3. **債腳的外溢別當方向訊號**：買債 ⇒ 殖利率下行 ⇒「利好成長股」這條推論，受 [[project_rate_beta_regime_no_forward_power]]（殖利率是同日溫度計）與 [[project_semi_rate_hedge_is_beta_double_buy]] 雙重限制。

### S_3_4｜季節統計的地位

[[23-06-2026_seasonal-rebalance_strategy]]（`ls_strategy/june-2026/`）引用「7 月上半 SPX 上漲 ~69%」等外部統計，**我方未做條件對照組驗證**（[[feedback_hitrate_needs_conditional_baseline]]），在驗證前只可當背景，不可當論據。

---

## S_4｜JPM Collar：到期那組通常是死的，新一季那組才是 Q 結構

### S_4_1｜機制（官方 edu 出處）

- 結構：JHEQX 每季末建**零成本 collar**：賣約 +3~5% 價外 call → 買約 -5% put → 賣約 -20% put（`digest_SpotGamma_member-qa-2022-12-29-jpm-collar-vt-vs-zg.md` 二節；`digest_SpotGamma_best-options-data-strategy.md:130-152`）。
- dealer 是對手方 ⇒ collar 履約價是**整季都在、可數的真 gamma**；對比 0DTE 撐盤不可依靠（`digest_SpotGamma_0dte-mechanics.md:30,37`）。
- 遠月／已穿價的大部位 gamma 小，不構成當下對沖壓力（[[kb_wall-tenor-flow-vs-standing-oi]] :33）。

### S_4_2｜展期當天：知道會發生、沒有 edge

- 以 broker print ＋ EFP／MOC 完成，收盤出數十億美元印單，但**淨方向事前難判**：Brent 原話 *"you can appreciate what is about to happen in the market without having a tradable edge"*（member-qa digest 二節）。
- 全市場都知道它在那 ⇒ 對手方**有動機不在預期時點行動**（`digest_SpotGamma_fixed-strike-vol-is-your-real-risk-miax.md:100-101`）。
- **HIRO 排除大 cross、FP 會收** ⇒ 展期日前後兩者結構性分歧，不是任一邊錯（`digest_SpotGamma_hiro-bloomberg-crosses-excluded-sp-complex-alerts.md:63,69`）。展期日次日讀 FP 時，SPX 大額 C/P 包裹單先當 collar 候選，再照 [[kb_fp-spread-label-vs-greek-sign]] 逐腳覆核。
- SG 在展期前後會**人工 discount 模型讀數**（member-qa digest 一節末）⇒ 這段時間 VT/ZG 降權。

### S_4_3｜兩步判讀法

1. **到期那組**：算三腳距現價 %。若 call/put 都在 ±2% 以外且剩 ≤2 天，到期當下無 pin／無壓制，**不用管**。
2. **新一季那組**：roll 當天收盤推估三腳位置，**次日用 SG keyLevels 覆核**後才寫進任何觸發表；推估數字不得直接當水位（[[feedback_wall_levels_ssot_sg_data_table]]）。

### S_4_4｜2026Q3 讀數（時效；履約價為社群推估，**未經 SG 驗證**）

| 腳 | 到期組（06-30 建） | 距 09-28 收 7,684 | 新一季推估（ref 7,684） |
|---|---|---|---|
| 賣 call | ~7,890 | +2.7% | ~8,083 |
| 買 put | ~7,090 | -7.7% | ~7,261 |
| 賣 put | ~5,990 | -22% | ~6,139 |

- 到期組推估與 06-30 收 7,499 × (+5.2% / -5.5% / -20.1%) 自洽，但只有單一社群來源（見 S_8）。
- 依 S_4_3 第 1 步：到期組兩腳都在 ±2% 外、剩 2 天 ⇒ **09-30 到期本身無作用**；Q4 結構待 10-01 keyLevels。

---

## S_5｜落到部位決策上

1. **季末同日疊事件時，把「機械流」與「基本面催化」拆開**。2026-09-30 疊了季末再平衡＋collar 展期＋PCE＋MU ER（AMC）；對 semis 部位真正的尾部是 **MU ER**，前兩者只加收盤噪音。
2. **事件溢價通常已被定價**：SG 09-25 Forward IV 14.9% vs 期限結構 11.3%（差 3.6 vol pt）；09-28 SPX 本週到期 IV 再 +2~3 pt。⇒ 季末前買保護是在買被墊高的 vol；要不要買取決於**要保的那個基本面事件**，不是季末本身。
3. **ZG 附近的季末收盤**：MOC 大單可能把 SPX 機械性推過 ZG（2026-09-28：7,684 vs ZG 7,640，+0.6%）。這類穿越屬機械性，**不單獨觸發加保護**；配合 [[feedback_risk_pivot_is_vol_gate_not_direction]]：若真觸發，也是買凸性不是做空。

---

## S_6｜待辦

1. ☐ **SAVETODO 候選**：ROMA 事件日曆加「季末最後交易日」項（collar 展期＋再平衡），與現行 `opex_calendar.py` 的季度 OPEX 分開；展期日前後在 scan 的 VT/ZG 段附「SG 會人工 discount」提示。
2. ☐ **10-01**：用 SG keyLevels 覆核 Q4 collar 三腳，回填 S_4_4。
3. ☐ **可做的事件研究**（尚未做）：季末最後交易日 ±3 日 SPX 報酬，依 60/40 漂移方向分組；必附同長度非季末窗對照組與前窗（[[feedback_event_study_needs_pre_window]]），分母 n≈每年 4 個，樣本小，先估 CI 寬度再決定值不值得。

---

## S_7｜附錄

- 腳本：`py_dir/quarter_end_rebalance_gauge.py`（`--q-start` 指定基準日、`--ref` 指定推 collar 用的 SPX 收盤）
- 現查碼位（2026-09-29）：`romasys/src/opportunities/sg_signals/relative_bottom.py:59,211,311`、`opex_calendar.py`、`profit_protect_fp.py:23-40,71`、`flowpatrol/unusual.py:15`、`founders_signals.py:418`

## S_8｜證偽點與來源

1. collar 履約價只有單一社群推估：[Julie Wade on X](https://x.com/julie_wade/status/2087881359670862057)；機制參考 [SpotGamma — JPM Collar explained](https://spotgamma.com/jpm-collar-explained/)、[SG Support — JPM Collar](https://support.spotgamma.com/hc/en-us/articles/12763513348243-JPM-Collar)（support 層未逐字核對，依 [[reference_sg_official_docs_in_support_center]] 應補讀）。
2. 60/40 是簡化模型：真實退休金有容忍帶（未超帶不動）、目標日期基金權重不同、也有月末再平衡 ⇒ 規模可能高估或低估，方向較穩。
3. 「到期組無作用」只在距價平夠遠時成立；若季末前 SPX 貼近 call 腳，會變成 pin／上限，規則要反過來。

## 關聯

[[28-09-2026_SOXX_strategy]]、[[28-09-2026_TRENDFN]]、[[23-06-2026_seasonal-rebalance_strategy]]、[[21-04-2026_CC_對沖覆蓋率診斷與Collar方案]]、[[kb_wall-tenor-flow-vs-standing-oi]]、[[kb_fp-spread-label-vs-greek-sign]]、[[feedback_wall_levels_ssot_sg_data_table]]、[[feedback_hitrate_needs_conditional_baseline]]、[[feedback_event_study_needs_pre_window]]、[[project_rate_beta_regime_no_forward_power]]、[[project_semi_rate_hedge_is_beta_double_buy]]、[[feedback_risk_pivot_is_vol_gate_not_direction]]、[[reference_sg_official_docs_in_support_center]]
