---
statistics: True
comments: true
---

# Chapter 7 参数估计

设总体 $X$ 有未知参数 $\theta$ , $X_1,\dots,X_n$ 是 $X$ 的简单随机样本。

**点估计问题**：构造合适的统计量 $\hat{\theta}=\hat{\theta}(X_1,\dots,X_n)$ 用来估计未知参数 $\theta$ ，称 $\hat{\theta}$ 为 $\theta$ 的**点估计量**。

当给定样本观察值 $x_1,\dots,x_n$ 时，$\hat{\theta}(x_1,\dots,x_n)$ 为 $\theta$ 的**点估计值**。

## 矩估计法

**统计思想**：用样本矩估计总体矩，用样本矩的函数估计总体矩的函数。

**理论依据**：辛钦大数定律和依概率收敛的性质。

假设 $\mu_j = E(X^j)$ 存在， $j=1,\dots,k$ ，则

$$\hat{\mu}_j = A_j =\frac{1}{n}\sum_{i=1}^n X_i^j, j=1,\dots,k$$

$$\hat{h}(\mu_1,\dots,\mu_k) = h(A_1,\dots,A_k)$$

设总体有 $k$ 个未知参数 $\theta_1,\dots,\theta_k$ ， $X_1,\dots,X_n$ 是来自总体的样本，假设总体的前 $k$ 阶矩存在，矩估计的步骤如下：

1. 建立 $(\theta_1,\dots,\theta_k)$ 与 $(\mu_1,\dots,\mu_k)$ 之间的联系，求总体前 $k$ 阶矩关于 $k$ 个参数的函数， $\mu_j = E(X^i) = h_i(\theta_1,\dots,\theta_k) , i=1,\dots,k$
2. 求各参数关于 $k$ 阶矩的反函数， $\theta_i = g_i(\mu_1,\dots,\mu_k) , i=1,\dots,k$
3. 以样本各阶矩 $A_1,\dots,A_k$ 代替总体各阶矩 $\mu_1,\dots,\mu_k$ ，得到参数的矩估计

$$\hat{\theta}_i = g_i(A_1,\dots,A_k) , i=1,\dots,k$$

???+ question
    现随机选出100名学生,计算得他们的平均成绩为72.3分,标准差为15.8分.试估计全部学生的平均成绩.

??? note "Answer"
    $$\begin{cases}\mu_1 = E(X) = \mu \\ \mu_2 = E(X^2) = \mu^2 + \sigma^2 \end{cases} \Rightarrow \begin{cases}\mu = \mu_1 \\ \sigma = \sqrt{\mu_2 - \mu_1^2} \end{cases}$$

    $$\Rightarrow \begin{cases}\hat{\mu} = 72.3 \\ \hat{\sigma} = \sqrt{A_2 - \overline{X}^2} = \sqrt{B_2} = \sqrt{\frac{99}{100} \times 15.8^2} = 15.7 \end{cases}$$

???+ question
    设总体 $X \sim B(1,p)$ ， $X_1,\dots,X_n$ 是样本，求 $p$ 的矩估计量. (Something like 标记重捕法)

??? note "Answer"
    $$\mu = E(X) = p$$

    $$\hat{p} = \overline{X} = \frac{1}{n} \sum_{i=1}^n X_i$$

???+ question
    设总体的密度为: $f(x;\theta) = \begin{cases} \sqrt{\theta}x^{\sqrt{\theta}-1},&0 \le x \le 1 \\ 0, & \text{otherwise}\end{cases} , \theta > 0$ 未知，其中 $X_1,\dots,X_n$ 为样本，求 $\theta$ 的矩估计量.

    若已获得 $n = 10$ 的样本值如下,
    
    0.43  0.01  0.30  0.04  0.54
    
    0.14  0.99  0.18  0.98  0.02
    
    求 $\theta$ 的矩估计值.

??? note "Answer"
    (1)
    
    $$\mu = E(X) = \int_0^1 x \sqrt{\theta} x^{\sqrt{\theta}-1} dx = \frac{\sqrt{\theta}}{\sqrt{\theta}+1}$$
    
    $$\theta = (\frac{\mu_1}{1 - \mu_1})^2$$
    
    $$\hat{\theta} = (\frac{\overline{X}}{1-\overline{X}})^2$$
    
    (2)
    
    $$\overline{X} = \frac{1}{10} \sum\limits_{i=1}^{10} X_i = 0.363$$
    
    $$\hat{\theta} = (\frac{0.363}{1-0.363})^2 = 0.325$$

???+ question
    设总体 $X$ 服从均匀分布 $U(a,b)$ ，其中 $a,b$ 为未知参数， $X_1,\dots,X_n$ 为样本，求 $a,b$ 的矩估计量.

??? note "Answer"
    (1)求矩关于参数的函数

    $$\mu_1 = E(X) = \frac{a+b}{2}$$
    
    $$Var_2 = \frac{(b-a)^2}{12}$$
    
    (2)求参数关于矩的反函数
    
    $$a = \mu_1 - \sqrt{3Var_2}$$
    
    $$b = \mu_1 + \sqrt{3Var_2}$$
    
    (3)以样本矩 $A_1 = \overline{X}$ 代替总体矩 $\mu_1$ ， $B_2 = \frac{1}{n}\sum\limits_{i=1}^{n}(X_i - \overline{X})^2$ 代替总体方差 $Var_2$ ，得到参数的矩估计量
    
    $$\hat{a} = \overline{X} - \sqrt{3B_2}$$
    
    $$\hat{b} = \overline{X} + \sqrt{3B_2}$$

---

## 极大似然估计

**思想**:用“最像” $\theta$ 真值的值去估计 $\theta$ 换言之，在参数空间中找一个 $\theta$ 使得 $L(\theta)$ 达到最大。

---

设**离散型**总体 $X \sim p(x;\theta)$ ，$\theta \in \Theta$ , $\theta$ 未知. $X_1,\dots,X_n$ 为样本，其观察值为 $x_1,\dots,x_n$ ，则事件 $\{X_1 = x_1 , \dots , X_n = x_n\}$ 发生的概率为 

似然函数 ： $L(\theta) = \prod\limits_{i=1}^{n} p(x_i;\theta)$ 

极大似然原理 ： $L(\hat{\theta}(x_1,\dots,x_n)) = \max\limits_{\theta \in \Theta} L(\theta)$

称 $\hat{\theta}(x_1,\dots,x_n)$ 为 $\theta$ 的极大似然估计值，相应统计量 $\hat{\theta} = \hat{\theta}(X_1,\dots,X_n)$ 为 $\theta$ 的极大似然估计量(MLE).

---

**连续型**总体 $X$ 概率密度为 $f(x;\theta)$ ，$\theta \in \Theta$ ，$\theta$ 未知. $X_1,\dots,X_n$ 为样本，其观察值为 $(x_1,\dots,x_n)$ 邻域发生的概率为

