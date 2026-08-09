# 2026-08-09 TSM IVR/GarchR vs SkewR 背離深度解讀（agy）

> **承接**：[[09-08-2026_TSM_strategy]]（§一 表格兩條觀察的展開）
> **數據時間戳**：同母卡（SG data_table as-of 08-07 session，D−2 校正）

## 縮寫對照
| 縮寫 | 全稱 |
|---|---|
| **IVR** | IV Rank — 隱含波動率在過去一年的百分位（0~1） |
| **GarchR** | Garch Rank — GARCH 模型預測波動率在歷史區間的百分位（0~1） |
| **SkewR** | Skew Rank — 1M 25Δ call vs put IV 差之歷史百分位（高＝call 貴，低＝put 貴；[[kb_skew-rank-direction-convention]]） |
| **RV** | Realized Volatility 已實現波動率 |
| **IV** | Implied Volatility 隱含波動率 |
| **VRP** | Volatility Risk Premium (IV − RV) |

---

## 一、IVR 80%→38%：隱含 vol 整體潮退

**IVR 測量什麼**：當前 1M IV 在過去一年的百分位。

**軌跡**：07/21 的 79.6% → 08/07 的 38.5%，**近乎腰斬**。

**含義**：
- 07-21（閃跌前夕）IV 在年內 80th percentile ＝ 期權市場已提前給高價——**「不安」已定價進去了**。
- 07-29 觸底反彈後，IV 一路降：跌了又漲回來的事件讓 realized vol 從「異常高」回歸「正常」，IV 跟著被拉下。
- 到 08-07 的 38.5%，接近 SG 在 ROMA 裡設的「不賣便宜 vol」閘門 `iv_rank_floor = 0.35`（`vol_calendar.py:292-303`）→ **期權已不算貴了**。

---

## 二、GarchR 78%→55%：模型預測波動率跟著降溫

**GarchR 測量什麼**：GARCH 模型（歷史殘差加權估計的 **predicted vol**）在其歷史區間的百分位。

**IVR vs GarchR 差異**：
| | IVR | GarchR |
|---|---|---|
| 來源 | **市場交易出來的**隱含 vol（contains risk premium） | **統計模型估出來的** RV 前瞻預測（pure statistical forecast） |
| 降速 | 42pp（80→38） | 23pp（78→55） |

**解讀**：
- **GARCH 模型具 volatility clustering 記憶**（近期大跌的殘差衰減較慢），所以 GarchR 比 IVR 降得慢是正常的——模型還「記得」07-29 那波劇烈波動。
- 如果 GarchR 降得比 IVR 還快，那才可疑（代表 implied vol 有無法解釋的 premium）。
- 現況 **GarchR > IVR（55% > 38%）＝ 模型認為 RV 還有降的空間但 IV 已經搶先定價了 → VRP 被壓薄**。市場不只不害怕，甚至比模型更樂觀。

---

## 三、SkewR 20%→86%：Call 被搶＝方向性追價

**SkewR 測量什麼**：1M 25Δ call IV vs 25Δ put IV 之差在過去一年的百分位。依 `kb_skew-rank-direction-convention.md` 明確定義：

> **高（→1.0）＝ call IV 相對 put IV 高 ＝ call 貴**
> **低（→0.0）＝ put IV 相對 call IV 高 ＝ put 貴**

**軌跡**：
| Trade Date | SkewR | 含義 |
|---|---|---|
| 07/21 | 20.1% | **put-skewed**，避險需求尚存 |
| 07/29（底部）| 48.2% | 急速翻中性 |
| 08/05 | **83.2%** | call-skewed，追價升溫 |
| 08/06 | 64.0% | 回落（09-08 tracking 證實 ＝ Dec 500C 大量賣 call 壓出來） |
| 08/07 | **86.0%** | **再衝新高**，86th %ile |

---

## 四、核心：IVR/GarchR 下滑 × SkewR 暴衝 ＝ 什麼訊號？

這不是矛盾，**兩者測量的維度完全不同**——正如 SG 教學（`digest_SpotGamma_skew-iv-rank.md`）反覆強調的「**level vs skew 是二維**」：

| 維度 | 指標 | 訊號 |
|---|---|---|
| **Level（潮位）** | IVR、GarchR | 整體 vol 降溫 ＝ 恐慌消退、市場「穩了」|
| **Skew（浪形）** | SkewR | call 端被搶 → 追價/FOMO/偏多慣性 |

