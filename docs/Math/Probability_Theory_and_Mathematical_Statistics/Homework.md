---
statistics: True
comments: true
---

# Homework

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Chapter1 </div>
<div class="file-meta"> 9,023 KB / 2024-11-24</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/HW.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

## HW1(习题一)

### A4

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

### A5

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

### A12

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

### A15

???+ question
    编号为1,2,…,9的9辆车，随机地停入编号为1,2,…,9的9个车位中.当车号与车位编号一样时称该车配对，求：

    (1)1号车配对的概率；

    (2)1号车配对而9号车不配对的概率.

??? Note "Answer [(📝配对问题例题)](https://melody12020831.github.io/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/Chapter1/#a1)"
    1. $\frac{1}{9}$

    2. $\frac{1}{9} \times \frac{7}{8} = \frac{7}{72}$

---

### A16

???+ question
    依次将5个不同的球随机放入3个不同的盒子中，盒子容量不限，求3号盒子中恰好有两个球的概率.

??? Note "Answer"
    $\frac{C_5^2 \times 2^3}{3^5} = \frac{80}{243}$

---

## HW2(习题一)

### A19

???+ question
    设A,B为两个随机事件，已知 $P(A)=0.7,P(\overline{B})=0.6,P(A\overline{B})=0.5$

    (1)$P(A|A \cup B);$

    (2)$P(A|\overline{A} \cup B);$

    (3)$P(AB|A \cup B);$

??? Note "Answer"
    1. $\frac{P(A)}{P(A) + P(B) - P(AB)} = \frac{P(A)}{P(A\overline{B}) + P(B)} = \frac{7}{9}$

    2. $\frac{P(AB)}{P(\overline{A}) + P(B) - P(\overline{A}B)} = \frac{P(A)-P(A\overline{B})}{P(\overline{A}) + P(AB)} = \frac{2}{5}$

    3. $\frac{P(AB)}{P(A) + P(B) - P(AB)} = \frac{2}{9}$

---

### A24

???+ question
    在某一时间点对某证券营业点进行统计.得知入市时间在1年以内的股民赢、平、亏的概率分别为10%,20%,70%;入市时间在1年及以上且不大于4年的股民赢、平、亏的概率分别为20%,30%,50%;入市时间大于4年的股民赢、平、亏的概率分别为50%,30%,20%.入市时间少于1年、1年及以上且不大于4年、大于4年的股民数分别占40%,40%,20%.现从该营业点随机找一股民，

    (1)求其有赢利的概率；

    (2)若已知其亏损了，求他为新股民(入市时间在1年以内)的概率.

??? Note "Answer"
    1. $10\% \times 40\% + 20\% \times 40\% + 50\% \times 20\% = \frac{11}{50}$

    2. $\frac{40\% \times 70\%}{40\% \times 70\% + 50\% \times 40\% + 20\% \times 20\%} = \frac{7}{13}$

---

### A33

???+ question
    已知一批照明灯管使用寿命大于1000h的概率为95%,大于2000h的概率为30%,大于4000h的概率为5%.

    (1)已知一个灯管用了1000 h没有坏，求其使用寿命大于4000 h的概率；

    (2)取10个灯管独立地装在一大厅内，过了2000 h,求至少有3个损坏的概率.


??? Note "Answer"
    1. $\frac{5\%}{95\%} = \frac{5}{95}$

    2. $1-0.3^{10}-0.7\cdot 0.3^9 \cdot C_{10}^1 - 0.7^2 \cdot 0.3^8 \cdot C_{10}^2 = 0.9984$

---

### B5

???+ question
    某产品12个一箱，成箱出售，某人购买时随机从中取2个检查，如果没有发现次品就买下.假设一箱中有0个、1个、2个次品的概率分别为0.8,0.15,0.05,求他买下的一箱中的确没有次品的概率.

??? Note "Answer"
    $\frac{0.8}{0.8+0.15 \cdot \frac{C_{11}^2}{C_{12}^2} + 0.05 \cdot \frac{C_{10}^2}{C_{12}^2}} = \frac{176}{211}$


---

### B6

???+ question
    有两组同类产品，第一组有30件，其中有10件为优质品；第二组有20件，其中有15件为优质品.今从两组中任选一组，然后从该组中任取2次(每次取1件，无放回抽样).

    (1)求第一次取到的是优质品的概率；

    (2)在已知第1次取到的是优质品的条件下，求第2次取到的不是优质品的概率.

