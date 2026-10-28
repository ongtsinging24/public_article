# AI 實驗室的算力承諾怎麼讀成供應商影響：角色／硬度／認列／份額四軸拆解（以 Anthropic S-1 對 AVGO／GOOG／AMZN／MSFT／SPCX／NVDA／TSM 為例）

- 建立：2026-10-27（台北）
- 性質：**框架筆記（未跑回測）**。案例數字取自 Anthropic S-1（2026-10-26 EDGAR）與我方 digest，推論處另外標「推測」
- 素材：[[27-10-2026_Street_anthropic-s1-views-16b-h1-ops-turn-855b-commit]]（市場彙整）、[[29-09-2026_SEC_anthropic-s1-leak-vendor-rpo]]（外流稿＋對手方 RPO 反推）

**縮寫**：S-1＝IPO 招股書；MTM＝持股市價重估；GCP＝Google Cloud；ASIC＝客製化晶片（TPU／Trainium）；
SPV＝特殊目的公司（買硬體再出租的融資載體，本案運作見 S_2_7）；RPO／backlog＝已簽未認列的合約金額；ER＝財報；NRR＝淨營收留存率

---

## TL;DR

1. **「某供應商拿到 $X 承諾」不能直接讀成利多金額**。要先過四軸：(1) 供應商在這筆錢裡扮演什麼角色；(2) 承諾的硬度；(3) 承諾怎麼變成供應商的營收；(4) 這筆錢對供應商的份額有什麼含義。
2. 套用到 Anthropic S-1，影響是**四檔各打在不同地方**，不是同一條利多：
   - AVGO：最硬的承諾，但同時有擔保左尾。
   - GOOG／AMZN：中等硬度，但錢有一部分是循環資金，EPS 也被 MTM 污染。
   - NVDA：只有間接曝險，而且是最軟、可取消的那一層；真正的訊號在**份額**這一軸。
   - SPCX：夾在中間的中介算力商，可能長租入、可短退出（推測）。
   - TSM／MU：不在承諾鏈上，份額軸中性，只吃總量。
3. 媒體最常見的錯誤是把**承租方要付的租金**當成**供應商的營收**（「Broadcom 拿最多，$161B」）。

---

## S_1｜理論框架：四軸

| 軸 | 要回答的問題 | 常見誤讀 |
|---|---|---|
| A 角色 | 供應商只是賣方，還是同時是股東、放款方、擔保人、通路？ | 只看賣方那一面。多重角色代表 backlog 裡有自己的錢繞回來，且多了信用／殘值風險 |
| B 硬度 | 不可取消的租約、最低承諾、驗收後才計費、可提前通知取消，各是哪一種？ | 把「最高可達」與「最低承諾」相加成一個總額（同一份 S-1，媒體口徑從 $430B 到 $855B 都有） |
| C 認列路徑 | 這筆錢會以什麼形式、在哪一年進入供應商的損益？ | 租金總額≠供應商營收（租約可轉讓給金融方，供應商可能只認列硬體銷售）；總承諾≠年度支出（期限越長，每年攤得越薄） |
| D 份額 | 這筆錢流向 GPU 還是 ASIC？流向誰的生態系？ | 把「AI capex 池子變大」直接等同於「每家供應商都受益」 |

另外有一條**跨四軸的共同變數**：承諾方本身的成長二階導。承諾是用未來營收付的；承諾方放緩時，四軸全部要打折。

## S_2｜案例：Anthropic S-1 對四檔供應商的影響

### S_2_1｜四軸對照表

