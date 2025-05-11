---
statistics: True
comments: true
---

# Homework

## 第一次作业

### 1.9

???+ question
    Server farms such as Google and Yahoo! provide enough compute capacity for the highest request rate of the day. Imagine that most of the time these servers operate at only 60% capacity. Assume further that the power does not scale linearly with the load; that is, when the servers are operating at 60% capacity, they consume 90% of maximum power. The servers could be turned off, but they would take too long to restart in response to more load. A new system has been proposed that allows for a quick restart but requires 20% of the maximum power while in this "barely alive" state.

    a. How much power savings would be achieved by turning off 60% of the servers?
    
    b. How much power savings would be achieved by placing 60% of the servers in the "barely alive" state?
    
    c. How much power savings would be achieved by reducing the voltage by 20% and frequency by 40%?
    
    d. How much power savings would be achieved by placing 30% of the servers in the "barely alive" state and 30% off?

??? note "answer"
    a. 
    
    关掉 60% 的服务器，所以是 40% 的服务器在运行。此时总功率是 $40\% \times 90\% \times \text{最大功率} = 36\% \times \text{最大功率}$。
    
    原来的总功率是 $100\% \times 90\% \times \text{最大功率} = 90\% \times \text{最大功率}$。
    
    节省的功率是 $90\% \times \text{最大功率} - 36\% \times \text{最大功率} = 54\% \times \text{最大功率}$。
    
    所以节省的比例为 $\frac{54\% \times \text{最大功率}}{90\% \times \text{最大功率}} = 60\%$。
    
    b. 
    
    $60\% \times 20\% \times \text{最大功率} + 40\% \times 90\% \times \text{最大功率} = 48\%$。
    
    节省的功率为 $90\% \times \text{最大功率} - 48\% \times \text{最大功率} = 42\% \times \text{最大功率}$。
    
    所以节省的比例为 $\frac{42\% \times \text{最大功率}}{90\% \times \text{最大功率}} = 46.67\%$。
    
    c. 
    
    每个晶体管所需要的功耗 $\text{功耗}_{\text{动态}} \propto \frac{1}{2} \times \text{容性负载} \times \text{电压}^2 \times \text{开关频率}$
    
    80% * 80% * 60% = 38.4%
    
    所以节省了 61.6% 的功耗。
    
    d. 
    
    $30\% \times 20\% \times \text{最大功率} + 40\% \times 90\% \times \text{最大功率} = 42\%$。
    
    节省的功率为 $90\% \times \text{最大功率} - 42\% \times \text{最大功率} = 48\% \times \text{最大功率}$。
    
    所以节省的比例为 $\frac{48\% \times \text{最大功率}}{90\% \times \text{最大功率}} = 53.33\%$。

---

### 1.11 ab

???+ question
    In a server farm such as that used by Amazon or eBay, a single failure does not cause the entire system to crash. Instead, it will reduce the number of requests that can be satisfied at any one time.

    a. If a company has 10,000 computers, each with an MTTF of 35 days, and it experiences catastrophic failure only if 1/3 of the computers fail, what is the MTTF for the system?
    
    b. If it costs an extra $1000, per computer, to double the MTTF, would this be a good business decision? Show your work.

??? note "answer"
    a. 

    假设每台服务器的故障时间服从指数分布，故障率 $\lambda = \frac{1}{35}$ 每天。系统崩溃需至少 $\frac{1}{3}$ 服务器故障。
    
    总故障过程为泊松过程，系统 MTTF 为第 $\frac{10000}{3}$ 次故障的期望时间：
    
    $$\text{系统}_{MTTF} = \frac{k}{n\lambda} = \frac{\frac{10000}{3}}{10000 \times 35} \approx 11.67 \text{天}$$


    b. 
    
    若每台服务器 MTT F翻倍至 70 天，则 $\lambda = \frac{1}{70}$，系统 MTTF 为第 $\frac{10000}{3}$ 次故障的期望时间：
    
    $$\text{系统}_{MTTF} = \frac{k}{n\lambda} = \frac{\frac{10000}{3}}{10000 \times 70} \approx 23.33 \text{天}$$
    
    总成本增加 $1000 \times 10000 = 1000000$ 美元。
    
    如果设每次损失成本为 $X$ 而这一整套系统寿命为 $Y$ 那么每年可以减少维修 $\frac{365}{11.67} - \frac{365}{23.33} = 15.63$ 次。
    
    那么只要 $X \times Y \times 15.63$ > 1000000 美元，也即 $X \times Y > 639795$ 美元，那么这个决策就是值得的。

