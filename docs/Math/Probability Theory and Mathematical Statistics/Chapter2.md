---
comments: true
statistics: True
---

# Chapter 2 随机变量及其分布

定义：设随机试验的样本空间为$S = \{e\}$，若$X=X(e)$为定义在样本空间$S$上的实值单值函数，则称X=X(e)为随机变量。

- 常用大写字母 X,Y,Z*X*,*Y*,*Z* 来表示**随机变量**
- 用小写字母 x,y,z*x*,*y*,*z* 表示其**取值**。

---

## 离散型随机变量

定义：取值至多可数的随机变量

若其可能取值为 $\{x_i\}$，则称 $P\{X=x_k\}=p_k$,$k=1,2,\dots $ 为$X$ 的**概率分布律(probability mass function)**，也可以用列表的方式表达。
因为样本空间 $S=\{X=x_1,X=x_2,\dots,X=x_n \dots \}$中各样本点两两不相容，所以：
$$1 = P(S) = \sum_{i=1}^{+\infty}P(X = x_i) = \sum_{i=1}^{+\infty}p_i$$

---

### 0-1分布/两点分布

如果随机变量 X 的概率分布律为：

|  X   |  0   |  1   |
| :--: | :--: | :--: |
|  P   |  p   | 1-p  |

则称 X 为服从**参数为 p 的 0−1分布**，也称为**两点分布**，并记为 $X∼B(1,p)$ 或者 $X∼0−1(p)$

它的分布律还可以写为

$$P(X = k) = p^k(1-p)^{1-k},k = 0,1$$

---

### 二项分布

定义**Bernoulli试验**：在$ n $次独立重复试验中，每次只有$ A$  和 $\overline{A}$ 两种结果，且概率不变，则这一系列试验为伯努利试验。

若随机变量 $X$表示 $ n $**重贝努力实验中事件A发生的次数**，其概率分布律为：

$$P(X = k) = C_n^k p^k(1-p)^{n-k},k = 0,1,\dots,n$$

则称 X 为服从**参数为** $(n,p)$ **的二项分布(binomial distribution)**，并记为 $X∼B(n,p)$

根据二项式定理，二项分布有如下性质：

$$\sum_{k=0}^n C_n^kp^k(1-p)^{n-k} = 1$$

???+ question 
	甲和乙比赛,甲的实力更强一点。每一局甲赢的概率为*p*,这里$0.5\le p \le1$。设各局胜负相互独立。设*k*是一正整数.问：对甲而言，$2k-1$局$k$胜制有利还是$2k+1$局$k+1$胜制有利？

   <details>
   <summary>答案</summary>
   <img src = "Math/Probability Theory and Mathematical Statistics/概率论与数理统计.assets/image-20241010152832029.png">
   <img src = "Math/Probability Theory and Mathematical Statistics/概率论与数理统计.assets/image-20241010152839373.png">
   </details>

---

### 泊松分布

若随机变量X的概率分布律为

$$P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!},k = 0,1,\dots,\lambda > 0$$

称X服从参数为λ的泊松分布，记$$X ∼ P(\lambda)$$

**二项分布与泊松分布有以下近似公式**：当$n >10,p <0.1$时，其中，$\lambda = np$

$$C_n^k p^k(1-p)^{n-k} \approx \frac{\lambda^k e^{-\lambda}}{k!}$$

---

### 超几何分布

若随机变量X的概率分布律为

$$P(X = k) = \frac{C_a^{k}C_b^{n-k}}{C_N^n},k = l_1,l_1+1,\dots,l_2$$

其中，$l_1 = max(0,n-b),l_2 = max(a,n)$则称$X$服从超几何分布，并记为 $X∼H(n,a,p)$

---

### 几何分布

若随机变量X的概率分布律为

$$P(X=k) = p(1-p)^{k-1},k = 1,2,\dots,0<p<1$$

则称$X$服从参数为$p$的几何分布

---

### 巴斯卡分布

若随机变量X的概率分布律为

$$P(X=k)=C_{k-1}^{r-1}p^r(1-p)^{k-r},k=r,r+1,\dots,0<p<1$$

则称$X$服从参数为$(r,p)$的巴斯卡分布

---

## 随机变量的分布函数

定义：随机变量X，若对任意实数x，函数$F(x) = P(X \le x)$称为X 的分布函数。

