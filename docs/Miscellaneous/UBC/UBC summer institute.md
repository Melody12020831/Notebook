---
statistics: True
comments: true
---

# block chain DAY 1

## **I. 区块链概览**

### **区块链定义**

* 区块链是一种数字账本 (digital ledger)，用于记录有价值的事物。
* 它是分布式 (distributed) 的，并利用网络处理交易 (transactions)。
* 它利用密码学 (cryptography) 使记录安全且不可篡改 (immutable)。
* 一些区块链具备以下特性：代表资产的数字代币 (digital tokens that represent assets)、不同类型的权限 (different types of permissions) 和智能合约 (smart contracts)。

### **区块链的关键组成部分与概念**

1. **Blocks**：区块链的"构建块 (building blocks)"。

* 区块链中的每个区块都像一份详细的发票或费用清单，其中包含交易列表或摘要。
* 区块链交易等同于价值单位的转移，表现为账本条目，用于跟踪"账户 (account)"中价值的累积及其在账户之间的移动。
* 并非所有分布式数字账本 (distributed digital ledgers) 都使用区块数据结构 (block data structures) (例如，IOTA 和 Nano 使用有向无环图数据结构 (Directed Acyclic Graph data structures (DAGs)))。

2. **Chain**：新数据以区块的形式添加，这些区块相互链接形成链。

* 密码学 (Cryptography) 将区块链接在一起，有助于使账本"不可篡改 (immutable)"。
* 链中越靠前的区块越"安全 (more secure)"。

3. **A Distributed Network Structure**：网络中的所有节点 (nodes) 都拥有账本的相同副本，这增强了信任 (trust)。

4. **共识 (Consensus)**：网络就账本状态达成一致的方式。

* 常见的共识机制 (Consensus Mechanisms) 包括工作量证明 (Proof of Work)、权益证明 (Proof of Stake) 和实用拜占庭容错 (Practical Byzantine Fault Tolerance (PBFT))。
* **工作量证明 (Proof of Work) (例如比特币)**：矿工 (miners) "挖掘 (mine)"区块。随着区块链的增长，挖矿难度 (mining difficulty) 会增加，以保持约每 10 分钟创建一个区块的稳定速率，尽管计算能力 (computational power) 不断提高。当更多矿工加入网络且总哈希率 (hash rate) 增加时，协议会每 2,016 个区块（约 2 周）调整难度，以确保区块不会被挖得太快，从而保持系统的安全性 (security) 和可预测性 (predictability)。
* **权益证明 (Proof of Stake)**：验证者 (Validators) "铸造 (mint)"或"锻造 (forge)"区块，而不是"挖掘"区块。

5. **公共与许可区块链 (Public vs. Permissioned Blockchains)**：

* **公共区块链 (Public blockchain)**：所有人都可以加入并参与。
* **许可区块链 (Permissioned blockchain)**：参与者需要获得许可。
* 存在不同类型的权限 (different types of permission)：加入权限 (permission to join)、写入交易权限 (permission to write transactions)、读取所有交易权限 (permission to read all transactions)，或读取特定交易权限 (permission to read certain transactions) (例如，只读取自己参与的交易)。
* **以太坊 (Ethereum)**：公共 (public)、开源 (open-source) 区块链，首先实现了智能合约。它设计用于去中心化应用程序 ("dApps")，有自己的加密货币 (cryptocurrency) (以太币 Ether)。共识机制 (Consensus mechanism) 最初是工作量证明 (Proof of Work (PoW))，计划变更为权益证明 (Proof of Stake (PoS))。
* **超级账本 (Hyperledger)**：一个开源项目 (open source project)，用于构建许可区块链 (permissioned blockchains)。它设计用于工业应用 (industrial applications) (例如供应链解决方案 (supply chain solutions))。由 Linux 基金会开发 (Developed by the Linux Foundation) 并被 IBM 大量使用。它没有自己的加密货币。共识机制可以根据应用而改变，但通常使用实用拜占庭容错 (Practical Byzantine Fault Tolerance (PBFT))。
* **许可区块链网络中的共识 (Consensus in permissioned blockchain networks)**：用户是已知的（例如供应链），共识协议是可定制的 (customizable)，达成共识所需的能源消耗更少。由于节点数量较少，相对更容易被破坏 (corrupt)，因此用户之间需要信任。

6. **智能合约 (Smart contracts) 和数字代币 (digital tokens)**：

* **智能合约 (Smart contracts)**：执行"如果-那么 (if-then)"语句。
* **数字代币 (Digital Tokens)**：基本上可以代表任何可以在区块链账本上记录和交易的资产。包括货币 (Currencies) (例如比特币)、商品 (Commodities)、财产 (Property)、艺术品 (Artwork)、积分 (Loyalty points) 和股票凭证 (Share certificates)。
* **代币化 (Tokenization)**：将现实世界资产的权利转换为区块链上的数字代币的过程。可以是"一对一 (1 to 1)"的 (例如土地登记 (Land registry)) 或"一对多 (1 to Many)"的 (例如零碎的产权所有权 (Fragmented property ownership))。

7. **个人用户使用区块链 (Blockchain for the individual user)**：

* 使用"钱包 (wallet)"来访问、发送和接收价值。
* 钱包有一个"公钥 (public key)"和一个"私钥 (private key)"。

    * 公钥允许人们找到你的钱包并放入价值。
    * 私钥允许你查看钱包内部并取出价值。

* **数字签名 (Digital Signatures)**：举例说明了 Sally 创建比特币钱包、Jim 向 Sally 的公钥发送比特币以及 Sally 钱包中拥有比特币的过程。
* **"非你的密钥，非你的比特币 (Not Your Keys, Not Your Bitcoin)"**：强调拥有私钥的重要性。

### * **区块链的适用场景**

* 当交易各方目标和激励不一致，导致不信任时。
* 当缺乏透明度 (transparency) 时。
* 当参与者不可信，可能作弊时。
* 区块链解决方案在跨组织层面 (interorganizational level) 最有意义。

### **区块链的非适用场景**

* 当单个行为者可以被信任来维护记录和促进交易时 (例如公司内部的 IT 和会计部门)。
* 区块链解决方案在单个组织内部通常是不必要的。

## **II. 区块链应用**

### **区块链用例概览(基于 ISO TR 3242:2022)**

* **数据溯源 (Data Provenance)**：数据问责 (Data Accountability)、产权记录管理 (Property Records Management)、学生记录管理 (Student Records Management)、教育证书溯源 (Education Certificate Provenance)、自证主权身份 (Self-Sovereign Identity (SSID))、内容时间戳验证 (Content Timestamp Verification)。

    * **产权记录管理 (Property Records Management)**：印度于 2017 年启动了 PRMS 计划，旨在简化土地登记流程。

* **金融科技 (Fintech)**：应收账款 (Accounts Receivable)、银行间贷款对账 (Interbank Loan Reconciliation)、有组织合会 (Organised CHIT Funds)、养老金流程优化 (Pension Process Optimisation)、透明证券化 (Transparent Securitisation)、去中心化慈善平台 (Decentralized Charity Platform)。

    * **银行间对账和结算 (Interbank Reconciliation and Settlement)**：区块链技术可以将结算周期从 $T+1$ 或 $T+2$ 天缩短到 $T+0$ 天，解决效率低下和信息不对称问题。这是中国的一个实际应用。
    * **去中心化援助平台 (Decentralized Aid Platform) (WFP Building Blocks)**：通过消除交易成本 (transaction costs)、直接向个人发送援助、整合生物识别扫描 (biometric scanning) 以防止欺诈 (fraud)、提供更大的隐私 (privacy) 以及为每个人创建不可篡改的数字身份 (immutable digital identity) 来解决向叙利亚难民提供粮食援助的挑战。由以太坊提供支持 (powered by Ethereum)。

* **供应链 (Supply Chain)**：国际贸易透明度 (International Trade Transparency)、海运提单 (Maritime Bills of Lading)、特许制药供应链管理 (Franchised Pharma Supply Management)、药品防伪 (Anti-counterfeit Pharma)、IGP 可追溯性 (IGP Traceability)、通用农场合规 (Universal Farm Compliance)、国际废物管理系统 (Intl. Waste Management System)。

    * **农产品可追溯性 (Traceability of Agricultural Food Products)**：ROUGE (Red Orange Upgrading Green Economy) 解决方案为 IGP 红橙提供了经认证且不可更改的产品历史，支持打击欺诈和伪造，并确保供应链中的透明度、安全性 (security) 和弹性 (Resilience)。

* **智能能源 (Smart Energy)**：合作能源交易 (Cooperative Energy Trading)、能源交易 (Energy Trading)、可再生能源产消者微电网 (Renewable Energy Prosumer Microgrids)。

### **变革性应用**

* 实现没有中心权力机构 (no central authority) 的分布式组织 (distributed organizations)。
* 规避中介 (Circumventing intermediaries) (例如公司、银行、政府)。
* 实现新的治理结构 (new governance structures)。
* 实现个人数据所有权 (individual data ownership) 和控制权。

    * 允许个人在不同平台之间携带数据。

* 创建新的资产和市场 (new assets and markets)。

    * 新的数字资产 (New digital assets) (例如效用代币 utility tokens、加密货币 cryptocurrencies)。
    * 现实世界资产的代币化 (Tokenization)、碎片化 (fragmentation) 和重组 (recombination)。

## **III. The Three Layer Model**

### **目的 (Purpose)**：

一个用于设计和分析区块链/DLT 系统 (blockchain/DLT systems) 的框架。

* 其必要性在于该技术仍处于理论不足阶段 (under theorized)，现有模型在全面考虑权衡 (trade-offs) 方面存在不足，这可能导致次优设计 (sub-optimal designs) 和意想不到的负面后果 (negative unintended consequences)。

### **Systems Thinking**：

* 以整体方式 (holistically) 和事物之间相互关系 (inter-relationships) 的角度进行思考的过程，而不是将其视为不相关的实体。

### **Definition of a System**：

* 一个被感知的整体，其元素随着时间不断相互影响，并朝着共同的目标运作。系统由子系统 (subsystems) 或功能 (functions)、过程 (processes)、活动 (activities) 和任务 (tasks) 组成。

* **功能 (Functions) (目的 Purpose)**：系统实现其目的的方式。
* **子系统 (Subsystems)**：系统通常包含子系统。例如，地球是太阳系 (Solar System) 的一个子系统，但也可以被视为一个独立的系统，海洋则是地球的一个子系统。

### **Activities、Transactions、Processes**：

* **活动 (Activities)**：系统通过开展活动来实现其目的。
* **交易 (Transaction)**：涉及多人的行为或相互关联的行为，通过这些行为，这些人的关系发生改变，或是由两人或多个系统之间交换的最小工作过程单元。
* **业务 (或工作) 过程 (Business (or work) process)**：一个或多个交易序列 (sequences of transactions)，需要产生符合管理规则 (governing rules) 的结果 (outcome)。
* **序列 (Sequence)**：一系列交易，其连接要求是，后续交易的进行依赖于先前交易的完成。

### **系统方法设计区块链的优势 (Advantages of a Systems Approach to Blockchain Design)**：

* 使我们能够理解设计组件 ("子系统") 如何与其他组件动态交互。
* 使我们能够整体评估系统，并识别盲点 (blind spots)、隐藏假设 (hidden assumptions) 和意外结果 (unexpected outcomes)。
* 为深入研究不同的子系统提供了基础。

### **The Three Layers**：

每一层都可以被视为不同的抽象层 (abstraction layers)。

* **社会层 (Social Layer)**：涵盖社会参与者 (social actors)，以及这些工具和平台的社会 (social)、政治 (political) 和经济影响 (economic implications)。
* **信息层 (Informational Layer)**：侧重于账本本身作为交易数据 (transactional data) 的"不可篡改 (immutable)"存储库。
* **技术层 (Technical Layer)**：指实施区块链和分布式账本系统的技术组件 (technical components)，即使仍存在需要克服的新技术挑战。

### **区块链的动机**：

* 中本聪 (Satoshi Nakamoto) 创建比特币 (Bitcoin)（以及其底层技术区块链）是为了解决信任问题 (problem of TRUST)，而无需依赖受信任的中介 (trusted intermediary)（通常并不可靠），换句话说，实现"无信任的信任 (TRUSTLESS TRUST)"。

### **深入理解区块链/DLT 的关键方面**：

* **治理 (Governance)**：区块链/DLT 的控制机制 (control mechanism)，可以是内部 (Internal) 或外部 (External) 的。
* **激励 (Incentives)**：一种"执行器 (actuator)"，作用于所有系统组件所拥有的信息处理"逻辑 (logic)"或指令集 (set of instructions)。
* **安全 (Security)**：设计涉及权衡，不仅包括安全性和可扩展性 (scalability) 之间常见的权衡，还包括不同安全属性 (security properties) 之间的权衡，即机密性 (confidentiality) 与透明度 (transparency)，或数据完整性 (data integrity) 与隐私 (privacy)。同样，在不同层或同一层内不同抽象级别 (levels of abstraction) 应用的同一安全属性内部也可能存在权衡。
* **去中心化 (Decentralization)**：DLT 系统每个子系统/层的架构可以集中 (centralized) 或去中心化 (decentralized) 到不同程度，以影响整个系统的运行。
* **溯源追踪 (Provenance tracking)**：一种功能能力 (functional capability)，而非 DLT 系统、其子系统或组件的固有属性 (inherent property)。
* **时间性 (Temporality)**：区块链/DLT 系统并非静态的 (static)，其属性 (properties) 和能力 (capabilities) 可能并非完全可预测。

### **基于三层概念模型的问题导向设计框架**：

* **系统层面 (System Level)**：

    * **系统目标 (System Goal)**：DLT 系统的既定目的是什么？既定目的如何支持社会信任？该系统应解决哪些问题？系统旨在支持哪些用例？。
    * **系统约束 (System Constraints)**：系统必须被设计成不容忍哪些行为？系统的允许行为空间是什么？。
    * **系统能力 (System Capabilities)**：系统需要具备哪些能力才能在其规定约束 (prescribed constraints) 内实现其目标？。
    * **环境 (Environment)**：DLT 系统运行的环境是相对同质的 (homogeneous) 还是更异质的 (heterogenous)？DLT 系统在其设计/运行中对环境做出了哪些假设？系统依赖于环境的哪些方面？在哪些点和为了什么目的依赖这些方面？DLT 系统与环境的所有方面匹配程度如何？环境中的哪些元素影响或约束 DLT 系统的设计者？环境中的哪些元素影响或约束系统参与者 (system actors) 或行动者 (actants)？。
    * **时间性 (Temporality)**：系统未来必须能够应对哪些已知变化？需要建立哪些机制来确保系统的寿命 (longevity)？未来的事件是否可能导致平台完全被替换或停止运行？治理子系统 (governance sub-system) 将如何随着时间推移处理参与者/行动者与系统之间不断变化的关系？如何解决风险因素 (risk factors)，包括那些未来未知且可能带来生存或系统性风险的因素？权力如何在社会参与者之间随时间推移而转移？。

* **子系统层面 (Sub-System Level)**：

    * **社会子系统 (Social Sub-System)**：DLT 中的社会参与者是谁？他们如何被识别/代表？他们的身份如何被规范？DLT 系统如何赋予或限制他们的代理权 (agency)？哪些类型的社会参与者行为是被禁止、鼓励或容忍的？权力在社会参与者中位于何处？哪些价值观对该系统中的社会参与者很重要？我们对社会参与者的行为有什么期望？他们将或可能采取哪些行动？这些行动预计会如何影响其他人？何时需要、授予或假定社会参与者的同意 (consent)、许可 (permission) 和授权 (authority)？一些社会参与者是否会代表他人行事？他们基于什么（道德、法律？）基础执行他人的意愿？在出现冲突时，社会参与者如何需要行使（或者他们是否行使）酌情权 (discretion)？。
    * **信息子系统 (Informational Sub-System)**：账本如何在 DLT 系统中支持社会信任？哪些数据被捕获/流经系统以支持系统目标？生成哪些记录以支持系统目标，无论是在账本上还是链下？系统中数据/记录行动者如何被识别以及他们的身份如何被规范？系统必须存储哪些数据和/或记录？（法律或监管义务是什么？）系统中不得存储哪些数据和/或记录？（为了隐私、财务风险管理或公司政策。）是否存在需要特殊考虑的数据和/或记录？例如，是否存在包含个人可识别信息 (personally identifiable information) 且法律要求特殊处理的数据和/或记录？是否存在不得无限期保存的数据和/或记录？记录存储在哪里？它们如何在网络中传播？记录的知识组件如何被组装？。
    * **技术子系统 (Technical Sub-System)**：DLT 系统中的物理行动者 (physical actants) 是什么（例如传感器 (sensors)、车辆 (vehicles)）？系统中的技术行动者如何被识别以及他们的身份如何被规范？物理行动者如何在 DLT 系统中支持社会信任？他们需要哪些能力和属性来支持系统目标？系统架构 (system architecture) 是什么？网络架构/拓扑 (network architecture/topography) 是什么？哪些社会参与者控制 DLT 系统中的物理行动者？这些社会参与者如何赋予或限制物理行动者的活动？物理行动者拥有什么级别的权限/授权 (authority/authorization)？。
    * **治理子系统 (Governance Sub-System)**：在正常运行条件下，对内部或自律治理 (internal or self-regulating governance) 与外部治理 (external governance) 的依赖程度如何？在异常运行条件下呢？在技术、信息和社会行动者/参与者之间如何做出共识决策 (consensus decisions)？需要建立哪些激励措施，以使共识机制 (consensus mechanism) 按照支持系统目标的方式运行？决策管理权 (decision management rights) 和决策控制权 (decision control rights) 应如何在各种相互作用的组件（社会、信息或技术）之间分配？如何解决有关这些决策的分歧？。

### **三层模型的优势**：

* 创建了一个用于多学科、问题导向的设计空间的通用概念框架 (common conceptual framework) 和语言。
* 能够"看到"设计选择可能产生的交叉影响和连锁效应（即在设计背景下调动"系统思维" (systems thinking)）。
* 通过利用问题导向框架 (Question-led Framework) 来锚定范围讨论，设计团队可以更清晰地界定即时原型 (immediate prototype) 的必要需求与完整系统的长期设计目标之间的区别。
* 有助于识别以前的"未知未知 (unknown unknowns)"。
* 技术问题的框架引导了对新颖技术能力 (novel technical capabilities) 的探索，例如与物联网 (IoT) 的集成。

