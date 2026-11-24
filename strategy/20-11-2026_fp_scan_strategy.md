## 07:05:40 — `roma_cli fp_scan 2026-11-20`

<sub>`v7.40 (7d13b007) | loaded 2026-11-20T00:47:06 | src ✅`</sub>

### 🎯 fp_scan 機會掃描（2026-11-20 🟡age=2td）

來源：flowpatrol_2026_11_20.pdf  
🟡 FP age=2td（偏舊）：資料截至 2026-11-19 收盤（此檔 publish=2026-11-20）、非 live tape；如需同日水位見 data_table  
模式：寬鬆 (cross≥2  extreme≤5  p8≤2)   候選 19 sym  

#### 📖 圖例（內容固定，只講讀法；與當日判斷無關。4 段）

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

---

### 📐 本 session 組合結構（幾何候選 1 組）

- `[struct·強]` VIX 蝶式1:2:1 17/18/19P exp=2026-12-16  （分類量 47,147/97,579/52,704）
  - ↳ 幾何偏差 10.5%（候選帶）｜等距 0.0%·量比 10.5%｜pkg 圖樣 FFF｜來源 index_etfs+largest_premium｜**無 spread_id**·僅本層看得到

### 🟢 VIX — (8 合約 / 22 榜次 ＋ 1 sym級)

- `[pkg #11579.0]` 2 腿·strangle(雙買) exp=2026-12-16  買20P/買45C（分類量 78,633/45,012）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #11584.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣18P/賣45C（分類量 97,579/56,924）
  - ↳ 淨prem$=-45.29M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #11614.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣65C/買65C（分類量 101,635/119,942）
  - ↳ 淨v$=+330.73K ⇒ 買方側淨**買** vega｜淨d$=+71.71M  淨prem$=+35.51M
- `[sig_position]` d= 53th g= 49th v= 94th sector=Volatility ETF
- `[unusual]` 65.00C exp=2027-01-20(DTE=62) dir=BUY(greek) tot_prem=+45.95M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 100%，已分類 119,942 口）  [SG:11614.0]
- `[unusual]` 65.00C exp=2026-12-16(DTE=27) dir=SELL(greek) tot_prem=+10.59M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 101,635 口）  [SG:11614.0]
- `[unusual]` 45.00C exp=2027-01-20(DTE=62) dir=SELL(prem) tot_prem=+35.84M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 56,924 口）  [SG:11584.0]
- `[unusual]` 18.00P exp=2026-12-16(DTE=27) dir=SELL(prem) tot_prem=+17.12M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 97,579 口）  [SG:11584.0]
- `[unusual]` 20.00P exp=2026-12-16(DTE=27) dir=BUY(prem) tot_prem=+19.44M spread✓組合單(標籤不採信) → ⚪ Long Put → 方向中性（pkg strangle(雙買)＝同邊 C+P 波動包裹，不逐腿判多空；prem 判邊，已分類 78,633 口）  [SG:11579.0]
- `[unusual]` 45.00C exp=2026-12-16(DTE=27) dir=BUY(prem) tot_prem=+12.62M spread✓組合單(標籤不採信) → ⚪ Long Call → 方向中性（pkg strangle(雙買)＝同邊 C+P 波動包裹，不逐腿判多空；prem 判邊，已分類 45,012 口）  [SG:11579.0]
- `[top_delta]` 65.00C exp=2026-12-16(DTE=27) dir=SELL(greek) d$=-42.92M spread✓組合單(標籤不採信)
- `[top_delta]` 65.00C exp=2027-01-20(DTE=62) dir=BUY(greek) d$=+114.63M spread✓組合單(標籤不採信)
- `[top_vega]` 65.00C exp=2026-12-16(DTE=27) dir=SELL(greek) v$=-182.07K spread✓組合單(標籤不採信)
- `[top_vega]` 65.00C exp=2027-01-20(DTE=62) dir=BUY(greek) v$=+512.80K spread✓組合單(標籤不採信)
- `[largest_premium]` 65.00C exp=2026-12-16(DTE=27) dir=SELL(greek) prem$=-10.43M spread✓組合單(標籤不採信)
- `[largest_premium]` 18.00P exp=2026-12-16(DTE=27) dir=SELL(prem) prem$=-9.45M spread✓組合單(標籤不採信)
- `[largest_premium]` 65.00C exp=2027-01-20(DTE=62) dir=BUY(greek) prem$=+45.94M spread✓組合單(標籤不採信)
- `[largest_premium]` 45.00C exp=2027-01-20(DTE=62) dir=SELL(prem) prem$=-35.84M spread✓組合單(標籤不採信)
- `[index_etfs]` 17.00P exp=2026-12-16(DTE=27) dir=?(none·勿判) iv=90.5% bto/sto⚠未校驗·勿判向：STO=12,671 STC=34,476
- `[index_etfs]` 18.00P exp=2026-12-16(DTE=27) dir=?(none·勿判) iv=96.1% bto/sto⚠未校驗·勿判向：STO=53,837 STC=43,742
- `[index_etfs]` 19.00P exp=2026-12-16(DTE=27) dir=?(none·勿判) iv=102.3% bto/sto⚠未校驗·勿判向：BTO=28,312 BTC=24,392
- `[index_etfs]` 20.00P exp=2026-12-16(DTE=27) dir=?(none·勿判) iv=107.6% bto/sto⚠未校驗·勿判向：BTO=43,693 BTC=34,940
- `[index_etfs]` 45.00C exp=2026-12-16(DTE=27) dir=?(none·勿判) iv=190.7% bto/sto⚠未校驗·勿判向：BTC=44,642 STC=370
- `[index_etfs]` 65.00C exp=2026-12-16(DTE=27) dir=SELL(greek) iv=218.3% bto/sto⚠未校驗·勿判向：STO=1,601 STC=100,034
- `[index_etfs]` 45.00C exp=2027-01-20(DTE=62) dir=?(none·勿判) iv=143.6% bto/sto⚠未校驗·勿判向：STO=56,923 STC=1
- `[index_etfs]` 65.00C exp=2027-01-20(DTE=62) dir=BUY(greek) iv=163.4% bto/sto⚠未校驗·勿判向：BTO=119,940 STO=2
- **F7 unusual**: 🟢 Long Call → bullish（greek 判向，集中度 100%，已分類 119,942 口）  [SG:11614.0]  [prem_conc=100%]
- **Structure**: 🔷 p36_roll_or_calendar  (p3–p6 fallback（main side=buy type=C 非賣方側 put/call）｜spread_id=11614.0｜賣65C/買65C｜跨 exp 2026-12-16/2027-01-20｜淨v$=+330.73K)
- **資料品質**: ✅ bto/sto 欄與 greek=buy 一致
- **F8 sig 跨日**: ⚪ 跨日無極端 (2/10 報告 d 在 30~70)  d_seq=[65, 53]

