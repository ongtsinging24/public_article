# AVGO 策略卡：機構遠月 call 階梯上滾 × opex 後回補 × 持倉待財報

**建卡**：2026-07-24（GMT+8）｜來源：TREND AVGO 覆盤
**價格錨**：AVGO **$392.47**（2026-07-23 16:00 EDT 收盤＝07-24 04:00 GMT+8）；查詢 2026-07-24 11:04 GMT+8（美股休市，下次開盤 21:30 GMT+8）
**持倉**：AVGO Nov20'26 $350 Call ×2（深 ITM，裸多無保護）｜MV $15,370.70（NAV 2.38%）／UPL +$1,940／Δ=+0.72／delta notional +$56,908（NAV 8.80%，有效槓桿 ~3.7×）（來源 `brokerage_log/23-07-2026-brokerage-03.xlsx.log`）
**承接**：[[22-07-2026_AVGO_tracking]]（v3, SSOT, A1–A9）｜[[23-07-2026_AVGO_tracking]]｜[[AVGO_daily_watch]]｜[[kb_far-call-prepositioning-into-weakness]]｜[[kb_synth-vs-v4-breakout-caliber]]

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| FP | FlowPatrol（SG 大單掃描）｜HW/CW/PW = Hedge/Call/Put Wall |
| LVP/HVP | Low/High Vol Point（v4 口徑 PW/CW）｜KG/KD = Key Gamma/Delta Strike |
| OI | Open Interest｜P/C OI = Put/Call OI Ratio｜DTE = Days To Expiry |
| d$/g$/v$ | delta$/gamma$/vega$（買方側，見 kb_fp-greek-sign-convention）｜bto/stc = Buy-To-Open/Sell-To-Close |
| DPI | Dark Pool Indicator｜IVR/SkewR = IV Rank/Skew Rank｜NTM = Next Twelve Months |
| SSOT | Single Source of Truth |

---

## 一、機構操作判讀（TREND 結論）

**一句話**：機構近 4 週用遠月 call 往上滾（360→410→440）、用 07/17 opex 洗掉近月，然後在 $370–380 區間安靜回補 call OI——但 07/17 後**沒有新的方向性加碼 block**，屬「持倉待財報」而非「持續加碼」。

### 主線：遠月 call 履約階梯上滾（吻合 kb_far-call-prepositioning 四要件）

| 階段 | 出處 | 動作 |
|---|---|---|
| 建倉 | `flowpatrol_2026_04_16.log` | Jul17 **$360C** d$ +855.52M／prem +$173.40M／OI 31,916；`sig_position` d%=100th |
| 局部減 | `04_20`/`04_21` | 360C d$ −154.64M / −147.30M，OI →21,854 |
| **★核心 roll** | `flowpatrol_2026_06_30.log`（session 06-29）| Jul17 360C **stc 17,515**（prem −$49.29M）→ Oct16 **$410C bto 26,392**／prem +$104.39M／d$ +465.88M／g$ +11.06M；spread=Call Roll，bto/sto 與 greek 一致 |
| 第二段 roll-up | synth_oi `Large Call OI` | **07-16 起 $410→$440**，且跨過 07/17 opex 未消失（非近月殘留）|

- 逢跌閘 ✓（06/29 px $372.44、5dR −5.00%）｜遠月價外 call ✓（DTE 109，OTM +10.1%，OTM band 部分符合）｜roll-up ✓（往上+往後 3 個月）｜cross-day OI ✓（單日建 26.4k）
- **收頂鏡像零出現**：4–7 月 FP 無 `Call Vert Credit`、無短月 call 爆量追價、無大額 protective put block。

### opex 後回補（本週最有價值新資訊）

| Quote Date | 收盤 | Call OI Sum | Put OI Sum | P/C OI |
|---|---:|---:|---:|---:|
| 07-16 | 374.46 | 1,272,989 | 1,270,587 | 0.998 |
| 07-17 opex | 370.83 | 1,066,318 | 1,116,756 | 1.047 |
| 07-20 | 378.21 | 1,083,806 | 1,122,914 | 1.036 |
| 07-21 | 386.50 | 1,112,595 | 1,138,573 | 1.023 |
| **07-22** | **396.69** | **1,140,253** | 1,139,444 | **0.999** |

- Call OI 3 場回補 +73,935（+6.9%），Put 僅 +22,688（+2.0%）→ **Call 回補速度 3.26×Put**
- P/C OI 1.047→0.999，回到 opex 前、也是 6 月以來最低（6 月全月 1.06–1.10）
- **A9 (b) 進度**：目標 ~1.27M，現 1.14M，缺 132,736；近 3 日均速 +24,645/場 → **約 5.4 場 ≈ 07/30 前後達標**（落在複查窗 07/27–07/31 內）

### Dealer gamma/delta 連 4 日單調加深（非單日噪音）

| Trade Date | Dealer Call Gamma | Dealer Put Gamma | Dealer Call Delta |
|---|---:|---:|---:|
| 07-17 | −112.8M | −113.9M | −14.31B |
| 07-22 | **−157.4M** | **−101.1M** | **−19.27B** |

Dealer short call gamma 4 日 +39.5%、put gamma 反淺；買方側 Put Gamma 26.4M→10.8M（−59.1%）同向佐證。

---

## 二、水位結構（結構口徑用 history_v4；data_table 07-23/24 缺 HW/CW/PW/DPI 欄）

| Trade Date | PW (LVP) | CW (HVP) |
|---|---:|---:|
| 07-17 | 320 | 440 |
| 07-20 | 320 | 410 |
| 07-21 | 320 | 390 |
| **07-22** | **320** | **410** ← 震盪後回升 |

