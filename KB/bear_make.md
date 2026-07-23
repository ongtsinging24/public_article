## 一句話

`bear -- make` 是用 **Bear (Build EAR)** 攔截整個 build 過程，產生 `compile_commands.json`（compilation database），讓 clangd / ccls / VS Code 能正確做跳轉、補全、診斷。

```bash
# Bear 3.x（現行版本，必須有 --）
make clean
bear -- make -j$(nproc)

# Bear 2.x（舊版，不用 --）
bear make -j$(nproc)
```

---

## 為什麼要 `--`

Bear 3.0 重寫了 CLI，`--` 是 **分隔符**：左邊是 bear 自己的參數，右邊是要被攔截的完整 build 命令。沒有 `--`，bear 3.x 會把 `make` 當成自己的未知選項而報錯。

```bash
bear --output cdb.json --append -- make V=s -j8
#    └────── bear 的參數 ──────┘    └── build 命令 ──┘
```

## 運作原理

| 階段 | 做的事 |
|---|---|
| `intercept` | 用 `LD_PRELOAD` 塞入 `libexec.so`，攔截 `exec*()` 系列 syscall，記錄每次 `argv[]` + `cwd` |
| `citnames` | 從記錄中篩出「長得像 compiler 呼叫」的項目，展開成 JSON entry |

所以它**不需要改 Makefile**，也不管你是 autotools、kbuild 還是手刻 Makefile。

## 常用參數

```bash
bear --output compile_commands.json -- make    # 指定輸出
bear --append -- make target2                  # 累積多次 build 的結果
bear --config bear.json -- make                # 自訂過濾規則（排除 host tools 等）
```

---

## 對你的場景幾個關鍵坑

**1. 必須是「真的有編譯」的 build**
增量 build 已經是最新 → bear 只會拿到空的或殘缺的 db。務必先 `make clean`，或用 `make -B`。

**2. Linux kernel 不要用 bear**
kbuild 有原生的更可靠做法（5.x 以後）：

```bash
make CC=gcc compile_commands.json
# 或直接跑 scripts/clang-tools/gen_compile_commands.py
```
它是從 `.cmd` 檔生成的，比 LD_PRELOAD 準，也不會漏掉 `__init` 那類特殊編譯單元。RTL8198D 那類 out-of-tree module 則可以 `bear -- make -C $KDIR M=$PWD modules`。

**3. hostapd 最單純**

```bash
cd hostapd && make clean && bear -- make -j8
```
`wpa_auth.c` / `ctrl_iface_ap.c` 的 `#ifdef CONFIG_USER_RTK_26062026_DEBUG` 這種，**只有在 build 時該 macro 有開，clangd 才會把該區塊當作 active code**；沒開的話那段會是灰的、跳不進去。要看 debug 區塊就先在 `.config` 打開再產 db。

**4. Cross-compile 的 clangd 會爆一片紅**
MIPS toolchain 的 system include 路徑 clangd 猜不到，要授權它去問 gcc：

```jsonc
// .vscode/settings.json
"clangd.arguments": [
  "--query-driver=/path/to/staging_dir/**/mips-openwrt-linux-*-gcc",
  "--compile-commands-dir=${workspaceFolder}"
]
```

搭配專案根目錄 `.clangd` 移掉 clang 不認得的 GCC flag：

```yaml
CompileFlags:
  Remove: [-mno-branch-likely, -fno-caller-saves, -flto-partition=*]
```

**5. OpenWrt package 的路徑問題**
`make package/hostapd/compile` 實際編譯發生在 `build_dir/target-*/hostapd-*/`，產出的 db 裡是那份 copy 的路徑，不是你 feeds 裡的原始碼。要嘛直接開 build_dir 那份改，要嘛用 `sed` 把路徑重寫回來。

**6. `LD_PRELOAD` 會被吃掉的情況**
static-linked 的 wrapper、`fakeroot`、某些 sandbox/container 會讓攔截失效，此時 db 會缺一大塊。替代方案：`compiledb`（解析 `make -n` 輸出，不靠 LD_PRELOAD）。

```bash
pip install compiledb
compiledb -n make       # dry-run 模式，不實際編譯
```

---

## 安裝

```bash
sudo apt install bear          # Ubuntu/Debian/Kali
bear --version                 # 確認是 2.x 還是 3.x，決定要不要打 --
```
