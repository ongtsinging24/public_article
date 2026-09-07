# 估值方法論：NTM (Next Twelve Months) Blend Forward Window

> **建立日期**：2026-05-21
> **用途**：個股估值的 forward window 標準作法 — 套用於 ANA / SAVEST / 加倉評估、stock_valuation.md / sector_valuation.md 維護
> **相關記憶**：[[feedback_ntm_blend_valuation]]、[[feedback_conservative_base_pe_no_rerating]]
>
> ⭐ **`zone_lo` / `zone_hi` 折價帶規則的權威正文在本檔 [§12](#12-zone_lo--zone_hi-折價帶定錨規則權威正文)**
> （2026-07-21 從 gitignored 的 `.claude/valuation_convention.md` 搬入版控；舊指標一律改指這裡）。

---

## 「估值往前 6–12 個月」真偽查核

### 一句話
✅ **基本為真**，是業界主流；對應的標準術語是 **NTM（Next Twelve Months）** 估值法，但有明確適用條件。

---

## 1. 學術 / 業界主流共識

| 來源 | 結論 |
|---|---|
| **Charles Schwab / Seeking Alpha** | 股市「9–12 個月 forward」是傳統共識（"the 9-month rule"）— 早盤股價反映 1–2 季後的盈餘預期 |
| **TIKR / Wall Street Prep** | 標準 forward P/E 用 **NTM EPS**（next twelve months），不是 current FY |
| **SaaS / 高成長業界** | EV/NTM Revenue 是 headline 估值倍數；高 NRR 標的（>120%）甚至看 **FY+2** |
| **Calendarization 方法** | NTM = `(剩餘季數權重 × FY1 EPS) + (其餘權重 × FY2 EPS)` — 自動 blend 跨 fiscal year |

→ 所以「半年到一年」是 **NTM 的口語化版本**，與機構共識一致。

---

## 2. 適用條件（✅ 6–12 月 forward 成立）

| 條件 | 為什麼 |
|---|---|
| **高 earnings visibility** | SaaS、訂閱制、消費龍頭 — 未來營收能見度高，市場敢預付 |
| **高成長 (>20% YoY)** | growth premium 把估值往未來推；越成長越往前看 |
| **多頭 / risk-on regime** | 投資人「願意」付未來盈利，forward window 拉長 |
| **接近 FY 末段（H2 of current FY）** | 自然從 NTM 偏向 FY+1 加權 |
| **低 macro 不確定性** | 利率、總體穩定 → DCF 折現率穩 → 願意看更遠 |

---

## 3. 不適用條件（❌ 退回 current FY / 甚至 TTM）

| 條件 | 為什麼 |
|---|---|
| **強週期股**（半導體、能源、原物料、銀行）| 盈利週期反轉風險大，市場只敢看下個轉折點，常用 TTM 或 next-quarter |
| **盈利能見度差** | 一次性事件、訴訟、重組中 — forward EPS 不可靠 |
| **空頭 / risk-off regime** | de-rate 過程中 forward window 縮短，2022 Q3 NASDAQ 例子退到 TTM |
| **總體不確定性高**（衰退恐慌、利率衝擊）| 投資人懷疑 forward EPS 估算 → 折現窗收窄 |
| **pre-profit / 負 EPS** | EPS 框架失效，改用 EV/Sales、EV/EBITDA |
| **管理層 guidance 失信** | 一次重大 miss 後，市場暫時不採信 NTM consensus |
| **Style rotation 期** | 從 growth → value 切換時，forward 估值集體被砍 |

---

## 4. 經驗法則 / Rule of Thumb

```
高成長 SaaS（NRR>120%）  → 估 NTM 甚至 FY+2     （提前 12-24 月）
一般成長股 (10-20% YoY)   → 估 NTM              （提前 9-12 月）
穩定成熟（公用、消費必需） → 估 NTM + DCF        （提前 12 月 + 永續）
週期股                    → TTM 或 next-2Q     （提前 0-6 月）
深度週期 / 困境股          → TTM / book value   （幾乎不 forward）
```

---

## 5. NTM Blend 計算公式

```
remaining_quarters_in_FY1 = 4 − months_elapsed_in_FY1 / 3
weight_FY1 = remaining_quarters_in_FY1 / 4
weight_FY2 = 1 − weight_FY1

NTM_EPS = weight_FY1 × FY1_EPS + weight_FY2 × FY2_EPS
NTM_target = NTM_EPS × 適當 P/E
```

### 5.1 ⚠️ 先確認「FY1 是哪一年」再套權重（2026-07-28 立，待辦⑧ 實證）

上式**預設 FY1 ＝ 尚未結束的當期會計年度**。這個前提在
**「FY 已結束、年報還沒發」** 的窗內不成立（FN 6/30→8/18、LITE 6/27→8/12，各約 6–7 週）：
街口共識的 `0y` 這時仍指**已經結束**的那個年度。

- **人工算會踩**：看到「FY 6 月底結束、現在 7 月」直覺算「還剩 11 個月 ⇒ w_FY1=0.92」，
  但那 92% 屬於的是 `+1y`，不是 `0y`。
- **機器也踩過**：`val_refresh` v3.61 前用 yfinance `lastFiscalYearEnd` 推年份，
  該欄**只在年報發佈後才前滾** ⇒ 多推一年。實測 LITE fair 344 vs 正解 697（**少算 51%**）。
- ★ **最難察覺的地方**：權重的**數值是對的**（確實是 0.92），錯的是它乘到哪一年
  ⇒ 看輸出完全正常。**索引差一年不會讓數字看起來可疑。**

**判準**（v3.61 起 `fy1_anchor_is_stale()` 自動判，人工比照）：
看**最後一季已公佈財報**的期末日 Q —— 若 Q 還沒走到該 FY 的收尾季、且該 FY 結束日已過今天，
則 `0y` 已是過去式 ⇒ **NTM 直接取 `+1y`**（其餘不足一年的部分落在無共識的次一年度，
不外推＝偏保守）。**不要用「上一個 FY 結束日」推**——一年才更新一次的欄位，
無法用來判「現在是哪一年」。

### 5.1.1 🔴 同一道守衛的**鏡像**失效：年報**已發**卻仍被判 stale（2026-08-19 立，v4.34 修）

上面那條只守了一半。另一半是：**年報已發、`0y` 已經滾動了**，
但拿來判的端點還沒吃到年報那一季 ⇒ 守衛照樣判 stale、把錨**再往前推一年**（用到 FY+2 的共識）。

**FN 2026-08-19（年報 08-18 發，T+1）**：工具提案 NTM 22.21 / fair **843.85（+28.2%）**，
正解 w_fy1=312/365 ⇒ NTM **18.35** / fair **697（+5.9%）**。
同一個 yfinance 的 `income_stmt` **年度列早就有 2026-06-30（GAAP EPS 13.05）那一筆**——
資料自己已經說 FY2026 收完了，只是守衛沒問它。

★ **根因不是「挑錯欄位」，是「挑了單一欄位」**：年報那一季正是每個端點各自最慢的那一筆，
而且**「誰在落後」會隨時點輪替**——

| 時點 | `income_stmt` 年度列 | `quarterly_income_stmt` | `mostRecentQuarter` | `lastFiscalYearEnd` |
|---|---|---|---|---|
| FN 2026-08-19（T+1） | ✅ 已有 | ❌ 落後 | ❌ 落後 | ❌ 落後 |
| FN 2026-08-30（T+12） | ✅ 已有 | ❌ **仍**落後 | ✅ 已滾 | ✅ 已滾 |
| INTU 2026-08-30（T+5） | ❌ 落後 | ❌ 落後 | ✅ 已滾 | ✅ 已滾 |

**v4.34 判準**：四個端點 **OR** —— 年度列／季列／`mostRecentQuarter` 任一走到 FY 結束日（±14 天）
即代表年報季已公佈、`0y` 已滾到新 FY；`lastFiscalYearEnd` **只當佐證**（v3.61 已證它最慢，
單獨成立時不下結論）。**證據不足一律 skip ＋印出兩種 NTM 讓人選**，不猜方向——
兩個方向都各出過一次事（猜「還是當期」＝ LITE 少算 51%；猜「已是過去式」＝ FN 多算 28.2%）。

**全表量（2026-08-30，43 檔）**：舊判準觸發 6 檔、**4 檔是偽陽性（66.7%）**——
FN／COHR／LITE／INTU 年報都已發（08-18／08-12／08-11／08-25），
只有 MU（FY 08-28 才收）與 PANW（FY 07-31 收、09-01 才發）是真的。

★ 通則（與 §15.1 並列）：**同一個資料源的不同端點新鮮度不一致，而且誰在落後會輪替**
⇒ 任何「挑一個最好的欄位當唯一判準」的修法都只是把翻車窗口挪到別的時點。

### 範例：CRWD（FY 結束 Jan，2026-05-21 計算）

- FY27 = Feb 2026 - Jan 2027（current）
- 已走 ~3 個月（Feb-Apr），May 是 Q1 進行中
- 剩餘 FY27：~9 個月 → weight_FY27 = 9/12 ≈ 0.67
- weight_FY28 = 1 − 0.67 = 0.33
- NTM_EPS = 0.67 × $6.17 + 0.33 × $8.00 = **$6.77**
- NTM 合理目標 75x = **$508**
- NTM Bull 90x = **$609**

→ 比 FY27 框架（$463 合理 / $555 Bull）寬鬆，比 FY28 框架（$600 合理 / $720 Bull）保守，**這才是市場實際定價的 baseline**。

---

## 6. 何時市場會「跳到純 FY+1」？

典型觸發：
1. **進入 FY 下半年**（自然 blend 偏向 FY+1）
2. **重大 beat + raise**：管理層把 FY+1 guidance 拉高 → 市場提前換軌
3. **產業 re-rating**（如 AI 故事重新定義 TAM）— 但 user 既定原則 [[feedback_conservative_base_pe_no_rerating]] **不上修 P/E**
4. **接近 next ER 預期 strong beat**：市場可能提前數週切換

---

## 7. 套用到 ROMA / Valuation 維護的 4 步驟

做 ANA / SAVEST / 加倉評估時：

1. **先查標的目前在 FY 哪個季度**（fiscal year 結束月）
2. **計算 NTM blend 權重**（剩餘季數 / 4）
3. **給出三個目標價**：current FY、NTM blend、FY+1 — 讓現價落點透明
4. **結論用 NTM blend 為 base**；FY+1 為樂觀 stretch
5. **若標的不符合適用條件**（週期 / 困境 / 負 EPS），明確說明並退回 TTM 框架

---

## 8. 常見 fiscal year 結束月（持倉 / 監控標的）

| Symbol | FY 結束 | 2026-05-21 進度 | NTM 主導 |
|---|---|---|---|
| GOOG, META, AMZN, TSM, AMD, ANET, PLTR, LLY, NFLX, ASML, VRT, TER, GLW, ETN, NOW | Dec（calendar） | FY26 5/12 | NTM = 58% FY26 + 42% FY27 |
| MSFT, LRCX, KLAC, COHR, FN, LITE | Jun | FY26 11/12 | NTM ≈ 92% FY27 |
| **SNDK, WDC** ※52/53 週制 | Jun/Jul | FY26 11/12 | NTM ≈ 92% FY27 |
| INTU, PANW | Jul | FY26 10/12 | NTM ≈ 83% FY27 |
| MU | Aug | FY26 9/12 | NTM ≈ 75% FY27 |
| AAPL, QCOM | Sep | FY26 8/12 | NTM = 33% FY26 + 67% FY27 |
| AVGO, SNPS, AMAT | Oct | FY26 7/12 | NTM = 42% FY26 + 58% FY27 |
| NVDA, CRWD, MRVL, WDAY | Jan | FY27 3/12 | NTM = 67% FY27 + 33% FY28 |

> ※ **SNDK / WDC 是 52/53 週制**（FY 結束＝最接近 6/30 的**週五**，FY2026 結束 **2026-07-03**）⇒ 權重分母不是 365 而是該 FY 的實際天數（FY2027 = 2026-07-04~2027-07-02，**364 天**）。
> 2026-09-06 建卡時 w_fy1 = 300/364 = **0.824**（見 `valuation_log/SNDK.md` / `WDC.md`）。

---

## 9. 與既有原則的關係

- **[[feedback_conservative_base_pe_no_rerating]]**：NTM blend 處理「往哪個 EPS 推估」；保守 base_pe 處理「給多少 P/E」。兩者**互補不衝突**：NTM 給合理 EPS scale，保守 P/E 確保不在 AI re-rating 中追高。
- **三檔目標價的意義**：current FY = 短線錨點、NTM blend = 市場真實定價、FY+1 = 樂觀 stretch（不當 base case）。
- **遇上週期股 / 困境股**：直接退回 TTM 框架；NTM blend 不適用。

---

## 10. 估值資料來源（交叉驗證）

| 來源 | 欄位 / 用途 | 對應 ROMA 框架 |
|---|---|---|
| ~~**[EVC — Easy Value Check](https://www.easyvaluecheck.com/watchlist)**~~<br/>⛔ **已停訂 2026-07-15** | ~~當前財年合理估值（區間）<br/>前瞻下個財年合理估值（區間）<br/>前瞻下個財年最大估值範圍<br/>Forward PE / PE (TTM) / Beta~~ | **不再是有效來源。** 最後快照 `2026-05-27`，`collectors/evc_*` 六模組已標 deprecated。<br/>散落各估值卡的 EVC 數據皆為**歷史快照**（已於 2026-07-21 批次加警語），保留供決策追溯，**不得引用為現值**。<br/>⚠️ 缺口：失去**獨立第三方**交叉檢核 —— `pct_to_fair` 大正值時只能自己查自己（[[feedback_pct_to_fair_decompose]]）。<br/>**✅ 2026-07-29 裁決：不補**（收尾卡待辦②，採方案 a）。理由＝爬蟲替代源（stockanalysis/finviz）本身也內含它自己的 PE assumption，換來的不是「獨立」錨、是另一個要維護且會過期的口徑；改**靠 §12 保守 base_pe 紀律 + §13 死規則把關**。<br/>⚠️ **代價要記住**：`pct_to_fair` 大正值時，「便宜」與「我把 base_pe 設寬了」兩者**沒有外部證據可分辨** —— 只能靠 §12.3 自我檢查，這是已知且被接受的殘餘風險。<br/>六模組（1,144 行）已於 **v3.62 (2026-07-29) 刪除** |
| **Yahoo Finance** | 現價、analyst mean target、consensus EPS（FY1/FY2）、街口 high/low | 三檔目標價中 base / 街口均價對照 |
| **SEC EDGAR** | 10-K/10-Q 原始 EPS / Revenue、管理層 guidance | actual EPS 校準、財報後 revaluation 依據 |
| **Seeking Alpha** | 個股 thesis、estimates revision、quant grade | 訊號驗證、bear/bull 假設源頭 |

> **使用順序建議（現行）**：ROMA 自有三檔目標價先建立 → 用 **yfinance 街口共識 EPS + analyst mean/high/low target** 比對是否吻合 → 偏離 >15% 時回頭檢查 EPS 或 PE 假設哪一邊有問題。
> **注意**：外部來源給的區間內含它自己的 PE assumption，一律不取代 [[feedback_conservative_base_pe_no_rerating]] 紀律 — 若其上緣是基於 AI re-rating 後的 PE，仍以 ROMA 保守 base_pe 為準。
>
> <details><summary>⛔ 歷史：EVC 停訂前的使用順序（2026-07-15 前，僅供追溯）</summary>
>
> ROMA 自有三檔目標價先建立 → EVC 比對「合理區間」是否吻合 → 偏離 >15% 時回頭檢查 EPS 或 PE 假設哪一邊有問題。EVC 給的是區間（含 PE assumption），不取代保守 base_pe 紀律。
>
> </details>

---

## 11. 來源 / 方法論參考

- [Seeking Alpha — What Forward Period Do S&P 500 Earnings Discount?](https://seekingalpha.com/article/4241709-what-forward-period-s-and-p-500-earnings-discount)
- [Charles Schwab — Stock Analysis Using P/E Ratio](https://www.schwab.com/learn/story/stock-analysis-using-pe-ratio)
- [TIKR — NTM Explained: How Forward-Looking Metrics Help Value Stocks](https://www.tikr.com/blog/ntm-next-twelve-months-explained-how-forward-looking-metrics-help-you-value-stocks)
- [Wall Street Prep — Forward Multiple Formula](https://www.wallstreetprep.com/knowledge/forward-multiple/)
- [IB Interview Questions — LTM vs NTM Multiples: Trailing, Forward, and Calendarized](https://ibinterviewquestions.com/guides/valuation-investment-banking/ltm-vs-ntm-multiples-trailing-forward-calendarized)
- [Meritech Capital — Public SaaS Valuation Update Post Q1 Earnings](https://www.meritechcapital.com/blog/public-saas-valuation-update-post-q1-earnings-part-2-2)
- [Smart Asset — Forward P/E vs Trailing P/E](https://smartasset.com/investing/forward-p-e-vs-trailing-p-e)

---

## 12. `zone_lo` / `zone_hi` 折價帶定錨規則（權威正文）

> **立規**：2026-07-15（EVC 停訂當日）｜**搬入版控**：2026-07-21（EVC 收尾④ dangling pointer）
> **權威性**：本節即正文。`.claude/valuation_convention.md` 是 **gitignored 的本機副本**，只保留指標；
> 兩者若不一致，**以本節為準**（[[project_evc_discontinued_zone_from_fair]]）。
> **背景**：EVC 已停訂 → 原本靠 EVC 支撐帶當 zone 錨的做法失效，改用自家估值口徑的折價帶，無外部依賴。

### 12.1 定義與公式

`zone_lo` / `zone_hi` 是 ROMA `opportunities/valuation_meta.py::classify_zone` 的**建倉等待區**邊界，
**不是**技術支撐、**不是**選擇權牆位。

```
zone_lo = zone_fair × 折價下緣
zone_hi = zone_fair × 折價上緣
```

| 標的性質 | 折價帶 | 理由 |
|---|---|---|
| 低 beta / 現金流穩定 | fair × **0.80 ~ 0.92** | 回檔淺，等太深等不到 |
| 高 beta / 週期 / 半導體 | fair × **0.70 ~ 0.85** | 波動大，要求更厚的進場 MoS |

判定用 beta（yfinance `info['beta']`）＋板塊週期性，**在明細檔寫明採用哪一檔與理由**。

**推導實例**：`valuation_log/NVDA.md`（2026-07-15 重估）— β 2.24 → 高 beta 檔 →
`fair 287 × 0.70 = zone_lo 201`、`287 × 0.85 = zone_hi 244`。

### 12.2 ⚠️ 不可混用的口徑

- SG data_table 的 **PW / HW / CW 是選擇權水位**，日更，屬 levels 口徑 → **不進 zone 欄**
  （[[feedback_wall_levels_ssot_sg_data_table]] 管的是 levels，不是估值）
- **技術帶**（MA / ATR / 52W）是技術口徑 → **不進 zone 欄**
- zone **只在重估時**更新，跟著 `zone_fair` 走

### 12.3 自我檢查（算完必做）

回頭看現價落在哪一區。若結論與 implied P/E 明顯矛盾（例如 implied NTM 19x 卻判 `above_waiting`），
代表折價帶或 `base_pe` 設錯 —— **先查框架自己、再下市場結論**（[[feedback_pct_to_fair_decompose]]）。
單調性必須成立：`zone_lo < zone_hi < zone_fair < zone_bull`（違反＝壞卡，
2026-07-15 全表曾有 8 檔 `zone_hi ≥ zone_fair` 導致 `above_waiting` 級整個消失）。

### 12.4 已知未涵蓋範圍

**ETF / 指數（IGV / QQQ / SPY / IWM / SMH / SOXX）沒有個股 beta，本節（§12.1）的兩條帶不適用。**
✅ **EPS/倍數怎麼算** 已於 2026-08-05 定案 → **§12.6**。
✅ **`zone_lo`/`zone_hi` 的折價帶** 已於 2026-08-19 定案 → **§12.7**（待辦④ 結案）。
⇒ 本節的「未涵蓋」現在只剩**槓桿 ETF／現金等價／期貨**（見 §12.7 末段）。

### 12.5 EPS 共識來源（2026-07-15 起，同批立規）

- 街口共識用 **yfinance**：`Ticker(SYM).earnings_estimate`（`0y`=FY1／`+1y`=FY2）、
  `.eps_trend`（看 7d/30d/60d/90d 上修下修軌跡，判斷是趨勢還是雜訊）
- ⚠️ **別只看 FY1/FY2**：一併看 `0q`（下一季）。**遠端上修＋近端下修＝街口在把成長往後推**，
  是要標註的反向訊號（[[feedback_ntm_blend_valuation]]）
- P/E 框架不隨股價 re-rate，重估只動 EPS（[[feedback_conservative_base_pe_no_rerating]]）

**★ 12.5.1 `eps_trend` 的歷史欄是「期別錨定」，不會 roll（2026-08-19 實測定案）**

一度懷疑 `0q`/`+1q` 在財報後會 roll（`0q` 由 Q2 變 Q3），因此 `current` 與
`7/30/60/90daysAgo` 比的不是同一季 —— **實測反過來，該懷疑已證偽**。

- 自證判準（不需外部共識，同一張表就能測）：若真的會 roll，今天的 `+1q[90daysAgo]`
  與今天的 `0q[current]` 會指**同一個會計季** ⇒ 兩者只該差 90 天的共識修正。
- 12 檔全部「近 90 天內有 ER」，7 檔季節性夠強、有決定性，**0/12 支持 roll**：

  | AAPL | LULU | COST | AMZN | MU | AVGO | GOOG | （不決定性：兩季太接近） |
  |---|---|---|---|---|---|---|---|
  | +49.1% | +48.4% | −26.7% | +21.3% | −20.4% | +17.2% | +9.3% | NVDA / WMT / ORCL / ADBE / CRM |

- ⇒ **不加**「距 ER < N 天，趨勢欄不可比」這類警告：它對每一檔剛財報的卡都會噴一條
  **永遠是假的**旗。腳本 `py_dir/19-08-2026_eps_trend_period_anchor_probe.py`。

**★ 12.5.2 一次性利益的判準是「跨 ER 的階梯」，不是「FY1 > FY2」（v4.15）**

真正長在 ER 邊界上的東西是本節主題本身：一次性利益（投資評價 MTM 之類）只墊高
**已實現的那一年** —— 街口不預測未來的 MTM ⇒ `0y` 在財報當下出現**階梯**，`+1y` 幾乎不動。

```
確認軸 = Δ90d(`0y`) ≥ +15%  且  Δ90d(`0y`) − Δ90d(`+1y`) ≥ +20pp
```

2026-08-19 實測分佈（n=8，兩群完全不重疊）：

| 判定 | 標的 | Δ90d `0y` | Δ90d `+1y` | 差 |
|---|---|---|---|---|
| 🔴 一次性 | GOOG | +44.6% | +1.9% | **+42.7pp** |
| 🔴 一次性 | AMZN | +44.3% | +6.3% | **+38.0pp** |
| ✅ 真 beat-and-raise | MU | +26.2% | +52.1% | −25.9pp |
| ✅ 正常 | NVDA / AVGO / AAPL / COST / WMT | — | — | −5.1 ~ +1.8pp |

- ★ **幅度大 ≠ 被污染**：MU 的 `0y` 也漲 26%，但 `+1y` 漲更多 ⇒ 兩腳一起動＝真的上修。
- ★ 這一軸修掉的是靜態形狀自己列的偽陽性：**週期見頂**也長成 FY1 > FY2，
  但那是「一直都在的形狀」，不是「ER 當下才出現的階梯」。
- ★ 也修掉靜態門檻的**脆弱性**：AMZN 2026-08 的靜態形狀只險過 1.15 門檻（餘裕 **1.2%**），
  同一檔在趨勢軸上餘裕是 **38pp**。
- ⚠️ n=8（2 陽 6 陰）**極小**，陽性又正是立卡當初那兩檔 ⇒ 本軸定位是**確認/排除軸**
  （升級或降級既有旗），不是獨立取代靜態形狀的新判準；`+1y` 覆蓋殘缺時（§15.2）
  一律**先當殘缺處理**，因為趨勢軸的分母就是壞掉的那一格。

**★ 12.5.3 META `eps_basis=clean|reported`（v4.15）**

人工剔除一次性後，**要在卡上留機器可讀的記號**，否則工具每次複跑都拿乾淨的 `base_eps`
去比未剔除的街口共識，穩定報出 +16~17% 的假 Δ —— 下一個人看到會以為卡舊了，
把它「修正」回**錯的方向**（2026-08-05 GOOG/AMZN 實例）。

| 值 | 意思 | `val_refresh` 行為 |
|---|---|---|
| `clean` | `base_eps` 已剔除一次性 | 本輪共識仍髒 ⇒ 標 **hold**（⚠SYM，不可直接套用）；共識乾淨後自動安靜 |
| `reported` | `base_eps` 用街口原始口徑 | 本輪判定含一次性 ⇒ 警告**卡片本身**可能也被污染 |
| 缺 | 未聲明 | 判定含一次性時提示補標 |

⚠️ **別跟 `base_eps_basis` 搞混**（欄名只差三個字、語意正交）：
`eps_basis` 答「有沒有剔除一次性」，`base_eps_basis` 答「是不是 NTM blend 口徑」。
互填會靜默失效 ⇒ 工具用詞表機械反查，填錯欄會出 🔴 而不是安靜不生效。

### 12.6 籃子（ETF / 指數）NTM P/E 口徑（2026-08-05 立，權威正文）

> 立項背景：§12.4 的「ETF 口徑待議」在 2026-07-28（SMH/SOXX）與 2026-08-05（QQQ/SPY/SMH）兩次
> 實作後定案。本節只規範 **EPS / 倍數怎麼算**；**zone 折價帶**另見 **§12.7**（2026-08-19 立）。

**① 加總方式＝盈餘加權（調和），不是簡單加權平均**

```
basket_PE = Σw ÷ Σ(w / PE_i)        # 等價於 Σ市值 ÷ Σ盈餘
PE_i      = price_i / NTM_EPS_i     # 個股照 §5 做 NTM blend
隱含每股 EPS = ETF價 / basket_PE
```

簡單加權平均會被「小權重 × 高倍數」整個拉高（實測 SMH 29.0x vs 調和 22.5x、NDX 61.2x vs 25.2x）。
**兩種口徑的數字不可相減當 de-rate**。外部校驗用 LSEG/FactSet 的 forward P/E（同期、同指數）。

**② 三個必查的陷阱（每一個都會讓籃子看起來比實際便宜）**

| 陷阱 | 症狀 | 處置 |
|---|---|---|
| **幣別**：yfinance `earnings_estimate` 有時以 `financialCurrency` 計價（ASML/FER/CCEP=EUR、PDD=CNY），price 卻是 USD | PDD 算出 **1.2x**（實 8.1x），單檔佔籃子盈餘 6% | 轉匯。**但不能只看 `financialCurrency`** —— TSM 是 TWD 而估計本就是 USD。判準＝「我方 PE ÷ Yahoo `forwardPE` ≈ 匯率」才轉 |
| **一次性利益污染共識**：街口 FY1 含投資評價利益 | 2026-08-05 GOOG（+$6.26/股）、AMZN（+$3.80/股），合計 NDX 權重 18% ⇒ 籃子 24.4x vs 乾淨 25.2x | 以 `stock_valuation.md` 當日重估的乾淨 EPS **覆寫**（house SSOT 優先於機械共識） |
| **負 EPS / 無盈餘成分股** | WBD / NBIS / CRWV / RKLB 被剔除；SPCX 有 3.6% 權重但幾乎沒盈餘（793x） | 剔除負值並**明報覆蓋率**；高權重無盈餘股要單獨點名（它墊高的倍數是真的，但成因不是「貴」） |

**③ 權重來源**：SMH/SOXX 用 stockanalysis.com；**NDX/QQQ 用 slickcharts.com/nasdaq100**
（⛔ stockanalysis 的 QQQ 頁免費層只給 top 25，且實測與市值比對不上）。
**落地前一律用 yfinance 市值比交叉驗證至少 3 組比值**（如 NVDA/AAPL、NVDA/MU、AVGO/NVDA）。

**④ 指數層 EPS 不准用頂層推估**：2026-06-14 的 NDX「$1,110（自推估）」實測低估 **6.8%**，
把倍數讀成 26.7x（實 ~25x）——**偏低的分母會讓「已經很貴」的結論看起來更硬**，方向性錯誤。
SPX 有 FactSet Earnings Insight 官方 bottom-up（免費 PDF，每週五）⇒ **直接用官方值**，
其餘指數/ETF 走上述籃子法。腳本：`py_dir/05-08-2026_basket_ntm_pe.py`。

**⑤ ⚠️ 籃子 P/E ≠ 全基金 P/E —— 隱含每股 EPS 只能用後者算（2026-08-08 補，IGV/AGIX 重估時踩到）**

`basket_PE = Σw ÷ Σ(w/PE_i)` 的分子只加總**有盈餘那些成分股**的權重
⇒ 它是「**覆蓋部分**的 市值 ÷ 盈餘」，不是全基金的。被剔除的成分（負 EPS、私募/pre-IPO、現金）
盈餘是 **0 但市值不是 0**，所以：

```
全基金有效 P/E   = 100 ÷ Σ(w_i / PE_i)        # w_i 以「佔全基金 %」計
隱含每股 EPS     = ETF 價 × Σ(w_i / PE_i) ÷ 100
⛔ 錯誤寫法       = ETF 價 ÷ basket_PE          # 等於假設覆蓋率 100%
```

覆蓋率越低，兩者差越大。實測（2026-08-08）：

| ETF | 覆蓋率 | 籃子 P/E | 全基金有效 P/E | 錯誤 EPS | 正確 EPS |
|---|---|---|---|---|---|
| IGV | 97.33% | 26.09x | 26.80x | $3.94 | **$3.83** |
| AGIX | 83.45% | 21.63x | **25.92x** | $2.10 | **$1.75**（差 **20%**）|

★ 2026-08-05 的 QQQ / SMH / SOXX 三卡覆蓋率都 ≥96.7%，用錯誤寫法的偏差 <3.5%，**數字不必回頭改**；
但**低覆蓋率的 thematic ETF 一定要用正確式**——AGIX 若沿用錯誤寫法會把 fair 從 $52 灌到 $63。
⇒ 卡片的 `NTM_BLEND|` 行請同時寫 `basket_ntm_pe` 與 `fund_eff_ntm_pe` 兩欄，`ntm_eps` 一律取後者導出。

**⑥ 峰值盈餘要按「盈餘份額」而不是「權重」盤查（同批立）**

調和口徑下，**低 P/E 的小權重股會扛掉不成比例的盈餘**，而它們往往正是週期高點的那幾檔。
AGIX 實例：SK Hynix ＋ Samsung ＋ MU ＋ Kioxia **權重合計僅 5.39%**，卻貢獻 **33.2% 的籃子盈餘**
（P/E 3.4~5.8x）；剔掉它們，子籃子由 21.63x 跳到 **30.30x**。
⇒ 每次算完籃子，**必列「盈餘貢獻 top10」**，凡「權重小但盈餘份額大」的就要單獨做 EPS 打折敏感度；
否則會把週期高點的分母當成常態，得出「這支 ETF 很便宜」的方向性錯誤結論。

### 12.7 ETF / 指數的 zone 折價帶（2026-08-19 立，權威正文｜待辦④ 結案）

個股帶是**從 beta 導出**的；ETF 沒有個股 beta ⇒ 改從**價格自己實際走到過哪裡**導。
量 2014-08~2026-08（12 年）距 **252d 高點**的回檔分布：

| 組別 | 成分（量測樣本） | 日別 p25 | 日別 p10 | 年度最深回檔中位 |
|---|---|---:|---:|---:|
| broad | SPY / QQQ / IWM | −8.3% | −15.9% | −18.3% |
| sector | SMH / SOXX / IGV | −12.3% | −23.1% | −24.1% |

```
etf_broad  = fair × 0.80 ~ 0.92      # ＝低β 帶（量測支持沿用，不另造數字）
etf_sector = fair × 0.76 ~ 0.88      # 新帶
```

**★ 兩個結論都是量出來的，不是套用直覺：**
- **broad 幾乎逐格對上既有低β 帶**（hi −8.3% vs 0.92、lo −18.3% vs 0.80）⇒ 沿用，不發明新數字。
- **sector 不能套高β 帶**：`0.70` ＝ −30%，比它自己的年度最深回檔中位（−24.1%）還深、
  接近 Q1（−34%）⇒ 那正是 `BAND_DEEP` 想擋的「等待區實務上等不到」失效模式本身。

**★ 兩條導出路徑互相印證**（立帶當下的交叉檢核）：新 `zone_lo` 落點換算回倍數，
幾乎就是各卡自己 bottom-up 的 **bear 倍數** —— SMH 16.0x vs 自家 bear 17x｜SOXX 14.4x vs 15x｜
IGV 18.3x vs 18x｜SPY 15.2x vs 16x｜IWM 14.4x vs 15x。
⇒ 採用本帶**不是丟掉**舊的倍數推導，而是把它一般化；真正被修掉的是**過緊的 `zone_hi`**
（舊 hi/fair 為 0.90~0.96，`above_waiting` 級只剩 4~10% 寬，退化成二元）。

**帶別歸屬**（`valuation_zone_audit.ETF_BAND_OF`；未登記的新 ETF 會被當個股檢查而噴 `BAND_*`，
**這是刻意的**——逼人來登記，而不是靜默套到錯的帶上）：

| 帶 | 標的 |
|---|---|
| `etf_broad` | SPY / QQQ / IWM / XLK / RSP |
| `etf_sector` | SMH / SOXX / IGV / **AGIX** |

⚠️ **AGIX 不用它自己的數字校準**：2024-07 才上市，樣本僅 2 年且全落在多頭窗
（量到 −16.8% 年度最深，看起來比 broad 還溫和，那是樣本期假象）⇒ 依 thematic 性質掛 sector 帶。

**連 ETF 帶都不適用者**（`NO_BAND_SYMS`，仍驗單調性與格式）：
- **SOXL**（3x 槓桿）：12 年年度最深回檔中位 **−65.6%**，與任何非槓桿帶都不同量級。
- **BOXX**（現金等價，無估值 zone 概念）、**MES/MNQ 期貨**。

⚠️ **ETF 帶刻意不併進 `BANDS` 一起比**：否則個股卡「湊巧落在 0.76/0.88」就會矇混過關，
等於偷偷放寬個股規則（有回歸測試守）。

⚠️ `zone_lo`/`zone_hi` 是**導出欄**（§13.5）⇒ 本次改帶**不動 7 張卡的 `last_updated`**。

---

### 12.8 同儕倍數錨的口徑（2026-09-06 立，權威正文）

> 立項：FN（Fabrinet）2026-09-04 倍數下修卡，09-06 覆核時抓到。
> §12.2 管的是「別把 levels／技術帶塞進 zone 欄」；**本節管的是另一個軸——`base_pe` 的同儕錨本身混了口徑**。

#### 12.8.1 死規則

```
yfinance info['forwardPE']  ≡  股價 ÷ earnings_estimate['+1y']（FY2 EPS）
                            ≢  股價 ÷ NTM blend EPS
```

**我方 `base_pe` 是對 NTM EPS 定義的**（§5）⇒ **同儕錨也必須是 NTM 口徑**。
✅ 允許：自算同儕 NTM blend P/E　｜　❌ 禁止：拿 `forwardPE` 當同儕錨去乘溢價倍數
（要放 `forwardPE` 只能當「對照·勿混用」欄，且**必須標明是 FY2 口徑**）。

**自算法**（逐檔，與 §5 同一套權重）：

```
w_fy1 = clamp( (info['nextFiscalYearEnd'] − today).days / 365 , 0, 1 )
NTM_eps  = w_fy1 × earnings_estimate['0y'] + (1 − w_fy1) × earnings_estimate['+1y']
peer_pe  = 現價 ÷ NTM_eps
```

腳本：`py_dir/06-09-2026_fn_peer_ntm_pe_caliber_check.py`（同時輸出 `P/E_FY2` 供逐檔驗證恆等式）。

#### 12.8.2 為什麼會系統性偏一邊（不是隨機誤差）

成長股 **FY2 EPS > NTM EPS** ⇒ FY2 口徑的 P/E **恆低於** NTM 口徑。
拿偏低的同儕中位去乘一個溢價倍數，**`base_pe` 會被設得比原意低、`zone_fair` 跟著偏低**。
方向固定往下 ⇒ 這不是雜訊，是偏誤。

**FN 實例（2026-09-04 建卡 → 09-06 校正）**：

| | FY2 口徑（誤用） | **NTM 同口徑（正確）** |
|---|---|---|
| EMS 同儕中位（CLS/JBL/FLEX/SANM） | 16.1x | **18.45x**（+15%） |
| FN 自己 | 18.7x | **21.6x** |
| COHR | 20.2x | **27.5x** |

**★ 最硬的證據是一條結論方向反轉**：卡上原本用「FN 21.5x **已貴過** COHR 20.1x」佐證下修，
同口徑下是 **FN 21.6x ＜ COHR 27.5x（便宜 21%）** —— 該格不成立。
**混口徑不只是把數字放大縮小，它會讓比較的正負號反過來。**

#### 12.8.3 用之前先驗 `earnings_estimate` 的列有沒有壞

`0y` 列出現以下**任一**特徵 ⇒ 判壞值，該檔**整檔剔除、不得當倍數錨**（連它的 `forwardPE` 也不可信，因為分母同源）：

| 判準 | FN 批次實例（LITE，2026-09-06） |
|---|---|
| `avg` 落在 `low` / `high` **之外** | avg **8.227** vs low 19.05 / high 25.27 |
| `avg == yearAgoEps`（去年值被抄進當年 avg） | 兩欄逐字相同 |
| `growth == 0.0000` 但 `+1y` growth 巨大 | 0y growth 0.00 ／ +1y growth 3.048 |

⇒ LITE 被剔除後，「元件商」錨只剩 COHR 一檔（n=1）——**這件事要寫在卡上**，
不能讓讀者以為錨是兩檔的中位。錨的樣本數本身就是判讀資訊。

#### 12.8.4 校正後 `base_pe` 怎麼處理（三條，順序不可換）

1. **若校正方向是要「上修」`base_pe` ⇒ 不自動套用**，受 [[feedback_conservative_base_pe_no_rerating]] 管，需 user 裁決。
   FN 實例：照原文「EMS 中位 ×1.6」字面重算 = 18.45 × 1.6 = **29.5x**（fair $557）⇒ 上修，**未套用**。
2. **再做一次合理性夾擠**：校正後的 `base_pe` 不得高過**商模更好的那一層**的同口徑倍數。
   FN 實例：29.5x 會高過 COHR 自己的 27.5x —— 12% GM 代工廠定價高於 37% GM 元件商，內部不自洽 ⇒ 又一個不套用的理由。
3. **數字不動時，依據敘述仍必須改**。FN 的 26x 由「EMS 中位 16.1x **×1.6**」改述為
   「EMS NTM 中位 18.45x **×1.41**，落在 EMS 18.45x → COHR 27.5x 帶的 83% 分位」。
   ⚠️ 這屬 §15「**口徑對齊 ≠ 重估**」⇒ **`last_updated` 不推**（沒有新資料進來，推日期＝重置 AGE 時鐘假裝新鮮）。

> **一句話**：口徑錯了而數字剛好還能用，**不代表可以不改**——下一次有人照著那句錯敘述外推，就會外推到錯的地方。

#### 12.8.5 為什麼不做成機器規則

同儕清單是逐卡人工選的（誰算同儕本身就是判斷），無法從 META 反推 ⇒ `val_audit` 驗不了。
本節是**人工守則**，靠三個地方接住：① 建卡時的同儕表必須有「口徑」欄；
② §12.3 自我檢查（implied P/E 與結論矛盾 ⇒ 先查框架自己）；③ §16.1 `PE_IMPLIED_GAP` 的單側告警。

---

## 13. `last_updated` 語意（權威正文，2026-07-22 立死規則）

> 立項：`document/todo_idea/15-07-2026_估值zone欄壞卡盤點與折價帶對齊.md` 待辦⑦（裁決＝修法 **(b)**：
> 維持單欄、立死規則，**不拆 `record_touched` 欄**——零 schema 變更，v3.40 財報週期錨與 `val_audit` 都不用改）。

### 13.1 死規則

**`last_updated` ＝ 估值數字被重新計算的日期。只有重估才動它。**

「重估」的唯一判準是**數字有沒有變**（可機器判定，不看 commit message 怎麼寫）：

**判準欄分兩軸**（2026-07-22 晚間補；見 13.5 的訂正紀錄）：

- **基準欄 `BASIS_KEYS`**＝`zone_fair`、`zone_bull`、`bear/base/bull` 的 `eps`/`pe`/`target`
  —— 這些是**基本面基準**，動了才叫重估。
- **導出欄 `zone_lo` / `zone_hi`** —— 由 `zone_fair × 折價帶`（§12）機械導出，
  **動它們不等於重估**（壞卡修正、帶別改判都會動到，但基本面基準日沒變）。

| 動作 | 動 `last_updated`？ |
|---|---|
| **基準欄**任一改變（EPS 校準 / NTM roll-forward / P/E 框架調整） | ✅ **要動** |
| **只重算 `zone_lo/hi`**（壞卡修正、折價帶對齊；`zone_fair` 不變） | ❌ **不動** |
| 加/刷新價格快照 `mkt_px` / `mkt_px_date` / `valuation_flag` | ❌ **不動**（只動 `mkt_px_date`） |
| 修 `next_earnings` 日程、補 `fy_anchor`/`split`/`anchor`/`cyclical`/`eps_basis` 等註記欄 | ❌ **不動** |
| 複核後**確認框架仍成立、一個數字都沒改**（「refresh 但無新財報」） | ❌ **不動** |
| 純單位換算（如 split ÷4，P/E 不動） | ❌ **不動**（基準沒變，只換單位） |
| 把既有分析首次抄進主表建卡 | ❌ 填**原分析的計算日**，不是抄進來的日期 |

★ 中間那幾列是最容易破功的：*「我今天認真看過了」不等於「今天重算過」*。
價格變了、zone 邊界重算了、判讀變了，但 EPS / P/E 框架一個字沒動
⇒ 這張卡的基本面基準日還是舊的那天。
要記錄複核，寫進明細卡的日期段落，**不要動 META 的 `last_updated`**。

### 13.2 為什麼（三個具體後果）

1. **`DETAIL_DRIFT` 會週期性復發** —— 主表每加一次價格快照就與 `valuation_log/<SYM>.md` 差一個日期，
   待辦⑥ 那 41 欄的回標白做。
2. **`AGE` 稽核被稀釋** —— 被動 touch 讓一張沒重估的卡看起來很新鮮，正好躲過 45 天盤點門檻。
3. **🔴 直接打壞 v3.40 財報週期錨** —— `valuation_meta.staleness_level()` 判準 (1) 是
   「`last_earnings > last_updated` ⇒ severe」。`last_updated` 被價格快照推到財報之後，
   **一張沒重估的卡會被判成 fresh**。
   ⚠️ 現況（2026-07-22）prod 呼叫端 `sg_institutional/layer0.py:124` **沒有傳 `last_earnings`**，
   `er_since` 退化為只看 `next_earnings < today` ⇒ 這條後果目前是**潛伏**的，
   顯性影響只有 banner 的「N 天前」與 `AGE`。但 `staleness_level` 的判準已經寫在那，
   一旦接上 `last_earnings` 就立刻materialize —— 所以規則現在立、不等它爆。

### 13.3 機器守門

`roma_cli val_audit --history` → 規則 **`UPDATED_NO_DELTA`**：掃 git 歷史，
找出「某次 commit 推後了 `last_updated`，但 §13.1 表中的估值欄零變動」的違規。
純事後稽核（本工具**只讀不改**，同 §12 的設計原則），但讓這條規則可被驗證而不只是紙上公約。

### 13.4 立規當下的存量修正（2026-07-22）

2026-07-01 一批四個 commit（`55ebd60`/`9b23ee7`/`dc8718b`/`dbe9d0e`）把 10 檔推到 `last_updated=2026-07-01`。
逐 commit 比對 META 估值欄後：**4 檔真重估、6 檔非重估**（見待辦⑦ 的證據表），
6 檔已回捲到真正的重估日（主表 + 4 張明細卡同步，`DETAIL_DRIFT` 維持 0）。
★ 這批的 commit message 全部寫著「估值 refresh」——**訊息說重估、diff 說沒有**，
再次印證 13.1「只看數字不看訊息」的判準是對的。

### 13.5 訂正：`zone_lo/hi` 是導出欄，不是基準欄（2026-07-22 晚間）

§13 立規當天的第一版把 `zone_lo`/`zone_hi` 也算成「重估欄」。**那是錯的**，
在著手待辦③（Bucket C freshness 重估）時當場踩到：

- ③ 與先前的 ①②（Bucket A/B 壞卡修正）都會大量改動 `zone_lo/hi`。
  照第一版規則，**單純把 zone 對齊折價帶就要推後 `last_updated`**
  ⇒ 一張兩個月沒重估的卡，只因為修好了它的 zone 邊界就變「新鮮」
  ⇒ **正好重新製造出待辦⑦ 要根治的那個缺陷**。
- 查 git 確認既有做法本來就是對的：Bucket A（`90f60f7`）與 Bucket B（`78925a7`）
  合計改了 17 檔的 zone，**`last_updated` 一個都沒動**（逐檔日期 `-`/`+` 成對相同）。
  ⇒ 錯的是我寫的規則，不是既有實作。

**訂正**：拆 `BASIS_KEYS`（基準）與導出欄，稽核只看基準欄。
`valuation_zone_audit.VALUATION_KEYS` 同步排除 `zone_lo`/`zone_hi`。

⚠️ **回溯影響為零**：用新舊兩組 key 各掃一次全庫歷史，違規數**同為 18 筆、完全相同**
（因為 ①② 本來就沒推日期）⇒ 這是**前瞻性的指引缺陷**，不是既有資料的損害。

★ 教訓：**規則寫完的當下無從驗證它對不對，要等下一個真實任務去撞。**
§13 立規到被自己的下一項待辦推翻，中間只隔了一小時——
所以立規時把「訂正紀錄」也留在正文裡（而不是覆蓋掉），下一個人才看得到邊界在哪。

### 13.6 `recheck_by` / `guard_until`：卡片自己武裝的閘（權威正文，2026-09-06 立）

> ★ 一句話：**`last_updated` 是回顧（上次動基準欄的日子），
> `recheck_by` 是前瞻（卡片自己承諾的下一個看的日子）。兩者語意正交。**

#### 病灶（COHR 2026-08-14 → 09-06 實例）

估值卡常在**正文**寫下對自己的追蹤承諾：

> 「`+1y` 8.37117 是 **pre-ER 共識**⋯⋯post-ER 上修後 FY27 大概率落 $9.0± ⇒
> 本卡 fair 刻意偏保守，**7–14 天內須複核共識**」

這句話是**散文**，不是機器可讀欄位 ⇒ **沒有任何東西會在到期日提醒它**。
應於 08-21～08-28 複核，實際 **09-06** 才做、**逾期 23 天**。
期間卡上 fair $335、真值 **$410**（NTM EPS 8.37→10.26，**+22.6%**），
`fp_alpha` C 級 14 檔裡名次由**第 1 沉到第 11** —— 分子過期不只是數字不準，
是**把真便宜的標的藏起來**。

#### 為什麼既有四道閘全部接不住

| 閘 | 為什麼漏 |
|---|---|
| `AGE`（45 天） | COHR 只有 23 天 ⇒ 遠未觸發。AGE 量「多久沒看」，量不到「卡片自己說 14 天內要看」 |
| `ER_PAST` | ER 是 08-12，卡片**已經**基於它重估過 ⇒ 不觸發 |
| `PE_IMPLIED_GAP` | ★ 最惡：過期分子把 fair 壓低 ⇒ 隱含 gap **看起來比較小**（−15.8% vs 真值 −31.3%）⇒ **分子過期會抑制本來會抓到它的那個閘** |
| `val_refresh` Bucket C | 依 AGE 排隊 ⇒ 同上 |

#### 兩個新欄（都放 META 行、都**選填**）

| 欄 | 值 | 規則 | 語意 |
|---|---|---|---|
| `recheck_by` | ISO 日期 | `RECHECK_OVERDUE` 🟠 | 卡片自訂的下一個複核日。**凡在正文寫「N 天內須複核／待 X 確認」就必須同時填這一欄** |
| `guard_until` | ISO 日期 **或**條件字串 | `GUARD_EXPIRED` 🟠／`GUARD_COND` ℹ️ | 「因資料源當下缺一格而採取的**保守處置**」的**解除條件** |

`guard_until` 的由來，是 §5.1 那一課的一般化：
§5.1 的處置（「FY 已結束、`0y` 尚未 roll ⇒ NTM 直接取 `+1y`」）是**窗內正確**的，
問題是**窗會關**（`0y` 一 roll 就關），而沒有任何東西提醒它關了。

> **同一個欄位形狀，在窗內是保守、在窗外變成低估。**

⇒ 凡是「因為資料源當下缺一格而採取的保守處置」，都應該同時登記**解除條件**，
否則保守處置會在資料源修好之後**繼續生效**，變成無人察覺的偏誤。
（同型前例：LIN 的 `SPARSE_COVERAGE`、PANW 的 `+1y` 改錨 —— 那兩張至少有 §15.3 的 META 欄
記錄決定，COHR 那型是**連決定都只寫在散文裡**。）

#### 三個刻意的邊界

1. **一律 🟠 WARN，不做 🔴 ERROR**：逾期不等於數字錯 —— 複核後一個字都不動是常態
   （2026-09-05 的 INTU/SNPS/DDOG/LIN 四檔即是）。ERROR 留給結構破損。
2. **`guard_until` 的條件字串不自動判**：自動判需要在只讀稽核裡重建資料源狀態，
   那是把稽核變成 runtime 依賴。條件字串只出 ℹ️ `GUARD_COND` 清單 ——
   **先讓它能被 grep 到就有一半價值**；日期形式才進 `GUARD_EXPIRED` 判決。
3. **與 AGE 不去重**：兩者都報。AGE 說「卡舊了」，`recheck_by` 說「卡答應要做的沒做」，
   而且只有後者說得出**欠的是什麼**。

#### ★ 立規前先量：本規則的純偵測增量只有 1/4

2026-09-06 全表回掃（`stock_valuation.md` ＋ `valuation_log/*.md`，
語型 `待…確認|校準|複核` ／ `N 天內須…` ／ `必重估` ／ `屆時`）撈到
**4 張未兌現的散文承諾**：

| 卡 | 承諾 | 逾期 | 既有閘 |
|---|---|---|---|
| COHR | 「7–14 天內須複核共識」(08-14) | 23 天 | ❌ **四閘全盲** |
| TSM | zone_lo/hi「財報後待重新校準」(07-16) | 52 天 | ✅ AGE |
| PANW | 「09-01 後必重估」(08-19 ER) | 5 天 | ✅ ER_PAST + AGE |
| IWM | RUT NTM EPS「待 bottom-up 校準」(06-14) | 84 天 | ✅ AGE |

**3/4 既有閘已經在報** ⇒ 保留本規則的理由不是「多抓幾張」，而是：

- **(a)** 那 1/4 正是唯一造成實質損害的一張。**承諾期 < 45 天的窗在定義上就是 AGE
  看不見的窗**，而卡片刻意寫短承諾，正因為它自知那段時間內數字會動
  ⇒ AGE 抓不到的**不是邊緣案例，是主要案例**。
- **(b)** `recheck_by` 是觸發器，欄位本身是**內容**。TSM 被 AGE 報了 7 天，
  沒有任何讀數告訴人「它欠的是 zone_lo/hi 重新校準」。

#### 立規當下的存量修正（2026-09-06）

回掃後補欄四張（**只加欄、零數字變動**）：

| 卡 | 補的欄 | 依據 |
|---|---|---|
| TSM | `recheck_by=2026-07-20` | 承諾＝「財報後待重新校準」；ER 07-16（四），SG 水位正常落後 D−2 ⇒ 07-20（一）是最早可兌現日 |
| PANW | `recheck_by=2026-09-01`＋`guard_until=2026-08-19` | 前者為卡片原文明載日期；後者＝`feed_reject=+1y` 的解除點（08-19 發 FY2026 年報＋給 FY2027 guidance） |
| IWM | `guard_until=rut_bottom_up_consensus` | 承諾無日期、等的是**外部資料源**（FactSet/Bloomberg RUT bottom-up）⇒ 條件字串型 |
| ACN | `guard_until=0y_rolled_to_FY2027` | 09-06 建卡即在 §5.1 窗內（`w_fy1=0.00 / w_fy2=1.00`，因 yfinance `0y` 尚未 roll）⇒ **預先武裝，不等它變成第二個 COHR** |

⚠️ COHR 本身**不補**：09-06 已複核、承諾已兌現，補一個過去的 `recheck_by` 只會製造恆真警報。

---

## 14. 情境階梯（bear / base / bull）不變式（權威正文，2026-07-22 立）

> 立項：待辦③ 的 B 群實測。`val_refresh` 提案時發現 **6 檔的新 `base_eps` 已超過卡上 `bull_eps`**
> （AMD/NFLX/ASML/VRT/GLW/CRM）⇒ 若只套新 base 不動 bear/bull，會留下
> **「樂觀情境比基準還低」** 的自相矛盾卡。
> Bucket C 的 `AGE` 只量天數，**量不到這一類**——而它的殺傷力比單純日期過期大。

### 14.1 不變式

| 軸 | 規則 | 嚴格度 |
|---|---|---|
| `*_eps` | `bear_eps ≤ base_eps ≤ bull_eps` | **允許相等** |
| `*_target` | `bear_target < base_target < bull_target` | **嚴格遞增** |
| `*_pe` | ❌ **不是不變式，刻意不檢查** | — |

**為什麼 eps 允許相等**：NOW / SOXX 三情境 EPS 全等（`4.54` / `25.5`），
價差整個放在倍數上——這是合法的建模方式。寫成嚴格遞增會製造兩筆恆存在的假警報。

**為什麼 target 可以嚴格**：全表 48 檔實測 strict 違反 **0**。
兩個情境的目標價相等＝情境退化，本來就該報。

### 14.2 ★ 為什麼 P/E 軸不查（最重要的一條）

直覺會說「三個軸都該單調」。**實測不是**——全表有 3 筆 `pe` 倒掛，逐張看過**全是合理建模**：

| SYM | bear→base→bull P/E | 為什麼合理 |
|---|---|---|
| SNOW | 75 → 140 → **131** | bull 情境 EPS 更高（1.85→2.60），成長兌現後倍數自然壓縮；target 仍 139<259<341 |
| ORCL | 18 → 26 → **25** | 同型（EPS 8.05→10.87） |
| INTC | 30 → **27** → 30 | bear 用 **trough EPS × 高倍數**（週期股低點的 P/E 反而高） |

三者 `target` 皆嚴格遞增 ⇒ 卡片是自洽的。**把 pe 納入規則會製造 3 筆恆存在的假警報，
把真警報淹掉**（同 [[kb_greek-sign-is-identity-not-independent-check]] 的教訓：
在自己 cohort 內恆觸發的閘資訊量為零，而恆誤報的規則比沒有規則更糟——它會被學會忽略）。

★ **通則：「看起來該單調」是直覺，「實測真的單調」才是不變式。立規前先全表量一次。**

### 14.3 機器守門與分工

`roma_cli val_audit` 規則 **`LADDER`（🔴 ERROR）**，判準函式 `ladder_violations()`。

⚠️ **它上線時全表 0 命中——那是對的，不是失效**：現有卡片內部自洽，
倒掛只在「套用 base-only 重估的那一刻」發生 ⇒ 它是**寫入時的回歸護欄**，不是現況偵測器。
實測：模擬把 B 群 11 檔的新 `base_eps` 套進去（不動 bear/bull）→ **LADDER 由 0 變 6、exit code 0→1**。

`val_refresh` 用**同一個** `ladder_violations()` 問「套用後會不會破」（DRY，判準只有一份），
所以提案表在你動手前就先警告，`val_audit` 則在你動手後把關。兩道都在，
是因為**提案階段的警告可以被忽略，commit 階段的 ERROR 不行**。

---

## 15. 資料源守門：三類系統性假警報（權威正文，2026-08-18 立）

> 立項：`document/todo_idea/14-08-2026_val_refresh兩類假警報守門.md`（2026-08-14 那批 9 檔重估）。
> 實作：`src/opportunities/valuation_ntm_refresh.py`、`valuation_zone_audit.py`（v4.10）。
> **2026-09-06 補第三類**（`document/todo_idea/06-09-2026_net_cash欄缺口徑宣告致第三類假警報.md`、
> 實作 v4.77）：本節標題原為「兩類」。

| 類別 | 病灶 | 判別憑據 | 實例 | 正文 |
|---|---|---|---|---|
| ① feed 損壞／覆蓋殘缺 | 資料**進來就是壞的** | 覆蓋比、`90daysAgo==0` | PANW `+1y` | §15.2 |
| ② 框架誤套 | 用**錯的公式**算對的資料 | `anchor` 欄 | SNOW 被套 P/E 路徑 | §15.4 |
| **③ 口徑未宣告** | 公式與資料**各自都對，但講的不是同一件事** | `net_cash_basis` / `base_eps_basis` 欄 | SNOW `net_cash` 的 STI↔LTI 重分類 | **§15.5.1**、§15.6 |

★ ③ 最難察覺 —— ① 有壞值形狀、② 有 `anchor` 欄可判，而 ③ **兩邊數字都健康**，
**只有把兩條機讀行（或資產負債表的相鄰兩格）擺在一起才現形**。

### 15.1 通則（最重要的一條）

> **幅度最大的提案，最需要先懷疑資料源，而不是市場。**

2026-08-14 那批四筆「幅度大」的提案：

| 標的 | 提案 | 真相 |
|---|---|---|
| COHR | +54% | ✅ 真——FY 錨位滾動 |
| MRVL | +31% | ⚠️ 一半是口徑差（純 FY2027 vs NTM blend），只有 +9.9% 是共識真的動 |
| SNOW | +27% | ❌ 框架誤套（EV/Rev 卡被套 P/E 路徑） |
| PANW | −53% | ❌ `+1y` feed 損壞 |

⇒ **四筆裡只有一筆是純粹的基本面訊號**。這與「先看幅度大的」的直覺剛好相反。

同一精神見 [[reference_yfinance_oi_zero_is_feed_failure]]、
[[reference_yfinance_volume_carries_over_stale_session]]：yfinance 的欄位在
「狀態轉換窗」（ER 後數日、FY 交界、**新覆蓋開張**）內會出現
**數值正常但語意錯位**的讀數，而且**看起來完全不可疑**。

### 15.2 `SPARSE_COVERAGE`：`+1y` 覆蓋殘缺 ≠ 一次性利益

兩者的**症狀完全相同**（`0y` > `+1y`），**病因與修法相反**：

| | 一次性利益污染（§5 舊規、GOOG/AMZN） | 覆蓋殘缺（本節新規、PANW） |
|---|---|---|
| 髒的是 | `0y`（被 MTM 利得墊高） | `+1y`（覆蓋才剛開） |
| 遠端樣本 | 正常 | n 少、分歧大、90 天前不存在 |
| 修法 | **改錨 `+1y`** 或人工剔除一次性項 | **別碰 `+1y`**（改錨 `+1y` 只會更錯） |

★ 舊文案把兩者混為一談，還直接建議「改用 `+1y` 為錨」——對 PANW 那類
正好是**把人推向壞掉的那一格**。所以這兩條旗**必須分開講**。

**觸發判準（只認「覆蓋」兩條）**：

1. 覆蓋比 `n(+1y) / n(0y)` < **0.5**　— PANW 實測 16/53 = 0.30
2. `eps_trend['+1y']['90daysAgo'] == 0`　— 該欄 90 天前**根本不存在**

**佐證（不獨立觸發）**：遠端分歧 `(high−low)/|avg|` > 50%。
⚠️ 2026-08-18 首跑實測訂正：**NVDA 遠端分歧 51.1%，覆蓋卻是 48/48 滿的**
——那是「分析師對 2027 真的意見分歧」，不是「覆蓋才剛開」。
高不確定性**照樣可以套用**（標分歧即可），資料源殘缺**不能套用**。
把分歧當獨立觸發，等於**把本卡要修的病換個方向再犯一次**。

觸發後：提案標 `hold`（表上 sym 前綴 `⚠`）＝**不可直接套用**，
先對外部共識交叉（PANW 的 Zacks FY2027 $3.98 vs 卡錨 $4.12，差 −3.4% ⇒ 框架成立）。

### 15.3 META 新欄（工具尊重卡片既有的決定）

> ★ 這條比任何判別規則都根本：**判別會漏，但「人已經判過的事」不該每輪重來。**
> PANW 在 2026-06-22 就判定 `+1y` 損壞並改錨 `forwardEps`，工具讀不到那個決定，
> 於是**每次跑都重新提一次同樣的 −52.5% 假警報**。

| 欄 | 值 | 誰讀 | 語意 |
|---|---|---|---|
| `eps_source` | `forwardEps` / `0y` / `+1y` | `val_refresh` | 本卡的 EPS 錨已由人指定，工具不重算 blend |
| `feed_reject` | 逗號分隔，如 `+1y` | `val_refresh` | 該 feed 已判定損壞；缺 `eps_source` 時退回 `0y` |
| `anchor` | `EV/Rev` / `deal_price` / …（缺值＝P/E） | `val_refresh` | **框架**別。非 P/E ⇒ 整檔跳過 |
| `net_cash` | `0.183B` | `val_refresh` | EV/Rev 卡的淨現金（**基準欄**，計入 §13 重估欄） |
| `net_cash_basis` | `cash_sti`（預設）/ `total_inv` | `val_refresh` | 上一欄的**口徑**宣告（§15.5.1）。缺值＝`cash_sti`＝現行行為 ⇒ 零回溯影響。**不計入 §13 重估欄**（它宣告口徑、不是基本面數字，同 `base_eps_basis`） |
| `base_eps_basis` | `FY27` / `NTM` | `val_audit` | 聲明 `base_eps` 的口徑；非 NTM ⇒ BASIS_MISMATCH 降 INFO |
| `shares` | `359.0M` | （目前人讀） | 目標價公式的分母；**雙層股權公司必填**（§15.7）。與 `net_cash` 同性質＝公式的**輸入**，待升格為 §13 重估欄 |
| `recheck_by` | ISO 日期 | `val_audit` | 卡片自訂的下一個複核日（**§13.6 權威正文**）|
| `guard_until` | ISO 日期／條件字串 | `val_audit` | 保守處置的**解除條件**；`eps_source`/`feed_reject`/`SPARSE_COVERAGE` 這類決定都該配一個（**§13.6**）|

⚠️ `anchor`（哪套框架）與 `fy_anchor`（哪一年）欄名相似但**語意正交**，別誤跳。

### 15.4 `anchor != P/E` 的卡不得套 P/E 路徑

SNOW META 明載 `anchor=EV/Rev`（GAAP 仍負、SBC 沉重，P/E 無意義）。
`base_pe=120` 是**由 EV/Rev 目標反解**出來的顯示值（供 ROMA Layer 0 算距離/R:R），
**不是估值框架**。`NTM_EPS × base_pe` ＝ 拿反解值去推導它自己的來源 ＝ **循環論證**。

★ 危險不在於算錯，而在於**輸出看起來完全正常**（$328.06、+26.7%）。
⇒ 跳過是唯一正確的處置；正解走營收路徑：
`fair = (EV/Rev 倍數 × NTM Rev + 淨現金) ÷ 股數`。

### 15.5 EV/Rev 卡的淨現金會過期

SNOW 舊卡寫「淨現金 ~$1.3B」，2026-08-14 實測只剩 **$0.183B**
（cash $2.955B − debt $2.772B，發債/可轉債吃掉），每股差約 **$3.2**。

★ **P/E 卡的 EPS 每輪被 `val_refresh` 重估，EV/Rev 卡的淨現金卻沒有任何機制在看。**
它一樣是會過期的基準欄，只是過期時沒有人會叫。
⇒ `net_cash` 升格為機讀欄、納入 §13 的重估欄清單，
並在 `val_refresh` 對非 P/E 卡的**跳過區**照樣印出核對結果（漂移 ≥20% 出 🔴）。

#### 15.5.1 `net_cash` 的**口徑**：這條檢查自己會製造第三型假警報（2026-09-06 立，v4.77 實作）

上一節那條檢查的「實測值」寫死成 `totalCash − totalDebt`，
而 yfinance 的 `totalCash` **只含 cash + STI，不含長期投資（LTI）**；
卡上 `net_cash=` 那一欄**也沒有任何地方說明它是用哪個口徑算的**。
⇒ 公司只要把錢在 **STI ↔ LTI 之間挪一次**，這條檢查就報一個**幅度巨大、但完全是假的**漂移。

**實例（SNOW 2026-09-06，`val_refresh` 實跑報 −329%）**：

| 項目 | Q1（04-30） | Q2（07-31） | Δ |
|---|---|---|---|
| cash + STI（＝ yfinance `totalCash`） | $2.955B | **$2.345B** | **−$0.610B** |
| **LTI**（`Investments And Advances`） | $1.432B | **$1.984B** | **＋$0.552B** |
| **總 cash＋投資** | $4.387B | $4.329B | **−$0.058B（−1.3%）** |
| totalDebt | $2.772B | $2.764B | −$0.008B |

⇒ **掉的 $0.610B 裡有 $0.552B（91%）只是搬到隔壁那一格。** 公司沒有燒錢，動的是**分類**。
而 −329% 正好落在 §15.1 那條通則的靶心上：**幅度最大的提案最需要先懷疑資料源。**

**規則**：

1. **口徑宣告欄 `net_cash_basis=cash_sti | total_inv`**（缺值＝`cash_sti`＝現行行為）。
   實測公式依該欄選：`totalCash − totalDebt`（`cash_sti`）／
   `totalCash + Investments And Advances − totalDebt`（`total_inv`）。
   ★ 同 §15.3 `eps_source` / `feed_reject` 的原則：**工具尊重卡片既有的決定。**
2. **🔴 旗標一併印 LTI 的同期變化**（不加欄、不改判準）——
   抵銷比例 ≥50% 時直接寫「多半是分類移動，不是燒錢」並指路到本節。
   抓不到 `Investments And Advances` 那一列時**退回舊文字，但不因此不印旗標**。
3. **同期原則（2026-09-07 實跑撞出，最重要的一條）**：`info` 與 `quarterly_balance_sheet`
   是**兩個端點，新鮮度不保證一致**。SNOW 09-07 實測：`info.totalCash` 已是 Q2（07-31）的 $2.345B，
   而 `quarterly_balance_sheet` 最新欄還停在 **Q1（04-30）**的 $2.955B。
   ⇒ `total_inv` 的實測值**整條算式取自同一個端點（資產負債表）**並印出 as-of；
   湊不齊就說「**本輪不給判決**」，**絕不**把 `info` 的 cash 與 bs 的長投相加。
   ★ 初版就是這樣寫的，實跑當場報出 −35% 的假漂移 —— **在修第三型的同時再犯一次第三型**。
   同理，🔴 旗標裡的 LTI 兩季一律**印出期別**，並在 bs 落後 `info` 時明說
   「這兩季不是上面漂移所在的那一季」。（同 §15.1 那條：同一資料源的不同端點誰在落後**會輪替**。）
4. 宣告了 `total_inv` 卻湊不齊資產負債表 ⇒ **不給判決**（🟡），
   **不**退回 `cash_sti` 比對 —— 兩個口徑差的正好是長期投資那一格，跨口徑比＝再造一次假警報。

**（不做）判準改用「總 cash＋投資」**：那會把分類移動整個排除在告警外，
**同時弱化「真的燒錢」的偵測**。要做得先拆成兩條旗（分類移動 vs 真實水位下降）。

⚠️ `net_cash_basis` **不進 `VALUATION_KEYS`**（§13 重估欄）：它宣告口徑、不是基本面數字，
與 `base_eps_basis` 同級。改口徑而 `net_cash` 的**數字**沒動，不該推後 `last_updated`。

### 15.6 `BASIS_MISMATCH`：`base_eps` 的單位不是它宣稱的單位

MRVL 舊 META `base_eps=4.00` ＝ **純 FY2027**，同一張卡的 `NTM_BLEND` 行卻早就寫
`ntm_eps=4.75`。README 規定 `base_eps` 應為 NTM blend ⇒ 舊 META 違規。
後果：`val_refresh` 報「+30.5% 漂移」，其中**只有 +9.9% 是共識真的動**，其餘 20.6% 是口徑差。
（同型前例：2026-08-05 ETN 那筆「大半是 FY26 單年→NTM blend 的口徑改正」。）

`val_audit` 的 🟠 `BASIS_MISMATCH`：兩欄相差 > **2%** 即報。
★ **純靜態、零外部依賴**——但這種病在單一數字上看不出來，
**只有把同一張卡的兩條機讀行擺在一起才現形**。

修法有兩條，工具**不替人選**：
① 把 `META.base_eps` 換成真正的 NTM blend（並連動 zone/target）；
② 用 `base_eps_basis=FY27` 明說它刻意不是（NVDA 走這條：zone 錨 FY27 base_target 287）。

刻意設為 WARN 而非 ERROR：立規當下全庫 4 檔命中，設 ERROR 會當場把 `run_all` 弄紅、
**逼人在沒想清楚前草率改估值**——那比留著債更糟。

#### 15.6.1 存量 4 檔的裁決結果（2026-08-30 結案）

| 卡 | 舊 `base_eps` | `ntm_eps` | 差 | 裁決 | 結果 |
|---|---|---|---|---|---|
| NVDA | — | — | — | **②** 聲明 `base_eps_basis=FY27` | 2026-08-18 隨立規當日處理，降 INFO |
| DDOG | 2.68 | 2.59 | −3.4% | —（自然消解） | 2026-08-30 post-ER refresh 後兩欄同為 **2.82**，差 0% |
| **MU** | 112（純 FY27） | 105 | −6.2% | **①** user 2026-08-30 裁決 | `base_eps`→105、`base_target`/`zone_fair`→945、zone→662/803 |
| **MDB** | 6.7（來源不明） | 7.73 | +15.4% | **①** user 2026-08-30 裁決 | `base_eps`→7.73、`base_target`/`zone_fair`→387、zone→271/329 |

⇒ `BASIS_MISMATCH` 的 WARN 由 **3 清到 0**（剩 NVDA 一筆已聲明的 INFO）。

★ **執行時撞出的一條邊界：修法① 動了基準欄，但 `last_updated` 不動。**
§13.1 的表寫「基準欄任一改變 ⇒ ✅ 要動 `last_updated`」，照字面 MU/MDB 都該推到 2026-08-30。
**那是錯的**——修法① 抄進 META 的 `ntm_eps` 是卡片**自己早就算好**的值
（MU 的 105 算於 2026-07-01、MDB 的 7.73 算於 2026-06-04），今天沒有任何新資料進來。
推後日期會製造 §13.2 第 2 點那個後果：**一張 60 天沒重估的卡（MU）被重置 `AGE` 時鐘、假裝新鮮**，
而它恰恰是全庫最需要重估的一張（見下）。
⇒ **判準補一列**：「把同卡 `NTM_BLEND` 的既有值抄進 META（口徑對齊）」⇒ **❌ 不動**，
與表中「把既有分析首次抄進主表建卡 ⇒ 填原分析的計算日」同一精神——
**`last_updated` 記的是那個數字被算出來的日子，不是它被搬到哪一行的日子。**

★ **第二條：口徑對齊 ≠ 重估，兩者不可互相冒充。**
同日 `val_refresh` 對兩檔都提出了**真正的**重估提案，兩筆都**刻意未套用**：

- **MU**：當前共識 NTM EPS **155.03**（+38% vs 105）。套進去會破 §14 階梯（base 155 > bull 125，
  `LADDER` 🔴）⇒ bear/bull 要一起重想；且 FY2 分歧 74%、`cyclical=deep` 屬 §3 不適用條件。
  留給 2026-09-24 Q4 FY26 財報。
- **MDB**：權重滾動後（FY27 7/12 done，w_fy1 0.67→0.42）NTM EPS 掉到 **6.83**（−11.6%）⇒ fair $342。
  留給 2026-09-03 Q2 FY27 財報。

⇒ 清掉 `BASIS_MISMATCH` **不代表這兩張卡的數字現在是對的**，只代表**同一張卡的兩條機讀行不再互相矛盾**。
這條規則量的是內部一致性，`AGE` / `ER_PAST` 才量新鮮度——**別把前者的綠燈讀成後者的綠燈**。

---

### 15.7 雙層股權的股數陷阱：`sharesOutstanding` 只回 Class A（2026-09-06 立）

**病灶**：yfinance `info["sharesOutstanding"]` 對 dual-class 公司**只回 Class A**。
EV/Rev 卡的目標價公式 `fair = (倍數 × NTM Rev + 淨現金) ÷ 股數`（§15.4）直接吃這個分母
⇒ **股數低估多少，每股目標就高估多少**。

**已知兩例，相隔 24 天**：

| 卡 | `sharesOutstanding` | 實際 A+B | 低估 | 後果 |
|---|---|---|---|---|
| WDAY（2026-08-30 記下） | 196M | **241.0M**（卡上寫 ~247M） | **18.7%** | 市值被低估近兩成（該卡當時**自己抓到了**，寫在敘述裡） |
| DDOG（2026-09-06 抓到） | 334.9M | **359.0M** | 7.2% | 三檔目標全高估 7.2%、分級由 `above_waiting` 誤標成 `in_waiting`、R:R 由 0.92 虛胖成 1.35 |

★ **這條規則存在的唯一理由是：WDAY 已經抓到過一次，但只寫在自己卡裡、沒有升格成規則，
於是 DDOG 照樣中招。** 個案敘述不會保護下一張卡 —— 這正是 §15.1 通則的精神。

**判別（三路互證；2026-09-06 補第 3 路）**：
1. 資產負債表 `Ordinary Shares Number` / `Share Issued`（`Ticker.quarterly_balance_sheet`）
2. `info["marketCap"] ÷ info["currentPrice"]` 反推
3. **`(info["enterpriseValue"] − totalDebt + totalCash) ÷ px` 反解**
與 `sharesOutstanding` 有落差 ⇒ **一律採較大的那個**（見下「為什麼取最大」）。

★ **第 3 路是為了另一種病灶加的：股數單純過期**。
`sharesOutstanding` 有**兩種**偏低方式，而第 1、2 路只抓得到第一種：

| | 病灶 | 第 2 路（`marketCap÷px`）抓得到？ | 實例 |
|---|---|---|---|
| A | dual-class 只回 Class A | ✅ 抓得到（marketCap 用 A+B） | DDOG −7.2%、WDAY −18.7% |
| **B** | **股數過期**（`sharesOutstanding` 停在上一季） | ❌ **抓不到** —— marketCap 用的是**同一份舊股數**，兩路逐位吻合 | SNOW 346.6M vs 10-Q 封面 352.8M（−1.8%） |

SNOW 2026-09-06 實測：同一份 `info` 裡 **`marketCap` 用舊股數、`enterpriseValue` 用新股數**
（相差 $2.4B）⇒ 第 3 路反解得 **352.4M**，與 10-Q 封面 352.8M 吻合。
**不必開 10-Q 就能先發現兩欄打架**——這條對所有 EV/Rev 卡都適用。
⚠️ 反過來說，「第 1、2 路逐位吻合」**不是**股數正確的證據
（SNOW 那張卡當時就是這樣寫的，而它其實已經過期一季）。

★ **為什麼取最大**：兩種已知病灶**都讓 `sharesOutstanding` 偏低**，沒有已知的反向病例。
這是從病灶推出來的規則，不是保守；分歧一律標旗（門檻 1%，比最小的已知病例 1.8% 再嚴一級），
工具選一個能跑的分母，**要不要去翻 10-Q 封面由人決定**。卡片已填 `shares=` 時以卡片為準
（§15.3「人已經判過的事不重來」），但分歧照樣標旗——卡上的股數自己也會過期（WDAY 的 `~247M`）。

**適用範圍不只 EV/Rev 卡**：任何「用市值/EV 推每股」的路徑都中招，
包括 §15.5 淨現金漂移的**每股衝擊**換算。

⚠️ **P/E 卡不受影響**（EPS 共識本身已是 per-share，分母不經手），
所以這個病**只在非 P/E 路徑上發作** —— 而那正是最少人複核的一群卡。

**✅ 工具層（v4.77，2026-09-06 修）**：
`valuation_ntm_refresh.shares_flags()` 實作上面的三路互證（＋卡上 `shares=` 共四路），
`net_cash_flags()` 的每股衝擊改吃它選出的分母（§15.5）。
旗標**只掛在 `anchor != P/E` 的卡**——P/E 卡的共識已是 per-share，分母不經手（見下）。
⚠️ 仍未做：把 `shares` 納入 `valuation_zone_audit.VALUATION_KEYS`（與 `net_cash` 同級）——
那會動 §13 history 稽核的**回溯面**（`net_cash` 立規時全庫沒有卡填該欄，`shares` 現在 DDOG/SNOW 都有值），
且與 §15.6.1「口徑對齊 ≠ 重估」的邊界糾纏 ⇒ 留為卡片
`document/todo_idea/06-09-2026_net_cash欄缺口徑宣告致第三類假警報.md` 的尾巴 ⑤。

⚠️ **順帶：WDAY 卡上的 `~247M` 本身也已過期** —— 248,973,479（2026-04-30）→ **241,000,000**（2026-07-31，回購）。
`marketCap ÷ px` 反推亦為 241.0M。該卡下次重估時應一併更新（本次不動別人的卡）。

**全庫現況（2026-09-06 掃描）**：`anchor=EV/Rev` 的卡只有 **DDOG / SNOW** 兩張。
~~SNOW 用 346.6M，與 `marketCap ÷ px` 反推逐位吻合（單一股權級別）⇒ 未受影響。~~
⚠️ **同日訂正**：那句話正是上表病灶 B 的示範——兩路吻合只證明它們用同一份股數。
SNOW 實際已過期一季（346.6M → 10-Q 封面 **352.8M**），由第 3 路（EV 反解 352.4M）抓到，
卡上已改填 `shares=352.8M`。

---

## 16. 現價隱含 P/E vs 我方 `base_pe`（權威正文，2026-08-19 立）

§12.3 的自我檢查「若結論與 implied P/E 明顯矛盾 ⇒ 先查框架自己」立了三個月，
一直**只是人工守則**：2026-07-28 那批重估後有 4 檔踩到它（NFLX −41%／CRM −35%／
FN −28%／LLY −26%），全表沒有任何規則出聲。本節把它變成機器規則。
（卡：`document/todo_idea/15-07-2026_估值zone欄壞卡盤點與折價帶對齊.md` 待辦⑩）

### 16.1 `PE_IMPLIED_GAP`（🟠 WARN，單側）

```
gap = 現價 ÷ eps ÷ base_pe − 1   eps 序：NTM_BLEND.ntm_eps → META 行內 ntm_eps → base_eps
告警條件（兩個都要成立）：gap ≤ −25%   且   現價 < zone_lo（＝分級 super_oversold）
```

意思是「**卡片正在輸出一個『深度超跌』讀數，而它的來源是我方的倍數假設**」。
這條要求的是**寫出理由與可證偽點**，不是自動下修 `base_pe`
（[[feedback_conservative_base_pe_no_rerating]] 管的是禁止**上**修；反向也沒有自動修法）。

**★★ 第二條件在 v4.21 換過一次 —— 本節最重要的一課**
v4.16 原本寫的是 `現價隱含 P/E < 卡上 bear_pe`（「連我方最悲觀倍數市場都沒付」）。
它讀起來很合理，但**口徑是錯的**：`bear_pe` 是對 `bear_eps` 定義的，`implied_pe` 是對 NTM EPS 算的，
兩者分母不同年、不同情境 ⇒ 比值不可比。實測後果（2026-08-19 逐檔覆核抓到）：

| 型 | 標的 | 舊判準 | 實情 |
|---|---|---|---|
| 假陽性 | **NVDA** | NTM 基準 19.8x < bear 22x ⇒ 告警 | 卡上 `base_eps_basis=FY27`，同基準是 **24.5x > 22x**；且分級是 `in_waiting`（219.6 > zone_lo 201）＝**沒有傷害** |
| 假陰性 | **FN / CRM** | implied 高於自家 bear_pe ⇒ 靜默放過 | 兩檔都 `super_oversold`，傷害是真的 |

★ 而 **FN／CRM 正是本規則立項時點名的 4 檔中的 2 檔**（NFLX/CRM/FN/LLY）
⇒ **舊判準漏掉自己創始樣本的一半**，這是判準寫錯軸最硬的證據。
**通則：判準要用「傷害怎麼定義」的那個單位去寫，不要用看起來相關的另一個軸。**
（這裡傷害是「分級落 super_oversold」＝價格 vs zone，所以判準也要用價格 vs zone。）
`bear_pe` 仍印在訊息裡當對照，但訊息會明說它**不是判準**。

### 16.2 ★ 為什麼只查負向、以及為什麼要兩個條件（立規前先量全表）

**全表量測（2026-08-19，49 檔可算）**：
`p5 −35.8%｜p25 −15.9%｜median +0.7%｜p75 +16.7%｜p95 +91.0%`（sd 33.9%）。

- **正向側刻意不查**：>+20% 有 10 檔（INTC +94%／CRWD +101%／PANW +102%／半導體整群），
  而「市場付的倍數遠高於我方 `base_pe`」正是保守 `base_pe` 政策的**設計輸出**。
  在那個 cohort 內近乎恆真的閘＝資訊量趨零（同 [[kb_greek-sign-is-identity-not-independent-check]]）。
- **幅度門檻（gap ≤ −25%）只對「淺帶」卡有作用**：高β 帶 `lo/fair=0.70` 的卡，
  `現價 < zone_lo` 已蘊含 gap ≤ −30%（門檻多餘）；但低β／ETF 帶 `lo/fair=0.80~0.92` 的卡
  可以在 gap 只有 −9% 時就 `super_oversold` ⇒ 門檻擋的是那一類。
  ⚠️ 2026-08-19 實測它對現況**不 binding**（7 檔 super_oversold 的 gap 全 ≤ −27%）。
  若長期完全不 binding，**該刪不該留**（同 §14.2：恆真的閘資訊量為零）。

2026-08-19 全表命中 **7 檔**：ORCL −37%／INTU −36%／NFLX −34%／META −34%／
LLY −29%／FN −27%／CRM −27%（判準換掉後 NVDA、SNPS 退出，見上表與 §16.5）。

### 16.3 價源新鮮度在這條規則裡是**正負號問題**

價源優先序：**注入價源（`roma_cli val_audit` 預設接 SG data_table 現價）**
→ META `mkt_px`（**限 10 天內**）→ 都沒有就報 🟡 `PE_GAP_NA`（顯式，不靜默跳過）。

理由是實測的：META `mkt_px` 是**手寫快照欄、無人自動刷新**（51 卡只有 19 卡有值，
其中 3 卡停在 06-30）。拿過期值算 gap 會**翻號**——
`MDB −13.1% → +12.5%`（Δ25.5pp）、`MU +22.1% → −0.4%`（Δ22.6pp）、`CRM Δ14.8pp`。
⇒ 過期價一律判「不可評估」，不硬算；報告抬頭一定印出價源場次
（SG data_table 停更時 `Current Price` 也會凍結，價齡必須看得見）。

### 16.5 命中之後怎麼處理（2026-08-19 首批七檔實作出來的流程）

**規則只負責點名，不負責裁決。** 命中後照這個順序走，**前三步都在查我方自己**：

| 步 | 問題 | 工具 | 2026-08-19 首批結果 |
|---|---|---|---|
| 1 | 是不是**判準/格式假象**？ | 逐檔覆核 | **2 檔**：NVDA（判準口徑錯，見 §16.2）、SNPS（`ntm_eps` 寫在 META 行 ⇒ 用錯分母） |
| 2 | 是不是 **EPS 過期**？ | `val_refresh` ＋ ER 日曆 | **1 檔**：FN（08-18 年報後重估，NTM +5.9%） |
| 3 | 是不是 **NTM 口徑效應**？ | 用**當期 FY** 再算一次 | **1 檔**：LLY（NTM 把 FY27 的 +29% 跳升前置；當期 FY 算是 33.4x，不會觸發） |
| 4 | 街口 EPS **在往哪走**？ | `eps_trend` 0y/+1y 的 90 天軌跡 | 上修＝純倍數爭議（INTU/FN）；**不動**＝分子還沒被砍、便宜是假的（ORCL） |
| 5 | 是**個股**還是**板塊**？ | 同日板塊 ETF 的隱含倍數 | INTU 12.8x vs `IGV` 26.6x ⇒ 個股專屬折價 |
| 6 | 到這裡才輪到**倍數裁決** | user | de-rate：NFLX 32x→24x、META 25x→20x｜維持：LLY 40x、ORCL 26x（等 ER） |

★ **多數命中不需要動倍數**：首批 7 檔裡只有 **2 檔**走到第 6 步，另外 5 檔分別是
判準假象（2）、格式假象（1）、EPS 過期（1）、口徑效應（1）＋「等 ER」。

**`pe_gap_reviewed=<ISO>`（META 新欄）**
判讀寫進卡片後掛這個欄 ⇒ 規則降為 🟡 INFO（同 `base_eps_basis` 的處理：人已經判過，不該每次重報）。
★ **但豁免有到期日**：`next_earnings` 一過就自動轉回 🟠 ——
因為卡片自己寫的可證偽點就是下一次財報。判不出 ER 日（sentinel／髒格式）一律維持 🟠：
**沒有到期日的豁免＝永久豁免**，那會讓規則退化成裝飾。

**卡片要寫的四件事**（首批七檔都照這個格式）：
① 事實（現價、隱含倍數、距 52w 高）② 診斷（EPS 軸還是倍數軸、個股還是板塊）
③ 處置（動什麼／不動什麼／等什麼）④ **可證偽點**（哪一天、哪個數字會推翻這個判斷）。
⚠️ ④ 不能寫成「股價漲回來就算對」——**倍數不因股價回升而回調**，只因新的基本面資訊而改。

### 16.4 `TABLE_PE_DRIFT`：同一張卡的第三種拷貝漂移

估值卡正文有一張「保守／合理／樂觀 ×（Nx）」表給**人**讀，META 行的
`bear_pe/base_pe/bull_pe` 給**機器**讀。兩份拷貝會各自漂——這是同一條債的第三次現形：

| 型態 | 誰跟誰漂 | 立規/處置 |
|---|---|---|
| ⑥ | 主表 META vs 明細卡 META | `DETAIL_DRIFT`（2026-07-21） |
| ⑥″ | 同一份文件的 META 行 vs 散文行 | 人工（稽核盲區） |
| **⑩ 後半** | **同一張卡的 META 行 vs 正文表頭** | **`TABLE_PE_DRIFT`（本節）** |

- **只在抓得到標準表頭時才判**（2026-08-19：51 卡有 37 張）。ETF／指數／EV-Rev 卡格式不同 ⇒
  靜默跳過；**猜非標準格式會讓稽核自己變成雜訊源**。
- **只看第一張表**：CRWD 型卡把 pre-split 舊表封存在 `<details>`，那是刻意保留的歷史。
- **例外要靠聲明取得**：META 卡的表頭「街口/保守（20x）」是**市場當前壓縮倍數**（誠實地板錨），
  不是 `bear_pe` 18x ⇒ 掛 `table_pe_basis=street_compressed_20x`，規則降為 🟡 INFO
  （同 `base_eps_basis` 的處理：人已經判過，不該每次重報）。
- **立規當下 12 檔不一致，其中只有 1 檔有正當理由**（META 卡）。
  ★ 更值得記的是：2026-07-28 已經**人工**對齊過 10 檔，三週後又漂掉 12 檔
  （GOOG/ANET/LIN 正是 08-05 重估時重新漂掉的）⇒ **人工清一次撐不過三週**。

**修法：META 為權威，改表頭並重算該欄**（12 檔的 META 皆已自洽 `target = eps × pe`，逐檔驗過）。
**例外：倍數壓縮型的卡要改表格結構、不是改數字**（ORCL，2026-08-19 裁決）——
`bull_pe 25x < base_pe 26x` 是刻意建模（bull 的價差全部來自 EPS），塞進「同一 EPS × 三倍數」
的 grid 會出現「樂觀欄低於合理欄」，舊表因此擅自把樂觀欄寫成 32x。
改為**逐情境各用自己的 EPS 與倍數**後，壓縮建模顯示得出來，表頭也不再需要一個對不上 META 的數字
（同 §14.2 不查 pe 軸的理由）。這類卡沒有標準表頭 ⇒ 本規則自動跳過，不需要 `table_pe_basis=` 豁免。
⚠️ 純顯示層修正**不動 `last_updated`**（§13.1：只有重估才動）。
⚠️ **明細卡不要只修表頭**：9 張明細卡的 EPS 是舊 vintage（TSM $16.30 vs 主表 $17.45…），
單修表頭就會踩 ⑥′ 那條「一張過期的表往往同時過期在兩個軸上，只修被指派的那個軸
會造出**看起來已更新、實際更難察覺錯誤**的文件」。