| | A 角色 | B 硬度 | C 認列路徑 | D 份額 |
|---|---|---|---|---|
| **AVGO** | 硬體供應商＋擔保人（residual value support ≈ first lien 約 $43.5B，細解見 S_2_4）＋本票持有人（$42B 額度，可轉 Class N；兩角色與租約硬度的關聯見 S_2_5） | **最硬**：$161.2B 五年 TPU finance lease，除違約外不可取消 | 租約轉讓給金融夥伴，SPV（$63B）買 XPU＋網通，2027 起交貨 ⇒ AVGO 認列的是硬體銷售，**不是**租金總額；轉讓比例未揭露 | ASIC 側最大受益者 |
| **GOOG** | 雲供應商＋股東（Class N 上限 15%）＋放款方（$20B 本票）；IPO 時可再認購 $10B | 中：最低承諾 ≥$114.5B（至 2033-07） | GCP backlog；約占 6-30 backlog $514B 的 22% | TPU 生態系受益，但**推測**：部分 TPU 經濟利益經 AVGO 租約流走，不經 GCP 營收 |
| **AMZN** | 雲供應商＋股東（上限 12%）＋放款方（$15B，IPO 後 30 個月到期） | 中：最低承諾 ≥$110.0B（至 2036-04） | AWS backlog；約占 6-30 backlog $496B 的 22%。三朵雲中期限最長 ⇒ 每年認列最薄 | Trainium 生態系（S-1 未拆雲內 GPU／ASIC 比例） |
| **MSFT** | 雲供應商；同時是 OpenAI 大股東 ⇒ Anthropic 對它是分散客戶來源，不是核心 | 中：最低承諾 ≥$44.9B（至 2033-05） | Azure backlog；只占約 6.6%（分母 $678B 含軟體），三朵雲中曝險最小 | 未揭露雲內 GPU／ASIC 比例 |
| **SPCX** | 中介算力商：對 Anthropic 是供應商，對 Apollo 是承租人 | **軟**：最高 $120.5B，2027 年初起 Anthropic 可提前 90 天通知取消 | 另與 Apollo 簽約 ~$40B master finance lease 買 Vera Rubin，2027H1 起租、每批 5–5.25 年、掛表內 ⇒ **推測**（未證實兩筆對應同一批算力）：長租入、可短退出，期限錯配風險落在 SPCX | GPU（NVDA）路徑 |
| **NVDA** | 無直接合約；經 neocloud／SPCX 間接 | **最軟**：SpaceXAI 可取消；Nscale 約 $44.6B、Lambda 約 $41.3B，驗收後才計費 | neocloud／Apollo 先買卡，NVDA 出貨時就入帳 ⇒ 取消風險先由中介承擔，但會回傳成 NVDA 的訂單風險 | **偏負**：最大的 frontier lab 把不可取消的硬承諾大量放在 ASIC，NVDA 主要出現在軟承諾層（為何是 AVGO 不是 NVDA，見 S_2_6） |
| **TSM** | 無直接合約；TPU／Trainium／GPU 全數在此投片 | 不適用（不在承諾鏈上） | 吃總量：承諾越硬，2027 先進製程＋CoWoS 能見度越好 | **中性（份額軸免疫）**：錢流向 ASIC 或 GPU 都經 TSM |

- **AMD**：S-1 只有一行「AMD 系統 >$20B」，不計入 $637B 具名合計；規模約 AVGO 的 1/8、硬度未揭露 ⇒ 只是「供應商分散」的訊號，不改變份額結論。
- **MU**：S-1 未提；每顆加速器都需要 HBM，邏輯同 TSM（份額軸中性、只吃總量），但無任何數量條款可落地，屬弱間接。
- **INTC**：S-1 與兩份 digest 均無直接連結，不納入。

### S_2_2｜共同變數：承諾方的二階導

- 季營收：Q1-26 $4.73B → Q2-26 $11.56B → Q3-26 約 $17B（**推算**，S-1 留白）。環比從 +144% 降到約 +47%。
- 放緩集中在前五大客戶（+17%），其他客戶 +57%。前 9 個月有 5–7% 營收來自事後發現違規的客戶，清理屬一次性。
- 對手方風險則是**下降**：Q2 營業利益 $974M 首度轉正、1H 營業現金流 +$3.9B、現金 $131.7B。⇒ 「客戶付不出錢」的尾巴變薄，但「客戶成長放緩、承諾消化變慢」是新的爭點。

### S_2_3｜三個額外陷阱

