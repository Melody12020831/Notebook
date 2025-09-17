---
statistics: True
comments: true
---

# Chapter 1

**Fundamental questions of Computer Science**

- What is an algorithm?
- What is computable?
- How can we characterize the difficulty of computation?

**The purpose of this course**

- Introduce a formal and rigorous definition of these concepts 给出形式化和严格的定义

The content of this course: Turing Machine

- Basic Concepts & Properties of the Turing Machine
- Foundations for Turing Machine invention

!!! info "Turing Machine (definition from Wiki)"
    A Turing machine is a mathematical model of computation describing an abstract machine that manipulates symbols on a strip of tape according to a table of rules. Despite the model's simplicity, it is capable of implementing any computer algorithm.

    [img](./assets/1-1.png)

    图灵机是一种计算的数学模型，它描述了一台抽象的机器，这台机器可以根据一套规则，在一条纸带上操作符号。尽管图灵机的模型非常简单，但它却能够实现任何计算机算法。

首先需要对实际问题进行描述（Problem Description），比如用数学语言表达问题。问题描述之后，需要对问题进行符号化（Problem Symbolization），也就是用数学符号、公式等形式将问题抽象出来，便于后续分析和处理。最后，通过形式化的模型（如图灵机）来分析问题，寻找反例（Find a counterexample），验证某个命题是否成立，或者证明某个问题是否可计算。

**algorithmic number theory**

problem $\rightarrow$ sets of symbols $ \rightarrow$ languages $ \leftrightarrow$ computational models

也就是说，实际问题可以转化为符号集合，再进一步转化为形式语言，而这些语言与计算模型（如图灵机）之间是等价的。

The equivalent relationship between computational model (solution) and language (problem)

计算模型（解）与语言（问题）之间存在等价关系，即每一个形式语言都对应一个计算模型，反之亦然。

## 离散知识的回顾

### Set

- A set is a collection of objects, an unordered collection of elements
- Objects in a set are called **elements** or **members** of the set.
- a $\in$ A if a is an element of A; a $\notin$ A, otherwise.

- A set is **empty** if it contains no element.
- A set is a **singleton(单元集)** if it contains only one element.
- A set is **finite** if it contains finite number of elements.
- A set is **infinite** if it contains infinite number of elements.

---

### Subsets

- A is a **subset** of B if each element of A is also an element of B.

$$A \subseteq B \leftrightarrow (x \in A \rightarrow x \in B)$$

We also say that B is a **superset** of A.

- A is a **proper subset** of B if $A \subseteq B$ and $A \neq B$.

$$ A \subset B$$

We also say that B is a **proper superset** of A.

- Two sets are Equal iff they contain the same elements

???+ example
    How to define equal if we do not have the concept of subsets?

??? note "answer"
    Two sets A and B are equal iff $A \subseteq B$ and $B \subseteq A$.

---

### Set Operations

- **Union**: $A \cup B = \{x : x \in A \lor x \in B\}$
- **Intersection**: $A \cap B = \{x : x \in A \land x \in B\}$
- **Complement**: $\overline{A} = \{x : x \notin A\}$
- **Difference**: $A - B = \{x : x \in A \land x \notin B\}$
- **Symmetric Difference**: $A \oplus B = (A - B) \cup (B - A)$
- **Power Set**: $2^A = \{S : S \subseteq A\}$

---

#### Set Identities

- Idempotent Laws

$$A \cup A = A, \quad A \cap A = A$$

- Commutative Laws

$$A \cup B = B \cup A, \quad A \cap B = B \cap A$$

- Associative Laws

$$(A \cup B) \cup C = A \cup (B \cup C), \quad (A \cap B) \cap C = A \cap (B \cap C)$$

- Distributive Laws

$$A \cup (B \cap C) = (A \cup B) \cap (A \cup C), \quad A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$$

- Absorption Laws

$$A \cup (A \cap B) = A, \quad A \cap (A \cup B) = A$$

- De Morgan's Laws

$$\overline{A \cup B} = \overline{A} \cap \overline{B}, \quad \overline{A \cap B} = \overline{A} \cup \overline{B}$$

$$A - (B \cup C) = (A - B) \cap (A - C), \quad A - (B \cap C) = (A - B) \cup (A - C)$$

???+ example
    Why some problems can be solved by employing computational models?

??? note "answer"
    Problem $\leftrightarrow$ Sets or language

    Automated solution $\leftrightarrow$ problem has identities $\leftrightarrow$ can be computed

---

### Partition

A partition of a non-empty set A is a subset $\Pi$ of $2^A$ such that

- $\emptyset \neq \Pi$
- $\forall S,T \in \Pi, S \cap T = \emptyset$ （任意两部分不相交）
- $\bigcup \Pi = A$ （所有部分的并集为 A）

---