- **PW $320 連 6 場完全不動**＝目前結構最硬的一條線
- CW 在 390–440 震盪、落點 $410（＝機構錨 Oct16 $410）→ A9 (a) 單邊移動仍成立，但「收斂到 $410」是震盪落點非單調收斂，**確定性語氣下修**
- **Large Call OI strike 錨在 $440**（07-16 起）＝比 CW 敏感的機構意圖代理

---

## 三、估值（沿用，不上修倍數；[[feedback_conservative_base_pe_no_rerating]]、[[feedback_ntm_blend_valuation]]）

| 情境 | 目標價 | 倍數/依據 | vs $392.47 |
|---|---:|---|---:|
| Bear | $225 | 需求證偽/ASIC 訂單落空 | −42.7% |
| **Base（NTM fair）** | **$451** | **28× NTM blend** | **+14.9%（現折價 −13.0%）** |
| Bull | $550 | AI ASIC 超預期 + re-rating | +40.1% |

賣方共識（滯後參考）：48 家 Strong Buy、均價 $525.44；13F 6,278 家持有、季增 +2.85%、權重 +0.39pt（擴散非撤退）。**我方不因外部評級上修倍數。**

---

## 四、觸發回標（v3 卡 A1–A9）

| # | 狀態 | 說明 |
|---|---|---|
| A1 | ☐ | 07-22 $396.81、07-23 $392.47 兩根皆未達 $400，且回落 |
| A2 | 🟢 解除 | 07-21~23 三根收盤站穩 $380；**07-23 盤中低 $386.82 未破 HW**（更正 daily_watch 誤植 $375.96＝07-20 低點）|
| A3 | ☐ | 未落入 $340–360 |
| A4 | 🟡 改口徑 | FP 07-22 量能/OI 回來（Call:Put vol 3.37:1、tot_oi_chg +67,151）但**五個 conviction 分類連 5 場缺席**；heavy_daytrade 單獨出現不計入 |
| A5 | ☐ | 無 conviction block 可比對 |
| A6 | **T-41** | 09-03 財報；未進 T-14 窗（08-20 起）|
| A7 | 🔴 凍結 | DPI 42.68/5d 0.4389（as-of 07-21）**已斷 3 個交易日**，凍結非「持續確認」，不可當新證據 |
| A8 | 作廢 | EVC 已停訂 |
| A9 | 🟡 累積中 | (a) 單邊移動 ✓（PW $320 死錨；CW 語氣下修）／(b) OI 回補外推 **07/30 達標**／(c) FP 無方向 block |

---

## 五、裁決與動作

**持倉裁決不變：Nov20'26 $350C ×2 持有不動、不加碼。**

**理由更換**：不再以「DPI 未承接」為由（該資料已斷 3 天無從驗證），改為「**FP 無 conviction block、機構自身 07/17 後亦未加碼**」。

### 動作點

1. **A9 (b) 檢查日訂 07/30**（回補外推達標日），不在窗口末 07/31 直接判否。
2. **A9 (a) 語氣下修**：CW 為震盪後落 $410，非單調收斂。
3. **A4 改口徑**：以「是否出現 conviction 分類（top_delta/gamma/vega/largest_premium/single_stocks）」為準，heavy_daytrade 單獨不計。
4. **新增監看：Large Call OI strike 是否守 $440**——比 CW 敏感（CW opex 後本就震盪）；掉回 $410 或更低＝履約階梯反向＝真正機構退場訊號。
5. **Protective put 時機**：09/03 財報（T-41）前決定 Nov 350C 是否配 put／改 BuCS；成本結構最佳窗＝**08 月中若 SkewR >0.85 而股價未破 $420**。

### 鎖利紀律回標（[[feedback_profit_protect_skew_near_high]]）

| 項目 | 現值 | 門檻 | 觸發？ |
|---|---:|---|---|
| Skew Rank | 0.621（07-22）| ≥0.90 | ✗ |
| 距 52W 高 $495 | −20.7% | ≤8% | ✗ |

→ **兩條皆不成立，鎖利未觸發**（07-16 曾衝 0.964 但為 opex 前尖點、隔日回落）。

### 不做什麼

- ❌ 不因外部 Strong Buy/$525 目標追價或上修倍數（[[feedback_conservative_base_pe_no_rerating]]）
- ❌ 不把 DPI 凍結值當「反彈無承接」的新證據
- ❌ 不把 CW $410 當單調收斂坐實（尚缺 (b)(c)）
- ❌ 不因 Netlist v. Samsung ITC（Inv. 337-TA-1511，Broadcom 列被告）片面下修估值——供應鏈法律風險，非公司/客戶 AI 營收口徑下修

---

## 六、資料空窗與待辦

- 🔴 **data_table 07-23/07-24 缺 HW/CW/PW/KG/KD + DPI 欄**（全市場性）→ 建議本機查 SG 官網匯出格式或抓取腳本漏欄
- 🟡 **DPI 已斷 3 個交易日**（最後 42.68 @ 07-21）
- 🔧 回頭更正 `AVGO_daily_watch.md` 24-07 筆的 $375.96 誤植（實為 07-20 低點，07-23 盤中低為 $386.82）

**關聯**：[[22-07-2026_AVGO_tracking]]｜[[23-07-2026_AVGO_tracking]]｜[[AVGO_daily_watch]]｜[[kb_far-call-prepositioning-into-weakness]]｜[[kb_synth-vs-v4-breakout-caliber]]｜[[feedback_ntm_blend_valuation]]｜[[feedback_profit_protect_skew_near_high]]
