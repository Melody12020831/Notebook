# block chain DAY 1

## **I. 区块链概览 (Overview of Blockchain)**

### **区块链定义 (What is Blockchain?)**

* 区块链是一种数字账本 (digital ledger)，用于记录有价值的事物。
* 它是分布式 (distributed) 的，并利用网络处理交易 (transactions)。
* 它利用密码学 (cryptography) 使记录安全且不可篡改 (immutable)。
* 一些区块链具备以下特性：代表资产的数字代币 (digital tokens that represent assets)、不同类型的权限 (different types of permissions) 和智能合约 (smart contracts)。

### **区块链的关键组成部分与概念 (Key Components & Concepts of Blockchain Solutions)**

1. **区块 (Blocks)**：区块链的"构建块 (building blocks)"。

* 区块链中的每个区块都像一份详细的发票或费用清单，其中包含交易列表或摘要。
* 区块链交易等同于价值单位的转移，表现为账本条目，用于跟踪"账户 (account)"中价值的累积及其在账户之间的移动。
* 并非所有分布式数字账本 (distributed digital ledgers) 都使用区块数据结构 (block data structures) (例如，IOTA 和 Nano 使用有向无环图数据结构 (Directed Acyclic Graph data structures (DAGs)))。

2. **链 (Chain)**：新数据以区块的形式添加，这些区块相互链接形成链。

* 密码学 (Cryptography) 将区块链接在一起，有助于使账本"不可篡改 (immutable)"。
* 链中越靠前的区块越"安全 (more secure)"。

3. **分布式网络结构 (A Distributed Network Structure)**：网络中的所有节点 (nodes) 都拥有账本的相同副本，这增强了信任 (trust)。

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

### * **区块链的适用场景 (When Blockchain is Useful)**

* 当交易各方目标和激励不一致，导致不信任时。
* 当缺乏透明度 (transparency) 时。
* 当参与者不可信，可能作弊时。
* 区块链解决方案在跨组织层面 (interorganizational level) 最有意义。

### **区块链的非适用场景 (When Blockchain is Less Useful)**

* 当单个行为者可以被信任来维护记录和促进交易时 (例如公司内部的 IT 和会计部门)。
* 区块链解决方案在单个组织内部通常是不必要的。

## **II. 区块链应用 (Applications of Blockchain)**

### **区块链用例概览 (Overview of Blockchain Use Cases) (基于 ISO TR 3242:2022)**

* **数据溯源 (Data Provenance)**：数据问责 (Data Accountability)、产权记录管理 (Property Records Management)、学生记录管理 (Student Records Management)、教育证书溯源 (Education Certificate Provenance)、自证主权身份 (Self-Sovereign Identity (SSID))、内容时间戳验证 (Content Timestamp Verification)。

    * **产权记录管理 (Property Records Management)**：印度于 2017 年启动了 PRMS 计划，旨在简化土地登记流程。

* **金融科技 (Fintech)**：应收账款 (Accounts Receivable)、银行间贷款对账 (Interbank Loan Reconciliation)、有组织合会 (Organised CHIT Funds)、养老金流程优化 (Pension Process Optimisation)、透明证券化 (Transparent Securitisation)、去中心化慈善平台 (Decentralized Charity Platform)。

    * **银行间对账和结算 (Interbank Reconciliation and Settlement)**：区块链技术可以将结算周期从 $T+1$ 或 $T+2$ 天缩短到 $T+0$ 天，解决效率低下和信息不对称问题。这是中国的一个实际应用。
    * **去中心化援助平台 (Decentralized Aid Platform) (WFP Building Blocks)**：通过消除交易成本 (transaction costs)、直接向个人发送援助、整合生物识别扫描 (biometric scanning) 以防止欺诈 (fraud)、提供更大的隐私 (privacy) 以及为每个人创建不可篡改的数字身份 (immutable digital identity) 来解决向叙利亚难民提供粮食援助的挑战。由以太坊提供支持 (powered by Ethereum)。

* **供应链 (Supply Chain)**：国际贸易透明度 (International Trade Transparency)、海运提单 (Maritime Bills of Lading)、特许制药供应链管理 (Franchised Pharma Supply Management)、药品防伪 (Anti-counterfeit Pharma)、IGP 可追溯性 (IGP Traceability)、通用农场合规 (Universal Farm Compliance)、国际废物管理系统 (Intl. Waste Management System)。

    * **农产品可追溯性 (Traceability of Agricultural Food Products)**：ROUGE (Red Orange Upgrading Green Economy) 解决方案为 IGP 红橙提供了经认证且不可更改的产品历史，支持打击欺诈和伪造，并确保供应链中的透明度、安全性 (security) 和弹性 (Resilience)。

