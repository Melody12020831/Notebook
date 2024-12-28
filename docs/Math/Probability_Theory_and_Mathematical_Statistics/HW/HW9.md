---
statistics: True
comments: true
---

# HW9(习题四、五)

## B24

???+ question
    (接第B20题)(1)求X与|X|的相关系数，并判断两者是否相关；

    (2)判断X与|X|是否相互独立.

??? Note "Answer"
    1. $Cov(X,|X|)=E(X|X|)−E(X)E(|X|) = 0$所以$\rho = 0$， $X$ 与 $|X|$ 不相关；

    2. 

    $$f_X(x) = \frac{1}{2} e^{-|x|},-\infty < x < +\infty$$

    $$f_{|X|}(y) = P\{|X| \le y\}\text{的导数} = e^{-y}, 0 \le y < +\infty$$

    $$f_{X,|X|}(x,y) = \begin{cases}0.5 \cdot e^{-y} , & x = y \text{或} x = -y , y \ge 0\\ 0,& \text{其他} \end{cases}$$

    而$f_{X,|X|}(x,y) \neq f_X(x) \cdot f_{|X|}(y)$，所以不独立

---

## B28

???+ question
    设随机变量 $X_1,X_2,\dots,X_n$ 均服从标准正态分布并且相互独立。记$S_k = \sum\limits_{i=1}^k X_i,T_k = \sum\limits_{j = n_0+1}^{n_0+k}X_j$，其中$1 \le n_0 < k < n_o+k \le n$，求 $S_k$ 与 $T_k$ 的相关系数

??? Note "Answer"
    $$\rho(S_k, T_k) = \frac{\operatorname{Cov}(S_k, T_k)}{\sqrt{\operatorname{Var}(S_k) \cdot \operatorname{Var}(T_k)}}$$

    方差：$\operatorname{Var}(X_i) = 1 \quad \text{且} \quad \operatorname{Cov}(X_i, X_j) = 0 \, (i \neq j)$

    于是：$\operatorname{Var}(S_k) = \operatorname{Var}\left(\sum_{i=1}^k X_i\right) = \sum_{i=1}^k \operatorname{Var}(X_i) = k$

    同理，$T_k = \sum_{j=n_0+1}^{n_0+k} X_j$ ，且随机变量仍然相互独立，因此：

    $$\operatorname{Var}(T_k) = \operatorname{Var}\left(\sum_{j=n_0+1}^{n_0+k} X_j\right) = \sum_{j=n_0+1}^{n_0+k} \operatorname{Var}(X_j) = k$$

    随机变量的协方差定义为：$\operatorname{Cov}(S_k, T_k) = \mathbb{E}[S_k T_k] - \mathbb{E}[S_k]\mathbb{E}[T_k]$

    由于 $X_i$ 是标准正态分布，因此 $\mathbb{E}[S_k] = \mathbb{E}[T_k] = 0$，从而：$\operatorname{Cov}(S_k, T_k) = \mathbb{E}[S_k T_k]$ 利用独立性和交叉项的性质，仅保留 $X_i$ 同时出现在两个求和中的项：

    $$\mathbb{E}[S_k T_k] = \sum_{i=1}^k \sum_{j=n_0+1}^{n_0+k} \mathbb{E}[X_i X_j] = \text{重叠项的数量}$$

    因此：$\operatorname{Cov}(S_k, T_k) = k - n_0 \Rightarrow \rho(S_k, T_k) = \frac{k - n_0}{k}$

---

## B29

???+ question
    设 $X ∼ N(0,1)$, Y的可能取值为 $\pm 1$，且$P\{Y=1\} = p \ (0<p<1)$.设 $X$ 与 $Y$ 相互独立，记 $\xi = X \cdot Y$

    (1)证明：$\xi ∼ N(0,1)$;

    (2)计算 $\rho_{X_{\xi}}$ ，并判断 $X$ 与 $\xi$ 的相关性和独立性.