### Sequences

- A sequence is a list of objects in some order.

$$(1,2) \neq (2,1)$$

- A finite sequence is also called a **tuple**. A sequence of k elements is called a **k-tuple**.
- A 2-tuple is also called an **ordered pair**.

$$(a,b) = (c,d) \leftrightarrow (a = c) \land (b = d)$$

---

### Cartesian Product

- The **Cartesian product** of two sets A and B is

$$A \times B = \{(a,b) : a \in A \land b \in B\}$$

- The **Cartesian production** of k sets $A_1, A_2, \ldots, A_k$ is

$$A_1 \times A_2 \times \ldots \times A_k = \{(a_1, a_2, \ldots, a_k) : a_i \in A_i\}$$

---

### Relations

- A binary relation R from A to B is a subset of $A \times B$.

$$R \subseteq A \times B$$

---

#### Operations of Relations

- Inverse

$$R \subseteq A \times B \Rightarrow R^{-1} \subseteq B \times A$$

- Composition

Let A, B, and C be sets

Let R be a relation from A to B and let S be a relation from B to C

$$(R \subseteq A \times B) \land (S \subseteq B \times C)$$

Then R and S give rise to a relation from A to C(composition) indicated by RoS

$$RoS = \{(a,c) : \exists b \in B, (a,b) \in R \land (b,c) \in S\}$$

---

#### Domain and Range

关系的域是所有输入值的集合，值域是所有输出值的集合。

- Domain of any relation is the set of input values of the relation
- Range of any relation is the set of output values of the relation

???+ example
    If we take two sets A and B, and define a relation $R = \{(a,b) | a \in A, b \in B\}$

??? note "answer"
    The set of values of A is called the domain of the function. 
    
    The set of values of B is called the range of the function.

---

### Functions

- A function $f : A \rightarrow B$ assigns each $a \in A$ a **unique** $f(a) \in B$.

$$f \subseteq A \times B$$

$$\forall a \in A, \exists \text{ exactly one } b \in B, (a,b) \in f$$

> f(a) is the **image** of a.
> A is called the **domain** of f.
> **Range** of f is the set of all images, denoted as f(A).

- Let $f : A \rightarrow B$ be a function.

- f is **one-to-one(injective)** if 

$$\forall a, b \in A, a \neq b \rightarrow f(a) \neq f(b)$$

单射（Injective）：不同的输入有不同的输出。

- f is **onto(surjective)** 

$$\forall b \in B, \exists a \in A, f(a) = b$$

满射（Surjective）：B 中每个元素都至少有一个 $a \in A$ 使 $f(a)=b$ 。

- f is **bijective(one-to-one correspondence)** if it is both one-to-one and onto.

既是单射又是满射。

???+ example
    Another type of "Not a Function"?

??? note "answer"
    A relation that assigns multiple outputs to a single input is not a function.

???+ example
    Can a function be neither Injective nor Surjective?

??? note "answer"
    Yes, a function can be neither injective nor surjective.

    设 A = {1,2,3}，B = {a,b,c,d}，定义 f : A → B 如下：

    - f(1) = a
    - f(2) = a
    - f(3) = b

    此时：

    - f(1) = f(2) = a，说明 f 不是单射（injective）。
    - c 和 d 都没有被任何 $a \in A$ 映射到，说明 f 不是满射（surjective）。

---

### Special Types of Binary Relations

#### Directed Graph

For any set A, a relation $R \subseteq A \times A$ can be represented by a directed graph.

> A node: represented by a small circle, represent each element of A
> An arrow: is the edge of the graph, drawn from a to b iff (a,b) $\in R$
> From a node to another, there is either no edge or one edge

![img](./assets/1-2.png)

---

#### Matrix

- If R is a binary relation between sets X and Y, so $R \subseteq X \times Y$
- R can be represented by the logical matrix M whose row and column indices index the elements of X and Y, respectively.
- The entries of M are defined by

$$M_{ij} = \begin{cases} 1 & \text{if } (x_i, y_j) \in R \\ 0 & \text{if } (x_i, y_j) \notin R \end{cases}$$

---

#### Properties of Relations ($R \subseteq X \times Y$)

(a) **reflexive(自反性)**: 

$$\forall a \in A, (a,a) \in R$$

- consider all $a \in A$

(b) **symmetric(对称性)**: 

$$(a,b) \in R \land a \neq b \rightarrow (b,a) \in R$$

- Reflexive is alternative
- Not necessarily consider all pairs 
- Represented by undirected graph

(c) **antisymmetric(反对称性)**:

$$(a,b) \in R \land a \neq b \rightarrow (b,a) \notin R$$

- Reflexive is alternative

(d) **transitive(传递性)**: 

$$(a,b) \in R \land (b,c) \in R \rightarrow (a,c) \in R$$

