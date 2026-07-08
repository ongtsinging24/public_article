# Synthetic Long Stock 合成多頭

**結論先講：`Long Call + Short Put，同 K、同到期日` = 完全複製 100 股現股，combo delta 鎖定 +1.00，其餘 Greeks 幾乎歸零。** 這不屬於你四個 spread 縮寫（BuPS/BeCS/BePS/BuCS）的任何一個 — 它是雙腿方向相同（都做多），不是價差。

## 一、結構

| Leg | 動作 | Strike | 到期 | 用途 |
|---|---|---|---|---|
| Leg 1 | **Long Call** | K | T | 提供上方無限 upside |
| Leg 2 | **Short Put** | K（同上）| T（同上）| 提供下方全額 downside + 收權利金融資 |

到期損益 = `max(S−K,0) − max(K−S,0) = S − K` → 一條 45° 直線，斜率 = 1，與持有現股完全一致。

## 二、為什麼它 = 現股（Greeks 自證）

現股沒有 gamma / theta / vega，合成多頭也一樣，這是它「等價」的數學證明：

| Greek | Long Call | Short Put（同 K）| Net | 意義 |
|---|---|---|---|---|
| **Delta** | +Δc | +(1−Δc) | **+1.00** | 無論 K 選哪裡都鎖 1.0 |
| **Gamma** | +Γ | −Γ | **≈ 0** | Γc = Γp 同 K → 抵銷 |
| **Vega** | +ν | −ν | **≈ 0** | 對 IV 中性，無 vol 曝險 |
| **Theta** | −θc | +θp | **≈ 0** | 只剩 carry 項 |

> 推導基礎：put-call parity 的 delta 恆等式 `Δc − Δput = 1`。short put 的 delta = `−Δput = 1 − Δc`，兩腿相加恆為 1.00。

## 三、成本 = 現股的融資成本

淨權利金 = `C − P`，由 parity：

```
C − P = S − K·e^(−rT) − PV(div)
```

- **K = 現價（ATM）**：淨支出 ≈ `carry − dividend`（小額 debit / credit，取決於利率與配息）
- 你付的其實就是「用槓桿持有 100 股」的融資成本，但**不佔用全額現金**
- Skew 是你的朋友：equity put skew 讓同 K 的 put IV ≥ call IV，short put 收到的權利金偏貴 → 進一步壓低甚至倒貼你的進場成本

## 四、兩種變體（關鍵抉擇）

| | Pure Synthetic（同 K）| Split-Strike / Risk Reversal（分 K）|
|---|---|---|
| 結構 | Long Call K / Short Put K | Long Call K_high (OTM) / Short Put K_low (OTM) |
| Combo Delta | 恆 +1.00 | < 1.0，隨價格移動才爬升 |
| 成本 | ≈ carry | 常為 **net credit / near-zero**（吃 put skew）|
| 中間帶 | 無 | 兩 strike 間有一段「dead zone」P&L 近平 |
| 複製度 | 完美現股 | 近似，非線性 |
| 適用 | 要精準 1:1 替代現股 | 要便宜方向曝險、願放棄部分近價敏感度 |

大多數人口語說「做 combo / 合成多頭」時，實際做的是 **split-strike risk reversal**，因為吃 skew 後常常 0 成本甚至倒收。

## 五、相對直接買現股：優劣

**優點**
- **資本效率**：只需 short put 的 margin + call 淨權利金，遠低於全額現金買 100 股
- 內建槓桿，delta-equivalent share 精準（`contracts × 100 × 1.00`，直接進你的 rr6 beta-weighted 計算不用調整）
- 可挑到期日錯開財報、控制 carry 窗口

**風險 / 成本**
- **Short put = margin 佔用 + assignment 風險**，尤其接近到期或深價內時可能被提前指派
- **無配息**：你是合成方，拿不到現金股利（但定價已反映）
- **Pin risk**：到期日 S 恰在 K 附近時兩腿處置麻煩
- 下方全額暴露 — 這**不是**避險，跌多少賠多少，與現股相同

## 六、對接你的 context（TSM / NRA）

1. **Delta 追蹤**：合成多頭 combo delta = +1.00，IB 可能把兩腿拆兩行顯示 → 沿用你的紀律，**short put 腿務必單獨核對**，別漏算負 delta 那側。
2. **vs 你現有的 naked call**：naked long call 有 +Δ 但也吃 theta/vega（IV crush 傷你）；補一條 short put 變合成多頭後 → **theta/vega 歸零**，變成純方向工具。若你只想要方向、不想被 vol 侵蝕，合成多頭比裸買 call 乾淨。
3. **NRA / US-situs 提醒**：US equity options 的 US 遺產稅 situs 定性不像現股那麼明確，但 short put 被指派後你會**實際持有 US-situs 現股** → 落回你已在處理的 estate tax 曝險。合成多頭不會讓你繞開這個問題，指派後反而直接觸發。

需要的話，下一步我可以用 TSM 現價幫你抓一組 same-strike vs split-strike 的實際報價對比（含 skew 差、margin 估算、carry），你再決定走哪個變體。

要不要我畫一張三線疊加的損益圖，把「long call + short put = 直線」視覺化？
