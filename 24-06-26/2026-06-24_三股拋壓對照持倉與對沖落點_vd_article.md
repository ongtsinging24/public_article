<!-- short_topic: quarter-end-selloff-portfolio-hedge -->

# 三股拋壓 → 我方倉位落點與對沖決策（6/23 拋售的 actionable 落地篇）

- 日期: 2026-06-24（台北）
- 性質: video_digest 綜評的 **actionable 落地篇**（VDA）｜把博主敘事打到實際持倉、轉成對沖行動
- 索引: [[_INDEX_2026-06-24]]
- 來源 digest: [[nana_2026-06-24]]（偏多/陰謀論框架）、[[rhino_2026-06-24]]（偏空/數據框架）
- 姊妹篇: [[2026-06-24_kospi-circuit-breaker-quarter-end-selloff_vd_article]]（綜評框架）、[[2026-06-24_MU博主期權對撞ROMA_vd_article]]（MU 對撞 ROMA）
- 資料時點: 美股 **2026-06-23 收盤**（最新已成交）＋ 隔夜期貨/MU 即時快照 **≈ 2026-06-24 10:1x GMT+8**
- 關聯紀律: [[feedback_tsm_high_conviction_hold]]、[[feedback_conservative_base_pe_no_rerating]]、[[feedback_profit_protect_skew_near_high]]、[[feedback_cross_broker_position_merge]]

## 縮寫對照

CTA＝Commodity Trading Advisor（系統化趨勢跟蹤基金，到觸發位機械拋售）｜NDX＝納斯達克100｜UPL＝未實現損益｜MV＝市值｜OI＝未平倉量｜IV＝隱含波動率｜DTE＝距到期日｜β-weighted＝以 β 加權後的指數等效曝險｜rrN＝brokerage 解析檔的風險比率欄位。

---

## 一、為什麼這篇要單獨寫

兩支影片講的「三股拋壓洪流」（季末保證金盤潰敗 + 養老金再平衡 ~$1000 億賣股買債 + CTA 趨勢觸發）不是空泛敘事——**它打的標的群（semi + NDX 多頭 + AI proxy）剛好就是我方倉位的三大支柱**。綜評篇講「該不該信博主」；這篇只回答一件事：

> **如果博主說的拋壓是真的，我的倉位站在哪、會被打多痛、該怎麼補保險。**

## 二、落點：倉位正站在拋壓正中央（6/21 倉位，6/24 解析）

對沖前的風險畫面（brokerage_2026-06-21）：

```
半導體 directional 曝險   semi 44.6% (rr9)
MNQ 期貨 NDX notional     54.4% NAV (7 口多單)
AGIX (AI proxy)          13.1% NAV
β-weighted NDX 等效多頭   221.6%      ← 槓桿多頭
index put 對沖 (rr4)      0.00%       ← 完全裸多,無下檔保護
現金 (rr5)               27.2%       ← 唯一緩衝
```

三股拋壓鎖定的三類標的，我方三項全中，且零對沖。

## 三、防線對照（CTA 觸發位 / 真正的防線=call 履約價）

```
標的    6/23收盤   當日%     角色            離防線
────────────────────────────────────────────────────────────
SPX    7365.46   -1.44%   CTA觸發=7312    +0.73% (53pt,一根長黑就破)
SOX指數 13482.5   -7.88%   半導體核心      ※digest「554」非指數刻度,見註
────────────────────────────────────────────────────────────
TSM     436.39   -6.69%   最大倉(52%dir)  call 400→ -8.3% / 380→ -12.9%
SOXX    603.39   -7.88%   Nov 570 call    -5.5% 即價平
SMH     622.05   -6.86%   Jan 580 call    -6.8%
NVDA    200.04   -4.13%   Oct185/Nov190   190→ -5.0% / 185→ -7.5%
AVGO    380.15   -3.06%   Nov 350 call    -7.9%
QQQ     713.65   -3.29%   116 股          —
AGIX     45.36   -3.43%   AI proxy        —
────────────────────────────────────────────────────────────
MNQ(NQ) 29698    -3.12%   7口多單,隔夜29692(持平)
MU      1051.77 -14.52%   風暴眼,財報已引爆(博主說中)
```

**註「SOX 554」校正**：^SOX 指數現為 13,482，554 不可能是指數刻度；對照我方倉位，最貼近的防線是 **SOXX ETF（持 570 call，現價 603 僅剩 5.5% 即價平）**。研判 digest 為口誤/筆誤，追蹤時以 SOXX/SMH ETF 與履約價為真實防線。

## 四、當日傷害估算（6/22→6/23 拋壓日，directional 曝險×跌幅）

