# 2026-07-31 Put Wall「支撐」的條件基準率 —— 官方 89%/93% 的分母陷阱與對沖飽和機制

> ⚠️ **本篇對 [[kb_put-wall-support-mechanics]] 引用的官方 base rate 提出「條件化限定」**
> （非證偽其機制論述；機制部分完全採納。修正的是 **89%/93% 的分母** —— 那是無條件統計，
> 條件化到「真的觸及 PW」之後守住率降到 **66.7%**，SPY 單標的僅 **53.8%**。）
> 同時修正本 session 我自己在 SMH 對話中「跌破 PW 會加速下跌」的**強度**陳述 —— 見 §5.3。

**觸發**：討論 SMH 530 履約價（put OI 29,594、GEX −71.1M）是否等於「較強支撐」。
**資料日**：keyLevels 樣本 2026-04-27 ~ 2026-07-31；SMH 個案為 2026-07-31 盤中（10:53 ET）。

---

## 0. 縮寫對照

| 縮寫 | 全稱 | 備註 |
|---|---|---|
| PW | Put Wall | SG 定義的 put gamma 最大履約價 |
| CW / KG / HW | Call Wall / Key Gamma / Hedge Wall | |
| GEX | Gamma Exposure | dealer 側 net gamma notional |
| OI | Open Interest | |
| 0DTE | Zero Days To Expiration | 當日到期 |
| flip | gamma flip point | net GEX 由負轉正的 spot |
| BTO / STO | Buy To Open / Sell To Open | |
| FP | FlowPatrol | SG 的大單流量報告 |
| CI | Confidence Interval | 本篇一律 bootstrap 95%，n=10,000 |
| pp | percentage point | 差值單位，與 % 區分 |

---

## 1. 研究問題

零售直覺：**「某履約價有大量 put OI ⇒ 那裡是支撐」**。

SG 官方替這個直覺背書了一組數字（`digest_SpotGamma_key-levels-series-1to7.md:66-68`）：

> put wall 對 S&P 在 **89%** 交易日守住支撐；**93%** 的時間 S&P 收在 put wall 之上。

而 ROMA 直接把這組數字寫進了 `put_wall_support` 訊號的 detail、並綁定 `action="buy_dip"`
（`romasys/src/opportunities/sg_signals/equity_signals.py:762-764`）。

本篇問三件事：

- **Q1** 觸及 PW 之後的前瞻報酬，是否優於**同條件對照組**（同樣回檔到近期低點、但沒碰到 PW）？
- **Q2** 89%/93% 這組守住率，換成「真的接近 PW 時」的分母之後還剩多少？
- **Q3** 「守住」與「跌破」之後的分佈差多少？（我在 SMH 對話裡宣稱跌破會加速，該檢驗）

---

## 2. 理論框架：支撐來自「對沖飽和」，不是「有人承接」

這一段完全承襲 [[kb_put-wall-support-mechanics]]，僅重述為本篇檢定的前提。

### 2.1 符號分水嶺（決定一切的一格）

| 客戶側 | dealer 側 | dealer gamma | 價格下跌時 dealer 動作 | 對價格的效果 |
|---|---|---|---|---|
| **賣** put（CSP／收租） | **long** put | **正** | \|Δ\| 上升 → **被迫買股** | 🟢 機械性買盤＝真支撐 |
| **買** put（買保護） | **short** put | **負** | \|Δ\| 上升 → **被迫賣股** | 🔴 機械性賣壓＝加速器 |

⇒ **同一道厚 put OI 牆，兩種歸屬結論完全相反。** 只看 OI 數字無法判斷，必須看符號。

而我方 chain 自算 GEX 的「call 記 +、put 記 −」是**慣例假設**（假設 dealer 空 call 空 put），
不是實測；必須靠 FP 列尾 `dir=` 交叉驗證（[[feedback_fp_spread_label_leg_check]]、
[[project_gex_recompute_from_chain_fallback]]）。

### 2.2 就算是「真支撐」，止跌機制也不是承接而是耗盡

dealer long put 的買盤來自 Δ 隨價格下跌而變化（Γ）。當 put 深度 ITM，**Δ → −1、Γ → 0**，
對沖已做滿，**再跌也不會再買**。這就是 [[kb_put-wall-support-mechanics]] 的失效路徑①「Δ 飽和」。

