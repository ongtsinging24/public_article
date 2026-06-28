# 2026-06-28 Hyperscaler capex × backlog 跨標的對照（抽掉 backlog 墊）

> 縮寫：capex=資本支出｜FCF=自由現金流｜backlog/RPO=已簽未交付合約訂單（Remaining Performance Obligations）｜de-rate=估值倍數下修｜SOTP=分部加總｜DCF=現金流折現。
> 性質：**跨檔導覽/對照層**——個股地板細節各自看 strategy 檔；本檔只做「同一根軸上的相對排序」。
> 起源：由 META vs AMZN 兩份壓力估值檔延伸（[[project_software_sector_frame]]）。

## 0. TL;DR
- 這波 2026-06 大跌是**全板塊「show me the payback」de-rate**——四家被同一根軸打：**capex 暴衝 → FCF 被吃乾**。
- 但 **META 跌最慘有結構原因**：它站在這根軸**最差的一角**＝最高 capex/營收比 **＋** 唯一沒有 backlog 墊。
- **市場還沒把任何一家打到 stripped-backlog 地板**：META $553 vs 地板 $405（+36%）、AMZN $232 vs 地板 $142（+63%）。現價裡仍含「AI 回補會發生」的賭注，只是賭注被砍薄。
- 排序（被「抽墊」抽得最兇 → 最輕）：**META ＞ GOOG ≈ AMZN ＞ MSFT**。

## 1. 核心軸：capex 重量 ×  backlog 墊
兩個獨立維度，META 唯一**兩維都最差**：

```
  capex/營收 高
        │
  META ●│              ← 最高 capex 比 + 零墊 = 雙重劣勢
        │
  MSFT ●│● AMZN
        │● GOOG
        │
  ──────┼──────────── backlog 墊 厚 →
   無墊  │           有合約托底
```

- **維度 A — capex 吃掉多少營收**：比例越高，FCF 越快見骨、敘事越黑。
- **維度 B — capex 有沒有外部合約托底（backlog/RPO）**：有 → 市場能說服自己「這是被訂單背書的投資，不是浪費」；無 → 純自賭，倍數沒東西撐。

## 2. 四標的對照表
| | capex/營收(FY26E,約) | backlog 墊 | capex 性質 | FCF 傷害(近況) |
|------|------|------|------|------|
| **META** | **~57%**（$135B/$237B）最高 | **零**（無雲、無外部客戶、無 RPO）| 100% 自賭廣告回補 | 2026–27 FCF **歸零/轉負** |
| **GOOG** | ~25–30%（待校）| **部分**（Cloud RPO 有；但大半 capex 服務內部 Search/AI）| 半賭 | Q1 FCF **−47% YoY**（$10.1B）|
| **AMZN** | ~25%（$200B/$796B）| **有**（AWS RPO + 零售現金引擎墊底）| 合約拉動為主 | 滾動 FCF **崩 95% → $1.2B**（FY25 $11B）|
| **MSFT** | ~35–40%（待校）| **有**（Azure 商用 RPO、OpenAI/企業合約）| 合約拉動為主 | FCF 受壓但仍正、最穩 |

> META 的 $135B = 2026 指引中點、近翻倍；AMZN 的 $200B = 史上單一公司最高。MSFT/GOOG 比例待補實際指引（見 §5 建檔進度）。

## 3. 各家 backlog 墊體質（為何 META 是唯一「無墊」）
- **MSFT**：賣算力給第三方——Azure 商用 RPO、OpenAI/企業合約。capex 有合約拉動，墊最厚。
- **AMZN**：AWS RPO 托底 **＋** 零售是第二層現金墊（即使雲不兌現，零售仍造血）。墊厚但被合併報表稀釋可見度（故 AMZN 須 **SOTP** 才看得到，見 `2026-06-28_AMZN_strategy.md` §1）。
- **GOOG**：Cloud RPO 有墊，但**很大一塊 capex 是餵內部 Search/AI**——這部分跟 META 一樣是自賭，故介於中間。
- **META**：**沒有雲業務、沒有外部客戶、沒有 RPO**。100% 自己吃自己的算力，賭未來廣告高毛利賺回來——**這個「賭」就是被抽掉的那塊墊**（[[project_nvda_structural_cheap]] capex 四拆的 (d) 無合約需求托底，META 卡得最死）。