1. **EPS 被 MTM 灌胖**：GOOG／AMZN 的持股重估會進 Other income。AMZN 1H26 $62.8B；GOOG Q1 $2.27、Q2 $6.26／股。IPO 估值 $1.5–2T 代表後續季度還會再出現。規則見 [[feedback_consensus_eps_contaminated_by_oneoff]]。
2. **承租側與出租側不可相加**：AVGO 的 $42B 本票（承租側）與 SPV 銀團（出租側）是同一條租金流的兩端。規則見 [[project_avgo_anthropic_financing_two_layers]]。
3. **backlog 占比越高，品質越要打折**：22% 的 backlog 來自一個同時被自己投資、放款的客戶，backlog 的成長有一部分是循環資金。

### S_2_4｜AVGO 的 residual value support ≈ first lien 是什麼意思

縮寫：RVS = residual value support（殘值支持）；SPV = special purpose vehicle；1L／2L = first lien／second lien（第一／第二順位擔保債權）。

**一句話**：AVGO 承諾 SPV 持有的硬體將來至少值 X，而 X 約等於 1L 貸款額（約 $43.5B）。因此 1L 貸款人幾乎不承擔硬體跌價風險，跌價的部分由 AVGO 補足。Reuters 因此定性為「effectively providing a guarantee」。

**結構（2026-10-26 公告）**

```
            $63B 債務融資
  1L ~$43.5B (69%)  BofA/Citi/MS 安排   <-- AVGO RVS 罩住這層
  2L ~$19.5B        Blackstone 獨家     <-- 無人罩，真正吃信用風險
                 |
                 v
   SPV --- 買 ---> AVGO XPU + 網通（2027 起交貨）
    |
    +--- 出租 ---> Anthropic（五年 finance lease，付租金）
```

- **Lien**：以 SPV 資產（硬體＋租約）為抵押的擔保債權。處分抵押品時，所得先還 1L，再還 2L，最後才輪到股東權益。
- **Residual value**：硬體在租約到期或違約被收回時的剩餘價值。加速器折舊很快，換代後二手價可能很差。
- **RVS**：處分所得低於 X 時，差額由 AVGO 補。X 約等於 1L 額，這就是「≈ first lien」的意思。

**數字例子（假設）**：2029 年 Anthropic 違約，SPV 收回 TPU，只賣到 $15B。

| 步驟 | 金額 |
|---|---|
| 處分所得先還 1L | $15B |
| 1L 缺口 $43.5B − $15B，由 AVGO 依 RVS 補足 | **$28.5B** |
| 2L（Blackstone） | 0，自吃損失 |

1. AVGO 付的是**缺口**，不是全額：損失 = 1L 餘額 − 硬體殘值。$43.5B 是硬體歸零時的上限情境。
2. 1L 的信用主要靠 AVGO 撐，所以利率低；2L 無保護，所以要更高利率（Benzinga 單源稱 Hock Tan 以更高利率＋更多違約損失保護救回交易）。
3. 如果 1L 隨租金攤還而遞減，曝險也會跟著下降，但攤還條款未揭露。

**為什麼 C7 轉 🔴**

- **錯向風險（wrong-way risk）**：Anthropic 會違約的情境，通常就是 AI 需求或算力價格崩的時候，而那時 TPU 二手價也最差。客戶違約和抵押品貶值是同一個衝擊，所以 RVS 最可能在 AVGO 最不想付錢的時候觸發。
- **營收品質**：AVGO 認列硬體銷售，但殘值風險留在自己身上，本質接近 vendor financing。營收能見度上升與左尾變厚可以同時成立。
- 曝險上限從 10-Q 的 backstop $29B 升級到約 1L 額。

**未定之處（「≈」的由來）**

- $43.5B 是 Reuters 引兩名消息人士的拆分，公告只給 $63B 總額和「AVGO 提供 RVS」。
- RVS 的上限、分層、觸發條件（僅違約，還是到期也算）、遞減方式都未揭露。
- 判定點：AVGO FY26 10-K（約 12 月中）的 guarantee／related party 段。澄清有上限或分層 ⇒ C7 回 🟠；揭露額 > $43.5B，或出現第二筆同類 SPV（Moody's 已警示）⇒ 維持 🔴，並檢討倉位上限。

