# SpotGamma — Vanna / Charm / Delta：高階希臘字母如何推動市場

> **來源性質**：SpotGamma 官方教學。SpotGamma 為主數據源（SG_DIR），與 ROMA opportunities 同源——常青知識庫，高方法論價值。
> 影片：Options Vanna Delta Charm: How it Moves Markets｜SpotGamma（2021-12-08，9.4 分鐘）
> 連結：https://www.youtube.com/watch?v=veJRTWLNvoU

---

## 縮寫對照
| 縮寫     | 全稱                          | 說明                                                       |
|----------|-------------------------------|------------------------------------------------------------|
| IV       | Implied Volatility            | 隱含波動率                                                 |
| VIX      | Volatility Index              | SPX 隱含波動率指數，片中當 IV 的溫度計                     |
| SPX      | S&P 500 Index                 | 標普 500 指數                                              |
| Delta    | Delta                         | 選擇權價值對標的價格的敏感度（避險比率）                  |
| Vanna    | Vanna                         | delta 對 IV 變動的敏感度（IV 動 → 避險比率變）            |
| Charm    | Charm                         | delta 對時間衰減的敏感度（時間過 → 避險比率變）          |
| Gamma    | Gamma                         | delta 對標的價格變動的敏感度                              |
| MM       | Market Maker / Dealer         | 做市商；力求 delta neutral，靠對沖股票調整曝險            |
| OPEX     | Options Expiration            | 選擇權到期日                                              |
| OI       | Open Interest                 | 未平倉量                                                  |
| Rule of 16| Rule of 16                   | VIX ÷ 16 ≈ 市場定價的單日 SPX 百分比波幅                  |

---

## 一句話總結
**當 IV 下滑或時間流向 OPEX，賣方做市商手上的空頭 put 對沖（delta）會自動縮水，迫使其回補股票（buy back），在沒有任何新聞的情況下把市場一路往上「漂移」——這就是 vanna 與 charm 的對沖流機制。**

## 重點

### Delta（複習）
- Delta 是選擇權對標的價格的敏感度，也就是做市商的避險比率。
- 買進 put = 負 delta = 等於做空市場；對手方（賣出 put 的做市商）因此持有正 delta（long delta）。
- 做市商要維持 **delta neutral**：賣出 40 delta 的 put 給客戶後，自己 long 40 delta，於是去**賣出 40 deltas 的股票**對沖。
- 片中例子：市場約 4700（當日大致水位），4600 put 約 40 delta。

### Vanna（delta 對 IV 的敏感度）
- 定義：**IV 變動時，delta（避險比率）隨之改變**。「IV 一動，hedging ratio 就變」。
- 片中圖：同一張 4600 put，藍線為 15% IV、另一條為 30% IV。
- 機制（標的不動、IV 從 30% 掉到 15%）：
  - 該 put 的 delta 從約 40 縮到約 30。
  - 做市商原本 short 40 股對沖，但選擇權現在只剩 30 delta → **空頭對沖過多、向下曝險過頭**。
  - 為回到 delta neutral，需**買回 10 deltas / 10 股**。
- 規模放大：SPX 有數百萬張 put（跨不同到期、不同履約價）。當淨 short put 的 dealer 同步回補空頭對沖 → **把市場往上推**。
- 反身性回饋迴圈（compounding / reflexive loop）：
  - 市場上漲 → put 的 delta 下降（這是 gamma：標的漲、put delta 降）→ dealer 再買回股票。
  - 市場上漲又會**壓低 IV**（vanna 再起）→ dealer 又買回更多股票 → 市場再漲……自我強化。
- 平倉 / 賣 IV 也放大效果：
  - 新交易者認為「不會再崩」（新疫苗、Fed 政策轉向等）而**平掉 put** → dealer 該 put 的 delta 從 40 歸 0 → 須買回 40 deltas。
  - 有人認為該 put 不該值 30% IV、只值 15% 而**做空該 put** → dealer 反而變成 long put → 可進一步回補（cover）更多股票。

### Charm（delta 對時間的衰減 / OPEX 對沖流）
- 片中圖：灰色選擇權維持 15% IV 不變，只把到期天數從 30 天縮到 10 天，以隔離時間因素。
- 機制（標的 4700 不動、IV 不變、僅時間經過約 20 天）：
  - delta 從約 35 衰減到約「略低於 20」。
  - dealer 須買回的股票 = 圖上這段 delta 缺口。
- 結論：在 put 很多的市場（如 SPX），**單純時間流逝（衰減因子）就會製造往上的緩漲 / creep higher**。

### 這些如何造成市場「無新聞的漂移」/ 月中至 OPEX 的順風
- 市場「彈弓」（slingshot）類比：拉高 IV 就像把彈弓的橡皮筋往後拉，儲存能量；一旦放手，IV 釋放會帶動市場走高，而 vanna 是這個類比的關鍵。
- VIX 過高的判讀（片中當下背景）：
  - VIX 來到 35，但 SPX 距高點只跌約 3–4%。
  - 歷史對照：VIX > 30 對應 Volmageddon、2018-12 崩盤（當月 SPX 跌逾 10%、VIX 觸 35）。
  - 用 Rule of 16：VIX ÷ 16 ≈ 1.8，代表 30 出頭的 VIX 在定價約 1.8% 的單日 SPX 波幅；但過去約五天 / 一個月實際少見 1.8% 的波動（尤其在 4500 這個因大量 OI 形成的支撐附近），故判斷該 VIX「太高」。
  - 此即「彈弓拉滿」狀態：定價的恐慌 > 實際波動 → IV 有下滑空間 → vanna 順風。
- OPEX 具體情境（片中當下）：
  - 12/17 到期掛著約 **300 萬張 put**，未來幾天有大量 charm 時間衰減。
  - 12/15（週三）有 Fed → 在那之前 IV 會被撐住一點。
  - 一旦 Fed 出來且**沒有驚嚇市場**（不打翻 apple cart），IV 往往**直接下滑**。
  - 此時兩股力量疊加：(1) 隨 12/17 逼近而**加速的時間衰減（charm）** + (2) **IV 下滑（vanna）** → 常常因此啟動一波 rally。
- 漂移的本質：上述都是「**沒有新消息、純粹做市商被迫對沖**」造成的方向性買盤，故呈現月中至 OPEX 的順風 / 無新聞漂移。

## ROMA 對照註記
- vanna/charm 對沖流是 SG 月中至 OPEX 漂移、GEX 的進階解讀；建議回填 ROMA_SIGNAL_DESIGN.md gamma/對沖流章節。
- 與「無新聞急動=強制對沖流」框架相連：本片正是該框架的「上行」版本——IV 收斂（vanna）+ 時間衰減（charm）共同迫使 net-short-put 的 dealer 回補，形成自我強化的上漲漂移。
- 可操作觀察點：VIX 相對實現波動偏高（Rule of 16 偏離）+ 大量 put OI 集中於近 OPEX + 已知事件（如 Fed）為「IV 釋放扳機」，三者同時出現時，月中至 OPEX 偏多漂移機率升高。
