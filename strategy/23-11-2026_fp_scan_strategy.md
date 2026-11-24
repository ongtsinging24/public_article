## 07:05:14 — `roma_cli fp_scan 2026-11-23`

<sub>`v7.43 (0775a8c6) | loaded 2026-11-23T22:59:14 | src ✅`</sub>

### 🎯 fp_scan 機會掃描（2026-11-23 🟡age=2td）

來源：flowpatrol_2026_11_23.pdf  
🟡 FP age=2td（偏舊）：資料截至 2026-11-20 收盤（此檔 publish=2026-11-23）、非 live tape；如需同日水位見 data_table  
模式：寬鬆 (cross≥2  extreme≤5  p8≤2)   候選 19 sym  

#### 📖 圖例（內容固定，只講讀法；與當日判斷無關。5 段）

- `[dir=]` 判方向**只看這一欄** —— 買方側，greek 優先 g$ > v$ > d$ > prem
  - BUY/SELL(greek|prem)＝可信；?(none·勿判)＝無證據
  - BUY/SELL(sym·單列)（v5.71）＝由 p9 symbol 級 greek 下傳  
    成立條件＝該 sym 當日在 p1/p2 僅此一列（p9 聚合由它支配）
  - (sym·單列) 實測閘門內 94.5%（n=73）  
    裁判＝跨表 greek 列、對照組基準 51.4%  
    ⇒ 證據等級低於 (greek)，勿與之並列引用；d$ 軸不採（54.7%，CI 壓基準線）
  - ⚠bto/sto=X＝該列 bto/sto 與判決相反  
    （pkg＝包裹單反號／部分＝分類未涵蓋全量）
  - 🔴 spread✓ 與 bto/sto 皆未校驗，不得用來判方向
  - spread✓組合單＝SG 把這腳編進某組多腳成交  
    （只取存在性，標籤全文不採信；`--raw` 印全文）
  - exp=…(DTE=n)：n 以成交場次日（session_date）為基準  
    ＝這筆單的天期性質
  - ⛔已到期／⚠️短天期 以卡片產出日（report_date）為基準  
    ＝現在還剩幾天
- `[⬜/⚪]` banner／Structure 色塊：⬜＝**無 F7 解碼**（不是判決）
  - ⬜＝p8 未命中 ⇒ 沒有資訊；⚪＝F7 解出真正的多空混雜（有資訊）
  - ⚠️ 實測 74.7% 的 p3–p6 候選沒上 p8  
    ⇒ ⬜ 是常態不是例外，別把它讀成「中性」
  - v4.49：F7 行不再印 `conf=high/med/low`  
    （實證那個等級量不到可靠度也量不到強度）  
    改印基準＋原始集中度 `prem_conc=NN%`
  - `greek` 基準＝符號本身即答案，無集中度可談
- `[pkg #id]` **只取分組鍵**，標籤全文不印
  - 依 SG `spread_id` 把同一筆組合單的各腳併起來
  - 三個口徑限制（整張卡只講一次）：
    - (1) 淨值只在全腿都有該軸時才算，缺一腿即標「不可算」，  
      不以部分腿加總冒充淨部位
    - (2) 只涵蓋有上榜的腳 —— SG 沒把某腳排進任何榜就看不到，  
      故淨值是「已上榜腳的淨」不是「整包的淨」，  
      腿間分類量差距大時尤其可能還有沒看到的腳
    - (3) 分類量＝bto+btc+sto+stc，中位僅涵蓋約 19% 成交量  
      ⇒ 是下限不是部位規模
  - 群組只給結構形狀＋買/賣軸，不給多空判決；逐腿列在下方原樣保留
- `[struct]` **幾何候選不是成交事實**
  - p1/p2 的 `spread_id` 恆空（全庫 2,584 腿、非空 0 腿）  
    ⇒ 這裡沒有 ground truth，同一份報告的三列可能來自三筆不相干的單
  - 不給方向、不給多空（p1 全列 `dir=?`、包裹單的 bto/sto 逐腳反號）
  - 分類量＝bto+btc+sto+stc，中位僅涵蓋約 19% 成交量 ⇒ 是下限不是部位規模
  - 只看得到上榜的腳（p1/p2 每段每 session 只收 10 列）
  - `pkg 圖樣` 的 `TFT` 是必然的  
    （蝶式 body 對 wing 恰 2.0x，過不了規則 2b 的等量閘）
  - `[struct·強/弱]`＝證據等級（對隨機配對的檢定力）  
    不是幾何貼合度 —— 後者仍在 bits 的「幾何偏差」帶標籤
  - `強`＝butterfly（對有檢定力的虛無超額 100x+）
  - `弱`＝vertical/roll（同一虛無下只有 ~2x）  
    不是雜訊，但證據量級差 1–2 個數量級  
    見卡 `01-09-2026_FP結構卡片層vertical佔比過高但超額未證實`
  - ★ 完整口徑與證據見 `sg_signals/flowpatrol/structure.py` 檔頭
- `[econ]` **模型值不是成交價** —— 沒有任何一個數字來自真實報價
  - 用該腿自帶的 IV ＋ 同 session 跨段落借來的現價跑 BS  
    （r=4.05%、不計股利）
  - 借/貸兩側是同一條損益曲線的鏡像（一側的最大賺＝另一側的最大賠）  
    ⇒ 兩邊的 RR 不是兩個獨立觀測，判決只有一個自由度
  - `傾向借方/貸方`＝另一側要扛 ≥20x 自己能賺的
  - `兩側皆可能` 是預設不是失敗
  - ⚠️ 本判準推不翻「這是既有庫存的 overlay」那種讀法  
    （overlay 要連庫存一起算，我方看不到）
  - 組數＝min(翼1,翼2,體/2) 且殘量不歸屬  
    ⇒ 金額是下限的模型值，兩層低估疊在一起
  - ★ 完整口徑與證據見 `sg_signals/flowpatrol/economics.py` 檔頭

---

### 📐 本 session 組合結構（幾何候選 1 組）

- `[struct·強]` SPX 蝶式1:2:1 7360/7400/7450P exp=2026-11-30  （分類量 2,066/4,534/2,080）
  - ↳ 幾何偏差 20.0%（候選帶）｜等距 20.0%·量比 8.6%｜pkg 圖樣 TFT｜來源 top_index｜**無 spread_id**·僅本層看得到