当 $X$ 为**离散型随机变量**时，设 $X$ 的概率分布律为 $P\{X=x_i\}=p_i,i=1,2,\dots$ 则 $X$的分布函数为：

$$F(x)=P\{X\le x\}=\sum_{x_i \le x}P\{X=x_i\}$$

### $F(x)$的性质

1. $F(x)$ 单调不减；
2. $0 \le F(x) \le 10$ 且 $F(−\infty)=0$，$F(+\infty)=1$；
3. $F(x)$ 右连续，即 $F(x+0)=F(x)$；
4. $P(a< X \le b)=F(b)−F(a)$；
5. 分布函数$F(x)$在$x = x_k$处有跳跃，其跳跃值为$p_k = P(X=x_k)$

---

## 连续型随机变量及其密度函数

如果对于随机变量 $X$ ，其**分布函数**为 $F(x)$，若存在一个非负的实函数 $f(x)$，使对于**任意实数** $x$，有：

$$F(x) = \int_{-\infty}^{+\infty}f(x)dx = 1$$

则称 $X$ 为**连续型随机变量**，并且称 $f(x)$ 为 $X$ 的**概率密度函数**，简称为**密度函数**。

关于 f(x)*f*(*x*) 有以下结论：

1. $f(x)\ge 0$；
2. $\int_{\infty}^{+\infty}f(x)dx = 1$；
3. $\forall x_1,x_2 \in R (x_1 < x_2),P\{x_1 < X \le x_2 \} = F(x_2) - F(x_1) = \int_{x_1}^{x_2}f(t)dt$;
4. 在$f(x)$ 的连续点 $x$ 处，$F′(x)=f(x)$
5. $P\{X=a\}=0$，即连续型随机变量任取一个定值的概率为零，因此连续型随机变量落在开区间与相应闭区间上的概率相等；
6. 与物理学中的质量线密度的定义相类似$P( x < X \le x+ \Delta x) \approx  f( x) \cdot x$

???+ question 
	设 $A,B$ 为随机事件，若 $P(A)=1$，则 $A$为必然事件吗？若 $P(B)=0$，则 $B$ 为不可能事件吗？若$P(AB) = 0$ ，则 $A$ 与 $B$ 不相容吗？

<details>
    <summary>答案</summary>
<img src = "Math/Probability Theory and Mathematical Statistics/概率论与数理统计.assets/image-20241010153109801.png">
	<p>1. 空集发生的概率为0，但0概率事件不一定是空集。例如在(0,1)上取0.5</p>
    <p>2. 一个事件发生的概率为1，但不是整个样本空间（去掉0概率那个点即可）</p>
    <p>3. AB互斥则P(AB)= 0，但反之不成立。例如A为在(0,1)上去掉0.4，B为在(0,1)上取出0.5</p>
</details>

---

### 均匀分布

设随机变量 $X$就有密度函数：

$f(x)=\begin{cases}\frac{1}{b−a},&x\in (a,b)\\0,&else\end{cases}$

则称 $X$ 服从区间 $(a,b)$上的均匀分布，并记为 $X∼U(a,b)$

而得到对应的分布函数为：

$$F(x)=\begin{cases}0,&x<a\\\frac{x−a}{b−a},&a\le x\le b\\1,&x\ge b\end{cases}$$

???+ question 
	杭州某长途汽车站每天从早上6点（第一班车）开始，每隔30分钟有一班车开往上海。王先生在早上6:20过X分钟到达车站，设X服从（0，50）上的均匀分布，
	（1）求王先生候车时间不超过15分钟的概率；
	（2）如果王先生一月中有两次按此方式独立地去候车，求他一次候车不超过15分钟，另一次候车大于10分钟的概率。

<details> 
<summary>提示</summary>
<p><mark>什么时候可以相加？</mark></p>
<p>互斥时才能相加，当这两个事件可以同时发生时就要注意。</p>
</detais>
<details>
<summary>答案</summary>
<img src = "Math/Probability Theory and Mathematical Statistics/概率论与数理统计.assets/image-20241010153141624.png">
</details>

---

### 指数分布

若随机变量 $X$ 具有密度函数：

$$f(x) = \begin{cases}\lambda e^{-\lambda x},&x > 0\\0,&x \le 0\end{cases}$$

其中 $\lambda > 0$，则称 $X$ 服从**参数为** $\lambda$**的指数分布(exponential distribution)**，记为 $X∼E(\lambda)$或 $X ∼ Exp(\lambda)$

