(python3) ojy@e67-4b1:~/ongtradingsys/spotgamma_report$ roma_cli fp_alpha all sort=fair asc
[####################] 100.0%  彙整  (8s)
🎯 FP Alpha 掃描  資料日 2026-08-14 🟡age=2td  範圍 49 sym（持倉∪估值表）  排序: 距合理目標 asc
🟡 FP age=2td（偏舊）：資料截至 2026-08-13 收盤（此檔 publish=2026-08-14）、非 live tape；如需同日水位見 data_table
🎯 *FP Alpha Candidates*（估值入區 × FP 機構訊號）  共 49 筆
══════════════════════════════════════════════════════════════════════

🟡   C 級觀察（估值入區，FP 無有據方向訊號）
  🟡 C_watch  AGIX $46.68 (等待區)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +11.4%
  🟡 C_watch  LIN $482.74 (等待區)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +13.1%
  🟡 C_watch  AVGO $392.99 (等待區)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +14.8%
  🟡 C_watch  FN $570.22 (等待區)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +15.4%
  🟡 C_watch  AMZN $262.65 (等待區)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 +27.2%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_delta:C245)
  🟡 C_watch  NVDA $225.16 (等待區)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 +27.5%
     ⚪ 註記(不計分) top_*[call×3/put×0] → overheat_short_term (top_delta:C240/top_gamma:C227/top_vega:C240)
  🟡 C_watch  SNPS $421.50 (等待區)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +29.8%
  🟡 C_watch  CRM $196.21 (超跌)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +36.1%
  🟡 C_watch  META $589.85 (等待區)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 +40.5%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_vega:C930)
  🟡 C_watch  LLY $1180.16 (超跌)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +47.0%
  🟡 C_watch  ORCL $150.52 (超跌)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +48.8%
  🟡 C_watch  NFLX $78.16 (超跌)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +52.3%
  🟡 C_watch  INTU $345.66 (超跌)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +57.7%

⚪   參考（估值高於等待區）
  ⚪ skip_above_zone  PANW $384.27 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -51.9%
  ⚪ skip_above_zone  INTC $102.50 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -51.2%
  ⚪ skip_above_zone  CRWD $216.95 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -51.1%
  ⚪ skip_above_zone  KLAC $203.72 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -31.8%
  ⚪ skip_above_zone  GLW $165.99 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -30.1%
  ⚪ skip_above_zone  AMAT $507.18 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -28.8%
  ⚪ skip_above_zone  MDB $460.33 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -27.2%
  ⚪ skip_above_zone  LRCX $332.36 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -27.2%
  ⚪ skip_above_zone  AMD $514.39 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -24.8%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_delta:C570)
  ⚪ skip_above_zone  TER $418.79 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -24.5%
  ⚪ skip_above_zone  ASML $1844.08 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -21.3%
  ⚪ skip_above_zone  LITE $926.14 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -17.4%
  ⚪ skip_above_zone  ANET $198.82 (估值偏高)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -17.0%
  ⚪ skip_above_zone  SOXX $550.42 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -16.6%
  ⚪ skip_above_zone  SNOW $328.92 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -14.9%
  ⚪ skip_above_zone  IWM $305.09 (偏樂觀)  FP=+0 (0🟢/0🔴/2⚪)  距合理目標 -11.8%
     ⚪ 註記(不計分) top_*[call×2/put×1] → overheat_short_term (top_delta:C307/top_gamma:P300/top_vega:C307)
     ⚪ 註記(不計分) sig_position:d=16th → observe（買/賣軸實測零前瞻方向性·v3.66 拔軸）
  ⚪ skip_above_zone  IGV $104.08 (偏樂觀)  FP=+0 (0🟢/0🔴/2⚪)  距合理目標 -11.6%
     ⚪ 註記(不計分) top_*[call×0/put×1] → downside_priced_in (top_vega:P85)
     ⚪ 註記(不計分) unusual[call×0/put×1] → downside_priced_in
  ⚪ skip_above_zone  DDOG $255.46 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -8.8%
  ⚪ skip_above_zone  SMH $587.82 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -8.3%
     ⚪ 註記(不計分) top_*[call×0/put×1] → downside_priced_in (top_gamma:P575)
  ⚪ skip_above_zone  AAPL $305.93 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -7.2%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_gamma:C305)
  ⚪ skip_above_zone  SPY $776.34 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -7.1%
     ⚪ 註記(不計分) sig_position:d=6th → observe（買/賣軸實測零前瞻方向性·v3.66 拔軸）
  ⚪ skip_above_zone  NOK $10.76 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -6.1%
  ⚪ skip_above_zone  MRVL $222.02 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -5.9%
  ⚪ skip_above_zone  PLTR $174.04 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -5.8%
  ⚪ skip_above_zone  WDAY $198.68 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -5.4%
  ⚪ skip_above_zone  QQQ $731.07 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -5.3%
     ⚪ 註記(不計分) sig_position:d=100th → observe（買/賣軸實測零前瞻方向性·v3.66 拔軸）
  ⚪ skip_above_zone  NOW $124.00 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -3.2%
  ⚪ skip_above_zone  MSFT $495.40 (偏樂觀)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 -2.9%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_delta:C382)
  ⚪ skip_above_zone  GOOG $343.54 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -2.5%
  ⚪ skip_above_zone  QCOM $165.79 (偏樂觀)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 -0.5%
  ⚪ skip_above_zone  COHR $325.83 (等待區之上)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +2.8%
  ⚪ skip_above_zone  MU $971.66 (等待區之上)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 +3.7%
     ⚪ 註記(不計分) top_*[call×1/put×0] → overheat_short_term (top_vega:C1300)
  ⚪ skip_above_zone  ETN $451.51 (等待區之上)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +5.9%
  ⚪ skip_above_zone  MNDY $87.52 (等待區之上)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +6.3%
  ⚪ skip_above_zone  VRT $293.84 (等待區之上)  FP=+0 (0🟢/0🔴/0⚪)  距合理目標 +10.3%
  ⚪ skip_above_zone  TSM $426.35 (等待區之上)  FP=+0 (0🟢/0🔴/1⚪)  距合理目標 +12.3%
     ⚪ 註記(不計分) top_*[call×0/put×1] → downside_priced_in (top_delta:P460)
══════════════════════════════════════════════════════════════════════
⚪ 註記＝**不計分**。v3.66 起 FP 的買/賣軸（BTO·C/STO·P… 與 sig_position 的 delta_pct）實測**零前瞻方向性**（同為 CALL 時 BUY·C 43.9% vs SELL·C 43.8%），四個方向來源全部拔除 ⇒ FP score 恆 0、分級只會落在 C/⚪。
   overheat_short_term＝call 側為主（列層級後續偏弱，但標的層級不顯著）；downside_priced_in＝put 側為主，**不是看空**（實測 put 側前瞻為正）；observe＝無偏側或該軸無前瞻依據。
(python3) ojy@e67-4b1:~/ongtradingsys/spotgamma_report$