# SG 訂閱降到 Essential 的真實代價：欄位層 divergent ≠ 決策層不可用

> 建檔 2026-08-31｜起因：評估把 SpotGamma 訂閱從 Alpha 年繳降到 Essential 是否夠用

## 縮寫對照

| 縮寫 | 全稱 | 語境 |
|---|---|---|
| SG | SpotGamma | 資料供應商 |
| EH | Equity Hub | SG 個股期權影響模組 |
| Total OI | Total Open Interest lens | EH 傳統模型（Essential 有）→ `/v4/historical` |
| Synth OI | Synthetic OI lens | EH 進階模型（**Alpha 年繳限定**）→ `/synth_oi/v1/historical` |
| FN / FP | Founder's Note / FlowPatrol | 每日筆記／異常流量報告 |
| MO | Market Overview | `/home/keyLevels`，6 指數水位 |
| IVR / GR / DR | IV Rank / Garch Rank / Delta Ratio | synth canonical 欄位 |
| PW / CW / VT | Put Wall / Call Wall / Vol Trigger | 關鍵水位 |
| PIT | Point-in-time | 回放／回測的無洩漏基準 |
| kappa | Cohen's kappa | 扣掉「碰巧一致」後的兩源一致度 |

---

## 一、理論框架：訂閱層級 → 端點 → 欄位 owner → 閘門

降級評估容易停在「功能清單有沒有這一項」，但實際代價要沿著四層傳導才看得到：

```
訂閱層級          端點                       欄位 owner              決策閘門
Essential   →  /v4/historical        →  Total OI 版 9 欄   →  Skew Rank ≥ .90 …
Alpha(年繳) →  /synth_oi/v1/historical →  synth canonical 9 欄 →  同上
```

**第 1 層（官方口徑）** — SG Support 2026-08-16 版明列 Essential 的 *Not included*：
TRACE / HIRO / Volatility Dashboard / **Equity Hub Synthetic OI lens**；
Alpha 那行還帶一個容易漏看的括號：`Synthetic OI lens (annual plan only)`
⇒ **Alpha 月繳一樣沒有 synth**。

**第 2 層（端點）** — ROMA 的 SG 取數面（`romasys/src/collectors/sg_downloader/_http.py:13-16`）：

| 端點 | 落檔 | Essential 保得住？ |
|---|---|---|
| `/foundersNotes` | `auto/founders_note/`（160 檔）| ✅ |
| `/flow-patrol` | `auto/flowpatrol/`（235 檔）| ✅ |
| `/home/keyLevels` | `auto/market_overview/`（6 指數）| ✅ Key Levels for major indices |
| `spotgamma.com/wp-json/wp/v2/posts` | `auto/sg_weekly/`（58 檔）| ✅ **零認證**，與訂閱無關 |
| `/v4/historical`（27 欄／9 筆）| `auto/history_v4/`（66 檔）| ✅ 對應 Total OI lens |
| **`/synth_oi/v1/historical`（57 欄／30 筆）** | `auto/synth_oi/`（66 檔）| ❌ **斷** |
| Scanners Export CSV（5,282 檔 × 40 欄）| `auto/data_table/`（92 檔）| ⚠️ **未知**，見 §五 |

**第 3 層（欄位 owner）** — `sg_loaders/caliber.py:71` 的 `COLUMN_CALIBER` 是口徑 SSoT：
v4 的 27 欄有 26 欄與 synth 同名，其中 **9 欄 owner="synth"**（`caliber.py:99-107`），
載入時被 `apply_v4_column_policy()`（`caliber.py:134`，呼叫點 `v4.py:44` / `v4.py:65`）
改名成 `v4_*` 遮蔽 ⇒ `row.get("Garch Rank")` 回 `None` 而非一個貌似合理的浮點數。

**第 4 層（閘門）** — 這 9 欄直接餵四個現行閘門（皆現查行號）：

| 閘門 | 條件 | 出處 |
|---|---|---|
| G1 profit_protect A | `Skew Rank ≥ 0.90` | `sg_signals/profit_protect.py:168` |
| G2 skew_divergence ③ | `IV Rank < 0.40` | `sg_signals/skew_signals.py:66`；值見 `manifest/skew_signals.md:31` |
| G3 crowding 極端 | `IV Rank ≥ 0.90` | `sg_signals/skew_signals.py:403` |
| G4 relative_bottom | `IV Rank ≥ 0.70` | `sg_signals/relative_bottom.py:167` |

**血緣量級**：`load_synth_rows` / `_load_synth_oi_hub` / `SYNTH_OI_DIR` 共 **96 個呼叫點**；
讀 synth-owned 欄位的檔案 **30 個**（skew_signals、regime、relative_top/bottom、profit_protect、
garch_profile、vrp_replay、bias/single_stock、risk/volatility …）。

