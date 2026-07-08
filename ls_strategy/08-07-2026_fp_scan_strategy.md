## 21:39:29 — `roma_cli fp_scan 2026-07-08`

🎯 fp_scan 機會掃描（2026-07-08）
   來源：flowpatrol_2026_07_08.pdf
   模式：寬鬆 (cross≥2)   候選 20 sym
════════════════════════════════════════════════════════════
⚪ NVDA  (17 hits / 7 sections)
  [sig_position    ] d= 32th g= 82th v= 98th sector=Technology
  [top_delta       ]  205.00C exp=2026-07-08 d$=-3.10M spread=Short Strangle
  [top_delta       ]  200.00C exp=2026-07-17 d$=-264.38M
  [top_delta       ]  200.00P exp=2026-08-21 d$=-172.10M spread=Short Strangle
  [top_delta       ]  195.00C exp=2026-09-18 d$=+475.62M spread=Long Strangle
  [top_gamma       ]  200.00C exp=2026-07-17 g$=-36.69M
  [top_gamma       ]  195.00C exp=2026-09-18 g$=+18.19M spread=Long Strangle
  [top_vega        ]  205.00C exp=2026-07-08 v$=-3.71K spread=Short Strangle
  [top_vega        ]  200.00C exp=2026-07-17 v$=-402.51K
  [top_vega        ]  200.00P exp=2026-08-21 v$=+478.67K spread=Short Strangle
  [top_vega        ]  195.00C exp=2026-09-18 v$=+1.46M spread=Long Strangle
  [top_vega        ]  210.00C exp=2027-12-17 v$=-401.40K
  [top_vega        ]  220.00C exp=2027-12-17 v$=+368.40K
  [largest_premium ]  195.00C exp=2026-09-18 prem$=+65.92M spread=Long Strangle
  [single_stocks   ]  200.00C exp=2026-07-17 BTO=36,963 BTC=5,471 iv=41.0%
  [single_stocks   ]  195.00C exp=2026-09-18 BTO=42,150 BTC=11 iv=45.2%
  [heavy_daytrade  ] flow_ratio=  7.21 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 跨日無極端 (2/10 報告 d 在 30~70)  d_seq=[33, 32]

🟢 SOXX  (4 hits / 4 sections)
  [unusual         ]  670.00C exp=2026-09-18 vol=71,208 tot_prem=+55.90M → 🟢 BTO 14,543 主導 (100%) → Long Call → bullish
  [top_delta       ]  670.00C exp=2026-09-18 d$=+284.98M
  [top_vega        ]  670.00C exp=2026-09-18 v$=+1.34M
  [largest_premium ]  670.00C exp=2026-09-18 prem$=+55.90M
  F7 unusual  : 🟢 BTO 14,543 主導 (100%) → Long Call → bullish  [conf=high]
  Structure   : ⚪ unknown  (main side=BTO type=C 非 short put/call)
  Greeks 一致 : ✅ d>0 ✓ v>0 ✓
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ TSLA  (7 hits / 4 sections)
  [sig_position    ] d=  0th g=  1th v=  6th sector=Consumer Cyclical
  [top_delta       ]  390.00C exp=2026-07-17 d$=-265.22M spread=Call Spread Open
  [top_delta       ]  400.00C exp=2026-07-17 d$=+143.45M spread=Call Spread Open
  [top_delta       ]  400.00P exp=2026-07-17 d$=+133.14M spread=Put Spread Open
  [top_delta       ]  250.00P exp=2026-07-17 d$=+68.62 spread=Put Spread Open
  [top_gamma       ]  410.00C exp=2026-07-08 g$=+24.48M
  [heavy_daytrade  ] flow_ratio=  9.48 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[7, 0]

