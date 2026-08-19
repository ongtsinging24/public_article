# FP p9 極端 greek 的前瞻報酬 —— 「賣方三件套」沒有 edge，反而是「真買 call」逆向有效

**日期**：2026-07-25
**主題**：把 FP `sig_positions`(p9) 的 (d%'ile, g%'ile) 象限當訊號，實測 1/5/10 交易日前瞻報酬
**起因**：[[24-07-2026_FP_TREND_ALL]] 建立了「`+d / −g / −v` ⇒ 賣方結構（賣 put／covered call）」的判讀，
並在卡上留了「若後續持續有效，值得沉澱為長青筆記」。本篇即該項的結案。

> ⚠️ **本篇對 [[24-07-2026_FP_TREND_ALL]] 與 [[25-07-2026_FP_TREND_ALL]] 的判讀框架提出部分證偽**：
> 「+d/−g/−v ⇒ 賣方結構」作為**分類**是對的（且根本不需要驗證，它是恆等式），
> 但把它當**方向訊號**用（「封頂潮 ⇒ 後續漲不動」）**沒有實證支持**。
> 真正有統計顯著性的，是它的**鏡像**：d 與 g **同時**極高（＝真的在大買 call）→ **後續下跌**。
> 已回頭在 [[24-07-2026_FP_TREND_ALL]] 加註記。

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| **FP** | FlowPatrol（SpotGamma 盤後選擇權流量 PDF） |
| **p9 / sig_positions** | Statistically Significant Positions —— SG 自算的 **symbol 層淨額**（含 %'ile） |
| **d\$ / g\$ / v\$** | `$ Delta / Gamma / Vega Chg`，**皆買方側（BuySide）** |
| **%'ile** | 同標的自身歷史百分位（0–100），≤5 極空 / ≥95 極多 |
| **session** | FP 資料 as-of 收盤日（＝publish − 1td），非 publish 日 |
| **td** | trading day（交易日） |
| **CI** | Confidence Interval；本篇 proportion 用 Wilson，另附 **cluster bootstrap by symbol（5,000 次）** |
| **cohort** | 符合某條件的觀測子集 |
| **ER** | Earnings Report（財報） |

---

## 1. 理論框架：哪一段需要驗證、哪一段不需要

### 1.1 分類那一段是**恆等式**，不需要驗證

官方教材已把 (買/賣 × call/put) → greek 符號定義死：**買進選擇權（不論 call/put）＝ 正 gamma；賣出＝負 gamma**；
call 正 delta、put 負 delta。四個象限完全被決定：

| 買方側動作 | d\$ | g\$ | v\$ |
|---|---|---|---|
| 買 call | + | + | + |
| **賣 put** | **+** | **−** | **−** |
| 買 put | − | + | + |
| 賣 call | − | − | − |

∴「看到 +d/−g/−v 就判賣 put（或 covered call）」**是代數推導，不是實證發現**。
這點 [[kb_greek-sign-is-identity-not-independent-check]] 已定案（拿 greek 驗 greek 恆真）。
本篇**不重複**驗證分類，只驗證**它有沒有前瞻預測力**。

### 1.2 真正的 research question

> **給定 p9 上某 sym 落在某個 (d%, g%) 象限，它接下來 1/5/10 td 的報酬，和「同期間同母體」的對照組比，有沒有差？**

四個可測象限（用百分位而非原始符號，因為 p9 只給 symbol 層淨額）：

| cohort | 條件 | 結構含義 |
|---|---|---|
| **A** | d ≥95th **且** g ≤5th | 賣方三件套（賣 put／covered call／封頂） |
| **B** | d ≥95th **且** g ≥95th | 真買 call（長 gamma 偏多） |
| **C** | d ≥95th（不看 g） | 「delta 極多＝看多」的**天真讀法** |
| **D** | d ≤5th **且** g ≥95th | 真買 put（長 gamma 偏空） |
| **E** | d ≤5th（不看 g） | 天真讀法的反面 |

---

## 2. 實驗設計

