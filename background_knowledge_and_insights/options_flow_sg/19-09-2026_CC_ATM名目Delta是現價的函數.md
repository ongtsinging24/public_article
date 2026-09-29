# ATM 名目 Delta 是現價的函數，不是機構部位訊號 —— 兼論「水準判準 vs 背離判準」的分野

> **建檔**：2026-09-19 01:xx–02:xx GMT+8 ＝ **2026-09-18 13:xx ET（美股盤中，季度三巫 OPEX 當日）**
> **觸發**：跑 AMZN 的 TREND2＋TREND 時，ROMA scan 印出
> `DN=-3467M$：Put Delta 主導（機構淨空頭 Notional）`，且該值一個月內從 −801M「惡化」到 −3467M，
> 看起來像機構大舉布空 —— 但同期價格從 $284 跌到 $246。**兩者長得太像了。**
> ⚠️ 本篇**不證偽**任何既有筆記，是對 [[feedback_monotone_column_may_be_a_function_of_another]]
> 的一次實證落地 ＋ 把它的適用邊界講清楚。
> ⚠️ 本篇**確實打到一張現行追蹤卡的判準**：`ls_strategy/event_tracking/NVDA_daily_watch.md` 的 **N4**
> （已於 2026-09-19 在該卡加註）。

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| DN | ATM Delta Notional（SG synth_oi 欄位；ROMA scan 印為 `DN=...M$`） |
| DR / GR | Delta Ratio／Gamma Ratio |
| ρ | Spearman 等級相關係數 |
| CI | 信賴區間（本篇一律 bootstrap 95%，5,000 resample，seed 固定） |
| td | trading day（交易日） |
| SSOT | Single Source of Truth |
| OPEX | 選擇權到期日 |
| 水準判準 | 拿欄位的**絕對值**比固定門檻（如「DN < −3,500M 就觸發」） |
| 背離判準 | 要求欄位**與價格反向**才算數（如「價漲**且** DN 改善 ≥15%」） |

---

## CC_ALL_1909_1｜TL;DR

1. **`ATM Delta Notional` 的水準幾乎就是現價的單調變換。** 75 檔 synth_oi 宇宙，
   `Spearman(現價, DN)` median **+0.653**，**52.0%** 的標的 |ρ| > 0.7。
2. **它沒有任何隔日前瞻力，而且是全宇宙一致的沒有。**
   `Spearman(ΔDN_t, Δ現價_{t+1})` median **−0.078**、p10 −0.251、p90 +0.148 ——
   **75 檔裡沒有一檔 |ρ| > 0.7（0.0%）**。
3. ⇒ **凡是「拿 DN 的水準比固定門檻」的判準，測到的是價格自己，不是機構。**
   價格一跌，門檻自動被穿過，看起來像「機構淨空頭加深」。
4. **但「背離判準」不受影響。** 明文要求「價**漲** 且 DN 改善」的條件已經把價格軸控制掉了，
   剩下的殘差才有可能帶訊息。本篇不否定這一類。
5. **對照組不是乾淨的，這點必須講清楚**：`Delta Ratio` 的 `Spearman(現價, DR)` median 也有 **+0.579**、
   41.3% 標的 |ρ|>0.7。⇒ **「改用 DR 就安全了」是錯的**；AMZN 的 DR ρ=+0.021 只是個別特例。

---

## CC_ALL_1909_2｜理論框架：為什麼 DN 必然跟著價格走

`ATM Delta Notional` ≈ Σ(平價附近各履約價的 delta × OI × 100 × S)，且 call/put 兩側符號相反。
三個機制讓它在**機構一動都不動**的情況下隨價格變化：