指数分布对应的分布函数为：

$$F(x)=\int_{-\infty}^{x}f(t)dt=\begin{cases}1-e^{-\lambda x}, &x>0\\0,&x \le 0\end{cases}$$

指数分布具有无记忆性，即 $P(X>s∣X>t_0)=P(X>s−t_0)$。

???+ question 
	某大型设备在任何长度为$t$的区间内发生故障的次数$N(t)$服从参数为$\lambda t$的Poisson分布，记设备无故障运行的时间为 $T$ .
	(1)求$T$ 的概率分布函数；
	(2)已知设备无故障运行10个小时，求再无故障运行8个小时的概率。

<details>
    <summary>答案</summary>
<img src = "Math/Probability Theory and Mathematical Statistics/概率论与数理统计.assets/image-20241010153212016.png">
</details>

---

### 正态分布

如果随机变量 $X$ 具有密度函数：

$$f(x)=\frac{1}{\sqrt{2\pi}\sigma} e^{−\frac{(x−\mu)^2}{2\sigma^2}},∣x∣< +\infty$$

其中 $\sigma > 0 ,∣\mu∣<+\infty$为常数，则称 $X$ 服从**参数为** $(\mu ,\sigma )$ **的正态分布(normal distribution / Gauss distribution)**，或者称 $X$ 为**正态变量**，记为 $X∼N(\mu ,\sigma^2)$。

其对应的分布函数为：

$$F(x) = \int_{−\infty}^{x}\frac{1}{\sqrt{2\pi}\sigma} e^{−\frac{(t−\mu)^2}{2\sigma^2}}dt$$  

在上面出现的式子中，$\mu$ 为**位置参数**，决定了分布图像的对称轴位置；$\sigma$ 为**尺度参数**，决定了形状，$\sigma$  越小，图像越集中。

特别的，当 $\mu = 0, \sigma = 1$时，如果记这时的正态变量为 $Z$，即 $Z∼N(0,1)$ 则它服从**标准正态分布(standard normal distribution)**。则其**密度函数**为：

$$\varphi(x)=\frac{1}{\sqrt{2\pi}} e^{−\frac{x^2}{2}},∣x∣< +\infty$$

则对应的**分布函数**为：

$$\Phi(x) = \int_{−\infty}^{x}\frac{1}{\sqrt{2\pi}} e^{−\frac{t^2}{2}}dt$$  

- 则显然有$\Phi(x) + \Phi(-x) = 1$

而对于不是标准正态分布的正态分布，我们可以通过线性变换（标准化）来转换为标准正态分布：

- 若 $X∼N(\mu ,\sigma^2)$，则 $P\{a<X<b\}=P\{\frac{a−\mu}{\sigma}< \frac{X−\mu }{\sigma}< \frac{b−\mu}{\sigma} \}= \Phi (\frac{b−\mu }{\sigma})− \Phi (\frac{a−\mu}{\sigma})$
- 特别的：若  $X∼N(\mu ,\sigma^2)$，则 $P{∣X− \mu ∣< k \sigma }=\Phi (k)− \Phi (−k)= 2 \Phi (k) −1$
- 若 $X∼N(\mu ,\sigma^2)$，则 $Y=aX+b∼N(a\mu +b,a^2\sigma^2)$

---

## 随机变量函数的分布

关键是找出等价事件。

1. 若Y为离散量

   先写出Y的可能取值$y_1,y_2,\dots,y_j,\dots$，再找出$(Y = y_j)$的等价表达事件$(X \in D)$，得$P(Y = y_i) = P(X \in D)$

2. 若Y为连续量

   先写出Y的概率分布函数$F_Y(y) = P(Y \le y)$，找出$(Y\le y)$的等价事件$(X \in D)$，得$F_Y(y) = P(X \in D)$，再求出Y的概率密度函数$f_Y(y)$；

如果：

- 随机变量 $Y=g(X)$；
- 函数 $y=g(x)$ 为一严格单调（增/减）函数，并且可微；

则记 $y=g(x)$ 的反函数为 $x=h(y)$，得到 $Y$的密度函数为：

$$f_Y(y)= \begin{cases}f_X(h(y)) \cdot∣h′(y)∣,&y \in D\\ 0,&y\notin D\end{cases}$$

其中 $D$ 为 $y=g(x)$ 的值域。
---