| 項目 | 設定 |
|---|---|
| 樣本 | 全部 136 份 `flowpatrol_*.log` → 依 `session_date` 去重後 **131 個 session**，其中 86 個有 p9 段 |
| 樣本期 | **2026-01-06 → 2026-07-23**（約 6.5 個月） |
| 觀測 | p9 列 **n=658**（133 個 sym；SPX/VIX/XSP 無 yfinance 對應，自動剔除） |
| t0 | **session 收盤日**（＝FP 資料 as-of 日，非 publish 日）——用 publish 日會多算 1td 的前瞻資訊 |
| 報酬 | `close(t0+k td) / close(t0) − 1`，k ∈ {1, 5, 10}；價格 yfinance auto_adjust |
| **對照組（關鍵）** | **同期間、同 p9 母體的全部列**。⚠️ 不用 50% 當隨機基準（[[feedback_hitrate_needs_conditional_baseline]]） |
| regime 對照 | 同窗 SPY 報酬；另做「cohort 報酬 − **當日 p9 中位數**」的超額，剝掉當日大盤 |
| CI | proportion 用 Wilson 95%；並對 cohort A/B/BASELINE 另跑 **cluster bootstrap by symbol**（同 sym 多次上榜彼此相依，重抽 sym 整群） |

腳本：`py_dir/fp_trend/exp_sellside_triplet.py`（見附錄）。

---

## 3. 結果

### 3.1 主表（P(>0)＝報酬為正的比率）

**前瞻 5 td：**

| cohort | n | mean | median | P(>0) | Wilson 95% CI |
|---|---|---|---|---|---|
| **BASELINE 全 p9 列** | 597 | +0.77% | +0.13% | **51.3%** | [47.3, 55.2] |
| SPY 同窗（regime） | 630 | +0.27% | +0.40% | 56.3% | [52.4, 60.2] |
| **A 賣方三件套 (d≥95 & g≤5)** | 17 | +1.13% | +0.19% | **52.9%** | [31.0, 73.8] |
| **B 真買 call (d≥95 & g≥95)** | 36 | **−2.49%** | −1.00% | **25.0%** | **[13.8, 41.1]** |
| C 只看 d 極高 (d≥95) | 145 | +0.22% | +0.11% | 51.0% | [43.0, 59.0] |
| D 真買 put (d≤5 & g≥95) | 21 | +2.95% | +2.23% | 61.9% | [40.9, 79.2] |
| E 只看 d 極低 (d≤5) | 134 | +1.12% | −0.23% | 47.0% | [38.8, 55.4] |

**1 td / 10 td（摘要）：**

| cohort | 1td mean / P(>0) | 10td mean / P(>0) |
|---|---|---|
| BASELINE | +0.30% / 52.1% | +0.75% / 53.1% |
| **B 真買 call** | **−0.69% / 32.4%** | **−4.20% / 34.3%** |
| A 賣方三件套 | +1.39% / 61.9% | −0.38% / 60.0% |
| D 真買 put | +1.13% / 72.7% | +3.57% / 66.7% |

### 3.2 剝掉當日 regime（cohort 報酬 − 當日 p9 中位數，5td）

| cohort | n | mean 超額 | P(>0) |
|---|---|---|---|
| A 賣方三件套 | 17 | +0.48% | 52.9% |
| **B 真買 call** | 36 | **−2.44%** | **25.0%** |
| C 只看 d 極高 | 145 | −0.71% | 40.0% |
| D 真買 put | 21 | **−0.56%** | 38.1% |
| E 只看 d 極低 | 134 | −0.17% | 38.1% |

> **D 的 raw +2.95% 在剝掉當日中位數後翻負** ⇒ D 的「亮眼」全是**當日 regime**（那些日子整個 p9 母體都在漲），
> **不是 cohort 特性**。B 的負值則在剝掉 regime 後**幾乎不變**（−2.49% → −2.44%）⇒ 是 cohort 自身效應。

### 3.3 穩健性（cohort B）

| 檢查 | 結果 |
|---|---|
| 是否單一事件叢集 | ❌ 不是：**29 個 session × 33 個 sym**（36 列）；最高重複 EWZ×3、CRWV×2，其餘皆 ×1 |
| 每 sym 只取首次 | n=33，mean **−2.37%**、P(>0) **27.3%** [15.1, 44.2] |
| 子期間 1–4 月 | n=13，mean −2.51%、P(>0) 38.5%（同期 BASELINE +0.88% / 55.5%） |
| 子期間 5–7 月 | n=23，mean −2.49%、P(>0) **17.4%**（同期 BASELINE +0.71% / 49.0%） |
| **cluster bootstrap by sym（5,000×，5td）** | **B：P(>0) CI [11.1, 40.5]、mean CI [−4.64%, −0.38%]** |
| 同法 A | **A：P(>0) CI [33.3, 75.0]、mean CI [+0.07%, +2.30%]** |
| 同法 BASELINE | **P(>0) CI [46.8, 55.4]、mean CI [+0.02%, +1.60%]** |

