# 數位IC設計 理論基礎 — 六層學習路線圖

> 從電晶體到 tape-out，由下而上。下層是上層的物理約束，跳層會在時序收斂（timing closure）或良率上卡死。

```
第六層：實體實作與簽核  合成 · STA · DFT · 布局繞線 · 功耗/IR/EM · sign-off
第五層：驗證           Testbench · SystemVerilog/UVM · 覆蓋率 · Formal · 模擬/硬體加速
第四層：架構與微架構    處理器管線 · 記憶體階層 · 匯流排/NoC · 加速器 · 低功耗架構
第三層：RTL 設計        Verilog/SV · 同步設計 · 管線化 · CDC · 可合成寫法
第二層：數位邏輯        布林代數 · 組合/循序電路 · FSM · 時序參數 · 算術電路
第一層：元件與電路基礎   半導體物理 · MOSFET · CMOS 反相器 · 延遲/功耗模型 · 內連線
```

縮寫對照（abbreviations）：
- **RTL** = Register Transfer Level 暫存器傳輸層級
- **HDL / SV** = Hardware Description Language / SystemVerilog
- **FSM** = Finite State Machine 有限狀態機
- **CDC / RDC** = Clock Domain Crossing / Reset Domain Crossing 跨時脈域 / 跨重置域
- **STA** = Static Timing Analysis 靜態時序分析
- **WNS / TNS** = Worst / Total Negative Slack 最差 / 總負裕度
- **OCV / AOCV / POCV** = On-Chip Variation（及其 Advanced / Parametric 版本）晶片內變異
- **PVT** = Process / Voltage / Temperature 製程/電壓/溫度角
- **DFT / ATPG / BIST** = Design for Test / Automatic Test Pattern Generation / Built-In Self-Test
- **UVM** = Universal Verification Methodology
- **SVA** = SystemVerilog Assertions 斷言
- **UPF** = Unified Power Format（IEEE 1801，低功耗意圖描述）
- **DVFS** = Dynamic Voltage and Frequency Scaling 動態電壓頻率調整
- **P&R / APR** = Place and Route 布局繞線
- **CTS** = Clock Tree Synthesis 時脈樹合成
- **DRC / LVS** = Design Rule Check / Layout Versus Schematic
- **IR / EM** = IR drop 壓降 / Electromigration 電遷移
- **PPA** = Power / Performance / Area 功耗/效能/面積
- **PDK** = Process Design Kit 製程設計套件
- **AXI / AHB / APB** = ARM AMBA 匯流排協定家族
- **NoC** = Network-on-Chip 晶片網路

---

## 第一層：元件與電路基礎（最重要，不能跳）

所有「為什麼時序過不了、為什麼功耗爆、為什麼先進製程變難」的答案都在這層。這層不紮實，上層就只剩「跑工具看報表」。

- **半導體物理（Semiconductor Physics）**：能帶、摻雜（n/p-type）、PN 接面、載子遷移率（mobility）。
  - 遷移率 n > p，是「PMOS 要做得比 NMOS 寬」的根源。
- **MOSFET 模型**：截止/線性/飽和區、閾值電壓 Vt、長通道平方律 vs 短通道速度飽和（velocity saturation）、次臨界漏電（subthreshold leakage）。
  - Vt 的取捨：低 Vt 快但漏電大、高 Vt 省電但慢——這是後面「multi-Vt 庫」與漏電優化的物理根據。
- **CMOS 反相器（Inverter）**：VTC 電壓轉移曲線、雜訊邊限（noise margin）、上升/下降時間。反相器懂了，所有靜態 CMOS 閘都懂了一半。
- **延遲模型（Delay）**：RC 模型、**邏輯努力（Logical Effort）**、扇出（fan-out）、驅動強度（sizing）、緩衝器鏈（buffer chain）。
  - 標準元件庫（standard cell library）的 NLDM/CCS 時序表，本質就是這些模型的查表化。
- **功耗（Power）**：
  - 動態功耗 `P_dyn = α · C · V² · f`（α 為切換率）——V 是平方項，所以**降電壓是最有效的省電手段**（串起 DVFS）。
  - 短路功耗、靜態漏電（leakage）；先進製程下漏電佔比上升。
- **內連線（Interconnect）**：導線 RC、Elmore delay、串擾（crosstalk）、耦合電容。先進製程**線延遲已壓過閘延遲**，這是後端難度暴增的主因。
- **製程演進**：Planar → FinFET → GAA（Gate-All-Around / nanosheet）→ 背面供電（backside power delivery）。每一步都是在對抗短通道效應與漏電。

