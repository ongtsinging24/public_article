# FP 大額 BuCS 與「高 call skew ＋ 低 IVR」的前瞻力檢定 —— 兩者皆未檢出

> 2026-09-18 ｜ 起於 META 8/18 起漲（+24.1%）的復盤：「事先有何端倪？」
> 結論先講：**兩個候選端倪擴到全市場後都未檢出前瞻超額。META 那兩筆漂亮的大單是事後挑選的倖存者。**

⚠️ **本篇對本人 2026-09-18 對話中的階段性說法提出自我證偽**：
當時只看到 META 的 2 筆（08-17 BuCS 595/665、09-08 BuCS 650/750，兩次都在跳動前 1 個 session），
寫成「這是本題唯一真正具備前瞻性的東西」。擴樣本到 n=65 後，**對正確對照組的點估計轉負、且全部 CI 跨零**。
⇒ 保留紀錄，作為 [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] 的**第四個活例**。

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| FP | FlowPatrol（SG 每日大單報告；`d$/g$/v$` ＝**買方側**） |
| DT | data_table（SG 每日結構化表） |
| **BuCS** | **Bull Call Spread**（看多／Debit；四字母制見 `.claude/option_term_conventions.md`） |
| BeCS | Bear Call Spread（看空／Credit） |
| IVR / SkewR | IV Rank ／ Skew Rank（**高＝call 貴**） |
| LEAP | 長天期選擇權（此處指 2027–2028 到期） |
| CW / PW | Call Wall ／ Put Wall |
| CI | 信賴區間（本篇一律 bootstrap 95%） |
| pp | percentage point |

---

## 一、理論框架：為什麼會覺得這兩個是「端倪」

**候選 A｜FP 大額 BuCS 領先 1 個 session。**
直覺：BuCS 是**有方向、有到期日、有履約價、需付出淨權利金**的下注。
不像裸買 call 可能是避險或換腿，BuCS 幾乎只能解讀為「我認為到 X 日之前會漲到 K1 以上」。
若機構在資訊上領先，這種單應該印在行情之前。

**候選 B｜「高 call skew ＋ 低 IVR」。**
直覺：SkewR 高＝市場仍願意為右尾付溢價；IVR 低＝整體選擇權絕對成本便宜。
兩者同時成立 ＝「右尾被看好、但買它很便宜」。
META 谷底附近正是這個組合（2026-08-19 檔：SkewR 0.896、IVR 0.3064，
而股價已自 7/16 高點 675.61 回落至 543.67，**跌 19.5% 而 SkewR 全程沒垮**）。

**兩者共同的陷阱**：都是先看到結果、再回頭找特徵。
必須用**同條件對照組**檢定，且**兩個軸的對照組都要跑**（見下）。

---

## 二、實驗設計

### 共同口徑

| 項目 | 做法 | 依據 |
|---|---|---|
| FP 去重 | 以 `session_date` 取最新 publish 檔（110 檔 → 105 session） | [[feedback_fp_log_dedup_by_session_date]] |
| DT 去重 | 以 SPY 的 `Previous Close` 當 session 指紋（111 檔 → 75 session） | [[reference_date_aliasing_inflates_backtest_n]]、[[reference_sg_levels_as_of_trade_date_not_filename]] |
| 腿位判定 | **自己重算**：同 `spread=` id、同到期、兩腿皆 call、買低賣高才算 BuCS | [[feedback_fp_spread_label_leg_check]]、[[feedback_option_spread_rule1]] |
| 方向判定 | greek 優先序 `g$ > v$ > d$ > prem`，**不讀 bto/sto** | [[feedback_fp_greek_is_buyside_btosto_unreliable]] |
| ETF 剔除 | 以 FP 的 `sector=` 欄含 "ETF" 為準（硬名單只當雙保險） | 實測 EWY `sector=Non-US ETF` 會漏過硬名單 |
| 觸發率 | **先算再談 edge** | [[feedback_check_signal_fire_rate_before_edge]] |
| 對照組 | **兩組都跑**（見下），禁用 50% 當隨機基準 | [[feedback_hitrate_needs_conditional_baseline]] |

### 候選 A 的兩個對照組（關鍵設計）