$\prod\limits_{i=1}^{n} P(x_i < X_i < x_i + \Delta x_i) \approx \prod\limits_{i=1}^{n} f(x_i;\theta) \Delta x_i$ , $\Delta x_i$ 与参数 $\theta$ 无关.

因此，似然函数取为 $L(\theta) = \prod\limits_{i=1}^{n} f(x_i;\theta)$

---

极大似然原理 ： $L(\hat{\theta}(x_1,\dots,x_n)) = \max\limits_{\theta \in \Theta} L(\theta)$

???+ question
    设总体 $X$ 的概率分布律为:
    
    $$ \left(\begin{array}{cc}1&2&3\\ \theta & \frac{\theta}{2} & 1-\frac{3\theta}{2}\end{array}\right)$$
    
    其中 $0 < \theta < \frac{2}{3}$ ，现得到样本观测值 2，3，2，1，3，求 $\theta$ 的矩估计值与极大似然估计值.

??? note "Answer"
    (1)矩估计:

    $$\mu_1 = E(X) = 3 - \frac{5\theta}{2}$$
    
    $$\hat{\theta} = \frac{2(3 - \mu_1)}{5}$$
    
    $$\overline{X} = 2.2 \Rightarrow \hat{\theta} = 0.32$$
    
    (2)极大似然估计:
    
    $$L(\theta) = (\frac{\theta}{2}) \cdot (1 - \frac{3\theta}{2}) \cdot (\frac{\theta}{2}) \cdot \theta \cdot (1-\frac{3\theta}{2}) = \frac{1}{16} \theta^3 (2 - 3 \theta)^2$$
    
    可以直接求导或是取 $lnL(\theta)$ 求导，得到 $\hat{\theta} = 0.4$ .

---

- 说明：

    1. 未知参数可能不是一个,设为 $\theta = (\theta_1,\dots,\theta_k)$ ;

    2. 求 $L(\theta)$ 的最大值时，可转换为求 $\ln L(\theta)$ 的最大值, $\ln L(\theta)$ 称为对数似然函数.

    通常利用 $\frac{\partial \ln L(\theta)}{\partial \theta} = 0,i = 1,2,\dots,k$ 解得 $\hat{\theta_i}, i = 1,2,\dots,k$ 

    3. 若 $L(\theta)$ 关于某个 $\theta_i$ 是单调的，则 $\theta_i$ 的极大似然估计在其边界取得；

    4. 若 $\hat{\theta}$ 是 $\theta$ 的极大似然估计，则 $g(\theta)$ 的极大似然估计为 $g(\hat{\theta})$ .

???+ question
    设总体的密度为: $f(x;\theta) = \begin{cases} \sqrt{\theta}x^{\sqrt{\theta}-1},&0 \le x \le 1 \\ 0, & \text{otherwise}\end{cases} , \theta > 0$ 未知，其中 $X_1,\dots,X_n$ 为样本，求 $\theta$ 的极大似然估计值.

    若已获得 $n = 10$ 的样本值如下,
    
    0.43  0.01  0.30  0.04  0.54
    
    0.14  0.99  0.18  0.98  0.02
    
    求 $\theta$ 的极大似然估计值

??? note "Answer"
    $$L(\theta) = \prod_{i=1}^{n} f(x_i;\theta) = \theta^{\frac{n}{2}} (\prod\limits_{i=1}^{n} x_i)^{\sqrt{\theta}-1}$$

    $$\frac{\partial \ln L(\theta)}{\partial \theta} = \frac{n}{2} \cdot \frac{1}{\theta} + \frac{1}{2\sqrt{\theta}} \sum\limits_{i=1}^{n} \ln x_i = 0$$
    
    $$\Rightarrow \frac{n}{\sqrt{\theta}} = - \sum\limits_{i=1}^{n} \ln x_i$$
    
    $\theta$ 的极大似然估计量： $\hat{\theta} = \frac{n^2}{(\sum\limits_{i=1}^{n} \ln x_i)^2}$
    
    代入 $n = 10$ 的样本值，得 $\hat{\theta} = 0.305$ .

???+ question
    设总体 $X \sim N(\mu,\sigma^2)$ ，其中 $\mu$ 和 $\sigma^2$ 均未知，$X_1,\dots,X_n$ 为样本，求 $\mu$ 和 $\sigma^2$ 的极大似然估计值.

??? note "Answer"
    过程省略，这里直接给出结果。

    $$\hat{\mu} = \overline{X}$$
    
    $$\hat{\sigma}^2 = B_2$$

???+ question
    设总体 $X$ 服从均匀分布 $U(0,\theta)$ ，其中 $\theta$ 未知，$X_1,\dots,X_n$ 为样本，求 $\theta$ 的矩估计和极大似然估计值.

??? note "Answer"
    (1) 矩估计

    $$E(X) = \frac{\theta}{2}$$
    
    $$\hat{\theta} = 2\overline{X}$$
    
    (2) 极大似然估计
    
    当 $0 \le x_1, \dots, x_n \le \theta$ 时，似然函数为
    
    $$L(\theta) = \prod_{i=1}^{n} \frac{1}{\theta} = \frac{1}{\theta^n}$$
    
    可以发现关于 $\theta>0$ 的似然函数是单调递减的
    
    而 $\theta$ 的取值范围是 $\theta = \max\{x_1,\dots,x_n\}$
    
    $$\therefore \hat{\theta} = \max\{X_1,\dots,X_n\}$$

???+ question
    设总体 $X$ 服从均匀分布 $U(a,b)$ ，其中 $a$ 和 $b$ 均未知，$X_1,\dots,X_n$ 为样本
    
    (1)求 $a$ 和 $b$ 的极大似然估计.
    
    (2)求 $E(X)$ 的极大似然估计.
    
    (3)若已获得 $n = 5$ 的样本值如下，
    
    0.34  0.59  0.16  0.96  0.84
    
    求 $a$ , $b$ , $E(X)$ 的极大似然估计值.

??? note "Answer"
    ![image-20241205120245350](images/image-20241205120245350.png)
    ![image-20241205120258788](images/image-20241205120258788.png)

---

## 估计量的评价准则

### 四条评价准则：
1. 无偏性准则

2. 有效性准则

3. 均方误差准则

4. 相合性准则

### 定义

若参数 $\theta$ 的估计量 $\hat{\theta} = \hat{\theta}(X_1,X_2,\cdots,X_n)$ 满足 $E(\hat{\theta}) = \theta$ ，则称 $\hat{\theta}$ 为 $\theta$ 的无偏估计量.

若 $E(\hat{\theta}) \neq \theta$ ，那么 $E(\hat{\theta}) - \theta$ 称为估计量 $\hat{\theta}$ 的偏差.

