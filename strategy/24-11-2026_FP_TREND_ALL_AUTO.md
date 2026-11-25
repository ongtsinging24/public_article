# FP_TREND ALL 24-11-2026（自動，FP 落地後）

## S_1｜AUTO FP_TREND ALL 21:11｜s11-23 反彈日，指數和半導體的多頭在了結；NVDA 把遠價外 put 換成 120/130 履約價；TSM 連 3 場都標平倉，要等 OI 驗證；我方保護總量仍是 0%

**TL;DR**
- **資料範圍與 as-of**
  - 本輪新檔是 `flowpatrol_2026_11_24.log`：publish 2026-11-24，session_date 2026-11-23，parsed_at 2026-11-24T21:02。
  - 往前併了 8 檔，session 分別是 s11-12、13、16、17、18、19、20、23。逐檔讀過 `# session_date`，日期都不重複，不需要去重。
  - 持倉來源是 `brokerage_log/24-11-2026-brokerage.xlsx.log`（parsed_at 2026-11-24T07:51）。
- **s11-23 是單日大漲**（來源：FP 11-24 檔的 `px=`／`1dR=`）：
  - SPY 722.00，+4.56%；TSM 363.34，+13.70%；AMZN 255.42，+3.35%。
  - NVDA 165.19，1dR +31.32%。這是 FP 列尾值，沒有拿其他來源核對，引用前要先驗。
- **買方側 delta 從極高翻到極低**（p9／p13）：
  - Technology 板塊 d$ 是 -2,473M（第 0 百分位）。s11-12 時是 +1,111M（第 97 百分位）。
  - Equity ETF 板塊是 -2,254M（第 10 百分位）。前一場 s11-20 是 -801.9M（第 29 百分位）。
  - 按 memory 卡，買／賣軸的前瞻力是零，所以**這只描述「了結」，不預測方向**。
- **NVDA（未持有，但驅動半導體）：保護往上換履約價**
  - 賣出 80P Jan'27／Apr'27，四欄 stc 分別是 149,892 和 149,189。
  - 同一包裡買進 120P Jan'27、130P Jan'27、120P Feb'27，bto 分別是 98,087、72,435、100,265。另外買了 140P Jun'27，bto 20,298。四腳都判 BUY(greek)。
  - 形狀是把「價外約 52% 的 put」換成「價外 21% 到 27% 的 put」，**屬於加強避險的動作**。開倉還是平倉要等 T+1 的 OI 才能定（下表標 [ ]）。
  - 同一場 NVDA 的 Dec／Jan'27 160C、170C 被 stc 變現。
- **TSM（P1 持倉）已連續 3 場都標成平倉**
  - s11-17：深價內 put 被 btc。
  - s11-20：Jan'27 400P／410P／420P 被 btc，合計約 3 萬口。
  - s11-23：Jan'27 420C 判 BUY(greek)，四欄 btc 51,247；同一包的 360C 判 SELL(greek)，四欄 stc 28,380；兩腳同一個 spread=12184。
  - 照標籤讀，是 360/420 的 BuCS 在出場；但 09-01 起源端口徑有斷層，這包也可能是 360C 換到 420C。strike_ladder 最新的 OI 只到 2026-11-20，**判不了**。
- **指數層的 OI 大減要打折**
  - p17 寫 SPY tot_oi_chg -2,754,837，QQQ -1,101,524。
  - 但 2026-11-20 是 11 月的月結算日（第三個週五），**到期合約自然消失會混在裡面**，所以不能當「機構撤掉避險」的證據。
  - p1 的 SPY 有三組 put 價差，每組約 6.6 萬到 9 萬口，標籤是高履約價那腳 stc、低履約價那腳 btc。照字面是 BePS 在結清。這三組 dir 都是 `?(none·勿判)`，買賣軸不判。
