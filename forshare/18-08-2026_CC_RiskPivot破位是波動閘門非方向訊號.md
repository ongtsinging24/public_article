# Risk Pivot 破位是「波動閘門」而非「方向訊號」——兼證偽 ROMA fn_risk_pivot_breach 的語意

> ⚠️ 本篇對 ROMA 現行訊號 `fn_risk_pivot_breach` 的**語意標籤與 action 的一半**提出證偽（程式對照見下）。
> 亦更正本人同日稍早（n=7 事件研究）「破位與隨機無差異」的初步說法——樣本設計不當，見「方法論教訓」。

## 縮寫對照
FN=Founder's Note（SpotGamma 平日 note）｜SG=SpotGamma｜Risk Pivot=SG 在 FN "Key SG levels" 段落標示的多空分界 SPX 水位（原文 `Pivot: 7,775 (bearish <, bullish >)`）｜rv=realized volatility 實現波動（年化）｜mdd=maximum drawdown 最大回撤｜below/above=收盤位於 pivot 下方／上方｜permutation test=標籤重排檢定｜CI=bootstrap 信賴區間

## 問題（research question）
SG 在 FN 中反覆使用 "only look to press shorts on break of the Risk Pivot" 這類條件式指令，ROMA 也已將其實作為 🔴 訊號。
**破 Risk Pivot 究竟預測了什麼？是方向（該做空）、還是波動（該買凸性）？兩者的操作工具完全不同。**

## 理論框架
Risk Pivot 在 SG 體系內是 dealer gamma 結構的分界：pivot 之上 dealer 多半處於正 gamma（逆勢對沖、抑制波動），之下轉負 gamma（順勢對沖、放大波動）。
若此機制為真，則破位的**一階效果應該是「波動放大」，方向是二階、且未必為空**——因為負 gamma 放大的是「既有動能」，不指定符號。
但市場慣用讀法（含 ROMA 的實作）把它讀成 bearish regime shift。本篇即檢定這兩種讀法孰是。

## 實驗設計
- **樣本**：`log_gen_by_roma/founders_digest/**/*_founders_{AM,PM}.md`，逐檔以 regex `Pivot:\s*\$?([0-9],?[0-9]{3})` 抽當日 SG 掛出的 pivot 值；同日 **PM 優先**（代表收盤當下的水位），fallback AM。142 份 .md 全數抽取成功（0 miss），去重後得 **71 個交易日**。
- **價格**：`yfinance ^GSPC` 實際收盤。**刻意不用 FN 內文引述的收盤價**，避免轉述誤差污染判定。
- **分組**：`below` = 收盤 < pivot（n=19）；`above` = 收盤 ≥ pivot（n=52）。
- **對照組設計（關鍵）**：以 above 組為基準，而非「全樣本」——全樣本含 below 日本身，會稀釋差異（這正是初版 n=7 研究失敗之處）。
- **應變數**：+1/+3/+5 日報酬與勝率（方向）；後續 5 日 rv 年化與 mdd（風險）。
- **統計**：bootstrap 95% CI（10,000 次）＋ permutation test（20,000 次標籤重排，雙尾，無分佈假設；因 n=19 不適用常態近似，且環境無 scipy）。
- **樣本期**：**2026-05-06 ~ 2026-08-17**。

## 結果

### (a) 方向預測力 —— 與慣用讀法**相反**

| 指標 | below (n=19) | above (n=52) | 差異 | below 95% CI | permutation p |
|---|---|---|---|---|---|
| +1d | +0.22%（勝率61%）| +0.02%（勝率52%）| +0.20% | [-0.23%, +0.66%] | — |
| +3d | +0.84%（勝率67%）| +0.04%（勝率56%）| +0.80% | [+0.06%, +1.66%] | — |
| **+5d** | **+1.64%（勝率78%）** | **-0.07%（勝率50%）** | **+1.71%** | **[+0.88%, +2.41%]** | **0.0002** |

+1d 的 CI 跨 0（不顯著），但 +3d/+5d 的 CI 已完全在正值區，且 +5d permutation p=0.0002。
**破位後五日不但沒跌，反而顯著上漲；pivot 之上才是報酬平庸區（+5d 勝率恰好 50%）。**

