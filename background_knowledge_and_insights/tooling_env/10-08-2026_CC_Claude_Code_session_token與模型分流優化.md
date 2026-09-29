# Claude Code Session Token 與模型分流優化

> **定位**：本篇是 2026-08-10 對這台機器本機保留之 Claude Code session JSONL 的操作稽核。Token 是 API 回傳 usage 欄位的累計處理量，**不是帳單金額，也不是訂閱 quota**；已刪除及其他機器上的 session 不在樣本內。由於不同模型與 cache 類型的計價權重不同，raw token 只能用來找 context 熱點，不能直接比較成本。

---

## 一、縮寫對照

- **CC** = Claude Code
- **FP** = FlowPatrol
- **FN** = Founders Note
- **KB** = Knowledge Base
- **RCA** = Root Cause Analysis，根因分析
- **SSOT** = Single Source of Truth，單一真相來源
- **RTK** = Rust Token Killer，CLI 輸出壓縮代理
- **Fresh tokens** = regular input + cache creation input + output；本篇為方便診斷自訂的操作指標，不是官方計費項目

---

## 二、理論框架

Claude Code 的 raw token 消耗可拆成四類：

1. regular input；
2. cache creation input；
3. cache read input；
4. output。

實務上有三種不同的優化問題，不能混為一談：

- **要降低 raw processed tokens**：主要縮短 session context、避免無關主題同居、限制多 agent 重讀同一 corpus。
- **要降低 model-weighted cost／quota**：把機械工作從 Opus 下放至 Sonnet／Fable／Haiku，Opus 只做高價值裁決。
- **要降低工具輸出帶入 context**：使用 targeted grep、分段讀檔與 RTK；但若這一層已高度優化，邊際改善會低於 session hygiene。

核心假說：當 cache read 佔壓倒性多數時，真正瓶頸不是最終回答太長，而是每次 tool round-trip 都反覆攜帶一個過大的 context。此時**切 session 比單純換 model 更能降低 raw token**；換 model 的主要效果則是降低成本權重，兩者應同時做但不可混稱。

---

## 三、實驗設計

### 3.1 資料與去重口徑

- **資料源**：`~/.claude/projects/**/*.jsonl`
- **快照基準**：主稽核於 2026-08-10 10:26 GMT+8；腳本重跑時數字會隨 session 繼續活動而增加
- **邏輯 session**：將 `session-id/subagents/*.jsonl` 歸入同一 parent session
- **去重**：同一 logical session 內，以 assistant `message.id` 去除 streaming snapshot 重複，只保留 usage 最大的紀錄
- **統計欄位**：`input_tokens`、`cache_creation_input_tokens`、`cache_read_input_tokens`、`output_tokens`
- **限制**：本地留存偏差、不同模型計價差異、cache read 與 fresh token 成本不可等權視之

### 3.2 同條件比較基準

本篇不用「50%」作無意義基準，而採三個同條件基準：

1. **全機器 usage mix**：比較各 token 類型占全體比例；
2. **session 間 fresh-token share**：避免只因 cache read 大就誤判成本熱點；
3. **同一高耗用 session 內的 model/call/task 結構**：辨識是否由 model 過度配置或 context 混題造成。

### 3.3 不確定性與 CI

這不是隨機抽樣，而是本機留存 session 的 census，因此不對「本機保留資料本身」估抽樣 CI。也不能把結果外推到未保留、其他機器或未來工作負載；若要量化政策效果，需執行前後期或 A/B 工作流實驗，附每任務 token／成本分布及 bootstrap CI。

---

## 四、結果表

### 4.1 全機器主快照

主快照掃到 33 個 logical sessions、1,645 個 unique assistant calls：

| 類型 | Tokens | 佔比 |
|---|---:|---:|
| Cache read input | 146,361,935 | **87.14%** |
| Regular input | 11,040,128 | 6.57% |
| Cache creation input | 9,008,517 | 5.36% |
| Output | 1,556,871 | **0.93%** |
| **合計** | **167,967,451** | **100%** |

排除 cache read 後，fresh tokens 為 21,605,516（raw total 的 12.86%）。因此：

- 把回答再縮短只能碰到不到 1% 的 output；
- 最大 raw-token 槓桿是 context 重讀；
- raw total 與 fresh-token ranking 必須並看。

### 4.2 Project 分布

