# AVGO 追蹤卡（建卡 2026-07-08）

- 基準價：AVGO **$370.97**（07-08 收盤，SG data_table）
- 背景：TREND AVGO 深挖結論；持倉 = **Nov20'26 350C ×2**（UPL -3,050 @07-03 brokerage log）
- 關聯：[[08-07-2026_AVGO_strategy]]（母策略卡）、[[08-07-2026_TRENDFP]]（semis 啞鈴結構）、[[08-07-2026_SMH_strategy]]（SMH BePS 已間接罩 AVGO beta）

**縮寫**：KG/HW/CW/PW = Key Gamma/Hedge Wall/Call Wall/Put Wall；DPI = Dark Pool Indicator；BuCS = Bull Call Spread；FP = FlowPatrol

---

## 核心論點（被追蹤的劇本）

1. **機構多頭錨 = Oct16 410C 26,392 張（$104M prem，06/30 由 Jul 360C roll 入）**——反彈劇本定價在 Q3 財報（~9 月初）後、目標 410+
2. 現貨層無人搶跑：DPI 35 / 5d 37% 弱、heavy_daytrade OI 淨減 → 「有錨的等待」
3. 天花板 410-430（6 月機構已清倉 430/740 LEAP call，無人押回前高 495）

## 結構地圖（07-08 基準）

```
價位    角色                      狀態
-----   -----------------------   ------------------
 410    Large Call OI 機構席位    劇本目標區
 400    KG ＋ CW                  gamma 阻力主樞紐
 380    Large Put OI              舊 HW
 370    HW                        ★現價貼著
 350    PW ＝ 我方 350C 履約價    下方唯一大支撐
```

## 追蹤點

### 觸發型（命中即行動）
- [ ] 🟢 **收復 400（KG+CW）** → dealer 對 410C 對沖轉助漲 → 加碼 Oct/Nov 370/410 BuCS
- [ ] 🔴 **跌破 350 PW** → 我方 350C 轉 OTM ＋ 機構劇本失效警訊 → 減碼
- [ ] 🟡 **機構 Oct 410C 席位變動**（FP 出現 Oct16 410C 大量 STC/roll）→ 劇本轉向，重評

### 觀察型（每次 CHKTR 覆核）
- [ ] 5d DPI 是否回 50 上方（反彈可信度前置條件）
- [ ] HW 是否繼續下移（380→370→?；牆跟跌 = 弱勢延續）
- [ ] IVR 變化（07-08 = 49.8th；若飆向 SMH 級別 95th → 加碼工具改用 spread 不用裸 call）
- [ ] FQ3 財報日確認（預估 ~9 月初；data_table Earnings Date 欄目前空值）
- [ ] SMH BePS（Aug21 580/545 ×5，07-08 已成交）到期後，AVGO 的 7-8 月 beta 保護是否需要接棒

### 持倉紀律
- Nov 350C ×2 **續持**——與機構 Oct 410C 同向且更保守（deep ITM、到期更晚、strike 站 PW 上）
- 進場時已接受的條件（財報後 de-rate 波動、-3k UPL 浮虧）不是新風險，不因單日 snapshot 翻多為空
- 加碼只在 🟢 觸發後執行，**不在 400 之下追**

## 更新記錄

```
日期        px       事件/覆核
---------   ------   ----------------------------------------
2026-07-08  370.97   建卡（TREND AVGO 深挖）
```