**B 的 CI 與 BASELINE 完全不重疊，且 mean CI 不含 0；A 的 CI 把 BASELINE 整個包住。**

---

## 4. 結論與行動

### 4.1 三條結論

1. **A（賣方三件套）沒有前瞻 edge。** n=17、P(>0) 52.9%、CI [31, 74] 把對照組 51.3% 整個包住。
   ∴「封頂潮 ⇒ 之後漲不動」在本樣本期**不成立**。它仍是**正確的結構描述**（拿來讀「機構願意在哪接刀／上檔賣在哪」有價值），
   但**不能當方向訊號下單**。
2. **B（d 與 g 同時極高＝真的在大買 call）是本實驗唯一顯著者，而且是反向的**：5td mean −2.49%、P(>0) 25%，
   1/5/10 td 三個天期同向、兩個子期間同向、cluster bootstrap 後 CI 仍不重疊。
   **看到 p9 某 sym d≥95 且 g≥95，不要跟單，反而該視為短期過熱。**
3. **「d 極高＝看多」的天真讀法（C）比對照組還差**（5td 超額 P(>0) **40.0%** vs 對照組定義上的 ~50%）。
   這一點**支持** [[24-07-2026_FP_TREND_ALL]] 原本的告誡「不要把 d 極多當多頭」——
   **但理由不是「因為它是賣方結構」，而是「極端 delta cohort 整體就是負 edge」**。

### 4.2 ROMA 程式對照（line 現查於 2026-07-25，非憑記憶）

| 位置 | 現況 | 本篇的意涵 |
|---|---|---|
| `romasys/src/opportunities/sg_signals/flowpatrol/alpha.py:180-186` | p9 只讀 `delta_pct`：**≥70 → bull、≤30 → bear**，**完全不看 `gamma_pct`** | 🔴 **這正是 cohort C 的天真讀法**。實測 d≥95 的 5td 超額 P(>0) 僅 40%；而其中 d&g 同高的子集（B）方向是**反的** → 現行 tag 對 B 子集**貼反標籤** |
| `romasys/src/opportunities/sg_loaders/flowpatrol.py:120-129`（`FPSigPosition`） | 已同時解析 `gamma_pct` / `vega_pct`，**資料是現成的** | ✅ 修法不需改 loader，只需在 alpha 層加 gamma 條件 |
| `romasys/src/opportunities/sg_signals/flowpatrol/fp_scan.py:254`（`_GREEKS_EXPECTED_SIGN`） | (side, type) → greek 符號的恆等式表 | 佐證 §1.1：分類那段是代數，不是實證 |
| `romasys/src/opportunities/sg_loaders/flowpatrol.py:314`（`flow_direction`）／`:498`（`contract_direction`） | 優先序 g\$ > v\$ > d\$ > prem | 合約層方向來源；與本篇 symbol 層 p9 是兩個不同層次，勿混用 |

### 4.3 建議動作

- ☐ **ROMA**：`alpha.py:180-186` 加 gamma 條件——`d≥95 且 g≥95` 時**不要**加 bull tag（至少降權或改標 `overheated`）。
  ⚠️ 上線前先跑 outcome_updater → outcome_stats 對照（[[project_outcome_stats_needs_updater_first]]），且 decided<30 不採信。
- ☐ **人工判讀**：FP_TREND / 策略卡上看到 p9 `d≥95 & g≥95`，寫成「**短期過熱**」而非「機構偏多」。
- ✅ **保留**：A 象限繼續當**結構描述**用（找機構的接刀價與上檔天花板），不當方向訊號。

---

## 5. 待辦 / 本篇的已知弱點（誠實清單）

1. **樣本期只有 6.5 個月、單一 regime**（SPY 同窗均值皆正，屬多頭偏移環境）。**沒有空頭樣本**，B 的反向 edge 可能是「多頭市場中追高被修理」的特例。
2. **未控制 ER**：極端長 gamma 流量常叢集在財報前後，B 的負報酬可能有一部分是 **post-ER IV crush + 財報後漂移**，而非「買 call 本身是反指標」。
   → **下一步**：把 ER 日期併進來，分「ER±3td 內」與「非 ER」兩組重跑。