??? Note "Answer"
    1. $0.5 \cdot \frac{10}{30} + 0.5 \cdot \frac{15}{20} = \frac{13}{24}$

    2. $\frac{0.5 \cdot \frac{10}{30} \cdot \frac{20}{29} + 0.5 \cdot \frac{15}{20} \cdot \frac{5}{19}}{\frac{13}{24}} = \frac{2825}{7163}$

---

### B10

???+ question
    飞机坠落在A,B,C三个区城中一个，营救部门判断其概率分别为0.7,0.2,0.1.用直升机搜索这些区域，若有残骸，残骸被发现的概率分别为0.3,0.4,0.5.若已用直升机搜索过A,B两个区域，均未发现残骸，求在这样的搜救现状下飞机坠落在C区域的概率.

??? Note "Answer"
    $\frac{0.1}{0.7 \cdot 0.7 + 0.2 \cdot 0.6 + 0.1} = \frac{10}{71}$

    **attention**:一个我自己会犯的错，全概率公式没写全哈。

---

## HW3(习题一、二)

### B8

???+ question
    设某地出现雾霾的概率为0.4,在雾霾天，该地居民独立地以0.2的概率戴口罩；在非雾霾天，该地居民独立地以0.01的概率戴口罩.

    (1)在该地随机选一位居民，求其戴口罩的概率；

    (2)若在该地同时选3位居民，求至少有一位居民戴口罩的概率.

??? Note "Answer [(📝例题)](https://melody12020831.github.io/Notebook/Math/Probability_Theory_and_Mathematical_Statistics/Chapter1/#a2)"
    1. $0.4 \cdot 0.2 + 0.6 \cdot 0.01 = 0.086$

    2. $0.4 \cdot (1 - 0.8^3) + 0.6 \cdot (1 - 0.99^3) = 0.2130206$

---

### B1

???+ question
    从1,2,3,4,5,6,7这7个数中随机抽取3个数(无放回抽样),并将其从小到大排列，设排在中间的数为X,求X的概率分布律.

??? Note "Answer"
    $$P\{X = i\} = \frac{C_{i-1}^{1} \cdot C_{7-i}^{1}}{C_7^3}=\frac{(i-1)(7-i)}{35},i = 2,3,4,5,6$$

---

### B6

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

### B8

???+ question
    从一批不合格率为 $p$ $(0<p<1)$的产品中随机抽查产品，如果查到不合格品就停止检查，且最多检查5件产品.设停止时已检查了$X$件产品，求：

    (1)X的概率分布律；

    (2)$P\{X \le 2.5\};$

??? Note "Answer"
    1. $P\{X = i\} = (1-p)^{i-1}p,i=1,2,3,4 \quad P\{X = 5\} = (1-p)^4$

    2. $P\{X \le 2.5\} = p + (1-p)p = (2-p)p$

---

### B12

???+ question
    设某手机在早上9:00至晚上9:00的任意长度为 $t$ (单位：min)的时间区间内收到的短信数 $X$ 服从参数为 $\lambda t$ 的泊松分布，$\lambda =\frac{1}{20}$,且与时间起点无关

    (1)求10:00到12:00期间恰好收到6条短信的概率；

    (2)已知在10:00到12:00期间至少收到5条短信，求在该时段恰好收到6条短信的概率.

??? Note "Answer"
    1. $P(X=6) = \frac{(\frac{120}{20})^{6} \cdot e^{-\frac{120}{20}}}{6!} = \frac{324 \cdot e^{-6}}{5}$

    2. $\frac{P(X=6)}{\sum\limits_{i=1}^{6}P(X = i)} = \frac{324}{5\cdot e^6 -575}$

---

### B15

???+ question
    小王租到一所房子，房东给了他5把钥匙，其中只有一把能打开大门.计算在以下两种方式下，他打开大门所需的试钥匙次数的概率分布律：

    (1)每次都从全部5把钥匙中任选一把试开；

    (2)每次试开失败后，将该把钥匙单独放置，从剩余的钥匙中任选一把试开.

??? Note "Answer"
    1. $P\{X=i\} = (\frac{4}{5})^{k-1}(\frac{1}{5}) = \frac{4^{k-1}}{5^k},k=1,2,\dots$

    2. $P\{X = k\} = \frac{1}{5},k=1,2,3,4,5$

---

## HW4(习题二)

### B16

???+ question
    设随机变量X具有以下性质：当 $0 \le x \le 1$ 时，$P\{0\le X \le x\}=\frac{x}{2}$;当$2\le x \le 3$ 时，$P\{2 \le X \le x\}=\frac{x-2}{2}$

    (1)写出X的分布函数；

    (2)求$P\{X≤2.5\}.$

