# 11-11-2026 TV alert 依 TRENDFN 更新＋FN／VD2A 多空條件整理

> **TL;DR**：
> - 依 [[11-11-2026_TRENDFN_AUTO]] 更新 TV 的 FC 系列 alert：刪 3、建 6、改名 2。首建的 6 條在 TV 端消失（原因不明），已重建並以 get_alerts 驗證 active。
> - 新增 settings allow 規則：`mcp__claude_ai_TradingView__mcp-tv-delete-alert`（user 同意）。
> - SMH 6 條無名 % 漲跌 alert 是 user 11-11 手動刪的（「alert 的確跳出有點多」），已寫入 memory。
> - 整理 SG FN（11/10 場次）與 VD2A（10-11 批 7 卡）的看多／看空條件，見 S_3、S_4。

縮寫：FN＝SG Founder's Note｜PW／HW／CW／KGS＝Put Wall／Hedge Wall／Call Wall／Key Gamma Strike｜RP＝Risk Pivot｜ZG＝Zero Gamma｜DT＝SG data_table｜FC＝FN Checks（追蹤卡代號前綴）｜IV／RV＝隱含／已實現波動率｜ER＝財報｜OPEX＝月選擇權到期｜CTA＝趨勢跟隨基金｜DMA＝日均線

- 來源：`ls_strategy/11-11-2026_TRENDFN_AUTO.md`；`log_gen_by_roma/founders_digest/10-11-2026_founders_{AM,PM}.md`；`log_gen_by_roma/video_digest/10-11-2026/_INDEX_10-11-2026.md` 與 7 張 digest 卡；`spotgamma_report/auto/market_overview/2026_1111_keyLevels.json`（trade_date 11-09）。
- 價格錨：全部為 11/10 收盤讀數（FN／DT），本 session 未另抓現價。
- 對應追蹤卡：`ls_strategy/event_tracking/22-10-2026_SG-FN-long-short-checks_tracking.md` S_2（已同步）。

---

## S_1 TV alert 變更（FC 系列，到期 2026-11-20，全部 auto_deactivate）

### S_1_1 新建（現行 ID）

| 代號 | 條件 | 依據 | ID |
|---|---|---|---|
| FC_S6b | SPX cross_down 7,300 | FN 11-10 AM 主支撐由 7,200 上移 | 6043290632 |
| FC_S5c | SPX cross_down 7,500 | PW（keyLevels td 11-09）；取代已觸發停用的 S5b | 6043290645 |
| FC_H3 | SMH cross_down 475 | DT 11-11 PW；TRENDFN 菜單 B 的 BePS 短腿錨 | 6043290658 |
| FC_T2 | TSM cross 400 | DT 11-11 KGS＝HW＝PW＝400，最大曝險 +91.6% NAV | 6043290675 |
| FC_N2 | NVDA cross_up 180 | DT 11-11 KGS | 6043290686 |
| FC_N3 | NVDA cross_down 150 | FN 11-09 AM 下行目標 | 6043290705 |

- 代號避撞：FC_T1 曾用於 TSLA、FC_S6 曾用於 7,300 PW（11-11 已刪），故用 T2／S6b。
- 首建 ID（6043252712／845／860／875／6043253651／659）在 TV 端被移除，alert log 無線索；已重建。

### S_1_2 刪除
- FC_S7（6031336149，SPX 7,200）→ 由 S6b 接手
- FC_S5b（6039988228，SPX 7,500，11-10 已觸發）→ 由 S5c 接手
- FC_N1（6031335174，NVDA 175，已跌破）→ 由 N2／N3 接手
- 首次刪除被 auto mode 分類器擋（設定檔無 deny 規則）；加 allow 規則後成功。

### S_1_3 改名／改訊息
- FC_H2（SMH > 500 KGS）：PW 由 445 更新為 475，註明 CW 495 < KGS。
- FC_Q4（QQQ < 650 PW）：DT 11-06、11-11 兩個場次一致，兼 BePS 短腿錨。

### S_1_4 未動
- FC_L7（ZG 7,562）：keyLevels 11-11 檔 trade_date 仍為 11-09，ZG 未變。
- FC_L4／L5／L6／C1、VIX 階梯、RVOL、MNQ／MES % alert。
- VIX_L20 不知何時被重新啟用；屬 user 自設，未處理（VIX 19.77 貼線，可能頻繁推播）。

