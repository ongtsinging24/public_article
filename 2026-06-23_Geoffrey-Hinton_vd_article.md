# 傑夫里·辛頓（Geoffrey Hinton）：深度學習教父的傳奇

> 縮寫對照：**AI** = 人工智慧；**NN** = 神經網路（Neural Network）；**CIFAR** = 加拿大高等研究院（Canadian Institute for Advanced Research）；**NCAP** = 神經計算與適應性感知（Neural Computation and Adaptive Perception）；**FRS** = 英國皇家學會院士（Fellow of the Royal Society）

## 1　簡介　傑夫里·辛頓

傑夫里·埃弗里斯特·辛頓（Geoffrey Everest Hinton，生於 1947 年）是英裔加拿大籍的認知心理學家與電腦科學家，被尊稱為「**深度學習教父**」（Godfather of Deep Learning）。他半世紀的研究——**反向傳播**（backpropagation）、**波茲曼機**（Boltzmann machine）、**深度信念網路**（deep belief nets），以及 2012 年點燃整場 AI 革命的 **AlexNet**——構成了當代神經網路的理論骨幹。

榮譽包括 2018 年圖靈獎（與 Yann LeCun、Yoshua Bengio 共獲，三人合稱「深度學習三巨頭」），以及 **2024 年諾貝爾物理學獎**（表彰其以物理方法奠定機器學習基礎）。2023 年他離開 Google，公開警示 AI 的潛在風險，成為業界最受矚目的「吹哨者」之一。

## 2　辛頓的傳奇家族背景

辛頓出身一個橫跨數學、邏輯、測量與科學的「智識王朝」（intellectual dynasty），其家譜幾乎是一部濃縮的科學史：

| 人物 | 關係 | 成就 |
|----------------|------------------|--------------------------------------|
| George Boole | 高祖父（great-great-grandfather） | 布林代數（Boolean algebra）之父，數位邏輯的源頭 |
| Mary Everest Boole | 高祖母 | 數學教育家；Boole 之妻 |
| George Everest | 高祖母的伯父 | 印度測量總監，**聖母峰（Mount Everest）以其命名** |
| Charles Howard Hinton | 曾祖父（great-grandfather） | 數學家，創造「tesseract（超立方體）」一詞，研究四維幾何 |
| Mary Ellen Boole | 曾祖母 | George Boole 之女，嫁給 C. H. Hinton |
| George Boole Hinton | 祖父 | 採礦工程師 |
| Howard Everest Hinton | 父親 | 著名昆蟲學家，布里斯托大學教授、FRS |

辛頓的中間名「**Everest**」即源自這條與聖母峰共享的血脈。值得一提的是，他的遠親還包括參與曼哈頓計畫、後赴中國的核物理學家瓊·辛頓（Joan Hinton，中文名「寒春」）。可謂「天才，是會遺傳的」。

## 3　辛頓的求學過程

> 縮寫對照：**MRC** = 英國醫學研究委員會（Medical Research Council）；**PDP** = 平行分散式處理（Parallel Distributed Processing）；**DARPA** = 美國國防高等研究計畫署

辛頓的求學史是一部「**屢試屢換、屢換屢退**」的反覆橫跳——但貫穿其中的，是一條始終不變的主線：**搞懂「大腦/心智究竟如何運作」**。出身第 2 節那個「智識王朝」，家族對成功的期待如影隨形（他日後自承「家庭因素逼我必須成功……其中有快樂，但更多是焦慮」），這份壓力與他真正的好奇心，構成他一路轉系的張力底色。

### 3.1　中學：克利夫頓公學（Clifton College）
辛頓於布里斯托的私立名校 **Clifton College** 完成中學教育。也正是在這裡，一位同學首次向他提到「大腦可能像**全像片（hologram）** 一樣儲存記憶」——分散式表徵的種子，早早埋下。

### 3.2　劍橋大學國王學院（King's College, 1967–1970）：一部「連環輟學記」
1967 年入學後，辛頓的主修像走馬燈一樣換個不停，堪稱「**慣性輟學者**（habitual dropout）」：

1. 先讀**物理與化學**——**一個月**就退掉；
2. 隔一年回來，到建築系上了**整整一天**課，又轉走；
3. 改念**物理與生理學**——再退；
4. 轉攻**哲學**——還是退；
5. 最後落腳**實驗心理學**，於 **1970 年**總算拿到學士學位。

諷刺的是，他發現連心理學也**回答不了「心智如何運作」**這個他最在意的問題——這份對既有學科的集體失望，正是他日後轉向「用神經網路逆向工程大腦」的最初動力。

### 3.3　木工歲月（carpentry interlude）
拿到學位後，辛頓並未直奔研究所，而是**當了約一年木工**。他終生熱愛木工，曾說：「我一直熱愛木工，也常想，如果當了建築師會不會更快樂。做科研時我總得逼自己……」——這段「逃離學術」的插曲，反襯出他最終回頭做研究，是出於難以擺脫的內在追問（與家族期待）。

