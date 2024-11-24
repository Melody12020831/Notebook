---
statistics: True
comments: true
---

# HW1(习题一)

## A4

???+ Question 
    设A,B,C为3个随机事件，请用事件的运算关系式表示：

    (1)A,B,C至少有2个发生；

    (2)A,B,C最多有1个发生；

    (3)A,B,C恰有1个不发生；

    (4)A,B,C至少有1个不发生。

??? Note "Answer"
    答案不唯一

    1. $AB \cup AC \cup BC$

    2. $\overline{AB \cup AC \cup BC}$

    3. $\overline{A}BC \cup A\overline{B}C \cup AB\overline{C}$

    4. $\overline{ABC}$

---

## A5

???+ question
    设A,B为两个随机事件，且A,B中至少有一个发生的概率为0.9.

    (1)若B发生的同时A不发生的概率为0.4,求P(A)；

    (2)若P(B)=0.6,求A发生的同时B不发生的概率.

??? Note "Answer"
    1. 

    $$\begin{cases}P(A\cup B) &= 0.9\\P(\overline{A}B) &= 0.4\end{cases} \Rightarrow \begin{cases}P(A) + P(B) - P(AB) = P(A) + P(\overline{A}B) &= 0.9 \\ P(\overline{A}B) &= 0.4 \end{cases} \Rightarrow P(A) = 0.5$$

    2. 

    $$\begin{cases}P(A\cup B) &= 0.9\\P(B) &= 0.6\end{cases} \Rightarrow \begin{cases}P(A) + P(B) - P(AB) = P(B) + P(A\overline{B}) &= 0.9 \\ P(B) &= 0.6 \end{cases} \Rightarrow P(A\overline{B}) = 0.3$$

---

## A12

???+ question "[⭐$(球盒问题)_{先咕咕咕有空就整理再做链接跳转}$]"
    一袋中有10个球，其中8个是红球.每次摸一球，共摸2次，在有放回抽样与无放回抽样两种抽样方式下分别求：

    (1)“两次均为红球”的概率；

    (2)“恰有1个红球”的概率；

    (3)“第2次是红球”的概率.

??? Note "Answer"
    有放回抽样：

    1. $(\frac{8}{10})^2 = \frac{16}{25}$

    2. $\frac{8}{10} \times \frac{2}{10} \times 2= \frac{8}{25}$ 

    3. $\frac{8}{10} = \frac{4}{5}$

    无放回抽样：

    1. $\frac{8}{10} \times \frac{7}{9} = \frac{28}{45}$
    
    2. $\frac{8}{10} \times \frac{2}{9} + \frac{2}{10} \times \frac{8}{9} = \frac{16}{45}$
    
    3. $\frac{8}{10} \times \frac{7}{9} + \frac{2}{10} \times \frac{8}{9} = \frac{4}{5} \rightarrow$ 无放回抽样中概率与第几次无关（抽奖）

---

## A15

???+ question
    编号为1,2,…,9的9辆车，随机地停入编号为1,2,…,9的9个车位中.当车号与车位编号一样时称该车配对，求：

    (1)1号车配对的概率；

    (2)1号车配对而9号车不配对的概率.

??? Note "Answer [(📝配对问题例题)](https://melody12020831.github.io/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/Chapter1/#a1)"
    1. $\frac{1}{9}$

    2. $\frac{1}{9} \times \frac{7}{8} = \frac{7}{72}$

---

## A16

???+ question
    依次将5个不同的球随机放入3个不同的盒子中，盒子容量不限，求3号盒子中恰好有两个球的概率.

??? Note "Answer"
    $\frac{C_5^2 \times 2^3}{3^5} = \frac{80}{243}$

---