若 $\mathop{lim}\limits_{n \to \infty} E(\hat{\theta}) = \theta$ ，则称 $\hat{\theta}$ 为 $\theta$ 的渐进无偏估计量.

---

- 无偏性的统计意义是指在**大量重复**试验下，由 $\hat{\theta}(X_1,\cdots.X_n)$ 所作的估计值的**平均恰是** $\theta$ ，从而无偏性保证了 $\hat{\theta}$ **没有系统误差**.

???+ question
    设总体 $X$ 的一阶和二阶矩存在， $E(X) = \mu$ , $D(X) = \sigma^2$ 

    (1)证明： 样本均值 $\overline{X}$ 和样本方差 $S^2$ 分别是 $\mu$ 和 $\sigma^2$ 的无偏估计.

    (2)判断： $B_2$ 是否为 $\sigma^2$ 的无偏估计？是否为 $\sigma^2$ 的渐进无偏估计？

??? note "Answer"
    (1) 因为 $X_1,\cdots,X_n$ 与 $X$ 同分布，所以

    $$E(\overline{X}) = E\left(\frac{1}{n}\sum\limits_{i=1}^n X_i\right) = \frac{1}{n}\sum\limits_{i=1}^n E(X_i) = \mu$$

    故 $\overline{X}$ 是 $\mu$ 的无偏估计.

    $$E(S^2) = E\left(\frac{1}{n-1}\sum\limits_{i=1}^n (X_i - \overline{X})^2\right) = \frac{1}{n-1}\sum\limits_{i=1}^n E((X_i - \overline{X})^2) = \sigma^2$$

    故 $S^2$ 是 $\sigma^2$ 的无偏估计.

    (2) 

    $$B_2 = \frac{n-1}{n}S^2$$

    $$E(B_2) = \frac{n-1}{n}E(S^2) = \frac{n-1}{n}\sigma^2 \neq \sigma^2$$

    故 $B_2$ 不是 $\sigma^2$ 的无偏估计.

    $$\mathop{lim}\limits_{n \to \infty} E(B_2) = \mathop{lim}\limits_{n \to \infty} \frac{n-1}{n}\sigma^2 = \sigma^2$$

    故 $B_2$ 是 $\sigma^2$ 的渐进无偏估计.

???+ question
    设总体 $X$ 服从均匀分布 $U(0,\theta)$ ， $X_1,\cdots,X_n$ 是来自 $X$ 的样本，$\theta$ 是未知参数

    (1)求 $\theta$ 的矩估计，判断是否无偏

    (2)求 $\theta$ 的最大似然估计，判断是否无偏

??? note "Answer"
    (1) 矩估计

    $$\mu_1 = E(X) = \frac{\theta}{2}$$

    $$\Rightarrow \theta = 2 \mu_1 \Rightarrow \hat{\theta} = 2\overline{X}$$

    $$E(\hat{\theta}) = E(2\overline{X}) = 2E(\overline{X}) = 2\mu = 2\cdot\frac{\theta}{2} = \theta$$

    故 $\hat{\theta}$ 是 $\theta$ 的无偏估计.

    (2) 最大似然估计

    $$L(\theta) = \prod\limits_{i=1}^n \frac{1}{\theta}I(0 < X_i < \theta)$$

    $$\hat{\theta_L} = X_{(n)} = max\{X_1,\cdots,X_n\}$$

    $$F_{X_{(n)}}(x) = [F_X(x)]^n = \begin{cases} 0, & x < 0 \\ (\frac{x}{\theta})^n, & 0 \leq x \leq \theta \\ 1, & x > \theta \end{cases}$$

    $$f_{X_{(n)}}(x) = \begin{cases} n\frac{x^{n-1}}{\theta^n}^n ,& 0 \leq x \leq \theta \\ 0, & x < 0, x > \theta \end{cases}$$

    $$E(\hat{\theta_L}) = E(X_{(n)}) = \int_0^\theta x f_{X_{(n)}}(x) dx = \int_0^\theta \frac{n}{\theta^n} x^{n} dx = \frac{n}{n+1}\theta \neq \theta$$

    故 $\hat{\theta_L = X_{(n)}}$ 是有偏的.

---

### 纠偏方法

如果 $E(\hat{\theta})  = a \theta + b$， $\theta \in \Theta$ ， 其中 $a,b$ 是常数，且 $a \neq 0$，则 $\frac{1}{a}(\hat{\theta} - b)$ 是 $\theta$ 的无偏估计.

---

## 有效性与均方误差

### 有效性准则

**定义**： 设 $\hat{\theta}_1,\hat{\theta}_2$ 是参数 $\theta$ 的两个无偏估计，若 $D(\hat{\theta}_1) \leq D(\hat{\theta}_2)$ ，对一切 $\theta \in \Theta$ 成立，且不等号至少对某一 $\theta \in \Theta$ 成立，则称 $\hat{\theta}_1$ 比 $\hat{\theta}_2$ 有效.

也即：**方差较小的无偏估计量是一个更有效的估计量。**

???+ question
    设总体为 $X$ , $E(X) = \mu$，$D(X) = \sigma^2$， $X_1,\cdots,X_n$ 是样本，对 $1 \le k \le n$ , $\hat{\theta}_k = \frac{1}{k} \sum\limits_{i=1}^k X_i$ ，为前 $k$ 个样本的样本均值，则 $\hat{\theta}_k$ 是 $\mu$ 的无偏估计.判断 $\hat{\theta}_1,\hat{\theta}_2,\dots, \hat{\theta}_n$ 中哪个最有效？

??? note "Answer"
    $$D(\hat{\theta}_k) = \frac{1}{k^2} D(\sum\limits_{i=1}^k X_i) = \frac{\sigma^2}{k}$$

    随着 $k$ 的增大，$D(\hat{\theta}_k)$ 越来越小，故 $\hat{\theta}_n$ 最有效.

???+ question
    设总体 $X \sim U[0,\theta]$，$X_1,\cdots,X_n$ 是样本，已知 $\theta$ 的两个无偏估计为 $\hat{\theta}_1 = 2\overline{X}, \hat{\theta}_2 = \frac{n+1}{n}X_{(n)}$，判断哪个更有效？

??? note "Answer"
    $$D(\hat{\theta}_1) = D(2\overline{X}) = \frac{4}{n} \cdot \frac{\theta^2}{12} = \frac{\theta^2}{3n}$$

    $$f_{X_{(n)}}(x) = \frac{n}{\theta^n} x^{n-1} ,0<x<\theta$$

    $$E(X_{(n)}^2) = \int_0^\theta \frac{nx^{n+1}}{\theta^n} dx = \frac{n}{n+2} \theta^2$$

    <div id = 'D2'></div>

    $$D(X_{(n)}) = E(X_{(n)}^2) - [E(X_{(n)})]^2 = \frac{n}{n+2} \theta^2 - \left(\frac{n+1}{n}\theta\right)^2 = \frac{\theta^2}{n(n+2)}$$

    $$D(\hat{\theta}_1) > D(\hat{\theta}_2)$$

    $$\therefore \hat{\theta}_2 \text{更有效.}$$

