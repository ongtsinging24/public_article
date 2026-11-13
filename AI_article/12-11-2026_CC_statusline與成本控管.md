# CC statusline 介紹、加上 cost 與改動行數、同事一天燒 1500 USD 的成因

> 寫於 2026-11-12（台北），Home 機（`ong-home-pc`）。
> 縮寫：CC = Claude Code；ctx = context window；TTL = time-to-live（快取存活時間）；ANSI = 終端色碼

## S_0 | TL;DR

- statusline 是 CC 輸入框下方的一行自訂狀態列。CC 把 session 狀態用 JSON 從 stdin 傳給 `settings.json` 的 `statusLine.command`，再把腳本 stdout 的第一行顯示出來。
- 本機設定：`~/.claude/settings.json` 指向 `~/.claude/statusline.py`。本次在尾端加上 `$花費` 和 `+新增/-刪除` 行數，已用兩組假資料測過。
- 同事一天燒 1500 USD：成本約等於「每輪 ctx 大小 × 輪數 × 單價」。最大的元兇通常是 ctx 從不清理，再加上快取失效和平行化太多。

## S_1 | statusline 機制

設定方式（user 層或 project 層 `settings.json`）：

```json
"statusLine": { "type": "command", "command": "python3 /home/ojy/.claude/statusline.py", "padding": 0 }
```

- 也可以在 CC 裡打 `/statusline <描述>`，由內建的 statusline-setup agent 產生腳本並改好設定
- 觸發時機：對話狀態有變化時就更新，有節流（throttle）
- 輸出：stdout 第一行，可以用 ANSI 上色。腳本必須跑得快，不要在裡面打網路 API

stdin JSON 常用欄位：

| 欄位 | 內容 |
|---|---|
| `model.id` / `model.display_name` | 目前使用的模型 |
| `workspace.current_dir` / `project_dir` | cwd 與專案根目錄 |
| `transcript_path` | 本 session 的 jsonl 對話紀錄 |
| `session_id`, `version`, `output_style.name` | session 和版本資訊 |
| `cost.total_cost_usd`, `total_duration_ms`, `total_lines_added/removed` | 花費、耗時、改動行數 |
| `context_window.*`（新版才有） | ctx 用量 |

## S_2 | 本機 statusline.py 現況（本次改動後）

顯示範例：

```
ojy@ong-home-pc:/home/ojy/ongtradingsys (master) [Opus 5.5] ctx 86.0k 43% $1.23 +120/-8
```

- 原本就有的：user@host、cwd、git branch（detached 時顯示 `@short-sha`；git 呼叫設了 `timeout=1`）、model、ctx 用量
- ctx 的 fallback：JSON 裡沒有 `context_window` 時，改讀 transcript 最後一筆 assistant `usage`，把 input、cache_read、cache_creation 三項加總後自己算
- ctx 變色：低於 60% 青色、60–79% 黃色、80% 以上紅色
- **本次新增**：`cost.total_cost_usd` 顯示為灰色 `$x.xx`；`total_lines_added/removed` 顯示為綠色 `+N`／紅色 `-N`。欄位不存在時自動隱藏
- 驗證：完整 JSON 輸出正確；傳空的 `{}` 時新的兩項不顯示，也不報錯
- `~/.claude/` 不在 repo 內，所以這次改動不進版控

## S_3 | 同事一天燒 1500 USD 的常見成因

先確認：`total_cost_usd` 是**按 API 牌價換算的等值金額**。訂閱制（Pro/Max）只是估算，不會真的照額扣款；走 API key 或企業按量計費才是真的要付的錢。

核心機制：CC 每一輪（包含每一次工具呼叫）都會把整段 ctx 重送一次，所以

> 成本約等於 每輪的 ctx 大小 × 輪數 × 單價（快取命中時便宜，沒命中時貴）

壞習慣，大致依影響排序：

1. **ctx 從不清理**：一個 session 做到底、換題目也不 `/clear`，開了 1M ctx 長到幾十萬 token 還繼續聊。同樣讀一個檔，ctx 20k 和 600k 時成本可差 30 倍
2. **把大東西倒進 ctx**：讀整份大檔或完整 log、跑會吐大量輸出的指令。內容進了 ctx 之後，每一輪都要再付一次錢
3. **快取一直失效**：超過 TTL 才回來、中途切換 model、改 CLAUDE.md 或增減 MCP，整包 ctx 都要用較貴的價格重新寫入快取
4. **輪數爆炸**：短間隔的 `/loop` 輪詢、沒有方向地反覆試錯、headless（`claude -p`）迴圈沒設上限
5. **平行化太多**：同時開很多 session、大量 subagent／workflow fan-out（每個 agent 都有自己的 ctx）
6. **模型和思考強度一律開到最高**：小事也用 Opus 加 max effort，產生大量 thinking token
7. **MCP 工具定義太肥**：每輪都要送幾萬 token 的工具定義

診斷法：

1. 用 `/cost`，或用 `ccusage` 分析 `~/.claude/projects/*/` 底下的 jsonl
   - 少數幾個巨大 session 佔大宗 → 第 1、2 項
   - session 數量非常多 → 第 4、5 項
2. 拆 usage 欄位：`cache_creation_input_tokens` 偏高 → 快取失效（第 3 項）；`cache_read_input_tokens` 很高 → ctx 太大或輪數太多（第 1、4 項）
3. 可以沿用我方 token 用量統計腳本（memory「Claude token 用量統計腳本」）。注意要用 `message.id` 去重，否則會高估約 1.8 倍

給同事的建議：一個任務一個 session，換題目就 `/clear`；ctx 超過約 60% 時先 `/compact` 或開新 session；大檔只讀需要的段落，log 先用 grep、head、tail 過濾；日常改碼用 Sonnet，難題再切 Opus；自動化迴圈設輪數上限，不要短間隔輪詢；statusline 加上 ctx% 和 `$`，即時看到花費。
