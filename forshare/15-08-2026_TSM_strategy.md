# TSM 機構動向深挖與策略 — 2026-08-15

> 觸發：`TREND2 TREND TSM` → `SAVEST`（本地 session，非雲端 routine）
> 產出時間：**2026-08-15 23:5x 台北（週六，美股休市）**
> **現價：$426.35（2026-08-14 確定收盤，已過 04:00 GMT+8 門檻）**，較 08-13 收盤 $430.49 **−0.96%**；距 CW $425 僅 **+0.32%**（三日收盤站穩但 buffer 明顯收窄）
> 本篇承接 [[14-08-2026_TSM_strategy]] 與追蹤卡 [[14-08-2026_TSM_tracking]]（T1–T15 編號沿用，本篇僅新增 T16，不重複展開已收斂項）
>
> **本篇相對前卡的核心結論**：① 08-14→08-15 兩份 scan_result（結構日 8/12→8/13）之間 **GEX regime 明確轉強**（GR 0.46→2.74、Net GEX +35M→+245M、Large Put OI 460→320 下移），裁決由「多層矛盾/等待回撤」轉「偏多/繼續觀察」；② 但 **T12/T13/T15 三項待驗全數凍結**（OI 現查與 08-13 結算值逐一比對完全不變，FP 也是同一份 08-13 session 重複發布），本輪無新增量機構訊號；③ 🆕 **T16：ARK 對 TSM 的「減倉」查明為 ETF 贖回雜訊，非個股訊號**（Δwt 實為正值，且與 NVDA/AMD/AVGO/GOOG/AMZN 等近 30 檔同步 TRIM）；④ 🆕 市場層新警示：**Dispersion 擁擠**（Corr Proxy 0.080 <0.08），單股 call 過度擁擠，不利進一步加碼 TSM call。

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| FP | FlowPatrol（SG 大單流） |
| OI / Vol | Open Interest 未平倉／成交量｜**V/OI** >1 幾乎必為開倉 |
| **ltd** | lastTradeDate — 該合約最後成交日，yfinance 對不活躍履約會沿用舊日 volume |
| PW/CW/KG/HW | Put Wall／Call Wall／Key Gamma／Hedge Wall |
| IVR / SkewR / GarchR | IV Rank／Skew Rank／Garch Rank |
| GR / DR | Gamma Ratio／Delta Ratio |
| VRP | Variance Risk Premium（IV − RV，負值＝已實現波動高於隱含） |
| PS | Put Spread（保護型） |
| rr8b | 持倉方向性曝險（Δ加權，equiv_mv/NAV） |

---

## 樣本邊界

| 來源 | 實際 as-of | 備註 |
|---|---|---|
| yfinance 全鏈（OI/Vol） | **OI = 08-13 結算**（現查值與前卡逐一比對完全不變，08-14 盤中成交尚未入 OI） | 已用 `ltd` 過濾 |
| ROMA scan_section | **14-08-2026**（結構日 8/12）＋ **15-08-2026**（結構日 8/13） | 本篇 TREND2 主體，跨卡比較 |
| SG data_table 牆位 | **08-11 收盤**（檔名仍卡在 08-12，缺 3 個交易日未推進） | PW 400／CW 425（官方口徑未更新） |
| FP flowpatrol | 08-14 publish，但 `session_date=08-13`，**與前卡同一份資料重複** | 無新增量 |
| ARK inst_flow | 08-14 publish（08-12→08-13 diff） | 本次覆核判定為 ETF 贖回雜訊，見 T16 |
| 我方持倉 | `14-08-2026-brokerage.xlsx.log`（週末無更新） | NAV $643,405 |
| founders_digest | 08-14 AM/PM，連續 15 份零次提及 TSM | SG 敘事層持續靜音 |

---

## 一、TL;DR — 五條

1. **GEX regime 於 08-12→08-13 結構日之間明確轉強**：ATM Net GEX +35M→**+245M**（7倍）、GR 0.46→**2.74**（Put主導翻轉為Call主導）、CW $425 pin強度 67→**83/100**。ROMA 綜合裁決由「多層矛盾/低可信度/等待回撤」轉為「偏多/中可信度/繼續觀察」（§二）。

2. **Large Put OI 結構下移**：08-12 資料的大額 put OI 聚集在 $460（貼近現價），08-13 資料已降到 **$320**（深度價外），近端下檔套牢帶鬆動，P/C OI 比同時從 1.22 升到 **1.75**（§二）。