**動手點**：用 SPICE（ngspice 免費）模擬一個 CMOS 反相器：掃 VTC、量 tpd、改 W/L 與負載電容觀察延遲變化，再算一次動態功耗與模擬值對照。

---

## 第二層：數位邏輯（Digital Logic）

別因為「大學學過」就跳過。這層的觀念在百萬閘等級的晶片上「完全」適用，而且在小電路上最容易看清原理。

- **布林代數與化簡**：De Morgan、卡諾圖（K-map）、Quine–McCluskey、SOP/POS。理解合成工具在做什麼的起點。
- **組合邏輯（Combinational）**：多工器（MUX）、解碼器、編碼器、比較器；**hazard / glitch**（突波）成因。
- **循序邏輯（Sequential）**：
  - Latch vs Flip-Flop（邊緣觸發）的差別，以及為什麼 ASIC 設計「原則上不要 latch」（例外：time borrowing、clock gating cell）。
  - **時序三參數**：setup time、hold time、clock-to-Q。這是整個 STA 的原子。
  - **亞穩態（Metastability）**：MTBF 公式、為什麼要兩級同步器（2-flop synchronizer）——串起第三層 CDC。
- **有限狀態機（FSM）**：Moore vs Mealy、狀態編碼（binary / one-hot / gray）的面積與速度取捨。
- **算術電路（Arithmetic）**：
  - 加法器家族：Ripple-carry → Carry-lookahead → Carry-select → **Prefix adder（Kogge-Stone / Brent-Kung）**，一條線看懂「面積換速度」。
  - 乘法器：Booth 編碼、Wallace/Dadda tree；定點數（fixed-point）與浮點（IEEE 754）表示。
- **核心觀念（跨層通用）**：
  - **關鍵路徑（critical path）**決定最高頻率 `f_max = 1 / (t_cq + t_logic + t_setup + t_skew)`。
  - 同步設計原則：單一時脈邊緣、所有狀態都在暫存器裡。

**動手點**：手推一個 4-bit 同步計數器 + 序列偵測 FSM，畫出時序圖，再手算最長路徑決定的最高頻率。

---

## 第三層：RTL 設計（RTL Design）

- **HDL 語言**：Verilog / SystemVerilog（業界主流），VHDL（歐洲/國防/FPGA 常見）。
  - **最重要的一句話：HDL 是在「描述硬體」，不是在「寫程式」。** 每一行都要能在腦中對應到閘和暫存器。
- **可合成寫法（Synthesizable Coding）**：
  - `always_ff` 用 non-blocking（`<=`）、`always_comb` 用 blocking（`=`）——Cummings 的經典規則，違反會造成模擬與合成結果不一致（sim/synth mismatch）。
  - 避免意外推出 latch（組合邏輯 case/if 沒寫滿）、避免組合迴路（combinational loop）。
- **同步設計與重置（Reset）**：同步 vs 非同步重置、**非同步 assert / 同步 de-assert**（reset synchronizer）。
- **管線化（Pipelining）**：切管線換頻率、代價是延遲（latency）與面積；valid/ready 握手（handshake）與 back-pressure。
- **跨時脈域（CDC）**——這層的分水嶺，**真正理解過一次**：
  - 單 bit：兩級同步器。
  - 多 bit：**不能**逐 bit 同步（會拿到不一致組合）→ 用 gray code、握手協定（req/ack）、或**非同步 FIFO**（async FIFO，gray-code 指標）。
  - 快轉慢的脈衝會被吃掉 → pulse synchronizer / toggle 法。
- **時脈閘控（Clock Gating）**：用 ICG cell 做、不要手寫 AND gate（會產生 glitch）——串起第一層動態功耗 α 項。
- **參數化與可重用**：parameter / generate、介面（interface）、模組化，為第四層 IP 整合打底。

**動手點**：寫一個參數化的 **非同步 FIFO**（gray-code 指標 + 兩級同步 + full/empty 判斷），用 Verilator 或 Icarus 模擬兩個不同頻率的時脈，確認不掉資料、不溢位。

---

## 第四層：架構與微架構（Architecture & Microarchitecture）