---

### 均方误差准则

**定义** ：

设 $\hat{\theta}$ 是 $\theta$ 的点估计，方差存在，则称 $E(\hat{\theta} - \theta)^2$ 为估计量 $\hat{\theta}$ 的均方误差（Mean Square Error，MSE），记为 $Mse(\hat{\theta})$.

若 $\hat{\theta}$ 是 $\theta$ 的无偏估计，则 $Mse(\hat{\theta}) = D(\hat{\theta})$.

!!! Info
    在实际应用中,均方误差准则比无偏性准则更重要.

???+ question
    利用均方误差准则，对用样本方差 $S^2$ 和样本二阶中心矩 $B_2$ 分别估计正态总体方差 $\sigma^2$ 时进行评价.

??? note "Answer"
    在正态总体下，

    $$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$$

    又因为 $S^2$ 是 $\sigma^2$ 的无偏估计，所以 
    
    $$Mse(S^2) = D(S^2) = \frac{2\sigma^4}{n-1}$$

    而对于 $B_2$，有

    $$Mse(B_2) = E[(B_2 - \sigma^2)^2] = D(B_2 - \sigma^2) + [E(B_2) - \sigma^2]^2 = D(B_2) + [E(B_2) - \sigma^2]^2$$

    $$= D(\frac{n-1}{n}S^2) + [E(\frac{n-1}{n}S^2) - \sigma^2]^2 = \frac{2n-1}{n^2} \sigma^4$$

    当 $n > 1$ 时有 $Mse(S^2) > Mse(B_2)$

    因此在均方误差准则下， $B_2$ 优于 $S^2$.

---

**Conclusion** ：在正态分布下，$D(S^2) = \frac{2\sigma^4}{n-1}$

??? note "证明"
    $$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$$

    $$D(\frac{(n-1)S^2}{\sigma^2}) = 2(n-1)$$

    $$\therefore D(S^2) = \frac{2\sigma^4}{n-1}$$

---

## 相合性

### 相合性准则

**定义**：设 $\hat{\theta}(X_1,\cdots,X_n)$ 为参数 $\theta$ 的估计量，若对于任意 $\theta \in \Theta$，当 $n \rightarrow +\infty$ 时

$$\hat{\theta_n} \mathop{\rightarrow}\limits^p \theta$$

即 $\forall \varepsilon > 0$，有 $\mathop{lim}\limits_{n \rightarrow +\infty} P(|\hat{\theta_n} - \theta| \ge \varepsilon) = 0$，则称 $\hat{\theta_n}$ 为 $\theta$ 的**相合估计量**或**一致估计量**.

---

- **一致性** 随着样本容量的增大，估计量越来越接近被估计的总体参数

$A_1,\dots,A_k$ 是 $\mu_1,\dots,\mu_k$ 的相合估计,即 $A_i \mathop{\rightarrow}\limits^p \mu_i$ ，且 $g(\mu_1,\dots,\mu_k)$ 是连续函数，则

$$g(A_1,\dots,A_k) \mathop{\rightarrow}\limits^p g(\mu_1,\dots,\mu_k)$$

即 $g(A_1,\dots,A_k)$ 也是 $g(\mu_1,\dots,\mu_k)$ 的相合估计.

???+ question
    设总体 $X$ 的 $k$ 阶矩 $E(X^k) = \mu_k(k \ge 2)$ 存在， $X_1,\cdots,X_n$ 是来自 $X$ 的样本，证明：

    (1)$A_l = \frac{1}{n}\sum\limits_{i=1}^n X_i^l$ 是 $\mu_l$ 的相合估计， $l = 1,\cdots,k$

    (2) $B_2,S^2$ 是 $D(X) = \sigma^2$ 的相合估计

    (3) $S$ 是 $\sigma$ 的相合估计

??? note "Answer"
    (1) 由辛钦大数定律知，对 $l = 1,\cdots,k$，有

    $$A_l = \frac{1}{n}\sum\limits_{i=1}^n X_i^l \mathop{\rightarrow}\limits^p \mu_l = E(X^l)$$

    (2)

    由强大数定律， $\overline{X}$ 和 $A_2$ 分别一致收敛于 $\mu_1$ 和 $\mu_2$

    $$B_2 = \frac{1}{n}\sum\limits_{i=1}^n (X_i - \overline{X})^2 = A_2 - \overline{X}^2$$

    $\therefore B_2,S^2$ 是 $\sigma^2$ 的相合估计

    (3)

    $S = \sqrt{S^2}$ 是 $\sigma$ 的相合估计

???+ question
    设总体 $X \sim U[0,\theta]$， $X_1,\cdots,X_n$ 是来自 $X$ 的样本，证明 $\hat{\theta_1} = 2\overline{X}$ 和 $\hat{\theta_2} = \frac{n+1}{n}\overline{X}$ 都是 $\theta$ 的相合估计