### **三层模型的局限性**：

* 问题高层次且复杂，需要时间学习和理解。
* 仍需要更广泛的实证验证 (empirical validation) 和可复现性 (reproducibility)。
* 对其他技术（例如人工智能 (AI)）的适用性 (applicability) 仍有待观察。

## **IV. 案例研究：Swear (区块链 + 人工智能)**

### **背景**：

* 聚焦于深度伪造 (deepfakes)，其中伪造图像和视频正在侵蚀建立对真相主张 (truth claims) 信任的视觉基础。区块链被认为具有防御深度伪造的能力。

### **Swear 解决方案**：

* 用于视频捕获的移动应用程序 (Mobile App for video capture)。
* 支持的格式 (Supported formats)：D1, 960H, HD SDI, AHD, HD-TVI, HD-CVI, IP, 4k。
* 编解码器 (Codecs)：H.264, AVI, AVCHD H.265 (HVEC)。
* 兼容 DVR 和 NVR。
* Web3.0 区块链 (Web3.0 Blockchain) 保护指纹 (fingerprints)，建立不可篡改的保管链 (immutable chain-of-custody)。
* 数字媒体真实性 (Digital media authenticity) 持续实时验证 (verified continuously and in real time)。
* 在像素级别识别媒体篡改 (identification of media manipulation at the pixel level)。
* 集成到现有监控系统 (Integrates into existing surveillance systems)。

### **案例研究分析下一步**：

* 使用三层模型审查和讨论 Swear 解决方案，根据三层模型对解决方案的特性 (features) 和能力 (capabilities) 进行分类；寻找模型各"层 (layer)"之间的相互联系和互动（例如，账本如何增强信任？社会参与者和机构 (social actors and institutions) 是谁？使用了哪种类型的区块链 (type of blockchain)？如何形成共识 (consensus is formed)？）。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Day 1 Introduction </div>
<div class="file-meta"> 6,172 KB / 2025-07-08</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Day 1 Introduction.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Blockchain_DLT System Design and Analysis Framework </div>
<div class="file-meta"> 51 KB / 2025-07-08</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Blockchain_DLT System Design and Analysis Framework.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> 20241127-WIFS 2024-Smart Contract Kill Switch for Security in a Private Blockchain-based Software Transaction System-v1.0 </div>
<div class="file-meta"> 1,397 KB / 2025-07-08</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/20241127-WIFS 2024-Smart Contract Kill Switch for Security in a Private Blockchain-based Software Transaction System-v1.0.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 2

## 经济系统的问题分析

### **干预无效论**：

- H.L. Mencken :"对于每一个复杂的问题，都有一个清晰、简单且错误的答案"
- Saint Bernard of Clairvaux :"通往地狱的道路是用良好意图铺成的"
- Hippocrates :"无为有时是良药"

指出干预往往因为未能考虑系统的复杂性而失败。

### **经济衰败的四个阶段**：

1. **现实脱节**（Reality Disconnection）：干预使我们脱离真实情况，导致意想不到的后果，反而使问题持续存在。
2. **扼杀竞争**（Stifled Competition）：干预扼杀了创新和创造性破坏的自然过程，阻碍了新思想和产业的增长。
3. **资本流向扭曲**（Distorted Capital Flows）：干预扭曲了资本分配，将资源从蓬勃发展的行业重定向到衰退的行业，削弱了整体经济。
4. **决策受损**（Impaired Decision-Making）：创新受到抑制、资本和资源错配导致信息错误，从而损害决策，加剧经济脆弱性。

### **货币对行为的影响**：

- **时间偏好**（Time Preference）：如果钱在贬值，我们是否有动力为未来储蓄？
- **无意义感与冷漠**（Meaninglessness & Apathy）：购买力下降是否真的能培养我们的掌控感？
- **利他主义努力**（Altruistic Endeavours）：当我们为了满足最基本需求而奋斗时，我们真的能成为最好的自己吗？
- 金钱始终是生活中排名第一的压力源。

## **比特币的解决方案**

**比特币的特性**：稀缺、无许可、去信任、去中心化。它是一种有利于所有者的更好的货币。

**经济繁荣的四个阶段**（比特币模型）：

1. **现实重新校准**（Reality Re-Alignment）：比特币反映现实，将价格与真实市场状况对齐，随着创新推进导致成本下降。
2. **促进竞争**（Fostering Competition）：干预有限，比特币促进竞争，从而推动创新和创造性破坏——价值浮现。
3. **资本流向同步**（Capital Flow Synchronization）：比特币支持价值驱动的资本流动，奖励成功的行业而非失败的行业，反映了社会所重视的。
4. **知情决策**（Informed Decision-Making）：比特币通过提供对资本流动和社会价值观的清晰洞察，支持知情决策，促进进步和繁荣。

**衡量"好货币"的标准**：稀缺性、可携带性、耐用性、可分割性、可识别性、抗审查性。

**比特币的工作原理**：

- **挖矿**：验证交易并保护网络的过程。
- **区块链技术**：记录交易的分布式账本，确保安全。
- **私钥和公钥**：用户发送和接收比特币的方式。

## **容错机制**

### **良性故障 (Benign failures) 与 CFT 共识 (Crash Fault Tolerance)**：

* **故障类型**：服务器崩溃、消息丢失、消息乱序、消息重复。
* **特点**：节点要么正常，要么停止工作，不会恶意发送错误信息。
* **应用**：文件系统（HDFS, GFS）、数据库（Spanner, etcd）、领导者选举/协调（Chubby, Zookeeper）等所有分布式系统。

### **任意故障 (Arbitrary failures) / 拜占庭故障 (Byzantine failures) 与 BFT 共识 (Byzantine Fault Tolerance)**：

* **故障类型**：任意行为；故障节点（有意或无意），节点可能撒谎、发送错误消息（不遵循协议、存在 Bug）。
* **特点**：节点行为不可预测，可能恶意欺骗或因错误发送错误信息。
* **应用**：安全关键系统（如指挥控制系统、飞机等）、分布式账本（DLs，如 Diem, CCF）。

### **PrestigeBFT 总结**：

* **首个主动视图变更协议**：服务器可以主动争取领导权，防止不可用或缓慢的领导者出现。
* **声誉系统**：将节点的行为历史转化为声誉分数，代表节点行为正确的可能性。
* **鲁棒性与效率的独特结合**：有故障的服务器在执行损害其声誉的攻击后，会被压制，无法窃取领导权。

不同 **failure types** :

1.  **崩溃失效 (Crash Failure)**

* **定义内容**：指系统或其组件突然停止响应或完全停止工作，无法继续提供其预期的服务。这种失效通常是由于内部错误、硬件故障或外部不可预测的事件（如蓝屏死机）导致系统终止。在检测到崩溃时，系统通常会停止所有操作。
* **在问题中的应用**：在"蓝屏死机"的例子中，系统停止运行并显示错误，这就是典型的崩溃失效。在高尔夫球杆击穿物体的"hunting"事故中，物体（如自行车架）因物理冲击而损坏并失去功能，也可视为一种崩溃失效。

2.  **遗漏失效 (Omission Failure)**

* **定义内容**：指系统未能产生预期的输出或未能按时发送信息。它表示系统应该执行某个动作但未执行，导致信息丢失或服务未被提供。
* **在问题中的应用**：在"信号衰减"的例子中，信号强度减弱可能导致数据包丢失或信息未被完整接收，这属于系统未能生成（接收）预期输出，因此是遗漏失效。

3.  **时序失效 (Timing Failure)**

* **定义内容**：指系统在错误的时间（过早或过晚）产生输出或执行操作。系统可能正确地生成了结果，但其交付或执行的时间点不符合规范或预期，导致功能异常。
* **在问题中的应用**：在前面的例子中，没有直接的时序失效案例被明确提及作为主要原因。在"信号衰减"的背景下，严重的衰减可能导致传输延迟，间接影响时序，但它并非时序失效的核心定义。

4.  **故障停止失效 (Fail-Stop Failure)**

* **定义内容**：一种特殊的失效模式，指系统在发生故障时能够立即停止运行并明确地发出故障信号，而不会产生任何错误或误导性的输出。这种失效模式在设计容错系统时很受欢迎，因为它简化了错误检测和恢复。
* **在问题中的应用**：在"切断通讯线路"的例子中，通讯线路被切断后，数据传输立即停止，系统无法再提供通讯服务，并且这种停止是显而易见的，符合故障停止失效的特点。

5.  **良性失效 (Benign Failure)**

* **定义内容**：指那些对系统功能影响较小，或者系统能够优雅地从其中恢复的失效。这类失效通常不会导致灾难性的后果或服务完全中断，系统可能能够容忍它们，或者通过简单的机制进行补偿和恢复。
* **在问题中的应用**：在"信号衰减"的例子中，如果信号衰减不导致完全的服务中断，并且系统能够通过重传或纠错机制进行补偿，那么这种情况下可以被视为良性失效。

6.  **任意失效 (Arbitrary Failure)**

* **定义内容**：也称为"任意错误"（arbitrary error），指系统行为以不可预测且可能具有恶意的方式偏离其规范。在这种失效模式下，系统可能会产生任何输出，包括完全错误的、不一致的或恶意的数据，并且行为模式难以预测。
* **在问题中的应用**：在"加密货币黑客攻击"的例子中，黑客利用系统漏洞，导致系统执行攻击者意图的恶意操作，这些操作对于系统的正常功能而言是"任意"和不可预测的，完全偏离了预期的规范。

7.  **拜占庭失效 (Byzantine Failure)**

* **定义内容**：是分布式系统中最为复杂和严重的失效模型。它描述的是系统中的一个或多个组件（或"节点"）可能以任何方式行为失常，包括发送错误、矛盾或恶意的消息，并且不遵守协议，甚至主动进行欺骗。在拜占庭失效下，无法区分是节点停止工作还是在发送错误信息。
* **在问题中的应用**：在"加密货币黑客攻击"的例子中，尤其是在区块链这类分布式系统中，如果攻击者控制部分节点并以恶意方式行动（如双重支付，即一个币被消费了两次，或者向不同节点发送矛盾的交易信息），这种行为正是拜占庭失效的典型特征，因为它涉及恶意行为、信息不一致性以及对共识机制的破坏。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Breaking the Cycle Blockchain UBC </div>
<div class="file-meta"> 5,263 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Breaking the Cycle Blockchain UBC.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 3

## **Consensus 基础**

### **共识的定义**：

* 普遍同意，达到一致。
* 由大多数相关方做出的判断。
* 共识算法协调系统节点，就应用程序输入（如日志、账本、值、命令、交易、区块）达成一致。
* 共识需要维护事件的全局顺序。

### **何时需要共识**：

* 操作、事件的顺序。
* 复制日志的内容。
* 决定领导者。
* 写入分布式账本（DL）的区块和交易。

### **容错（Fault Tolerance）**：

* 系统（节点）需要容忍故障，即在发生（部分）故障时仍能正常运行。
* **故障类型**：
    * **良性故障（Benign Failures）/CFT共识**：服务器崩溃、消息丢失、重排序、重复。
        * 应用：文件系统（HDFS、GFS）、数据库（Spanner、etcd）、领导者选举/协调（Chubby、Zookeeper）。
    * **拜占庭故障（Byzantine Failures）/BFT共识**：任意行为；故障节点（故意或无意）、节点可能撒谎、发送错误消息（不遵循协议、存在bug）。
        * 应用：安全关键系统（指挥控制系统、飞机等）、分布式账本（Diem、CCF等）。

### **系统故障示例**：
    * “蓝屏死机”：是一种崩溃故障。
    * 通信线路中断、信号衰减、打猎“事故”（指物理线路被切断）：属于通信中断。
    * 加密货币黑客攻击：
        * Ronin Bridge攻击：损失6.24亿美元，原因是验证者节点被攻陷，攻击者控制了多数（5/9）验证者。
        * Poly Network攻击：损失6.11亿美元，原因是智能合约漏洞导致访问控制不足，跨链消息存在关键错误。攻击者后来返还了资金。
        * Wormhole攻击：损失3.2亿美元，原因是Solana VAA验证失败，未验证“守护者”账户，未打补丁的Rust智能合约被利用。
        * 这些加密黑客攻击通常是由于协议设计问题、验证者被排除在验证集之外（协议缺陷）等引起。

## **PrestigeBFT：基于声誉的主动视图变更**

### **问题**：

传统基于领导者的BFT共识存在被动视图变更的问题。

* 当领导者节点崩溃时，需要等待超时才能发现，导致延迟。
* 如果新选的领导者日志落后于其他节点，需要先同步日志，进一步增加延迟。
* 拜占庭服务器可能会撒谎并启动选举活动。

### **目标**：

在BFT中实现主动视图变更，节点可以主动竞选领导者，从而避免不可用或缓慢的领导者。

* 没有固定的领导者调度。
* 检测到领导者故障的节点可以启动选举。
* 只选举最新（up-to-date）的节点。

### **PrestigeBFT方案**：

* **声誉机制**：将节点行为转换为声誉分数，反映节点行为正确的可能性。
* **奖惩制度**（受美国侵权法中的“威慑和赔偿”理论启发）：
    * **惩罚（Penalization）**：对每个竞选者施加惩罚。
    * **补偿（Compensation）**：奖励最新日志复制（计算增量日志响应度 `δtx`），奖励过去惩罚没有或仅逐渐增加的节点（计算过去视图变更中所有惩罚的Z分数 `δvc`），并扣除惩罚。
* **效果**：
    * 行为良好（遵守协议）的节点获得高声誉，更有可能成为新领导者。
    * 行为不端（可疑故障）的节点获得低声誉，更不可能成为新领导者。
    * 逐步区分拜占庭服务器和正确服务器。
    * 通过施加计算工作，随着时间推移抑制故障服务器。

### **主动视图变更协议的状态和转换**：

* Follower（跟随者）可以触发视图变更（VC）。
* Redeemer（赎回者）计算声誉惩罚，可能超时并重复VC。
* Candidate（候选者）接收来自 $2f+1$ 个服务器的投票，如果发现更高视图，则转换。
* Leader（领导者）接收投票，生成vcBlock，并将信息提供给Prestige BFT Reputation Engine。

### **性能**：

* **正常运行下**：PrestigeBFT在吞吐量方面优于SBFT、HotStuff和Prosecutor，性能提高约5.4倍。
* **节点数量影响**：随着节点数量增加，PrestigeBFT的吞吐量和延迟变化与HotStuff类似，但总体性能更好。
* **故障下（攻击场景）**：
    * **静默参与者（Quiet participants）**：不响应任何请求（类似崩溃故障）。
    * **含糊其辞（Equivocation）**：通过发送错误消息响应查询。
    * **重复视图变更攻击（Repeated view-change attacks）**：在非领导者时竞选领导者。
* **总结**：PrestigeBFT是第一个用于BFT共识的主动视图变更协议，实现了鲁棒性和效率的独特结合。故障服务器在攻击后声誉下降，无法篡夺领导权。

## **V-Guard：动态成员变化的分布式账本设计**

### **动机**：

* 当前的BFT共识算法假设一个稳定的环境，即预先固定、静态的节点集合。
* 车联网（V2X）无法保证稳定环境，车辆会频繁加入/离开，在线/离线。
* V2X分布式账本必须能够在动态环境中运行，成员资格频繁变化。

### **车辆自动化的问题**：

* 制造商的自动驾驶（Autopilot、SuperCruise）等数据仅由制造商收集，是中心化模式。
* 消费者对自己的数据访问受限。
* 中心化的数据处理造成数据垄断，损害数据完整性。
* V2X需求推动了以DL为中心的设计，通过共识保证数据完整性。
* 车辆固有可识别，因此适用于许可型DL。许多汽车制造商都在进行DL计划。

### **V-Guard设计理念**：

* 将成员资格配置绑定到交易中。
* “展台（booth）”是描述符，指定一组参与车辆的成员配置。
* 展台组合器（Booth composer）准备一个有效展台队列，作为共识的目标（`<t1, B1, O1, Q1>`：交易、展台、排序、法定人数）。

### **V-Guard架构**：

* **基础设施层（Infrastructure Layer）**：数据收集、网络。
* **V-Guard框架（V-Guard Framework）**：
    * **共识模块（Consensus Module）**：包含Ordering（排序）和Consensus（共识）子模块，并通过Booth Composer连接。排序与共识分离，可以在不同的展台中进行。
    * **存储模块（Storage Module）**：包含Temporary（临时）和Permanent（永久）存储。
    * **Gossip模块（Gossip Module）**：包含Sender（发送者）和Receiver（接收者），用于进一步传播已提交的交易。
* **应用层（Application Layer）**：分布式账本、证据链等。

### **性能**：

* **峰值性能（静态排序、共识）**：
    * V-Guard的峰值吞吐量比HotStuff高22倍，比ResilientDB高9.5倍，比Narwhal高1.8倍。
    * V-Guard的延迟显著低于HotStuff和ResilientDB。
* **动态性下的吞吐量/延迟**：V-Guard在成员变化数量增加时，吞吐量下降幅度较小，延迟增加幅度也相对可控。

### **总结**：

* V-Guard快速：将排序与共识分离。
* V-Guard动态：在动态变化的成员资格下运行。
* V-Guard多功能：适用于在不稳定网络（如间歇性连接）下运行的应用。

## **Prism协议：去中心化智能合约平台共识瓶颈的移除**

### **背景**：

* 现有许可链智能合约平台（如以太坊）的性能受限于共识层。
* 最长链协议（如比特币、以太坊所用）在保持高安全性的同时，存在吞吐量和延迟差的缺点，导致网络拥堵（例如CryptoKitties事件）。
* 去中心化金融（DeFi）应用的快速增长使得智能合约平台的性能扩展变得紧迫。

### **现有扩展方案**：

* **改进虚拟机执行速度**：优化操作码或设计新操作码（如Libra的MoveVM），或并行执行智能合约（通过锁或乐观并发+回滚）。这些方法有性能提升，但可能引入新的攻击，且未解决计量问题。
* **设计高吞吐量共识协议**：
    * 从无许可转向许可型共识（如Facebook的Libra/HotStuff、IBM的Hyperledger Fabric）。这些牺牲了无许可特性。
    * Prism、OHIE、Algorand、Bitcoin-ng等协议也走这条路，但通常没有在这些协议上运行智能合约的实现。
