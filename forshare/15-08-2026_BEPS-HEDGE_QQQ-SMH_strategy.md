# QQQ/SMH 避險佈局（BEPS）— 2026-08-15（台北，週六）

## 主題：rr4/rr4b/rr4t 避險比 0.00% × rr3 槓桿 2.25x〈警示〉；QQQ SkewR 0.984 是近月最便宜的買 put 時機窗，趁窗口建立起始避險倉

> **建卡時點＝台北 08-15（週六）**，美股本週最後一個場次是 **08-14（五）收盤**。本卡未跑完整 TREND2/TREND 跨日框架，是單場次「持倉盤點 → 避險缺口 → 具體結構」的快速評估，屬 SAVEST 的輕量版本。
>
> **來源**：
> `brokerage_log/14-08-2026-brokerage.xlsx.log`（持倉 SSOT）
> ＋ `spotgamma_report/auto/market_overview/2026_0815_keyLevels.json`（QQQ 列，trade_date 2026-08-13，D−2 正常滯後）
> ＋ `spotgamma_report/auto/history_v4/{QQQ,SMH}/*_v4_gex_2026-08-15.csv`（同一組 D−2 結構層）
> ＋ yfinance 現查：QQQ/SMH 現價（2026-08-14 收盤）＋ Sep-18'26／Oct-16'26 put chain（即時 bid/ask，抓取時點為台北 08-15 21:48，市場已收盤，值＝上一場次 08-14 定盤）
>
> **產出方式**：即時盤點（非 TREND2/TREND 全流程）→ `SAVEST`
> **姊妹卡**：[[14-08-2026_QQQ_strategy]]（同標的前一版，跨日框架/vol surface 反轉/CW測試——本卡未重跑，直接沿用其 §1 結論作背景）

---

## 縮寫對照

| 縮寫 | 全稱 | 說明 |
|---|---|---|
| BePS | Bear Put Spread（看空／Debit） | [[option_term_conventions]] |
| PW / CW | Put Wall / Call Wall | SSOT＝ `data_table`/`history_v4`（[[feedback_wall_levels_ssot_sg_data_table]]），本卡 QQQ/SMH 皆讀 `history_v4` 的 Low Vol Point / High Vol Point 欄位當 PW/CW proxy |
| IVR / GarchR / SkewR | IV Rank / Garch Rank / Skew Rank | SkewR 高＝call 貴/put 便宜（[[feedback_skew_rank_direction_high_means_call_expensive]]） |
| NAV | 淨資產 | |
| rr3 | gross_leverage（槓桿倍數） | >2.0x 為警示級 |
| rr4 / rr4b / rr4t | index_hedge_pct / sector_hedge_pct / 兩者合計 | [[project_rr4_index_put_only]] |
| DTE | Days To Expiration | |

---

## 1. 持倉對照（SSOT＝`brokerage_log/14-08-2026-brokerage.xlsx.log`）

| 項目 | 值 |
|---|---|
| NAV | **$643,405.08** |
| **rr3 gross_leverage** | **2.25x〈過度槓桿警示〉**（long premium 段下檔封頂 $146,831＝22.8% NAV；期貨/正股才是線性無下限） |
| **rr4 / rr4b / rr4t** | **0.00% / 0.00% / 0.00%**（無任何 index 或 sector put 保護） |
| rr5 cash_ratio | 25.89% |
| rr6 β-weighted | 282.43%（⚠️ TSM 一腳 IV 取不到，用預設 30%） |
| QQQ 等效曝險（rr6-2） | $550,110（85.50% NAV；116股 + 2×Jan27'720C + 2×725C + 5口 MNQ） |
| 半導體整包曝險（TSM+SOXX+SMH+AVGO） | **$825,205（128.2% NAV）**——SMH 直接部位僅 $69,011（10.73%），BEPS SMH 實質是幫整個半導體籃子買保險 |

依 [[feedback_low_hedge_may_be_deliberate_ask_first]]，rr4=0% 本身不預設是缺口；本卡是使用者主動要求評估避險佈局（非本卡主動標紅），故直接進入結構設計。

---

## 2. 時機面（現查，2026-08-14 收盤基準）

| SYM | 現價(08-14收盤) | IVR | GarchR | SkewR |
|---|---|---|---|---|
| QQQ | $731.07 | 0.273（低） | 0.537 | **0.984（極高）** |
| SMH | $587.82 | 0.377（中低） | 0.375 | 0.487（中性） |

QQQ SkewR 0.984＋IVR 27分位低 ⇒ put 相對便宜、且絕對 vol 便宜，雙重利多買方。SMH 中性，無特別時機訊號，純依槓桿需求建倉。

## 3. 牆位（`history_v4`，trade_date 2026-08-13，D−2 正常滯後）

| SYM | PW(Low Vol Point) | CW(High Vol Point) |
|---|---|---|
| QQQ | 660 | 735 |
| SMH | 500 | 600 |