- **處理器管線（CPU Pipeline）**：經典五級管線（IF/ID/EX/MEM/WB）、三種 hazard（結構/資料/控制）、forwarding、stall、分支預測（branch prediction）。
  - 進階：超純量（superscalar）、亂序執行（out-of-order，Tomasulo / ROB）。
  - **RISC-V**：開放 ISA，現代教學與開源 IP 的共同語言。
- **記憶體階層（Memory Hierarchy）**：cache（直接映射/組相聯、寫回/寫穿、替換策略）、TLB、一致性協定（MESI）、DRAM / HBM 介面。
  - **Memory wall**：算力成長遠快於記憶體頻寬——理解它才懂 HBM 與先進封裝為何是 AI 晶片的核心。
- **匯流排與互連（Interconnect）**：AMBA **AXI**（通道分離、outstanding、burst）/ AHB / APB；多核與大晶片走 **NoC**。
- **領域專用加速器（DSA）**：脈動陣列（systolic array，如 TPU）、資料流（dataflow）、SIMD / 向量；PPA 取捨與 roofline model（算力 vs 頻寬上限）。
- **低功耗架構**：DVFS、power gating（電源關斷 + isolation + retention）、multi-voltage domain——以 **UPF** 描述電源意圖。
- **系統整合（SoC）**：IP 重用、時脈/重置架構、中斷控制；**Chiplet** 與 die-to-die 介面（UCIe）、2.5D/3D 封裝（CoWoS、SoIC）。

**動手點**：用 SV 寫一個 RV32I 五級管線 CPU（含 forwarding 與 hazard detection），跑通一段組合語言程式；再加一個小型直接映射 cache，量測 hit rate 對 CPI 的影響。

---

## 第五層：驗證（Verification）

業界經驗法則：**驗證工時與人力常超過設計本身**。晶片沒有「上線後修 bug」這回事，一次 respin 是數百萬到上億美元與數個月。

- **驗證計畫（Verification Plan）**：先列功能點（feature list）與覆蓋目標，再寫 testbench。沒有計畫的驗證永遠不知道何時算完。
- **Testbench 架構**：stimulus（激勵）→ DUT → monitor → scoreboard / reference model（黃金模型）比對。
- **SystemVerilog 驗證特性**：class / OOP、**約束隨機（constrained random）**、**功能覆蓋率（covergroup）**、**斷言（SVA）**。
- **UVM**：業界標準方法論——agent（driver / sequencer / monitor）、sequence、factory、config_db、phase。理解它「為什麼要這麼重」：為了跨專案重用與規模化。
- **覆蓋率（Coverage）**：
  - Code coverage（line / toggle / FSM / branch）：「有沒有跑到」。
  - Functional coverage：「規格裡的情境有沒有被驗到」。
  - **100% code coverage ≠ 沒有 bug**——覆蓋率只證明「跑過」，不證明「檢查過」。
- **形式驗證（Formal Verification）**：
  - Property checking（用 SVA 窮舉證明）、**等價性檢查（LEC，RTL vs 合成後網表）**、CDC / RDC 靜態檢查、X-propagation。
  - 形式驗證擅長「角落情境」，模擬擅長「長序列行為」，兩者互補。
- **系統級與加速**：FPGA prototyping、硬體模擬器（emulator）、軟硬體協同驗證（跑真的 firmware / OS 開機）。

**動手點**：替第三層的非同步 FIFO 寫一個 UVM（或精簡 SV class-based）testbench：約束隨機讀寫、scoreboard 比對、covergroup 覆蓋 full/empty/同時讀寫；再用 SVA 寫「full 時不得寫入成功」並跑 formal（SymbiYosys 免費）。

---

## 第六層：實體實作與簽核（Physical Implementation & Sign-off）

RTL 能模擬通過 ≠ 能做成晶片。頻率、面積、功耗、良率，全在這層定生死。

- **邏輯合成（Logic Synthesis）**：RTL → 門級網表（gate-level netlist）；technology mapping、**SDC 時序約束**（create_clock、input/output delay、false path、multicycle path）。
  - **約束寫錯比設計錯更危險**：false path 設錯，STA 會「乾淨地」放過一條真的違規路徑。
- **靜態時序分析（STA）**：
  - setup / hold check、slack、WNS / TNS；**hold 違規與頻率無關，降頻救不了**。
  - PVT corner、**多模式多角（MMMC）**、OCV / AOCV / POCV、CRPR（時脈共同路徑悲觀消除）。
  - 訊號完整性：串擾造成的延遲變動（SI-aware STA）。
