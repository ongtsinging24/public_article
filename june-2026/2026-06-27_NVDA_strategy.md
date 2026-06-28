# NVDA 多空策略 — 2026-06-27

> 緣起：本日 video_digest 寶哥「NVDA 已跟雲廠商同進退」論點的拆解（[[../log_gen_by_roma/video_digest/2026-06-27/digest_寶哥_msft-bounce-burry-nvda-headshoulders-spacex-bond-crack]]）+ 我方現有 NVDA 偏多倉診斷。
> 數據源優先級：估值/結構以 ROMA + SG 為主，博主僅參考（[[feedback_data_source_priority]]）；我方持倉 SSOT = brokerage_log（[[feedback_holdings_ssot_brokerage_log]]）。

## 縮寫
- 賣鏟 = NVDA 賣 GPU 給所有買家｜hyperscaler = 雲四巨頭 capex 大戶
- 循環融資 = NVDA 投資客戶（CoreWeave/OpenAI/xAI）→ 客戶回頭買卡
- capex四拆 = (a)需求會不會花／(b)二階導回報質量／(c)份額／(d)融資形式（[[project_nvda_structural_cheap]]）
- PW/CW = Put Wall / Call Wall（V4）｜DR = Delta Ratio｜GEX = Gamma Exposure｜call-path = 用 call 表達多頭時的「路徑/時間」風險

---

## 一、現價與我方持倉（時間戳）
- **現價**：S=$192.53（brokerage 2026-06-26 mark）｜$195.74（6/25 收盤，ROMA scan 結構日）。*非即時，盤中對照券商。*
- **我方持倉（套牢的偏多倉）**：
  | 部位 | qty | MV | UPL | 距價外/到期 |
  |------|----:|----:|----:|------|
  | NVDA Oct16'26 185 Call | +3 | $7,099 | **−$3,470** | 微價內、~3.7 月 |
  | NVDA Nov20'26 190 Call | +1 | $2,443 | **−$581** | 近價平、~4.7 月 |
  - 合計偏多 Δ≈ +2.5 張正股當量；兩腿皆**負 UPL**＝**這就是「波動 MoS / call-path 風險」的活生生案例**（估值對、但路徑與時間在咬）。

## 二、核心矛盾（一句話）
**估值 MoS（多）vs 波動 MoS + regime（空）並存**：NVDA 結構性便宜（~19.7x NTM、PEG 0.47，capex四拆唯一 🟢 超跌）的論點未變；但 ① beta 2.24 高、② 市場負 gamma + credit_leads_equity risk-off、③ ROMA scan 中性偏空/暫緩進場、④ 我方用 call 表達多頭＝同時承擔方向+時間+IV 三重風險。

## 三、寶哥「同進退」論點的策略意涵（拆兩層）
- **股價/情緒層 = 對**：NVDA 是 AI basket 核心、動量權重高、beta 2.24，de-risk 時跌更兇 → **這解釋我方 call 為何套牢，但不是看空基本面的理由**。
- **基本面層 = 被誇大**：NVDA 賣出即入帳、毛利 ~75%、正 FCF（與燒 FCF 的 hyperscaler 相反），需求基礎比任一 hyperscaler 分散。循環融資佔比是零頭 = capex四拆的 **(d)⚠️**，非主體。
- **唯一成立的硬內核 = capex四拆 (a)**：NVDA 營收終究是 hyperscaler capex 決策的下游。**真利空 = 某巨頭真砍 capex**；在那之前，「同進退」主要是倉位/情緒現象。
- 本日反證偏「情緒非基本面」：下游股價跌、但 **MU 財報爆表 + 供需緊 beyond 2027**（上游需求沒減）。

## 四、ROMA / SG 結構水位（2026-06-27 scan，結構日 6/25）
- 綜合裁決：🟠 **中性偏空、暫緩進場**（中可信度）；bias −5/22 偏空；DR 0.365 強勢 Put 主導。
- **PW 195 / CW 220（V4）**；現價貼 PW（距 +0.4%）、距 CW −11%。
- IV Rank 0.251（冷卻）→ 不利新開 long call（但對既有倉的 IV crush 已大致發生）。
- **市場負 gamma**（QQQ GEX −2829M / SPY −5941M）+ MOVE/SKEW 升 = risk-off 放大下行波動。
- ⚠️ 水位分歧重度：synth HVP $175 vs V4 CW $220 分歧 20.5% → **Layer 3 雙止損**、估值軸陳舊 37 天降權。