- **對照 A｜擇時軸**：*同一批標的、同一批 session 的所有格子，扣掉訊號格*。
  回答「**這一天** vs 這檔股票的**其他天**」——這才是「訊號有沒有擇時力」的正確問法。
- **對照 B｜選標的軸**：*同一批 session、FP 全宇宙的其他標的*。
  回答「**這檔** vs 當天**其他檔**」。

🔴 **兩組符號會相反，這正是本實驗最重要的方法論產出**（見結果表）。

### 候選 B 的去漂移

forward 報酬一律**減掉同日全市場中位數**，否則量到的是大盤 beta 而非選股力。
有效樣本以「**獨立日**」計（54 日），不是以 sym×day 格子數（25 萬）計。
四個互斥子集另做加總驗算 `n(A)+n(B)+n(C)+n(D) ≡ 母體`（[[feedback_decluster_before_splitting_complementary_subsets]]）。

### ROMA 對照（現查行號，2026-09-18）

- FP 方向判決優先序定義：`romasys/src/opportunities/sg_loaders/flowpatrol.py:108`、`:241`
- `spread_id` **只採信存在性、不採信內容**：同檔 `:325`–`:328`
- log 的 `session_date` 輸出（資料真實場次 ＝ publish 前一交易日）：
  `romasys/src/opportunities/sg_loaders/flowpatrol_dump.py:297`–`:298`

---

## 三、結果

### 候選 A：FP 大額 BuCS（樣本 2026-04-17 ~ 2026-09-17，105 session）

抽出 **65 筆** BuCS，涉及 **26 檔個股**。母體 sym×session ≈ 18,165 格
⇒ **觸發率 0.358%**。

> 🔴 **觸發率 0.358% 本身就是結論的一部分**：依 [[feedback_check_signal_fire_rate_before_edge]]，
> <2% 的觸發率在統計上幾乎不可能測到 edge。**n 不足是結構性的，不是這次樣本剛好太短。**

| 窗口 | 規模門檻 `|d$|` | n | 訊號中位 | 勝率 | 對 A 超額 | **對 A 超額 95% CI** | 對 B 超額 |
|---|---|---|---|---|---|---|---|
| T+1 | ≥ $0M | 65 | +0.29% | 52.3% | **+0.29pp** | **[−1.09, +0.58]** 跨零 | +0.51pp |
| T+1 | ≥ $50M | 35 | −0.03% | 48.6% | −0.02pp | [−1.06, +0.65] 跨零 | +0.26pp |
| T+1 | ≥ $150M | 16 | −0.05% | **37.5%** | −0.01pp | [−1.54, +0.45] 跨零 | +0.32pp |
| T+5 | ≥ $0M | 56 | +0.15% | 53.6% | −0.17pp | [−1.56, +1.77] 跨零 | +0.85pp |
| T+5 | ≥ $50M | 32 | −0.25% | 46.9% | −0.46pp | [−2.20, +0.94] 跨零 | +0.24pp |
| T+5 | ≥ $150M | 14 | **−1.17%** | 42.9% | **−1.33pp** | [−3.66, +0.26] 跨零 | −0.99pp |
| T+21 | ≥ $0M | 15 | +0.63% | 60.0% | +0.15pp | [−4.31, +6.18] 跨零 | +2.87pp |
| T+21 | ≥ $50M | 10 | −0.43% | 50.0% | +0.35pp | [−4.02, +10.11] 跨零 | +1.37pp |
| T+21 | ≥ $150M | 6 | −1.52% | 50.0% | −1.45pp | 太少 | +0.30pp |

**九格全部 CI 跨零 ⇒ 沒有任何一格檢出前瞻力。**

兩個必須點名的型態（皆為**點估計傾向、非檢出**）：

1. **規模越大，隔日越差。** `|d$|` 門檻從 $0M → $150M，T+1 勝率 52.3% → 48.6% → **37.5%**；
   T+5 對 A 超額 −0.17 → −0.46 → **−1.33pp**。與「大單＝聰明錢」的直覺**相反**。
