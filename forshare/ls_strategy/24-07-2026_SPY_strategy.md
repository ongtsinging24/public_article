# TREND / STRATEGY — 機構近期對 SPY 的操作足跡（session 07-14 → 07-22，含 07-23 收盤驗證）

- 生成日：2026-07-24（GMT+8）；快照抓取 2026-07-24 10:14 台北
- 資料範圍：flowpatrol session 07-14 → 07-22（logs 07_15 → 07_23）＋ data_table 07-24（trade_date 07-22）＋ FN 07-21 ~ 07-23
- 來源：`spotgamma_report/auto/flowpatrol/*.log`、`auto/data_table/SPX_data-table_*.csv`、`auto/market_overview/2026_0724_keyLevels.json`、`log_gen_by_roma/founders_digest/`
- **現價**：SPY **$739.30**（2026-07-23 美股收盤，−1.20%）｜對照 SPX **7,408**（−1.2%）、VIX 18.69（+12.3%）、VVIX 102.17（+6.9%）
- ⚠️ 07-23 session 的 FP 明天（07-24）才 publish；本篇最新機構明細 = session 07-22。

**縮寫**：FP=FlowPatrol｜FN=Founder's Note｜d$/g$/v$=顯著部位 delta/gamma/vega notional（**買方側**，見 [[feedback_fp_greek_is_buyside_btosto_unreliable]]）｜%ile=歷史百分位｜OI=未平倉｜0DTE=當日到期｜PW/CW=Put Wall/Call Wall｜ZG=zero gamma strike｜COR1M=1M 隱含相關性（SG 風險旗標，<8 紅色警戒）｜Put Roll=保護 put 展期/移倉｜Collar=買 put＋賣 OTM call｜IVR/SkewRank=IV Rank/Skew Rank（0~1）。

---

## 一、SPY 是「一路往下、往遠拉保護」的單向流

| session | SPY 關鍵掛單 | 性質 |
|---|---|---|
| 07-14 | 732P(7/17) 買 30.9k、740P(8/07) 買 26.9k、710P(8/07) 賣 26.8k | put spread 開倉 |
| 07-15 | 732P 買 20.8k、715P(8/21) 買 16.0k | 續補 |
| 07-16 | 732P 買 24.9k、735P 買 22.8k、**955C(8/21) 賣 27.6k** | 賣遠 OTM call（collar 化） |
| 07-17 | **825C(9/30) 平倉 78.8k（−$23.1M）** | **收掉上檔 call** |
| 07-20 | **740P(7/31) 買 44.7k（+$31.7M）**、715P 賣 30k、750P 賣 30.7k | 保護往下滾（put spread） |
| 07-21 | 725P(7/31) 買 15.7k | 再往下 |
| **07-22（ER 當日）** | **705P(8/31) 買 16.1k**、**730P(8/31) 買 +$9.12M**、740P(7/31) 續買 +$3.74M | **展期到 8 月底 + 行權價下探 705** |

**07-22 的兩個升級（07-23 那份 QQQ/SPY TREND 的待回補項）**：
1. **時間軸拉長**：保護從 7/31 到期整批延伸到 **8/31**（705P/730P）——非 ER 事件避險，是準備更長下行窗口。
2. **行權價下移**：740 → 730 → 705（距當時 747 約 −1.3% / −2.3% / **−5.6%**）。
3. **740P(7/31) OI**：61,899(07-17) → **73,324(07-22)**，+11.4k 張，全期最厚的一堵下檔牆。

**SPX 同步（session 07-22）**：put 全面往下滾（賣 7,575(7/29)、7,550(8/12)、7,500(7/31)；買 7,450/7,440(7/31)、**7,250(2027-02) +$11.0M**）。
> **上檔長尾態度轉折**：07-21 session 還在買 8,250C(12/18) 上檔尾；**07-22 session 改成賣 8,500C(2027-06) −$38.5M**。**上檔從「留著」變「賣掉」，是這波最重要的訊號。**

**Equity ETF 板塊 delta / gamma（FP aggregate）**：
| session | delta_m | gamma_m (%ile) |
|---|---|---|
| 07-16 | −2,206 | +157 (58) |
| 07-17 | −3,422 | +955 (81) |
| 07-20 | −452 | +219 (60) |
| 07-21 | −523 | **−1,525 (12th)** |
| 07-22 | −927 | −989 (24th) |
→ **短 gamma 環境已成形**：破位會被放大，不是緩跌。

---

