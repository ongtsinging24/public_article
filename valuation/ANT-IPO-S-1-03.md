# Anthropic, PBC — Form S-1（公開版 2026-10-26）摘錄

- EDGAR 原文: https://www.sec.gov/Archives/edgar/data/0002130357/000162828026067168/anthropicpbc-sx1.htm（CIK 0002130357，accession 0001628280-26-067168；HTML 約 14 MB，**不進版控**，需要時重抓）
- Nasdaq 代碼 **ANT**；價格、股數仍留白（報導目標 11-16 當週上市）
- 摘錄日: 2026-10-27（讀全文純文字版約 157 萬字元，逐段 grep 定位）
- 頁碼: 以 S-1 頁尾「N Table of Contents」標記推定（`p.N`）；財報附註為 `F-N`
- 用途: 估值卡（GOOG／AMZN／AVGO／AMD／MSFT／NVDA）引用 Anthropic 承諾額時的一手出處；**引用一律帶本檔列號（R1…）＋頁碼**
- 相關: memory `project_avgo_anthropic_financing_two_layers`；`log_gen_by_roma/video_digest/27-10-2026/digest_NaNa_1026-midterm-18of19-ok-hynix-not-4pct-spcx-lease-on-bs.md` R9

⚠️ 本檔所有金額為 Anthropic **支付義務**（承租側／買方側），不等於交易對手的營收或 backlog；換算到對手估值前先判角色（[[feedback_capex_commitment_vs_annual_spend]]）。

---

## 縮寫對照

| 縮寫 | 全稱 | 說明 |
|---|---|---|
| NPA | Note Purchase Agreement | 本票購買協議；這裡指 Anthropic 發給對手的可轉換本票額度 |
| PIK | Paid-in-kind | 利息不付現，累加進本金 |
| VWAP | Volume-weighted average price | 成交量加權均價 |
| take-or-pay | 最低承諾＋差額補足（true-up） | 用不滿也要付到最低額 |
| finance lease | 融資租賃 | ASC 842 下承租人表內認列 |
| Class N | Anthropic 無投票權普通股 | 本票轉股、策略投資人持有的股別 |

---

## S_1 總承諾與財務規模

| # | 原文要點 | 頁碼 |
|---|---|---|
| R1 | 截至 6-30：固定或最低保證承諾約 **$265.6B**，期限 1–20 年；另有無固定金額的算力協議，**不計入**此數但「預期金額重大」 | F-59 |
| R2 | 6-30 之後新簽／修訂：未來最低付款約 **$245B**（2026–2036 起算、最長 20 年，部分附條件）；另有短期合約最低 **~$21B** | F-65 起（Subsequent Events） |
| R3 | 2026H1 營收 **$16.3B**（2025H1 $1.2B）；營業虧損 $693M（2025H1 $2.1B）；Adjusted Operating Income **$1.6B** | p.137 |
| R4 | 淨虧損：2023 $1.5B、2024 $8.3B、2025 $42.0B、2026H1 **$80.7B**——主要是可轉債／衍生負債／SAFE 公允價值變動（非現金） | p.64 |
| R5 | 6-30 現金及約當現金 **$112.4B**、短期投資 $19.3B、受限現金 $2.5B（多為租約擔保） | p.173 |

> 媒體總額（$417B／$567B／$637B／~$650B）口徑不一；**以 R1＋R2 原文為準**，並註明是否含 R8 的 $125–150B 估計。

---

## S_2 逐對手承諾（Infrastructure Service Arrangements，p.171–172）

| # | 對手 | 原文要點 | 可取消性 | 頁碼 |
|---|---|---|---|---|
| R6 | **Microsoft** | 2025-11 簽、2026-02／10 修訂；最低 **$44.9B**，2026-11 至 2033-05 | 除 MSFT 重大違約或未交付分批外不可取消 | p.171 |
| R7 | **Google** | 2026-03 簽、05–08 修訂；最低約 **$114.5B**，2026-04 至 2033-07，用不滿須補差額（true-up） | 除 Google 重大違約外不可取消 | p.171 |
| R8 | Google 等 TPU 供應商（加購） | 2028–2031 交付的額外 TPU 算力，估計付款 **$125.0–150.0B**，**不在承諾表內**（依容量、部署、定價而定） | 附條件 | p.171 |
| R9 | **Amazon** | 2026-04 簽；最低 **$110.0B**，2026-05 至 2036-04，用不滿須補差額 | 除 Amazon 重大違約外不可取消 | p.172 |
| R10 | **SpaceXAI**（SpaceX 全資子公司，原 X.AI） | 2026-05~10 多份協議；NVIDIA GPU 算力，**最多 $120.5B**、期限至 2029；全部容量交付（預期 2026-12）後約 **$3.1B／月** | 初始不可取消期至 2027-01／2027-03，之後**任一方 90 天通知可取消** ⇒ 上限非下限 | p.172 |
| R11 | **Nscale** | NVIDIA GPU 算力，**最多約 $44.6B**、期限至 2033；容量交付並驗收後才計費；Nscale 須盡力取得 GPU／機房融資 | 附融資條件 | p.172 |
| R12 | **Lambda** | NVIDIA GPU 算力約 **$41.3B**、期限至 2034；其中 2026-08 協議約 $34.9B，Lambda 未及時取得機房租約則任一方可終止 | 部分附條件 | p.172 |
| R13 | **AMD** | 2026-07 硬體供應框架協議（Helios rack、MI450）；2027 年首批算力，無固定金額，若全數採購預期整個期間支出 **> $20.0B**（不在承諾表內） | 附部署條件 | p.164、p.172 |
| R14 | AMD（股權） | AMD 承諾依 GPU 交付／部署里程碑分批**最多買 $5.0B Class N 股票**；首個里程碑預期 2027 | — | p.164 |
| R15 | NVIDIA | 無直接金額；經 MSFT、SpaceXAI、Nscale、Lambda 等取得 NVIDIA 算力（含 Grace Blackwell、Vera Rubin） | — | 業務章節 |