| Project | Tokens | 全部佔比 |
|---|---:|---:|
| `ongtradingsys` | 90,110,378 | **53.65%** |
| `sdk/knowledge-base` | 40,602,357 | **24.17%** |
| `sdk/openwrt-sd9-openwrt-24-10` | 29,159,233 | **17.36%** |
| `sdk/knowledge-base-packet-engine` | 7,975,499 | 4.75% |
| home directory sessions | 119,984 | 0.07% |

### 4.3 最高耗用 session：`c69a135c…`

| 指標 | 數值 |
|---|---:|
| Raw total | 47,829,491 |
| 全機器佔比（主快照） | **28.48%** |
| Cache read | 46,014,008（**96.20%**） |
| Fresh tokens | 1,815,483（3.80%） |
| Output | 217,548（0.45%） |
| 有效 assistant calls | 158 |
| 平均每 call raw tokens | 約 303K |
| 平均每 call cache read | 約 291K |

Model 結構：

| Model | Tokens | Session 佔比 | Calls |
|---|---:|---:|---:|
| Opus 4.8 | 43,645,109 | **91.25%** | 132 |
| Fable 5 | 4,184,382 | 8.75% | 26 |

同一 session 混合至少五個 domain：FP/AAPL 交易分析、SemiAnalysis 網路研究、`gh_sync.sh` 修改、ROMA TODO／Phase C 開發、FN 抓取與 Markdown 生成。這表示後段每次搜尋、讀檔、編輯與測試，都可能帶著前段無關 context。此 session 的問題首先是**context 混題與過長 tool loop**，其次才是 Opus 使用比例。

### 4.4 Raw total 與 fresh ranking 的分歧

在主快照中：

- `c69a135c…` raw share 28.48%，但 fresh share 只有 8.40%；
- `sdk/knowledge-base/3457a74a…` raw share 17.64%，fresh share卻為 30.57%；
- `sdk/knowledge-base/8d2a7427…` raw share 4.18%，fresh share為 16.25%。

因此不能只依 raw total 判斷「哪個 session 最花錢」。第一個 session 是 cache 重讀熱點，後兩個 session 則更像 fresh-input／多 agent 重讀熱點。

### 4.5 RTK 現況

`rtk gain --history` 快照：

- 1,684 commands
- 約 15.8M input tokens
- 約 997.9K output tokens
- 約 **14.8M tokens saved（93.7%）**
- 最大貢獻是 `rtk read`

結論：CLI output 壓縮已相當有效，後續主要槓桿不再是繼續擠工具輸出，而是 context 與 model routing。

---

## 五、結論與行動

### 5.1 優先順序

1. **不同 domain 立即切新 session／`/clear`**：直接降低 raw context 重讀。
2. **Sonnet 5 作預設 workhorse；Opus 4.8 escalation-only**：降低 model-weighted cost／quota。
3. **Fable／Haiku 處理 scan、extract、format、index 與既定規格的機械修改**。
4. **限制 subagent fan-out**：只在 corpus 可明確切分或需獨立驗證時並行，避免多 agent 重讀相同資料。
5. **維持 RTK 與 targeted read**；不把「縮短 final answer」當首要優化。

### 5.2 建議 Model Routing

| Model | 定位 | 適合任務 |
|---|---|---|
| Haiku 4.5 | Scan / Extract | 找檔、grep、分類、抽取欄位、簡單索引 |
| Fable 5 | Mechanical execution | README、重新命名、格式轉換、既定模板 `SAVE*`、低風險落檔 |
| Sonnet 5 | **Default workhorse** | 一般 coding、ROMA 修改、KB 整合、測試、正常 RCA |
| Opus 4.8 | Judge / Deep reasoning | 根因不明、跨模組設計、矛盾訊號裁決、高風險 final review |

#### Trading / ROMA

- 抓現價、找報告、抽取公開資料：Haiku／Fable
- `FP_TODAY`：Fable 或 Sonnet
- `FP_TREND`、`FN_TREND`：Sonnet
- SG DATA 矛盾與跨來源判讀：Sonnet；必要時 Opus
- 新 signal algorithm／跨模組 architecture：Opus 設計，Sonnet 實作
- 已有模板的 `SAVEFP`、`SAVEFN`、`SAVESE`：Fable

#### Driver / OpenWrt

- symbol 搜尋、列 caller、簡單 call graph：Haiku／Fable；複雜時 Sonnet
- 已知問題 patch、probe、logging、測試：Sonnet
- root cause 未明、race/corruption、硬體與 driver path 交錯：Opus
- issue log、README、commit summary：Fable