### 3.4　愛丁堡大學博士（1972–1978）：逆風中的孤獨堅持
- 1972 年入學，師從 **Christopher Longuet-Higgins**，1978 年取得**人工智慧博士**，論文題為《**Relaxation and Its Role in Vision**》（鬆弛法在視覺中的角色，1977/78）。
- **最大的反諷**：他選 Longuet-Higgins 正因對方曾是神經網路的支持者，沒想到入學時這位導師**剛剛「叛變」轉向符號主義 AI**。於是整個博士生涯，辛頓幾乎是**在自己導師與主流學界的雙重質疑下**，獨自死守「類腦／連結主義」路線——這份在寒冬中不改其志的執拗，正是日後第 5 節「神經網路密謀」的人格原型。

### 3.5　學術流浪與早期任職
博士畢業後，神經網路依舊冷門，辛頓四處輾轉、居無定所：
- 英國 **Sussex 大學**、**MRC 應用心理學研究單位（Applied Psychology Unit）**；
- 再赴美國 **加州大學聖地牙哥分校（UCSD）**，加入 Rumelhart、McClelland 的 **PDP（平行分散式處理）小組**——這是連結主義復興的大本營，1986 年三人合作的論文讓**反向傳播**廣為人知；
- 之後任教 **卡內基美隆大學（CMU）**。

### 3.6　落腳多倫多大學（1987 起）
1987 年，辛頓因**不願接受美國軍方（DARPA 等）研究經費**而移居加拿大，長期任教於 **多倫多大學**，並把這裡經營成深度學習的全球重鎮（後與第 12 節 Zemel 共同奠基 Vector Institute）。一場橫跨二十年的「學術流浪」，至此終於定錨。

## 4　辛頓的學術血脈：門生即半部 AI 產業史

辛頓的**直系博士生**包括：**Ilya Sutskever、Alex Krizhevsky、Ruslan Salakhutdinov、Radford Neal、Richard Zemel、Brendan Frey**；**博士後**則有**楊立昆（Yann LeCun）、Peter Dayan、Max Welling、Zoubin Ghahramani、Alex Graves**。這份名單幾乎就是現代 AI 產業的核心人名錄：

- **Ilya Sutskever**——AlexNet 共同作者、OpenAI 共同創辦人暨前首席科學家（ChatGPT 背後的關鍵推手）。
- **Alex Krizhevsky**——AlexNet 第一作者，2012 年 ImageNet 奪冠引爆深度學習浪潮。
- **Ruslan Salakhutdinov**——前 Apple AI 研究總監、CMU 教授。
- **楊立昆（Yann LeCun）**——卷積神經網路之父、Meta 首席 AI 科學家、圖靈獎共得主。
- **Max Welling / Zoubin Ghahramani**——分別在貝氏深度學習、機率機器學習領域舉足輕重（後者曾任 Google/DeepMind 與 Uber AI 要角）。
- **Alex Graves**——LSTM 序列模型與神經圖靈機的重要貢獻者（DeepMind）。

> 一個關鍵歷史節點：2012 年 Hinton、Sutskever、Krizhevsky 三人成立 **DNNresearch**，旋即被 Google 收購，Hinton 自此一腳跨入工業界，門生則散佈至 OpenAI、Google、Meta、Apple，奠定今日 AI 版圖。

## 5　2004 年「神經網路密謀」

進入 2000 年代初，神經網路再度跌入低谷——主流轉向 SVM 等方法，NN 被視為過時。2004 年，辛頓向 **CIFAR** 成功提案，啟動了 **神經計算與適應性感知（NCAP）** 計畫，業界戲稱為「**神經網路密謀**（the neural network conspiracy）」。

這並非陰謀，而是一場刻意的「逆勢結社」：

- **目的**：在學界普遍唱衰的寒冬中，為深度學習研究社群提供**社會性基礎設施**（social infrastructure）——資金、定期聚會、跨域對話，讓火種不滅。
- **成員**：匯聚 Yoshua Bengio、Yann LeCun，以及神經科學家、生物學家、物理學家、心理學家等跨領域研究者。
- **影響**：辛頓領導 NCAP 長達十年。正是這個小圈子的堅持，撐過了 2006–2012 年的關鍵醞釀期（深度信念網路、預訓練、GPU 加速逐一突破），最終在 2012 年 AlexNet 一役全面引爆，徹底改寫科技與資本市場格局。

這場「密謀」的回報極為豐厚：圖靈獎、諾貝爾獎，以及一個市值以兆美元計、由其門生主導的 AI 產業。

## 6　AlexNet 深度剖析：寒冬終結的那一刀

> 縮寫對照：**CNN** = 卷積神經網路（Convolutional Neural Network）；**ReLU** = 線性整流單元（Rectified Linear Unit）；**ILSVRC** = ImageNet 大規模視覺辨識挑戰賽；**SOTA** = 當時最佳水準（State-of-the-art）；**top-5 error** = 模型前 5 個猜測都沒中的錯誤率

第 5 節那場「神經網路密謀」撐過的 2006–2012 醞釀期，回報就兌現在 **AlexNet** 這一役。它既是辛頓學術血脈的集大成（三位作者全在第 4 節的名單上），也是下一節 NVDA 兆美元敘事的技術第 0 天，值得單獨一節講透。

