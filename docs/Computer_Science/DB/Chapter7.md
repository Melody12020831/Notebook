---
statistics: True
comments: true
---

# Chapter 7 | Relational Database Design

Suppose we combine instructor and department into inst_dept.

![img](./assets/7-1.png)

所有这些元组的预算数额统一这一点是重要的，否则我们的数据库将会不一致。在使用 `instructor` 和 `department` 的原始设计中，我们对每个预算的数额只存储一次。这说明使用 `inst_dept` 是一个坏主意，因为它重复存储预算数额，并且需要承担某些用户可能更新一个元组而不是所有元组中的预算数额并因此产生不一致性的风险。

即使我们决定容忍冗余的问题，`inst_dept` 模式仍然存在其他问题。假设我们在大学里创立一个新的系。在上面的备选设计方案中，我们无法直接表达关于一个系的信息(`dept_name,building,budget`)，除非该系在大学中至少有一位教师。这是因为 `inst_dept` 表中的元组需要 `ID`、`name` 和 `salary` 的值。这意味着我们不能记录新成立的系的相关信息，直到这个新系录用了第一位教师为止。在旧的设计中，`department` 模式可以处理这种情况，但是在修改后的设计中，我们将不得不创建一个 `building` 和 `budget` 为空值的元组。在某些情况下，空值会带来麻烦。

Pitfalls of the "bad" relations:

- Information repetition (信息重复)
- Insertion anomalies (插入异常)
- Update difficulty (更新困难)

---

## Decomposition

避免 `inst_dept` 模式中的信息重复问题的唯一方式是将其分解为两个模式(在本例中为 `instructor` 和 `department` 模式)。

并非所有的模式分解都是有益的。请考虑所有模式都由一个属性构成的极端情况。任何类型的有意义的联系都无法被表示。

Now consider a less extreme case where we choose to decompose the employee schema : employee (ID, name, street, city, salary), into the following two schemas: employee1 (ID, name)  employee2 (name, street, city, salary)

![img](./assets/7-2.png)

在企业可能拥有两个重名职员的情况下会暴露这个分解的缺陷。虽然我们拥有更多的元组，但是实际上从以下意义来讲我们却拥有更少的信息。我们能够指出一个特定的街道、城市和工资属于某个名为 Kim 的人，但是我们无法区分出是哪一个 Kim 。因此，我们的分解无法表达关于大学职员的特定的重要事实。我们想要避免这样的分解。我们将这样的分解称为**有损分解**(lossy decomposition)，而将那些没有信息丢失的称为**无损分解**(lossless decomposition)。

---

### Lossless Decomposition

令 R 为关系模式，并令 $R_1$ 和 $R_2$ 构成 R 的分解——也就是说，将R、 $R_1$ 和 $R_2$ 视为属性集， $R = R_1 \cup R_2$ 。如果用两个关系模式 $R_1$ 和 $R_2$ 去替代 R 时没有信息丢失，则我们称该分解是一个无损分解。

In SQL query:

```sql
select *
from (select R1 from r)
    natural join
    (select R2 from r)
```

In the relational algebra:

$$\Pi_{R_1}(r) \bowtie \Pi_{R_2}(r) = r$$

---

## Functional Dependencies

Let R be a relation schema $\alpha \subseteq R$ and $\beta \subseteq R$ . 

The functional dependency $\alpha \rightarrow \beta$ holds on R if and only if for any legal relations r(R), whenever any two tuples $t_1$ and $t_2$ of r agree on the attributes $\alpha$, they also agree on the attributes $\beta$. 

That is, $t_1[\alpha] = t_2[\alpha] \rightarrow t_1[\beta] = t_2[\beta]$

使用函数依赖这一概念，我们说如果函数依赖 $K \rightarrow R$ 在 r(R) 上成立，则 K 是 r(R) 的一个超码。换句话说，如果对于 r(R) 的每个合法实例，对于来自实例的每对元组 $t_1$ and $t_2$ ，只要 $t_1$ [K] = $t_2$ [K]，就总有 $t_1$ [R]= $t_2$ [R]成立(即 $t_1 = t_2$)，则 K 就是一个超码。

---

### Trivial Functional Dependencies

Some functional dependencies are said to be **trivial** because they are satisfied by all relations. In general, a functional dependency of the form $\alpha \rightarrow \beta$ is trivial if $\beta \subseteq \alpha$.

For example, $A \rightarrow A$ is satisfied by all relations involving attribute A. Reading the definition of functional dependency literally, we see that, for all tuples $t_1$ and $t_2$ such that $t_1$[A] = $t_2$[A], it is the case that $t_1$[A] = $t_2$[A]. Similarly, $AB \rightarrow A$ is satisfied by all relations involving attribute A.