- **我方影響**
  - rr4u 是 0.00%，rr6（β 加權）是 224.67%，現金 20.58%，NAV 429,217.66。來源：24-11 brokerage log。
  - 半導體 call 集中，但沒有任何保護。NVDA 的 put 換履約價，是今天唯一稱得上「機構在加強避險」的訊號。
  - 本輪沒有拿到選擇權報價，**不列保護菜單的成本**，下一輪 NOFP 或 SAVEST 再補。

**縮寫對照**
- FP = SpotGamma FlowPatrol（每日期權流向報告；檔名是 publish 日，資料 as-of 看 session_date）
- s11-23 = session_date 2026-11-23（資料 as-of 收盤日），其他 sNN-NN 依此類推
- p1/p3/p4/p5/p6/p7/p8/p9/p13/p17 = FP 分頁：Index/Single/Asset 表、Top Delta、Top Gamma、Top Vega、Largest Premium、Top Index、Unusual、Statistically Significant、Sector Stat、Heavy DayTrading
- d$/g$/v$ = 買方側的 delta／gamma／vega 曝險金額；prem = 權利金
- bto/btc/sto/stc = buy-to-open／buy-to-close／sell-to-open／sell-to-close（開平倉四欄；09-01 起源端口徑斷層）
- dir=(greek)/(prem)/(sym·單列) = 買賣軸判決的證據等級：greek > prem > sym·單列
- pkg 旗標 = 包裹單腿（oi= 是整包值，不是這一腳的真實 OI）
- OI = Open Interest（未平倉量）；tot_oi_chg = p17 的 symbol 層 OI 變化
- 1dR/5dR = FP 列尾的 1 日／5 日報酬
- BuCS/BePS/BuPS = Bull Call Spread／Bear Put Spread／Bull Put Spread
- rr4u/rr6 = brokerage log 的保護總量比率／β 加權曝險比率；NAV = Net Asset Value（淨資產）
- LEAP = 長天期期權（到期在 1 年以上）
- opex = 月選擇權結算日（2026-11-20）

---

### S_1_1｜持倉標的在 FP 的出現狀況（s11-12 到 s11-23）

部位來源是 24-11 brokerage log；價外距離也直接引用 brokerage log 的值。

| SYM | 我方部位 | s11-23 FP 有沒有列 | 近 8 場 FP 重點 |
|---|---|---|---|
| TSM | 430 股，加上 Feb/Apr'27 的 400/410/430C 共 14 口（價外 8.0% 到 14.4%） | 有，p3/p4/p5/p6/p8 | 連 3 場標平倉（見 S_1_2） |
| QQQ | 116 股，加上 Jun'27 700C 4 口、710C 2 口 | 有，p1 和 p17 | 450P/550P Jan'27 結清，約 5 萬口；tot_oi_chg -1,101,524（受 opex 影響） |
| MU | Mar'27 900C 1 口（價外 22.1%） | 只在 p17 | call 價差的履約價一路往下挪（見 S_1_4） |
| SMH / SOXX | SMH May'27 525C 2 口、SOXX Feb'27 165C 9 口 | SMH 只在 p17 | 板塊 put 跟著價格往下換；s11-23 沒有新列 |
| AMZN | 100 股 | 有，p5 和 p9 | v$ -1.3M，第 0 百分位；275C/350C Dec'27 是同一包 |
| AVGO | 20 股，加上 Feb'27 350C 2 口 | 沒有 | 最後一次出現是 s11-12：320C Feb'27 BUY(greek)，d$ +174.66M |
| GOOG | Mar'27 310C 1 口 | 沒有（出現的是 GOOGL） | s11-19：GOOGL 400P Dec'28 SELL(greek)，prem -62.11M |

### S_1_2｜TSM：連 3 場都標平倉，開平倉軸還沒驗