### 組合解讀

> **「風平浪靜但大家在搶船票往上」＝ melt-up chase 訊號**

具體機制：
1. 閃跌 424→375 的 realized vol 消化後，整體 vol 回歸 → **期權便宜了**（IVR 降）
2. 期權便宜＋股價 V 型收復 → **追多者湧入買 call**（SkewR 升）
3. call 買盤推高 call 端 IV，但 put 端沒人要 → skew 扭向 call 端
4. 同時 GarchR 仍在 55%（模型記得波動）而 IVR 已到 38% → **VRP 壓薄，市場比模型更「不擔心」**

---

## 五、這不是避險訊號的三重確認

| 如果是避險/分派 | 你會看到 | 實際看到 |
|---|---|---|
| 機構買 put 保護 | SkewR **降**（put 貴） | SkewR **升**（call 貴）❌ |
| 恐慌性加價 | IVR **升** | IVR **降** ❌ |
| FP 大戶建 put 部位 | sig_positions 有顯著 put delta | 6 週掛零 ❌ |

⇒ **三條避險訊號全不成立**。

---

## 六、操作含義

- **對多頭**：melt-up chase 環境有利持有，但 SkewR 86th %ile 意味 **call 端已擁擠**——如果要加碼，現在追買 call 的「油水」已經被先到者吃掉大半。
- **對保護**：**put 反而是便宜的那一側**。IVR 38% + SkewR 86% ＝ 如果此刻要買 put 保護，成本是近期最有利的窗口之一（整體 vol 低 + put 相對 call 便宜），與 `05-08-2026_TRENDFN` 和 `08-08-2026 _INDEX_` 記錄的「絕對便宜 + 相對便宜同時出現」窗口是同一類型。
- **⚠️ 風險**：melt-up ≠ 永續。當 SkewR 從 86% 回落（如 08-06 的 64%），且 FP 出現 Dec 500C 大量賣 call（[[09-08-2026_TSM_tracking]] §三），已經有人在 SkewR 高位 **主動賣 call 端收割溢價**——這是 overwrite 程式「趁 call 貴收租」的合理行為，也是 SkewR 的天然壓力閥。

---

## 七、方法論沉澱

> **可複用框架**：「IVR/GarchR 降 + SkewR 升」＝ **level 降溫 × skew 追價**的 melt-up 組合。
> 反向組合「IVR/GarchR 升 + SkewR 降」＝ **level 升溫 × skew 避險**的 panic/crash 組合。
> 任何時候同時看到 level 和 skew 往同一方向走（如 IVR↑ + SkewR↑），那是**純粹的 call-side vol bid**（如 squeeze/meme 股），而非結構性的 level-skew 分離。

### ROMA 程式對照
| 檔 | 行 | 內容 |
|---|---|---|
| `data_table.py` | 49-51 | `COL_IV_RANK` / `COL_SKEW_RANK` / `COL_GARCH_RANK` 欄位定義 |
| `vol_calendar.py` | 292-303 | `iv_rank_floor = 0.35`：低 IVR ＝ 不賣便宜 vol |
| `scoring.py` | 33, 51-56 | `_cap_skew_trend`：SkewR > 0.90 時封頂/軟化 D8 |
| `spy_qqq.py` | 197-211 | GarchR < 0.15/0.25/0.35 → squeeze 壓縮乘數 1.3x/1.2x/1.1x |
| `single_stock.py` | 312-320 | 同上 squeeze 乘數（個股版） |
| `relative_top.py` | 19, 169 | ✅ SkewR ≥ 0.90 ＝ call 保護/skew 貴（方向正確） |

---

## 關聯

- 母卡：[[09-08-2026_TSM_strategy]]
- 追蹤：[[09-08-2026_TSM_tracking]]
- 方向公約：[[kb_skew-rank-direction-convention]]｜[[feedback_skew_rank_direction_high_means_call_expensive]]
- SG 教學：[[digest_SpotGamma_skew-iv-rank]]（level vs skew 二維）
- 同類窗口記錄：[[05-08-2026_TRENDFN]]（「絕對便宜＋相對便宜同時出現」）｜[[_INDEX_08-08-2026]]
- 追蹤 SkewR 壓力閥：[[09-08-2026_TSM_tracking]] §三（Dec 500C 大量賣 call）