## 4. 為什麼 META 跌最慘——但別過度歸因
- **相對 de-rate 最深**：同樣 FCF 被 capex 吃掉，三家雲廠能講「被 30%+ 成長雲訂單背書」的故事，**META 沒有故事可講** → 同樣的傷、唯獨它的倍數沒墊撐 → 跌最多。✅ 吻合「抽墊」框架。
- **但這是全板塊事件，非 META 獨有**：GOOG 6/22 單日 **−6%**（一年最慘）、AMZN FCF 崩 95%、四家 2026 合計 capex **>$4,520億**。大家被同一根軸打，META 只是站在最差那一角。
- **關鍵澄清**：框架解釋的是**相對排序**（誰跌多），不是說市場已用 stripped-backlog DCF 給絕對定價——**沒有一家被打到地板**。

## 5. 地板 vs 現價（建檔進度）
| | 現價(時間戳) | 無墊地板 | 距地板 | 地板檔 |
|------|------|------|------|------|
| META | $553（06-26）| **$405**（DCF）| −27% | `2026-06-28_META_strategy.md` ✅ |
| AMZN | $232（06-27）| **$142**（SOTP）| −39% | `2026-06-28_AMZN_strategy.md` ✅ |
| GOOG | ~$380（06-27,待校）| 未算 | — | ☐ TODO |
| MSFT | ~$373（06-28,待校）| 未算 | — | ☐ TODO |

> 下一步若要補齊：GOOG 須拆 Search(現金牛) / Cloud(有墊) / 內部 AI(自賭) 三層；MSFT 用 Azure RPO 覆蓋率折現，墊最厚、地板距現價可能最小。

## 6. 多空操作（跨標的共通）
- **共通分界線邏輯**：現價 → 無墊地板之間，你付的是**「賭墊會回來」的價**；地板之下才是「連回補都不給也便宜」的真便宜（[[feedback_13f_is_lagging_not_entry_signal]]：主題對≠進場價）。
- **若要在這四家裡選多**：偏好「**墊厚 + 距地板近**」者（MSFT/AMZN 體質），而非單純「跌最多」者（META 跌多但墊最薄、賭最大）。
- **反向 META 的上檔彈性**：唯獨 META 的算力**直接餵自家高毛利廣告**，不必等第三方付費——一旦 §5 回補訊號（廣告增速 + AI 變現）出現，「無墊」假設被推翻、地板上修，**回補彈性四家最大**。賭的是這個，但別在沒訊號前先付。
- 載體：偏空/避險用 cash-equivalent，不 rotate 防禦股（[[feedback_derisk_to_cash_not_defensive_equity]]）。

## 7. 追蹤證偽點（共通，每季更新）
1. **季度現金 capex 實際 vs 指引**（驗真花/沙袋；口徑用當年度實際 vs 當年度指引，[[feedback_capex_commitment_vs_annual_spend]]）。
2. **backlog/RPO 增速**（雲三家的墊在變厚還變薄？META 無此項 → 只能看廣告變現）。
3. **FCF 何時轉正**（被 capex 吃乾的傷口何時收口）。
4. **capex/營收何時、降到多少**（normalize 訊號 vs 卡高檔）。

## 8. 關聯
- 個股檔：[[2026-06-28_META_strategy]]、[[2026-06-28_AMZN_strategy]]（對照檔，互為樞紐）。
- [[project_software_sector_frame]]：跌是敘事 de-rate 非基本面崩。
- [[project_nvda_structural_cheap]]：capex 四拆；本表的「backlog 墊」＝四拆的 (d) 下游合約需求托底。
- [[feedback_conservative_base_pe_no_rerating]]：保守倍數、不在 AI 狂熱中樞估值喊折價。
- [[feedback_capex_commitment_vs_annual_spend]]：驗 capex 真花用當年度口徑，別被多年總承諾誤導。

## 來源
- [AI Stocks Selloff June 2026 — Nasdaq −2.2%](https://intellectia.ai/blog/ai-stocks-selloff-june-2026)
- [Big Tech AI spending — investors want proof of payback (CBS News)](https://www.cbsnews.com/news/ai-bubble-tech-selloff-investment-consumer-business-demand/)
- [Tech losses fuel global market sell-off (Washington Post)](https://www.washingtonpost.com/business/2026/06/23/big-tech-losses-fuel-global-stock-market-sell-off/)
- 現價：[CNBC META](https://www.cnbc.com/quotes/META)｜[GOOG](https://www.cnbc.com/quotes/GOOG)｜[MSFT](https://www.cnbc.com/quotes/MSFT)｜[AMZN](https://www.cnbc.com/quotes/AMZN)