??? note "Answer"
    $$\hat{\theta_1} = 2\overline{X} = \mathop{\rightarrow}\limits^p 2E(X) = \theta$$

    $\therefore \hat{\theta_1}$ 是 $\theta$ 的相合估计

    $$E(\hat{\theta_2}) = \theta,D(\hat{\theta_2}) = \frac{\theta^2}{n(n+2)}$$

    (关于 $D(\hat{\theta_2})$ 已在前文证明过，如果忘记了可以移步[这里](#D2))

    由切比雪夫不等式， $\forall \varepsilon > 0$， 当 $n \to \infty$ 时，有

    $$P(|\hat{\theta_2} - \theta| \geq \varepsilon) \leq \frac{D(\hat{\theta_2})}{\varepsilon^2}  = \frac{\theta^2}{n(n+2)\varepsilon^2} \to 0$$

    所以 $\hat{\theta_2}$ 也是 $\theta$ 的相合估计

---

## 置信区间, 置信限

设 $X$ 是总体， $X_1,\cdots,X_n$ 是来自 $X$ 的样本， 区间估计的目的是找到两个统计量：

$$\hat{\theta_1} = \theta_1(X_1,\cdots,X_n),\hat{\theta_2} = \theta_2(X_1,\cdots,X_n)$$

使**随机区间** $(\hat{\theta_1},\hat{\theta_2})$ 以一定可靠程度盖住 $\theta$

---

### 定义一

设总体 $X$ 的分布函数 $F(x;\theta)$  $\theta$ 未知，对给定值 $\alpha$ ( $0 < \alpha < 1$ )，有两个统计量 $\theta_L = \theta_L(X_1,\cdots,X_n)$ 和 $\theta_U = \theta_U(X_1,\cdots,X_n)$，使得

$$P(\theta_L(X_1,\cdots,X_n)) < \theta < \theta_U(X_1,\cdots,X_n) \ge 1 - \alpha$$


称 $(\theta_L,\theta_U)$ 为 $\theta$ 的置信水平为 $1-\alpha$ 的双侧置信区间， $\theta_L$ 和 $\theta_U$ 分别称为双侧置信下限和双侧置信上限.

---

**说明：**

1. $\theta$ 是**确定**的值，未知。

2. $\theta_L$ 和 $\theta_U$ 是统计量，**随机**的，依赖于样本.

3. 置信区间 $(\theta_L,\theta_U)$ 是随机的，依赖于样本。样本不同，算出的区间也可能不同。

4. 对于有些样本观察值,区间覆盖 $\theta$ ，但对于于另一些样本观察值,区间则不能覆盖 $\theta$ .

???+ example
    设总体 $X \sim N(\mu,4)$ , $\mu$ 未知， $X_1,\cdots,X_4$ 是样本，则 $\overline{X} \sim N(\mu,1)$

    $$P(\overline{X} - 2 < \mu < \overline{X} + 2) = P(|\overline{X} - \mu| < 2) = 2 \Phi(2) - 1 = 0.9544$$

    $\Rightarrow (\overline{X} - 2,\overline{X} + 2)$ 是 $\mu$ 的置信水平为 $0.95$ 的置信区间

---

如果 $P\{\hat{\theta_L}(X_1,\dots,X_n) < \theta < \hat{\theta_U}(X_1,\dots,X_n)\} = 1 - \alpha$，则置信区间 $(\hat{\theta_L},\hat{\theta_U})$ 的含义为：

反复抽样多次(各次样本容量都为 n ).每个样本值确定一个区间 $(\hat{\theta_L},\hat{\theta_U})$ .每个这样的区间或包含 $\theta$ 的真值，或不包含 $\theta$ 的真值. 按照伯努利大数定律，在这些区间中，包含 $\theta$ 真值的比例约为 $1-\alpha$.

---

### 定义二

如果 $P\{\hat{\theta_L}(X_1,\dots,X_n) < \theta \} \ge 1 - \alpha$ ，则称 $\hat{\theta_L}$ 是参数为 $\theta$ 的置信水平为 $1-\alpha$ 的单侧置信下限.

如果 $P\{\theta < \hat{\theta_U}(X_1,\dots,X_n)\} \ge 1 - \alpha$ ，则称 $\hat{\theta_U}$ 是参数为 $\theta$ 的置信水平为 $1-\alpha$ 的单侧置信上限.

---

**单侧置信限和双侧置信区间的关系**

设 $\theta_L$ 是 $\theta$ 的置信水平为 $1-\alpha_1$ 的单侧置信下限， $\theta_U$ 是 $\theta$ 的置信水平为 $1-\alpha_2$ 的单侧置信上限，则 $(\theta_L,\theta_U)$ 是 $\theta$ 的置信水平为 $1-\alpha_1-\alpha_2$ 的双侧置信区间.

---

### 定义三

称置信区间 $[\hat{\theta_L},\hat{\theta_U}]$ 的平均长度 $E(\hat{\theta_U} - \hat{\theta_L})$ 为区间的**精确度**，精确度的一半为**误差限**。

- 在给定的样本容量下,置信水平和精确度是相互制约的。

---

### Neyman原则

在置信水平达到 $1-\alpha$ 的置信区间中，选精确度尽可能高的置信区间.

---

## 枢轴量法

设总体 $X$ 的分布有未知参数 $\theta$ ， $X_1,\dots,X_n$ 是来自 $X$ 的样本， 如何给出 $\theta$ 的置信度为 $1-\alpha$ 的双侧置信区间？

1. 找一个量 $G$ ,使 $G$ 分布已知

2. 找 $a < b$ ,使 $P(a < G(X_1,\dots,X_n) < b) \ge 1-\alpha$

因为要求 $\theta$ 的区间估计，所以 $G$ 应该是 $\theta$ 和样本 $X_1,\dots,X_n$ 的函数，而要求最小的区间长度时基本上是**等于**时取得。

3. 从 $a < G < b$ 解出 $\theta_L < \theta < \theta_U$

$(\theta_L,\theta_U)$ 就是 $\theta$ 的置信度为 $1-\alpha$ 的双侧置信区间

---

### 定义一

设总体 $X$ 有概率密度(或分布律) $f(x;\theta)$ ，其中 $\theta$ 是待估的未知参数.

设 $X_1,\dots,X_n$ 是来自 $X$ 的样本，称样本和未知参数 $\theta$ 的函数 $G(X_1,\dots,X_n;\theta)$ 为**枢轴量**。

如果 $G$ 的分布已知，不依赖于未知参数 $\theta$ .

!!! note "枢轴量和统计量的区别"
    (1)枢轴量是样本和待估参数的函数，其分布不依赖于任何未知参数；

    (2)统计量只是样本的函数，其分布常依赖于未知参数。

???+ question
    总体 $X \sim N(\mu,\sigma^2)$ ，$\mu,\sigma^2$ 为未知参数，$X_1,\dots,X_n$ 为样本，对 $\mu$ 进行区间估计.下面三个量中哪些是统计量？哪些是枢轴量？

    $\overline{X},\frac{\overline{X} - \mu}{\sigma/\sqrt{n}},\frac{\overline{X} - \mu}{S/\sqrt{n}}$

??? note "Answer"
    (1) $\overline{X}$ 是统计量，因为它是样本的函数；

    (2) $\frac{\overline{X} - \mu}{\sigma/\sqrt{n}}$ 不是统计量也不是枢轴量，因为它含有除了 $\mu$ 之外的未知参数 $\sigma$

    (3) $\frac{\overline{X} - \mu}{S/\sqrt{n}}$ 是枢轴量，因为它只是样本和 $\mu$ 的函数，服从 $t(n-1)$ 分布.

---

对枢轴量 $G$ ，满足 $P(a<G<b) \ge 1 - \alpha$ 的 $a,b$ 可能有很多，那么选择哪个呢？

1. 根据 Neyman 原则：求 $a$ 和 $b$ 使得区间长度最短；

2. 如果最优解不存在或比较复杂,对连续型总体,常取 $a,b$ 满足：

$$P(G(X_1,\dots,X_n;\theta) \le a) = P(G(X_1,\dots,X_n;\theta) \ge b) = \frac{\alpha}{2}$$

对于(2),构造置信区间三步骤也十分类似:

1. 构造枢轴量 $G(X_1,\cdots,X_n;\theta)$

2. 对连续型总体,找 $a<b$ 满足 $P(G \le a) = P(G \ge b) = \frac{\alpha}{2}$

3. 从 $a<G<b$ 解出 $\theta_L < \theta < \theta_U$

那么 $(\theta_L,\theta_U)$ 就是置信度为 $1-\alpha$ 的双侧置信区间，

$\theta_L$ 是 $\theta$ 的置信度为 $1-\frac{\alpha}{2}$ 的单侧置信下限，

$\theta_U$ 是 $\theta$ 的置信度为 $1-\frac{\alpha}{2}$ 的单侧置信上限.

!!! Info
    枢轴量 $G(X_1,\cdots,X_n;\theta)$ 的构造，通常从 $\theta$ 的点估计 $\hat{\theta}$ (如极大似然估计,矩估计等)出发，根据 $\hat{\theta}$ 的分布进行改造而得.

---

## 单个正态总体均值的区间估计

设总体 $X\sim N(\mu,\sigma^2)$ ， $X_1,\dots,X_n$ 为样本, $\overline{X}$ 和 $S^2$ 分别是样本均值和样本方差.置信水平为 $1-\alpha$ 

### 均值 $\mu$ 的置信区间

1. $\sigma^2$ 已知

$\overline{X}$ 是 $\mu$ 的无偏估计，取枢轴量 $\frac{\overline{X} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)$

设常数 $a<b$ 满足： $P(a < \frac{\overline{X} - \mu}{\sigma/\sqrt{n}} < b) = 1-\alpha$ 

等价于 $P\{\overline{X} - b\frac{\sigma}{\sqrt{n}},\overline{X} - a\frac{\sigma}{\sqrt{n}}\} \ge 1 - \alpha$

区间长度 $(b-a)\frac{\sigma}{\sqrt{n}}$ ,也即我们需要使得 $(b-a)$ 尽可能小

由于正态分布的性质可知， $a = -b = -Z_{\frac{\alpha}{2}}$ 时，区间的长度达到最短。

所以 $\mu$ 的双侧置信区间为： ($\overline{X} - \frac{\sigma}{\sqrt{n}}Z_{\frac{\alpha}{2}} , \overline{X} + \frac{\sigma}{\sqrt{n}}Z_{\frac{\alpha}{2}}$)

单侧置信下限为 (把 $\frac{\alpha}{2}$ 改为 $\alpha$ ) : $\overline{X} - \frac{\sigma}{\sqrt{n}}Z_{\alpha}$

单侧置信上限为： $\overline{X} + \frac{\sigma}{\sqrt{n}}Z_{\alpha}$

---

2. $\sigma^2$ 未知

此时我们用 $S^2$ 估计 $\sigma^2$ 得枢轴量 $G = \frac{\overline{X} - \mu}{S/\sqrt{n}} \sim t(n-1)$

同理可得， $\mu$ 的双侧置信区间为： ($\overline{X} - \frac{S}{\sqrt{n}}t_{\frac{\alpha}{2}}(n-1) , \overline{X} + \frac{S}{\sqrt{n}}t_{\frac{\alpha}{2}}(n-1)$)

单侧置信上限为： $\overline{X} + \frac{S}{\sqrt{n}}t_{\alpha}(n-1)$

单侧置信下限为： $\overline{X} - \frac{S}{\sqrt{n}}t_{\alpha}(n-1)$

??? note "简单证明一下 G 服从 t(n-1)"
    $$Z = \frac{\overline{X} - \mu}{\sigma / \sqrt{n}} \sim N(0, 1)$$

    $$\frac{(n-1) S^2}{\sigma^2} \sim \chi^2(n-1)$$

    $$\frac{S}{\sigma} = \sqrt{\frac{\frac{(n-1) S^2}{\sigma^2}}{n-1}} \sim \sqrt{\frac{\chi^2(n-1)}{n-1}}$$

    $$G = \frac{\frac{\overline{X} - \mu}{\sigma / \sqrt{n}}}{\frac{S}{\sigma}} = \frac{\overline{X} - \mu}{S / \sqrt{n}} \sim t(n-1)$$

---

### 成对数据均值差

例：为考察某种降压药的降压效果，测试了 n 个高血压病人在服药前后的血压（收缩压）分别为 $(X_1,Y_1),\dots,(X_n,Y_n)$ ，由于个人体质的差异， $X_1,\dots,X_n$ 不能看成来自同一个正态总体的样本，即 $X_1,\dots,X_n$ 是相互独立但不同分布的样本， $Y_1,\dots,Y_n$ 也是.另外对同一个个体， $X_i$ 和 $Y_i$ 也是不独立的.

作差值 $D_i = X_i - Y_i,i=1,\dots,n$ 则取消了个体的差异，仅与降压药的作用有关,因此可以将 $D_1,\dots,D_n$ 看作来自同一正态总体 $N(\mu_D,\sigma_D^2)$ 的样本，且相互独立。

$\mu_d$ 的置信水平为 $1-\alpha$ 的置信区间为： $(\overline{D} - t_{\frac{\alpha}{2}}(n-1)\frac{S_D}{\sqrt{n}},\overline{D} + t_{\frac{\alpha}{2}}(n-1)\frac{S_D}{\sqrt{n}})$

其中 $\overline{D} = \overline{X} - \overline{Y}$ ， $S_D^2 = \frac{1}{n-1}\sum_{i=1}^n (D_i - \overline{D})^2$

---

### 方差 $\sigma^2$ 的置信区间

$\mu$ 未知

设总体 $X\sim N(\mu,\sigma^2)$ ， $X_1,\dots,X_n$ 为样本, $\overline{X}$ 和 $S^2$ 分别是样本均值和样本方差.置信水平为 $1-\alpha$ 

由 $\sigma^2$ 的无偏估计 $S^2$ 想到枢轴量 $\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$

$$\therefore \frac{(n-1)S^2}{\chi^2_{\alpha/2}(n-1)} < \sigma^2 < \frac{(n-1)S^2}{\chi^2_{1-\alpha/2}(n-1)}$$

!!! ATTENTION
    上述双侧置信区间估计不是最优解

---

## 两个正态总体参数的区间估计

设样本 $(X_1,\dots,X_n)$ 和 $(Y_1,\dots,Y_m)$ 分别来自总体 $X\sim N(\mu_1,\sigma^2_1)$ 和 $Y\sim N(\mu_2,\sigma^2_2)$ ,并且它们相互独立. 样本均值和样本方差分别为 $\overline{X}$ , $\overline{Y}$ , $S^2_1$ , $S^2_2$ . 置信水平为 $1-\alpha$

---

### $\mu_1 - \mu_2$ 的置信区间

1. $\sigma^2_1 , \sigma^2_2$ 已知

由 $\mu_1 - \mu_2$ 的估计 $\overline{X} - \overline{Y}$ 想到枢轴量:

$$\frac{(\overline{X} - \overline{Y}) - (\mu_1 - \mu_2)}{\sqrt{\frac{\sigma^2_1}{n} + \frac{\sigma^2_2}{m}}} \sim N(0,1)$$

得置信区间: 

$$(\overline{X} - \overline{Y} \pm z_{\frac{\alpha}{2}}\sqrt{\frac{\sigma^2_1}{n} + \frac{\sigma^2_2}{m}})$$

---

2. $\sigma^2_1 = \sigma^2_2$ 未知

关于[(📝为什么使用 $S_w^2$)](https://melody12020831.github.io/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/Chapter6/#whySw)

以 $S_w^2 = \frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}$ 代替 $\sigma^2$ 得到枢轴量:

$$\frac{(\overline{X} - \overline{Y}) - (\mu_1 - \mu_2)}{S_w\sqrt{\frac{1}{n_1} + \frac{1}{n_2}}} \sim t(n_1+n_2-2)$$

得置信区间:

$$((\overline{X} - \overline{Y}) \pm t_{\frac{\alpha}{2}}(n_1+n_2-2)S_w\sqrt{\frac{1}{n_1} + \frac{1}{n_2}})$$

---

3. $\sigma^2_1 \neq \sigma^2_2$ 未知

以 $S_1^2$ 估计 $\sigma^2_1$ , $S_2^2$ 估计 $\sigma^2_2$ 得到枢轴量

- 当样本量 $n_1,n_2$ 都充分大时(一般要>30)

$$\frac{(\overline{X} - \overline{Y}) - (\mu_1 - \mu_2)}{\sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}}} \mathop{\sim}\limits^{\text{近似}} N(0,1)$$

