# SpotGamma 教學 Digest — 0DTE 機制全解（7 片合併）

> 來源逐字稿（`knowledge/edu/`，2022-11 ~ 2026-02，Brent Kochuba）：
> - The Risk in 0DTE (Short-Dated Options Volume)（2022-11-16，11min，奠基片）
> - How 0DTE Options Move Markets（2023-02-23，5min）
> - 0DTE SEEK AND DESTROY（2025-09-08，6min，seek-and-destroy algo）
> - The Illusion of Support from 0DTE Options（2026-01-06，2min）
> - 0DTE Triggers Crashes（2026-02-03，3min）
> - 0DTE STICKY STRIKES（2025-12-12，2min）
> - +90% of Options Volume is Noise（2026-02-22，<1min teaser）
> **性質**：evergreen 機制框架（0DTE 如何驅動盤中價格），非時效水位；引用的具體 % / 日期屬當時觀察。整理日 2026-06-14。

## 縮寫
- 0DTE = zero days to expiration（當日到期超短天期期權）｜OI = open interest（未平倉）｜GEX = 做市商 gamma 曝險｜HIRO/hero = SG 即時對沖流工具（每筆成交的對沖壓力）｜TRACE = SG 大倉位地貌（每 10 分鐘更新，顯示大 0DTE 倉位在哪）｜teal/purple = hero 中 0DTE flow（teal）vs 全到期 flow（purple）｜weaponized gamma = 用大量 0DTE call 逼做市商被動買股｜JPM strike = JP Morgan collar put strike（不到期不消失的真 gamma 磁吸）

## 一、0DTE 是什麼、有多大（奠基片 2022 + Noise teaser）
- **定義**：當日（或數日內）到期的超短天期期權。2022 起 SPX / SPY / QQQ 每日都有到期，個股（TSLA/AAPL）每週五到期 → 交易集中往最短天期擠。
- **量能**：占總期權量 ~50%（一週內到期），SPX 單日 0DTE 占比常 >40%，2025 多次破 60%，2025-09 創 69.91% 高。
- **關鍵：量大但不轉成 OI** → 這是 **day-trading flow**，早上開倉、收盤前平掉。Noise teaser 實例：687k 0DTE 成交僅造成 6k 合約的 absolute OI change（flow ratio 107% = 「巨量 flow，零實際客戶持倉變化」）。
- **誰在做**：JPM 估 retail 僅占 0DTE 的 10–15%，**其餘是機構**（非「散戶在媽媽地下室」）。
- **為何做 0DTE**：①賣短天期吃 IV premium / 相對 theta decay 快（condor/straddle/call spread）②做市商精細動態對沖 ③當 futures/stock 的 delta 替代（省 margin 的槓桿 hedge）④低成本槓桿方向投機 ⑤weaponized gamma（買大量 0DTE call 逼 dealer 買股）。

## 二、0DTE 如何驅動盤中價格（How 0DTE Move Markets 2023 + Seek & Destroy 2025 + Sticky Strikes 2025）
- **乒乓盤（ping-pong）**：盤中在區間上下打。green/hero line（0DTE 對沖流）是**領先指標**——flow 先動、價格後跟。早上買 put 壓低 → 在低點蓋 put 改買 call → 推升 → 到區間頂負 delta flow 進場止漲。**net 效果常是「收斂/壓抑」波動，而非放大**。
- **Seek-and-Destroy algo**（2025 已成日常）：盤中 hero flow 上行 = call 買進 / put 賣出，市場壓力被「抬起」。配合 TRACE 找 **99th percentile strike**（巨型 strike = magnet target）。algo 持續買到「目標達成」才停（實例：午後到收盤吸 ~10–11 億 delta，把 SPX 釘在 6500）。teal≈purple 證明純 0DTE。
- **Sticky strikes**：大 0DTE 倉位（如賣出的 put spread，dealer 接走）會讓價格在該 strike「磁吸/反應」——市場碰到就停/彈。倉位「這一秒在、下一秒消失」，必須盤中盯 TRACE 看倉位演變。

## 三、0DTE 的真正風險：穩定是幻象（Illusion 2026 + Triggers Crashes 2026 + 奠基片）
- **Illusion of support**：銀行報告說「今天有 $4B 正 gamma」——那只是**今日到期**的 gamma。把今日到期剔除（GEX − next exp），剩下常是**負的**。這個正 gamma 是 transient：盤中 9:30→收盤會大幅漂移，且當晚到期就歸零。
- **壞消息來時 0DTE 不會救你**：開盤前一條壞 headline / 數據 / 推文 / 地緣事件，0DTE positioning 還沒進場 → 沒有「0DTE 撐盤」這回事。對比 **JPM collar strike**：到 3 月到期前都在、不管發生什麼都可數，那才是可依靠的真 gamma。
- **Triggers Crashes（結構性不穩）**：現在「sum the gamma」幾乎全部 gamma 都來自 0DTE。看似 rolling 基礎上每天有穩定 gamma（隔天再賣 put 補上），但**只要某天他們不賣 / 賣太便宜被軋**，gamma 瞬間消失 → 市場直接塌。三年前是賣一個月 call、gamma 卡到月度到期不動；現在全是 0DTE，inherently unstable。
- **奠基片宏觀風險**：option 量創高 + ES 期貨等底層流動性創低 → 同樣 notional 對沖造成更大衝擊（要吃更多價差成交）→ **flash crash 機率上升**。SG 定調這是 **market-structure issue（槓桿過度），非投資議題**；Goldman 同期亦背書。

## 四、ROMA 對照重點
- **「剔除今日到期看真 gamma」應內建為訊號層**：ROMA 的 GEX/gamma 解讀不可只看當日總 gamma，要算 **GEX − next-expiration**；若剔除後轉負 → 標記「support 為 0DTE 幻象、結構脆弱」，提高 severity（呼應核心任務「避開像 2026/06/05 大跌」）。
- **TRACE 99th-percentile strike = 盤中 magnet target**；hero teal vs purple 判斷是否純 0DTE 驅動 → 對應 SG_MARKET_LEVEL / ROMA opportunities（wall_signals / flowpatrol）。
- **JPM collar strike 是唯一可依靠的真 gamma 磁吸**，0DTE 撐盤不可依靠 → 與 recent 系列 [[digest_SpotGamma_opex-live-series]]、[[digest_SpotGamma_iran-crisis-vol-mechanics-2026]] 的 JPM collar 論點一致；ROMA 區分「結構性 wall」vs「transient 0DTE flow」。
- **0DTE 是壓抑波動 vs 觸發崩盤的雙面性**：平日 net 收斂 vol（乒乓盤），但壞消息 + flow 缺席 = 正回饋下殺 → ROMA scan 應把「0DTE 占比極高 + GEX 剔今日後負」列為脆弱旗標。
- **flow ratio ≫100% 但 OI 幾乎不變 = 純 day-trading noise**：判讀 flow 時先看 OI change，避免被巨量 0DTE flow 灌水誤判機構建倉；呼應 [[feedback_13f_is_lagging_not_entry_signal]] 與 [[feedback_pct_to_fair_decompose]] 的「先查框架/數據真實性」紀律。

> 連結：[[_INDEX_SpotGamma_edu]]、[[digest_SpotGamma_key-levels-series-1to7]]（vol trigger / wall）、[[feedback_squeeze_entry_dual_trigger]]。