⇒ 正確心理模型是 **煞車皮，不是彈簧**：
- 支撐是「**帶**」不是「線」，強度峰值在 Γ 峰（PW 上方 3–5% 就開始承接）
- 逼近的過程買盤**遞增**，跌穿之後買盤**歸零**（不是變成賣盤，是消失）
- 若是 dealer short gamma（客戶買 put），連煞車皮都沒有，只有加速器

---

## 3. 實驗設計

**腳本**：`py_dir/2026-07-31_putwall_support_baserate.py`

| 項目 | 設定 |
|---|---|
| PW 來源 | `spotgamma_report/auto/market_overview/*_keyLevels.json` 的 `putwallstrike` |
| **防 look-ahead** | 檔名日＝publish 日，`trade_date` 才是資料日 ⇒ PW(trade_date=T) **只作用於 session T+1** |
| 去重 | 同一 `(sym, trade_date)` 被多份 publish 檔重複（停更/重刷）→ 保留最後一份 |
| 標的 | **SPY / QQQ / IWM**；排除 SPX/NDX/RUT（與 ETF 同標的，計入會製造偽重複，見 [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]]） |
| 樣本期 | 2026-04-27 ~ 2026-07-31，**174 個 sym-session**（每標的 58 個 session） |
| 「觸及 PW」定義 | 當日 `Low ≤ PW × 1.005` **且** 前一日收盤 > PW（＝新鮮觸及，非長期在下方） |
| 前瞻報酬 | 自該 session 收盤起算 T+1 / T+5 |
| **無條件對照組** | 全部 174 個 sym-session |
| ★**條件對照組** | 「當日 Low ≤ 前 10 日最低 ×1.005（＝回檔到近期低點）**但未觸及 PW**」 |
| 統計 | bootstrap 95% CI，n=10,000，seed=42 |

**條件對照組是本篇的關鍵設計**。若不設它，就會犯 [[feedback_hitrate_needs_conditional_baseline]]
警告的錯：在一個修復/反彈期裡，**任何**「回檔到近期低點」都會反彈，PW 只是剛好在那裡。

---

## 4. 結果

事件分佈：`touch = 33`（守住 22 / 跌破 11）｜負 gamma 環境佔 `127/174 = 73.0%`

### 4.1 前瞻報酬（%）

**T+1**

| 分組 | n | 平均 | 95% CI | 上漲率 |
|---|---:|---:|---|---:|
| 無條件對照 ALL | 171 | +0.07 | [−0.10, +0.24] | 53.8% |
| 觸及 PW | 32 | +0.53 | [+0.05, +0.98] | 65.6% |
| ★條件對照（觸 10 日低未觸 PW） | 12 | −0.05 | [−0.56, +0.51] | 50.0% |
| 觸及且守住 | 21 | +0.51 | [−0.11, +1.15] | 61.9% |
| 觸及且跌破 | 11 | +0.55 | [−0.12, +1.15] | 72.7% |

**T+5**

| 分組 | n | 平均 | 95% CI | 上漲率 |
|---|---:|---:|---|---:|
| 無條件對照 ALL | 159 | +0.33 | [−0.05, +0.71] | 54.1% |
| **觸及 PW** | 25 | **+2.09** | [+1.30, +2.86] | 84.0% |
| ★條件對照（觸 10 日低未觸 PW） | 9 | +1.08 | [−0.01, +2.01] | 77.8% |
| 觸及且守住 | 17 | +2.52 | [+1.67, +3.41] | 94.1% |
| 觸及且跌破 | 8 | +1.18 | [−0.18, +2.54] | 62.5% |
| 觸及 PW × 負 gamma | 23 | +2.29 | [+1.49, +3.09] | 87.0% |
| 觸及 PW × 正 gamma | **2** | −0.19 | n 太小 | — |

### 4.2 差異檢定（bootstrap 差值 CI）

