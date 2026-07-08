# 2026-07-08 INTU 策略卡 — 敘事 de-rate 待判決股：現價低於我方 bear target、反彈是 beta 不是 alpha，觸發綁結構確認或 8/21 ER

> 數據時間戳：現價 **$281.34**（2026-07-07 收盤，SG data_table；+3.4%，日內 274.36–283.79；prev close $272.14）
> 盤面：52wk 252.84–813.70｜**距 52W 高 -65%**、距 52W 低 +11%｜**除息 7/9（$1.20/季，+15%）**｜財報 **2026-08-21 Q4 FY26**（valuation 檔）
> 我方**現無持倉**（brokerage_2026-07-06 查無；曾持 OCT16'26 280C，**06-04 出清 @S~$311**，其後股價再跌 ~15%——出場已兌現）
> 源出：`TREND INTU`（07-08 凌晨 session）；估值 SSOT＝[[valuation_log/INTU]]（05-29 校準）；大盤背景＝[[07-07-2026_TRENDFP]]

## 縮寫對照
- **FP** = FlowPatrol（SG 盤後機構選擇權流量）｜**ER** = 財報｜**IGV** = 北美軟體 ETF｜**QBO** = QuickBooks Online
- **CW/PW/HW/KG/KD** = Call/Put/Hedge Wall、Key Gamma/Delta Strike｜**IVR** = IV Rank｜**DPI** = 暗池指標（越高承接越強）
- **sig** = FP 統計顯著部位（百分位）｜**NTM** = 未來十二個月｜**R:R** = 風險報酬比

---

## 一、時間軸（機構視角）

```
05-20  Q3 FY26 beat+raise（EPS 指引上修至 $23.83, +18%），但「裁員17% for AI」
       自證 AI 顛覆敘事 → 盤後 -13.4%；DPI 崩至 15（恐慌拋售）
05-21  我方框架 de-rate：base_pe 32x→20x（user 決策），bear $308 / base $538 / NTM $528
06-02  GS 下調 Neutral→Sell（Stifel 亦下調）——最後一刀
06-04  ★我方出清 OCT16'26 280C（S~$311）；躲過末跌段
06-22  觸底 $252.84（52W 低）；Skew Rank 已塌至 0.26
06-25  Citi 重申 Buy → 「SaaSpocalypse」超跌軟體板塊反彈啟動
06-29  IGV sig delta +$405M（100th）+ Jan'27 80P→70P roll down ×10萬口（板塊級回補）
07-07  收 $281.34（+3.4%），站上 CW/KG 270
```

## 二、機構定位總結（TREND 挖掘結果）

| 層面 | 證據 | 判讀 |
|------|------|------|
| 個股期權（FP） | 半年僅 1 次上榜（03-06 噪音段）；崩盤前後皆無大單 | **機構沒在單名期權表態**——無搶跑、無抄底 |
| 板塊 ETF（FP） | IGV 06-29 +$405M(100th) + put roll down ×100k；07-02 +$218M(93th) | 機構用**整籃 IGV** 回補軟體，INTU 吃 beta |
| 結構（data_table） | Skew Rank 0.97→**0.24**（對沖盤撤）；px 站上 CW=KG 270；KD 500→240 歸位 | 空頭動能衰竭三訊號 |
| 暗池 | DPI：15（5/25 恐慌）→ 42（6月底承接）→ 33（現在溫吞） | 低點有人接，但**無持續累積型買盤** |
| 賣方 | GS Sell(6/2) vs Citi Buy(6/25)；共識 27/34 Buy、mean ~$487–491（+73%）；單點 $875（OpenAI 合作 de-risk） | 分歧極大＝敘事股特徵 |
| 13F（Q1，滯後） | 1,029 加 / 963 減 | 無方向共識，僅主題確認用 |
| 公司自身 | 股息 +15%、Q3 回購 $1.6B、深化 OpenAI/Anthropic 合作 | 管理層「威脅內化」路線 |

**一句話**：基本面數字全程向上（EPS 指引 +18%、共識 EPS 反升 +1.5%）、股價 -65%——教科書級敘事 de-rate。目前反彈成色＝short-cover ＋板塊 beta ＋ Citi/OpenAI de-risk 敘事，**尚無 smoking-gun 機構單名回補**。

## 三、估值 vs 結構（雙錨）

**估值錨**（[[valuation_log/INTU]]，base_pe 20x 已含 AI overhang）：
- 現價 $281 **低於 bear target $308 達 -8.8%**、低於等待區 zone 310–360 ——市場定價比我方最悲觀劇本更悲觀
- vs base $538：**+91%**｜vs NTM $528：+88%｜vs bull $812：+189%
- 帳面 R:R 極佳，但同 NOW/WDAY 警語：**低 P/E 可能是顛覆論的合理定價而非錯殺**，判決 SSOT＝8/21 ER 的 TurboTax 留存 / QBO seat / Intuit Assist 變現

