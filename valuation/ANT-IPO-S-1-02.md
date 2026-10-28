# 市場彙整：Anthropic 公開版 S-1 的多空看法 —— 1H 營收 $16.3B、Q2 營業利益首度轉正，固定算力承諾 $431B（含「最高可達」為 $637B）

- 抓取日：2026-10-27（台北）
- 觸發：Anthropic PBC 於 2026-10-26 向 EDGAR 公開送件 S-1（Nasdaq，代號 **ANT**；招股價區間／股數／募資額留白）
- 性質：**第三方評論彙整**（媒體／substack／研究機構），數字以 S-1 為準；推算值另外標注
- 前檔：[[29-09-2026_SEC_anthropic-s1-leak-vendor-rpo]]（外流稿＋對手方 RPO 反推）、[[08-07-2026_SemiAnalysis_anthropic-ipo-financials]]

**縮寫**：S-1＝IPO 招股書；NRR＝淨營收留存率（net revenue retention）；LTBT＝長期利益信託（Long-Term Benefit Trust）；
FV＝公允價值（fair value）；ARR＝年化經常性營收；SBC＝股權報酬費用；DCF＝現金流折現；AD＝Artificial Diligence（substack）

---

## TL;DR

1. **成長是真的，但 Q3 在放緩**：2026 季營收依序為 Q1 $4.73B、Q2 $11.56B、Q3 約 $17B（推算）。環比成長從 +144% 掉到約 +47%，放緩集中在前五大客戶（只 +17%，其他客戶 +57%）。
2. **$80.7B 淨損主要是非現金項目**：其中 $72.4B 是可轉債／SAFE 的 FV 重估。營業面看，Q2 營業利益 $974M 首度轉正，1H 營業現金流 +$3.9B，現金 $131.7B。但算進 SBC 之後，1H 營業利益率約 −18%。
3. **NRR 900% 不可跟 SaaS 比**：基期只要有 $1 營收就算合格客戶，又是消費型營收，用量擴張很快、收縮也很快。
4. **估值分歧極大**：報導區間 $1.5–2T（約 22–31 倍年化營收）。Artificial Diligence 機率加權約 $0.88T（$51/股）；New Constructs 反向 DCF 只給約 $150B。
5. **對我方最有用的是供應鏈口徑**：AVGO $161.2B 是五年租金，**不等於 AVGO 營收**。另外，GOOGL 週三財報的 Cloud backlog 是本檔第一個可證偽點。

---

## S_1｜核心數字（S-1 原文＋推算值）

| 項目 | 數字 | 註 |
|---|---|---|
| 年營收 | 2023 $41M → 2025 $4.59B | |
| 季營收 | Q1-25 $376M／Q2-25 $787M／Q3-25 $1,382M／Q4-25 $2,040M／Q1-26 $4,731M／Q2-26 $11,555M | Kepler 整理 |
| Q3-26 營收 | 約 $16.9–17B | **推算**（依 S-1 的「86 倍」比較反推），S-1 留白 |
| 1H26 淨損 | $80.7B | FV 重估 $72.4B＋其他費用淨額 $8.8B（未說明）−利息收入 $1.1B |
| FV 重估歷年 | 2023 $1.0B／2024 $5.4B／2025 $34.3B／1H26 $72.4B | 估值越高、虧損越大 |
| 營業損益 | Q2-26 營業利益 $974M（首度轉正）；1H 營業損失 $693M；1H 調整後營業利益 $1,618M | 算進 SBC 後 1H 營業利益率約 −18% |
| 毛利率 | Q2 約 85%（推算）；扣通路費（約占營收 17%）約 68% | S-1 未直接揭露毛利率 |
| 1H 算力／基建費用 | 約 $8.95B（上年同期 $2.33B） | 已超過 2025 全年的 $7.3B |
| NRR | 約 900%（截至 9-30） | 排除 Pro/Max 訂閱；季營收對季營收 |
| 現金 | $131.7B（現金 $112.4B＋短期投資 $19.3B） | 1H 營業現金流 +$3.9B、FCF 約 +$3.4B |
| 信用額度 | $15B 循環信用（2031 到期），12-31 起每季底流動性須 ≥ $5B | |
| 有條件融資 | 本票額度最高 $77B（含 Google $20B、Amazon $15B） | |
| 違規客戶營收 | 前 9 個月營收的 5–7% | **新揭露**：事後發現違反使用政策／商業條款的客戶 |
| 客戶集中度 | 前五大客戶約占前 9 個月營收 25% | 外流稿是「2 大客戶約占 2025 年營收 25%」 |
| 通路 | Marketplace 占 1H 營收 48%；消費型計費占 80% | 三大雲同時是投資人、供應商、通路與競爭對手 |
| 未認列 RSU | $26.6B | IPO 完成時有一次性補提 |