⚪ AMZN  (8 hits / 3 sections)
  [top_delta       ]  250.00C exp=2026-07-17 d$=+106.28M spread=Short Straddle
  [top_delta       ]  250.00C exp=2026-08-21 d$=-141.56M
  [top_delta       ]  250.00P exp=2026-08-21 d$=-139.70M spread=Short Straddle
  [top_gamma       ]  250.00C exp=2026-07-17 g$=+17.95M spread=Short Straddle
  [top_gamma       ]  250.00P exp=2026-08-21 g$=+8.97M spread=Short Straddle
  [top_vega        ]  250.00C exp=2026-07-17 v$=+168.60K spread=Short Straddle
  [top_vega        ]  250.00C exp=2026-08-21 v$=-409.21K
  [top_vega        ]  250.00P exp=2026-08-21 v$=+379.09K spread=Short Straddle
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ SMH  (10 hits / 3 sections)
  [top_delta       ]  600.00P exp=2026-07-17 d$=+283.26M spread=Put Roll
  [top_delta       ]  555.00P exp=2026-07-31 d$=-91.33M spread=Put Roll
  [top_delta       ]  545.00P exp=2026-07-31 d$=-142.20M spread=Put Spread Open
  [top_delta       ]  535.00P exp=2026-07-31 d$=+96.12M spread=Put Spread Open
  [top_vega        ]  600.00P exp=2026-07-17 v$=-305.82K spread=Put Roll
  [top_vega        ]  545.00P exp=2026-07-31 v$=+412.10K spread=Put Spread Open
  [top_vega        ]  535.00P exp=2026-07-31 v$=-298.98K spread=Put Spread Open
  [top_vega        ]  555.00P exp=2026-07-31 v$=+246.08K spread=Put Roll
  [largest_premium ]  600.00P exp=2026-07-17 prem$=-28.98M spread=Put Roll
  [largest_premium ]  555.00P exp=2026-07-31 prem$=+11.20M spread=Put Roll
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : 🟡 雙極切換 (4/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[2, 100, 100, 100]

⚪ SPX  (31 hits / 3 sections)
  [top_index       ] 7500.00C exp=2026-07-08 prem$=+1.75M spread=Long Strangle
  [top_index       ] 7540.00C exp=2026-07-08 prem$=-1.78M spread=Call Spread Open
  [top_index       ] 7550.00C exp=2026-07-08 prem$=+1.09M spread=Call Spread Open
  [top_index       ] 7580.00C exp=2026-07-08 prem$=+658.54K spread=Call Spread Open
  [top_index       ] 7640.00C exp=2026-07-08 prem$=-52.03K spread=Call Spread Open
  [top_index       ] 7470.00C exp=2026-07-08 prem$=+2.75M spread=Call Roll
  [top_index       ] 7550.00C exp=2026-07-10 prem$=+2.98M spread=Long Strangle
  [top_index       ] 7495.00C exp=2026-07-10 prem$=-2.85M spread=Call Roll
  [top_index       ] 7525.00C exp=2026-07-10 prem$=-3.24M spread=Short Strangle
  [top_index       ] 5400.00P exp=2026-07-15 prem$=+0.00 spread=Long Strangle
  [top_index       ] 8000.00P exp=2026-07-17 prem$=-464.22M spread=Put Spread Open
  [top_index       ] 7000.00P exp=2026-07-17 prem$=+96.79K spread=Put Spread Open
  [top_index       ] 5200.00P exp=2026-07-28 prem$=+0.00 spread=Short Strangle
  [top_index       ] 7620.00C exp=2026-07-31 prem$=+72.90M spread=Short Strangle
  [top_index       ] 7600.00C exp=2026-07-31 prem$=-40.91M
  [top_index       ] 7650.00C exp=2026-07-31 prem$=-31.07M
  [top_index       ] 7405.00P exp=2026-07-31 prem$=+8.42M spread=Long Strangle
  [top_index       ] 5900.00P exp=2026-08-04 prem$=+0.01 spread=Long Strangle
  [top_index       ] 7300.00P exp=2026-08-21 prem$=+63.91M spread=Short Strangle
  [top_index       ] 7550.00C exp=2026-08-21 prem$=-17.98M
  [top_index       ] 7225.00P exp=2026-09-18 prem$=+50.94M spread=Put Spread Open
  [top_index       ] 7565.00P exp=2026-09-18 prem$=-61.76M spread=Put Spread Open
  [top_index       ] 7565.00C exp=2026-09-18 prem$=+59.29M spread=Short Strangle
  [top_index       ] 5200.00P exp=2026-09-18 prem$=+0.20 spread=Short Strangle
  [top_index       ] 7800.00C exp=2026-09-18 prem$=-16.71M spread=Long Strangle
  [top_index       ] 7125.00C exp=2026-09-30 prem$=-49.61M spread=Long Strangle
  [top_index       ] 7100.00P exp=2026-10-16 prem$=+11.89M spread=Long Strangle
  [top_index       ] 6000.00C exp=2026-12-18 prem$=+107.15M spread=Call Spread Open
  [top_index       ] 7000.00C exp=2026-12-18 prem$=-46.62M spread=Call Spread Open
  [index_etfs      ] 6125.00P exp=2026-08-21 BTO=52,070 STO=7 iv=30.7%
  [heavy_daytrade  ] flow_ratio=  9.75 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ SPY  (6 hits / 3 sections)
  [top_index       ]  757.00C exp=2026-07-15 prem$=+6.50M spread=Call Spread Open
  [top_index       ]  769.00C exp=2026-07-15 prem$=-1.83M spread=Call Spread Open
  [index_etfs      ]  728.00P exp=2026-07-15 BTO=22,261 STO=23 iv=15.2%
  [index_etfs      ]  757.00C exp=2026-07-15 BTO=19,843 STO=2 iv=10.2%
  [index_etfs      ]  769.00C exp=2026-07-15 BTO=75 STO=19,648 iv=9.2%
  [heavy_daytrade  ] flow_ratio= 25.76 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[89, 95]

⚪ TLT  (13 hits / 3 sections)
  [top_gamma       ]   84.50P exp=2026-07-08 g$=+33.08M spread=Put Spread Open
  [top_gamma       ]   85.00P exp=2026-07-08 g$=-9.60M spread=Put Spread Open
  [top_gamma       ]   84.50P exp=2026-07-10 g$=+20.92M spread=Put Spread Open
  [top_gamma       ]   85.00P exp=2026-07-10 g$=-17.35M spread=Put Spread Open
  [top_gamma       ]   84.00P exp=2026-08-21 g$=-19.42M
  [top_gamma       ]   83.00P exp=2026-09-18 g$=+26.12M spread=Put Spread Open
  [top_gamma       ]   80.00P exp=2026-09-18 g$=-10.60M spread=Put Spread Open
  [top_vega        ]   83.00P exp=2026-09-18 v$=+496.08K spread=Put Spread Open
  [top_vega        ]   80.00P exp=2026-09-18 v$=-201.26K spread=Put Spread Open
  [asset_etfs      ]   84.00P exp=2026-08-21 BTO=20,058 STO=285 iv=9.4%
  [asset_etfs      ]   80.00P exp=2026-09-18 BTO=40,293 STO=15 iv=11.3%
  [asset_etfs      ]   83.00P exp=2026-09-18 STO=39,872 STC=8 iv=10.3%
  [asset_etfs      ]   70.00P exp=2027-06-17 BTO=15,000 STO=20 iv=13.1%
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 跨日無極端 (1/10 報告 d 在 30~70)  d_seq=[50]

🔴 WBD  (5 hits / 3 sections)
  [unusual         ]   25.00P exp=2026-10-16 vol=235,714 tot_prem=+2.79M → 🔴 BTO 42,158 主導 (71%) → Long Put → bearish
  [unusual         ]   23.00P exp=2027-03-19 vol=235,714 tot_prem=+2.12M → 🟢 STO 51,060 主導 (84%) → Short Put → bullish
  [top_vega        ]   23.00P exp=2027-03-19 v$=+310.94K
  [single_stocks   ]   25.00P exp=2026-10-16 BTO=42,158 STO=16,900 iv=41.2%
  [single_stocks   ]   23.00P exp=2027-03-19 BTO=10,003 STO=51,060 iv=44.3%
  F7 unusual  : 🔴 BTO 42,158 主導 (71%) → Long Put → bearish  [conf=med]
              ↳ Put Buying（panic / conviction 型）：主動新開空頭，短暫恐慌或強空論點驅動 — 持續性中等，留意反轉
  Structure   : ⚪ unknown  (main side=BTO type=P 非 short put/call)
  Greeks 一致 : —（無 top_delta / top_vega 資料）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ XLF  (6 hits / 3 sections)
  [sig_position    ] d= 22th g= 90th v=  1th sector=Financial ETF
  [top_vega        ]   57.50C exp=2026-07-17 v$=+39.33K spread=Long Strangle
  [top_vega        ]   56.00P exp=2028-01-21 v$=-384.46K spread=Long Strangle
  [asset_etfs      ]   57.50C exp=2026-07-17 BTO=3,151 BTC=14,992 iv=18.1%
  [asset_etfs      ]   40.00P exp=2028-01-21 BTO=1 STO=30,000 iv=24.0%
  [asset_etfs      ]   56.00P exp=2028-01-21 BTO=15,000 iv=14.9%
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[22]

⚪ AAPL  (5 hits / 2 sections)
  [top_gamma       ]  305.00P exp=2026-07-08 g$=+27.19M
  [top_gamma       ]  312.50C exp=2026-07-08 g$=+19.77M spread=Long Strangle
  [top_gamma       ]  320.00C exp=2026-07-10 g$=-19.30M
  [top_gamma       ]  290.00P exp=2026-07-17 g$=+1.89M spread=Long Strangle
  [heavy_daytrade  ] flow_ratio=  8.24 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 偶發極端 (1/10 報告，未過半)，雜訊概率高  d_seq=[24]

🔴 BP  (4 hits / 2 sections)
  [unusual         ]   42.00C exp=2026-09-18 vol=126,840 tot_prem=+3.05M spread=Call Spread Open → 🔴 STO 29,911 主導 (100%) → Short Call → bearish  [SG:Call Spread Open]
  [unusual         ]   50.00C exp=2026-09-18 vol=126,840 tot_prem=+262.10K spread=Call Spread Open → 🟢 BTO 30,000 主導 (100%) → Long Call → bullish  [SG:Call Spread Open]
  [single_stocks   ]   42.00C exp=2026-09-18 BTO=59 STO=29,911 iv=28.9%
  [single_stocks   ]   50.00C exp=2026-09-18 BTO=30,000 STO=21 iv=33.0%
  F7 unusual  : 🔴 STO 29,911 主導 (100%) → Short Call → bearish  [SG:Call Spread Open]  [conf=high]
              ↳ Call Selling（distribution 型）：持有者放棄上行保護，delta hedge 形成穩定賣壓 — 下跌持續性強
  Structure   : 🔴 bear_call_spread  (sibling 50C BTO (100% main) → 賣低買高 call 信用價差)
  Greeks 一致 : —（無 top_delta / top_vega 資料）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

🟡↘ CLF  (3 hits / 2 sections)
  [unusual         ]   12.00C exp=2026-08-21 vol=38,722 tot_prem=+605.13K spread=Call Vert Debit → 🟡↘ STC 19,496 主導 (99%) → Close Long Call → neutral_bearish  [SG:Call Vert Debit]
  [unusual         ]   11.00C exp=2026-08-21 vol=38,722 tot_prem=+550.98K spread=Call Vert Debit → 🟢 BTO 10,639 主導 (99%) → Long Call → bullish  [SG:Call Vert Debit]
  [single_stocks   ]   12.00C exp=2026-08-21 STO=100 STC=19,496 iv=81.0%
  F7 unusual  : 🟡↘ STC 19,496 主導 (99%) → Close Long Call → neutral_bearish  [SG:Call Vert Debit]  [conf=high]
  Structure   : ⚪ unknown  (main side=STC type=C 非 short put/call)
  Greeks 一致 : —（side=STC/type=C 不在支援組合）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ IWM  (4 hits / 2 sections)
  [top_gamma       ]  274.00P exp=2026-07-08 g$=+0.00 spread=Put Roll
  [top_gamma       ]  300.00C exp=2026-07-08 g$=+21.79M
  [top_gamma       ]  294.00P exp=2026-07-10 g$=-25.79M spread=Put Roll
  [heavy_daytrade  ] flow_ratio= 13.57 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ META  (4 hits / 2 sections)
  [top_vega        ]  550.00P exp=2026-08-21 v$=-83.64K spread=Long Strangle
  [top_vega        ] 1200.00C exp=2028-06-16 v$=+304.18K
  [top_vega        ] 1310.00C exp=2028-12-15 v$=+517.20K spread=Long Strangle
  [heavy_daytrade  ] flow_ratio=  7.16 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ MTUM  (2 hits / 2 sections)
  [top_delta       ]  310.00P exp=2026-07-17 d$=+171.61M
  [top_gamma       ]  310.00P exp=2026-07-17 g$=-20.88M
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ NDX  (2 hits / 2 sections)
  [top_index       ] 29850.00C exp=2026-07-10 prem$=+5.14M
  [heavy_daytrade  ] flow_ratio= 23.71 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

⚪ QQQ  (3 hits / 2 sections)
  [largest_premium ]    3.00C exp=2026-07-09 prem$=-99.95M spread=Short Strangle
  [largest_premium ]  695.00P exp=2026-07-09 prem$=-182.29K spread=Short Strangle
  [heavy_daytrade  ] flow_ratio= 24.85 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : ⚪ 偶發極端 (2/10 報告，未過半)，雜訊概率高  d_seq=[97, 97]

⚪ XLE  (3 hits / 2 sections)
  [top_vega        ]   55.00P exp=2027-12-17 v$=+401.29K
  [asset_etfs      ]   55.00P exp=2027-01-15 BTO=16,002 STO=2 iv=22.8%
  [asset_etfs      ]   55.00P exp=2027-12-17 STO=16,000 iv=20.7%
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : 🟡 雙極切換 (2/10 報告觸 d≤30 與 d≥70)，事件驅動高 IV  d_seq=[86, 7]

⚪ XSP  (8 hits / 2 sections)
  [largest_premium ]  749.00P exp=2026-07-09 prem$=-27.88M
  [largest_premium ]  690.00P exp=2026-07-17 prem$=-34.19M spread=Put Roll
  [largest_premium ]  700.00P exp=2026-07-29 prem$=+109.75M
  [largest_premium ]  775.00P exp=2026-08-21 prem$=+51.64M spread=Put Roll
  [largest_premium ]  720.00P exp=2026-08-28 prem$=-225.13M
  [largest_premium ]  645.00P exp=2026-12-18 prem$=-103.68M spread=Put Spread Close
  [largest_premium ]  585.00P exp=2026-12-18 prem$=+94.04M spread=Put Spread Close
  [heavy_daytrade  ] flow_ratio=  6.33 (HFT 主導)
  F7 unusual  : —（無 unusual 段命中或無 trade-side 資料）
  Structure   : ⚪ unknown  (F7 conf 不足或無解碼)
  Greeks 一致 : —（無 F7 解碼）
  F8 sig 跨日 : —（聚合無紀錄或 sig_position 未上榜過）

════════════════════════════════════════════════════════════
摘要：20 候選 / 0 教科書級
────────────────────────────────────────────────────────────
🏷️  F12 Cross-day IC / Strangle 賣方收斂結構（掃描 10 日）
────────────────────────────────────────────────────────────
📌 FXI
   雙側 STO：賣 33C（1日）+ 賣 31P（1日）（prem 資料缺失，無法確認賣方收 prem）
   G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [4, 0, 0, 0, 0, 0, 0, 0]）→ 鋪倉完成
   建議 IC：sell BeCS ≤33C + sell BuPS ≥31P
   現價 $32.52，在區間 [31~33] 的 76th 百分位
   ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

📌 NU
   雙側 STO：賣 18C（1日）+ 賣 12P（1日）（prem 資料缺失，無法確認賣方收 prem）
   G3 建倉狀態：✅ 鋪倉完成  近 1 日未上榜（counts: [4, 0, 0]）→ 鋪倉完成
   建議 IC：sell BeCS ≤18C + sell BuPS ≥12P
   現價 $13.67，在區間 [12~18] 的 28th 百分位
   ⚠️ 機構已建倉，確認方向後跟進；避免把 STO 負 delta 誤讀為純看空