- [econ·兩側皆可能] S=6910｜2,066 組｜long fly（買翼賣體） 付 $2.2M／最大賺 $8.2M（RR 3.7）｜short fly（買體賣翼） 收 $2.2M／最大賠 $8.2M

### 🟢 SPY — (12 合約 / 21 榜次 ＋ 2 sym級)

- `[pkg #12416.0]` 2 腿·P 垂直 exp=2026-11-27  買675P/賣700P（分類量 52,540/48,193）
  - ↳ 淨prem$=-48.64M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #12709.0]` 2 腿·P 垂直 exp=2026-12-18  買710P/賣735P（分類量 11,215/15,895）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #12717.0]` 2 腿·P 垂直 exp=2027-03-19  買590P/賣690P（分類量 26,016/27,630）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #12840.0]` 2 腿·P 垂直 exp=2026-11-27  賣660P/買680P（分類量 66,395/59,480）
  - ↳ 淨prem$=+19.10M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #12861.0]` 2 腿·P 垂直 exp=2026-12-04  賣650P/買675P（分類量 91,467/137,897）
  - ↳ 淨prem$=+62.44M ⇒ 買方側淨**付**權利金(借記)
- `[sig_position]` d= 51th g= 79th v= 96th sector=Equity ETF
- `[unusual]` 700.00P exp=2026-12-04(DTE=14) dir=SELL(prem) tot_prem=+90.85M → 🟢 Short Put → bullish（prem 判向，集中度 64%，已分類 54,988 口）
- `[unusual]` 690.00P exp=2027-03-19(DTE=119) dir=SELL(prem) tot_prem=+83.92M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 27,630 口）  [SG:12717.0]
- `[unusual]` 590.00P exp=2027-03-19(DTE=119) dir=BUY(prem) tot_prem=+8.69M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 100%，已分類 26,016 口）  [SG:12717.0]
- `[unusual]` 735.00P exp=2026-12-18(DTE=28) dir=SELL(prem) tot_prem=+73.10M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 43%，已分類 15,895 口）  [SG:12709.0]
- `[unusual]` 710.00P exp=2026-12-18(DTE=28) dir=BUY(prem) tot_prem=+30.33M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 95%，已分類 11,215 口）  [SG:12709.0]
- `[unusual]` 675.00P exp=2026-12-04(DTE=14) dir=BUY(prem) tot_prem=+72.30M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 137,897 口）  [SG:12861.0]
- `[unusual]` 650.00P exp=2026-12-04(DTE=14) dir=SELL(prem) tot_prem=+8.90M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 100%，已分類 91,467 口）  [SG:12861.0]
- `[unusual]` 700.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=SELL(prem) tot_prem=+65.02M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 85%，已分類 48,193 口）  [SG:12416.0]
- `[unusual]` 675.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(prem) tot_prem=+13.62M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 52,540 口）  [SG:12416.0]
- `[top_index]` 700.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=SELL(prem) prem$=-60.15M spread✓組合單(標籤不採信)
- `[top_index]` 675.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(prem) prem$=+11.51M spread✓組合單(標籤不採信)
- `[top_index]` 680.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(prem) prem$=+22.97M spread✓組合單(標籤不採信)
- `[top_index]` 660.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=SELL(prem) prem$=-3.87M spread✓組合單(標籤不採信)
- `[top_index]` 675.00P exp=2026-12-04(DTE=14) dir=BUY(prem) prem$=+71.33M spread✓組合單(標籤不採信)
- `[top_index]` 650.00P exp=2026-12-04(DTE=14) dir=SELL(prem) prem$=-8.89M spread✓組合單(標籤不採信)
- `[top_index]` 700.00P exp=2026-12-04(DTE=14) dir=SELL(prem) prem$=-74.43M
- `[index_etfs]` 660.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) iv=44.4% bto/sto⚠未校驗·勿判向：STO=98 STC=66,297
- `[index_etfs]` 680.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) iv=39.3% bto/sto⚠未校驗·勿判向：BTC=59,089 STC=391
- `[index_etfs]` 650.00P exp=2026-12-04(DTE=14) dir=?(none·勿判) iv=43.1% bto/sto⚠未校驗·勿判向：BTC=78 STC=91,389
- `[index_etfs]` 675.00P exp=2026-12-04(DTE=14) dir=?(none·勿判) iv=37.8% bto/sto⚠未校驗·勿判向：BTO=1,855 BTC=136,042
- `[index_etfs]` 605.00P exp=2027-03-19(DTE=119) dir=?(none·勿判) iv=31.0% bto/sto⚠未校驗·勿判向：BTC=59,997 STC=4
- `[heavy_daytrade]` vol=17,649,473 |ΔsynthOI|=1,975,734 ΔOI=+230,671 flow_ratio=  8.93 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: 🟢 Short Put → bullish（prem 判向，集中度 64%，已分類 54,988 口）  [prem_conc=64%]
- **Structure**: 🟢 bull_put_spread  (sibling 675P buy (80% main) → 賣高買低 put 信用價差)
- **資料品質**: ✅ bto/sto 欄與 prem=sell 一致
- **F8 sig 跨日**: 🟡 雙極切換 (7/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[37, 7, 19, 70, 97, 99, 51]

### 🔴 VIX — (6 合約 / 13 榜次 ＋ 1 sym級)

- `[pkg #14414.0]` 2 腿·C 垂直 exp=2026-12-01  賣24C/買28C（分類量 45,513/45,541）
  - ↳ 淨prem$=-13.24M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #14481.0]` 2 腿·C 垂直 exp=2027-01-20  賣35C/買45C（分類量 56,524/56,389）
  - ↳ 淨prem$=-9.21M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #14517.0]` 2 腿·C 垂直 exp=2026-12-16  賣20C/買24C（分類量 68,981/48,725）
  - ↳ 淨d$=-179.54M ⇒ 買方側淨 delta **空**｜淨prem$=-73.55M
- `[sig_position]` d=  5th g= 48th v= 79th sector=Volatility ETF
- `[unusual]` 20.00C exp=2026-12-16(DTE=26) dir=SELL(greek) tot_prem=+120.16M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 92%，已分類 68,981 口）  [SG:14517.0]
- `[unusual]` 24.00C exp=2026-12-16(DTE=26) dir=BUY(greek) tot_prem=+71.54M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 16%，已分類 48,725 口）  [SG:14517.0]
- `[unusual]` 35.00C exp=2027-01-20(DTE=61) dir=SELL(prem) tot_prem=+76.02M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（prem 判向，集中度 82%，已分類 56,524 口）  [SG:14481.0]
- `[unusual]` 45.00C exp=2027-01-20(DTE=61) dir=BUY(prem) tot_prem=+60.05M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 56,389 口）  [SG:14481.0]
- `[top_delta]` 20.00C exp=2026-12-16(DTE=26) dir=SELL(greek) d$=-203.37M spread✓組合單(標籤不採信)
- `[top_delta]` 24.00C exp=2026-12-16(DTE=26) dir=BUY(greek) d$=+23.83M spread✓組合單(標籤不採信)
- `[largest_premium]` 24.00C exp=2026-12-01(DTE=11) dir=SELL(prem) prem$=-58.59M spread✓組合單(標籤不採信)
- `[largest_premium]` 28.00C exp=2026-12-01(DTE=11) dir=BUY(prem) prem$=+45.35M spread✓組合單(標籤不採信)
- `[largest_premium]` 20.00C exp=2026-12-16(DTE=26) dir=SELL(greek) prem$=-115.18M spread✓組合單(標籤不採信)
- `[largest_premium]` 24.00C exp=2026-12-16(DTE=26) dir=BUY(greek) prem$=+41.63M spread✓組合單(標籤不採信)
- `[largest_premium]` 35.00C exp=2027-01-20(DTE=61) dir=SELL(prem) prem$=-69.25M spread✓組合單(標籤不採信)
- `[largest_premium]` 45.00C exp=2027-01-20(DTE=61) dir=BUY(prem) prem$=+60.04M spread✓組合單(標籤不採信)
- `[index_etfs]` 20.00C exp=2026-12-16(DTE=26) dir=SELL(greek) iv=112.0% bto/sto⚠未校驗·勿判向：BTC=2,860 STC=66,121
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 92%，已分類 68,981 口）  [SG:14517.0]  [prem_conc=92%]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（STC）**為主 ⇒ 是了結既有多頭 call，**不是**新開空頭／派發；勿當 distribution 讀（已分類量 68,981 口、平倉佔 100%）
- **Structure**: 🔴 bear_call_spread  (sibling 24C buy (60% main) → 賣低買高 call 信用價差)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (3/10 報告，未過半)，雜訊概率高  d_seq=[65, 53, 5]

### ⬜ MU — (1 合約 / 3 榜次 ＋ 1 sym級)　⚑ 單筆極端 v$#4

- `[top_delta]` 780.00C exp=2027-02-19(DTE=91) dir=BUY(greek) d$=+200.20M
- `[top_vega]` 780.00C exp=2027-02-19(DTE=91) dir=BUY(greek) v$=+997.07K
- `[largest_premium]` 780.00C exp=2027-02-19(DTE=91) dir=BUY(greek) prem$=+53.34M
- `[heavy_daytrade]` vol=1,638,019 |ΔsynthOI|=209,235 ΔOI=+133,269 flow_ratio=  7.83 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 NVDA — (5 合約 / 7 榜次 ＋ 1 sym級)　⚑ 單筆極端 v$#1

- `[pkg #7561.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買115P/賣200P（分類量 5,362/6,598）
  - ↳ 淨prem$=-42.81M ⇒ 買方側淨**收**權利金(貸記)
- `[unusual]` 240.00C exp=2029-01-19(DTE=791) dir=SELL(greek) tot_prem=+66.05M → 🔴 Short Call → bearish（greek 判向，集中度 98%，已分類 29,951 口）
- `[top_vega]` 210.00C exp=2028-01-21(DTE=427) dir=BUY(greek) v$=+657.47K
- `[top_vega]` 240.00C exp=2029-01-19(DTE=791) dir=SELL(greek) v$=-2.12M
- `[top_vega]` 200.00C exp=2029-01-19(DTE=791) dir=BUY(greek) v$=+626.45K
- `[largest_premium]` 115.00P exp=2026-12-18(DTE=28) dir=BUY(prem) prem$=+1.92M spread✓組合單(標籤不採信)
- `[largest_premium]` 200.00P exp=2028-01-21(DTE=427) dir=SELL(prem) prem$=-44.73M spread✓組合單(標籤不採信)
- `[largest_premium]` 240.00C exp=2029-01-19(DTE=791) dir=SELL(greek) prem$=-65.32M
- `[heavy_daytrade]` vol=9,092,747 |ΔsynthOI|=1,106,213 ΔOI=+1,053,379 flow_ratio=  8.22 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 98%，已分類 29,951 口）  [prem_conc=98%]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜distribution 型：持有者放棄上行保護 — 下跌持續性強（已分類量 29,951 口、開倉佔 100%）
- **Structure**: 🔴 short_call_flow  (同 expiry 無其他 unusual leg)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[82, 97]

### 🔴 SPX — (26 合約 / 34 榜次 ＋ 1 sym級)　⚑ 單筆極端 prem#1

- `[pkg #11453.0]` 2 腿·C 垂直 exp=2027-04-30  買8200C/賣8250C（分類量 8,183/8,062）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #11454.0]` 2 腿·P 垂直 exp=2026-11-27  賣6400P/買6500P（分類量 58,412/58,387）
  - ↳ 淨prem$=+7.99M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #11455.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣6350P/買7430P（分類量 3,820/2,079）
  - ↳ 淨prem$=+105.72M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #11638.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  ?5600P/賣7100P（分類量 6,965/7,962）
  - ↳ 淨prem$=-186.22M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #11814.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買6350P/賣6000P（分類量 59,347/58,301）
  - ↳ 淨prem$=-11.89M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #11824.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  ?4400P/買7400P（分類量 4,418/4,534）
  - ↳ 淨prem$=+199.60M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #11949.0]` 2 腿·P 垂直 exp=2026-12-18  賣6700P/買7200P（分類量 2,664/2,508）
  - ↳ 淨prem$=+66.19M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #12042.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買6500P/買7000C（分類量 5,891/6,682）
  - ↳ 淨prem$=+82.55M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #12062.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  ?8700C/賣7325P（分類量 1,168/1,947）
  - ↳ 淨prem$=-44.23M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #12088.0]` 2 腿·P 垂直 exp=2026-12-18  賣5000P/買8000P（分類量 1,915/6,928）
  - ↳ 淨prem$=+578.42M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #12104.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7000P/買7100P（分類量 2,654/1,000）
  - ↳ 淨prem$=+44.39M ⇒ 買方側淨**付**權利金(借記)
- `[sig_position]` d= 16th g= 89th v= 99th sector=Equity ETF
- `[unusual]` 8000.00P exp=2026-12-18(DTE=28) dir=BUY(prem) tot_prem=+741.14M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 56%，已分類 6,928 口）  [SG:12088.0]
- `[unusual]` 7100.00P exp=2026-12-18(DTE=28) dir=SELL(prem) tot_prem=+216.29M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 72%，已分類 7,962 口）  [SG:11638.0]
- `[unusual]` 7000.00C exp=2026-12-18(DTE=28) dir=BUY(prem) tot_prem=+92.77M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（prem 判向，集中度 72%，已分類 6,682 口）  [SG:12042.0]
- `[unusual]` 6500.00P exp=2026-11-30(DTE=10) dir=BUY(prem) tot_prem=+2.83M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 89%，已分類 5,891 口）  [SG:12042.0]
- `[unusual]` 8200.00C exp=2027-04-30(DTE=161) dir=BUY(prem) tot_prem=+69.24M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（prem 判向，集中度 97%，已分類 8,183 口）  [SG:11453.0]
- `[unusual]` 8250.00C exp=2027-04-30(DTE=161) dir=SELL(prem) tot_prem=+63.18M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（prem 判向，集中度 100%，已分類 8,062 口）  [SG:11453.0]
- `[top_index]` 4400.00P exp=2026-11-23(DTE=3 ⛔已到期) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[top_index]` 6350.00P exp=2026-11-23(DTE=3 ⛔已到期) dir=SELL(prem·微量) prem$=-88.51 spread✓組合單(標籤不採信)
- `[top_index]` 5600.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[top_index]` 6500.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(prem) prem$=+10.44M spread✓組合單(標籤不採信)
- `[top_index]` 6400.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=SELL(prem) prem$=-2.45M spread✓組合單(標籤不採信)
- `[top_index]` 8700.00C exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[top_index]` 7400.00P exp=2026-11-30(DTE=10) dir=BUY(prem) prem$=+199.60M spread✓組合單(標籤不採信)
- `[top_index]` 6500.00P exp=2026-11-30(DTE=10) dir=BUY(prem) prem$=+2.68M spread✓組合單(標籤不採信)
- `[top_index]` 7430.00P exp=2026-11-30(DTE=10) dir=BUY(prem) prem$=+105.72M spread✓組合單(標籤不採信)
- `[top_index]` 7360.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-92.23M
- `[top_index]` 7380.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-95.70M
- `[top_index]` 7450.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-109.51M
- `[top_index]` 7325.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-44.23M spread✓組合單(標籤不採信)
- `[top_index]` 7000.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-27.67M spread✓組合單(標籤不採信)
- `[top_index]` 6350.00P exp=2026-12-04(DTE=14) dir=BUY(prem) prem$=+16.25M spread✓組合單(標籤不採信)
- `[top_index]` 7100.00P exp=2026-12-18(DTE=28) dir=SELL(prem) prem$=-186.22M spread✓組合單(標籤不採信)
- `[top_index]` 8000.00P exp=2026-12-18(DTE=28) dir=BUY(prem) prem$=+578.42M spread✓組合單(標籤不採信)
- `[top_index]` 5000.00P exp=2026-12-18(DTE=28) dir=SELL(prem·微量) prem$=-0.87 spread✓組合單(標籤不採信)
- `[top_index]` 7000.00C exp=2026-12-18(DTE=28) dir=BUY(prem) prem$=+79.87M spread✓組合單(標籤不採信)
- `[top_index]` 7050.00P exp=2026-12-18(DTE=28) dir=SELL(prem) prem$=-85.15M
- `[top_index]` 7200.00P exp=2026-12-18(DTE=28) dir=BUY(prem) prem$=+84.27M spread✓組合單(標籤不採信)
- `[top_index]` 6700.00P exp=2026-12-18(DTE=28) dir=SELL(prem) prem$=-18.08M spread✓組合單(標籤不採信)
- `[top_index]` 6000.00P exp=2026-12-31(DTE=41) dir=SELL(prem) prem$=-28.14M spread✓組合單(標籤不採信)
- `[top_index]` 7100.00P exp=2028-12-15(DTE=756) dir=BUY(prem) prem$=+72.06M spread✓組合單(標籤不採信)
- `[index_etfs]` 6400.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) iv=50.6% bto/sto⚠未校驗·勿判向：STO=69 STC=58,343
- `[index_etfs]` 6500.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=?(none·勿判) iv=47.9% bto/sto⚠未校驗·勿判向：BTO=69 BTC=58,318
- `[index_etfs]` 6350.00P exp=2026-12-04(DTE=14) dir=?(none·勿判) iv=47.3% bto/sto⚠未校驗·勿判向：BTO=461 BTC=58,886
- `[index_etfs]` 6000.00P exp=2026-12-31(DTE=41) dir=?(none·勿判) iv=42.2% bto/sto⚠未校驗·勿判向：STO=57,600 STC=701
- **F7 unusual**: 🔴 Long Put → bearish（prem 判向，集中度 56%，已分類 6,928 口）  [SG:12088.0]  [prem_conc=56%]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（BTC）**為主 ⇒ 是回補既有空頭 put，**不是**新開空單；勿當 panic 讀（已分類量 6,928 口、平倉佔 100%）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（F7 集中度不足）｜spread_id=12088.0｜賣5000P/買8000P｜exp=2026-12-18｜淨prem=+578.42M)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[67, 16]

### ⬜ TLT — (9 合約 / 14 榜次 ＋ 1 sym級)　⚑ 單筆極端 g$#4

- `[pkg #13199.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣79P/買78P（分類量 97,175/100,890）
  - ↳ 淨g$=-13.70M ⇒ 買方側淨**賣** gamma｜淨v$=+12.11K
- `[pkg #13268.0]` 2 腿·C 垂直 exp=2026-11-27  賣80.5C/買82.5C（分類量 21,035/7,329）
  - ↳ 淨g$=-20.66M ⇒ 買方側淨**賣** gamma
- `[sig_position]` d= 61th g= 42th v= 97th sector=Bond ETF
- `[top_gamma]` 80.50C exp=2026-11-27(DTE=7 ⚠️短天期) dir=SELL(greek) g$=-31.22M spread✓組合單(標籤不採信)
- `[top_gamma]` 82.50C exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(greek) g$=+10.56M spread✓組合單(標籤不採信)
- `[top_gamma]` 82.00C exp=2026-12-18(DTE=28) dir=SELL(greek) g$=-17.54M
- `[top_gamma]` 79.00P exp=2026-12-31(DTE=41) dir=SELL(greek) g$=-53.61M spread✓組合單(標籤不採信)
- `[top_gamma]` 78.00P exp=2027-01-15(DTE=56) dir=BUY(greek) g$=+39.91M spread✓組合單(標籤不採信)
- `[top_gamma]` 83.00C exp=2027-01-15(DTE=56) dir=BUY(greek) g$=+31.91M
- `[top_vega]` 79.00P exp=2026-12-31(DTE=41) dir=SELL(greek) v$=-716.97K spread✓組合單(標籤不採信)
- `[top_vega]` 78.00P exp=2027-01-15(DTE=56) dir=BUY(greek) v$=+729.07K spread✓組合單(標籤不採信)
- `[asset_etfs]` 75.00P exp=2026-12-31(DTE=41) dir=?(none·勿判) iv=14.6% bto/sto⚠未校驗·勿判向：BTC=126,369
- `[asset_etfs]` 79.00P exp=2026-12-31(DTE=41) dir=SELL(greek) iv=13.0% bto/sto⚠未校驗·勿判向：BTC=67 STC=97,108
- `[asset_etfs]` 74.00P exp=2027-01-15(DTE=56) dir=?(none·勿判) iv=14.6% bto/sto⚠未校驗·勿判向：BTO=21 STO=129,925
- `[asset_etfs]` 78.00P exp=2027-01-15(DTE=56) dir=BUY(greek) iv=12.9% bto/sto⚠未校驗·勿判向：BTO=100,299 BTC=591
- `[asset_etfs]` 83.00C exp=2027-01-15(DTE=56) dir=BUY(greek) iv=12.8% bto/sto⚠未校驗·勿判向：BTO=7,109 BTC=40,369
- `[asset_etfs]` 94.00C exp=2027-02-19(DTE=91) dir=?(none·勿判) iv=17.4% bto/sto⚠未校驗·勿判向：BTO=95,096 BTC=400
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=13268.0｜賣80.5C/買82.5C｜exp=2026-11-27｜淨g$=-20.66M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (4/10 報告，未過半)，雜訊概率高  d_seq=[86, 50, 95, 61]

### ⬜ IWM — (14 合約 / 22 榜次)　⚑ 單筆極端 d$#1 g$#1 v$#3

- `[pkg #4955.0]` 2 腿·P 垂直 exp=2026-12-18  賣256P/買266P（分類量 10,117/10,035）
  - ↳ 淨d$=-56.53M ⇒ 買方側淨 delta **空**
- `[pkg #5046.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣265P/買245P（分類量 39,089/37,101）
  - ↳ 淨g$=-28.29M ⇒ 買方側淨**賣** gamma｜淨v$=+122.15K  淨d$=+507.13M
- `[pkg #5093.0]` 2 腿·P 垂直 exp=2026-11-24  賣250P/買255P（分類量 4,998/5,950）
  - ↳ 淨g$=+13.08M ⇒ 買方側淨**買** gamma
- `[pkg #5103.0]` 2 腿·P 垂直 exp=2026-12-18  買240P/賣265P（分類量 9,169/10,898）
  - ↳ 淨d$=+173.04M ⇒ 買方側淨 delta **多**
- `[pkg #5104.0]` 2 腿·P 垂直 exp=2026-12-18  買248P/賣270P（分類量 3,449/9,950）
  - ↳ 淨d$=+161.15M ⇒ 買方側淨 delta **多**
- `[pkg #5111.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買255P/賣260P（分類量 5,884/8,991）
  - ↳ 淨g$=-4.85M ⇒ 買方側淨**賣** gamma
- `[pkg #5112.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買254P/賣251P（分類量 55,932/28,970）
  - ↳ 淨g$=+73.06M ⇒ 買方側淨**買** gamma｜淨v$=+325.52K  淨d$=-300.83M
- `[top_delta]` 265.00P exp=2026-12-04(DTE=14) dir=SELL(greek) d$=+718.53M spread✓組合單(標籤不採信)
- `[top_delta]` 254.00P exp=2026-12-04(DTE=14) dir=BUY(greek) d$=-553.00M spread✓組合單(標籤不採信)
- `[top_delta]` 245.00P exp=2026-12-18(DTE=28) dir=BUY(greek) d$=-211.40M spread✓組合單(標籤不採信)
- `[top_delta]` 251.00P exp=2026-12-18(DTE=28) dir=SELL(greek) d$=+252.17M spread✓組合單(標籤不採信)
- `[top_delta]` 270.00P exp=2026-12-18(DTE=28) dir=SELL(greek) d$=+185.74M spread✓組合單(標籤不採信)
- `[top_delta]` 248.00P exp=2026-12-18(DTE=28) dir=BUY(greek) d$=-24.59M spread✓組合單(標籤不採信)
- `[top_delta]` 265.00P exp=2026-12-18(DTE=28) dir=SELL(greek) d$=+177.41M spread✓組合單(標籤不採信)
- `[top_delta]` 240.00P exp=2026-12-18(DTE=28) dir=BUY(greek) d$=-4.37M spread✓組合單(標籤不採信)
- `[top_delta]` 266.00P exp=2026-12-18(DTE=28) dir=BUY(greek) d$=-170.67M spread✓組合單(標籤不採信)
- `[top_delta]` 256.00P exp=2026-12-18(DTE=28) dir=SELL(greek) d$=+114.14M spread✓組合單(標籤不採信)
- `[top_gamma]` 255.00P exp=2026-11-24(DTE=4 ⚠️短天期) dir=BUY(greek) g$=+20.54M spread✓組合單(標籤不採信)
- `[top_gamma]` 250.00P exp=2026-11-24(DTE=4 ⚠️短天期) dir=SELL(greek) g$=-7.46M spread✓組合單(標籤不採信)
- `[top_gamma]` 255.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(greek) g$=+16.87M spread✓組合單(標籤不採信)
- `[top_gamma]` 260.00P exp=2026-11-30(DTE=10) dir=SELL(greek) g$=-21.72M spread✓組合單(標籤不採信)
- `[top_gamma]` 254.00P exp=2026-12-04(DTE=14) dir=BUY(greek) g$=+112.51M spread✓組合單(標籤不採信)
- `[top_gamma]` 265.00P exp=2026-12-04(DTE=14) dir=SELL(greek) g$=-69.36M spread✓組合單(標籤不採信)
- `[top_gamma]` 251.00P exp=2026-12-18(DTE=28) dir=SELL(greek) g$=-39.45M spread✓組合單(標籤不採信)
- `[top_gamma]` 245.00P exp=2026-12-18(DTE=28) dir=BUY(greek) g$=+41.07M spread✓組合單(標籤不採信)
- `[top_vega]` 254.00P exp=2026-12-04(DTE=14) dir=BUY(greek) v$=+1.08M spread✓組合單(標籤不採信)
- `[top_vega]` 265.00P exp=2026-12-04(DTE=14) dir=SELL(greek) v$=-663.29K spread✓組合單(標籤不採信)
- `[top_vega]` 251.00P exp=2026-12-18(DTE=28) dir=SELL(greek) v$=-754.48K spread✓組合單(標籤不採信)
- `[top_vega]` 245.00P exp=2026-12-18(DTE=28) dir=BUY(greek) v$=+785.44K spread✓組合單(標籤不採信)
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=5103.0｜買240P/賣265P｜exp=2026-12-18｜淨d$=+173.04M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: 🟡 雙極切換 (5/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[38, 6, 92, 93, 100]

### 🟢 QQQ — (4 合約 / 6 榜次 ＋ 1 sym級)

- `[pkg #9068.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買590P/賣650P（分類量 21,495/18,067）
  - ↳ 淨prem$=-96.19M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9147.0]` 2 腿·P 垂直 exp=2026-11-30  賣630P/買665P（分類量 3,651/9,673）
  - ↳ 淨prem$=+44.32M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 650.00P exp=2027-01-15(DTE=56) dir=SELL(prem) tot_prem=+99.40M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 99%，已分類 18,067 口）  [SG:9068.0]
- `[unusual]` 590.00P exp=2026-11-23(DTE=3 ⛔已到期) dir=BUY(prem) tot_prem=+2.85M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 85%，已分類 21,495 口）  [SG:9068.0]
- `[largest_premium]` 590.00P exp=2026-11-23(DTE=3 ⛔已到期) dir=BUY(prem) prem$=+2.64M spread✓組合單(標籤不採信)
- `[largest_premium]` 665.00P exp=2026-11-30(DTE=10) dir=BUY(prem) prem$=+53.18M spread✓組合單(標籤不採信)
- `[largest_premium]` 630.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-8.86M spread✓組合單(標籤不採信)
- `[largest_premium]` 650.00P exp=2027-01-15(DTE=56) dir=SELL(prem) prem$=-98.83M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=11,244,078 |ΔsynthOI|=939,954 ΔOI=+147,755 flow_ratio= 11.96 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: 🟢 Short Put → bullish（prem 判向，集中度 99%，已分類 18,067 口）  [SG:9068.0]  [prem_conc=99%]
- **Structure**: 🟢 short_put_flow  (同 expiry 無其他 unusual leg)
- **資料品質**: ✅ bto/sto 欄與 prem=sell 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 SOXX — (2 合約 / 5 榜次)

- `[pkg #10754.0]` 2 腿·P 垂直 exp=2026-12-18  買125P/賣150P（分類量 29,617/15,827）
  - ↳ 淨prem$=+48.22M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 125.00P exp=2026-12-18(DTE=28) dir=BUY(prem) symvol=350,883 tot_prem=+142.81M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 29,617 口）  [SG:10754.0]
- `[unusual]` 150.00P exp=2026-12-18(DTE=28) dir=SELL(prem) symvol=350,883 tot_prem=+105.01M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 15,827 口）  [SG:10754.0]
- `[largest_premium]` 125.00P exp=2026-12-18(DTE=28) dir=BUY(prem) prem$=+116.64M spread✓組合單(標籤不採信)
- `[largest_premium]` 150.00P exp=2026-12-18(DTE=28) dir=SELL(prem) prem$=-68.42M spread✓組合單(標籤不採信)
- `[single_stocks]` 125.00P exp=2026-12-18(DTE=28) dir=?(none·勿判) iv=74.2% bto/sto⚠未校驗·勿判向：BTO=24,191 BTC=5,426
- **F7 unusual**: 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 29,617 口）  [SG:10754.0]  [prem_conc=n/a]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜panic / conviction 型：主動新開空頭 — 持續性中等，留意反轉（已分類量 29,617 口、開倉佔 82%）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（main side=buy type=P 非賣方側 put/call）｜spread_id=10754.0｜買125P/賣150P｜exp=2026-12-18｜淨prem=+48.22M)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 TSM — (3 合約 / 9 榜次)　⚑ 單筆極端 d$#3

- `[unusual]` 420.00P exp=2027-01-15(DTE=56) dir=BUY(greek) symvol=255,583 tot_prem=+103.57M → 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,914 口）
- `[unusual]` 410.00P exp=2027-01-15(DTE=56) dir=BUY(greek) symvol=255,583 tot_prem=+95.89M → 🔴 Long Put → bearish（greek 判向，集中度 100%，已分類 10,016 口）
- `[unusual]` 400.00P exp=2027-01-15(DTE=56) dir=BUY(greek) symvol=255,583 tot_prem=+87.00M → 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,975 口）
- `[top_delta]` 420.00P exp=2027-01-15(DTE=56) dir=BUY(greek) d$=-263.91M
- `[top_delta]` 410.00P exp=2027-01-15(DTE=56) dir=BUY(greek) d$=-257.33M
- `[top_delta]` 400.00P exp=2027-01-15(DTE=56) dir=BUY(greek) d$=-248.23M
- `[largest_premium]` 420.00P exp=2027-01-15(DTE=56) dir=BUY(greek) prem$=+103.56M
- `[largest_premium]` 410.00P exp=2027-01-15(DTE=56) dir=BUY(greek) prem$=+95.69M
- `[largest_premium]` 400.00P exp=2027-01-15(DTE=56) dir=BUY(greek) prem$=+86.88M
- **F7 unusual**: 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,914 口）  [prem_conc=n/a]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（BTC）**為主 ⇒ 是回補既有空頭 put，**不是**新開空單；勿當 panic 讀（已分類量 9,914 口、平倉佔 100%）
- **Structure**: ⬜ unknown  (main side=buy type=P 非賣方側 put/call)
- **資料品質**: ✅ bto/sto 欄與 greek=buy 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ XAR — (2 合約 / 6 榜次)

- `[pkg #14852.0]` 2 腿·P 垂直 exp=2027-01-15  買200P/賣225P（分類量 24,995/18,001）
  - ↳ 淨v$=+248.57K ⇒ 買方側淨**買** vega｜淨d$=+50.33M  淨prem$=-19.83M
- `[top_delta]` 225.00P exp=2027-01-15(DTE=56) dir=SELL(greek) d$=+249.47M spread✓組合單(標籤不採信)
- `[top_delta]` 200.00P exp=2027-01-15(DTE=56) dir=BUY(greek) d$=-199.14M spread✓組合單(標籤不採信)
- `[top_vega]` 200.00P exp=2027-01-15(DTE=56) dir=BUY(greek) v$=+770.85K spread✓組合單(標籤不採信)
- `[top_vega]` 225.00P exp=2027-01-15(DTE=56) dir=SELL(greek) v$=-522.28K spread✓組合單(標籤不採信)
- `[largest_premium]` 225.00P exp=2027-01-15(DTE=56) dir=SELL(greek) prem$=-44.39M spread✓組合單(標籤不採信)
- `[largest_premium]` 200.00P exp=2027-01-15(DTE=56) dir=BUY(greek) prem$=+24.56M spread✓組合單(標籤不採信)
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=14852.0｜買200P/賣225P｜exp=2027-01-15｜淨v$=+248.57K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ AAPL — (2 合約 / 2 榜次 ＋ 1 sym級)

- `[pkg #225.0]` 2 腿·P 垂直 exp=2026-11-25  賣325P/買335P（分類量 3,658/5,252）
  - ↳ 淨g$=+15.21M ⇒ 買方側淨**買** gamma
- `[top_gamma]` 335.00P exp=2026-11-25(DTE=5 ⚠️短天期) dir=BUY(greek) g$=+17.99M spread✓組合單(標籤不採信)
- `[top_gamma]` 325.00P exp=2026-11-25(DTE=5 ⚠️短天期) dir=SELL(greek) g$=-2.78M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=1,378,640 |ΔsynthOI|=197,773 ΔOI=-211,017 flow_ratio=  6.97 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=225.0｜賣325P/買335P｜exp=2026-11-25｜淨g$=+15.21M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ CCJ — (2 合約 / 4 榜次)

- `[pkg #1930.0]` 2 腿·C 垂直 exp=2027-03-19  買80C/賣90C（分類量 72,556/72,717）
  - ↳ 淨v$=+222.38K ⇒ 買方側淨**買** vega
- `[top_vega]` 80.00C exp=2027-03-19(DTE=119) dir=BUY(greek) v$=+649.20K spread✓組合單(標籤不採信)
- `[top_vega]` 90.00C exp=2027-03-19(DTE=119) dir=SELL(greek) v$=-426.82K spread✓組合單(標籤不採信)
- `[single_stocks]` 80.00C exp=2027-03-19(DTE=119) dir=BUY(greek) iv=57.3% bto/sto⚠未校驗·勿判向：BTO=72,555 STO=1
- `[single_stocks]` 90.00C exp=2027-03-19(DTE=119) dir=SELL(greek) iv=56.9% bto/sto⚠未校驗·勿判向：STO=14 STC=72,703
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=1930.0｜買80C/賣90C｜exp=2027-03-19｜淨v$=+222.38K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ CORZ — (3 合約 / 3 榜次 ＋ 1 sym級)

- `[sig_position]` d=  0th g= 41th v= 36th sector=Technology
- `[single_stocks]` 9.00P exp=2026-12-18(DTE=28) dir=?(none·勿判) iv=117.0% bto/sto⚠未校驗·勿判向：BTO=60,447
- `[single_stocks]` 15.00C exp=2026-12-18(DTE=28) dir=?(none·勿判) iv=91.2% bto/sto⚠未校驗·勿判向：BTO=2,371 STO=35,357
- `[single_stocks]` 7.00P exp=2027-01-15(DTE=56) dir=?(none·勿判) iv=108.3% bto/sto⚠未校驗·勿判向：BTO=4 STO=37,020
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[55, 0]

### ⬜ HYG — (8 合約 / 10 榜次)　⚑ 單筆極端 g$#2

- `[pkg #4280.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買76P/賣77P（分類量 5,092/5,060）
  - ↳ 淨g$=+8.30M ⇒ 買方側淨**買** gamma
- `[pkg #4285.0]` 2 腿·P 垂直 exp=2027-01-15  賣73P/買76P（分類量 54,514/56,960）
  - ↳ 淨g$=+77.98M ⇒ 買方側淨**買** gamma
- `[pkg #4292.0]` 2 腿·P 垂直 exp=2026-12-11  買74.5P/賣76.5P（分類量 15,000/13,000）
  - ↳ 淨g$=-32.68M ⇒ 買方側淨**賣** gamma
- `[pkg #4294.0]` 2 腿·P 垂直 exp=2026-12-18  賣74P/買76P（分類量 12,943/16,867）
  - ↳ 淨g$=+32.27M ⇒ 買方側淨**買** gamma
- `[top_gamma]` 76.00P exp=2026-11-27(DTE=7 ⚠️短天期) dir=BUY(greek) g$=+16.57M spread✓組合單(標籤不採信)
- `[top_gamma]` 76.50P exp=2026-12-11(DTE=21) dir=SELL(greek) g$=-35.06M spread✓組合單(標籤不採信)
- `[top_gamma]` 74.50P exp=2026-12-11(DTE=21) dir=BUY(greek) g$=+2.38M spread✓組合單(標籤不採信)
- `[top_gamma]` 76.00P exp=2026-12-18(DTE=28) dir=BUY(greek) g$=+33.22M spread✓組合單(標籤不採信)
- `[top_gamma]` 74.00P exp=2026-12-18(DTE=28) dir=SELL(greek) g$=-950.24K spread✓組合單(標籤不採信)
- `[top_gamma]` 76.00P exp=2027-01-15(DTE=56) dir=BUY(greek) g$=+80.04M spread✓組合單(標籤不採信)
- `[top_gamma]` 73.00P exp=2027-01-15(DTE=56) dir=SELL(greek) g$=-2.06M spread✓組合單(標籤不採信)
- `[top_gamma]` 77.00P exp=2027-01-15(DTE=56) dir=SELL(greek) g$=-8.27M spread✓組合單(標籤不採信)
- `[asset_etfs]` 73.00P exp=2027-01-15(DTE=56) dir=SELL(greek) iv=11.2% bto/sto⚠未校驗·勿判向：BTO=13 STO=54,501
- `[asset_etfs]` 76.00P exp=2027-01-15(DTE=56) dir=BUY(greek) iv=8.9% bto/sto⚠未校驗·勿判向：BTO=56,871 STO=89
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=4285.0｜賣73P/買76P｜exp=2027-01-15｜淨g$=+77.98M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[17]

### ⬜ META — (3 合約 / 6 榜次)　⚑ 單筆極端 v$#2

- `[pkg #5825.0]` 2 腿·C 垂直 exp=2027-02-19  買650C/賣700C（分類量 5,824/17,593）
  - ↳ 淨v$=-778.71K ⇒ 買方側淨**賣** vega｜淨d$=-90.91M
- `[top_delta]` 635.00C exp=2027-01-15(DTE=56) dir=BUY(greek) d$=+179.57M
- `[top_delta]` 700.00C exp=2027-02-19(DTE=91) dir=SELL(greek) d$=-187.31M spread✓組合單(標籤不採信)
- `[top_delta]` 650.00C exp=2027-02-19(DTE=91) dir=BUY(greek) d$=+96.40M spread✓組合單(標籤不採信)
- `[top_vega]` 635.00C exp=2027-01-15(DTE=56) dir=BUY(greek) v$=+862.40K
- `[top_vega]` 700.00C exp=2027-02-19(DTE=91) dir=SELL(greek) v$=-1.34M spread✓組合單(標籤不採信)
- `[top_vega]` 650.00C exp=2027-02-19(DTE=91) dir=BUY(greek) v$=+561.29K spread✓組合單(標籤不採信)
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=5825.0｜買650C/賣700C｜exp=2027-02-19｜淨v$=-778.71K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ NDX — (4 合約 / 4 榜次 ＋ 1 sym級)　⚑ 單筆極端 prem#2

- `[pkg #6749.0]` 2 腿·P 垂直 exp=2026-11-30  買27000P/賣28000P（分類量 510/507）
  - ↳ 淨prem$=-48.02M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #6758.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣27000P/買24000P（分類量 1,168/1,043）
  - ↳ 淨prem$=-117.44M ⇒ 買方側淨**收**權利金(貸記)
- `[top_index]` 28000.00P exp=2026-11-30(DTE=10) dir=SELL(prem) prem$=-150.03M spread✓組合單(標籤不採信)
- `[top_index]` 27000.00P exp=2026-11-30(DTE=10) dir=BUY(prem) prem$=+102.01M spread✓組合單(標籤不採信)
- `[top_index]` 27000.00P exp=2026-12-18(DTE=28) dir=SELL(prem) prem$=-256.63M spread✓組合單(標籤不採信)
- `[top_index]` 24000.00P exp=2027-03-19(DTE=119) dir=BUY(prem) prem$=+139.19M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=89,632 |ΔsynthOI|=8,324 ΔOI=-9,743 flow_ratio= 10.77 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_roll_or_calendar  (p3–p6 fallback（無 F7 解碼）｜spread_id=6758.0｜賣27000P/買24000P｜跨 exp 2026-12-18/2027-03-19｜淨prem=-117.44M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ SMH — (1 合約 / 2 榜次)

- `[top_delta]` 480.00P exp=2026-12-18(DTE=28) dir=SELL(greek) d$=+166.30M
- `[largest_premium]` 480.00P exp=2026-12-18(DTE=28) dir=SELL(greek) prem$=-43.98M
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ XSP — (2 合約 / 4 榜次)

- `[pkg #15137.0]` 2 腿·P 垂直 exp=2027-03-19  買690P/賣710P（分類量 5,273/5,141）
  - ↳ 淨v$=+11.26K ⇒ 買方側淨**買** vega｜淨d$=+27.50M
- `[top_delta]` 710.00P exp=2027-03-19(DTE=119) dir=SELL(greek) d$=+185.83M spread✓組合單(標籤不採信)
- `[top_delta]` 690.00P exp=2027-03-19(DTE=119) dir=BUY(greek) d$=-158.33M spread✓組合單(標籤不採信)
- `[top_vega]` 690.00P exp=2027-03-19(DTE=119) dir=BUY(greek) v$=+818.83K spread✓組合單(標籤不採信)
- `[top_vega]` 710.00P exp=2027-03-19(DTE=119) dir=SELL(greek) v$=-807.57K spread✓組合單(標籤不採信)
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=15137.0｜買690P/賣710P｜exp=2027-03-19｜淨v$=+11.26K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[1]

---

**摘要**：19 候選 / 0 教科書級

---

### 🏷️ F12 Cross-day IC / Strangle 賣方收斂結構（掃描 10 日）

#### 📌 SOXX

- 雙側 STO：賣 170C（2日）+ 賣 150P（1日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [6, 0, 3, 0, 0, 0, 2, 0, 1, 2]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤170C + sell BuPS ≥150P
- 現價 $123.38，在區間 [150~170] 的 -133th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SPX

- 雙側 STO：賣 8175C（2日）+ 賣 7520P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [4, 0, 1, 0, 1, 5, 2, 0, 4, 6]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤8175C + sell BuPS ≥7520P
- 現價 $6910.39，在區間 [7520~8175] 的 -93th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 NVDA

- 雙側 STO：賣 190C（5日）+ 賣 185P（3日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [5, 20, 0, 13, 7, 1, 0, 5, 1, 1]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤190C + sell BuPS ≥185P
- 現價 $125.79，在區間 [185~190] 的 -1184th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SPCX

- 雙側 STO：賣 160C（1日）+ 賣 115P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [6, 2, 0, 0, 0, 0, 5, 0, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤160C + sell BuPS ≥115P
- 現價 $127.96，在區間 [115~160] 的 29th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 VIX

- 雙側 STO：賣 24C（2日）+ 賣 20P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [4, 2, 7, 0, 6, 4]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤24C + sell BuPS ≥20P
- 現價 $35.89，在區間 [20~24] 的 397th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空