## 二、07-23 收盤：機構的單子全部打中（驗證）

- SPX 收 **7,408**，跌破 SG Risk Pivot **7,480**；SPY 收 **739.30**，**跌破 Put Wall 740**。
- VIX +12.3%→18.69、VVIX +6.9%→102.17；**COR1M 單日 +71%→7.3**（機構最怕的 dispersion 反轉真的啟動）。
- Mag7 單日最差 since 2025-04 關稅崩；GOOGL −7%（CapEx 上修）、TSLA −16%。
- SG 自營 Aug 7300/7100 put spread **單日 +53%**。
- HIRO：Mag7 佔 S&P Equities 流量 ~75%，結構=**長天期 call 賣出 + put 買入**（減上檔＋加下檔，與 FP 的 825C/955C/8,500C 賣出同源）。

**結論**：這波不是事後合理化——機構從 07-14 就在買 725–740 put、07-16/17 起收上檔 call，**07-23 的跌被提前約 6 個交易日定價**。呼應 [[feedback_ai_capex_momentum_overruns_bearish_structure]]：GOOGL 這次是**支出側上修 → capex 反跌**，屬該筆記劃出的降權失效邊界，偏空訊號**不降權**。

---

## 三、結構層現況（as-of 07-22 keyLevels + 07-24 data_table）

| 項目 | 值 | 讀法 |
|---|---|---|
| SPY Call Wall / Put Wall | 755 / **740** | **PW 已失守** → 下方無 gamma 支撐錨 |
| zero gamma strike | 751 | 現價 739 遠在其下 |
| Put Gamma / Call Gamma | **−5.87B** / +1.76B | put gamma 持續加深（07-22 −3.81B → 07-24 −5.87B） |
| IV Rank | **0.185** | **保護仍便宜**（沒被搶貴） |
| Skew Rank | 0.476 | 中性；**未觸發**鎖利紀律（門檻 ≥0.9，見 [[feedback_profit_protect_skew_near_high]]） |
| 1M IV / 1M RV | 13.9% / 11.8% | 溢價薄 |
| 距 52W 高 760.40 | −2.8% | 才剛離開高點，恐慌未極端 |
| SG 下一關鍵 | **SPX 7,300 ≈ SPY ~729** | 0DTE put selling 到期後續買 put → dealer gamma **翻負** |

---

## 四、判讀與操作含義

**TL;DR — 機構做了什麼**
1. **SPY = 純避險主戰場**：連續 7 個 session 買下檔 put，07-22 完成「展期到 8/31 + 行權價下探 705」升級。
2. **上檔被系統性放棄**：825C 平倉 → 955C 賣出 → SPX 8,500C(2027) 賣出。機構不再為上檔付錢。
3. **短 gamma + COR1M 反轉已啟動**：Equity ETF gamma 12th %ile，07-23 COR1M +71%，SG 警告的 vol spasm 進第一段。

**給我方多空**
- **引信已觸發**：SPX 7,480、SPY 740 PW 皆破。原本「守住續釘 7,500」情境失效，現為**下行情境**。
- **補保護仍划算**：IVR 僅 0.185。持指數 beta 者，比照機構做 **SPY 730/705 put spread（8/21 或 8/31 到期）**——複製 07-22 session 機構結構，不自創行權價。
- **下一觀察點 SPY ≈ 729（SPX 7,300）**：SG 明講此處續買 put 會讓 dealer gamma 翻負；破則加速，非緩跌。守住則 739–747 震盪打底。
- **不追空**：SkewRank 0.476、距高僅 −2.8%，恐慌未極端；機構是**避險**不是**做空**（705P = −5.6% OTM 保險，非趨勢空單）。
- **不追多**：機構賣了 2027 上檔尾。**盯 SPX 8,000+ call 是否恢復買盤**——那才是趨勢反轉訊號。

---

## 待回補
07-23 session（ER 崩盤當日）的 FP 明天（07-24）才 publish——機構是**加碼保護**還是**獲利了結下檔 put**，需追；同時看 705/730 那批 8/31 put 有無再往下展。

---
關聯：[[23-07-2026_QQQ_SPY_strategy]]、[[23-07-2026_TRENDFN]]、[[23-07-2026_FP_TREND_ALL]]、[[feedback_fp_greek_is_buyside_btosto_unreliable]]、[[feedback_ai_capex_momentum_overruns_bearish_structure]]、[[feedback_profit_protect_skew_near_high]]、[[reference_fp_index_tables_t1_settled]]