## S_2 其他變更
- `~/.claude-personal/settings.json` 的 `permissions.allow` 加入 `mcp__claude_ai_TradingView__mcp-tv-delete-alert`（原檔備份在 session scratchpad）。
- memory `feedback_tv_pct_alerts_are_mood_gauge`：18 條改為 MNQ／MES 12 條；SMH 6 條為 user 自刪，不回報遺失、不重建。

## S_3 SG FN 多空條件（11/10 AM／PM）

定調：去槓桿已完成、vol premium 已被吃光、盤面「某種程度重置」；但 SPX 在 RP 7,690 下，仍是淨負 gamma。

### S_3_1 看多
- L1 SPX 站上 RP 7,690（Banner：bearish <, bullish >）
- L2 測到 7,700，gamma 才轉正（AM）
- L3 買回三條件任一：(1) 測 7,000 區（Wash Out 7,000–7,100，未發生）(2) 11/17 到感恩節的到期窗口（未到）(3) neocloud 實質事件（CRWV beat、盤後 +3%，部分接近）
- L4 11/18 VIX 到期＝「unlock upside」窗口
- L5 個股 skew 由 put 側轉 call 側＝上檔燃料
- L6 守住 PW 7,500 且 HIRO 0DTE call 流持續（PM 觀察點）
- L7 RV 先降，IV 才能再降

### S_3_2 看空
- S1 7,690 下淨負 gamma，dealer 避險放大波動
- S2 跌破 7,500 → 7,450 → 主支撐 7,300
- S3 7,700 為 NVDA ER／ANT IPO／OPEX 前阻力（非 0DTE call 加碼）
- S4 VIX < SPX 1M RV，vol 收斂推升力道已用完
- S5 數據、NVDA ER、ANT IPO、伊朗變數 ⇒ 不會 full smash
- S6 個股層長天期賣 call（S&P Equities HIRO −599M）
- S7 NVDA 收在 PW 170 下，HIRO −838M 為 30 日最低
- S8 CPI 偏熱，週五 PPI
- S9 Claude Sheets 再點燃 AI 取代軟體敘事（IGV −1.1%、MSFT −2.2%）
- Banner 仍是 11/5 版，水位以正文與 DT 為準。

## S_4 VD2A（10-11 批）多空條件

依 [[feedback_data_source_priority]]，博主觀點只當參考。⚪＝無原始出處。

### S_4_1 看多
- NaNa：週收盤站上 50 週均與 5 週均才算確認（本週五驗）
- 美投轉述 Hartnett：10Y < 4.5%、油 < $80（皆未到：4.86%、WTI 約 86）
- Rhino 轉述 GS CTA：SPX > 7,676 加速買 ⚪（貼近 RP 7,690）
- Rhino NVDA 計畫：132–150 止跌買回 5%、突破 194 買回 3%（博主計畫）
- 游庭皓：NVDA NTM 12.4x ✅；SOX 距 250DMA −0.8%
- Karsan：未延續下跌則可能回 ATH（SPX 距高 −3.4%，未驗）
- Monetary Matters：OPEX 前後 vanna／charm 支撐（與 SG 同源，非獨立證據）
- 寶哥：12 月 SPCX 被動買盤約 $109 億 ⚪
- MS（轉述）：不確定性出清非週期終結 ⚪

### S_4_2 看空
- Rhino 轉述 GS CTA：SPX < 7,084 加速賣，本週全情境賣 ⚪
- Rhino：黃仁勳離職即清倉 NVDA；2027 年 1–2 月財報季為 capex 高風險窗口
- Rhino：CRWV < 37 無支撐（SG PW 35）
- 寶哥：NVDA 支撐 163–170／壓力 196–200；MRVL 破 142、RKLB 46.5 停損
- GS／美銀喊頂 ⚪；Hartnett「SOX 低於 200DMA 17%」為 11/05 讀數，11/09 已 −7.4%
- Karsan：2027 年 6 月前危機 ⚪；離散度創紀錄 ✅
- 「高 skew 半年後大跌」❌（5 段 6 個月報酬全正）
- Sacks：2028 年 DC 管線大縮 ⚪
- Chamath：DC 審批凍結傷 neocloud（事後描述）
- NaNa：QQQ 200DMA 681 下、700 強阻力；SPX 7,600 支撐轉阻力
- NVDA 11/18 閉門簡報（4 個來源，原始報導未核 ⚪）

### S_4_3 交叉
- SG RP 7,690 與 CTA 7,676 幾乎重疊 ⇒ SPX 7,700 一帶是共同分界。
- SG 與 Monetary Matters 都看 11/17–11/20 事件串，但同源，不互證。
- 宏觀觸發（10Y、油）與 2027–2028 capex 時間軸只有博主側，皆無原始出處。
