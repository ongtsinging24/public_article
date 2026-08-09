# 2026-07-13 TSM 策略卡 — FP_TREND 全段重解（買方側符號）＋ 財報前最後 2 個交易日

> **數據時間戳**
> - 現價 **$430.33**（yfinance，07-13 收盤；抓取 2026-07-13 23:34）｜前收 434.11（07-10）｜**當日 −0.87%**
> - 結構水位 SG `data_table` **2026-07-13**（SSOT，[[feedback_wall_levels_ssot_sg_data_table]]）
> - FP 最新 session = **2026-07-10**（`flowpatrol_2026_07_12/13.log` 內容相同，07-13 場次尚未 publish）
> - 我方持倉 SSOT = `brokerage_log/13-07-2026-brokerage.xlsx.log`（[[feedback_holdings_ssot_brokerage_log]]）
>
> 承接：[[event_tracking/13-07-2026_TSM_tracking]]（符號定案＋collar rollout 解碼）｜[[10-07-2026_TSM_strategy]]（§2b 已證偽）

## 縮寫對照
- **FP** = FlowPatrol（SG 盤後機構期權流）｜**session** = FP 內文的真實場次日（≠ 檔名 publish 日）
- **d$ / g$ / v$ / prem** = FP 的 $Delta / $Gamma / $Vega Chg 與權利金。**符號 = 買方(BuySide)側**（+ = 買/付出，− = 賣/收取），07-13 定案（[[kb_fp-greek-sign-convention]]）
- **bto / sto** = SG 成交分類欄。⚠️ **不可當方向依據**（包裹單逐腳反號 + 只分類部分成交量）→ 一律以 greek 為準
- **KG / KD** = Key Gamma / Key Delta Strike｜**CW / PW / HW** = Call / Put / Hedge Wall
- **IVR / GR / SR** = IV Rank / Garch Rank / Skew Rank｜**DPI** = Dark Pool Index｜**DR** = Delta Ratio
- **RR** = Risk Reversal｜**IC** = Iron Condor｜**collar** = 買下檔 put ＋ 賣上檔 call｜**BMO** = 盤前發布

---

## 一、當下狀態（一句話）

**機構是「被 collar 罩住的多」，我方是「82.9% 曝險、零保護的裸多」，而財報在 2 個交易日後。**
方向判斷不用改（仍偏多），要改的是**風險結構**：補下檔保護，且保護要活過財報。

---

## 二、結構水位（SG data_table 2026-07-13）

| 項目 | 數值 | 讀法 |
|------|------|------|
| Current Price | **435.10**（SG 快照）／**430.33**（07-13 實收） | SG 快照略高於實收，以實收為準 |
| **Earnings Date** | **07-16 BMO（盤前）** | **只剩 07-14、07-15 兩個交易日可調部位** |
| Key Gamma Strike | **460** | ← **機構 collar 的履約，就是 KG** |
| Key Delta Strike | **400** | ← **機構反覆 roll 的 call 履約，就是 KD** |
| Hedge Wall | 440 | 現價 430 在 HW 之下 → dealer 偏負 gamma |
| Call Wall | 480 | 上緣（≈52wk 高 479） |
| Put Wall | **420** | **距現價僅 −2.4%**；破 420 負 gamma 助跌 |
| IV Rank | 0.851 | 高 |
| Garch Rank | 0.809 | 高 |
| Skew Rank | **0.932** | **極高 → 市場願為下檔付溢價** |
| 1M IV / 1M RV | 52.7% / 60.3% | **VRP 為負**（IV < RV）→ 買選擇權相對不貴 |
| Options Implied Move | **±$14.45（≈ ±3.3%）** | 單位為「點數」，由跨標的比對推得（SPY 6.05 / NVDA 5.07 皆為點）<br>→ 財報 ±1σ 區間 **≈ 416 – 445**，**PW 420 正好落在 −1σ 邊緣** |
| P/C OI Ratio | 1.246 | put 持續累積 |
| DPI / 5d DPI | 39.9 / 38.2 | 低 = 暗池偏空 |
| Delta Ratio | −2.075 | ⚠️ **這是 data_table 口徑（帶號恆負）**，與 07-11 卡的 synth +2.120（恆正）**不是同一個東西**，<br>不可互比。兩者 \|DR\|≈2.1 一致 → call 主導。三模型口徑見 [[kb_delta-ratio-three-models]]、§7-b |

---