* **Plasma和分片（Sharding）**：
    * Plasma：链下扩容方案，是二级链网络，通过欺诈证明解决冲突。安全性较弱，易受“大逃亡”攻击。
    * 分片：以太坊2.0、NEAR、Polkadot等采用，通过运行多个区块链实例并汇集它们来水平扩展吞吐量。安全性优于Plasma，但仍低于纯共识协议。

### **Prism的核心贡献**：

* 一种新的工作量证明（PoW）区块链协议。
* **同时实现**：
    1.  **安全性**：可抵御高达50%的恶意哈希算力攻击。
    2.  **吞吐量**：达到网络容量C的 $(1-\beta)C$ 吞吐量（接近最优）。
    3.  **确认延迟**：诚实交易的确认延迟与传播延迟D成比例，确认错误概率随带宽-延迟积指数级减小。
    4.  **最终总排序**：所有交易的最终总排序。
* **核心思想**：通过将中本聪区块链分解为基本功能（交易提案、验证、确认），并系统地扩展这些功能以接近物理限制。
    * 将区块分解为三种类型：**提案者区块（proposer blocks）**、**交易区块（transaction blocks）** 和 **投票者区块（voter blocks）**。
    * **提案者区块树**：锚定Prism区块链骨架，包含对交易区块和父提案者区块的引用链接。诚实节点在最长链上挖矿，但最长链不决定最终确认的提案者区块序列（领导者序列）。
    * **投票者区块**：在m个独立投票者链上挖矿，每个投票者区块通过引用链接投票给一个提案者区块。领导者区块是获得最多票数的提案者区块。
    * **交易区块**：包含交易，并由提案者区块引用。
    * **解耦**：通过解耦这些区块类型，Prism可以实现低延迟和高吞吐量，同时保持高安全性。
        * 增加交易吞吐量：通过增加提案者区块指向的交易区块数量，而不影响安全性。
        * 提供快速确认：通过增加并行投票树的数量，并行投票提案区块，从而提高投票率，直至达到光速延迟和极高可靠性的物理极限。

### **Prism的设计与实现**：

* 用Rust语言实现了Prism全节点客户端，集成了EVM和MoveVM虚拟机。
* **架构**：
    * **Prism共识模块**：负责与对等节点交换区块，遵循Prism共识确认区块，并将确认的区块推送到VM执行器。
        * **Blocktree Manager（区块树管理器）**：维护客户端的区块链视图，与对等节点交换区块，验证PoW，检查数据可用性，处理排序和交易签名，并将区块插入Prism区块树。
        * **Ledger Manager（账本管理器）**：定期查询Blocktree Manager以获取新的确认区块，遵循Prism的确认规则，并将区块推送到VM执行器。
        * **Miner（矿工）**：维护一个内存池，收集待处理交易并组装成新区块。通过泊松过程模拟挖矿，并将新区块广播给对等节点。
    * **VM Executor（虚拟机执行器）模块**：维护已确认账本的状态数据库。接收来自Ledger Manager的确认区块，从区块中检索交易并顺序执行，更新状态。无效交易会被清理出账本。
* **设计亮点**：
    * **确认机制**：仅维护最后确认区块的状态，因为Prism以极高概率保证确认，且确认区块不太可能被取消。在收到新区块时，仅当区块被确认时才更新状态，并定期进行确认程序。
    * **交易验证与状态更新解耦**：Prism矿工不进行交易验证或状态更新。只有在区块被确认后，其中的交易才被验证，状态才相应更新。这与Hyperledger Fabric类似，但Prism是“order-execute-validate”范式，而Hyperledger Fabric是“execute-order-validate”范式。Prism的验证不需要背书，而是每个节点复制执行和验证。
    * **无待处理交易交换**：由于Prism的挖矿速率很高，矿工无需在对等节点之间交换待处理交易。交易区块直接广播，这减少了网络带宽的浪费，并有助于高吞吐量。
    * **共识中的签名验证**：将交易签名验证移至Prism共识模块中并行执行，减轻了VM执行器的负担，有助于提高吞吐量。

### **评估**：

* **实验设置**：在Amazon EC2上使用100个c5d.4xlarge实例，形成4-regular拓扑，引入120ms的传播延迟和300Mbps的速率限制。
* **应用程序**：
    * **基本应用**：Native Payment（原生代币支付）、Do Nothing（空函数合约）。
    * **基准应用**：CPU Heavy（CPU密集型）、IO Heavy（IO密集型）。
    * **实际应用**：ERC20（以太坊代币标准）、CryptoKitties（计算密集型游戏）。
* **吞吐量和延迟（EVM Prism）**：
    * EVM Prism的吞吐量接近EVM Executor Only（单节点无共识）的85%，表明Prism移除了共识瓶颈，虚拟机本身成为瓶颈。
    * Prism Consensus Only（无智能合约平台，原始交易吞吐量）的吞吐量很高（超过80K tx/s），说明如果虚拟机未来更快，Prism也能支持。
    * 与以太坊的21 tx/s相比，Prism的吞吐量显著更高。
    * 确认延迟：所有Prism实验（包括EVM Prism）的确认延迟不超过130秒，远低于以太坊（需要2670秒才能达到相似安全性）。
    * 资源利用率：Prism共识模块使用多线程，VM执行器单线程。CPU平均使用率不超过50%。签名验证占用CPU时间高达39.2%。
    * 区块数据：交易区块占总生成区块数据的71.2%，表明大部分带宽用于高吞吐量交易，Prism开销（提案者和投票者区块）很小。
* **吞吐量和延迟（MoveVM Prism）**：
    * MoveVM Prism的基本应用吞吐量（1.1K-2.2K tx/s）比EVM低一个数量级，但基准应用（CPU Heavy、IO Heavy）吞吐量高于EVM，表明MoveVM在执行指令方面更高效。
    * MoveVM Prism的吞吐量接近MoveVM Executor Only的81%，再次确认Prism移除了共识瓶颈，虚拟机是瓶颈。
    * 确认延迟与EVM Prism类似，不超过130秒。
    * 资源利用率：内存使用低于3.2GB，CPU平均使用不超过32%，因吞吐量较小且签名验证更高效（MoveVM采用Ed25519签名，比EVM的ECDSA更快）。
* **可扩展性**：
    * Prism能够扩展到大量网络参与者（例如300个节点），只要底层点对点网络提供合理的区块传播延迟。
    * 在100和300节点情况下，吞吐量和延迟非常相似，分叉率略有增加但仍可接受。
    * 每个节点的资源利用率也相似。

### **总结**：

* 区块链研究之前是模块化的，协议（尤其是共识）与上层应用（虚拟机、应用编程）分离。Prism协议受到中本聪比特币设计的启发，是一个完整的系统。
* Prism无缝集成了EVM和MoveVM，在多种应用中实现了接近最佳的虚拟机吞吐量。
* Prism不仅消除了裸金属吞吐量和延迟的共识瓶颈，而且在与两个流行智能合约平台交互时也做到了这一点。
* 未来智能合约性能的进一步提升需要虚拟机和编译器的新设计以及支持并行执行智能合约的架构。

## **Smart Contract Kill Switch**

简单来说，**智能合约的"自毁开关"是一个预先设定好的功能，允许合约的创建者或特定授权方在紧急情况下禁用或销毁合约。** 想象一下，你开发了一个非常重要的软件，但万一软件出现严重漏洞或被恶意攻击，你需要一个紧急停止的按钮，对吧？"自毁开关"在智能合约中就扮演了类似的角色。

### 为什么需要"自毁开关"？

智能合约一旦部署到区块链上，通常是不可更改的。这意味着，如果合约代码中存在错误（bug）、安全漏洞，或者出现不可预见的紧急情况（比如，市场剧烈波动导致合约行为异常，或者被黑客攻击），传统的做法很难及时止损。

有了"自毁开关"，合约的管理者可以在以下情况下采取行动：

* **修复漏洞：** 如果发现合约有重大安全漏洞，可以通过触发"自毁开关"停止合约运行，防止更多损失，然后部署一个修复后的新合约。
* **应对攻击：** 在遭受恶意攻击时，可以迅速禁用合约，阻止攻击者进一步窃取资产或破坏系统。
* **紧急情况处理：** 应对一些极端但未预料到的市场或外部事件，避免合约按照原定逻辑造成不可挽回的损失。
* **升级合约：** 在某些设计中，它也可以作为一种升级机制的一部分，旧合约被禁用后，用户可以迁移到新合约。

### "自毁开关"如何工作？

通常，"自毁开关"会作为智能合约代码的一部分进行编写。它会包含以下几个关键点：

1.  **触发条件：** 只有满足特定条件才能触发。例如，只有合约的**所有者**（创建者）才能调用这个功能，或者需要**多方签名**才能激活（比如，需要3个密钥中的2个才能触发）。
2.  **执行动作：** 一旦触发，合约会执行预设的动作。这可能包括：

    * **阻止新的交易：** 合约不再接受新的资金或操作。
    * **将合约中的资产转移到安全地址：** 将所有剩余的加密货币转移到一个安全的地址，防止被盗。
    * **让合约无法执行：** 使合约进入一个"锁定"状态，所有功能都无法使用。
    * **销毁合约本身：** 从区块链上移除合约代码，释放存储空间（这个操作在以太坊等区块链上被称为 `selfdestruct`）。

### "自毁开关"的优缺点

**优点：**

* **增强安全性：** 提供应对紧急情况的"安全网"，降低风险。
* **提高灵活性：** 在一定程度上为不可更改的智能合约增加了可控性。
* **保护用户资产：** 在遭受攻击时，可以及时止损，避免用户资产损失。

**缺点：**

* **中心化风险：** 如果"自毁开关"的权限过于集中在一个人或少数几个人手中，可能会带来中心化风险。这些拥有权限的人可能会滥用权力，随意禁用合约，损害用户利益。
* **信任问题：** 用户需要信任合约的创建者不会滥用这个功能。
* **复杂性增加：** 设计一个安全且有效的"自毁开关"需要额外的代码和考虑，增加了合约的复杂性。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> BFT-Consensus-HAJ </div>
<div class="file-meta"> 2,970 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/BFT-Consensus-HAJ.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Prism_Blockchain_Trilemma </div>
<div class="file-meta"> 2,064 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Prism_Blockchain_Trilemma.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Prism_Plus </div>
<div class="file-meta"> 901 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Prism_Plus.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 4

## **拜占庭容错（BFT）共识算法概述**

### **定义**：

BFT共识算法是分布式系统的核心，即使在出现任意故障（拜占庭故障，即故障服务器行为不受限制，可能撒谎、发送错误消息、串通等）的情况下，也能提供安全性和活性保证。

### **应用**：

* 长期用于安全关键系统，如飞机、潜艇等，在恶劣环境下（极端天气、辐射）硬件可能变得不可靠。
* 近年来，随着区块链技术的发展，BFT算法被广泛部署于众多区块链平台，提供无需第三方信任的去中心化解决方案，支持加密货币、供应链、国际贸易平台和物联网（IoT）等应用。
* 在这些应用中，由于恶意行为日益普遍，BFT算法对于共识的正确性保证至关重要。

### **挑战**：

* 不同算法使用的假设（如故障模型、网络模型）差异大。
* 复杂性指标（如消息复杂性、时间复杂性）标准不一致。
* 缺乏全面、标准和直观的协议描述（如消息传递模式和工作流程）。

## **BFT共识算法分类（分类法）**

文章提出了BFT共识算法的三大类分类法：

1.  **更高效的BFT (More Efficient BFT)**：

* **目标**：专注于提高复制效率，如减少消息复杂性和共识前的流水线机制。
* **子类别**：
    * **减少消息复杂性**：如Zyzzyva、SBFT、HotStuff。
    * **多领导者共识**：如MirBFT、ISS。
    * **基于DAG的协议**：如DAG-Rider、Narwhal、Bullshark、Shoal。

2.  **更鲁棒的BFT (More Robust BFT)**：

* **目标**：优先考虑针对各种攻击和恶意行为的鲁棒性和安全性。
* **子类别**：
    * **防御各种攻击**：如Prime（时间攻击）、Spin（垄断攻击）、Aardvark（性能攻击）。
    * **声誉共识**：如Prosecutor、PrestigeBFT。
    * **排序公平性**：如Pompe、Fairy。

3.  **更可用（高可用）的BFT (More Available BFT)**：

* **目标**：优先考虑在不同网络条件下（包括异步协议和无领导者协议）的可用性和系统响应性。
* **子类别**：
    * **异步和无领导者协议**：如DBFT、BEATS、Honeybadger。

## **BFT共识的背景概念**

### **共识问题和状态机复制（SMR）**：

* SMR是分布式系统中通过一组服务器副本协调工作，为客户端提供一个或多个服务的模型。
* 状态机包括状态变量（系统当前状态）和命令（不同状态间的转换）。
* 共识算法同步和协调多个状态机，确保每个机器计算相同结果，即使部分机器出现故障也能保持统一和一致的系统状态视图。

### **拜占庭故障**：

SMR中最强的故障形式。故障服务器可以表现出任意行为，包括改变消息内容和变异自身状态，并可能与其他故障服务器串通，共同表现恶意行为。与良性故障（消息内容不变，状态变化可检测）不同。

### **拜占庭法定人数（Byzantine Quorums）**：

* BFT算法的决策通常依赖于法定人数证书（Quorum Certificates），即从不同参与者收集的一组相同消息。
* 容忍良性故障的最小法定人数大小是 $f+1$。
* 容忍拜占庭故障的最小法定人数大小是 $2f+1$。在总共 $n=3f+1$ 个节点中，由于假设有 $f$ 个故障节点，系统必须足够灵活以在法定人数中排除 $f$ 个故障节点，并至少包含 $f+1$ 个非故障节点。

### **网络假设**：

* **同步网络**：消息传递时间有固定上限（$\Delta$），处理器时钟差异有固定上限（$\delta$），允许将执行划分为轮次。
* **异步网络**：消息传递无固定上限（$\Delta$不存在），或处理器时钟差异无固定上限（$\delta$不存在）。
* **部分同步网络**：$\Delta$和$\delta$都存在但未知，或在全局稳定时间（GST）后已知。

### **复杂性度量**：

* **消息复杂性（Message Complexity）**：发送消息的总数。在 $n$ 个服务器的完全连接集群中，如果一个服务器广播消息 $k$ 轮，消息复杂性为 $O(kn)$；如果每个服务器广播消息 $k$ 轮，则为 $O(kn^2)$。
* **时间复杂性（Time Complexity）**：共识执行所需的消息传递轮数。如果服务器 $S_i$ 向 $S_j$ 发送消息，$S_j$ 回复 $S_i$，时间复杂性为2。

### **服务属性（正确性保证）**：

* **终止（Termination）**：每个非故障服务器最终决定一个值。
* **协议（Agreement）**：没有两个非故障服务器决定不同的值。
* **有效性（Validity）**：如果所有服务器输入相同，则非故障服务器决定的任何值必须是该共同输入。
* 这些属性也可解释为：
    * **安全性（Safety）**：在故障存在下，没有两个非故障副本对请求的执行总顺序达成不同意见。
    * **活性（Liveness）**：如果输入正确，执行最终会终止；在SMR中，客户端最终会收到对其请求的回复。

## **更高效的BFT共识算法（代表性算法）**

1.  **PBFT (Practical Byzantine Fault Tolerance)**：

* **模型与属性**：开创性的BFT共识实用解决方案。在 $n=3f+1$ 个副本中最多容忍 $f$ 个故障副本。在异步网络中提供安全性，但活性需要有界消息延迟的同步性。复制协议通过视图（views）连续进行，每个视图有一个主副本。
* **复制协议**：
    * 客户端向主节点发起操作（Request Phase），设置计时器。若 $f+1$ 条回复，则操作完成。若超时，则向所有副本广播请求。
    * 主节点开始共识：Pre-prepare Phase（分配唯一序列号，组装PRE-PREPARE消息并发送给所有备份）。
    * Prepare Phase（备份验证PRE-PREPARE，广播PREPARE消息；收集2f个PREPARE消息后，认为请求已准备好，形成法定人数证书）。
    * Commit Phase（副本广播COMMIT消息；收集2f个COMMIT消息后，认为请求已提交）。
    * Reply Phase（备份向客户端发送REPLY消息；客户端等待 $f+1$ 条有效签名的回复以确认）。
    * 使用检查点（Checkpoints）定期验证执行状态，形成稳定检查点以清理旧日志。
* **视图变更协议**：
    * 当主节点失败时（客户端请求超时），备份启动视图变更。
    * 进入新视图（$v+1$），新主节点为 $P=(v+1)$ mod $n$。
    * 备份广播VIEW-CHANGE消息（包含新视图号、最新稳定检查点信息C、以及预准备P和准备Q的请求信息）。
    * 新主节点收集 $2f-1$ 个VIEW-CHANGE-ACK消息，形成视图变更证书。
    * 新主节点广播NEW-VIEW消息，包含新视图号V和之前视图中未提交但被法定人数看到的请求X。
    * 备份验证新主节点的决定，否则再次启动视图变更。
* **优缺点**：
    * **优点**：开创性实用解决方案，对高效BFT算法影响深远，被许多许可型区块链采用。扩展版本支持主动恢复。
    * **缺点**：二次消息复杂性 $O(n^2)$ 限制其大规模应用。故障客户端可能导致系统重复视图变更而无法进展。

2.  **SBFT (A Scalable and Decentralized Trust Infrastructure)**：
    
* **模型与属性**：领导者型BFT共识算法，容忍 $f$ 个拜占庭服务器和 $c$ 个崩溃或滞后服务器，共 $3f+2c+1$ 个服务器。在无故障同步网络下有“快速路径”，否则无缝切换到“慢路径”（linear-PBFT），无需视图变更。通过使用门限签名将消息复杂性从 $O(n^2)$ 降低到 $O(n)$。
* **复制协议**：
    * **快速路径**：主节点发送指令；服务器验证后将回复发送给Commit Collector (C-collector)；C-collector收集签名回复，聚合为门限签名消息广播给其他服务器；Execution Collector (E-collector) 收集回复，聚合为门限签名消息并分发给客户端。
    * **linear-PBFT**：在故障或部分同步下切换。消息复杂性为 $O(n)$。主节点始终是最后一个收集器。
* **视图变更协议**：消息传输复杂性为 $O(n^2)$。由副本触发超时或 $f+1$ 副本怀疑主节点故障的证明来启动。新主节点收集 $2f+2c+1$ 个视图变更消息，发起新视图。
* **优缺点**：
    * **优点**：门限签名实现线性消息传输。客户端通信从 $O(f+1)$ 降至 $O(1)$。
    * **缺点**：继承PBFT的弱点。故障客户端可能通过选择性通信触发不必要的视图变更。

