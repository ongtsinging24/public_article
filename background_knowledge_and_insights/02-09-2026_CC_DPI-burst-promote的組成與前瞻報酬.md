# ruleB `dpi_burst` 的組成與前瞻報酬 —— 六成是產不出水位的 ETF，而 edge 在獨立窗校正後全數跨零

**日期**：2026-09-02
**主題**：拆解 `roma_cli scout` [BUILDUP] 段 ruleB（DPI ≥ 85）的名單構成，並實測「單日 DPI burst」
相對**同日／同流動性閘／DPI < 85** 全市場對照組的 close-to-close 前瞻報酬
**起因**：user 問「解釋這段數據的意義」（2026-09-02 scout 的 ruleB top 20）。回答過程中發現
表面讀法（「這是 DPI 最高的 20 檔」）與實際口徑（「DPI ≥ 85 **且過流動性閘**後剩下的全部」）
差了 4 倍以上，且名單被 ETF 主導 —— 值得從「這張表怎麼讀」升級成「這條規則有沒有 edge」。

> ✅ **本篇不證偽任何既有筆記**，但為兩件既有設計決策補上**實證背書**（此前只有推理與事故經驗）：
> ① `promote ≠ 訊號`（dynamic_watchlist 只給觀察權、不給方向）；
> ② 卡 ③-8「不補 DPI 偏空側」的裁決 —— 偏多側本身在獨立窗下都撐不住，補鏡像側更無依據。

---

## 縮寫對照

| 縮寫 | 全稱 | 說明 |
|---|---|---|
| **DPI** | Dark Pool Indicator | SG Equity Hub 欄位，0–100 橫斷面相對刻度；高＝偏多 |
| **BUILDUP** | — | `roma_cli scout` 三段之首：全市場 data_table 掃描 |
| **ruleA / ruleB** | `oimp_pre_event` / `dpi_burst` | dynamic_watchlist 兩條 auto-promote 規則（OR 關係） |
| **OImp** | Options Impact | data_table 選擇權隱含衝擊欄；**index/ETF 大量缺值** |
| **data_table** | — | SG Scanners 頁匯出的全市場單日快照 CSV（約 4,900 列 × 40 欄） |
| **promote** | — | 把 sym 暫時放進 `dynamic_watchlist`（7 天 rolling），**不是訊號** |
| **cap** | `max_promotions_per_day` | 單日新 promote 上限（25），按訊號強度取 top-N |
| **td** | trading day | 本篇一律指「**去凍結後的可用場次**」，非日曆日 |
| **bp** | basis point | 1 bp = 0.01% |
| **CI** | Confidence Interval | 本篇對「日層級差值」做 t-CI；另附非重疊子樣本複驗 |

---

## 一、理論框架

### 1-1 官方對 DPI 的定義（原始層）

`spotgamma_report/knowledge/support/equity-hub/dark-pool-indicator-dpi.md`（Zendesk 官方說明中心，
**非 edu/ 影片層** —— 這個來源分層的教訓見 [[kb_dpi-direction-convention]] §0）：

- 追蹤**場外（dark pool）成交**。機構在暗池建倉是為了不讓 lit market 看見量；FINRA 要求隔夜申報。
- **高 = 偏多（綠）／低 = 偏空（紅）**，官方原文：「An increasing DPI may infer new or smart buyers coming into the stock.」
- **每日 3AM EST 更新** ⇒ 內容是**前一完整場次**的結算資料，天生 T+1。
- 官方方向門檻 **>60 偏多 / <30 偏空、60 日視野**（art `14356662523027`）。

### 1-2 ROMA 的 ruleB 是「更嚴的偏多側單邊規則」

我方 85 落在官方偏多帶內且更嚴；v3.73 複核裁決門檻不改（下修 60 會有全市場 30.5% 通過，
2026-06-14 曾灌爆 dynamic list 至 1,216 sym 使 scan 卡死）。**只有偏多側**，DPI 低位極端不 promote
（卡 ③-8，2026-08-15 裁決不補：官方查無「burst／單日極端」概念）。

### 1-3 本篇要問的三件事