## 三、機構足跡全段（FP_TREND，方向一律由 greek 判、忽略 bto/sto）

```
session  現價     機構動作（買方側）                        權利金       證據／備註
──────────────────────────────────────────────────────────────────────────────────
05-29   418.61   買 Dec18-350P                            —           v$ +320K = 買  ← 遠月尾部保護早已在
06-01   436.01   賣 Sep18-430C ＋ 買 Sep18-510C           淨收 50.1M   兩腳 tot_vol 均 156,506 = package
                 ＝ 平掉 430/510 bull call spread（獲利了結）
06-09   427.85   賣 Jun18-400C ＋ 買 Jul17-400C           淨付 9.9M    400C 由 6 月 roll 到 7 月
                 ＋ 賣 Jul17-350P                                      標籤寫 "Condor Open" ← 標籤錯
                 ★ sig_position 三軸全 96th 百分位                     d$/g$/v$ = 96 / 96 / 96
06-12   423.78   賣 Jul17-420C ＋ 賣 Jul17-420P（收租）    —           ＋ 買回 Jun18-400C 平倉
06-18   462.22   賣 Jul17-450C（當天 +6.99%，高點封頂）    —           g$ −16.31M / v$ −606K = 賣
                                                                       bto=12,202 僅分類 11% ← 陷阱列
06-23   436.62   ★買 Jul17-460P（當天 −6.63%）            付 38.93M    prem / v$ / d$ 三欄互證 = 買
                                                                       ← 460 保護的起點
06-25   435.25   IC：賣 Jul17-440C ＋ 賣 Jul17-390P        —           兩邊收租
06-26   432.35   ★賣 Jul17-400C ＋ 賣 Sep18-400P          收 81.91M    四欄全負；SG 原文 "large call sale"
                 ★ sig_position 崩到 d 9th / g 4th / v 10th            ← 19 天內從 96th 翻到 4th
06-29   455.06   買 Sep18-400C ＋ 賣 Jul31-420P           付 61.05M    v$ +538K = 買
06-30   477.24   買 Sep18-400C ＋ 賣 Sep18-420P（Bull RR） 付 65.54M    Sep400C OI 14.7k → 21.7k
──────── 07-01 ~ 07-09：機構 flow 完全靜默（7 個交易日）────────
07-10   434.29   ★★460 collar rollout：Jul-17 → Aug-21    —           package 四腳，bto/sto 全反號
──────── 07-13：FP 尚未 publish（明日確認）────────
```

**07-10 四腳逐腳覆核**（[[kb_fp-spread-label-vs-greek-sign]]：標籤不可信，逐腳看 greek）：

| 腳 | greek | 買方方向 | 意義 |
|----|-------|---------|------|
| Jul17-460**P** | d$ **+149.37M** | **賣出** | 平掉舊 put 保護 |
| Jul17-460**C** | d$ +86.64M、g$ **+13.69M** | **買回** | 平掉舊 short call |
| Aug21-460**C** | d$ **−84.25M** | **賣出** | 新 short call |
| Aug21-460**P** | d$ −111.22M、g$ **+3.91M** | **買進** | 新 put 保護 |

→ **整組 = 把 460 collar 從 Jul-17 展期到 Aug-21**。OI 兩兩相同（Jul 20,170/20,170；Aug 16,250/16,250）→ `is_package_leg()` 判定 package。
**機構不是解除保護，是把保護延長到財報之後。**

### 三-b 現金流總帳（有 prem 欄的大單，買方側）

| 付出（買） | 金額 | 收取（賣） | 金額 |
|-----------|------|-----------|------|
| Sep18-510C（06-01） | 25.68M | Sep18-430C（06-01） | 75.76M |
| Jul17-400C（06-09） | 39.92M | Jun18-400C（06-09） | 30.03M |
| **Jul17-460P（06-23）** | **38.93M** | **Jul17-400C（06-26）** | **81.91M** |
| Sep18-400C（06-29） | 61.05M | Sep18-420P（06-30） | 12.65M |
| Sep18-400C（06-30） | 65.54M | | |
| **合計** | **231.12M** | **合計** | **200.35M** |

**機構整段淨掏錢僅約 $31M** → 結構是「**賣近月 call 收到的錢，拿去養遠月 call ＋ 下檔 put**」。
**不是裸多，是自融資的 diagonal + collar。**

### 三-c 三個新發現（07-13 追蹤卡未涵蓋）