## S_2｜算力承諾分供應商

| 供應商 | 金額 | 性質 |
|---|---|---|
| Broadcom (AVGO) | 約 $161.2B | 五年 TPU 設備租約（finance lease），違約外不可取消；不含利息 |
| Google Cloud | 至少約 $114.5B | 至 2033-07 |
| AWS | 至少 $110.0B | 至 2036-04 |
| Azure | 至少 $44.9B | 至 2033-05 |
| **固定小計** | **約 $431B** | 最低承諾／租金 |
| SpaceXAI（NVDA GPU） | 最高 $120.5B | 初期之後（2027 年初起）可提前 90 天通知取消 |
| Nscale | 最高約 $44.6B | 驗收後才計費 |
| Lambda | 約 $41.3B | 驗收後才計費 |
| **具名合計** | **約 $637B** | 不含 TPU 產能估計（$125–150B）與 AMD 系統（>$20B） |

- 媒體口徑：$430B（Yahoo）／$518B（外流稿）／$637B（Kepler）／$750B（WSJ）／$855B（Artificial Diligence 含全部固定與最低義務）。**S-1 自己的總額留白**，引用前務必帶口徑。
- 承諾占供應商 backlog 比重（Yahoo，以 6-30 backlog 計）：AWS 約 22%（$496B）、Google Cloud 約 22%（$514B）、MSFT 約 6.6%（$678B，含軟體）。

## S_3｜多方看法

| 誰 | 看法 |
|---|---|
| Gavin Baker（Atreides） | 10 月降 token 價格後 ARR「可能已經垂直上升」，年底有機會到 $100B run-rate |
| Ben Bajarin（Creative Strategies） | 超過一半的 Fortune 500 已是大客戶，但花在 Anthropic 的錢不到其總支出 0.1%；前十大也不到 1% ⇒ 滲透率還很低 |
| Daniel McCarthy（馬里蘭大學） | 「強烈正面數據點」；Q2 GAAP 營業利益率 8.4%、毛利率 85.4%；「算力被用滿時就賺錢」，每 token 成本快速下降 |
| Erica Brescia（Redpoint） | 「absolutely blockbuster business」 |
| HackerNoon | 證明是一門真生意、不是燒錢研究室；但「值不值 $2T」要留給 roadshow 回答 |
| Artificial Diligence（多方論點） | 超過 11,900 個年付 $100K 以上的客戶；集中度下降、營業槓桿真實；歷史上降價之後成長加速；管理層一再低估自己的成長 |

## S_4｜空方與質疑

| 誰 | 看法 |
|---|---|
| New Constructs（10-07，根據外流稿） | 「2026 最荒謬的 IPO」；反向 DCF 只估到約 $150B，以 $2T 計算高估最多 93%；要撐 $2T，獲利得到 NVDA 過去四季的兩倍；「不認為 Anthropic 是可行的生意」 |
| Artificial Diligence（Austin Johnsen） | 機率加權每股約 **$51**（約 $0.88T），敏感度 $42–63；若照報導區間下緣 $85 定價，等於貴約 40%。疑點：Q3 營收超過 80% 來自上市不到 6 個月的新模型（營收容易「過期」）；合約化 backlog 只有 $10.8B，對上約 $855B 固定義務；融資對手方同時賣算力給它，下行時脆弱。附註：其六份分析中有五份由 Claude 撰寫（作者自揭利益衝突） |
| Morningstar／PitchBook | 部分算力成本還沒完整反映在帳上；NRR 建立在小基期，目前沒有任何客戶 cohort 留存資料 |
| Michael Burry | $2T 等於 78 家 S&P 500 公司市值加總 |
| Austin Allred | 900% NRR 是「ridiculous stat」 |
| CNBC | 點名 Q2→Q3 明顯減速；有投資人說「沒被驚豔，但算是小驚喜」 |

## S_5｜治理結構與籌碼

- **Class A**（公開發行）：投票權上限 49.9%。
- **Class F**：一股，由七位共同創辦人的 LLC 持有，在 sunset 前握 50.1% 投票權。
- **Class T**：LTBT 持有，一般可選出 7 席董事中的 4 席。
- **Class N**：無投票權，策略夥伴（AMZN 上限 12%、GOOGL 上限 15%）持有；GOOGL 可在 IPO 價格再認購最多 $10B。
- **Class E**：員工股，投票權有限。
- Delaware PBC，屬 Nasdaq 規則下的「受控公司」。批評者的說法是：公開市場股東只拿到經濟利益，拿不到控制權。
- 解禁：一年內分超過 20 個窗口。

