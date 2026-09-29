# 2026-04-21 Short MNQ 決策與 GEX 助漲跌環境分析

**背景：** 當日已平倉 MNQM6 多倉，再評估是否反手 Short MNQ。
**資料源：** ROMA CLI `scan QQQ` 輸出（`input_tmp.md`），數據日 2026/4/17。

## 縮寫對照

- GEX: Gamma Exposure
- DR: Delta Ratio
- DN: Delta Notional
- GR: Gamma Ratio
- HVP: High Volume Put（Call Wall）
- LVP: Low Volume Put（Put Wall）
- ZG: Zero Gamma
- IV: Implied Volatility
- OI: Open Interest
- CC: Covered Call

---

## 1. GEX 制度判定：✅ 助漲助跌（負 Gamma）

```
指標                數值            判定
----------------------------------------------
Net GEX            -$1.59B         🔴 負 Gamma 制度
Gamma Ratio         0.06           Put gamma 絕對主導
Dealer 行為        追漲殺跌         放大方向波動
制度穩定度         近 10 日維持負   波動放大 regime 穩定
```

**典型「助漲助跌」環境，尤其助「跌」。**

## 2. Short MNQ 信號面

### ✅ 支持 Short

```
信號                    讀數            權重
----------------------------------------------
DR=0.31                 強勢 Put 主導   🔴 -2
DR 趨勢 0.99→0.55       快速下降        🔴 -2
GEX -1590M$            負 gamma 加速   🔴 -2
GR=0.06 + P/C=1.47     Put 結構偏重    🔴 -1
Activity 0.02→0.16     建倉加速        🟡 中
綜合評級                                 🔴 偏空風險升高
```

### ⚠️ 反對 / 警示

```
信號                        讀數              讀法
----------------------------------------------------
DN=+$5.4B                   機構 Delta 淨多    多頭 Notional 仍大
Large OI Call/Put 650/570   大倉偏 Call +1    機構未翻空
LVP 445→454 上遷            Gamma 支撐抬升    ⬆️ 偏多結構
IV Rank 0.17                低波動率          不預期大行情
現價 $648.85 ≈ Call Wall    +0.13% 貼牆       squeeze 風險高
Garch 壓縮 0.19→0.21        方向未定          雙向 tail
```

### 🎯 關鍵決策點

**Call Wall $648.85（QQQ）= MNQ ~26,700**

目前 QQQ 站在 Call Wall 上方僅 **0.13%**，GEX 翻正臨界位：
- 站穩：dealer 轉壓抑波動 + squeeze 到 Bull Target $672 → Short 被絞殺
- 跌破：負 Gamma 啟動，dealer 殺跌加速，$648→$616 空間開 → Short 大贏

## 3. Short MNQ 具體條件

**不建議「此時此刻裸 Short」**，原因：
1. 價格在 Call Wall 上方 0.13% 是模糊帶
2. DN 仍偏多，機構未翻空
3. Put Hedge 已很重（SPY P680x3 + SPY P670x3 + QQQ P620x3 + TSM Collar），Net β 已壓到 80.9%

**若真要 Short，條件化進場：**

```
情境                觸發                       Short MNQ 口數
---------------------------------------------------------------
A. 跌破確認         QQQ 日內跌破 $645         1-2 口
                    且 MNQ 跌破 26,650
                    停損：QQQ $651 (MNQ 26,850)
                    目標：QQQ $630 (MNQ 25,950)

B. Squeeze 失敗     QQQ 日內上衝 $655 後        同上
                    快速回落至 $648            （反轉追空）

C. 現況盤整         不 Short                   等方向確認
```

## 4. 對沖 vs 投機界線

```
動機              性質                建議
------------------------------------------------
加強對沖          已不需要            NO - over-hedge 失去 upside
方向性投機        信號偏空但未確認    條件化小倉 OK
                  (1-2 口 MNQ)
抄短線順勢        依賴跌破觸發        Setup A 可執行
```

**1 口 MNQ ≈ $2 × NDX points**，26,700 ≈ notional $53k，2% 停損 ≈ -$1,060 風險。
NAV $609k，單筆風險 0.17% 合理。

## 5. 結論

**不急著 Short，等 Call Wall $648.85 方向確認。**

- 明日開盤 QQQ gap up 突破 $650 站穩 → 跟著 squeeze，別 Short
- QQQ 跌破 $645 且 MNQ 跌破 26,650 → Short MNQ 1-2 口（Setup A）
- 盤整則觀察 LVP 是否開始下移（目前 445→454 上遷，反而是空單不利訊號）

## 6. 監控觸發點

- [ ] QQQ 是否跌破 $645（Setup A 觸發）
- [ ] QQQ 是否突破 $650 並站穩（squeeze 模式，不 Short）
- [ ] LVP 445→454 上遷是否延續（上遷延續則偏多，空單取消）
- [ ] GEX 是否翻正（Net GEX 由負轉正 → regime change，必須反手）
- [ ] DN +$5.4B 是否開始下降（機構開始翻空的領先指標）

## 7. 核心策略備忘連結

- Put Hedge 已到位，此 Short 動機屬「方向性投機」而非對沖
- 不違反「Alpha 來自避免下跌」原則 — 但必須有明確觸發訊號
- 若 Short 成功跌破，考慮同步把 TSM Collar 向下 roll（更積極收割）