### S_2_5｜AVGO 兩個角色（RVS／本票）與「最硬」租約的關聯

縮寫：NPA = note purchase agreement（本票購買協議）；PIK = payment in kind（以加發本票代替付現息）；RVS、SPV、1L 同 S_2_4。

**一句話**：租約「除違約外不可取消」，所以唯一的出口就是違約。AVGO 的兩個角色剛好坐在這條租金流的兩端：本票在承租側，RVS 在出租側。兩端都綁在「Anthropic 付不付得出租金」這件事上。硬度有一部分是 AVGO 自己撐出來的；硬，不代表風險小，而是把風險從「取消」換成「違約」，再由 AVGO 兩頭接住。

```
  承租側                                    出租側
  Anthropic ===== 租金（$125.2B，2026 租約）=====> SPV（承接 AVGO 轉讓的租約）
     ^                                             |   ^
     | 本票：$42B 額度                              |   | $63B 債務（1L ~$43.5B + 2L）
     |       只能用來付這份租約的季租                |   |
     |                                             v   |
  AVGO（或其指定金融夥伴）                  SPV 拿錢向 AVGO 買 XPU+網通
                                                   |
                                       RVS：AVGO 罩住 1L 的硬體殘值
```

| | 本票（承租側） | RVS（出租側） |
|---|---|---|
| 作用 | 借錢給 Anthropic 付租金，降低違約機率 | 違約、硬體被收回賣掉後，補 1L 的缺口 |
| 什麼時候受傷 | 付不出錢時，PIK 讓面額越滾越大，但它是次順位擔保，回收率低 | 違約，而且殘值 < 1L 餘額 |
| 好的情境 | 轉成 Class N 股權（30 日 VWAP 的 90%），分到上檔 | 永遠不觸發 |

**三個關聯**

1. **硬度是條件式的**：不可取消的前提是付得出租金，而本票就是為了這件事設計的。AVGO 借錢讓客戶付錢給（已轉讓給 SPV 的）自己的租約，這就是 S_1 角色軸說的「自己的錢繞回來」。
2. **兩個角色在同一事件上一起受傷**：違約時本票和 RVS 同時虧損，加上錯向風險（違約當下 TPU 二手價最差，見 S_2_4）。兩者都不是在分散風險，而是加重同一個左尾。「最硬」和「擔保左尾」是同一枚硬幣的兩面。
3. **金額口徑**：
   - $161.2B 是全部租約；本票只服務 $125.2B 那份 2026 租約，額度約可支付其租金的 1/3。
   - 依 [[project_avgo_anthropic_financing_two_layers]]，本票和 SPV 融資是付款端和收款端，不能相加成融資規模。
   - 但就 AVGO 的損失曝險而言，這是兩筆不同的法律債權，違約時可能兩邊都虧。能不能相加，要看靠本票付的租金有沒有拿去攤還 1L：有的話，1L 下降，RVS 缺口縮小。條款未揭露，因此寫「兩筆分列、同一觸發點」，不寫加總數。

**待驗**

- 本票截至 S-1 一張都還沒發，動用期也還沒開始算；持有人可以轉給金融夥伴，風險最後不一定留在 AVGO 帳上。
- 判定點同 S_2_4：AVGO FY26 10-K 的 guarantee／related party 段，同時看 RVS 金額和本票有沒有轉讓。

### S_2_6｜為什麼 ANT 找 AVGO 當這個角色，而不是 NVDA

縮寫：ANT = Anthropic；TCO = total cost of ownership；RVS、SPV、1L 同 S_2_4。現價（2026-10-28 00:02 台北，美東 10/27 盤中，yfinance）：AVGO $342.83｜NVDA $219.04｜GOOG $317.23。

