---
statistics: True
comments: true
---

# HW6(习题三)

## A11

???+ question
    设二维离散型随机变量 $(X,Y)$ 的联合分布律为

    | X\Y  |  0   |  1   |  2   |
    | :--: | :--: | :--: | :--: |
    |  0   | 0.1  | 0.1  |  0   |
    |  1   |  0   | 0.2  | 0.2  |
    |  2   | 0.2  |  0   | 0.2  |

    记 $F(x,y),F_X(x)$ 分别是 $(X,Y)$ 的联合分布函数和 $X$ 的边际分布函数.
    
    (1)求 $F(0,1),F(1,1,5),F(2.1,1.1)$;

    (2)求 $F_X(x)$

??? Note "Answer"
    1. 

    $F(0,1) = P(X=0,Y=1) + P(X=0,Y=1) = 0.1 + 0.1 = 0.2$

    $F(1,1.5) = P(X=0,Y=0) + P(X=0,Y=1) + P(X=0,Y=2) + P(X=1,Y=0)$
    
    $\quad \quad \quad \quad + P(X=1,Y=1) = 0.1 + 0.1 + 0 + 0 + 0.2 = 0.4$

    $F(2.1,1.1) = P(X=0,Y=0) + P(X=0,Y=1) + P(X=1,Y=0) + P(X=1,Y=1)$
    
    $\quad \quad \quad \quad + P(X=2,Y=0) + P(X=2,Y=1) = 0.1 + 0.1 + 0 + 0.2 + 0.2 + 0 = 0.6$

    2.

    $$F_X(x) = \begin{cases}0,&x<0 \\ 0.2,&0 \le x < 1 \\ 0.6,& 1 \le x < 2\\ 1,& 2 \le x\end{cases}$$

---

## A12

???+ question
    设二维离散型随机变量 $(X,Y)$ 的边际分布函数为

    $F_X(x) = \begin{cases}0,&x<1\\ 0.3,&1 \le x < 2\\ 1,& x\ge 2\end{cases},F_Y(y) = \begin{cases}0,&y<0 \\ 0.4,& 0 \le y <1 \\ 1,&y \ge 1\end{cases}$

    且已知 $P\{X=1,Y=0\}=0.1$

    (1)求 $(X,Y)$ 的联合分布律;

    (2)求给定 $\{Y = 0\}$ 的条件下 $X$ 的条件分布函数.

??? Note "Answer"
    1. 

    | X\Y  |  0   |  1   |
    | :--: | :--: | :--: |
    |  1   | 0.1  | 0.2  |
    |  2   | 0.3  | 0.4  |

    2.

    $$F_{X|Y}(X|0) = \begin{cases}0,&x<1 \\ \frac{1}{4},&1 \le x < 2\\ 1,& x \ge 2\end{cases}$$
---

## A17

???+ question
    二维随机变量 $(X,Y)$ 的联合密度函数为

    $$f(x,y) = \begin{cases}e^{-x},&0<y<x\\ 0,&其他\end{cases}$$

    (1)分别求 $X$ 和 $Y$ 的边际密度函数 $f_X(x)$ 和 $f_Y(y)$;

    (2)求条件密度函数 $f_{Y|X}(y|x)$.

    (3)给定 $\{X = x\}$ 的条件下， $Y$ 的条件分布是均匀分布吗？为什么？

??? Note "Answer"
    1.

    $$f_X(x) = \int_{-\infty}^{+\infty} f(x,y)dy = \begin{cases}xe^{-x},&x >0 \\ 0,&\text{其他}\end{cases}$$

    $$f_Y(y) = \int_{-\infty}^{+\infty} f(x,y)dx = \begin{cases}e^{-y},&y >0 \\ 0,&\text{其他}\end{cases}$$

    2. 当 $x > 0$ 时，

    $$f_{Y|X}(y|x) = \begin{cases}\frac{1}{x},&0<y<x\\ 0,&\text{其他}\end{cases}$$

    3. 当 $y >0$ 时， 
    
    $$f_{Y|X}(y|x) = \begin{cases}\frac{1}{x},&0<y<x \\ 0,& \text{其他}\end{cases}$$

    $$\therefore \text{为均匀分布}$$

---

## A19