| # | 機制 | 說明 |
|---|---|---|
| 1 | **Delta 本身是 S 的函數** | 同一批 OI 不變，S 下跌 ⇒ 上方 call 的 delta 往 0 收、下方 put 的 |delta| 往 1 走。淨值必然往負向移動。 |
| 2 | **「ATM 切片」的成分會隨 S 平移** | S 從 284 跌到 246，被納入「ATM 附近」的履約價整組換掉 —— 比較的是**兩組不同的合約**。 |
| 3 | **名目化乘上了 S 本身** | 末項 × S ⇒ 即使前兩項中性，讀數也會隨價格等比縮放。 |

三者都與「機構今天買了什麼」無關。所以**先驗上就該預期 ρ 高**；本篇只是把它量出來，
並且證明**扣掉價格後沒有剩下東西**。

直觀佐證（AMZN，同一批資料）：

| 日期 | 現價 | DN |
|---|---|---|
| 2026/8/5 | $272.60 | −1M |
| 2026/8/10 | **$278.08** | **+402M** |
| 2026/9/16 | $245.84 | **−3467M** |

價格漲 ⇒ DN 轉正；價格跌穿上方 call 群 ⇒ DN 翻負並放大。

**ROMA 對應碼（現查，非憑記憶）**

| 位置 | 內容 |
|---|---|
| `romasys/src/opportunities/sg_institutional/layer3.py:189` | `dom = "Put Delta 主導（機構淨空頭 Notional）" if dn_m < 0 else "Call Delta 主導（機構淨多頭 Notional）"` |
| `romasys/src/opportunities/sg_institutional/layer3.py:190` | `level_lines.append(f"  ▸ DN={dn_m:+.0f}M$：{dom}")` |
| `romasys/src/opportunities/sg_institutional/data.py:36` | `"dn": _f(r.get("ATM Delta Notional"))` |
| `romasys/src/collectors/sg_downloader/synth.py:82` | `("atm_delta_not", "ATM Delta Notional")` |

⇒ 這行只用 `dn_m` 的**正負號**下「機構淨空/淨多」的語義標籤，**沒有任何價格控制**。

---

## CC_ALL_1909_3｜實驗設計

**資料**：`spotgamma_report/auto/synth_oi/<SYM>/<SYM>_synth_oi_<date>.csv`，每檔取最新一份的全窗。
**樣本期**：**2026-08-05 ~ 2026-09-16**（AMZN n=30）。
🔴 **SG Essential 訂閱只保留最近 30 個交易日 ⇒ 全窗即上限，這是資料上限不是我方截斷**
（同 [[project_evc_discontinued_zone_from_fair]] 之後的降級後果）。**樣本期限制見 CC_ALL_1909_6。**

**四個檢定**（每檔各跑一次，再看橫斷面分布）：

| ID | 檢定 | 問的問題 |
|---|---|---|
| E1 | `Spearman(現價, DN)` | DN 的**水準**是不是價格的函數？ |
| E2 | `Spearman(現價, DR)` ← **對照組** | 高 ρ 是「DN 的毛病」還是「所有機構欄位都這樣」？ |
| E3 | `Spearman(Δ現價, ΔDN)` 同日 | 變化量層級是否也同步？ |
| E4 | `Spearman(ΔDN_t, Δ現價_{t+1})` | **這才是「是不是訊號」的真問題。** |

**對照組設計理由**（依 `alias_runbooks.md` 的 saveana 第 4 條，**禁用 50% 當隨機基準**）：
E2 取同一張表、同一批日期、同一個機構口徑的 `Delta Ratio` —— 它是**比值**不是**水準**，
若 E2 的 ρ 顯著低於 E1，就能把矛頭指向「水準欄位」這個性質，而不是泛泛地說「SG 欄位都沒用」。

**橫斷面設計理由**：單一標的 n=30 撐不起全稱結論。把 75 檔各自的 ρ 排成分布，
AMZN 的讀數才有分位可看 —— 避免拿一檔的巧合當通則（同 [[reference_date_aliasing_inflates_backtest_n]] 的警戒）。