| session | 列（同一包） | 判決 | 四欄 | 量級 | px（FP） |
|---|---|---|---|---|---|
| s11-17 | 430P Dec04 ／ 400P Dec18 | 兩腳 BUY(greek) | btc 5,939 ／ btc 6,924 | prem 42.33M ／ 34.24M | 359.69 |
| s11-20 | 420P ／ 410P ／ 400P，皆 Jan'27 | 三腳 BUY(greek) | btc 9,913 ／ 9,995 ／ 9,961 | prem 103.56M ／ 95.69M ／ 86.88M | 319.55 |
| s11-23 | 420C Jan'27 | BUY(greek) | btc 51,247 | d$ +677.23M，g$ +24.56M，v$ +2.66M，prem 113.40M | 363.34 |
| s11-23 | 360C Jan'27 | SELL(greek) | stc 28,380 | d$ -594.21M，v$ -1.54M，prem -123.35M | 363.34 |

- **s11-23 這一包的讀法**
  - 兩腳的 spread 都是 12184.0，屬於同一包；口數比約 1.8:1，不是標準的垂直價差。
  - 買方側淨 d$ 約 +83.02M（677.23 − 594.21，手算），整包仍偏多。
- **兩種解讀，目前無法區分**
  - 照標籤字面：360/420 BuCS 在出場（360C 多單 stc、420C 空單 btc）。
  - 標籤不可信時：360C 換到 420C 的上移，多頭部位仍保留。
  - 判準是 Jan'27 420C 和 360C 的 OI 變化。strike_ladder 的 TSM 最新 meta 是 `oi_asof` 2026-11-20、`fetched_at_et` 2026-11-23 19:01，比 s11-23 晚一場以上才有資料。下面標 [ ]。
- **跨日型態**：s11-17、s11-20 兩場都是賣 put 的一方在下跌中回補深價內 put。到 s11-23 價格大漲時，換成 call 包裹動作。三場都**不是新建的空方避險**。

### S_1_3｜指數層：反彈日了結 call／put 價差，OI 讀數受 opex 污染

- **p9 的 SPY d$ 序列**（單位 M，括號內是百分位）：
  - s11-13 -757.3（第 19）→ s11-16 +348.2（第 70）→ s11-17 +1,413（第 97）
  - s11-19 +2,084（第 99）→ s11-20 +59.8（第 51）→ s11-23 -1,493（第 4）
  - s11-23 的 g$ 是 -560.7M（第 7 百分位）。
- **p13 的板塊 d$ 序列**（單位 M，括號內是百分位；「未列」表示該場沒進前 10）：

| 板塊 | s11-12 | s11-13 | s11-16 | s11-17 | s11-18 | s11-19 | s11-20 | s11-23 |
|---|---|---|---|---|---|---|---|---|
| Equity ETF | +1,234 (74) | -694.5 (33) | +1,277 (73) | +2,168 (86) | +1,174 (70) | +1,966 (82) | -801.9 (29) | -2,254 (10) |
| Technology | +1,111 (97) | -105.6 (44) | +33.9 (53) | 未列 | +372.4 (73) | +64.7 (54) | -35.7 (48) | -2,473 (0) |

- **p1 的 SPY（s11-23）**：三組成對的 put 價差，dir 都是 `?(none·勿判)`。
  - Nov27：680P stc 66,300 ／ 660P btc 66,834
  - Nov30：675P stc 74,395 ／ 570P btc 74,997
  - Dec04：675P stc 89,737 ／ 650P btc 88,736
  - 照字面是 BePS 在結清。另外 550P Jan'27 有 sto 61,912。
- **p1 的 QQQ**：Jan'27 450P stc 50,134 ／ 550P btc 50,190，1:1 包裹，dir 不判。
- **p7 的 SPX 主要列**（買賣軸用 prem，證據等級低於 greek）：
  - 8500C／8700C Feb'27：BUY 42.69M ／ SELL -30.44M，兩腳都是 pkg，屬於 BuCS 形狀。
  - 8200C Jun'27：BUY 65.63M。
  - 6850P Jan'27：SELL -79.27M，四欄 stc 6,466，形狀是長天期 put 變現。
- **p17 的 symbol 層 OI**：SPY -2,754,837、SPX -1,760,046、QQQ -1,101,524、IWM -725,063。
  - **2026-11-20 是月結算日**，這幾個數字包含 11 月到期合約自然消失，**不能當「有平無開」的證據**。
  - 前卡 s11-20 時 SPY 是 +230,671，兩場不能直接比。
