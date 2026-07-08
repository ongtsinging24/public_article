# SpotGamma — 波動率、Skew 與尾部風險（Scott Nations, Nations Index）

> **來源性質**：SpotGamma 與 Scott Nations（Nations Index，VolDex/SkewDex 等指數創製者）對談。SpotGamma 為主數據源（SG_DIR）——高方法論價值，常青知識庫。
> 原片：YouTube `yTzNl8o7Jp4`，2022-09-30，39.6 分鐘，yt-caption(en-orig)。錄製當日市場大跌（英國央行/英鎊危機背景），多項波動率指標正釋放重要訊息。

---

## 縮寫對照
| 縮寫       | 全稱                                  | 說明                                                                 |
|------------|---------------------------------------|----------------------------------------------------------------------|
| VolDex     | Volatility Index (Nations 自製)       | 純粹「價平 (ATM) 隱含波動率」的封閉解；片中口語常作 "volley/valdex"   |
| SkewDex    | Skew Index (SDEX)                      | 1 個標準差價外 put IV 減 ATM、再正規化，量化 skew                     |
| TailDex    | Tail Index (TDEX)                      | 30 天、3 個標準差價外 put 的正規化成本＝對沖尾部事件的保險費          |
| TermDex    | Term-structure Index                   | 用單一數字量化期限結構斜率（7 天～360 天的最佳擬合斜率）             |
| VolQ       | VolDex 方法論套用於 NDX（NASDAQ 100）  | 期貨在 CME 交易，代碼 BLQ；選擇權代碼 VOLQ                            |
| VIX        | CBOE Volatility Index                  | 用兩個近月所有價外選擇權算的「變異數 (variance)」衡量                |
| SKEW       | CBOE SKEW Index                        | CBOE 的 skew 指數；Nations 認為其算法不合理且僅收盤計算一次          |
| IV / RV    | Implied / Realized Volatility          | 隱含波動率 / 已實現波動率                                            |
| ATM / OTM  | At-the-money / Out-of-the-money        | 價平 / 價外                                                          |
| SD         | Standard Deviation                     | 標準差（指數均以「當下 ATM 選擇權成本」反推，而非歷史 RV）           |
| SPX / SPY  | S&P 500 指數 / 其 ETF                  | VolDex 算 SPX；SkewDex/TailDex 算 SPY                                 |
| NDX / QQQ  | NASDAQ 100 指數 / 其 ETF               | VolQ 對應標的                                                        |

---

## 一句話總結
**波動率的本質是「市場此刻對未來波動的定價」，而 skew 量化了 IV 隨偏離 ATM 而變化的形狀、tail risk 則是 3 個 SD 外深價外 put 的保險成本——關鍵在於用「乾淨的 ATM IV」當基準（VolDex），再正規化衡量 skew/tail/term，才不被 VIX 那種把深價外選擇權過度加權的「變異數」雜訊污染。**

## 重點

### 波動率的本質（realized vs implied、VIX 的侷限）
- **VolDex (volley) = 純 ATM 隱含波動率的封閉解**。Nations 做了 25 年期權造市（CME 場內，先做美債選擇權、後做 S&P 期貨選擇權）後，回到交易台第一個會問的問題就是「ATM IV 是多少？」——一切對期權市場的理解都從 ATM 開始，再往價外加上自己的判讀。故 VolDex 刻意排除那些「有自己生命、不真正反映 IV」的深價外選擇權。
- **VolDex vs VIX 的根本差異**：
  - VolDex 只看 SPX 的 ATM 波動率。
  - VIX 用兩個近月幾乎所有價外選擇權（只要有非零 bid 就算進去），包含一堆深價外 put。
  - 致命缺陷：**離 ATM 越遠的選擇權，依其「價格」在 VIX 裡的加權曝險反而越大**——這些深價外 put 並非市場真實狀態的表達，卻被過度加權。這正是 Nations 創 VolDex 的理由。