2. **對照 A 與對照 B 符號相反。** 對 B 幾乎全正（最高 +2.87pp），對 A 幾乎全負。
   ⇒ 對 B 的正值是**選標的偏誤**：BuCS 只出現在大型權值股，而 FP 全宇宙混著一堆小型雜訊股。
   **只跑對照 B 就會得到「這個訊號很準」的相反結論。**

⚠️ 一律寫成「**未檢出**」不是「已證偽」——
CI 跨零同時排除不了正向與反向，這與 [[feedback_hiro_eod_net_not_overnight_signal]] 採同一措辭紀律。
**不得據此建反向策略。**

### 候選 B：高 call skew ＋ 低 IVR（樣本 2026-05-04 ~ 2026-09-18，75 session，H=21）

去漂移後（減同日全市場中位數）：

| 條件 | 逐筆 n | 逐筆中位超額 | 逐筆勝率 | 獨立日 n | 日勝率 |
|---|---|---|---|---|---|
| **SkewR≥0.85 且 IVR≤0.35** | 21,893 | **+0.33pp** | 52.6% | 54 | 70.4% |
| SkewR≥0.85 且 IVR>0.35 | 29,075 | +0.11pp | 50.5% | 54 | 55.6% |
| **SkewR<0.85 且 IVR≤0.35（補集）** | 88,740 | **+0.17pp** | 51.3% | 54 | **72.2%** |
| SkewR<0.85 且 IVR>0.35（補集） | 112,163 | **−0.35pp** | 48.3% | 54 | 20.4% |

驗算：四子集合計 251,871 ≡ 母體有效格子 251,871 ✅　主條件觸發率 **8.7%**。

🔴 **真正有分辨力的是 IVR 軸，不是 skew 軸。**
兩個低 IVR 組都正（+0.33 / +0.17）、兩個高 IVR 組一組近零一組負（+0.11 / −0.35）。
把 SkewR 從 <0.85 提到 ≥0.85 只多拿 **+0.16pp／月**，而**日勝率反而從 72.2% 掉到 70.4%**。

⇒ 「call skew 高」這個軸**自己幾乎不帶資訊**。這與 [[feedback_ratio_field_direction_needs_leg_split]]
是同一個教訓：**看起來是一個訊號的東西，拆軸之後發現只有一個軸在工作。**

⚠️ 樣本限制：僅 4.5 個月、單一多頭窗口，且含 **2026-08-20~08-28 四源斷檔**
（[[reference_sg_data_gap_aug2026_travel]]）⇒ H=21「session」實際跨越 > 1 個日曆月。
**不足以下永久結論，只足以說「這個篩不足以解釋 META 那一波」。**

---

## 四、順帶落地的三個結構性事實（非統計，直接查證）

**(1) META 的 CW 750 是 2027-01 的 LEAP 積木，不是近月牆。**

直接查 OI（2026-09-18）：

| 到期 | 750C OI |
|---|---|
| **2027-01-15** | **245,536（83.5%）** |
| 2026-10-16 | 14,925 |
| 2026-09-18 | 14,637 |
| 其餘合計 | ~18,900 |

DT 的 CW 從 7 月釘到 9 月都是 750，就是被這塊 LEAP 撐著。
⇒ **拿它當近月壓力／目標價會判錯。** 已沉澱為 [[project_meta_callwall_is_leap_oi]]。

**(2) META 8 月的 VRP −22.5 vol pts 是財報的機械產物。**

2026-08-01 DT：IV 0.3822 / RV 0.6075 ⇒ VRP **−0.2253**，看起來像教科書級「選擇權便宜」。
但 7/30 META 自 595.76 崩至 535.77（−10%，財報）—— **1M RV 窗口含著那根 gap，IV 卻已排除財報**。
決定性證據：**9/2 RV 突然掉到 0.2950**，正是財報日滾出 21 日窗口那天，VRP 同步翻正 +0.0482。
⇒ 看到跨財報的 IV/RV 比較，先問 **RV 窗口是否含財報日**，再談 VRP。

**(3) 5 日 DPI 觸底是同步不是領先。**
5d DPI 在 8/19 檔觸及 7–9 月序列最低 0.29344，之後單調升到 9/18 的 0.43524 ——
但它**就在底部那天觸底**，當天不帶前瞻資訊。