3. **⚠️ CW $425 站穩 buffer 收窄**：08-14 收盤 $426.35（−0.96%），距 CW 僅 +0.32%，是三日站穩以來最薄的一次，屬於「持續觀察」而非「確認突破」（§二）。

4. **T12/T13/T15 三項前卡待驗全數凍結、無新資訊**：OI 現查（ltd=08-14）與前卡 08-13 結算值逐一比對**完全不變**；FP 08-14 publish 的 `session_date` 仍是 08-13，與前卡同一份資料重複發布，非新增量。下一個真實檢查點是週一 08-17（§三）。

5. **🆕 T16：兩則新查核，一則排除、一則列為觀察**：
   - **ARKK/ARKQ「減倉」TSM 查明為 ETF 贖回雜訊**：Δwt 實為正值（+0.010pp / +0.040pp），且與 NVDA/AMD/AVGO/GOOG/AMZN 等近 30 檔同步 TRIM，非 TSM 特定訊號（§四）。
   - **Dispersion 擁擠新警示**（Corr Proxy 0.080 <0.08）：單股 call 過度擁擠，dispersion premium 高，對我方 94.38% 方向性曝險是「不利加碼」的提醒，非動作訊號（§四）。

---

## 二、TREND2：08-14 → 08-15 scan_result 跨日框架比較