### 6.1　AlexNet 是什麼

2012 年由 **Alex Krizhevsky（第一作者）、Ilya Sutskever、Geoffrey Hinton** 三人發表的論文《ImageNet Classification with Deep Convolutional Neural Networks》（業界俗稱 AlexNet，以第一作者命名）。它是一個 **8 層的深度 CNN**（5 層卷積 + 3 層全連接），約 **6,000 萬參數、65 萬個神經元**，任務是把 ImageNet 的 120 萬張圖片分到 1,000 個類別。

它的歷史地位不在於「發明」了什麼全新理論——CNN 早在 1989 年就由楊立昆（LeCun）的 LeNet 做出來了——而在於**第一次證明「深 + 大數據 + GPU」這條路能在真實世界尺度上輾壓所有傳統方法**。

### 6.2　為什麼是「引爆點」：ILSVRC 2012 那一戰

| 指標 | 數字 | 意義 |
|----------------------|----------|----------------------------|
| AlexNet top-5 error | **15.3%** | 奪冠 |
| 第二名（傳統方法） | **26.2%** | 用 SVM／手工特徵 |
| 領先差距 | **約 11 個百分點** | 在電腦視覺界是「碾壓級」斷層 |

在此之前，ILSVRC 的進步是每年擠牙膏式的 1–2%。AlexNet 一次砍掉近 11 個百分點，等於把整個領域過去十年的「手工特徵工程」路線一夜宣判出局。**這就是「深度學習寒冬」結束、AI 黃金十年開始的那一刀。**

### 6.3　四個關鍵技術創新（為什麼它能贏）

1. **ReLU 取代 sigmoid/tanh**：激活函數改用 `max(0,x)`，不會在兩端飽和導致梯度消失，訓練速度快了約 **6 倍**——這是「深網路終於訓得動」的關鍵。今天幾乎所有網路仍用 ReLU 家族。
2. **雙 GPU 平行訓練（GTX 580 × 2）**：這正是下一節 NVDA 那段的技術內核。單張 GTX 580 只有 **3GB 顯存**，裝不下整個 6,000 萬參數的網路，於是他們把網路「**切兩半、各跑一張卡**」，只在特定層交換資料。這個被顯存逼出來的工程妥協，意外地既是平行化先驅、又是黃仁勳口中「AI 從這兩張卡開始」的實體起點。
3. **Dropout**：訓練時隨機關掉一半神經元，強迫網路不依賴單一路徑，大幅抑制過擬合——辛頓本人的招牌正則化發明。
4. **資料增強（data augmentation）**：對訓練圖做隨機裁切、翻轉、PCA 色彩擾動，等於免費把資料集放大，再壓低過擬合。

### 6.4　被應用「追認」的 GPU

值得補一個常被忽略的點：AlexNet 之所以選 GPU，**不是因為 GPU「為 AI 設計」，而是因為它便宜、平行、剛好能算矩陣乘法**。也就是說，NVDA 護城河的起點是一場「**被應用追認**」的運氣 + CUDA 十年生態卡位的必然。理解這個「先有顯卡、後被 AI 認領」的次序，正是理解 NVDA 敘事為何是「結構性」而非「週期性」的根。

> **投資視角**：AlexNet 是「需求證明鏈」的第 0 天——
> `AlexNet(2012, 顯存逼出的雙卡平行) → 證明 GPU = AI 算力載體 → CUDA 生態綁定 → 資料中心 GPU 需求啟動 → NVDA 從繪圖品牌變兆美元算力帝國`。
> 同時，「AlexNet 三作者」也是後續人脈分流的源頭：Krizhevsky 點火後低調隱退（見第 12 節）、Sutskever 順勢成為 OpenAI 首席科學家再到 SSI（$32B）。下一節將承接這條鏈，講辛頓與黃仁勳的歷史交會。

## 7　辛頓 & 黃仁勳（NVDA / Jensen Huang）

辛頓與黃仁勳之間沒有師徒或共事關係，但兩人的命運在 **2012 年的 AlexNet** 上發生了歷史性交會——這也是 NVDA 從「遊戲顯卡公司」蛻變為「AI 算力帝國」的引爆點。

- **GTX 580 的傳奇**：辛頓的兩名學生 Alex Krizhevsky、Ilya Sutskever 用**兩張 NVIDIA GTX 580（3GB，SLI 串接）** 訓練出 AlexNet，2012 年於 ImageNet 競賽碾壓奪冠。網路被特別優化成在雙 GPU 上跑、僅在必要時交換資料，大幅縮短訓練時間。
- **黃仁勳的「認證」**：黃仁勳多次（包含在 Joe Rogan podcast）公開表示——當代 AI 「全是從 2012 年那兩張 GTX 580 開始的」；若沒有那對顯卡，NVIDIA 可能至今仍只是個「繪圖品牌」。
- **互補的兩條曲線**：黃仁勳早年押注「GPU 不只用來畫圖」並建立 **CUDA** 生態；辛頓則用數十年逆勢堅持，提供了**驗證這個賭注的殺手級應用**。一個造槍、一個證明子彈有用——共同點燃了 NVDA 兆美元市值的引信。

