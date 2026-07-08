# 期權策略命名統一表（Glossary）
> 建立日期：2026-04-26
> 目的：統一術語，避免縮寫衝突（BPS / BCS 同名歧義）
> 後續筆記、策略討論一律以本表縮寫為準

---

#期權策略縮寫公約（避免歧義，未來討論一律沿用）
- 命名邏輯：Bu/Be(方向) + P/C(用什麼) + S(Spread)
- 雙腿 spread 統一用以下 4 個縮寫：
  - BuPS = Bull  Put  Spread （看多 / Credit；舊稱 PCS）
  - BeCS = Bear  Call Spread （看空 / Credit；舊稱 CCS）
  - BePS = Bear  Put  Spread （看空 / Debit ；舊稱 PDS）
  - BuCS = Bull  Call Spread （看多 / Debit ；舊稱 CDS）
- 禁用 BPS / BCS（單字母 B 在 Bull/Bear 之間有歧義）
- 單腿：CSP (Cash Secured Put)、CC (Covered Call)
- 組合：IC = sell BuPS + sell BeCS（Iron Condor）

## 命名公約

```
 統一縮寫   方向 + 用 Call/Put + Spread
─────────────────────────────────────────
 BuPS  =  Bull  Put  Spread   (看多 / Credit)
 BePS  =  Bear  Put  Spread   (看空 / Debit)
 BuCS  =  Bull  Call Spread   (看多 / Debit)
 BeCS  =  Bear  Call Spread   (看空 / Credit)

 命名邏輯：Bu/Be(方向) + P/C(用什麼) + S(Spread)
 用 Bu/Be 兩字母區分，避免單字母 B 撞名
```

---

## 一、單腿策略（Single Leg）

```
 縮寫   全稱                       建構方式             權利金   Bias
──────────────────────────────────────────────────────────────────
 CSP    Cash Secured Put           Sell Put + 預備現金   Credit   看多 / 想低接
 CC     Covered Call               持有股票 + Sell Call  Credit   看震/微多
```

**用途差異**：
- CSP：「我想在 $X 接股票，邊等邊收 premium」
- CC：「股票漲不動，賣 OTM call 賺額外現金流」

---

## 二、雙腿價差策略（4 大象限）

### 1️⃣ BuPS = Bull Put Spread（看多 / 收錢）
```
 舊縮寫       PCS (Put Credit Spread)
 別名         多頭看跌價差 / 牛市賣沽
 建構         Sell  高價 Put (收高 premium)
              Buy   低價 Put (付低 premium，作保護)
              → 淨 Credit（收錢）
 賺錢條件     到期股價 ≥ 賣方 Put 履約價
 用法         看不跌（中性偏多 / 想低吸）
```

### 2️⃣ BeCS = Bear Call Spread（看空 / 收錢）
```
 舊縮寫       CCS (Call Credit Spread)
 別名         空頭看漲價差 / 熊市賣 call
 建構         Sell  低價 Call (收高 premium)
              Buy   高價 Call (付低 premium，作保護)
              → 淨 Credit（收錢）
 賺錢條件     到期股價 ≤ 賣方 Call 履約價
 用法         看不漲（中性偏空 / 收租）
```

### 3️⃣ BePS = Bear Put Spread（看空 / 付錢）
```
 舊縮寫       PDS (Put Debit Spread)
 別名         空頭看跌價差 / 熊市買沽
 建構         Buy   高價 Put (付高 premium，主多)
              Sell  低價 Put (收低 premium，降成本)
              → 淨 Debit（付錢）
 賺錢條件     到期股價 < 買方 Put 履約價，越低越賺（封頂）
 用法         看大跌（直接做空，但限制成本）
```

### 4️⃣ BuCS = Bull Call Spread（看多 / 付錢）
```
 舊縮寫       CDS (Call Debit Spread)
 別名         多頭看漲價差 / 牛市買 call
 建構         Buy   低價 Call (付高 premium，主多)
              Sell  高價 Call (收低 premium，降成本)
              → 淨 Debit（付錢）
 賺錢條件     到期股價 > 買方 Call 履約價，越高越賺（封頂）
 用法         看大漲（直接做多，但限制成本）
```