| 項目 | 08-14 卡（結構日 8/12，收盤429.15） | 08-15 卡（結構日 8/13，收盤430.55） | 讀點 |
|---|---|---|---|
| 綜合裁決 | 🔴 多層矛盾／低可信度／**等待回撤** | 🚀 偏多／中可信度／**繼續觀察** | 矛盾消失 |
| ATM Net GEX | +35M（邊緣正） | **+245M**（中正，+7×） | dealer 吸震力顯著增強 |
| Gamma Ratio [ATM] | 0.46（Put主導） | **2.74**（Call主導，翻轉） | 方向性轉正 |
| Call Wall $425 pin強度 | 67/100 | **83/100** | pin 力道增強，本週 pin-to-strike 機率上升 |
| Large C/P OI（履約價/比） | 560/460，比1.22 | 560/**320**，比**1.75** | 大額 put OI 從 460→320 下移 |
| IV term structure（NE45 slope） | Backwardation −0.05（財報前IV crush確定性高） | 恢復正常 **+0.39** | crush 訊號減弱 |
| VWAP(week) vs 現價 | 427.52，現價其下（偏空） | 427.39，現價其下（偏空） | 未變，仍在機構成本帶下方 |
| 進場確認條件 | 5/5 達成（DR/Act 尚可信） | 3/5（DR=1911異常/Act 因 synth 分母趨近0降級為不可信） | 條件數下降是資料品質問題非結構轉弱 |

⚠️ **兩個口徑不可混淆**：以上翻轉是 **history_v4 dealer 口徑**算出來的，SG **官方 data_table 牆位（PW$400/CW$425）本身仍卡在 08-11**，已缺 3 個交易日未推進。若下一份 data_table 真的上修 CW，才是官方口徑確認；目前只能說 dealer 對沖行為已經轉強，牆位數字未必馬上跟著改。

---

## 三、TREND：即時多源覆核 — T12/T13/T15 待驗現況

### T12（Dec-18 500C 回補 vs $500天花板）— 凍結

| 履約 | 08-13 結算 OI（前卡） | 現查（ltd=08-14） | Δ |
|---|---|---|---|
| Dec-18 500C | 25,758 | **25,758** | 0 |
| Dec-18 560C | 37,155 | **37,155** | 0 |
| Dec-18 530C | 5,234 | **5,234** | 0 |

**判定不變**：前卡已判「回升 ≥1,000 ⇒ T9反轉判定作廢，退回$500天花板敘事」，本輪無新變化可推翻或加強此判定。

### T13（Sep-11 週選 435/440/450/470C 事件倉）— 凍結

現查 OI：673 / 1,162 / 842 / 383，與前卡完全一致，08-14 盤中無新增量（週選契約流動性低，08-14單日成交量未進一步推高持倉）。

### T15（遠價外 call 階梯 ＋ Nov-20 390P）— 凍結，方向仍未定

現查：Dec-18 630C OI 1,167（08-14 盤中成交量 450 但未反映進 OI，符合結算延遲慣例）、Nov-20 390P OI 4,044、Nov-20 600C/680C OI 1,303/1,078 — 六筆全數與前卡數字一致。**方向仍未定**，唯一錨點仍是前卡引用的 08-06 同族 500C `SELL(greek)` 判決（推論非證據）。

### FP：無新 session

08-14 publish 的 flowpatrol log 標頭 `session_date: 2026-08-13`，內容（460P/460C Aug-21，皆 ⚠pkg、oi失真）與前卡引用的 08-13 session **逐字相同**，非新資料。依 [[feedback_fp_log_dedup_by_session_date]] 判定不重複計入。

---

## 四、🆕 T16：兩則新查核

### ① ARK inst_flow「減倉」TSM — 判定為 ETF 贖回雜訊，非個股訊號

`log_gen_by_roma/inst_flow/14-08-2026_ark_flow.md`（08-12→08-13 diff）：

| Fund | Δsh | Δsh% | **Δwt** | 今日權重 |
|---|--:|--:|--:|--:|
| ARKK | −1,089 | −0.7% | **+0.010** | 1.05% |
| ARKQ | −1,028 | −0.6% | **+0.040** | 3.42% |

股數雖降，但 **Δwt 為正**（相對權重上升）。且同一份報告的「跨基金共識 SELL」清單中，TSM 與 NVDA/AMD/AVGO/GOOG/GOOGL/AMZN/TSLA/PLTR/DE 等**近 30 檔近乎全數同步 TRIM**——依該檔案自身警語「ETF 申贖會等比例改變 shares，NEW/EXIT 最乾淨，ADD/TRIM 參考 Δwt」，這是**基金整體遭贖回、全倉位等比例收縮**的結果，不是機構主動看空 TSM。**排除為雜訊**。

### ② Dispersion 擁擠 — 新市場層警示，列入觀察

08-15 scan 新增：Corr Proxy 0.080 <0.08（VIX 14.2% / 均股 1M IV 50.4%）— 單股 call 過度擁擠，dispersion premium 高，官方建議「等 proxy 回升後才是建多時機」。

**對我方的意涵**：我方 TSM 方向性曝險已達 rr8b **94.38% NAV**、rr4t 避險 **0.00%**，本身就已是重倉單股 call 的極端配置。此警示不要求動作，但**強化「不加碼」的既有立場**（§五）。

---

## 五、對我方持倉的意涵（結論不變，數字更新）

**SSOT**：`brokerage_log/14-08-2026-brokerage.xlsx.log`（週末無新檔）｜NAV $643,405｜TSM 方向性曝險 **rr8b 94.38%**（Δ加權）／原始市值集中度 **rr8 39.78%**（$255,958）｜避險 rr4t **0.00%**

機構訊號本輪**無任何新增量**（T12/T13/T15 凍結、FP 重複、ARK雜訊已排除），依 [[feedback_tsm_high_conviction_hold]] 維持**不砍倉、不動作**。

- GEX regime 轉強 + CW 站穩但 buffer 收窄，是「觀察不確定性升高」而非「反轉訊號」——不需要因為 GR 翻正就急著加碼，也不需要因為 buffer 收窄就急著減碼。
- Dispersion 擁擠 + 已 94.38% 方向性曝險 + 0% 避險 ⇒ **不建議在此時點加碼 TSM call**。若要動作，優先方向仍是前卡§六的保護窗口：Sep-18/Oct-16/Dec-18 400/360 PS（財報前保護，需下單前重新取價）。

---

## 六、待驗（下週一 08-17 觸發點）

- [ ] 🔴 **T12/T13/T15 週一結算更新後重查**——本輪 OI 全數凍結，下一個真實資料點才會揭曉是否延續
- [ ] **新一份 FP 是否為非 08-13 重複的真實新 session**——覆核 dir= 判決
- [ ] **CW $425 站穩是否延續或被跌破測試**——buffer 已收窄至 +0.32%
- [ ] **data_table 官方牆位是否終於推進**（目前仍卡在 08-11，缺 3 個交易日）
- [ ] **Dispersion Corr Proxy 是否回升 ≥0.08**——若持續探底，強化「不加碼」立場的持續性

---

## 關聯

[[14-08-2026_TSM_strategy]]｜[[14-08-2026_TSM_tracking]]｜[[13-08-2026_TSM_strategy]]｜[[feedback_tsm_high_conviction_hold]]｜[[feedback_fp_log_dedup_by_session_date]]｜[[feedback_top_gamma_delta_exp_caliber_split]]｜[[feedback_wall_levels_ssot_sg_data_table]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_verify_oi_directly_not_fp_absence]]｜[[feedback_us_close_price_only_after_0400_tpe]]