---

## 五、結論與行動

1. **不要用「FP 出現大額 BuCS」當進場扳機。** 未檢出前瞻力，且規模越大點估計越差。
   它仍有用 —— 當**敘事佐證**（「誰在什麼天期押什麼位置」），**不當時機訊號**。
   這與 [[project_fp_p9_extreme_greek_forward_return]]（FP 買/賣軸零預測力）同一家族。
2. **不要用「call skew 高」當看多理由。** 有用的是 **IVR 低**（保護／凸性便宜），
   那是**成本論述**不是**方向論述**。⇒ 呼應 [[feedback_skew_rank_direction_high_means_call_expensive]]。
3. **任何「某訊號很準」的宣稱，先問跑的是哪個對照組。** 本篇兩組符號相反，
   只跑一組會得到完全相反的結論。**這條要進每一次量化宣稱的檢查表。**
4. **META 復盤的真正教訓不是資料缺口，是注意力缺口。**
   `ls_strategy/` 最後一張 META 卡是 `july_2026/20-07-2026_META_strategy.md`；
   整個 8 月 FP／DT 都正常落檔，**沒有人去讀**。

---

## 六、待辦

| # | 項目 | 為什麼 |
|---|---|---|
| 1 | 樣本延到 2025 全年（含 2025 年的下跌段） | 現有 4.5 個月是單一多頭窗口，**方向性結論不可外推** |
| 2 | 把「規模越大隔日越差」單獨檢定 | 目前只是點估計傾向、CI 跨零；若成立則與 [[project_fp_p9_extreme_greek_forward_return]] 可合併成一條 |
| 3 | BuCS 的**到期天期**切軸（近月 vs LEAP） | 本篇把 exp 1 天與 exp 2027 混在一起算，天期很可能是被壓掉的那個維度 |
| 4 | 補 BeCS／BuPS 對照 | 只驗看多結構＝單邊驗證；依 [[feedback_protection_needs_reverse_control_group]] 要配反方向對照組 |
| 5 | 淨 debit 而非單腿 `|d$|` 當規模軸 | `prem` 欄只有上了 largest_premium 榜的腿才有值（中位數 0.00）⇒ 現在的規模軸是代理不是真值 |

---

## 七、附錄：腳本

| 腳本 | 用途 |
|---|---|
| `py_dir/18-09-2026_fp_dated_call_spread_lead.py` | 候選 A。`--dump` 逐筆列出 65 筆命中；含 bootstrap CI |
| `py_dir/18-09-2026_dt_skew_ivr_forward.py` | 候選 B。參數為 forward session 數（預設 21）；含四子集加總驗算 |

兩支皆 hermetic 讀本機落檔；候選 A 的價格面板快取在 `py_dir/.cache_fp_bucs_px.csv`
（避免重跑觸發 yfinance 限流，見 [[reference_yfinance_bulk_ratelimit_backoff]]）。

---

## 關聯

[[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]]・[[31-08-2026_CC_FP-p9極端greek的OOS複核]]・[[30-07-2026_CC_HIRO日終淨值非隔夜方向訊號]]・[[31-07-2026_CC_訊號覆蓋率與辨別力上限_以FN謹慎語氣為例]]
[[feedback_hitrate_needs_conditional_baseline]]・[[feedback_check_signal_fire_rate_before_edge]]・[[feedback_decluster_before_splitting_complementary_subsets]]・[[reference_date_aliasing_inflates_backtest_n]]
[[feedback_fp_greek_is_buyside_btosto_unreliable]]・[[feedback_fp_spread_label_leg_check]]・[[feedback_fp_log_dedup_by_session_date]]・[[feedback_option_spread_rule1]]
[[feedback_skew_rank_direction_high_means_call_expensive]]・[[feedback_ratio_field_direction_needs_leg_split]]・[[project_fp_p9_extreme_greek_forward_return]]・[[project_meta_callwall_is_leap_oi]]
[[reference_sg_data_gap_aug2026_travel]]・[[reference_yfinance_bulk_ratelimit_backoff]]・[[feedback_protection_needs_reverse_control_group]]・[[18-09-2026_TRENDFN]]