??? Note "Answer"
    1. 当 $Y = 1$ 时， $\xi = X$ ；当 $Y = -1$ 时，$ \xi = -X$ 。

    于是，混合分布：
    
    $$f_\xi(x) = P(Y=1) f_X(x) + P(Y=-1) f_X(-x) = p \cdot \frac{1}{\sqrt{2\pi}} e^{-x^2/2} + (1-p) \cdot \frac{1}{\sqrt{2\pi}} e^{-(-x)^2/2} = \frac{1}{\sqrt{2\pi}} e^{-x^2/2}.$$

    因此， $\xi \sim N(0,1).$

    2. 
    - $\operatorname{Var}(X) = \operatorname{Var}(\xi) = 1$ ，因为 $X \sim N(0,1)$ 且 $\xi \sim N(0,1)$ 。
    - 因此：$\rho_{X \xi} = \operatorname{Cov}(X, \xi).$

    $$ \operatorname{Cov}(X, \xi) = \mathbb{E}[X \cdot \xi] - \mathbb{E}[X] \mathbb{E}[\xi] = \mathbb{E}[X \cdot \xi] = \mathbb{E}[X \cdot (X \cdot Y)] = \mathbb{E}[X^2 \cdot Y] = \mathbb{E}[X^2] \cdot \mathbb{E}[Y]$$

    由 $\mathbb{E}[X^2] = \operatorname{Var}(X) + (\mathbb{E}[X])^2 = 1$ ，而 $\mathbb{E}[Y] = p \cdot 1 + (1-p) \cdot (-1) = 2p - 1$。

    因此：$\operatorname{Cov}(X, \xi) = 1 \cdot (2p - 1) = 2p - 1 \rightarrow \rho_{X_\xi} = 2p - 1$

    当 $p=\frac{1}{2}$ 时， $X$与$\xi$不相关；当 $p > \frac{1}{2}$ 时， $X$与$\xi$正相关；当 $p < \frac{1}{2}$ 时， $X$与$\xi$负相关；

    取 $p = 0.75$ ，则 $\mathbb{E}[X \cdot \xi] = 2 \cdot 0.75 - 1 = 0.5$ 

    此时 $\mathbb{E}[X] = 0$ ， $\mathbb{E}[\xi] = 0$ ， $\mathbb{E}[X \cdot \xi] \neq \mathbb{E}[X] \cdot \mathbb{E}[\xi]$

    因此 $X$与$\xi$不独立。

    当 $0 < p <1$ 时， $X$与$\xi$不独立；

!!! Info
    不独立是需要举反例或者写严谨的证明来说明的，不能用显然或者xx是xx的函数这种不严格的说法。

    在p＝1/2的时候，这里只是分别满足正态分布（不满足联合正态分布）所以不能拿相关系数＝0判断独立性，这里的不独立是需要详细说明，不能一笔带过。

---

## B33

???+ question
    已知三维正态变量 $X = (X_1,X_2,X_3)^T \sim N(a,B)$ ，其中

    $$a = (0,0,1)^T, B = \begin{pmatrix} 1 & 2 & -1 \\ 2 & 16 & 0 \\ -1 & 0 & 4 \end{pmatrix}$$

    (1)写出 $X$ 的每个分量的分布；

    (2)判别 $X_1,X_2,X_3$ 的相关性与独立性；

    (3)若 $Y_1 = X_1 - X_2$ ， $Y_2 = X_3 - X_1$ ，求 $Y = (Y_1,Y_2)^T$ 的分布.

??? Note "Answer"
    (1) $X_1 \sim N(0,1), X_2 \sim N(0,16), X_3 \sim N(1,4)$

    (2)

    $$Cov(X_1,X_2) = 2 \quad Cov(X_1,X_3) = -1 \quad Cov(X_2,X_3) = 0$$

    $\rho_{X_1X_2} = 1$ $X_1,X_2$ 相关不独立
    
    $\rho_{X_1X_3} = -\frac{1}{\sqrt{2}}$ $X_1,X_3$ 相关不独立
    
    $\rho_{X_2X_3} = 0$ $X_2,X_3$ 不相关且独立

    $X_1,X_2,X_3$ 相关且不独立

    (3)

    $$E(Y_1) = 0 \quad E(Y_2) = 1$$

    $$Cov(Y_1,Y_1) = 13 \quad Cov(Y_2,Y_2) = 7 \quad Cov(Y_1,Y_2) = 0$$

    $$\therefore Y \sim N(\mu, \varepsilon)$$

    $$\mu = (0,1)^T \quad \varepsilon = \begin{pmatrix} 13 & 0 \\ 0 & 7 \end{pmatrix}$$