- **VIX 衡量的其實是「變異數 (variance)」，VolDex 衡量的是「波動率 (volatility)」**。兩者相關性極高、非常相似，但複製/對沖時建構的投資組合不同；**當兩者背離時，是出於重要原因，此時 VolDex 是更恰當的衡量**。（WSJ 有文章把 VIX 當 fear gauge、並看 VIX 與 volley 之差。）
- **RV 的觀察（主持人 Brent）**：當年 S&P 的已實現波動率維持在近 10 年最高的「持續水準」（非只是幾次零星 spike）。風險在於這種高波動被「正常化」，市場與交易者習以為常，最終可能害人——例如為選擇權付太多錢，或在過渡期被甩。
- **波動率具異質變異 (heteroskedastic) 與群聚 (clustering)**：市場會有一段比正常更波動的時期，接著一段比正常更平靜的時期；不會出現「極波動的一天後緊接極平靜的一天」。存在「波動率預算」概念。

### Skew 是什麼、為何存在、怎麼讀
- **Skew = IV 隨著偏離 ATM 而改變這個事實**；其形狀（skew 或有人叫 smirk）很有資訊量，但必須「能量化」——只說「有點/很多」沒用。
- **IV 大家有公認算法（頂多邊緣有分歧）；skew 則沒有公認的單一算法**——存在多種「合理」的衡量方式。
- **SkewDex (SDEX) 算法**：取 SPY 中「1 個 SD 價外 put」的 IV，**減去 ATM vol，再用 ATM vol 正規化**。
- **`VIX ÷ volley`（或 VIX − volley 再除以 VIX）也是一種 skew 衡量**：它量化「所有那些價外選擇權貢獻了多少額外輸入」，是另一種角度但與 SDEX「本質上量同一件事」。錄製當時 `VIX/volley` 與 SDEX 都壓在接近年內低點（類似 2019、covid 崩盤前的水準）。
- **為何 skew 當時偏低（重要解讀）**：
  1. 人們相對自滿，就算買保護也只買一點，且買「ATM put」——沒在為真正嚴重的事件做準備（沒去買價外 put）。1～3 個 SD 以下的買盤減少 → 這些 skew/tail 衡量值就收斂下來。**「買 ATM 而非深價外 put」本身就透露了不少資訊。**
  2. **整條波動率曲線整體上移時，兩翼相對 belly 沒被定得那麼高** → 曲線/skew 變平 → 兩翼相對沒那麼貴。
  3. **機制性原因**：因為指數用「當下 ATM 選擇權成本」反推 1 個 SD（不用陳舊的歷史 RV），所以 **volley（ATM vol）一升高，1 SD / 3 SD 價外的門檻就被推得更遠**，也會壓低這些 OTM 指標的讀值。
- **錄製當下的轉折**：上週大家認定 8 月的做法錯了，開始「搶買價外 put」——沒人敢在英國央行快崩時賣 put。TailDex 開始 spike、「甦醒」。

### 尾部風險 (tail risk) 與其定價 / 對沖
- **TailDex (TDEX) = 30 天、3 個 SD 價外 put 的正規化成本**。取 3 個 SD 是因為這是大家公認「尾部事件」發生的門檻。**白話：TailDex 就是未來 30 天為投資組合對沖尾部事件的保險費。**
- **相對 vs 絕對水準**（主持人提問，Nations 同意）：應看「相對移動」而非錨定絕對位置（例如別硬比 2021/12 的數值）。
  - **「從 10 漲到 15 比從 50 漲到 75 容易」**——低基期時 tail 容易被推升，因為那些 put 之前在相對基礎上變得很便宜（不確定性下被低估）。
  - 即便如此，Nations 認為 **TailDex 在 15 並不算特別偏高**，他「很難為 TailDex=15 感到興奮」。
- **尾部定價的悖論（主持人）**：類似 VIX 衝到 80，沒人真會去買 80 的 put（多半永遠不會 pay off，除非 VIX 衝 200）；TailDex 是「極端恐懼」的衡量，類似 volley/VIX spike。
- **延伸玩法**：可看 `volley ÷ TailDex` 比率——能凸顯「長期以來大家想買保護時都買 ATM、不買深價外 put」這個事實。

