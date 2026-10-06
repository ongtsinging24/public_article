```text
# brokerage parse log
# file        : 06-10-2026-brokerage.xlsx
# parsed_at   : 2026-10-06T14:20:55
# roma_version: v6.47 (95dce4bc)
# roma_runtime: loaded 2026-10-06T14:20:53 | src ✅
# sheetnames  : ['工作表1']
# force_source: None

# format      : B (sheet='工作表1')

[hsbc       ] sym=QQQ    qty=116.00 last=755.27     mv=   87,611.32  src=ib_xlsx_inline

# === abbr (欄名縮寫；逐項表格版見 brokerage_log/README.md) ===
#   NAV 淨資產 | MV 市值(option 為權利金) | UPL 未實現損益 | DTE 距到期天數 | ITM/OTM 價內/價外
#   Δ 對標的價格一階敏感度 | σ 隱含波動率 IV | θ 時間價值衰減 | intrinsic/extrinsic 內在/時間價值
#   gross/net leverage 總/淨槓桿 | rr* 本 log 的 Ratios & Risk 編號
#   rr4/rr4b/rr4c 保護口徑＝指數(SPY/QQQ/IWM/DIA)/板塊(SMH/SOXX/XL*)/個股(限同標的有多頭曝險)；
#   三者皆指 long put or bear put spread，rr4t＝rr4+rr4b，rr4u＝保護總量

# === positions (stock → option → futures → cash) ===
[stock ] qty=[ 116]  mv=[        87,611]  UPL=[   +8,643]  sym=QQQ    last=   755.27
[stock ] qty=[ 100]  mv=[        25,386]  UPL=[     -274]  sym=AMZN   last=   253.86
[stock ] qty=[  20]  mv=[         7,259]  UPL=[     +144]  sym=AVGO   last=   362.93
[stock ] qty=[  50]  mv=[        24,222]  UPL=[     +763]  sym=LIN    last=   484.45
[stock ] qty=[ 410]  mv=[       199,328]  UPL=[  +46,430]  sym=TSM    last=   486.16

[option ] qty=[  2] mv=[       8,950]  UPL=[      -50]  DTE= 136  ITM  +3.7%  desc="AVGO Feb19'27 350 Call"
[option ] qty=[  1] mv=[       5,383]  UPL=[     +459]  DTE= 164  ITM +11.0%  desc="GOOG Mar19'27 310 Call"
[option ] qty=[  2] mv=[      15,203]  UPL=[   +4,362]  DTE= 101  ITM  +7.9%  desc="QQQ Jan15'27 700 Call"
[option ] qty=[  2] mv=[      12,090]  UPL=[   +3,445]  DTE= 101  ITM  +4.9%  desc="QQQ Jan15'27 720 Call"
[option ] qty=[  2] mv=[      11,378]  UPL=[   +2,861]  DTE= 101  ITM  +4.2%  desc="QQQ Jan15'27 725 Call"
[option ] qty=[  2] mv=[      16,145]  UPL=[   -8,702]  DTE= 101  ITM  +9.2%  desc="SMH Jan15'27 580 Call"
[option ] qty=[  3] mv=[      36,039]  UPL=[  +18,292]  DTE= 136  ITM +19.0%  desc="SOXX Feb19'27 495 Call"
[option ] qty=[  5] mv=[      46,245]  UPL=[  +12,447]  DTE=  73  ITM +21.5%  desc="TSM Dec18'26 400 Call"
[option ] qty=[  2] mv=[      16,731]  UPL=[   +4,237]  DTE=  73  ITM +18.6%  desc="TSM Dec18'26 410 Call"
[option ] qty=[  4] mv=[      37,153]  UPL=[  +18,424]  DTE= 136  ITM +18.6%  desc="TSM Feb19'27 410 Call"
[option ] qty=[  2] mv=[      19,255]  UPL=[     -532]  DTE= 101  ITM +21.5%  desc="TSM Jan15'27 400 Call"

[cash   ] mv=    129,072.60  key=IBKR_CASH

# === summary ===
# positions   : 17
#   cash      count=1    mv_sum=    129,072.60
#   option    count=11   mv_sum=    224,571.98
#   stock     count=5    mv_sum=    343,805.77
# total NAV  :     697,450.35  (期貨 notional/UPL 不計入；曝險見 rr2/rr3/rr8c)

# === Ratios & Risk ===
# rr1 equity_ratio       (stock + |option|) / NAV         :  81.49%  ≡ 1 − rr5（無 short option 時；有則多 2×|short MV|/NAV）
# rr2 futures_ratio      futures_notional / NAV           :   0.00%

# rr3 gross_leverage (總槓桿比率)(stock+|optΔ|+fut_not)/NAV=[  2.21x]
# <過度槓桿（無期貨/short option/融資 ⇒ 無爆倉路徑；option 段下檔封頂 32.2% NAV）>

#     option 用 Δ 等效曝險 $1,196,000
#     gross ≠ 最大損失：long premium 那段下檔封頂在 $224,572（32.2% NAV），期貨/正股才是線性無下限

# rr3n net_leverage (淨槓桿比率)      (stock + ΣoptΔ + fut_signed) / NAV :   2.21x
#     (signed；與 rr6 同源不乘 β；保險/空方向 Δ 在此沖銷不墊高 
#      ⇒ 有開 PUT/保險時 rr3n 會低於 rr3 ; 凸性帳，愈跌 Δ 愈負=>槓桿愈低)
#     scale: <0.7 保守 | 0.7-1.0 健康 | 1.0-1.3 輕度 | 1.3-1.6 中度 | 1.6-2.0 高 | >2.0 警示

# rr4 index_hedge_pct    index_put_hedge / NAV            :   0.00%
# rr4b sector_hedge_pct  sector_put_hedge / NAV           :   0.00%
# rr4t systemic_hedge_pct (rr4 + rr4b) / NAV              :   0.00%
# rr4c single_hedge_pct  single-name_put_hedge / NAV      :   0.00%
# rr4u all_hedge_pct     (rr4t + rr4c) / NAV              :   0.00%   ← **保護總量看這欄**

# rr5 cash_ratio         cash / NAV                       :  18.51%

# rr6 β-weighted_pct     Σ(exposure × β) / NAV            : 274.90%   (SPX等效多頭)
#     曝險加總（raw ＝未乘 β；beta ＝乘上 POSITION_META 的 β。兩列不可混讀）:
#                     stock          option       futures           total     %NAV
#       raw        +343,806      +1,196,000            +0      +1,539,806 +220.78%
#       beta       +412,243      +1,505,035            +0      +1,917,278 +274.90%   <- rr6 主行分子
#       ↳ 兩列差 $+377,472（+54.12pp NAV）＝ β 放大效果，不是新增曝險；隱含平均 β 1.25
#       ↳ raw total ≡ rr3n 淨槓桿的分子（見上方 rr3n 行）；逐 sym 拆解見下方 rr6-2 的 equiv_mv 欄

# rr6-1 (option exposure) = qty×delta×100×spot 
#      （名目價值合計 $1,196,000 ； premium MV $224,572 ； σ 來源全部 broker）
#       AVGO_C350_FEB1927            Δ=+0.63 qty= +2 S=$ 362.93 σ=0.40 → exp=$     +45,921
#       GOOG_C310_MAR1927            Δ=+0.75 qty= +1 S=$ 344.07 σ=0.34 → exp=$     +25,684
#       QQQ_C700_JAN1527             Δ=+0.78 qty= +2 S=$ 755.27 σ=0.24 → exp=$    +117,828
#       QQQ_C720_JAN1527             Δ=+0.72 qty= +2 S=$ 755.27 σ=0.22 → exp=$    +108,127
#       QQQ_C725_JAN1527             Δ=+0.70 qty= +2 S=$ 755.27 σ=0.22 → exp=$    +105,353
#       SMH_C580_JAN1527             Δ=+0.73 qty= +2 S=$ 633.10 σ=0.36 → exp=$     +92,839
#       SOXX_C495_FEB1927            Δ=+0.81 qty= +3 S=$ 588.84 σ=0.43 → exp=$    +142,311
#       TSM_C400_DEC1826             Δ=+0.92 qty= +5 S=$ 486.16 σ=0.35 → exp=$    +222,775
#       TSM_C410_DEC1826             Δ=+0.89 qty= +2 S=$ 486.16 σ=0.34 → exp=$     +86,811
#       TSM_C410_FEB1927             Δ=+0.83 qty= +4 S=$ 486.16 σ=0.35 → exp=$    +162,275
#       TSM_C400_JAN1527             Δ=+0.89 qty= +2 S=$ 486.16 σ=0.36 → exp=$     +86,078

# rr6-2 Δ-equivalent shares  (正股 + option Δ + 指數期貨 ＝ 等效持有幾股正股；
#       option 等效股數 = exposure / spot，期貨 = notional / 代理 ETF spot):
#       ※ equiv_mv = stock MV + Σopt exposure + Σfut notional（期貨 β 不套用，見 _FUT_EQUITY_PROXY）
#       sym      stock_sh  opt_lots     optΔ_sh  fut_lots     futΔ_sh    equiv_sh  ×stock       equiv_mv     %NAV
#       TSM           410       +13      +1,148        +0          +0      +1,558   3.80x       +757,267 +108.58%
#       QQQ           116        +6        +439        +0          +0        +555   4.78x       +418,919  +60.06%
#       SOXX            0        +3        +242        +0          +0        +242     n/a       +142,311  +20.40%
#       SMH             0        +2        +147        +0          +0        +147     n/a        +92,839  +13.31%
#       AVGO           20        +2        +127        +0          +0        +147   7.33x        +53,180   +7.62%
#       GOOG            0        +1         +75        +0          +0         +75     n/a        +25,684   +3.68%
#       AMZN          100        +0          +0        +0          +0        +100   1.00x        +25,386   +3.64%
#       LIN            50        +0          +0        +0          +0         +50   1.00x        +24,222   +3.47%
#       TOTAL          --        --          --        --          --          --      --     +1,539,808 +220.78%
#       ※ 無排除項 ⇒ TOTAL ≡ rr6 註腳的 raw total ≡ rr3n 淨槓桿的分子
#       ※ +220.78% 是**名目 gross**：指數/板塊 ETF 與其成分股在本表各算一次（重複計數），不等於分散化後的曝險

# rr9 sector breakdown (top 5；|MV| 口徑，futures 用 notional 計，總和可 >100%):
#       semi           387,104.67  (55.50%)
#       cash           129,072.60  (18.51%)
#       index          126,282.32  (18.11%)
#       tech            30,768.51  ( 4.41%)
#       materials       24,222.25  ( 3.47%)

# rr9b sector directional exposure (top 4；口徑同 rr6-2 equiv_mv/rr8c，與 rr9 的 |MV| 不同軸，勿並排相減):
#       semi        +1,045,594.74  (+149.92%)
#       index         +418,919.51  ( +60.06%)
#       tech           +51,069.61  (  +7.32%)
#       materials      +24,222.25  (  +3.47%)
#     ↳ 與 rr9 差在 option：rr9 用 premium MV、本表用 Δ 等效曝險（22-09-2026 實帳 semi 50.45% vs 137.23%，差 2.7×）
#     ↳ **不穿透 ETF 籃子成分**（QQQ 內含的半導體不併入 semi）——穿透會與 index 那列重複計數；要看穿透口徑得另立欄位

# rr11 expiry ladder (option premium by DTE bucket；⚠️ 到期歸零的只有 ext＝extrinsic，intrinsic 到期轉成正股不歸零):
#       ≤30d               0.00  ( 0.00% NAV)  ext         0.00 ( 0.00% NAV)
#       31-60d             0.00  ( 0.00% NAV)  ext         0.00 ( 0.00% NAV)
#       61-90d        62,976.12  ( 9.03% NAV)  ext     4,664.12 ( 0.67% NAV)  TSM×2
#       91-180d      161,595.86  (23.17% NAV)  ext    44,972.86 ( 6.45% NAV)  QQQ×3 TSM×2 AVGO×1 GOOG×1 SMH×1 SOXX×1
#       >180d              0.00  ( 0.00% NAV)  ext         0.00 ( 0.00% NAV)
#     by expiry (roll / 平倉決策的實際單位):
#       2026-12-18 (  73 DTE)     62,976.12  ( 9.03% NAV)  ext     4,664.12 ( 0.67% NAV)  TSM×2
#       2027-01-15 ( 101 DTE)     74,071.18  (10.62% NAV)  ext    22,057.18 ( 3.16% NAV)  QQQ×3 SMH×1 TSM×1
#       2027-02-19 ( 136 DTE)     82,142.17  (11.78% NAV)  ext    20,940.17 ( 3.00% NAV)  AVGO×1 SOXX×1 TSM×1
#       2027-03-19 ( 164 DTE)      5,382.51  ( 0.77% NAV)  ext     1,975.51 ( 0.28% NAV)  GOOG×1
#     intrinsic/extrinsic split: intrinsic $174,935 (25.08% NAV，到期轉正股、不隨 θ 歸零) | extrinsic $49,637 (7.12% NAV ← 真正 at risk on θ 的規模)
#     moneyness split: ITM $224,572 (100.0% of premium) | OTM $0 (0.0%)

# rr12 unrealized P&L (cost = mv − UPL 反推；期貨以 margin 計故不列成本):
#       stock        +55,705.99  on cost     288,099.78  ( +19.34%)
#       option       +55,242.93  on cost     169,329.05  ( +32.62%)
#       total       +110,948.92  on cost     457,428.83  ( +24.25%)

# rr10 sharpe (年化；rf=4.02% via yfinance_^IRX):
#     ex-ante  (前瞻/持倉加權) Sharpe= 1.40  [ann_ret +106.59% / ann_vol 69.98% | 8 syms × 250d yf；gross_w 2.21]
#     realized (NAV序列/已實現) Sharpe= 0.01  [ann_ret  +4.26% / ann_vol 43.66% | 91 pts 2026-04-28..2026-10-06]
#              ⚠️ NAV 序列受出入金汙染且點數少，僅供交叉參考，非嚴格績效
#              ↳ 已剔除 1 個殘缺快照（summary 缺 cash 列＝xlsx 匯出被截斷）: 2026-08-10
```
