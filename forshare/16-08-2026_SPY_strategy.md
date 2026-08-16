# SPY 機構尾部保護解構與我方避險策略 — 2026-08-16

> 觸發：`TREND2 TREND SPY`（[[16-08-2026-SPY_TREND2_TREND_agy]]）→ 細解 Put Butterfly 段落 → `SAVEST`
> 產出時間：**2026-08-16（台北週末，美股休市）**
> **現價 as-of：SPY $776.34 / SPX 7,785.76 / VIX 14.26（2026-08-14 確定收盤）**
> 本篇不重複 TREND2/TREND 全篇，只聚焦「機構深度虛值 Put Butterfly」結構解構＋對我方持倉的意涵

---

## 縮寫對照

| 縮寫 | 全稱 |
|---|---|
| OTM / ATM | Out-of-the-Money（價外）/ At-the-Money（價平） |
| Fly | Butterfly（蝶式價差） |
| 1:-2:1 | 買1腳低履約價 : 賣2腳中間履約價 : 買1腳高履約價（等距蝶式標準比例） |
| IVR | IV Rank |
| Skew Rank | Put/Call 相對貴賤的歷史分位排名（方向見下方修正） |
| P/C OI | Put/Call Open Interest Ratio |
| rr4 / rr4t | 指數避險比 / 總避險比（[[feedback_low_hedge_may_be_deliberate_ask_first]] 定義） |
| rr6 | β-weighted 曝險（SPX 等效多頭） |

---

## 一、機構結構解構：10/30 + 11/20 雙月 Put Butterfly

### 1.1 結構本體

| 到期 | 結構（1:-2:1） | 口數 | 蝶心距現價 | 下緣距現價 |
|---|---|---|---|---|
| 10/30 | 470P / 570P×2 / 670P | 75k:150k:75k = 300k | 570P −26.6% | 470P −39.5% |
| 11/20 | 400P / 520P×2 / 640P | 75k:150k:75k = 300k | 520P −33.0% | 400P −48.5% |

兩組同於 8/12 session 建倉，淨成本接近零（中間腳賣 2 口權利金 fund 兩側買進）。

### 1.2 ⚠️ Payoff 關鍵限制（原始 TREND2/TREND 卡未點出）

等距蝶式的 payoff **在兩端都收斂為零**——不只上緣（670P/640P）之上是零，**下緣（470P/400P）之下也是零**。最大獲利精準落在蝶心（10/30 打到 ~$570、11/20 打到 ~$520），跌破下緣後 payoff 不再隨跌幅擴大、反而封頂打平。

**結論**：這不是「線性擴大的無上限尾部保護」，而是精準對沖「−27%~−40%」這個特定中度危機區間的結構；真正 −50% 以上的黑天鵝需要另外的 far-OTM put 或 VIX call 承接（機構本身也同步在做，見 §1.4）。

### 1.3 🔴 Skew Rank 方向修正

原始卡片 §3.1 讀「Skew Rank 96-98th %ile → Put skew 處歷史極值，保護需求重」，經現查 SG data_table 修正：

- `spotgamma_report/auto/data_table/SPX_data-table_2026-08-12.csv` SPY 列：**Skew Rank = 0.98**
- 按已驗證口徑（[[feedback_skew_rank_direction_high_means_call_expensive]]，2026-08-03 QQQ 案例同型誤讀）：**Skew Rank 高＝call 相對貴 / put 相對便宜**，不是「put 貴、保護需求重」
- 用同檔 TLT 列交叉驗證（Skew Rank 0.1767，偏低，對應 TLT 長期 put 溢價明確）方向一致，確認修正成立

**修正後意涵**：SPY 現在 put 相對 call 是「便宜」而非「貴到極值」。這反而**強化**「例行趁便宜買保」的敘事——絕對 IV（IVR 10.85%，data_table 現查值）與相對定價（put 對 call 便宜）兩個維度同時對齊「全年買保護最省錢的窗口」，只是原文措辭方向反了。

### 1.4 定性：例行買保，非賭跌單

機構同時在做的，不只是這組蝶式：

- SG 自己買 ≥1M put/put spread（8/11）
- SG 下週加 VIX calls（8/14 PM 宣布）
- 8/13 session 另有 BTO 745P/735P/739P（16k-18k 口級，中線避險帶，非本篇蝶式的一部分）

蝶式（中度危機區間）＋ 中線 put（近端）＋ VIX call（波動率本身）構成分層避險組合，與「保費全年最低時的例行採購」定性一致。

---

## 二、對我方持倉的意涵

**SSOT**：`brokerage_log/14-08-2026-brokerage.xlsx.log`｜NAV $643,405

| 指標 | 數值 | 讀點 |
|---|---|---|
| rr4（index_hedge_pct） | **0.00%** | 無任何 SPY/QQQ/IWM/DIA put 或 bear put spread |
| rr4t（總避險） | **0.00%** | 完全無避險 |
| rr6（β-weighted） | **282.43%** | SPX 等效多頭曝險遠大於 NAV，主要由 TSM 集中倉位貢獻 |
| rr2（futures_ratio） | 46.41% | MNQ Sep'26×5 口，notional $298,590，margin 計不計入 NAV |
| rr3（gross_leverage） | 2.25x | 已達過度槓桿警示帶 |

**我方目前狀態＝零指數避險 + 高 β-weighted 曝險 + 高槓桿**，恰好與本篇機構觀察到的「保護窗口 8/17-8/20、8/21 OPEX 後關閉」形成直接對照。依 [[feedback_low_hedge_may_be_deliberate_ask_first]]，此處不預設零避險是缺口而主動提問：

**這是否為刻意決策？若否，本篇提供的具體行動選項：**

1. **窗口內（8/17-8/20）低成本試探**：可比照機構思路，用近月 far-OTM SPY/QQQ put spread（非蝶式，蝶式口數門檻高、對我方 NAV 規模不合適）於 IV 全年低檔時建立薄避險，成本遠低於 8/21 OPEX 後
2. **蝶式結構本身不建議直接複製**：300k 口級的口數規模是機構資產配置級別，且如 §1.2 所述其保護區間有限（不覆蓋真正的極端尾部），對我方 NAV $643k 的規模不成比例
3. **若維持零避險是刻意決策**（如判斷 TSM 集中倉位的產業風險與大盤系統性風險相關性低），則本篇僅供背景參考，不需動作

---

## 三、待驗

- [ ] 8/17（一）開盤：ATM IV 是否如預期落在全年最低點，若要行動窗口在此
- [ ] 8/19（三）VIX Exp：SG 只看多到此，留意結構轉折
- [ ] 8/21（五）OPEX：保護窗口關閉，IV 觸底回升預期，錯過窗口後保護費上升
- [ ] 8/26 NVDA ER / 8/27-29 JHOLE：事件溢價集中，若窗口內未動作，此後保護成本明顯墊高
- [ ] Skew Rank 修正是否影響原卡其他段落判讀（本篇僅覆核 §3.1 一處，未逐段複查）

---

## 關聯

[[16-08-2026-SPY_TREND2_TREND_agy]]｜[[feedback_skew_rank_direction_high_means_call_expensive]]｜[[feedback_low_hedge_may_be_deliberate_ask_first]]｜[[feedback_wall_levels_ssot_sg_data_table]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_qqq_call_preferred_mnq_is_fallback]]