> **投資視角**：AlexNet→CUDA→資料中心 GPU 的這條「需求證明鏈」，是理解 NVDA 結構性護城河（軟硬體生態綁定）敘事的源頭；辛頓那條學術血脈（門生散佈 OpenAI/Google/Meta）至今仍是 NVDA 終端需求的核心買方。

## 8　辛頓 & 馬斯克（Elon Musk）

辛頓對馬斯克的態度，是其「AI 安全吹哨者」立場的縮影——**理念分歧明確、且公開保持距離**。

- **婉拒 xAI**：辛頓婉拒加入 xAI 顧問相關邀約，並公開質疑該公司「偏離了對安全的承諾」。
- **核心分歧**：辛頓 2023 年離開 Google 後，反覆警示三類風險——惡意行為者濫用、技術性失業（job losses 衝擊社區）、以及 AGI 的存在性風險（existential risk）。他對 Grok 轉向「去過濾／NSFW」內容、xAI 弱化內部安全團隊的方向明顯不以為然。
- **時代背景（2026 上半）**：xAI 安全爭議持續發酵——OpenAI、Anthropic 研究者公開批評其安全做法「魯莽」「極不負責」；6 月並有前 xAI 工程師控告公司因其示警 Grok 安全問題而將其解雇。辛頓的立場與這股批評浪潮同調。

> **投資視角**：辛頓 vs. 馬斯克 代表 AI 產業「安全派 vs. 加速派」的路線張力。對追蹤 xAI（及其與 SpaceX/Tesla 資金、IPO 連動）的部位而言，這條監管/聲譽風險線值得持續納入避險評估。

## 9　辛頓 & 谷歌（GOOG / Alphabet）

辛頓與 Google 是一段「**高價聯姻、體面分手**」的關係，貫穿其十年（2013–2023）的工業界生涯。

- **2012–2013 收購**：辛頓與兩名學生成立 **DNNresearch**（多倫多大學 spinout）。2013 年 3 月 Google 以約 **4,400 萬美元** 收購（傳為 Google、Microsoft、DeepMind、Baidu 競價搶人的結果）。此後辛頓「一半時間做學術、一半時間在 Google」。
- **在 Google 的貢獻**：其影像辨識技術被用於強化 Google 相簿搜尋等產品；他也持續推動 Google Brain 體系的深度學習研究。
- **2023 年 5 月請辭**：辛頓公開離開 Google，理由是想「自由地談論 AI 的風險」，並坦言「對自己畢生工作有一部分感到後悔」。他特別點出：身為 Google 員工的**利益衝突**，妨礙了他公開示警的自由。他也強調此舉不是為了批評 Google（稱 Google 在此議題上「行為相當負責任」），而是為了能無拘束地發聲。

> **投資視角**：辛頓的加入（2013）與離開（2023）剛好框住 Google 在深度學習的黃金十年；他離場時點亦與生成式 AI 競賽白熱化（ChatGPT 衝擊 GOOG 搜尋護城河）同期，可作為理解 Alphabet AI 敘事轉折的人物錨點。

## 10　辛頓 & 楊立昆（Yann LeCun）

辛頓與楊立昆是「**師出同門、同台封神，卻在安全議題上分道揚鑣**」的經典案例——既是深度學習史上最緊密的合作血脈，也是當代 AI 風險辯論中最鮮明的對立兩極。

- **師徒淵源**：1987–1988 年，楊立昆完成博士後即赴多倫多大學，進入辛頓的研究組做**博士後**。據述他是讀了辛頓論文、深受啟發後主動找上門的。這段師承後來開花結果——楊立昆成為**卷積神經網路（CNN）之父**、Meta 首席 AI 科學家。
- **同台封神**：2018 年兩人與 Yoshua Bengio 共獲**圖靈獎**（深度學習三巨頭）；外加辛頓的諾貝爾物理獎，這條血脈幾乎壟斷了 AI 領域的最高榮譽。
- **核心分歧——存在性風險（x-risk）**：
  - **辛頓（警鐘派）**：2024 年底轉趨悲觀，估計未來三十年 AI 導致人類滅絕的機率「**10–20%**」。其核心論點——一旦 AI 遠比人類聰明，傳統「控制」將失效（少有「低智支配高智」的先例）。他並提出 AI 應內建「**母性本能（maternal instincts / maternal AI）**」以保護人類。
  - **楊立昆（樂觀派）**：認為現行 AI **不構成真正的存在性威脅**，x-risk 論調被過度誇大；甚至暗指這是大型科技公司用來鞏固權力、收緊監管的「話術」。他主張務實推進能力，而非被末日敘事綁架。
- **同源異流的意義**：兩人共享同一套科學地基，卻對「這套技術會不會反噬人類」給出相反答案——這場辯論本身，正是 AI 產業最深層不確定性的人格化體現。