**一個在實作中踩到的坑**：`Quote Date` 是 `YYYY/M/D` 字串，**直接 `sort_values` 是字典序** ——
`"2026/9/16"` 會被排在 `"2026/9/9"` 前面（`'1'<'9'`），差分序列整條錯位 ⇒ E3/E4 全廢。
必須先 `pd.to_datetime(..., format="%Y/%m/%d")` 再排。修正前後 AMZN 的 E4 從 −0.167 變成 −0.263
（結論不變，但**這種錯不會報錯，只會靜默給你一個看起來很合理的數字**）。

---

## CC_ALL_1909_4｜結果

### CC_ALL_1909_4_1｜橫斷面（75 檔）

| ID | 檢定 | median | p10 | p90 | \|ρ\|>0.7 佔比 |
|---|---|---|---|---|---|
| E1 | Spearman(現價, **DN**) | **+0.653** | −0.729 | +0.943 | **52.0%** |
| E2 | Spearman(現價, **DR**)（對照組） | +0.579 | −0.153 | +0.918 | 41.3% |
| E3 | 同日 Spearman(Δ現價, ΔDN) | +0.640 | −0.666 | +0.894 | 48.0% |
| **E4** | **前瞻 Spearman(ΔDN_t, Δ現價_{t+1})** | **−0.078** | **−0.251** | **+0.148** | **0.0%** |

**E4 是決定性的那一行：75 檔沒有一檔的前瞻 |ρ| 超過 0.7，p10~p90 整段橫跨 0。**

### CC_ALL_1909_4_2｜AMZN 個案（n=30）

| 檢定 | ρ | bootstrap 95% CI | 同儕分位 |
|---|---|---|---|
| E1 現價 vs DN | **+0.899** | **[+0.722, +0.973]** | 第 **76%** 分位 |
| E2 現價 vs DR | +0.021 | — | （個別特例，見下） |
| E3 同日 | +0.677 | — | — |
| **E4 前瞻** | **−0.263** | **[−0.556, +0.095]（含 0）** | — |

### CC_ALL_1909_4_3｜🔴 一個反直覺的結果：對照組沒有比較乾淨

我原本的假設是「DR 是比值，應該不受價格污染」。**橫斷面把它否掉了**：
E2 median +0.579、41.3% 標的 |ρ|>0.7，只比 E1 低一點。

⇒ **不能寫「改用 DR 就安全」。** AMZN 的 DR ρ=+0.021 是它自己的特例，不是 DR 這個欄位的性質。
真正的分野不在「哪個欄位」，而在 **CC_ALL_1909_5 的水準判準 vs 背離判準**。

---

## CC_ALL_1909_5｜結論與行動：水準判準 vs 背離判準

**這不是「SG 欄位沒用」，是「同一個欄位，兩種用法，一種必錯一種可用」。**

| 判準型 | 形狀 | 有沒有控制價格 | 判定 |
|---|---|---|---|
| **水準判準** | 「DN < −3,500M 就觸發」 | ❌ 沒有 | 🔴 **必錯** —— 價格一跌就自動觸發 |
| **背離判準** | 「**價漲** 且 DN 改善 ≥15%」 | ✅ 有（明文要求價格方向） | 🟢 **可用** —— 測的是殘差 |
| **同日歸因** | 「今天 DN 惡化，因為今天跌了」 | n/a | 🟡 **可用但無資訊** —— 這是溫度計不是訊號 |

**實例對照（本庫現行的兩張追蹤卡，剛好一個各站一邊）**：

| 卡 | 判準 | 原文 | 判定 |
|---|---|---|---|
| `NVDA_daily_watch.md` | **N4** | 「ATM Delta Notional 突破 −3,500M 門檻」 | 🔴 **水準判準，已失效** |
| `AVGO_daily_watch.md` | **T6** | 「DN 背離逆轉（**價漲**且 DN 改善 ≥15%）」 | 🟢 **背離判準，不受影響** |

NVDA 卡在 08-05 自己寫過「疑為崩盤機械效應待驗」——**本篇的答案是：對，就是機械效應。**
已於 2026-09-19 在該卡加註（`ls_strategy/event_tracking/NVDA_daily_watch.md` 頭部）。

