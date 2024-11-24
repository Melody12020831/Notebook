---
statistics: True
comments: true
---

# HW8(习题四)

## A4

???+ question
    设二维离散型随机变量 $(X,Y)$ 的联合分布律为

    | X\Y  |  0   |  1   |  2   |
    | :--: | :--: | :--: | :--: |
    |  1   | 0.2  | 0.1  | 0.3  |
    |  2   | 0.2  |  0   | 0.2  |

    求随机变量 $Z$ 的数学期望 $E(Z)$;

    (1) $Z = XY$

    (2) $Z = min\{X,Y\};$

    (3)$Z = max\{X,Y\};$

??? Note "Answer"
    1. $E(Z) = 1 \times 0.1 + 2 \times 0.3 + 4 \times 0.2 = 1.5$

    2. $E(Z) = 1 \times 0.4 + 2 \times 0.2 = 0.8$

    3. $E(Z) = 1 \times 0.3 + 2 \times 0.7 = 1.7$

---

## B6

???+ question
    设二维离散型随机变量 $(X,Y)$ 的联合密度函数为

    $$f(x,y) = \begin{cases}\frac{2}{x}e^{-2x}, &0<x<+\infty,0<y<x \\ 0, &\text{其他}\end{cases}$$

    (1)求 $E(X)$

    (2)求 $E(3X-1)$

    (3)求 $E(XY)$

??? Note "Answer"
    1. $E(X) = \int xf(x,y)dx = \frac{1}{2}$

    2. $E(3X-1) = 3E(X)-1 = \frac{1}{2}$

    3. $E(XY) = \int (xy)f(x,y)d(xy) = \frac{1}{4}$

---

## B11

???+ question
    某电子监视器的圆形屏幕半径为 $r(r>0)$ ,若目标出现的位置点 $A$ 服从均匀分布.以圆形屏幕的圆心为原点，设点A的平面直角坐标为 $(X,Y)$.

    (1)求 $E(X)$ 与 $E(Y)$;

    (2)求点A与屏幕中心位置(0,0)的平均距离

??? Note "[⭐$(微积分二积分的变换)_{先咕咕咕有空就整理再做链接跳转}$]"
    1. $E(X) = E(Y) = \int_{-r}^r dx \int_{-r}^r x\cdot \frac{1}{\pi r^2} dy = 0$

    2. $E(\sqrt{x^2+y^2}) = \mathop{\int \int}\limits_{x^2+y^2 \le r^2} \sqrt{x^2+y^2} \cdot \frac{1}{\pi r^2} dxdy \mathop{=}\limits^{\textbf{极坐标变换}} \int_0^{2 \pi}d\theta \int_0^r \frac{R^2}{\pi r^2}dR= \frac{2}{3}r$

---

## B14

???+ question
    有n张各不相同的卡片，采用有放回抽样，每次取一张，共取n次，则有些卡片会被取到，甚至被取到很多次，但有些卡片可能不曾被取到.设这n张卡片中被取到的共有X张，计算E(X),并计算当 $n \rightarrow +\infty$ 时，$E(\frac{X}{n})$ 的极限.

??? Note "Answer"
    这张卡被抽到过 $P = 1 - (1-\frac{1}{n})^n$

    $$E(X) = \sum\limits_{i=1}^nE(X_i) = n(1 - (1-\frac{1}{n})^n)$$

    $$\mathop{lim}\limits_{n\rightarrow +\infty} E(\frac{X}{n}) = \mathop{lim}\limits_{n\rightarrow +\infty}(1 - (1-\frac{1}{n})^n) = 1-e^{-1}$$

---

## B15

???+ question
    在区间(0,1)中随机地取n(n $\ge$ 2)个点，求相距最远的两个点的距离的数学期望

??? Note "Answer"
    当n较大时可视作每个点之间相距$\frac{1}{n+1}$，所以$E(X) = 1 - \frac{2}{n+1} = \frac{n-1}{n+1}$

---

## B20

???+ question
    设随机变量X服从拉普拉斯分布，密度函数为

    $$f(x) = \frac{1}{2} e^{-|x|},-\infty < x < +\infty$$

    计算 $X$ 与 $|X|$ 的方差

??? Note "Answer"
    $$E(X) = \int xf(x)dx = 0$$

    $$E(X^2) =  \int x^2f(x)dx \mathop{=}\limits^{\text{分部积分}} 2$$

    $$D(X) = E(X^2) - E^2(X) = 2$$

    $$E(|X|) = \int |x|f(x)dx = 1$$

    $$E(|X|^2) =  \int |x|^2f(x)dx \mathop{=}\limits^{\text{分部积分}} 2$$

    $$D(|X|) = E(|X|^2) - E^2(|X|) = 1$$

---