---

### 1.16

???+ question
    When parallelizing an application, the ideal speedup is speeding up by the number of processors. This is limited by two things: percentage of the application that can be parallelized and the cost of communication. Amdahl's Law takes into account the former but not the latter.

    a. What is the speedup with N processors if 80% of the application is parallelizable, ignoring the cost of communication?
    
    b. What is the speedup with eight processors if, for every processor added, the communication overhead is 0.5% of the original execution time.
    
    c. What is the speedup with eight processors if, for every time the number of processors is doubled, the communication overhead is increased by 0.5% of the original execution time?
    
    d. What is the speedup with N processors if, for every time the number of processors is doubled, the communication overhead is increased by 0.5% of the original execution time?
    
    e. Write the general equation that solves this question: What is the number of processors with the highest speedup in an application in which P% of the original execution time is parallelizable, and, for every time the number of processors is doubled, the communication is increased by 0.5% of the original execution time?

??? note "answer"
    a. 

    加速后是原来的 $20\% + \frac{80\%}{N}$
    
    所以加速比是 $\frac{1}{20\% + \frac{80\%}{N}}$
    
    b. 
    
    加速后是原来的 $S = 20\% + \frac{80\%}{8} + 0.5\% \times (8 - 1) = 33.5\%$
    
    所以加速比是 $\frac{1}{33.5\%} = 2.985$
    
    c.
    
    加速后是原来的 $S = 20\% + \frac{80\%}{8} + 0.5\% \times log_2(8) = 31.5\%$
    
    所以加速比是 $\frac{1}{31.5\%} = 3.1746$
    
    d. 
    
    加速后是原来的 $S = 20\% + \frac{80\%}{N} + 0.5\% \times log_2(N)$
    
    所以加速比是 $\frac{1}{20\% + \frac{80\%}{N} + 0.5\% \times log_2(N)}$
    
    e. 
    
    总时间是 $T = (1 - P)\% + \frac{P\%}{N} + 0.5\% \times log_2(N)$
    
    那么求解 $\frac{\mathrm{d}T}{\mathrm{d}N} = 0$ 可以得到
    
    $$N = \frac{P\% \times ln2}{0.5\%}$$

---

## 第二次作业

### 2.17

