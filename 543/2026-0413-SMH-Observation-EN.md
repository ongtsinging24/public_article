# SMH Institutional Activity Analysis
**Source: synth_oi + history_v4, as of April 10, 2026**

## I. Price Trend Review
- **3/27:** $374 → **3/30:** $363 (Plunge) → **3/31:** $383
- **4/1:** $392 → **4/2:** $392 → **4/7:** $400
- **4/8:** $423 → **4/9:** $430 → **4/10:** $437 (**↑+20.5%** from local lows)

**Observation:** This rebound occurred in an environment of overall **Negative GEX**. Dealers provided no hedging support (buy-side liquidity), meaning the rally was driven purely by real buyer order flow.

---

## II. Institutional Core Position Signals

### A. Large OI Structure (Crucial)

| Date | Large Call OI | Large Put OI | Interpretation |
|:---:|:---:|:---:|:---|
| 3/27 | 605 | 310 | Institutional Call position static |
| 3/30 | 605 | 310 | Same as above |
| 4/1 | 605 | 352 | Slight increase in Put OI |
| 4/6 | 605 | 310 | |
| 4/9 | 605 | 310 | |
| 4/10 | 605 | **405** | ⚠ **Put OI spiked by +95 contracts** |

**Interpretation:**
- **Large Call OI:** Remained at 605 contracts, static for 10 days. This indicates institutions hold a fixed, large-scale Call position (likely long-term, not short-term).
- **Put OI Spike:** On 4/10, Put OI jumped from 310 to 405 exactly as SMH hit a local high of $437. Institutions are adding Put hedges at the top.

---

### B. Put/Call OI Ratio Trend
- **3/27:** 1.86 → **3/30:** 1.89
- **4/1:** 1.98 → **4/2:** 1.76
- **4/7:** 1.78 → **4/8:** 1.83
- **4/9:** 1.86 → **4/10:** **2.26** (Cycle High)

**Analysis:** The P/C OI ratio soared to 2.26 at the peak of the rally. The market overall continues to stack Puts during the rise, indicating a profound lack of trust in this rebound.

---

### C. 4/10 Put Volume Anomaly
- **Call Volume:** 60,333
- **Put Volume:** 375,196 (**6.2x higher**)

On the day of the rebound high, Put trading volume was more than 6 times that of Calls. Institutions bought protection in massive quantities near $437.

---

### D. GEX Structure (via v4 history - more reliable)

| Date | Gamma Ratio | ATM Gamma Notional | Structure |
|:---:|:---:|:---:|:---|
| 3/27 | 0.00093 | -$91.5M | Extremely Negative |
| 3/30 | 0.027 | -$62.0M | Negative |
| 4/7 | 0.683 | — | Negative, Improving |
| 4/8 | 0.973 | — | Near Neutral |
| 4/9 | 1.173 | — | Flipped to Positive GEX |
| 4/10 | 0.550 / 0.223 | **-$264M** | **Flipped back to Negative** |

- GEX briefly turned positive on 4/9 (Dealers supporting the floor), but flipped aggressively back to **-$264M** on 4/10.
- **Negative GEX** means dealers are "selling into weakness." If SMH drops, there is no dealer buffer to slow the fall; instead, they will accelerate the decline through hedging.

---

### E. Key Levels (v4 data)
- **Put Wall / Low Vol Point:** $405 (-7.3% buffer)
- **Call Wall / High Vol Point:** $450 (+3.0% upside)
- **Current Price:** $437 (Trapped between walls)

SMH is currently sandwiched in a narrow range between the $405 and $450 walls.

---

### F. Skew / IV Structure

| Date | Put Skew Pct | Call Skew Pct | IV Rank |
|:---:|:---:|:---:|:---:|
| 3/27 | 0.956 | 0.088 | 0.44 |
| 4/7 | 0.983 | 0.119 | 0.41 |
| 4/8 | 0.876 | 0.199 | 0.31 |
| 4/9 | 0.824 | 0.231 | 0.28 |
| 4/10 | 0.810 | 0.402 | 0.32 |

- **Put Skew Pct:** Remained > 0.80 throughout the period, showing that the "fear index" is persistently extreme.
- **Call Skew Pct:** Rose to 0.40 for the first time on 4/10—some players are starting to buy Calls, though Puts remain overwhelming.
- **IV Rank:** 0.32 (Medium-low), favorable environment for option sellers.

---

### G. 4/1 Activity Factor = 2.741 (Major Institutional Event)
On 4/1, the Activity Factor spiked to an abnormal 2.741 (compared to < 0.15 on other days), with a Position Factor of 0.595. This marks the most intense day of the tariff shock, where massive institutional rebalancing left a clear footprint.

---

## III. Institutional Strategy Summary

> **Institutional Intent: "Hold Longs + Heavy Hedging, Not Betting on Direction."**
>
> - ✅ **Static 605 Large Call OI:** Core long-term long position remains untouched.
> - ⚠ **4/10 Put OI Spike:** Added 95 Put contracts at the top for protection.
> - 📊 **P/C OI 2.26 + 6x Put Vol:** Institutions do not trust the $437 level.
> - 🔴 **GEX -$264M (Extremely Negative):** No buffer for downside; potential for accelerated selling.
> - 📍 **Walls:** Support at $405 (Put Wall), Resistance at $450 (Call Wall).

**In plain terms:** Institutions hold long-term Call positions (bullish long-term), but they bought massive Put hedges at the $437 peak. This suggests they anticipate short-term pullback risks or at least want to guard against tail-end downside. This is a structure of **"Holding long core + hedging short-term downside,"** not blind bullishness.

---

## IV. Implications for Your Operations

You currently hold **TSM** (direct semiconductor exposure), though not SMH:

| Warning | Content |
|:---|:---|
| **TSM Risk** | If SMH breaks **$405 (Put Wall)**, the semiconductor sector will face collective pressure. |
| **TSM 2nd Batch** | Your limit order logic at **$355-360** is correct; do not chase. |
| **GEX Alert** | If SMH's negative GEX worsens, TSM's "GEX vacuum" structure becomes more dangerous. |
| **Signal to Watch** | Whether SMH can break the **$450 Call Wall** is the key confirmation signal for the sector. |