---

## B34

???+ question
    设有一煤矿一天的产煤量 $X$ (以 $10^4t$ 计)服从正态分布 $N(1.5,0.1^2)$ .设每天产量相互独立，一个月按30天计，求一个月总产量超 $46 \times 10^4t$ 的概率.

??? Note "Answer"
    30天则 $N(45,0.3) \rightarrow 1 - \Phi (\sqrt{\frac{10}{3}}) \approx 0.0339$

---

## B3

???+ question
    设随机变量 $X_i$ 的密度函数

    $$f_i(x) = \begin{cases}\frac{i|x|^{i-1}}{2},&|x| \le 1 \\ 0, & \text{其他}\end{cases}, i=1,2,\dots,n$$

    且 $X_1,X_2,\dots,X_n$ 相互独立。令 $Y_n = X_1X_2\dots X_n$，用切比雪夫不等式求使 $P\{|Y_n| \ge \frac{1}{2}\} \le \frac{1}{9}$ 成立的最小 $n$。

??? Note "Answer"
    $$E(X_i) = 0 \rightarrow E(Y_n) = 0$$
    
    $$E(X_i^2) = \frac{i}{i+2} \rightarrow Var(X_i) = \frac{i}{i+2} \rightarrow Var(Y_n) = \frac{2}{(n+1)(n+2)}$$

    $$P\{|Y_n| \ge \frac{1}{2}\} \le 4Var(Y_n) \le \frac{1}{9} \Rightarrow n_{min} = 7$$

---

## B4

???+ question
    设随机变量序列 ${X_n，n\ge 1}$独立同分布，都服从U(0,a)，其中a>0，令$X_{(n)} = max_{1\le i \le n}X_i$，证明: $X_{(n)} \xrightarrow{P} a ,n \rightarrow \infty$

??? Note "Answer"
    1. 要证$\mathop{\lim}\limits_{n \to \infty} P(a - X_{(n)} \geq \varepsilon) = 0.$由于 $X_i \sim U(0, a)$ ，其分布函数为：

    $$F(x) = P(X_i \leq x) = \begin{cases}  0, & x < 0, \\ \frac{x}{a}, & 0 \leq x \leq a, \\ 1, & x > a. \end{cases}$$

    对 $X_{(n)} = \max(X_1, X_2, \dots, X_n)$ ，有：$P(X_{(n)} \leq x) = P(X_1 \leq x, X_2 \leq x, \dots, X_n \leq x) = \left(P(X_i \leq x)\right)^n = F(x)^n.$

    因此：

    $$P(X_{(n)} \leq x) =  \begin{cases}  0, & x < 0, \\ \left(\frac{x}{a}\right)^n, & 0 \leq x \leq a, \\ 1, & x > a. \end{cases}$$

    由于$P(a - X_{(n)} \geq \varepsilon) = P(X_{(n)} \leq a - \varepsilon) = \left(\frac{a - \varepsilon}{a}\right)^n.$ 
    
    且当$n \rightarrow \infty$ 时 $\left(\frac{a - \varepsilon}{a}\right)^n \to 0.$ 
    
    得到 $X_{(n)} \xrightarrow{P} a.$

    2. $$\mathbb{E}[X_{(n)}] = \int_0^a x f_{X_{(n)}}(x) \, dx = \int_0^a x \cdot \frac{n}{a} \left(\frac{x}{a}\right)^{n-1} \, dx = \frac{1}{n+1}.$$

    同理， $\mathbb{E}[X_{(n)}^2] = a^2 \cdot \frac{n}{n+2}.$

    因此：$\operatorname{Var}(X_{(n)}) = a^2 \cdot \frac{n}{n+2} - \left(\frac{an}{n+1}\right)^2.$

    当 $n \to \infty$ 时：$\operatorname{Var}(X_{(n)}) \to 0$ ，因此：$P(|X_{(n)} - a| \geq \varepsilon) \to 0.$

    由切比雪夫不等式得：$X_{(n)} \xrightarrow{P} a$

!!! Info
    不能拿大数定律去做，这里不涉及均值，标准的做法是直接计算分布函数（需要根据分布放缩一步）或者切比雪夫不等式（计算均值和方差）

---