#### Knowledge Base

- 搬檔、命名、更新 index：Fable／Haiku
- 技術文件去重、合併、建立脈絡：Sonnet
- 多個根因候選最終排序：Opus

### 5.3 Opus 的使用方式

避免讓 Opus 執行完整長鏈：

```text
搜尋 → 讀大量檔案 → 規劃 → 修改 → 測試 → README → commit
```

改用：

```text
Haiku/Fable scout
→ Sonnet 建 evidence packet
→ Opus 只裁決根因／架構／修法
→ Sonnet 實作與測試
→ Fable 更新文件與索引
→ 高風險時 Opus 做一次 final review
```

`c69a135c…` 有 132 次 Opus calls；依任務內容，真正需要 Opus 的主要是 FP/AAPL 最終判讀、Phase C 架構與疑難 pipeline 裁決，其餘 README、commit、抓資料、補 alias 與一般落檔不值得維持 Opus。對類似 session，可將 Opus calls 設為 20–30 次以下的操作目標，但這是管理目標，尚非實證節省率。

### 5.4 Session hygiene 規則

符合任一條件就切 session：

- 任務 domain 改變；
- 已完成 `SAVE*` 或 commit，且準備轉題；
- 已產生可作 handoff 的 summary／artifact；
- 開始讀另一個 repo 或 subsystem；
- context 曾 compact，後續又進入新工作階段。

操作節奏：

```text
完成分析
→ SAVESE / SAVEKB / SAVEISSUEANA / commit
→ /clear
→ 新 session 只讀剛保存的 summary 與必要檔案
→ 進入下一階段
```

- 同一問題仍在調查：`/compact`
- 已完成一個 artifact 且準備轉題：`/clear`
- `/fast` 是加速 Opus inference，不是小模型或 token-saving mode

### 5.5 Subagent 原則

適合 fan-out：

- agent 各負責互不重疊的目錄／subsystem；
- 需要獨立驗證不同根因候選；
- 每個 agent 最後只回傳短、結構化 summary。

不適合 fan-out：

- 多個 agent 都讀同一 issue folder；
- 單純搬檔、命名與 README；
- 已知只需讀少數明確檔案；
- 一個 Sonnet 足以完成的工作。

Token-conscious 預設可採「1 個 Haiku/Fable scout + 1 個 Sonnet implementer + 必要時 1 個 Opus reviewer」，而非多個高階 agent 探索同一 corpus。

---

## 六、待辦

- ☐ 連續記錄 2–4 週，按 task type 統計 raw、fresh、model、calls、duration 與估算成本
- ☐ 做前後期比較：舊流程 vs「Sonnet default + domain 切 session + Opus escalation-only」
- ☐ 以 task 為單位做 bootstrap CI，評估 median raw token、fresh token 與成本的下降幅度
- ☐ 加入 session prompt/topic 轉換偵測，標記可能該 `/clear` 的斷點
- ☐ 若要自動估算費用，另外維護各 model 與 cache 類型當期價格表；不可直接把所有 raw tokens 等權相加
- ☐ 檢查是否值得將 audit script 擴充成按 model、日期、parent/subagent 分層輸出

---

## 七、附錄

### 腳本

- `py_dir/2026-08-10_claude_session_token_usage_audit.py`

執行：

```bash
python py_dir/2026-08-10_claude_session_token_usage_audit.py --top 10
```

腳本現查資料，因此重跑數字會高於本篇固定的 10:26 主快照；這是 session 持續活動造成，不是統計矛盾。

### ROMA 程式對照

本篇是 Claude Code 作業流程與本機 usage 分析，**未引用或修改 ROMA runtime 程式**，故無 ROMA `file:line` 對照。

### 限制

- 只涵蓋本機仍保留的 JSONL；
- 不涵蓋已刪除 session 與其他機器；
- raw tokens 不等同實際收費；
- 目前只是觀察式稽核，未對 routing 政策做隨機或準實驗驗證；
- 「切 session 可省 40–60%」之類數字在沒有前後期實驗前不應當成量化結論。

---

## 關聯

- [[reference_env_office_home]]：多機環境會造成單機 session census 不完整
- [[feedback_multi_machine_sync_via_gh_sync]]：跨機協作與 session handoff 應以持久化 artifact 為界
- [[reference_nested_repo_detach_runbook]]：跨 repo 工作應切 session，避免不同 repository context 混居