| 檢定 | 差值 | 95% CI | 判定 |
|---|---:|---|---|
| T+1 觸PW − 無條件對照 | +0.45pp | [−0.04, +0.95] | 含 0，無法拒絕「無增量」 |
| T+1 觸PW − ★**條件對照** | +0.57pp | [−0.15, +1.28] | 含 0，無法拒絕 |
| T+1 守住 − 跌破 | −0.03pp | [−0.92, +0.88] | 含 0，無法拒絕 |
| T+5 觸PW − 無條件對照 | **+1.76pp** | [+0.89, +2.64] | **不含 0** |
| T+5 觸PW − ★**條件對照** | +1.01pp | [−0.21, +2.34] | **含 0，無法拒絕「無增量」** |
| T+5 守住 − 跌破 | +1.34pp | [−0.23, +2.99] | 含 0，無法拒絕 |

➡️ **對上無條件對照顯著（+1.76pp），對上條件對照就消失了（CI 含 0）。**
也就是：那 +2.09% 大部分是「回檔到近期低點會反彈」貢獻的，**不是 PW 這個特定水位的增量資訊**。

### 4.3 ★ 守住率：分母決定一切

| 口徑 | 數值 | n | 對應官方 |
|---|---:|---:|---|
| [無條件] 收盤 ≥ PW | **92.0%** | 174 | 官方 **93%** ✅ 複製成功 |
| [無條件] 盤中 Low ≥ PW | **85.6%** | 174 | 官方 **89%** ✅ 接近 |
| **[條件化] 觸及 PW 後收盤守住** | **66.7%** | **33** | ★ 真正可交易的分母 |

**觸及率只有 19.0%** ⇒ 官方那 92% 裡面，有 **81% 的樣本根本沒接近過 PW**，
是「距離太遠所以自然守住」灌出來的。

分標的更難看：

| 標的 | n | touch | 無條件收 ≥ PW | **觸及後守住** |
|---|---:|---:|---:|---:|
| SPY | 58 | 13 | 84.5% | **53.8%** ← 接近丟銅板 |
| QQQ | 58 | 10 | 96.6% | 80.0% |
| IWM | 58 | 10 | 94.8% | 70.0% |

---

## 5. 結論與行動

### 5.1 官方 89%/93% 不可直接當進場勝率 🔴

那是**無條件**統計，分母含 81% 根本沒接近 PW 的日子。
你真正會用到 PW 的時刻（價格打到那裡），守住率是 **66.7%**，SPY 只有 **53.8%**。

**ROMA 待修**：`equity_signals.py:762-764` 的 `put_wall_support` detail 直接引用
「官方統計（89% 守支撐 / 93% 收其上）錨在此近距離區，此處才是進場點」——
「錨在此近距離區」這句話在資料上**不成立**，官方數字錨在全體交易日，不是近距離區。
建議改述為「無條件 89/93%；條件化到實際觸及後 ~67%（我方 3 個月 index ETF 樣本）」。
訊號本身仍可留，但 `action="buy_dip"` 的措辭應降級。

### 5.2 PW 對「回檔就會彈」沒有增量資訊（本樣本）

T+5 觸 PW 對上條件對照組 +1.01pp、CI [−0.21, +2.34] 含 0。
⇒ **不能宣稱「因為到了 PW 所以會彈」**，只能宣稱「回檔到近期低點後傾向反彈」（而那是 regime）。

### 5.3 ⚠️ 修正我自己：「跌破 PW 會加速下跌」在資料上不成立

我在本 session 的 SMH 回答中，用機制推論斷言跌破會加速。**資料不支持這個強度**：

- 觸及且跌破後 T+5 = **+1.18%**（n=8，CI [−0.18, +2.54]）—— 不是負的
- 守住 − 跌破 = +1.34pp，**CI 含 0**
- 這與 SG 官方「突破後 1 日 +14bps / 5 日 +7bps」方向一致（[[kb_put-wall-break-is-oversold-not-collapse]]）

**該怎麼改述**：跌破 PW 後**分佈變寬、方向不明**（Γ 塌陷 ⇒ 下方無機械性買盤墊底），
**不是**「必然加速下跌」。機制上「買盤消失」≠「賣壓出現」—— 我把這兩件事混為一談了。

### 5.4 機制層仍然成立且仍是首要判別

實證打掉的是「PW 是可交易的支撐水位」這個**強度宣稱**，沒有打掉 §2 的機制。
實務上第一步永遠是問符號：**這批 put 是誰買的？**