3.  **HotStuff (BFT Consensus in the Lens of Blockchain)**：

* **模型与属性**：领导者型BFT共识算法，容忍 $f$ 个拜占庭服务器，共 $3f+1$ 个服务器。活性需要部分同步网络，安全性不依赖同步假设。保证乐观响应性（$2f+1$ 条消息即可进展）。每个共识实例轮换主服务器以确保链质量。使用门限签名实现线性共识（$O(n)$ 消息复杂性）。
* **复制协议**：
    * 客户端广播请求。主节点广播PREPARE消息；副本验证后发送签名prepare-vote给主节点。
    * 主节点收集 $2f+1$ 个prepare-vote形成prepareQC，广播PRE-COMMIT消息。副本存储prepareQC，发送commit-vote给主节点。
    * 主节点收集 $2f+1$ 个commit-vote形成pre-commitQC，广播COMMIT消息。副本更新lockedQC，发送COMMIT vote给主节点。
    * 主节点收集 $2f+1$ 个COMMIT vote，广播DECIDE消息。副本执行操作，递增viewNum，发送NEW-VIEW给新主节点。客户端等待 $f+1$ 条回复确认。
    * 每个共识实例轮换领导者。
* **视图变更协议**：频繁的视图变更。新主节点由 $p=v$ mod $n$ 决定。
* **优缺点**：
    * **优点**：门限签名实现线性消息传输。决策可以流水线化，降低时间复杂性。可扩展到无许可区块链。
    * **缺点**：频繁的领导者轮换在故障存在时会出现问题。故障服务器被分配主节点职责时吞吐量显著下降。

4.  **ISS (State Machine Replication Scalability Made Simple)**：
    
* **模型与属性**：通用框架，将单领导者全序广播（TOB）协议扩展为多领导者协议。通过将工作负载分配给多个领导者，每个领导者运行一个独立的Sequenced Broadcast (SB) 实例，从而实现并行TOB实例。假设部分同步网络，容忍 $f$ 个拜占庭故障节点，共 $3f+1$ 个节点。吞吐量显著高于单领导者协议。
* **复制协议**：
    * 每个节点维护一个连续日志，包含所有接受的消息（批处理）。
    * 日志分为纪元（Epochs），每个纪元包含一组连续的序列号（SNs）。纪元进一步划分为段（Segments），每个段分配给一个领导者。
    * 客户端请求根据哈希函数分类到不同的桶（Buckets），每个领导者被分配一个桶。
    * 领导者使用其SNs和桶中的客户端请求进行提案。
    * 每个领导者运行底层TOB协议（如PBFT、HotStuff、Raft）为其SB实例达成共识，并行运行。
    * 当SB实例达成共识时，所有非故障节点sb-deliver该批次。若无法达成共识，则将一个空值放入日志。
    * 当所有前序SNs填满日志时，请求被SMR-DELIVERED给客户端。
* **多领导者选择**：每个纪元选择多个领导者，领导者选择（LE）策略可定制，只要能保证活性。使用BFTMencius保持足够多的正确节点在领导者集中。使用故障检测器识别静默节点，并将其从领导者集中移除，分配新领导者。
* **优缺点**：
    * **优点**：并行运行多个共识实例，显著提高吞吐量。允许客户端请求在发送后即可执行，无需等待当前纪元完成，提供更快响应。通过分桶避免重复处理请求。
    * **缺点**：引入额外共识延迟。客户端请求必须发送并哈希到所有节点。多领导者方式在节点故障时可能导致SB实例失败概率更高，若请求分布不均，某些节点故障会造成更大损失。

5.  **DAG-Rider (All You Need is DAG)**：
    
* **模型与属性**：异步拜占庭原子广播（BAB）协议，具有最优时间和消息复杂性，实现量子后安全性。包含两层：基于轮次的结构化DAG用于可靠消息传播；零开销共识协议允许节点独立确定消息的总顺序，无需额外通信。使用Bracha广播，容忍 $f$ 个故障节点，共 $3f+1$ 个节点。通过假设全局完美硬币保证活性。
* **DAG流水线**：每个节点独立维护DAG，表示其对消息传播拓扑的解释。DAG按轮次进展，节点根据其轮次和事务块添加新顶点。定义强边（直接连接）和弱边（非直接连接）。客户端提案时，节点接收顶点，存入缓冲区，等待所有前置顶点到位后整合入DAG。当收到当前轮次 $2f+1$ 个顶点后，进入下一轮并广播新顶点。最终DAG在非故障节点间收敛。
* **DAG中的共识**：利用完美硬币机制，节点独立检查DAG并决定要交付的区块及顺序，无需额外协调。DAG分为波次（waves），每个波次跨四轮。选择一个随机领导者顶点，交付该领导者顶点或其因果历史中的所有区块。领导者顶点必须有 $2f+1$ 条强边连接到下一轮。
* **优缺点**：
    * **优点**：DAG结构同时用于消息传播和投票。底层可靠广播保证DAG视图一致。实现并行事务流水线，高吞吐量。
    * **缺点**：高延迟，因为事务分发与共识分离。消息复杂性高 $O(n^3 \log n + nM)$。

6.  **Narwhal and Tusk (A DAG-based Mempool and Efficient BFT Consensus)**：

* **模型与属性**：Narwhal使用基于DAG的内存池（Mempool）将事务传播与事务排序分离，以实现高性能共识。将可靠事务传播卸载到Mempool协议，共识仅负责排序少量元数据。容忍 $f$ 个故障，共 $n=3f+1$ 个节点。提供完整性、区块可用性、包含性、2/3因果性、1/2链质量等服务属性。
* **DAG复制协议**：与DAG-Rider类似，但采用新的可靠广播实现。DAG由区块组成，每个区块包含哈希签名、事务列表和上一轮区块的可用性证书。可用性证书包含对应区块的哈希以及来自 $2f+1$ 个其他验证者的签名。
    * 验证者不断接收客户端事务和证书。
    * 当收到 $2f+1$ 个证书后，验证者进入新轮次，创建新区块并广播。
    * 收到区块后，验证者验证签名，确保是源验证者唯一的区块，然后签名哈希以确认。
    * 当收到 $2f+1$ 个确认签名后，验证者创建并广播可用性证书，停止广播原始区块。
    * Tusk负责共识过程。通过减少波次数将共识总时间复杂性降至4.5轮。
* **优缺点**：
    * **优点**：作为基于DAG的BFT协议的实际实现，在经验实验中吞吐量优于传统BFT算法。
    * **缺点**：内存池不维护顺序，导致事务共识延迟高，需等待多轮。

## **更鲁棒的BFT共识算法（代表性算法）**

1.  **Aardvark (Making Byzantine Fault-Tolerant Systems Tolerate Byzantine Failures)**：

* **模型与属性**：旨在提高在“宽容执行”（gracious executions，同步网络、所有客户端和服务器都正确）下实现高性能的BFT算法的鲁棒性。容忍 $f$ 个故障副本，共 $3f+1$ 个副本。安全性在异步网络中得到保证，活性需要有界消息延迟。强调BFT算法应首先能够容忍拜占庭故障和恶意攻击，在“不友好执行”（uncivil executions，有界网络延迟，最多 $f$ 个拜占庭故障服务器，无限拜占庭客户端）下性能下降应保持在合理水平。
* **鲁棒性改进**：更强的消息认证（签名客户端请求）、独立通信（资源隔离）、自适应领导者轮换（定期视图变更）。
* **日志复制鲁棒性**：客户端请求使用数字签名进行认证。通信使用独立的NICs和线路。副本有独立的客户端请求和内部副本消息队列。验证客户端和副本消息，检查黑名单、MAC、序列、冗余、签名、每视图一次等。
* **视图变更鲁棒性**：采用与PBFT相同的视图变更协议，但增加了对主节点行为的两种预期：及时、公平地发出PRE-PREPARE消息，并保持持续吞吐量。若主节点未满足，则强制视图变更，即使主节点是正确的。
* **优缺点**：
    * **优点**：解决了PBFT类共识算法的鲁棒性问题，尤其是在容忍故障客户端方面。在不友好执行下的吞吐量下降低于宽容执行。
    * **缺点**：对正确主节点的严格要求（保持90%吞吐量）可能给正确副本带来不必要负担。主节点行为可能导致更多性能下降。可能不必要地替换正确主节点，阻碍更高吞吐量。

2.  **Pompe (Byzantine Ordered Consensus Without Byzantine Oligarchy)**：

* **模型与属性**：构建在标准共识算法之上（如SBFT、HotStuff）的排序协议。通过民主地收集法定人数的偏好顺序来防止拜占庭副本操纵命令顺序。容忍 $f$ 个故障副本，共 $3f+1$ 个副本。引入“拜占庭有序共识”新属性，为每个操作分配排序指示器，防止拜占庭寡头操纵排序。
* **复制协议**：
    * **排序阶段**：提议者广播REQUESTTS消息以征求命令的首选时间戳；提议者收集RESPONSETS消息形成法定人数后，选择中位数时间戳作为命令的顺序，并广播SEQUENCE消息。副本验证并接受顺序。
    * **共识阶段**：Pompe依赖于周期性运行的应用共识算法（如HotStuff）来对有序命令批次进行共识。
* **视图变更协议**：没有新的视图变更设计。当主节点故障时，依赖于应用共识算法检测故障并启动视图变更。
* **优缺点**：
    * **优点**：将BFT SMR的正确性讨论扩展到操作排序，对金融应用有重要影响。操作排序由法定人数民主决定。将共识分为排序和共识两个主要阶段。
    * **缺点**：未设计特定的共识算法，而是使用任何标准算法执行第二阶段。不清楚当这些算法应用于排序服务时如何保证安全性和活性。

3.  **Spin (Byzantine Fault Tolerance With a Spinning Primary)**：

* **模型与属性**：解决领导者型BFT算法在故障领导者下性能下降的问题。容忍 $f$ 个故障，共 $3f+1$ 个副本。使用每请求轮换主节点的方式，避免特定副本的领导者垄断。使用黑名单防止被怀疑的故障副本成为主节点。
* **日志复制鲁棒性**：正常操作遵循PBFT通信模式，包括PRE-PREPARE、PREPARE和COMMIT阶段。每处理一个批次请求就轮换主节点，无需序列号，使用视图号代替。副本在超时或收到 $f+1$ 个MERGE消息时触发合并操作，确定前一视图中哪些请求可以接受和执行。
* **视图变更鲁棒性**：由于每请求轮换领导者，不需要显式视图变更协议。使用黑名单排除行为不当的副本作为主节点。黑名单容量最多为 $f$。故障主节点触发合并操作时被列入黑名单。
* **优缺点**：
    * **优点**：通过每请求轮换领导者，在针对主节点的恶意攻击下更鲁棒。分摊协调工作负载，缓解单主节点瓶颈。
    * **缺点**：在无故障情况下，领导者轮换会引入额外消息传递开销。合并操作的消息复杂性为 $O(n^2)$，在每次副本故障时都会触发，对系统性能产生负面影响。

4.  **Prosecutor (Behavior-Aware Penalization Against Byzantine Attacks)**：

* **模型与属性**：假设部分同步网络，容忍 $f$ 个拜占庭故障，共 $3f+1$ 个副本。允许服务器副本主动声称自己是新主节点并进入“候选者”中间状态。通过对候选者施加计算惩罚来抑制拜占庭服务器成为主节点，惩罚难度随其过去行为而变化。
* **复制协议**：高效复制客户端请求，消息复杂性为 $O(n)$。使用门限签名。协议有五个阶段：客户端广播请求；主节点分配顺序并发送给所有副本；副本部分签名背书并回复主节点；主节点收集 $2f+1$ 条回复后发布提交指令；副本检查指令并通知客户端本地已提交。
* **视图变更协议**：与计算惩罚相关联。包含执行计算和投票两个主要步骤。备份在计时器过期时执行类似工作量证明的哈希计算。结果需满足一定阈值，否则重复计算。满足后成为候选者，广播VOTEME消息并等待投票。若收集到 $2f$ 票，则成为新主节点并广播NEW-VIEW消息。每次竞选会增加计算难度，行为不当的候选者会被逐渐边缘化。
* **优缺点**：
    * **优点**：惩罚可疑故障副本，实现线性消息复杂性下的高效共识。拜占庭服务器发动攻击篡夺领导权时，会被惩罚并强制执行指数级增长的计算工作，从而被抑制和边缘化。
    * **缺点**：工作量证明式的惩罚在故障服务器计算能力强时效率可能降低，可能导致长时间无正确领导者。PrestigeBFT通过更细粒度和高效的方式量化可疑服务器的声誉。

5.  **RBFT (Redundant Byzantine Fault Tolerance)**：

* **模型与属性**：解决Prime、Aardvark、Spin等旨在提高容错鲁棒性的方法在某些极端情况下可能导致性能下降的问题。这些极端情况通常针对主节点，可能导致单点故障。通过并行执行多个PBFT协议实例来增加共识过程中的冗余。每个副本在相应实例中扮演主节点角色。其中一个实例是“主”实例，其他是“备份”实例，监控主实例的处理速度，防止其故意减慢共识过程。容忍 $f$ 个故障，共 $3f+1$ 个副本。
* **复制鲁棒性**：
    * 请求阶段：客户端向所有副本广播请求。
    * 传播阶段：副本检查签名后向所有其他副本广播请求。
    * 本地PBFT实例：每个副本启动本地PBFT共识实例。
    * 提交与回复：收集 $2f+1$ 个COMMIT消息后提交请求并回复客户端。
    * 冗余监控：多个并行运行的实例监控主实例的处理速度。若主实例处理速度低于阈值，则认为其故障，并启动实例变更。
    * 公平性监控：实例还跟踪每个请求的平均处理延迟。若主实例对某些客户端处理时间偏离平均值过大，则认为其不公平，备份实例启动实例变更。
* **实例变更鲁棒性**：与PBFT的视图变更协议类似，用于替换故障主节点。每个实例维护一个计数器 $c$。若主实例不满足阈值，备份实例递增 $c$ 并广播INSTANCE-CHANGE消息。收集到 $2f+1$ 个相同计数器的INSTANCE-CHANGE消息后，选择新的主实例，系统进入新视图。
* **优缺点**：
    * **优点**：通过并行运行多个实例监控主实例性能，解决某些极端情况下的性能下降问题。
    * **缺点**：引入更多操作成本（冗余）。消息复杂性高 $O(|M|(n^3+n^2+n))$。在地理分布应用中，由于客户端与不同副本之间的通信延迟差异，可能导致不必要的实例变更。

## **更可用的BFT共识算法（代表性算法）**