3. **多重比較未校正**：5 cohorts × 3 天期 = 15 個檢定。B 在三個天期＋兩個子期間都同向，降低了偶然性，但**未做 Bonferroni／FDR**。
4. **n 偏小**：A 只有 17 列、D 21 列，任何關於 A/D 的「無效」結論都應讀成「**本樣本沒測出效應**」，不是「證明無效」。
5. **p9 是 SG 的黑箱 aggregate**：百分位的母體與視窗未公開；只能當「SG 認為異常」的代理。
6. **43 份舊 log 的 session 是回推的**（`publish − 1td`，因舊版 dumper 無 `session_date` 表頭）。碰上非交易日重發會有 ±1td 誤差。
   → **下一步**：只留 header 來源的 session 重跑一次，看結論是否穩定。

---

## 附錄：腳本路徑

| 檔案 | 用途 |
|---|---|
| `py_dir/fp_trend/fp_trend.py` | 掃 136 份 FP log → 依 `session_date` 去重（缺表頭時用 `trading_days.json` 回推 publish−1td，標 `session_src`）→ `fp_trend.json` |
| `py_dir/fp_trend/rpt.py` | 檢視器：`sector` / `sig` / `sym` / `rows SYM` / `newmover` |
| **`py_dir/fp_trend/exp_sellside_triplet.py`** | **本篇實驗**：cohort × 前瞻報酬 × Wilson CI × cluster bootstrap by sym × 子期間拆分 |
| `py_dir/fp_trend/trading_days.json` | 交易日曆快取（^GSPC，2025-11-03~2026-07-24） |
| `py_dir/fp_trend/prices_cache.json` | 價格快取（134 sym） |

重跑：

```bash
cd py_dir/fp_trend
python3 fp_trend.py --since 2026-01-01     # → fp_trend.json（131 sessions）
python3 exp_sellside_triplet.py            # 讀快取；--refresh 重抓價格
```

> 過程中修掉一個解析 bug：k=v 正則的 lookahead 用 `\s+`，遇到**空值欄位**（`spread=` 後直接接 `dir=`）
> 會把下一個 k=v 整個吞進值裡 → **方向判決 `dir=` 整欄遺失**。已改為 `\s*`（`fp_trend.py` KV_RE）。

---

## 關聯

[[kb_greek-sign-is-identity-not-independent-check]]（分類是恆等式的官方層定案，本篇的前提）｜

---

## 📌 2026-07-31 後續：擴大樣本已複測並推廣

本篇只測 p9 子集（658 列）。[[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] 把樣本擴到**全 FP section**（4,037 列 / 216 檔 / 48 天，依 session_date 去重），結論：

- 本篇「買 call ≠ 機構偏多、應寫短期過熱」**成立且推廣**（上 call 榜 T+1 44.1% / T+5 41.2%，對照組 48.7% / 47.2%，CI 不重疊）
- **新增更基本的一層**：`dir=` 的**買/賣軸零預測力**（買 CALL 44.1% vs 賣 CALL 43.4%）→ 有訊息的是 **C/P 軸**，不是 BUY/SELL
- ⚠️ **但保守口徑下顯著性消失**：列層級 CI 因**偽重複**假性變窄；標的層級（n=85/60）兩效應皆不顯著。本篇的 cluster bootstrap 慣例是對的，方向應繼續沿用

---

[[kb_fp-toplists-are-not-trade-tape]]（為何 symbol 層只能用 p9、不能加總 p3–p6）｜
[[kb_fp-greek-sign-convention]]｜[[kb_fp-spread-label-vs-greek-sign]]｜
[[24-07-2026_FP_TREND_ALL]]（本篇部分證偽其方向性用法）｜[[25-07-2026_FP_TREND_ALL]]（結案回標於其 §七）｜
[[feedback_hitrate_needs_conditional_baseline]]（對照組不得用 50%）｜
[[project_outcome_stats_needs_updater_first]]（若要把結論接進 ROMA 的驗證前置條件）｜
[[22-07-2026_CC_MFI_vs_OBV四象限與週線OBV實證]]（同型：指標有效度實證＋cluster bootstrap 慣例）
