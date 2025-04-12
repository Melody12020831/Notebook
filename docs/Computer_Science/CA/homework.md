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
    The following questions investigate the impact of small and simple caches using CACTI and assume a 65 nm (0.065 m) technology. ([CACTI is available in an online form at](http://quid.hpl.hp.com:9081/cacti/).)

    a. Compare the access times of 64 KB caches with 64-byte blocks and a single bank. What are the relative access times of two-way and four-way set associative caches compared to a direct mapped organization?

    b. Compare the access times of four-way set associative caches with 64-byte blocks and a single bank. What are the relative access times of 32 and 64 KB caches compared to a 16 KB cache?

    c. For a 64 KB cache, find the cache associativity between 1 and 8 with the lowest average memory access time given that misses per instruction for a certain workload suite is 0.00664 for direct-mapped, 0.00366 for two-way set associative, 0.000987 for four-way set associative, and 0.000266 for eight-way set associative cache. Overall, there are 0.3 data references per instruction. Assume cache misses take 10 ns in all models. To calculate the hit time in cycles, assume the cycle time output using CACTI, which corresponds to the maximum frequency a cache can operate without any bubbles in the pipeline.

??? note "answer"

---

### 2.18

???+ question
    You are investigating the possible benefits of a way-predicting L1 cache. Assume that a 64 KB four-way set associative single-banked L1 data cache is the cycle time limiter in a system. For an alternative cache organization, you are considering a way-predicted cache modeled as a 64 KB direct-mapped cache with 80% prediction accuracy. Unless stated otherwise, assume that a mispredicted way access that hits in the cache takes one more cycle. Assume the miss rates and the miss penalties in question 2.8 part (c).

    a. What is the average memory access time of the current cache (in cycles) versus the way-predicted cache?

    b. If all other components could operate with the faster way-predicted cache cycle time (including the main memory), what would be the impact on performance from using the way-predicted cache?

    c. Way-predicted caches have usually been used only for instruction caches that feed an instruction queue or buffer. Imagine that you want to try out way prediction on a data cache. Assume that you have 80% prediction accuracy and that subsequent operations (e.g., data cache access of other instructions, dependent operations) are issued assuming a correct way prediction. Thus a way misprediction necessitates a pipe flush and replay trap, which requires 15 cycles. Is the change in average memory access time per load instruction with data cache way prediction positive or negative, and how much is it?

    d. As an alternative to way prediction, many large associative L2 caches serialize tag and data access so that only the required dataset array needs to be activated. This saves power but increases the access time. Use CACTI's detailed web interface for a 0.065 m process 1 MB four-way set associative cache with 64-byte blocks, 144 bits read out, 1 bank, only 1 read/write port, 30 bit tags, and ITRS-HP technology with global wires. What is the ratio of the access times for serializing tag and data access compared to parallel access?

??? note "answer"

---

### 2.26

???+ question
    The ways of a set can be viewed as a priority list, ordered from high priority to low priority. Every time the set is touched, the list can be reorganized to change block priorities. With this view, cache management policies can be decomposed into three sub-policies: Insertion, Promotion, and Victim Selection. Insertion defines where newly fetched blocks are placed in the priority list. Promotion defines how a block’s position in the list is changed every time it is touched (a cache hit). Victim Selection defines which entry of the list is evicted to make room for a new block when there is a cache miss.

    a. Can you frame the LRU cache policy in terms of the Insertion, Promotion, and Victim Selection sub-policies?

    b. Can you define other Insertion and Promotion policies that may be competitive and worth exploring further?

??? note "answer"

---

### 2.27

???+ question
    In a processor that is running multiple programs, the last-level cache is typically shared by all the programs. This leads to interference, where one program’s behavior and cache footprint can impact the cache available to other programs. First, this is a problem from a quality-of-service (QoS) perspective, where the interference leads to a program receiving fewer resources and lower performance than promised, say by the operator of a cloud service. Second, this is a problem in terms of privacy. Based on the interference it sees, a program can infer the memory access patterns of other programs. This is referred to as a timing channel, a form of information leakage from one program to others that can be exploited to compromise data privacy or to reverse-engineer a competitor’s algorithm. What policies can you add to your last-level cache so that the behavior of one program is immune to the behavior of other programs sharing the cache?

??? note "answer"

---

### 2.28

???+ question
    A large multimegabyte L3 cache can take tens of cycles to access because of the long wires that have to be traversed. For example, it may take 20 cycles to access a 16 MB L3 cache. Instead of organizing the 16 MB cache such that every access takes 20 cycles, we can organize the cache so that it is an array of smaller cache banks. Some of these banks may be closer to the processor core, while others may be further. This leads to nonuniform cache access (NUCA), where 2 MB of the cache may be accessible in 8 cycles, the next 2 MB in 10 cycles, and so on until the last 2 MB is accessed in 22 cycles. What new policies can you introduce to maximize performance in a NUCA cache?

??? note "answer"

---

### 2.32

???+ question
    You are provisioning a server with eight-core 3 GHz CMP that can execute a workload with an overall CPI of 2.0 (assuming that L2 cache miss refills are not delayed). The L2 cache line size is 32 bytes. Assuming the system uses DDR2-667 DIMMs, how many independent memory channels should be provided so the system is not limited by memory bandwidth if the bandwidth required is sometimes twice the average? The workloads incur, on average, 6.67 L2 misses per 1 K instructions.

??? note "answer"

---

### 2.33

???+ question
    Consider a processor that has four memory channels. Should consecutive memory blocks be placed in the same bank, or should they be placed in different banks on different channels?

??? note "answer"

---

### 2.36

???+ question
    Whenever a computer is idle, we can either put it in standby (where DRAM is still active) or we can let it hibernate. Assume that, to hibernate, we have to copy just the contents of DRAM to a nonvolatile medium such as Flash. If reading or writing a cache line of size 64 bytes to Flash requires 2.56 J and DRAM requires 0.5 nJ, and if idle power consumption for DRAM is 1.6 W (for 8 GB), how long should a system be idle to benefit from hibernating? Assume a main memory of size 8 GB.

??? note "answer"

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

---

### 2.41

???+ question
    Since instruction-level parallelism can also be effectively exploited on in-order superscalar processors and very long instruction word (VLIW) processors with speculation, one important reason for building an out-of-order (OOO) superscalar processor is the ability to tolerate unpredictable memory latency caused by cache misses. Thus you can think about hardware supporting OOO issue as being part of the memory system. Look at the floorplan of the Alpha 21264 in Figure 2.36 to find the relative area of the integer and floating-point issue queues and mappers versus the caches. The queues schedule instructions for issue, and the mappers rename register specifiers. Therefore these are necessary additions to support OOO issue. The 21264 only has L1 data and instruction caches on chip, and they are both 64 KB two-way set associative. Use an OOO superscalar simulator such as [SimpleScalar](http://www.cs.wisc.edu/~mscalar/simplescalar.html) on memory-intensive benchmarks to find out how much performance is lost if the area of the issue queues and mappers is used for additional L1 data cache area in an in-order superscalar processor, instead of OOO issue in a model of the 21264. Make sure the other aspects of the machine are as similar as possible to make the comparison fair. Ignore any increase in access or cycle time from larger caches and effects of the larger data cache on the floorplan of the chip. (Note that this comparison will not be totally fair, as the code will not have been scheduled for the in-order processor by the compiler.)

    ![img](./assets/hw2-1.png)

    **Figure 2.36 Floorplan of the Alpha 21264 [Kessler 1999].**

??? note "answer"

---