得置信区间:

$$(\overline{X} - \overline{Y} \pm z_{\frac{\alpha}{2}}\sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}})$$

- 当样本量 $n_1,n_2$ 小时

$$\frac{(\overline{X} - \overline{Y}) - (\mu_1 - \mu_2)}{\sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}}} \mathop{\sim}\limits^{\text{近似}} t(k)$$

其中 $k \approx min(n_1-1,n_2-1)$

得近似置信区间:

$$(\overline{X} - \overline{Y} \pm t_{\frac{\alpha}{2}}(k)\sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}})$$

---

### $\frac{\sigma_1^2}{\sigma_2^2}$ 的置信区间

由 $\frac{\sigma_1^2}{\sigma_2^2}$ 的估计 $\frac{S_1^2}{S_2^2}$ 得枢轴量:

$$\frac{\frac{S_1^2}{S_2^2}}{\frac{\sigma_1^2}{\sigma_2^2}} \sim F(n_1-1,n_2-1)$$

$$\because F_{1 - \frac{\alpha}{2}}(n_1-1,n_2-1) \leq \frac{\frac{S_1^2}{S_2^2}}{\frac{\sigma_1^2}{\sigma_2^2}} \leq F_{\frac{\alpha}{2}}(n_1-1,n_2-1)$$