- Reflexive is alternative
- Not necessarily consider all pairs

???+ example
    Is there a relation belong neither or both of symmetric and antisymmetric?

??? note "answer"
    **情况一：既不是对称关系，又不是反对称关系**

    设集合 $A = \{1, 2, 3\}$，我们定义关系 $R = \{(1, 2), (2, 1), (2, 3)\}$

    1.  **不是对称关系？**，因为我们看到 $(2, 3) \in R$，但是它的反向序对 $(3, 2) \notin R$。这违反了对称关系的定义。

    2.  **不是反对称关系？**，因为我们看到 $(1, 2) \in R$ 并且 $(2, 1) \in R$，但是 $1 \neq 2$。这违反了反对称关系的定义。

    由于关系 $R$ 既不满足对称关系的要求，也不满足反对称关系的要求，因此它就是一个“既不属于对称也不属于反对称”的关系。

    **情况二：既是对称关系，又是反对称关系**

    一个关系要满足这个条件，它必须同时满足对称性和反对称性的定义。

    让我们来推导一下这意味着什么：

    1.  假设关系 $R$ 中有一个有序对 $(a, b)$，即 $(a, b) \in R$。
    2.  根据**对称性**的定义，如果 $(a, b) \in R$，那么 $(b, a)$ 也必须在 $R$ 中。
    3.  现在我们同时有了 $(a, b) \in R$ 和 $(b, a) \in R$。
    4.  根据**反对称性**的定义，如果 $(a, b) \in R$ 且 $(b, a) \in R$，那么必须有 $a = b$。

    **结论**：通过上述推导，我们发现，一个同时满足对称和反对称的关系，它包含的任何有序对 $(a, b)$ 都必须满足 $a = b$ 的条件。换句话说，这种关系只能包含形如 $(x, x)$ 的元素。

    在任意非空集合 $A$ 上，空关系 $R = \emptyset$（不包含任何有序对）也是一个特殊的例子。

    * **验证对称性**：定义是对所有 $(a, b) \in R$ 进行要求。因为 $R$ 中没有任何元素，所以这个条件的前提（`if` 部分）永远为假，因此整个逻辑蕴含式是“真值已满”(vacuously true)。所以它是对称的。
    * **验证反对称性**：同理，因为找不到任何 $(a, b) \in R$ 和 $(b, a) \in R$，所以反对称的定义也是“真值已满”。所以它也是反对称的。

    因此，**空关系**也是既对称又反对称的。

---

#### Equivalence Relation

- A binary relation R on $A \times A$ is an **equivalence relation** if it is reflexive, symmetric, and transitive.

若 R 同时具备自反性、对称性和传递性，则 R 是等价关系（equivalence relation）。

- A representation of an equivalent relation $R \subseteq A \times A$ as an undirected graph consists of several clusters, within clusters each pair is connected by a line

等价关系可以用无向图来表示：每个"团簇"（cluster）代表一个等价类，团簇内的任意两个元素之间都有连线。

---

#### Equivalence Classes

$$[a] = \{b | (a,b) \in R \}$$

- The set of nodes in a cluster is an equivalence class

在无向图表示中，每个团簇（cluster）中的所有节点就组成了一个等价类。

---

#### Partition

**Theorem:** Let R be an equivalence relation on a nonempty set A. Then the equivalence classes of R constitute a partition of A.

等价关系会把集合 A 划分为若干个互不重叠的子集（等价类），每个元素只属于一个等价类，所有等价类的并集就是 A 本身。这种划分方式就叫做集合的“分割”。

---

#### Partial Order

**Definition:** Given a set A, a partial ordering of A is a binary relation $\le$ satisfying the following axioms:

- Reflexive: for each $a \in A$ , we have $a \le a$
- Transitive: if $a \le b$ and $b \le c$ , then $a \le c$
- Antisymmetric: if $a \le b$ and $b \le a$ , then a = b

!!! tip "example"
    Let A be the set of real numbers. Define $a \le b$ if $b - a$ is a nonnegative. Then $\le$ is a partial ordering of A.

    实数集R上的≤关系（即 a≤b 当且仅当 b−a 为非负数）是一个偏序关系。

    Let S be a set, and let P(S) denote the collection of all subsets of S. For T, T' $\in$ P(S), write $T \le T'$ if $T \subseteq T'$. This relation makes P(S) into a partially ordered set.

    集合 S 的所有子集组成的集合 P(S)，用包含关系 ⊆ 作为偏序关系。

    Let Z be the set of positive integers. Then Z is partially ordered by divisibility: we can define $a \le b$ iff a|b

    正整数集 $Z^+$ ，用整除关系 a∣b 作为偏序关系。

##### 偏序集中的极小/极大元素

