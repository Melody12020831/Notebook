---
statistics: True
comments: true
---

# HW3(习题一、二)

## B8

???+ question
    设某地出现雾霾的概率为0.4,在雾霾天，该地居民独立地以0.2的概率戴口罩；在非雾霾天，该地居民独立地以0.01的概率戴口罩.

    (1)在该地随机选一位居民，求其戴口罩的概率；

    (2)若在该地同时选3位居民，求至少有一位居民戴口罩的概率.

??? Note "Answer [(📝例题)](https://melody12020831.github.io/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/Chapter1/#a2)"
    1. $0.4 \cdot 0.2 + 0.6 \cdot 0.01 = 0.086$

    2. $0.4 \cdot (1 - 0.8^3) + 0.6 \cdot (1 - 0.99^3) = 0.2130206$

---

## B1

???+ question
    从1,2,3,4,5,6,7这7个数中随机抽取3个数(无放回抽样),并将其从小到大排列，设排在中间的数为X,求X的概率分布律.

??? Note "Answer"
    $$P\{X = i\} = \frac{C_{i-1}^{1} \cdot C_{7-i}^{1}}{C_7^3}=\frac{(i-1)(7-i)}{35},i = 2,3,4,5,6$$

---

## B6

???+ question
    一系统由5个独立的同类元件组成，每个元件正常工作的概率为0.8,求：

    (1)恰有3个元件正常工作的概率；

    (2)至少有4个元件正常工作的概率；

    (3)至多有2个元件正常工作的概率；

??? Note "Answer"
    1. $0.8^3 \cdot 0.2^2 \cdot C_5^3 = 0.2048$

    2. $0.8^5 + 0.8^4 \cdot 0.2 \cdot C_5^1 = 0.73728$

    3. $0.2^5 + 0.2^4 \cdot 0.8 \cdot C_5^1 + 0.2^3 \cdot 0.8^2 \cdot C_5^3 = 0.05792$

---

## B8

???+ question
    从一批不合格率为 $p$ $(0<p<1)$的产品中随机抽查产品，如果查到不合格品就停止检查，且最多检查5件产品.设停止时已检查了$X$件产品，求：

    (1)X的概率分布律；

    (2)$P\{X \le 2.5\};$

??? Note "Answer"
    1. $P\{X = i\} = (1-p)^{i-1}p,i=1,2,3,4 \quad P\{X = 5\} = (1-p)^4$

    2. $P\{X \le 2.5\} = p + (1-p)p = (2-p)p$

---

## B12

???+ question
    设某手机在早上9:00至晚上9:00的任意长度为 $t$ (单位：min)的时间区间内收到的短信数 $X$ 服从参数为 $\lambda t$ 的泊松分布，$\lambda =\frac{1}{20}$,且与时间起点无关

    (1)求10:00到12:00期间恰好收到6条短信的概率；

    (2)已知在10:00到12:00期间至少收到5条短信，求在该时段恰好收到6条短信的概率.

??? Note "Answer"
    1. $P(X=6) = \frac{(\frac{120}{20})^{6} \cdot e^{-\frac{120}{20}}}{6!} = \frac{324 \cdot e^{-6}}{5}$

    2. $\frac{P(X=6)}{\sum\limits_{i=1}^{6}P(X = i)} = \frac{324}{5\cdot e^6 -575}$

---

## B15

???+ question
    小王租到一所房子，房东给了他5把钥匙，其中只有一把能打开大门.计算在以下两种方式下，他打开大门所需的试钥匙次数的概率分布律：

    (1)每次都从全部5把钥匙中任选一把试开；

    (2)每次试开失败后，将该把钥匙单独放置，从剩余的钥匙中任选一把试开.

??? Note "Answer"
    1. $P\{X=i\} = (\frac{4}{5})^{k-1}(\frac{1}{5}) = \frac{4^{k-1}}{5^k},k=1,2,\dots$

    2. $P\{X = k\} = \frac{1}{5},k=1,2,3,4,5$

---