### (b) 風險/波動 —— 與 gamma 機制**一致**

| 指標 | below (n=19) | above (n=52) | 差異 | permutation p |
|---|---|---|---|---|
| 後續5日 rv（年化）| 14.77%  CI[12.52, 17.03] | 11.31%  CI[9.91, 12.87] | **+3.45%** | **0.0195** |
| 後續5日 mdd | -0.69%  CI[-0.99, -0.39] | -0.89%  CI[-1.20, -0.61] | +0.20%（below 回撤反而**更淺**）| — |

rv 的兩組 CI **不重疊**，差異顯著。而 mdd 顯示破位後的下檔並沒有比較深——再次否證「破位＝下跌前兆」。

### (c) 首破日 vs 持續破位日

| 分組 | n | +5d 報酬 | 後續5日 rv | 後續5日 mdd |
|---|---|---|---|---|
| **首破日** | 8 | **+0.44%（勝率50%）** | **15.40%** | **-1.08%** |
| 持續破位 | 11 | +2.40%（勝率91%）| 14.37% | -0.44% |

**首破當下方向勝率恰為 50%（擲硬幣），且波動最高、回撤最深。** 均值回歸的甜點在「已確認持續破位」之後，不在破位當下。
→ 這是 (a) 的重要限定：不能把「破位＝買點」簡化執行，**買點在確認之後，破位當下只有波動是可交易的**。

### (d) 破位當下 VIX 水位是否調節結果

| 分組 | n | +5d 報酬 | 後續5日 rv |
|---|---|---|---|
| 破位 & VIX ≤ 18.7（中位數）| 9 | +1.51%（勝率67%）| 13.42% |
| 破位 & VIX > 18.7 | 9 | +1.76%（勝率89%）| 16.11% |

VIX 水位**不是**強調節變數（方向差異僅 0.25%）；它只調節後續波動幅度。
→ 破位時「VIX 高低」不改變該不該做空的答案（答案都是：不該）。

## 結論與行動

1. **Risk Pivot 是波動閘門，不是方向訊號。** 破位對後續 5 日波動放大有顯著預測力（+3.45%，p=0.0195），對方向的預測力則是**反向**（+1.71%，p=0.0002）。
2. **對應工具**：破位該做的是**買凸性**（long straddle / VIX call / 既有 put 續抱），**不是賣 delta（做空）**。照 SG banner "press shorts on break" 直接操作，在本樣本期是負期望值。
3. **時點分層**：首破日只有波動可交易（方向勝率 50%）；要押均值回歸須等持續破位確認。
4. **實例對照（2026-08-17）**：SPX 收 7,745 破 pivot 7,775（首破日），當日 VIX +7%、VVIX +7%、fixed-strike vol +1~5 點、實現波幅為 0DTE straddle 定價的 2 倍。
   同期 SG 8/16 週報建議的 8/28 到期 long straddle（買凸性）＝正確工具；SG 8/14 banner 的 press shorts（賣 delta）＝錯誤工具。**同一家機構的兩份產品給出工具相反的建議，實證站在週報那邊。**

### ROMA 程式對照（現查，非憑記憶）

| 位置 | 現行實作 | 本篇裁決 |
|---|---|---|
| `romasys/src/opportunities/sg_signals/founders_signals.py:11` | 註解定義 `fn_risk_pivot_breach` ＝「🔴 制度惡化（SPX < risk_pivot）」 | ❌ 語意錯誤：實證顯示後續 5 日報酬顯著為**正** |
| `romasys/src/opportunities/sg_signals/founders_signals.py:164` | `"priority": Priority.REGIME_SHIFT_BEAR.value` | ❌ 應改為波動類 priority（同族 `VOLATILITY_WARN`，見 :182 approach 訊號用法） |
| `romasys/src/opportunities/sg_signals/founders_signals.py:170` | detail 文字「→ 降級多單」 | ❌ 被證偽（below 組 +5d 勝率 78%） |
| `romasys/src/opportunities/sg_signals/founders_signals.py:170-171` | detail 文字「持倉 long put 對沖效益放大」「觸發 tail hedge 評估」 | ✅ 被證實（rv +3.45%，p=0.0195） |
| `romasys/src/opportunities/sg_signals/founders_signals.py:173` | `"action": Action.REDUCE_OR_HEDGE.value` | ⚠️ 一半對一半錯：**HEDGE 對、REDUCE 錯** |