---

## 二、實驗設計

**研究問題**：降級後只剩 v4 同名欄，**決策**會翻掉多少？（不是「數值差多少」）

- 樣本：本地存檔 `auto/history_v4/` × `auto/synth_oi/`，逐 (SYM, session) 內接
  ⇒ **5,952 列 = 60 檔 × 127 sessions，2026-02-27 ～ 2026-08-28**
  （檔案僅回溯到 2026-05-06，但每份 CSV 內含 9／30 筆歷史列，故樣本上溯到 2 月底）
- 同 session 出現在多份快照時取檔名最新那份，與 loader 的 `_pick_file_as_of` 同向
- 指標：
  - 欄位層：中位 |相對誤差|、>10%／>50% 佔比（以 synth 為分母）
  - 決策層：翻轉率（+Wilson 95% CI）、**漏發** `P(v4 不觸發 | synth 觸發)`、
    **誤發** `P(synth 不觸發 | v4 觸發)`、kappa
- **對照基準**：不是 50%。用「兩源邊際觸發率不變但彼此獨立」時的期望不一致率
  （若 v4 與 synth 只是碰巧邊際像、逐列其實無關，翻轉率應該長這樣）

與 `py_dir/10-08-2026_v4_vs_synth_shared_columns_audit.py` 分工：那支做**欄位層**，本支做**決策層**。

---

## 三、結果

### ① 欄位層（owner=synth 的 9 欄，v4 同名欄 vs synth canonical）

| 欄位 | n | 中位 &#124;相對誤差&#124; | >10% 佔比 | >50% 佔比 |
|---|---:|---:|---:|---:|
| IV Rank | 5,946 | 1.3% | 29.1% | 13.2% |
| Garch Rank | 5,946 | 2.8% | **41.6%** | 22.4% |
| Skew Rank | 5,946 | 3.7% | 25.6% | 5.2% |
| Skew | 5,541 | 4.6% | 30.8% | 8.7% |
| NE Skew | 5,555 | 8.5% | **45.6%** | 14.7% |
| 1 M IV | 5,952 | 0.1% | 0.9% | 0.1% |
| 1 M RV | 5,952 | 2.0% | 5.1% | 0.4% |
| Options Implied Move | 5,952 | 0.1% | 0.8% | 0.1% |
| Put/Call OI Ratio | 5,545 | 1.3% | 13.6% | 0.0% |

與 `caliber.py` 的分帶一致：Garch Rank / NE Skew / Skew 是 divergent 群，
`1 M IV` / `Options Implied Move` 幾乎可互換（near）。

### ② 決策層（synth = canonical 真值，v4 = 降級後唯一可得）

| 閘門 | n | synth 觸發率 | v4 觸發率 | 翻轉率 [95% CI] | 獨立基準 | kappa | 漏發 | 誤發 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| G1 `Skew Rank ≥ .90` | 5,946 | 20.6% | 23.4% | 4.8% [4.3, 5.4] | 34.4% | 0.86 | 4.8% | **16.2%** |
| G2 `IV Rank < .40` | 5,946 | 38.1% | 30.5% | 9.8% [9.1, 10.6] | 45.4% | 0.78 | **22.8%** | 3.7% |
| G3 `IV Rank ≥ .90` | 5,946 | 10.0% | 11.9% | 2.5% [2.2, 3.0] | 19.6% | 0.87 | 3.0% | **18.6%** |
| G4 `IV Rank ≥ .70` | 5,946 | 28.4% | 32.3% | 5.8% [5.3, 6.5] | 42.4% | 0.86 | 3.4% | **15.1%** |
| G5 `Garch Rank ≥ .80`（示意）| 5,946 | 8.2% | 9.5% | 1.8% [1.5, 2.2] | 16.1% | 0.89 | 3.1% | 16.1% |

---

## 四、結論

**① 欄位層 divergent 不等於決策層不可用 —— 這是本篇最反直覺的一點。**
Garch Rank 有 41.6% 的列相對誤差 >10%，但同一欄的 0.80 閘門翻轉率只有 1.8%。
原因是 rank 類欄位大量分佈在遠離閾值的區間，數值差再大也不改變布林結果。
kappa 0.78–0.89、翻轉率全部只有獨立基準的 1/5 ~ 1/7 ⇒ v4 **不是**另一個隨機源。
（本篇對「v4 完全不能替代」的直覺提出**部分**修正；`caliber.py` 的遮蔽設計仍然正確——
它守的是「誤用做不到」，不是「兩源預測力差很多」。）