???+ question
    设 $(X,Y)$ 为二位随机变量， $X$ 的密度函数为

    $$f_X(x) = \begin{cases}\lambda^2xe^{-\lambda x},&x>0\\0,&x\le 0\end{cases}$$

    其中 $\lambda >0$ ,当 $x>0$ 时， 给定 $\{X=x\}$ 的条件下 $Y$ 的条件密度函数为

    $$f_{Y|X}(y|x) = \begin{cases}\frac{1}{x}e^{-\frac{y}{x}},&y > 0 \\ 0,&y \le 0\end{cases}$$

    (1)求 $X$ 和 $Y$ 的联合密度函数;

    (2)求当 $x>0$ 时，给定 $\{X=x\}$ 的条件下 $Y$ 的条件分布函数;

    (3)求 $P\{Y>1|X=1\}$.

??? Note "Answer"
    1. 
    
    $$f(x,y) = \begin{cases} \lambda^2e^{-(\frac{y}{x}+\lambda x)},&x>0,y>0 \\ 0,&\text{其他}\end{cases}$$

    2. 

    $$f_{Y|X}(y|x) = \begin{cases} \frac{1}{x} e^{-\frac{y}{x}},& x>0,y>0 \\ 0,&\text{其他}\end{cases}$$

    $$F_{Y|X}(y|x) = \begin{cases} 1-e^{-\frac{y}{x}},& y >0 \\ 0,& y \le 0\end{cases}$$

    3. 
    
    $$P\{Y \le 1 | X = 1\} = 1-e^{-1}$$

    $$\therefore P\{Y > 1 | X = 1\} = e^{-1}$$

---

## A27

???+ question
    在半圆 $D = \{(x,y):x^2+y^2 \le 1,x>0\}$ 内随机投点 $A$ ，设 $A$ 点的坐标为 $(X,Y)$.
    
    (1)求 $X$ 的边际密度函数函数 $f_X(x)$ ;

    (2)求 $P\{X<\frac{1}{2}\}$;

    (3) $X$ 与 $Y$ 相互独立？为什么？

??? Note "Answer"
    1.
    
    $$S = \frac{1}{2} \pi$$

    $$f(x,y) = \begin{cases}\frac{2}{\pi},&0<x<1\\0,&\text{其他}\end{cases}$$

    $$f_X(x) = \begin{cases}\int_{-\sqrt{1-x^2}}^{\sqrt{1-x^2}}\frac{2}{\pi}dy = \frac{4\sqrt{1-x^2}}{\pi},& 0<x \le 1 \\ 0,& \text{其他}\end{cases}$$

    2. 
    
    $$P\{X < \frac{1}{2}\} = F_X(\frac{1}{2}) = \int_0^{\frac{1}{2}} \frac{4\sqrt{1-x^2}}{\pi}dx = \frac{1}{3} + \frac{\sqrt{3}}{2\pi}$$

    3. 
    
    $$f_Y(y) = \int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} \frac{2}{\pi}x dx = \frac{2}{\pi} \sqrt{1-y^2}, -1 \le y \le 1$$

    $$f_{X,Y}(x,y) \neq f_X(x) \cdot f_Y(y)$$

    $$\therefore \text{不独立}$$

---

## B4

???+ question
    设二维随机变量 $(X,Y)$ 的联合密度函数为

    $$f(x,y) = \begin{cases}c(y-x),&0<x<y<1\\ 0,&其他\end{cases}$$

    (1)求常数 $c$ ;

    (2)求 $P\{X+Y \le 1\}$ ;

    (3)求 $P\{X<0.5\}$ .

??? Note "Answer"
    1.
    
    $$\int_0^1dy\int_0^yc(y-1)dx = \frac{1}{6}c = 1$$

    $$\therefore c = 6$$

    2. 
    
    $$P\{X+Y \le 1\} = \int_0^{\frac{1}{2}}dx\int_x^{1-x}6(y-x)dy = \frac{1}{2}(2x-1)^3 |_0^{\frac{1}{2}} = \frac{1}{2}$$

    3. 

    $$P\{X<0.5\} = \int_0^{0.5}dx\int_x^{1}6(y-x)dy = (x-1)^3 |_0^{\frac{1}{2}} = \frac{7}{8}$$

---