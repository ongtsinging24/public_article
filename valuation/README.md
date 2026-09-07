# ROMA Valuation Tracker

估值追蹤子目錄，記錄 FY2026/FY2027 大盤、板塊、個股的 EPS 與目標價。

## 檔案結構

| 檔案 | 內容 |
|------|------|
| `index_valuation.md` | 大盤指數估值（SPX / NDX / RUT） |
| `sector_valuation.md` | 11 個板塊 EPS 增速與輪動觀察 |
| `stock_valuation.md` | 個股追蹤：EPS / 目標價 / 建倉建議 |
| `methodology_NTM_blend.md` | **估值方法論：NTM blend forward window**（套到 ANA / SAVEST 必讀） |
| `valuation_log/` | 個股估值更新記錄（pre/post earnings、initial valuation） |

## 方法論（必讀）
做 ANA / SAVEST / 加倉評估前，先理解：
- 📐 **[NTM Blend Forward Window](methodology_NTM_blend.md)**
  - 業界主流：股市 forward-look 9–12 個月（NTM 慣例）
  - 公式：`NTM_EPS = weight_FY1 × FY1_EPS + weight_FY2 × FY2_EPS`，權重 = 剩餘季數 / 4
  - 給三檔目標價：current FY（短線錨）/ NTM blend（市場真實定價）/ FY+1（樂觀 stretch）
  - 適用：高成長 SaaS / risk-on / FY 後半段
  - 不適用：強週期 / risk-off / 重組中 → 退回 TTM
  - 各標的 fiscal year 結束月對照表見 §8

## 更新原則
- 財報季後（Q1/Q2/Q3/Q4）更新個股實際 EPS，同步修正全年預估
- 重大事件（Fed 決策、關稅政策）後更新大盤與板塊估值
- 每次更新在檔案頂端加 `## 更新記錄` 行（日期 + 修改項目）
- 個股估值表 `base_eps` 應使用 **NTM blend EPS**，不是粗暴的 current FY；FY 進度大於 50% 時必須切換到 FY+1 主導
  - 刻意不用 NTM blend 的卡（如 NVDA 錨 FY27）必須在 META 標 `base_eps_basis=FY27` 聲明；
    未聲明的口徑不一致由 `val_audit` 的 🟠 `BASIS_MISMATCH` 抓（methodology §15.6）
- 資料源守門（`eps_source` / `feed_reject` / `anchor` / `net_cash` 四個 META 欄）見 methodology **§15**；
  ★ 通則：**幅度最大的重估提案，最需要先懷疑資料源而不是市場**
- 更新後 git commit（在 romasys/ 內執行）
