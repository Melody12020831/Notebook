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
    
    $60\% \times 20\% \times \text{最大功率} + 40% \times 90\% \times \text{最大功率} = 48\%$。

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

    那么只要 $X \times Y \times 15.63 $ > 1000000 美元，也即 $X \times Y > 639795$ 美元，那么这个决策就是值得的。

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