> **投資視角**：辛頓 vs. 楊立昆 = 「監管收緊風險 vs. 加速開放（如 Meta 的開源 Llama 路線）」的縮影。對佈局 AI 板塊者，這條「安全派 vs. 開源加速派」的張力，直接牽動未來監管力度、開源/閉源商業模式與雲端算力需求結構——是中長線敘事的關鍵分水嶺。

### 番外：楊立昆 vs 馬斯克 —— 推特上的「酸宴」

如果說辛頓 vs 楊立昆是「安全 vs 加速」的**學理對決**，那麼楊立昆 vs 馬斯克就是同一條光譜上的**人身火拼**——兩人自 2024 年起在 X（前 Twitter）上公開交火，至 2025 年仍未停火。

- **導火線（2024-05）**：馬斯克發文替 xAI 招募，楊立昆隨即開酸——批評馬斯克一邊聲稱要「極致嚴謹地追求真理」，一邊散布「瘋癲的陰謀論」；並嘲諷其「明顯造假」的預測（「AGI 明年就到」「2020 年百萬輛 robotaxi」始終跳票）。
- **楊立昆的核心立場——科研需開放**：他主張前沿研究**必須公開發表**，保密只會拖慢進展、嚇跑人才。值得注意的是他並非全盤否定馬斯克——曾公開說「我喜歡他的車（自己就有兩台 Model S）、火箭、太陽能與衛星通訊，也認同他在開源與專利上的立場」，但在 AI 議題上「強烈不同意」。這種「對事不對人」的切割，反而讓批評更具殺傷力。
- **2025 升級——「xAI 是個失敗」**：楊立昆近一步唱衰，稱 xAI「基本上算失敗」，理由是**除馬斯克外幾乎所有創始成員都已出走**，並譏其本質淪為「**租資料中心的二房東**」（rent-a-data-center，靠轉租算力回血）。

> **投資視角**：這場口水戰看似八卦，實則是兩種 AI 商業模式的對撞——**Meta 開源路線（LeCun/Llama）vs xAI 閉源 + 重資本算力路線（Musk）**。楊立昆點名的「創始團隊出走、淪為算力二房東」若屬實，正是評估 xAI 估值（及其與 SpaceX/Tesla 資金、潛在 IPO 連動）時最該盯的**人才流失 + 商業模式空心化**雙風險；與第 8 節辛頓對 xAI 安全的質疑，構成「安全 + 體質」兩路夾擊。

## 11　辛頓 & Sam Altman（OpenAI）

辛頓與 Sam Altman 之間**沒有師承、也無共事**，但 Altman 是本篇繞不開的人物——他的連結透過兩條線交會於辛頓：一是**門生 Sutskever**（辛頓首席弟子、OpenAI 共同創辦人），二是貫穿全篇的**「安全 vs 營利」路線之爭**。而辛頓本人，曾極不尋常地對 Altman 公開「補刀」。

- **諾貝爾記者會的金句（2024-10）**：辛頓在獲頒諾貝爾物理獎當天的記者會上主動表示——「我特別**自豪**，我的一個學生（Sutskever）**開除了 Sam Altman**。」被追問這句針對性發言時，他解釋：「久而久之，事實證明 **Sam Altman 對安全的關注，遠不及對營利的關注**，我認為這很不幸。」
- **連結點 Sutskever**：2023 年 11 月，身為 OpenAI 董事的 Sutskever 投票罷免 Altman（見第 12 節）。政變雖在數日內逆轉、Altman 回鍋，但 Sutskever 隨後於 2024 年 5 月離開，另創安全優先的 **SSI**。辛頓的「自豪」正是把這條師承血脈，明確標定在自己的「安全派」陣營這一側。
- **路線分歧的本質**：OpenAI 設立初衷以安全為核心（「開發 AGI 並**確保其安全**」）；辛頓的批評是它**逐漸從安全使命漂移向商業化**。這與第 8 節（馬斯克／xAI 弱化安全）、第 10 節（楊立昆唱反調）構成同一張「安全派 vs 加速派」光譜——只是這次辛頓的箭頭直指 OpenAI 的當家 CEO。

> **投資視角**：Altman 是 AI「加速／商業化派」最具份量的代表，OpenAI 從非營利初衷轉向營利結構、加上 2023 董事會動盪，使其**治理風險**成為整個 AI 敘事的人物錨。對追蹤未上市 AI 純度標的者，這條線同時牽動兩端——OpenAI（估值最大的私有 AI 資產、潛在 IPO）與 Sutskever 出走後的 **SSI（$32B）**；兩者的此消彼長，本質上就是「Altman 路線 vs 辛頓路線」在資本市場上的對價。

### 延伸：達里奧·阿莫代伊（Dario Amodei / Anthropic）vs Altman —— 另一個從 OpenAI 出走的安全派

如果 Sutskever 是「**從內部**用董事會票罷免 Altman」的安全派，那麼 **達里奧·阿莫代伊** 就是更早「**直接出走另立門戶**」的那一個——兩條線同源（都來自 OpenAI、都打安全旗號），構成 Altman 身邊「安全派出走」的雙生案例。

