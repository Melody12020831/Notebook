---
statistics: True
comments: true
---

# Chapter 7 矩估计

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

---