SMH 2026-07-31 個案（見 [[../../ls_strategy/31-07-2026_SMH_strategy]]）：
FP `flowpatrol_2026_07_30.log`（session 07-29）明載
`sym=SMH strike=530 type=P exp=2026-07-31 d$=-219.93M oi=23,588 dir=BUY(greek)`
⇒ **客戶買 put** ⇒ dealer short gamma ⇒ 530 是加速器側，不是承接側。
且 530 正落在 chain 自算的負 GEX 谷底（500–530）。
價格實證：07-27 收 548.55 → 07-28 low 518.25 → 07-29 low **503.63**，
**穿透 535 / 530 / 520 毫無停頓**，止跌在 500（那裡有六萬口 BTO put，Δ 飽和）。

---

## 6. 效力邊界（必讀，勿超用）

| 限制 | 說明 |
|---|---|
| **樣本期僅 3 個月** | 2026-04-27 ~ 07-31，且是修復/反彈期（無條件 T+5 +0.33%、up 54%）。**不足以外推到下跌 regime** |
| **正 gamma 樣本 n=2** | Q2（負 gamma 是否讓 PW 失效）**無法檢定**。ROMA 的 S1 降級規則既未被證實也未被證偽 |
| **僅 index ETF** | SPY/QQQ/IWM。個股與板塊 ETF（如 SMH）的 PW 深度、流動性、單一 flow 主導程度都不同 |
| **三標的高度相關** | 有效獨立樣本遠小於 174；CI 實際上比報出來的更寬 |
| **PW 定義用 SG 的** | 未測 chain 自算的 put gamma 峰值；兩者可能不同（SMH 案例中 SG PW=500 已凍結，自算峰值在 530） |
| **未控制到期日** | 未區分 PW 落在近月 flow 牆 vs 遠月 standing OI（[[kb_wall-tenor-flow-vs-standing-oi]] 的維度） |

---

## 7. 待辦

| # | 項目 | 為何重要 |
|---|---|---|
| ☐ 1 | 累積 keyLevels 到 ≥12 個月再重跑，**必須跨一段下跌 regime** | 現樣本的反彈偏誤是最大威脅 |
| ☐ 2 | 補正 gamma 樣本（需要 SG 正 gamma 環境的日子）後重測 Q2 | ROMA S1/S3 降級規則的有效度目前無證據 |
| ☐ 3 | 個股 PW 版本（`history_v4/[SYM]` 的 Low Vol Point）—— index 結論不可直接套個股<br>⚠️ **2026-08-12 前置條件**：個股 PW 走 MO>v4>synth 階層，v4 過期（日曆日>3）會靜默退 synth，實測 TSM/AVGO/QQQ **每週二 100% 換源**、換源日牆位跳幅中位 25–38%（同源日 0–4%）。做這題**必須先過濾到同源日**，否則 PW 逐日換定義，守住率必被污染。見 [[12-08-2026_CC_牆位換源假崩盤與分歧懲罰不對稱]] | SMH/NVDA 類板塊/個股才是我方主要戰場 |
| 🔶 4 | 提 ROMA issue：`equity_signals.py:762-764` 的 base rate 措辭修正（§5.1） | 現行措辭會讓 `buy_dip` 訊號被高估 ／ **2026-08-12 部分完成**（`fb5f1d3` 已限定距離；條件化 base rate 數字仍未寫入）→ 見文末註記 |
| ☐ 5 | 測「PW 上方 3–5% 支撐帶」vs「貼身 <1%」的報酬差 | KB 說支撐是帶不是線，但進場點該站哪裡未量化 |
| ☐ 6 | 把 `dir=` 符號判定接進事件表，分「dealer long put」vs「short put」重測 | §2.1 的分水嶺是機制核心，目前完全沒進統計 |

---

## 8. 附錄

**腳本**：`py_dir/2026-07-31_putwall_support_baserate.py`
**事件表輸出**：`py_dir/fp_trend/putwall_events_2026-07-31.csv`（174 列，含 touch/held/broke/dip 標記）

**ROMA 程式對照**（2026-07-31 現查）：

