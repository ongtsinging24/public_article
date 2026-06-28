# 2026-06-28 META 壓力 DCF（抽掉 backlog 墊）策略

> 縮寫：OCF=營運現金流｜FCF=自由現金流｜EV=企業價值｜TV=終值｜WACC=加權資金成本｜g=永續成長率
> 性質：框架級**保守地板估算**，非市場共識；輸入隨每季 capex 實際數變動。
> 起源：由 MSFT「1900億豪賭」video_digest 的 DCF 框架延伸（[[project_software_sector_frame]]）。

## 0. TL;DR
- **META 無墊地板 ≈ $390–420（中值 ~$405）**。
- 現價 **$553**（2026-06-26）→ 到地板 **~-27%**。
- 結論：**$405 進、$553 不追**。地板可信度**高**（DCF 是 META 的對工具）。

## 1. 壓力測試定義（「抽掉 backlog 墊」）

### 1.0 名詞：什麼是「backlog 墊」（backlog=未交付的合約訂單積壓）
- **backlog 墊** = 用「已簽、未交付的合約訂單」當未來現金流的安全墊（托底）。
- **抽掉墊** = 故意把這托底拿走，看 META 在「沒有任何訂單保證」最壞情況下還值多少 → 找**價值地板**。
- 對 META 是壓力測試的原因：**META 的 capex 沒有 backlog 托底**（對照 [[project_nvda_structural_cheap]] capex 四拆，META 卡在「(d) 無合約需求托底」）。

| | 有 backlog 墊（如 NVDA 下游 hyperscaler 訂單）| META（無墊）|
|----------|----------------------------|------------------------------|
| 誰買單 | 客戶**先簽約**、需求被鎖定 | **沒有外部合約**，自賭 AI 廣告回補 |
| capex 性質 | 對應確定訂單、低風險 | **防禦性過建**，怕落後而先蓋 |
| 風險 | 訂單即現金流保證 | 蓋了若沒變現 → 純折舊燒錢 |

→ META 是自掏腰包蓋算力、賭未來廣告毛利賺回來——**這個「賭」就是墊**。

### 1.1 抽掉墊 = 關掉回補鏈
正常 bull DCF 假設 AI capex → 廣告高毛利回補 → capex/營收正常化 → FCF 強彈。
**抽掉墊** = 關掉回補：
1. capex 維持高檔、只緩慢下台階，回不到歷史輕資產水位（無合約需求托底 → 防禦性過建 + 更快折舊汰換）。
2. 營收/毛利不給 AI 變現的超額上修，只當普通成長。
→ 目的是找**價值地板**，不是預測中樞。

## 2. 起點（FY2025 實際）
| 項 | 值 |
|----|----|
| 營收 | $201B |
| OCF | $113B（margin 56%）|
| capex（含融資租賃）| $69.7B |
| FCF | $43.6B |
| 股數 | 2.53B |
| 2026 capex 指引 | **$125–145B**（中點 $135B，近翻倍）|

## 3. 明確期現金流（WACC 9.5%、g 4%）
| 年 | 營收 | OCF@55% | capex/營收 | capex | FCF |
|----|------|---------|-----------|-------|-----|
| 2026 | 237 | 130 | 57% | 135 | **-5** |
| 2027 | 273 | 150 | 50% | 137 | 13 |
| 2028 | 308 | 169 | 45% | 139 | 30 |
| 2029 | 342 | 188 | 40% | 137 | 51 |
| 2030 | 373 | 205 | 37% | 138 | 67 |

- 終值 FCF（2031，capex 卡 35% 地板）≈ $78B → TV = 78/(0.095-0.04) = **$1,418B**
- PV(明確期 FCF) ≈ $107B｜PV(TV) ≈ $900B｜+ 淨現金 ~$20B
- **權益 ≈ $1,027B ÷ 2.53B = ~$405/股**

## 4. 多空操作
- **分界線**：$405（無墊地板）。
  - < $405：連需求墊都不給也便宜 → 真便宜，可建多。
  - $405–553：賭 AI 廣告回補的價，逐步減持/不追。
  - 接近 $553+：估值已含完整回補，偏空/避險（用 cash-equivalent，[[feedback_derisk_to_cash_not_defensive_equity]]）。
- 最痛點是 **2026-27 FCF 歸零**——敘事最黑時段，符合 [[feedback_squeeze_entry_dual_trigger]]：別把進場綁死「等回撤」，設雙觸發（A 地板區分批 / B 突破回補確認加碼）。

## 5. 追蹤證偽點（每季更新本檔）
1. 季度**現金 capex 實際數** vs $135B 指引（驗是否真衝 / 有無踩煞車）。
2. 廣告營收增速 + Reality Labs/AI 是否開始變現（回補訊號）。
3. OCF margin 是否守住 ~55%（毀則地板下修）。
4. capex/營收何時、降到多少（bull 看 normalize 到 25%；無墊假設卡 35%）。

## 6. 關聯
- [[project_software_sector_frame]]：跌是敘事 de-rate 非基本面崩。
- [[feedback_conservative_base_pe_no_rerating]]：別用 AI 狂熱中樞估值喊折價。
- [[project_nvda_structural_cheap]]：capex 四拆，META 卡在「(d) 無合約需求托底」。
- 對照檔：`2026-06-28_AMZN_strategy.md`
- 跨標的樞紐：`2026-06-28_hyperscaler_capex_backlog_compare.md`（MSFT/META/GOOG/AMZN 同軸對照；META 站在 capex 比最高＋零墊的最差一角）

## 來源
- [Meta Q4/FY2025 8-K](https://www.sec.gov/Archives/edgar/data/0001326801/000162828026003832/meta-12312025xexhibit991.htm)
- [Meta FY2025 results](https://investor.atmeta.com/investor-news/press-release-details/2026/Meta-Reports-Fourth-Quarter-and-Full-Year-2025-Results/default.aspx)
- 現價 [CNBC META](https://www.cnbc.com/quotes/META)