---

## 三、組合策略（Multi-leg）

### IC = Iron Condor（鐵鷹式價差）
```
 建構         Sell BuPS（下方收錢腿）
            + Sell BeCS（上方收錢腿）
              → 淨 Credit（收兩邊 premium）

 [校正]     舊筆記寫「賣出 CCS 和 BPS」其中 BPS 容易誤讀
            用新命名：IC = sell BuPS + sell BeCS
 賺錢條件     到期股價落在兩賣方履約價之間
 用法         賭區間震盪 / IV 過高想吃 theta
```

---

## 四、四象限速查表

```
                Credit (收錢/收 theta)      Debit (付錢/方向押注)
 ─────────────────────────────────────────────────────────────
 看多 (Bull)    BuPS  (舊 PCS)              BuCS  (舊 CDS)
                Sell 高 Put + Buy 低 Put    Buy 低 Call + Sell 高 Call

 看空 (Bear)    BeCS  (舊 CCS)              BePS  (舊 PDS)
                Sell 低 Call + Buy 高 Call  Buy 高 Put + Sell 低 Put
```

**記憶口訣**：
- 同方向 Spread，**Put 才有 Credit/Debit 之分**：BuPS 收錢、BePS 付錢
- 同方向 Spread，**Call 才有 Credit/Debit 之分**：BeCS 收錢、BuCS 付錢
- **看法 + 用什麼期權 + 賠率（Credit/Debit）三選二就能定**

---

## 五、舊縮寫對照（外部資料閱讀時轉換）

```
 外部常見縮寫   全稱                          本筆記統一寫法
──────────────────────────────────────────────────────────
 PCS           Put  Credit Spread             BuPS
 CCS           Call Credit Spread             BeCS
 PDS           Put  Debit  Spread             BePS
 CDS           Call Debit  Spread             BuCS
 BPS (歧義)    Bull Put Spread / Bear Put     視上下文 → BuPS 或 BePS
 BCS (歧義)    Bull Call / Bear Call Spread   視上下文 → BuCS 或 BeCS
```

---

## 六、舊筆記的邏輯錯誤校正

```
 原文                                          問題           校正
────────────────────────────────────────────────────────────────────
 「BPS (Bull Put Spread)」+「BPS (Bear Put    縮寫衝突       BuPS / BePS
 Spread)」同檔同縮寫
────────────────────────────────────────────────────────────────────
 「BCS」同時被 Bear Call Spread 和 Bull Call  縮寫衝突       BeCS / BuCS
 Spread 共用
────────────────────────────────────────────────────────────────────
 IC「同時賣出一個 CCS 和一個 BPS」             BPS 歧義       IC = sell BuPS
                                                            + sell BeCS
────────────────────────────────────────────────────────────────────
 BePS 描述為「直接做空用」                     語意需強化     直接做空，但限損
                                                            (vs 裸 long put)
```

---

## 七、決策流程（怎麼選 spread）

```
 Q1：方向看法？
   看多 → 進到 Q2a
   看空 → 進到 Q2b

 Q2a：看多
   想收錢、看不跌就好  → BuPS  (賣高 Put + 買低 Put)
   想押大漲、付小成本  → BuCS  (買低 Call + 賣高 Call)

 Q2b：看空
   想收錢、看不漲就好  → BeCS  (賣低 Call + 買高 Call)
   想押大跌、付小成本  → BePS  (買高 Put + 賣低 Put)

 Q3（IV 維度）：
   IV 高 (IVR>50)      → 偏向 Credit (BuPS / BeCS)，吃 theta + IV mean reversion
   IV 低 (IVR<30)      → 偏向 Debit  (BuCS / BePS)，便宜的方向押注
   財報前              → 都不開（見 2026-04-26_THETA_EARNINGS_concept.md）
```
