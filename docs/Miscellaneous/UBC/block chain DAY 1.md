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

### **区块链的适用场景**

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