### Scott Nations 的指數方法論（VolDex / SkewDex / TailDex / TermDex / VolQ）
- **共通設計**：所有指數的 1 SD / 3 SD「都用當下 ATM 選擇權的成本」來反推標準差，**不用過去 20 日/50 日的 RV（那是陳舊的）**——要讓「此刻的市場」告訴我們一個 SD 是多少。
- **TermDex（期限結構）**：
  - 不做盤中發布；Nations 個人 Twitter 與公司帳號 `@Nations_Indexes` 常貼。
  - 是把「期限結構斜率」量化成單一數字＝**7 天到 360 天的最佳擬合斜率**。
  - **正常 = 短天期 IV < 長天期 IV**（contango，左下到右上）；**反轉 (inversion) = 短天期比長天期貴**，代表世界「不正常」。
  - **TermDex 強烈為負（斜率從左上陡到右下）時，傾向標記 S&P 的「低點」**——有相當的預測力，事實表 (fact sheet) 第二頁列其對未來 20 個交易日 S&P 走勢的預測價值。
  - 官網「index values」可下載歷史值（盡量月更、實際多季更）；Twitter 置頂有期限結構的動畫（藍線＝SPY IV 期限結構的歷史平均形狀，紅線＝2022 年 9 月中當時形狀；可回看 2020/03、2018/02 的極端）。
  - 用 SPY 選擇權（到期日近乎無限多），所以**不像 VIX 期限結構那樣受「有限的 VIX 期貨到期、結算同步、日曆多一天」等技術扭曲**；TermDex 真正會被弄亂的是**催化事件 (catalysts)**——大家想持有某特定到期日的選擇權去接事件，曲線就出現怪 kink（如上次 Fed 會議前）。
- **VolQ（NDX 版）**：把 VolDex 方法論套到 NDX 選擇權；期貨在 CME（BLQ），選擇權在各 NASDAQ 交易所掛牌（VOLQ）。**選擇權與期貨都是「指數的衍生品」，選擇權不是期貨的選擇權**。
  - 重要趨勢：**投資組合越來越像 NASDAQ 100、越來越不像 S&P 500**——因為 Apple 當年表現相對好，在組合中佔比變大，而 Apple 是 NDX 第一大成分（也是全球 ETF 資金流最大受益者）。故該用「貼合自己組合」的波動率衡量。
- **對 CBOE `SKEW` 指數的批評**：算法「很 goofy」，Nations 不知有任何業界實務者或學者認為那是衡量 skew 的正確甚至合法方式；且**只在收盤算一次**（盤中沒用）。技術上：SKEW 用 SPX 標準差當分母，該 SD 起落會導致異常計算。Nations 重申「skew 有不只一種合理算法，但 SKEW 不是其中之一」。

### 片中實例與數字
- **2020/03~04（covid 崩盤）**：TermDex 動畫顯示「7 天」數值衝到約 **90，甚至接近 100**——「看起來像世界要終結、沒人知道怎麼收場」，正是極端的例證。
- **錄製當下（2022/09/30 前後，約中午）**：市場大跌、英國央行/英鎊危機。大家在搶買「短天期」選擇權（短天期＝出於恐懼），擔心明後天再跌 100 點。期限結構處於反轉/backwardation。
- **未來 30 天事件密集**：CPI 10/3、財報季、ECB 10/27、FOMC 11/2、英國央行 11/3、還有一場選舉——Nations 認為這段曲線「沒太多理由回落或急轉 contango」；若在下一個催化前曲線變平，是自滿訊號，他會很意外（投資人記憶短，但沒那麼短）。
- **VolQ vs VIX 的 basis 套利（compliance 聲明：非交易建議）**：
  - basis = 指數 − 期貨價。
  - 當時：VolQ 期貨「高於」指數約 0.80（正基差）；VIX 期貨「低於」其指數約 1.20（負基差），spread 近 2 點。
  - 利用方式：**賣 VolQ 期貨、買 VIX 期貨**（因兩者到期都收斂於指數值，且同在「下月到期前 30 天」的同一個週三同時結算）。VolQ 期貨乘數僅 **$100**（VIX 較大），故約需 **10 口 VolQ 對 1 口 VIX**。小乘數、買賣價差常 10 美分寬，利於小額表達觀點。