* **智能能源 (Smart Energy)**：合作能源交易 (Cooperative Energy Trading)、能源交易 (Energy Trading)、可再生能源产消者微电网 (Renewable Energy Prosumer Microgrids)。

### **变革性应用 (Transformative Applications) (区块链如何颠覆现有做事方式)**

* 实现没有中心权力机构 (no central authority) 的分布式组织 (distributed organizations)。
* 规避中介 (Circumventing intermediaries) (例如公司、银行、政府)。
* 实现新的治理结构 (new governance structures)。
* 实现个人数据所有权 (individual data ownership) 和控制权。

    * 允许个人在不同平台之间携带数据。

* 创建新的资产和市场 (new assets and markets)。

    * 新的数字资产 (New digital assets) (例如效用代币 utility tokens、加密货币 cryptocurrencies)。
    * 现实世界资产的代币化 (Tokenization)、碎片化 (fragmentation) 和重组 (recombination)。

## **III. 三层模型 (The Three Layer Model)**

### **目的 (Purpose)**：一个用于设计和分析区块链/DLT 系统 (blockchain/DLT systems) 的框架。

* 其必要性在于该技术仍处于理论不足阶段 (under theorized)，现有模型在全面考虑权衡 (trade-offs) 方面存在不足，这可能导致次优设计 (sub-optimal designs) 和意想不到的负面后果 (negative unintended consequences)。

### **系统思维 (Systems Thinking)**：

* 以整体方式 (holistically) 和事物之间相互关系 (inter-relationships) 的角度进行思考的过程，而不是将其视为不相关的实体。

### **系统定义 (Definition of a System)**：

* 一个被感知的整体，其元素随着时间不断相互影响，并朝着共同的目标运作。系统由子系统 (subsystems) 或功能 (functions)、过程 (processes)、活动 (activities) 和任务 (tasks) 组成。

* **功能 (Functions) (目的 Purpose)**：系统实现其目的的方式。
* **子系统 (Subsystems)**：系统通常包含子系统。例如，地球是太阳系 (Solar System) 的一个子系统，但也可以被视为一个独立的系统，海洋则是地球的一个子系统。

### **活动 (Activities)、交易 (Transactions)、过程 (Processes)**：

* **活动 (Activities)**：系统通过开展活动来实现其目的。
* **交易 (Transaction)**：涉及多人的行为或相互关联的行为，通过这些行为，这些人的关系发生改变，或是由两人或多个系统之间交换的最小工作过程单元。
* **业务 (或工作) 过程 (Business (or work) process)**：一个或多个交易序列 (sequences of transactions)，需要产生符合管理规则 (governing rules) 的结果 (outcome)。
* **序列 (Sequence)**：一系列交易，其连接要求是，后续交易的进行依赖于先前交易的完成。

### **系统方法设计区块链的优势 (Advantages of a Systems Approach to Blockchain Design)**：

* 使我们能够理解设计组件 ("子系统") 如何与其他组件动态交互。
* 使我们能够整体评估系统，并识别盲点 (blind spots)、隐藏假设 (hidden assumptions) 和意外结果 (unexpected outcomes)。
* 为深入研究不同的子系统提供了基础。

### **三层 (The Three Layers)**：每一层都可以被视为不同的抽象层 (abstraction layers)。

* **社会层 (Social Layer)**：涵盖社会参与者 (social actors)，以及这些工具和平台的社会 (social)、政治 (political) 和经济影响 (economic implications)。
* **信息层 (Informational Layer)**：侧重于账本本身作为交易数据 (transactional data) 的"不可篡改 (immutable)"存储库。
* **技术层 (Technical Layer)**：指实施区块链和分布式账本系统的技术组件 (technical components)，即使仍存在需要克服的新技术挑战。

### **区块链的动机 (Motivation for Blockchain) (信任 Trust)**：

* 中本聪 (Satoshi Nakamoto) 创建比特币 (Bitcoin)（以及其底层技术区块链）是为了解决信任问题 (problem of TRUST)，而无需依赖受信任的中介 (trusted intermediary)（通常并不可靠），换句话说，实现"无信任的信任 (TRUSTLESS TRUST)"。

### **深入理解区块链/DLT 的关键方面 (Deeper Understanding about Key Aspects of Blockchains/DLTs)**：