???+ question
    The following questions investigate the impact of small and simple caches using CACTI and assume a 65 nm (0.065 ms) technology. ([CACTI is available in an online form at](http://quid.hpl.hp.com:9081/cacti/).)

    a. Compare the access times of 64 KB caches with 64-byte blocks and a single bank. What are the relative access times of two-way and four-way set associative caches compared to a direct mapped organization?

    b. Compare the access times of four-way set associative caches with 64-byte blocks and a single bank. What are the relative access times of 32 and 64 KB caches compared to a 16 KB cache?

    c. For a 64 KB cache, find the cache associativity between 1 and 8 with the lowest average memory access time given that misses per instruction for a certain workload suite is 0.00664 for direct-mapped, 0.00366 for two-way set associative, 0.000987 for four-way set associative, and 0.000266 for eight-way set associative cache. Overall, there are 0.3 data references per instruction. Assume cache misses take 10 ns in all models. To calculate the hit time in cycles, assume the cycle time output using CACTI, which corresponds to the maximum frequency a cache can operate without any bubbles in the pipeline.

??? note "answer"
    a. 由 CACTI 模拟结果 得到
    
    a direct mapped organization : 0.86 ns

    a two-way set associative organization : 1.12 ns

    a four-way set associative organization : 1.37 ns

    relatively, the access time

    $$\frac{\text{two-way}}{\text{direct mapped}} = \frac{1.12}{0.86} = 1.30 \ ns$$

    $$\frac{\text{four-way}}{\text{direct mapped}} = \frac{1.37}{0.86} = 1.59 \ ns$$

    b. 由 CACTI 模拟结果 得到

    a 16 KB direct-mapped organization : 1.27 ns

    a 32 KB two-way set associative organization : 1.35 ns

    a 64 KB four-way set associative organization : 1.37 ns

    relatively, the access time

    $$\frac{\text{two-way}}{\text{direct mapped}} = \frac{1.35}{1.27} = 1.06 \ ns$$

    $$\frac{\text{four-way}}{\text{direct mapped}} = \frac{1.37}{1.27} = 1.08 \ ns$$

    c. 

    先计算缺失率

    $$\text{direct mapped} = \frac{0.00664}{0.3} \approx 2.21\%$$

    $$\text{two-way} = \frac{0.00366}{0.3} \approx 1.22\%$$

    $$\text{four-way} = \frac{0.000987}{0.3} \approx 3.29\%$$

    $$\text{eight-way} = \frac{0.000266}{0.3} \approx 0.09\%$$

    再把命中时间转换成周期（周期要向上取整）

    $$\text{direct mapped} = \lceil \frac{0.86}{0.5} \rceil = 2 \ ns$$

    $$\text{two-way} = \lceil \frac{1.12}{0.5} \rceil = 3\ ns$$

    $$\text{four-way} = \lceil \frac{1.37}{0.83} \rceil = 2 \ ns$$

    $$\text{eight-way} = \lceil \frac{2.03}{0.79} \rceil = 3 \ ns$$

    再把 miss penalty 转换成周期（周期要向上取整）

    $$\text{direct mapped} = \lceil \frac{10}{0.5} \rceil = 20 \ ns$$

    $$\text{two-way} = \lceil \frac{10}{0.5} \rceil = 20 \ ns$$

    $$\text{four-way} = \lceil \frac{10}{0.83} \rceil = 13 \ ns$$

    $$\text{eight-way} = \lceil \frac{10}{0.79} \rceil = 13 \ ns$$

    最后计算 AMAT

    $$AMAT = \text{hit time} + \text{miss rate} \times \text{miss penalty}$$

    1. 直接映射 $((1 - 2.21\%) \times 2 + 2.21\% \times 20 ) \times 0.5 \approx 1.20 \ ns$

    2. 两路 $((1 - 1.22\%) \times 3 + 1.22\% \times 20 ) \times 0.5 \approx 1.59 \ ns$

    3. 四路 $((1 - 3.29\%) \times 2 + 3.29\% \times 13 ) \times 0.83 \approx 1.96 \ ns$

    4. 八路 $((1 - 0.09\%) \times 3 + 0.09\% \times 13 ) \times 0.79 \approx 2.38 \ ns$

    直接映射的 cache 的 AMAT 最小

---

### 2.18

???+ question
    You are investigating the possible benefits of a way-predicting L1 cache. Assume that a 64 KB four-way set associative single-banked L1 data cache is the cycle time limiter in a system. For an alternative cache organization, you are considering a way-predicted cache modeled as a 64 KB direct-mapped cache with 80% prediction accuracy. Unless stated otherwise, assume that a mispredicted way access that hits in the cache takes one more cycle. Assume the miss rates and the miss penalties in question 2.8 part (c).

    a. What is the average memory access time of the current cache (in cycles) versus the way-predicted cache?

    b. If all other components could operate with the faster way-predicted cache cycle time (including the main memory), what would be the impact on performance from using the way-predicted cache?

    c. Way-predicted caches have usually been used only for instruction caches that feed an instruction queue or buffer. Imagine that you want to try out way prediction on a data cache. Assume that you have 80% prediction accuracy and that subsequent operations (e.g., data cache access of other instructions, dependent operations) are issued assuming a correct way prediction. Thus a way misprediction necessitates a pipe flush and replay trap, which requires 15 cycles. Is the change in average memory access time per load instruction with data cache way prediction positive or negative, and how much is it?

    d. As an alternative to way prediction, many large associative L2 caches serialize tag and data access so that only the required dataset array needs to be activated. This saves power but increases the access time. Use CACTI's detailed web interface for a 0.065 m process 1 MB four-way set associative cache with 64-byte blocks, 144 bits read out, 1 bank, only 1 read/write port, 30 bit tags, and ITRS-HP technology with global wires. What is the ratio of the access times for serializing tag and data access compared to parallel access?

??? note "answer"
    a. current cache

    $$AMAT = (\lceil \frac{1.37}{0.83} \rceil \times (1 - 0.33\%) + 0.33\% \times \lceil \frac{10}{0.83} \rceil) \times 0.83 \approx 1.69 \ ns$$

    way-predicted cache

    $$AMAT = ((\lceil \frac{0.86}{0.5} \rceil \times 80\% + (\lceil \frac{0.86}{0.5} \rceil + 1) \times 20 \% ) \times (1 - 0.33\%) + 0.33\% \times \lceil \frac{10}{0.5} \rceil) \times 0.5 \approx 1.13 \ ns$$

    b. 

    the max frequency of the four-way set associative cache $\frac{1}{0.83} \approx 1.20 GHz$

    the max frequency of the way-predicted cache $\frac{1}{0.5} \approx 2.00 GHz$

    the ratio of the access times is $ \frac{2.00}{1.20} \approx 1.67$

    c. 

    way-predicted cache

    $$AMAT = ((\lceil \frac{0.86}{0.5} \rceil \times 80\% + 15 \times 20 \% ) \times (1 - 0.33\%) + 0.33\% \times \lceil \frac{10}{0.5} \rceil) \times 0.5 \approx 2.33 \ ns$$

    so, negative

    the ratio is $\frac{1.69}{2.33} \approx 0.73$

    d.

    Parallel access: Tags and data are read at the same time with an access time of 1.59 ns.

    Serial access: read the tag first, hit and then read the data, and the access time is 2.4 ns.

    the ratio is $\frac{2.4}{1.59} \approx 1.51$

---

### 2.26

???+ question
    The ways of a set can be viewed as a priority list, ordered from high priority to low priority. Every time the set is touched, the list can be reorganized to change block priorities. With this view, cache management policies can be decomposed into three sub-policies: Insertion, Promotion, and Victim Selection. Insertion defines where newly fetched blocks are placed in the priority list. Promotion defines how a block’s position in the list is changed every time it is touched (a cache hit). Victim Selection defines which entry of the list is evicted to make room for a new block when there is a cache miss.

    a. Can you frame the LRU cache policy in terms of the Insertion, Promotion, and Victim Selection sub-policies?

    b. Can you define other Insertion and Promotion policies that may be competitive and worth exploring further?

??? note "answer"
    a.

    **Insertion**: 
    
    The newly acquired block is inserted into the head of the priority list (the highest priority position).

    **Promotion**:

    Whenever a block is hit (accessed), it is immediately moved to the head of the priority list.

    **Victim Selection**:

    When it's time to retire, select the tail of the priority list (the block that hasn't been visited for the longest time).

    b.

    **Insertion**:

    1. A new block is inserted in the middle of the priority list or the penultimate bit.
    2. Adjust the insertion position based on the block type or prefetch information. The prefetched data is inserted near the tail. Hot data is inserted directly into the head.

    **Promotion**:

    1. After each hit, the block moves forward by a fixed step.
    2. Adjust the lift based on the cumulative number of visits to the block.
    3. Raised to the head only with multiple hits in a short period of time.

    **Victim Selection**:

    No need to change.

---

### 2.27

???+ question
    In a processor that is running multiple programs, the last-level cache is typically shared by all the programs. This leads to interference, where one program's behavior and cache footprint can impact the cache available to other programs. First, this is a problem from a quality-of-service (QoS) perspective, where the interference leads to a program receiving fewer resources and lower performance than promised, say by the operator of a cloud service. Second, this is a problem in terms of privacy. Based on the interference it sees, a program can infer the memory access patterns of other programs. This is referred to as a timing channel, a form of information leakage from one program to others that can be exploited to compromise data privacy or to reverse-engineer a competitor's algorithm. What policies can you add to your last-level cache so that the behavior of one program is immune to the behavior of other programs sharing the cache?

??? note "answer"
    在多程序共享LLC的场景中，以下两种问题尤为突出：

    1. 服务质量（QoS）问题：某个程序占用过多缓存资源，导致其他程序无法达到性能承诺。

    2. 隐私泄露问题：通过缓存访问的时间差异（时间通道），推断其他程序的内存访问模式，可能导致数据泄露或算法逆向工程。

    解决方案：缓存策略设计

    1. 缓存分区，将缓存划分为多个独立区域，每个程序独占一部分。可以是预先固定分配每个程序的缓存 way 数量，或者根据程序行为动态调整分配。
    
    2. 配额管理，限制每个程序可占用的缓存块数量。

    3. 替换策略优化，比如可以为每个程序独立维护替换队列，仅在本程序分配的缓存区域内淘汰。

    4. 使用程序独有的密钥生成缓存索引，使其他程序无法通过地址推断缓存位置，用于实现实现地址混淆。

---

### 2.28

???+ question
    A large multimegabyte L3 cache can take tens of cycles to access because of the long wires that have to be traversed. For example, it may take 20 cycles to access a 16 MB L3 cache. Instead of organizing the 16 MB cache such that every access takes 20 cycles, we can organize the cache so that it is an array of smaller cache banks. Some of these banks may be closer to the processor core, while others may be further. This leads to nonuniform cache access (NUCA), where 2 MB of the cache may be accessible in 8 cycles, the next 2 MB in 10 cycles, and so on until the last 2 MB is accessed in 22 cycles. What new policies can you introduce to maximize performance in a NUCA cache?

??? note "answer"
    1. Record the frequency of access or the most recent access time for each cache block. Blocks of high-frequency access are gradually migrated to the nearest bank. Blocks that have not been accessed within the period are migrated to the remote bank to free up near-end space.

    2. Each bank maintains the tags of the local block, reducing the delay of global tag lookup. Send requests to multiple banks at the same time and take advantage of physical distribution to reduce response times.

---

### 2.32

???+ question
    You are provisioning a server with eight-core 3 GHz CMP that can execute a workload with an overall CPI of 2.0 (assuming that L2 cache miss refills are not delayed). The L2 cache line size is 32 bytes. Assuming the system uses DDR2-667 DIMMs, how many independent memory channels should be provided so the system is not limited by memory bandwidth if the bandwidth required is sometimes twice the average? The workloads incur, on average, 6.67 L2 misses per 1 K instructions.

??? note "answer"
    $$\text{指令吞吐量} = \frac{\text{核心数} \times \text{频率}}{\text{CPI}} = \frac{8 \times 3 \times 10^9}{2.0} = 12 \times 10^9\ \text{指令/秒}$$

    $$\text{平均L2未命中次数/秒} = 12 \times 10^9\ \text{指令/秒} \times \frac{6.67}{1000} = 8 \times 10^7\ \text{次/秒}$$

    $$\text{平均带宽} = 8 \times 10^7\ \text{次/秒} \times 32\ \text{字节/次} = 2560\ \text{MB/秒}$$

    $$\text{峰值带宽} = 2 \times 2560\ \text{MB/秒} = 5120\ \text{MB/秒}$$

    由 DDR2-667 DIMMs :
    
    $$\text{带宽} = 667 \times 10^6\ \text{次/秒} \times 8\ \text{字节/次} = 5336\ \text{MB/秒} > 5120\ \text{MB/秒}$$

    So, one memory channel is enough.

---

### 2.33

???+ question
    Consider a processor that has four memory channels. Should consecutive memory blocks be placed in the same bank, or should they be placed in different banks on different channels?

??? note "answer"
    In a four-channel memory system, the placement strategy for contiguous memory blocks needs to weigh row buffer hits (low latency) with parallel access (high throughput).

    be placed in the same bank: 

    After the first access to the active row, subsequent visits directly read the row buffer to reduce latency. But, sequential requests need to be processed serially, and multi-channel parallelism cannot be leveraged. And if continuous access is intensive, the channel bandwidth utilization is low.

    be placed in different banks on different channels:

    Requests from different channels/banks can be processed at the same time, improving throughput, which take advantage of multi-channel parallelism and make it suitable for burst access. And each visit may require the activation of a new line, adding a single delay.

    In summary, in a four-channel memory system, sequential memory blocks should be distributed across different channels and banks. Although each access may face latency from row buffer misses, the overall throughput and system performance by processing multiple requests in parallel can result in significant overall throughput and system performance, especially for high-concurrency workloads.

---

### 2.36

???+ question
    Whenever a computer is idle, we can either put it in standby (where DRAM is still active) or we can let it hibernate. Assume that, to hibernate, we have to copy just the contents of DRAM to a nonvolatile medium such as Flash. If reading or writing a cache line of size 64 bytes to Flash requires 2.56 $\mu$ J and DRAM requires 0.5 nJ, and if idle power consumption for DRAM is 1.6 W (for 8 GB), how long should a system be idle to benefit from hibernating? Assume a main memory of size 8 GB.

??? note "answer"
    8 GB = 8 * $2^{30}$ bytes = $2^{33}$ bytes = $2^{27}$ cache lines

    读 + 写一次的总功耗是一次 flash 的能耗 $2 \times 2.56 \ J$ = 5.12 J

    待机功耗 1.6 W = 1.6 J/s

    $\therefore \ t = \frac{2^{27} \times 5.12 \ \mu J}{1.6 \ J/s} \approx 429.50 \ s$

    When the system is idle for more than 429.50 seconds, sleep is more energy-efficient than standby.

---

### 2.37

???+ question
    Virtual machines (VMs) have the potential for adding many beneficial capabilities to computer systems, such as improved total cost of ownership (TCO) or availability. Could VMs be used to provide the following capabilities? If so, how could they facilitate this?

    a. Test applications in production environments using development machines?

    b. Quick redeployment of applications in case of disaster or failure?

    c. Higher performance in I/O-intensive applications?

    d. Fault isolation between different applications, resulting in higher availability for services?

    e. Performing software maintenance on systems while applications are running without significant interruption?

??? note "answer"
    a. Yes. Create a virtual machine (such as an operating system, dependent libraries, and network settings) on the development machine that is consistent with the configuration of the production environment, and deploy the application to be tested on the VM for testing.

    b. Yes. Package the application and its runtime environment as a virtual machine image and load the image on the standby hardware to boot the virtual machine for rapid recovery.

    c. No. The hypervisor needs to intercept I/O requests, resulting in additional context switching and latency.

    d. Yes. Each application runs on an independent virtual machine, allocating exclusive CPU, memory, and disk resources. A single VM crash or resource exhaustion does not affect other VMs.

    e. Yes. Migrate running virtual machines from one physical host to another without service interruption.

---

### 2.38

???+ question
    Virtualmachines canlose performance froma number of events, such as the execution of privileged instructions, TLB misses, traps, and I/O. These events are usually handled in system code. Thus one way of estimating the slowdown when running under a VM is the percentage of application execution time in system versus user mode. For example, an application spending 10% of its execution in system mode might slow down by 60% when running on a VM. Figure 2.35 lists the early performance of various system calls under native execution, pure virtualization, and paravirtualization for LMbench using Xen on an Itanium system with times measured in microseconds (courtesy of Matthew Chapman of the University of New South Wales).

    a. What types of programs would be expected to have smaller slowdowns when running under VMs?

    b. If slowdowns were linear as a function of system time, given the preceding slowdown, how much slower would a program spending 20% of its execution in system time be expected to run?

    c. What is the median slowdown of the system calls in the table above under pure virtualization and paravirtualization?

    d. Which functions in the table above have the largest slowdowns? What do you think the cause of this could be?

    |Benchmark|Native|Pure|Para|
    |:---|:---:|:---:|:---:|
    |Null call|0.04|0.96|0.50|
    |Null I/O|0.27|6.32|2.91|
    |Stat|1.10|10.69|4.14|
    |Open/close|1.99|20.43|7.71|
    |Install signal handler|0.33|7.34|2.89|
    |Handle signal|1.69|19.26|2.36|
    |Fork|56.00|513.00|164.00|
    |Exec|316.00|2084.00|578.00|
    |Fork + exec sh|1451.00|7790.00|2360.00|

    **Figure 2.35 Early performance of various system calls under native execution, pure virtualization, and paravirtualization.**

??? note "answer"
    a. 计算密集型（大部分时间执行用户态指令）、内存工作集小（减少因虚拟内存管理导致的性能损失）、且较少进行I/O或系统调用的程序。

    b. According to "an application spending 10% of its execution in system mode might slow down by 60% when running on a VM."

    $$60 \% \times \frac{20 \%}{10 \%} = 120 \%$$

    so the total times is $100\% + 120\% = 220\%$.

    c. 

    | Benchmark          | 纯虚拟化减速比 | 半虚拟化减速比 |
    |:------------------:|:--------------:|:--------------:|
    | Null call          | 0.96/0.04 = 24   | 0.50/0.04 = 12.5 |
    | Null I/O           | 6.32/0.27 $\approx$ 23.41| 2.91/0.27 $\approx$ 9.67|
    | Stat               | 10.69/1.10 $\approx$ 9.72| 4.14/1.10 $\approx$ 3.76 |
    | Open/close         | 20.43/1.99 $\approx$ 10.27|7.71/1.99 $\approx$ 3.87 |
    | Install signal     |7.34/0.33 $\approx$ 22.24 |2.89/0.33 $\approx$ 8.76 |
    | Handle signal      |19.26/1.69 $\approx$ 11.40|2.36/1.69 $\approx$ 1.40 |
    | Fork               |513/56 $\approx$ 9.16     |164/56 $\approx$ 2.93    |
    | Exec               |2084/316 $\approx$ 6.59   |578/316 $\approx$ 1.83   |
    | Fork + exec sh     |7790/1451 $\approx$ 5.37  |2360/1451 $\approx$ 1.63 |

    排序后得到:纯虚拟化中位减速比为 **10.27**，半虚拟化中位减速比为 **3.76**。

    d. Null call and Null I/O, because they have no actual work, the virtualization overhead is very high.

---

### 2.41

???+ question
    Since instruction-level parallelism can also be effectively exploited on in-order superscalar processors and very long instruction word (VLIW) processors with speculation, one important reason for building an out-of-order (OOO) superscalar processor is the ability to tolerate unpredictable memory latency caused by cache misses. Thus you can think about hardware supporting OOO issue as being part of the memory system. Look at the floorplan of the Alpha 21264 in Figure 2.36 to find the relative area of the integer and floating-point issue queues and mappers versus the caches. The queues schedule instructions for issue, and the mappers rename register specifiers. Therefore these are necessary additions to support OOO issue. The 21264 only has L1 data and instruction caches on chip, and they are both 64 KB two-way set associative. Use an OOO superscalar simulator such as [SimpleScalar](http://www.cs.wisc.edu/~mscalar/simplescalar.html) on memory-intensive benchmarks to find out how much performance is lost if the area of the issue queues and mappers is used for additional L1 data cache area in an in-order superscalar processor, instead of OOO issue in a model of the 21264. Make sure the other aspects of the machine are as similar as possible to make the comparison fair. Ignore any increase in access or cycle time from larger caches and effects of the larger data cache on the floorplan of the chip. (Note that this comparison will not be totally fair, as the code will not have been scheduled for the in-order processor by the compiler.)

    ![img](./assets/hw2-1.png)

    **Figure 2.36 Floorplan of the Alpha 21264 [Kessler 1999].**

??? note "answer"
    1. 假设 Issue Queues 和 Mappers 的面积占芯片总逻辑面积的 15%。将 15% 的面积用于扩大 L1 数据缓存，假设面积与容量线性相关，则新缓存容量为：  
    
    $$64\ \text{KB} \times \left(1 + \frac{15\%}{\text{原缓存面积占比}}\right)$$

    若原缓存面积占比为20%，则新容量为：  
    
    $$64\ \text{KB} \times \left(1 + \frac{15\%}{20\%}\right) = 64 \times 1.75 = 112\ \text{KB}.$$

    2. for OOO L1 cache ：64 KB，2-way。
    
    for In-Order L1 cache ：112 KB  

    3. 假设模拟结果：

    | **配置**       | IPC  | L1缺失率 | 执行时间（秒） |
    |:-------------:|:----:|:--------:|:-------------:|
    | 乱序（64 KB）  | 2.0  | 5%       | 100           |
    | 顺序（112 KB） | 1.5  | 3%       | 133           |

    4. 
    
    $$\text{性能损失} = \frac{133 - 100}{100} \times 100\% = 33\%$$
    
---