We shall use the notation $F^+$ to denote the **closure** of the set F, that is, the set of all functional dependencies that can be inferred given the set F. $F^+$ contains all of the functional dependencies in F.

---

### Lossless Decomposition and Functional Dependencies

We can find $F^+$, the closure of F, by repeatedly applying Armstrong’s Axioms:

if $\beta \subseteq \alpha$ , then $\alpha \rightarrow \beta$ (reflexivity,自反率)

if $\alpha \rightarrow \beta$ , then $\gamma \alpha \rightarrow \gamma\beta$ (augmentation，增补率)

if $\alpha \rightarrow \beta$ and $\beta \rightarrow \gamma$ , then $\alpha \rightarrow \gamma$ (transitivity，传递率)

??? Example "Exercise"
    ![img](./assets/7-3.png)

**Additional rules**:

If $\alpha \rightarrow \beta$ holds and $\alpha \rightarrow \gamma$ holds, then $\alpha \rightarrow \beta \gamma$ holds (union，合并)

If $\alpha \rightarrow \beta \gamma$ holds, then $\alpha \rightarrow \beta$ holds and $\alpha \rightarrow \gamma$ holds (decomposition，分解)

If $\alpha \rightarrow \beta$ holds and $\gamma \beta \rightarrow \delta$ holds, then $\alpha \gamma \rightarrow \delta$ holds (pseudo transitivity，伪传递)

---

#### Algorithm to compute $\alpha^+$, the closure of $\alpha$ under F

result := $\alpha$;

while (changes to result) do

    for each $\beta \rightarrow \gamma$ in F do

        begin

            if $\beta \subseteq result$ then result := result $\cup \ \gamma$

        end

**Prove:**

![img](./assets/7-10.png)

??? Example "Exercise"
    ![img](./assets/7-4.png)

??? Example "Exercise"
    ![img](./assets/7-5.png)

---

## Canonical Cover（正则覆盖）

Sets of functional dependencies may have redundant dependencies that can be inferred from the others.

Parts of a functional dependency may be redundant:

{A $\rightarrow$ B, B $\rightarrow$ C, A $\rightarrow$ CD} can be simplified to  {A $\rightarrow$ B, B $\rightarrow$ C, A $\rightarrow$ D}

> .A $\rightarrow$ CD=> A $\rightarrow$ D
> .A $\rightarrow$ B,B $\rightarrow$ C => A $\rightarrow$ C , A $\rightarrow$ D => A $\rightarrow$ CD

Intuitively, a canonical cover of F is a "minimal" set of functional dependencies equivalent to F, having no redundant dependencies or redundant parts of dependencies.

---

## Extraneous Attributes(无关属性)

Consider a set F of functional dependencies and the functional  dependency $\alpha \rightarrow \beta$ in F. 

- Attribute A is extraneous in $\alpha$ if $A \in \alpha$ and F logically implies $(F - \{\alpha \rightarrow \beta \}) \cup \{ (\alpha - A) \rightarrow \beta \}$.
- Attribute A is extraneous in $\beta$ if $A \in \beta$ and the set of functional dependencies $(F - \{\alpha \rightarrow \beta \}) \cup \{ \alpha \rightarrow (\beta - A) \}$ logically implies F.

Note: implication in the opposite direction is trivial in each of the cases above, since a "stronger" functional dependency always implies a weaker one

???+ Example
    1. Given F = {A $\rightarrow$ C, AB $\rightarrow$ C }

    2. Given F = {A $\rightarrow$ C, AB $\rightarrow$ CD}

??? Example "answer"
    1. B is extraneous in AB $\rightarrow$ C because {A $\rightarrow$ C, AB $\rightarrow$ C} logically  implies A $\rightarrow$ C (I.e. the result of dropping B from AB $\rightarrow$ C).

    2. C is extraneous in AB $\rightarrow$ CD since AB $\rightarrow$ C can be inferred even after deleting C

???+ Question "Computing a Canonical Cover"
    R = (A, B, C)

    F = {A $\rightarrow$ BC  B $\rightarrow$ C  A $\rightarrow$ B  AB $\rightarrow$ C}

??? Example "answer"
    ![img](./assets/7-6.png)

    合理运用画图

    ![img](./assets/7-7.png)

???+ Example "Exercise"
    ![img](./assets/7-8.png)

??? Example "answer"
    ![img](./assets/7-9.png)

---

## Boyce-Codd Normal Form

A relation schema R is in BCNF with respect to a set F of functional dependencies if for all functional dependencies in $F^+$ of the form $\alpha \rightarrow \beta$, where $\alpha \subseteq R$ and $\beta \subseteq R$, at least one of the following holds:

1. $\alpha$ is a superkey for R
2. $\alpha \rightarrow \beta$ is trivial