- **VIX**：26C Dec16 stc 58,688，判 SELL(sym·單列)。p9 的 VIX d$：s11-20 -223.8M（第 5 百分位），s11-23 -125.2M（第 20 百分位）。連 2 場在減少 VIX call 多單。

### S_1_4｜半導體：MU、SMH、SOXX（持有 call）

- **MU：同一本約 8.7k 口的 call 價差，履約價一路往下挪**（四欄數字來自 p8）
  - s11-12：Dec'27 700C BUY(prem) 39.92M ／ 800C SELL(prem) -35.53M，px 798.90。
  - s11-16：Feb'27 920C 判 BUY(greek)，bto 8,775；1000C 判 SELL(greek)，stc 8,664。px 719.02。
  - s11-18：Feb'27 850C 判 BUY(greek)，bto 8,740；920C 判 SELL(greek)，stc 8,710。px 705.00。
  - s11-19：Dec'27 700C 判 SELL(prem)，-29.65M，形狀是 s11-12 那腳的出場。px 690.12。
  - s11-20：Feb'27 780C 判 BUY(greek)，d$ +200.20M，prem 53.34M，沒有看到配對的短腳。px 594.39。
  - s11-23：p3 到 p8 都沒有 MU。散文裡 MU 的 -1,026.4M 不在 p9 前 10，屬衍生層，不採用。p17 的 tot_oi_chg -368,233 受 opex 影響。
  - 按 memory 卡，大額 BuCS 的前瞻力是零：**多方還在，但這不是加碼理由**。我方 900C 價外 22.1%。
- **SOXX／SMH：put 跟著價格往下換**
  - s11-13：SOXX 150P Dec BUY(prem) 21.01M；145P Mar'27 BUY(prem) 25.34M。
  - s11-17：SOXX Jan'27 150C ／ 180C，bto 9,236 ／ sto 9,200，屬於 BuCS 形狀。
  - s11-19：SMH Feb'27 430P bto 5,003 ／ 330P sto 5,000，屬於 BePS 形狀。
  - s11-20：SOXX Dec 125P bto 24,191 ／ 150P sto 10,313；SMH Dec 480P 判 SELL(greek)，prem -43.98M，屬於深價內 put 變現。
  - s11-23：沒有新列。p17 的 SMH tot_oi_chg -343,563 受 opex 影響。
  - 結論同前卡：**上 put 榜代表已經反映在價格裡，不追買板塊 put**。

### S_1_5｜NVDA（未持有，作為半導體避險風向）

- **p9**：d$ -2,474M（第 0 百分位）、g$ -22.10M（第 34 百分位）、v$ -2.10M（第 2 百分位）。s11-12 是 +1,074M（第 97 百分位）。
- **put 換履約價**（按 spread id 配對；四欄來自 p2／p8）：

| spread id | 買進腳（皆 BUY(greek)） | 賣出腳（皆 SELL(greek)） |
|---|---|---|
| 6698 | 120P Jan'27，bto 98,087，prem 62.68M | 80P Jan'27，stc 149,892，prem -8.60M |
| 6756 | 120P Feb'27，bto 100,265，prem 110.93M | 80P Apr'27，stc 149,189，prem -69.27M |
| 6704 | 130P Jan'27，bto 72,435，prem 68.07M | 160C Jan'27，stc 55,553，prem -158.77M |
| 6522 | 140P Jun'27，bto 20,298，prem 67.42M | 100P Jun'27，stc 19,765，prem -28.42M |

