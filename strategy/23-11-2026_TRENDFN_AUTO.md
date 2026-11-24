# TRENDFN 23-11-2026（自動，FN 落地後）

## S_1｜AUTO FN_TREND 21:13｜SG 從「反彈上看 7,700」轉成「這週反彈、但大概撐不過這週」：EOM 目標下修到 7,400–7,500，開始布 12 月到 1 月的下檔部位。我方此時零保護，半導體 Δ 曝險約 100% NAV

**TL;DR**
- [回補] 原輪 11-23 21:13 陣亡，2026-11-24 補跑。資料 as-of 為 2026-11-23 21:13 台北（= 08:13 ET，**美股 11/23 現貨還沒開盤**）。
- **SG 的立場變了**（11-23 AM）。SPX 期貨 +2.75%，SG 把月底目標從「≥7,600」下修到 **7,400–7,500**，並明講這波反彈是 flows-based、"very unstable"、"unlikely to last past this week"。它會逢漲獲利了結並 roll up；第一支撐在 6,900s。第二支撐「不是價格，是時間」，要等到 **DEC OPEX** 才有事件能出清風險。
- **新增的偏空布局**：SG 第一次明講 "We want to own downside exposure into the end of December and/or January"。因為裸 put 太貴，它改用短天期深價外 put fly、ratio calendar 這類結構。
- **週報（22-11）**：
  - COR1M 在 4 天內從 13 升到 46，代表 dispersion 交易被平倉，SG 稱為 "equity-wide event"。
  - VVIX 從 102 升到 146。依 SG 統計，VVIX 收盤 >125 時，SPX 之後 1 日與 5 日報酬的中位數偏正。
  - 週報的判讀閘門：週一收回 SPX 7,000、IV 回落 ⇒ 部位轉為支撐；收不回 7,000 或 VIX 停在 40 附近 ⇒ 壓力延續。11-23 盤前指示開盤約 7,100，但**現貨收盤在 as-of 時點還沒發生**，這個閘門還不能判。
- **對我方**：as-of 快照是 rr4u 0%、rr5 20.16%、rr6 205.48%、semi +100.04% NAV。SG 的劇本給了一個明確的時間窗：**這週反彈期間減倉、補 12 月到 1 月的保護**；反彈結束後，SG 認為下檔沒有部位面的穩定器（每跌 1% 有 $3–4bn 負 gamma）。
- 預測帳本：補跑不寫。

**縮寫對照**
- FN = Founder's Note（SG 平日 AM/PM 短評）
- SG = SpotGamma
- EOM = End of Month（月底，本月是 11/30）
- OPEX / DEC OPEX = 月選擇權到期日（11/20）／12 月季度到期（12/18）
- GEX = Gamma Exposure（造市商 gamma 曝險）
- PW = Put Wall（put 牆）
- COR1M = Cboe 1-Month Implied Correlation Index（一個月隱含相關性指數）
- VVIX = VIX 的波動率指數
- IV / RV = Implied / Realized Volatility（隱含／實現波動率）
- ATH = All-Time High（歷史高點）
- rr3 / rr4u / rr5 / rr6 / rr9b = brokerage log 的風險欄位：總槓桿／保護總量／現金比／β 加權曝險／板塊方向曝險
- MNQ = Micro E-mini Nasdaq-100 期貨
- BePS = Bear Put Spread（買高履約 put、賣低履約 put）
- BOXX = Alpha Architect 1-3 Month Box ETF（我方的現金停泊載體）

### S_1_1 跨日趨勢（11/13 至 11/23 AM）

來源都在 `log_gen_by_roma/founders_digest/`；11/13 到 11/20 PM 的列沿用前卡 `ls_strategy/21-11-2026_TRENDFN_AUTO.md` S_1_1。水位是 FN 敘事版，不是 data_table SSOT。

| 場次 | SPX | VIX | Pivot | 壓力 | 支撐 | SG 的 base case |
|---|---|---|---|---|---|---|
| 11/13（15-11 週報） | 7,563 | n/a | 7,590 | 7,700 | 7,400 | 事件出清後漲向 Thanksgiving |
| 11/18 PM | 7,324 | n/a | 7,590 | 7,400–7,450 | 7,300 / 7,000 | 反彈到 >7,600，7,700 是大壓力 |
| 11/20 AM | 期貨指示約 7,100 開盤 | >30 | 7,300（下修） | 7,300 / 7,500 | 7,100 / 7,000 | OPEX 是階段低點，用固定風險 call 押反彈 |
| 11/20 PM | **6,910（−4%）** | 36（盤中 40） | 7,300 | 同上 | 同上 | RV 上升可能引發 vol-control 賣壓 |
| **11/23 AM** | 期貨 **+2.75%**，指示約 7,100 開盤 | **30**（−9） | 7,300（banner 沒改） | 7,300 / 7,500 | 7,100 / 7,000；正文寫第一支撐 **6,900s** | **反彈到 7,400–7,500 就到頂，撐不過這週；12 月到 1 月要持有下檔部位** |