- **可測試性設計（DFT）**：scan chain（掃描鏈）、ATPG（stuck-at / transition fault 模型）、MBIST（記憶體自測）、JTAG（IEEE 1149.1）、壓縮（test compression）。
  - DFT 決定**測試成本與良率學習速度**，直接影響毛利。
- **布局繞線（P&R）**：
  - Floorplan（巨集擺放、電源規劃 power grid）→ Placement → **CTS（時脈樹：skew / latency 平衡）** → Routing → 時序優化（ECO）。
  - 擁塞（congestion）是先進製程常見卡點——串起第一層「線延遲壓過閘延遲」。
- **簽核（Sign-off）**：
  - 物理驗證：**DRC、LVS**、天線效應（antenna）、DFM。
  - 電源完整性：**IR drop**（靜態/動態）、**EM**（電遷移，長期可靠度）。
  - 功耗簽核：向量驅動（vector-based）功耗分析。
  - 全部通過才能 **tape-out**（交 GDSII / OASIS 給晶圓廠）。
- **量產端**：良率（yield）、binning（依速度分級）、老化（aging / NBTI / HCI）。

**動手點**：用開源流程 **OpenROAD / OpenLane + SkyWater 130nm PDK**，把第三層的 FIFO 從 RTL 跑到 GDSII：讀合成報表、STA 報表、看 CTS 前後 skew、打開版圖觀察擁塞；或直接投 **Tiny Tapeout** 拿到真的晶片。

---

## 經典教材：《CMOS VLSI Design》（Weste & Harris）

**書名**：*CMOS VLSI Design: A Circuits and Systems Perspective*（第 4 版）
**作者**：Neil H. E. Weste、David Money Harris（2010, Addison-Wesley / Pearson）
**地位**：數位 IC 領域與 Rabaey《Digital Integrated Circuits》並列的**奠基聖經**。Rabaey 偏電路理論推導，Weste & Harris 偏「從電晶體一路做到系統」的設計者視角，覆蓋面最完整，本文以它為主軸。

### 全書結構（依主題分組）

| 組 | 章節 | 內容 | 對應本文層級 |
|--------|----------|---------------------------------|--------------|
| 基礎    | Ch 1–3   | 總覽、MOS 元件理論、CMOS 製程    | 第一層       |
| 電路分析 | Ch 4–8   | 延遲、功耗、內連線、穩健性、電路模擬 | 第一層（核心）|
| 電路設計 | Ch 9–10  | 組合電路、循序電路設計          | 第二、三層   |
| 子系統   | Ch 11–13 | 資料路徑、陣列（記憶體）、特殊子系統 | 第二、四層   |
| 方法論   | Ch 14–15 | 設計方法與工具、測試/除錯/驗證   | 第五、六層   |

### 分章導讀與閱讀建議

**基礎（對應第一層）**
- **Ch 1 Introduction** ✅ 必讀：用一顆小處理器走完整個設計流程，是全書地圖。
- **Ch 2 MOS Transistor Theory** ✅ 必讀：長/短通道模型、漏電、Vt——所有延遲與功耗的根源。
- **Ch 3 CMOS Processing Technology** 🔵 選讀：製程步驟與版圖規則，做前端可略讀、做後端要讀。

**電路分析（對應第一層，落地最相關）**
- **Ch 4 Delay** ✅ 必讀：RC 延遲與 **Logical Effort**——**全書最該精讀的一章**，把「怎麼讓電路變快」講透。
- **Ch 5 Power** ✅ 必讀：動態/靜態功耗、低功耗技術，直接串到 DVFS 與 power gating。
- **Ch 6 Interconnect** ⭐ 重要：導線 RC、串擾、repeater 插入；後端與先進製程必讀。
- **Ch 7 Robustness** ⭐ 重要：製程變異、可靠度、scaling 趨勢——OCV 與 corner 分析的理論解釋。
- **Ch 8 Circuit Simulation** 🔵 選讀：SPICE 使用與模型，動手點用得上。

**電路設計（對應第二、三層）**
- **Ch 9 Combinational Circuit Design** ✅ 必讀：靜態 CMOS、動態邏輯、pass-transistor 等電路家族的取捨。
- **Ch 10 Sequential Circuit Design** ✅ 必讀：latch/flip-flop 時序、**時脈偏移（skew）與 time borrowing**、同步器與亞穩態——STA 的電路層根據。