??? Note "Answer"
    1. $\begin{cases}0,&x<0\\ \frac{x}{2},&0 \le x < 1\\ \frac{1}{2}.&1 \le x < 2 \\ \frac{x-1}{2}, &2 \le x < 3 \\ 1, & x \ge 3\end{cases}$

    2. $P\{X≤2.5\} = F(2.5) = \frac{3}{4}$

---

### B17

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

### B18

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

### B19

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

### B29

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

## HW5(习题二、三)

### B23



---

### B33



---

### B39



---

### A5



---

### A8



---

### A9



---

## HW6(习题三)

### A11


---

### A12



---

### A17



---

### A19



---

### A27



---

### B4



---

## HW7(习题三)

### A32



---

### A38



---

### B6



---

### B7



---

### B10



---

### B11



---

## HW8(习题四)

### A4

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

### B6

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

### B11

???+ question
    某电子监视器的圆形屏幕半径为 $r(r>0)$ ,若目标出现的位置点 $A$ 服从均匀分布.以圆形屏幕的圆心为原点，设点A的平面直角坐标为 $(X,Y)$.

    (1)求 $E(X)$ 与 $E(Y)$;

    (2)求点A与屏幕中心位置(0,0)的平均距离

??? Note "[⭐$(微积分二积分的变换)_{先咕咕咕有空就整理再做链接跳转}$]"
    1. $E(X) = E(Y) = \int_{-r}^r dx \int_{-r}^r x\cdot \frac{1}{\pi r^2} dy = 0$

    2. $E(\sqrt{x^2+y^2}) = \mathop{\int \int}\limits_{x^2+y^2 \le r^2} \sqrt{x^2+y^2} \cdot \frac{1}{\pi r^2} dxdy \mathop{=}\limits^{\textbf{极坐标变换}} \int_0^{2 \pi}d\theta \int_0^r \frac{R^2}{\pi r^2}dR= \frac{2}{3}r$

---

### B14

???+ question
    有n张各不相同的卡片，采用有放回抽样，每次取一张，共取n次，则有些卡片会被取到，甚至被取到很多次，但有些卡片可能不曾被取到.设这n张卡片中被取到的共有X张，计算E(X),并计算当 $n \rightarrow +\infty$ 时，$E(\frac{X}{n})$ 的极限.

??? Note "Answer"
    这张卡被抽到过 $P = 1 - (1-\frac{1}{n})^n$

    $$E(X) = \sum\limits_{i=1}^nE(X_i) = n(1 - (1-\frac{1}{n})^n)$$

    $$\mathop{lim}\limits_{n\rightarrow +\infty} E(\frac{X}{n}) = \mathop{lim}\limits_{n\rightarrow +\infty}(1 - (1-\frac{1}{n})^n) = 1-e^{-1}$$

---

### B15

???+ question
    在区间(0,1)中随机地取n(n $\ge$ 2)个点，求相距最远的两个点的距离的数学期望

??? Note "Answer"
    当n较大时可视作每个点之间相距$\frac{1}{n+1}$，所以$E(X) = 1 - \frac{2}{n+1} = \frac{n-1}{n+1}$

---

### B20

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

## HW9(习题四、五)

### B24

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

### B28

???+ question
    设随机变量 $X_1,X_2,\dots,X_n$ 均服从标准正态分布并且相互独立。记$S_k = \sum\limits_{i=1}^k X_i,T_k = \sum\limits_{j = n_0+1}^{n_0+k}X_j$，其中$1 \le n_0 < k < n_o+k \le n$，求 $S_k$ 与 $T_k$ 的相关系数

??? Note "Answer"
    $$\rho(S_k, T_k) = \frac{\operatorname{Cov}(S_k, T_k)}{\sqrt{\operatorname{Var}(S_k) \cdot \operatorname{Var}(T_k)}}$$

    方差：$\operatorname{Var}(X_i) = 1 \quad \text{且} \quad \operatorname{Cov}(X_i, X_j) = 0 \, (i \neq j)$

    于是：$\operatorname{Var}(S_k) = \operatorname{Var}\left(\sum_{i=1}^k X_i\right) = \sum_{i=1}^k \operatorname{Var}(X_i) = k$

    同理，$T_k = \sum_{j=n_0+1}^{n_0+k} X_j$ ，且随机变量仍然相互独立，因此：

    $$\operatorname{Var}(T_k) = \operatorname{Var}\left(\sum_{j=n_0+1}^{n_0+k} X_j\right) = \sum_{j=n_0+1}^{n_0+k} \operatorname{Var}(X_j) = k$$

    随机变量的协方差定义为：$\operatorname{Cov}(S_k, T_k) = \mathbb{E}[S_k T_k] - \mathbb{E}[S_k]\mathbb{E}[T_k]$

    由于$ X_i $ 是标准正态分布，因此 $\mathbb{E}[S_k] = \mathbb{E}[T_k] = 0$，从而：$\operatorname{Cov}(S_k, T_k) = \mathbb{E}[S_k T_k]$ 利用独立性和交叉项的性质，仅保留 $X_i$ 同时出现在两个求和中的项：

    $$\mathbb{E}[S_k T_k] = \sum_{i=1}^k \sum_{j=n_0+1}^{n_0+k} \mathbb{E}[X_i X_j] = \text{重叠项的数量}$$

    因此：$\operatorname{Cov}(S_k, T_k) = k - n_0 \Rightarrow \rho(S_k, T_k) = \frac{k - n_0}{k}$