- **手算合計**：買進 put 約 29.1 萬口，prem 309.10M；賣出 put 約 31.9 萬口，prem -106.29M。
- **價外距離**（以 px 165.19 手算）：80P 約 51.6%、120P 約 27.4%、130P 約 21.3%、140P 約 15.2%。
- **讀法**
  - 把遠到沒有作用的保護換到 -21% 到 -27% 的區間；6704 那包同時把 call 多單換成 put，形狀是 collar 或 risk-reversal 偏空。
  - 同一場 Dec／Jan'27 的 160C、170C 都在 stc，屬於大漲日的多單了結。
  - Jan'29 的 150C 判 BUY(greek)，四欄 btc 10,028；170C 判 SELL(greek)，四欄 sto 10,162，屬於 BuCS 形狀，LEAP 多方仍在。
- **證據等級**
  - 買賣軸是 greek 級，可信。
  - 開平倉軸只有 V/OI 可看：120P Feb'27 是 100,265 ÷ OI 162,340 ≈ 0.62，**下不了「新開倉」的結論**。
- **我方意涵**：我方曝險在 TSM、MU、AVGO、SMH、SOXX 的 call，rr4u 是 0.00%。這是 8 場內**唯一一筆有規模、往價平方向移的避險動作**，記為觀察項。保護是否補、補多少，由 user 依既有配置決定；本卡不給報價。

### S_1_6｜AMZN 與其他

- **AMZN（s11-23）**
  - p9：d$ -143.1M（第 15 百分位）、v$ -1.3M（第 0 百分位）。
  - p5：Dec'27 350C 判 SELL(greek)，v$ -1.16M；275C 判 BUY(greek)，v$ +519,485。兩腳 spread 都是 704，逐腳看是 BuCS 形狀。
  - 這兩腳沒有 p8 列，口數比不可知。所以 SG 散文的「extreme short vol」只成立在 vega 淨額，**方向上是多頭價差**。
  - 先前出現過：s11-16 的 295C／350C Feb'27 包裹（btc 15,515 ／ stc 15,469），s11-17 的 400C Jun'28 判 BUY(greek)。
- **債與信用**
  - TLT Jan'27：79P bto 62,675，判 BUY(greek)；78P stc 49,728，判 SELL(greek)。屬於 put 小幅上移。
  - HYG 76.5P Nov27：判 BUY(greek)，g$ +16.77M。
  - Bond ETF 板塊 d$ -165.7M（第 14 百分位）。按 memory 卡，殖利率沒有前瞻力，**不據此加利率保護**。
- **金融**
  - p13 的 Financial Services：g$ 第 100 百分位、v$ 第 100 百分位、d$ 第 1 百分位。
  - p4 有 JPM 290P Jan'27 判 BUY(greek)，g$ +15.20M。屬於買保護，與我方持倉無關。
- **口徑提醒**
  - SNDK 的 5dR -88.75% 是 8:1 拆股造成的斷點，不是崩盤。SNDK 75P Dec 判 SELL(prem)，prem -192.61M，只用 prem 級證據。
  - SPCX 有小樣本旗標（54 bar），百分位不可信。
  - SMCI 的 v$ 是第 100 百分位，但金額只有 0.1M，規模無意義。
  - AMD 870C 的 prem 被標成名目金額嫌疑（⚠名目?），不引用。

### S_1_7｜待驗與下一步

- [ ] TSM Jan'27 420C／360C 的 OI 變化：等 strike_ladder 出 `oi_asof` 2026-11-23 的資料，或直接查 yfinance。用來分辨是 BuCS 出場還是 call 上移。
- [ ] NVDA 120P Jan/Feb'27、130P Jan'27 的 OI 變化：確認換履約價是新開倉。如果 OI 沒增加，第 1 條 TL;DR 降級。
- [ ] 指數層的開平倉判讀要等 s11-24 這場（不受 opex 影響）的 p17，再和 s11-23 比較。
- [ ] NVDA 1dR +31.32% 要拿第二個來源核對，之後才可以引用。
- 本輪讀過的來源：`flowpatrol_2026_11_13.log` 到 `_24.log`，共 8 檔，session s11-12 到 s11-23；`brokerage_log/24-11-2026-brokerage.xlsx.log`；`strike_ladder/TSM/TSM_ladder_2026-11-20.meta.json`。
- 本輪沒用的來源：data_table、FN、yfinance 現查。