**子系統（對應第二、四層）**
- **Ch 11 Datapath Subsystems** ⭐ 重要：加法器（含 prefix adder）、乘法器、移位器——算術電路最完整的整理。
- **Ch 12 Array Subsystems** ⭐ 重要：SRAM、DRAM、ROM、CAM；理解記憶體為何佔晶片面積大宗。
- **Ch 13 Special-Purpose Subsystems** 🔵 選讀：封裝、電源分配、時脈產生（PLL）、I/O。

**方法論（對應第五、六層）**
- **Ch 14 Design Methodology and Tools** ⭐ 重要：設計流程與 EDA 工具鏈的全景。
- **Ch 15 Testing, Debugging, and Verification** ⭐ 重要：故障模型、scan、BIST——DFT 的入門版。

### 重要提醒：這本書的時間侷限
> 第 4 版出版於 **2010 年，早於 FinFET 量產（Intel 22nm, 2011）**。書中**沒有**或僅淺提：FinFET / GAA 元件行為、UVM 驗證方法論（2011 才發布 1.0）、先進 OCV 模型（POCV）、Chiplet / UCIe、2.5D/3D 先進封裝、AI 加速器架構、背面供電。
>
> 因此它的定位是：**打穩第一～二層（與第六層原理）的電路地基**。第三～六層的業界實務請接專書、標準文件與開源工具（見下方清單）。

### 怎麼用這本書（依目標分流）
- **走類比/全客製或後端（APR / STA / sign-off）**：Ch 2 → 4 → 5 → 6 → 7 → 10 精讀，Ch 3 補製程。
- **走前端 RTL / 架構**：Ch 1、4、9、10、11 讀懂即可，省下時間投到第三～四層的專書與實作。
- **走驗證**：Ch 1、10、15 即可；主力放在 SystemVerilog / UVM / formal。
- **完全別「從第一頁讀到最後一頁」**：這是參考書（reference），不是小說。按本文六層的缺口針對性補。

---

## 接續閱讀清單：第三層以後（這本書沒有或太淺的部分）

標記：✅奠基必讀 / ⭐重要 / 🔵延伸。

### A. 第二～四層 — 邏輯、RTL 與架構（書與論文）

| 資源 | 年 | 一句話重點 | 程度 |
|------|----|------------|------|
| **Harris & Harris《Digital Design and Computer Architecture: RISC-V Edition》** | 2021 | 從閘到 RISC-V 管線 CPU 一條龍，含 SV 範例，最佳入門 | ✅ |
| **Cummings: Nonblocking Assignments in Verilog Synthesis (SNUG)** | 2000 | blocking/non-blocking 規則的出處，sim/synth mismatch 必讀 | ✅ |
| **Cummings: Clock Domain Crossing Design & Verification (SNUG)** | 2008 | CDC 全套手法（同步器、握手、多 bit 陷阱）的業界標準參考 | ✅ |
| **Cummings: Simulation and Synthesis Techniques for Asynchronous FIFO Design (SNUG)** | 2002 | gray-code 指標 async FIFO 的經典實作 | ✅ |
| **Patterson & Hennessy《Computer Organization and Design: RISC-V Edition》** | 2017+ | 計算機組織標準教材，管線與記憶體階層 | ✅ |
| **Hennessy & Patterson《Computer Architecture: A Quantitative Approach》(6th)** | 2017 | 量化架構分析，含 DSA/TPU 章節 | ⭐ |
| **ARM AMBA AXI Protocol Specification** | — | SoC 匯流排事實標準，讀規格本身 | ⭐ |
| **In-Datacenter Performance Analysis of a TPU (Jouppi et al.)** | 2017 | 脈動陣列加速器的經典實例 | ⭐ |
| **Roofline Model (Williams et al.)** | 2009 | 算力 vs 頻寬上限的分析框架 | 🔵 |

### B. 第五層 — 驗證（書與標準）

| 資源 | 年 | 一句話重點 | 程度 |
|------|----|------------|------|
| **Spear & Tumbush《SystemVerilog for Verification》(3rd)** | 2012 | OOP、約束隨機、covergroup 的標準入門 | ✅ |
| **IEEE 1800 SystemVerilog LRM** | 2017/2023 | 語言最終權威，查規格用 | 🔵 |
| **IEEE 1800.2 UVM + Accellera UVM User's Guide** | 2017/2020 | UVM 官方規格與使用指南 | ⭐ |
| **Salemi《The UVM Primer》** | 2013 | 最短路徑看懂 UVM 為什麼這樣設計 | ✅ |
| **Seligman et al.《Formal Verification: An Essential Toolkit》(2nd)** | 2023 | 形式驗證實務，FPV / LEC / 應用案例 | ⭐ |
| **Cerny et al.《SVA: The Power of Assertions in SystemVerilog》** | 2015 | 斷言寫法完整參考 | 🔵 |