---

### B29

???+ question
    设 $X ∼ N(0,1)$, Y的可能取值为 $\pm 1$，且$P\{Y=1\} = p \ (0<p<1)$.设 $X$ 与 $Y$ 相互独立，记 $\xi = X \cdot Y$

    (1)证明：$\xi ∼ N(0,1)$;

    (2)计算 $\rho_{X_{\xi}}$ ，并判断 $X$ 与 $\xi$ 的相关性和独立性.

??? Note "Answer"
    1. 当 $Y = 1$ 时，$ \xi = X$ ；当 $Y = -1$ 时，$ \xi = -X$ 。

    于是，混合分布：
    
    $$f_\xi(x) = P(Y=1) f_X(x) + P(Y=-1) f_X(-x) = p \cdot \frac{1}{\sqrt{2\pi}} e^{-x^2/2} + (1-p) \cdot \frac{1}{\sqrt{2\pi}} e^{-(-x)^2/2} = \frac{1}{\sqrt{2\pi}} e^{-x^2/2}.$$

    因此， $\xi \sim N(0,1).$

    2. 
    - $\operatorname{Var}(X) = \operatorname{Var}(\xi) = 1$ ，因为 $X \sim N(0,1)$ 且 $\xi \sim N(0,1)$ 。
    - 因此：$\rho_{X_\xi} = \operatorname{Cov}(X, \xi).$

    $$ \operatorname{Cov}(X, \xi) = \mathbb{E}[X \cdot \xi] - \mathbb{E}[X] \mathbb{E}[\xi] = \mathbb{E}[X \cdot \xi] = \mathbb{E}[X \cdot (X \cdot Y)] = \mathbb{E}[X^2 \cdot Y] = \mathbb{E}[X^2] \cdot \mathbb{E}[Y]$$

    由 $\mathbb{E}[X^2] = \operatorname{Var}(X) + (\mathbb{E}[X])^2 = 1$ ，而 $\mathbb{E}[Y] = p \cdot 1 + (1-p) \cdot (-1) = 2p - 1$。

    因此：$\operatorname{Cov}(X, \xi) = 1 \cdot (2p - 1) = 2p - 1 \rightarrow \rho_{X_\xi} = 2p - 1$

    当 $p=\frac{1}{2}$ 时， $X$与$\xi$不相关；当 $p > \frac{1}{2}$ 时， $X$与$\xi$正相关；当 $p < \frac{1}{2}$ 时， $X$与$\xi$负相关；

    $\xi$ 的分布依赖于 $X$，当 $0 < p <1$ 时， $X$与$\xi$不独立；

---

### B33



---

### B34

???+ question
    设有一煤矿一天的产煤量 $X$ (以 $10^4t$ 计)服从正态分布 $N(1.5,0.1^2)$ .设每天产量相互独立，一个月按30天计，求一个月总产量超 $46 \times 10^4t$ 的概率.

??? Note "Answer"
    30天则 $N(45,0.3) \rightarrow 1 - \Phi (\sqrt{\frac{10}{3}}) \approx 0.0339$

---

### B3

???+ question
    设随机变量 $X_i$ 的密度函数

    $$f_i(x) = \begin{cases}\frac{i|x|^{i-1}}{2},&|x| \le 1 \\ 0, & \text{其他}\end{cases}, i=1,2,\dots,n$$

    且 $X_1,X_2,\dots,X_n$ 相互独立。令 $Y_n = X_1X_2\dots X_n$，用切比雪夫不等式求使 $P\{|Y_n| \ge \frac{1}{2}\} \le \frac{1}{9}$ 成立的最小 $n$。

??? Note "Answer"
    $E(X_i) = 0 \quad E(X_i^2) = \frac{i}{i+2} \rightarrow Var(X_i) = \frac{i}{i+2} \rightarrow Var(Y_n) = \frac{2}{(n+1)(n+2)}$

     $$P\{|Y_n| \ge \frac{1}{2}\} \le 4Var(Y_n) \le \frac{1}{9} \Rightarrow n_{min} = 7$$