### 🔴 XSP — (3 合約 / 10 榜次 ＋ 1 sym級)　⚑ 單筆極端 d$#1 g$#1 v$#1

- `[sig_position]` d=  1th g= 98th v=  5th sector=Equity ETF
- `[unusual]` 730.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(greek) symvol=338,327 tot_prem=+26.45M → 🔴 Long Put → bearish（greek 判向，集中度 90%，已分類 21,127 口）
- `[unusual]` 695.00P exp=2027-01-29(DTE=71) dir=SELL(greek) symvol=338,327 tot_prem=+23.60M → 🟢 Short Put → bullish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 17,264 口）
- `[top_delta]` 730.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(greek) d$=-1.30B
- `[top_delta]` 715.00P exp=2026-12-11(DTE=22) dir=SELL(greek) d$=+115.57M
- `[top_delta]` 695.00P exp=2027-01-29(DTE=71) dir=SELL(greek) d$=+390.88M
- `[top_gamma]` 730.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(greek) g$=+141.67M
- `[top_gamma]` 695.00P exp=2027-01-29(DTE=71) dir=SELL(greek) g$=-49.48M
- `[top_vega]` 695.00P exp=2027-01-29(DTE=71) dir=SELL(greek) v$=-1.94M
- `[largest_premium]` 730.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(greek) prem$=+25.19M
- `[largest_premium]` 695.00P exp=2027-01-29(DTE=71) dir=SELL(greek) prem$=-23.60M
- **F7 unusual**: 🔴 Long Put → bearish（greek 判向，集中度 90%，已分類 21,127 口）  [prem_conc=90%]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（BTC）**為主 ⇒ 是回補既有空頭 put，**不是**新開空單；勿當 panic 讀（已分類量 21,127 口、平倉佔 100%）
- **Structure**: ⬜ unknown  (main side=buy type=P 非賣方側 put/call)
- **資料品質**: ✅ bto/sto 欄與 greek=buy 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[1]

### 🟢 AMD — (2 合約 / 8 榜次 ＋ 1 sym級)　⚑ 單筆極端 v$#4

- `[pkg #438.0]` 2 腿·C 垂直 exp=2027-02-19  買640C/賣700C（分類量 9,479/9,717）
  - ↳ 淨v$=+58.53K ⇒ 買方側淨**買** vega｜淨d$=+32.35M  淨prem$=+11.31M
- `[unusual]` 640.00C exp=2027-02-19(DTE=92) dir=BUY(greek) tot_prem=+58.26M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 100%，已分類 9,479 口）  [SG:438.0]
- `[unusual]` 700.00C exp=2027-02-19(DTE=92) dir=SELL(greek) tot_prem=+47.99M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 96%，已分類 9,717 口）  [SG:438.0]
- `[top_delta]` 640.00C exp=2027-02-19(DTE=92) dir=BUY(greek) d$=+194.60M spread✓組合單(標籤不採信)
- `[top_delta]` 700.00C exp=2027-02-19(DTE=92) dir=SELL(greek) d$=-162.25M spread✓組合單(標籤不採信)
- `[top_vega]` 640.00C exp=2027-02-19(DTE=92) dir=BUY(greek) v$=+909.21K spread✓組合單(標籤不採信)
- `[top_vega]` 700.00C exp=2027-02-19(DTE=92) dir=SELL(greek) v$=-850.68K spread✓組合單(標籤不採信)
- `[largest_premium]` 640.00C exp=2027-02-19(DTE=92) dir=BUY(greek) prem$=+58.23M spread✓組合單(標籤不採信)
- `[largest_premium]` 700.00C exp=2027-02-19(DTE=92) dir=SELL(greek) prem$=-46.92M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=1,206,132 |ΔsynthOI|=161,779 ΔOI=+43,532 flow_ratio=  7.46 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: 🟢 Long Call → bullish（greek 判向，集中度 100%，已分類 9,479 口）  [SG:438.0]  [prem_conc=100%]
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（main side=buy type=C 非賣方側 put/call）｜spread_id=438.0｜買640C/賣700C｜exp=2027-02-19｜淨v$=+58.53K)
- **資料品質**: ✅ bto/sto 欄與 greek=buy 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[95]

### ⬜ IWM — (21 合約 / 35 榜次 ＋ 1 sym級)　⚑ 單筆極端 d$#2 g$#2