### C. 第六層 — 實作與簽核（書與標準）

| 資源 | 年 | 一句話重點 | 程度 |
|------|----|------------|------|
| **Bhasker & Chadha《Static Timing Analysis for Nanometer Designs》** | 2009 | STA 聖經：setup/hold、OCV、CRPR、SI | ✅ |
| **Keating et al.《Low Power Methodology Manual》** | 2007 | clock gating、power gating、multi-Vdd 實務（ARM/Synopsys 合著） | ⭐ |
| **IEEE 1801 UPF** | 2018+ | 低功耗意圖描述標準 | 🔵 |
| **Bushnell & Agrawal《Essentials of Electronic Testing》** | 2000 | 故障模型、ATPG、BIST 的 DFT 經典 | ⭐ |
| **Kahng et al.《VLSI Physical Design: From Graph Partitioning to Timing Closure》(2nd)** | 2022 | 布局/繞線/CTS 演算法原理 | ⭐ |
| **Rabaey《Digital Integrated Circuits》(2nd)** | 2003 | 電路層另一本聖經，推導更深 | 🔵 |

### D. 開源工具、課程與實作平台

| 資源 | 形式 | 特點 |
|------|------|------|
| **HDLBits** | 線上練習 | Verilog 題庫，即時模擬判題，入門最快 |
| **Verilator / Icarus Verilog / cocotb** | 模擬器 / Python testbench | 免費模擬，cocotb 讓 Python 使用者快速上手驗證 |
| **Yosys + SymbiYosys** | 合成 / 形式驗證 | 開源合成與 formal，能實際跑 SVA 證明 |
| **OpenROAD / OpenLane + SkyWater 130 / GF180 PDK** | RTL→GDSII 全流程 | 唯一能完整走過後端的免費途徑 |
| **Tiny Tapeout** | 共乘投片 | 低成本拿到真的晶片，走完一次 tape-out |
| **Berkeley EECS 151/251A、MIT 6.004 / 6.111、Chipyard** | 課程 / SoC 框架 | 從數位設計到 RISC-V SoC 產生器 |
| **ChipVerify / Verification Academy** | 教學網站 | SV / UVM 範例與方法論文章 |

### 給半導體投資研究者（非工程師）的最短路徑
> 不必學會寫 RTL。要懂的是「產業鏈每一段的瓶頸與護城河在哪」。優先序：
> **第一層的功耗公式與 scaling（懂 FinFET→GAA→背面供電為何是節點賣點）→ 第四層的 memory wall 與 chiplet/先進封裝（懂 HBM、CoWoS 為何是 AI 晶片瓶頸）→ 第六層的流程全景（懂 EDA 為何是寡占、tape-out 成本為何逐節點暴增）**。
> 對照產業：製程與封裝 → 晶圓代工；合成/STA/P&R/sign-off 工具 → EDA 雙寡頭（Synopsys、Cadence）；AXI/CPU IP → ARM；加速器架構 → GPU/ASIC 設計公司。第三、五層理解概念即可。

---

## 學習順序與心法

1. **不能跳第一層**。不懂延遲與功耗的物理來源，後面所有 PPA 取捨都只能靠背。
2. **每層都要手動跑通一個最小實作**：SPICE 反相器 → 手推 FSM → async FIFO → RV32I 管線 → UVM testbench → OpenLane 出 GDSII。光看會的是錯覺。
3. **腦中永遠要有「這行 RTL 對應什麼硬體」**：寫 code 時想的是閘、暫存器與線，而不是程式邏輯。
4. **由下而上理解、由上而下實作**：先建立全圖，再按你的目標（前端設計 / 驗證 / 後端實作 / 架構 / 產業研究）深挖某一支。
5. **對大多數職位**：第一、二層打底 → 選定一個主軸（RTL、驗證或後端）重押 → 其他層懂到能跟隔壁團隊溝通的程度即可。

> 要深入哪一層，或針對特定方向（CPU/AI 加速器架構、UVM 驗證、STA/後端、低功耗設計）展開更細的路線與資料清單？