- **出走始末（2016–2021）**：阿莫代伊 2016–2020 年在 OpenAI 任**研究副總裁**（主攻安全），就在 Altman 麾下。他對 OpenAI **在擴大 ChatGPT 規模時的安全鬆動**愈發不安，2021 年與妹妹 Daniela 及十餘名前 OpenAI 員工出走，創辦 **Anthropic**，定位「安全優先」的對手。
- **真正的裂痕——是「信任」不只是「政策」**：阿莫代伊近期澄清，安全分歧並非唯一原因；壓垮他的是**信任崩潰**——「當你覺得無法信任一個人、覺得他的價值觀與他口中說的不一致、覺得他不誠實時」。這把矛頭比單純的技術路線之爭更直指 Altman 個人。
- **2026 的白熱化**：兩家的競爭已升級為公開敵意——2026 年 2 月印度 AI 峰會上，兩位 CEO **在台上拒絕牽手**（viral 畫面，阿莫代伊事後稱「峰會極度混亂」）；此前 Anthropic 更砸下四支 **Super Bowl 廣告**（主題 *A Time and a Place*）影射 OpenAI 在 ChatGPT 裡塞廣告的爭議。

> **投資視角**：Sutskever（SSI）與 Amodei（Anthropic）是辛頓「安全派」敘事在資本市場的**兩個最大落地標的**，且都直接從 Altman 的 OpenAI 分裂而出。**Anthropic vs OpenAI** 已是當前最關鍵的閉源前沿雙雄對決——牽動雲端算力歸屬（Anthropic↔AMZN/GOOG、OpenAI↔MSFT）、企業 API 市占與監管站隊。追蹤 AI 私有資產對價時，這組「Altman vs Amodei」是比「Altman vs Musk」更具基本面含金量的一條線。

## 12　辛頓 & 直系博士生群像：可補充的故事

辛頓的多倫多研究組，是一個「**論文掛名橫跨三十年、彼此互為合著者**」的緊密家族。1990 年代他們就一起做出兩篇奠基之作——**Wake-Sleep 演算法**（Science 1995，Hinton–Dayan–Frey–Neal 合著）與 **Helmholtz Machine**（Dayan–Hinton–Neal–Zemel）。以下逐一補述：

### Ilya Sutskever — 從 AlexNet 到「政變」再到 SSI
- 辛頓最著名的門生。AlexNet 共同作者、seq2seq 奠基者、**OpenAI** 共同創辦人暨前首席科學家（GPT/ChatGPT 的關鍵推手）。
- **戲劇性轉折**：2023 年 11 月，身為董事的他投票**罷免 Sam Altman**，引爆 OpenAI 內亂；事敗後逐漸淡出，2024 年 5 月離職。
- **新局**：2024 年 6 月創立 **Safe Superintelligence（SSI）**——主打「唯一產品就是安全的超智能，在那之前不出任何商業產品」。2024 年 9 月募 10 億美元，2025 年 3 月再募 20 億、估值傳達 **$32B**（幾乎純靠其聲望）。其「安全優先」路線與恩師辛頓的憂慮一脈相承。

### Alex Krizhevsky — 點火者，卻悄然退場
- **AlexNet 第一作者**，2012 年 ImageNet 一役改寫歷史。
- 鮮為人知的貢獻：他一手整理出 **CIFAR-10 / CIFAR-100** 影像資料集（沿用至今的基準）。
- **反差故事**：他在引爆 AI 革命後反而**低調隱退**，約 2017 年離開 Google、淡出主流研究圈——與 Sutskever 的鋒芒形成強烈對比，是「點火者未必想當主角」的典型。

### Ruslan Salakhutdinov — 把深度學習帶進蘋果
- 深度波茲曼機（Deep Boltzmann Machines）的核心推手，CMU 教授。
- 2016 年成為 **Apple 首任 AI 研究總監**，是學界大牛跨入頂級科技公司的早期代表；象徵 AAPL 在這波 AI 浪潮的補課起點。

### Radford Neal — 貝氏與 MCMC 的隱形巨人
- 1994 年博士論文《**Bayesian Learning in Neural Networks**》是貝氏神經網路的開山之作。
- 在 **MCMC、HMC（Hamiltonian Monte Carlo）、糾錯碼** 領域影響深遠——今日機率程式設計（如 Stan）的取樣核心都站在他的肩膀上。屬「不在鎂光燈下、卻被無數論文引用」的學者典型。

### Richard Zemel — 從 MDL 到打造 Vector Institute
- 1994 年博士論文以「最小描述長度（MDL）」框架做非監督學習。
- 後來成為加拿大 **Vector Institute**（與辛頓共同奠基的 AI 重鎮）的研究要角、Columbia 教授——把老師的學術香火制度化、組織化。

### Brendan Frey — 把深度學習轉向「治病救人」
- 1997 年博士做圖模型與數位通訊（factor graph / sum-product 演算法的重要貢獻者）。
- **最具人文色彩的轉向**：他將 AI 用於**基因體醫學**，2015 年創辦 **Deep Genomics**（以深度學習預測基因變異、加速新藥開發）。據報導其投入部分源於切身的家庭基因遭遇——是「AI 三巨頭血脈裡，最早把技術引向生技/製藥」的人。