- **選擇權賣方應用**：
  - VolQ 一般水準決定該不該賣 VolQ 選擇權；**VolQ 在 10（下界）時絕不賣**（尤其不賣上方 call），因波動率有下界且均值回歸。
  - VolQ 低時 → 賣 **call spread**（收權利金、限制上方風險）；當時 VolQ 約 35（更高）仍認為賣 call spread 很合理（定義風險、收權利金，但要認知均值回歸，不會永遠在 35）。
  - backwardation 難持續（短天期相對貴必須回落）→ 可考慮賣 **put spread**（非投資建議）：即便長天期 vol 維持（如 90 天 ~27），曲線可快速變平＝短天期 IV 下滑。
  - **VolQ 選擇權的 calendar spread**（如賣 Oct 40 call、買 Nov 40 call）：定義風險，同時利用「大家搶短天期、沒人在乎長天期」。
- **避險比例**：QQQ 部位想用 VolQ 對沖時，因 QQQ 屬他司產品 Nations 不便明講；建議看官網 VolQ fact sheet 的「NDX 相關係數」自行算 hedging ratio。
- **平台操作（thinkorswim）**：`/BLQ` 叫期貨、`VOLQ` 叫選擇權。

### 行為金融補充（Scott Nations 著作《The Anxious Investor》，2022/04 出版）
- 他出過 4 本書，含 2017 年《A History of the United States in Five Crashes》。《The Anxious Investor》分析 **15 種行為偏誤，透過 3 個著名股市泡沫/崩盤情境呈現**；**15 種偏誤沒有一種能改善投資報酬，每一種都有害**，且多半是「身為人」的天性。
- 當前環境最該警惕的兩個相關偏誤：
  - **近因偏誤 (recency)**：傾向相信「最近發生的＝正常、會延續」。最近股市的情況其實不正常，卻被當常態 → 人們因撐不住痛苦而在底部砍出。
  - **可得性偏誤 (availability)**：相信「記憶中能想起的＝正常」；但若一件事能被你記住、且發生在約一個月以前，幾乎可確定它不正常。
  - 實例：2008/02~03 股票型共同基金出現數十年來最大淨流出（＝在絕對底部賣出），且之後多年才回場。
- **「股市沒有動能 (momentum)」**：把道瓊自 1896 年以來的自相關算出來，數值實質為零——各時期之間無相關。

## ROMA 對照註記
- **Skew 解讀直接對應本系統「Skew Rank>90% 壓過 Layer 0 超跌訊號」** [[feedback_skew_overrides_layer0_undervalued]]：片中強調 skew 是「IV 隨偏離 ATM 變化的形狀」、且須正規化量化（SDEX = 1SD OTM put IV − ATM，再除 ATM）。當 skew 高（搶買價外 put、付高保險費）時，市場在為嚴重下行定價，這比單純估值超跌更具優先資訊量——與本系統「skew 暴衝壓過超跌」一致；可把「skew 高＝下行保護需求真實上升」當作價值陷阱的早期過濾器。
- **ATM-反推 SD 的方法論可借鑑**：Nations 全套指數都用「當下 ATM 選擇權成本反推 1SD/3SD」而非歷史 RV——比用陳舊 realized vol 更即時。若 ROMA 後續要自算 skew/tail 門檻，宜用 forward-looking ATM IV 推 SD，避免 stale。
- **VIX 過度加權深價外選擇權的缺陷** → 若 ROMA 用到 VIX 類輸入，理解其本質是「variance、深 OTM 過度加權」，背離 ATM IV 時以 ATM 為準更恰當。
- **TermDex 的低點預測力**：期限結構強烈負斜率（反轉）傾向標記 S&P 低點；可作為 ROMA 期限結構/抄底訊號的設計參考。
- **可回填 `ROMA_SIGNAL_DESIGN.md` 的 skew / vol 章節**：補充「skew 多算法、SDEX 正規化定義、VolDex(ATM) vs VIX(variance)、TailDex(3SD 保險費)、TermDex(7d~360d 斜率) 反轉標低點」等方法論條目。