**一句話**：S-1 沒有寫動機，以下是推論。最主要的原因是 ANT 要「擁有」的是 TPU 機隊，而 TPU 的硬體賣方就是 AVGO，NVDA 不賣 TPU；融資和擔保的角色跟著「誰賣硬體」走。更深一層是抵押品的性質不同：TPU 幾乎沒有二手市場，貸款人要原廠擔保（RVS）才肯放款；GPU 有流動的二手市場，金融方可以直接拿 GPU 當抵押品，不需要 NVDA 背書。

| # | 原因 | 性質 |
|---|---|---|
| 1 | **晶片架構**：ANT 的**不可取消承諾集中在 TPU**（AVGO 租約＋Google 雲），但 S-1 把 Trainium／TPU／NVIDIA／AMD 四種晶片寫成並列、可互換，**沒有揭露各晶片用量比例**（S_2_8）。TPU 由 Google 設計、AVGO 負責 ASIC 協同設計和出貨。要自己持有 TPU 而不是租雲端，交易對手只能是 AVGO | 部分事實＋推論：Broadcom 租約是 TPU 設備（事實，p.172）；「主力是 TPU」原寫法不成立，已於 10-28 訂正 |
| 2 | **單位算力成本**：NVDA 毛利率約 75%，ASIC 路線讓 ANT 少付一層 GPU 溢價。燒錢中的 lab，硬承諾應押在成本最低的地方 | 推論 |
| 3 | **抵押品流動性決定要不要原廠擔保**：TPU 只有 Google 和 ANT 生態系能用、殘值難估 ⇒ 1L 要 AVGO 用 RVS 兜底（S_2_4）。GPU 可以轉賣給 neocloud ⇒ Apollo 直接拿 Vera Rubin 做 ~$40B 租賃融資（SPCX），不需要 NVDA 背書 | 推論，但能解釋兩邊結構的差異 |
| 4 | **誰需要用資產負債表搶份額**：AVGO 是挑戰者，要在 Google 自家 TPU 和 NVDA 之間鎖住第四家 XPU 大客戶，所以拿出租約＋本票＋RVS 三件套。NVDA 有定價權，不需要承擔客戶信用風險；它的做法是股權投資＋經雲端銷售（2025-11 宣布投資 ANT 最高 $10B，搭配 ANT 對 Azure 的算力承諾），租賃風險留給 MSFT 這類雲端商 | 投資案是既有知識，不在本 repo 一手檔；動機屬推論 |
| 5 | **ANT 刻意把軟硬承諾分層**：不可取消的硬承諾放在 TPU（AVGO 租約），GPU 放在可取消層（SpaceXAI 可提前 90 天取消、Nscale／Lambda 驗收後才計費）。GPU 流動性好，退出成本低；TPU 是專屬產能，要先鎖住 | 條款是事實（[[27-10-2026_Street_anthropic-s1-views-16b-h1-ops-turn-855b-commit]]）；分層意圖屬推論 |

**NVDA 不是缺席，是換了位置**

```
AVGO: 直接賣硬體 + 租約 + 本票 + RVS  -> 硬度最高，ANT 的信用風險在自己帳上
NVDA: 賣卡給雲端/neocloud/SPCX       -> 出貨就入帳，取消風險先由中介吸收
                                        (但中介被取消時，會回傳成 NVDA 的訂單風險)
```

**交易含義**

- NVDA 份額軸偏負（同 S_2_1），但 NVDA 沒有 ANT 的信用左尾，這是它沒拿到這個角色的好處。
- AVGO 的硬度和 C7 🔴 同源：因為 TPU 抵押品沒有二手市場才需要 AVGO 擔保，這也是錯向風險的來源（S_2_4）。
- 待驗：NVDA ER（2026-11-18）看 neocloud 訂單和可取消條款的揭露；AVGO FY26 10-K 看 RVS 和本票條款。若 RVS 有上限或分層 ⇒ 原因 4 的力度下修。

### S_2_7｜SPV 在本案怎麼運作

縮寫：SPV = special purpose vehicle（特殊目的載體，亦稱 SPE）；ANT = Anthropic；RVS、1L／2L 同 S_2_4。通用概念（破產隔離、分層、擔保回流、讀財報的檢查清單）見 [[28-10-2026_CC_SPV特殊目的載體_破產隔離與擔保回流]]。

