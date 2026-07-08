# kb — Vol Trigger vs Zero Gamma（VT vs ZG 兩條 gamma 翻轉線的差異）

> 性質：**evergreen 機制**（純方法論，不涉當時水位）。整理日 2026-06-30。
> 衍生層筆記：問題 → 結論 → SGKNOW 佐證（帶行號）→ ROMA 程式對照 → 行動 → 關聯。

## 縮寫
- **VT** = Vol Trigger｜SpotGamma 專有的「波動 regime 開關」水位
- **ZG** = Zero Gamma / Gamma Flip｜淨 dealer gamma = 0 的價位（GEX 曲線變號點）
- **GEX** = Gamma Exposure（dealer 逐 strike 加總的 gamma 曝險曲線）
- **+γ / −γ** = dealer 正 / 負 gamma 部位（逆勢 / 順勢對沖）

## 問題（research question）
VT 與 ZG 都標「dealer gamma 翻轉」，差別到底在哪？實戰該守哪一條、兩者背離怎麼讀？ROMA 現在是把兩者當同一條，還是分開算？

## 結論（TL;DR）
1. **同源不同算**：兩者都標 dealer 由逆勢對沖（+γ）→ 順勢對沖（−γ）的分界，SGKNOW 明寫「**vol trigger ≈ zero gamma level**」。但 **ZG = 機械算出的 GEX=0 變號點**；**VT = SG 模型修正/平滑、刻意做穩、拿來真正用的那條線**。
2. **VT 較鈍較穩、ZG 較敏較跳**：put skew 低/有人賣 put 買 call 時，真實 gamma flip 位置會漂移，SG 在 morning notes 更新 VT；naive ZG 對 OI/現價敏感、盤中漂移大，不適合當「線」守。**守 VT、ZG 當理論底**。
3. **方向性**：regime 翻轉通常是**向下跌破** VT 才發生，第一動多半是**較大 drawdown + VIX spike**（SGKNOW 統計）。
4. **背離 = 警訊**：價已破 ZG 但仍在 VT 上方（或反之）＝ 裸 GEX 與含 skew 模型分歧、盤性不穩，別重押方向。**ROMA 已把這個背離做成 caveat**（見下）。

## SGKNOW 佐證（出處＋行號）
- `digest_SpotGamma_vol-trigger-gamma-regime.md:13` — 「**vol trigger ≈ zero gamma level**：dealer 淨 gamma 翻正/負的分界（例 4000）」＝兩者同源定義。
- 同檔 `:14-15` — 下方=short gamma=高波（跌賣漲買、放大波動、VIX spike 快）；上方=long gamma=低波（漲漸賣跌買、壓抑波動）。
- 同檔 `:16` — **方向性**：通常向下**跌破** vol trigger 才翻 regime → 第一動多半較大 drawdown + VIX spike。
- 同檔 `:17` — **VT≠裸 ZG 的關鍵**：「put skew 低/有人賣 put/買 call，gamma flip 實際位置會移 → SG 在 morning notes 更新真實正負 gamma 邊界」＝VT 是含 skew 修正、會被 SG 主動更新的那條。
- 同檔 `:21-23` — 收盤分布統計：收 VT 之上→黏住小波（可賣 condor/straddle）；收 VT 之下→報酬大幅外擴（high vol）；兩側行為鮮明分界。
- 同檔 `:10`（縮寫列）— 「vol trigger / zero gamma = dealer 淨 gamma 由正翻負的 SPX 水位」＝SGKNOW 把兩者並列為同一概念，差異在「算法/穩定度/用途」而非「方向意義」。

## ROMA 程式對照（file:line）
**ROMA 已把 VT 與 ZG 當兩種不同口徑分開處理**，正好印證本筆記：
- **VT 來源 = SG morning notes 直讀**：`sg_loaders/levels.py:68`（`vol_trigger = float(parts[4])`）、`:79`（`zero_gamma = float(parts[15])`）— 注意 ZG 這欄也來自 SG 檔，但 ROMA 另有自算版（下）。
- **ZG 自算 = GEX 曲線線性插值變號點**：`sg_loaders/gamma_profile.py:32` `zero_cross_strike()` — 遍歷 strike 找第一個 `g0*g1<0`，線性插值 → 這是「機械版 ZG」，與 SG 給的 VT 是兩條獨立來源。
- **VT 波動制度監控（守 VT）**：`sg_gex.py:120` `_vt_regime_lines()` — 依現價 vs `vol_trigger` 判 🟢壓波動 / 🔴放波動 / ⚡臨界，並算 VT 跨日漂移（突變警示）。**ROMA 主守的就是 VT 這條**。
- **VT/ZG 背離 caveat（核心對照點）**：`sg_gex.py:171` `_regime_caveat()` — 註解明寫「ATM 切片 Net GEX 正負，與『現價 vs VT/ZG』位置是**兩種不同口徑、常打架**」；當 ATM 號誌與 VT/ZG 位置相反、或現價夾在 VT 與 ZG 之間（臨界）時回 caveat，避免單一口徑定調。**這就是本筆記第 4 點「背離=警訊」的程式落地**。
- **四象限分類**：`sg_gex.py:37` `classify_gex_regime()`；`sg_gamma_profile.py:54,71`（VT/ZG 跨日、current vs next_exp 翻轉）。

## 行動連結
- ✅ **已落地**：ROMA 已分別讀 VT（SG 直給）、自算 ZG（插值），且 `_regime_caveat` 已處理兩者背離 → 與本筆記結論一致，**無新 feat 缺口**。
- 🔎 **可選 feat 候選**：目前 `_vt_regime_lines` 只用 SG 的 `vol_trigger`；可加一行輸出「VT 與自算 ZG 的間距%」——間距小=翻轉一觸即發、間距大=跌破 VT 後尚有緩衝到 ZG 才是深 −γ。對應本筆記「VT 是守的線、ZG 是心裡的底」。→ 若要做，記 `SAVETODO`。
- 回填 `ROMA_SIGNAL_DESIGN.md` vol 章節：收盤相對 VT 位置 → vol 策略（上方賣 condor/下方買保險），引 `digest:21-23`。

## 關聯
- [[digest_SpotGamma_vol-trigger-gamma-regime]]（原始層，本筆記主佐證）
- [[digest_SpotGamma_key-levels-series-1to7]]（VT = Key Levels #7）
- [[kb_synth-vs-v4-breakout-caliber]]（同屬「兩口徑打架，哪個為準」方法論）
- [[feedback_squeeze_entry_dual_trigger]]（跌破 VT 初動偏大跌 + squeeze 入場）