### CC_ALL_1909_5_1｜可直接套用的三條操作規則

1. **看到任何「機構水準欄位 + 固定門檻」的判準，先跑 `Spearman(現價, 該欄)`。**
   ρ > 0.7 就當它是價格的替身，**不要用它的水準做判斷**。
2. **要用它，就把價格控制掉**：改成背離式（要求與價格反向）、或對價格回歸取殘差。
3. **報告「惡化/改善」時一律附同期價格變動。** 只寫「DN 從 −801M 惡化到 −3467M」而不寫
   「同期價格 $284 → $246」，等於把價格變動包裝成機構行為。

---

## CC_ALL_1909_6｜待辦與本篇的弱點

| # | 項目 | 為什麼 |
|---|---|---|
| W1 | **樣本期只有 30td（2026-08-05 ~ 09-16），且落在單一區間震盪 regime** | SG Essential 保留上限。橫斷面 75 檔提供了寬度但**沒有提供時間深度** —— 本篇的 E4 不能宣稱「在崩盤/趨勢行情也成立」。⇒ 待每日快照累積到 ≥6 個月再重跑。 |
| W2 | **E4 的 n 只有 ~28/檔** | 前瞻檢定本來就需要大 n。目前只能說「測不到」，**不能說「證明為零」**。 |
| W3 | **未做 OPEX 換月控制** | 已知 8/21 那天 `Call OI Sum` 單日 −18.7%（見 [[19-09-2026_AMZN_TREND2-TREND_strategy]] `ST_AMZN_1909_2_2`）⇒ 跨 OPEX 的差分含結構斷點。下一版應把 OPEX 當日的 Δ 剔除後重跑 E3/E4。 |
| W4 | **未檢驗 ROMA 是否有其他同型欄位** | `Gamma Notional`、`Call/Put Gamma`、`Call/Put Delta` 都是水準欄位，很可能同病。⇒ 待把 E1/E4 掃過 synth_oi 全部數值欄。 |
| W5 | **未回頭修 ROMA 的輸出文案** | `layer3.py:189` 那句語義標籤仍會照印。要不要改成「同日溫度計」措辭、或直接在 scan 輸出附上同期價格變動，需 user 裁決（改的是 ROMA 產出口徑，非分析層）。 |

---

## CC_ALL_1909_7｜附錄：腳本與資料

| 項目 | 路徑 |
|---|---|
| 本篇主腳本（E1–E4 ＋ bootstrap CI ＋ 橫斷面） | `py_dir/19-09-2026_delta_notional_is_price_function.py` |
| 同批次的 AMZN OPEX 後 gamma 剖面（非本篇論點，同次分析產出） | `py_dir/19-09-2026_amzn_postopex_gamma_profile.py` |
| 資料源 | `spotgamma_report/auto/synth_oi/<SYM>/<SYM>_synth_oi_2026-09-18.csv`（75 檔；**內容 trade date 止於 2026/9/16**） |
| ROMA 版本 | `v5.48 (b418a6b)` |
| 重跑方式 | `python3 py_dir/19-09-2026_delta_notional_is_price_function.py` |

---

**關聯**：[[feedback_monotone_column_may_be_a_function_of_another]]｜
[[project_rate_beta_regime_no_forward_power]]（同一類「同日溫度計 vs 前瞻訊號」的分野）｜
[[feedback_ratio_field_direction_needs_leg_split]]（比值欄位的另一種誤讀）｜
[[feedback_check_signal_fire_rate_before_edge]]｜[[feedback_hitrate_needs_conditional_baseline]]｜
[[feedback_signal_gate_vs_weight_upgrader]]｜[[reference_date_aliasing_inflates_backtest_n]]｜
[[19-09-2026_AMZN_TREND2-TREND_strategy]]｜[[project_roma_divergence_layer_falsified]]