**未提及**：CoreWeave、Nebius、Oracle、Meta、IREN／TeraWulf／Cipher／Hut 8（全文 0 次）。TSMC、SK hynix／Samsung／Micron 只出現在風險因子（供應集中）。

---

## S_3 Broadcom 租約與 $42B 本票

| # | 原文要點 | 頁碼 |
|---|---|---|
| R16 | 與 Broadcom 的**全部**五年期主設備租約（Lease Arrangements）租金合計約 **$161.2B（不含利息）**；以 **finance lease** 入帳；TPU 算力，部分 2026 上線、其餘 2027 起 | p.172 |
| R17 | 其中 2026-03「2026 Lease Arrangement」租金約 **$125.2B（不含利息）**，季付，設備 ready for service 起算；除違約外不可取消 | p.75 |
| R18 | 承租方為兩家 SPV 子公司，由 Anthropic, PBC 擔保，以租賃設備為擔保品；含交叉違約 | p.172 |
| R19 | Broadcom **打算把 2026 租約轉讓給指定金融夥伴**；2026 Q2 已將**其中一份主租約部分權利轉讓給第三方** | p.58–59、p.173 |
| R20 | Infrastructure Partner 2026 NPA：可發可轉換本票**最多 $42.0B**，持有人＝Broadcom **或其指定金融夥伴**（須 Anthropic 同意、不得無理拒絕），**只能用來付 2026 租約季租** | p.166–167 |
| R21 | 條款：9.00% PIK（營收條件未達時 13.00%、轉換價 85%）；轉 Class N＠30 日 VWAP 90%；期限：前 $24B 60 個月、$24–32B 63 個月、$32B 以上 57 個月；次順位擔保；控制權變更時持有人可要 150% 本息 | p.167 |
| R22 | 動用期**尚未起算**（設備 ready for service 才開始）；**截至招股書一張未發**，預期 IPO 前不發 | p.167、p.302 |
| R23 | 6-30 帳上 finance lease 負債僅 **$443M**（2025 年底為 0）⇒ $161.2B 自 2027 起隨設備上線逐步上表 | F-36 |
| R24 | 受限現金：2026-04 存入受限帳戶「for the benefit of Broadcom」，在特定情況下最多還可能再受限 **$10.0B** | p.75、F-36 |

**S-1 未提及**：$60B SPV 銀團、Blackstone（只出現在一位董事的履歷）、AVGO 10-Q 的 $29B backstop。這些都在出租側，要看 AVGO 自己的揭露。

---

## S_4 其他 NPA（策略股東的融資額度，p.164–166）

| # | 對手 | 原文要點 | 頁碼 |
|---|---|---|---|
| R25 | Google 2026 NPA | 額度 **$20.0B**，動用期至 2030-12；若 Google 在 IPO 時以發行價私募 Class N，額度最多減 **$10.0B**。2023／2024 舊本票已全數轉成無投票權可贖回可轉換優先股 | p.164–166 |
| R26 | Amazon 舊本票 | 2023／2024 NPA 剩餘本金約 **$6.2B**；IPO 時在 Amazon 持股上限內轉股，轉不完的每季末續轉，到期仍轉不完則付現 | p.58、p.164 |
| R27 | Amazon 2026 NPA | 額度 **$15.0B**，動用期為 IPO 後 30 個月 | p.166 |

---

## S_5 對我方估值卡的用法（2026-10-27 判讀，非原文）

| 標的 | 可引用 | 注意 |
|---|---|---|
| GOOG | R7、R8、R25 | IPO 後 Anthropic 持股有公開市價 ⇒ **MTM 每季依 ANT 股價波動**，other income 污染常態化（[[feedback_consensus_eps_contaminated_by_oneoff]]） |
| AMZN | R9、R26、R27 | 同上；AMZN.md 既有的 $3.80/股剔除口徑之後要逐季重算 |
| AVGO | R16–R24 | $161.2B 是 Anthropic 租金，**≠ AVGO 營收**；租約轉讓比例未揭露 |
| AMD | R13、R14 | 2027 年 MI450 營收能見度；AMD 成為股東後也會有 MTM |
| MSFT | R6 | MSFT 是否持有 Anthropic 股權本檔未查 |
| NVDA | R10～R12、R15 | 間接需求，不可直接加進 NVDA 營收 |
| CRWV／NBIS | — | S-1 零提及；同業比較改用 Nscale S-1（EDGAR CIK 0002110365，2026-09） |