## 五、策略（分多/空/避險三劇本）

### A. 既有偏多倉的處置（核心，優先）
- **不因「同進退」恐慌平倉**：進場時就接受的估值便宜論點未變（[[feedback_no_flip_without_entry_context]]）；call 套牢是**已知的 call-path 風險**、非新發現的利空。
- **但承認 call 表達方式在 risk-off + 負 gamma 下吃虧**：
  - **防守線**：跌破 **PW 195→191（synth/年線+0.618 ~192 區）** 且**收盤**站不回，啟動 Layer 3 雙止損的減碼腿（先砍 Nov 190C 這條較弱、Δ 較低、UPL 較小的腿，保留 Oct 185C 微價內主倉）。
  - **時間風險**：Oct16 到期 ~3.7 月，須在 **7 月 hyperscaler 財報（capex 指引）** 這個基本面催化前後做決斷，別讓 theta 在無催化的橫盤裡空燒。
- **若想降 call-path 風險又留多頭曝險**：考慮把部分 long call **roll 成正股 / 價內更深的 call / 或 call spread 封頂降成本**（IV Rank 低，賣 OTM call 收權利金有限，但能降 theta、把「方向對、時間錯」的痛點壓低）。

### B. 多方加碼劇本（條件觸發，勿在 risk-off 中盲加）
- **觸發**：① 市場 GEX 翻正 / SPY 脫離負 gamma；② NVDA 收復 **CW 220** 或站穩 **200（dealer short straddle 區、SG pin）**；③ 7 月 hyperscaler 財報 capex 指引續增（capex (a) 證實）。
- **載體**：站穩 200 後用**正股/價內 call 半倉**，而非再追 OTM call（[[feedback_squeeze_entry_dual_trigger]] 的雙觸發精神：別把進場綁死「等回撤」，也別在負 gamma 裡硬追）。

### C. 空方/避險（不主動做空 NVDA，只管理組合 beta）
- 我方是**多頭被套**，方向上不反手做空 NVDA。
- 若要降整體 AI/beta 曝險，**避險載體 = cash-equivalent（BOXX），不 rotate 防禦 equity、不做空 NVDA 個股**（[[feedback_derisk_to_cash_not_defensive_equity]]）。
- 組合層的指數避險另見 [[2026-06-26_QQQ_put_hedge_strategy]]。

## 六、可證偽觀察點（判「同進退」真假 = 判多頭論點是否破）
| 觀察 | 真捆綁（轉空訊號） | 純情緒（多頭續抱） |
|------|------|------|
| 7 月 hyperscaler 財報 | 任一巨頭**下修 capex** → NVDA 下季 guidance 同步下修 | capex 指引續增（「花更多」） |
| 上游 vs 下游 | MU/TSMC 營收同步轉弱 | 下游股價跌、上游需求/ASP 仍爆（如本日 MU） |
| 結構水位 | 跌破 PW 195 且 synth HVP 175 接力 | 收復 200 / CW 220、GEX 翻正 |
| 估值 | base_pe 重估後 implied P/E >50x 假超漲 | NTM 仍 ~20x、PEG <0.5 |

## 七、一句話結論
**估值論點未破、不反手；但承認 call-path 在 risk-off 中吃虧——以 PW 195 為防守、7 月 capex 財報為決斷點，先處置較弱的 Nov 190C 腿、保留主倉，加碼等「站穩 200 + GEX 翻正 + capex 證實」三共振。** 寶哥「同進退」的價值在提醒 beta/路徑風險（已反映在套牢的 call），但他把基本面捆綁講過頭；ROMA 仍以估值 MoS 為錨（[[project_nvda_structural_cheap]]、[[feedback_conservative_base_pe_no_rerating]]）。

---
*關聯：[[project_nvda_structural_cheap]]｜[[project_software_sector_frame]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_derisk_to_cash_not_defensive_equity]]｜[[feedback_13f_is_lagging_not_entry_signal]]｜scan: log_gen_by_roma/scan_section/2026-06-27_NVDA_scan_result.md*