得置信区间:

$$(\frac{S_1^2}{S_2^2} \frac{1}{F_{\frac{\alpha}{2}}(n_1-1,n_2-1)} , \frac{S_1^2}{S_2^2} \frac{1}{F_{1 - \frac{\alpha}{2}}(n_1-1,n_2-1)})$$

??? note "需要简单证明吗🥺"
    $$\frac{(n_1-1)S_1^2}{\sigma_1^2} \sim \chi^2(n_1-1)$$

    $$\frac{(n_2-1)S_2^2}{\sigma_2^2} \sim \chi^2(n_2-1)$$

    $$\frac{\frac{(n_1-1)S_1^2}{\sigma_1^2 \cdot (n_1 - 1)}}{\frac{(n_2-1)S_2^2}{\sigma_2^2 \cdot (n_2-1)}} = \frac{\frac{S_1^2}{\sigma_1^2}}{\frac{S_2^2}{\sigma_2^2}} \sim F(n_1-1,n_2-1)$$

---

## Conclusion for 正态总体下常见枢轴量

### 单个正态总体 

$$N(\mu,\sigma^2)$$

$$\mu \text{的枢轴量} \begin{cases} \frac{\overline{X} - \mu}{\frac{\sigma}{\sqrt{n}}} \sim N(0,1) ,& (\sigma \text{已知}) \\ \frac{\overline{X} - \mu}{\frac{S}{\sqrt{n}}} \sim t(n-1) ,& (\sigma^2 \text{未知}) \end{cases}$$

$$\sigma^2 \text{的枢轴量} \frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1) ,(\mu \text{未知})$$

---

### 两个正态总体 

$$N(\mu_1,\sigma_1^2)$ 和 $N(\mu_2,\sigma_2^2)$$

$$\mu_1 - \mu_2 \text{的枢轴量} \begin{cases} \frac{(\overline{X}-\overline{Y}) - (\mu_1 - \mu_2)}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}} \sim N(0,1),& \sigma_1^2 , \sigma_2^2 \text{已知} \\ \frac{(\overline{X}-\overline{Y}) - (\mu_1 - \mu_2)}{S_w\sqrt{\frac{1}{n_1} + \frac{1}{n_2}}} \sim t(n_1 + n_2 - 2) ,& \sigma_1^2 = \sigma_2^2 \text{未知} \end{cases}$$

$$\frac{\sigma_1^2}{\sigma_2^2} \text{的枢轴量} \frac{\frac{S_1^2}{S_2^2}}{\frac{\sigma_1^2}{\sigma_2^2}} \sim F(n_1-1,n_2-1) ,(\mu_1,\mu_2 \text{未知})$$

---

## 置信区间例题汇总

???+ question "例题 1"
    某袋装食品重量(单位：克) $X\sim N(\mu,9)$ 现从一大批该产品中随机抽取 10 件,称得重量为：

    101.3 99.6 100.4 98.8 96.4 99.1 102.3 97.5 105.4 100.2

    求 $\mu$ 的置信水平为 95% 的双侧置信区间.

??? note "Answer"
    计算得 $\overline{X} = 100.1$

    所以， 样本均值服从 $N(100.1,\frac{9}{10})$

    查表得 $z_{0.025} = 1.96$

    $$\therefore (\overline{X} - z_{0.025}\sqrt{\frac{9}{10}},\overline{X} + z_{0.025}\sqrt{\frac{9}{10}}) = (98.24,101.96)$$

---

???+ question "例题 2"
    设新生儿体重(单位：克) $X \sim N(\mu,\sigma^2)$ ， $\mu,\sigma^2$ 未知， 现从某妇产医院随机抽查 16 名新生儿,称得重量为：

    3200 3050 2600 3530 3840 4450 2900 4180 
    
    2150 2650 2750 3450 2830 3730 3620 2270

    求 $\mu$ 的置信水平为 95% 的双侧置信区间.

??? note "Answer"
    计算得 $\overline{X} = 3165$ ， $s = 665.48$

    查表得 $t_{0.025}(15) = 2.1315$

    $$\therefore (\overline{X} - t_{0.025}(15)\sqrt{\frac{665.48^2}{16}},\overline{X} + t_{0.025}(15)\sqrt{\frac{665.48^2}{16}}) = (2845.4,3554.6)$$