- `[pkg #4202.0]` 2 腿·P 垂直 exp=2026-11-25  賣240P/買261P（分類量 6,027/6,943）
  - ↳ 淨g$=+21.64M ⇒ 買方側淨**買** gamma
- `[pkg #4205.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣265P/買260P（分類量 12,456/8,500）
  - ↳ 淨g$=-17.71M ⇒ 買方側淨**賣** gamma
- `[pkg #4214.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買250P/賣290P（分類量 5,005/5,001）
  - ↳ 淨v$=-491.70K ⇒ 買方側淨**賣** vega
- `[pkg #4261.0]` 2 腿·P 垂直 exp=2026-12-18  買256P/賣279P（分類量 9,696/10,005）
  - ↳ 淨d$=+127.96M ⇒ 買方側淨 delta **多**
- `[pkg #4262.0]` 2 腿·P 垂直 exp=2026-12-18  買251P/賣257P（分類量 28,986/30,009）
  - ↳ 淨g$=-9.79M ⇒ 買方側淨**賣** gamma｜淨v$=-185.60K  淨d$=+94.44M
- `[pkg #4291.0]` 2 腿·P 垂直 exp=2026-12-18  賣240P/買270P（分類量 6,511/7,040）
  - ↳ 淨d$=-100.36M ⇒ 買方側淨 delta **空**
- `[pkg #4312.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣263P/賣315C（分類量 13,365/12,468）
  - ↳ 淨g$=-110.34M ⇒ 買方側淨**賣** gamma｜淨v$=-852.89K  淨d$=+48.32M
- `[pkg #4325.0]` 2 腿·P 垂直 exp=2026-12-18  買230P/賣265P（分類量 7,229/12,110）
  - ↳ 淨d$=+113.08M ⇒ 買方側淨 delta **多**
- `[pkg #4330.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣270P/買255P（分類量 20,183/18,250）
  - ↳ 淨g$=-13.47M ⇒ 買方側淨**賣** gamma｜淨v$=+428.01K  淨d$=+362.85M
- `[pkg #4334.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣235P/買265P（分類量 4,333/7,119）
  - ↳ 淨v$=+747.64K ⇒ 買方側淨**買** vega
- `[sig_position]` d=100th g=  1th v=  1th sector=Equity ETF
- `[top_delta]` 270.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) d$=+494.81M spread✓組合單(標籤不採信)
- `[top_delta]` 263.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) d$=+124.51M spread✓組合單(標籤不採信)
- `[top_delta]` 270.00P exp=2026-11-27(DTE=8) dir=SELL(greek) d$=+437.04M
- `[top_delta]` 255.00P exp=2026-12-18(DTE=29) dir=BUY(greek) d$=-131.96M spread✓組合單(標籤不採信)
- `[top_delta]` 257.00P exp=2026-12-18(DTE=29) dir=SELL(greek) d$=+248.65M spread✓組合單(標籤不採信)
- `[top_delta]` 251.00P exp=2026-12-18(DTE=29) dir=BUY(greek) d$=-154.21M spread✓組合單(標籤不採信)
- `[top_delta]` 279.00P exp=2026-12-18(DTE=29) dir=SELL(greek) d$=+203.11M spread✓組合單(標籤不採信)
- `[top_delta]` 256.00P exp=2026-12-18(DTE=29) dir=BUY(greek) d$=-75.15M spread✓組合單(標籤不採信)
- `[top_delta]` 265.00P exp=2026-12-18(DTE=29) dir=SELL(greek) d$=+116.20M spread✓組合單(標籤不採信)
- `[top_delta]` 230.00P exp=2026-12-18(DTE=29) dir=BUY(greek) d$=-3.12M spread✓組合單(標籤不採信)
- `[top_delta]` 270.00P exp=2026-12-18(DTE=29) dir=BUY(greek) d$=-111.20M spread✓組合單(標籤不採信)
- `[top_delta]` 240.00P exp=2026-12-18(DTE=29) dir=SELL(greek) d$=+10.84M spread✓組合單(標籤不採信)
- `[top_delta]` 315.00C exp=2027-06-30(DTE=223) dir=SELL(greek) d$=-76.19M spread✓組合單(標籤不採信)
- `[top_gamma]` 263.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) g$=-104.96M spread✓組合單(標籤不採信)
- `[top_gamma]` 265.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) g$=-37.33M spread✓組合單(標籤不採信)
- `[top_gamma]` 270.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) g$=-37.32M spread✓組合單(標籤不採信)
- `[top_gamma]` 261.00P exp=2026-11-25(DTE=6 ⚠️短天期) dir=BUY(greek) g$=+21.78M spread✓組合單(標籤不採信)
- `[top_gamma]` 240.00P exp=2026-11-25(DTE=6 ⚠️短天期) dir=SELL(greek) g$=-135.21K spread✓組合單(標籤不採信)
- `[top_gamma]` 270.00P exp=2026-11-27(DTE=8) dir=SELL(greek) g$=-58.29M
- `[top_gamma]` 260.00P exp=2026-11-30(DTE=11) dir=BUY(greek) g$=+19.62M spread✓組合單(標籤不採信)
- `[top_gamma]` 257.00P exp=2026-12-18(DTE=29) dir=SELL(greek) g$=-41.78M spread✓組合單(標籤不採信)
- `[top_gamma]` 251.00P exp=2026-12-18(DTE=29) dir=BUY(greek) g$=+31.99M spread✓組合單(標籤不採信)
- `[top_gamma]` 255.00P exp=2026-12-18(DTE=29) dir=BUY(greek) g$=+23.85M spread✓組合單(標籤不採信)
- `[top_gamma]` 315.00C exp=2027-06-30(DTE=223) dir=SELL(greek) g$=-5.38M spread✓組合單(標籤不採信)
- `[top_vega]` 263.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) v$=-68.64K spread✓組合單(標籤不採信)
- `[top_vega]` 270.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(greek) v$=-24.41K spread✓組合單(標籤不採信)
- `[top_vega]` 235.00P exp=2026-12-04(DTE=15) dir=SELL(greek·微量) v$=-4.34K spread✓組合單(標籤不採信)
- `[top_vega]` 250.00P exp=2026-12-04(DTE=15) dir=BUY(greek) v$=+51.64K spread✓組合單(標籤不採信)
- `[top_vega]` 257.00P exp=2026-12-18(DTE=29) dir=SELL(greek) v$=-792.39K spread✓組合單(標籤不採信)
- `[top_vega]` 251.00P exp=2026-12-18(DTE=29) dir=BUY(greek) v$=+606.80K spread✓組合單(標籤不採信)
- `[top_vega]` 255.00P exp=2026-12-18(DTE=29) dir=BUY(greek) v$=+452.42K spread✓組合單(標籤不採信)
- `[top_vega]` 315.00C exp=2027-06-30(DTE=223) dir=SELL(greek) v$=-784.25K spread✓組合單(標籤不採信)
- `[top_vega]` 265.00P exp=2027-12-17(DTE=393) dir=BUY(greek) v$=+751.97K spread✓組合單(標籤不採信)
- `[top_vega]` 290.00P exp=2027-12-17(DTE=393) dir=SELL(greek) v$=-543.35K spread✓組合單(標籤不採信)
- `[index_etfs]` 257.00P exp=2026-12-18(DTE=29) dir=SELL(greek) iv=27.6% bto/sto⚠未校驗·勿判向：STO=11 STC=29,998
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=4261.0｜買256P/賣279P｜exp=2026-12-18｜淨d$=+127.96M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: 🟡 雙極切換 (5/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[38, 6, 92, 93, 100]

### 🟢 SPY — (10 合約 / 11 榜次 ＋ 2 sym級)

- `[pkg #10043.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣715P/買635P（分類量 25,591/21,977）
  - ↳ 淨prem$=-2.66M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #10052.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣750P/買670P（分類量 6,080/7,499）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #10066.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買740P/賣720P（分類量 6,665/6,740）
  - ↳ 淨值**不可算**（腿間無共同量級軸 ⇒ 不以部分腿加總冒充淨部位）
- `[pkg #10278.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣725P/買692P（分類量 16,877/12,497）
  - ↳ 淨prem$=-12.17M ⇒ 買方側淨**收**權利金(貸記)
- `[sig_position]` d= 99th g=  6th v= 90th sector=Equity ETF
- `[unusual]` 775.00C exp=2026-12-31(DTE=42) dir=BUY(prem) tot_prem=+20.81M → 🟢 Long Call → bullish（prem 判向，集中度 100%，已分類 59,888 口）
- `[unusual]` 750.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) tot_prem=+20.76M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 80%，已分類 6,080 口）  [SG:10052.0]
- `[unusual]` 670.00P exp=2026-12-18(DTE=29) dir=BUY(prem) tot_prem=+1.62M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 50%，已分類 7,499 口）  [SG:10052.0]
- `[unusual]` 740.00P exp=2026-11-24(DTE=5 ⚠️短天期) dir=SELL(prem) tot_prem=+18.93M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 100%，已分類 7,723 口）  [SG:9870.0]
- `[unusual]` 740.00P exp=2026-11-30(DTE=11) dir=BUY(prem) tot_prem=+17.27M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 6,665 口）  [SG:10066.0]
- `[unusual]` 720.00P exp=2026-12-18(DTE=29) dir=SELL(prem) tot_prem=+11.73M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 90%，已分類 6,740 口）  [SG:10066.0]
- `[top_index]` 715.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-5.59M spread✓組合單(標籤不採信)
- `[top_index]` 725.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-14.76M spread✓組合單(標籤不採信)
- `[top_index]` 692.00P exp=2026-11-30(DTE=11) dir=BUY(prem) prem$=+2.59M spread✓組合單(標籤不採信)
- `[top_index]` 635.00P exp=2027-01-15(DTE=57) dir=BUY(prem) prem$=+2.93M spread✓組合單(標籤不採信)
- `[index_etfs]` 775.00C exp=2026-12-31(DTE=42) dir=SELL(sym·單列) ⚠bto/sto=BUY·部分 iv=17.0% bto/sto⚠未校驗·勿判向：BTO=59,875 STO=13
- `[heavy_daytrade]` vol=16,672,206 |ΔsynthOI|=1,159,746 ΔOI=+391,382 flow_ratio= 14.38 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: 🟢 Long Call → bullish（prem 判向，集中度 100%，已分類 59,888 口）  [prem_conc=100%]
- **Structure**: 🔷 p36_roll_or_calendar  (p3–p6 fallback（main side=buy type=C 非賣方側 put/call）｜spread_id=10278.0｜賣725P/買692P｜跨 exp 2026-11-20/2026-11-30｜淨prem=-12.17M)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: 🟡 雙極切換 (6/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[37, 7, 19, 70, 97, 99]

### ⬜ META — (3 合約 / 7 榜次)　⚑ 單筆極端 v$#2

- `[pkg #4847.0]` 2 腿·C 垂直 exp=2029-01-19  賣600C/買700C（分類量 2,922/2,923）
  - ↳ 淨v$=+70.01K ⇒ 買方側淨**買** vega｜淨d$=-17.34M  淨prem$=-10.23M
- `[top_delta]` 600.00C exp=2029-01-19(DTE=792) dir=SELL(greek) d$=-115.02M spread✓組合單(標籤不採信)
- `[top_delta]` 700.00C exp=2029-01-19(DTE=792) dir=BUY(greek) d$=+97.68M spread✓組合單(標籤不採信)
- `[top_vega]` 700.00C exp=2029-01-19(DTE=792) dir=BUY(greek) v$=+1.01M spread✓組合單(標籤不採信)
- `[top_vega]` 600.00C exp=2029-01-19(DTE=792) dir=SELL(greek) v$=-939.99K spread✓組合單(標籤不採信)
- `[largest_premium]` 600.00C exp=2029-01-19(DTE=792) dir=SELL(greek) prem$=-45.19M spread✓組合單(標籤不採信)
- `[largest_premium]` 700.00C exp=2029-01-19(DTE=792) dir=BUY(greek) prem$=+34.96M spread✓組合單(標籤不採信)
- `[single_stocks]` 647.50C exp=2026-11-20(DTE=1 ⛔已到期) dir=?(none·勿判) iv=74.2% bto/sto⚠未校驗·勿判向：BTO=163 STO=22,750
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=4847.0｜賣600C/買700C｜exp=2029-01-19｜淨v$=+70.01K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[5]

### ⬜ TLT — (4 合約 / 7 榜次 ＋ 1 sym級)

- `[sig_position]` d= 95th g= 85th v= 99th sector=Bond ETF
- `[top_gamma]` 80.00C exp=2026-11-30(DTE=11) dir=BUY(greek) g$=+30.41M
- `[top_gamma]` 88.00C exp=2027-01-15(DTE=57) dir=BUY(greek) g$=+24.21M
- `[top_vega]` 88.00C exp=2027-01-15(DTE=57) dir=BUY(greek) v$=+428.75K
- `[asset_etfs]` 80.00C exp=2026-11-30(DTE=11) dir=BUY(greek) iv=10.4% bto/sto⚠未校驗·勿判向：BTO=19,442 STO=2
- `[asset_etfs]` 82.00C exp=2026-12-18(DTE=29) dir=?(none·勿判) iv=12.1% bto/sto⚠未校驗·勿判向：BTO=23,177 STO=1,349
- `[asset_etfs]` 76.00P exp=2027-01-15(DTE=57) dir=?(none·勿判) iv=12.6% bto/sto⚠未校驗·勿判向：STO=19 STC=13,108
- `[asset_etfs]` 88.00C exp=2027-01-15(DTE=57) dir=BUY(greek) iv=14.2% bto/sto⚠未校驗·勿判向：BTO=451 BTC=199,999
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_pkg_other  (p3–p6 fallback（無 F7 解碼）｜同 sym 僅此 2 腿｜買80C/買88C｜跨 exp 2026-11-30/2027-01-15｜淨g$=+54.62M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (3/10 報告，未過半)，雜訊概率高  d_seq=[86, 50, 95]

### ⬜ HYG — (3 合約 / 4 榜次 ＋ 1 sym級)

- `[sig_position]` d= 17th g= 46th v=  6th sector=Bond ETF
- `[top_gamma]` 78.00C exp=2027-02-19(DTE=92) dir=SELL(greek) g$=-34.81M
- `[asset_etfs]` 76.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=?(none·勿判) iv=9.4% bto/sto⚠未校驗·勿判向：BTO=91 BTC=26,443
- `[asset_etfs]` 75.00P exp=2026-12-18(DTE=29) dir=?(none·勿判) iv=9.1% bto/sto⚠未校驗·勿判向：BTO=69 BTC=15,506
- `[asset_etfs]` 78.00C exp=2027-02-19(DTE=92) dir=SELL(greek) iv=3.9% bto/sto⚠未校驗·勿判向：BTC=10,000 STC=38,968
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[17]

### 🔴 PANW — (5 合約 / 7 榜次)

- `[pkg #6359.0]` 2 腿·C 垂直 exp=2026-12-18  買250C/賣410C（分類量 3,000/1,536）
  - ↳ 淨prem$=+32.03M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #6364.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買375C/賣260C（分類量 1,841/2,000）
  - ↳ 淨prem$=-23.41M ⇒ 買方側淨**收**權利金(貸記)
- `[unusual]` 330.00C exp=2026-11-27(DTE=8) dir=SELL(greek) symvol=79,545 tot_prem=+25.01M → 🔴 Short Call → bearish（greek 判向，集中度 100%，已分類 7,015 口）
- `[top_delta]` 330.00C exp=2026-11-27(DTE=8) dir=SELL(greek) d$=-209.17M
- `[largest_premium]` 375.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(prem) prem$=+209.31K spread✓組合單(標籤不採信)
- `[largest_premium]` 330.00C exp=2026-11-27(DTE=8) dir=SELL(greek) prem$=-24.97M
- `[largest_premium]` 250.00C exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+33.93M spread✓組合單(標籤不採信)
- `[largest_premium]` 410.00C exp=2026-12-18(DTE=29) dir=SELL(prem) prem$=-1.90M spread✓組合單(標籤不採信)
- `[largest_premium]` 260.00C exp=2027-03-19(DTE=120) dir=SELL(prem) prem$=-23.62M spread✓組合單(標籤不採信)
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 100%，已分類 7,015 口）  [prem_conc=100%]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（STC）**為主 ⇒ 是了結既有多頭 call，**不是**新開空頭／派發；勿當 distribution 讀（已分類量 7,015 口、平倉佔 100%）
- **Structure**: 🔴 short_call_flow  (同 expiry 無其他 unusual leg)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 QQQ — (4 合約 / 5 榜次 ＋ 1 sym級)

- `[pkg #7187.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣656C/賣710P（分類量 6,284/3,641）
  - ↳ 淨prem$=-25.51M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #7199.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買677C/買660P（分類量 11,713/7,719）
  - ↳ 淨prem$=+23.10M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 660.00P exp=2026-12-18(DTE=29) dir=BUY(prem) tot_prem=+23.14M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 7,719 口）  [SG:7199.0]
- `[largest_premium]` 656.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-307.79K spread✓組合單(標籤不採信)
- `[largest_premium]` 677.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(prem·微量) prem$=+3.49K spread✓組合單(標籤不採信)
- `[largest_premium]` 660.00P exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+23.10M spread✓組合單(標籤不採信)
- `[largest_premium]` 710.00P exp=2027-01-15(DTE=57) dir=SELL(prem) prem$=-25.20M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=10,998,552 |ΔsynthOI|=603,696 ΔOI=+259,929 flow_ratio= 18.22 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 7,719 口）  [SG:7199.0]  [prem_conc=n/a]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜panic / conviction 型：主動新開空頭 — 持續性中等，留意反轉（已分類量 7,719 口、開倉佔 100%）
- **Structure**: 🔷 p36_pkg_other  (p3–p6 fallback（main side=buy type=P 非賣方側 put/call）｜spread_id=7187.0｜賣656C/賣710P｜跨 exp 2026-11-20/2027-01-15｜淨prem=-25.51M)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🟢 SPX — (28 合約 / 32 榜次 ＋ 1 sym級)　⚑ 單筆極端 prem#1

- `[pkg #9062.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7360P/買7360P（分類量 1,649/1,433）
  - ↳ 淨prem$=+910.00K ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9103.0]` 2 腿·P 垂直 exp=2027-01-15  買6775P/賣6800P（分類量 7,879/9,251）
  - ↳ 淨prem$=-4.35M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9139.0]` 2 腿·C 垂直 exp=2027-04-16  買7000C/賣9000C（分類量 2,020/1,998）
  - ↳ 淨prem$=+99.11M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9338.0]` 2 腿·P 垂直 exp=2026-12-18  賣5800P/買7245P（分類量 3,560/3,393）
  - ↳ 淨prem$=+63.92M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9378.0]` 2 腿·P 垂直 exp=2026-11-27  賣6975P/買7000P（分類量 7,771/7,730）
  - ↳ 淨prem$=+3.13M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9392.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7290P/賣7450P（分類量 2,244/1,308）
  - ↳ 淨prem$=-21.12M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9438.0]` 2 腿·P 垂直 exp=2027-04-16  賣7000P/買9000P（分類量 1,923/2,000）
  - ↳ 淨prem$=+297.88M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9508.0]` 2 腿·strangle(雙賣) exp=2026-11-20  賣7310P/賣7400C（分類量 2,013/1,221）
  - ↳ 淨prem$=-15.88M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9531.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7405P/買7475C（分類量 2,423/2,509）
  - ↳ 淨prem$=+73.94M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9543.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7390P/買8000C（分類量 1,763/1,710）
  - ↳ 淨prem$=+63.91M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9550.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7200P/賣8200C（分類量 4,952/4,586）
  - ↳ 淨prem$=-111.80M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9552.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7485P/買7600C（分類量 1,394/1,302）
  - ↳ 淨prem$=+51.32M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #9558.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7000C/賣7400P（分類量 1,798/2,013）
  - ↳ 淨prem$=-77.43M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9572.0]` 2 腿·P 垂直 exp=2026-11-20  賣7200P/買7220P（分類量 3,567/3,019）
  - ↳ 淨prem$=+1.81M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 6800.00P exp=2027-01-15(DTE=57) dir=SELL(prem) tot_prem=+68.16M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 70%，已分類 9,251 口）  [SG:9103.0]
- `[unusual]` 6775.00P exp=2027-01-15(DTE=57) dir=BUY(prem) tot_prem=+53.47M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 100%，已分類 7,879 口）  [SG:9103.0]
- `[unusual]` 7000.00P exp=2026-11-27(DTE=8) dir=BUY(prem) tot_prem=+17.79M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 7,730 口）  [SG:9378.0]
- `[unusual]` 6975.00P exp=2026-11-27(DTE=8) dir=SELL(prem) tot_prem=+14.31M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 99%，已分類 7,771 口）  [SG:9378.0]
- `[top_index]` 7220.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(prem) prem$=+15.32M spread✓組合單(標籤不採信)
- `[top_index]` 7200.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-13.51M spread✓組合單(標籤不採信)
- `[top_index]` 7290.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(prem) prem$=+14.21M spread✓組合單(標籤不採信)
- `[top_index]` 7310.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-15.88M spread✓組合單(標籤不採信)
- `[top_index]` 7400.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem·微量) prem$=-4.82K spread✓組合單(標籤不採信)
- `[top_index]` 7000.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-31.76M spread✓組合單(標籤不採信)
- `[top_index]` 7390.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=BUY(prem) prem$=+33.82M spread✓組合單(標籤不採信)
- `[top_index]` 7360.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-26.05M spread✓組合單(標籤不採信)
- `[top_index]` 7360.00P exp=2026-11-23(DTE=4 ⚠️短天期) dir=BUY(prem) prem$=+26.96M spread✓組合單(標籤不採信)
- `[top_index]` 7450.00P exp=2026-11-27(DTE=8) dir=SELL(prem) prem$=-35.33M spread✓組合單(標籤不採信)
- `[top_index]` 7405.00P exp=2026-11-27(DTE=8) dir=BUY(prem) prem$=+58.30M spread✓組合單(標籤不採信)
- `[top_index]` 7000.00P exp=2026-11-27(DTE=8) dir=BUY(prem) prem$=+17.39M spread✓組合單(標籤不採信)
- `[top_index]` 6975.00P exp=2026-11-27(DTE=8) dir=SELL(prem) prem$=-14.26M spread✓組合單(標籤不採信)
- `[top_index]` 7485.00P exp=2026-11-27(DTE=8) dir=BUY(prem) prem$=+43.45M spread✓組合單(標籤不採信)
- `[top_index]` 7200.00P exp=2026-12-18(DTE=29) dir=SELL(prem) prem$=-81.59M spread✓組合單(標籤不採信)
- `[top_index]` 7475.00C exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+15.64M spread✓組合單(標籤不採信)
- `[top_index]` 7245.00P exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+63.92M spread✓組合單(標籤不採信)
- `[top_index]` 5800.00P exp=2026-12-18(DTE=29) dir=SELL(prem·微量) prem$=-2.15K spread✓組合單(標籤不採信)
- `[top_index]` 7400.00P exp=2026-12-18(DTE=29) dir=SELL(prem) prem$=-45.67M spread✓組合單(標籤不採信)
- `[top_index]` 7600.00C exp=2026-12-31(DTE=42) dir=BUY(prem) prem$=+7.87M spread✓組合單(標籤不採信)
- `[top_index]` 6775.00P exp=2027-01-15(DTE=57) dir=BUY(prem) prem$=+53.47M spread✓組合單(標籤不採信)
- `[top_index]` 6800.00P exp=2027-01-15(DTE=57) dir=SELL(prem) prem$=-57.82M spread✓組合單(標籤不採信)
- `[top_index]` 8200.00C exp=2027-03-19(DTE=120) dir=SELL(prem) prem$=-30.21M spread✓組合單(標籤不採信)
- `[top_index]` 9000.00P exp=2027-04-16(DTE=148) dir=BUY(prem) prem$=+343.67M spread✓組合單(標籤不採信)
- `[top_index]` 7000.00P exp=2027-04-16(DTE=148) dir=SELL(prem) prem$=-45.79M spread✓組合單(標籤不採信)
- `[top_index]` 7000.00C exp=2027-04-16(DTE=148) dir=BUY(prem) prem$=+103.31M spread✓組合單(標籤不採信)
- `[top_index]` 9000.00C exp=2027-04-16(DTE=148) dir=SELL(prem) prem$=-4.20M spread✓組合單(標籤不採信)
- `[top_index]` 8000.00C exp=2027-06-17(DTE=210) dir=BUY(prem) prem$=+30.09M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=7,344,253 |ΔsynthOI|=671,249 ΔOI=+415,777 flow_ratio= 10.94 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: 🟢 Short Put → bullish（prem 判向，集中度 70%，已分類 9,251 口）  [SG:9103.0]  [prem_conc=70%]
- **Structure**: 🟢 bull_put_spread  (sibling 6775P buy (78% main) → 賣高買低 put 信用價差)
- **資料品質**: ✅ bto/sto 欄與 prem=sell 一致
- **F8 sig 跨日**: ⚪ 跨日無極端 (1/10 報告 d 在 30~70)  d_seq=[67]

### ⬜ TSLA — (2 合約 / 4 榜次 ＋ 1 sym級)

- `[pkg #10930.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  ?120P/買500P（分類量 2,009/2,998）
  - ↳ 淨v$=+642.15K ⇒ 買方側淨**買** vega｜淨prem$=+52.15M
- `[top_vega]` 120.00P exp=2026-11-27(DTE=8) dir=?(none·勿判) v$=+0.00 spread✓組合單(標籤不採信)
- `[top_vega]` 500.00P exp=2028-12-15(DTE=757) dir=BUY(greek) v$=+642.15K spread✓組合單(標籤不採信)
- `[largest_premium]` 120.00P exp=2026-11-27(DTE=8) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[largest_premium]` 500.00P exp=2028-12-15(DTE=757) dir=BUY(greek) prem$=+52.15M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=1,092,826 |ΔsynthOI|=136,710 ΔOI=-50,443 flow_ratio=  7.99 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_pkg_other  (p3–p6 fallback（無 F7 解碼）｜spread_id=10930.0｜?120P/買500P｜跨 exp 2026-11-27/2028-12-15｜淨v$=+642.15K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ CG — (2 合約 / 4 榜次)

- `[pkg #1674.0]` 2 腿·RR/collar exp=2027-01-15  賣37.5P/買40C（分類量 63,998/53,015）
  - ↳ 淨d$=+189.24M ⇒ 買方側淨 delta **多**
- `[top_delta]` 37.50P exp=2027-01-15(DTE=57) dir=SELL(greek) d$=+106.64M spread✓組合單(標籤不採信)
- `[top_delta]` 40.00C exp=2027-01-15(DTE=57) dir=BUY(greek) d$=+82.60M spread✓組合單(標籤不採信)
- `[single_stocks]` 37.50P exp=2027-01-15(DTE=57) dir=SELL(greek) iv=39.8% bto/sto⚠未校驗·勿判向：STO=2 STC=63,996
- `[single_stocks]` 40.00C exp=2027-01-15(DTE=57) dir=BUY(greek) iv=43.6% bto/sto⚠未校驗·勿判向：BTO=15 BTC=53,000
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_risk_reversal  (p3–p6 fallback（無 F7 解碼）｜spread_id=1674.0｜買40C/賣37.5P｜exp=2027-01-15｜淨d$=+189.24M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ GDX — (1 合約 / 1 榜次 ＋ 1 sym級)

- `[sig_position]` d= 91th g= 83th v= 99th sector=Metals ETF
- `[asset_etfs]` 80.00C exp=2027-01-15(DTE=57) dir=BUY(sym·單列) iv=45.2% bto/sto⚠未校驗·勿判向：BTO=30,415 STO=471
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[100, 91]

### ⬜ GOOGL — (1 合約 / 2 榜次)　⚑ 單筆極端 prem#5

- `[top_vega]` 400.00P exp=2028-12-15(DTE=757) dir=SELL(greek) v$=-672.18K
- `[largest_premium]` 400.00P exp=2028-12-15(DTE=757) dir=SELL(greek) prem$=-62.11M
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ MU — (2 合約 / 2 榜次 ＋ 1 sym級)

- `[pkg #5448.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  ?1650C/賣700C（分類量 1,470/1,202）
  - ↳ 淨prem$=-29.65M ⇒ 買方側淨**收**權利金(貸記)
- `[largest_premium]` 1650.00C exp=2026-11-20(DTE=1 ⛔已到期) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[largest_premium]` 700.00C exp=2027-12-17(DTE=393) dir=SELL(prem) prem$=-29.65M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=910,121 |ΔsynthOI|=96,730 ΔOI=-27,187 flow_ratio=  9.41 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_pkg_other  (p3–p6 fallback（無 F7 解碼）｜spread_id=5448.0｜?1650C/賣700C｜跨 exp 2026-11-20/2027-12-17｜淨prem=-29.65M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 NVDA — (1 合約 / 1 榜次 ＋ 1 sym級)

- `[unusual]` 180.00P exp=2026-12-18(DTE=29) dir=BUY(prem) tot_prem=+17.24M → 🔴 Long Put → bearish（prem 判向，集中度 98%，已分類 5,071 口）
- `[heavy_daytrade]` vol=4,799,159 |ΔsynthOI|=116,637 ΔOI=-23,453,976 flow_ratio= 41.15 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: 🔴 Long Put → bearish（prem 判向，集中度 98%，已分類 5,071 口）  [prem_conc=98%]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（BTC）**為主 ⇒ 是回補既有空頭 put，**不是**新開空單；勿當 panic 讀（已分類量 5,071 口、平倉佔 100%）
- **Structure**: ⬜ unknown  (main side=buy type=P 非賣方側 put/call)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[82, 97]

### ⬜ SOFI — (1 合約 / 1 榜次 ＋ 1 sym級)

- `[sig_position]` d= 98th g=  3th v= 85th sector=Financial Services
- `[single_stocks]` 14.00P exp=2026-11-20(DTE=1 ⛔已到期) dir=SELL(sym·單列) iv=66.1% bto/sto⚠未校驗·勿判向：STO=131 STC=33,257
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[98]

### 🔴 SOXX — (3 合約 / 4 榜次)　⚑ p8 量級 p8prem#1

- `[pkg #8536.0]` 2 腿·P 垂直 exp=2026-12-18  賣130P/買140P（分類量 4,407/7,448）
  - ↳ 淨prem$=+6.15M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 150.00P exp=2026-12-18(DTE=29) dir=BUY(prem) symvol=172,114 tot_prem=+79.60M → 🔴 Long Put → bearish（prem 判向，集中度 24%，已分類 12,846 口）
- `[largest_premium]` 150.00P exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+49.22M
- `[largest_premium]` 140.00P exp=2026-12-18(DTE=29) dir=BUY(prem) prem$=+27.30M spread✓組合單(標籤不採信)
- `[largest_premium]` 130.00P exp=2026-12-18(DTE=29) dir=SELL(prem) prem$=-21.15M spread✓組合單(標籤不採信)
- **F7 unusual**: 🔴 Long Put → bearish（prem 判向，集中度 24%，已分類 12,846 口）  [prem_conc=24%]
  - ↳ 買 Put 流量：dealer 接下空單 → 賣股對沖，形成賣壓｜panic / conviction 型：主動新開空頭 — 持續性中等，留意反轉（已分類量 12,846 口、開倉佔 100%）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（F7 集中度不足）｜spread_id=8536.0｜賣130P/買140P｜exp=2026-12-18｜淨prem=+6.15M)
- **資料品質**: ✅ bto/sto 欄與 prem=buy 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

---

**摘要**：19 候選 / 0 教科書級

---

### 🏷️ F12 Cross-day IC / Strangle 賣方收斂結構（掃描 10 日）

#### 📌 SPX

- 雙側 STO：賣 8200C（3日）+ 賣 7520P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [7, 4, 0, 1, 0, 1, 5, 2, 0, 4]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤8200C + sell BuPS ≥7520P
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 NVDA

- 雙側 STO：賣 255C（5日）+ 賣 185P（3日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [4, 5, 20, 0, 13, 7, 1, 0, 5, 1]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤255C + sell BuPS ≥185P
- 現價 $128.71，在區間 [185~255] 的 -80th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 CCJ

- 雙側 STO：賣 115C（1日）+ 賣 55P（1日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [2, 0, 0, 0, 0, 0, 2, 0, 0, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤115C + sell BuPS ≥55P
- 現價 $58.50，在區間 [55~115] 的 6th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SPCX

- 雙側 STO：賣 160C（1日）+ 賣 115P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [6, 2, 0, 0, 0, 0, 5, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤160C + sell BuPS ≥115P
- 現價 $129.10，在區間 [115~160] 的 31th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 VIX

- 雙側 STO：賣 24C（2日）+ 賣 20P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [4, 2, 7, 0, 6]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤24C + sell BuPS ≥20P
- 現價 $35.88，在區間 [20~24] 的 397th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空
