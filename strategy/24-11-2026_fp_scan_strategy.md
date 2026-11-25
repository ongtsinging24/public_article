## 07:04:22 — `roma_cli fp_scan 2026-11-24`

<sub>`v7.44 (77711e94) | loaded 2026-11-24T11:25:58 | src ✅`</sub>

### 🎯 fp_scan 機會掃描（2026-11-24 🟡age=2td）

來源：flowpatrol_2026_11_24.pdf  
🟡 FP age=2td（偏舊）：資料截至 2026-11-23 收盤（此檔 publish=2026-11-24）、非 live tape；如需同日水位見 data_table  
模式：寬鬆 (cross≥2  extreme≤5  p8≤2)   候選 16 sym  
⚠️ R7 p8 排名池排除 1 sym（PREMIUM_IMPLAUSIBLE：名目金額非權利金）：AMD  
⚠️ prem 軸略過 1 列（PREMIUM_IMPLAUSIBLE：名目金額非權利金，不參與排名/R6）  

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

### 📐 本 session 組合結構（幾何候選 7 組）

- `[struct·強]` SPX 蝶式1:2:1 7290/7350/7400P exp=2026-12-18  （分類量 1,816/4,018/2,098）
  - ↳ 幾何偏差 16.7%（候選帶）｜等距 16.7%·量比 13.4%｜pkg 圖樣 FFF｜來源 top_index｜**無 spread_id**·僅本層看得到
- [econ·兩側皆可能] S=7237｜1,816 組｜long fly（買翼賣體） 付 $173K／最大賺 $8.9M（RR 4.5）｜short fly（買體賣翼） 收 $173K／最大賠 $8.9M
- `[struct·弱]` SPY 垂直價差 650/675P exp=2026-12-04  （分類量 89,256/89,759）
  - ↳ 幾何偏差 0.6%（高信心帶）｜pkg 圖樣 TT｜來源 index_etfs｜**無 spread_id**·僅本層看得到
- [econ·兩側皆可能] S=722｜89,256 組｜借方價差（買貴腳） 付 $10.7M／最大賺 $212.4M（RR 19.8）｜貸方價差（賣貴腳） 收 $10.7M／最大賠 $212.4M
- `[struct·弱]` SPY 垂直價差 570/675P exp=2026-11-30  （分類量 75,035/74,748）
  - ↳ 幾何偏差 0.4%（高信心帶）｜pkg 圖樣 TT｜來源 index_etfs｜**無 spread_id**·僅本層看得到
- [econ·傾向借方] S=722｜74,748 組｜借方價差（買貴腳） 付 $6.7M／最大賺 $778.1M（RR 115.8）｜貸方價差（賣貴腳） 收 $6.7M／最大賠 $778.1M
  - ↳ ⚠️ bto/sto 讀出來是**另一側**（卡 §2.3 的腿標記反號現象）
- `[struct·弱]` SPY 垂直價差 660/680P exp=2026-11-27  （分類量 67,030/66,542）
  - ↳ 幾何偏差 0.7%（高信心帶）｜pkg 圖樣 TT｜來源 index_etfs｜**無 spread_id**·僅本層看得到
- [econ·傾向借方] S=722｜66,542 組｜借方價差（買貴腳） 付 $2.7M／最大賺 $130.3M（RR 47.4）｜貸方價差（賣貴腳） 收 $2.7M／最大賠 $130.3M
  - ↳ ⚠️ bto/sto 讀出來是**另一側**（卡 §2.3 的腿標記反號現象）
- `[struct·弱]` PCG 垂直價差 18/23C exp=2027-03-19  （分類量 61,683/60,908）
  - ↳ 幾何偏差 1.3%（高信心帶）｜pkg 圖樣 TT｜來源 single_stocks｜**無 spread_id**·僅本層看得到
- `[struct·弱]` QQQ 垂直價差 450/550P exp=2027-01-15  （分類量 50,283/50,214）
  - ↳ 幾何偏差 0.1%（高信心帶）｜pkg 圖樣 TT｜來源 index_etfs｜**無 spread_id**·僅本層看得到
- `[struct·弱]` FXI 垂直價差 29/31P exp=2027-03-19  （分類量 44,570/44,559）
  - ↳ 幾何偏差 0.0%（高信心帶）｜pkg 圖樣 TT｜來源 asset_etfs｜**無 spread_id**·僅本層看得到

### 🔴 NVDA — (16 合約 / 66 榜次 ＋ 1 sym級)　⚑ 單筆極端 prem#2 d$#1 v$#2

- `[pkg #6455.0]` 2 腿·C 垂直 exp=2029-01-19  買150C/賣170C（分類量 10,358/10,584）
  - ↳ 淨v$=-48.27K ⇒ 買方側淨**賣** vega｜淨d$=+3.15M  淨prem$=+3.28M
- `[pkg #6522.0]` 2 腿·P 垂直 exp=2027-06-17  賣100P/買140P（分類量 20,227/20,463）
  - ↳ 淨v$=+286.10K ⇒ 買方側淨**買** vega｜淨prem$=+39.00M
- `[pkg #6698.0]` 2 腿·P 垂直 exp=2027-01-15  賣80P/買120P（分類量 150,122/99,109）
  - ↳ 淨v$=+1.01M ⇒ 買方側淨**買** vega｜淨d$=-201.87M  淨prem$=+54.08M
- `[pkg #6704.0]` 2 腿·RR/collar exp=2027-01-15  買130P/賣160C（分類量 73,426/56,244）
  - ↳ 淨v$=+0.00 ⇒ 買方側淨**買** vega｜淨d$=-808.58M  淨prem$=-90.70M
- `[pkg #6709.0]` 2 腿·C 垂直 exp=2027-02-19  買175C/賣200C（分類量 23,032/51,190）
  - ↳ 淨v$=-914.08K ⇒ 買方側淨**賣** vega｜淨d$=-173.97M  淨prem$=-44.64M