---

## 4. 建議結構（Sep-18'26，36DTE，實查 bid/ask）

短腳一律落在 PW（把「跌破 PW 才賠光」的區間讓給市場換便宜保費）。

| SYM | 結構 | Long ask | Short bid | Debit/組 | Width | Max profit | 倍數 | Breakeven |
|---|---|---|---|---|---|---|---|---|
| **QQQ** | **BePS 715P/660P** | $10.19 | $2.39 | **$7.80** | 55 | $47.20 | 605% | $707.20 |
| **SMH** | **BePS 560P/500P** | $14.70 | $3.50 | **$11.20** | 60 | $48.80 | 436% | $548.80 |

**口數（起始倉，非滿倉避險）**：保費預算抓 NAV 2%（≈$12,868），依 QQQ:半導體整包曝險比≈40:60 分配 →
- QQQ：**6 口**（成本≈$4,680，最大理賠$28,320）
- SMH：**7 口**（成本≈$7,840，最大理賠$34,160）
- 合計保費≈$12,520（≈1.9% NAV）

**Oct-16'26（62DTE）備選**（保費貴約30%但少一次 roll）：QQQ 715/660 debit $10.83（maxP $44.17，408%）；SMH 需另查（本卡未逐一列出，roll 時再現查）。

**選 Sep-18 理由**：34-36DTE 落在常見「≥1個月」避險窗，成本較 Oct-16 低約25-30%，到期需重新校準履約價/roll。

### 4.1 情境：MNQ 平倉後 QQQ 口數重算

同一套「2% NAV 預算、依相對曝險佔比分配」框架，換掉分子(QQQ曝險)/分母(NAV)重算：

| | 原案（含 MNQ） | MNQ 平倉後 |
|---|---|---|
| QQQ 曝險 | $550,110（85.50% NAV，含期貨） | **$251,520**（rr8b 純方向曝險，−54.3%，MNQ 平倉即拿掉槓桿腿） |
| 半導體整包曝險 | $825,205（不變） | $825,205（不變） |
| QQQ 佔比 | 40.0% | **23.4%** |
| NAV | $643,405 | **$657,795**（MNQ +$14,390 UPL 平倉實現併入現金，近似值） |
| 避險預算(2% NAV) | $12,868 | $13,156 |
| **QQQ 避險預算 → 口數** | $5,147 → 6 口 | **$3,073 → 4 口**（成本≈$3,120，最大理賠≈$18,880） |
| （對照）SMH 避險預算 → 口數 | $7,721 → 7 口 | $10,083 → **9 口**（總預算變大＋佔比被 QQQ 讓出） |
| rr3 槓桿 | 2.25x〈警示〉 | **≈1.75x**（脫離警示區間） |

**結論**：MNQ 平倉拿掉槓桿腿後，QQQ 自身避險需求同步變薄（6口→4口），但半導體整包（TSM為主）不受影響，佔比反而被動拉高，同預算下 SMH 反而該加碼（7口→9口）——rr3 脫離警示區間後，槓桿風險集中點從「QQQ+MNQ」轉移到「半導體整包」，BePS SMH 才是重點。

---

## 5. 加碼觸發

- QQQ 收盤跌破 **$715**（=long put 進 ITM，確認下跌動能）→ 加碼同等一輪
- SMH 收盤跌破 **$560** → 加碼同等一輪
- 邏輯類比 [[feedback_squeeze_entry_dual_trigger]]（雙觸發精神，非該筆記直接適用場景）：先開小倉搶便宜時機面，確認突破後再加碼，不把整個避險預算押在單一進場點

---

## 6. 待辦 / 續盯

- [ ] 本卡未跑 TREND2 跨日框架，僅單場次盤點；後續若要驗證 SMH 結構穩定性，建議補跑 `TREND2 SMH`
- [ ] Sep-18 到期前（約 08-15 起算 33 天內）觀察加碼觸發是否命中
- [ ] 到期前 roll：依當時最新 PW/CW 重新校準履約價，不可沿用本卡水位
- [ ] SMH 未見於 `market_overview keyLevels.json`（僅 QQQ/SPX/SPY/DJI 等指數層有收），SMH 水位改讀 `history_v4`，兩者欄位定義是否完全對齊未逐一核對，留待下次 SMH TREND2 一併驗證

---

## 7. 關聯

[[14-08-2026_QQQ_strategy]]（同標的跨日框架前卡，本卡未重跑其 §1 結論，直接沿用背景）· [[option_term_conventions]] · [[feedback_wall_levels_ssot_sg_data_table]] · [[feedback_skew_rank_direction_high_means_call_expensive]] · [[feedback_holdings_ssot_brokerage_log]] · [[feedback_low_hedge_may_be_deliberate_ask_first]] · [[project_rr4_index_put_only]] · [[feedback_squeeze_entry_dual_trigger]]