---

???+ question "例题 3"
    某种产品的寿命(单位：千小时) $X \sim N(\mu,\sigma^2)$ ， $\mu,\sigma^2$ 未知， 现随机抽查 10 件产品进行寿命试验，测得：样本均值 $\overline{X} = 5.78$ ,样本标准差 $s = 0.92$ . 求 $\mu$ 的置信水平为 95% 的单侧置信下限.

??? note "Answer"
    查表得 $t_{0.05}(9) = 1.8331$

    $$\therefore \mu_{L} = \overline{X} - t_{0.05}(9)\sqrt{\frac{s^2}{n}} = 5.25$

---

???+ question "例题 4"
    某市随机抽取 1500 个家庭，调查知道其中有 375 家拥有私家车.试根据此调查结果，求该市拥有私家车比例 p 的置信水平为 95% 的近似置信区间.

??? note "Answer"
    计算得 $\hat{p} = \overline{x} = \frac{375}{1500} = 0.25$ , $s^2 = \hat{p}(1-\hat{p}) = 0.1875$

    $$\therefore (\overline{x} - z_{0.025}\sqrt{\frac{s^2}{n}},\overline{x} + z_{0.025}\sqrt{\frac{s^2}{n}}) = (0.228,0.272)$$

---

???+ question "例题 5 成对数据情形"
    为评价某种训练方法是否能有效提高大学生的立定跳远成绩,在某大学随机选中 16 名学生，测量他们的立定跳远成绩(三次中最好成绩)，经过三个月训练后再测量他们的成绩。实验数据如下.

    |编号| 1| 2| 3| 4| 5| 6| 7| 8|
    |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
    |训练前|189|193|230| 210| 198| 230 |210| 198|
    |训练后 |220 |195 |234 |231 |225| 228 |238| 240|
    |数据差| 31| 2 | 4 | 21 | 27 | 13 | 4 | 16|

    |编号| 9| 10| 11| 12| 13| 14| 15| 16|
    |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
    |训练前| 209| 220| 195| 211| 228| 216| 212| 231|
    |训练后| 221| 218| 214| 236| 248| 248| 230| 245|
    |数值差| 12 | -2 | 19 | 25 | 20 | 32 | 18 | 14|

    假设训练前后成绩差 $D\sim N(\mu_D, \sigma^2_D)$ ，求 $\mu_D$ 的置信水平为 95% 的双侧置信区间.

??? note "Answer"
    计算得 $\overline{D} = 16$ , $s_d = 10.24$

    查表得 $t_{0.025}(15) = 2.1315$

    $$\therefore (\overline{D} - t_{0.025}(15)\sqrt{\frac{s^2_D}{n}},\overline{D} + t_{0.025}(15)\sqrt{\frac{s^2_D}{n}}) = (10.5,21.5)$$

---

???+ question "例题 6"
    一个园艺科学家正在培养一个新品种的苹果这种苹果除了口感好和颜色鲜艳以外，另一个重要特征是单个重量差异不大.为了评估新苹果，她随机挑选了 25 个测试重量 (单位：克) 其样本方差为 $s^2 = 4.25$ 试求 $\sigma^2$ 的置信度为 95% 的双侧置信区间和单侧置信上限.

??? note "Answer"
    查表得 $\chi^2_{0.025}(24) = 39.4, \chi^2_{0.975}(24) = 12.4, \chi^2_{0.95}(24) = 13.85$

    $$\therefore (\frac{(n-1)s^2}{\chi^2_{0.025}(n-1)}, \frac{(n-1)s^2}{\chi^2_{0.975}(n-1)}) = (2.59,8.23)$$

    $$\therefore \frac{(n-1)s^2}{\chi^2_{0.95}(n-1)} = 7.36$$

---

???+ question "例题 7"
    两台机床生产同一型号滚珠.从甲机床生产的滚珠中取 8 个，从乙机床生产的滚珠的中取 9 个.测得这些滚珠的直径（单位：毫米）如下：

    甲机床: 15.0 14.8 15.2 15.4 14.9 15.1 15.2 14.8

    乙机床: 15.2 15.0 14.8 15.1 14.6 14.8 15.1 14.5 15.0

    设两机床生产的滚珠直径分别为 $X$ 和 $Y$ ，且 $X \sim N(\mu_1, \sigma^2_1), Y \sim N(\mu_2, \sigma^2_2)$ ，求置信水平为 0.9 的双侧置信区间.

    (1) $\sigma_1 = 0.18, \sigma_2 = 0.24$ 求 $\mu_1 - \mu_2$ 的置信区间

    (2) 若 $\sigma_1 = \sigma_2$ 且未知，求 $\mu_1 - \mu_2$ 的置信区间

    (3) 若 $\sigma_1 \neq \sigma_2$ 且未知，求 $\mu_1 - \mu_2$ 的置信区间

    (4) 若 $\mu_1, \mu_2$ 均未知，求 $\frac{\sigma_1^2}{\sigma_2^2}$ 的置信区间

??? note "Answer"
    计算得 $\overline{X} = 15.05, S_1^2 = 0.0457, \overline{Y} = 14.9 , S_2^2 = 0.0575$

    1. 查表得 $z_{0.05} = 1.645$

    $$\therefore (\overline{X} - \overline{Y} \pm z_{\frac{\alpha}{2}}\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}) = (-0.018,0.318)$$

    2. 查表得 $t_{0.05}(15) = 1.7531$

    计算得 $S_w = 0.228$

    $$\therefore (\overline{X} - \overline{Y} \pm t_{\frac{\alpha}{2}}(n_1+n_2-2)\sqrt{\frac{S_w^2}{n_1} + \frac{S_w^2}{n_2}}) = (-0.044,0.344)$$

    3. $k = min(n_1-1, n_2-1) = 7$

    查表得 $t_{0.05}(7) = 1.895$

    $$\therefore (\overline{X} - \overline{Y} \pm t_{\frac{\alpha}{2}}(k)\sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}}) = (-0.058,0.358)$$

    4. 查表得 $F_{0.05}(7,8) = 3.50, F_{0.95}(7,8) = 0.268$

    $$\therefore \left(\frac{\S_1^2}{\S_2^2} \frac{1}{F_{\frac{\alpha}{2}}(n_1-1, n_2-1)} , \frac{\S_1^2}{\S_2^2} \frac{1}{F_{1-\frac{\alpha}{2}}(n_1-1, n_2-1)}\right) = (0.227,2.965)$$

!!! info
    由(1)、（2）和（3）求得的三个区间都包含了 0 ，说明两机床生产的滚珠的平均直径没有显著差异.

    (4)中所求置信区间包含 1 ,说明两机床生产的滚珠直径的方差没有显著差异.

---