`romasys/src/opportunities/sg_opportunities.py:464` 為呼叫端（`detect_founders_signals()`），語意修正後不需改呼叫端。

## 方法論教訓（自我更正）

同日稍早我先做了一版 **n=7 的「事件首日」研究**，結論是「破位後 +1/+3/+5 日與全樣本基準無可辨識差異」。**該結論是錯的**，兩個設計缺陷：
1. **對照組污染**：用「全樣本每日」當基準，而全樣本**包含 below 日本身**，等於拿處理組去比「處理組＋對照組」的混合，系統性稀釋真實差異。正確做法是 below vs above 直接對照。
2. **事件併合丟資訊**：把連續破位日併為單一「事件首日」，n 從 19 掉到 7，同時**丟掉了 (c) 首破 vs 持續破位這個最有操作價值的切分**——而那正好是本篇最重要的發現之一。

→ 一般化教訓：**做條件基準率時，對照組必須是「條件不成立」的那些觀測，不能用全樣本**；事件併合前先確認被併掉的維度不是應變數。

## ⚠️ 樣本限制（不可略過）

- **樣本期 2026-05-06 ~ 2026-08-17，僅 71 個交易日，且全程多頭 regime。** 起點不是任意選的——`founders_digest` 管線最早只到 2026-05-06，**無法回補**，這是資料源的硬邊界而非取樣選擇。
- 因此 **(a) 方向結論高機率是「多頭 regime 內的均值回歸」**，任何「跌了就買」在此期間都會贏。**不可外推到下跌 regime。**
- **(b) 波動結論對 regime 的依賴較低**（負 gamma 放大波動是機制性的，不分多空），可信度較高，是本篇最該保留的部分。
- below n=19、首破 n=8，(c)(d) 的細分格皆為個位數至十位數，**僅供方向性參考，不足以支撐精確估計**。

## 待辦
- [ ] 進 2027 或市場出現下跌 regime 後回測本篇，檢驗 (a) 是否翻轉、(b) 是否維持——這是判定「均值回歸假說 vs pivot 本身有 alpha」的唯一乾淨檢定。
- [ ] 開 SAVETODO 卡修正 `founders_signals.py` 的 breach 語意與 priority（REGIME_SHIFT_BEAR → 波動類），並把 detail 的「降級多單」改為「買凸性/續抱既有對沖」。
- [ ] 擴充應變數：加入後續 5 日 **IV 變動**（而非只有 rv），檢驗破位是否也能預測 IV 上升——若能，long straddle 的期望值可直接量化。
- [ ] 檢查 `fn_risk_pivot_approach`（:181-190）是否有同類語意問題（目前標 VOLATILITY_WARN，方向上反而比 breach 正確）。

## 附錄：腳本與資料
- 腳本：`py_dir/risk_pivot_gate_vs_predictor.py`（可重跑，含 bootstrap CI + permutation test）
- 逐日明細：`py_dir/risk_pivot_gate_daily.csv`（date / close / pivot / sess / state / fwd1,3,5 / rv5 / mdd5）
- 重跑：`python3 py_dir/risk_pivot_gate_vs_predictor.py`

## 關聯
- [[18-08-2026_TRENDFN]]（本篇的觸發來源：8/17 首破 Risk Pivot 的 FN_TREND 分析）
- [[31-07-2026_CC_PutWall支撐的條件基準率與對沖飽和機制]]（同族：SG 水位的條件基準率檢定）
- [[31-07-2026_CC_訊號覆蓋率與辨別力上限_以FN謹慎語氣為例]]（同族：FN 衍生訊號的辨別力上限）
- [[22-04-2026_CC_制度信號vs市場信號]]（本篇屬「制度信號」——SG 分析師掛出的水位——被市場資料檢定的案例）
- [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]]（本篇「方法論教訓」段是該篇陷阱清單的第四例：對照組污染）