1. **口徑**：輸出標題寫「DPI ≥ 85 — top 20」，但那 20 檔是**全市場前 20 名**，還是**閘後全部**？
2. **組成**：名單裡有多少是 `OImp` 缺值的 index/ETF —— 這些名字 synth_oi 與 v4 皆 0 檔、
   下游產不出 CW/PW（[[13-08-2026_水位可信度前置閘缺席…]] 已測），對 ROMA 而言等於**空轉**。
3. **有效度**：單日 DPI burst 之後，該標的的前瞻報酬是否優於同條件對照組？
   —— 若有，ruleB 有機會從「觀察權」升級為「加權訊號」；若無，維持現狀就是正解。

---

## 二、實驗設計

| 項目 | 設定 |
|---|---|
| 資料源 | `spotgamma_report/auto/data_table/SPX_data-table_YYYY-MM-DD.csv`，95 個檔 |
| 樣本期 | **2026-05-04 ~ 2026-09-02**（去凍結後 **67 個有效場次**，剔除 28 個凍結快照） |
| 訊號組 | 該場次 `DPI ≥ 85` **且** `Stock Volume ≥ 365,000`（＝實際流動性閘） |
| **對照組（基準）** | **同一場次、同樣過流動性閘、但 `DPI < 85` 的全市場其餘標的**（每日約 1,900+ 檔） |
| 價格錨 | **`Previous Close`**，不用 `Current Price`（後者會靜默凍結，見 [[reference_sg_levels_as_of_trade_date_not_filename]]） |
| 前視偏差 | 檔案 D 的 DPI ＝ D−1 場次資料；檔案 D 的 `Previous Close` ＝ D−1 收盤 ⇒ **同錨，無前視** |
| 凍結偵測 | 某檔 `Previous Close` 向量與前一保留檔完全相同 → 整檔丟棄 |
| 視野 | k = 1 / 3 / 5 / 10 個可用場次，close-to-close |
| 護欄 | 單筆報酬 \|r\| > 80% 剔除（併股／資料錯誤） |
| 統計 | **逐日**算「訊號組均值 − 對照組均值」→ 對「日」做 t-CI ⇒ 自動吸收同日齊漲齊跌的橫斷面相關 |
| 穩健性 ④ | **非重疊子樣本**（stride = k，跨 k 個 offset 合併）—— 修正重疊窗自相關（[[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] 陷阱 3） |
| 穩健性 ⑤ | **可執行性修正**：入場延後一場次（DPI 3AM EST 才更新，訊號當場次收盤實際上買不到） |

ETF/個股分層採 **`OImp` 缺值** 當 proxy（該欄缺值 100% 集中在 index/ETF，已於
[[13-08-2026_水位可信度前置閘缺席…]] P0 實測）。

---

## 三、結果

### 3-1 組成：標題誤導、六成空轉、四分之一場次貼頂

| 指標（每場次） | 中位 | 範圍 |
|---|---:|---|
| 全市場 `DPI ≥ 85` 原始檔數 | **98** | 58 – 147 |
| 過流動性閘後 | **21** | 8 – 31 |
| ↳ 流動性閘砍掉 | **79%** | — |
| 其中 `OImp` 缺值（＝index/ETF） | **13**（占閘後 **60%**） | — |
| 閘後檔數 ≥ cap(25) 的場次 | **16 / 67 ＝ 24%** | — |

三個直接可用的結論：

1. **「top 20」是顯示截斷，不是排名前 20。** 全市場 DPI ≥ 85 中位有 98 檔；表上剩下的是
   **過了流動性閘的全部**（中位 21 檔），所以絕大多數場次 top-20 ≈ 全部。
   ⇒ 讀法應是「**DPI ≥ 85 且場外量夠厚**的名單」，不是「暗池最活躍的 20 檔」。
   2026-09-02 當日：原始 **104** 檔 → 閘後 **23** 檔（被砍掉的含 DVSP / BAY 各 100.00 滿分）。
2. **六成是 ROMA 下游吃不到的名字。** `OImp` 缺值的 ETF 進了 dynamic list，但水位迴圈
   （`equity_signals.py:461`）只跑 `WATCH_SYMBOLS`、不吃 dynamic list，且這些名字 synth_oi/v4 皆 0 檔
   ⇒ **promote 了也不會產生任何下游輸出**。
3. **cap 咬得比想像頻繁。** 有 24% 的場次光 ruleB 閘後就 ≥ 25 檔，加上 ruleA 只會更高
   ⇒ 這些日子的實際門檻不是 85，而是被 `_strength()` 排序截出來的更高值。
   2026-09-02 正好是 2 (ruleA) + 23 (ruleB) = **25，剛好貼頂未截斷**。

### 3-2 前瞻報酬（逐日重疊窗，②③）

| k | 交易日 n | 訊號 n | 訊號均值 | 對照均值 | 差 (bp) | 95% CI (bp) | p |
|---:|---:|---:|---:|---:|---:|---|---:|
| 1 | 66 | 1,375 | 0.11% | 0.09% | **0.0** | [−16.3, 16.3] | 1.000 |
| 3 | 64 | 1,333 | 0.51% | 0.26% | **+25.6** | [−4.9, 56.2] | 0.096 |
| 5 | 62 | 1,289 | 0.59% | 0.38% | **+27.0** | [−15.6, 69.6] | 0.208 |
| 10 | 57 | 1,182 | 1.06% | 0.58% | **+53.9** | [1.0, 106.9] | 0.043 |

分層（同日對照組亦同樣分層）：

| k | 層 | 訊號 n | 差 (bp) | 95% CI (bp) | p |
|---:|---|---:|---:|---|---:|
| 3 | ETF | 841 | +22.0 | [−7.0, 51.0] | 0.133 |
| 3 | **個股** | 492 | **+80.0** | [16.8, 143.1] | **0.012** |
| 5 | ETF | 810 | +36.7 | [−3.1, 76.4] | 0.067 |
| 5 | **個股** | 479 | **+110.8** | [16.3, 205.2] | **0.020** |
| 10 | ETF | 740 | +110.1 | [63.9, 156.3] | 0.000 |
| 10 | **個股** | 442 | **+187.3** | [61.0, 313.7] | **0.003** |

表面讀法：**k=1 完全沒有 edge**（0.0 bp），edge 隨視野拉長而增，且**個股腿約為 ETF 腿的 2 倍**。

### 3-3 ④ 非重疊子樣本複驗 —— **全數跨零**

k > 1 時逐日滾動的前瞻窗互相重疊，日層級差值序列自相關 ⇒ 3-2 的 CI 過窄（k=10 的有效獨立樣本
約 67/10 ≈ 6，不是 57）。以 stride = k 取非重疊子樣本、跨 offset 合併後：

| k | 層 | 獨立窗 n | 差 (bp) | 95% CI (bp) |
|---:|---|---:|---:|---|
| 3 | 全部 | 21 | +25.4 | [−27.0, 77.8] |
| 3 | 個股 | 21 | +79.8 | [−25.6, 185.2] |
| 5 | 全部 | 12 | +26.2 | [−69.3, 121.6] |
| 5 | 個股 | 12 | +108.8 | [−96.7, 314.2] |
| 10 | 全部 | 5 | +53.9 | [−115.5, 223.3] |
| 10 | ETF | 5 | +110.7 | [−38.3, 259.7] |
| 10 | 個股 | 5 | +191.7 | [−215.5, 599.0] |

**點估計一字不改（+25.4 / +26.2 / +53.9 與 3-2 幾乎相同），但 CI 全部跨零。**
3-2 那三顆 p < 0.05 是**偽重複製造出來的**，不是新資訊。

### 3-4 ⑤ 可執行性修正 —— 再削 14~68 bp

DPI 3AM EST 才更新、scout 早盤前跑 ⇒ 「訊號當場次收盤」買不到。入場延後一場次後（重疊窗口徑，與 3-2 可直接對照）：

| k | 層 | 差 (bp)（原 → 修正後） | 修正後 95% CI (bp) |
|---:|---|---|---|
| 3 | 個股 | +80.0 → **+66.0** | [−3.8, 135.8]（**由顯著轉跨零**） |
| 5 | 個股 | +110.8 → **+101.1** | [12.6, 189.6] |
| 10 | 個股 | +187.3 → **+119.3** | [5.1, 233.6] |
| 10 | 全部 | +53.9 → **+35.9** | [−16.5, 88.3]（**由顯著轉跨零**） |

隔夜跳空吃掉 14~68 bp，且 k=3 個股與 k=10 全部這兩格**單靠這一項修正就翻回不顯著**。
兩項修正（④非重疊 ＋ ⑤可執行）**未曾聯合施加**，但④單獨已全數跨零 ⇒ 聯合後不可能救回。

---

## 四、限制

1. **樣本期只有 67 個有效場次、單一 regime。** 2026-05 ~ 09 全期 VIX 低檔 contango
   （2026-09-02 VIX 16.34、VIX3M/VIX 1.122），**沒有任何高波/倒掛樣本**。
   本篇的「無 edge」只證到「這段多頭低波期無 edge」，不可外推到壓力期。
2. **凍結快照剔除 28/95（29%）是全欄比對 `Previous Close` 的粗篩。** 若某檔只有部分欄凍結
   （SG 已知會靜默凍結，見 [[reference_sg_levels_as_of_trade_date_not_filename]]），本法抓不到。
3. **訊號集是「閘後全體」，不是實際 promote 名單。** 未模擬 cap 截斷（24% 場次會咬）、
   retired sym 過濾、7 天 retention。cap 會讓實際名單**更偏高 DPI**，方向上對本篇結論不利也不有利。
4. **ETF/個股分層用 `OImp` 缺值當 proxy**，非嚴格證券類型分類。
5. **對照組是「同日全市場其餘」，不是風格/beta 中性。** 若高 DPI 標的系統性偏某種 beta 或市值段，
   差值會混入風格報酬 —— 本篇未剝 beta（作法見 [[feedback_rotation_needs_beta_stripped_residual_corr]]）。
6. **未做對稱檢定。** 只測了偏多側；DPI 低端是否為反向訊號未驗（見 §六 待辦）。

---

## 五、ROMA 程式對照

| 項目 | 位置 |
|---|---|
| ruleB 規則說明 | `romasys/src/opportunities/sg_loaders/dynamic_watchlist.py:19` |
| ruleB 觸發判定 | `romasys/src/opportunities/sg_loaders/dynamic_watchlist.py:362-366` |
| 品質閘（流動性 + cap） | `romasys/src/opportunities/sg_loaders/dynamic_watchlist.py:431-455` |
| 門檻 fallback 常數 | `dynamic_watchlist.py:79`（DPI 85）、`:81`（vol，注意 fallback 仍是 1,000,000）、`:83`（cap 25） |
| 生效門檻（yaml，SSOT） | `romasys/manifest/thresholds_current.yaml:838-839`（85）、`:853`（365,000）、`:856`（cap 25） |
| 「top 20」顯示截斷 | `romasys/src/notifications/cmd_scout.py:91-99` |
| dynamic list 併入 watchlist | `romasys/src/opportunities/sg_loaders/symbols.py:56` |
| 水位迴圈**不吃** dynamic list | `romasys/src/opportunities/sg_signals/equity_signals.py:461`（`for sym in WATCH_SYMBOLS`） |

⚠️ `dynamic_watchlist.py:81` 的 fallback 仍是 `1_000_000`，與 yaml 生效值 `365000` 不一致。
yaml 讀得到時無害，但若 THRESHOLDS 載入失敗會**靜默變嚴 2.74 倍**（見 §六 待辦 3）。

---

## 六、結論與行動

**結論**

| # | 結論 | 依據 |
|---|---|---|
| ① | 「ruleB top 20」**不是排名前 20**，是「DPI ≥ 85 且過流動性閘」的**全部**（中位 21 檔，原始 98 檔） | §3-1 |
| ② | 名單**六成是 `OImp` 缺值的 index/ETF**，下游產不出水位 ⇒ 對 ROMA **空轉** | §3-1 |
| ③ | 24% 的場次光 ruleB 就貼上 cap(25)，那些日子的實際門檻高於 85 | §3-1 |
| ④ | **k=1 完全無 edge（0.0 bp）**；長視野點估計為正且個股腿 ≈ ETF 腿 2 倍 | §3-2 |
| ⑤ | **但 ④ 的顯著性在非重疊子樣本下全數跨零**，可執行性修正再削 14~68 bp ⇒ **本樣本期不支持把 `dpi_burst` 當方向訊號** | §3-3、§3-4 |

**行動**

1. ✅ **維持現狀，不動門檻、不加權。** `promote = 觀察權` 的設計是對的，本篇為它補上實證背書。
   任何把 DPI 寫進評分/方向判斷的提案，須先跨 regime 複驗。
2. ✅ **卡 ③-8（補偏空側）維持「不做」。** 偏多側在獨立窗下都撐不住，鏡像側更無依據。
3. 📌 **讀 scout 輸出時的實務口訣**：ruleB 名單先**刪掉 ETF 那半**，只看有 OImp 的個股
   （2026-09-02 ＝ BKU / WIX / QNST / SWKS / AWK / PONY / HAWK / FDS / SM / UNIT / MAS），
   ETF 那半當**宏觀情緒讀**（今日簇＝信用 JNK/SRLN/JCPB/LEMB ＋ 短存續期 STIP/SCHO ＋ 通膨商品 HGER/SDCI/DBMF
   ⇒ 防禦性配置味道），不當個股訊號。
4. 📌 **`cmd_scout.py:94` 的標題文字建議修正**：「top 20」→「閘後全部（顯示上限 20）」，
   避免每次讀都要重新推導口徑。（小改，未動手，見待辦 1）

---

## 七、待辦

1. **`cmd_scout.py:94` 標題改口徑** —— 順手可做，但屬 UX 文字，等下次動 scout 時一併改。
2. **對稱檢定（DPI 低端）** —— 本篇只測偏多側。若低端有顯著負向 edge，卡 ③-8 的裁決需要重開。
   腳本已備妥分層框架，改門檻方向即可。
3. **`dynamic_watchlist.py:81` fallback 與 yaml 對齊** —— `1_000_000` → `365_000`，消除
   THRESHOLDS 載入失敗時的靜默行為漂移。
4. **跨 regime 複驗** —— 等 data_table 累積到含高波/倒掛場次（VIX > 25 或 backwardation）後重跑，
   屆時才有資格談「DPI burst 在壓力期是否轉為有效」。**在那之前不得宣稱本篇結論普適。**
5. **beta 中性版對照組** —— 若 4 跑出正結果，需先剝 beta 再下結論。

---

## 附錄：腳本

- `py_dir/02-09-2026_dpi_burst_forward_return_audit.py` —— 本篇全部數字的唯一來源，可複跑：
  ```bash
  python3 py_dir/02-09-2026_dpi_burst_forward_return_audit.py            # ①②③ 組成 + 逐日重疊窗
  python3 py_dir/02-09-2026_dpi_burst_forward_return_audit.py --nooverlap # ④ 非重疊子樣本
  python3 py_dir/02-09-2026_dpi_burst_forward_return_audit.py --exec      # ⑤ 可執行性修正
  python3 py_dir/02-09-2026_dpi_burst_forward_return_audit.py --all       # 全部
  ```
  （教訓沿用 [[31-08-2026_CC_FP-p9極端greek的OOS複核]]：**實驗腳本必須進版控**，
  否則下次複核只能照口徑重寫、數字會漂移。）
- 本篇分析對象原始輸出：`log_gen_by_roma/scout_section/02-09-2026_multi_scout.md:21-44`

---

## [[關聯]]

- [[kb_dpi-direction-convention]] —— DPI 方向/門檻/視野的官方口徑（本篇的定義層前提）
- [[13-08-2026_水位可信度前置閘缺席_OptionsImpact只讀高端與流動性未過濾]] —— 首次點出
  「`dpi_burst` 每天 promote 27~31 檔無 OImp 值的 ETF」；本篇把它從**觀察**升級為**跨 67 場次的量化**
- [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] —— 陷阱 3（偽重複）在本篇 §3-3 再次現形
- [[25-07-2026_CC_FP-p9極端greek的前瞻報酬]] / [[31-08-2026_CC_FP-p9極端greek的OOS複核]] —— 同一套
  「極端百分位 → 前瞻報酬 vs 同條件對照組」方法論
- [[reference_sg_levels_as_of_trade_date_not_filename]] —— 為何價格錨用 `Previous Close` 不用 `Current Price`
- [[feedback_signal_gate_vs_weight_upgrader]] —— 「單維達標 ≠ 等級成立」；本篇是同一原則在 promote 層的實證
- [[reference_grep_skips_nested_romasys_repo]] —— 查 ROMA 程式對照時的路徑陷阱