## S_6｜市場反應與相關標的現價

10-26 美股收盤（抓取時間 2026-10-27 15:04 台北，yfinance）：

| 標的 | 收盤 | 當日 |
|---|---|---|
| NVDA | $216.00 | +2.3% |
| AVGO | $329.17 | +2.2% |
| MSFT | $532.60 | +1.5% |
| AMZN | $249.09 | +0.1% |
| GOOGL | $316.80 | −1.4% |
| AGIX | $43.82 | +4.1% |

- AI 交易隨 S-1 回溫；GOOGL 逆勢收黑。
- AGIX 是我方的 IPO 代理，見 [[feedback_anthropic_ipo_proxy_prefer_agix]]。

## S_7｜對我方框架的意義

- **AVGO**：$161.2B 是全部主租約、五年租金、不含利息；其中 2026 單一租約 $125.2B。**不等於 AVGO 營收**，因為租約轉讓給金融夥伴之後，AVGO 可能只認硬體銷售。媒體寫「Broadcom 拿最多」常把兩者畫上等號。詳見 [[project_avgo_anthropic_financing_two_layers]]。
- **GOOGL／AMZN**：Anthropic 承諾約占兩家雲 backlog 的 22%。持股重估會灌進 Other income，EPS 有一次性污染（見前檔 S_4）。
- **NVDA**：直接曝險主要經 SpaceXAI（最高 $120.5B，但可提前 90 天取消）及 Nscale／Lambda（驗收後才計費），硬度低於 AVGO 的 TPU 租約。

## S_8｜與前檔對帳（29-09 外流稿 → 10-26 公開版）

| 項目 | 外流稿（09-29） | 公開版（10-26） |
|---|---|---|
| 算力承諾 | $518B，無分年表 | 具名合計約 $637B（固定約 $431B），總額仍留白 |
| 客戶集中度 | 2 大客戶約占 2025 年營收 25% | 前五大約占前 9 個月營收 25% |
| 毛利率 | 未知 | Q2 推算約 85%（S-1 未直接揭露） |
| 前檔 S_7 待驗項 | 公開版 S-1 的 contractual obligations 分年表、take-or-pay 比例 | 已部分解答：取消條款逐家揭露（SpaceXAI 可取消、Nscale／Lambda 驗收後才計費）；分年表仍留白 |

## S_9｜追蹤（可證偽點）

- [ ] **GOOGL Q3 財報（週三 10-28）**：Cloud backlog 明顯超過 $514B ⇒ Anthropic 租金開始入帳；持平 ⇒ 租金還沒起算。
- [ ] **AMZN Q3 10-Q**：$15B 本票額度是否開始動用。
- [ ] **S-1/A 定價**：區間下緣若 ≤ $60/股，就落進 Artificial Diligence 的合理區（$42–63）。
- [ ] **Q3 環比**：若正式揭露後低於 +40%，代表「放緩是常態化」的空方論點成立。
- [ ] **AVGO FY26 10-K（約 12 月中）**：related party／guarantee 段落，承接 [[project_avgo_anthropic_financing_two_layers]]。
- [ ] **Q4 環比（S-1/A 或第一份季報）**：低於 +30% 空方成立；回到 +50% 以上，「一路下滑」改判「先降後穩」（見 S_10）。

## S_10｜晨報觀點檢驗（27-10-2026_morning_call.md 主講人）

原句：「Anthropic IPO **不要碰**，除非拿得到原始股；要看淨損不要看營業損益，成長率會一路下滑」

