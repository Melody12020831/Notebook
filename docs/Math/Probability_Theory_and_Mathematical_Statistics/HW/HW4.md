---
statistics: True
comments: true
---

# HW4(习题二)

## B16

???+ question
    设随机变量X具有以下性质：当 $0 \le x \le 1$ 时，$P\{0\le X \le x\}=\frac{x}{2}$;当$2\le x \le 3$ 时，$P\{2 \le X \le x\}=\frac{x-2}{2}$

    (1)写出X的分布函数；

    (2)求$P\{X≤2.5\}.$

??? Note "Answer"
    1. $\begin{cases}0,&x<0\\ \frac{x}{2},&0 \le x < 1\\ \frac{1}{2}.&1 \le x < 2 \\ \frac{x-1}{2}, &2 \le x < 3 \\ 1, & x \ge 3\end{cases}$

    2. $P\{X≤2.5\} = F(2.5) = \frac{3}{4}$

---

## B17

???+ question
    设随机变量 $X$ 的密度函数为

    $$f(x) = \begin{cases}c(4-x^2),&0 < x < 2\\ 0, &\text{其他} \end{cases}$$

    (1)求常数c;

    (2)求X的分布函数 $F(x)$ ;

    (3)求 $P\{-1<X<1\}$ ;

    (4)对 $X$独立观察5次，求事件$\{-1<X<1\}$ 恰好发生2次的概率.

??? Note "Answer"
    1. $\int_{0}^{2} f(x)dx = 1 \rightarrow c = \frac{3}{16}$

    2. $F(x) = \int f(x)dx = \begin{cases}0, &x<0 \\ -\frac{1}{16}x^3 + \frac{3}{4}, & 0 \le x <2 \\ 1, & x \ge 2 \end{cases}$

    3. $P\{ -1 < x < 1 \} = F(1) - F(-1) = \frac{11}{16}$

    4. $C_5^2 \cdot (\frac{11}{16})^2 \cdot (\frac{5}{16})^3 = \frac{75625}{524288}$

---

## B18

???+ question
    设随机变量 $X$ 的分布函数为

    $$F(x) = \begin{cases}0, &x<0 \\ ax^2, & 0 \le x < 1 \\ bx, & 1 \le x < 2 \\ 1, & x \ge 2 \end{cases}$$

    (1)求常数 $a$ , $b$;

    (2)求 $X$ 的密度函数 $f(x)$;

    (3)求 $P\{0.5 <X<1.5\}$;

??? Note "Answer"
    1. $\begin{cases} F(1^-) = F(1^+) \\ F(2) = 1\end{cases} \rightarrow \begin{cases} a=\frac{1}{2} \\ b = \frac{1}{2} \end{cases}$

    2. $f(x) = F'(x) = \begin{cases} x, & 0<x<1 \\ \frac{1}{2}, & 1< x<2 \\ 0,&\text{其他}\end{cases}$

    3. $P\{0.5 <X<1.5\} = F(1.5) = F(0.5) = \frac{5}{8}$

---

## B19

???+ question
    已知在早上7:00—8:00有两班车从A校区到B校区，出发时间分别是7:30和7:50,一学生在7:20—7:45随机到达车站乘这两班车.

    (1)求该学生等车时间小于10 min的概率；

    (2)求该学生等车时间大于5 min且小于15 min的概率；

    (3)已知该学生等车时间大于5 min的条件下，求他能赶上7:30这班车的概率.

??? Note "Answer"
    1. 7:20-7:30，7:40-7:45 $\rightarrow \frac{15}{25} = \frac{3}{5}$

    2. 7:20-7:25， 7:35-7:45 $\rightarrow \frac{15}{25} = \frac{3}{5}$

    3. 7:20-7:25， 7:30-7:45 $\rightarrow P_1 = \frac{20}{25} = \frac{4}{5}$，7:20-7:25 $\rightarrow P_2 = \frac{5}{25} = \frac{1}{5} \Rightarrow P = \frac{P_2}{P_1} = \frac{1}{4}$

---

## B29

???+ question
    设甲、乙两厂生产的同类型产品寿命(单位：年)分别服从参数为和言的指数分布，将两厂的产品混在一起，其中甲厂的产品数占40%.现从这批混合产品中随机取一件.

    (1)求该产品寿命大于6年的概率；

    (2)若已知取到的是甲厂产品，在已用了4个月没有坏的条件下，求其用到1年还不坏的概率；

    (3)在该产品已用了4个月没有坏的条件下，求其用到1年还不坏的概率.

??? Note "Answer"
    1. $x =6 \rightarrow P_{\text{甲}} = 1 - F_{\text{甲}} = e^{-2} \quad P_{\text{乙}} = 1 - F_{\text{乙}} = e^{-1} \rightarrow P = 0.4 \cdot e^{-2} + 0.6 \cdot e^{-1}$
  
    2. $P = \frac{P_{\text{一年}}}{P_{\text{四个月}}} = e^{-\frac{2}{9}}$

    3. $P = \frac{0.4 \cdot e^{-\frac{1}{3}} + 0.6 \cdot e^{-\frac{1}{6}}}{ 0.4 \cdot e^{-\frac{1}{9}} + 0.6 \cdot e^{-\frac{1}{18}}}$

---