**① 機構的兩個履約錨點 = SG 的兩道結構水位。**
機構整段只反覆操作 **400**（Jun→Jul→Sep 一路 roll call、加賣 400P）與 **460**（買 put → roll collar）。
而 data_table 給的 **Key Delta Strike = 400、Key Gamma Strike = 460**。
兩條獨立資料鏈（FP 逐筆 flow vs data_table 聚合水位）指向同一組數字
→ **機構部位大到自己把水位釘出來了；460 collar 不是隨手掛的價位，是 gamma 重心。**

**② 賣 call 履約一路下移，8 月又搬回 460。**
450（06-18，價 462）→ 440（06-25，價 435）→ 400（06-26，價 432）：封頂位跟著價格往下壓。
但 07-10 的新 short call 腳是 **Aug21-460C**。
→ **近月極度保守（賣到價內 400C），財報後卻把上緣重新放回 460。** 這比單看 07-10 更能解釋 collar 的形狀。

**③ 下檔保護是三層、從未斷過。**
Dec18-350P（05-29，尾部）→ Jul17-460P（06-23，已平）→ Aug21-460P（07-10，現行）。
**機構沒有一天是沒保護的。** 我方 rr4 = 0%。

---

## 四、我方持倉（SSOT：`brokerage_log/13-07-2026-brokerage.xlsx.log`）

```
股票   TSM ×400 股                          mv  175,200   UPL +26,490
選擇權 TSM Sep18'26 400C ×5                 mv   29,383   UPL    +176
       TSM Sep18'26 420C ×2                 mv    9,456   UPL    +539
       TSM Nov20'26 380C ×2                 mv   17,266   UPL  +1,770
       TSM Nov20'26 400C ×2                 mv   14,893   UPL    −292
       TSM Jan15'27 400C ×2                 mv   16,941   UPL  −2,850
```

| 風險比 | 數值 | 評語 |
|--------|------|------|
| NAV | $689,002.90 | |
| **rr8b TSM 方向性曝險** | **+$570,937 ＝ NAV 的 82.86%** | ⚠️ 單一標的吃掉 8 成 NAV |
| rr8 TSM 市值集中度 | $263,140 ＝ 38.19% | |
| **rr4 index put 保護** | **0.00%** | ⚠️ **零下檔保護** |
| rr3 gross leverage | 1.32x | 中度 |

**方向與機構一致（多），但結構完全不同：機構有 collar、有近月收租、有三層 put；我方全是裸 long call ＋ 現股。**
※ rr4=0% ≠ 無保護，但本次確認：TSM 個股層面**確實沒有任何 put/collar**（[[project_rr4_index_put_only]]）。

---

## 五、決策

### 5.1 立場
- **核心多單不減**（[[feedback_tsm_high_conviction_hold]]）。TSM 方向論點未變，機構遠月仍偏多（Sep18-400C 兩天砸 $126.6M）。
- **要補的是保護，不是砍倉。** 這不是「新發現的風險」而是「一直缺的結構」（[[feedback_no_flip_without_entry_context]]）。
- **collar 已從「我方風控提議」升級為「與機構同型的動作」**——07-10 機構做的正是買下檔 put ＋ 賣上檔 call ＋ 跨過財報。

### 5.2 方案 F′（修正版 collar；**put 腳月份是本次唯一實質修改**）

| 腳 | 內容 | 理由 |
|----|------|------|
| **買 put** | **Aug21-420P ×6**（或 Jul17 / Aug21 各 3 口對半） | **420 = PW，且正好在財報 −1σ（±$14.45）邊緣**。<br>**月份跟機構走**：機構自己花錢把保護從 Jul-17 搬到 Aug-21 |
| **賣 call** | Sep18-480C ×2 | 480 = CW ≈ 52wk 高 479；不動現股與 5 組 Sep400C |

**為何 put 腳要離開 Jul-17（本卡對 [[event_tracking/11-07-2026_TSM_tracking]] 方案 F 的修正）**
Jul-17 到期只比財報（07-16 BMO）**晚一天**。用 Jul17-420P ＝ **只買那一根跳空**，跳空一過就歸零，
**保護不了財報後的續跌**。機構原本的保護就是 Jul17-460P，卻在 07-10 **花錢**把它 roll 到 Aug-21 ——
它用真金白銀告訴你：**風險不在跳空那一天，在財報之後。**

