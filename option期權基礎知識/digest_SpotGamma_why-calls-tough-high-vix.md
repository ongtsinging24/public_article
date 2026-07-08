# SpotGamma — 為何高 VIX 時買 Call 是艱難選擇

> **來源性質**：SpotGamma 教學。SpotGamma 為主數據源（SG_DIR），與 ROMA opportunities 同源——常青知識庫，高方法論價值。
>
> 原片：Why Calls Are a TOUGH Choice with HIGH VIX | SpotGamma（2022-03-04，約 8.2 分鐘）

---

## 縮寫對照
| 縮寫 | 全稱 | 說明 |
|------|------|------|
| VIX  | Volatility Index | CBOE 波動率指數，反映 S&P 500 隱含波動率 |
| IV   | Implied Volatility | 隱含波動率，市場對未來波動幅度的估計 |
| DTE  | Days To Expiration | 距到期日天數 |
| OPEX | Options Expiration | 期權到期日 |
| FOMC | Federal Open Market Committee | 聯準會公開市場委員會（決定利率）|
| QE   | Quantitative Easing | 量化寬鬆 |
| vega | （希臘字母）| 期權價格對 IV 變動的敏感度 |
| theta| （希臘字母）| 時間衰減；每過一天期權損失的時間價值 |
| SPX  | S&P 500 Index | （片中以 spiders / SPY 對應的 S&P 500 期權討論）|

---

## 一句話總結
**高 VIX 時 long call 要付昂貴的高 IV 權利金，而一旦市場上漲、IV 回落，vega 反向吃掉漲幅，加上 theta 時間衰減，等於繳「雙重通行費」——你必須漲得又快又猛才賺得到錢。**

---

## 重點

### 高 VIX 下 call 權利金與 IV crush 的問題

- **當下情境（片中時點）**：2022-03-04，開盤跌約 1%，VIX 在 33，屬於高 IV 狀態。地緣政治（俄烏）加上貨幣政策（升息路徑）雙重不確定性，市場由 **負 gamma** 主導，put 部位主宰盤面波動。

- **波動率期限結構：backwardation（逆價差）**
  - 片中用 spiders 的 30-delta 期權收盤 IV 圖（回溯至前一年 10 月），不同顏色代表不同 DTE：藍色＝短天期（5 天），黃色＝長天期（30 天）。
  - 此時藍點（短天期）IV **高於** 黃點（長天期）→ 即 **backwardation**，是市場「crash mode」的典型特徵：短天期期權需求暴增、把短天期 IV 推到長天期之上。
  - 對照：1 月初的相對平靜期，長天期 IV 高於短天期，稱 **contango**，才是 spiders 平時的正常狀態。

- **IV 有「下界」（lower bound）**
  - IV 本質是市場預估的移動幅度；市場每天至少會動 20–40 個基點，所以波動率往下有限。
  - VIX 過去雖偶爾被壓到 10 附近，但 12–13 通常就是歷史下界。
  - **Rule of 16（16 法則）**：把 VIX ÷ 16 即可換算成預期單日波動。VIX 33 ÷ 16 ≈ 2%，代表市場正在 price in 每日約 2% 的波動。

- **核心矛盾——IV 像「價格」**
  - 買期權的理想時機是 **IV 低、且預期 IV 會上升**（call、put 皆然）。
  - 反之，若你持有 long 期權而 IV 回落，這會是部位的拖累（vega 為正的 long 部位被 IV 下降所傷）。
  - 現在 VIX 在 33 的高位，IV 大幅回落的機率很高 → long call 天生逆風。

### 片中實例與數字

片中以單一 **4500 call** 為例，做時間與波動率的情境推演：

| 情境 | 設定 | 對 call 價值的影響 |
|------|------|--------------------|
| 今日基準（藍線）| S&P ≈ 4350、IV 21%、約 40 DTE | 把 Fed 與地緣政治化解所需時間都涵蓋進去的合理存續期 |
| 只動 IV（IV 下降）| 其他不變，僅把 IV 往下調 | call 價值 **大幅下滑**；市場上漲時 IV 本就「應該」回落，故漲價賺的錢被 IV crush 抵銷 |
| 只動時間（綠線）| IV 維持 21%，DTE 由 40 → 30 | 純 theta 衰減，同樣拖累部位 |

- 為何選 40 DTE：要留時間讓 Fed（3/16 FOMC，當時約兩週後）與地緣政治有機會釐清，是「合理的存續期長度」。
- **雙重通行費（double toll）的邏輯**：
  1. 若市場真的反彈 → IV 大概率回落 → vega 反向殺傷 call（雖然方向對了，獲利不如預期）。
  2. 若認為「在 Fed 釐清前不會有實質大漲」（片中 SpotGamma 的看法：市場大約在 4400–4500 遇阻，之後在貨幣政策明朗前都是磨盤 grind）→ 期間白繳高昂的 **theta tax**。
  - 兩者疊加 = 買 long call 在此情境下的核心難題。

### 替代做法（spread / 賣方 / 等 IV 回落）

- **Short put（賣 put）**：是取得做多曝險的有趣方法，但此時多數人不願 short vol / short put——週末地緣政治尾部風險（tail risk）太高，「什麼都可能發生」。
- **Long stock（直接持股）**：避開 IV 拖累的乾淨做多方式（片中點到為止）。
- **各式 spread 結構**：可用價差結構去 **抵銷波動率下降的成本**；片中說「有很多種方式可圍繞這點來組裝交易、緩解 IV 回落對 long call 的傷害」，但未列出具體腿別與行權價 (片中未明確)。
- 片中主旨是傳達這個 **基礎概念**——解釋為何高 VIX 會成為許多人不願建立 call 部位的「勸退因子」。

---

## ROMA 對照註記
- 呼應 squeeze 雙觸發紀律「vol 便宜才進」[[feedback_squeeze_entry_dual_trigger]] 與 skew 優先 [[feedback_skew_overrides_layer0_undervalued]]。本片正是反面教材：VIX 33、backwardation 的高 IV 環境，恰恰是「vol 貴」、不該裸買 long call 的時點。
- 與「用 call 撈底的難題」同主題，可互相參照：方向對了仍可能因 IV crush + theta 雙殺而賺不到錢，撈底宜優先考慮 spread / 賣方結構或直接持股。
- 操作上可內化的檢核：建 long call 前先看 VIX 是否處高位、期限結構是否 backwardation；若是，default 改走價差（如 BuCS 降低淨 vega/權利金）或持股，而非裸 call。