Suppose we have a schema R and a non-trivial dependency $\alpha \rightarrow \beta$ causes a violation of BCNF.

We decompose R into: $(\alpha \cup \beta)$ and $R - (\beta - \alpha)$

---

### BCNF Decomposition Algorithm

result := {R };

done := false;

while (not done) do

    if (there is a schema $R_i$ in result that is not in BCNF)

    then begin

        let $\alpha \rightarrow \beta$ be a nontrivial functional dependency that holds on $R_i$ such that $\alpha^+$ does not contain $R_i$ and $\alpha \cap \beta = \emptyset$;

        result := (result – $R_i$) $\cap$ ($R_i – \beta$) $\cap$ ($\alpha$, $beta$);

    end

    else done := true;

---

???+ Example "Exercise"
    ![img](./assets/7-11.png)

??? Example "answer"
    ![img](./assets/7-12.png)

---

## Dependency Preservation

If it is sufficient to test only those dependencies on each individual relation of a decomposition in order to ensure that all functional dependencies hold, then that decomposition is dependency preserving.

如果通过检验单一关系上的函数依赖，就能确保所有的函数依赖成立，那么这样的分解是依赖保持的。或者，原来关系 R 上的每一个函数依赖，都可以在分解后的单一关系上得到检验或者推导得到。

Let $F_i$ be the set of all functional dependencies in $F^+$ that include only attributes in $R_i$. ($F_i$ : the restriction of F on $R_i$ )

- A decomposition is dependency preserving, if (F1 $\cup$ F2 $\cup$ … $\cup$ Fn )$^+$ = F$^+$
- If it is not, then checking updates for violation of functional  dependencies may require computing joins, which is expensive.

???+ Example "Exercise"
    R = (A, B, C )

    F = {A $\rightarrow$ B  B $\rightarrow$ C}

    Key = {A}

??? Example "answer"
    ![img](./assets/7-13.png)

???+ Example "Exercise"
    ![img](./assets/7-14.png)

??? Example "answer"
    ![img](./assets/7-15.png)
    ![img](./assets/7-16.png)

It is not always possible to get a BCNF decomposition that is  dependency preserving.

![img](./assets/7-17.png)

---

## Third Normal Form

There are some situations where BCNF is not dependency preserving, and efficient checking for FD violation on updates is important

Solution: define a weaker normal form, called Third Normal Form (3NF)

- Allows some redundancy
- But functional dependencies can be checked on individual relations without computing a join 
- There is always a lossless-join, dependency-preserving decomposition into 3NF.

A relation schema R is in third normal form (3NF) if for all: $\alpha \rightarrow \beta \in F^+$

at least one of the following holds:

1. $\alpha$ is a superkey for R
2. $\alpha \rightarrow \beta$ is trivial (i.e., $\beta \in \alpha$)
3. Each attribute A in $\beta - \alpha$ is contained in a candidate key for R. (NOTE: each attribute may be in a different candidate key)

也就是说，3NF的定义是：对于关系模式R中的每一个非平凡函数依赖X→Y，要么X是超键，要么Y是主属性（即Y属于某个候选键）。

- If a relation is in BCNF it is in 3NF (since in BCNF one of the first two conditions above must hold).
- Third condition is a minimal relaxation of BCNF to ensure dependency preservation.

???+ Question
    Relation dept_advisor:

    dept_advisor (s_ID, i_ID, dept_name)

    F = {s_ID, dept_name $\rightarrow$ i_ID, i_ID $\rightarrow$ dept_name}

    Two candidate keys: s_ID, dept_name, and i_ID, s_ID

??? answer
    R is in 3NF
    
    s_ID, dept_name $\rightarrow$ i_ID
    
    – s_ID, dept_name is a superkey
    
    i_ID $\rightarrow$ dept_name
    
    – dept_name is contained in a candidate key

---

### 3NF Decomposition Algorithm

![img](./assets/7-18.png)

---

## Goals of Normalization

Let R be a relation scheme with a set F of functional dependencies. Decide whether a relation scheme R is in "good" form.

In the case that a relation scheme R is not in "good" form, decompose it into a set of relation scheme {$R_1, R_2, ..., R_n$} such that

- each relation scheme is in good form (i.e., BCNF or 3NF)
- the decomposition is a lossless-join decomposition
- Preferably, the decomposition should be dependency preserving.

???+ Example "Exercise"
    ![img](./assets/7-19.png)

??? Example "answer"
    ![img](./assets/7-20.png)

---

## Multivalued Dependencies

有些关系模式虽然属于BCNF，但从某种意义上说仍然遭受信息重复问题的困扰，所以看起来并没有被充分地规范化。

Consider a relation inst_info ($\underline{ID, child\_name, phone}$) where an instructor may have more than one phone and can have multiple children.