**取捨**：Jul-17 = 最便宜的純事件險；Aug-21 = 機構選的、涵蓋 post-earnings 續跌（貴，但 VRP 為負 → 買方不吃虧）。
**建議：至少一半保護放 Aug-21；若成本允許，全放 Aug-21。**

### 5.3 ⚠️ 未完成的前置（不可跳過）
- 方案 F 的「零成本」是 **BS 估價、非真實 chain**。財報週 put IV 可能衝 75%+。
- **07-14 開盤必須用實際買賣價複核**：`Jul17-420P` / **`Aug21-420P`** / `Sep18-480C` 三腳報價。
- 若 Aug21-420P 成本明顯為負（付太多）→ 退路是**賣 100–200 股 TSM 轉 BOXX**（[[feedback_derisk_to_cash_not_defensive_equity]]，**不接受 rotate to 防禦股**）。

---

## 六、時間表（硬約束）

```
07-13（一）已收盤 430.33 −0.87%，未動作 ← 已用掉一天
07-14（二）★ 報價複核 + 下單（建議日）
07-15（三）★★ 最後一班車（收盤前必須完成）
07-16（四）BMO 財報 → 跳空
```

**只剩 2 個交易日。** 每拖一天，put IV 只會更貴。

---

## 七、驗證點 / 失效條件

- ☐ **07-14 盤中**：Jul17-420P / **Aug21-420P** / Sep18-480C 真實報價 → 決定 collar 月份與是否仍近零成本
- ☐ **07-14 FP publish（07-13 場次）**：TSM 有無新腳？特別看 **Aug21-460C / 460P 的 OI 是否續增**
      → 增 = 機構加碼保護（跟進）；減 = 機構平倉（重新評估）
- ✅ **`regime.py` 的 DR 閘誤用 v4 口徑 → 已結案（ROMA v3.36，2026-07-15）**（見 §7-b）
      → PIT 回放裁決：**DR 方向軸整個拔除**（不是判反，是「閘在 cohort 內恆真＝資訊量為零」）
      → 「🔴 NDX 下行 Gamma Crash / emergency_hedge」**該論據作廢**；該象限現輸出「⚡ 雙向負 Gamma・波動放大・方向待定」
      → [[event_tracking/13-07-2026_TSM_tracking]] §4 的「疊加宏觀 🔴NDX 負gamma risk-off」**已撤回**
      → 結案卡：[[../romasys/document/todo_idea/14-07-2026_regime-DR閘誤用v4口徑]]｜口徑：[[kb_delta-ratio-three-models]]
- ☐ 現價 430 能否守 **PW 420**？破 420 進負 gamma 助跌區（且 420 = 財報 −1σ）
- ☐ **07-16 BMO 後**：IV crush 幅度、守 420(PW) / 收復 440(HW)？
- ✅ FP 符號定案（買方側）→ 6 月以來所有「方向未定」事件已全部結案
- ✅ [[10-07-2026_TSM_strategy]] §2b「機構沒替 TSM 封頂／大單都是買 call」→ **已證偽**（機構近月一路賣 call：450→440→400）

**本卡失效條件**：若 07-14 FP 顯示機構**平掉** Aug21-460 collar（OI 大減）→ 「跟機構做 collar」的論據消失，退回純風控口徑重評。

---

## 七-b、✅ regime 的 DR 判讀為何作廢（2026-07-14 查證 → **2026-07-15 結案，v3.36 已拔除**）

**這一節取代本卡初版的「DR 符號矛盾」驗證點——那是假警報，真問題在別的地方。**

**假警報的部分**：SG 有**三個模型**各自輸出一欄叫 "Delta Ratio"，三個數字都對，只是不能互比。
`kb_datatable-vs-synth-gamma-delta-ratio-caliber.md`（2026-07-06）早已寫明「不可互換」，我沒先查 KB 就喊矛盾。

| 來源 | 公式 | 符號 | TSM 07-13 |
|------|------|------|-----------|
| **synth**（Synthetic OI） | `\|CallΔ ÷ PutΔ\|` | **恆正** | +2.1199（= 07-11 卡引用的 +2.120，結構日 07-09） |
| **data_table**（Scanners） | 自身模型、帶號 | **恆負** | −2.0754 |
| **v4**（GEX_History） | `CallΔ ÷ \|PutΔ\|` | **帶號** | −3.017 |

**真問題**：`regime.py` 的 `detect_index_regime()` 把 **synth 校準的門檻**（`dr_bull=1.0` / `dr_bear=0.5`，
為恆正比值設計）套在 **v4 的帶號 DR** 上。