---

### B4

???+ question
    设随机变量序列 ${X_n，n\ge 1}$独立同分布，都服从U(0,a)，其中a>0，令$X_{(n)} = max_{1\le i \le n}X_i$，证明: $X_{(n)} \xrightarrow{P} a ,n \rightarrow \infty$

??? Note "Answer"
    1. 要证$\mathop{\lim}\limits_{n \to \infty} P(a - X_{(n)} \geq \varepsilon) = 0.$由于 $X_i \sim U(0, a)$ ，其分布函数为：

    $$F(x) = P(X_i \leq x) = \begin{cases}  0, & x < 0, \\ \frac{x}{a}, & 0 \leq x \leq a, \\ 1, & x > a. \end{cases}$$

    对 $X_{(n)} = \max(X_1, X_2, \dots, X_n)$ ，有：$P(X_{(n)} \leq x) = P(X_1 \leq x, X_2 \leq x, \dots, X_n \leq x) = \left(P(X_i \leq x)\right)^n = F(x)^n.$

    因此：

    $$P(X_{(n)} \leq x) =  \begin{cases}  0, & x < 0, \\ \left(\frac{x}{a}\right)^n, & 0 \leq x \leq a, \\ 1, & x > a. \end{cases}$$

    由于$P(a - X_{(n)} \geq \varepsilon) = P(X_{(n)} \leq a - \varepsilon) = \left(\frac{a - \varepsilon}{a}\right)^n.$ 且当$n \rightarrow \infty$$\left(\frac{a - \varepsilon}{a}\right)^n \to 0.$ 得到 $X_{(n)} \xrightarrow{P} a.$

    2. $$\mathbb{E}[X_{(n)}] = \int_0^a x f_{X_{(n)}}(x) \, dx = \int_0^a x \cdot \frac{n}{a} \left(\frac{x}{a}\right)^{n-1} \, dx. = \frac{1}{n+1}.$$

    同理， $\mathbb{E}[X_{(n)}^2] = a^2 \cdot \frac{n}{n+2}.$

    因此：$\operatorname{Var}(X_{(n)}) = a^2 \cdot \frac{n}{n+2} - \left(\frac{an}{n+1}\right)^2.$

    当 $n \to \infty$ 时：$\operatorname{Var}(X_{(n)}) \to 0$ ，因此：$P(|X_{(n)} - a| \geq \varepsilon) \to 0.$

    由切比雪夫不等式得：$X_{(n)} \xrightarrow{P} a$

---

## HW10(习题五、六)

### B6

???+ question
    设 $\{X_i,i \ge 1\}$ 为独立同分布的正态随机变量序列，若 $X_1 \sim N(\mu , \sigma^2)$ ，其中 $\sigma > 0$ 。问以下的随机变量序列当 $n \rightarrow +\infty$ 时依概率收敛吗？若收敛。请给出收敛的极限值，否则，请说明理由：

    (1) $\frac{1}{n}\sum\limits_{i=1}^nX_i^2$;

    (2) $\frac{1}{n}\sum\limits_{i=1}^n(X_i - \mu )^2$

    (3) $\frac{X_1 + X_2 + \dots + X_n}{X_1^2 + X_2^2 + \dots + X_n^2}$;

    (4) $\frac{X_1 + X_2 + \dots + X_n}{\sqrt{n\sum\limits_{i=1}^n(X_i - \mu)^2}}$;

??? Note "Answer"
    (1)$Var(X_i) = E(X_i^2) - E^2(X_i)$ 得到 $E(X_i^2) = \mu^2 + \sigma^2$

    $P(|\frac{1}{n} \sum\limits_{i=1}^n X_i^2 - E(X_i^2)| \ge \varepsilon ) \le \frac{Var(\frac{1}{n} \sum\limits_{i=1}^n X_i^2)}{\varepsilon^2} = \frac{1}{n\varepsilon^2}Var(X_i^2)$

    收敛于 $\mu^2 + \sigma^2$

    (2)同理，收敛于 $\sigma^2$

    (3)$\sum\limits_{i=1}^nX_i$ 收敛于 $n\mu$ 且 $\sum\limits_{i=1}^nX_i^2$ 收敛于 $n(\mu^2 + \sigma^2)$ 所以收敛于 $\frac{\mu}{\mu^2 + \sigma^2}$

    (4)同理，收敛于 $\frac{\mu}{\sigma}$

---

### B7



---

### B9(2)



---

### B11



---

### A1



---

### A3