**11-23 AM 的新內容**（`23-11-2026_founders_AM.md`）：
1. **目標下修**。原本寫「≥7,600 by EOM」，改成 "closer to 7,400-7,500"，理由是 7,500 以下的負 gamma 減少了，反彈速度會變慢。以 11/20 收盤 6,910 計，7,400 是 +7.1%，7,500 是 +8.5%（我方換算）。
2. **GEX 曲線在每個 strike 都是負值**，而且 11/23 這條比 OPEX 前那條更負。負 gamma 的谷底在 7,100 的 PW。6,900 以下的負 gamma 雖然收斂，但跌穿 6000s 時仍是 "$3-4bn of negative gamma per 1% down"。SG 原話是："We just don't have this downside stabilizer"。
3. **風險來源分散**。SG 列了 NVDA、AI & credit、outages、wars、rates 五項，各自獨立運作，所以 "very hard to clear risk from the system"。
4. **波動數據**：
   - Dec SPX skew 單日 −3 vol pt。
   - 1M SPX put-call skew 已高過 3 月伊朗戰爭爆發時，只低於 2025 年 4 月關稅那次。
   - 上週的個股 put 週成交量是 "biggest ... ever"。
   - VIX 單週 +16 點，是史上第 5 大。
5. **SG 的操作**：持有上週的 call fly，可能再加幾組；逢漲獲利並 roll up；"Longer dated options are still expensive"，所以用 fly 不用 outright。下檔用短天期深價外 put fly 或 ratio calendar。

**SG 立場的軌跡（照實寫）**：
- 11/13–11/18：看漲到 7,600–7,700。
- 11/20：預期出現階段低點，押反彈。
- 11/23：只押一週的反彈，並轉向布局 12 月到 1 月的下檔。

SG 第一次把「反彈之後」的劇本寫成偏空，而不是延續上漲。前卡記過，SG 這兩週的 base case 已經錯過一次（11/13 起看 7,700，實際跌 8.6% 到 6,910）。這次它把多頭時間窗縮短到一週，可以讀成它在修正先前過度樂觀的時間假設。

**數字口徑不一致（並列，不裁決）**：
- 11/20 到期部位中 put 的佔比：11-20 AM 寫 "~75% of that delta"；22-11 週報寫 "puts made up 80%+"。
- VVIX：11-20 PM 寫「盤中 120→146、收 138」；22-11 週報寫「上週 102→146」。兩者是不同區間（日內 vs 整週），不衝突。

### S_1_2 前瞻層（22-11 週報＋11-23 AM）

**22-11 週報（"Violent Capitulation & Volatility: What's Next?"）重點**：
- 11/20 收盤時，SPX 距 10/6 ATH 約 −12%，NDX 約 −20%；VIX 一週從 22 升到 40。
- **COR1M 4 天從 13 升到 46**，是 3 月伊朗戰爭以來最大跳升。10 月時 COR1M 低於 8，代表 dispersion 交易很擁擠；這次是一次性平倉，所以全市場一起跌，只有債券和美元沒跌。
- OPEX 之後，SPX 的 dealer gamma **仍是負值**，只是 7,000 附近較不負。週報結論是 "less fragile ... although by no means fully repaired"。
- 週報點出週一要看的兩件事：
  - 短天期 vol seller 進場會提供正 gamma；
  - 長假週末的 theta 會讓人不太想持有 long option。

**兩份文件合起來看，未來兩週的路徑**：

| 時段 | SG 的劇本 | 依據 |
|---|---|---|
| 11/23–11/27（假期週） | flows 帶動的反彈，上限 7,400–7,500 | post-OPEX IV 回落，加上 vanna 效應（11/19 AM：IV 崩落 ⇒ 造市商到 11/30 都得買期貨） |
| 11/30 之後到 DEC OPEX（12/18） | 沒有出清事件，低點要用時間而不是價格來看 | 每跌 1% 有 $3–4bn 負 gamma；五個風險來源各自獨立 |
| 12 月到 1 月 | SG 自己要持有下檔部位 | 11-23 AM 原文 |

**可證偽的閘門**（as-of 時點都還沒觸發，因為現貨未開盤）：

| 條件 | 讀法 |
|---|---|
| 11/23 SPX 收盤 ≥7,000，VIX 從 30 往下走 | 週報的「部位轉為支撐」成立，反彈劇本啟動 |
| SPX 在 11/27 前到 7,400–7,500 後回落 | SG 的「反彈不穩定」劇本兌現，是減倉窗口 |
| SPX 收盤站上 7,500 並守住到 11/30 | SG 的反彈上限被證偽，偏多 |
| 11/23 收不回 7,000，或 VIX 回到 40 附近 | 週報的壓力情境，跌向 6,900s 第一支撐 |

**和前卡閘門的接續**：前卡 S_1_2 的「收回 7,000 且 VIX 從 36 下行」，在 11-23 盤前已部分符合（VIX 30、期貨指示約 7,100），但還需要現貨收盤確認。依我方慣例，04:00 台北之前看到的都是盤中價，不能當收盤。