**一句話**：SPV 是只為做一件事而成立的空殼公司，帳上只有「一批資產＋為買它借的錢」，目的是把這批資產的風險和母公司或客戶隔開。本案的 SPV 只擁有 TPU／XPU＋網通、對 ANT 的租約，和 $63B 的債。

```
          [貸款人]  1L ~$43.5B (BofA/Citi/MS)  +  2L ~$19.5B (Blackstone)
               |  放款 $63B，抵押品 = SPV 裡的硬體 + 租約
               v
  AVGO ----> [SPV] ----出租----> ANT
  賣硬體     只擁有：             付五年租金
  收現金     - 一批 TPU/XPU+網通   （SPV 用租金還 1L/2L）
             - 對 ANT 的租約
             - $63B 的債
```

| 角色 | 在 SPV 結構裡做什麼 | 得到什麼 |
|---|---|---|
| AVGO | 把硬體賣給 SPV，把租約權利轉讓給 SPV | 出貨即收現金、認列營收；但透過 RVS 留住殘值風險（S_2_4） |
| ANT | 向 SPV 承租 | 不用一次掏出幾百億，改成分五年付租金 |
| 貸款人 | 借錢給 SPV | 收利息；還款來源只看 ANT 的租金和硬體殘值，1L 再加上 AVGO 的 RVS |

**為什麼繞這一圈**

1. **ANT 自己借不到這麼多、這麼便宜的錢**（還在燒錢、沒有投資評級）。SPV 有具體抵押品，分成 1L／2L，1L 再加上 AVGO 的 RVS，部分債就能做成高信用等級。
2. **風險切塊**：銀行拿 1L（低風險、低利率），Blackstone 拿 2L（高風險、高利率）。
3. **AVGO 不用自己當出租人**：否則 $63B 的應收租金和硬體會留在 AVGO 表上；透過 SPV 變成「賣硬體收現金」。
4. 本案**不是**為了讓 ANT 的債消失：finance lease 起租後照樣上表（S-1：2027 起陸續上表）。

**本案的關鍵**：隔離不完整。AVGO 的 RVS 就是風險回流母公司的管道，所以不把它當成乾淨的銷售（C7 🔴）。對照 SPCX × Apollo ~$40B：結構類似，但 NVDA 沒有提供擔保，因為 GPU 抵押品有二手市場（S_2_6 原因 3）。同樣叫 SPV，要看誰背著殘值風險。

### S_2_8｜S-1 有沒有揭露 GPU／TPU／Trainium 用量比例（2026-10-28 補）

縮寫：ANT = Anthropic；R# = `romasys/valuation/source_docs/26-10-2026_Anthropic_S-1_excerpts.md` 列號。

**一句話**：沒有揭露。S-1 全文（約 157 萬字元）逐字搜過，沒有任何按晶片列的百分比、算力份額或工作負載份額。唯一能拿來推的代理是**合約金額**，但那是未來的付款義務，不是用量；而且三朵雲的主約都沒寫晶片。

**S-1 原文怎麼寫**

| 位置 | 原文要點 | 對「比例」的含義 |
|---|---|---|
| p.136 附近、Business | "We train and serve Claude natively across **four major chip families** (AWS Trainium, Google TPUs, NVIDIA GPUs, and AMD GPUs)" | 四種晶片並列，不分主次 |
| Business（Multi-Chip Compute Approach） | "Our compute pool is **fungible by design**… regardless of provider, chip architecture, or physical location" | 強調同一批算力可以跨晶片調度，不強調哪種晶片是主力 |
| p.31 風險因子 | "the composition of our committed compute portfolio, including the **mix of accelerator architectures**… reflects our demand forecasts… at the time those commitments are made" | 承認有組合、而且組合可能和實際工作負載對不上，但沒給數字 |
| p.171–172 | MSFT／Google／Amazon 三份主約只寫「committed to spend at least $X」，**沒有寫晶片**；明確寫晶片的只有 Google 加購（TPU）、Broadcom 租約（TPU）、SpaceXAI／Nscale／Lambda（NVIDIA）、AMD（MI450） | 金額代理裡有約 $270B 的晶片歸屬只能推定 |