**Definition:** Given a partially ordered set A, we say that an element $a \in A$ is a least element of A if $a \le b$ for all $b \in A$. We say that a is a minimal element of A if $b \le a$ implies $a = b$.

**Definition:** Given a partially ordered set A, we say that an element $a \in A$ is a greatest element of A if $b \le a$ for all $b \in A$. We say that a is a maximal element of A if $a \le b$ implies $a = b$.


* **最小元素 (Least Element)** 如果存在一个元素 $a \\in A$，对于**所有**的 $b \\in A$，都有 $a \\le b$，则称 $a$ 是集合 $A$ 的最小元素。

* **极小元素 (Minimal Element)** 如果存在一个元素 $a \\in A$，**不存在**任何**不同于** $a$ 的元素 $b \\in A$ 使得 $b \\le a$，则称 $a$ 是集合 $A$ 的极小元素。

* **最大元素 (Greatest Element)** 如果存在一个元素 $a \\in A$，对于**所有**的 $b \\in A$，都有 $b \\le a$，则称 $a$ 是集合 $A$ 的最大元素。

* **极大元素 (Maximal Element)** 如果存在一个元素 $a \\in A$，**不存在**任何**不同于** $a$ 的元素 $b \\in A$ 使得 $a \\le b$，则称 $a$ 是集合 $A$ 的极大元素。

###### 核心区别解析

这四个概念的关键区别在于 **“全局性”** vs **“局部性”**，这通常取决于集合的序关系是 **全序 (Total Order)** 还是 **偏序 (Partial Order)**。

1.  **最大/最小元素 (全局最优)**

* **要求**：必须能与集合中 **所有** 其他元素进行比较，并且是 "最强" 的。
* **唯一性**：如果存在，最大元素和最小元素一定是 **唯一** 的。

2.  **极大/极小元素 (局部最优)**

* **要求**：只需要满足 **没有** 其他元素比它 "更强" 即可。它 **不一定** 需要和所有元素都能比较。
* **唯一性**：极大元素和极小元素可能 **不唯一**，可以存在多个。

??? example "举例说明"
    让我们用一个具体的例子来展示这些区别。

    **集合**： 设集合 $A = {2, 3, 4, 6, 8, 12}$。
    **序关系 `≤`**： 定义为 **"整除"** 关系，即 $a \\le b$ 当且仅当 $a$ 能整除 $b$ (记作 $a | b$)。

    这是一个偏序集，因为有些元素之间无法比较，例如 `3` 不能整除 `4`，`4` 也不能整除 `3`。

    我们可以画出这个集合的哈斯图（Hasse Diagram）来帮助理解：

    ```
        8      12
        |     / |
        4    /  6
        |   /  /
        2  /  /
        \/  /
        (3)  <-- 3 和 2 无法比较
    ```

    **分析这个集合 A：**

    1.  **极小元素 (Minimal Elements)**

    * 我们需要找到那些**不能被集合中任何其他元素整除**的数。
    * `2`：不能被 `3, 4, 6, 8, 12` 整除。所以 `2` 是一个极小元素。
    * `3`：不能被 `2, 4, 6, 8, 12` 整除。所以 `3` 也是一个极小元素。
    * **结论**：集合 $A$ 有两个极小元素：${2, 3}$。

    2.  **最小元素 (Least Element)**

    * 我们需要找到一个能**整除集合中所有元素**的数。
    * `2` 能整除 `4, 6, 8, 12`，但不能整除 `3`。
    * `3` 能整除 `6, 12`，但不能整除 `2, 4, 8`。
    * **结论**：集合 $A$ **没有**最小元素。

    3.  **极大元素 (Maximal Elements)**

    * 我们需要找到那些**不能整除集合中任何其他元素**的数。
    * `8`：不能整除 `12`。集合中没有别的数是 `8` 的倍数。所以 `8` 是一个极大元素。
    * `12`：不能整除 `8`。集合中没有别的数是 `12` 的倍数。所以 `12` 也是一个极大元素。
    * `4` 可以整除 `8` 和 `12`，所以它不是极大元素。
    * `6` 可以整除 `12`，所以它不是极大元素。
    * **结论**：集合 $A$ 有两个极大元素：${8, 12}$。

    4.  **最大元素 (Greatest Element)**

    * 我们需要找到一个能**被集合中所有元素整除**的数（即所有元素的公倍数）。
    * `8` 不能被 `3, 6, 12` 整除。
    * `12` 不能被 `8` 整除。
    * **结论**：集合 $A$ **没有**最大元素。

!!! tip "example"
    Given the collection S = { {d, o}, {d, o, g}, {g, o, a, d}, {o, a, f} } ordered by containment.

    Element {d,o} is minimal as it contains no sets
    
    Element {g,o,a,d} is minimal as there is no set containing it
    
    Element {d, o,g} is neither, while {o, a, f} is both

---