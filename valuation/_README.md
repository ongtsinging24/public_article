# val_watch — 估值入區觀察清單（`roma_cli val_watch`）

**v4.85（2026-09-08）正名前為 `log_gen_by_roma/fp_alpha/`。**

## 這個目錄裡是什麼
`[dd-mm-yyyy]-val-watch.md`，每次執行 `roma_cli val_watch [all] [sort=fair|score] [asc|desc]`
自動落檔（覆寫模式，同日重跑只留最新一份；檔名日期取**執行日**非 FP 報告日）。

## ⚠️ 這不是機構流量報告
選標的的是**估值軸**（`valuation/stock_valuation.md` 的 zone × `pct_to_fair`）。
FlowPatrol 在這裡**只貢獻一個布林事實**：摘要行的 `FP⚪N` ＝「這檔今天有沒有出現在 FP 榜」，
**不含方向、不參與排序、不參與分級**。

理由是自家實證：v3.66（2026-07-31）拔掉四個 FP 方向來源、v4.24（2026-08-19）再推翻 C/P 軸
⇒ `fp_score ≡ 0` ⇒ grade 只可能落 `C_watch` 🟡 / `skip_above_zone` ⚪。
**整張榜全是 C／⚪ 是結構性後果，不是「今天沒訊號」。**

休眠 grade `A_dir_confirmed` / `B_dir_confirmed` / `D_dir_adverse` 需要 `fp_score ≠ 0`
才走得到，而那要先有**通過前瞻檢定的方向源**。

## 要機構流量維度請走別的指令
`roma_cli fp_scan` 或 FlowPatrol g$ 明細（`FP_TODAY` / `FP_TREND`，資料在 `spotgamma_report/auto/flowpatrol/`）。

## 舊目錄
`log_gen_by_roma/fp_alpha/` 保留正名前的歷史產出，**原地凍結、不再新增**。

出處：`romasys/document/ROMA_CHANGE_LOG.md` v4.85、
`romasys/document/ROMA_SIGNAL_DESIGN.md#H1_F11-`、
`romasys/src/opportunities/sg_signals/flowpatrol/alpha.py` 檔頭。