**② 但代價是非對稱的，而且落在最貴的方向。**
四個真實閘門的**誤發率 15–19%**：降級後每 6 個訊號約有 1 個是 synth 不認的假訊號。
G2 更糟，**漏發 22.8%**——每 4~5 個真訊號漏掉 1 個。以 profit_protect（大贏家鎖利）
為例，16.2% 誤發 = 每 6 次減倉建議有 1 次是資料源造成的，這種錯誤在強勢股上很貴。

**③ 真正不可替代的不是欄位，是「30 日窗」與「時序連續性」。**
- synth 30 筆 vs v4 9 筆 ⇒ 所有 `rot_lookback` / 多日滑窗類邏輯的可用窗腰斬
- 換源當天所有 rank 類時序出現永久結構斷點（同「牆位每週二換源假崩盤」的病，
  只是變成一次性、不可回復）
- 本地 66 檔 × 64 天的 synth 存檔降級後**停止增長**，PIT replay 樣本就此凍結

**④ HIRO / TRACE / Volatility Dashboard 損失 ≈ 0。** 這三項沒有 fetcher、不進管線，
且 HIRO 日終淨值已被判定非隔夜方向訊號。真正的成本 100% 集中在 Synth OI 一項。

**⑤ 價差**：Alpha 年繳 $2,691／年 vs Essential 年繳 $891／年 ⇒ **$1,800／年**。
換算：買回 4 個閘門的 15–19% 誤發率 + 30 日窗 + 樣本連續性。

### 行動

- **維持 Alpha 年繳**（且不要為了彈性改月繳——月繳同樣沒有 synth）。
- 若未來仍要降，降級前必做：① 備份 synth／data_table 存檔；② 向 SG 客服確認
  Essential 下 Scanners Export CSV 是否仍含 IV Rank / Skew Rank / Garch Rank
  且值由哪個模型算；③ 改寫 `caliber.py` 的 owner 表並在切換日標 regime break。

---

## 五、未解未知數：data_table 的存活性

`collectors/sg_data_table.py:7` 自述：Scanners Export CSV 是 SPA 前端把
**`/synth_oi/v1/equities`**（`sg_data_table.py:63` 用它當「資料就緒」訊號）+ `/home/keyLevels`
+ DPI 衍生欄拼出的 client-side blob；那 40 欄裡含全部 9 個 synth-owned 欄位。

Essential 名義上「有 Scanners」，但降級後三種結果都可能：
(a) 欄位整段消失、(b) 欄位還在但改由 Total OI 算（**值靜默翻轉，最惡劣**）、(c) 不變。
**事前無法從外部驗證**——這是本評估唯一沒有數據支撐的環節，只能問客服或實測。

若 (c) 成立，data_table 反而是最佳降級路徑：覆蓋 5,282 檔（>> synth 的 66 檔），
且自 2026-05-04 起已累積 92 天自家歷史；代價是只有當日快照、無 30 日窗。

---

## 待辦

- [ ] 向 SG 客服確認 Essential 下 Scanners Export CSV 的欄位存活與計算模型（§五）
- [ ] 把「誤發 15–19%」納入 `profit_protect` 的降級預案：若真降級，`skew_rank_min`
      需重新校準（現行 0.90 是對 synth 分佈校的，v4 觸發率系統性偏高 20.6%→23.4%）
- [ ] G5 用的 0.80 是示意閾值，不是現行閘門；若日後 garch 壓縮訊號要固化閾值，回頭補實測

## 附錄

- 本篇腳本：`py_dir/31-08-2026_v4_vs_synth_gate_flip_audit.py`（可重跑，無外部相依）
- 前作（欄位層）：`py_dir/10-08-2026_v4_vs_synth_shared_columns_audit.py`
- 口徑 SSoT：`romasys/src/opportunities/sg_loaders/caliber.py:71`（表）／`:99-107`（9 欄）／`:134`（遮蔽）
- 端點常數：`romasys/src/collectors/sg_downloader/_http.py:13-16`
- 取數：`sg_downloader/synth.py:112`（v4）／`:143`（synth）
- 官方來源：SG Support「What is included in each SpotGamma subscription plan? (Essentials vs Alpha)」
  （article 50272097356819，2026-08-16 更新）／`spotgamma.com/subscribe-to-spotgamma/`

## 關聯

- [[30-07-2026_CC_HIRO日終淨值非隔夜方向訊號]] — 為什麼失去 HIRO 對管線損失 ≈ 0
- [[08-08-2026_CC_Garch壓縮跨標的軟體股前兆觀察]] — 用的 Garch Rank 正是 owner=synth 欄
- [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] — 本篇刻意用獨立基準而非 50% 的同一紀律
- [[19-08-2026_CC_聚合層級先於保守化_列權重假象]] — 「聚合層級決定結論」的另一個實例：
  欄位層與決策層看同一批資料會給出相反的可用性判斷