### S_1_3 與我方持倉的含意

**as-of 持倉快照**：`brokerage_log/20-11-2026-brokerage-02.xlsx.log`，parsed_at 2026-11-20 22:26 台北，這是 as-of 之前的最新一份。

| 項目 | 數值 |
|---|---|
| NAV | $398,441 |
| rr3 / rr3n | 1.64x / 1.64x |
| rr4u 保護總量 | **0.00%** |
| rr5 現金 | 20.16%（目標 40%，容許帶 35–45%） |
| rr6 β 加權多頭 | 205.48%（SPX 每動 1% ≈ $8,187） |
| rr9b semi / index 方向曝險 | +$398,581（+100.04%）/ +$222,296（+55.79%） |
| 正股 | TSM 430 股 $144,820、QQQ 116 股 $73,971、AMZN 100 股 $25,381、AVGO 20 股 $6,830 |
| Option | 全部是 long call 且都在價外。最近的到期日是 2027-02-19（91 DTE），最遠是 QQQ Jun17'27 700/710C |

**含意**
1. **SG 劇本裡的減倉窗口就在這週**。SG 認為反彈到 7,400–7,500 就到頂，之後到 DEC OPEX 都沒有部位面的支撐。這和前卡 S_1_3 的方案 C（「反彈到 7,000–7,300 再減正股進 BOXX」）同方向，而且 SG 現在把窗口的上限和期限都講清楚了：**7,400–7,500，11/27 前**。rr5 要從 20.16% 拉回 ≥35%，大約要減 $59k 正股或 ETF 進 BOXX（(35%−20.16%) × $398,441，我方換算）。
2. **保護的時點從「不適合」變成「有結構可用」**。11-20 AM 說 put 太貴；11-23 AM 指出的路線是：**不買裸 put，改用短天期深價外 put fly、ratio calendar，鎖定 12 月到 1 月**。依我方的避險載體原則，QQQ put 蓋不住半導體尾部，所以載體要對準 semi 那 +100.04% NAV：
   - A：SMH 或 SOXX 的 Jan'27 BePS 或 put fly。賣出的那條腿收回高 skew，到期日對準 SG 說的 12 月到 1 月時間窗。
   - B：TSM 是高信心部位，處理方式是**買保護不減倉**（佔比大正是拉高保護預算的理由）。可以在反彈時做 TSM Jan'27 BePS。
   - C：只減倉進 BOXX，不做結構性保護，代價是 6,900s 以下沒有任何保護。
   - 成本沒有列，因為本輪是補跑，沒有 as-of 時點的鏈上報價；實際下單前要在盤中重新取價。
3. **長天期 call 的處理**。SG 寫 "Longer dated options are still expensive" 並會逢漲 roll up。我方 11 組 long call 都在價外（11-20 快照的 OTM 幅度在 −2.4% 到 −25.7%），如果反彈到 7,400–7,500，可以在這段 IV 偏高時檢討是否把一部分 roll 成 call spread，賣掉貴的上檔 vol。這只是選項，不是必做，依我方慣例要先查各部位的進場邏輯再談。
4. **NVDA 與 AI 板塊**。SG 把 "NVDA, AI & credit" 列為獨立的風險源。我方沒有 NVDA，但 TSM、AVGO、MU、SMH、SOXX 和它在同一個籃子裡。依前卡框架，目前仍是股價層的連動，還不是 hyperscaler 砍 capex 的基本面利空。

**事後資訊（補跑時點，不作 as-of 判讀）**：
- `brokerage_log/23-11-2026-brokerage.xlsx.log` 的 parsed_at 是 2026-11-23 23:16 台北，晚於 as-of。內容如下：
  - 新出現 **MNQ Dec'26 ×10 long**，notional $536,884（rr2 123.91%），快照時 UPL +$9,289；
  - rr3 升到 3.05x、rr6 升到 376.17%，rr4u 仍是 0%，rr5 20.73%，NAV $433,285；
  - QQQ last 652.48（11-20 快照是 637.68），TSM last 368.86（11-20 快照是 336.79）。
- 依我方慣例，MNQ 口數變動預設是計畫內的決策，盤前 QQQ 跳空時常是「call 買不到的替代」，這裡不追問。兩件事照列：
  - SG 11/20 的 banner 明講反彈 "only ... via fixed-risk call structures, not with hard deltas"，MNQ 正好是硬 delta；
  - 要補回下檔那條底，**買 put 比換成 call 便宜**（long future + long put ≡ long call）。可以在這週反彈時買 QQQ 或 NDX 的 Dec'26 put，到期日對齊 12/18 的 MNQ 轉倉日和 DEC OPEX；也可以直接在 12/18 轉倉時把 MNQ 換回 QQQ call。
- 我方的 MNQ long 規則寫明「notional ≤ NAV × 5%」，目前 123.91% 明顯超出。但這條規則有例外：hedge、換倉、事件 trade 不適用。這筆屬於哪一類要看當時的進場紀錄，本輪不判定。