全文出現次數：TPU 10、Trainium 7、GPU 24、NVIDIA 15；沒有一處和 % 或 share 連在一起。

**代理：按晶片路徑分的合約金額**

| 晶片路徑 | 合約 | 金額 | 晶片歸屬 | 硬度 |
|---|---|---|---|---|
| TPU | Broadcom 租約（R16） | $161.2B | S-1 明寫 | 最硬，除違約外不可取消 |
| TPU（推定） | Google 雲（R7） | ≥$114.5B | 主約未寫晶片 | 硬（true-up） |
| TPU 加購 | R8 | $125–150B（估計） | S-1 明寫 | 附條件，不在承諾表內 |
| Trainium（推定） | Amazon（R9） | ≥$110.0B | 主約未寫晶片 | 硬（true-up） |
| NVIDIA（推定） | Microsoft（R6） | ≥$44.9B | 主約未寫晶片 | 硬（按批次） |
| NVIDIA | SpaceXAI／Nscale／Lambda（R10–R12） | 最多約 $206.4B | S-1 明寫 | 軟：可取消、驗收後計費、附融資條件 |
| AMD | R13 | >$20B | S-1 明寫 | 附部署條件，不在承諾表內 |

依晶片路徑加總：
- **TPU**：硬承諾約 $275.7B（$161.2B＋$114.5B），加上 R8 估計後約 $401–426B。
- **NVIDIA**：約 $251.3B，其中約 $206B 在可取消層。
- **Trainium**：約 $110B（推定）。
- **AMD**：超過 $20B（附條件）。

**這個代理的三個限制**

1. **只有約半數金額能確認晶片**。MSFT、Google、Amazon 三份主約的晶片歸屬是我方推定，雲端商可以在合約內混用 GPU 和自家 ASIC。
2. **期限不同**，從 SpaceXAI 約 3 年到 Amazon 約 10 年，總額不能直接換算成年度份額。單看年度化，SpaceXAI 全量交付後約 $3.1B／月（約 $37B／年），2027 年的 NVIDIA 年度支出可能不輸 TPU。
3. **承諾≠用量**：fungible 的設計就是讓 ANT 能把工作負載移到最划算的晶片上。合約組合是簽約當下的預測（p.31 原文），而且「upon 90 days' notice」的 GPU 層正是為了讓組合可以改。

**判讀**

- 可以說的是：**TPU 是 ANT 最大、最硬的承諾層**。和 S_2_6 原因 5（硬承諾放 TPU、GPU 放可取消層）一致。
- 不能說的是：**「ANT 主力是 TPU」**或任何用量百分比。S_2_6 原因 1 原本的寫法已訂正。
- 對份額軸（S_1 D 軸、S_3 第 3 點 (c) 格）的影響：NVDA 份額偏負的結論只建立在**承諾硬度**上，不是建立在用量上。如果 2027 年 SpaceXAI 沒有被取消，ANT 的實際 NVIDIA 用量可能和 TPU 同一量級，到時要把 (c) 格的力度下修。

## S_3｜結論與行動

1. 讀任何「AI 實驗室對某供應商承諾 $X」的新聞，先填 S_1 四軸表。填不出 B 或 C 時，該數字只能當上限，不能當營收能見度。
2. 硬度排序（本案）：**AVGO > GOOG ≈ AMZN > MSFT（同硬度但占比最小）> SPCX／NVDA（可取消層）**；TSM、MU 不在此排序上，只吃總量、份額軸中性。但硬度高不等於純利多；AVGO 的硬度同時帶來擔保左尾。我方 AVGO 卡的 C7 已依「AVGO 為擔保人見報」轉 🔴，與營收能見度上升並不矛盾。
3. NVDA 框架（[[project_nvda_structural_cheap]]）的對應：
   - 第 (d) 格（融資形式的信用尾）：Anthropic 轉盈＋現金厚，這格變輕。
   - 第 (c) 格（份額）：被這份 S-1 加重。
   - 第 (b) 格（二階導）：Q3 放緩是第一個實證。