> **投資視角**：這份門生地圖標出了 AI 算力需求的**終端買方分布**——OpenAI（Sutskever 舊巢）、SSI（$32B 新勢力）、Apple（Salakhutdinov）、Vector Institute（Zemel）、生技製藥（Frey/Deep Genomics）。理解「辛頓血脈流向何處」，就是理解未來幾年 GPU/雲端算力與 AI 應用落地的需求版圖；而 Sutskever 的 SSI 更是值得追蹤的非上市 AI 純度標的（潛在 IPO/估值錨）。

## 13　辛頓 & 直系博士後群像：可補充的故事

相對於博士生多是「年輕被帶大」，這批**博士後**多半是帶著各自鋒芒來找辛頓「鍍金、碰撞」的成熟學者——他們把辛頓的連結主義往**神經科學、生成模型、貝氏、記憶網路**四個方向擴張。（楊立昆已見第 10 節，此處不重複。）

### Peter Dayan — 把 AI 接回大腦的人
- 與辛頓合著 **Helmholtz Machine / Wake-Sleep**（1990s 非監督學習奠基）。
- **最深遠的貢獻**：他提出「**多巴胺訊號 = 獎勵預測誤差（reward prediction error）**」，把強化學習（RL）的 TD/Q-learning 與大腦獎勵機制對接——這是**計算神經科學的里程碑**，至今仍是「AI ↔ 腦科學」雙向啟發的核心橋樑。
- 現任德國 **Max Planck 生物控制論研究所**所長（曾長期執掌 UCL Gatsby Unit）。

### Max Welling — 生成式 AI 的「另一條源頭」
- **最關鍵貢獻**：2013 年與 Diederik Kingma 共同發表《Auto-Encoding Variational Bayes》，提出 **VAE（變分自編碼器）**——與 GAN 並列為深度生成模型兩大支柱，是今日生成式 AI 的理論源頭之一。
- 也是**圖神經網路（GNN）、等變性（equivariance）** 的重要推手。
- **產學雙棲**：阿姆斯特丹大學教授；企業端歷任 **Qualcomm**（技術副總，主攻邊緣端 AI）與 Microsoft Research；創業端 Scyfer（賣給 Qualcomm）、近期創辦 **CuspAI**（用 AI 設計新材料，如碳捕捉材料）。

### Zoubin Ghahramani — 貝氏旗手，如今掌 Gemini 研究
- 1995 年赴多倫多大學跟辛頓做博士後；之後成為**貝氏機器學習**最重要的旗手之一、劍橋大學教授。
- **創業到大廠**：共同創辦 **Geometric Intelligence → 賣給 Uber**（成 Uber AI Labs 首席科學家）；後加入 Google，現任 **Google DeepMind 研究副總裁**，深度參與 **Gemini** 等旗艦模型。是辛頓血脈中**最貼近 GOOGL 當前 AI 主戰場**的人。

### Alex Graves — 「雙教父」門徒，記憶網路的開創者
- 罕見地**同時師承兩位 RNN/深度學習教父**：先在慕尼黑跟 Schmidhuber（LSTM 之父），後到多倫多跟辛頓。
- **關鍵貢獻**：**CTC（連結時序分類）** 讓 LSTM 真正能用於語音辨識與手寫辨識（2009 年首個贏得比賽的 RNN）；2014 年提出 **神經圖靈機（Neural Turing Machine）** 與 DRAW，開啟「**記憶增強神經網路**」一脈——可視為今日 agentic AI／外部記憶的思想前身。長年任 **DeepMind** 研究科學家。

> **投資視角**：博士後血脈把訊號指向幾個關鍵節點——**Ghahramani → Google DeepMind/Gemini（GOOGL 的 AI 核心戰力）**；**Welling → Qualcomm（QCOM 邊緣 AI）＋ CuspAI（AI×新材料/碳捕捉，一條被低估的 AI 應用賽道）**；**Graves → 記憶增強網路（agentic AI 的思想源頭）**；**Dayan → 神經科學橋樑（長線決定下一代架構走向）**。其中 Ghahramani 在 Gemini 的位置，是評估 Alphabet 能否守住 AI 第一梯隊的人物級觀察點。

---

## Sources