| 檔案:行 | 內容 |
|---|---|
| `romasys/src/opportunities/sg_signals/equity_signals.py:755-767` | `put_wall_support`（🟢 SUPPORT / `action="buy_dip"`），引用官方 89%/93% ← **§5.1 待修** |
| `romasys/src/opportunities/sg_signals/equity_signals.py:707` | `put_wall_neg_gamma`（🟠 支撐降級 / `monitor_risk`）：淨 dealer gamma 為負時降級 |
| `romasys/src/opportunities/sg_signals/equity_signals.py:737` | `put_wall_support_rolldown`（🟠）：LVP 連日下移＝防線後撤 |
| `romasys/src/opportunities/sg_signals/equity_signals.py:806` | `put_wall_broken_deep`（🟠 / `monitor_risk`）—— 措辭已是 monitor 非「加速下跌」，與 §5.3 一致 ✅ |
| `romasys/src/opportunities/sg_signals/wall_signals.py:20-23` | G2 `pw_downgraded`：兩源分歧＋v4 雙負 → **不應依賴 PW 為支撐做止損/加倉** ✅ 與本篇一致 |
| `romasys/src/opportunities/sg_signals/put_wall_replay.py:1-4` | S3 hit/miss PIT 回放（phase2）—— **可直接擴充成待辦 ☐2/☐5 的驗收框架** |

---

### 📌 2026-08-12 追加註記（行號漂移 ＋ ☐4 部分結案）

**① 上表行號已漂移**（現查 2026-08-12，hostname `e67-4b1`）：

| 內容 | 本篇原記載 | 現況 |
|---|---|---|
| `put_wall_support` 訊號 emit | :755-767 / :762-764 | **:846** |
| `approach_dist_max` 距離閘 | — | **:763** |

⚠️ 舊行號 762-764 **現在仍有程式碼**（是距離閘），只驗「該行號有東西」會得到**假的驗證通過**。
複驗一律 grep 符號名，不跳行號。

**② 待辦 ☐4（base rate 措辭修正）＝ 部分完成**：
commit `fb5f1d3`（*put_wall ⑤ 文案 — 支撐帶≠進場點*）已把官方 89%/93% **限定在
「PW 上方 `approach_max` 內」**，並註明外緣（`approach_max`–5%）是「支撐帶不是進場點」
（`equity_signals.py:853-855`）；另加正 gamma regime ＋ PW 未連降的雙重前置（:840-843）。
**尚未做**：detail 內未寫入本篇條件化後的 66.7% / SPY 53.8%，讀者仍只看得到官方無條件數字。

→ 本註記緣由與後續揭露規則見 [[12-08-2026_CC_證據交換分層與setup有效度盤點]]。

**SGKNOW 佐證**：
`spotgamma_report/knowledge/edu/after_digest/digest_SpotGamma_key-levels-series-1to7.md:66-68`（89%/93% 原文）

---

## 9. 關聯

- [[kb_put-wall-support-mechanics]] — 機制母篇（符號分水嶺／四條失效路徑）；本篇限定其 base rate 分母
- [[kb_put-wall-break-is-oversold-not-collapse]] — 「破了不必然崩」，本篇 §5.3 獨立複現
- [[kb_wall-tenor-flow-vs-standing-oi]] — 近月 flow 牆 vs 遠月 standing OI（待辦 ☐6）
- [[feedback_hitrate_needs_conditional_baseline]] — 本篇是這條規則最完整的實例（89% → 66.7%）
- [[31-07-2026_CC_事後挑贏家與偽重複_三個回測陷阱]] — 排除 SPX/NDX/RUT 的理由
- [[project_fp_p9_extreme_greek_forward_return]] — 「上 put 榜＝下方已 price in」，與本篇 §5.2 相互印證
- [[feedback_wall_levels_ssot_sg_data_table]] — PW 取值的 SSOT 與 as-of 判定
- [[project_gex_recompute_from_chain_fallback]] — SG 停更時自算 GEX；符號慣例需 `dir=` 驗證
- [[feedback_fp_spread_label_leg_check]] — `dir=` 判決的取用方式
- [[21-04-2026_CC_Short_MNQ決策與GEX助漲跌環境]] — 負 gamma regime 的早期筆記