```
TSM (股+option)   ≈ -27,700
MNQ 期貨 7口       ≈ -13,400
SOXX option       ≈  -9,300
SMH option        ≈  -5,700
AGIX              ≈  -3,500
QQQ               ≈  -2,800
NVDA option       ≈  -2,200
AVGO option       ≈  -1,600
────────────────────────────
單日合計          ≈ -66,000   (約 NAV 的 -8.3%)
```

裸多 + 季末機械拋壓 = 單日吞掉約 8% NAV。這是「0% 對沖」的真實代價。

## 五、決策與行動

### 5-1 MNQ 7 口 → 已平倉（本波最大一步減壓）

平倉直接拿掉 54% NAV 的 NDX notional：

```
                     平倉前        平倉後
NDX β等效多頭        221.6%   →   ~167%
gross leverage       1.27x    →   ~0.73x (保守區)
最大單一風險         MNQ/TSM並列 → TSM 52% directional 獨大
釋放保證金           →  現金緩衝實質再升 (原 27% cash 之上)
```

→ MNQ 一平，**TSM 變成唯一的集中風險源（單點故障）**，因此下一步優先補 TSM 保險。

### 5-2 TSM（400 股，現價 $436.39，IV ~50%）→ 零成本 collar

```
方案                       結構(Aug21,58DTE)        成本/NAV%        地板       上檔
──────────────────────────────────────────────────────────────────────────────────
A 純保護put(留全upside)    買 400p @18.98 ×4        -$7,592 /0.97%   400(-8.3%) 無限
B 零成本collar(採用)       買400p@18.98 賣480c@21.88 +$1,160 淨收     400(-8.3%) 股480封頂(+10%)
便宜版(Jul31,35DTE)        買 400p @13.18 ×4        -$5,272 /0.67%   400(-8.3%) 無限
```

**採 B（collar）**，理由貼合紀律：
- TSM upside 已由 **6 口長天期 call（380/400 Nov/Sep）扛凸性**；400 股的「線性」上漲是可讓出的部分。
- 賣 480 call 只封頂這 400 股，長 call 凸性完全不動 → 用不需要的 upside 零成本換到 400 地板。
- 符合 [[feedback_tsm_high_conviction_hold]]（核心倉不減、用補 put 管風險）＋ [[feedback_conservative_base_pe_no_rerating]]（480=+10%，本就不該為再評級埋單）。

### 5-3 SOXX / SMH → SOXX 全留、SMH 當籃子保險

關鍵流動性發現決定做法：

```
            倉位                UPL      現價    距履約     期權流動性
SOXX  Nov20 570c ×3 ($40k)    +7,410   603.39  +5.9%ITM   ❌ put OI個位數,spread寬,IV 60-64%
SMH   Jan15 580c ×2 ($30k)    +5,300   622.05  +6.8%ITM   ✅ put OI數千,IV~56%,可成交
```

- **SOXX → 全留**：長天期（Nov 還 5 個月）、ITM、贏家；其期權爛流動性不適合避險，let it ride。
- **SMH → 籃子保險**：買 **SMH Aug21 600 put @43.18 ×1-2（-$4.3k~8.6k / 0.5-1.1% NAV）**，一張流動的 put 同時罩住 SOXX+SMH＋部分 NVDA/AVGO 的相關 semi delta，留全 upside。
- **不砍 call**：MNQ 已拿掉系統性風險，現在缺的是「保險」不是「減倉」；且 semi 剛跌 8%、不貼 52W 高，不觸發 [[feedback_profit_protect_skew_near_high]] 的硬鎖利條件。

## 六、組合結論（一句話）

> **MNQ 7 口已平（−54% NDX notional）＋ TSM 400 股零成本 collar（買400p/賣480c ×4）＋ SMH Aug21 600 put 1-2 張當 semi 籃子保險。**
> 現金支出 ≈ **$4.3k–8.6k（~0.5–1.1% NAV）**，把組合從「0% 對沖的 221% β 裸多」轉為「β ~167%、TSM 有地板、semi 籃子有保險、長 call 凸性全留」。

## 七、後續追蹤錨點（待 SAVETR）

- **SPX 7312**：CTA 機械拋售觸發位；失守則 semi 多頭被放大，重新評估 SMH put 加碼。
- **TSM 400 / 380**：collar 地板與長 call 履約價；跌破 400 啟動地板，跌破 380 長 call 轉 OTM。
- **SOXX 570 / SMH 580**：贏家 call 的價平防線；接近即重評是否鎖利。
- **MU 財報後跳空**：風暴眼是否外溢到 HBM 同業（影響 TSM/semi 情緒）。

---

> 數據口徑：directional 曝險取自 brokerage_2026-06-21 的 rr8b/rr8c；現價為 6/23 收盤、期權為當日收盤靜態報價（盤後抓取，僅供 ballpark）；隔夜期貨/MU 為 6/24 上午 GMT+8 即時快照。實單前以盤中即時報價複核 collar 是否仍為淨 credit。