- [Geoffrey Hinton — Wikipedia](https://en.wikipedia.org/wiki/Geoffrey_Hinton)
- [The Hinton Intellectual Dynasty — Yiqin Fu](https://yiqinfu.github.io/posts/hinton-intellectual-dynasty/)
- [Geoffrey Hinton Family Tree: From Mount Everest to AI — Larry Cao](https://www.larrycao.com/geoffrey-hinton-family-tree-from-mount-everest-to-ai)
- [Boole family — Wikipedia](https://en.wikipedia.org/wiki/Boole_family)
- [Geoffrey Hinton — Britannica](https://www.britannica.com/biography/Geoffrey-Hinton)
- [AI Godfather Hinton: Born Into a Genius Family but a Habitual Dropout — HyperAI](https://hyper.ai/en/news/36312)
- [Geoffrey E. Hinton — A.M. Turing Award Laureate, ACM](https://amturing.acm.org/award_winners/hinton_4791679.cfm)
- [U of T professor Geoffrey Hinton hailed as guru of new era of computing — The Globe and Mail](https://www.theglobeandmail.com/news/toronto/u-of-t-professor-geoffrey-hinton-hailed-as-guru-of-new-era-of-computing/article34639148/)
- [Long-time CIFAR Fellow Geoffrey Hinton awarded 2024 Nobel Prize — CIFAR](https://cifar.ca/cifarnews/2024/10/08/long-time-cifar-fellow-geoffrey-hinton-awarded-2024-nobel-prize-in-physics/)
- [Two GTX 580s in SLI are responsible for the AI we have today — Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/two-gtx-580s-in-sli-are-responsible-for-the-ai-we-have-today-nvidias-huang-revealed-that-the-invention-of-deep-learning-began-with-two-flagship-fermi-gpus-in-2012)
- [ImageNet Classification with Deep Convolutional Neural Networks (AlexNet paper) — NeurIPS 2012](https://papers.nips.cc/paper_files/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html)
- [AlexNet — Wikipedia](https://en.wikipedia.org/wiki/AlexNet)
- [Hinton says he's proud Ilya Sutskever 'fired Sam Altman' — TechCrunch](https://techcrunch.com/2024/10/09/after-winning-nobel-for-foundational-ai-work-geoffrey-hinton-says-hes-proud-ilya-sutskever-fired-sam-altman/)
- [New Nobel winner Hinton says he's proud his student fired Sam Altman — Fortune](https://fortune.com/2024/10/09/openai-sam-altman-geoffrey-hinton-nobel-prize-physics-ilya-sutskever-toronto/)
- [Elon Musk and Yann LeCun's social media feud — VentureBeat](https://venturebeat.com/ai/elon-musk-and-yann-lecuns-social-media-feud-highlights-key-differences-in-approach-to-ai-research-and-hype)
- [Yann LeCun calls xAI a 'failure,' reignites feud with Elon Musk — Gizmodo](https://gizmodo.com/yann-lecun-calls-xai-a-failure-reignites-feud-with-elon-musk-2000773710)
- [Yann LeCun on X — "I like his cars... but I disagree with him"](https://x.com/ylecun/status/1797270661192155427)
- [Sam Altman and Dario Amodei refused to hold hands at India AI summit — Fortune](https://fortune.com/2026/02/19/openai-anthropic-sam-altman-dario-amodei-refused-to-hold-hands-ai-super-bowl-ad-war-ceos-big-tech-conflict/)
- [Why Anthropic CEO Dario Amodei left OpenAI — StackUmbrella](https://www.stackumbrella.com/technology/why-anthropic-ceo-dario-amodei-left-openai-the-real-story-behind-the-split-from-sam-altman-12005509)
- [Deep learning pioneer Geoffrey Hinton quits Google — MIT Technology Review](https://www.technologyreview.com/2023/05/01/1072478/deep-learning-pioneer-geoffrey-hinton-quits-google/)
- [Geoffrey Hinton Raises Red Flags on AI Industry — Value The Markets](https://www.valuethemarkets.com/cryptocurrency/news/geoffrey-hinton-raises-red-flags-on-ai-industry-and-its-impact-on-society)
- [xAI fired an engineer who raised alarms about Grok safety — TechCrunch](https://techcrunch.com/2026/06/10/xai-fired-an-engineer-who-raised-alarms-about-grok-safety-new-lawsuit-claims/)
- [AI pioneers Hinton, Ng, LeCun, Bengio amp up x-risk debate — VentureBeat](https://venturebeat.com/ai/ai-pioneers-hinton-ng-lecun-bengio-amp-up-x-risk-debate)
- [Yann LeCun and Geoffrey Hinton Clash on AI Safety in 2025 — WebProNews](https://www.webpronews.com/yann-lecun-and-geoffrey-hinton-clash-on-ai-safety-in-2025/)
- [Ilya Sutskever — Wikipedia](https://en.wikipedia.org/wiki/Ilya_Sutskever)
- [Safe Superintelligence reportedly valued at $32B — TechCrunch](https://techcrunch.com/2025/04/12/openai-co-founder-ilya-sutskevers-safe-superintelligence-reportedly-valued-at-32b/)
- [Geoffrey Hinton's former PhD students — cs.toronto.edu](http://www.cs.toronto.edu/~hinton/gradstuphd.html)
- [Radford M. Neal — Wikipedia](https://en.wikipedia.org/wiki/Radford_M._Neal)
- [Peter Dayan — Wikipedia](https://en.wikipedia.org/wiki/Peter_Dayan)
- [Zoubin Ghahramani — Wikipedia](https://en.wikipedia.org/wiki/Zoubin_Ghahramani)
- [Variational autoencoder — Wikipedia](https://en.wikipedia.org/wiki/Variational_autoencoder)
- [Alex Graves (computer scientist) — Wikipedia](https://en.wikipedia.org/wiki/Alex_Graves_(computer_scientist))