4. GOOG／AMZN 的 ER 讀法：先拆 MTM，再看 backlog 有沒有跳升（代表租金起算），不要被報導 EPS 的大勝帶走。

## S_4｜待驗（可證偽點）

- [ ] GOOGL Q3 ER（2026-10-28 AMC＝台北 10-29 04:00）：Cloud backlog 是否明顯超過 $514B。超過代表租金開始入帳。
- [ ] AMZN Q3 ER（2026-10-29 AMC＝台北 10-30 04:00）：AWS backlog 是否超過 $496B；$15B 本票額度是否開始動用。
- [ ] Anthropic Q3 正式揭露：環比若低於 +40%，「放緩常態化」成立，四檔的承諾消化都要往後推。
- [ ] AVGO FY26 10-K（約 12 月中）：guarantee／related party 段落，確認擔保的精確金額。
- [ ] MSFT Q3 ER（2026-10-28 AMC，與 GOOGL 同晚）：Azure backlog 變化；Anthropic 占比小，預期不顯著。
- [ ] SPCX：Apollo ~$40B finance lease 的承租用途是否對應 Anthropic 合約（期限錯配推測的驗證點）。
- [ ] NVDA ER（2026-11-18）：neocloud 訂單是否出現與 SpaceXAI 可取消條款相關的揭露或指引變化。
- [ ] 「GOOG 部分 TPU 經濟利益經 AVGO 流走」這條推測：需要 GOOG 揭露 TPU 授權或分潤條款才能驗證，目前只能當假說。
- [ ] ANT 晶片用量比例（S_2_8）：S-1 未揭露。看 S-1 修訂版、ANT 上市後第一份 10-Q／法說會有沒有給晶片組合；以及 2027-01／03 SpaceXAI 不可取消期結束後是否被取消（沒取消 ⇒ NVIDIA 用量和 TPU 同量級，S_3 第 3 點 (c) 格下修）。

## S_5｜附錄

- S_2_8 來源：2026-10-28 重抓 EDGAR S-1 全文（accession 0001628280-26-067168），轉純文字後 grep TPU／Trainium／GPU／NVIDIA／mix／percent；全文不進版控，需要時依 excerpts 檔 header 的 URL 重抓。
- 本篇未跑腳本。現價抓取時間：2026-10-27 22:58 台北（美東 10:58 盤中，yfinance）。當時 AMZN $251.74｜GOOG $316.62｜AVGO $339.79｜NVDA $217.59；23:05 補抓 SPCX $149.43｜MSFT $533.31｜TSM $435.43｜AMD $553.16｜MU $925.77｜INTC $92.92。
- 我方估值錨（romasys/valuation/stock_valuation.md，各卡 last_updated 不同）：AMZN zone 247/300、fair $353（clean）；GOOG zone 231/281、fair $330（clean）；AVGO zone 343/416、fair $490；NVDA zone 209/253、fair $298。

## 關聯

- [[27-10-2026_Street_anthropic-s1-views-16b-h1-ops-turn-855b-commit]]
- [[29-09-2026_SEC_anthropic-s1-leak-vendor-rpo]]
- [[digest_NaNa_1026-midterm-18of19-ok-hynix-not-4pct-spcx-lease-on-bs]]（R19：SPCX × Apollo ~$40B finance lease）
- [[project_avgo_anthropic_financing_two_layers]]
- [[28-10-2026_CC_SPV特殊目的載體_破產隔離與擔保回流]]（SPV 通用概念＋10-K 讀法清單）
- [[project_nvda_structural_cheap]]
- [[feedback_consensus_eps_contaminated_by_oneoff]]
- [[feedback_capex_commitment_vs_annual_spend]]
- [[23-07-2026_CC_hyperscaler_capex_防禦性軍備賽_vs_ROI框架]]
- [[11-09-2026_CC_AI-capex一個機制三張臉_半導體的利率保護是重複計價]]
