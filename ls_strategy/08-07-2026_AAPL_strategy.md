# AAPL 機構動向深挖 + 策略（TREND）

- 分析日：2026-07-08（台北 11:03，美股未開盤）
- 現價錨：**$310.66**（2026-07-07 收盤，yfinance）
- 持倉狀態：無 AAPL 持倉
- 資料源：FP logs（06-24 → 07-07）、ROMA scan `scan_section/08-07-2026_AAPL_scan_result.md`、關聯：[[08-07-2026_TRENDFP.md]]

**縮寫**：RR=Risk Reversal；CW/PW=Call/Put Wall；DR=Delta Ratio；IVR=IV Rank；VRP=Vol Risk Premium（IV−RV）；synthetic long=買 call + 賣 put 同履約價合成多頭；ITM/OTM=價內/價外；d$=Delta 美元曝險

**口徑校正**（依 [[kb_flowpatrol-eod-plus1-delivery-vs-datatable-sameday]]：FP 檔名日=該 session 收盤、px 欄位=PrevClose by design）：FP 07-07 報告的流量 = **07-07（週二）session**；px=312.81 顯示的是 07-06 前收。07-07 實際收 310.66（-0.65%）——即 **99th 分位極端流發生在回吐日，機構是在買回檔**。

---

## 一、FP 流量時間軸：從砍倉到 All-in（6/24 → 7/7）

```
報告日   px      關鍵流量                                  解讀
06-24   294    310C 7/17 BTO 27.7k                        追多
06-26   275    320C 9/18 STC 22.1k、350C STC 20.2k        ← -6.2% 大跌日
                                                            砍光 9 月上檔
06-30   284    285/280C vert credit                       跌後賣壓性 overwrite
07-01   282    280/300C 7/17 call spread 開倉 (+$87M d$)   低點回補上檔
07-02   289    320C 9/18 vega +$308k                      重新買回 9 月 call
07-03   308    350C 9/18 BTO vega +$765k                  加碼更高履約價
07-07   313    ★ 290C+290P 8/03 synthetic long            全劇本高潮
               call BTO prem $52.3M / put 賣方 prem -$6.3M
               d$ 合計 +$610M（99th 分位）
               同時 320C 7/31 賣出 -$92.6M
```

機構在 6/26 大跌日**恐慌性清掉 9 月 call**，7/1 起用四個交易日**逐步買回並升級部位**——最終形態是 **8/03 到期 290 synthetic long（深度 ITM 合成股票）**，非裸買 OTM call。

## 二、為什麼是 synthetic long？結構選擇即訊息

ROMA /vol 背景：
- **IVR 75%、近月 IV > 遠月（backwardation）→ 財報後 IV crush 高確定性**
- 財報 ~**07-30**，部位到期 **08-03 = 財報後第一個到期**，且 ROMA levels 顯示 8/03 為全鏈**最大 Delta 到期日**——兩邊資料互相印證，即該筆 combo。

機構結構三段：
1. **買深度 ITM 290C**（幾乎純 delta、時間價值少）→ 吃方向、不吃 IV crush
2. **賣 290P** → 收權利金、再加 delta（承擔下行義務 = 信念強）
3. **賣 320C 7/31**（-$92.6M d$）→ 賣掉財報前最貴的 OTM vol，320 剛好是 Call Wall

翻譯：**「我要財報的方向上行，但我不付 vol 的錢——反而把貴的 vol 賣回給你」**。專業級 pre-earnings 多頭表達。

## 三、ROMA 系統面：結構偏多 vs 估值極差的對撞

| 維度 | 讀數 | 方向 |
|------|------|------|
| GEX 制度 | +$458M 中正 gamma，CW $320 pin 強度 83/100 | 短線釘價 320 |
| 反彈品質 | 🟢 flow-supported（GR 1.3→2.1、CW 300→320 上移） | 多方有燃料 |
| DR 趨勢 | 4.4→6.0（+35%），7/6 DR=10.45（synth 異常標記） | 極端 call 主導 |
| IV 訊號 | IVR 75% + term 倒掛 → 系統打 -2「crash mode」 | ⚠️ |
| VRP | -10.3pt（RV 39% > IV 29%） | vol 沒補償尾部 |
| Layer 0 估值 | Base $267（-14%）/ Bull $336（+8%）/ Bear $156，R:R=0.16 | 🔴 極差（陳舊 60 天，7/30 後須重估） |
| 綜合裁決 | ⬜ 中性・多層矛盾・低可信度 | 觀察 |

**ROMA 的矛盾正是市場的矛盾**：flow 全面偏多且自我強化，但價格在合理估值上方 16%、左尾保護買盤明顯（年化 skew +9.1pt）、07-07 sig_position 99th 分位 = 擁擠度極限。

## 四、綜合判讀

1. **短線（本週）**：正 gamma + CW $320 強 pin → 大概率 310–320 區間磨；日 1σ $307–318、週 1σ $300–326。突破需站穩 320 才打開（CW 再上移是最好的確認訊號）。
2. **財報窗口（7/30 前後）**：機構已用最優結構押注財報上行，方向參考價值高；但 99th 分位擁擠是雙面刃——**財報不及預期時，+$610M delta 解倉本身就是下跌燃料**，Bear 情境估值遠在下方（$156）。
3. **與 [[08-07-2026_TRENDFP.md]] 對照**：AAPL 是「melt-up with a seatbelt」裡跑最快的，seatbelt（320C 賣出、skew 保護）也繫得最緊。

## 五、行動方案（目前無持倉）

- ❌ **不建議**：裸買 OTM call（IVR 75% + 倒掛，crush 吃掉方向利潤）；現價直接追股票（高於 ROMA 等待區 $240、估值 R:R 0.16）。
- ✅ **結構上可行**（模仿機構、風險有限）：**Aug 290/320 call vertical**（買 ITM 賣 CW；delta 正、vega 近中性、320 pin 反而有利）；或等 **320 突破站穩**後的動能單，近端止損 $315 一線。
- 🅿️ **保守**：按 ROMA 裁決觀察，7/30 財報後 Layer 0 重估（現已陳舊 60 天）再決定；EVC 拉最新合理區間交叉驗證。

## 追蹤點

- [ ] 290C/290P 8/03 OI（各 ~22k 口）後續增減 — 機構加碼或撤退的直接指標
- [ ] Call Wall 是否從 $320 再上移（多方燃料確認）
- [ ] 7/17 opex：280/300C spread、310C 到期處理
- [ ] 7/30 財報：方向驗證 + IV crush 兌現；財報後重估 Layer 0
- [ ] sig_position d% 從 99th 回落的速度（擁擠度釋放 vs 解倉）