* **特点**：专注于解决BFT共识中的可用性问题，在同步性有限的场景下运行。通常是无领导者算法，因为领导者型算法存在单点故障风险，且主服务器工作负载重。
* **基础构建块**：

    1.  **可靠广播 (Reliable Broadcast, Bracha's RBC)**：在异步网络中实现协议。

* 发送者广播INITIAL消息。
* 接收到INITIAL消息的副本广播ECHO消息。
* 若收到 $n-f$ 个相同ECHO消息，或 $f+1$ 个相同READY消息，副本广播READY消息。
* 若收到 $n-f$ 个相同READY消息，副本交付值。
* 保证若提议者正确，所有正确进程交付其提议值；若提议者故障，所有正确进程要么交付相同值，要么都不交付。

    2.  **二元拜占庭协议 (Binary Byzantine Agreement, BA)**：在异步网络中运行。通过多轮协调达到共识。每轮有三个阶段。

* 阶段1 (BV-broadcast)：每个副本提议一个估计值（0或1），广播。若收到 $f+1$ 个相同值，则重新广播。若收到 $2f+1$ 个相同值，则视为交付。
* 阶段2：副本广播AUX消息。
* 阶段3：若收到 $n-f$ 个AUX消息，且所有消息包含单个值，则启动硬币翻转过程决定最终交付，并设定下一轮的估计值。
* 保证有效性（决定值由正确副本提议）、协议（无冲突决定）和终止（最终达成决定）。

### 1.  **DBFT (Democratic Byzantine Consensus)**：

* **模型与属性**：无领导者BFT协议，容忍 $f$ 个拜占庭副本，至少 $3f+1$ 个副本。在部分同步网络中运行，消息模式结合RBC和BA的派生版本Psync（使用弱协调器）。最佳情况下时间复杂性为6轮，消息复杂性为 $O(n^3)$。
* **二元拜占庭共识 (Psync)**：对BA协议进行三项主要修改：增加超时触发器以处理部分同步网络；在阶段2增加弱协调器以解决冲突；在阶段3增加终止条件。弱协调器以轮询方式选择，通过广播COORD消息来解决冲突。
* **DBFT协议**：由RBC实例（每个实例对应一个提议值）和 $n$ 个Psync实例（每个副本贡献一个）组成，这些Psync实例可以并行执行。
    * **快速路径**：若副本通过RBC交付数据，则跳过Psync阶段1的两次广播，直接从阶段2开始。
    * **常规路径**：若副本未通过RBC交付数据，则加入每个Psync实例，从阶段1开始，提议值为0。
    * 当某个Psync实例交付1时，DBFT共识实例决定数据。
* **优缺点**：
    * **优点**：通过引入冲突解决器（弱协调器）改进BA协议。Psync在快速路径中直接决定二元值，提高吞吐量和延迟。
    * **缺点**：需要部分同步网络。在有 $f$ 个拜占庭副本时，仍需要 $O(f)$ 的延迟。

### 2.  **HoneyBadgerBFT (The Honey Badger of BFT Protocols)**：

* **模型与属性**：无领导者BFT共识协议，容忍 $f$ 个拜占庭副本，共 $3f+1$ 个副本。可在异步网络中运行。使用门限加密防御审查攻击。时间复杂性为 $O(\log n)$，消息复杂性为 $O(|M|n + |c|n^3 \log n)$。
* **高效大消息可靠广播**：通过在Bracha的RBC协议中使用擦除编码，将通信复杂性从 $O(|B|n^2)$ 降低到 $O(|B|n)$。
    * 发送者使用Reed-Solomon码编码数据批次，并分发到每个副本。
    * 副本接收INITIAL消息后广播ECHO消息，并验证数据块的校验和。
    * 副本在满足条件后广播READY消息。
    * 收到 $n-f$ 个READY消息后，副本收集足够数据块解码并交付。
* **带加密共同硬币的二元拜占庭协议**：修改BA协议，使用门限签名生成共同硬币。新增终止条件以防BA长时间循环。
* **异步共同子集（ACS）**：HoneyBadgerBFT的核心构建块。一个ACS实例包含多达 $n$ 个修改后的RBC实例和多达 $n$ 个修改后的BA实例并行运行。
    * 阶段1：副本启动RBC实例。
    * 阶段2：副本加入多达 $n$ 个BA实例来决定是否接受提议。
* **完整协议**：分三个阶段协调所有副本的步调以达成共识。
    * 阶段1：副本随机选择事务批次并用门限加密方案加密。
    * 阶段2：加密数据作为ACS实例的输入，获取加密数据块的集合。
    * 阶段3：副本解密每个加密数据块以获取原始事务集。
* **消息复杂性与批次大小**：总消息复杂性约为 $O(|M|n+|c|n^3 \log n)$。为获得最佳吞吐量，设置全局批次大小 $M=\Omega(|c|n^2 \log n)$。
* **优缺点**：
    * **优点**：在数百个副本中可实现每秒数万次事务的高吞吐量。首个保证异步网络活性的实用解决方案。提供多种加密机制防御审查攻击。
    * **缺点**：为实现高吞吐量而牺牲延迟（当 $n>48$ 时延迟较高，>10s）。擦除编码库将 $n$ 的上限设为128。

### 3.  **BEAT (Asynchronous BFT Made Practical)**：

* **模型与属性**：包含五种无领导者异步BFT协议（BEAT0到BEAT4），旨在解决吞吐量、延迟、带宽使用和BFT存储等不同目标。受HoneyBadgerBFT启发并进行改进。
* **BEAT0**：
    * 使用带标签的门限加密机制，并用TDH2替换基于配对的加密，显著降低加密延迟。
    * 通过直接应用门限硬币剪裁器方法，替换HoneyBadgerBFT的共同硬币协议，降低获取共同硬币的延迟。
    * 使用更高效的擦除编码库Jerasure 2.0，性能高于zfec，可扩展集群大小至128个副本以上。
* **BEAT1和BEAT2**：
    * BEAT1使用原始Bracha的RBC，以获得更低的广播延迟。
    * BEAT2将带标签的门限加密从服务器端移到客户端端，防止故障副本延迟事务处理进行审查攻击。使用匿名通信网络隐藏客户端信息以防御审查攻击，实现弱一致性保证（因果顺序保存）。
* **BEAT3**：
    * 使用基于擦除编码的RBC协议AVID-FP，只在第一阶段广播分段数据块，其余阶段只传输全局交叉校验和，大幅减少网络带宽使用 $O(|B|)$。
    * 不保证所有正确副本最终收到原始数据，但客户端可以从 $f+1$ 个分段和校验和重建原始数据。
    * 性能优于HoneyBadgerBFT，在吞吐量、延迟、可扩展性、网络带宽和存储开销方面都有提升。
* **BEAT4**：
    * 用AVID-FP-Pyramid（使用金字塔码）替换BEAT3中的AVID-FP，降低读操作的数据重构成本。
    * 金字塔码引入额外奇偶校验数据，但允许用更少信息进行部分数据重构，实现更高效数据恢复。
    * 客户端可直接从对应副本请求特定数据分段和校验和，若分段故障，可先从组级别分段重建。
    * 可节省50%读取带宽，增加约10%存储空间。
    * 当 $f=1$ 时延迟高于HoneyBadgerBFT，但当 $f>1$ 时，BEAT4在所有性能指标上均优于HoneyBadgerBFT。
* **讨论**：BEAT0、BEAT1、BEAT2适用于通用SMR应用，而BEAT3、BEAT4更适合BFT存储服务。

## **未来研究方向**

1.  **可扩展性（Scalability）**：在高性能（高吞吐量、低延迟）与大规模系统（数千个节点）间取得平衡仍是挑战。
2.  **排序公平性（Ordering Fairness）**：防止故障领导者不公平处理客户端请求（如“抢跑攻击”），确保信任和公正。
3.  **量子安全BFT共识（Post-quantum safe BFT consensus）**：当前BFT算法依赖传统密码学，易受量子计算机攻击。需研究后量子密码学或减少密码学参与来防御量子拜占庭攻击。
4.  **互操作性（Interoperability）**：不同BFT区块链和分布式系统间的互操作性日益重要。研究跨链共识和机制以促进无缝数据和资产转移，增强系统灵活性和实用性。
5.  **机器学习中的BFT共识（BFT consensus for machine learning）**：在分布式训练中，BFT共识对于维护数据和训练完整性至关重要，以确保机器学习模型的准确性和可靠性。在高并发多智能体系统中，高性能、鲁棒的BFT算法可防御恶意智能体和行为。

这些挑战反映了业界对构建更具可扩展性、鲁棒性和可操作性的BFT应用的需求，将极大促进安全高效分布式系统的发展和采用。

## Verifiable Computing、Optimistic Approach、Coded Computing

在区块链领域，**可验证计算 (Verifiable Computing)**、**乐观方法 (Optimistic Approach)** 和 **编码计算 (Coded Computing)** 是三种不同的技术或范式，它们各自从不同角度解决区块链面临的挑战，主要是关于**可扩展性、效率和信任**。

### 1. 可验证计算

**核心思想：**

可验证计算是一种密码学技术，允许一个**验证者 (verifier)** 能够高效地检查由另一个**证明者 (prover)** 执行的计算结果的正确性，而无需自己重新执行整个计算。它旨在将计算任务外包给可能不完全受信任的第三方，同时仍然确保计算结果的完整性和准确性。

**工作原理：**

* **外包计算：** 复杂的计算任务被外包给一个或多个计算提供者（证明者）。
* **生成证明：** 证明者在执行计算的同时，会生成一个简洁的**正确性证明 (proof of correctness)**，这个证明通常比原始计算本身小得多。
* **高效验证：** 验证者接收计算结果和证明，并使用密码学方法（如零知识证明 ZKP、SNARKs/STARKs）快速验证证明的有效性，从而确认计算结果的正确性。验证证明的开销远小于重新执行计算。

**在区块链中的应用：**

* **链下计算 (Off-chain Computation)：** 区块链本身处理复杂计算的效率很低，成本很高。可验证计算允许将大量计算从主链转移到链下执行，然后只将计算结果和相应的正确性证明提交到链上进行验证。这显著提高了区块链的可扩展性和吞吐量。
* **智能合约的复杂逻辑：** 使得智能合约能够处理更复杂、计算密集型的任务，而无需在链上消耗大量Gas。
* **数据隐私：** 某些可验证计算技术（如零知识证明）还可以用于在不泄露底层数据的情况下证明计算的正确性，从而增强隐私性。

**优势：**

* **提高可扩展性：** 大幅减少链上计算负担。
* **降低成本：** 减少交易费用和资源消耗。
* **增强安全性：** 即使在不信任的环境下也能保证计算结果的正确性。

### 2. 乐观方法 (Optimistic Approach)

**核心思想：**

乐观方法，尤其是在区块链的**Optimistic Rollups (乐观汇总)** 中，采取一种"性善论"的假设：**默认情况下，所有链下执行的交易和计算都是有效的，除非有人证明它们是欺诈性的。**

**工作原理：**

* **链下批处理：** 大量的交易和计算在链下进行处理和打包（"汇总"），然后将汇总后的结果（通常是一个状态根的更新）提交到主链上。
* **挑战期 (Challenge Period)：** 在提交到主链后，会有一个**"挑战期"**（通常为几天到几周）。在这个挑战期内，任何人都可以提交**"欺诈证明 (fraud proof)"**来质疑链下计算的正确性。
* **欺诈证明与争议解决：** 如果有人发现欺诈行为，他们可以提交一个欺诈证明。主链上的智能合约会验证这个证明。如果欺诈被证实，则错误的状态更新会被回滚，并且提交欺诈行为的节点会受到惩罚（例如，他们的抵押资产会被罚没），而挑战者可能会获得奖励。
* **无挑战即最终确定：** 如果在挑战期内没有提出有效的欺诈证明，那么链下提交的计算结果就被认为是最终有效的。

**在区块链中的应用：**

* **Layer 2 扩容方案：** Optimistic Rollups 是目前最流行的 Layer 2 扩容方案之一（例如 Optimism、Arbitrum），旨在提高以太坊等区块链的吞吐量并降低交易费用。
* **链下状态转换：** 允许复杂的DApp逻辑在链下运行，显著减轻主链负担。

**优势：**

* **高吞吐量：** 通过链下批处理实现更高的交易处理速度。
* **成本效益：** 大幅降低链上交易费用。
* **EVM兼容性好：** 相对于零知识证明的方案，Optimistic Rollups 通常更容易与现有的以太坊虚拟机 (EVM) 兼容。

**局限性：**

* **提款延迟：** 由于挑战期的存在，从 Layer 2 提款到 Layer 1 需要等待挑战期结束，这导致了用户资金的锁定时间。
* **需要活跃的监督者：** 尽管理论上任何人都可以在挑战期内提交欺诈证明，但在实践中，需要有足够的激励机制来确保有足够多的"诚实"节点来监控和提交欺诈证明。

### 3. 编码计算

**核心思想：**

编码计算是一种利用**编码理论**（类似于通信中的纠错码）来提高**分布式计算**的鲁棒性、效率和安全性的技术。它通过在计算任务中**引入冗余**来应对分布式系统中常见的挑战，例如**"掉队者" (stragglers)**（运行缓慢或失败的节点）、通信开销和数据隐私问题。

**工作原理：**

* **任务编码：** 原始的计算任务或数据会被编码成带有冗余信息的形式，然后分发给多个工作节点。
* **冗余处理：** 每个工作节点可能只执行部分编码后的计算，或者执行多个冗余的计算。
* **容错性：** 即使某些节点失败或运行缓慢（掉队），系统仍然可以通过从其他成功完成任务的节点收集足够多的结果来恢复或完成整个计算，而无需等待所有节点。
* **减少通信或隐私：** 通过巧妙的编码设计，有时可以减少通信量，或者在计算过程中提供额外的隐私保护。

**在区块链中的应用（潜在或研究方向）：**

虽然编码计算不像可验证计算和乐观方法那样直接应用于区块链的Layer 2扩容，但在更广义的分布式系统背景下，它与区块链的某些特性是契合的：

* **分布式存储：** 在去中心化存储网络中，编码计算可以增强数据的可靠性和可用性，即使部分存储节点离线也能恢复数据。
* **分布式共识：** 在某些需要大量计算的共识机制中，编码计算可能有助于提高其鲁棒性，应对节点故障。
* **链下计算的容错性：** 在可验证计算的外包计算阶段，如果证明者是分布式集群，编码计算可以帮助提高其容错性，确保即使部分证明者出现问题也能生成证明。

**优势：**

* **提高鲁棒性/容错性：** 应对分布式系统中的节点故障或性能下降。
* **提高效率：** 通过避免等待慢节点来加速整体计算。
* **潜在的数据安全和隐私：** 某些编码方案可以提供额外的安全层。

### 区别总结

特性|可验证计算 (Verifiable Computing)  | 乐观方法 (Optimistic Approach) | 编码计算 (Coded Computing)|
|:---------------:| :-------------------:|:----------------:|:------------------:|
| **核心目标** |证明计算结果的**正确性**，无需重新执行。|默认计算**有效**，通过**挑战**纠正错误。| 提高分布式计算的**鲁棒性、效率和安全性**，应对故障。|
| **信任假设** |验证者信任证明的有效性，而非计算执行者的诚实性。| 乐观假设诚实，通过**欺诈证明**机制应对不诚实。 | 基于编码冗余，容忍部分节点故障。|
| **验证机制** | 密码学证明 (ZKP, SNARKs/STARKs) | **欺诈证明** (Fraud Proofs)     | 基于编码理论的**冗余和恢复**机制。 |
| **关键应用** | **链下计算扩容**、隐私保护、智能合约复杂逻辑。 | **Layer 2 扩容** (Optimistic Rollups)。  | 去中心化存储、分布式AI训练、通用分布式计算容错。|
| **链上交互** | 提交简洁的**证明**进行验证。| 提交**批处理结果**，挑战期内可提交**欺诈证明**。 | 间接相关，主要用于优化链下分布式计算或存储。|
| **提款/最终性** | 证明验证后立即最终确定（如果证明是有效的）。| 有**挑战期**，导致提款延迟。| 依赖于底层应用，本身不直接涉及链上最终性。|

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> survey_Jacobson </div>
<div class="file-meta"> 2,338 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/survey_Jacobson.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 5

## **Solana 区块链生态系统**

1.  **Solana的特点**

* 被称为"世界上使用最多的区块链"。
* 专为广泛、主流应用而设计：快速、可扩展、能源效率高。

2.  **区块链对比 (截至2024年12月)**

* **交易速度 (确认时间)**：
    * Solana：0.4秒。
    * 以太坊：15分钟。
    * 比特币：60分钟。
* **平均费用**：
    * Solana：一分钱的零头。
    * 以太坊：3.09美元。
    * 比特币：5.31美元。
* **效率**：
    * Solana：高吞吐量，底层低延迟。
    * 以太坊：低吞吐量，Layer 2解决方案提高效率但有风险和缺点。
    * 比特币：低吞吐量，高费用。
* **共识机制**：
    * Solana：权益证明 (Proof of Stake) 和历史证明 (Proof of History)。
    * 以太坊：权益证明 (Proof of Stake)。
    * 比特币：工作量证明 (Proof of Work)。
* **Solana交易吞吐量**：最高记录7,229 TPS，理论上可处理高达65,000 TPS。

3.  **Solana的关键数据**

* 每秒事务处理量：4,393+。
* 总交易量：3750亿+。
* 每笔交易中位费用：0.00064美元。
* 净碳足迹：0%。
* Solana每天处理的交易量超过所有其他链的总和。

4.  **核心创新：历史证明 (Proof of History)**

* **问题**：许多可编程区块链（如以太坊）依赖外部程序分配“中位”时间戳来验证交易顺序。
* **解决方案**：历史证明允许将“时间戳”内置到区块链本身中，通过可验证延迟函数 (VDF) 实现，与权益证明结合使用，以提高速度和可扩展性。

5.  **为大规模采用而生**

* 快速、去中心化、可扩展。
* USDC流通量：6.95亿+。
* 每日活跃账户：28万。
* 每日活跃交易量：1400万。
* 赋能全球多家公司的工具和集成，包括Mastercard、CIRCLE、VISA、Discord、Stripe、Shopify、Meta、Jump、Google。

6.  **赋能金融基础设施**

* 闪电般快速的跨境支付：近乎零费用，无中介。
* 下一代支付轨道正在Solana上构建。
* **Mastercard**：与Solana合作制定新的加密凭证标准 (2023年4月)。
* **Mercuryo**：推出Spend，连接Solana钱包到9000万+Mastercard商户 (2024年9月)。
* **Libre - RWA**：与Hamilton Lane和Brevan Howard合作，将现实世界资产上链。
* **Lulo - Savings**：稳定币储蓄平台，优化DeFi收益，存款1.25亿美元+。
* **Kast**：稳定币支付卡，全球1亿+商户和ATM接受。
    * 无国界支付：无银行延迟或转换问题。
    * 有竞争力的奖励：每笔交易高达10%现金返还。
    * 由金融专家创立：团队来自Circle、Phantom、Revolut、Wise等顶级公司。
* **Lulo (储蓄应用)**：
    * 收益：6%-15%。
    * 安全性：受保护存款（相较于Coinbase、Robinhood的FDIC银行保护或其他DeFi的无保护）。
    * 费用：无费用（相较于Robinhood的5美元/月或其他DeFi的性能+提现费）。
    * 提现：即时（相较于2-3天+）。
    * 总存款：1.25亿+美元。
    * 用户数量：1.5万。

7.  **Solana的金融基础设施工具**

* 实时结算：实现全球金融交易的即时共识和实时结算。Solana架构旨在同时处理大量交易。
* 可定制合规性：新的代币标准与大型机构合作构建，专为复杂行为和监管合规性设计。
* 全球支付：Solana的速度和低费用使得大规模去中心化支付成为可能。

8.  **Solana用例**

* **支付卡**：Kast。
* **储蓄应用**：Lulo。
* **健康追踪**：Cudis (健康与长寿协议)。

    * 用户拥有健康数据、赚取奖励。
    * 首款奖励健康之旅的AI智能戒指。
    * 社区成员200K+，来自103个国家和地区。
    * 测量心跳40M+次。
    * 奖励健身课程500K+次。
    * 捕捉总睡眠时间35亿+小时。
    * 步数40亿+步。

9. **资本市场中的Solana**

* **代币化股票和现实世界资产**：
    * 传统金融轨道需要升级，Solana区块链正在推动资本市场的下一次演变。
    * 截至2025年5月，已有210亿美元的现实世界资产在公共区块链上代币化。麦肯锡预测到2030年将达到2万亿美元。
    * 提供关于在Solana上发行代币化股票的报告。
* **代币化股票 (XxStocks)**：
    * 将美国股票市场带到链上：可访问且兼容DeFi的代币化股票。
    * 由Backed提供支持，它是业内历史最悠久的RWA发行方之一。
    * 可转移代币：可在钱包中持有，或在链上应用中买卖。
    * 兼容DeFi：可在DEXs（去中心化交易所）、借贷协议和DeFi应用中使用。

10. **Solana生态系统现状**

* 越来越多的DeFi项目和传统金融公司正在Solana上构建应用。
* 链上GDP：1.7亿美元（环比增长213%）。
* 月活跃钱包：510万。
* DeFi TVL (总锁定价值)：86亿美元，是DeFi TVL第二大链。
* 每日平均费用支付者：15万。
* 建设者和创作者：39亿+美元（环比增长53%）。
* USDC市值：86亿美元。

11. **Solana上的机会 (Superteam)**

* **人才**：通往领先Solana工作岗位的门户。一个由社区驱动的招聘机构，在Solana生态系统中建立职业生涯。
* **挣钱**：基于项目的机会和奖金。
    * 例如：LastMint Play Test（铸造最多者获胜，150 USDC奖金）；Build Vietnam's Blockchain Future（超级团队越南，1500 USDC奖金）；制作宣传视频（300 USDC奖金）。
* **即时拨款 (Instagrants)**：来自资助伙伴的免股权资助。
    * 最高可达1万美元资助。
* **创业支持**：加速器快速通道、活动与社交、演示日与反馈、黑客松支持。
* **合作周五**：在多伦多、温哥华、蒙特利尔设有联合办公点。
* **成员**：50多名成员，来自Solana生态系统中的顶级组织和创始人，包括BONK、CLAYNOSAURZ、TENSOR、MONKE DAO、PYTH、Newton、MCA、HELIUS、ORCA、Sec3、The Graph、VYBE、TARS AI、SONIC、Buddy.link、THE WEB3 PROF、SUPERBASEDD、Websto、fractl、BR1、UBC、TITAN、Astralane、Lucid Drakes。

## **Polygon：扩展以太坊以实现大规模采用**

1.  **什么是Polygon？**

* 一个全面的扩容平台，旨在使以太坊更快、更实惠。
* **起源**：最初作为以太坊的侧链（Sidechain）推出，具有自己的安全模型和验证器网络。
* **演进**：扩展为Layer 2框架，包含直接由以太坊共识机制保障的Rollup技术。
* Polygon不是一个单一的区块链，而是一个兼容以太坊的链框架。

2.  **Polygon解决的问题（以太坊的局限性）**

* **以太坊吞吐量有限**：每秒约15笔交易。
* **高昂的Gas费用**：网络拥堵时交易成本可能飙升至50美元以上。
* **大规模采用障碍**：无法支持数百万用户进行DeFi、NFT和游戏应用。
* 以太坊优先考虑安全性而非性能，并遵循以Rollup为中心的路线图。

3.  **Polygon的扩容技术**

* **Polygon PoS (Proof of Stake)**：
    * 侧链解决方案，带桥接功能。
    * 验证器网络：105个活跃验证器使用委托权益证明共识。
    * Heimdall层：管理权益质押合约，创建并提交检查点到以太坊。
    * Bor层：处理区块生产和交易执行，完全兼容EVM。
* **Polygon Miden**：
    * 基于ZK-STARK的Rollup。
    * 支持定制的ZK应用。
* **Polygon zkEVM**：
    * 零知识Rollup。
    * 提供以太坊安全性，同时兼容EVM。
    * **工作流**：
        * Sequencer (排序器)：收集用户交易，建立顺序，并在Layer 2执行。
        * zkProver：生成加密零知识证明，验证批次中所有交易的有效性。
        * Aggregator (聚合器)：将交易及其证明打包并提交到以太坊。
        * Verifier (验证器)：以太坊上的智能合约，高效验证ZK证明。
* **Polygon CDK (Chain Development Kit)**：
    * 用于开发自己的定制Layer 2区块链的工具包。

4.  **性能对比 (以太坊 vs. Polygon解决方案)**

* **速度 (TPS)**：
    * 以太坊：慢 (~15 TPS)。
    * Polygon PoS：快 (~7,000 TPS)。
    * Polygon zkEVM：中等 (~40-50 TPS 目前)。
* **费用**：
    * 以太坊：昂贵 ($0.1-$50)。
    * Polygon PoS：非常便宜 (< $0.01)。
    * Polygon zkEVM：低 (~$0.01-$0.10)。
* **交易最终性**：
    * 以太坊：~1-5分钟。
    * Polygon PoS：~1-2秒。
    * Polygon zkEVM：~30-60秒。
* **验证器**：
    * 以太坊：~1,000,000 (去中心化POS)。
    * Polygon PoS：~100个验证器 (有限的PoS集合)。
    * Polygon zkEVM：无验证器 (使用排序器+zkProver+以太坊验证器)。

5.  **POL：Polygon的实用代币**

* MATIC是为Polygon PoS提供gas、质押和奖励的代币。
* POL是Polygon 2.0下所有Polygon链的升级代币。
* **代币功能**：
    * **交易费用**：用于支付Polygon网络上的操作。
    * **质押**：验证器质押POL以参与共识。
    * **治理**：代币持有者对协议升级和变更进行投票。
* **代币分配**：验证器和质押者、生态系统基金、社区、基金会、团队和顾问。

6.  **挑战与局限性**

* **安全权衡**：PoS侧链依赖于相对中心化的验证器集（105个验证器）。
* **用户复杂性**：对新用户来说，了解不同的Polygon解决方案和桥接资产可能令人困惑。
* **激烈竞争**：zkEVM面临来自更成熟的Optimistic Rollups（如Base、Arbitrum、Optimism）的竞争。
* **技术限制**：零知识证明生成仍然是计算密集型且昂贵的。

7.  **Polygon 2.0 愿景**

* Polygon旨在从单一PoS链发展成为一个完全由ZK保障的、可互操作的网络。
* **无限可扩展性**：可定制的Layer 2链，根据特定应用需求进行定制。
* **以太坊级安全性**：共享零知识证明系统，确保L1等效的安全保证。
* **无桥集成**：本地跨链消息传递和资产转移，无需脆弱的桥接。
* **生态系统协同效应**：整个网络中统一的验证器集。

8.  **直播演示内容**

* 设置数字钱包。
* 添加Polygon测试网。
* 桥接资产。
* **资源**：
    * Polygon Bridge。
    * MetaMask Wallet。
    * StakePool Faucet。
    * Uniswap。
    * Chainlist。

## **BFT共识算法的文艺复兴：革新普遍去中心化系统的共识架构**

* **讲座信息**：Hans-Arno Jacobsen, Jeffrey Skoll计算机网络与创新教授，多伦多大学。与Edward (Gengrui) Zhang合作。2025年7月9日，BTS，加拿大温哥华。
* **主题**：BFT共识算法的复兴：为普及型去中心化系统革新共识架构。
* **共识**：
    * 定义：普遍同意，一致，或多数相关方达成的判断。
    * 共识算法协调系统节点，就应用程序输入（日志、账本、值、命令、事务、区块）达成一致。
    * 何时需要共识：操作顺序、复制日志内容、确定领导者、分布式账本中写入的区块和事务。
* **容错性**：
    * 系统（节点）需要容忍故障，即在发生（部分）故障时能正常工作。
    * **故障类型**：
        * **良性故障 (Benign Failures)**：服务器崩溃、消息丢失、重排序、重复。应用于文件系统、数据库、领导者选举/协调。对应CFT（Crash Fault-Tolerant）共识。
        * **拜占庭故障 (Byzantine Failures)**：任意行为；故障节点（有意或无意）、节点可能撒谎、发送错误消息（不遵循协议、存在bug）。应用于安全关键系统、分布式账本。对应BFT（Byzantine Fault-Tolerant）共识。
    * **系统故障示例**：
        * “蓝屏死机”是一种崩溃故障。
        * 切断通信线路是一种遗漏故障。
        * 信号衰减是一种时序故障或良性故障。
        * “打猎事故”（物理线路损坏）被认为是崩溃故障（可能同时是遗漏故障或时序故障）。
        * 加密货币黑客攻击（如Ronin Bridge，Poly Network，Wormhole）：是由验证者妥协、智能合约漏洞、协议设计缺陷等造成的，被认为是拜占庭故障。
* **主动视图变更**：
    * **问题**：被动视图变更的问题在于需要等待超时才能发现领导者故障，且新领导者需要同步日志，增加延迟。拜占庭服务器可能撒谎并启动选举。
    * **目标**：实现主动视图变更，节点可以主动竞选领导权。不使用领导者调度，而是由检测到领导者故障的节点启动选举，只选举最新节点。
    * **PrestigeBFT**：一种基于声誉的方法，实现BFT中的主动视图变更。
        * 声誉机制：将节点行为转化为声誉分数，反映节点正确的可能性。
        * 惩罚：对每个竞选者施加惩罚。
        * 补偿：奖励最新日志复制，奖励过去惩罚没有或只有逐渐增加的节点。
        * 系统根据声誉得分选择领导者，声誉越高，成为新领导者的机会越大。
        * 性能：在正常操作下（无故障），吞吐量比SBFT、HotStuff、Prosecutor高出约5.4倍。在节点数量增加时，性能优于HotStuff。在静默参与者和含糊其辞攻击下，吞吐量有弹性。
        * 优点：第一个主动视图变更协议，能有效抑制恶意服务器。
* **动态成员资格变更**：
    * **问题**：BFT共识算法通常假设静态的节点集合，而V2X网络（车辆来去、在线/离线）无法保证环境稳定。中心化数据处理导致数据垄断，损害数据完整性。
    * **V-Guard**：应对动态成员变化的DL设计。
        * 将配置和交易绑定，引入“booth”（描述符，指定参与车辆成员配置的集合）。
        * V-Guard框架将排序与共识分离，可以发生在不同的booth中。
        * Gossip协议用于进一步传播已提交的事务。
        * 性能：在静态排序和共识方面，V-Guard的峰值吞吐量比HotStuff高22倍，比ResilientDB高9.5倍，比Narwhal高1.8倍。在成员动态变化下，吞吐量和延迟表现良好。
        * 优点：快速、动态（适用于不稳定网络、间歇性连接）、多功能。

## **关于BFT共识算法的全面回顾（调查报告）**

1.  **引言**：

* BFT共识算法在区块链应用中广泛部署，提供去中心化信任。
* 文章旨在通过新的分类法（更高效、更鲁棒、更可用）对现有BFT算法进行系统性调查，并提供详细的协议描述、优缺点以及消息和时间复杂性对比。

2.  **背景**：

* **状态机复制 (SMR)**：共识算法确保多台状态机协调运行，即使部分机器故障也能提供统一视图。
* **拜占庭故障**：故障服务器可表现任意恶意行为，与良性故障不同。
* **拜占庭法定人数**：为容忍 $f$ 个故障节点，通常需要 $2f+1$ 的法定人数。
* **网络假设**：同步、异步、部分同步网络。
* **复杂性度量**：消息复杂性（发送消息总数）和时间复杂性（消息传递轮数）。
* **服务属性**：终止、协议、有效性（或安全性和活性）。

3.  **更高效的BFT共识**：

* **PBFT**：现代BFT共识算法的基础。
    * **系统模型与服务属性**：容忍 $f$ 个故障副本 ($n=3f+1$)。安全性在异步网络中，活性需要有界消息延迟的同步性。
    * **复制协议**：三阶段提交协议（预准备-准备-提交），客户端等待 $f+1$ 条回复。
    * **视图变更**：当主节点失败时，启动视图变更协议选择新主节点。
    * **优缺点**：开创性贡献，但二次消息复杂性 $O(n^2)$ 限制其扩展性。
* **SBFT**：
    * **系统模型与服务属性**：容忍 $f$ 个拜占庭服务器和 $c$ 个崩溃/滞后服务器 ($3f+2c+1$)。使用门限签名实现线性消息复杂性 $O(n)$。
    * **复制协议**：快速路径 (无故障) 和线性PBFT (有故障)。
    * **视图变更**：$O(n^2)$ 消息复杂性。
    * **优缺点**：线性消息传输，客户端通信 $O(1)$。但故障客户端可能触发不必要视图变更。
* **HotStuff**：
    * **系统模型与服务属性**：容忍 $f$ 个拜占庭服务器 ($3f+1$)。部分同步网络下保证活性。乐观响应性。每个共识实例轮换主节点。
    * **复制协议**：四阶段协议 (准备-预提交-提交-决定)，使用QC (法定人数证书)。
    * **视图变更**：频繁轮换领导者。
    * **优缺点**：线性消息传输，支持流水线化。但频繁领导者轮换在故障时性能下降。
* **ISS**：
    * **系统模型与服务属性**：多领导者SMR框架。将工作负载分配给多个领导者，并行运行SB实例。容忍 $f$ 个拜占庭故障节点 ($3f+1$)。
    * **复制协议**：日志分纪元和段，领导者负责各自段。并行运行SB实例。
    * **多领导者选择**：基于领导者选择策略，结合BFTMencius和故障检测器。
    * **优缺点**：显著提高吞吐量，更快客户端响应。但增加共识延迟，故障时SB实例失败概率高。
* **DAG-Rider**：
    * **系统模型与服务属性**：异步BAB协议，最优时间/消息复杂性。两层架构：结构化DAG用于可靠消息传播，零开销共识协议确定总顺序。
    * **DAG流水线**：节点维护DAG，包含强边和弱边。通过BAB协议保证DAG最终一致。
    * **DAG中共识**：使用完美硬币机制独立决定区块顺序。
    * **优缺点**：高吞吐量（并行流水线），但高延迟。
* **Narwhal and Tusk**：
    * **系统模型与服务属性**：基于DAG的内存池，分离事务传播和排序。
    * **DAG复制协议**：类似DAG-Rider，但使用更高效的可靠广播。
    * **优缺点**：经验上吞吐量有优势，但由于内存池不维护顺序，事务共识延迟高。

4.  **更鲁棒的BFT共识**：

* **Aardvark**：
    * **系统模型与服务属性**：改善高效BFT算法在“不友好执行”下的鲁棒性。
    * **鲁棒性改进**：更强的消息认证（签名客户端请求）、独立通信（资源隔离）、自适应领导者轮换（定期视图变更）。
    * **优缺点**：在故障客户端场景下更鲁棒，但对主节点性能期望过严可能导致不必要视图变更。
* **Pompe**：
    * **系统模型与服务属性**：排序协议，构建在标准共识算法之上。引入“拜占庭有序共识”，防止领导者操纵命令顺序。
    * **复制协议**：排序阶段（民主决定顺序）和共识阶段（周期性提交批次命令）。
    * **优缺点**：引入操作排序公平性，但未设计特定共识算法，安全性和活性与底层算法相关。
* **Spin**：
    * **系统模型与服务属性**：解决故障领导者导致的性能下降。每请求轮换主节点，使用黑名单排除故障副本。
    * **鲁棒性改进**：领导者轮换和合并操作。
    * **优缺点**：在主节点攻击下更鲁棒，但无故障时引入额外消息开销。
* **Prosecutor**：
    * **系统模型与服务属性**：允许服务器主动竞选主节点，对故障行为施加计算惩罚。
    * **复制协议**：O(n) 消息复杂性，使用门限签名。
    * **视图变更**：与计算惩罚关联，故障服务器需要执行指数级增长的计算工作。
    * **优缺点**：惩罚恶意服务器，但计算能力强的故障服务器可能导致长时间无正确领导者。
* **RBFT**：
    * **系统模型与服务属性**：通过并行执行多个PBFT实例来增加冗余，监控主实例性能。
    * **鲁棒性改进**：多实例并发运行，监控主实例速度和公平性。
    * **优缺点**：解决主节点单点故障问题，但引入大量额外消息开销 O(|M|(n^3+n^2+n))。

5.  **更可用的BFT共识**：

* **基本模型**：
    * **可靠广播 (Bracha's RBC)**：异步网络中的协议。
    * **二元拜占庭协议 (BA)**：异步网络中的多轮共识。
* **DBFT**：
    * **系统模型与服务属性**：无领导者BFT，部分同步网络。结合RBC和Psync（带弱协调器的BA变体）。
    * **Psync**：BA协议的修改版，增加超时、弱协调器和终止条件。
    * **优缺点**：改进BA，但仍需部分同步网络。
* **HoneyBadgerBFT**：
    * **系统模型与服务属性**：无领导者BFT，异步网络。使用门限加密防御审查攻击。
    * **高效大消息可靠广播**：RBC中使用擦除编码，降低消息复杂性。
    * **带加密共同硬币的BA**：更安全的硬币翻转和终止条件。
    * **异步共同子集 (ACS)**：核心构建块，并行运行RBC和BA实例。
    * **优缺点**：异步网络下的高吞吐量实用解决方案，但延迟较高。
* **BEAT**：
    * **系统模型与服务属性**：五种无领导者异步BFT协议 (BEAT0-BEAT4)。
    * **BEAT0**：带标签门限加密，TDH2，更高效的擦除编码。
    * **BEAT1 & BEAT2**：使用原始Bracha的RBC降低延迟。BEAT2将加密移到客户端，并使用匿名通信。
    * **BEAT3**：使用AVID-FP，进一步降低带宽使用。
    * **BEAT4**：使用AVID-FP-Pyramid（金字塔码）降低数据重构成本，尤其适用于部分数据读取。
    * **优缺点**：全面提升性能，BEAT3/4更适合BFT存储服务，但在某些情况下有更高延迟。

6.  **未来研究方向**：

* **可扩展性**：在保持高吞吐量和低延迟的同时，扩展到数千个节点。
* **排序公平性**：防止领导者操纵交易顺序（如抢跑），确保系统公正透明。
* **量子安全BFT共识**：应对量子计算对传统密码学的威胁。
* **互操作性**：实现不同BFT区块链和分布式系统之间的跨链共识和数据/资产转移。
* **机器学习中的BFT共识**：确保分布式训练中数据和模型更新的完整性，以及多智能体学习中的鲁棒性。

## 以太坊 (Ethereum)

以太坊是一个**去中心化的、全球共享的计算平台**，能够运行各种应用程序，且一旦部署就无法被关闭或审查。其核心创新在于能够运行**智能合约**。

### **诞生与发展**：

由 Vitalik Buterin 在 2013 年提出，于 2015 年上线。2022 年 9 月，“The Merge”（合并）升级将其共识机制从**工作量证明 (Proof-of-Work, PoW)** 转换到了**权益证明 (Proof-of-Stake, PoS)**。

### **以太币 (Ether, ETH)**：

* **燃料 (Gas)**：作为以太坊网络的**原生加密货币**，主要用于支付网络操作（发送 ETH、执行智能合约、部署合约等）所需的费用，并以此激励**验证者 (Validators)**。
* **价值储存和交换媒介**：ETH 也是一种有价值的数字资产。

### **智能合约 (Smart Contracts)**：

* 存储在区块链上的**计算机程序**，按照预设规则自动执行，无需第三方干预。
* **图灵完备**：其智能合约语言 **Solidity** 是图灵完备的，可实现任何复杂逻辑。
* **不可篡改与透明**：部署后代码无法篡改，公开透明。

### **以太坊虚拟机 (Ethereum Virtual Machine, EVM)**：

* **运行环境**：智能合约的运行时环境，每次合约执行都在 EVM 中。
* **沙盒环境**：隔离合约执行，确保错误不影响网络。

### **区块链**：

* **分布式账本**：去中心化、不可篡改的分布式账本，记录所有交易和合约执行。
* **共识机制**：
    * **PoW (旧机制)**：矿工通过解决数学难题竞争打包区块。
    * **PoS (新机制)**：验证者通过**质押 32 ETH** 获得验证区块的权利，并获得新发行的 ETH 奖励。不诚实行为可能导致 ETH 被“罚没 (Slashing)”。

### **应用场景**：去中心化金融 (DeFi)、非同质化代币 (NFTs)、游戏 (GameFi)、去中心化自治组织 (DAOs)、元宇宙 (Metaverse) 等。

### **挑战与未来**：

* **可扩展性**：通过 Layer 2 解决方案（如 Arbitrum、Optimism）和未来分片 (Sharding) 升级来解决。
* **EIP-1559**：升级后交易费用包含被销毁的“基本费用”和给验证者的“优先费用”，有助于 ETH 的通缩。

## Gas

Gas 在区块链中是执行操作所需的**“燃料”或“计算力成本”**。

### **目的**：

* **支付给验证者/矿工的报酬**：激励他们维护网络。
* **防止网络滥用/垃圾信息**：增加攻击成本。
* **衡量计算复杂性**：不同操作消耗不同 Gas 单位。

### **工作原理**：Gas 本身是计价单位，最终用 ETH 支付。

* **Gas 单位 (Gas Units)**：每种操作的固定成本，例如简单 ETH 转账为 21,000 Gas 单位。
* **Gas 价格 (Gas Price)**：你愿意为每 Gas 单位支付的 ETH 数量，通常以 **Gwei** ($1 \text{ Gwei} = 10^{-9} \text{ ETH}$) 为单位，价格动态变化。
* **Gas 限制 (Gas Limit)**：你为交易支付的最大 Gas 单位数量，用于防止无限循环。

### **Gas 费用计算**：

总 Gas 费用 = Gas 单位 (实际消耗量) $\times$ Gas 价格。

### **EIP-1559 变化**：

* **基本费用 (Base Fee)**：由网络动态计算并**销毁 (burned)**，不进入验证者手中，有助于限制 ETH 供应量。
* **优先费用 (Priority Fee / Tip)**：给验证者的“小费”，激励优先处理交易。
* 销毁的 ETH 并非去了任何可访问的地址，而是发送到一个**无法访问的地址**，永久从流通中移除。

## Hardhat

Hardhat 是一个**以太坊开发环境**，帮助开发者构建、测试和部署智能合约及去中心化应用 (dApps)。

### **主要功能**：

* **本地以太坊网络 (Hardhat Network)**：内置私有区块链，用于快速迭代和调试。
* **合约编译**：将 Solidity 代码编译成 EVM 字节码和 ABI。
* **合约部署**：自动化部署智能合约到各种网络。
* **自动化测试**：集成 JavaScript 测试框架（Mocha, Chai），编写合约测试。
* **插件系统**：提供大量插件扩展功能（如与 Ethers.js 集成、Gas 报告）。
* **任务运行器**：定义和运行自定义任务，自动化开发流程。

## IPFS (InterPlanetary File System)

IPFS 是一个**去中心化、点对点 (P2P) 的分布式文件存储和共享网络**。

### **解决问题**：

* **中心化和单点故障**：HTTP 依赖中心服务器，易受攻击和审查。
* **效率低下**：请求需到特定服务器，速度慢。
* **内容重复存储**：浪费资源。

### **工作原理**：

* **内容寻址 (Content Addressing)**：文件通过其内容的加密哈希值（**内容标识符，CID**）来标识，而非位置。CID 具有唯一性、不变性和内容校验功能。
* **点对点网络 (P2P)**：网络中的每个参与者都是一个节点，既是客户端也是服务器。
* **分布式哈希表 (DHT)**：用于查找哪个节点拥有特定 CID 对应的文件。
* **文件持久性 (Pinning)**：通过“钉住”文件来确保其长期可用性，通常需要支付存储费用（如通过 Filecoin）。

### **优势**：

去中心化、抗审查、高可用性、高效、版本控制、成本效益、Web3 基础。

### **局限性**：

数据持久性需额外保障、实时性挑战、难以移除非法内容、隐私问题、入门门槛。

### **与区块链的关系**：

互补。区块链存储小而重要的安全数据（如 CID），IPFS 存储大文件，共同构建高效的去中心化应用。

## Remix (Web 框架)

Remix 是一个**全栈的 Web 框架**，利用现代 Web 标准来构建高性能、高用户体验的应用程序。

### **主要用途**：

构建快速、流畅且具有弹性的 Web 应用程序。

### **特点**：

* **服务器端渲染 (SSR)**：加快页面初始加载速度，利于用户体验和 SEO。
* **简化数据加载和表单提交**：在路由中定义数据加载器（`loader`）和操作（`action`），在服务器上运行。
* **利用 Web 标准**：基于 Web Fetch API、HTTP 缓存和 HTML 表单等。
* **优化用户体验 (UX)**：嵌套路由、错误边界、渐进式增强。
* **与 Remix - Ethereum IDE 的区别**：Remix IDE 是一个用于以太坊智能合约开发的**在线 IDE**，通常用 JavaScript/TypeScript 构建，**与 Remix Web 框架是两个完全不同的概念**。

## Solana

Solana 是一个**高性能的区块链平台**，旨在解决传统区块链在**速度、可扩展性和成本**方面的挑战。

### **核心目标**：

在不牺牲去中心化和安全性的前提下，大幅提高可扩展性。

### **主要创新技术**：

* **历史证明 (Proof of History, PoH)**：核心时间戳技术，允许验证者对交易顺序和时间进行加密证明，提升效率。
* **塔式拜占庭容错 (Tower BFT)**：基于 PoH 的权益证明 (PoS) 共识机制，快速达成共识。
* **管道化 (Pipelining)**：将交易处理阶段分配给不同硬件，提高并发性。
* **海平面 (Sealevel)**：并行智能合约运行时环境，允许合约并发执行。
* **涡轮 (Turbine)**：区块传播协议，分片传播区块，降低延迟。
* **云裂 (Cloudbreak)**：横向扩展的账户数据库，支持高并发读写。
* **海湾流 (Gulf Stream)**：无内存池的交易转发协议，优化确认时间。

### **SOL (原生代币)**：

用于交易费用、质押和治理。

### **优势**：

极高的吞吐量和低延迟（每秒数万次交易）、低交易费用、活跃的生态系统、单链架构。

### **挑战**：

去中心化程度的权衡（节点硬件要求高）、网络稳定性问题、对 Rust 开发者友好度（学习成本）。

### **现实世界问题及解决方案示例**：

解决**大规模微支付**问题，例如在流媒体/游戏或物联网设备网络中，利用 Solana 的高吞吐量、低费用和快速最终性，实现每秒数万笔的自动化微支付交易，并用智能合约自动化分成和状态更新。

## Polygon

Polygon 是一个**以太坊扩容解决方案**和**多链生态系统**，旨在解决以太坊高交易费用、低速度和可扩展性不足的问题，同时保持以太坊的安全性、去中心化和兼容性。

### **解决问题**：

通过提供一系列扩容解决方案，如 PoS 侧链和 ZK Rollups，来提高以太坊的吞吐量并降低交易成本。

### **核心技术和组件**：

* **Polygon PoS 链 (Matic PoS Chain)**：最广泛使用的组件，是一个**权益证明 (PoS) 侧链**。它在链上处理交易，定期将验证状态提交到以太坊主网，安全性锚定以太坊。具有高吞吐量（最高可达 65,000 TPS）、极低费用和 EVM 兼容性。
* **Polygon ZK Rollups (如 Polygon zkEVM)**：重要发展方向，通过**零知识证明 (Zero-Knowledge Proofs)** 将大量交易在链下打包并生成证明提交到以太坊主网，继承以太坊安全性，实现更高扩展性和 EVM 等效性。
* **Polygon Supernets (现在也称为 Polygon Chain Development Kit - CDK)**：模块化框架，允许开发者构建自己的定制化区块链网络（应用专用链），可高度定制、具有主权性并与以太坊互操作。

### **MATIC 代币 (现在升级为 POL)**：

Polygon 网络的**原生代币**。用于质押、交易费用和治理。POL 代币旨在实现更灵活的多链质押。

### **架构层次**：

通常包括以太坊层、安全层、Polygon 网络层和执行层。

### **优势**：

解决以太坊痛点、EVM 兼容性、多样化的扩容方案、强大的生态系统。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Overview-of-Polygon-Ibrahim </div>
<div class="file-meta"> 1,503 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Overview-of-Polygon-Ibrahim.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Solana Resources </div>
<div class="file-meta"> 98 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/Solana Resources.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> STCA Solana Deck UBC </div>
<div class="file-meta"> 18,059 KB / 2025-07-16</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/STCA Solana Deck UBC.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 6

## **去中心化身份（Decentralized Identity, DI）简介**

1.  **为什么需要数字身份？**

* 漫画“在互联网上，没人知道你是一条狗”形象说明了数字世界中身份真实性验证的挑战。
* 去中心化身份提供了一种在数字世界中建立身份及其属性真实性的方法。

2.  **身份是多维的**

* **关系**：你对鲍勃（姐妹）、你对Acme（雇主）、你对美国（访客）等。
* **代理（Agent）**：帮你做事，如云代理、iPad/笔记本、手机。
* **属性**：出生日期、教育、健康等。

## **去中心化身份堆栈**

### **Trust over IP（ToIP）框架**：

将信任分为人类信任和技术信任，并分别对应治理和技术堆栈的四个层次。

* **技术信任（Technical Trust）**：
    * **Layer 1 (公共设施层)**：DID方法，基于各种去中心化记录技术，如区块链、分布式账本、去中心化文件系统。DID（去中心化标识符）是唯一的标识符，可被个人拥有和控制，通过公钥基础设施控制，可记录在可验证数据注册表（如区块链）上，并可解析为DID文档。
    * **Layer 2 (点对点协议层)**：DIDComm点对点协议，用于代理/钱包之间通过对等DID建立连接和交换数据。数据钱包可以互操作，无需中介即可交换对等DID和公钥。
    * **Layer 3 (数据交换协议层)**：可验证凭证（Verifiable Credential），用于发行方、持有方、验证方之间交换可验证凭证和证明。发行方颁发凭证，持有方持有凭证，验证方验证凭证证明。
    * **Layer 4 (应用生态系统层)**：数字信任生态系统，最终用户应用层。
* **人类信任（Human Trust）**：
    * **Layer 1 (公共设施治理框架)**：交易发起方、交易背书方、管家。
    * **Layer 2 (提供者治理框架)**：硬件提供者、软件提供者、代理。
    * **Layer 3 (凭证治理框架)**：凭证注册表、权威发行方、保险公司。
    * **Layer 4 (生态系统治理框架)**：成员目录、审计师、审计师认证机构。
* **治理当局**（Governance Authority）在每个层面发布（Publishes）治理框架（Governance Framework），以建立信任。

## **去中心化身份工作原理**

### **可验证凭证信任三角**：

* **发行方（Issuer）**：创建并签署可验证凭证。
* **持有方（Holder）**：接收、存储和管理凭证。
* **验证方（Verifier）**：从持有方接收凭证证明，并验证其真实性。
* **公钥**和**加密元数据**：由DID（去中心化标识符）和区块链（可验证数据注册表）支持。
* **关键在于“无需集成”**：发行方和验证方之间不需要直接信任或事先集成，信任通过共享的区块链注册表和密码学建立。

### **医生护照示例**：

1.  **英国NHS（发行方）**：向医生**写入**其DID（去中心化标识符）到**Sovrin区块链**。
2.  **英国NHS（发行方）**：签署**医生护照**可验证凭证并颁发给医生（持有方）。
3.  **医生（持有方）**：创建其医生执照的**证明**。
4.  **医院（验证方）**：**读取**医生的DID（从Sovrin区块链获取公钥）。
5.  **医院（验证方）**：从医生（持有方）处接收执照证明，并**验证**该证明。

## **可验证凭证类型（Infographic）**

* **VC是标准化数据模型**，具有广泛的表达能力。
* **VC是W3C标准化的**，目标是确保长期增长。
* **三种主要凭证格式**：

1.  **JSON-JWT**：

* **简洁性**：所有格式中最简单。
* **隐私保护**：否。
* **选择性披露**：否。
* **零知识证明**：否。
* **持久性**：需要解析持久标识符。
* **语义消歧**：否。
* **实现**：JWS（JSON Web Signature）在JWT中，整个凭证由关联公钥对的私钥签署。

2.  **JSON-LD with LD Signature**：

* **简洁性**：相对复杂。
* **隐私保护**：是。
* **选择性披露**：是。
* **零知识证明**：否。
* **持久性**：需要解析持久标识符。
* **语义消歧**：是。
* **实现**：整个凭证由发行方使用关联公钥对的私钥签署。持有方可选择性披露凭证中的部分属性。

3.  **ZKP-CL (Zero-Knowledge Proof - Camenisch-Lysyanskaya)**：

* **简洁性**：所有格式中最复杂。
* **隐私保护**：是。
* **选择性披露**：是。
* **零知识证明**：是。
* **持久性**：不需要解析持久标识符。
* **语义消歧**：是。
* **实现**：CL签名由发行方签署，与关联公钥对的私钥相关联。持有方仅展示验证所需的属性，并通过加密证明（零知识证明）完成验证。

4.  **JSON-LD ZKP with BBS+**：

* **简洁性**：复杂。
* **隐私保护**：是。
* **选择性披露**：是。
* **零知识证明**：是（但尚未实现）。
* **持久性**：不需要解析持久标识符。
* **语义消歧**：是。
* **实现**：BBS+签名由发行方签署，与关联公钥对的私钥相关联。持有方仅展示验证所需的属性，验证方可选择不包含凭证中所有数据。

## **NFT与VC的比较**

| 特征           | NFT (非同质化代币)     | VC (可验证凭证)       | SBT (灵魂绑定代币) |
| :--------------: | :----------------------: | :---------------------: | :-------------------: |
| **是什么？** | 公开展示的数字权利     | 私有持有的数字事实    |                     |
| **驱动价值** | 稀缺性                 | 是                    | 否                  |
| **可转移性** | 是                     | 否                    | 否 (永久绑定)        |
| **平台特定** | 是                     | 否                    |                     |
| **实现方式** | 仅在区块链上实现       | 可在区块链或无区块链实现 |                     |
| **用途** |                        | 证明资质、身份、凭证  | 表示个人、不可转移的属性和声誉 |
| **验证** |                        | 通过密码学证明验证    | 存在于区块链上，可见的唯一属性 |
| **隐私** |                        | 可选择性披露信息给验证方 | 在区块链上公开可见，隐私性可能较低 |

## **去中心化身份堆栈的详细技术**

1.  **Layer 1 (公共设施层)**：

* **DIDs**：根据DID方法创建，针对不同的凭证类型进行优化。
* **Utility**：可使用多种去中心化记录技术，如区块链、分布式账本、去中心化文件系统。
* **互操作性**：不同DID方法和底层技术之间可以互操作。

2.  **Hyperledger Indy**：

* 一个用于去中心化身份的许可型账本（Permissioned Ledger）。
* 没有原生加密货币或代币。
* 采用**Plenum共识协议**（BFT协议的变体，可容忍超过1/3的腐败节点）。
* 可处理高交易量。
* 不变性保证取决于谁控制账本节点（单一实体或去中心化实体）。
* 点对点交易不存储在账本中。
* **每个节点运行四种类型的账本**：
    * **审计账本（Audit Ledger）**：跨账本排序。
    * **池账本（Pool Ledger）**：用于添加、编辑、移除节点。包含池中每个节点的事务。
    * **配置账本（Config Ledger）**：池配置参数，用于事务验证。
    * **域账本（Domain Ledger）**：身份特定事务，应用特定事务。
    * 可通过插件添加新账本。
* **架构概述 - 共识**：
    * **Indy-Plenum**：共识协议。
    * **Indy-Node**：依赖indy-plenum，处理身份特定事务（如GET SCHEMA请求、GET CRED DEF请求）。
* **密码学概述**：
    * **账本**：Merkle Tree（账本）、Patricia Merkle Trie（状态）。
    * **节点到节点通信**：ZMQ (libsodium) 作为安全传输，CurveCP握手，认证加密（Poly1305 MAC），对称密钥加密（XSalsa20），公钥加密（Curve25519）。没有数字签名。使用BLS多重签名签署Merkle根。
    * **客户端到节点通信**：Ed25519数字签名。

3.  **Layer 2 & 3 (DIDComm & 数据交换)**：

* **Ceremony**：钱包到钱包连接的建立和保持，直到一方选择退出。
* **Exchange**：数据钱包互操作，无需中介即可交换对等DID和公钥。
* **Issue**：可验证凭证颁发给持有方。
* **Verify**：验证方检查凭证证明。
* **Index**：发行方的公钥被索引以供验证方访问。
* **Lookup**：验证方检索公钥。
* **Trust**：发行方和验证方之间无需集成。

## **案例研究**

1.  **用例示例1：访问法院服务**

* **问题**：法律专业人员需要安全高效地访问法院服务。
* **解决方案**：不列颠哥伦比亚省律师协会与BC省政府数字信任与身份计划合作，建立数字信任的三大支柱。
    * 律师协会向律师颁发**会员卡数字凭证**，证明其良好执业资格。
    * 同时向律师颁发基于BC Services Card信息的**个人凭证**。
    * 两种数字凭证均集成到BC Wallet（用户友好、安全的数字钱包智能手机应用）中。
    * 律师使用数字凭证和BC Wallet快速安全地访问法院服务。

2.  **用例示例2：管理健康数据交换的同意**

* **问题**：健康研究人员需遵守法律法规，验证个人身份、提供数据共享同意证明（何种数据？何种用途？多长时间？）、保留可审计的同意证据。合规性可能减缓健康创新。
* **解决方案**：健康智能公司Molecular You和不列颠哥伦比亚大学的Blockchain@UBC开发了使用可验证凭证管理细粒度、动态同意的解决方案。

3.  **用例示例3：可持续采矿证明**

* **问题**：加拿大采矿协会（MAC）的可持续采矿（TSM）计划评估采矿公司在生物多样性承诺、水资源管理、健康安全等方面的表现。公司需每年报告进展。
* **解决方案**：MAC与能源与矿产数字信任（Energy & Mines Digital Trust）合作，探索采矿运营商使用数字凭证提交TSM分数，安全高效地满足会员要求。矿山可以继续使用数字凭证向客户和投资者分享其ESG（环境、社会、治理）表现。

## **问题与挑战**

1.  **QR码安全性**：

* **观察**：QR码不安全，易受中间人攻击。
* **建议**：始终使用DIDComm（它对消息进行签名，确保通信不被拦截和伪造）或其他安全通信形式进行凭证交换。

2.  **凭证发行方的权限能力**：

* **观察**：演示中未包含凭证是否由合格机构颁发的检查。
* **建议**：需要建立治理框架，确保后续验证检查凭证是否由合格机构数字签名（可通过区块链查询其VerKey）。

3.  **对治理机构的社会信任**：

* **观察**：个人可能不信任凭证发行机构（如政府）。例如，萨斯喀彻温省政府停止推行潜在数字身份，主要担忧是隐私问题，即使政府承诺不是强制性的。
* **建议**：需要建立治理框架，包含保障措施和限制，以避免权力滥用/人权侵犯/弱势群体被排斥。

4.  **加拿大去中心化身份的进展**：

* 2020年8月：加拿大财政委员会秘书处宣布正在为加拿大制定数字身份系统。
* 2023年：加拿大财政委员会秘书处成立数字身份工作组。
* 2024年2月：加拿大政府发布“数字凭证发行和验证（IVDC）”RFI。
* 2024年10月：特鲁多表示自由党“反对”加拿大数字身份。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> DecentralizedIdentityIntroduction </div>
<div class="file-meta"> 3,955 KB / 2025-07-17</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/DecentralizedIdentityIntroduction.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 7

## **Mines Digital Trust (MDT) 概述**

1.  **定义**：Mines Digital Trust (MDT) 是不列颠哥伦比亚省政府、采矿运营商、行业协会、绩效认证机构和技术提供商之间的合作项目。
2.  **项目驱动因素**：

* 消费者、投资者和监管机构对负责任采购产品的需求不断增长。
* 对卑诗省有能力供应的关键矿产的需求不断增长。
* 卑诗省在身份验证先进技术方面的世界领先地位。

3.  **数字凭证 (Digital Credentials)**：

* 日常凭证的数字版本，如教育证书、许可证、执照和注册。
* 不需要区块链进行数据交换。
* **发布示例**：

    * 卑诗省采矿运营商 **发布** 数字产品护照。
    * 卑诗省政府 **发布** 卑诗省矿业许可证状态证明数字凭证。
    * 加拿大采矿协会 (MAC) **发布** 可持续采矿数字凭证。
    * Copper Mark **发布** Copper Mark数字凭证。

4.  **测试完成情况**：

* 参与方包括：获得认证的TSM审计师 (PwC, Envirochem)、卑诗省注册服务机构、数字信任服务提供商 (Northern Block, Neoflow, Spherity)、矿业/关键矿产部、行业协会 (加拿大采矿协会)、卑诗省采矿公司 (Teck, Hudbay)、卑诗省政府公共目录 (OrgBook BC)、ESG投资公司 (La Mancha)、金属和矿产市场 (LME, HKEX Company)、美国海关和边境保护局。

## **UN Transparency Protocol (UNTP)**

1.  **项目动机**：

* 世界面临可持续发展挑战。
* 监管机构和市场正在做出回应，这为可持续行为提供了有意义的激励。
* 这些激励措施也鼓励了更多的“漂绿”行为。
* 为了保持激励的价值，需要通过透明度来打击“漂绿”——以数字化允许的规模。
* 实现供应链大规模透明度存在许多挑战，因此催生了UNTP。

2.  **协议而非平台**：

* UNTP是一种数字标准，而不是一种技术或平台。
* 如果拥有产品ID，就可以获取数据，并且人类和机器都可以读取。
* **挑战与解决方案**：

    * **许多可追溯性平台**：选择符合UNTP的平台。
    * **商业激励不足**：产品护照作为差异化价值的捆绑。
    * **供应链尽职调查义务**：通过合格凭证提供可验证的符合性证据。
    * **商业机密**：隐私工具，包括选择性编辑。
    * **数字成熟度和采用不均**：实现无需系统间依赖。
    * **与现有标识符的兼容性**：利用现有标识符和链接解析器。
    * **ESG标准混乱**：可扩展的语义映射架构。
    * **身份、假冒、质量平衡欺诈**：信任图和信任锚。

3.  **UNTP的构成**：

* **可追溯性（Traceability）**：数字可追溯性事件（产品ID、批次ID、位置ID、可追溯性事件：检查、包装、运输、制造）。
* **透明度（Transparency）**：数字产品护照（组织、设施数据、产品信息、来源数据、可持续性声明、ESG指标值、物料/批次数据、可追溯性事件）。
* **信任（Trust）**：数字合规性凭证（认证、方案或法规、符合性声明、评估机构、符合性评估、产品/设施、标准/指标、评估值）。
* 这些模块通过“跟随链接”相互关联。

## **UNTP/CRM - 整个价值链视角**

**关键矿产价值链**：

* 示例展示了从采矿到最终产品（如汽车电池、新旧车辆）的完整价值链，以及相关的合规性、运输、销售等环节。
* **参与实体**：权威机构、锂矿、铜矿、加工厂、电池制造商、汽车制造商、消费者、回收商。
* **数字凭证和事件**：原产地保证、采矿许可证、销售事件、矿物护照、加工事件、产品护照、生产事件、环境产品声明（EPD）、电池护照、CBAM关税（碳边境调节机制）、材料护照。
* **数据流**：B2B尽职调查、G2B评估、消费者选择。
* 数字凭证可以相互链接，使价值链透明化，就像拉动一串相互连接的数据的末端。

## **UNTP扩展方法论**

1.  **跨行业可重用核心**：

* UNTP提供了一个跨行业可重用的“核心”。
* 各行业可以在此基础上创建不破坏兼容性的扩展，以满足自身需求，同时保持跨行业互操作性。

2.  **扩展示例**：

* **UN Governance (UNTP)** **扩展到**：
    * 纺织品透明协议 → 纺织品DPP。
    * 农业透明协议 → 农业DPP。
    * 关键原材料透明协议 → 原材料DPP。
    * 国家透明协议（国家X）→ 国家X DPP。
* 这些行业和国家治理协议**实施**各自的数字产品护照（DPP），并通过“互操作”连接。

## **UNTP的扩展承诺**

1.  **电子和汽车零部件**：

* 负责任商业联盟（RBA）成员和倡议包括全球主要汽车和电子产品供应商。
* 他们的年收入超过8万亿美元，产品销往120多个国家。

2.  **全球建筑环境**：

* 通用数据协议（UDP）是UNTP的扩展。
* 旨在利用其去中心化框架，在**全球建筑环境**中提供透明、可信和可验证的数据。

3.  **澳大利亚农业**：

* Food Agility Operating作为一个治理框架，通过UNTP的这种适应性，促进了多个认证机构、农场系统和企业系统之间的互动。

4.  **关键原材料和纺织品**：

* 与联合国可持续发展目标（SDGs）保持一致。
* 基于UNECE纺织品和皮革可追溯性项目的成功经验。
* 这些扩展旨在为行业提供实用的成本工具，用于数字数据交换。

5.  **价值链图谱**：展示了电子和汽车行业的锡/钽/钴、铜、稀土、皮革等价值链，涵盖从初级生产到回收/再制造的各个环节。

* **数据类型**：数字产品护照 (DPP)、数字设施记录 (DFR)、数字可追溯性事件 (DTE)、数字合规性凭证 (DOC)、数字身份锚 (DIA)。
* **实体类型**：生产/制造设施、散装材料（交易）、产品（交易）。
* 尽管看起来复杂，但存在简单的重复模式：**权威机构**通过**数字设施记录**描述**生产/制造设施**，由**数字身份锚**认证/许可；**生产/制造设施**生产**产品或材料**；**产品或材料**通过**数字可追溯性事件**被**追踪**；**产品或材料**从**源头**制造。

## **下一步计划**

1.  继续与国际铜业协会合作，完善UN透明协议草案并创建铜扩展。
2.  与负责任商业联盟和全球电池联盟合作，推进UNECE与采矿运营商、冶炼厂和下游制造商之间的铜供应链试点项目。
3.  与国际伙伴合作，实现标准（如Catena-X和ISO/IEC）的互操作性和相互认可。

## **时间线**

* **2023年7月**：UNECE建议49（草案政策）。
* **2024年7月**：UNECE建议49（公众审查与同意）。
* **2024年9月**：UNTP规范（发现v0.1 + PoCs）。
* **2025年1月**：UNTP规范（Alpha v0.5 + 试点）。
* **2025年7月**：UNTP规范（Beta v1.0 规模化）。
* **2025年11月**：UNECE建议49（采纳和实施承诺）。
* **关键矿产扩展（铜、锂、钴、铝）**：UN/CEFACT CRM项目 - 阶段1 → BC铜概念验证 → UNECE铜试点。
* **负责任商业联盟（RBA） - 电子和汽车零部件**：RBA电子和汽车零部件试点。
* **全球电池联盟**：全球电池联盟试点。

## **联系方式**

* Nancy Norris, Chair, Ministry of Mining and Critical Minerals, British Columbia.
* 邮箱：Nancy.Norris@gov.bc.ca

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> UBC_UNTP-CRM_MDT_July2025 </div>
<div class="file-meta"> 2,624 KB / 2025-07-17</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/UBC_UNTP-CRM_MDT_July2025.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---

# block chain DAY 8

## **区块链治理：概念、挑战和启示**

1.  **讲座目标**

* 了解“治理”一词的历史和起源。
* 识别区块链系统中的关键问题。
* 调查区块链治理研究的演变。
* 研究并实践一些区块链治理模型（对blockathon项目有帮助）。

## **什么是治理(governance)？**

1.  **治理与政府**

* 许多人认为“治理”是组织的一种范式转变，一个关键概念。
* 有些人认为“治理”仅仅是行话，一个模糊而难以捉摸的概念。
* 许多人混淆了“治理”和“政府”。

2.  **“治理”的起源与发展**

* 英文单词“governance”源于拉丁语“gubergare”和希腊语“kybernan”，意为“掌舵”。治理是管理的过程。
* **1980年代**：“治理”引起学术界兴趣。
    * 关键里程碑：威廉姆森的《交易成本经济学：契约关系的治理》（1979）。
    * 法律和经济学界对公司治理的兴趣日益增长。
* **1990年代**：“治理”变得无处不在，成为一个流行概念。
    * 更多社会团体（私人、非政府组织）作为承包商参与政府工作。
* **2010年代**：对“治理”的兴趣进一步加速，超越了其最初的领域（法律、政治学、经济学、公共行政）。
    * 全球问题（环境）的交流日益增多。
    * 国际协调的日益复杂。
    * 先进和重要的创新（区块链、DAO攻击等）。

3.  **定义**

* “治理指所有社会组织和社会协调的过程。”
* “治理是一个关于秩序与无序、效率与合法性的跨学科研究议程，所有这些都在模式和控制混合的背景下进行，这些模式和控制允许在国家内部、通过国家、没有国家以及超越国家的情况下产生碎片化和多维度的秩序。”

4.  **治理与政府的区别**

* 政府是治理大环境中的一个政治机构。
* 政府通过塑造、启用和执行治理过程来参与其所在社会的治理。
* 治理包含政府，但超越政府，涉及其他组织（公司、市场）在社会组织和协调过程中的参与。

5.  **治理的四种视角**

* **作为结构（Governance as Structure）**：规则、法律、法规、司法判决和行政实践的体系。反映了社会科学中的制度主义。
* **作为过程（Governance as Process）**：旨在捕捉多个社会参与者之间的动态互动。不如结构视图稳定，关注持续的“掌舵”过程。
* **作为机制（Governance as Mechanism）**：治理是建立并使决策成为常规。关键考虑因素包括货币化交换、非货币化交换、命令、说服、团结。
* **作为策略（Governance as Strategy）**：治理系统的设计、创建和适应。侧重于权力下放和非正式、创造性系统。

6.  **一些治理类型**

* **公司治理**：平衡董事会、管理层和所有者之间的权力；保护股东和利益相关者的利益。
* **IT治理**：使IT战略与业务目标保持一致；确保技术使用中的问责制、透明度、绩效和合规性。
* **全球治理**：协调国家与全球行动者之间在安全、气候、跨境贸易等全球问题上的国际合作和规则制定。
* **环境治理**：侧重于管理自然资源、执行环境法规，以及平衡发展与可持续性。
* **AI治理、区块链治理**。

## **区块链系统中的关键问题**

1.  **区块链类型**

* 根据“对交易验证的访问”和“对交易的访问”进行分类。
    * **许可型 (Permissioned)**：
        * 公开访问交易：混合区块链。
        * 私有访问交易：私有区块链。
    * **无许可型 (Permissionless)**：
        * 公开访问交易：公共区块链。
        * 私有访问交易：不适用。

2.  **区块链作为社会-信息-技术系统**

* 区块链治理连接了**社会（链下治理）**、**信息（区块链治理）**和**技术（链上治理）**三个方面。

3.  **技术问题：区块链不可能三角 (Blockchain Trilemma)**

* **定义**：区块链技术在安全性、可扩展性和去中心化这三个关键方面之间的权衡。
* **示例**：比特币网络保持1MB的区块大小和10分钟的区块时间，导致每秒处理约7笔交易。
* **讨论**：2017年比特币硬分叉对区块链不可能三角的解决有何影响？

4.  **社会问题：参与度、参与和监管适应**

* 参与决策。
* 应对不确定的监管环境。
* 管理公众情绪（区块链炒作、能源消耗、加密欺诈）。
* 经济激励。
* **区块链采用中的社会-组织障碍**：

1.  对区块链技术的负面刻板印象。
2.  区块链的感知复杂性。
3.  用例行业（本文中指医疗保健）的惰性/难以改变的性质。
4.  缺乏“生态系统”思维。
5.  缺乏成熟的治理框架。

* **示例：加密货币的能源消耗**

    * 比特币每年消耗约150太瓦时的电力，超过阿根廷全国的电力消耗。
    * 产生约65兆吨二氧化碳，相当于希腊的排放量，对全球空气污染和气候变化贡献显著。

* **示例：社会-组织挑战导致TradeLens中断**

    * TradeLens的愿景是成为一个开放、中立的全球供应链数字化平台，实现真实信息共享和协作。
    * 但这种合作和支持未能实现，A.P. Moller-Maersk和IBM宣布停止TradeLens平台。
    * “事实证明，在传统政治体系之外建立一个网络需要大量的政治决策。”

5.  **信息问题：不变性、匿名性、透明度、隐私**

* **数据托管、所有权和访问权**：中心化风险。

    * 谁保管数据（Custody）？
    * 谁拥有数据（Ownership）？
    * 谁控制数据（Access right）？

* **匿名性 vs KYC（了解你的客户）**。
* **合规性 vs 弹性**。
* **透明度 vs 隐私**。
* **区块链 vs GDPR（通用数据保护条例）**。

## **区块链治理**

1.  **区块链治理研究的发展历程**

* **2008年**：比特币白皮书发布。
* **2014年**：区块链社会方面的研究开始出现。区块链治理开始指代通过区块链实现的治理。
* **2016年**：区分“区块链的治理”和“通过区块链的治理”。
* **2017年**：DAO攻击和比特币硬分叉。
* **2019年**：区块链治理研究。
* 即使是“区块链革命”最坚定的支持者也承认，分布式账本增长的最大挑战将是治理。
* 区块链和区块链治理仍然是混淆的来源。

2.  **什么是区块链治理？**

* **区块链的治理**：影响“人”（称为“利益相关者”）的决策过程。
    * 例如：加密项目如何进行更改。
    * 包括：

        * **链上治理（On-chain governance）**：内置于协议中，链上投票。
        * **链下治理（Off-chain governance）**：人工协调和决策，改进提案。

* Vlad Zamfir是一位著名的区块链研究员和软件开发人员，对以太坊网络做出了重大贡献，尤其在权益证明（PoS）共识算法方面。

3.  **区块链治理的关键考虑因素**

* 谁决定更新代码？
* 改进提案如何处理和批准？
* 谁为项目提供资金？
* 谁拥有权力以及拥有多少权力（核心开发者、矿工、代币持有者、社区）？
* 谁将做出哪些决策？
* 区块链如何充当信任（或信心）机器？

## **区块链治理模型**

1.  **基于IT治理的模型（Beck et al., 2018）**

* **决策权（Decision rights）**：管理过程中涉及的实体的权限、责任和能力。决策权的分配表明区块链的去中心化程度。
* **问责制（Accountability）**：监督决策和处理这些行动后果的责任。
* **激励（Incentives）**：促使参与者与区块链互动并调整其行为的动机。

2.  **区块链治理框架（Rikken, Janssen, and Kwee, 2019）**

* **不可直接影响的治理（非技术治理）**：

    * **机构层面**：法律/法规、协议（联盟）、标准。

* **可直接影响的治理（技术治理）**：

    * **公司/个人层面**：个人行为意识协议。
    * **应用层面**：业务规则和应用安全。
    * **基础设施/区块链层面**：协议安全、共识、密码学。

* **治理生命周期**：

    * **设计（Design）**：

        * 目的：设计解决方案。
        * 时间：非时间关键。
        * 利益相关者角色：合作。

    * **操作（Operate）**：

        * 目的：日常操作（决策和行动）。
        * 时间：受限于规则和协议。
        * 利益相关者角色：常规。

    * **演变-危机（Evolve-crisis）**：

        * 目的：更新过程。
        * 时间：时间关键。
        * 利益相关者角色：关键代码更新、硬分叉/软分叉。

3.  **综合区块链治理模型（Tan et al., 2022）**

* **微观层（Micro-level governance）**：

    * **描述**：与区块链设计者关于基于区块链系统的基础设施决策相关。
    * **决策类型**：基础设施架构、应用架构、互操作性。
    * **相关事项**：公有/私有、区块链协议、系统开发、维护和更新；dApps、智能合约、预言机；标准、互操作性、度量。

* **中观层（Meso-level governance）**：

    * **描述**：与决策和行动中的组织过程相关。
    * **决策类型**：决策机制、激励机制、共识机制。
    * **相关事项**：链上/链下、社区治理、投票、通信；激励结构、参与者动机；共识模型（工作量证明、权益证明）。
    
* **宏观层（Macro-level governance）**：

    * **描述**：侧重于制度规则和规范。
    * **决策类型**：治理组织、治理问责制、治理控制。
    * **相关事项**：去中心化程度、层级结构、成员资格、角色；治理规则、分叉、争议/冲突解决、契约框架；决策权、控制系统、方向、监督。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> BSI 2025_Trinh Nguyen (Blockchain governance)_Jul 16 2025 </div>
<div class="file-meta"> 2,609 KB / 2025-07-17</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Miscellaneous/UBC/BSI 2025_Trinh Nguyen (Blockchain governance)_Jul 16 2025.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>