全宇宙實測（75 標的 / 46,123 列 v4 GEX_History）：
```
負 = 45,433 (98.50%)   正 = 690 (1.50%)   零 = 0
→ dr_bear=0.5 命中率 = 98.50%  ← 「🔴 下行 Gamma Crash / emergency_hedge」幾乎無條件觸發
→ dr_bull=1.0 命中率 =  1.50%  ← 「🚀 上行 Gamma Squeeze」幾乎是死碼
```

~~**而且符號可能判反**：07-13 scan 的 NDX `|DR| = 2.19 > dr_bull = 1.0` → 應判「上行 Squeeze / 偏多」，
實際輸出卻是「下行 Crash / 偏空」。方向相反。~~

### ✅ 結案（ROMA v3.36，2026-07-15）：不是「判反」，是**那個閘不存在**

上面那段推論**本身也錯了**（它拿 `|DR|` 去對門檻，但 prod 比的是**帶號** DR）。PIT 回放（3,833 事件 /
75 標的 / 2026-02→07，去市場漂移 alpha）給出的真相更徹底：

| 檢驗 | 結果 |
|---|---|
| `negative+高GR` cohort（n=1,367）| `emergency_hedge` 觸發 **1367/1367 ＝ 100%**、上行 squeeze **0 ＝ 死碼** |
| `negative+低GR` cohort（n=2,138）| 2026-05-31 加的「下行確認閘」擋下 **0/2138 ＝ 假修** |
| 改用 `abs(DR)` 能否救 | ❌ `\|DR\|` 五分位 α5d 非單調 ＝ **無區辨力** |

**★ 一個在自己 cohort 內 100% 觸發的閘，資訊量是零。它既不是「判反」也不是「歪打正著」——它不存在。**
真正在做事的一直是 `regime==negative` 和 `GR>1.5` 兩軸，DR 只是搭便車。

**處置**：DR 方向軸已從 `detect_index_regime` **整個拔除**；該象限現輸出「⚡ 雙向負 Gamma・波動放大・
方向待定」（`wait_for_direction`）——**是波動警示，不是方向偏空**（符合官方語意：negative gamma 是波動
放大器，不是方向指標）。

**對本卡的影響**：§5 的 collar 建議**不依賴** regime 訊號（建立在 FP 機構足跡 + 我方 82.9% 曝險 + rr4=0%
三項獨立事實上）→ **結論不變**。但 [[event_tracking/13-07-2026_TSM_tracking]] §4 的「疊加宏觀 🔴NDX 負gamma
risk-off」**已撤回**（該行已標 ❌作廢）——它 100% 來自那個恆真的假閘，不得作為偏空/避險論據。
NDX 負 gamma 只說明「**上下都會被放大**」，方向中性。

→ 結案卡：[[../romasys/document/todo_idea/14-07-2026_regime-DR閘誤用v4口徑]]（PIT 回放全文＋修法）
→ 公約：`ROMA_SIGNAL_DESIGN #G3_dr_caliber_convention`（**吃 DR 前必讀：先確認是哪個模型的 DR**）

---

## 八、關聯
- 追蹤卡：[[event_tracking/13-07-2026_TSM_tracking]]｜[[event_tracking/11-07-2026_TSM_tracking]]（曝險全景表）
- 前策略卡：[[10-07-2026_TSM_strategy]]（§2b 已證偽）｜[[09-07-2026_TSM_strategy]]
- 方法論：[[kb_fp-greek-sign-convention]]（買方側符號）｜[[kb_fp-spread-label-vs-greek-sign]]（標籤不可信，逐腳覆核）
- 口徑：[[kb_delta-ratio-three-models]]（三個模型的 DR，不可互比）｜[[kb_datatable-vs-synth-gamma-delta-ratio-caliber]]（母題：SG 多模型同名欄不可混用）
- 待修：[[../romasys/document/todo_idea/14-07-2026_regime-DR閘誤用v4口徑]]（§7-b 的 bug 立項）
- 慣例：[[feedback_tsm_high_conviction_hold]]｜[[feedback_holdings_ssot_brokerage_log]]｜[[feedback_wall_levels_ssot_sg_data_table]]｜[[feedback_derisk_to_cash_not_defensive_equity]]｜[[feedback_no_flip_without_entry_context]]｜[[project_rr4_index_put_only]]