![img](./assets/7-21.png)

There are no non-trivial functional dependencies and therefore the 
relation is in BCNF.

Insertion anomalies – i.e., if we add a phone 981-992-3443 to 99999, 
we need to add two tuples

(99999, David, 981-992-3443)

(99999, William, 981-992-3443)

Therefore, it is better to decompose inst_info into:

![img](./assets/7-22.png)

This suggests the need for higher normal forms, such as Fourth Normal Form (4NF).

---

### definition

Let R be a relation schema and let $\alpha \subseteq R$ and $\beta \subseteq R$. The multivalued dependency 

$$\alpha \rightarrow \rightarrow \beta$$ 

holds on R if in any legal relation r(R), for all pairs for tuples $t_1$ and $t_2$ in r such that $t_1[\alpha] = t_2[\alpha]$, there exists tuples $t_3$ and $t_4$ in r such that:

$$t_3[\alpha] = t_4[\alpha] = t_1[\alpha] = t_2[\alpha]$$

$$t_3[\beta] = t_1[\beta]$$

$$t_3[R - \beta] = t_2[R - \beta]$$

$$t_4[\beta] = t_2[\beta]$$

$$t_4[R - \beta] = t_1[R - \beta]$$

!!! note
    也就是在 $\alpha$ 相同的情况下，有一对 $\beta$ 相同，剩下一对是交换了的。

Tabular representation of $\alpha \rightarrow \rightarrow \beta$

![img](./assets/7-23.png)

---

### another version

Let R be a relation schema with a set of attributes that are partitioned into 3 nonempty subsets.

Y,Z,W

We say that $Y \rightarrow \rightarrow Z$ (Y multidetermines Z ) if and only if for all possible relations r(R)

< y1, z1, w1 > $\in$ r and < y1, z2, w2 > $\in$ r

then,

< y1, z1, w2 > $\in$ r and < y1, z2, w1 > $\in$ r

---

From the definition of multivalued dependency, we can derive the following rule:

If $\alpha \rightarrow \beta$ ,then $\alpha \rightarrow \rightarrow \beta$

That is, every functional dependency is also a multivalued dependency.

---

## Fourth Normal Form

A relation schema R is in 4NF with respect to a set D of functional and multivalued dependencies if for all multivalued dependencies in $D^+$ of the form $\alpha \rightarrow \rightarrow \beta$ , where $\alpha \subseteq R$ and $\beta \subseteq R$, at least one of the following hold:

1. $\alpha$ is a superkey for R
2. $\alpha \rightarrow \rightarrow \beta$ is a trivial (i.e., $\beta \subseteq \alpha$ or $\alpha \cup \beta$ = R)

If a relation is in 4NF it is in BCNF.

---

### 4NF Decomposition Algorithm

![img](./assets/7-24.png)

---

???+ Example "Exercise"
    ![img](./assets/7-25.png)

??? Example "answer"
    ![img](./assets/7-26.png)

---

## Overall Database Design Process

We have assumed schema R is given

- R could have been generated when converting E-R diagram to a set of tables.
- R could have been a single relation containing all attributes that are of interest (called universal relation).Normalization breaks R into smaller relations.
- R could have been the result of some ad hoc design of relations, which we then test/convert to normal form.

---

## ER Model and Normalization

- When an E-R diagram is carefully designed, identifying all entities correctly, the tables generated from the E-R diagram should not need further normalization.
- However, in a real (imperfect) design, there can be functional dependencies from non-key attributes of an entity to other attributes of the entity

---

## Denormalization for Performance

- May want to use non-normalized schema for performance
- For example, displaying *prereqs* along with *course_id* and *title* requires join of *course* with *prereq*

1. Alternative 1: Use denormalized relation containing attributes of course as well as prereq with all above attributes

- faster lookup
- extra space and extra execution time for updates
- extra coding work for programmer and possibility of error in extra code

2. Alternative 2: use a materialized view defined as $course \bowtie prereq$

- Benefits and drawbacks same as above, except no extra coding work 
for programmer and avoids possible errors

---

## Other Design Issues

- Some aspects of database design are not caught by normalization
- Examples : 3 approaches to represent the same information:
    1. earnings (company_id, year, amount )
    2. ernings_2012(company_id, earnings)
    
    earnings_2013(company_id, earnings)
    
    earnings_2014(company_id, earnings)

    - Above are in BCNF, but make querying across years difficult and needs new table each year
    - 可以提高并发度

    3. company_year (company_id, earnings_2012, earnings_2013, earnings_2014)

    - Also in BCNF, but also makes querying across years difficult and requires new attribute each year.
    - Is an example of a crosstab, where values for one attribute become column names
    - Used in spreadsheets, and in data analysis tools1

---