- `[pkg #6756.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買120P/賣80P（分類量 100,326/149,218）
  - ↳ 淨v$=+40.00K ⇒ 買方側淨**買** vega｜淨d$=-127.08M  淨prem$=+41.66M
- `[sig_position]` d=  0th g= 34th v=  2th sector=Technology
- `[unusual]` 160.00C exp=2027-01-15(DTE=53) dir=SELL(greek) tot_prem=+160.75M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 98%，已分類 56,244 口）  [SG:6704.0]
- `[unusual]` 130.00P exp=2027-01-15(DTE=53) dir=BUY(greek) tot_prem=+69.00M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 73,426 口）  [SG:6704.0]
- `[unusual]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) tot_prem=+131.77M → 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 82,366 口）
- `[unusual]` 200.00C exp=2027-02-19(DTE=88) dir=SELL(greek) tot_prem=+114.27M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 51,190 口）  [SG:6709.0]
- `[unusual]` 175.00C exp=2027-02-19(DTE=88) dir=BUY(greek) tot_prem=+69.35M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 23,032 口）  [SG:6709.0]
- `[unusual]` 120.00P exp=2027-02-19(DTE=88) dir=BUY(greek) tot_prem=+111.00M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（greek 判向，集中度 100%，已分類 100,326 口）  [SG:6756.0]
- `[unusual]` 80.00P exp=2027-04-16(DTE=144) dir=SELL(greek) tot_prem=+69.28M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 149,218 口）  [SG:6756.0]
- `[unusual]` 210.00C exp=2028-01-21(DTE=424) dir=SELL(greek) tot_prem=+109.91M → 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 18,081 口）
- `[unusual]` 150.00C exp=2029-01-19(DTE=788) dir=BUY(greek) tot_prem=+101.45M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 94%，已分類 10,358 口）  [SG:6455.0]
- `[unusual]` 170.00C exp=2029-01-19(DTE=788) dir=SELL(greek) tot_prem=+98.87M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 92%，已分類 10,584 口）  [SG:6455.0]
- `[unusual]` 140.00P exp=2027-06-17(DTE=206) dir=BUY(greek) tot_prem=+67.97M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 20,463 口）  [SG:6522.0]
- `[unusual]` 100.00P exp=2027-06-17(DTE=206) dir=SELL(greek) tot_prem=+29.08M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（greek 判向，集中度 95%，已分類 20,227 口）  [SG:6522.0]
- `[unusual]` 160.00C exp=2026-12-18(DTE=25) dir=SELL(greek) tot_prem=+67.41M → 🔴 Short Call → bearish（greek 判向，集中度 87%，已分類 32,882 口）
- `[unusual]` 120.00P exp=2027-01-15(DTE=53) dir=BUY(greek) tot_prem=+63.33M spread✓組合單(標籤不採信) → 🔴 Long Put → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 99,109 口）  [SG:6698.0]
- `[unusual]` 80.00P exp=2027-01-15(DTE=53) dir=SELL(greek) tot_prem=+8.61M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（greek 判向，集中度 100%，已分類 150,122 口）  [SG:6698.0]
- `[unusual]` 150.00C exp=2027-01-15(DTE=53) dir=SELL(prem) tot_prem=+46.84M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（prem 判向，集中度 21%，已分類 13,998 口）  [SG:6429.0]
- `[top_delta]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) d$=-701.61M
- `[top_delta]` 160.00C exp=2026-12-18(DTE=25) dir=SELL(greek) d$=-285.01M
- `[top_delta]` 160.00C exp=2027-01-15(DTE=53) dir=SELL(greek) d$=-557.01M spread✓組合單(標籤不採信)
- `[top_delta]` 130.00P exp=2027-01-15(DTE=53) dir=BUY(greek) d$=-251.57M spread✓組合單(標籤不採信)
- `[top_delta]` 120.00P exp=2027-01-15(DTE=53) dir=BUY(greek) d$=-252.90M spread✓組合單(標籤不採信)
- `[top_delta]` 80.00P exp=2027-01-15(DTE=53) dir=SELL(greek) d$=+51.03M spread✓組合單(標籤不採信)
- `[top_delta]` 200.00C exp=2027-02-19(DTE=88) dir=SELL(greek) d$=-388.20M spread✓組合單(標籤不採信)
- `[top_delta]` 175.00C exp=2027-02-19(DTE=88) dir=BUY(greek) d$=+214.23M spread✓組合單(標籤不採信)
- `[top_delta]` 120.00P exp=2027-02-19(DTE=88) dir=BUY(greek) d$=-305.67M spread✓組合單(標籤不採信)
- `[top_delta]` 80.00P exp=2027-04-16(DTE=144) dir=SELL(greek) d$=+178.59M spread✓組合單(標籤不採信)
- `[top_delta]` 210.00C exp=2028-01-21(DTE=424) dir=SELL(greek) d$=-193.82M
- `[top_delta]` 150.00C exp=2029-01-19(DTE=788) dir=BUY(greek) d$=+129.70M spread✓組合單(標籤不採信)
- `[top_delta]` 170.00C exp=2029-01-19(DTE=788) dir=SELL(greek) d$=-126.55M spread✓組合單(標籤不採信)
- `[top_gamma]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) g$=-19.93M
- `[top_vega]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) v$=-1.42M
- `[top_vega]` 120.00P exp=2027-01-15(DTE=53) dir=BUY(greek) v$=+1.48M spread✓組合單(標籤不採信)
- `[top_vega]` 80.00P exp=2027-01-15(DTE=53) dir=SELL(greek) v$=-468.52K spread✓組合單(標籤不採信)
- `[top_vega]` 130.00P exp=2027-01-15(DTE=53) dir=BUY(greek) v$=+1.32M spread✓組合單(標籤不採信)
- `[top_vega]` 160.00C exp=2027-01-15(DTE=53) dir=SELL(greek) v$=-1.32M spread✓組合單(標籤不採信)
- `[top_vega]` 120.00P exp=2027-02-19(DTE=88) dir=BUY(greek) v$=+2.17M spread✓組合單(標籤不採信)
- `[top_vega]` 200.00C exp=2027-02-19(DTE=88) dir=SELL(greek) v$=-1.65M spread✓組合單(標籤不採信)
- `[top_vega]` 175.00C exp=2027-02-19(DTE=88) dir=BUY(greek) v$=+735.92K spread✓組合單(標籤不採信)
- `[top_vega]` 80.00P exp=2027-04-16(DTE=144) dir=SELL(greek) v$=-2.13M spread✓組合單(標籤不採信)
- `[top_vega]` 140.00P exp=2027-06-17(DTE=206) dir=BUY(greek) v$=+831.94K spread✓組合單(標籤不採信)
- `[top_vega]` 100.00P exp=2027-06-17(DTE=206) dir=SELL(greek) v$=-545.84K spread✓組合單(標籤不採信)
- `[top_vega]` 210.00C exp=2028-01-21(DTE=424) dir=SELL(greek) v$=-1.19M
- `[top_vega]` 170.00C exp=2029-01-19(DTE=788) dir=SELL(greek) v$=-687.77K spread✓組合單(標籤不採信)
- `[top_vega]` 150.00C exp=2029-01-19(DTE=788) dir=BUY(greek) v$=+639.50K spread✓組合單(標籤不採信)
- `[largest_premium]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) prem$=-129.68M
- `[largest_premium]` 160.00C exp=2026-12-18(DTE=25) dir=SELL(greek) prem$=-63.02M
- `[largest_premium]` 160.00C exp=2027-01-15(DTE=53) dir=SELL(greek) prem$=-158.77M spread✓組合單(標籤不採信)
- `[largest_premium]` 130.00P exp=2027-01-15(DTE=53) dir=BUY(greek) prem$=+68.07M spread✓組合單(標籤不採信)
- `[largest_premium]` 120.00P exp=2027-01-15(DTE=53) dir=BUY(greek) prem$=+62.68M spread✓組合單(標籤不採信)
- `[largest_premium]` 80.00P exp=2027-01-15(DTE=53) dir=SELL(greek) prem$=-8.60M spread✓組合單(標籤不採信)
- `[largest_premium]` 200.00C exp=2027-02-19(DTE=88) dir=SELL(greek) prem$=-111.58M spread✓組合單(標籤不採信)
- `[largest_premium]` 175.00C exp=2027-02-19(DTE=88) dir=BUY(greek) prem$=+66.94M spread✓組合單(標籤不採信)
- `[largest_premium]` 120.00P exp=2027-02-19(DTE=88) dir=BUY(greek) prem$=+110.93M spread✓組合單(標籤不採信)
- `[largest_premium]` 80.00P exp=2027-04-16(DTE=144) dir=SELL(greek) prem$=-69.27M spread✓組合單(標籤不採信)
- `[largest_premium]` 140.00P exp=2027-06-17(DTE=206) dir=BUY(greek) prem$=+67.42M spread✓組合單(標籤不採信)
- `[largest_premium]` 100.00P exp=2027-06-17(DTE=206) dir=SELL(greek) prem$=-28.42M spread✓組合單(標籤不採信)
- `[largest_premium]` 210.00C exp=2028-01-21(DTE=424) dir=SELL(greek) prem$=-75.85M
- `[largest_premium]` 150.00C exp=2029-01-19(DTE=788) dir=BUY(greek) prem$=+98.21M spread✓組合單(標籤不採信)
- `[largest_premium]` 170.00C exp=2029-01-19(DTE=788) dir=SELL(greek) prem$=-94.93M spread✓組合單(標籤不採信)
- `[single_stocks]` 170.00C exp=2026-12-18(DTE=25) dir=SELL(greek) iv=64.2% bto/sto⚠未校驗·勿判向：STO=1,308 STC=81,058
- `[single_stocks]` 80.00P exp=2027-01-15(DTE=53) dir=SELL(greek) iv=96.0% bto/sto⚠未校驗·勿判向：BTC=230 STC=149,892
- `[single_stocks]` 120.00P exp=2027-01-15(DTE=53) dir=BUY(greek) iv=69.6% bto/sto⚠未校驗·勿判向：BTO=98,087 BTC=1,022
- `[single_stocks]` 130.00P exp=2027-01-15(DTE=53) dir=BUY(greek) iv=64.9% bto/sto⚠未校驗·勿判向：BTO=72,435 BTC=991
- `[single_stocks]` 160.00C exp=2027-01-15(DTE=53) dir=SELL(greek) iv=59.3% bto/sto⚠未校驗·勿判向：BTC=691 STC=55,553
- `[single_stocks]` 120.00P exp=2027-02-19(DTE=88) dir=BUY(greek) iv=61.6% bto/sto⚠未校驗·勿判向：BTO=100,265 STO=61
- `[single_stocks]` 80.00P exp=2027-04-16(DTE=144) dir=SELL(greek) iv=69.7% bto/sto⚠未校驗·勿判向：STO=29 STC=149,189
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 98%，已分類 56,244 口）  [SG:6704.0]  [prem_conc=98%]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（STC）**為主 ⇒ 是了結既有多頭 call，**不是**新開空頭／派發；勿當 distribution 讀（已分類量 56,244 口、平倉佔 100%）
- **Structure**: 🔴 short_call_flow  (4 sibling 但規模均 < 50% main)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: 🟡 雙極切換 (2/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[97, 0]

### 🔴 AMD — (2 合約 / 8 榜次 ＋ 1 sym級)

- `[pkg #416.0]` 2 腿·C 垂直 exp=2027-02-19  賣640C/買870C（分類量 9,473/9,507）
  - ↳ 淨v$=-203.65K ⇒ 買方側淨**賣** vega｜淨d$=-77.09M  淨prem$=-27.61M
- `[unusual]` 640.00C exp=2027-02-19(DTE=88) dir=SELL(greek) symvol=859,951 tot_prem=+50.27M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,473 口）  [SG:416.0]
- `[unusual]` 870.00C exp=2027-02-19(DTE=88) dir=BUY(greek) symvol=859,951 tot_prem=+22.59M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,507 口）  [SG:416.0]
- `[top_delta]` 640.00C exp=2027-02-19(DTE=88) dir=SELL(greek) d$=-166.12M spread✓組合單(標籤不採信)
- `[top_delta]` 870.00C exp=2027-02-19(DTE=88) dir=BUY(greek) d$=+89.03M spread✓組合單(標籤不採信)
- `[top_vega]` 640.00C exp=2027-02-19(DTE=88) dir=SELL(greek) v$=-807.99K spread✓組合單(標籤不採信)
- `[top_vega]` 870.00C exp=2027-02-19(DTE=88) dir=BUY(greek) v$=+604.35K spread✓組合單(標籤不採信)
- `[largest_premium]` 640.00C exp=2027-02-19(DTE=88) dir=SELL(greek) prem$=-50.19M spread✓組合單(標籤不採信)
- `[largest_premium]` 870.00C exp=2027-02-19(DTE=88) dir=BUY(greek) prem$=+22.58M⚠名目? spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=859,951 |ΔsynthOI|=132,774 ΔOI=-386,145 flow_ratio=  6.48 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 9,473 口）  [SG:416.0]  [prem_conc=n/a]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（STC）**為主 ⇒ 是了結既有多頭 call，**不是**新開空頭／派發；勿當 distribution 讀（已分類量 9,473 口、平倉佔 100%）
- **Structure**: 🔴 short_call_flow  (1 sibling 但規模均 < 50% main)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🔴 TSM — (2 合約 / 10 榜次)　⚑ 單筆極端 prem#4 d$#2 g$#4 v$#1

- `[pkg #12184.0]` 2 腿·C 垂直 exp=2027-01-15  賣360C/買420C（分類量 28,386/51,264）
  - ↳ 淨g$=+10.38M ⇒ 買方側淨**買** gamma｜淨v$=+1.12M  淨d$=+83.02M  淨prem$=-9.95M
- `[unusual]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) symvol=156,165 tot_prem=+123.38M spread✓組合單(標籤不採信) → 🔴 Short Call → bearish（greek 判向，集中度 100%，已分類 28,386 口）  [SG:12184.0]
- `[unusual]` 420.00C exp=2027-01-15(DTE=53) dir=BUY(greek) symvol=156,165 tot_prem=+113.44M spread✓組合單(標籤不採信) → 🟢 Long Call → bullish（greek 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 51,264 口）  [SG:12184.0]
- `[top_delta]` 420.00C exp=2027-01-15(DTE=53) dir=BUY(greek) d$=+677.23M spread✓組合單(標籤不採信)
- `[top_delta]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) d$=-594.21M spread✓組合單(標籤不採信)
- `[top_gamma]` 420.00C exp=2027-01-15(DTE=53) dir=BUY(greek) g$=+24.56M spread✓組合單(標籤不採信)
- `[top_gamma]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) g$=-14.18M spread✓組合單(標籤不採信)
- `[top_vega]` 420.00C exp=2027-01-15(DTE=53) dir=BUY(greek) v$=+2.66M spread✓組合單(標籤不採信)
- `[top_vega]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) v$=-1.54M spread✓組合單(標籤不採信)
- `[largest_premium]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) prem$=-123.35M spread✓組合單(標籤不採信)
- `[largest_premium]` 420.00C exp=2027-01-15(DTE=53) dir=BUY(greek) prem$=+113.40M spread✓組合單(標籤不採信)
- **F7 unusual**: 🔴 Short Call → bearish（greek 判向，集中度 100%，已分類 28,386 口）  [SG:12184.0]  [prem_conc=100%]
  - ↳ 賣 Call 流量：dealer 接下多單 → 賣股對沖，形成賣壓｜🔴 已分類量以**平倉（STC）**為主 ⇒ 是了結既有多頭 call，**不是**新開空頭／派發；勿當 distribution 讀（已分類量 28,386 口、平倉佔 100%）
- **Structure**: 🔴 bear_call_spread  (sibling 420C buy (92% main) → 賣低買高 call 信用價差)
- **資料品質**: ✅ bto/sto 欄與 greek=sell 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ AAPL — (1 合約 / 3 榜次 ＋ 1 sym級)　⚑ 單筆極端 g$#5

- `[top_delta]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) d$=-216.68M
- `[top_gamma]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) g$=-21.88M
- `[top_vega]` 360.00C exp=2027-01-15(DTE=53) dir=SELL(greek) v$=-775.00K
- `[heavy_daytrade]` vol=1,158,535 |ΔsynthOI|=163,730 ΔOI=-568,938 flow_ratio=  7.08 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ SPY — (13 合約 / 13 榜次 ＋ 2 sym級)

- `[pkg #10871.0]` 2 腿·P 垂直 exp=2026-12-11  賣675P/買700P（分類量 33,318/34,315）
  - ↳ 淨prem$=+16.77M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #11193.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣730C/賣610P（分類量 26,108/36,009）
  - ↳ 淨prem$=-18.68M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #11244.0]` 2 腿·C 垂直 exp=2026-11-27  買710C/賣715C（分類量 8,075/19,223）
  - ↳ 淨prem$=-10.46M ⇒ 買方側淨**收**權利金(貸記)
- `[sig_position]` d=  4th g=  7th v= 15th sector=Equity ETF
- `[top_index]` 730.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=SELL(prem) prem$=-11.18M spread✓組合單(標籤不採信)
- `[top_index]` 715.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=SELL(prem) prem$=-20.45M spread✓組合單(標籤不採信)
- `[top_index]` 710.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=BUY(prem) prem$=+9.99M spread✓組合單(標籤不採信)
- `[top_index]` 700.00P exp=2026-12-11(DTE=18) dir=BUY(prem) prem$=+24.41M spread✓組合單(標籤不採信)
- `[top_index]` 675.00P exp=2026-12-11(DTE=18) dir=SELL(prem) prem$=-7.64M spread✓組合單(標籤不採信)
- `[top_index]` 610.00P exp=2027-02-19(DTE=88) dir=SELL(prem) prem$=-7.50M spread✓組合單(標籤不採信)
- `[index_etfs]` 660.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=?(none·勿判) iv=44.7% bto/sto⚠未校驗·勿判向：BTO=196 BTC=66,834
- `[index_etfs]` 680.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=?(none·勿判) iv=37.6% bto/sto⚠未校驗·勿判向：BTC=242 STC=66,300
- `[index_etfs]` 570.00P exp=2026-11-30(DTE=7) dir=?(none·勿判) iv=65.7% bto/sto⚠未校驗·勿判向：BTO=38 BTC=74,997
- `[index_etfs]` 675.00P exp=2026-11-30(DTE=7) dir=?(none·勿判) iv=33.2% bto/sto⚠未校驗·勿判向：BTC=353 STC=74,395
- `[index_etfs]` 650.00P exp=2026-12-04(DTE=11) dir=?(none·勿判) iv=39.2% bto/sto⚠未校驗·勿判向：BTC=88,736 STC=520
- `[index_etfs]` 675.00P exp=2026-12-04(DTE=11) dir=?(none·勿判) iv=33.5% bto/sto⚠未校驗·勿判向：BTC=22 STC=89,737
- `[index_etfs]` 550.00P exp=2027-01-15(DTE=53) dir=?(none·勿判) iv=42.1% bto/sto⚠未校驗·勿判向：BTO=3 STO=61,912
- `[heavy_daytrade]` vol=13,640,545 |ΔsynthOI|=1,607,787 ΔOI=-2,754,837 flow_ratio=  8.48 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=10871.0｜賣675P/買700P｜exp=2026-12-11｜淨prem=+16.77M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: 🟡 雙極切換 (7/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[7, 19, 70, 97, 99, 51, 4]

### ⬜ IWM — (8 合約 / 10 榜次 ＋ 1 sym級)　⚑ 單筆極端 g$#1

- `[pkg #4352.0]` 2 腿·P 垂直 exp=2026-11-25  買240P/賣261P（分類量 6,058/5,723）
  - ↳ 淨g$=-19.88M ⇒ 買方側淨**賣** gamma
- `[pkg #4386.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買263P/買300C（分類量 3,575/4,030）
  - ↳ 淨g$=+18.04M ⇒ 買方側淨**買** gamma
- `[pkg #4398.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣266C/賣250P（分類量 2,488/2,633）
  - ↳ 淨g$=-17.45M ⇒ 買方側淨**賣** gamma
- `[pkg #4412.0]` 2 腿·P 垂直 exp=2026-12-18  賣245P/買252P（分類量 27,122/33,374）
  - ↳ 淨g$=+22.94M ⇒ 買方側淨**買** gamma｜淨d$=-129.71M
- `[top_delta]` 252.00P exp=2026-12-18(DTE=25) dir=BUY(greek) d$=-182.90M spread✓組合單(標籤不採信)
- `[top_delta]` 245.00P exp=2026-12-18(DTE=25) dir=SELL(greek) d$=+53.19M spread✓組合單(標籤不採信)
- `[top_gamma]` 266.00C exp=2026-11-24(DTE=1 ⛔已到期) dir=SELL(greek) g$=-15.05M spread✓組合單(標籤不採信)
- `[top_gamma]` 261.00P exp=2026-11-25(DTE=2 ⚠️短天期) dir=SELL(greek) g$=-19.88M spread✓組合單(標籤不採信)
- `[top_gamma]` 240.00P exp=2026-11-25(DTE=2 ⚠️短天期) dir=BUY(greek·微量) g$=+68.47 spread✓組合單(標籤不採信)
- `[top_gamma]` 263.00P exp=2026-11-25(DTE=2 ⚠️短天期) dir=BUY(greek) g$=+16.13M spread✓組合單(標籤不採信)
- `[top_gamma]` 250.00P exp=2026-12-04(DTE=11) dir=SELL(greek) g$=-2.40M spread✓組合單(標籤不採信)
- `[top_gamma]` 252.00P exp=2026-12-18(DTE=25) dir=BUY(greek) g$=+35.74M spread✓組合單(標籤不採信)
- `[top_gamma]` 245.00P exp=2026-12-18(DTE=25) dir=SELL(greek) g$=-12.80M spread✓組合單(標籤不採信)
- `[top_gamma]` 300.00C exp=2027-01-15(DTE=53) dir=BUY(greek) g$=+1.91M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=1,785,498 |ΔsynthOI|=202,108 ΔOI=-725,063 flow_ratio=  8.83 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=4412.0｜賣245P/買252P｜exp=2026-12-18｜淨g$=+22.94M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: 🟡 雙極切換 (4/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[6, 92, 93, 100]

### 🟢 SPX — (29 合約 / 31 榜次 ＋ 1 sym級)

- `[pkg #10272.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7350P/賣6750P（分類量 4,018/3,486）
  - ↳ 淨prem$=+56.23M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10361.0]` 2 腿·P 垂直 exp=2026-12-04  賣6925P/買6950P（分類量 7,996/8,159）
  - ↳ 淨prem$=+3.07M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10369.0]` 2 腿·P 垂直 exp=2026-11-24  買6975P/賣7700P（分類量 1,261/1,128）
  - ↳ 淨prem$=-51.65M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #10444.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7250C/賣7700C（分類量 1,762/1,683）
  - ↳ 淨prem$=+6.04M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10477.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7200C/買8200C（分類量 2,812/2,258）
  - ↳ 淨prem$=+41.20M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10569.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣7300C/賣7010P（分類量 3,442/2,408）
  - ↳ 淨prem$=-32.04M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #10585.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買8050C/買6775P（分類量 4,549/4,461）
  - ↳ 淨prem$=+61.06M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10587.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買7650C/買7060P（分類量 5,458/4,799）
  - ↳ 淨prem$=+56.16M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10606.0]` 2 腿·C+P 跨履約 exp=2026-11-27  ?4600P/買7250C（分類量 1,843/2,626）
  - ↳ 淨prem$=+17.00M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10614.0]` 2 腿·P 垂直 exp=2026-12-18  賣6000P/買6900P（分類量 1,108/5,424）
  - ↳ 淨prem$=+22.76M ⇒ 買方側淨**付**權利金(借記)
- `[pkg #10615.0]` 2 腿·RR/collar exp=2026-12-18  賣7300P/買7900C（分類量 4,436/4,819）
  - ↳ 淨prem$=-72.02M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #10623.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買6650P/賣6850P（分類量 4,874/6,541）
  - ↳ 淨prem$=-79.27M ⇒ 買方側淨**收**權利金(貸記)
- `[pkg #9903.0]` 2 腿·C 垂直 exp=2027-02-26  買8500C/賣8700C（分類量 6,001/6,002）
  - ↳ 淨prem$=+12.25M ⇒ 買方側淨**付**權利金(借記)
- `[unusual]` 6850.00P exp=2027-01-15(DTE=53) dir=SELL(prem) tot_prem=+80.19M spread✓組合單(標籤不採信) → 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 6,541 口）  [SG:10623.0]
- `[unusual]` 7000.00P exp=2026-12-18(DTE=25) dir=SELL(prem) tot_prem=+68.94M → 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 7,128 口）
- `[top_index]` 6650.00P exp=2026-11-24(DTE=1 ⛔已到期) dir=BUY(prem·微量) prem$=+0.01 spread✓組合單(標籤不採信)
- `[top_index]` 7650.00C exp=2026-11-24(DTE=1 ⛔已到期) dir=BUY(prem·微量) prem$=+464.71 spread✓組合單(標籤不採信)
- `[top_index]` 7700.00P exp=2026-11-24(DTE=1 ⛔已到期) dir=SELL(prem) prem$=-51.66M spread✓組合單(標籤不採信)
- `[top_index]` 6975.00P exp=2026-11-24(DTE=1 ⛔已到期) dir=BUY(prem) prem$=+14.42K spread✓組合單(標籤不採信)
- `[top_index]` 7300.00C exp=2026-11-25(DTE=2 ⚠️短天期) dir=SELL(prem) prem$=-7.99M spread✓組合單(標籤不採信)
- `[top_index]` 7200.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=SELL(prem) prem$=-24.43M spread✓組合單(標籤不採信)
- `[top_index]` 7250.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=BUY(prem) prem$=+17.00M spread✓組合單(標籤不採信)
- `[top_index]` 4600.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=?(none·勿判) prem$=+0.00 spread✓組合單(標籤不採信)
- `[top_index]` 7250.00C exp=2026-11-30(DTE=7) dir=BUY(prem) prem$=+14.33M spread✓組合單(標籤不採信)
- `[top_index]` 6950.00P exp=2026-12-04(DTE=11) dir=BUY(prem) prem$=+25.99M spread✓組合單(標籤不採信)
- `[top_index]` 6925.00P exp=2026-12-04(DTE=11) dir=SELL(prem) prem$=-22.92M spread✓組合單(標籤不採信)
- `[top_index]` 7000.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-66.09M
- `[top_index]` 7350.00P exp=2026-12-18(DTE=25) dir=BUY(prem) prem$=+89.45M spread✓組合單(標籤不採信)
- `[top_index]` 7060.00P exp=2026-12-18(DTE=25) dir=BUY(prem) prem$=+56.16M spread✓組合單(標籤不採信)
- `[top_index]` 7300.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-83.52M spread✓組合單(標籤不採信)
- `[top_index]` 7900.00C exp=2026-12-18(DTE=25) dir=BUY(prem) prem$=+11.50M spread✓組合單(標籤不採信)
- `[top_index]` 7010.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-24.05M spread✓組合單(標籤不採信)
- `[top_index]` 6900.00P exp=2026-12-18(DTE=25) dir=BUY(prem) prem$=+22.81M spread✓組合單(標籤不採信)
- `[top_index]` 6000.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-46.64K spread✓組合單(標籤不採信)
- `[top_index]` 7400.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-55.82M
- `[top_index]` 7700.00C exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-8.29M spread✓組合單(標籤不採信)
- `[top_index]` 7290.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-39.86M
- `[top_index]` 8050.00C exp=2026-12-31(DTE=38) dir=BUY(prem) prem$=+15.62M spread✓組合單(標籤不採信)
- `[top_index]` 6850.00P exp=2027-01-15(DTE=53) dir=SELL(prem) prem$=-79.27M spread✓組合單(標籤不採信)
- `[top_index]` 6750.00P exp=2027-01-15(DTE=53) dir=SELL(prem) prem$=-33.22M spread✓組合單(標籤不採信)
- `[top_index]` 6775.00P exp=2027-01-15(DTE=53) dir=BUY(prem) prem$=+45.44M spread✓組合單(標籤不採信)
- `[top_index]` 8500.00C exp=2027-02-26(DTE=95) dir=BUY(prem) prem$=+42.69M spread✓組合單(標籤不採信)
- `[top_index]` 8700.00C exp=2027-02-26(DTE=95) dir=SELL(prem) prem$=-30.44M spread✓組合單(標籤不採信)
- `[top_index]` 8200.00C exp=2027-06-17(DTE=206) dir=BUY(prem) prem$=+65.63M spread✓組合單(標籤不採信)
- `[heavy_daytrade]` vol=5,794,608 |ΔsynthOI|=668,082 ΔOI=-1,760,046 flow_ratio=  8.67 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: 🟢 Short Put → bullish（prem 判向，集中度 n/a（buy/sell prem 異號→恆等 100%，不可測），已分類 6,541 口）  [SG:10623.0]  [prem_conc=n/a]
- **Structure**: 🟢 short_put_flow  (同 expiry 無其他 unusual leg)
- **資料品質**: ✅ bto/sto 欄與 prem=sell 一致
- **F8 sig 跨日**: ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[67, 16]

### ⬜ TLT — (7 合約 / 13 榜次)　⚑ 單筆極端 g$#2

- `[pkg #11609.0]` 4 腿·多腿(4) exp=2027-01-15  賣78P/買79P/買80C/賣83C（分類量 50,344/62,783/5,187/498）
  - ↳ 淨g$=+15.02M ⇒ 買方側淨**買** gamma
- `[pkg #11616.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  買82.5C/賣80C（分類量 17,376/20,029）
  - ↳ 淨g$=+18.05M ⇒ 買方側淨**買** gamma｜淨d$=-128.83M
- `[top_delta]` 82.50C exp=2026-11-25(DTE=2 ⚠️短天期) dir=BUY(greek) d$=+19.13M spread✓組合單(標籤不採信)
- `[top_delta]` 80.00C exp=2026-11-30(DTE=7) dir=SELL(greek) d$=-147.96M spread✓組合單(標籤不採信)
- `[top_gamma]` 82.50C exp=2026-11-25(DTE=2 ⚠️短天期) dir=BUY(greek) g$=+34.57M spread✓組合單(標籤不採信)
- `[top_gamma]` 80.00C exp=2026-11-30(DTE=7) dir=SELL(greek) g$=-16.52M spread✓組合單(標籤不採信)
- `[top_gamma]` 79.00P exp=2027-01-15(DTE=53) dir=BUY(greek) g$=+30.67M spread✓組合單(標籤不採信)
- `[top_gamma]` 78.00P exp=2027-01-15(DTE=53) dir=SELL(greek) g$=-18.11M spread✓組合單(標籤不採信)
- `[top_gamma]` 80.00C exp=2027-01-15(DTE=53) dir=BUY(greek) g$=+2.48M spread✓組合單(標籤不採信)
- `[top_gamma]` 83.00C exp=2027-01-15(DTE=53) dir=SELL(greek) g$=-16.84K spread✓組合單(標籤不採信)
- `[asset_etfs]` 82.50C exp=2026-11-25(DTE=2 ⚠️短天期) dir=BUY(greek) iv=13.6% bto/sto⚠未校驗·勿判向：BTO=17,120 STO=256
- `[asset_etfs]` 80.00C exp=2026-11-30(DTE=7) dir=SELL(greek) iv=14.1% bto/sto⚠未校驗·勿判向：BTC=25 STC=20,004
- `[asset_etfs]` 87.00C exp=2026-12-18(DTE=25) dir=?(none·勿判) iv=15.0% bto/sto⚠未校驗·勿判向：BTC=18,712 STC=14
- `[asset_etfs]` 78.00P exp=2027-01-15(DTE=53) dir=SELL(greek) iv=12.2% bto/sto⚠未校驗·勿判向：BTC=616 STC=49,728
- `[asset_etfs]` 79.00P exp=2027-01-15(DTE=53) dir=BUY(greek) iv=11.9% bto/sto⚠未校驗·勿判向：BTO=62,675 STO=108
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_roll_or_calendar  (p3–p6 fallback（無 F7 解碼）｜spread_id=11616.0｜買82.5C/賣80C｜跨 exp 2026-11-25/2026-11-30｜淨g$=+18.05M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (4/10 報告，未過半)，雜訊概率高  d_seq=[86, 50, 95, 61]

### ⬜ AMZN — (2 合約 / 2 榜次 ＋ 1 sym級)

- `[pkg #704.0]` 2 腿·C 垂直 exp=2027-12-17  買275C/賣350C（分類量 4,986/12,035）
  - ↳ 淨v$=-640.51K ⇒ 買方側淨**賣** vega
- `[sig_position]` d= 15th g= 23th v=  0th sector=Consumer Cyclical
- `[top_vega]` 350.00C exp=2027-12-17(DTE=389) dir=SELL(greek) v$=-1.16M spread✓組合單(標籤不採信)
- `[top_vega]` 275.00C exp=2027-12-17(DTE=389) dir=BUY(greek) v$=+519.49K spread✓組合單(標籤不採信)
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_vertical  (p3–p6 fallback（無 F7 解碼）｜spread_id=704.0｜買275C/賣350C｜exp=2027-12-17｜淨v$=-640.51K)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[15]

### ⬜ HYG — (2 合約 / 2 榜次)

- `[top_gamma]` 76.50P exp=2026-11-27(DTE=4 ⚠️短天期) dir=BUY(greek) g$=+16.77M
- `[asset_etfs]` 73.00P exp=2027-01-15(DTE=53) dir=?(none·勿判) iv=10.4% bto/sto⚠未校驗·勿判向：STO=2,994 STC=19,702
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[17]

### ⬜ KWEB — (2 合約 / 2 榜次 ＋ 1 sym級)

- `[sig_position]` d= 13th g=  2th v= 27th sector=Chinese Equity ETF
- `[asset_etfs]` 21.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=?(none·勿判) iv=37.8% bto/sto⚠未校驗·勿判向：BTC=341 STC=24,997
- `[asset_etfs]` 21.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=?(none·勿判) iv=43.0% bto/sto⚠未校驗·勿判向：BTC=14 STC=24,562
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[13]

### ⬜ QQQ — (2 合約 / 2 榜次 ＋ 1 sym級)

- `[index_etfs]` 450.00P exp=2027-01-15(DTE=53) dir=?(none·勿判) iv=53.5% bto/sto⚠未校驗·勿判向：STO=149 STC=50,134
- `[index_etfs]` 550.00P exp=2027-01-15(DTE=53) dir=?(none·勿判) iv=39.9% bto/sto⚠未校驗·勿判向：BTC=50,190 STC=24
- `[heavy_daytrade]` vol=8,896,441 |ΔsynthOI|=846,947 ΔOI=-1,101,524 flow_ratio= 10.50 🔴 HFT 主導，gamma/regime 訊號需大幅折扣
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### 🟢 SNDK — (3 合約 / 4 榜次)　⚑ 單筆極端 prem#1

- `[pkg #9122.0]` 2 腿·跨期(roll/diagonal) exp=多exp(2)  賣100C/賣187.5P（分類量 3,446/3,643）
  - ↳ 淨prem$=-66.53M ⇒ 買方側淨**收**權利金(貸記)
- `[unusual]` 75.00P exp=2026-12-18(DTE=25) dir=SELL(prem) symvol=388,553 tot_prem=+195.72M → 🟢 Short Put → bullish（prem 判向，集中度 97%，已分類 45,637 口）
- `[largest_premium]` 100.00C exp=2026-11-27(DTE=4 ⚠️短天期) dir=SELL(prem) prem$=-6.81M spread✓組合單(標籤不採信)
- `[largest_premium]` 75.00P exp=2026-12-18(DTE=25) dir=SELL(prem) prem$=-192.61M
- `[largest_premium]` 187.50P exp=2027-06-17(DTE=206) dir=SELL(prem) prem$=-59.72M spread✓組合單(標籤不採信)
- **F7 unusual**: 🟢 Short Put → bullish（prem 判向，集中度 97%，已分類 45,637 口）  [prem_conc=97%]
- **Structure**: 🟢 short_put_flow  (同 expiry 無其他 unusual leg)
- **資料品質**: ✅ bto/sto 欄與 prem=sell 一致
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ TSLA — (1 合約 / 1 榜次 ＋ 1 sym級)

- `[top_vega]` 290.00P exp=2027-06-17(DTE=206) dir=SELL(greek) v$=-793.24K
- `[heavy_daytrade]` vol=1,919,333 |ΔsynthOI|=214,361 ΔOI=-676,678 flow_ratio=  8.95 🟡 HFT-heavy，dealer 反應可能被噪音蓋過
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: —（聚合無紀錄或 sig_position 未上榜過）

### ⬜ VIX — (1 合約 / 1 榜次 ＋ 1 sym級)

- `[sig_position]` d= 20th g= 15th v=  6th sector=Volatility ETF
- `[index_etfs]` 26.00C exp=2026-12-16(DTE=23) dir=SELL(sym·單列) iv=128.6% bto/sto⚠未校驗·勿判向：STO=21 STC=58,688
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: ⬜ unknown  (無 F7 解碼)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (4/10 報告，未過半)，雜訊概率高  d_seq=[65, 53, 5, 20]

### ⬜ XSP — (2 合約 / 3 榜次)

- `[top_delta]` 745.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=BUY(greek) d$=-213.30M
- `[top_gamma]` 745.00P exp=2026-11-27(DTE=4 ⚠️短天期) dir=BUY(greek) g$=+21.70M
- `[top_gamma]` 695.00P exp=2026-12-31(DTE=38) dir=SELL(greek) g$=-11.55M
- **F7 unusual**: —（無 unusual 段命中或無 trade-side 資料）
- **Structure**: 🔷 p36_roll_or_calendar  (p3–p6 fallback（無 F7 解碼）｜同 sym 僅此 2 腿｜買745P/賣695P｜跨 exp 2026-11-27/2026-12-31｜淨g$=+10.15M)
- **資料品質**: — 無 F7 解碼
- **F8 sig 跨日**: ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[1]

---

**摘要**：16 候選 / 0 教科書級

---

### 🏷️ F12 Cross-day IC / Strangle 賣方收斂結構（掃描 10 日）

#### 📌 NVDA

- 雙側 STO：賣 150C（5日）+ 賣 90P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [20, 0, 13, 7, 1, 0, 5, 1, 1, 16]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤150C + sell BuPS ≥90P
- 現價 $152.99，在區間 [90~150] 的 105th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SPCX

- 雙側 STO：賣 160C（1日）+ 賣 115P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [6, 2, 0, 0, 0, 0, 5, 0, 0, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤160C + sell BuPS ≥115P
- 現價 $126.52，在區間 [115~160] 的 26th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 VIX

- 雙側 STO：賣 24C（2日）+ 賣 20P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [4, 2, 7, 0, 6, 4, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤24C + sell BuPS ≥20P
- 現價 $26.35，在區間 [20~24] 的 159th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SPX

- 雙側 STO：賣 7650C（1日）+ 賣 6800P（2日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：🔄 仍在建  仍在榜（counts: [1, 0, 1, 5, 2, 0, 4, 6, 2]）→ 建倉可能仍在進行
- 建議 IC：sell BeCS ≤7650C + sell BuPS ≥6800P
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

#### 📌 SOXX

- 雙側 STO：賣 180C（1日）+ 賣 150P（1日）（prem 資料缺失，無法確認賣方收 prem）
- G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [3, 0, 0, 0, 2, 0, 1, 2, 0]）→ 鋪倉完成
- 建議 IC：sell BeCS ≤180C + sell BuPS ≥150P
- 現價 $128.64，在區間 [150~180] 的 -71th 百分位
- ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空