| 子句 | 判定 | 理由 |
|---|---|---|
| 不要碰，除非拿得到原始股 | **結論同意，理由要換** | 不追價的理由是估值（區間下緣 $85 比 AD 合理價 $51 貴約 40%）加上一年內超過 20 個解禁窗口。「原始股」是在賭上市首日跳空（打新），不是投資論點：承銷價本身偏貴時，拿到原始股也只是把成本降到「比較不那麼高估」，而且散戶很難分到配額。我方曝險維持 AGIX 代理，或透過 AVGO／GOOGL／AMZN 間接持有 |
| 要看淨損，不要看營業損益 | **反對** | 淨損 $80.7B 中 $72.4B（89.7%）是 FV 重估，估值越高、帳面虧越多，跟經營好壞反著走；上市轉股後這類費用大多消失，淨損「大幅改善」會是假象。主講人的直覺有一半對（營業損益被美化），但正解見下方，不是改看淨損 |
| 成長率會一路下滑 | **成立但沒有資訊量** | 基期已接近年化 $70B，放緩是數學必然（環比 +144%→+47%）。真正的問題是放緩比估值預期快還是慢（$2T 約需長期維持 50% 成長）。Q3 的放緩可能被高估：放緩集中在前五大客戶（+17% vs 其他 +57%），且 5–7% 違規營收的清理是一次性的。往上風險：10 月降價後 ARR 可能衝到 $100B（Baker）；往下風險：GPT-6.1 Terra 價格戰，且 Q3 營收超過 80% 來自不到 6 個月的新模型 |

**取代「看淨損」的判準**（上市後追蹤用）：

1. 算進 SBC 的營業利益率：1H 約 −18%，不是調整後的轉正。
2. FCF 扣掉起租後的租賃付款：目前 +$3.4B，但 $161.2B 的 Broadcom 租約從 2027 年才開始陸續上表。
3. 稀釋：$26.6B 尚未認列的 RSU，加上可轉債轉股。
4. 表外承諾：不可取消的固定部分約 $431B。
5. 「其他費用淨額」$8.8B 的組成：S-1 沒說明，roadshow 要追問。

**結論**：結論可以照用，**不申購、不追價**；但理由要換成「估值貴，加上解禁籌碼一路放出來」。「看淨損」這條判準要丟掉，否則上市後淨損隨轉股轉正時，會被誤導去追價。晨報內 Codex 的反駁（「只看 Anthropic 淨損會誤判」）與本節一致。

## Sources

- [SEC EDGAR – Anthropic, PBC Form S-1](https://www.sec.gov/Archives/edgar/data/0002130357/000162828026067168/anthropicpbc-sx1.htm)
- [Artificial Diligence – Anthropic S-1 Review](https://artificialdiligence.substack.com/p/anthropic-s-1-review)
- [Kepler – Anthropic S-1 Breakdown](https://kepler.ai/research/financial/s1-anthropic/)
- [HackerNoon – $80.7B Loss That Mostly Isn't](https://hackernoon.com/anthropics-s-1-shows-$163b-in-half-year-revenue-a-900percent-nrr-and-an-$807b-loss-that-mostly-isnt)
- [Yahoo – $430B locked-in compute, Broadcom tops](https://finance.yahoo.com/markets/article/anthropics-ipo-filing-reveals-430-billion-in-locked-in-ai-computing-chart-of-the-day-134457635.html)
- [Yahoo – S-1 draws reactions ($100B ARR)](https://finance.yahoo.com/markets/stocks/articles/anthropic-1-draws-reactions-investor-022736245.html)
- [CNBC – What investors like and key risks](https://www.cnbc.com/2026/10/26/anthropic-ipo-filing-investor-reaction.html)（403，未讀全文，內容取自搜尋摘要）
- [CNBC – IPO live updates](https://www.cnbc.com/2026/10/26/anthropic-ipo-live-updates-ai-s-1-filing.html)
- [CNBC – 'Most ridiculous IPO' (New Constructs)](https://www.cnbc.com/2026/10/07/anthropic-will-be-most-ridiculous-ipo-of-year-analyst-says.html)
- [24/7 Wall St – Overvalued by 93%](https://247wallst.com/investing/2026/10/08/unprecedented-test-of-investor-gullibility-analyst-says-anthropic-could-be-overvalued-by-as-much-as-93-at-a-2-trillion-ipo-valuation/)
- [Morningstar – 3 Charts on Anthropic's IPO Filing](https://www.morningstar.com/stocks/3-charts-anthropics-historic-ipo-filing)（403，未讀全文，內容取自搜尋摘要）
- [Yahoo – Inside Anthropic's massive and wild prospectus](https://finance.yahoo.com/technology/ai/articles/inside-anthropics-massive-wild-ipo-225844408.html)
- [TheNextWeb – $750B compute (WSJ)](https://thenextweb.com/news/anthropic-s-1-750bn-compute-80-7bn-loss)
- [Investing.com – 2 chipmakers most exposed](https://www.investing.com/news/stock-market-news/anthropic-ipo-these-2-chipmakers-are-the-most-exposed-to-more-compute-demand-93CH-4974069)
- [NPR – IPO could break records](https://www.npr.org/2026/10/26/nx-s1-6014772/anthropic-ai-ipo-could-break-records)