**結構錨**（data_table 2026-07-07，SSOT）：

| 項目 | 值 | 註 |
|------|-----|-----|
| CW = KG | **270** | 07-07 已收在其上＝短線突破；能否站穩+CW 上移是關鍵 |
| HW | 250 | gamma 正負分界 |
| PW = KD | **240** | 下檔結構支撐 |
| IVR / Garch Rank | 0.75 / 0.61 | vol 仍貴，裸買不划算 |
| Skew Rank | **0.24** | 下檔保護便宜＝對沖需求已撤 |
| DPI / 5d | 33% / 29% | 承接偏弱 |

## 四、狀態機（無持倉起手；重進場＝新決策，非補舊倉 [[feedback_no_flip_without_entry_context]]）

| 狀態 | 觸發條件 | 動作 |
|------|----------|------|
| **觀望（現況）** | 281 剛站上 270、除息 7/9、反彈屬 beta | 不追。等結構確認或 ER 判決 |
| **結構確認 → 試多** | 收穩 **270 之上 3–5 日且 CW 上移**（含除息調整）＋ IGV 板塊 flow 未轉負 | 小倉試多；**IVR 0.75 下用價差不裸買**：如 Oct'26 280/330 bull call spread，或賣 PW 下 240P 收租（skew 便宜=賣 put 權利金一般，優先 call spread） |
| **回踩接多** | 回踩 **250（HW）–240（PW）** 帶量縮 ＋ DPI 回升 >40 | 分批建（該區 = 我方 bear $308 下 -20%，深度安全邊際） |
| **失效** | 收破 **240（PW）** 或 IGV 機構 flow 轉賣（sig 轉負） | 全多頭分支凍結，等 ER |
| **ER 事件（8/21）** | 判決日：TurboTax 留存 / QBO seat / Assist 變現三指標 | seat 韌性證實 → 比照 SNOW「錯殺已修復」處理、可上正倉；證偽 → 降級至 ACN「真減損層」，框架 bear EPS 22.00 啟用 |

**三檔目標價**（NTM blend 口徑，[[methodology_NTM_blend]]）：
- Bear **$308**（14x × $22.00）：AI 侵蝕坐實、增速停滯——注意現價已低於此
- Base/NTM **$528–538**（20x）：FY26 指引兌現、QBO Enterprise +38% 抵銷 Consumer
- Bull **$812**（28x × $29.00）：Intuit Assist 變現、OpenAI 合作使 AI 由威脅轉動能

## 五、與軟體三層框架的掛鉤（[[project_software_sector_frame]]）

INTU 與 NOW 同屬「**待判決層**」（敘事 de-rate、基本面未證偽）：
- SNOW 路徑（錯殺修復）：需 8/21 ER 給出 seat/留存韌性證據
- ACN 路徑（真減損）：TurboTax DIY 用戶被 AI 自助報稅分流的實際數字出現
- INTU 特有變數：**顛覆者變盟友**（OpenAI/Anthropic 合作）——這是 NOW 沒有的牌

## 六、後續追蹤（→ 可轉 SAVETR）

- [ ] 270（CW）站穩與否＋CW 是否上移（每日 data_table）
- [ ] IGV 板塊 flow 是否持續（FP sig 段）；若 INTU **首次以單名身分上 FP** = 機構表態訊號，權重高
- [ ] DPI 能否回 40+（承接轉強）
- [ ] 8/21 ER：TurboTax 留存 / QBO seat / Intuit Assist ACV——判決三指標
- [ ] OpenAI/Anthropic 合作的實質內容落地（de-risk 敘事能否量化）
- [ ] 估值檔 8/21 後大版更新（FY27 指引進框架）

## 關聯
[[valuation_log/INTU]]｜[[07-07-2026_TRENDFP]]｜[[project_software_sector_frame]]｜[[feedback_no_flip_without_entry_context]]｜[[feedback_conservative_base_pe_no_rerating]]

Sources: [IBTimes — Intuit Shares Surge 6% on Rebound from AI Fears](https://www.ibtimes.com.au/intuit-shares-surge-6-rebound-ai-fears-strong-fundamentals-analyst-upgrades-1862751), [Motley Fool — Is OpenAI Coming for Intuit Next?](https://www.fool.com/investing/2026/05/26/is-openai-coming-for-intuit-next/), [Fintel — INTU Institutional Ownership](https://fintel.io/so/us/intu), [TIKR — Is Intuit Stock a Buy After Falling 67%?](https://www.tikr.com/blog/is-intuit-stock-a-buy-in-2026-after-falling-67-from-its-52-week-high)