* **治理 (Governance)**：区块链/DLT 的控制机制 (control mechanism)，可以是内部 (Internal) 或外部 (External) 的。
* **激励 (Incentives)**：一种"执行器 (actuator)"，作用于所有系统组件所拥有的信息处理"逻辑 (logic)"或指令集 (set of instructions)。
* **安全 (Security)**：设计涉及权衡，不仅包括安全性和可扩展性 (scalability) 之间常见的权衡，还包括不同安全属性 (security properties) 之间的权衡，即机密性 (confidentiality) 与透明度 (transparency)，或数据完整性 (data integrity) 与隐私 (privacy)。同样，在不同层或同一层内不同抽象级别 (levels of abstraction) 应用的同一安全属性内部也可能存在权衡。
* **去中心化 (Decentralization)**：DLT 系统每个子系统/层的架构可以集中 (centralized) 或去中心化 (decentralized) 到不同程度，以影响整个系统的运行。
* **溯源追踪 (Provenance tracking)**：一种功能能力 (functional capability)，而非 DLT 系统、其子系统或组件的固有属性 (inherent property)。
* **时间性 (Temporality)**：区块链/DLT 系统并非静态的 (static)，其属性 (properties) 和能力 (capabilities) 可能并非完全可预测。

### **基于三层概念模型的问题导向设计框架 (A Question-Led Design Framework Based Upon the Three Layer Conceptual Model)**：

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

### **三层模型的优势 (ADVANTAGES OF USING THE THREE LAYER MODEL)**：

* 创建了一个用于多学科、问题导向的设计空间的通用概念框架 (common conceptual framework) 和语言。
* 能够"看到"设计选择可能产生的交叉影响和连锁效应（即在设计背景下调动"系统思维" (systems thinking)）。
* 通过利用问题导向框架 (Question-led Framework) 来锚定范围讨论，设计团队可以更清晰地界定即时原型 (immediate prototype) 的必要需求与完整系统的长期设计目标之间的区别。
* 有助于识别以前的"未知未知 (unknown unknowns)"。
* 技术问题的框架引导了对新颖技术能力 (novel technical capabilities) 的探索，例如与物联网 (IoT) 的集成。

### **三层模型的局限性 (LIMITATIONS OF THE THREE LAYER MODEL)**：

* 问题高层次且复杂，需要时间学习和理解。
* 仍需要更广泛的实证验证 (empirical validation) 和可复现性 (reproducibility)。
* 对其他技术（例如人工智能 (AI)）的适用性 (applicability) 仍有待观察。

## **IV. 案例研究：Swear (区块链 + 人工智能) (Case Study: Swear (Blockchain + AI))**

### **背景 (Background)**：

* 聚焦于深度伪造 (deepfakes)，其中伪造图像和视频正在侵蚀建立对真相主张 (truth claims) 信任的视觉基础。区块链被认为具有防御深度伪造的能力。

### **Swear 解决方案 (Swear Solution)**：

* 用于视频捕获的移动应用程序 (Mobile App for video capture)。
* 支持的格式 (Supported formats)：D1, 960H, HD SDI, AHD, HD-TVI, HD-CVI, IP, 4k。
* 编解码器 (Codecs)：H.264, AVI, AVCHD H.265 (HVEC)。
* 兼容 DVR 和 NVR。
* Web3.0 区块链 (Web3.0 Blockchain) 保护指纹 (fingerprints)，建立不可篡改的保管链 (immutable chain-of-custody)。
* 数字媒体真实性 (Digital media authenticity) 持续实时验证 (verified continuously and in real time)。
* 在像素级别识别媒体篡改 (identification of media manipulation at the pixel level)。
* 集成到现有监控系统 (Integrates into existing surveillance systems)。

### **案例研究分析下一步 (CASE STUDY ANALYSIS . . .NEXT STEPS)**：

* 使用三层模型审查和讨论 Swear 解决方案，根据三层模型对解决方案的特性 (features) 和能力 (capabilities) 进行分类；寻找模型各"层 (layer)"之间的相互联系和互动（例如，账本如何增强信任？社会参与者和机构 (social actors and institutions) 是谁？使用了哪种类型的区块链 (type of blockchain)？如何形成共识 (consensus is formed)？）。

---

# UBC block chain DAY 2

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

### **PrestigeBFT 总结 (PrestigeBFT - Summary)**：

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

# UBC block chain DAY 3

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

# UBC block chain DAY 4

在区块链领域，**可验证计算 (Verifiable Computing)**、**乐观方法 (Optimistic Approach)** 和 **编码计算 (Coded Computing)** 是三种不同的技术或范式，它们各自从不同角度解决区块链面临的挑战，主要是关于**可扩展性、效率和信任**。

### 1. 可验证计算 (Verifiable Computing)

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

### 3. 编码计算 (Coded Computing)

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

# UBC block chain DAY 5

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

### **区块链 (Blockchain)**：

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